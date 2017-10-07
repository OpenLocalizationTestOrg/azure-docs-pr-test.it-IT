---
title: Backup - backup non in linea o iniziale usando seeding aaaAzure hello servizio importazione/esportazione di Azure | Documenti Microsoft
description: Informazioni su come il Backup di Azure consente dati toosend rete hello mediante il servizio di importazione/esportazione di Azure hello. Questo articolo spiega offline seeding hello hello iniziale dei dati di backup utilizzando il servizio di importazione/esportazione di Azure hello.
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: ada19c12-3e60-457b-8a6e-cf21b9553b97
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 4/20/2017
ms.author: saurse;nkolli;trinadhk
ms.openlocfilehash: f1696957c3e9684b800c8d030131255905459f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="offline-backup-workflow-in-azure-backup"></a>Flusso di lavoro del backup offline in Backup di Azure
Backup di Azure offre diversi miglioramenti di efficienza incorporati che ridurre i costi di rete e di archiviazione durante hello iniziale backup completi dei dati tooAzure. Backup completo iniziale, in genere trasferiscono grandi quantità di dati e richiedono maggiore larghezza di banda di rete quando vengono confrontati i backup toosubsequent che trasferiscono solo hello delta/incrementali. Backup di Azure consente di comprimere i backup iniziale hello. Attraverso il processo di seeding offline hello Azure Backup può utilizzare tooAzure dati di backup iniziali di hello compresso tooupload dischi non in linea.  

Hello offline seeding processo di Backup di Azure è strettamente integrato con hello [servizio di importazione/esportazione di Azure](../storage/common/storage-import-export-service.md) che consente di tootransfer dati tooAzure, utilizzando i dischi. Se si dispone di terabyte (TB) di dati di backup iniziali deve toobe trasferiti su una rete ad alta latenza e larghezza di banda ridotta, è possibile utilizzare hello offline seeding del flusso di lavoro tooship hello copia di backup iniziale in uno o più unità disco rigido tooan Data Center di Azure. In questo articolo viene fornita una panoramica dei passaggi hello completare il flusso di lavoro.

## <a name="overview"></a>Panoramica
Con funzionalità offline seeding hello di Backup di Azure e di importazione/esportazione di Azure, è semplice tooupload hello dati offline tooAzure utilizzando i dischi. Anziché trasferire la copia completa di hello iniziale tramite rete hello, dati di backup hello viene scritto tooa *percorso di gestione temporanea*. Percorso di gestione temporanea di hello copia toohello al termine utilizzando lo strumento di importazione/esportazione di Azure hello, questi dati vengono scritti tooone o SATA più unità, a seconda della quantità di hello di dati. Queste unità sono infine spedito toohello più vicino al Data Center di Azure.

