---
title: 'Esercitazione: Creare un dati toocopy della pipeline di Data Factory di Azure (portale di Azure) | Documenti Microsoft'
description: "In questa esercitazione, utilizzare toocreate portale Azure una pipeline di Data Factory di Azure con dati di toocopy un'attività di copia da un database di SQL Azure tooan di archiviazione blob di Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d9317652-0170-4fd3-b9b2-37711272162b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fadd840fe9a15cd8831cdb25dccbd10ac42fa161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-azure-portal-toocreate-a-data-factory-pipeline-toocopy-data"></a>Esercitazione: Usare toocreate portale Azure una Data Factory pipeline toocopy di dati 
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

In questo articolo viene illustrato come toouse [portale di Azure](https://portal.azure.com) toocreate una data factory con una pipeline che copia i dati da un database di SQL Azure tooan di archiviazione blob di Azure. Se si tooAzure nuova Data Factory, leggere hello [tooAzure introduzione Data Factory](data-factory-introduction.md) articolo prima di eseguire questa esercitazione.   

In questa esercitazione si crea una pipeline contenente una sola attività: un'attività di copia attività di copia Hello copia dati da un archivio dati di sink supportati tooa di archivio di dati supportati. Per un elenco degli archivi dati supportati come origini e sink, vedere gli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats). attività Hello è alimentato da un servizio disponibile a livello globale che è possibile copiare dati tra diversi archivi dati in modo sicuro, affidabile e scalabile. Per ulteriori informazioni sulle attività di copia hello, vedere [attività lo spostamento dei dati](data-factory-data-movement-activities.md).

Una pipeline può includere più attività Inoltre, è possibile concatenare le due attività (eseguire un'attività dopo l'altro) mediante l'impostazione di set di dati di hello output di un'attività come hello input set di dati di hello altre attività. Per altre informazioni, vedere [Attività multiple in una pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

> [!NOTE] 
> pipeline di dati Hello in questa esercitazione consente di copiare dati da un archivio dati di origine dati archivio tooa destinazione. Per un'esercitazione su come dati di tootransform tramite Data Factory di Azure, vedere [esercitazione: creare una pipeline di dati tootransform utilizzando cluster Hadoop](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Prerequisiti
Completare i prerequisiti elencati in hello [prerequisiti per l'esercitazione](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) articolo prima di eseguire questa esercitazione.

## <a name="steps"></a>Passi
Ecco i passaggi di hello che è eseguire come parte di questa esercitazione:

1. Creare una **data factory** di Azure. In questo passaggio viene creata una data factory denominata ADFTutorialDataFactory. 
2. Creare **servizi collegati** nella data factory di hello. In questo passaggio si creano due servizi collegati di tipo Archiviazione di Azure e database SQL di Azure. 
    
    Hello AzureStorageLinkedService collega la data factory toohello account di archiviazione di Azure. È stato creato un contenitore e caricare l'account di archiviazione di dati toothis come parte di [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

    AzureSqlLinkedService collega il toohello data factory di Azure SQL database. dati Hello che viene copiati dall'archiviazione blob hello vengono archiviati nel database. Come parte dei [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) è stata creata una tabella SQL in questo database.   
3. Creazione di input e output **set di dati** nella data factory di hello.  
    
    il servizio di archiviazione di Azure collegati Hello specifica hello stringa di connessione del servizio Data Factory utilizzata in fase di esecuzione tooconnect tooyour account di archiviazione di Azure. E specifica di set di dati blob di input hello hello contenitore e della cartella di hello che contiene i dati di input hello.  

    Analogamente, hello servizio Database SQL di Azure collegati specifica hello stringa di connessione del servizio Data Factory utilizzata nel database di SQL Azure tooyour tooconnect fase di esecuzione. E specifica di set di dati nella tabella SQL output hello tabella hello nei dati di hello database toowhich hello dall'archiviazione blob hello viene copiata.
4. Creare un **pipeline** nella data factory di hello. In questo passaggio viene creata una pipeline con un'attività di copia.   
    
    attività di copia Hello copia dati da un blob nella tabella tooa di archiviazione blob di Azure hello in database SQL di Azure hello. È possibile utilizzare un'attività di copia in una pipeline di dati da qualsiasi destinazione tooany supportato di origine supportata toocopy. Per un elenco degli archivi dati supportati, vedere l'articolo sulle [attività di spostamento dei dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats). 
5. Pipeline di hello monitor. In questo passaggio si **monitoraggio** hello sezioni dei set di dati di input e output tramite il portale di Azure. 

## <a name="create-data-factory"></a>Creare un'istanza di Data Factory
> [!IMPORTANT]
> Completamento [prerequisiti per l'esercitazione hello](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) se non è già fatto.   

Una data factory può comprendere una o più pipeline. Una pipeline può comprendere una o più attività. Ad esempio, una data toocopy attività di copia da un archivio dati di origine tooa destinazione e un toorun attività Hive di HDInsight un tootransform script Hive i dati di output tooproduct dati di input. Iniziamo con la creazione di data factory di hello in questo passaggio.

1. Dopo l'accesso toohello [portale di Azure](https://portal.azure.com/), fare clic su **New** scegliere dal menu a sinistra, hello **dati + Analitica**, fare clic su **Data Factory**. 
   
   ![Nuovo->DataFactory](./media/data-factory-copy-activity-tutorial-using-azure-portal/NewDataFactoryMenu.png)    
2. In hello **nuova data factory** pannello:
   
   1. Immettere **ADFTutorialDataFactory** per hello **nome**. 
      
         ![Pannello Nuova data factory](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-new-data-factory.png)
      
       nome Hello di hello Azure data factory deve essere **univoco globale**. Se viene visualizzato il seguente errore hello, modificare il nome di hello di hello data factory (ad esempio, yournameADFTutorialDataFactory) e provare a creare di nuovo. Per informazioni sulle regole di denominazione per gli elementi di Data factory, vedere l'argomento relativo alle [regole di denominazione di Data factory](data-factory-naming-rules.md) .
      
           Data factory name “ADFTutorialDataFactory” is not available  
      
       ![Nome di data factory non disponibile](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-not-available.png)
   2. Selezionare di Azure **sottoscrizione** in cui si desidera data factory di toocreate hello. 
   3. Per hello **gruppo di risorse**, effettuare una delle hello alla procedura seguente:
      
      - Selezionare **utilizzare esistente**e selezionare un gruppo di risorse esistente dall'elenco a discesa hello. 
      - Selezionare **Crea nuovo**e immettere il nome di hello di un gruppo di risorse.   
         
          Alcuni dei passaggi di hello in questa esercitazione si presuppone che venga utilizzato il nome di hello: **ADFTutorialResourceGroup** per il gruppo di risorse hello. toolearn sui gruppi di risorse, vedere [utilizzando risorse gruppi di risorse di Azure toomanage](../azure-resource-manager/resource-group-overview.md).  
   4. Seleziona hello **percorso** per data factory di hello. Solo le aree supportate dal servizio Data Factory hello vengono visualizzate nell'elenco a discesa hello.
   5. Selezionare **toodashboard Pin**.     
   6. Fare clic su **Crea**.
      
      > [!IMPORTANT]
      > le istanze di Data Factory toocreate, è necessario essere un membro di hello [Data Factory collaboratore](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) ruolo a livello di gruppo di risorse di sottoscrizione/hello.
      > 
      > nome Hello della hello data factory può essere registrato come un nome DNS in futuro hello e pertanto diventano visibili pubblicamente.                
      > 
      > 
3. Nel dashboard di hello, si vedrà hello segue riquadro con stato: **data factory di distribuzione**. 

    ![Riquadro Deploying data factory (Distribuzione della data factory)](media/data-factory-copy-activity-tutorial-using-azure-portal/deploying-data-factory.png)
4. Una volta completata la creazione di hello, vedrai hello **Data Factory** pannello, come illustrato nella figura hello.
   
   ![Home page di Data factory](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-home-page.png)

## <a name="create-linked-services"></a>Creare servizi collegati
Creare servizi collegati in un toolink factory dati i dati vengono archiviati e toohello data factory di servizi di calcolo. In questa esercitazione non si usano servizi di calcolo come Azure HDInsight o Azure Data Lake Analytics, ma due archivi dati di tipo Archiviazione di Azure (origine) e database SQL di Azure (destinazione). 

Si creano quindi due servizi collegati denominati AzureStorageLinkedService e AzureSqlLinkedService di tipo AzureStorage e AzureSqlDatabase.  

Hello AzureStorageLinkedService collega la data factory toohello account di archiviazione di Azure. Questo account di archiviazione è hello uno in cui è stato creato un contenitore e caricato dati hello come parte del [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

AzureSqlLinkedService collega il toohello data factory di Azure SQL database. dati Hello che viene copiati dall'archiviazione blob hello vengono archiviati nel database. Tabella emp hello è stato creato in questo database come parte di [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).  

### <a name="create-azure-storage-linked-service"></a>Creare il servizio collegato Archiviazione di Azure
In questo passaggio si collega la data factory tooyour account di archiviazione di Azure. Specificare il nome di hello e chiave dell'account di archiviazione di Azure in questa sezione.  

1. In hello **Data Factory** pannello, fare clic su **autore e distribuire** riquadro.
   
   ![Riquadro Creare e distribuire](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-author-deploy-tile.png) 
2. Vedrai hello **Editor delle Data Factory** come illustrato nella seguente immagine hello: 

    ![Editor di Data factory](./media/data-factory-copy-activity-tutorial-using-azure-portal/data-factory-editor.png)
3. Nell'editor di hello, fare clic su **nuovo archivio dati** pulsante sulla barra degli strumenti hello e selezionare **archiviazione di Azure** dal menu a discesa hello. Verrà visualizzato il modello JSON hello per la creazione di un servizio collegato di archiviazione Azure nel riquadro di destra hello. 
   
    ![Pulsante Nuovo archivio dati dell'editor](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-newdatastore-button.png)    
3. Sostituire `<accountname>` e `<accountkey>` con hello account nome e l'account di valori di chiave per l'account di archiviazione di Azure. 
   
    ![JSON dell'archivio BLOB dell'editor](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-json.png)    
4. Fare clic su **Distribuisci** sulla barra degli strumenti hello. Dovrebbe essere distribuito hello **AzureStorageLinkedService** nella struttura ad albero hello ora Visualizza. 
   
    ![Distribuzione dell'archivio BLOB dell'editor](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-deploy.png)

    Per ulteriori informazioni sulle proprietà JSON nella definizione di servizio collegato hello, vedere [connettore di archiviazione Blob di Azure](data-factory-azure-blob-connector.md#linked-service-properties) articolo.

### <a name="create-a-linked-service-for-hello-azure-sql-database"></a>Creare un servizio collegato per hello Database SQL di Azure
In questo passaggio si collega il tooyour data factory di Azure SQL database. Specificare nome del server SQL Azure hello, nome del database, nome utente e password dell'utente in questa sezione. 

1. In hello **Editor delle Data Factory**, fare clic su **nuovo archivio dati** pulsante sulla barra degli strumenti hello e selezionare **Database SQL di Azure** dal menu a discesa hello. Verrà visualizzato il modello JSON hello per la creazione di servizio collegato SQL Azure hello nel riquadro di destra hello.
2. Sostituire `<servername>`, `<databasename>`, `<username>@<servername>` e `<password>` con i nomi del server di Azure SQL e del database, l'account utente e la password. 
3. Fare clic su **Distribuisci** hello toocreate barra degli strumenti e distribuire hello **AzureSqlLinkedService**.
4. Verificare che sia visualizzato **AzureSqlLinkedService** nella visualizzazione struttura ad albero di hello in **servizi collegati**.  

    Per altre informazioni su queste proprietà JSON, vedere l'articolo relativo al [connettore del database SQL di Azure](data-factory-azure-sql-connector.md#linked-service-properties).

## <a name="create-datasets"></a>Creare set di dati
Nel passaggio precedente hello, servizi collegati toolink è creato l'account di archiviazione di Azure e la data factory di Azure SQL database tooyour. In questo passaggio si definiscono due set di dati denominati InputDataset e OutputDataset che rappresentano l'input e output i dati archiviati in archivi dati hello a cui fa riferimento AzureStorageLinkedService e AzureSqlLinkedService rispettivamente.

il servizio di archiviazione di Azure collegati Hello specifica hello stringa di connessione del servizio Data Factory utilizzata in fase di esecuzione tooconnect tooyour account di archiviazione di Azure. E, set di dati blob di input hello (InputDataset) specifica il contenitore di hello e la cartella di hello che contiene i dati di input hello.  

Analogamente, hello servizio Database SQL di Azure collegati specifica hello stringa di connessione del servizio Data Factory utilizzata nel database di SQL Azure tooyour tooconnect fase di esecuzione. E, di output di hello set di dati nella tabella SQL (OututDataset) specifica la tabella hello in hello di toowhich hello database vengono copiati dati dall'archiviazione blob hello. 

### <a name="create-input-dataset"></a>Creare set di dati di input
In questo passaggio, creare un set di dati denominato InputDataset che punta il file di blob tooa (emp.txt) nella cartella radice hello di un contenitore di blob (adftutorial) in hello rappresentato da hello AzureStorageLinkedService collegato servizio di archiviazione di Azure. Se non specifica un valore per il nome file hello (o ignorarlo), i dati da tutti i BLOB nella cartella input hello sono copiati toohello destinazione. In questa esercitazione, si specifica un valore per il nome file hello. 

1. In hello **Editor** per hello Data Factory, fare clic su **... Ulteriori**, fare clic su **nuovo set di dati**, fare clic su **archiviazione Blob di Azure** dal menu a discesa hello. 
   
    ![Menu Nuovo set di dati](./media/data-factory-copy-activity-tutorial-using-azure-portal/new-dataset-menu.png)
2. Sostituire JSON nel riquadro di destra hello con hello frammento di codice JSON seguente: 
   
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
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
          "folderPath": "adftutorial/",
          "fileName": "emp.txt",
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
3. Fare clic su **Distribuisci** hello toocreate barra degli strumenti e distribuire hello **InputDataset** set di dati. Assicurarsi di visualizzare hello **InputDataset** nella visualizzazione ad albero di hello.

### <a name="create-output-dataset"></a>Creare il set di dati di output
servizio collegato Database di SQL Azure Hello specifica hello stringa di connessione del servizio Data Factory utilizzata nel database di SQL Azure tooyour tooconnect fase di esecuzione. Hello output SQL tabella dataset (OututDataset) create in questo passaggio specifica tabella hello nei dati di hello database toowhich hello dall'archiviazione blob hello viene copiata.

1. In hello **Editor** per hello Data Factory, fare clic su **... Ulteriori**, fare clic su **nuovo set di dati**, fare clic su **SQL Azure** dal menu a discesa hello. 
2. Sostituire JSON nel riquadro di destra hello con hello frammento di codice JSON seguente:

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
        "linkedServiceName": "AzureSqlLinkedService",
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
3. Fare clic su **Distribuisci** hello toocreate barra degli strumenti e distribuire hello **OutputDataset** set di dati. Assicurarsi di visualizzare hello **OutputDataset** nella visualizzazione struttura ad albero di hello in **set di dati**. 

## <a name="create-pipeline"></a>Creare una pipeline
In questo passaggio viene creata una pipeline con un'**attività di copia** che usa **InputDataset** come input e **OutputDataset** come output.

Set di dati di output è attualmente, quali unità hello pianificazione. In questa esercitazione, set di dati di output è tooproduce configurato una sezione di una volta all'ora. pipeline Hello dispone ora di inizio e ora di fine di un giorno separato, ovvero 24 ore. Pertanto, 24 sezioni del set di dati di output vengono generate dalla pipeline hello. 

1. In hello **Editor** per hello Data Factory, fare clic su **... Altro** e quindi su **Nuova pipeline**. In alternativa, è possibile fare doppio clic **pipeline** in visualizzazione struttura ad albero hello e fare clic su **nuova pipeline**.
2. Sostituire JSON nel riquadro di destra hello con hello frammento di codice JSON seguente: 

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
              "retry": 0,
              "timeout": "01:00:00"
            }
          }
        ],
        "start": "2017-05-11T00:00:00Z",
        "end": "2017-05-12T00:00:00Z"
      }
    } 
    ```   
    
    Si noti hello seguenti punti:
   
    - Nella sezione attività hello, è presente una sola attività il cui **tipo** è troppo**copia**. Per ulteriori informazioni sulle attività di copia hello, vedere [attività lo spostamento dei dati](data-factory-data-movement-activities.md). Nelle soluzioni Data Factory è anche possibile usare le [attività di trasformazione dei dati](data-factory-data-transformation-activities.md).
    - Input per attività hello è troppo**InputDataset** e di output per attività hello è troppo**OutputDataset**. 
    - In hello **typeProperties** sezione **BlobSource** è specificato come tipo di origine hello e **SqlSink** è specificato come tipo di sink hello. Per un elenco completo degli archivi di dati supportati dall'attività di copia hello come origini e sink, vedere [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats). toolearn sulla modalità di memorizzazione toouse dati specifici supportati come origine/sink, fare clic su collegamento hello nella tabella hello.
    - Per la data e l'ora di inizio è necessario usare il [formato ISO](http://en.wikipedia.org/wiki/ISO_8601). ad esempio 2016-10-14T16:32:41Z. Hello **fine** è facoltativo, ma viene usata in questa esercitazione. Se non specifica alcun valore per hello **fine** proprietà, viene calcolato come "**start + 48 ore**". specificare in modo indefinito, pipeline hello toorun **9999-09-09** come valore hello hello **fine** proprietà.
     
    In hello sopra riportato, sono presenti sezioni dati 24 come ogni sezione di dati viene prodotta ogni ora.

    Per le descrizioni delle proprietà JSON nella definizione di una pipeline, vedere l'articolo su come [creare pipeline](data-factory-create-pipelines.md). Per le descrizioni delle proprietà JSON nella definizione di un'attività di copia, vedere le [attività di spostamento dei dati](data-factory-data-movement-activities.md). Per le descrizioni delle proprietà JSON supportate da BlobSource, vedere l'articolo relativo al [connettore BLOB di Azure](data-factory-azure-blob-connector.md). Per le descrizioni delle proprietà JSON supportate da SqlSink, vedere l'articolo relativo al [connettore del database SQL di Azure](data-factory-azure-sql-connector.md).
3. Fare clic su **Distribuisci** hello toocreate barra degli strumenti e distribuire hello **ADFTutorialPipeline**. Verificare che sia visualizzato pipeline hello nella visualizzazione ad albero di hello. 
4. A questo punto, chiudere hello **Editor** pannello facendo **X**. Fare clic su **X** nuovamente toosee hello **Data Factory** home page di hello **ADFTutorialDataFactory**.

**Congratulazioni.** Una data factory di Azure è stato creato con una pipeline toocopy dati da un database di SQL Azure tooan di archiviazione blob di Azure. 


## <a name="monitor-pipeline"></a>Monitorare la pipeline
In questo passaggio, utilizzare hello Azure toomonitor portale cosa accade in un data factory di Azure.    

### <a name="monitor-pipeline-using-monitor--manage-app"></a>Monitorare la pipeline con l'app Monitoraggio e gestione
Hello passaggi seguenti viene illustrato come toomonitor pipeline in una factory di dati tramite l'applicazione di monitoraggio e gestione hello: 

1. Fare clic su **monitoraggio e gestione** riquadro hello home page per la data factory.
   
    ![Riquadro Monitoraggio e gestione](./media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-manage-tile.png) 
2. L'**applicazione Monitoraggio e gestione** verrà visualizzata in una scheda separata. 

    > [!NOTE]
    > Se viene visualizzato il browser web hello è bloccata su "Autorizzazione …", effettuare una delle seguenti hello: crittografato hello **bloccare i cookie di terze parti e i dati del sito** casella di controllo (o) creare un'eccezione per **login.microsoftonline.com**, quindi riprovare a eseguire tooopen hello app.

    ![App Monitoraggio e gestione](./media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-and-manage-app.png)
3. Hello modifica **ora di inizio** e **ora di fine** tooinclude avviare (2017-05-11) e fine (2017-05-12) della pipeline e fare clic su **applica**.     
3. Vedrai hello **windows attività** associata a ogni ora tra l'inizio della pipeline e di fine volte nell'elenco di hello nel riquadro centrale hello. 
4. Dettagli toosee su una finestra attività hello finestra attività in hello **attività Windows** elenco. 
    ![Dettagli finestra attività](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-window-details.png)

    In Esplora finestra di attività a destra di hello, vedrai che hello intervalli di ora UTC corrente toohello (8:12 PM) vengono elaborati (in verde). le sezioni 8-9 PM, PM 9, 10, 10 11 PM, 11 PM - 12 AM Hello non vengono ancora elaborate.

    Hello **tentativi** sezione hello destra riquadro fornisce informazioni per la sezione dati hello di esecuzione dell'attività hello. Se si è verificato un errore, vengono forniti dettagli sull'errore hello. Ad esempio, se l'input hello cartella o del contenitore non esiste e hello sezione elaborazione ha esito negativo, viene visualizzato un messaggio di errore che informa che il contenitore hello o cartella non esiste.

    ![Tentativi di esecuzione dell'attività](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-run-attempts.png) 
4. Avviare **SQL Server Management Studio**, connettersi toohello Database SQL di Azure e verificare che le righe di hello vengono inserite in toohello **emp** tabella nel database di hello.
    
    ![Risultati della query SQL](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-sql-query-results.png)

Per informazioni dettagliate sull'uso di questa applicazione, vedere [Monitorare e gestire le pipeline di Azure Data Factory con la nuova app di monitoraggio e gestione](data-factory-monitor-manage-app.md).

### <a name="monitor-pipeline-using-diagram-view"></a>Monitorare la pipeline con la vista diagramma
È inoltre possibile pipeline di dati di monitoraggio tramite vista diagramma hello.  

1. In hello **Data Factory** pannello, fare clic su **diagramma**.
   
    ![Pannello Data factory - Riquadro Diagramma](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-datafactoryblade-diagramtile.png)
2. Dovrebbe essere simile toohello diagramma hello seguente immagine: 
   
    ![Vista diagramma](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-diagram-blade.png)  
5. Nella vista diagramma hello, fare doppio clic su **InputDataset** toosee sezioni per hello set di dati.  
   
    ![Set di dati con InputDataset selezionato](./media/data-factory-copy-activity-tutorial-using-azure-portal/DataSetsWithInputDatasetFromBlobSelected.png)   
5. Fare clic su **ulteriori** collegamento toosee tutte le sezioni di dati hello. Vengono visualizzate 24 sezioni orarie tra l'ora di inizio e di fine della pipeline. 
   
    ![Tutte le sezioni dati di input](./media/data-factory-copy-activity-tutorial-using-azure-portal/all-input-slices.png)  
   
    Si noti che tutte le sezioni di dati di ora UTC corrente toohello di hello sono **pronto** perché hello **emp.txt** file presente tutto il tempo hello nel contenitore di blob hello: **adftutorial\input**. le sezioni di Hello per le ore future hello non sono ancora nello stato pronto. Verificare che non sono presenti sezioni visualizzati in hello **recente sezioni con errori** sezione nella parte inferiore di hello.
6. Pannelli hello Chiudi finché non si vedere hello diagramma vista (o) scorrimento sinistro toosee hello visualizzare. quindi fare doppio clic su **OutputDataset**. 
8. Fare clic su **ulteriori** collegamento hello **tabella** pannello **OutputDataset** toosee tutti hello sezioni.

    ![Pannello Sezioni dati](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslices-blade.png) 
9. Si noti che tutti hello intervalli di ora UTC corrente toohello spostare da **in attesa di esecuzione** stato = > **In corso** ==> **pronto** stato. Hello sezioni da hello precedente (prima dell'ora corrente) vengono elaborati dal toooldest più recente per impostazione predefinita. Ad esempio, se hello ora corrente è 8:12 PM UTC, sezione hello per 19: 00 - 8 PM viene elaborato prima sezione 6 PM - 7 alle 19 hello. sezione alle 20.00-21: 00 Hello viene elaborata alla fine di hello hello dell'intervallo di tempo per impostazione predefinita, ovvero dopo 21: 00.  
10. Fare clic su qualsiasi sezione di dati dall'elenco hello e dovrebbe essere hello **sezione dati** blade. I dati associati a una finestra attività vengono chiamati sezione. Una sezione può essere costituita da uno o più file.  
    
     ![Pannello Sezione di dati](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslice-blade.png)
    
     Se la sezione hello non hello **pronto** stato, è possibile vedere le sezioni upstream hello che non sono pronti e bloccano l'intervallo corrente di hello l'esecuzione in hello **sezioni Upstream non pronte** elenco.
11. In hello **sezione dati** pannello, dovrebbe essere esegue tutte le attività nell'elenco di hello nella parte inferiore di hello. Fare clic su un **esecuzione dell'attività** toosee hello **Dettagli esecuzione attività** blade. 
    
    ![Dettagli esecuzione attività](./media/data-factory-copy-activity-tutorial-using-azure-portal/ActivityRunDetails.png)

    In questo pannello, viene visualizzato come ha richiesto l'operazione di copia hello lungo, quali la velocità effettiva, il numero di byte di dati sono di lettura e l'ora di inizio scritta, esecuzione, eseguire ora di fine e così via.  
12. Fare clic su **X** tooclose tutti i pannelli hello fino a tornare toohello pannello home hello **ADFTutorialDataFactory**.
13. (facoltativo) fare clic su hello **set di dati** riquadro o **pipeline** pannelli di hello tooget riquadro è stato illustrato hello passaggi precedenti. 
14. Avviare **SQL Server Management Studio**, connettersi toohello Database SQL di Azure e verificare che le righe di hello vengono inserite in toohello **emp** tabella nel database di hello.
    
    ![Risultati della query SQL](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-sql-query-results.png)


## <a name="summary"></a>Riepilogo
In questa esercitazione è creato un Azure factory toocopy dati da un database di SQL Azure tooan blob di Azure. È stato utilizzato hello toocreate portale Azure hello data factory, i servizi collegati, i set di dati e una pipeline. Ecco i passaggi di alto livello hello effettuati in questa esercitazione:  

1. Creare un'istanza di Azure **Data Factory**.
2. Creare **servizi collegati**:
   1. Un **di archiviazione di Azure** collegati toolink service account di archiviazione di Azure che contiene i dati di input.     
   2. Un **SQL Azure** collegati toolink servizio database SQL di Azure che contiene i dati di output di hello. 
3. Creare **set di dati** che descrivono dati di input e di output per le pipeline.
4. Creare una **pipeline** con un'**attività di copia** con **BlobSource** come origine e **SqlSink** come sink.  

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione sono stati usati l'archivio BLOB di Azure come archivio dati di origine e un database SQL di Azure come archivio dati di destinazione in un'operazione di copia. Hello nella tabella seguente fornisce un elenco di archivi di dati supportato come origini e destinazioni da attività di copia hello: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn su come archiviano dati toocopy da e verso un tipo di dati, fare clic su collegamento hello per hello archivio di dati nella tabella hello.
