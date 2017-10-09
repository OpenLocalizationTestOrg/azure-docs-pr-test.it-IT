---
title: Report aaaConfigure per il Backup di Azure
description: In questo articolo viene illustrata la configurazione dei report di Power BI per Backup di Azure usando l'insieme di credenziali di Servizi di ripristino.
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 86e465f1-8996-4a40-b582-ccf75c58ab87
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/24/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 503a240b36ea999e0fea434b6a50d26ddf7677bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-backup-reports"></a>Configurare report di Backup di Azure
In questo articolo parla passaggi tooconfigure report per il Backup di Azure utilizzando l'insieme di credenziali di servizi di ripristino e tooaccess questi report utilizzando Power BI. Dopo aver eseguito questi passaggi, è possibile direttamente passare tooview tooPower BI tutti i report di hello, personalizzare e creare report. 

## <a name="supported-scenarios"></a>Scenari supportati
1. I report di Azure Backup sono supportati per la macchina virtuale di Azure backup e file o la cartella backup toocloud utilizzando l'agente di servizi di ripristino di Azure.
2. In questo momento non sono supportati i report per Azure SQL, DPM e il server di Backup di Azure.
3. È possibile visualizzare i report tra insiemi di credenziali e tra le sottoscrizioni, se lo stesso account di archiviazione è configurato per ciascuno degli insiemi di credenziali hello. Account di archiviazione selezionato deve essere hello ripristino stessa area dell'insieme di credenziali dei servizi.
4. frequenza di Hello di aggiornamento pianificato per i report di hello è 24 ore in Power BI. È anche possibile eseguire un aggiornamento ad hoc di hello report in Power BI, in cui i casi dati più recenti nell'account di archiviazione di clienti viene utilizzati per il rendering dei report. 

## <a name="prerequisites"></a>Prerequisiti
1. Creare un [account di archiviazione Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) tooconfigure per i report. Questo account di archiviazione viene usato per archiviare i dati correlati ai report.
2. [Creare un account di Power BI](https://powerbi.microsoft.com/landing/signin/) tooview, personalizzare e creare report personalizzati usando il portale di Power BI.
3. Registrare il provider di risorse hello **Insights** se non è registrato già, con la sottoscrizione hello dell'account di archiviazione, nonché con sottoscrizione hello di servizi di ripristino dell'insieme di credenziali tooenable reporting dati tooflow toohello account di archiviazione. toodo hello stesso, è necessario passare portale tooAzure > sottoscrizione > provider di risorse e cercare tooregister questo provider è. 

## <a name="configure-storage-account-for-reports"></a>Configurare l'account di archiviazione per i report
Utilizzare hello seguente account di archiviazione hello tooconfigure passaggi per l'insieme di credenziali di recovery services tramite il portale di Azure. Si tratta di una configurazione unica e dopo aver configurato l'account di archiviazione, è possibile passare tooPower BI direttamente sfruttare e tooview pacchetto di contenuto dei report.
1. Se è già aperto un insieme di credenziali di servizi di ripristino, eseguire il passaggio di toonext. Se non è aperto un insieme di credenziali di servizi di ripristino, ma nel portale di Azure, nel menu Hub hello hello fare clic su **Sfoglia**.

   * Nell'elenco di hello delle risorse, digitare **servizi di ripristino**.
   * Si inizia a digitare, hello filtri di elenco in base all'input. Quando viene visualizzata l'opzione, fare clic su **Insiemi di credenziali dei servizi di ripristino**.

      ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 1](./media/backup-azure-vms-encryption/browse-to-rs-vaults.png) <br/>

     viene visualizzato l'elenco di Hello degli insiemi di credenziali di servizi di ripristino. Hello l'elenco degli insiemi di credenziali di servizi di ripristino, selezionare un insieme di credenziali.

     Apre il dashboard di Hello insieme di credenziali selezionato.
2. Hello elenco di elementi visualizzato in insieme di credenziali, fare clic su **report Backup** in Monitoraggio e report sezione tooconfigure hello account di archiviazione per i report.

      ![Selezionare la voce di menu Backup Reports (Report di backup) - Passaggio 2](./media/backup-azure-configure-reports/backup-reports-settings.PNG)
