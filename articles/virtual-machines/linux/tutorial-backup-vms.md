---
title: Eseguire il backup di macchine virtuali Linux in Azure | Microsoft Docs
description: Proteggere le macchine virtuali Linux eseguendo il backup con Backup di Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 7c00392d5185a2f067f2ee2717529dcbde1e71f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-linux--virtual-machines-in-azure"></a>Eseguire il backup di macchine virtuali Linux in Azure

È possibile proteggere i dati eseguendo backup a intervalli regolari. Backup di Azure crea punti di recupero che vengono archiviati negli insiemi di credenziali di ripristino con ridondanza geografica. Quando si ripristina da un punto di ripristino, è possibile ripristinare hello intera macchina virtuale o a specifici file. Questo articolo spiega come toorestore un singolo file tooa nginx in esecuzione Linux VM. Se si dispone già di un toouse VM, è possibile crearne uno utilizzando hello [delle Guide rapide Linux](quick-create-cli.md). In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Creare un backup di una macchina virtuale
> * Pianificare un backup giornaliero
> * Ripristinare un file da un backup



## <a name="backup-overview"></a>Panoramica del servizio Backup

Quando hello servizio Backup di Azure avvia un backup, attiva hello estensione backup tootake uno snapshot del punto nel tempo. Hello servizio Azure Backup utilizza hello _VMSnapshotLinux_ estensione in Linux. estensione Hello viene installato durante il backup di VM prima hello se hello macchina virtuale è in esecuzione. Se hello VM non è in esecuzione, il servizio di Backup hello crea uno snapshot di hello archiviazione sottostante (poiché non scritte dall'applicazione si verificano durante hello che macchina virtuale è stato arrestato).

Per impostazione predefinita, Backup di Azure richiede un backup coerente del file system per VM Linux ma può essere configurato tootake [backup coerente dell'applicazione tramite pre- script di e post-framework](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent). Una volta hello servizio Azure Backup istantanea hello, dati hello sono toohello trasferite insieme di credenziali. l'efficienza toomaximize servizio hello identifica e i trasferimenti di dati che sono stati modificati dal backup precedente hello solo i blocchi hello.

Una volta completato il trasferimento dei dati di hello, snapshot hello viene rimosso e viene creato un punto di ripristino.


## <a name="create-a-backup"></a>Creare un backup
Creare un semplice pianificata giornaliera backup tooa insieme di credenziali di servizi di ripristino. 

1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Dal menu hello hello sinistra, selezionare **macchine virtuali**. 
3. Dall'elenco di hello, selezionare una macchina virtuale tooback backup.
4. Nel pannello VM hello in hello **impostazioni** fare clic su **Backup**. Hello **Abilita backup** apre blade.
5. In **insieme di credenziali di servizi di ripristino**, fare clic su **Crea nuovo** e specificare il nome di hello per nuovo insieme di credenziali hello. Viene creato un nuovo insieme di credenziali in hello stesso gruppo di risorse e il percorso come macchina virtuale hello.
6. Fare clic su **Criterio di Backup**. Per questo esempio, mantenere i valori predefiniti di hello e fare clic su **OK**.
7. In hello **Abilita backup** pannello, fare clic su **Abilita Backup**. Verrà creato un backup giornaliero in base alla pianificazione predefinita hello.
10. un punto di ripristino iniziale, su hello toocreate **Backup** fare clic su pannello **Backup ora**.
11. In hello **Esegui Backup** pannello, fare clic sull'icona calendario hello, utilizzare hello tooselect di controllo calendario hello ultimo giorno di tale punto di ripristino è stato mantenuto e fare clic su **Backup**.
12. In hello **Backup** pannello per la macchina virtuale, viene visualizzato un numero di punti di ripristino che sono state completate hello.

    ![Punti di ripristino](./media/tutorial-backup-vms/backup-complete.png)

il primo backup di Hello richiede circa 20 minuti. Al termine del backup, procedere toohello parte successiva di questa esercitazione.

## <a name="restore-a-file"></a>Ripristinare un file

Se accidentalmente si elimina o si apporta modifiche tooa file, è possibile utilizzare file di ripristino di File toorecover hello dall'insieme di credenziali di backup. Ripristino di file usa uno script eseguito nella macchina virtuale, hello toomount hello di punto di ripristino come unità locale. Queste unità rimarrà montate per 12 ore in modo che è possibile copiare i file dal punto di ripristino hello e ripristinarli toohello macchina virtuale.  

In questo esempio, ecco come toorecover hello predefinito nginx pagina web /var/www/html/index.nginx-debian.html. indirizzo IP pubblico Hello della macchina virtuale in questo esempio è *13.69.75.209*. È possibile trovare l'indirizzo IP hello di macchina virtuale utilizzando:

 ```bash 
 az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
 ```

 
1. Nel computer locale, aprire un browser e digitare in indirizzo IP pubblico hello della VM toosee hello predefinito nginx pagina web.

    ![Pagina Web di nginx predefinita](./media/tutorial-backup-vms/nginx-working.png)

1. Stabilire una connessione SSH alla VM.

    ```bash
    ssh 13.69.75.209
    ```
2. Eliminare /var/www/html/index.nginx-debian.html.

    ```bash
    sudo rm /var/www/html/index.nginx-debian.html
    ```
    
4. Nel computer locale, aggiornare il browser di hello premendo CTRL + F5 toosee che nginx pagina predefinita non viene più visualizzato.

    ![Pagina Web di nginx predefinita](./media/tutorial-backup-vms/nginx-broken.png)
    
1. Nel computer locale, accedi toohello [portale di Azure](https://portal.azure.com/).
6. Dal menu hello hello sinistra, selezionare **macchine virtuali**. 
7. Elenco hello selezionare hello macchina virtuale.
8. Nel pannello VM hello in hello **impostazioni** fare clic su **Backup**. Hello **Backup** apre blade. 
9. Nel menu di hello nella parte superiore di hello del pannello hello, selezionare **ripristino File**. Hello **ripristino File** apre blade.
10. In **passaggio 1: selezionare il punto di ripristino**, selezionare un punto di ripristino dall'elenco a discesa hello.
11. In **passaggio 2: scaricare script toobrowse e recuperare i file**, fare clic su hello **scaricare eseguibile** pulsante. Salvare computer locale tooyour di hello file scaricato.
7. Fare clic su **scaricare script** locale file di script hello toodownload.
8. Aprire un hello di prompt dei comandi e il tipo del Bash seguente, sostituendo *Linux_myVM_05-05-2017.sh* con hello correggere percorso e il nome di script hello scaricato, *azureuser* con il nome utente di hello per hello VM e *13.69.75.209* con indirizzo IP pubblico hello per la macchina virtuale.
    
    ```bash
    scp Linux_myVM_05-05-2017.sh azureuser@13.69.75.209:
    ```
    
9. Nel computer locale, aprire un toohello connessione SSH macchina virtuale.

    ```bash
    ssh 13.69.75.209
    ```
    
10. Aggiungere la macchina virtuale, eseguire il file di script toohello autorizzazioni.

    ```bash
    chmod +x Linux_myVM_05-05-2017.sh
    ```
    
11. Nella macchina virtuale, eseguire un punto di ripristino hello toomount hello script come un file System.

    ```bash
    ./Linux_myVM_05-05-2017.sh
    ```
    
12. Hello output di hello script offre che Hello percorso per il punto di montaggio hello. output di Hello è toothis simile:

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
                          
    Connecting toorecovery point using ISCSI service...
    
    Connection succeeded!
    
    Please wait while we attach volumes of hello recovery point toothis machine...
                         
    ************ Volumes of hello recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath 

    1)  | /dev/sdc  |  /dev/sdc1  |  /home/azureuser/myVM-20170505191055/Volume1

    ************ Open File Explorer toobrowse for files. ************

    After recovery, tooremove hello disks and close hello connection toohello recovery point, please click 'Unmount Disks' in step 3 of hello portal.

    Please enter 'q/Q' tooexit...
    ```

12. Nella macchina virtuale, copiare pagina web predefinita di hello nginx da toowhere indietro punto di montaggio hello eliminato file hello.

    ```bash
    sudo cp ~/myVM-20170505191055/Volume1/var/www/html/index.nginx-debian.html /var/www/html/
    ```
    
17. Nel computer locale, aprire scheda del browser hello in cui si è connessi toohello l'indirizzo IP del hello VM la visualizzazione hello nginx predefinito della pagina. Premere CTRL + F5 pagina nel browser toorefresh hello. Si noterà ora che hello funziona di nuovo la pagina predefinita.

    ![Pagina Web di nginx predefinita](./media/tutorial-backup-vms/nginx-working.png)

18. Nel computer locale, tornare indietro toohello per hello portale di Azure e nella scheda del browser **passaggio 3: smontare dischi hello dopo il ripristino** fare clic su hello **smontare dischi** pulsante. Se si dimentica toodo questo passaggio, punto di montaggio toohello hello connessione è chiusa automaticamente dopo 12 ore. Dopo queste 12 ore, è necessario toodownload un nuovo toocreate script un nuovo punto di montaggio.


## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione si è appreso come:

> [!div class="checklist"]
> * Creare un backup di una macchina virtuale
> * Pianificare un backup giornaliero
> * Ripristinare un file da un backup

Spostare toohello toolearn esercitazione successiva sul monitoraggio delle macchine virtuali.

> [!div class="nextstepaction"]
> [Monitorare le macchine virtuali](tutorial-monitoring.md)

