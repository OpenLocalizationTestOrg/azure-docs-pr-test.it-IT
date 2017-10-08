---
title: software aaaConfigure RAID in una macchina virtuale che esegue Linux | Documenti Microsoft
description: Informazioni su come toouse mdadm tooconfigure RAID su Linux in Azure.
services: virtual-machines-linux
documentationcenter: na
author: rickstercdn
manager: timlt
editor: tysonn
tag: azure-service-management,azure-resource-manager
ms.assetid: f3cb2786-bda6-4d2c-9aaf-2db80f490feb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: rclaus
ms.openlocfilehash: f06e2679d953faf88ffee9991226cdb3cc1cbdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-software-raid-on-linux"></a>Configurare RAID software in Linux
Si tratta di un software di toouse uno scenario comune RAID nelle macchine virtuali Linux in Azure toopresent dati collegati più dischi come un singolo dispositivo RAID. In genere per possa essere utilizzati tooimprove prestazioni e migliorato velocità effettiva rispetto toousing solo un singolo disco.

## <a name="attaching-data-disks"></a>Collegamento di dischi dati
Due o più dischi dati vuoti sono necessari tooconfigure un dispositivo RAID.  Hello per la creazione di un dispositivo RAID viene principalmente tooimprove delle prestazioni dei / o del disco.  In base alle proprie esigenze dei / o, è possibile scegliere tooattach dischi che vengono archiviati nel nostro servizio di archiviazione Standard, con backup too500 IO/ps per ogni disco o l'archiviazione Premium con backup too5000 IO/ps per ogni disco. In questo articolo non descritte in dettaglio sul tooprovision e collegare la macchina virtuale dati dischi tooa Linux.  Vedere articolo di Microsoft Azure hello [collegare un disco](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) per istruzioni dettagliate su come tooattach dati vuoti di un disco di macchina virtuale di Linux tooa in Azure.

## <a name="install-hello-mdadm-utility"></a>Installare utilità mdadm hello
* **Ubuntu**
```bash
sudo apt-get update
sudo apt-get install mdadm
```

* **CentOS e Oracle Linux**
```bash
sudo yum install mdadm
```

* **SLES e openSUSE**
```bash  
zypper install mdadm
```

## <a name="create-hello-disk-partitions"></a>Creare partizioni del disco di hello
In questo esempio verrà creata una singola partizione del disco in /dev/sdc. partizione disco nuovo Hello verrà chiamato /dev/sdc1.

1. Avviare `fdisk` toobegin la creazione di partizioni

    ```bash
    sudo fdisk /dev/sdc
    Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
    Building a new DOS disklabel with disk identifier 0xa34cb70c.
    Changes will remain in memory only, until you decide toowrite them.
    After that, of course, hello previous content won't be recoverable.

    WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
                    switch off hello mode (command 'c') and change display units to
                    sectors (command 'u').
    ```

2. Premere ' n'in hello prompt toocreate un  **n** partizione uovo:

    ```bash
    Command (m for help): n
    ```

3. Successivamente, premere 'p' toocreate un **p**partizione primaria:

    ```bash 
    Command action
            e   extended
            p   primary partition (1-4)
    ```

4. Premere '1' numero di partizione tooselect 1:

    ```bash
    Partition number (1-4): 1
    ```

5. Selezionare hello punto iniziale della nuova partizione hello o premere `<enter>` partizione tooaccept hello predefinita tooplace hello all'inizio di hello di spazio libero hello hello unità:

    ```bash   
    First cylinder (1-1305, default 1):
    Using default value 1
    ```

6. Selezionare dimensione hello della partizione hello, ad esempio '+10G' di tipo toocreate una partizione di 10 GB. In alternativa, premere `<enter>` creare una singola partizione che si estende su intera unità hello:

    ```bash   
    Last cylinder, +cylinders or +size{K,M,G} (1-1305, default 1305): 
    Using default value 1305
    ```

7. Successivamente, cambiare ID hello e **t**ipo di partizione hello da predefinito hello ID tooID (Linux) '83' 'fd' (auto raid Linux):

    ```bash  
    Command (m for help): t
    Selected partition 1
    Hex code (type L toolist codes): fd
    ```

8. Infine, scrivere unità toohello tabella di partizione hello e uscire da fdisk:

    ```bash   
    Command (m for help): w
    hello partition table has been altered!
    ```

## <a name="create-hello-raid-array"></a>Creare una matrice RAID hello
1. Hello seguente verrà riportato "stripe" (livello RAID 0) e tre le partizioni si trovano su tre dischi dati separati (sdc1, sdd1, sde1).  Dopo l'esecuzione del comando verrà creato un nuovo dispositivo RAID denominato **/dev/md127** . Si noti inoltre che se questi dati dischi è già parte di un'altra matrice RAID inattiva potrebbe essere necessario tooadd hello `--force` parametro toohello `mdadm` comando:

    ```bash  
    sudo mdadm --create /dev/md127 --level 0 --raid-devices 3 \
        /dev/sdc1 /dev/sdd1 /dev/sde1
    ```

