---
title: "aaaUse attività personalizzate in una pipeline di Data Factory di Azure"
description: "Informazioni su come le attività personalizzate toocreate e utilizzarli in una pipeline di Data Factory di Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 8dd7ba14-15d2-4fd9-9ada-0b2c684327e9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 23e33727b2160541ab40938ffd911fdd484b3daa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-custom-activities-in-an-azure-data-factory-pipeline"></a>Usare attività personalizzate in una pipeline di Azure Data Factory

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Attività Hive](data-factory-hive-activity.md) 
> * [Attività di Pig](data-factory-pig-activity.md)
> * [Attività MapReduce](data-factory-map-reduce.md)
> * [Attività di Hadoop Streaming](data-factory-hadoop-streaming-activity.md)
> * [Attività Spark](data-factory-spark.md)
> * [Attività di esecuzione batch di Machine Learning](data-factory-azure-ml-batch-execution-activity.md)
> * [Attività della risorsa di aggiornamento di Machine Learning](data-factory-azure-ml-update-resource-activity.md)
> * [Attività stored procedure](data-factory-stored-proc-activity.md)
> * [Attività U-SQL di Data Lake Analytics](data-factory-usql-activity.md)
> * [Attività personalizzata di .NET](data-factory-use-custom-activities.md)

In una pipeline di Azure Data Factory è possibile usare due tipi di attività.

- [Le attività di spostamento dati](data-factory-data-movement-activities.md) dati toomove tra [archivi di dati di origine e sink supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).
- [Attività di trasformazione dei dati](data-factory-data-transformation-activities.md) tootransform dati utilizzando i servizi, ad esempio HDInsight di Azure, il Batch di Azure e Azure Machine Learning di calcolo. 

i dati toomove in o da un archivio dati che non supporta la Data Factory, creare un **attività personalizzata** con la propria spostamento logica e utilizzare hello attività di dati in una pipeline. Analogamente, tootransform/elaborare i dati in modo che non è supportato da Data Factory, creare un'attività personalizzata con la logica di trasformazione di dati e utilizzare attività hello in una pipeline. 

È possibile configurare un toorun di attività personalizzata in un **Azure Batch** pool di macchine virtuali o basato su Windows **Azure HDInsight** cluster. Quando si usa Azure Batch, è possibile usare solo un pool esistente di Azure Batch. Quando invece si usa HDInsight, è possibile usare un cluster HDInsight esistente o un cluster creato automaticamente su richiesta in fase di esecuzione.  

