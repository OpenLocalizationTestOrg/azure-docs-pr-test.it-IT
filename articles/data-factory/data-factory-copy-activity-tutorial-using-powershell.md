---
title: 'Esercitazione: Creare una pipeline di dati toomove tramite Azure PowerShell | Documenti Microsoft'
description: "In questa esercitazione viene creata una pipeline di Azure Data Factory con un'attività di copia usando Azure PowerShell."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 71087349-9365-4e95-9847-170658216ed8
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 21406d7dfaa0c555b2538fbb52839d761c140fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-data-factory-pipeline-that-moves-data-by-using-azure-powershell"></a>Esercitazione: Creare una pipeline di Data Factory per lo spostamento di dati con Azure PowerShell
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

In questo articolo viene illustrato come toouse PowerShell toocreate una data factory con una pipeline che copia i dati da un database di SQL Azure tooan di archiviazione blob di Azure. Se si tooAzure nuova Data Factory, leggere hello [tooAzure introduzione Data Factory](data-factory-introduction.md) articolo prima di eseguire questa esercitazione.   

In questa esercitazione si crea una pipeline contenente una sola attività: un'attività di copia attività di copia Hello copia dati da un archivio dati di sink supportati tooa di archivio di dati supportati. Per un elenco degli archivi dati supportati come origini e sink, vedere gli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats). attività Hello è alimentato da un servizio disponibile a livello globale che è possibile copiare dati tra diversi archivi dati in modo sicuro, affidabile e scalabile. Per ulteriori informazioni sulle attività di copia hello, vedere [attività lo spostamento dei dati](data-factory-data-movement-activities.md).

