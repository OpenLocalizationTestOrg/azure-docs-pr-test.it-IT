---
title: Copiare i dati locali tramite lo strumento Copia dati di Azure | Microsoft Docs
description: Creare una data factory di Azure e quindi usare lo strumento Copia dati per copiare i dati da un database SQL Server locale all'archivio BLOB di Azure.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.topic: hero-article
ms.date: 01/04/2018
ms.author: jingwang
ms.openlocfilehash: aba8b13d47b2b9236a0d5cc868e53780e894c406
ms.sourcegitcommit: f1c1789f2f2502d683afaf5a2f46cc548c0dea50
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2018
---
# <a name="copy-data-from-an-on-premises-sql-server-database-to-azure-blob-storage-by-using-copy-data-tool"></a>Copiare dati da un database SQL Server locale all'archivio BLOB di Azure usando lo strumento Copia dati
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Versione 1 - Disponibilità generale](v1/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Versione 2 - Anteprima](tutorial-hybrid-copy-data-tool.md)

In questa esercitazione si usa il portale di Azure per creare una data factory. Si userà quindi lo strumento Copia dati per creare una pipeline che copia i dati da un database SQL Server locale a un archivio BLOB di Azure.

> [!NOTE]
> - Se non si ha familiarità con Azure Data Factory, vedere [Introduzione ad Azure Data Factory](introduction.md).
>
> - Questo articolo si applica alla versione 2 del servizio Data Factory, attualmente in versione di anteprima. Se si usa la versione 1 del servizio Data Factory, disponibile a livello generale, vedere l'[introduzione a Data Factory versione 1](v1/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

In questa esercitazione vengono completati i passaggi seguenti:

> [!div class="checklist"]
> * Creare una data factory.
> * Usare lo strumento Copia dati per creare una pipeline
> * Monitorare le esecuzioni di pipeline e attività.

## <a name="prerequisites"></a>prerequisiti
### <a name="azure-subscription"></a>Sottoscrizione di Azure
Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/) prima di iniziare.

### <a name="azure-roles"></a>Ruoli di Azure
Per creare istanze di Data Factory, all'account utente usato per accedere ad Azure deve essere assegnato un ruolo *collaboratore* o *proprietario* oppure l'account deve essere un *amministratore* della sottoscrizione di Azure. 

Per visualizzare le autorizzazioni disponibili nella sottoscrizione, passare al portale di Azure, selezionare il nome utente nell'angolo in alto a destra e quindi **Autorizzazioni**. Se si accede a più sottoscrizioni, selezionare quella appropriata. Per istruzioni di esempio sull'aggiunta di un utente a un ruolo, vedere l'articolo [Aggiungere i ruoli](../billing/billing-add-change-azure-subscription-administrator.md).

### <a name="sql-server-2014-2016-and-2017"></a>SQL Server 2014, 2016 e 2017
In questa esercitazione si usa un database di SQL Server locale come archivio dati di *origine*. La pipeline nella data factory creata in questa esercitazione copia i dati da questo database di SQL Server locale (origine) all'archivio BLOB di Azure (sink). Si crea quindi una tabella denominata **emp** nel database di SQL Server e inserire una coppia di voci di esempio nella tabella. 

1. Avviare SQL Server Management Studio. Se non è già installato nel computer, passare a [Scaricare SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms). 

2. Connettersi all'istanza di SQL Server usando le credenziali. 

3. Creare un database di esempio. Nella visualizzazione struttura ad albero fare clic con il pulsante destro del mouse su **Database** e scegliere **Nuovo database**. 
 
4. Nella finestra **Nuovo database** immettere un nome per il database e fare clic su **OK**. 

5. Per creare la tabella **emp** e inserirvi alcuni dati di esempio, eseguire questo script di query sul database. Nella visualizzazione struttura ad albero fare clic con il pulsante destro del mouse sul database creato e scegliere **Nuova query**.

    ```sql
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50)
    )
    GO
    
    INSERT INTO emp (FirstName, LastName) VALUES ('John', 'Doe')
    INSERT INTO emp (FirstName, LastName) VALUES ('Jane', 'Doe')
    GO
    ```

### <a name="azure-storage-account"></a>Account di archiviazione di Azure
In questa esercitazione si usa un account di archiviazione di Azure per utilizzo generico (specificamente, un archivio BLOB) come archivio dati di destinazione/sink. Se non si ha un account di archiviazione di Azure per utilizzo generico, vedere [Creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account) per istruzioni su come crearne uno. La pipeline nella data factory creata in questa esercitazione copia i dati dal database di SQL Server locale (origine) a questo archivio BLOB di Azure (sink). 

