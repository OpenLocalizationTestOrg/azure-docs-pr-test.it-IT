---
title: aaaAttach tooa un disco VM Linux di Azure | Documenti Microsoft
description: "Informazioni su come tooattach dati disco tooa VM Linux utilizzando la distribuzione classica hello del modello e inizializzare il disco hello in modo che è pronto per l'utilizzo"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4901384d-2a6f-4f46-bba0-337a348b7f87
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: c76d8479ac2b522d2b6df658cd28f242473f30ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-virtual-machine"></a>Come tooAttach tooa un disco dati macchina virtuale Linux
> [!IMPORTANT] 
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. Vedere come troppo[collegare un disco dati con modello di distribuzione di gestione risorse di hello](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

È possibile collegare i dischi vuoti e i dischi che contengono dati tooyour macchine virtuali di Azure. In entrambi i casi i dischi sono file con estensione vhd che risiedono in un account di archiviazione di Azure. Come con l'aggiunta di computer Linux tooa disco, dopo aver collegato il disco di hello è necessario tooinitialize e formattarlo è quindi pronto per l'utilizzo. Questo articolo presenta il collegamento sia i dischi vuoti e i dischi che contiene già dati tooyour le macchine virtuali, nonché come toothen inizializzare e formattare un disco nuovo.

> [!NOTE]
> Si tratta di un migliore toouse pratica uno o più separare toostore dischi dati di una macchina virtuale. Al momento della creazione, una macchina virtuale di Azure dispone di un disco del sistema operativo e di un disco temporaneo. **Non utilizzare dati persistenti toostore di hello disco temporaneo.** Come suggerisce il nome di hello, fornisce esclusivamente all'archiviazione temporanea. Non offre funzionalità di ridondanza o backup perché non risiede nel servizio di archiviazione di Azure.
> in genere gestito da agente Linux di Azure hello e montato automaticamente troppo disco temporaneo Hello**/mnt/Retention/ risorse** (o **/mnt** sulle immagini Ubuntu). In hello invece, un disco dati potrebbe essere denominato dal kernel Linux hello simile `/dev/sdc`, ed è necessario toopartition, formattare e montare questa risorsa. Vedere hello [Guida dell'utente dell'agente Linux Azure] [ Agent] per informazioni dettagliate.
> 
> 

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-linux.md)]

