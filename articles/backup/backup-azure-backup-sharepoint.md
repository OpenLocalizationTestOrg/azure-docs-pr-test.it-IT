---
title: protezione di server/Azure aaaDPM Backup di un tooAzure di farm di SharePoint | Documenti Microsoft
description: In questo articolo viene fornita una panoramica di protezione di server DPM o Azure Backup di un tooAzure di farm di SharePoint
services: backup
documentationcenter: 
author: adigan
manager: Nkolli1
editor: 
ms.assetid: e0c0c252-dc1d-4072-b777-7222c13950b0
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: adigan;giridham;jimpark;trinadhk;markgal
ms.openlocfilehash: 726d59320b8d9f14b38e0f041308019eebcfb77b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-sharepoint-farm-tooazure"></a>Eseguire il backup di un tooAzure di farm di SharePoint
Eseguire il backup di SharePoint della farm tooMicrosoft Azure tramite System Center Data Protection Manager (DPM) in quantità hello stesso modo in cui eseguire il backup di altre origini dati. Backup di Azure fornisce flessibilità di hello toocreate di pianificazione del backup dei punti di backup giornalieri, settimanali, mensili o annuali e fornisce le opzioni di criteri di conservazione per vari punti di backup. DPM fornisce hello funzionalità toostore disco locale copie per gli obiettivi del tempo di recupero rapidi (RTO) e toostore copia tooAzure per la conservazione a lungo termine, economico.

## <a name="sharepoint-supported-versions-and-related-protection-scenarios"></a>Versioni supportate di SharePoint e relativi scenari di protezione
Backup di Azure per Data Protection Manager supporta hello seguenti scenari:

| Carico di lavoro | Versione | Distribuzione di SharePoint | Tipo di distribuzione di DPM | DPM - System Center 2012 R2 | Protezione e ripristino |
| --- | --- | --- | --- | --- | --- |
| SharePoint |SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0 |SharePoint distribuito come un server fisico o macchina virtuale Hyper-V o VmWare <br> -------------- <br> SQL AlwaysOn |Server fisico o macchina virtuale Hyper-V in locale |Supporta tooAzure backup dall'aggiornamento cumulativo 5 |Proteggere le opzioni di ripristino di farm di SharePoint: farm di ripristino, database, e file o voce di elenco dai punti di ripristino del disco.  Farm e ripristino dei database dai punti di ripristino di Azure. |

## <a name="before-you-start"></a>Prima di iniziare
Ci sono alcuni aspetti occorre tooconfirm prima di eseguire il backup di un tooAzure di farm di SharePoint.

