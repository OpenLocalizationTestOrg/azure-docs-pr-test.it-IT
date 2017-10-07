---
title: "Esercitazione: Creare una pipeline con l'attività di copia usando Visual Studio | Documentazione Microsoft"
description: "In questa esercitazione viene creata una pipeline di Azure Data Factory con un'attività di copia usando Visual Studio."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1751185b-ce0a-4ab2-a9c3-e37b4d149ca3
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: d99d8875807bab41f5122ab95a09f83f82923529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-visual-studio"></a>Esercitazione: Creare una pipeline con l’attività Copia utilizzando Visual Studio
> [!div class="op_single_selector"]
> * [Panoramica e prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Copia guidata](data-factory-copy-data-wizard-tutorial.md)
> * [Portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Modello di Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [API REST](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

In questo articolo viene illustrato come toouse hello Microsoft Visual Studio toocreate una data factory con una pipeline che copia i dati da un database di SQL Azure tooan di archiviazione blob di Azure. Se si tooAzure nuova Data Factory, leggere hello [tooAzure introduzione Data Factory](data-factory-introduction.md) articolo prima di eseguire questa esercitazione.   

In questa esercitazione si crea una pipeline contenente una sola attività: un'attività di copia attività di copia Hello copia dati da un archivio dati di sink supportati tooa di archivio di dati supportati. Per un elenco degli archivi dati supportati come origini e sink, vedere gli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats). attività Hello è alimentato da un servizio disponibile a livello globale che è possibile copiare dati tra diversi archivi dati in modo sicuro, affidabile e scalabile. Per ulteriori informazioni sulle attività di copia hello, vedere [attività lo spostamento dei dati](data-factory-data-movement-activities.md).

Una pipeline può includere più attività Inoltre, è possibile concatenare le due attività (eseguire un'attività dopo l'altro) mediante l'impostazione di set di dati di hello output di un'attività come hello input set di dati di hello altre attività. Per altre informazioni, vedere [Attività multiple in una pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

> [!NOTE] 
> pipeline di dati Hello in questa esercitazione consente di copiare dati da un archivio dati di origine dati archivio tooa destinazione. Per un'esercitazione su come dati di tootransform tramite Data Factory di Azure, vedere [esercitazione: creare una pipeline di dati tootransform utilizzando cluster Hadoop](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Prerequisiti
1. Leggere [esercitazione Panoramica](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) articolo e hello completo **prerequisito** passaggi.       
2. le istanze di Data Factory toocreate, è necessario essere un membro di hello [Data Factory collaboratore](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) ruolo a livello di gruppo di risorse di sottoscrizione/hello.
3. È necessario disporre delle seguenti hello installato nel computer: 
   * Visual Studio 2013 o Visual Studio 2015
   * Download di Azure SDK per Visual Studio 2013 o Visual Studio 2015. Passare troppo[pagina di Download di Azure](https://azure.microsoft.com/downloads/) e fare clic su **VS 2013** o **Visual Studio 2015** in hello **.NET** sezione.
   * Scaricare hello plug-in Data Factory di Azure più recenti per Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) o [Visual Studio 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005). È inoltre possibile aggiornare i plug-in hello effettuando hello alla procedura seguente: hello scegliere **strumenti** -> **estensioni e aggiornamenti** -> **Online**  ->  **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools per Visual Studio** -> **aggiornamento**.

## <a name="steps"></a>Passi
Ecco i passaggi di hello che è eseguire come parte di questa esercitazione:

1. Creare **servizi collegati** nella data factory di hello. In questo passaggio si creano due servizi collegati di tipo Archiviazione di Azure e database SQL di Azure. 
    
    Hello AzureStorageLinkedService collega la data factory toohello account di archiviazione di Azure. È stato creato un contenitore e caricare l'account di archiviazione di dati toothis come parte di [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

    AzureSqlLinkedService collega il toohello data factory di Azure SQL database. dati Hello che viene copiati dall'archiviazione blob hello vengono archiviati nel database. Come parte dei [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) è stata creata una tabella SQL in questo database.     
2. Creazione di input e output **set di dati** nella data factory di hello.  
    
    il servizio di archiviazione di Azure collegati Hello specifica hello stringa di connessione del servizio Data Factory utilizzata in fase di esecuzione tooconnect tooyour account di archiviazione di Azure. E specifica di set di dati blob di input hello hello contenitore e della cartella di hello che contiene i dati di input hello.  

    Analogamente, hello servizio Database SQL di Azure collegati specifica hello stringa di connessione del servizio Data Factory utilizzata nel database di SQL Azure tooyour tooconnect fase di esecuzione. E specifica di set di dati nella tabella SQL output hello tabella hello nei dati di hello database toowhich hello dall'archiviazione blob hello viene copiata.
3. Creare un **pipeline** nella data factory di hello. In questo passaggio viene creata una pipeline con un'attività di copia.   
    
    attività di copia Hello copia dati da un blob nella tabella tooa di archiviazione blob di Azure hello in database SQL di Azure hello. È possibile utilizzare un'attività di copia in una pipeline di dati da qualsiasi destinazione tooany supportato di origine supportata toocopy. Per un elenco degli archivi dati supportati, vedere l'articolo sulle [attività di spostamento dei dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats). 
4. Creare una **data factory** di Azure durante la distribuzione delle entità di Data Factory (servizi collegati, set di dati/tabelle e pipeline). 

## <a name="create-visual-studio-project"></a>Creare un progetto di Visual Studio
1. Avviare **Visual Studio 2015**. Fare clic su **File**, punto troppo**New**, fare clic su **progetto**. Dovrebbe essere hello **nuovo progetto** la finestra di dialogo.  
2. In hello **nuovo progetto** finestra di dialogo, seleziona hello **DataFactory** modello e fare clic su **progetto vuoto di Factory dati**.  
   
    ![Finestra di dialogo Nuovo progetto](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-project-dialog.png)
3. Specificare nome hello del progetto di hello, percorso per la soluzione hello e nome della soluzione hello e quindi fare clic su **OK**.
   
    ![Esplora soluzioni](./media/data-factory-copy-activity-tutorial-using-visual-studio/solution-explorer.png)    

## <a name="create-linked-services"></a>Creare servizi collegati
Creare servizi collegati in un toolink factory dati i dati vengono archiviati e toohello data factory di servizi di calcolo. In questa esercitazione non si usano servizi di calcolo come Azure HDInsight o Azure Data Lake Analytics, ma due archivi dati di tipo Archiviazione di Azure (origine) e database SQL di Azure (destinazione). 

Di conseguenza, si creano due servizi collegati di tipo AzureStorage e AzureSqlDatabase.  

Archiviazione di Azure Hello collegato collegamenti al servizio la data factory toohello account di archiviazione di Azure. Questo account di archiviazione è hello uno in cui è stato creato un contenitore e caricato dati hello come parte del [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

Collegato SQL Azure collegamenti al servizio il toohello data factory di Azure SQL database. dati Hello che viene copiati dall'archiviazione blob hello vengono archiviati nel database. Tabella emp hello è stato creato in questo database come parte di [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

Servizi collegati collegano archivi dati o servizi tooan data factory di Azure di calcolo. Vedere [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) per tutti hello origini e sink supportati dall'attività di copia hello. Vedere [servizi collegati di calcolo](data-factory-compute-linked-services.md) per elenco hello di servizi di calcolo supportati da Data Factory. Questa esercitazione non prevede l'uso di servizi di calcolo. 

### <a name="create-hello-azure-storage-linked-service"></a>Creare il servizio di archiviazione di Azure collegati hello
1. In **Esplora**, fare doppio clic su **servizi collegati**, punto troppo**Aggiungi**, fare clic su **nuovo elemento**.      
2. In hello **Aggiungi nuovo elemento** nella finestra di dialogo **servizio collegato di archiviazione di Azure** hello elenco e fare clic su **Aggiungi**. 
   
    ![Nuovo servizio collegato](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-linked-service-dialog.png)
3. Sostituire `<accountname>` e `<accountkey>`* con il nome di hello dell'account di archiviazione Azure e la relativa chiave. 
   
    ![Servizio collegato Archiviazione di Azure](./media/data-factory-copy-activity-tutorial-using-visual-studio/azure-storage-linked-service.png)
4. Salvare hello **AzureStorageLinkedService1.json** file.

    Per ulteriori informazioni sulle proprietà JSON nella definizione di servizio collegato hello, vedere [connettore di archiviazione Blob di Azure](data-factory-azure-blob-connector.md#linked-service-properties) articolo.

### <a name="create-hello-azure-sql-linked-service"></a>Creare servizio collegato SQL Azure hello
1. Fare clic su **servizi collegati** nodo hello **Esplora** nuovamente, scegliere troppo**Aggiungi**, fare clic su **nuovo elemento**. 
2. Questa volta selezionare **Servizio collegato SQL Azure** e fare clic su **Aggiungi**. 
3. In hello **AzureSqlLinkedService1.json file**, sostituire `<servername>`, `<databasename>`, `<username@servername>`, e `<password>` con nomi del server SQL Azure, database, account utente e password.    
4. Salvare hello **AzureSqlLinkedService1.json** file. 
    
    Per altre informazioni su queste proprietà JSON, vedere l'articolo relativo al [connettore del database SQL di Azure](data-factory-azure-sql-connector.md#linked-service-properties).


## <a name="create-datasets"></a>Creare set di dati
Nel passaggio precedente hello, servizi collegati toolink è creato l'account di archiviazione di Azure e la data factory di Azure SQL database tooyour. In questo passaggio si definiscono due set di dati denominati InputDataset e OutputDataset che rappresentano l'input e output i dati archiviati in archivi dati hello a cui fa riferimento AzureStorageLinkedService1 e AzureSqlLinkedService1 rispettivamente.

il servizio di archiviazione di Azure collegati Hello specifica hello stringa di connessione del servizio Data Factory utilizzata in fase di esecuzione tooconnect tooyour account di archiviazione di Azure. E, set di dati blob di input hello (InputDataset) specifica il contenitore di hello e la cartella di hello che contiene i dati di input hello.  

Analogamente, hello servizio Database SQL di Azure collegati specifica hello stringa di connessione del servizio Data Factory utilizzata nel database di SQL Azure tooyour tooconnect fase di esecuzione. E, di output di hello set di dati nella tabella SQL (OututDataset) specifica la tabella hello in hello di toowhich hello database vengono copiati dati dall'archiviazione blob hello. 

### <a name="create-input-dataset"></a>Creare set di dati di input
In questo passaggio, creare un set di dati denominato InputDataset che punta il file di blob tooa (emp.txt) nella cartella radice hello di un contenitore di blob (adftutorial) in hello rappresentato da hello AzureStorageLinkedService1 collegato servizio di archiviazione di Azure. Se non specifica un valore per il nome file hello (o ignorarlo), i dati da tutti i BLOB nella cartella input hello sono copiati toohello destinazione. In questa esercitazione, si specifica un valore per il nome file hello. 

In questo caso, utilizzare il termine hello "tables" anziché "set di dati". Una tabella è un set di dati rettangolare e hello solo i set di dati al momento è supportato. 

1. Fare doppio clic su **tabelle** in hello **Esplora**, punto troppo**Aggiungi**, fare clic su **nuovo elemento**.
2. In hello **Aggiungi nuovo elemento** nella finestra di dialogo **Blob di Azure**, fare clic su **Aggiungi**.   
3. Sostituire il testo JSON hello con hello segue testo e salvare hello **AzureBlobLocation1.json** file. 

  ```json   
  {
    "name": "InputDataset",
    "properties": {
      "structure": [
        {
          "name": "FirstName",
          "type": "String"
        },
        {
          "name": "LastName",
          "type": "String"
        }
      ],
      "type": "AzureBlob",
      "linkedServiceName": "AzureStorageLinkedService1",
      "typeProperties": {
        "folderPath": "adftutorial/",
        "format": {
          "type": "TextFormat",
          "columnDelimiter": ","
        }
      },
      "external": true,
      "availability": {
        "frequency": "Hour",
        "interval": 1
      }
    }
  }
  ``` 
    Hello nella tabella seguente vengono fornite descrizioni per le proprietà JSON hello utilizzate nel frammento di codice hello:

    | Proprietà | Descrizione |
    |:--- |:--- |
    | type | proprietà tipo Hello è troppo**AzureBlob** perché i dati risiedono in una risorsa di archiviazione blob di Azure. |
    | linkedServiceName | Fa riferimento toohello **AzureStorageLinkedService** creato in precedenza. |
    | folderPath | Specifica il blob hello **contenitore** hello e **cartella** che contiene il BLOB di input. In questa esercitazione, adftutorial è il contenitore di blob hello e cartella è hello radice. | 
    | fileName | Questa proprietà è facoltativa. Se si omette questa proprietà, vengono selezionati tutti i file da folderPath hello. In questa esercitazione, **emp.txt** specificato per hello fileName, in modo che solo tale file viene prelevato per l'elaborazione. |
    | format -> type |file di input di Hello è in formato testo hello, permette di usare **TextFormat**. |
    | columnDelimiter | Hello colonne nel file di input hello sono delimitate da **carattere virgola (`,`)**. |
    | frequenza/intervallo | frequenza Hello è troppo**ora** e l'intervallo viene impostato troppo**1**, il che significa che hello di input sono disponibili sezioni **oraria**. In altre parole, hello servizio Data Factory esegue la ricerca di dati di input ogni ora nella cartella radice hello del contenitore di blob (**adftutorial**) specificato. La ricerca di dati hello all'interno di hello pipeline inizio e fine volte, non prima o dopo tali periodi.  |
    | external | Questa proprietà è impostata troppo**true** se dati hello non viene generati da questa pipeline. dati di input Hello in questa esercitazione sono nel file di emp.txt hello, che non viene generato da questa pipeline, è necessario impostare tootrue questa proprietà. |

    Per altre informazioni su queste proprietà JSON, vedere l'articolo relativo al [connettore BLOB di Azure](data-factory-azure-blob-connector.md#dataset-properties).   

### <a name="create-output-dataset"></a>Creare il set di dati di output
In questo passaggio si crea un set di dati di output denominato **OutputDataset**. Questo set di dati fa riferimento nella tabella SQL tooa nel database di SQL Azure hello rappresentato da **AzureSqlLinkedService1**. 

1. Fare doppio clic su **tabelle** in hello **Esplora** nuovamente, scegliere troppo**Aggiungi**, fare clic su **nuovo elemento**.
2. In hello **Aggiungi nuovo elemento** nella finestra di dialogo **SQL Azure**, fare clic su **Aggiungi**. 
3. Sostituire il testo JSON hello con hello JSON seguente e salvare hello **AzureSqlTableLocation1.json** file.

  ```json
    {
     "name": "OutputDataset",
     "properties": {
       "structure": [
         {
           "name": "FirstName",
           "type": "String"
         },
         {
           "name": "LastName",
           "type": "String"
         }
       ],
       "type": "AzureSqlTable",
       "linkedServiceName": "AzureSqlLinkedService1",
       "typeProperties": {
         "tableName": "emp"
       },
       "availability": {
         "frequency": "Hour",
         "interval": 1
       }
     }
    }
    ```
    Hello nella tabella seguente vengono fornite descrizioni per le proprietà JSON hello utilizzate nel frammento di codice hello:

    | Proprietà | Descrizione |
    |:--- |:--- |
    | type | proprietà tipo Hello è troppo**AzureSqlTable** perché dati tabella tooa copiato in un database SQL di Azure. |
    | linkedServiceName | Fa riferimento toohello **AzureSqlLinkedService** creato in precedenza. |
    | tableName | Hello specificato **tabella** toowhich hello dati vengono copiati. | 
    | frequenza/intervallo | Hello frequency è impostato troppo**ora** e l'intervallo è **1**, il che significa che vengono create le sezioni di output di hello **oraria** tra hello pipeline iniziale e finale volte, non prima o Dopo tali periodi.  |

    Sono presenti tre colonne: **ID**, **FirstName**, e **LastName** : nella tabella emp hello nel database di hello. ID è una colonna identity, pertanto è necessario solo toospecify **FirstName** e **LastName** qui.

    Per altre informazioni su queste proprietà JSON, vedere l'articolo relativo al [connettore SQL di Azure](data-factory-azure-sql-connector.md#dataset-properties).

## <a name="create-pipeline"></a>Creare una pipeline
In questo passaggio viene creata una pipeline con un'**attività di copia** che usa **InputDataset** come input e **OutputDataset** come output.

Set di dati di output è attualmente, quali unità hello pianificazione. In questa esercitazione, set di dati di output è tooproduce configurato una sezione di una volta all'ora. pipeline Hello dispone ora di inizio e ora di fine di un giorno separato, ovvero 24 ore. Pertanto, 24 sezioni del set di dati di output vengono generate dalla pipeline hello. 

1. Fare doppio clic su **pipeline** in hello **Esplora**, punto troppo**Aggiungi**, fare clic su **nuovo elemento**.  
2. Selezionare **copia dati Pipeline** in hello **Aggiungi nuovo elemento** la finestra di dialogo e fare clic su **Aggiungi**. 
3. Sostituire hello JSON con hello JSON seguente e salvare hello **CopyActivity1.json** file.

  ```json   
    {
     "name": "ADFTutorialPipeline",
     "properties": {
       "description": "Copy data from a blob tooAzure SQL table",
       "activities": [
         {
           "name": "CopyFromBlobToSQL",
           "type": "Copy",
           "inputs": [
             {
               "name": "InputDataset"
             }
           ],
           "outputs": [
             {
               "name": "OutputDataset"
             }
           ],
           "typeProperties": {
             "source": {
               "type": "BlobSource"
             },
             "sink": {
               "type": "SqlSink",
               "writeBatchSize": 10000,
               "writeBatchTimeout": "60:00:00"
             }
           },
           "Policy": {
             "concurrency": 1,
             "executionPriorityOrder": "NewestFirst",
             "style": "StartOfInterval",
             "retry": 0,
             "timeout": "01:00:00"
           }
         }
       ],
       "start": "2017-05-11T00:00:00Z",
       "end": "2017-05-12T00:00:00Z",
       "isPaused": false
     }
    }
    ```   
    - Nella sezione attività hello, è presente una sola attività il cui **tipo** è troppo**copia**. Per ulteriori informazioni sulle attività di copia hello, vedere [attività lo spostamento dei dati](data-factory-data-movement-activities.md). Nelle soluzioni Data Factory è anche possibile usare le [attività di trasformazione dei dati](data-factory-data-transformation-activities.md).
    - Input per attività hello è troppo**InputDataset** e di output per attività hello è troppo**OutputDataset**. 
    - In hello **typeProperties** sezione **BlobSource** è specificato come tipo di origine hello e **SqlSink** è specificato come tipo di sink hello. Per un elenco completo degli archivi di dati supportati dall'attività di copia hello come origini e sink, vedere [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats). toolearn sulla modalità di memorizzazione toouse dati specifici supportati come origine/sink, fare clic su collegamento hello nella tabella hello.  
     
    Sostituire il valore di hello di hello **avviare** proprietà con hello giorno corrente e **fine** valore con hello giorno successivo. È possibile specificare solo parte della data hello e Ignora parte dell'ora hello di hello data ora. Ad esempio, "2016-02-03", che equivale troppo "2016-02-03T00:00:00Z"
     
    Per la data e l'ora di inizio è necessario usare il [formato ISO](http://en.wikipedia.org/wiki/ISO_8601). ad esempio 2016-10-14T16:32:41Z. Hello **fine** è facoltativo, ma viene usata in questa esercitazione. 
     
    Se non specifica alcun valore per hello **fine** proprietà, viene calcolato come "**start + 48 ore**". specificare in modo indefinito, pipeline hello toorun **9999-09-09** come valore hello hello **fine** proprietà.
     
    In hello sopra riportato, sono presenti sezioni dati 24 come ogni sezione di dati viene prodotta ogni ora.

    Per le descrizioni delle proprietà JSON nella definizione di una pipeline, vedere l'articolo su come [creare pipeline](data-factory-create-pipelines.md). Per le descrizioni delle proprietà JSON nella definizione di un'attività di copia, vedere le [attività di spostamento dei dati](data-factory-data-movement-activities.md). Per le descrizioni delle proprietà JSON supportate da BlobSource, vedere l'articolo relativo al [connettore BLOB di Azure](data-factory-azure-blob-connector.md). Per le descrizioni delle proprietà JSON supportate da SqlSink, vedere l'articolo relativo al [connettore del database SQL di Azure](data-factory-azure-sql-connector.md).

## <a name="publishdeploy-data-factory-entities"></a>Pubblicare/Distribuire le entità della data factory
In questo passaggio vengono pubblicate le entità di Data Factory, ovvero i servizi collegati, i set di dati e la pipeline, create in precedenza. È inoltre possibile specificare il nome di hello di hello nuova data factory toobe creato toohold queste entità.  

1. Fare clic sul progetto in Esplora soluzioni hello e fare clic su **pubblica**. 
2. Se viene visualizzato **Accedi tooyour account Microsoft** nella finestra di dialogo immettere le credenziali di account hello con sottoscrizione di Azure e fare clic su **Accedi**.
3. È necessario visualizzare hello la finestra di dialogo seguenti:
   
   ![Finestra di dialogo Pubblica](./media/data-factory-copy-activity-tutorial-using-visual-studio/publish.png)
4. Nella pagina di fabbrica dati Configura hello, hello i passaggi seguenti: 
   
   1. Selezionare l’opzione **Crea nuova data factory** .
   2. Immettere **VSTutorialFactory** per **Nome**.  
      
      > [!IMPORTANT]
      > nome Hello di hello Azure data factory deve essere globalmente univoco. Se si riceve un errore relativo a nome hello della data factory per la pubblicazione, è possibile modificare il nome di hello di hello data factory (ad esempio, yournameVSTutorialFactory) e provare a pubblicare di nuovo. Per informazioni sulle regole di denominazione per gli elementi di Data factory, vedere l'argomento relativo alle [regole di denominazione di Data factory](data-factory-naming-rules.md) .        
      > 
      > 
   3. Selezionare la sottoscrizione di Azure per hello **sottoscrizione** campo.
      
      > [!IMPORTANT]
      > Se non viene visualizzata alcuna sottoscrizione, assicurarsi che si è connessi con un account che è un amministratore o co-amministratore della sottoscrizione hello.  
      > 
      > 
   4. Seleziona hello **gruppo di risorse** per hello data factory toobe creato. 
   5. Seleziona hello **area** per data factory di hello. Solo le aree supportate dal servizio Data Factory hello vengono visualizzate nell'elenco a discesa hello.
   6. Fare clic su **Avanti** tooswitch toohello **pubblicare elementi** pagina.
      
       ![Pagina Configure data factory (Configura data factory)](media/data-factory-copy-activity-tutorial-using-visual-studio/configure-data-factory-page.png)   
5. In hello **pubblicare elementi** pagina, assicurarsi che tutti hello Data factory di entità vengono selezionate e fare clic su **Avanti** tooswitch toohello **riepilogo** pagina.
   
   ![Pagina Publish Items (Pubblica elementi)](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-items-page.png)     
6. Esaminare hello riepilogo e fare clic su **Avanti** toostart hello distribuzione elaborare e visualizzare hello **lo stato di distribuzione**.
   
   ![Pagina Riepilogo pubblicazione](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-summary-page.png)
7. In hello **lo stato di distribuzione** pagina, dovrebbe essere stato hello hello processo di distribuzione. Dopo la distribuzione hello viene eseguita, fare clic su Fine.
 
   ![Pagina Stato distribuzione](media/data-factory-copy-activity-tutorial-using-visual-studio/deployment-status.png)

Si noti hello seguenti punti: 

* Se viene visualizzato l'errore hello: "questa sottoscrizione non è registrato toouse dello spazio dei nomi Microsoft. DataFactory", effettuare una delle seguenti hello e riprovare: 
  
  * In Azure PowerShell, eseguire hello seguenti provider di comandi tooregister hello Data Factory. 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    È possibile eseguire hello successivo comando tooconfirm tale hello Data Factory di provider è registrato. 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Account di accesso tramite hello sottoscrizione di Azure in hello [portale di Azure](https://portal.azure.com) e passare a pannello di Data Factory tooa creare una data factory nel portale di Azure hello (o). Questa azione registra automaticamente i provider di hello.
* nome Hello della hello data factory può essere registrato come un nome DNS in futuro hello e pertanto diventano visibili pubblicamente.

> [!IMPORTANT]
> le istanze di Data Factory toocreate, è necessario toobe admin un co-amministratore della sottoscrizione di Azure hello

## <a name="monitor-pipeline"></a>Monitorare la pipeline
Passare toohello home page per la data factory:

1. Accedi troppo[portale di Azure](https://portal.azure.com).
2. Fare clic su **più servizi** hello menu a sinistra e fare clic su **Data factory**.

    ![Esplora data factory](media/data-factory-copy-activity-tutorial-using-visual-studio/browse-data-factories.png)
3. Iniziare a digitare il nome di hello della data factory.

    ![Nome della data factory](media/data-factory-copy-activity-tutorial-using-visual-studio/enter-data-factory-name.png) 
4. Scegliere la data factory di hello risultati elenco toosee hello home page per la data factory.

    ![Home page di Data factory](media/data-factory-copy-activity-tutorial-using-visual-studio/data-factory-home-page.png)
5. Seguire le istruzioni da [monitorare set di dati e della pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) pipeline hello toomonitor e set di dati è stato creato in questa esercitazione. Attualmente, Visual Studio non supporta il monitoraggio delle pipeline di Data Factory. 

## <a name="summary"></a>Riepilogo
In questa esercitazione è creato un Azure factory toocopy dati da un database di SQL Azure tooan blob di Azure. È stato utilizzato Visual Studio toocreate hello data factory, i servizi collegati, i set di dati e una pipeline. Ecco i passaggi di alto livello hello effettuati in questa esercitazione:  

1. Creare un'istanza di Azure **Data Factory**.
2. Creare **servizi collegati**:
   1. Un **di archiviazione di Azure** collegati toolink service account di archiviazione di Azure che contiene i dati di input.     
   2. Un **SQL Azure** collegati toolink servizio database SQL di Azure che contiene i dati di output di hello. 
3. Creare **set di dati**che descrivono dati di input e dati di output per le pipeline.
4. Creare una **pipeline** con un'**attività di copia** con **BlobSource** come origine e **SqlSink** come sink. 

toosee toouse un'attività Hive di HDInsight tootransform di dati tramite il cluster HDInsight di Azure, vedere [ esercitazione: creare i primi dati tootransform pipeline utilizzando cluster Hadoop](data-factory-build-your-first-pipeline.md).

È possibile concatenare le due attività (eseguire un'attività dopo l'altro) mediante l'impostazione di set di dati di hello output di un'attività come hello input set di dati di hello altre attività. Per informazioni dettagliate, vedere [Pianificazione ed esecuzione con Data Factory](data-factory-scheduling-and-execution.md). 

## <a name="view-all-data-factories-in-server-explorer"></a>Visualizzare tutte le data factory in Esplora server
In questa sezione viene descritto come toouse hello Esplora Server in Visual Studio tooview tutte le data factory hello nella sottoscrizione di Azure e creare un progetto di Visual Studio basato su una data factory esistente. 

1. In **Visual Studio**, fare clic su **vista** hello menu e fare clic su **Esplora Server**.
2. Nella finestra di Esplora Server hello, espandere **Azure** espandere **Data Factory**. Se viene visualizzato **Accedi tooVisual Studio**, immettere hello **account** associata con la sottoscrizione di Azure e fare clic su **continua**. Immettere la **password** e fare clic su **Accedi**. Visual Studio tenta tooget informazioni su tutte le data factory di Azure nella sottoscrizione. Viene visualizzato lo stato di hello di questa operazione in hello **elenco attività di Data Factory** finestra.

    ![Esplora server](./media/data-factory-copy-activity-tutorial-using-visual-studio/server-explorer.png)

## <a name="create-a-visual-studio-project-for-an-existing-data-factory"></a>Creare un progetto di Visual Studio per una data factory esistente

- Fare doppio clic su una data factory in Esplora Server e selezionare **tooNew esportare Data Factory progetto** toocreate un progetto di Visual Studio basato su una data factory esistente.

    ![Progetto VS tooa di esportazione data factory](./media/data-factory-copy-activity-tutorial-using-visual-studio/export-data-factory-menu.png)  

## <a name="update-data-factory-tools-for-visual-studio"></a>Aggiornare gli strumenti di Data factory di Azure per Visual Studio
hello tooupdate strumenti di Data Factory di Azure per Visual Studio, come segue:

1. Fare clic su **strumenti** nel menu hello e selezionare **estensioni e aggiornamenti**. 
2. Selezionare **aggiornamenti** in hello riquadro sinistro e quindi selezionare **Visual Studio Gallery**.
3. Selezionare **Azure Data Factory tools for Visual Studio** e fare clic su **Aggiorna**. Se non viene visualizzata questa voce, si dispone già di più recente degli strumenti hello hello. 

## <a name="use-configuration-files"></a>Usare i file di configurazione
È possibile utilizzare i file di configurazione nelle proprietà tooconfigure di Visual Studio per servizi/tabelle/pipeline del collegato in modo diverso per ogni ambiente.

Prendere in considerazione hello seguente definizione JSON per un servizio collegato di archiviazione di Azure. toospecify **connectionString** con valori diversi per accountname e accountkey in base a hello ambiente (sviluppo/Test o produzione) toowhich si distribuiscono le entità di Data Factory. usare un file di configurazione separato per ogni ambiente.

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

### <a name="add-a-configuration-file"></a>Aggiungere un file di configurazione
Aggiungere un file di configurazione per ogni ambiente eseguendo hello alla procedura seguente:   

1. Fare clic sul progetto Data Factory hello nella soluzione Visual Studio, scegliere troppo**Aggiungi**, fare clic su **nuovo elemento**.
2. Selezionare **Config** selezionare nell'elenco dei modelli installati a sinistra di hello hello **File di configurazione**, immettere un **nome** per la configurazione di hello file e fare clic su **Aggiungere**.

    ![Aggiungere un file di configurazione](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. Aggiungere parametri di configurazione e i relativi valori in hello seguente formato:

    ```json
    {
        "$schema": "http://datafactories.schema.management.azure.com/vsschemas/V1/Microsoft.DataFactory.Config.json",
        "AzureStorageLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        ],
        "AzureSqlLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value":  "Server=tcp:spsqlserver.database.windows.net,1433;Database=spsqldb;User ID=spelluru;Password=Sowmya123;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        ]
    }
    ```

    Questo esempio configura la proprietà connectionString di un servizio collegato Archiviazione di Azure e di un servizio collegato Azure SQL. Si noti che la sintassi di hello per specificare nome [JsonPath](http://goessner.net/articles/JsonPath/).   

    Se JSON ha una proprietà che è una matrice di valori, come illustrato nel seguente codice hello:  

    ```json
    "structure": [
          {
              "name": "FirstName",
            "type": "String"
          },
          {
            "name": "LastName",
            "type": "String"
        }
    ],
    ```

    Configurare le proprietà come illustrato nel seguente file di configurazione (utilizzare indicizzazione in base zero) hello:

    ```json
    {
        "name": "$.properties.structure[0].name",
        "value": "FirstName"
    }
    {
        "name": "$.properties.structure[0].type",
        "value": "String"
    }
    {
        "name": "$.properties.structure[1].name",
        "value": "LastName"
    }
    {
        "name": "$.properties.structure[1].type",
        "value": "String"
    }
    ```

### <a name="property-names-with-spaces"></a>Nomi delle proprietà con spazi
Se un nome di proprietà contiene spazi, utilizzare le parentesi quadre, come illustrato in hello (nome server di Database) di esempio seguente:

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a>Distribuire la soluzione usando una configurazione
Quando si pubblicano le entità di Azure Data Factory in Visual Studio, è possibile specificare una configurazione di hello che si vuole toouse per tale operazione di pubblicazione.

entità toopublish in un progetto di Data Factory di Azure tramite file di configurazione:   

1. Fare clic sul progetto Data Factory e fare clic su **pubblica** toosee hello **pubblicare elementi** la finestra di dialogo.
2. Selezionare una data factory esistente oppure specificare valori per la creazione di una data factory in hello **Configura data factory di** pagina e fare clic su **Avanti**.   
3. In hello **pubblicare elementi** pagina: viene visualizzato un elenco a discesa con le configurazioni disponibili per hello **selezionare configurazione della distribuzione** campo.

    ![Selezionare un file di configurazione](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. Seleziona hello **file di configurazione** che desideri toouse e fare clic su **Avanti**.
5. Assicurarsi di visualizzare il nome di hello del file JSON in hello **riepilogo** pagina e fare clic su **Avanti**.
6. Fare clic su **fine** al termine dell'operazione di distribuzione hello.

Quando si distribuisce, i valori hello dal file di configurazione hello sono tooset utilizzati valori di proprietà nei file JSON hello prima entità hello tooAzure distribuito il servizio Data Factory.   

## <a name="use-azure-key-vault"></a>Usare l'Insieme di credenziali delle chiavi di Azure
Non è consigliabile e spesso rispetto ai dati sensibili toocommit criteri di sicurezza, ad esempio repository di codice toohello stringhe di connessione. Vedere [ADF Secure pubblicare](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample in GitHub toolearn sull'archiviazione di informazioni riservate nell'insieme di credenziali chiave di Azure e l'uso durante la pubblicazione entità Data Factory. Hello Secure pubblicare l'estensione di Visual Studio consente hello toobe di segreti archiviati nell'insieme di credenziali chiave e solo i riferimenti toothem vengono specificati in servizi collegati o configurazioni di distribuzione. Questi riferimenti vengono risolti durante la pubblicazione tooAzure entità Data Factory. Questi file possono quindi essere eseguito il commit toosource repository senza esporre tutti i segreti.


## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione sono stati usati l'archivio BLOB di Azure come archivio dati di origine e un database SQL di Azure come archivio dati di destinazione in un'operazione di copia. Hello nella tabella seguente fornisce un elenco di archivi di dati supportato come origini e destinazioni da attività di copia hello: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn su come archiviano dati toocopy da e verso un tipo di dati, fare clic su collegamento hello per hello archivio di dati nella tabella hello.