## <a name="initialize-a-new-data-disk-in-linux"></a>Inizializzare un nuovo disco dati in Linux
1. SSH tooyour macchina virtuale. Per ulteriori informazioni, vedere [come toolog nella macchina virtuale tooa che eseguono Linux][Logon].
2. Successivamente sarà necessario identificatore del dispositivo hello toofind per hello dati disco tooinitialize. Esistono due modi toodo che:
   
    ) Grep per i dispositivi SCSI in hello accede, ad esempio hello comando seguente:
   
    ```bash
    sudo grep SCSI /var/log/messages
    ```
   
    Per le distribuzioni di Ubuntu recenti, potrebbe essere necessario toouse `sudo grep SCSI /var/log/syslog` perché troppo registrazione`/var/log/messages` potrebbero essere disabilitate per impostazione predefinita.
   
    È possibile trovare l'identificatore hello di hello ultimo disco dati in cui è stato aggiunto in messaggi hello che vengono visualizzati.
   
    ![Ottenere i messaggi hello del disco](./media/attach-disk/scsidisklog.png)
   
    OPPURE
   
    b) hello utilizzare `lsscsi` toofind comando out id dispositivo hello. `lsscsi` può essere installato mediante `yum install lsscsi` (in Red Hat in distribuzioni di base) o `apt-get install lsscsi` (in Debian in distribuzioni di base). È possibile trovare il disco hello desiderata dal relativo *lun* o **numero di unità logica**. Ad esempio, hello *lun* per dischi hello allegato possono essere facilmente visualizzati dal `azure vm disk list <virtual-machine>` come:

    ```azurecli
    azure vm disk list myVM
    ```

    output di Hello è simile toohello seguenti:

    ```azurecli
    info:    Executing command vm disk list
    + Fetching disk images
    + Getting virtual machines
    + Getting VM disks
    data:    Lun  Size(GB)  Blob-Name                         OS
    data:    ---  --------  --------------------------------  -----
    data:         30        myVM-2645b8030676c8f8.vhd  Linux
    data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
    info:    vm disk list command OK
    ```
   
    Confrontare questi dati con output di hello di `lsscsi` per hello stessa macchina virtuale di esempio:
   
    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```
   
    ultimo numero di Hello nella tupla hello in ogni riga è hello *lun*. Per altre informazioni, vedere `man lsscsi` .
3. Al prompt dei comandi hello, tipo hello comando che segue toocreate il dispositivo:
   
    ```bash
    sudo fdisk /dev/sdc
    ```

4. Quando richiesto, digitare  **n**  toocreate una partizione.

    ![Creare un dispositivo](./media/attach-disk/fdisknewpartition.png)

5. Quando richiesto, digitare **p** toomake hello hello primario partizione. Tipo **1** toomake hello prima partizione e quindi digitare Immettere valore predefinito di hello tooaccept per cilindro hello. In alcuni sistemi può Mostra i valori predefiniti di hello di hello prima e ultima settori, anziché cilindro hello hello. È possibile scegliere tooaccept queste impostazioni predefinite.

    ![Creare la partizione](./media/attach-disk/fdisknewpartdetails.png)


6. Tipo **p** dettagli hello toosee sul disco hello viene partizionato.

    ![Visualizzare le informazioni sul disco](./media/attach-disk/fdiskpartitiondetails.png)


7. Tipo **w** impostazioni hello toowrite per disco hello.

    ![Scrivere le modifiche ai dischi hello](./media/attach-disk/fdiskwritedisk.png)

8. È ora possibile creare hello file system nella nuova partizione hello. Aggiungere hello partizione numero ID dispositivo toohello (nell'esempio seguente hello `/dev/sdc1`). Hello esempio seguente viene creata una partizione ext4 su /dev/sdc1:
   
    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
   
    ![Creare il file system](./media/attach-disk/mkfsext4.png)
   
   > [!NOTE]
   > Che i sistemi SUSE Linux Enterprise 11 supportano solo l'accesso di sola lettura ai file system ext4. Per questi sistemi, è consigliabile tooformat hello nuovo file system come ext3 anziché ext4.

9. Rendere un directory toomount hello nuovo file system, come indicato di seguito:
   
    ```bash
    sudo mkdir /datadrive
    ```

10. È infine possibile montare unità hello, come indicato di seguito:
   
    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```
   
    disco dati Hello è ora pronto toouse come **/datadrive**.
   
    ![Crea disco di hello hello directory di montaggio](./media/attach-disk/mkdirandmount.png)