Una pipeline può includere più attività Inoltre, è possibile concatenare le due attività (eseguire un'attività dopo l'altro) mediante l'impostazione di set di dati di hello output di un'attività come hello input set di dati di hello altre attività. Per altre informazioni, vedere [Attività multiple in una pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

> [!NOTE]
> In questo articolo non copre tutti i cmdlet di hello Data Factory. Per la documentazione completa su questi cmdlet, vedere [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) (Informazioni di riferimento sui cmdlet di Data Factory).
> 
> pipeline di dati Hello in questa esercitazione consente di copiare dati da un archivio dati di origine dati archivio tooa destinazione. Per un'esercitazione su come dati di tootransform tramite Data Factory di Azure, vedere [esercitazione: creare una pipeline di dati tootransform utilizzando cluster Hadoop](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Prerequisiti
- Completare i prerequisiti elencati in hello [prerequisiti per l'esercitazione](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) articolo.
- Installare **Azure PowerShell**. Seguire le istruzioni hello [come tooinstall e configurare Azure PowerShell](../powershell-install-configure.md).

## <a name="steps"></a>Passi
Ecco i passaggi di hello che è eseguire come parte di questa esercitazione:

1. Creare una **data factory** di Azure. In questo passaggio viene creata una data factory denominata ADFTutorialDataFactoryPSH. 
2. Creare **servizi collegati** nella data factory di hello. In questo passaggio si creano due servizi collegati di tipo Archiviazione di Azure e database SQL di Azure. 
    
    Hello AzureStorageLinkedService collega la data factory toohello account di archiviazione di Azure. È stato creato un contenitore e caricare l'account di archiviazione di dati toothis come parte di [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

    AzureSqlLinkedService collega il toohello data factory di Azure SQL database. dati Hello che viene copiati dall'archiviazione blob hello vengono archiviati nel database. Come parte dei [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) è stata creata una tabella SQL in questo database.   
3. Creazione di input e output **set di dati** nella data factory di hello.  
    
    il servizio di archiviazione di Azure collegati Hello specifica hello stringa di connessione del servizio Data Factory utilizzata in fase di esecuzione tooconnect tooyour account di archiviazione di Azure. E specifica di set di dati blob di input hello hello contenitore e della cartella di hello che contiene i dati di input hello.  

    Analogamente, hello servizio Database SQL di Azure collegati specifica hello stringa di connessione del servizio Data Factory utilizzata nel database di SQL Azure tooyour tooconnect fase di esecuzione. E specifica di set di dati nella tabella SQL output hello tabella hello nei dati di hello database toowhich hello dall'archiviazione blob hello viene copiata.
4. Creare un **pipeline** nella data factory di hello. In questo passaggio viene creata una pipeline con un'attività di copia.   
    
    attività di copia Hello copia dati da un blob nella tabella tooa di archiviazione blob di Azure hello in database SQL di Azure hello. È possibile utilizzare un'attività di copia in una pipeline di dati da qualsiasi destinazione tooany supportato di origine supportata toocopy. Per un elenco degli archivi dati supportati, vedere l'articolo sulle [attività di spostamento dei dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats). 
5. Pipeline di hello monitor. In questo passaggio si **monitoraggio** hello sezioni dei set di dati di input e output tramite PowerShell.

## <a name="create-a-data-factory"></a>Creare un'istanza di Data factory
> [!IMPORTANT]
> Completamento [prerequisiti per l'esercitazione hello](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) se non è già fatto.   

Una data factory può comprendere una o più pipeline. Una pipeline può comprendere una o più attività. Ad esempio, una data toocopy attività di copia da un archivio dati di origine tooa destinazione e un toorun attività Hive di HDInsight un tootransform script Hive i dati di output tooproduct dati di input. Iniziamo con la creazione di data factory di hello in questo passaggio.

1. Avviare **PowerShell**. Mantenere aperta fino al fine di hello dell'esercitazione Azure PowerShell. Se si chiude e riapre, è necessario comandi hello toorun nuovamente.

    Eseguire hello comando seguente e immettere nome utente hello e la password usati toosign in toohello portale di Azure:

    ```PowerShell
    Login-AzureRmAccount
    ```   
   
    Eseguire hello successivo comando tooview tutte le sottoscrizioni di hello per questo account:

    ```PowerShell
    Get-AzureRmSubscription
    ```

    Sottoscrizione hello tooselect da toowork con il comando seguente hello esecuzione. Sostituire  **&lt;NameOfAzureSubscription** &gt; con nome hello della sottoscrizione di Azure:

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
2. Creare un gruppo di risorse di Azure denominato **ADFTutorialResourceGroup** eseguendo hello comando seguente:

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    
    Alcuni dei passaggi di hello in questa esercitazione si supponga di utilizza il gruppo di risorse hello denominato **ADFTutorialResourceGroup**. Se si utilizza un gruppo di risorse diverso, è necessario toouse, al posto di ADFTutorialResourceGroup in questa esercitazione.
3. Eseguire hello **New AzureRmDataFactory** toocreate cmdlet una data factory denominata **ADFTutorialDataFactoryPSH**:  

    ```PowerShell
    $df=New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH –Location "West US"
    ```
    È possibile che questo nome sia già in uso. Pertanto, rendere il nome di hello della data factory di hello univoco aggiungendo un prefisso o suffisso (ad esempio: ADFTutorialDataFactoryPSH05152017) ed eseguire nuovamente il comando hello.  

Si noti hello seguenti punti:

* nome Hello di hello Azure data factory deve essere globalmente univoco. Se viene visualizzato il seguente errore hello, modificare il nome di hello (ad esempio, yournameADFTutorialDataFactoryPSH). Durante l'esecuzione di passaggi in questa esercitazione usare questo nome anziché ADFTutorialFactoryPSH. Per informazioni sugli elementi di Data Factory, vedere [Data Factory - Regole di denominazione](data-factory-naming-rules.md).

    ```
    Data factory name “ADFTutorialDataFactoryPSH” is not available
    ```
* le istanze di Data Factory toocreate, è necessario essere un collaboratore o amministratore di hello sottoscrizione di Azure.
* nome di Hello della data factory di hello registrato come un nome DNS in futuro hello e pertanto diventano visibili pubblicamente.
* È possibile che venga visualizzato hello il seguente errore: "**questa sottoscrizione non è registrato toouse dello spazio dei nomi Microsoft. DataFactory.**" Effettuare una delle seguenti hello e riprovare:

  * In Azure PowerShell, eseguire hello seguenti provider di comandi tooregister hello Data Factory:

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

    Eseguire hello successivo comando tooconfirm tale hello Data Factory di provider è stato registrato:

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Accedi tramite hello sottoscrizione di Azure toohello [portale di Azure](https://portal.azure.com). Andare a pannello di Data Factory tooa o creare una data factory in hello portale di Azure. Questa azione registra automaticamente i provider di hello.

## <a name="create-linked-services"></a>Creare servizi collegati
Creare servizi collegati in un toolink factory dati i dati vengono archiviati e toohello data factory di servizi di calcolo. In questa esercitazione non si usano servizi di calcolo come Azure HDInsight o Azure Data Lake Analytics, ma due archivi dati di tipo Archiviazione di Azure (origine) e database SQL di Azure (destinazione). 

Si creano quindi due servizi collegati denominati AzureStorageLinkedService e AzureSqlLinkedService di tipo AzureStorage e AzureSqlDatabase.  

Hello AzureStorageLinkedService collega la data factory toohello account di archiviazione di Azure. Questo account di archiviazione è hello uno in cui è stato creato un contenitore e caricato dati hello come parte del [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

AzureSqlLinkedService collega il toohello data factory di Azure SQL database. dati Hello che viene copiati dall'archiviazione blob hello vengono archiviati nel database. Tabella emp hello è stato creato in questo database come parte di [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

### <a name="create-a-linked-service-for-an-azure-storage-account"></a>Creare un servizio collegato per un account di archiviazione di Azure
In questo passaggio si collega la data factory tooyour account di archiviazione di Azure.

1. Creare un file JSON denominato **AzureStorageLinkedService.json** in **C:\ADFGetStartedPSH** cartella con hello seguente contenuto: (Crea hello cartella ADFGetStartedPSH se non esiste già.)

    > [!IMPORTANT]
    > Sostituire &lt;accountname&gt; e &lt;accountkey&gt; con nome e la chiave dell'account di archiviazione di Azure prima di salvare il file hello. 

    ```json
    {
        "name": "AzureStorageLinkedService",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        }
     }
    ``` 
2. In **Azure PowerShell**, passare toohello **ADFGetStartedPSH** cartella.
4. Eseguire hello **New AzureRmDataFactoryLinkedService** cmdlet toocreate hello servizio collegato: **AzureStorageLinkedService**. Questo cmdlet e altri cmdlet di Data Factory da usare in questa esercitazione è necessario toopass valori per hello **ResourceGroupName** e **DataFactoryName** parametri. In alternativa, è possibile passare l'oggetto DataFactory hello restituito dal cmdlet New-AzureRmDataFactory hello senza digitare ResourceGroupName e DataFactoryName ogni volta che si esegue un cmdlet. 

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureStorageLinkedService.json
    ```
    Ecco l'output di esempio hello:

    ```
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ``` 

    Altre modalità di creazione di questo servizio collegato è toospecify nome gruppo di risorse e nome della data factory anziché specificare l'oggetto DataFactory hello.  

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName <Name of your data factory> -File .\AzureStorageLinkedService.json
    ```

### <a name="create-a-linked-service-for-an-azure-sql-database"></a>Creare un servizio collegato per un database SQL di Azure
In questo passaggio si collega il tooyour data factory di Azure SQL database.

1. Creare un file JSON denominato AzureSqlLinkedService.json nella cartella C:\ADFGetStartedPSH con hello seguente contenuto:

    > [!IMPORTANT]
    > Sostituire &lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt; e &lt;password&gt; con i nomi del server, database, account utente e password di Azure SQL.
    
    ```json
    {
        "name": "AzureSqlLinkedService",
        "properties": {
            "type": "AzureSqlDatabase",
            "typeProperties": {
                "connectionString": "Server=tcp:<server>.database.windows.net,1433;Database=<databasename>;User ID=<user>@<server>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        }
     }
    ```
2. Eseguire un servizio collegato di hello toocreate di comando seguente:

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureSqlLinkedService.json
    ```
    
    Ecco l'output di esempio hello:

    ```
    LinkedServiceName : AzureSqlLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ```

   Verificare che **Consenti l'accesso ai servizi tooAzure** è attivata per il server di database SQL. tooverify e accenderlo, hello i passaggi seguenti:

    1. Accedi toohello [portale di Azure](https://portal.azure.com)
    2. Fare clic su **più servizi >** a sinistra di hello e fare clic su **istanze di SQL Server** in hello **database** categoria.
    3. Selezionare il server nell'elenco di hello di SQL Server.
    4. Nel Pannello di hello SQL server, fare clic su **Mostra le impostazioni del firewall** collegamento.
    5. In hello **le impostazioni del Firewall** pannello, fare clic su **ON** per **Consenti l'accesso ai servizi tooAzure**.
    6. Fare clic su **salvare** sulla barra degli strumenti hello. 

## <a name="create-datasets"></a>Creare set di dati
Nel passaggio precedente hello, servizi collegati toolink è creato l'account di archiviazione di Azure e la data factory di Azure SQL database tooyour. In questo passaggio si definiscono due set di dati denominati InputDataset e OutputDataset che rappresentano l'input e output i dati archiviati in archivi dati hello a cui fa riferimento AzureStorageLinkedService e AzureSqlLinkedService rispettivamente.

il servizio di archiviazione di Azure collegati Hello specifica hello stringa di connessione del servizio Data Factory utilizzata in fase di esecuzione tooconnect tooyour account di archiviazione di Azure. E, set di dati blob di input hello (InputDataset) specifica il contenitore di hello e la cartella di hello che contiene i dati di input hello.  

Analogamente, hello servizio Database SQL di Azure collegati specifica hello stringa di connessione del servizio Data Factory utilizzata nel database di SQL Azure tooyour tooconnect fase di esecuzione. E, di output di hello set di dati nella tabella SQL (OututDataset) specifica la tabella hello in hello di toowhich hello database vengono copiati dati dall'archiviazione blob hello. 

### <a name="create-an-input-dataset"></a>Creare un set di dati di input
In questo passaggio, creare un set di dati denominato InputDataset che punta il file di blob tooa (emp.txt) nella cartella radice hello di un contenitore di blob (adftutorial) in hello rappresentato da hello AzureStorageLinkedService collegato servizio di archiviazione di Azure. Se non specifica un valore per il nome file hello (o ignorarlo), i dati da tutti i BLOB nella cartella input hello sono copiati toohello destinazione. In questa esercitazione, si specifica un valore per il nome file hello.  

1. Creare un file JSON denominato **InputDataset.json** in hello **C:\ADFGetStartedPSH** cartella, con hello seguente contenuto:

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
                "fileName": "emp.txt",
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
2. Eseguire hello seguente set di dati di comando toocreate hello Data Factory.

    ```PowerShell  
    New-AzureRmDataFactoryDataset $df -File .\InputDataset.json
    ```
    Ecco l'output di esempio hello:

    ```
    DatasetName       : InputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureBlobDataset
    Policy            : Microsoft.Azure.Management.DataFactories.Common.Models.Policy
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

### <a name="create-an-output-dataset"></a>Creare un set di dati di output
In questa parte del passaggio di hello, si crea un set di dati di output denominato **OutputDataset**. Questo set di dati fa riferimento nella tabella SQL tooa nel database di SQL Azure hello rappresentato da **AzureSqlLinkedService**. 

1. Creare un file JSON denominato **OutputDataset.json** in hello **C:\ADFGetStartedPSH** cartella con hello seguente contenuto:

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
2. Eseguire hello seguente set di dati di comando toocreate hello data factory.

    ```PowerShell   
    New-AzureRmDataFactoryDataset $df -File .\OutputDataset.json
    ```

    Ecco l'output di esempio hello:

    ```
    DatasetName       : OutputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureSqlTableDataset
    Policy            :
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

## <a name="create-a-pipeline"></a>Creare una pipeline
In questo passaggio viene creata una pipeline con un'**attività di copia** che usa **InputDataset** come input e **OutputDataset** come output.

Set di dati di output è attualmente, quali unità hello pianificazione. In questa esercitazione, set di dati di output è tooproduce configurato una sezione di una volta all'ora. pipeline Hello dispone ora di inizio e ora di fine di un giorno separato, ovvero 24 ore. Pertanto, 24 sezioni del set di dati di output vengono generate dalla pipeline hello. 


1. Creare un file JSON denominato **ADFTutorialPipeline.json** in hello **C:\ADFGetStartedPSH** cartella, con hello seguente contenuto:

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
     
    Sostituire il valore di hello di hello **avviare** proprietà con hello giorno corrente e **fine** valore con hello giorno successivo. È possibile specificare solo parte della data hello e Ignora parte dell'ora hello di hello data ora. Ad esempio, "2016-02-03", che equivale troppo "2016-02-03T00:00:00Z"
     
    Per la data e l'ora di inizio è necessario usare il [formato ISO](http://en.wikipedia.org/wiki/ISO_8601). ad esempio 2016-10-14T16:32:41Z. Hello **fine** è facoltativo, ma viene usata in questa esercitazione. 
     
    Se non specifica alcun valore per hello **fine** proprietà, viene calcolato come "**start + 48 ore**". specificare in modo indefinito, pipeline hello toorun **9999-09-09** come valore hello hello **fine** proprietà.
     
    In hello sopra riportato, sono presenti sezioni dati 24 come ogni sezione di dati viene prodotta ogni ora.

    Per le descrizioni delle proprietà JSON nella definizione di una pipeline, vedere l'articolo su come [creare pipeline](data-factory-create-pipelines.md). Per le descrizioni delle proprietà JSON nella definizione di un'attività di copia, vedere le [attività di spostamento dei dati](data-factory-data-movement-activities.md). Per le descrizioni delle proprietà JSON supportate da BlobSource, vedere l'articolo relativo al [connettore BLOB di Azure](data-factory-azure-blob-connector.md). Per le descrizioni delle proprietà JSON supportate da SqlSink, vedere l'articolo relativo al [connettore del database SQL di Azure](data-factory-azure-sql-connector.md).
2. Eseguire hello comando toocreate hello data factory nella tabella seguente.

    ```PowerShell   
    New-AzureRmDataFactoryPipeline $df -File .\ADFTutorialPipeline.json
    ```

    Ecco l'output di esempio hello: 

    ```
    PipelineName      : ADFTutorialPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.PipelinePropertie
    ProvisioningState : Succeeded
    ```

**Congratulazioni.** Una data factory di Azure è stato creato con una pipeline toocopy dati da un database di SQL Azure tooan di archiviazione blob di Azure. 

## <a name="monitor-hello-pipeline"></a>Pipeline hello monitoraggio
In questo passaggio, utilizzare Azure PowerShell toomonitor cosa accade in un data factory di Azure.

1. Sostituire &lt;DataFactoryName&gt; con nome hello della data factory e l'esecuzione **Get AzureRmDataFactory**e assegnare hello output tooa $df variabile.

    ```PowerShell  
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name <DataFactoryName>
    ```

    ad esempio:
    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH0516
    ```
    
    Eseguire quindi il contenuto di stampa hello di hello toosee $df seguente output: 
    
    ```
    PS C:\ADFGetStartedPSH> $df
    
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DataFactoryId     : 6f194b34-03b3-49ab-8f03-9f8a7b9d3e30
    ResourceGroupName : ADFTutorialResourceGroup
    Location          : West US
    Tags              : {}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DataFactoryProperties
    ProvisioningState : Succeeded
    ```
2. Eseguire **Get AzureRmDataFactorySlice** tooget dettagli su tutte le sezioni di hello **OutputDataset**, ovvero il set di dati di hello output della pipeline hello.  

    ```PowerShell   
    Get-AzureRmDataFactorySlice $df -DatasetName OutputDataset -StartDateTime 2017-05-11T00:00:00Z
    ```

   Questa impostazione deve corrispondere hello **avviare** valore in formato JSON della pipeline hello. Dovrebbe essere 24 sezioni, una per ogni ora dalla Mezzanotte di hello odierna too12 STO di hello giorno successivo.

   Ecco tre sezioni di esempio dall'output di hello: 

    ``` 
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 11:00:00 PM
    End               : 5/12/2017 12:00:00 AM
    RetryCount        : 0
    State             : Ready
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 9:00:00 PM
    End               : 5/11/2017 10:00:00 PM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0   

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 8:00:00 PM
    End               : 5/11/2017 9:00:00 PM
    RetryCount        : 0
    State             : Waiting
    SubState          : ConcurrencyLimit
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. Eseguire **Get AzureRmDataFactoryRun** tooget hello dettagli dell'attività viene eseguita per un **specifico** sezione. Copiare il valore di data / ora hello dall'output di hello hello comando toospecify hello valore precedente per il parametro StartDateTime hello. 

    ```PowerShell  
    Get-AzureRmDataFactoryRun $df -DatasetName OutputDataset -StartDateTime "5/11/2017 09:00:00 PM"
    ```

   Ecco l'output di esempio hello: 

    ```
    Id                  : c0ddbd75-d0c7-4816-a775-704bbd7c7eab_636301332000000000_636301368000000000_OutputDataset
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : ADFTutorialDataFactoryPSH0516
    DatasetName         : OutputDataset
    ProcessingStartTime : 5/16/2017 8:00:33 PM
    ProcessingEndTime   : 5/16/2017 8:01:36 PM
    PercentComplete     : 100
    DataSliceStart      : 5/11/2017 9:00:00 PM
    DataSliceEnd        : 5/11/2017 10:00:00 PM
    Status              : Succeeded
    Timestamp           : 5/16/2017 8:00:33 PM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : CopyFromBlobToSQL
    PipelineName        : ADFTutorialPipeline
    Type                : Copy  
    ```

Vedere le [informazioni di riferimento per i cmdlet di Data factory](/powershell/module/azurerm.datafactories) per la documentazione completa sui cmdlet di Data factory.

## <a name="summary"></a>Riepilogo
In questa esercitazione è creato un Azure factory toocopy dati da un database di SQL Azure tooan blob di Azure. È stato utilizzato PowerShell toocreate hello data factory, i servizi collegati, i set di dati e una pipeline. Ecco i passaggi di alto livello hello effettuati in questa esercitazione:  

1. Creare un'istanza di Azure **Data Factory**.
2. Creare **servizi collegati**:

   a. Un **di archiviazione di Azure** collegati toolink service account di archiviazione Azure che contiene i dati di input.     
   b. Un **SQL Azure** collegati toolink servizio database di SQL che contiene i dati di output di hello.
3. Creare **set di dati** che descrivono dati di input e di output per le pipeline.
4. Creare un **pipeline** con **attività di copia**, con **BlobSource** come origine di hello e **SqlSink** come sink hello.

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione sono stati usati l'archivio BLOB di Azure come archivio dati di origine e un database SQL di Azure come archivio dati di destinazione in un'operazione di copia. Hello nella tabella seguente fornisce un elenco di archivi di dati supportato come origini e destinazioni da attività di copia hello: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn su come archiviano dati toocopy da e verso un tipo di dati, fare clic su collegamento hello per hello archivio di dati nella tabella hello. 