Hello [aggiornamento di agosto 2016, di Backup di Azure (e versioni successive)](http://go.microsoft.com/fwlink/?LinkID=229525) include hello *lo strumento di preparazione del disco di Azure*, denominato AzureOfflineBackupDiskPrep, che:

* Consente di preparare le unità per l'importazione di Azure utilizzando lo strumento di importazione/esportazione di Azure hello.
* Verrà automaticamente creato un processo di importazione di Azure per il servizio di importazione/esportazione di Azure hello su hello [portale di Azure classico](https://manage.windowsazure.com) come toocreating anziché hello stesso manualmente con le versioni precedenti di Azure Backup.

Al termine di caricamento hello di hello tooAzure di dati di backup, Backup di Azure copia l'insieme di credenziali di backup toohello hello dati di backup e hello incrementali vengono pianificati.

> [!NOTE]
> toouse hello Azure disco Preparation tool, assicurarsi di aver installato l'aggiornamento di agosto 2016 hello di Backup di Azure (o versione successiva) e vengono eseguiti tutti i passaggi di hello del flusso di lavoro hello con esso. Se si utilizza una versione precedente di Backup di Azure, è possibile preparare l'unità SATA hello utilizzando lo strumento di importazione/esportazione di Azure hello come descritto in dettaglio nelle sezioni successive di questo articolo.
>
>

## <a name="prerequisites"></a>Prerequisiti
* [Acquisire familiarità con il flusso di importazione/esportazione di Azure hello](../storage/common/storage-import-export-service.md).
* Prima dell'avvio del flusso di lavoro di hello, verificare i seguenti hello:
  * È stato creato un insieme di credenziali di Backup di Azure.
  * Le credenziali dell'insieme di credenziali sono state scaricate.
  * Hello Azure Backup agent è stato installato in Windows Server e Windows client o server di System Center Data Protection Manager e computer di hello è registrato con l'insieme di credenziali di hello Azure Backup.
* [Il download delle impostazioni di file di pubblicazione Azure hello](https://manage.windowsazure.com/publishsettings) computer hello da cui si prevede tooback backup dei dati.
* Preparare un percorso di gestione temporanea, potrebbe essere una condivisione di rete o unità aggiuntive nel computer di hello. Hello percorso di gestione temporanea è di archiviazione temporaneo e viene utilizzato durante il flusso di lavoro. Verificare che hello percorso di gestione temporanea è sufficiente toohold di spazio su disco la copia iniziale. Ad esempio, se si sta tentando di tooback di un server di file di 500 GB, assicurarsi di che tale area di gestione temporanea hello è di almeno 500 GB. (Una quantità inferiore viene utilizzata scadenza toocompression.)
* Verificare che sia in uso un'unità supportata. Per l'utilizzo con servizio di importazione/esportazione hello sono supportati solo da 2,5 pollici unità SSD o 2.5 o 3,5 SATA II/III dischi rigidi interni. È possibile usare dischi rigidi backup too10 TB. Controllare hello [documentazione del servizio importazione/esportazione di Azure](../storage/common/storage-import-export-service.md#hard-disk-drives) per hello set più recente di unità che supporta servizio hello.
* Attivare BitLocker hello computer toowhich writer di unità SATA hello è connesso.
* [Scaricare lo strumento di importazione/esportazione di Azure hello](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409) del writer di unità SATA toohello computer toowhich hello è connesso. Questo passaggio non è obbligatorio se si hanno scaricato e installato l'aggiornamento di agosto 2016 hello di Backup di Azure (o versione successiva).

## <a name="workflow"></a>Flusso di lavoro
informazioni di Hello in questa sezione consentono di completamento del flusso di lavoro di hello backup offline in modo che i dati possono essere recapitati tooan Data Center di Azure e caricati tooAzure archiviazione. Se hai domande sul servizio di importazione hello o l'aspetto del processo di hello, vedere hello [Cenni preliminari sul servizio di importazione](../storage/common/storage-import-export-service.md) documentazione a cui fa riferimento in precedenza.

### <a name="initiate-offline-backup"></a>Avviare il backup offline
1. Quando si pianifica un backup, viene visualizzato hello seguente schermata (in Windows Server, client di Windows o System Center Data Protection Manager).

    ![Schermata di importazione](./media/backup-azure-backup-import-export/offlineBackupscreenInputs.png)

    Ecco schermata corrispondente hello in System Center Data Protection Manager: <br/>
    ![Schermata di importazione di DPM](./media/backup-azure-backup-import-export/dpmoffline.png)

    Descrizione Hello di input hello è come segue:

    * **Percorso gestione temporanea**: hello archiviazione temporanea percorso toowhich hello copia di backup iniziale viene scritto. Può essere una condivisione di rete o un computer locale. Se il computer di copia hello e computer di origine sono diverse, è consigliabile specificare il percorso di rete completo hello di hello percorso di gestione temporanea.
    * **Nome di processo di importazione Azure**: nome univoco di hello quali importazione di Azure Backup di Azure e servizio di tenere traccia del trasferimento hello dei dati inviati su dischi tooAzure.
    * **Impostazioni di pubblicazione di Azure**: file XML contenente informazioni sul profilo di sottoscrizione. Contiene anche le credenziali sicure associate alla sottoscrizione. È possibile [scaricare file hello](https://manage.windowsazure.com/publishsettings). Fornire hello percorso locale toohello pubblicare file di impostazioni.
    * **ID sottoscrizione Azure**: hello ID sottoscrizione di Azure per sottoscrizione hello in cui si prevede di processo di importazione di Azure tooinitiate hello. Se si dispone di più sottoscrizioni di Azure, utilizzare l'ID di hello della sottoscrizione di hello che si desidera tooassociate con il processo di importazione hello.
    * **Account di archiviazione Azure**: account di archiviazione di tipo classico hello in hello fornito sottoscrizione di Azure che verrà associato il processo di importazione di Azure hello.
    * **Contenitore di archiviazione Azure**: nome hello del blob di archiviazione di destinazione di hello in hello account di archiviazione di Azure in cui viene importati i dati di questo processo.

    > [!NOTE]
    > Se è stato registrato il tooan server Servizi di ripristino di Azure dell'insieme di credenziali da hello [portale di Azure](https://portal.azure.com) per il backup e non si trovano in una sottoscrizione di Provider di soluzioni Cloud (CSP), è possibile comunque creare un account di archiviazione di tipo classico da hello Portale di Azure e usarlo per flusso di lavoro di hello backup non in linea.
    >
    >

     Salvare tutte queste informazioni perché è necessario tooenter nuovamente nella procedura seguente. Solo hello *percorso di gestione temporanea* è necessario se si usa dischi hello tooprepare di hello Azure disco preparazione dello strumento.    
2. Completamento del flusso di lavoro hello e quindi selezionare **Effettua backup** nella copia di Backup di Azure management console tooinitiate hello-backup offline hello. backup iniziale Hello viene scritto l'area di gestione temporanea toohello come parte di questo passaggio.

    ![Esegui backup ora](./media/backup-azure-backup-import-export/backupnow.png)

    toocomplete hello corrispondente flusso di lavoro in System Center Data Protection Manager, fare doppio clic su hello **gruppo protezione dati**, quindi scegliere hello **Crea punto di ripristino** opzione. Scegliere quindi hello **Online Protection** opzione.

    ![Esegui backup di DPM ora](./media/backup-azure-backup-import-export/dpmbackupnow.png)

    Al termine dell'operazione di hello, hello percorso di gestione temporanea è pronto toobe utilizzato per la preparazione del disco.

    ![Stato del backup](./media/backup-azure-backup-import-export/opbackupnow.png)

### <a name="prepare-a-sata-drive-and-create-an-azure-import-job-by-using-hello-azure-disk-preparation-tool"></a>Preparare un'unità SATA e creare un processo di importazione di Azure utilizzando lo strumento di preparazione del disco di Azure hello
lo strumento di preparazione del disco di Azure Hello è disponibile nella directory di installazione dell'agente di servizi di ripristino hello (aggiornamento di agosto 2016 e versioni successive) nel seguente percorso hello.

   *\Microsoft* *Azure* *Recovery* *Services* *Agent\Utils\*

1. Passare la directory toohello e hello copia **AzureOfflineBackupDiskPrep** computer copia tooa di directory in cui hello sono montati toobe unità preparata. Verificare segue hello al computer di copia toohello considerare:

    * Hello copia computer possa accedere hello percorso flusso di lavoro non in linea seeding hello di gestione temporanea usando la stessa rete percorso fornito in hello hello **avviare il backup non in linea** flusso di lavoro.
    * BitLocker è abilitato nel computer di hello.
    * Hello hello portale di Azure può accedere.

    Se necessario, il computer di copia hello possibile hello stesso hello computer di origine.
2. Aprire un prompt dei comandi con privilegi elevati nel computer di copia hello con directory dello strumento di preparazione del disco di Azure hello come directory corrente hello ed eseguire hello comando seguente:

    `*.\AzureOfflineBackupDiskPrep.exe*   s:<*Staging Location Path*>   [p:<*Path tooPublishSettingsFile*>]`

    | . | Descrizione |
    | --- | --- |
    | s:&lt;*Percorso posizione staging*&gt; |Input obbligatori tooprovide hello percorso toohello percorso immesso in hello di gestione temporanea utilizzato **avviare il backup non in linea** flusso di lavoro. |
    | p:&lt;*tooPublishSettingsFile percorso*&gt; |Input facoltativi che è usato tooprovide hello percorso toohello **impostazioni di pubblicazione Azure** file immesso nella hello **avviare il backup non in linea** flusso di lavoro. |

    > [!NOTE]
    > Hello &lt;percorso tooPublishSettingFile&gt; valore è obbligatorio quando il computer di copia hello e computer di origine sono diverse.
    >
    >

    Quando si esegue il comando hello, strumento hello richiede la selezione hello del processo di importazione di Azure hello corrispondente unità toohello necessarie toobe preparato. Se solo hello fornito percorso gestione temporanea è associato un processo di importazione singola, viene visualizzata una schermata simile hello uno che segue.

    ![Input dello strumento di preparazione dischi di Azure](./media/backup-azure-backup-import-export/azureDiskPreparationToolDriveInput.png) <br/>
3. Immettere la lettera di unità hello senza hello finali di due punti per hello disco montato che si vuole tooprepare per tooAzure di trasferimento. Fornire la conferma per hello la formattazione dell'unità di hello quando richiesto.

    strumento di Hello inizia quindi a disco hello tooprepare con dati di backup hello. Potrebbe essere necessario tooattach dischi aggiuntivi quando viene richiesto dallo strumento hello nel caso in cui hello fornito disco non dispone di spazio sufficiente per i dati di backup hello. <br/>

    Alla fine di hello della corretta esecuzione dello strumento hello, uno o più dischi fornito dall'utente sono stati preparati per tooAzure di spedizione. Inoltre, un processo di importazione con nome hello fornita durante hello **avviare il backup non in linea** flusso di lavoro viene creato nel portale di Azure classico hello. Infine, hello strumento visualizza hello toohello indirizzo shipping Data Center di Azure in cui i dischi di hello devono toobe forniti e hello processo di importazione hello toolocate collegamento nel portale di Azure classico hello.

    ![Preparazione dischi di Azure completata](./media/backup-azure-backup-import-export/azureDiskPreparationToolSuccess.png)<br/>

4. Spedizione hello dischi toohello indirizzo tale strumento hello fornito e mantenere hello rilevamento numero per riferimento futuro.<br/>

5. Quando si passa toohello collegare tale strumento hello visualizzato, hello di account di archiviazione di Azure specificato nel hello **avviare il backup non in linea** flusso di lavoro. Qui è possibile visualizzare il processo di importazione hello appena creato in hello **importazione/esportazione** scheda hello dell'account di archiviazione.

    ![Processo di importazione creato](./media/backup-azure-backup-import-export/ImportJobCreated.png)<br/>

6. Fare clic su **informazioni sulla spedizione** nella parte inferiore di hello di hello pagina tooupdate i dettagli del contatto come illustrato nella seguente schermata hello. Microsoft utilizza questo tooship info del tooyou indietro dischi dopo il processo di importazione hello è terminata.

    ![Informazioni di contatto](./media/backup-azure-backup-import-export/contactInfoAddition.PNG)<br/>

7. Immettere i dettagli di spedizione nella schermata successiva hello hello. Fornire hello **vettore di recapito** e **rilevamento numero** dettagli corrispondenti toohello dischi che sono stati inviati toohello Data Center di Azure.

    ![INFORMAZIONI SULLA SPEDIZIONE](./media/backup-azure-backup-import-export/shippingInfoAddition.PNG)<br/>

### <a name="complete-hello-workflow"></a>Flusso di lavoro completo hello
Al termine del processo di importazione hello, dati di backup iniziali sono disponibili nell'account di archiviazione. Hello agente servizi di ripristino, quindi copia il contenuto di hello dati hello da questo insieme di credenziali di account toohello Backup o i servizi di ripristino di credenziali, a seconda del valore è applicabile. In fase di backup pianificato come successivo hello hello Azure Backup agent esegue backup incrementale hello sulla copia di backup iniziale hello.

> [!NOTE]
> Hello nelle sezioni seguenti si applicano toousers delle versioni precedenti di Azure Backup che non dispongono di strumento di preparazione del disco di Azure toohello di accesso.
>
>

### <a name="prepare-a-sata-drive"></a>Preparare un'unità SATA
1. Scaricare hello [dello strumento di importazione/esportazione di Microsoft Azure](http://go.microsoft.com/fwlink/?linkid=301900&clcid=0x409) toohello computer di copia. Verificare che hello percorso di gestione temporanea sia accessibile dal computer di hello in cui si prevede di set successivo di hello toorun dei comandi. Se necessario, il computer di copia hello possibile hello stesso hello computer di origine.

2. Decomprimere il file di WAImportExport.zip hello. Eseguire lo strumento WAImportExport hello che formatta unità SATA hello, scrive unità SATA toohello dati di backup di hello e viene crittografata. Prima di eseguire il comando seguente hello, assicurarsi che BitLocker è abilitato nel computer di hello. <br/>

    `*.\WAImportExport.exe PrepImport /j:<*JournalFile*>.jrn /id: <*SessionId*> /sk:<*StorageAccountKey*> /BlobType:**PageBlob** /t:<*TargetDriveLetter*> /format /encrypt /srcdir:<*staging location*> /dstdir: <*DestinationBlobVirtualDirectory*>/*`

    > [!NOTE]
    > Se è stato installato l'aggiornamento di agosto 2016 hello di Backup di Azure (o versione successiva), verificare che hello percorso immesso di gestione temporanea è hello stesso hello uno su hello **Effettua backup** schermata e contiene i file AIB e Blob di Base.
    >
    >

| . | Description |
| --- | --- |
| /j:<*FileJournal*> |file journal di Hello percorso toohello. Ogni unità deve contenere esattamente un file journal. file journal Hello non deve essere nell'unità di destinazione hello. estensione del file journal Hello è .jrn e viene creato come parte dell'esecuzione di questo comando. |
| /id:<*IDSessione*> |ID di sessione Hello identifica una sessione di copia. È utilizzato tooensure accurata del recupero di una sessione di copia interrotta. I file vengono copiati in una sessione di copia vengono archiviati in una directory denominata hello ID di sessione nell'unità di destinazione hello dopo. |
| /sk:<*ChiaveAccountArchiviazione*> |chiave dell'account per i dati hello hello storage account toowhich Hello viene importato. prova prova toobe esigenze chiave corrisponde a quello immesso durante la creazione del gruppo di criteri di backup/protezione dati. |
| /BlobType |tipo di Hello del blob. Il flusso di lavoro verrà completato correttamente solo se viene specificato **PageBlob** . Questo non è predefinita hello e dovrebbe essere citato in questo comando. |
| /t: <*LetteraUnitàDestinazione*> |lettera di unità Hello senza hello finali di due punti del disco rigido di destinazione hello per sessione di copia corrente di hello. |
| /format |unità di hello tooformat opzione Hello. Specificare questo parametro quando l'unità hello deve toobe formattata; in caso contrario, ometterlo. Prima di formattare unità hello hello, chiesta una conferma dalla console hello. toosuppress hello conferma, specificare il parametro /silentmode. hello. |
| /encrypt |unità di hello tooencrypt opzione Hello. Specificare questo parametro quando l'unità di hello non è ancora stata crittografata con BitLocker ed esigenze toobe crittografati dallo strumento hello. Se l'unità di hello è già stato crittografato con BitLocker, omettere questo parametro, specificare il parametro /bk hello e fornire chiave BitLocker esistente hello. Se si specifica il parametro /format hello, è necessario specificare hello / crittografare il parametro. |
| /srcdir: <*DirectoryOrigine*> |directory di origine Hello che contiene i file toobe copiati toohello unità di destinazione. Verificare che il nome di directory specificato hello è un percorso completo, invece che relativo. |
| /dstdir: <*DirectoryVirtualeBLOBDestinazione*> |Hello percorso toohello directory virtuale di destinazione nell'account di archiviazione di Azure. Essere toouse che i nomi di contenitore valido quando si specificano BLOB o directory virtuale di destinazione hello. Tenere presente che i nomi di contenitore devono essere costituiti da lettere minuscole.  Il nome di contenitore deve essere hello uno immessi durante la creazione del gruppo di criteri di backup/protezione dati. |

> [!NOTE]
> Nella cartella WAImportExport hello che acquisisce le informazioni sull'intero hello del flusso di lavoro hello viene creato un file di registrazione. Questo file è necessario quando si crea un processo di importazione nel portale di Azure hello.
>
>

  ![Output di PowerShell](./media/backup-azure-backup-import-export/psoutput.png)

### <a name="create-an-import-job-in-hello-azure-portal"></a>Creare un processo di importazione nel portale di Azure hello
1. Passare l'account di archiviazione tooyour in hello [portale di Azure classico](https://manage.windowsazure.com/), fare clic su **importazione/esportazione**e quindi **Crea processo di importazione** nel riquadro attività hello.

    ![Scheda importazione/esportazione hello portale di Azure](./media/backup-azure-backup-import-export/azureportal.png)

2. Nel passaggio 1 della procedura guidata hello, indicano che è stato preparato l'unità e di disporre hello file journal di unità disponibile.

3. Nel passaggio 2 della procedura guidata hello, fornire le informazioni di contatto per persona hello è responsabile di questo processo di importazione.

4. Nel passaggio 3, caricare il file journal di unità hello ottenuto nella sezione precedente hello.

5. Nel passaggio 4, immettere un nome descrittivo per il processo di importazione hello immessi durante la creazione del gruppo di criteri di backup/protezione dati. nome Hello immesso può contenere solo lettere minuscole, numeri, trattini e caratteri di sottolineatura, deve iniziare con una lettera e non può contenere spazi. nome Hello scelto è tootrack utilizzati i processi mentre sono in corso e una volta completati.

6. Successivamente, selezionare l'area Data Center dall'elenco di hello. area Data Center Hello indica toowhich hello Data Center e l'indirizzo, è necessario spedire il pacchetto.

    ![Selezionare l'area geografica del data center](./media/backup-azure-backup-import-export/dc.png)

7. Nel passaggio 5, hello riepilogo selezionare il vettore di ritorno e immettere il numero di account del vettore. Questo account viene utilizzato Microsoft tooship unità di backup tooyou dopo il completamento del processo di importazione.

8. Inviare il disco hello e immettere hello numero tootrack hello lo stato della spedizione hello di rilevamento. Dopo che il disco hello arriva nel Data Center di hello, viene copiato toohello account di archiviazione e lo stato di hello viene aggiornato.

    ![Stato di completamento](./media/backup-azure-backup-import-export/complete.png)

### <a name="complete-hello-workflow"></a>Flusso di lavoro completo hello
Dopo che i dati di backup iniziale hello sono disponibili nell'account di archiviazione, hello agente servizi di ripristino di Microsoft Azure copia il contenuto di hello di dati hello da questo insieme di credenziali di account toohello Backup o di un insieme di credenziali di servizi di ripristino, a seconda del valore è applicabile. Nella pianificazione successiva hello ora del backup, hello Azure Backup agent esegue backup incrementale hello sulla copia di backup iniziale hello.

## <a name="next-steps"></a>Passaggi successivi
* Per eventuali domande sul flusso di lavoro di hello importazione/esportazione di Azure, vedere troppo[utilizzare hello importazione/esportazione di Microsoft Azure service tootransfer tooBlob](../storage/common/storage-import-export-service.md).
* Vedere sezione backup non in linea toohello hello Azure Backup [domande frequenti su](backup-azure-backup-faq.md) per eventuali domande sul flusso di lavoro hello.