#### <a name="get-storage-account-name-and-account-key"></a>Recuperare il nome e la chiave dell'account di archiviazione
In questa esercitazione si usano il nome e la chiave dell'account di archiviazione di Azure. Recuperare il nome e la chiave dell'account di archiviazione seguendo questa procedura: 

1. Accedere al [portale di Azure](https://portal.azure.com) con nome utente e password. 

2. Nel riquadro a sinistra selezionare **Altri servizi**, usare la parola chiave **Archiviazione** come filtro e selezionare **Account di archiviazione**.

    ![Cercare l'account di archiviazione](media/tutorial-hybrid-copy-powershell/search-storage-account.png)

3. Nell'elenco degli account di archiviazione filtrare, se necessario, e quindi selezionare il proprio account di archiviazione. 

4. Nella finestra **Account di archiviazione** selezionare **Chiavi di accesso**.

    ![Recuperare il nome e la chiave dell'account di archiviazione](media/tutorial-hybrid-copy-powershell/storage-account-name-key.png)

5. Nelle caselle **Nome account di archiviazione** e **key1** copiare i valori e incollarli nel Blocco note o in un altro editor per usarli in seguito nell'esercitazione. 

#### <a name="create-the-adftutorial-container"></a>Creare il contenitore adftutorial 
In questa sezione si crea un contenitore BLOB denominato **adftutorial** nell'archivio BLOB di Azure. 

1. Nella finestra **Account di archiviazione** passare a **Panoramica** e quindi selezionare **BLOB**. 

    ![Selezionare l'opzione BLOB](media/tutorial-hybrid-copy-powershell/select-blobs.png)

2. Nella finestra **Servizio BLOB** selezionare **Contenitore**. 

    ![Pulsante Aggiungi contenitore](media/tutorial-hybrid-copy-powershell/add-container-button.png)

3. Nella finestra di dialogo **Nuovo contenitore** immettere **adftutorial** nella casella **Nome** e fare clic su **OK**. 

    ![Immettere il nome del contenitore](media/tutorial-hybrid-copy-powershell/new-container-dialog.png)

4. Selezionare **adftutorial** nell'elenco di contenitori.  

    ![Selezionare il contenitore](media/tutorial-hybrid-copy-powershell/seelct-adftutorial-container.png)

5. Tenere aperta la finestra **Contenitore** per **adftutorial**. perché verrà usata per verificare l'output alla fine di questa esercitazione. Data Factory crea automaticamente la cartella di output in questo contenitore, quindi non è necessario crearne uno.

    ![Finestra Contenitore](media/tutorial-hybrid-copy-powershell/container-page.png)


## <a name="create-a-data-factory"></a>Creare un'istanza di Data factory

1. Scegliere **Nuovo** dal menu a sinistra, fare clic su **Dati e analisi** e quindi fare clic su **Data factory**. 
   
   ![Nuovo->DataFactory](./media/tutorial-hybrid-copy-data-tool/new-azure-data-factory-menu.png)
2. Nella pagina **Nuova data factory** immettere **ADFTutorialDataFactory** per **Nome**. 
      
     ![Pagina Nuova data factory](./media/tutorial-hybrid-copy-data-tool/new-azure-data-factory.png)
 
   Il nome della data factory di Azure deve essere **univoco a livello globale**. Se viene visualizzato l'errore seguente per il campo Nome, modificare il nome della data factory, ad esempio nomeutenteADFTutorialDataFactory. Per informazioni sulle regole di denominazione per gli elementi di Data Factory, vedere l'articolo [Data Factory - Regole di denominazione](naming-rules.md).
  
     ![Pagina Nuova data factory](./media/tutorial-hybrid-copy-data-tool/name-not-available-error.png)
3. Selezionare la **sottoscrizione** di Azure in cui creare la data factory. 
4. Per il **gruppo di risorse**, eseguire una di queste operazioni:
     
      - Selezionare **Usa esistente**e scegliere un gruppo di risorse esistente dall'elenco a discesa. 
      - Selezionare **Crea nuovo**e immettere un nome per il gruppo di risorse.   
         
      Per informazioni sui gruppi di risorse, vedere l'articolo relativo all' [uso di gruppi di risorse per la gestione delle risorse di Azure](../azure-resource-manager/resource-group-overview.md).  
4. Selezionare **V2 (anteprima)** per **Versione**.
5. Selezionare la **località** per la data factory. Nell'elenco a discesa vengono mostrate solo le località supportate. Gli archivi dati (Archiviazione di Azure, database SQL di Azure e così via) e le risorse di calcolo (HDInsight e così via) usati dalla data factory possono trovarsi in altre località/aree.
6. Selezionare **Aggiungi al dashboard**.     
7. Fare clic su **Crea**.
8. Nel dashboard viene visualizzato il riquadro seguente con lo stato: **Deploying data factory** (Distribuzione della data factory). 

    ![Riquadro Deploying data factory (Distribuzione della data factory)](media/tutorial-hybrid-copy-data-tool/deploying-data-factory.png)
9. Al termine della creazione verrà visualizzata la pagina **Data factory**, come illustrato nell'immagine.
   
   ![Home page di Data factory](./media/tutorial-hybrid-copy-data-tool/data-factory-home-page.png)
10. Fare clic sul riquadro **Crea e monitora** per avviare l'interfaccia utente di Azure Data Factory in una scheda separata. 

## <a name="use-copy-data-tool-to-create-a-pipeline"></a>Usare lo strumento Copia dati per creare una pipeline

1. Nella pagina delle attività iniziali fare clic sul riquadro **Copia dati** per avviare lo strumento Copia dati. 

   ![Riquadro dello strumento Copia dati](./media/tutorial-hybrid-copy-data-tool/copy-data-tool-tile.png)
2. Nella pagina **Proprietà** dello strumento Copia dati specificare **CopyFromOnPremSqlToAzureBlobPipeline** per **Nome attività**, quindi fare clic su **Avanti**. Lo strumento Copia dati crea una pipeline con il nome specificato per questo campo. 
    
   ![Pagina Proprietà](./media/tutorial-hybrid-copy-data-tool/properties-page.png)
3. Nella pagina **Archivio dati di origine** selezionare **SQL Server** e fare clic su **Avanti**. Potrebbe essere necessario scorrere verso il basso per visualizzare **SQL Server** nell'elenco. 

   ![Pagina Archivio dati di origine](./media/tutorial-hybrid-copy-data-tool/select-source-data-store.png)
4. Immettere **SqlServerLinkedService** per **Connection name** (Nome connessione) e fare clic sul collegamento **Create Integration Runtime** (Crea runtime di integrazione). Per creare un runtime di integrazione self-hosted scaricarlo nel computer e registrarlo con il servizio Data Factory. Il runtime di integrazione self-hosted copia i dati tra l'ambiente locale e il cloud di Azure.

   ![Collegamento Create Integration Runtime (Crea runtime di integrazione)](./media/tutorial-hybrid-copy-data-tool/create-integration-runtime-link.png)
5. Nella finestra di dialogo **Create Integration Runtime** (Crea runtime di integrazione) immettere **TutorialIntegration Runtime** per il campo **Name** (Nome) e fare clic su **Create** (Crea). 

   ![Finestra di dialogo Create Integration Runtime (Crea runtime di integrazione)](./media/tutorial-hybrid-copy-data-tool/create-integration-runtime-dialog.png)
6. Fare clic su **Launch express setup on this computer** (Avvia installazione rapida sul computer). Questa azione installa il runtime di integrazione nel computer e lo registra con il servizio Data Factory. In alternativa è possibile usare l'opzione di installazione manuale per scaricare il file di installazione, eseguirlo e usare la chiave per registrare il runtime di integrazione. 

    ![Collegamento Create Integration Runtime (Crea runtime di integrazione)](./media/tutorial-hybrid-copy-data-tool/launch-express-setup-link.png)
7. Eseguire l'applicazione scaricata. In questa finestra viene visualizzato lo **stato** dell'installazione rapida. 

    ![Stato dell'installazione rapida](./media/tutorial-hybrid-copy-data-tool/express-setup-status.png)
8. Verificare che sia selezionato **TutorialIntegrationRuntime** per il campo **Integration Runtime** (Runtime di integrazione).

    ![Runtime di integrazione selezionato](./media/tutorial-hybrid-copy-data-tool/integration-runtime-selected.png)
9. In **Specify the on-premises SQL Server database** (Specificare il database SQL Server locale) seguire questa procedura: 

    1. Immettere **OnPremSqlLinkedService** per **Nome connessione**.
    2. Immettere il nome dell'istanza di SQL Server locale per **Nome server**.
    3. Immettere il nome del database locale per **Nome database**. 
    4. Impostare l'autenticazione appropriata per **Tipo di autenticazione**.
    5. Immettere il nome dell'utente con accesso all'istanza di SQL Server locale per **Nome utente**.
    6. Immettere la **password** dell'utente. 
10. Nella pagina **Select tables from which to copy the data or use a custom query** (Selezionare le tabelle dalle quali copiare i dati oppure usare una query personalizzata), selezionare la tabella **[dbo].[emp]** nell'elenco e fare clic su **Avanti**. 

    ![Selezionare la tabella emp](./media/tutorial-hybrid-copy-data-tool/select-emp-table.png)
11. Nella pagina **Destination data store** (Archivio dati di destinazione) selezionare **Archivio BLOB di Azure** e quindi fare clic su **Avanti**.

    ![Selezionare Archiviazione BLOB di Azure](./media/tutorial-hybrid-copy-data-tool/select-destination-data-store.png)
12. Nella pagina **Specify the Azure Blob storage account** (Specificare l'account di archiviazione BLOB di Azure) seguire questa procedura: 

    1. Immettere **AzureStorageLinkedService** per **Nome connessione**.
    2. Selezionare il proprio account di archiviazione di Azure dall'elenco a discesa **Nome account di archiviazione**. 
    3. Fare clic su **Avanti**.

        ![Selezionare Archiviazione BLOB di Azure](./media/tutorial-hybrid-copy-data-tool/specify-azure-blob-storage-account.png)
13. Nella pagina **Choose the output file or folder** (Scegliere il file o la cartella di output) seguire questa procedura: 
    
    1. Immettere **adftutorial/fromonprem** per **Percorso cartella**. Come parte dei prerequisiti è stato creato il contenitore **adftutorial**. Se la cartella output non esiste, il servizio Data Factory la crea automaticamente. È anche possibile usare il pulsante **Sfoglia** per passare all'archivio BLOB e ai relativi contenitori/cartelle. Si noti che il nome del file di output è **dbo.emp** per impostazione predefinita.
        
        ![Scegliere il file o la cartella di output](./media/tutorial-hybrid-copy-data-tool/choose-output-file-folder.png)
14. Nella pagina **File format settings** (Impostazioni di formato file) fare clic su **Avanti**. 

    ![Pagina di impostazioni del formato del file](./media/tutorial-hybrid-copy-data-tool/file-format-settings-page.png)
15. Nella pagina **Impostazioni** fare clic su **Avanti**. 

    ![Pagina Impostazioni](./media/tutorial-hybrid-copy-data-tool/settings-page.png)
16. Nella pagina **Riepilogo** esaminare i valori di tutte le impostazioni e fare clic su **Avanti**. 

    ![Pagina Riepilogo](./media/tutorial-hybrid-copy-data-tool/summary-page.png)
17. Nella pagina **Distribuzione** fare clic su **Monitoraggio** per monitorare la pipeline o l'attività creata.

    ![Pagina Distribuzione](./media/tutorial-hybrid-copy-data-tool/deployment-page.png)
18. Nella scheda **Monitoraggio** è possibile visualizzare lo stato della pipeline creata. I collegamenti nella colonna **Azione** consentono di visualizzare le esecuzioni di attività associate all'esecuzione della pipeline e di eseguire di nuovo la pipeline. 

    ![Esecuzioni di pipeline](./media/tutorial-hybrid-copy-data-tool/monitor-pipeline-runs.png)
19. Fare clic sul collegamento **View Activity Runs** (Visualizza le esecuzioni di attività) nella colonna **Azioni** per visualizzare le esecuzioni di attività associate all'esecuzione della pipeline. Per informazioni dettagliate sull'operazione di copia, fare clic sul collegamento **Dettagli** (icona degli occhiali) nella colonna **Azioni**. È possibile tornare alla visualizzazione delle esecuzioni della pipeline facendo clic su **Pipeline** in alto.

    ![Esecuzioni attività](./media/tutorial-hybrid-copy-data-tool/monitor-activity-runs.png)
20. Assicurarsi che venga visualizzato il file di output nella cartella **fromonprem** del contenitore **adftutorial**.   
 
    ![Blob di output](./media/tutorial-hybrid-copy-data-tool/output-blob.png)
21. Fare clic sulla scheda **Modifica** a sinistra per passare alla modalità di modifica. L'editor consente di aggiornare i servizi collegati, i set di dati e le pipeline creati dallo strumento. Fare clic su **Codice** per visualizzare il codice JSON associato all'entità aperta nell'editor. Per informazioni dettagliate sulla modifica di queste entità nell'interfaccia utente di Data Factory, vedere [la versione del portale di Azure di questa esercitazione](tutorial-copy-data-portal.md).

    ![Scheda Modifica](./media/tutorial-hybrid-copy-data-tool/edit-tab.png)


## <a name="next-steps"></a>Passaggi successivi
La pipeline in questo esempio copia i dati da un database di SQL Server locale a un archivio BLOB di Azure. Si è appreso come: 

> [!div class="checklist"]
> * Creare una data factory.
> * Usare lo strumento Copia dati per creare una pipeline
> * Monitorare le esecuzioni di pipeline e attività.

Per un elenco degli archivi dati supportati da Data Factory, vedere gli [archivi dati supportati](copy-activity-overview.md#supported-data-stores-and-formats).

Passare all'esercitazione successiva per ottenere informazioni sulla copia di dati in blocco da un'origine a una destinazione:

> [!div class="nextstepaction"]
>[Copiare i dati nel bulk](tutorial-bulk-copy-portal.md)