### <a name="prerequisites"></a>Prerequisiti
Prima di procedere, assicurarsi di aver soddisfatto tutti hello [prerequisiti per l'utilizzo di Microsoft Azure Backup](backup-azure-dpm-introduction.md#prerequisites) tooprotect i carichi di lavoro. Alcune attività per i prerequisiti includono: creare un insieme di credenziali di backup, scaricare l'insieme di credenziali, installare Azure Backup Agent e registrare i Server di Backup DPM/Azure insieme di credenziali hello.

### <a name="dpm-agent"></a>Agente DPM
agente DPM di Hello deve essere installato sul server hello che esegue SharePoint Server hello che eseguono SQL Server e tutti gli altri server che fanno parte della farm di SharePoint hello. Per ulteriori informazioni su come tooset di agente di protezione hello, vedere [il programma di installazione dell'agente di protezione](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).  Hello unica eccezione è che è installato l'agente di hello solo su un singolo server web. front-end (WFE). Come punto di ingresso hello per la protezione, DPM deve agente hello in uno tooserve solo di server front-end Web.

### <a name="sharepoint-farm"></a>Una farm di SharePoint
Per ogni 10 milioni di elementi nella farm hello, deve essere almeno 2 GB di spazio sul volume hello in cui si trova la cartella di DPM hello. Questo spazio è necessario per la generazione del catalogo. Per DPM toorecover elementi specifici (raccolte siti, siti, elenchi, raccolte documenti, cartelle, singoli documenti e gli elementi dell'elenco), generazione del catalogo consente di creare un elenco di URL hello contenuti all'interno di ogni database del contenuto. È possibile visualizzare l'elenco di hello degli URL nel riquadro elemento ripristinabile hello in hello **ripristino** area della Console amministrazione DPM attività.

### <a name="sql-server"></a>SQL Server
DPM viene eseguito come account LocalSystem. tooback dei database di SQL Server, DPM richiede privilegi di sysadmin per tale account per i server hello che esegue SQL Server. Impostare NT AUTHORITY\SYSTEM troppo*sysadmin* nel server di hello che esegue SQL Server prima di eseguirne il backup.

Se la farm di SharePoint hello dispone di database di SQL Server configurati con gli alias di SQL Server, installare i componenti client di SQL Server hello nel server Web front-end hello protetto da DPM.

### <a name="sharepoint-server"></a>SharePoint Server
Mentre le prestazioni dipendono da molti fattori, ad esempio la dimensione della farm di SharePoint, in linea generale un solo Server DPM può proteggere una farm di SharePoint da 25 TB.

### <a name="dpm-update-rollup-5"></a>Aggiornamento cumulativo 5 di DPM
toobegin protezione di un tooAzure di farm di SharePoint, è necessario tooinstall Data Protection Manager Update Rollup 5 o versione successiva. Aggiornamento cumulativo 5 fornisce hello possibilità tooprotect un tooAzure di farm di SharePoint se hello farm è configurata con SQL AlwaysOn.
Per ulteriori informazioni, vedere i post di blog che introduce hello [Data Protection Manager Update Rollup 5](http://blogs.technet.com/b/dpm/archive/2015/02/11/update-rollup-5-for-system-center-2012-r2-data-protection-manager-is-now-available.aspx)

### <a name="whats-not-supported"></a>Attività non supportate
* DPM protegge una farm di SharePoint, ma non protegge gli indici di ricerca e i database di servizio dell'applicazione. Sarà necessario protezione hello tooconfigure di questi database separatamente.
* DPM non esegue il backup dei database di SQL Server SharePoint ospitati in condivisioni di file server di scalabilità orizzontale.

## <a name="configure-sharepoint-protection"></a>Configurare la protezione di SharePoint
Prima di poter utilizzare DPM tooprotect SharePoint, è necessario configurare il servizio di SharePoint VSS Writer hello (servizio WSS Writer) utilizzando **ConfigureSharePoint.exe**.

È possibile trovare **ConfigureSharePoint.exe** nella cartella \bin hello [percorso di installazione di DPM] nel server web front-end hello. Questo strumento fornisce l'agente protezione hello con credenziali hello per la farm di SharePoint hello. È possibile eseguirlo in un unico server front-end Web. Se si dispone di più server WFE, selezionarne solo uno quando si configura un gruppo di protezione dati.

### <a name="tooconfigure-hello-sharepoint-vss-writer-service"></a>hello tooconfigure servizio SharePoint VSS Writer
1. Nel server di front-end Web hello, al prompt dei comandi, passare troppo \bin\ [percorso di installazione di DPM]
2. Digitare ConfigureSharePoint -EnableSharePointProtection.
3. Immettere le credenziali di amministratore di farm hello. Questo account deve essere un membro del gruppo Administrators locale di hello nel server WFE hello. Se l'amministratore della farm hello non è un hello di amministratore locale concedere queste autorizzazioni nel server front-end Web hello:
   * Concedere hello WSS_Admin_WPG controllo completo toohello DPM cartella gruppo (% programma Files%\Microsoft Data Protection Manager\DPM.).
   * Concedere hello WSS_Admin_WPG gruppo l'accesso in lettura toohello DPM chiave Registro di sistema (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).

> [!NOTE]
> Ogni volta che viene apportata una modifica in credenziali di amministratore di farm SharePoint hello, dovrai toorerun ConfigureSharePoint.exe.
> 
> 

## <a name="back-up-a-sharepoint-farm-by-using-dpm"></a>Eseguire il backup di una farm di SharePoint tramite DPM
Dopo aver configurato hello farm di SharePoint come descritto in precedenza e Data Protection Manager, SharePoint possono essere protetti da DPM.

### <a name="tooprotect-a-sharepoint-farm"></a>tooprotect una farm di SharePoint
1. Da hello **protezione** fare clic sulla scheda della Console amministrazione DPM, hello **New**.
    ![Nuova scheda Protezione](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)
2. In hello **Selezione tipo di gruppo protezione dati** pagina di hello **Crea nuovo gruppo protezione dati** procedura guidata, selezionare **server**, quindi fare clic su **Avanti** .
   
    ![Seleziona tipo di gruppo di protezione dati](./media/backup-azure-backup-sharepoint/select-protection-group-type.png)
3. In hello **Seleziona membri del gruppo** dello schermo, la casella di controllo selezionare hello per il server SharePoint hello tooprotect desiderato e fare clic su **Avanti**.
   
    ![Seleziona membri del gruppo](./media/backup-azure-backup-sharepoint/select-group-members2.png)
   
   > [!NOTE]
   > Con installato l'agente DPM hello, è possibile vedere server hello nella procedura guidata hello. DPM mostra anche la propria struttura. Poiché è stato eseguito ConfigureSharePoint.exe, DPM comunica con il servizio SharePoint VSS Writer hello e i database di SQL Server corrispondenti e riconosce struttura della farm SharePoint hello, hello associata database del contenuto e gli elementi corrispondenti.
   > 
   > 
4. In hello **Selezione metodo protezione dati** pagina, immettere il nome di hello di hello **gruppo protezione dati**e selezionare i Preferiti *metodi di protezione*. Fare clic su **Avanti**.
   
    ![Seleziona metodo protezione dati](./media/backup-azure-backup-sharepoint/select-data-protection-method1.png)
   
   > [!NOTE]
   > metodo di protezione disco Hello consente toomeet breve obiettivi del tempo di recupero. Azure è un tootapes destinazione confrontati protezione economico e a lungo termine. Per ulteriori informazioni, vedere [tooreplace utilizzare Azure Backup infrastruttura nastro](https://azure.microsoft.com/documentation/articles/backup-azure-backup-cloud-as-tape/)
   > 
   > 
5. In hello **Specifica obiettivi a breve termine** pagina, selezionare i Preferiti **mantenimento** e identificare quando si desidera che i backup toooccur.
   
    ![Specifica obiettivi a breve termine](./media/backup-azure-backup-sharepoint/specify-short-term-goals2.png)
   
   > [!NOTE]
   > Poiché ripristino è spesso necessario per i dati che sono inferiore a cinque giorni, è selezionato un intervallo di conservazione di cinque giorni su disco e garantire che il backup hello avviene durante le ore non di produzione, per questo esempio.
   > 
   > 
6. Spazio su disco del pool archiviazione hello allocato per il gruppo di protezione hello di esaminare e quindi fare clic su **Avanti**.
7. Per ogni gruppo protezione dati, DPM alloca toostore di spazio su disco e gestire le repliche. A questo punto, DPM deve creare una copia dei dati hello selezionato. Selezionare come e quando desidera che la replica hello creato e quindi fare clic su **Avanti**.
   
    ![Scelta del metodo per la creazione della replica](./media/backup-azure-backup-sharepoint/choose-replica-creation-method.png)
   
   > [!NOTE]
   > Assicurarsi che il traffico di rete non viene effettuato, toomake selezionare un'ora fuori dall'orario di produzione.
   > 
   > 
8. DPM assicura l'integrità dei dati mediante l'esecuzione di verifiche di coerenza sulla replica hello. Sono disponibili due opzioni: È possibile definire le verifiche della coerenza toorun una pianificazione o DPM può eseguire verifiche di coerenza automaticamente nella replica di hello ogni volta che diventa incoerente. Selezionare l'opzione preferita e fare clic su **Avanti**.
   
    ![Verifica coerenza](./media/backup-azure-backup-sharepoint/consistency-check.png)
9. In hello **specificare dati da proteggere Online** pagina, selezionare hello farm di SharePoint che desidera tooprotect e quindi fare clic su **Avanti**.
   
    ![DPM SharePoint Protection1](./media/backup-azure-backup-sharepoint/select-online-protection1.png)
10. In hello **specificare la pianificazione dei Backup Online** pagina, selezionare la pianificazione preferita e quindi fare clic su **Avanti**.
    
    ![Online_backup_schedule](./media/backup-azure-backup-sharepoint/specify-online-backup-schedule.png)
    
    > [!NOTE]
    > DPM fornisce un massimo di due tooAzure backup giornaliero in momenti diversi. Backup di Azure può inoltre controllare quantità hello di larghezza di banda WAN che può essere utilizzato per i backup in ore di punta e non di punta utilizzando [limitazione delle richieste di rete di Azure Backup](https://azure.microsoft.com/en-in/documentation/articles/backup-configure-vault/#enable-network-throttling).
    > 
    > 
11. A seconda della pianificazione del backup hello selezionato, hello **specificare criteri di conservazione Online** pagina Criteri di conservazione hello selezionare i punti di backup giornalieri, settimanali, mensili e annuali.
    
    ![Online_retention_policy](./media/backup-azure-backup-sharepoint/specify-online-retention.png)
    
    > [!NOTE]
    > DPM usa uno schema di conservazione GFS (Grandfather-Father-Son, nonno-padre-figlio) in cui è possibile scegliere criteri di conservazione diversi per punti di backup diversi.
    > 
    > 
12. Toodisk simile, una replica del punto di riferimento iniziale deve toobe creato in Azure. Selezionare il toocreate opzione preferita tooAzure una copia di backup iniziale e quindi fare clic su **Avanti**.
    
    ![Online_replica](./media/backup-azure-backup-sharepoint/online-replication.png)
13. Esaminare le impostazioni selezionate in hello **riepilogo** pagina e quindi fare clic su **Crea gruppo**. Dopo aver creato il gruppo di protezione dati hello, visualizzeranno un messaggio di conferma.
    
    ![Riepilogo](./media/backup-azure-backup-sharepoint/summary.png)

## <a name="restore-a-sharepoint-item-from-disk-by-using-dpm"></a>Ripristinare un elemento di SharePoint dal disco tramite DPM
Nell'esempio seguente di hello, hello *elemento di ripristino SharePoint* è stato accidentalmente eliminato ed è necessario toobe recuperato.
![DPM SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)

1. Aprire hello **Console amministrazione DPM**. Tutte le farm di SharePoint che sono protetti da DPM vengono visualizzate in hello **protezione** scheda.
   
    ![DPM SharePoint Protection3](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection4.png)
2. elemento hello toobegin toorecover hello seleziona **ripristino** scheda.
   
    ![DPM SharePoint Protection5](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection6.png)
3. È possibile eseguire ricerche in SharePoint relative all' *elemento di SharePoint da ripristinare* tramite una ricerca con caratteri jolly all'interno di un intervallo di punti di ripristino.
   
    ![DPM SharePoint Protection6](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection7.png)
4. Selezionare il punto di ripristino appropriato di hello dai risultati della ricerca hello, fare doppio clic su elemento hello e quindi selezionare **ripristinare**.
5. È anche possibile esplorare vari punti di ripristino e selezionare un database o un elemento di toorecover. Selezionare **data > tempo di recupero**, quindi selezionare hello corretto **Database > farm di SharePoint > punto di ripristino > elemento**.
   
    ![DPM SharePoint Protection7](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection8.png)
6. Elemento hello e quindi scegliere **ripristinare** tooopen hello **ripristino guidato**. Fare clic su **Avanti**.
   
    ![Verifica selezione per ripristino](./media/backup-azure-backup-sharepoint/review-recovery-selection.png)
7. Selezionare il tipo di hello di ripristino che desidera tooperform e quindi fare clic su **Avanti**.
   
    ![Tipo di ripristino](./media/backup-azure-backup-sharepoint/select-recovery-type.png)
   
   > [!NOTE]
   > selezione di Hello **ripristinare toooriginal** in hello viene recuperato hello elemento toohello originale sito di SharePoint.
   > 
   > 
8. Seleziona hello **il processo di ripristino** che si desidera toouse.
   
   * Selezionare **Ripristina senza utilizzare una farm di ripristino** se la farm di SharePoint hello non è stato modificato e hello identico ripristino hello punto di ripristino.
   * Selezionare **eseguire il ripristino utilizzando una farm di ripristino** farm di SharePoint hello è stato modificato dopo il punto di ripristino hello è stato creato.
     
     ![processo di ripristino](./media/backup-azure-backup-sharepoint/recovery-process.png)
9. Forniscono temporaneamente un database di hello toorecover gestione temporanea del percorso istanza SQL Server e una condivisione di file di gestione temporanea nel server DPM hello e hello elemento hello toorecover di SharePoint in esecuzione.
   
    ![Staging Location1](./media/backup-azure-backup-sharepoint/staging-location1.png)
   
    Data Protection Manager Collega database del contenuto hello che ospita hello SharePoint elemento toohello temporaneo istanza di SQL Server. Dal database del contenuto, hello server DPM hello Ripristina elemento hello e inserisce nel percorso di file nel server DPM hello di gestione temporanea hello. Hello elemento ripristinato nel percorso di gestione temporanea del server DPM hello ora hello deve toohello toobe esportato percorso nella farm di SharePoint hello di gestione temporanea.
   
    ![Gestione temporanea Location2](./media/backup-azure-backup-sharepoint/staging-location2.png)
10. Selezionare **Specifica opzioni di ripristino**e applicare le impostazioni di sicurezza toohello farm di SharePoint o applicare le impostazioni di sicurezza hello hello del punto di ripristino. Fare clic su **Avanti**.
    
    ![Opzioni di ripristino](./media/backup-azure-backup-sharepoint/recovery-options.png)
    
    > [!NOTE]
    > È possibile scegliere l'utilizzo della larghezza di banda di rete hello toothrottle. In questo modo viene ridotta del server di produzione toohello impatto durante le ore di produzione.
    > 
    > 
11. Esaminare le informazioni di riepilogo hello e quindi fare clic su **ripristinare** toobegin ripristino del file hello.
    
    ![Riepilogo di ripristino](./media/backup-azure-backup-sharepoint/recovery-summary.png)
12. A questo punto selezionare hello **monitoraggio** scheda hello **Console amministrazione DPM** tooview hello **stato** di ripristino hello.
    
    ![Stato di ripristino](./media/backup-azure-backup-sharepoint/recovery-monitoring.png)
    
    > [!NOTE]
    > file Hello viene ora ripristinato. È possibile aggiornare il file ripristinato hello toocheck di hello SharePoint del sito.
    > 
    > 

## <a name="restore-a-sharepoint-database-from-azure-by-using-dpm"></a>Ripristinare un database di SharePoint da Azure tramite DPM
1. toorecover un database del contenuto di SharePoint, esplorare i vari punti di ripristino (come illustrato in precedenza) e selezionare il punto di ripristino hello che si desidera toorestore.
   
    ![DPM SharePoint Protection8](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection9.png)
2. Fare doppio clic su hello SharePoint tooshow punto hello disponibili SharePoint catalogo informazioni di ripristino.
   
   > [!NOTE]
   > Poiché la farm di SharePoint hello è protetto per la conservazione a lungo termine in Azure, non è disponibile nel server DPM hello alcuna informazione di catalogo (metadati). Di conseguenza, ogni volta che un database del contenuto SharePoint in un momento deve toobe recuperato, è necessario farm di SharePoint hello toocatalog nuovamente.
   > 
   > 
3. Fare clic su **Ricatalogazione**.
   
    ![DPM SharePoint Protection10](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection12.png)
   
    Hello **Cloud ricatalogare** verrà visualizzata la finestra di stato.
   
    ![DPM SharePoint Protection11](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection13.png)
   
    Una volta terminata la catalogazione, hello passerà troppo*successo*. Fare clic su **Close**.
   
    ![DPM SharePoint Protection12](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection14.png)
4. Fare clic su oggetti di SharePoint hello nella hello DPM **ripristino** scheda struttura di database del contenuto tooget hello. Fare doppio clic su elemento hello e quindi fare clic su **ripristinare**.
   
    ![DPM SharePoint Protection13](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection15.png)
5. A questo punto, seguire hello [i passaggi di ripristino più indietro in questo articolo](#restore-a-sharepoint-item-from-disk-using-dpm) toorecover un database del contenuto di SharePoint dal disco.

## <a name="faqs"></a>Domande frequenti
D: quali versioni di DPM supportano SQL Server 2014 e SQL 2012 (SP2)?<br>
R: DPM 2012 R2 con aggiornamento cumulativo 4 supporta entrambi.

D: è possibile risolvere un percorso di SharePoint elemento toohello originale se SharePoint è configurato con AlwaysOn di SQL (con protezione disco)?<br>
R: Sì, elemento hello può essere ripristinato toohello originale sito di SharePoint.

D: è possibile risolvere un percorso originale del database toohello SharePoint se SharePoint è configurata con SQL AlwaysOn?<br>
R: poiché i database di SharePoint sono configurati in SQL AlwaysOn, non possono essere modificati a meno che non viene rimosso il gruppo di disponibilità hello. Di conseguenza, DPM non è possibile ripristinare un percorso del database toohello originale. È possibile ripristinare un'istanza di SQL Server tooanother database di SQL Server.

## <a name="next-steps"></a>Passaggi successivi
* Ulteriori informazioni su Protezione DPM di SharePoint, vedere [Serie di Video - Protezione DPM di SharePoint](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)
* Esaminare le [Note sulla versione di System Center 2012 - Data Protection Manager](https://technet.microsoft.com/library/jj860415.aspx)
* Esaminare le [Note sulla versione di Data Protection Manager in System Center 2012 SP1](https://technet.microsoft.com/library/jj860394.aspx)