Hello procedura riportata di seguito vengono fornite istruzioni dettagliate per la creazione di un'attività personalizzata di .NET e l'utilizzo di attività personalizzata hello in una pipeline. procedura dettagliata Hello viene utilizzato un **Azure Batch** servizio collegato. toouse HDInsight di Azure un servizio collegato, invece, si crea un servizio collegato di tipo **HDInsight** (il propria cluster HDInsight) o **HDInsightOnDemand** (Data Factory crea un cluster HDInsight su richiesta). Configurare quindi hello toouse attività personalizzata del servizio collegato di HDInsight. Vedere [servizi collegati HDInsight di Azure usare](#use-hdinsight-compute-service) per ulteriori informazioni sull'utilizzo di attività personalizzata hello toorun di Azure HDInsight.

> [!IMPORTANT]
> - attività .NET personalizzata Hello eseguito solo in cluster HDInsight basati su Windows. Una soluzione alternativa per questa limitazione è hello toouse codice personalizzato Java mappa ridurre attività toorun in un cluster HDInsight basati su Linux. Un'altra opzione è toouse un pool di Azure Batch di attività personalizzate di macchine virtuali toorun invece di usare un cluster HDInsight.
> - Non è possibile toouse un Gateway di gestione di dati da origini dati locali tooaccess attività personalizzata. Attualmente, [Gateway di gestione dati](data-factory-data-management-gateway.md) supporta solo attività di copia hello e attività di stored procedure nella Data Factory.   

## <a name="walkthrough-create-a-custom-activity"></a>Procedura dettagliata: creare un'attività personalizzata
### <a name="prerequisites"></a>Prerequisiti
* Visual Studio 2012/2013/2015
* Scaricare e installare [.NET SDK di Azure](https://azure.microsoft.com/downloads/)

### <a name="azure-batch-prerequisites"></a>Prerequisiti di Azure Batch
In questa procedura dettagliata hello, vengono eseguite attività .NET personalizzate usando Azure Batch come una risorsa di calcolo. **Azure Batch** è una piattaforma di servizio per l'esecuzione parallela su larga scala e ad alte prestazioni (HPC) applicazioni in modo efficiente nel cloud di hello di elaborazione. Azure Batch pianifica toorun di lavoro a utilizzo intensivo di calcolo in un oggetto gestito **raccolta di macchine virtuali**, e possa automaticamente la scala di calcolo esigenze hello toomeet di risorse dei processi. Vedere [nozioni di base di Azure Batch] [ batch-technical-overview] articolo per una panoramica dettagliata di hello servizio Azure Batch.

Per l'esercitazione hello, creare un account Azure Batch con un pool di macchine virtuali. Ecco i passaggi di hello:

1. Creare un **account Azure Batch** utilizzando hello [portale di Azure](http://portal.azure.com). Per istruzioni, vedere l'articolo su come [creare e gestire un account Azure Batch][batch-create-account].
2. Annotando il nome dell'account Azure Batch hello, chiave dell'account, URI e nome del pool. È necessario toocreate un servizio collegato Azure Batch.
    1. Nella home page a hello per account Azure Batch, viene visualizzato un **URL** in hello seguente formato: `https://myaccount.westus.batch.azure.com`. In questo esempio, **myaccount** nome hello di hello account Azure Batch. URI è utilizzato nella definizione di servizio collegato hello è hello URL senza nome hello dell'account di hello. Ad esempio: `https://<region>.batch.azure.com`.
    2. Fare clic su **chiavi** nel menu a sinistra di hello e hello copia **chiave di accesso primaria**.
    3. toouse un pool esistente, fare clic su **pool** menu hello e annotare hello **ID** del pool di hello. Se non si dispone di un pool esistente, è possibile spostare toohello successivo.     
2. Creare un **pool di Azure Batch**.

   1. In hello [portale di Azure](https://portal.azure.com), fare clic su **Sfoglia** in hello menu a sinistra, quindi fare clic su **account Batch**.
   2. Selezionare il hello tooopen di account Azure Batch **Account Batch** blade.
   3. Fare clic sul riquadro **Pool** .
   4. In hello **pool** pannello, fare clic su Aggiungi pulsante nella barra degli strumenti di hello tooadd un pool.
      1. Immettere un ID per il pool di hello (ID pool di applicazioni). Hello nota **ID del pool di hello**; è necessario durante la creazione di soluzioni di Data Factory hello.
      2. Specificare **Windows Server 2012 R2** per l'impostazione di hello famiglia di sistemi operativi.
      3. Selezionare un **piano tariffario per il nodo**.
      4. Immettere **2** come valore per hello **destinazione dedicato** impostazione.
      5. Immettere **2** come valore per hello **Max attività per ogni nodo** impostazione.
   5. Fare clic su **OK** pool hello toocreate.
   6. Annotare hello **ID** del pool di hello. 



### <a name="high-level-steps"></a>Procedure generali
Di seguito sono hello due operazioni eseguite come parte di questa procedura dettagliata: 

1. Creare un'attività personalizzata contenente una semplice logica di trasformazione/elaborazione dei dati.
2. Creare una data factory di Azure con una pipeline che utilizza l'attività personalizzata hello.

### <a name="create-a-custom-activity"></a>Creare un'attività personalizzata
creare un'attività personalizzata di .NET, toocreate un **libreria di classi .NET** progetto con una classe che implementa che **IDotNetActivity** interfaccia. Questa interfaccia ha un solo metodo, [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) , e la relativa firma è:

```csharp
public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
```


metodo Hello accetta quattro parametri:

- **linkedServices**. Questa proprietà è un elenco enumerabile di servizi di archiviazione di dati collegato a cui fa riferimento dal set di dati di input/output per l'attività hello.   
- **datasets**. Questa proprietà è un elenco di set di dati di input/output per l'attività hello enumerabile. È possibile utilizzare questo percorsi hello tooget di parametro e gli schemi definiti dal set di dati di input e output.
- **activity**. Questa proprietà rappresenta l'attività corrente hello. Può essere utilizzato tooaccess le proprietà estese associate attività personalizzata hello. Per i dettagli, vedere [Accedere a tutte le proprietà estese](#access-extended-properties).
- **logger**. Questo oggetto consente di scrivere commenti di debug di tale area nel Registro di hello utente per la pipeline di hello.

metodo Hello restituisce un dizionario che può essere attività personalizzate toochain utilizzati insieme in futuro hello. Questa funzionalità non ancora implementata, pertanto restituire un dizionario vuoto da metodo hello.  

### <a name="procedure"></a>Procedura
1. Creare un progetto **Libreria di classi .NET** .
   <ol type="a">
     <li>Avviare <b>Visual Studio 2017</b>, <b>Visual Studio 2015</b>, <b>Visual Studio 2013</b> oppure <b>Visual Studio 2012</b>.</li>
     <li>Fare clic su <b>File</b>, punto troppo<b>New</b>, fare clic su <b>progetto</b>.</li>
     <li>Espandere <b>Modelli</b> e quindi selezionare <b>Visual C#</b>. In questa procedura dettagliata, si utilizza c#, ma è possibile utilizzare qualsiasi attività personalizzate .NET language toodevelop hello.</li>
     <li>Selezionare <b>libreria di classi</b> dall'elenco di hello dei tipi di progetto su hello destra. In Visual Studio 2017, scegliere <b>Libreria di classi (.NET Framework)</b> </li>
     <li>Immettere <b>MyDotNetActivity</b> per hello <b>nome</b>.</li>
     <li>Selezionare <b>C:\ADFGetStarted</b> per hello <b>percorso</b>.</li>
     <li>Fare clic su <b>OK</b> progetto hello toocreate.</li>
   </ol>
2.Fare clic su **strumenti**, punto troppo**Gestione pacchetti NuGet**, fare clic su **Package Manager Console**.
3. Nella Console di gestione pacchetti hello, eseguire hello successivo comando tooimport **Microsoft.Azure.Management.DataFactories**.

    ```PowerShell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. Hello importazione **di archiviazione di Azure** pacchetto NuGet nel progetto toohello.

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    > [!IMPORTANT]
    > Utilità di avvio del servizio Data Factory richiede la versione di hello 4.3 di Windowsazure. Se si aggiunge un riferimento tooa ultima versione di assembly di archiviazione di Azure nel progetto di attività personalizzata, viene visualizzato un errore durante l'esecuzione di attività hello. Errore di hello tooresolve, vedere [isolamento](#appdomain-isolation) sezione. 
5. Aggiungere il seguente hello **utilizzando** istruzioni toohello file sorgente hello progetto.

    ```csharp

    // Comment these lines if using VS 2017
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    // --------------------

    // Comment these lines if using <= VS 2015
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    // ---------------------

    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;

    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. Modifica nome hello di hello **dello spazio dei nomi** troppo**MyDotNetActivityNS**.

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. Modificare il nome di hello della classe hello troppo**MyDotNetActivity** ed eseguirne la derivazione da hello **IDotNetActivity** interfaccia come illustrato nel seguente frammento di codice hello:

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. Hello implementare (Aggiungi) **Execute** metodo hello **IDotNetActivity** interfaccia toohello **MyDotNetActivity** classe e copia hello metodo toohello codice di esempio seguente.

    Hello seguente conta hello numero di occorrenze del termine di ricerca hello ("Microsoft") in ogni blob associato a una sezione di dati.

    ```csharp
    /// <summary>
    /// Execute method is hello only method of IDotNetActivity interface you must implement.
    /// In this sample, hello method invokes hello Calculate method tooperform hello core logic.  
    /// </summary>
    
    public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
    {
        // get extended properties defined in activity JSON definition
        // (for example: SliceStart)
        DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
        string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];
    
        // toolog information, use hello logger object
        // log all extended properties            
        IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
        logger.Write("Logging extended properties if any...");
        foreach (KeyValuePair<string, string> entry in extendedProperties)
        {
            logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
        }
    
        // linked service for input and output data stores
        // in this example, same storage is used for both input/output
        AzureStorageLinkedService inputLinkedService;

        // get hello input dataset
        Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
        // declare variables toohold type properties of input/output datasets
        AzureBlobDataset inputTypeProperties, outputTypeProperties;
        
        // get type properties from hello dataset object
        inputTypeProperties = inputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // log linked services passed in linkedServices parameter
        // you will see two linked services of type: AzureStorage
        // one for input dataset and hello other for output dataset 
        foreach (LinkedService ls in linkedServices)
            logger.Write("linkedService.Name {0}", ls.Name);
    
        // get hello first Azure Storate linked service from linkedServices object
        // using First method instead of Single since we are using hello same
        // Azure Storage linked service for input and output.
        inputLinkedService = linkedServices.First(
            linkedService =>
            linkedService.Name ==
            inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
            as AzureStorageLinkedService;
    
        // get hello connection string in hello linked service
        string connectionString = inputLinkedService.ConnectionString;
    
        // get hello folder path from hello input dataset definition
        string folderPath = GetFolderPath(inputDataset);
        string output = string.Empty; // for use later.
    
        // create storage client for input. Pass hello connection string.
        CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
        CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
        // initialize hello continuation token before using it in hello do-while loop.
        BlobContinuationToken continuationToken = null;
        do
        {   // get hello list of input blobs from hello input storage client object.
            BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                     true,
                                     BlobListingDetails.Metadata,
                                     null,
                                     continuationToken,
                                     null,
                                     null);
    
            // Calculate method returns hello number of occurrences of
            // hello search term (“Microsoft”) in each blob associated
               // with hello data slice. definition of hello method is shown in hello next step.
    
            output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
        } while (continuationToken != null);
    
        // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
        Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);

        // get type properties for hello output dataset
        outputTypeProperties = outputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // get hello folder path from hello output dataset definition
        folderPath = GetFolderPath(outputDataset);

        // log hello output folder path 
        logger.Write("Writing blob toohello folder: {0}", folderPath);
    
        // create a storage object for hello output blob.
        CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
        // write hello name of hello file.
        Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
        // log hello output file name
        logger.Write("output blob URI: {0}", outputBlobUri.ToString());

        // create a blob and upload hello output text.
        CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
        logger.Write("Writing {0} toohello output blob", output);
        outputBlob.UploadText(output);
    
        // hello dictionary can be used toochain custom activities together in hello future.
        // This feature is not implemented yet, so just return an empty dictionary.  
    
        return new Dictionary<string, string>();
    }
    ```
9. Aggiungere hello dei seguenti metodi di supporto: 

    ```csharp
    /// <summary>
    /// Gets hello folderPath value from hello input/output dataset.
    /// </summary>
    
    private static string GetFolderPath(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }

        // get type properties of hello dataset 
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello folder path found in hello type properties
        return blobDataset.FolderPath;
    }
    
    /// <summary>
    /// Gets hello fileName value from hello input/output dataset.   
    /// </summary>
    
    private static string GetFileName(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }
    
        // get type properties of hello dataset
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello blob/file name in hello type properties
        return blobDataset.FileName;
    }
    
    /// <summary>
    /// Iterates through each blob (file) in hello folder, counts hello number of instances of search term in hello file,
    /// and prepares hello output text that is written toohello output blob.
    /// </summary>
    
    public static string Calculate(BlobResultSegment Bresult, IActivityLogger logger, string folderPath, ref BlobContinuationToken token, string searchTerm)
    {
        string output = string.Empty;
        logger.Write("number of blobs found: {0}", Bresult.Results.Count<IListBlobItem>());
        foreach (IListBlobItem listBlobItem in Bresult.Results)
        {
            CloudBlockBlob inputBlob = listBlobItem as CloudBlockBlob;
            if ((inputBlob != null) && (inputBlob.Name.IndexOf("$$$.$$$") == -1))
            {
                string blobText = inputBlob.DownloadText(Encoding.ASCII, null, null, null);
                logger.Write("input blob text: {0}", blobText);
                string[] source = blobText.Split(new char[] { '.', '?', '!', ' ', ';', ':', ',' }, StringSplitOptions.RemoveEmptyEntries);
                var matchQuery = from word in source
                                 where word.ToLowerInvariant() == searchTerm.ToLowerInvariant()
                                 select word;
                int wordCount = matchQuery.Count();
                output += string.Format("{0} occurrences(s) of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
            }
        }
        return output;
    }
    ```

    Hello GetFolderPath metodo restituisce hello percorso toohello cartella hello set di dati punta tooand hello GetFileName restituisce hello nome del metodo hello/file blob hello per i punti di set di dati. Se si havefolderPath definisce l'utilizzo di variabili, ad esempio {Year}, {Month,} restituisce {Day} e così via, il metodo hello hello stringa perché è senza sostituirli con i valori di runtime. Per i dettagli sull'accesso a SliceStart, SliceEnd e così via, vedere [Accedere a tutte le proprietà estese](#access-extended-properties) .    

    ```JSON
    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "adftutorial/inputfolder/",
    ```

    metodo Calculate Hello calcola il numero di hello di istanze della parola chiave Microsoft nei file di input hello (BLOB nella cartella hello). il termine di ricerca Hello ("Microsoft") è hardcoded nel codice hello.
10. Compilare il progetto hello. Fare clic su **compilare** menu hello e fare clic su **Compila soluzione**.

    > [!IMPORTANT]
    > Versione set 4.5.2 di .NET Framework come framework di destinazione hello per il progetto: progetto hello di mouse e scegliere **proprietà** framework di destinazione tooset hello. Data factory non supporta le attività personalizzate compilate in versioni di .NET Framework successive alla 4.5.2.

11. Avviare **Esplora**e passare troppo**bin\debug** o **bin\release** cartella in base al tipo di hello di compilazione.
12. Creare un file zip **MyDotNetActivity.zip** che contiene tutti i file binari hello in hello <project folder>nella cartella \bin\Debug. Includere hello **MyDotNetActivity.pdb** file in modo che sia possibile ottenere ulteriori dettagli, ad esempio il numero di riga nel codice sorgente hello che ha causato il problema di hello se si è verificato un errore. 

    > [!IMPORTANT]
    > Tutti hello file nel file zip hello per attività personalizzata hello deve essere in hello **livello principale** con nessun le sottocartelle.

    ![File di output binari](./media/data-factory-use-custom-activities/Binaries.png)
14. Se non è già presente, creare un contenitore BLOB denominato **customactivitycontainer**. 
15. Caricare MyDotNetActivity.zip come un customactivitycontainer toohello blob in un **generica** archiviazione blob di Azure (archiviazione Blob non hot/cool) che fa riferimento AzureStorageLinkedService.  

> [!IMPORTANT]
> Se si aggiunge questa soluzione di tooa progetto attività .NET in Visual Studio contenente un progetto di Data Factory e aggiunta un progetto di attività too.NET riferimento dal progetto di applicazione hello Data Factory, non è necessario tooperform hello ultimi due passaggi per la creazione manuale file zip Hello e caricarlo nell'archiviazione blob di Azure generico toohello. Quando si pubblicano le entità di Data Factory utilizzando Visual Studio, questi passaggi vengono eseguiti automaticamente dal processo di pubblicazione hello. Per altre informazioni, vedere la sezione [Data Factory project in Visual Studio](#data-factory-project-in-visual-studio) (Progetto Data Factory in Visual Studio).

## <a name="create-a-pipeline-with-custom-activity"></a>Creare una pipeline con attività personalizzate
Aver creato un'attività personalizzata e caricato il file zip hello con il contenitore di blob tooa i file binari in un **generica** Account di archiviazione Azure. In questa sezione creare una data factory di Azure con una pipeline che utilizza l'attività personalizzata hello.

set di dati input Hello per attività personalizzata hello rappresenta BLOB (file) nella cartella customactivityinput hello del contenitore adftutorial nell'archiviazione blob hello. set di dati per l'attività hello output di Hello rappresenta il BLOB di output nella cartella customactivityoutput hello del contenitore adftutorial nell'archiviazione blob hello.

Creare **file.txt** file con hello seguente il contenuto e caricarla troppo**customactivityinput** cartella di hello **adftutorial** contenitore. Creare il contenitore di adftutorial hello se non esiste già. 

```
test custom activity Microsoft test custom activity Microsoft
```

cartella input Hello corrisponde sezione tooa nella Data Factory di Azure, anche se la cartella hello dispone di due o più file. Quando ogni sezione venga elaborato dalla pipeline di hello, attività personalizzata hello scorre tutti i BLOB hello nella cartella di input hello per tale sezione.

Viene visualizzato un file con nella cartella adftutorial\customactivityoutput hello di output con una o più righe (uguale al numero di BLOB nella cartella input hello):

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
```


Di seguito sono descritte hello che operazioni in questa sezione:

1. Creare una **data factory**.
2. Creare **servizi collegati** per pool di applicazioni Azure Batch hello di macchine virtuali in cui hello attività personalizzata viene eseguita e hello archiviazione di Azure che contiene il BLOB di input/output di hello.
3. Creazione di input e output **set di dati** che rappresentano l'input e output di attività personalizzata hello.
4. Creare un **pipeline** che usa l'attività personalizzata hello.

> [!NOTE]
> Creare hello **file.txt** e caricare il contenitore di blob tooa se non è già fatto. Vedere le istruzioni nella precedente sezione hello.   

### <a name="step-1-create-hello-data-factory"></a>Passaggio 1: Creare hello data factory
1. Dopo l'accesso toohello portale di Azure, hello alla procedura seguente:
   1. Fare clic su **NEW** nel menu di sinistra hello.
   2. Fare clic su **dati + Analitica** in hello **New** blade.
   3. Fare clic su **Data Factory** su hello **analitica dati** blade.
   
    ![Menu Nuova Azure Data Factory](media/data-factory-use-custom-activities/new-azure-data-factory-menu.png)
2. In hello **nuova data factory** pannello immettere **CustomActivityFactory** per hello Name. nome Hello di hello Azure data factory deve essere globalmente univoco. Se viene visualizzato l'errore hello: **"CustomActivityFactory" nome della Data factory non è disponibile**, modificare il nome di hello della data factory di hello (ad esempio, **yournameCustomActivityFactory**) e provare a creare nuovo.

    ![Pannello Nuova Azure Data Factory](media/data-factory-use-custom-activities/new-azure-data-factory-blade.png)
3. Fare clic su **NOME DEL GRUPPO DI RISORSE**e selezionare un gruppo di risorse esistente o crearne uno.
4. Verificare che si sta utilizzando hello corretto **sottoscrizione** e **area** in cui si desidera hello data factory toobe creato.
5. Fare clic su **crea** su hello **nuova data factory** blade.
6. Vedrai data factory di hello viene creato nel hello **Dashboard** di hello portale di Azure.
7. Dopo l'hello data factory è stata creata correttamente, vengono visualizzati pannello Data Factory di hello, che mostra contenuto della data factory di hello hello.
    
    ![Pannello Data factory](media/data-factory-use-custom-activities/data-factory-blade.png)

### <a name="step-2-create-linked-services"></a>Passaggio 2: Creare servizi collegati
Servizi collegati collegano archivi dati o servizi tooan data factory di Azure di calcolo. In questo passaggio è collegare l'account di archiviazione di Azure e la data factory di Azure Batch account tooyour.

#### <a name="create-azure-storage-linked-service"></a>Creare il servizio collegato Archiviazione di Azure
1. Fare clic su hello **autore e distribuire** riquadro hello **DATA FACTORY** pannello **CustomActivityFactory**. Vedrai hello Editor delle Data Factory.
2. Fare clic su **nuovo archivio dati** hello barra dei comandi e scegliere **archiviazione di Azure**. Dovrebbe essere hello script JSON per la creazione di una risorsa di archiviazione di Azure il servizio nell'editor di hello collegato.
    
    ![Nuovo archivio dati - Archiviazione di Azure](media/data-factory-use-custom-activities/new-data-store-menu.png)
3. Sostituire `<accountname>` con il nome dell'account di archiviazione di Azure e `<accountkey>` con la chiave di accesso di hello account di archiviazione di Azure. toolearn modalità di accesso di archiviazione di tooget chiave, vedere [visualizzazione, copia e l'archiviazione di rigenerare le chiavi di accesso](../storage/common/storage-create-storage-account.md#manage-your-storage-account).

    ![Servizio collegato Archiviazione di Azure](media/data-factory-use-custom-activities/azure-storage-linked-service.png)
4. Fare clic su **Distribuisci** sul comando hello barra toodeploy hello collegato servizio.

#### <a name="create-azure-batch-linked-service"></a>Creare il servizio collegato Azure Batch
1. Nell'Editor delle Data Factory hello, fare clic su **... Ulteriori** nella barra dei comandi di hello, fare clic su **nuovo calcolo**, quindi selezionare **Azure Batch** dal menu di hello.

    ![Nuovo calcolo - Azure Batch](media/data-factory-use-custom-activities/new-azure-compute-batch.png)
2. Apportare hello modifiche toohello JSON script seguente:

   1. Specificare il nome di account Azure Batch per hello **accountName** proprietà. Hello **URL** da hello **pannello account Azure Batch** in hello seguente formato: `http://accountname.region.batch.azure.com`. Per hello **batchUri** proprietà hello JSON, è necessario tooremove `accountname.` da hello URL e l'utilizzo di hello `accountname` per hello `accountName` proprietà JSON.
   2. Specificare una chiave dell'account Azure Batch hello per hello **accessKey** proprietà.
   3. Specificare il nome di hello del pool di hello creato come parte dei prerequisiti per hello **poolName** proprietà. È anche possibile specificare ID hello del pool di hello anziché il nome di hello del pool di hello.
   4. Specificare l'URI del Batch di Azure per hello **batchUri** proprietà. Esempio: `https://westus.batch.azure.com`.  
   5. Specificare hello **AzureStorageLinkedService** per hello **linkedServiceName** proprietà.

        ```json
        {
         "name": "AzureBatchLinkedService",
         "properties": {
           "type": "AzureBatch",
           "typeProperties": {
             "accountName": "myazurebatchaccount",
             "batchUri": "https://westus.batch.azure.com",
             "accessKey": "<yourbatchaccountkey>",
             "poolName": "myazurebatchpool",
             "linkedServiceName": "AzureStorageLinkedService"
           }
         }
        }
        ```

       Per hello **poolName** proprietà, è inoltre possibile specificare l'ID di hello del pool di hello anziché il nome di hello del pool di hello.

      > [!IMPORTANT]
      > Hello servizio Data Factory non supporta un'opzione su richiesta per il Batch di Azure a quanto accade per HDInsight. È possibile usare solo il proprio pool di Batch di Azure in una data factory di Azure.   
    

### <a name="step-3-create-datasets"></a>Passaggio 3: Creare set di dati
In questo passaggio, creare set di dati toorepresent input e i dati di output.

#### <a name="create-input-dataset"></a>Creare set di dati di input
1. In hello **Editor** per hello Data Factory, fare clic su **... Ulteriori** nella barra dei comandi di hello, fare clic su **nuovo set di dati**, quindi selezionare **archiviazione Blob di Azure** dal menu a discesa hello.
2. Sostituire hello JSON nel riquadro di destra hello con hello frammento di codice JSON seguente:

    ```json
    {
     "name": "InputDataset",
     "properties": {
         "type": "AzureBlob",
         "linkedServiceName": "AzureStorageLinkedService",
         "typeProperties": {
             "folderPath": "adftutorial/customactivityinput/",
             "format": {
                 "type": "TextFormat"
             }
         },
         "availability": {
             "frequency": "Hour",
             "interval": 1
         },
         "external": true,
         "policy": {}
     }
    }
    ```

   Più avanti in questa procedura dettagliata viene creata una pipeline con ora di inizio: 2016-11-16T00:00:00Z e ora di fine: 2016-11-16T05:00:00Z. È pianificato tooproduce dati ogni ora, pertanto vi sono cinque intervalli di input/output (tra **00**: 00:00 -> **05**: 00:00).

   Hello **frequenza** e **intervallo** per hello di un set di dati dell'input è troppo**ora** e **1**, il che significa che hello input sezione è disponibile ogni ora. In questo esempio, è hello stesso file (file. txt) in intputfolder hello.

   Di seguito sono ora di inizio hello per ogni sezione, rappresentata dalla variabile di sistema SliceStart in hello sopra il frammento JSON.
3. Fare clic su **Distribuisci** hello toocreate barra degli strumenti e distribuire hello **InputDataset**. Assicurarsi di visualizzare hello **tabella CREATA correttamente** messaggio sulla barra del titolo hello di hello Editor.

#### <a name="create-an-output-dataset"></a>Creare un set di dati di output
1. In hello **editor Data Factory**, fare clic su **... Ulteriori** nella barra dei comandi di hello, fare clic su **nuovo set di dati**, quindi selezionare **archiviazione Blob di Azure**.
2. Sostituire script JSON hello nel riquadro di destra hello con hello lo script JSON seguente:

    ```JSON
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "{slice}.txt",
                "folderPath": "adftutorial/customactivityoutput/",
                "partitionedBy": [
                    {
                        "name": "slice",
                        "value": {
                            "type": "DateTime",
                            "date": "SliceStart",
                            "format": "yyyy-MM-dd-HH"
                        }
                    }
                ]
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```

     Percorso di output è **adftutorial/customactivityoutput/** e nome file di output è aaaa-MM-GG-HH.txt, dove AAAA-MM-GG-HH è hello anno, mese, data e ora della sezione hello in fase di produzione. Per informazioni dettagliate, vedere la [guida di riferimento per gli sviluppatori][adf-developer-reference].

    Un BLOB o file di output viene generato per ogni sezione di input. Ecco come viene denominato il file di output per ogni sezione. Tutti i file di output di hello vengono generati in una cartella di output: **adftutorial\customactivityoutput**.

   | Sezione | Ora di inizio | File di output |
   |:--- |:--- |:--- |
   | 1 |2016-11-16T00:00:00 |2016-11-16-00.txt |
   | 2 |2016-11-16T01:00:00 |2016-11-16-01.txt |
   | 3 |2016-11-16T02:00:00 |2016-11-16-02.txt |
   | 4 |2016-11-16T03:00:00 |2016-11-16-03.txt |
   | 5 |2016-11-16T04:00:00 |2016-11-16-04.txt |

    Tenere presente che tutti i file hello in una cartella di input sono parte di una sezione con ora di inizio hello indicato in precedenza. Durante l'elaborazione di questa sezione, attività personalizzata hello esamina ogni file e produce una riga nel file di output di hello con numero di hello di occorrenze del termine di ricerca ("Microsoft"). Se sono presenti tre file in CartellaInput hello, sono presenti tre righe nel file di output di hello per ogni sezione oraria: 2016-11-16-00.txt 2016-11-16:01:00:00.txt, e così via.
3. hello toodeploy **OutputDataset**, fare clic su **Distribuisci** hello barra dei comandi.

### <a name="create-and-run-a-pipeline-that-uses-hello-custom-activity"></a>Creare ed eseguire una pipeline che utilizza l'attività personalizzata hello
1. Nell'Editor delle Data Factory hello, fare clic su **... Ulteriori**, quindi selezionare **nuova pipeline** hello barra dei comandi. 
2. Sostituire hello JSON nel riquadro di destra hello con hello lo script JSON seguente:

    ```JSON
    {
      "name": "ADFTutorialPipelineCustom",
      "properties": {
        "description": "Use custom activity",
        "activities": [
          {
            "Name": "MyDotNetActivity",
            "Type": "DotNetActivity",
            "Inputs": [
              {
                "Name": "InputDataset"
              }
            ],
            "Outputs": [
              {
                "Name": "OutputDataset"
              }
            ],
            "LinkedServiceName": "AzureBatchLinkedService",
            "typeProperties": {
              "AssemblyName": "MyDotNetActivity.dll",
              "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
              "PackageLinkedService": "AzureStorageLinkedService",
              "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
              "extendedProperties": {
                "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
              }
            },
            "Policy": {
              "Concurrency": 2,
              "ExecutionPriorityOrder": "OldestFirst",
              "Retry": 3,
              "Timeout": "00:30:00",
              "Delay": "00:00:00"
            }
          }
        ],
        "start": "2016-11-16T00:00:00Z",
        "end": "2016-11-16T05:00:00Z",
        "isPaused": false
      }
    }
    ```

    Si noti hello seguenti punti:

   * **Concorrenza** è troppo**2** in modo che le due sezioni vengono elaborate in parallelo da 2 macchine virtuali nel pool di hello Azure Batch.
   * È un'attività nella sezione attività hello ed è di tipo: **DotNetActivity**.
   * **AssemblyName** è impostato il nome toohello di hello DLL: **MyDotnetActivity.dll**.
   * **Punto di ingresso** è troppo**MyDotNetActivityNS.MyDotNetActivity**.
   * **PackageLinkedService** è troppo**AzureStorageLinkedService** che punta toohello archiviazione di blob che contiene i file zip di attività personalizzata hello. Se si utilizza input/output di diversi account di archiviazione di Azure per file e hello file zip di attività personalizzata, si crea un altro servizio collegato di archiviazione di Azure. Questo articolo si presuppone che si sta utilizzando hello stesso account di archiviazione di Azure.
   * **PackageFile** è troppo**customactivitycontainer/MyDotNetActivity.zip**. È in formato hello: containerforthezip/nameofthezip.zip.
   * attività personalizzata Hello accetta **InputDataset** come input e **OutputDataset** come output.
   * la proprietà linkedServiceName Hello di attività personalizzata hello punta toohello **AzureBatchLinkedService**, che indica Data Factory di Azure, tale attività personalizzata hello deve toorun nelle macchine virtuali di Azure Batch.
   * **isPaused** impostata troppo**false** per impostazione predefinita. pipeline Hello verrà eseguito immediatamente in questo esempio perché l'inizio delle sezioni hello in hello precedente. È possibile impostare la pipeline di hello toopause tootrue proprietà e impostarla toorestart toofalse indietro.
   * Hello **avviare** tempo e **fine** i tempi sono **cinque** ore separate e le sezioni vengono generate ogni ora, in modo da cinque sezioni vengono generate dalla pipeline hello.
3. pipeline di hello toodeploy, fare clic su **Distribuisci** hello barra dei comandi.

### <a name="monitor-hello-pipeline"></a>Pipeline hello monitoraggio
1. Nel Pannello di Data Factory hello in hello portale di Azure, fare clic su **diagramma**.

    ![Riquadro Diagramma](./media/data-factory-use-custom-activities/DataFactoryBlade.png)
2. Hello vista diagramma, fare clic su hello OutputDataset.

    ![Vista diagramma](./media/data-factory-use-custom-activities/diagram.png)
3. Dovrebbe essere che le sezioni di output cinque hello sono nello stato Ready hello. Se non sono in stato pronto hello, non sono state prodotte ancora. 

   ![Sezioni di output](./media/data-factory-use-custom-activities/OutputSlices.png)
4. Verificare che il file di output di hello vengono generato nell'archiviazione blob hello in hello **adftutorial** contenitore.

   ![output dell'attività personalizzata][image-data-factory-ouput-from-custom-activity]
5. Se si apre il file di output di hello, dovrebbe essere hello output toohello simile seguente output:

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
    ```
6. Hello utilizzare [portale di Azure] [ azure-preview-portal] toomonitor i cmdlet di Azure PowerShell o la data factory di pipeline e set di dati. È possibile visualizzare i messaggi da hello **ActivityLogger** nel codice hello di attività personalizzata hello nei registri di hello (in particolare 0.log utente) che è possibile scaricare dal portale di hello o utilizzo dei cmdlet.

   ![scaricare i log dall'attività personalizzata][image-data-factory-download-logs-from-custom-activity]

Vedere [Monitorare e gestire le pipeline](data-factory-monitor-manage-pipelines.md) per i passaggi dettagliati per il monitoraggio di set di dati e pipeline.      

## <a name="data-factory-project-in-visual-studio"></a>Progetto Data Factory in Visual Studio  
È possibile creare e pubblicare le entità di Data Factory usando Visual Studio anziché il portale di Azure. Per ulteriori informazioni sulla creazione e pubblicazione entità Data Factory con Visual Studio, vedere [compilare le pipeline prima con Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) e [copiare i dati da Blob di Azure tooAzure SQL](data-factory-copy-activity-tutorial-using-visual-studio.md) articoli.

Hello seguendo i passaggi aggiuntivi se si sta creando il progetto di Data Factory in Visual Studio:
 
1. Aggiungere hello Data Factory progetto toohello soluzione di Visual Studio contenente il progetto di attività personalizzata hello. 
2. Aggiungere un progetto di attività .NET toohello riferimento dal progetto di Data Factory hello. Fare clic sul progetto Data Factory, scegliere troppo**Aggiungi**, quindi fare clic su **riferimento**. 
3. In hello **Aggiungi riferimento** la finestra di dialogo, seleziona hello **MyDotNetActivity** del progetto e fare clic su **OK**.
4. Compilare e pubblicare la soluzione hello.

    > [!IMPORTANT]
    > Quando si pubblicano le entità di Data Factory, un file zip viene creato automaticamente ed è il contenitore di blob caricato toohello: customactivitycontainer. Se il contenitore di blob hello non esiste, viene automaticamente creato troppo.  


## <a name="data-factory-and-batch-integration"></a>Integrazione di Data Factory e Batch
Hello servizio Data Factory crea un processo in Batch di Azure con nome hello: **adf poolname: processo-xxx**. Fare clic su **processi** dal menu a sinistra di hello. 

![Azure Data Factory: processi di Batch](media/data-factory-use-custom-activities/data-factory-batch-jobs.png)

Per ogni esecuzione attività di una sezione viene creata un'attività. Se sono presenti toobe pronto cinque sezioni elaborate, cinque attività vengono create in questo processo. Se sono presenti più nodi di calcolo in hello pool Batch, è possono eseguire due o più sezioni in parallelo. Se il numero massimo di attività hello per ogni set di nodi di calcolo troppo > 1, è inoltre possibile avere più di una sezione in esecuzione su hello calcolo stesso.

![Azure Data Factory: attività processi di Batch](media/data-factory-use-custom-activities/data-factory-batch-job-tasks.png)

Hello seguente diagramma illustra la relazione hello tra le attività di Azure Data Factory e Batch.

![Data Factory e Batch](./media/data-factory-use-custom-activities/DataFactoryAndBatch.png)

## <a name="troubleshoot-failures"></a>Errori in fase di risoluzione dei problemi
La risoluzione dei problemi implica alcune tecniche di base:

1. Se viene visualizzato il seguente errore hello, si potrebbe utilizzando un'archiviazione blob Hot/Cool anziché un'archiviazione blob di Azure utilizzo generale. Caricare hello zip file tooa **generico Account di archiviazione di Azure**. 
 
    ```
    Error in Activity: Job encountered scheduling error. Code: BlobDownloadMiscError Category: ServerError Message: Miscellaneous error encountered while downloading one of hello specified Azure Blob(s).
    ``` 
2. Se viene visualizzato il seguente errore hello, confermare che il nome di hello del classe hello in hello CS corrispondenze hello nome di file specificato per hello **EntryPoint** proprietà in formato JSON della pipeline hello. In questa procedura dettagliata hello, nome della classe hello è: MyDotNetActivity e Ciao EntryPoint hello JSON è: MyDotNetActivityNS. **MyDotNetActivity**.

    ```
    MyDotNetActivity assembly does not exist or doesn't implement hello type Microsoft.DataFactories.Runtime.IDotNetActivity properly
    ```

   Se i nomi dei hello corrispondono, verificare che tutti i file binari hello attiva hello **cartella radice** del file zip hello. Ovvero, quando si apre file zip hello, si dovrebbe essere tutti i file hello nella cartella radice hello, non in tutte le relative sottocartelle.   
3. Se sezione input hello non è stato impostato troppo**pronto**, verificare che sia corretta struttura di cartelle di input di hello e **file.txt** presente nelle cartelle di input hello.
3. In hello **Execute** metodo dell'attività personalizzata, utilizzare hello **IActivityLogger** informazioni toolog oggetto che consente di risolvere i problemi. scaricare i messaggi Hello registrata nei file di log utente hello (uno o più file denominati: utente 0.log 1.log di utente, utente 2.log, ecc.).

   In hello **OutputDataset** pannello, fare clic su hello toosee di sezione hello **sezione dati** pannello per tale sezione. Verranno visualizzate le **esecuzioni di attività** per quella sezione. Verrà visualizzata un'attività eseguire per sezione hello. Se si fa clic su Esegui nella barra dei comandi di hello, è possibile avviare un'altra attività eseguita per hello stessa sezione.

   Quando si sceglie di eseguire attività di hello, vedrai hello **Dettagli esecuzione attività** pannello con un elenco di file di log. Vedere i messaggi registrati nel file user_0.log hello. Quando si verifica un errore, vengono visualizzati tre esecuzioni di attività perché il numero di tentativi di hello è too3 nella pipeline/attività hello JSON. Quando si sceglie di eseguire attività di hello, vedrai che è possibile esaminare l'errore hello tootroubleshoot i file di log hello.

   Nell'elenco di hello dei file di log, fare clic su hello **utente 0.log**. Nel riquadro di destra hello sono risultati hello dell'utilizzo di hello **IActivityLogger.Write** metodo. Se non si vedono tutti i messaggi, controllare se ci sono altri file di log denominati: user_1.log, user_2.log e così via. In caso contrario, il codice hello potrebbe non essere riuscita dopo l'ultimo messaggio registrato hello.

   Cercare anche eventuali messaggi di errore di sistema ed eccezioni nel file **system-0.log**.
4. Includere hello **PDB** file nel file zip hello in modo che i dettagli dell'errore hello presentano informazioni ad esempio **stack di chiamate** quando si verifica un errore.
5. Tutti hello file nel file zip hello per attività personalizzata hello deve essere in hello **livello principale** con nessun le sottocartelle.
6. Verificare che hello **assemblyName** (MyDotNetActivity.dll), **entryPoint**(MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer / MyDotNetActivity.zip) e **packageLinkedService** (deve puntare toohello **generica**archiviazione blob di Azure che contiene i file zip hello) sono impostate toocorrect valori.
7. Se è stata corretta una sezione di hello tooreprocess errore e si desidera, fare doppio clic su sezione hello hello **OutputDataset** pannello e fare clic su **eseguire**.
8. Se viene visualizzato il seguente errore hello, si utilizza il pacchetto di archiviazione di Azure hello di versione > 4.3.0. Utilità di avvio del servizio Data Factory richiede la versione di hello 4.3 di Windowsazure. Vedere [isolamento](#appdomain-isolation) sezione per risolvere se è necessario utilizzare hello versione più recente dell'assembly di archiviazione di Azure. 

    ```
    Error in Activity: Unknown error in module: System.Reflection.TargetInvocationException: Exception has been thrown by hello target of an invocation. ---> System.TypeLoadException: Could not load type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from assembly 'Microsoft.WindowsAzure.Storage, Version=4.3.0.0, Culture=neutral, 
    ```

    Se è possibile utilizzare la versione 4.3.0 hello del pacchetto di archiviazione di Azure, è possibile rimuovere hello riferimento tooAzure archiviazione pacchetto esistente di versione > 4.3.0. Eseguire quindi il comando seguente dalla Console di gestione pacchetti NuGet hello. 

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    Compilare il progetto hello. Eliminare assembly Azure.Storage di versione > 4.3.0 dalla cartella bin\Debug hello. Creare un file zip con i file binari e il file PDB hello. Sostituire il vecchio file zip di hello con nel contenitore blob hello (customactivitycontainer). Hello Riesegui sezioni che non è riuscita (fare clic sulla sezione e fare clic su Esegui).   
8. attività personalizzata Hello non utilizza hello **app** file dal pacchetto. Pertanto, se il codice legge tutte le stringhe di connessione dal file di configurazione di hello, non funziona in fase di esecuzione. Hello consigliata quando si utilizza Azure Batch è toohold tutti i segreti in un **KeyVault Azure**, utilizzare un hello tooprotect principale di servizio basata su certificati **keyvault**e distribuire il certificato di hello tooAzure pool Batch. attività personalizzate .NET Hello quindi possono accedere i segreti in hello KeyVault in fase di esecuzione. Questa soluzione è una soluzione generica e può essere ridimensionato tooany tipo di chiave privata, non solo stringa di connessione.

   È una soluzione più semplice (ma non consigliata): è possibile creare un **servizio collegato SQL Azure** con le impostazioni della stringa di connessione, creare un set di dati che utilizza hello servizio collegato e catena hello dataset come un set di dati di input fittizio attività di .NET toohello personalizzata. È possibile quindi hello accesso collegato stringa di connessione del servizio nel codice di attività personalizzata hello.  

## <a name="update-custom-activity"></a>Aggiornare l'attività personalizzata
Se si aggiorna il codice hello per attività personalizzata hello, compilarlo e caricare il file zip hello che contiene l'archiviazione blob di nuovo i file binari toohello.

## <a name="appdomain-isolation"></a>Isolamento di AppDomain
Vedere [Cross AppDomain esempio](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) che illustra come toocreate un'attività personalizzata che non è vincolato versioni tooassembly usate dal pulsante di visualizzazione della Data Factory hello (esempio: versione 4.3.0 Windowsazure v6.0.x newtonsoft. JSON, ecc.).

## <a name="access-extended-properties"></a>Accedere a tutte le proprietà estese
È possibile dichiarare le proprietà estese in formato JSON dell'attività hello, come illustrato nel seguente esempio hello:

```JSON
"typeProperties": {
  "AssemblyName": "MyDotNetActivity.dll",
  "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
  "PackageLinkedService": "AzureStorageLinkedService",
  "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
  "extendedProperties": {
    "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))",
    "DataFactoryName": "CustomActivityFactory"
  }
},
```


Nell'esempio hello, sono disponibili due proprietà estese: **SliceStart** e **DataFactoryName**. il valore di Hello per SliceStart si basa su una variabile di sistema SliceStart hello. Per un elenco delle variabili di sistema supportate, vedere [Pianificazione ed esecuzione con Data Factory](data-factory-functions-variables.md) . valore Hello DataFactoryName è tooCustomActivityFactory hardcoded.

tooaccess queste proprietà in hello estese **Execute** metodo, utilizzare codice simile toohello seguente codice:

```csharp
// tooget extended properties (for example: SliceStart)
DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];

// toolog all extended properties                               
IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
logger.Write("Logging extended properties if any...");
foreach (KeyValuePair<string, string> entry in extendedProperties)
{
    logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
}
```

## <a name="auto-scaling-of-azure-batch"></a>Scalabilità automatica di Azure Batch
È anche possibile creare un pool di Azure Batch con la funzionalità **Scalabilità automatica** . Ad esempio, è possibile creare un pool di batch di azure con macchine virtuali dedicate 0 e una formula di scalabilità automatica in base al numero di hello di attività in sospeso. 

formula di esempio Hello qui si ottiene hello seguente comportamento: quando viene creato inizialmente pool hello, inizia con 1 macchina virtuale. Metrica $PendingTasks definisce il numero di hello di attività in esecuzione + attivo (in coda) dello stato.  formula Hello trova numero medio di hello attività in sospeso in hello ultimi 180 secondi e imposta TargetDedicated di conseguenza. Assicura che TargetDedicated non vada mai oltre 25 macchine virtuali. In tal caso, come vengono inviate nuove attività, pool aumentano automaticamente e come attività di completamento, le macchine virtuali diventano disponibile uno alla volta e la scalabilità automatica hello compatta tali macchine virtuali. startingNumberOfVMs e maxNumberofVMs può essere adattato tooyour esigenze.

Formula di scalabilità automatica:

``` 
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
```

Per i dettagli, vedere [Ridimensionare automaticamente i nodi di calcolo in un pool di Azure Batch](../batch/batch-automatic-scaling.md) .

Se il pool di hello utilizza predefinito hello [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello servizio Batch può richiedere 15-30 minuti tooprepare hello VM prima di eseguire l'attività personalizzata hello.  Se il pool di hello sta utilizzando un diverso autoScaleEvaluationInterval, hello servizio Batch può assumere autoScaleEvaluationInterval + 10 minuti.

## <a name="use-hdinsight-compute-service"></a>Usare il servizio di calcolo di HDInsight
In questa procedura dettagliata hello, è stato utilizzato attività personalizzata hello toorun calcolo di Azure Batch. È possibile anche utilizzare un cluster HDInsight basati su Windows o Data Factory di creare cluster HDInsight basati su Windows su richiesta e dispone di attività personalizzata hello in esecuzione nel cluster HDInsight hello. Ecco i passaggi di alto livello hello per l'utilizzo di un cluster HDInsight.

> [!IMPORTANT]
> attività .NET personalizzata Hello eseguito solo in cluster HDInsight basati su Windows. Una soluzione alternativa per questa limitazione è hello toouse codice personalizzato Java mappa ridurre attività toorun in un cluster HDInsight basati su Linux. Un'altra opzione è toouse un pool di Azure Batch di attività personalizzate di macchine virtuali toorun invece di usare un cluster HDInsight.
 

1. Creare un servizio collegato Azure HDInsight.   
2. Servizio al posto di collegato di HDInsight utilizzare **AzureBatchLinkedService** in hello JSON di pipeline.

Se si desidera tootest con questa procedura dettagliata hello, modifica **avviare** e **fine** ore per la pipeline di hello in modo che è possibile testare uno scenario di hello con hello servizio Azure HDInsight.

#### <a name="create-azure-hdinsight-linked-service"></a>Creare un servizio collegato Azure HDInsight
Hello servizio Data Factory di Azure supporta la creazione di un cluster su richiesta e usarlo come dati di output tooprocess tooproduce input. È inoltre possibile utilizzare un cluster personale tooperform hello stesso. Quando si usa il cluster HDInsight su richiesta, viene creato un cluster per ogni sezione. Considerando che, se si utilizza un cluster HDInsight, cluster hello è pronto tooprocess hello sezione immediatamente. Pertanto, quando si utilizza cluster su richiesta, si potrebbero non visualizzare dati di output di hello più rapidamente quando si utilizza un cluster personale.

> [!NOTE]
> In fase di esecuzione, un'istanza di un'attività .NET viene eseguita solo su un nodo di lavoro nel cluster HDInsight hello. non può essere scalato toorun su più nodi. Più istanze di attività .NET è possono eseguire in parallelo in nodi diversi del cluster HDInsight hello.
>
>

##### <a name="toouse-an-on-demand-hdinsight-cluster"></a>toouse un cluster di HDInsight su richiesta
1. In hello **portale di Azure**, fare clic su **autore e distribuire** nella home page di hello Data Factory.
2. Nell'Editor delle Data Factory hello, fare clic su **nuovo calcolo** dal comando hello barra e selezionare **cluster HDInsight su richiesta** dal menu di hello.
3. Apportare hello modifiche toohello JSON script seguente:

   1. Per hello **clusterSize** proprietà, specificare le dimensioni di hello del cluster HDInsight hello.
   2. Per hello **timeToLive** proprietà, specificare quanto tempo cliente hello può essere inattivo prima che venga eliminato.
   3. Per hello **versione** proprietà, specificare la versione di HDInsight hello desiderato toouse. Se si esclude questa proprietà, viene utilizzata la versione più recente di hello.  
   4. Per hello **linkedServiceName**, specificare **AzureStorageLinkedService**.

        ```JSON
        {
           "name": "HDInsightOnDemandLinkedService",
           "properties": {
               "type": "HDInsightOnDemand",
               "typeProperties": {
                   "clusterSize": 4,
                   "timeToLive": "00:05:00",
                   "osType": "Windows",
                   "linkedServiceName": "AzureStorageLinkedService",
               }
           }
        }
        ```

    > [!IMPORTANT]
    > attività .NET personalizzata Hello eseguito solo in cluster HDInsight basati su Windows. Una soluzione alternativa per questa limitazione è hello toouse codice personalizzato Java mappa ridurre attività toorun in un cluster HDInsight basati su Linux. Un'altra opzione è toouse un pool di Azure Batch di attività personalizzate di macchine virtuali toorun invece di usare un cluster HDInsight.

4. Fare clic su **Distribuisci** sul comando hello barra toodeploy hello collegato servizio.

##### <a name="toouse-your-own-hdinsight-cluster"></a>toouse cluster HDInsight:
1. In hello **portale di Azure**, fare clic su **autore e distribuire** nella home page di hello Data Factory.
2. In hello **Editor delle Data Factory**, fare clic su **nuovo calcolo** dal comando hello barra e selezionare **cluster HDInsight** dal menu di hello.
3. Apportare hello modifiche toohello JSON script seguente:

   1. Per hello **clusterUri** proprietà, immettere l'URL di hello per HDInsight. Ad esempio: https://<clustername>.azurehdinsight.net/     
   2. Per hello **UserName** proprietà, immettere nome utente hello che dispone di cluster di HDInsight toohello di accesso.
   3. Per hello **Password** proprietà, immettere la password di hello hello utente.
   4. Per hello **LinkedServiceName** proprietà, immettere **AzureStorageLinkedService**.
4. Fare clic su **Distribuisci** sul comando hello barra toodeploy hello collegato servizio.

Per informazioni dettagliate, vedere [Servizi collegati di calcolo](data-factory-compute-linked-services.md) .

In hello **JSON di pipeline**, utilizzare HDInsight (su richiesta o la propria) il servizio collegato:

```JSON
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "HDInsightOnDemandLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00Z",
    "end": "2016-11-16T05:00:00Z",
    "isPaused": false
  }
}
```

## <a name="create-a-custom-activity-by-using-net-sdk"></a>Creazione di un’attività personalizzata tramite .NET SDK
In questa procedura dettagliata hello in questo articolo, creerai una data factory con una pipeline che utilizza l'attività personalizzata hello utilizzando hello portale di Azure. Hello di codice seguente viene illustrato come toocreate hello data factory di utilizzando invece .NET SDK. È possibile trovare ulteriori informazioni sull'utilizzo di SDK tooprogrammatically creare pipeline in hello [creare una pipeline con attività di copia utilizzando l'API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md) articolo. 

```csharp
using System;
using System.Configuration;
using System.Collections.ObjectModel;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.Azure;
using Microsoft.Azure.Management.DataFactories;
using Microsoft.Azure.Management.DataFactories.Models;
using Microsoft.Azure.Management.DataFactories.Common.Models;

using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Collections.Generic;

namespace DataFactoryAPITestApp
{
    class Program
    {
        static void Main(string[] args)
        {
            // create data factory management client

            // TODO: replace ADFTutorialResourceGroup with hello name of your resource group.
            string resourceGroupName = "ADFTutorialResourceGroup";

            // TODO: replace APITutorialFactory with a name that is globally unique. For example: APITutorialFactory04212017
            string dataFactoryName = "APITutorialFactory";

            TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
                ConfigurationManager.AppSettings["SubscriptionId"],
                GetAuthorizationHeader().Result);

            Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

            DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);

            Console.WriteLine("Creating a data factory");
            client.DataFactories.CreateOrUpdate(resourceGroupName,
                new DataFactoryCreateOrUpdateParameters()
                {
                    DataFactory = new DataFactory()
                    {
                        Name = dataFactoryName,
                        Location = "westus",
                        Properties = new DataFactoryProperties()
                    }
                }
            );

            // create a linked service for input data store: Azure Storage
            Console.WriteLine("Creating Azure Storage linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureStorageLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: Replace <accountname> and <accountkey> with name and key of your Azure Storage account.
                            new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>")
                        )
                    }
                }
            );

            // create a linked service for output data store: Azure SQL Database
            Console.WriteLine("Creating Azure Batch linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureBatchLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: replace <batchaccountname> and <yourbatchaccountkey> with name and key of your Azure Batch account
                            new AzureBatchLinkedService("<batchaccountname>", "https://westus.batch.azure.com", "<yourbatchaccountkey>", "myazurebatchpool", "AzureStorageLinkedService")
                        )
                    }
                }
            );

            // create input and output datasets
            Console.WriteLine("Creating input and output datasets");
            string Dataset_Source = "InputDataset";
            string Dataset_Destination = "OutputDataset";

            Console.WriteLine("Creating input dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Source,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FolderPath = "adftutorial/customactivityinput/",
                                Format = new TextFormat()
                            },
                            External = true,
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },

                            Policy = new Policy() { }
                        }
                    }
                });

            Console.WriteLine("Creating output dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Destination,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FileName = "{slice}.txt",
                                FolderPath = "adftutorial/customactivityoutput/",
                                PartitionedBy = new List<Partition>()
                                {
                                    new Partition()
                                    {
                                        Name = "slice",
                                        Value = new DateTimePartitionValue()
                                        {
                                            Date = "SliceStart",
                                            Format = "yyyy-MM-dd-HH"
                                        }
                                    }
                                }
                            },
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },
                        }
                    }
                });

            Console.WriteLine("Creating a custom activity pipeline");
            DateTime PipelineActivePeriodStartTime = new DateTime(2017, 3, 9, 0, 0, 0, 0, DateTimeKind.Utc);
            DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
            string PipelineName = "ADFTutorialPipelineCustom";

            client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new PipelineCreateOrUpdateParameters()
                {
                    Pipeline = new Pipeline()
                    {
                        Name = PipelineName,
                        Properties = new PipelineProperties()
                        {
                            Description = "Use custom activity",

                            // Initial value for pipeline's active period. With this, you won't need tooset slice status
                            Start = PipelineActivePeriodStartTime,
                            End = PipelineActivePeriodEndTime,
                            IsPaused = false,

                            Activities = new List<Activity>()
                            {
                                new Activity()
                                {
                                    Name = "MyDotNetActivity",
                                    Inputs = new List<ActivityInput>()
                                    {
                                        new ActivityInput() {
                                            Name = Dataset_Source
                                        }
                                    },
                                    Outputs = new List<ActivityOutput>()
                                    {
                                        new ActivityOutput()
                                        {
                                            Name = Dataset_Destination
                                        }
                                    },
                                    LinkedServiceName = "AzureBatchLinkedService",
                                    TypeProperties = new DotNetActivity()
                                    {
                                        AssemblyName = "MyDotNetActivity.dll",
                                        EntryPoint = "MyDotNetActivityNS.MyDotNetActivity",
                                        PackageLinkedService = "AzureStorageLinkedService",
                                        PackageFile = "customactivitycontainer/MyDotNetActivity.zip",
                                        ExtendedProperties = new Dictionary<string, string>()
                                        {
                                            { "SliceStart", "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"}
                                        }
                                    },
                                    Policy = new ActivityPolicy()
                                    {
                                        Concurrency = 2,
                                        ExecutionPriorityOrder = "OldestFirst",
                                        Retry = 3,
                                        Timeout = new TimeSpan(0,0,30,0),
                                        Delay = new TimeSpan()
                                    }
                                }
                            }
                        }
                    }
                });
        }

        public static async Task<string> GetAuthorizationHeader()
        {
            AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
            ClientCredential credential = new ClientCredential(
                ConfigurationManager.AppSettings["ApplicationId"],
                ConfigurationManager.AppSettings["Password"]);
            AuthenticationResult result = await context.AcquireTokenAsync(
                resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
                clientCredential: credential);

            if (result != null)
                return result.AccessToken;

            throw new InvalidOperationException("Failed tooacquire token");
        }
    }
}
```

## <a name="debug-custom-activity-in-visual-studio"></a>Eseguire il debug di attività personalizzate in Visual Studio
Hello [Azure Data Factory - ambiente locale](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) esempio in GitHub include uno strumento che consente attività .NET personalizzate toodebug all'interno di Visual Studio.  


## <a name="sample-custom-activities-on-github"></a>Attività personalizzata di esempio su GitHub
| Esempio | Funzioni delle attività personalizzate |
| --- | --- |
| [HttpDataDownloaderSample](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample)(Esempio relativo al downloader dati HTTP). |Scarica i dati da un archivio Blob utilizzando l'attività personalizzata in c# in Data Factory di tooAzure HTTP Endpoint. |
| [Esempio di analisi del sentimento su Twitter](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |Chiama un modello ML di Azure ed esegue l'analisi del sentimento, l'assegnazione dei punteggi, la stima e così via. |
| [RunRScriptUsingADFSample](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)(Esempio relativo all'esecuzione di script R con ADF). |Chiama lo script R eseguendo RScript.exe sul cluster HDInsight in cui è già installato R. |
| [Attività .NET per dominio app](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |Utilizza le versioni di assembly diverso da quelli utilizzati dalla visualizzazione della Data Factory di hello |
| [Rielaborare un modello in Azure Analysis Services](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/AzureAnalysisServicesProcessSample) |  Rielabora un modello in Azure Analysis Services. |

[batch-net-library]: ../batch/batch-dotnet-get-started.md
[batch-create-account]: ../batch/batch-account-create-portal.md
[batch-technical-overview]: ../batch/batch-technical-overview.md
[batch-get-started]: ../batch/batch-dotnet-get-started.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[data-factory-introduction]: data-factory-introduction.md
[azure-powershell-install]: https://github.com/Azure/azure-sdk-tools/releases


[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456

[new-azure-batch-account]: https://msdn.microsoft.com/library/mt125880.aspx
[new-azure-batch-pool]: https://msdn.microsoft.com/library/mt125936.aspx
[azure-batch-blog]: http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx

[nuget-package]: http://go.microsoft.com/fwlink/?LinkId=517478
[adf-developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[azure-preview-portal]: https://portal.azure.com/

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[hivewalkthrough]: data-factory-data-transformation-activities.md

[image-data-factory-ouput-from-custom-activity]: ./media/data-factory-use-custom-activities/OutputFilesFromCustomActivity.png

[image-data-factory-download-logs-from-custom-activity]: ./media/data-factory-use-custom-activities/DownloadLogsFromCustomActivity.png
