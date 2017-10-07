---
title: 'Backup di Azure: Ripristino dello stato del sistema tooa Windows Server | Documenti Microsoft'
description: Procedura dettagliata per il ripristino dello stato del sistema di Windows Server da un backup in Azure.
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/18/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: a45506507f53e2744350d3b6b2e52f1db415de4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="restore-system-state-toowindows-server"></a>Ripristino dello stato del sistema tooWindows Server

Questo articolo illustra come insieme di credenziali di backup dello stato del sistema di Windows Server toorestore da un ripristino di servizi di Azure. toorestore dello stato del sistema, è necessario eseguire il backup dello stato del sistema (create utilizzando le istruzioni di hello in [eseguire il backup dello stato del sistema](backup-azure-system-state.md#back-up-windows-server-system-state-preview)) e assicurarsi di aver installato hello [versione più recente di Microsoft Azure Recovery hello L'agente di servizi (MARS)](http://aka.ms/azurebackup_agent). Il ripristino dei dati dello stato del sistema di Windows Server da un insieme di credenziali di Servizi di ripristino di Azure è un processo in due passaggi:

1. Ripristinare lo stato del sistema sotto forma di file da Backup di Azure. Quando si ripristina lo stato del sistema sotto forma di file da Backup di Azure, è possibile eseguire una di queste operazioni:
  * Ripristino dello stato del sistema toohello nello stesso server in cui sono stati eseguiti backup hello, o
  * Server alternativo tooan file ripristino dello stato del sistema.

2. Applicare tooa di file hello ripristinato lo stato del sistema Windows Server.


## <a name="recover-system-state-files-toohello-same-server"></a>Ripristinare lo stato del sistema file toohello nello stesso server
Hello alla procedura seguente viene illustrato come tooroll eseguire il backup di stato precedente tooa configurazione del Server di Windows. Tooa indietro di configurazione noto, lo stato stabile, il server in sequenza può essere molto utile. Hello successivo dello stato del sistema del server di passaggi restore hello da un insieme di credenziali di servizi di ripristino. 

1. Aprire hello **Backup di Microsoft Azure** snap-in. Se non si conosce in hello snap-in è stato installato, eseguire la ricerca computer hello o un server per **Microsoft Azure Backup**.

    app desktop Hello dovrebbe essere visualizzato nei risultati della ricerca hello.

2. Fare clic su **Ripristina dati** guidata hello toostart.

    ![Ripristina dati](./media/backup-azure-restore-windows-server/recover.png)

3. In hello **Introduzione** riquadro, toorestore hello dati toohello stesso server o computer, selezionare **server (`<server name>`)** e fare clic su **Avanti**.

    ![Scegliere questo toohello di dati server opzione toorestore hello nello stesso computer](./media/backup-azure-restore-system-state/samemachine.png)

4. In hello **selezionare la modalità di ripristino** riquadro scegliere **dello stato del sistema** e quindi fare clic su **Avanti**.

    ![Ricerca dei file](./media/backup-azure-restore-system-state/recover-type-selection.png)

5. Nel calendario hello in **seleziona Volume e data** punto riquadro, selezionare un ripristino. 

    È possibile ripristinare da qualsiasi punto di ripristino. Le date in **grassetto** indicare hello la disponibilità di almeno un punto di ripristino. Dopo aver selezionato una data, se sono disponibili più punti di ripristino, scegliere il punto di ripristino specifico di hello da hello **ora** dal menu a discesa.

    ![Volume e dati](./media/backup-azure-restore-system-state/select-date.png)

6. Dopo aver scelto toorestore punto di ripristino hello, fare clic su **Avanti**.

    Backup di Azure monta il punto di ripristino locali hello che viene utilizzato come un volume di ripristino.

7. Nel riquadro successivo di hello, specificare una destinazione hello per hello ripristinati i file di stato del sistema e fare clic su **Sfoglia** tooopen in Esplora risorse e individuare i file hello e le cartelle desiderate. opzione Hello **crea copie in modo da mantenere entrambe le versioni**, crea le copie dei singoli file in un archivio di file di stato del sistema esistente anziché creare una copia di hello dell'intero archivio dello stato del sistema di hello.

    ![Opzioni di ripristino](./media/backup-azure-restore-system-state/recover-as-files.png)

8. Verificare i dettagli di hello di ripristino su hello **conferma** riquadro e fare clic su **ripristinare**.

   ![Fare clic su Ripristina tooacknowledge hello Ripristina azione](./media/backup-azure-restore-system-state/confirm-recovery.png)

9. Hello copia *WindowsImageBackup* directory hello volume non critici tooa destinazione di ripristino del server di hello. In genere, il volume del sistema operativo Windows hello è volume critico hello.

10. Dopo il ripristino di hello ha esito positivo, seguire i passaggi di hello nella sezione hello [applica ripristinato lo stato del sistema toohello di file Server Windows](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), hello toocomplete il processo di ripristino dello stato del sistema.

## <a name="recover-system-state-files-tooan-alternate-server"></a>Ripristinare lo stato del sistema file server alternativo tooan

Se il Server di Windows è danneggiato o non è accessibile e che si desidera toorestore è stabile tooa recuperando hello dello stato del sistema di Windows Server, è possibile ripristinare lo stato del sistema del server di hello danneggiato da un altro server. Utilizzare hello seguendo i passaggi toohello ripristino dello stato del sistema in un server distinto.  

terminologia di Hello utilizzata in questa procedura include:

- *Computer di origine* : macchina originale di hello dal backup hello è stato eseguito e non è attualmente disponibile.
- *Computer di destinazione* : dati di hello macchina toowhich hello viene ripristinati.
- *Insieme di credenziali di esempio* : hello toowhich insieme di credenziali per servizi di ripristino di hello *macchina di origine* e *nel computer di destinazione* registrati. <br/>

> [!NOTE]
> I backup eseguiti da un computer non possono essere ripristinato tooa macchina esegue una versione precedente del sistema operativo hello. Ad esempio, i backup eseguiti da Windows Server 2016 non può essere ripristino tooWindows Server 2012 R2. È tuttavia possibile inverso hello. È possibile utilizzare i backup di Windows Server 2012 R2 toorestore Windows Server 2016.
>

1. Aprire hello **Backup di Microsoft Azure** snap-in hello *nel computer di destinazione*.
2. Verificare che hello *inviala* hello e *macchina di origine* sono registrato toohello servizi di ripristino stesso insieme di credenziali.
3. Fare clic su **Ripristina dati** flusso di lavoro tooinitiate hello.

    ![Ripristina dati](./media/backup-azure-restore-windows-server-classic/recover.png)

4. Selezionare **Un altro server**

    ![Un altro server](./media/backup-azure-restore-system-state/anotherserver.png)

5. Fornire file delle credenziali dell'insieme di credenziali hello corrispondente toohello *insieme di credenziali di esempio*. Caso di file delle credenziali dell'insieme di credenziali hello (scaduti o non validi), è possibile scaricare un nuovo file delle credenziali dell'insieme di credenziali da hello *insieme di credenziali di esempio* in hello portale di Azure. Una volta file delle credenziali dell'insieme di credenziali hello viene fornito, viene visualizzata insieme di credenziali di servizi di ripristino hello associata al file delle credenziali dell'insieme di credenziali di hello.

6. Nel riquadro di selezione Server di Backup hello selezionare hello *macchina di origine* dall'elenco di hello macchine visualizzato.

    ![Elenco di computer](./media/backup-azure-restore-windows-server-classic/machinelist.png)

7. Nel riquadro di selezione modalità ripristino hello, scegliere **dello stato del sistema** e fare clic su **Avanti**. 

    ![Ricerca](./media/backup-azure-restore-system-state/recover-type-selection.png)

8. Nel calendario Ciao hello **seleziona Volume e data** punto riquadro, selezionare un ripristino. È possibile ripristinare da qualsiasi punto di ripristino. Le date in **grassetto** indicare hello la disponibilità di almeno un punto di ripristino. Dopo aver selezionato una data, se sono disponibili più punti di ripristino, scegliere il punto di ripristino specifico di hello da hello **ora** dal menu a discesa. 

    ![Ricerca di elementi](./media/backup-azure-restore-system-state/select-date.png)

9. Dopo aver scelto toorestore punto di ripristino hello, fare clic su **Avanti**.

10. In hello **selezionare modalità di ripristino dello stato sistema** riquadro specificare hello destinazione in cui si desidera toobe ripristinati i file dello stato del sistema, quindi fare clic su **Avanti**.

    ![Crittografia](./media/backup-azure-restore-system-state/recover-as-files.png)

    opzione Hello **crea copie in modo da mantenere entrambe le versioni**, crea le copie dei singoli file in un archivio di file di stato del sistema esistente anziché creare una copia di hello dell'intero archivio dello stato del sistema di hello.

11. Verificare i dettagli di hello di ripristino nel riquadro di conferma hello e fare clic su **ripristinare**. 

    ![Fare clic su processo di ripristino hello tooconfirm pulsante Ripristina hello](./media/backup-azure-restore-system-state/confirm-recovery.png)

12. Hello copia *WindowsImageBackup* volume non critici tooa di directory di server hello (ad esempio d:\). Volume del sistema operativo Windows hello è in genere volume critico hello.

13. processo di ripristino hello toocomplete, sezione troppo seguente hello utilizzare[applicare i file di stato del sistema hello ripristinato in un Server Windows](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).




## <a name="apply-restored-system-state-on-a-windows-server"></a>Applicare lo stato del sistema ripristinato a un'istanza di Windows Server

Dopo aver ripristinato lo stato del sistema come file con l'agente di servizi di ripristino di Azure, utilizzare hello Windows Server Backup Utilità tooapply hello recuperato tooWindows dello stato del sistema Server. Hello utilità di Windows Server Backup è già disponibile nel server di hello. Hello alla procedura seguente viene illustrato come tooapply hello ripristinato lo stato del sistema.

1. Seguente hello utilizzare comandi tooreboot server *modalità ripristino servizi Directory*. In un prompt dei comandi con privilegi elevati:

    ```
    PS C:\> Bcdedit /set safeboot dsrepair
    PS C:\> Shutdown /r /t 0
    ```

2. Dopo il riavvio di hello, aprire lo snap-in Windows Server Backup hello. Se non si conosce in hello snap-in è stato installato, eseguire la ricerca computer hello o un server per **Windows Server Backup**.

    app desktop Hello viene visualizzato nei risultati della ricerca hello.

3. Hello nello snap-in, selezionare **Backup locale**.

    ![Selezionare i Backup locale toorestore da qui](./media/backup-azure-restore-system-state/win-server-backup-local-backup.png)

4. Nella console di Backup locale hello in hello **riquadro azioni**, fare clic su **ripristinare** tooopen hello ripristino guidato.

5. Selezionare l'opzione di hello, **un backup archiviato in un'altra posizione**, fare clic su **Avanti**.

   ![Scegliere toorecover tooa diversi server](./media/backup-azure-restore-system-state/backup-stored-in-diff-location.png)

6. Quando si specifica il tipo di posizione hello, selezionare **cartella condivisa remota** se il backup dello stato del sistema è stato ripristinato tooanother server. Se lo stato del sistema è stato ripristinato localmente, selezionare **Unità locali**. 

    ![Selezionare se toorecovery dal server locale o in un altro](./media/backup-azure-restore-system-state/ss-recovery-remote-shared-folder.png)

7. Immettere hello percorso toohello *WindowsImageBackup* directory, oppure scegliere unità di hello locale contenente la directory (ad esempio, D:\WindowsImageBackup), ripristinata come parte del ripristino di file hello dello stato del sistema mediante il ripristino di Azure L'agente e fare clic su servizi **Avanti**.

    ![percorso file condiviso toohello](./media/backup-azure-restore-system-state/ss-recovery-remote-folder.png)

8. Versione di hello selezionare lo stato del sistema che desidera toorestore e fare clic su **Avanti**.

9. Nel riquadro di selezione tipo di ripristino hello, selezionare **dello stato del sistema** e fare clic su **Avanti**.

10. Per la posizione di hello di hello ripristino dello stato del sistema, selezionare **nel percorso originale**, fare clic su **Avanti**.

11. Rivedere i dettagli di conferma hello, verificare le impostazioni di riavvio hello e fare clic su **ripristinare** tooapplly hello ripristino dei file di stato del sistema.

    ![avvio hello ripristinare i file di stato del sistema](./media/backup-azure-restore-system-state/launch-ss-recovery.png)

## <a name="special-considerations-for-system-state-recovery-on-active-directory-server"></a>Considerazioni speciali per il ripristino dello stato del sistema nel server di Active Directory

Il backup dello stato del sistema include i dati di Active Directory. Utilizzare hello seguendo i passaggi toorestore servizi di dominio Active Directory (AD DS) dallo stato tooa precedente stato corrente.

1. Riavviare il controller di dominio di hello in Directory Services in modalità ripristino.
2. Seguire i passaggi di hello [qui](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) toorecover i cmdlet di Windows Server Backup toouse di dominio Active Directory.


## <a name="troubleshoot-failed-system-state-restore"></a>Risolvere i problemi relativi a un ripristino non riuscito dello stato del sistema

Se il processo precedente di hello dell'applicazione dello stato del sistema non viene completata correttamente, utilizzare hello ambiente ripristino (Win) toorecover di Windows Server. Hello passaggi seguenti illustrano come toorecover tramite ambiente ripristino Windows. Usare questa opzione solo se Windows Server non viene avviato normalmente dopo un ripristino dello stato del sistema. processo Hello Cancella i dati non di sistema, prestare attenzione. 

1. Avvio di Windows Server in ambiente ripristino (Win) hello.

2. Selezionare hello disponibili tre opzioni di risoluzione dei problemi.

    ![Menu iniziale](./media/backup-azure-restore-system-state/winre-1.png)

3. Da hello **opzioni avanzate** selezionare **prompt dei comandi** e fornire nome utente amministratore di server hello e una password.

   ![Menu iniziale](./media/backup-azure-restore-system-state/winre-2.png)

4. Specificare nome utente amministratore di server hello e la password.

    ![Menu iniziale](./media/backup-azure-restore-system-state/winre-3.png)

5. Quando si apre il prompt di comandi hello in modalità amministratore, eseguire versioni dello stato del sistema di hello tooget comando backup successivo.

    ```
    Wbadmin get versions -backuptarget:<Volume where WindowsImageBackup folder is copied>:
    ```
    ![Ottenere le versioni del backup dello stato del sistema](./media/backup-azure-restore-system-state/winre-4.png)

6. Eseguire hello successivo comando tooget tutti i volumi nel backup hello.

    ```
    Wbadmin get items -version:<copy version from above step> -backuptarget:<Backup volume>
    ```

    ![Ottenere le versioni del backup dello stato del sistema](./media/backup-azure-restore-system-state/winre-5.png)

7. Hello comando che segue recupera tutti i volumi che fanno parte di hello Backup dello stato del sistema. Si noti che questo passaggio consente di ripristinare solo hello volumi critici che fanno parte dello stato del sistema hello. Tutti i dati non di sistema vengono cancellati.

    ```
    Wbadmin start recovery -items:C: -itemtype:Volume -version:<Backupversion> -backuptarget:<backup target volume>
    ```
     ![Ottenere le versioni del backup dello stato del sistema](./media/backup-azure-restore-system-state/winre-6.png)



## <a name="next-steps"></a>Passaggi successivi
* Dopo aver ripristinato i file e le cartelle, è possibile [gestire i backup](backup-azure-manage-windows-server.md).
