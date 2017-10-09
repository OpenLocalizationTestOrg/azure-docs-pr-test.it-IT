---
title: aaaConfigure LVM in una macchina virtuale che esegue Linux | Documenti Microsoft
description: Informazioni su come tooconfigure LVM su Linux in Azure.
services: virtual-machines-linux
documentationcenter: na
author: szarkos
manager: timlt
editor: tysonn
tag: azure-service-management,azure-resource-manager
ms.assetid: 7f533725-1484-479d-9472-6b3098d0aecc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 8daf792d87c6bb3d91a2eddcd01cfab34fd28cff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-lvm-on-a-linux-vm-in-azure"></a>Configurare LVM in una macchina virtuale Linux in Azure
Questo documento verrà illustrate le modalità tooconfigure Manager di Volume logico (LVM) nella macchina virtuale di Azure. Sebbene sia possibile tooconfigure che LVM in qualsiasi disco collegato toohello macchina virtuale, per impostazione predefinita cloud la maggior parte delle immagini non avrà LVM configurato su hello disco del sistema operativo. Si tratta di problemi tooprevent con gruppi di volumi duplicati se hello disco del sistema operativo è sempre collegata tooanother VM di hello stessa distribuzione e il tipo, ad esempio durante uno scenario di ripristino. Pertanto è consigliabile solo nei dischi dati hello toouse LVM.

## <a name="linear-vs-striped-logical-volumes"></a>Volumi lineari e volumi con striping logici
LVM può essere utilizzato toocombine un numero di dischi fisici in un singolo volume di archiviazione. Per impostazione predefinita LVM in genere creerà i volumi logici lineari, il che significa che l'archiviazione fisica hello è concatenato. In questo caso le operazioni di lettura/scrittura in genere solo riceverà tooa singolo disco. Al contrario, è possibile creare anche i volumi con striping logici in cui le letture e scritture sono dischi toomultiple distribuita contenuti nel gruppo di volumi hello (vale a dire tooRAID0 simile). Per motivi di prestazioni, che è probabile che si desidererà toostripe i volumi logici in modo che le letture e scritture utilizzano tutti i dischi dati collegati.

Questo documento descrive come toocombine dischi di dati diversi in un singolo gruppo di volumi e quindi creare un volume logico con striping. passaggi Hello riportati di seguito sono in qualche modo generalizzato toowork con la maggior parte delle distribuzioni. In hello casi la maggior parte delle utilità e flussi di lavoro per la gestione LVM in Azure non sono fondamentalmente diversi da quello di altri ambienti. Come sempre, consultare anche il fornitore Linux per la documentazione e le procedure consigliate per l'uso delle LVM con una distribuzione particolare.

## <a name="attaching-data-disks"></a>Collegamento di dischi dati
Quando si utilizza LVM uno in genere consigliabile toostart con due o più dischi dati vuoti. In base alle proprie esigenze dei / o, è possibile scegliere tooattach dischi che vengono archiviati nel nostro servizio di archiviazione Standard, con backup too500 IO/ps per ogni disco o l'archiviazione Premium con backup too5000 IO/ps per ogni disco. In questo articolo non entra in dettaglio sul tooprovision e collegare la macchina virtuale dati dischi tooa Linux. Vedere articolo di Microsoft Azure hello [collegare un disco](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) per istruzioni dettagliate su come tooattach dati vuoti di un disco di macchina virtuale di Linux tooa in Azure.

## <a name="install-hello-lvm-utilities"></a>Installare utilità LVM hello
* **Ubuntu**

    ```bash  
    sudo apt-get update
    sudo apt-get install lvm2
    ```

* **RHEL, CentOS e Oracle Linux**

    ```bash   
    sudo yum install lvm2
    ```

* **SLES 12 e openSUSE**

    ```bash   
    sudo zypper install lvm2
    ```

* **SLES 11**

    ```bash   
    sudo zypper install lvm2
    ```

    In SLES11 è inoltre necessario modificare `/etc/sysconfig/lvm` e impostare `LVM_ACTIVATED_ON_DISCOVERED` troppo "Abilita":

    ```sh   
    LVM_ACTIVATED_ON_DISCOVERED="enable" 
    ```

## <a name="configure-lvm"></a>Configurare la LVM
In questa guida si presuppone che è stato collegato a tre dischi dati, che si farà riferimento tooas `/dev/sdc`, `/dev/sdd` e `/dev/sde`. Si noti che questi potrebbe non essere sempre hello stessi nomi di percorso nella macchina virtuale. È possibile eseguire '`sudo fdisk -l`' simile toolist di comando o i dischi disponibili.