3. Nel Pannello di hello i report di Backup, fare clic su **configura** pulsante. Si apre il pannello di Azure Application Insights hello viene utilizzato per l'inserimento di account di archiviazione di dati toocustomer.

      ![Configurare l'account di archiviazione - Passaggio 3](./media/backup-azure-configure-reports/configure-storage-account.PNG)
4. Impostare il pulsante Attiva/disattiva stato hello troppo**su** e selezionare **archiviare tooa Account di archiviazione** casella di controllo in modo che i dati è possono avviare il flusso nell'account di archiviazione toohello di reporting.

      ![Abilitare la diagnostica - Passaggio 4](./media/backup-azure-configure-reports/set-status-on.png)
5. Fare clic su selezione Account di archiviazione e l'account di archiviazione hello selezionare dall'elenco di hello per l'archiviazione dei report di dati e fare clic su **OK**.

      ![Selezionare l'account di archiviazione - Passaggio 5](./media/backup-azure-configure-reports/select-storage-account.png)
6. Selezionare **AzureBackupReport** casella di controllo e spostare anche periodo di memorizzazione di tooselect hello dispositivo di scorrimento per l'oggetto dati di report. Reporting dati nell'account di archiviazione hello viene mantenuto per il periodo di hello selezionato con questo dispositivo di scorrimento.

      ![Selezionare l'account di archiviazione - Passaggio 6](./media/backup-azure-configure-reports/save-configuration.png)
7. Esaminare tutte le modifiche di hello e fare clic su **salvare** pulsante nella parte superiore, come illustrato nella figura hello precedente. Questa azione assicura che tutte le modifiche vengano salvate e che l'account di archiviazione sia ora configurato per l'archiviazione dei dati dei report.

> [!NOTE]
> Una volta configurato, i report tramite il salvataggio di account di archiviazione, è necessario **attendere 24 ore** per toocomplete push di dati iniziale. È consigliabile importare il pacchetto di contenuto di Backup di Azure in Power BI solo dopo tale intervallo. Per altri dettagli, vedere la [sezione delle domande frequenti](#frequently-asked-questions). 
>
>

## <a name="view-reports-in-power-bi"></a>Visualizzare i report in Power BI 
Dopo la configurazione dell'account di archiviazione per i report utilizzando credenziali di servizi di ripristino, sono necessari circa 24 ore per la segnalazione toostart dati trasmessi. Dopo 24 ore di configurazione dell'account di archiviazione, utilizzare hello seguenti passaggi viene tooview report in Power BI:
1. [Accedi](https://powerbi.microsoft.com/landing/signin/) tooPower BI.
2. Fare clic su **Recupera dati** e selezionare Recupera in **Servizi** nella libreria del pacchetto di contenuto. Utilizzare i passaggi indicati in [pacchetto di contenuto Power BI documentazione tooaccess](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-packs-services/).

     ![Importare il pacchetto di contenuto](./media/backup-azure-configure-reports/content-pack-import.png)
3. Digitare **Backup di Azure** nella barra di ricerca e fare clic su **Scarica adesso**.

      ![Ottenere il pacchetto di contenuto](./media/backup-azure-configure-reports/content-pack-get.png)
4. Immettere il nome di account di archiviazione hello configurato nel passaggio 5 riportato sopra e fare clic su **Avanti** pulsante.

    ![Immettere il nome dell'account di archiviazione](./media/backup-azure-configure-reports/content-pack-storage-account-name.png)    
5. Immettere una chiave di account di archiviazione di hello per questo account di archiviazione. È possibile [consente di visualizzare e copiare le chiavi di accesso di archiviazione](../storage/common/storage-create-storage-account.md#manage-your-storage-account) passando tooyour account di archiviazione nel portale di Azure. 

     ![Immettere l'account di archiviazione](./media/backup-azure-configure-reports/content-pack-storage-account-key.png) <br/>
     
6. Fare clic sul pulsante **Accedi**. Dopo aver eseguito l'accesso, viene visualizzata la notifica **Importazione di dati**.

    ![Importazione del pacchetto di contenuto](./media/backup-azure-configure-reports/content-pack-importing-data.png) <br/>
    
    In un secondo momento, si ottiene **successo** notifica al termine dell'importazione di hello. Potrebbe richiedere poco più tooimport hello pacchetto di contenuto, se è presente una grande quantità di dati nell'account di archiviazione hello.
    
    ![Importazione riuscita del pacchetto di contenuto](./media/backup-azure-configure-reports/content-pack-import-success.png) <br/>
    
7. Una volta che i dati vengono importati correttamente, **Azure Backup** è visibile nel pacchetto di contenuto **app** nel riquadro di spostamento hello. elenco Hello verrà visualizzato il dashboard di Azure Backup, report e set di dati con una stella gialla che indica un report appena importato. 

     ![Pacchetto di contenuto Backup di Azure](./media/backup-azure-configure-reports/content-pack-azure-backup.png) <br/>
     
8. Fare clic su **Backup di Azure** nel dashboard, che illustra un set di report con chiavi associate.

      ![Dashboard di Backup di Azure](./media/backup-azure-configure-reports/azure-backup-dashboard.png) <br/>
9. set completo di hello tooview di report, fare clic su tutti i report nel dashboard di hello.

      ![Integrità dei processi di Backup di Azure](./media/backup-azure-configure-reports/azure-backup-job-health.png) <br/>
10. Fare clic su ogni scheda tooview rapporti hello in tale area.

      ![Schede dei report di Backup di Azure](./media/backup-azure-configure-reports/reports-tab-view.png)


## <a name="frequently-asked-questions"></a>Domande frequenti
1. **Come controllare se è stato avviato segnalazione dei dati trasmessi toostorage account?**
    
    È possibile passare toohello storage account configurati e selezionare i contenitori. Se il contenitore di hello dispone di una voce per approfondimenti-log-azurebackupreport, indica che dei dati di report sono stato avviato il flusso.

2. **Che cos'è la frequenza di hello di account toostorage push di dati e di pacchetto di contenuto di Backup di Azure in Power BI?**

   Per gli utenti di 0 giorni, occorrere account toostorage dati toopush di circa 24 ore. Una volta Cannot questo push iniziale, i dati vengono aggiornati con hello seguente frequenza illustrata nella figura che segue hello. 
      * Dati correlati troppo**processi, avvisi, gli elementi di Backup, gli insiemi di credenziali, i server protetti e i criteri di** viene inserito l'account di archiviazione toocustomer come e quando viene registrato.
      * Dati correlati troppo**archiviazione** viene inserito account di archiviazione toocustomer ogni 24 ore.
   
    ![Frequenza del push di dati dei report di Backup di Azure](./media/backup-azure-configure-reports/reports-data-refresh-cycle.png)

  Power BI esegue un [aggiornamento pianificato una volta al giorno](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/#what-can-be-refreshed). È possibile eseguire un aggiornamento manuale dei dati di hello in Power BI per pacchetto di contenuto hello.

3. **Quanto tempo è possibile mantenere report hello?** 

   Quando si configura l'account di archiviazione, è possibile selezionare il periodo di memorizzazione dei dati report nell'account di archiviazione hello (mediante il passaggio 6 Configura account di archiviazione per sezione report precedente). È anche possibile [analizzare i report in Excel](https://powerbi.microsoft.com/documentation/powerbi-service-analyze-in-excel/) e salvarli per un periodo di conservazione più lungo, in base alle esigenze. 

4. **Visualizzeranno tutti i dati del report dopo aver configurato l'account di archiviazione hello?**

   Tutti i dati generati dopo di hello **"configurazione di account di archiviazione"** avverranno toohello account di archiviazione e sarà disponibile nei report. Tuttavia, **i processi in corso non vengono sottoposti a push** per la creazione dei report. Una volta processo hello viene completata o non riesce, viene inviato tooreports.

5. **Se i report tooview account di archiviazione hello ho già configurato, è possibile modificare hello configurazione toouse un altro account di archiviazione?** 

   Sì, è possibile modificare l'account di archiviazione diverso tooa toopoint configurazione hello. È consigliabile utilizzare account di archiviazione hello appena configurato durante la connessione tooAzure pacchetto di contenuto di Backup. Dopo aver configurato un account di archiviazione diverso, i nuovi dati verranno trasferiti in questo account di archiviazione. Ma i dati meno recenti (prima della modifica della configurazione di hello) saranno comunque nell'account di archiviazione precedente hello.

6. **È possibile visualizzare i report negli insiemi di credenziali e nelle sottoscrizioni?** 

   Sì, è possibile configurare hello stesso account di archiviazione tra diversi insiemi di credenziali di report insieme di credenziali tra tooview. Inoltre, è possibile configurare hello stesso account di archiviazione per gli insiemi di credenziali per le sottoscrizioni. È quindi possibile utilizzare questo account di archiviazione durante la connessione tooAzure Backup pacchetto di contenuto report di Power BI tooview hello. Tuttavia, in cui deve essere selezionato l'account di archiviazione hello in hello ripristino stessa area dell'insieme di credenziali dei servizi.
   
## <a name="next-steps"></a>Passaggi successivi
Ora che è stato configurato l'account di archiviazione hello e importato pacchetto di contenuto di Backup di Azure, passaggio successivo hello è toocustomize questi report e utilizzare report toocreate modello di dati di reporting. Hello seguenti articoli per ulteriori informazioni, vedere.

* [Utilizzo del modello dati di Backup di Azure](backup-azure-reports-data-model.md)
* [Filtraggio dei report in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-about-filters-and-highlighting-in-reports/)
* [Creazione dei report in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-create-a-new-report/)