11. Aggiungere hello nuova unità troppo/ecc/fstab:
   
    unità di hello tooensure viene rimontato automaticamente dopo un riavvio del sistema che deve essere aggiunto file /etc/fstab. toohello. Inoltre, è consigliabile che hello UUID (Universally Unique IDentifier) viene usato in unità di toohello toorefer /etc/fstab. anziché semplicemente hello nome del dispositivo (ad esempio /dev/sdc1). Utilizzo di hello UUID evita disco non corretta di hello viene montato tooa percorso specificato, se hello del sistema operativo rileva un errore del disco durante l'avvio e di eventuali dischi dati rimanenti viene quindi assegnato a quelli ID dispositivo. toofind hello UUID della nuova unità hello, è possibile usare hello **ID blocco** utilità:
   
    ```bash
    sudo -i blkid
    ```
   
    output di Hello è simile toohello esempio seguente:
   
    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

    > [!NOTE]
    > Modifica in modo non corretto di hello **/e così via/fstab** file potrebbe causare un avvio del sistema. In caso di dubbi, consultare la documentazione della distribuzione toohello per informazioni su come tooproperly modificare questo file. È inoltre consigliabile che viene creato un backup di file /etc/fstab. hello prima della modifica.

    Aprire quindi hello **/e così via/fstab** file in un editor di testo:

    ```bash
    sudo vi /etc/fstab
    ```

    In questo esempio, si utilizza hello UUID valore per hello nuovo **dev/sdc1** dispositivo che è stato creato in precedenza hello e punto di montaggio hello **/datadrive**. Aggiungere hello successivo toohello riga alla fine di hello **/e così via/fstab** file:

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
    ```

    In alternativa, potrebbe essere necessario toouse un formato leggermente diverso in sistemi basati su SuSE Linux:

    ```sh
    /dev/disk/by-uuid/33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext3   defaults,nofail   1   2
    ```

    > [!NOTE]
    > Hello `nofail` opzione assicura che hello VM viene avviata anche se filesystem hello è danneggiato o hello disco non esiste in fase di avvio. Senza questa opzione, si verifichino comportamento come descritto in [Impossibile SSH tooLinux VM a causa di errori tooFSTAB](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).

    È ora possibile verificare che sia installato il sistema di file hello correttamente smontare e rimontare quindi sistema file hello, ad esempio mediante punto di montaggio di esempio hello `/datadrive` creato in hello precedenti passaggi:

    ```bash
    sudo umount /datadrive
    sudo mount /datadrive
    ```

    Se hello `mount` comando genera un errore, controllare hello e così via/fstab file per la sintassi corretta. Anche le eventuali altre unità o partizioni dati create devono essere inserite separatamente in /etc/fstab.

    Rendere modificabile unità hello tramite questo comando:

    ```bash
    sudo chmod go+w /datadrive
    ```

    > [!NOTE]
    > Rimozione di un disco dati successivamente senza dover modificare fstab potrebbe causare hello VM toofail tooboot. Se si tratta di un problema comune, la maggior parte delle distribuzioni forniscono entrambi hello `nofail` e/o `nobootwait` fstab opzioni che consentono un tooboot di sistema, anche se il disco di hello, toomount non riesce in fase di avvio. Per altre informazioni su questi parametri, consultare la documentazione della distribuzione.

### <a name="trimunmap-support-for-linux-in-azure"></a>Supporto delle funzioni TRIM/UNMAP per Linux in Azure
Alcuni kernel Linux supporto TRIM/UNMAP operazioni toodiscard i blocchi inutilizzati nel disco hello. Queste operazioni sono principalmente in tooinform standard di archiviazione Azure che pagine eliminate non sono più validi e possono essere ignorate. L'eliminazione delle pagine consente di risparmiare sui costi quando si creano file di grandi dimensioni per poi eliminarli.

Esistono due modi tooenable TRIM supportano le VM Linux. Come al solito, consultare la distribuzione hello approccio consigliato:

* Hello utilizzare `discard` montare opzione `/etc/fstab`, ad esempio:

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```

* In alcuni hello casi `discard` opzione può avere implicazioni sulle prestazioni. In alternativa, è possibile eseguire hello `fstrim` comando manualmente dalla riga di comando hello o aggiungerlo tooyour crontab toorun regolarmente:
  
    **Ubuntu**
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    **RHEL/CentOS**
  
    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a>Risoluzione dei problemi
[!INCLUDE [virtual-machines-linux-lunzero](../../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a>Passaggi successivi
È possibile leggere altre informazioni sull'utilizzo di VM Linux in hello seguenti articoli:

* [Come toolog nella macchina virtuale tooa che esegue Linux][Logon]
* [Come toodetach un disco da una macchina virtuale Linux](detach-disk.md)
* [Utilizzo di hello CLI di Azure con modello di distribuzione classica hello](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [Configurare RAID in una macchina virtuale Linux in Azure](../configure-raid.md)
* [Configurare LVM in una macchina virtuale Linux in Azure](../configure-lvm.md)

<!--Link references-->
[Agent]:../agent-user-guide.md
[Logon]:../mac-create-ssh-keys.md