1. Preparare volumi fisici hello:

    ```bash    
    sudo pvcreate /dev/sd[cde]
    Physical volume "/dev/sdc" successfully created
    Physical volume "/dev/sdd" successfully created
    Physical volume "/dev/sde" successfully created
    ```

2. Creare un gruppo di volumi. In questo esempio stiamo chiamando il gruppo di volumi hello `data-vg01`:

    ```bash    
    sudo vgcreate data-vg01 /dev/sd[cde]
    Volume group "data-vg01" successfully created
    ```

3. Creare volumi logici hello. Hello comando seguente si creerà un singolo volume logico chiamato `data-lv01` intero volume di toospan hello gruppo, ma si noti che è anche possibile toocreate più volumi logici nel gruppo di volumi hello.

    ```bash   
    sudo lvcreate --extents 100%FREE --stripes 3 --name data-lv01 data-vg01
    Logical volume "data-lv01" created.
    ```

4. Volume logico hello di formato

    ```bash  
    sudo mkfs -t ext4 /dev/data-vg01/data-lv01
    ```
   
   > [!NOTE]
   > Con l'uso di SLES11 `-t ext3` al posto di ext4. SLES11 supporta solo i file System tooext4 di accesso in sola lettura.

## <a name="add-hello-new-file-system-tooetcfstab"></a>Aggiungere hello nuovo file system troppo/ecc/fstab
> [!IMPORTANT]
> Modifica in modo non corretto di hello `/etc/fstab` file potrebbe causare un avvio del sistema. In caso di dubbi, consultare la documentazione della distribuzione toohello per informazioni su come tooproperly modificare questo file. È inoltre consigliabile che un backup di hello `/etc/fstab` file viene creato prima della modifica.

1. Creare il punto di montaggio hello desiderato per il nuovo file system, ad esempio:

    ```bash  
    sudo mkdir /data
    ```

2. Individuare il percorso di volume logico hello

    ```bash    
    lvdisplay
    --- Logical volume ---
    LV Path                /dev/data-vg01/data-lv01
    ....
    ```

3. Aprire `/etc/fstab` in un editor di testo e aggiungere una voce per hello nuovo file system, ad esempio:

    ```bash    
    /dev/data-vg01/data-lv01  /data  ext4  defaults  0  2
    ```   
    Salvare e chiudere `/etc/fstab`.

4. Verificare che hello `/etc/fstab` voce sia corretta:

    ```bash    
    sudo mount -a
    ```

    Se questo comando genera un messaggio di errore, controllare la sintassi di hello in hello `/etc/fstab` file.
   
    Prossima esecuzione hello `mount` comando tooensure hello file system è montato:

    ```bash    
    mount
    ......
    /dev/mapper/data--vg01-data--lv01 on /data type ext4 (rw)
    ```

5. (Facoltativo) Parametri di avvio alternativo in `/etc/fstab`
   
    Molte distribuzioni includono entrambi hello `nobootwait` o `nofail` montare i parametri che possono essere aggiunti toohello `/etc/fstab` file. Questi parametri consentono di errori durante il montaggio di un determinato file system e consentono hello Linux sistema toocontinue tooboot anche se è Impossibile tooproperly montaggio hello RAID file sistema. Per ulteriori informazioni su questi parametri, consultare la documentazione di tooyour della distribuzione.
   
    Esempio (Ubuntu):

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,nobootwait  0  2
    ```

## <a name="trimunmap-support"></a>Supporto per TRIM/UNMAP
Alcuni kernel Linux supporto TRIM/UNMAP operazioni toodiscard i blocchi inutilizzati nel disco hello. Queste operazioni sono principalmente in tooinform standard di archiviazione Azure che pagine eliminate non sono più validi e possono essere ignorate. L'eliminazione delle pagine consente di risparmiare sui costi quando si creano file di grandi dimensioni per poi eliminarli.

Esistono due modi tooenable TRIM supportano le VM Linux. Come al solito, consultare la distribuzione hello approccio consigliato:

- Hello utilizzare `discard` montare opzione `/etc/fstab`, ad esempio:

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,discard  0  2
    ```

- In alcuni hello casi `discard` opzione può avere implicazioni sulle prestazioni. In alternativa, è possibile eseguire hello `fstrim` comando manualmente dalla riga di comando hello o aggiungerlo tooyour crontab toorun regolarmente:

    **Ubuntu**

    ```bash 
    # sudo apt-get install util-linux
    # sudo fstrim /datadrive
    ```

    **RHEL/CentOS**

    ```bash 
    # sudo yum install util-linux
    # sudo fstrim /datadrive
    ```