2. Creare hello file system sul dispositivo RAID nuovo hello
   
    a. **CentOS, Oracle Linux, SLES 12, openSUSE e Ubuntu**

    ```bash   
    sudo mkfs -t ext4 /dev/md127
    ```
   
    b. **SLES 11**

    ```bash
    sudo mkfs -t ext3 /dev/md127
    ```
   
    c. **SLES 11**: abilitare boot.md e creare mdadm.conf

    ```bash
    sudo -i chkconfig --add boot.md
    sudo echo 'DEVICE /dev/sd*[0-9]' >> /etc/mdadm.conf
    ```
   
   > [!NOTE]
   > Dopo aver apportato queste modifiche nei sistemi SUSE può essere necessario il riavvio. Questo passaggio *non* è obbligatorio su SLES 12.
   > 
   > 

## <a name="add-hello-new-file-system-tooetcfstab"></a>Aggiungere hello nuovo file system troppo/ecc/fstab
> [!IMPORTANT]
> Modifica in modo non corretto di file /etc/fstab. hello può provocare un avvio del sistema. In caso di dubbi, consultare la documentazione della distribuzione toohello per informazioni su come tooproperly modificare questo file. È inoltre consigliabile che viene creato un backup di file /etc/fstab. hello prima della modifica.

1. Creare il punto di montaggio hello desiderato per il nuovo file system, ad esempio:

    ```bash
    sudo mkdir /data
    ```
2. Quando si modifica /etc/fstab., hello **UUID** deve essere utilizzato tooreference hello file system anziché hello dispositivo il nome.  Hello utilizzare `blkid` hello toodetermine di utilità UUID per il nuovo file system di hello:

    ```bash   
    sudo /sbin/blkid
    ...........
    /dev/md127: UUID="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee" TYPE="ext4"
    ```

3. Aprire /etc/fstab. in un editor di testo e aggiungere una voce per hello nuovo file system, ad esempio:

    ```bash   
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults  0  2
    ```
   
    In alternativa, in **SLES 11**:

    ```bash
    /dev/disk/by-uuid/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext3  defaults  0  2
    ```
   
    Salvare e chiudere /etc/fstab.

4. Verificare che /etc/hosts hello/fstab voce sia corretto:

    ```bash  
    sudo mount -a
    ```

    Se questo comando genera un messaggio di errore, controllare la sintassi di hello in file /etc/fstab. hello.
   
    Prossima esecuzione hello `mount` comando tooensure hello file system è montato:

    ```bash   
    mount
    .................
    /dev/md127 on /data type ext4 (rw)
    ```

5. (Facoltativo) Parametri di avvio alternativo
   
    **Configurazione di fstab**
   
    Molte distribuzioni includono entrambi hello `nobootwait` o `nofail` montare i parametri che possono essere aggiunti file di fstab toohello/e così via. Questi parametri consentono di errori durante il montaggio di un determinato file system e consentono hello Linux sistema toocontinue tooboot anche se è Impossibile tooproperly montaggio hello RAID file sistema. Consultare la documentazione della distribuzione tooyour per ulteriori informazioni su questi parametri.
   
    Esempio (Ubuntu):

    ```bash  
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,nobootwait  0  2
    ```   

    **Parametri di avvio di Linux**
   
    In aggiunta toohello sopra i parametri, hello parametro kernel "`bootdegraded=true`" può consentire hello sistema tooboot anche se hello RAID viene considerato come danneggiato o è danneggiato, ad esempio, se un'unità dati inavvertitamente viene rimosso dalla macchina virtuale hello. Per impostazione predefinita, questa situazione può rendere impossibile l'avvio del sistema.
   
    Per consultare la documentazione di tooyour della distribuzione in modalità tooproperly modificare i parametri del kernel. Ad esempio, in molte distribuzioni (CentOS, Oracle Linux SLES 11) questi parametri possono essere aggiunti manualmente toohello "`/boot/grub/menu.lst`" file.  In Ubuntu questo parametro può essere aggiunto toohello `GRUB_CMDLINE_LINUX_DEFAULT` variabile su "/ e così via/predefinito/grub".


## <a name="trimunmap-support"></a>Supporto per TRIM/UNMAP
Alcuni kernel Linux supporto TRIM/UNMAP operazioni toodiscard i blocchi inutilizzati nel disco hello. Queste operazioni sono principalmente in tooinform standard di archiviazione Azure che pagine eliminate non sono più validi e possono essere ignorate. L'eliminazione delle pagine consente di risparmiare sui costi quando si creano file di grandi dimensioni per poi eliminarli.

> [!NOTE]
> RAID non può rilasciare i comandi di eliminazione se le dimensioni del blocco hello per matrice hello è impostato tooless rispetto al valore predefinito di hello (512KB). Infatti, annullare il mapping di hello granularità su hello Host è 512KB. Se è stato modificato dimensioni del blocco della matrice hello tramite del mdadm `--chunk=` parametro, quindi le richieste TRIM/Annulla possono essere ignorato dal kernel hello.

Esistono due modi tooenable TRIM supportano le VM Linux. Come al solito, consultare la distribuzione hello approccio consigliato:

- Hello utilizzare `discard` montare opzione `/etc/fstab`, ad esempio:

    ```bash
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,discard  0  2
    ```

- In alcuni hello casi `discard` opzione può avere implicazioni sulle prestazioni. In alternativa, è possibile eseguire hello `fstrim` comando manualmente dalla riga di comando hello o aggiungerlo tooyour crontab toorun regolarmente:

    **Ubuntu**

    ```bash
    # sudo apt-get install util-linux
    # sudo fstrim /data
    ```

    **RHEL/CentOS**
    ```bash
    # sudo yum install util-linux
    # sudo fstrim /data
    ```
