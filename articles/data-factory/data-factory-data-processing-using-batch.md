---
title: aaaProcess set di dati su larga scala con Data Factory e Batch | Documenti Microsoft
description: "Viene descritto come pipeline di tooprocess enormi quantità di dati in una Data Factory di Azure con funzionalità di elaborazione parallela di Batch di Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 688b964b-51d0-4faa-91a7-26c7e3150868
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 6788f02de555d2e9d6588cc990a39043866d7e97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="process-large-scale-datasets-using-data-factory-and-batch"></a>Elaborazione di fogli dati su larga scala con Data Factory e Batch
Questo articolo descrive l'architettura di una soluzione di esempio che sposta ed elabora set di dati su larga scala in modo automatico e pianificato. Fornisce inoltre una soluzione di hello tooimplement procedura dettagliata end-to-end con Azure Data Factory e i Batch di Azure.

Questo articolo è più lungo dei nostri articoli tipici perché contiene la procedura dettagliata per un'intera soluzione di esempio. Se si sta tooBatch nuovo e Data Factory, è possibile acquisire informazioni questi servizi e come interagiscono tra loro. Se si conosca servizi hello e è progettazione/creazione di una soluzione, può concentrare su hello [sezione architettura](#architecture-of-sample-solution) di articolo hello e se si sviluppa una soluzione o un prototipo, è inoltre possibile tootry out istruzioni dettagliate sull'hello [procedura dettagliata](#implementation-of-sample-solution). Microsoft invita gli utenti a inviare i loro commenti su questo contenuto e sulle relative modalità di impiego.

In primo luogo, si esaminerà come servizi Data Factory e Batch agevola l'elaborazione di grandi set di dati nel cloud hello.     

## <a name="why-azure-batch"></a>Perché Azure Batch?
Azure Batch consente applicazioni su larga scala parallele e ad alte prestazioni (HPC) computing toorun in modo efficiente nel cloud di hello. È un servizio di piattaforma che pianifica toorun di lavoro a utilizzo intensivo di calcolo su una raccolta di macchine virtuali gestita e possa automaticamente la scala di calcolo esigenze hello toomeet di risorse dei processi.

Con il servizio Batch hello, definire tooexecute risorse di calcolo di Azure le applicazioni in parallelo e su larga scala. È possibile eseguire su richiesta o pianificati processi ed è necessario toomanually creare, configurare e gestire un cluster HPC, singole macchine virtuali, reti virtuali o un processo complesso e infrastruttura di pianificazione di attività.

Vedere i seguenti articoli se non si ha familiarità con Azure Batch modo di conoscere l'architettura di implementazione della soluzione hello descritto in questo articolo hello hello.   

* [Nozioni di base su Azure Batch](../batch/batch-technical-overview.md)
* [Panoramica delle funzionalità Batch](../batch/batch-api-basics.md)

(facoltativo) toolearn ulteriori informazioni su Azure Batch, vedere hello [il percorso di apprendimento per Azure Batch](https://azure.microsoft.com/documentation/learning-paths/batch/).

## <a name="why-azure-data-factory"></a>Perché Azure Data Factory?
Data Factory è un servizio di integrazione di dati basato su cloud che Orchestra e automatizza lo spostamento di hello e trasformazione dei dati. Con il servizio di Data Factory hello, è possibile creare pipeline di dati gestiti spostano i dati locali e cloud archivio dati centralizzata tooa archivi di dati (ad esempio: archiviazione Blob di Azure) e processo/trasformare dati tramite i servizi, ad esempio HDInsight di Azure e Azure Machine Learning. È inoltre possibile pianificare toorun pipeline di dati in un modo pianificato (oraria, giornaliera, settimanale, ecc.) e il monitoraggio e gestirli in problemi di tooidentify un riepilogo e intraprendere azioni.

Vedere i seguenti articoli se non si ha familiarità con Azure Data Factory modo di conoscere l'architettura di implementazione della soluzione hello descritto in questo articolo hello hello.  

* [Introduzione ad Azure Data Factory](data-factory-introduction.md)
* [Creare la prima pipeline di dati](data-factory-build-your-first-pipeline.md)   

(facoltativo) toolearn ulteriori informazioni su Data Factory di Azure, vedere hello [il percorso di apprendimento per Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).

## <a name="data-factory-and-batch-together"></a>Data Factory e Batch insieme
Data Factory include attività predefinite, ad esempio attività di copia toocopy o spostare i dati dai dati di origine archiviano tooa archivio dati di destinazione e dati tooprocess attività Hive con i cluster Hadoop (HDInsight) in Azure. Per un elenco delle attività di trasformazione supportate, vedere le informazioni sulle [attività di trasformazione dati](data-factory-data-transformation-activities.md) .

Inoltre consente si toocreate .NET attività personalizzate dati toomove o un processo con la logica personalizzata ed eseguire queste attività in un cluster HDInsight di Azure o in un pool di Batch di Azure di macchine virtuali. Quando si usa Azure Batch, è possibile configurare tooauto pool hello della scala (aggiungere o rimuovere le macchine virtuali in base al carico di lavoro hello) in base a una formula è fornire.     

## <a name="architecture-of-sample-solution"></a>Architettura della soluzione di esempio
Anche se l'architettura di hello descritto in questo articolo è per una semplice soluzione, è toocomplex rilevanti scenari di rischio per la modellazione servizi finanziari, l'elaborazione di immagini e il rendering e genomica analysis.

Hello illustrata 1) come Data Factory gestisce lo spostamento dei dati e l'elaborazione e 2) le modalità di elaborazione di Batch di Azure hello dati in modo parallelo. Download e il diagramma di stampa hello per semplificarne (11 x 17. o formato A3): [Orchestrazione di HPC e dati con Azure Batch e Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686).

[![Diagramma di elaborazione dei dati su larga scala](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)

Hello elenco seguente vengono illustrate operazioni di base hello del processo di hello. soluzione Hello include codice e le spiegazioni soluzione end-to-end di hello toobuild.

1. **Configurare Azure Batch con un pool di nodi di calcolo (VM)**. È possibile specificare il numero di hello dei nodi e le dimensioni di ogni nodo.
2. **Creare un'istanza di Azure Data Factory** configurata con le entità che rappresentano l'archiviazione BLOB di Azure, il servizio di calcolo di Azure Batch, i dati di input/output e una pipeline o un flusso di lavoro con attività per lo spostamento e la trasformazione dei dati.
3. **Creare un'attività personalizzata di .NET in pipeline di Data Factory hello**. attività Hello è codice utente in esecuzione su hello pool Batch di Azure.
4. **Archiviare grandi quantità di dati di input come BLOB nell'archiviazione di Azure**. I dati vengono divisi in sezioni logiche, in genere in base al tempo.
5. **Data Factory copia i dati elaborati in parallelo** posizione secondaria toohello.
6. **Data Factory viene eseguita l'attività personalizzata hello utilizzando hello pool allocato dal Batch**. Data Factory può eseguire attività contemporaneamente. Ogni attività elabora una sezione dei dati. Hello risultati vengono archiviati in archiviazione di Azure.
7. **Data Factory Sposta terza posizione hello risultati finali tooa**, per la distribuzione tramite un'app o per un'ulteriore elaborazione da altri strumenti.

## <a name="implementation-of-sample-solution"></a>Implementazione della soluzione di esempio
soluzione di esempio Hello è intenzionalmente semplice ed è tooshow è come toouse DataSet tooprocess insieme Data Factory e Batch. soluzione Hello semplicemente hello delle conta le occorrenze di un termine di ricerca ("Microsoft") nei file di input organizzati in una serie temporale. Restituisce i file toooutput conteggio hello.

**Tempo**: se si ha familiarità con concetti di base di Azure Data Factory e Batch e dispongano dei prerequisiti completato hello elencati di seguito, si stima la soluzione accetta toocomplete 1-2 ore.

### <a name="prerequisites"></a>Prerequisiti
#### <a name="azure-subscription"></a>Sottoscrizione di Azure
Se non si ha una sottoscrizione di Azure, è possibile creare un account di valutazione gratuita in pochi minuti. Vedere [Versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).

#### <a name="azure-storage-account"></a>Account di archiviazione di Azure
Utilizzare un account di archiviazione di Azure per archiviare i dati di hello in questa esercitazione. Se non si ha un account di archiviazione di Azure, vedere [Creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account). soluzione di esempio Hello utilizza l'archiviazione di blob.

#### <a name="azure-batch-account"></a>Account Azure Batch
Creare un account Azure Batch utilizzando hello [portale di Azure](http://manage.windowsazure.com/). Vedere [Creare e gestire un account Azure Batch nel portale di Azure](../batch/batch-account-create-portal.md). Si noti hello Azure nome account e la chiave dell'account Batch. È inoltre possibile utilizzare [New AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) toocreate cmdlet un account Azure Batch. Per istruzioni dettagliate sull'uso del cmdlet, vedere [Guida introduttiva ai cmdlet PowerShell di Azure Batch](../batch/batch-powershell-cmdlets-get-started.md) .

soluzione di esempio Hello utilizza dati tooprocess Batch di Azure (indirettamente tramite una pipeline di Data Factory di Azure) in modo parallelo in un pool di nodi di calcolo (una raccolta di macchine virtuali gestito).

#### <a name="azure-batch-pool-of-virtual-machines-vms"></a>Pool Azure Batch di macchine virtuali (VM)
Creare un **pool di Azure Batch** con almeno 2 nodi di calcolo.

1. In hello [portale di Azure](https://portal.azure.com), fare clic su **Sfoglia** in hello menu a sinistra, quindi fare clic su **account Batch**.
2. Selezionare il hello tooopen di account Azure Batch **Account Batch** blade.
3. Fare clic sul riquadro **Pool** .
4. In hello **pool** pannello, fare clic su Aggiungi pulsante nella barra degli strumenti di hello tooadd un pool.
   1. Immettere un ID per il pool di hello (**ID pool di applicazioni**). Hello nota **ID del pool di hello**; è necessario durante la creazione di soluzioni di Data Factory hello.
   2. Specificare **Windows Server 2012 R2** per l'impostazione di hello famiglia di sistemi operativi.
   3. Selezionare un **piano tariffario per il nodo**.
   4. Immettere **2** come valore per hello **destinazione dedicato** impostazione.
   5. Immettere **2** come valore per hello **Max attività per ogni nodo** impostazione.
   6. Fare clic su **OK** pool hello toocreate.

#### <a name="azure-storage-explorer"></a>Azure Storage Explorer
[Azure Storage Explorer 6 (strumento)](https://azurestorageexplorer.codeplex.com/) o [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (di ClumsyLeaf Software). Utilizzare questi strumenti per analizzare e modificare i dati di hello nei progetti di archiviazione di Azure, inclusi i log di hello delle applicazioni cloud ospitato.

1. Creare un contenitore denominato **mycontainer** con accesso privato (Nessun accesso anonimo)
2. Se si utilizza **CloudXplorer**, creare cartelle e sottocartelle con hello seguente struttura:

   ![](./media/data-factory-data-processing-using-batch/image3.png)

   `Inputfolder`e `outputfolder` sono le cartelle di livello superiore in `mycontainer`. Hello `inputfolder` contiene sottocartelle con data e ora (AAAA-MM-GG-HH).

   Se si utilizza **Azure Storage Explorer**, nel passaggio successivo hello, è necessario per i file con nomi tooupload: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` e così via. Questo passaggio Crea automaticamente cartelle hello.
3. Creare un file di testo **file.txt** nel computer con il contenuto che contiene la parola chiave hello **Microsoft**. Ad esempio: "test attività personalizzata Microsoft testare l'attività personalizzata Microsoft".
4. Caricare toohello file hello seguenti cartelle di input nell'archiviazione blob di Azure.

   ![](./media/data-factory-data-processing-using-batch/image4.png)

   Se si utilizza **Azure Storage Explorer**, caricare il file hello **file.txt** troppo**mycontainer**. Fare clic su **copia** nella barra degli strumenti di hello toocreate una copia di blob hello. In hello **Copy Blob** della finestra di dialogo Modifica hello **nome blob di destinazione** troppo`inputfolder/2015-11-16-00/file.txt`. Ripetere questo passaggio toocreate `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` e così via. Questa azione crea automaticamente cartelle hello.
5. Creare un altro contenitore denominato `customactivitycontainer`. Contenitore di toothis file zip attività personalizzata hello caricare.

#### <a name="visual-studio"></a>Visual Studio
Installare Microsoft Visual Studio 2012 o versioni successive toocreate hello personalizzato Batch attività toobe utilizzati in soluzioni di Data Factory hello.

### <a name="high-level-steps-toocreate-hello-solution"></a>Soluzione hello toocreate di passaggi di alto livello
1. Creare un'attività personalizzata che contiene la logica di elaborazione dei dati hello.
2. Creare una data factory di Azure che utilizza l'attività personalizzata hello:

### <a name="create-hello-custom-activity"></a>Creazione di attività personalizzata hello
attività di Data Factory personalizzata Hello è il cuore hello della soluzione di esempio. soluzione di esempio Hello Usa l'attività personalizzata hello toorun di Batch di Azure. Vedere [utilizzare attività personalizzate in una pipeline di Data Factory di Azure](data-factory-use-custom-activities.md) per attività personalizzate toodevelop informazioni di base di hello e l'utilizzo in Data Factory di Azure delle pipeline.

toocreate un'attività personalizzata .NET che è possibile utilizzare in una pipeline di Data Factory di Azure, è necessario toocreate un **libreria di classi .NET** progetto con una classe che implementa che **IDotNetActivity** interfaccia. Questa interfaccia ha un solo metodo, **Execute**. Questa è hello firma del metodo hello:

```csharp
public IDictionary<string, string> Execute(
            IEnumerable<LinkedService> linkedServices,
            IEnumerable<Dataset> datasets,
            Activity activity,
            IActivityLogger logger)
```

metodo Hello ha alcuni componenti chiave che è necessario toounderstand.

* metodo Hello accetta quattro parametri:

  1. **linkedServices**. Elenco enumerabile di servizi collegati che collegano le origini dati di input/output (ad esempio: archiviazione Blob di Azure) data factory di toohello. In questo esempio c'è un solo servizio collegato di tipo Archiviazione di Azure usato sia per l'input che per l'output.
  2. **datasets**. Un elenco enumerabile di set di dati. È possibile utilizzare questo percorsi hello tooget di parametro e gli schemi definiti dal set di dati di input e output.
  3. **activity**. Questo parametro rappresenta hello calcolo entità corrente, in questo caso, un servizio Azure Batch.
  4. **logger**. Consente di logger Hello di scrivere commenti debug tale area come "Utente" accesso per hello hello pipeline.
* metodo Hello restituisce un dizionario che può essere attività personalizzate toochain utilizzati insieme in futuro hello. Questa funzionalità non ancora implementata, pertanto restituire un dizionario vuoto da metodo hello.

#### <a name="procedure-create-hello-custom-activity"></a>Procedura: Creare attività personalizzata hello
1. Creare un progetto Libreria di classi .NET in Visual Studio.

   1. Avviare **Visual Studio 2012**/**2013/2015**.
   2. Fare clic su **File**, punto troppo**New**, fare clic su **progetto**.
   3. Espandere **Modelli** e quindi selezionare **Visual C\#**. In questa procedura dettagliata, si utilizza C\#, ma è possibile utilizzare qualsiasi attività personalizzate .NET language toodevelop hello.
   4. Selezionare **libreria di classi** dall'elenco di hello dei tipi di progetto su hello destra.
   5. Immettere **MyDotNetActivity** per hello **nome**.
   6. Selezionare **c:\\ADF** per hello **percorso**. Creare la cartella hello **ADF** se non esiste.
   7. Fare clic su **OK** progetto hello toocreate.
2. Fare clic su **strumenti**, punto troppo**Gestione pacchetti NuGet**, fare clic su **Package Manager Console**.
3. In hello **Package Manager Console**, eseguire hello successivo comando tooimport **Microsoft.Azure.Management.DataFactories**.

    ```powershell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. Hello importazione **di archiviazione di Azure** pacchetto NuGet nel progetto toohello. Poiché si utilizza l'API di archiviazione Blob di hello in questo esempio, è necessario il pacchetto.

    ```powershell
    Install-Package Azure.Storage
    ```
5. Aggiungere il seguente hello **utilizzando** direttive toohello file sorgente hello progetto.

    ```csharp
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;
    
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. Modifica nome hello di hello **dello spazio dei nomi** troppo**MyDotNetActivityNS**.

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. Modificare il nome di hello della classe hello troppo**MyDotNetActivity** ed eseguirne la derivazione da hello **IDotNetActivity** interfaccia come illustrato di seguito.

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. Hello implementare (Aggiungi) **Execute** metodo hello **IDotNetActivity** interfaccia toohello **MyDotNetActivity** classe e copia hello metodo toohello codice di esempio seguente. Vedere hello [metodo Execute](#execute-method) sezione per una descrizione per la logica di hello utilizzata in questo metodo.

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
    
       // declare types for input and output data stores
       AzureStorageLinkedService inputLinkedService;
    
       Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
       foreach (LinkedService ls in linkedServices)
           logger.Write("linkedService.Name {0}", ls.Name);
    
       // using First method instead of Single since we are using hello same
       // Azure Storage linked service for input and output.
       inputLinkedService = linkedServices.First(
           linkedService =>
           linkedService.Name ==
           inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
           as AzureStorageLinkedService;
    
       string connectionString = inputLinkedService.ConnectionString; // toocreate an input storage client.
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
           // with hello data slice.
           //
           // definition of hello method is shown in hello next step.
           output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
       } while (continuationToken != null);
    
       // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
       Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    
       folderPath = GetFolderPath(outputDataset);
    
       logger.Write("Writing blob toohello folder: {0}", folderPath);
    
       // create a storage object for hello output blob.
       CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
       // write hello name of hello file.
       Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
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
9. Aggiungere hello seguente classe toohello metodi di supporto. Questi metodi vengono richiamati dal hello **Execute** metodo. In particolare, hello **Calculate** metodo isola codice hello che scorre ogni oggetto blob.

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
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
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
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
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
    Hello **GetFolderPath** restituisce cartella toohello hello tale set di dati di prova punti tooand prova **GetFileName** metodo restituisce il nome di hello di hello/file blob che hello per i punti di set di dati.

    ```csharp

    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
    ```

    Hello **Calculate** metodo calcola il numero di hello di istanze della parola chiave **Microsoft** nei file di input hello (BLOB nella cartella hello). il termine di ricerca Hello ("Microsoft") è hardcoded nel codice hello.

1. Compilare il progetto hello. Fare clic su **compilare** menu hello e fare clic su **Compila soluzione**.
2. Avviare **Esplora**e passare troppo**bin\\debug** o **bin\\versione** cartella in base al tipo di hello di compilazione.
3. Creare un file zip **MyDotNetActivity.zip** che contiene tutti i file binari hello in hello  **\\bin\\Debug** cartella. È opportuno hello tooinclude MyDotNetActivity. **pdb** file in modo che sia possibile ottenere ulteriori dettagli, ad esempio il numero di riga nel codice sorgente hello che ha causato il problema di hello quando si verifica un errore.

   ![](./media/data-factory-data-processing-using-batch/image5.png)
4. Caricare **MyDotNetActivity.zip** come un contenitore di blob toohello blob: `customactivitycontainer` in hello Azure nell'archiviazione blob che hello **StorageLinkedService** servizio in hello collegato  **ADFTutorialDataFactory** utilizza. Creare il contenitore di blob hello `customactivitycontainer` se non esiste già.

#### <a name="execute-method"></a>Metodo Execute
Questa sezione vengono fornite altre informazioni e note sul codice hello in hello metodo Execute.

1. i membri di Hello per scorrere la raccolta di hello input presenti nei hello [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) dello spazio dei nomi. Scorrere la raccolta di blob hello richiede l'utilizzo di hello **BlobContinuationToken** classe. In pratica, è necessario utilizzare un do-durante il ciclo con token hello come meccanismo di hello di uscita ciclo hello. Per ulteriori informazioni, vedere [come archiviazione di Blob da .NET toouse](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Di seguito è illustrato un ciclo di base:

    ```csharp
    // Initialize hello continuation token.
    BlobContinuationToken continuationToken = null;
    do
    {
    // Get hello list of input blobs from hello input storage client object.
    BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
    
                         true,
                                   BlobListingDetails.Metadata,
                                   null,
                                   continuationToken,
                                   null,
                                   null);
    // Return a string derived from parsing each blob.
    
     output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
    } while (continuationToken != null);

    ```
   Vedere la documentazione di hello per hello [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) metodo per i dettagli.
2. Hello codice per l'utilizzo tramite set hello di BLOB logicamente passa all'interno di hello eseguire-il ciclo while. In hello **Execute** (metodo), eseguire hello-durante il ciclo passa elenco hello di BLOB metodo tooa denominato **Calculate**. metodo Hello restituisce una variabile di stringa denominata **output** ovvero hello risultato con scorrere tutti i BLOB hello nel segmento hello.

   Restituisce il numero di hello di occorrenze del termine di ricerca hello (**Microsoft**) in blob hello passato toohello **Calculate** metodo.

    ```csharp
    output += string.Format("{0} occurrences of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
    ```
3. Una volta hello **Calculate** metodo ha eseguito operazioni di hello, deve essere scritta tooa nuovo blob. Pertanto, per ogni set di BLOB elaborato, un nuovo blob possono essere scritti con risultati hello. primo set di output di hello trova toowrite tooa nuovo blob.

    ```csharp
    // Get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
    Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    ```
4. codice di Hello viene inoltre chiamato un metodo di supporto: **GetFolderPath** percorso della cartella hello tooretrieve (nome del contenitore di archiviazione a hello).

    ```csharp
    folderPath = GetFolderPath(outputDataset);
    ```
   Hello **GetFolderPath** cast hello set di dati oggetto tooan AzureBlobDataSet, che include una proprietà denominata FolderPath.

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FolderPath;
    ```
5. hello chiamate di codice Hello **GetFileName** metodo tooretrieve hello file nome (blob). codice Hello è simile toohello sopra percorso cartella hello tooget del codice.

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FileName;
    ```
6. nome di Hello del file hello viene scritta tramite la creazione di un oggetto URI. costruttore URI Hello utilizza hello **BlobEndpoint** nome del contenitore di proprietà tooreturn hello. nome file e percorso della cartella Hello vengono aggiunti tooconstruct hello output URI del blob.  

    ```csharp
    // Write hello name of hello file.
    Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    ```
7. nome di Hello del file hello è stato scritto e ora è possibile scrivere una stringa di output di hello da hello **Calculate** nuovo blob di metodo tooa:

    ```csharp
    // Create a blob and upload hello output text.
    CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
    logger.Write("Writing {0} toohello output blob", output);
    outputBlob.UploadText(output);
    ```

### <a name="create-hello-data-factory"></a>Creare hello data factory
In hello [creare attività personalizzata hello](#create-the-custom-activity) sezione creata un'attività personalizzata e il file zip hello caricato con i file binari e hello PDB file tooan contenitore blob di Azure. In questa sezione si crea un Azure **data factory di** con un **pipeline** che utilizza hello **attività personalizzata**.

Hello input set di dati per l'attività personalizzata hello rappresenta BLOB hello (file) nella cartella input hello (`mycontainer\\inputfolder`) nell'archiviazione blob. Hello set di dati di output per attività hello rappresenta BLOB di output di hello nella cartella di output di hello (`mycontainer\\outputfolder`) nell'archiviazione blob.

Eliminare uno o più file nelle cartelle di input hello:

```
mycontainer -\> inputfolder
    2015-11-16-00
    2015-11-16-01
    2015-11-16-02
    2015-11-16-03
    2015-11-16-04
```

Ad esempio, è possibile eliminare un file (file. txt) con hello dopo contenuto in ciascuna delle cartelle hello.

```
test custom activity Microsoft test custom activity Microsoft
```

Ogni cartella di input corrisponde sezione tooa nella Data Factory di Azure, anche se la cartella hello è 2 o più file. Quando ogni sezione venga elaborato dalla pipeline di hello, attività personalizzata hello scorre tutti i BLOB hello nella cartella di input hello per tale sezione.

Vedrai cinque dei file di output con hello stesso contenuto. Ad esempio, file di output di hello di elaborazione del file nella cartella hello 2015-11-16-00 hello è hello seguente contenuto:

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
```

Se si elimina più file (file. txt, file2.txt, file3.txt) con hello stesso contenuto toohello cartella di input, viene visualizzato dopo contenuto nel file di output di hello hello. Ogni cartella (2015-11-16-00, e così via) corrispondente sezione tooa in questo esempio, anche se la cartella hello dispone di più file di input.

```csharp
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file2.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file3.txt.
```

file di output di Hello con tre righe a questo punto, uno per ogni file di input (blob) nella cartella hello associata a una sezione hello (2015-11-16-00).

Per ogni esecuzione di attività viene creata un'attività. In questo esempio, è presente una sola attività nella pipeline hello. Quando una sezione venga elaborata dalla pipeline di hello, nella sezione di Azure Batch tooprocess hello viene eseguita l'attività personalizzata hello. Poiché ci sono cinque sezioni, e ogni sezione può contenere più BLOB o file, in Azure Batch vengono create cinque attività. Quando un'attività viene eseguita in Batch, è effettivamente hello attività personalizzata che è in esecuzione.

Hello seguendo questa procedura dettagliata fornisce dettagli aggiuntivi.

#### <a name="step-1-create-hello-data-factory"></a>Passaggio 1: Creare hello data factory
1. Dopo l'accesso toohello [portale di Azure](https://portal.azure.com/), hello i passaggi seguenti:

   1. Fare clic su **NEW** nel menu di sinistra hello.
   2. Fare clic su **dati + Analitica** in hello **New** blade.
   3. Fare clic su **Data Factory** su hello **analitica dati** blade.
2. In hello **nuova data factory** pannello immettere **CustomActivityFactory** per hello Name. nome Hello di hello Azure data factory deve essere globalmente univoco. Se viene visualizzato l'errore hello: **"CustomActivityFactory" nome della Data factory non è disponibile**, modificare il nome di hello della data factory di hello (ad esempio, **yournameCustomActivityFactory**) e provare a creare nuovo.
3. Fare clic su **NOME DEL GRUPPO DI RISORSE**e selezionare un gruppo di risorse esistente o crearne uno.
4. Verificare che la sottoscrizione corretta hello e regione in cui si desidera hello data factory toobe creato in uso.
5. Fare clic su **crea** su hello **nuova data factory** blade.
6. Vedrai data factory di hello viene creato nel hello **Dashboard** di hello portale di Azure.
7. Dopo aver hello data factory è stata creata correttamente, vedrai hello data factory pagina nella quale viene hello contenuto di data factory di hello.

   ![](./media/data-factory-data-processing-using-batch/image6.png)

#### <a name="step-2-create-linked-services"></a>Passaggio 2: Creare servizi collegati
Servizi collegati collegano archivi dati o servizi tooan data factory di Azure di calcolo. In questo passaggio si collega il **di archiviazione di Azure** account e **Azure Batch** tooyour data factory di account.

#### <a name="create-azure-storage-linked-service"></a>Creare il servizio collegato Archiviazione di Azure
1. Fare clic su hello **autore e distribuire** riquadro hello **DATA FACTORY** pannello **CustomActivityFactory**. Vedrai hello Editor delle Data Factory.
2. Fare clic su **nuovo archivio dati** hello barra dei comandi e scegliere **archiviazione di Azure.** Dovrebbe essere hello script JSON per la creazione di una risorsa di archiviazione di Azure il servizio nell'editor di hello collegato.

   ![](./media/data-factory-data-processing-using-batch/image7.png)

3. Sostituire **nome account** con nome hello dell'account di archiviazione di Azure e **chiave dell'account** con la chiave di accesso hello di hello account di archiviazione di Azure. toolearn modalità di accesso di archiviazione di tooget chiave, vedere [visualizzazione, copia e l'archiviazione di rigenerare le chiavi di accesso](../storage/common/storage-create-storage-account.md#manage-your-storage-account).

4. Fare clic su **Distribuisci** sul comando hello barra toodeploy hello collegato servizio.

   ![](./media/data-factory-data-processing-using-batch/image8.png)

#### <a name="create-azure-batch-linked-service"></a>Creare il servizio collegato Azure Batch
In questo passaggio si crea un servizio collegato per il **Azure Batch** account attività personalizzata utilizzata toorun hello Data Factory.

1. Fare clic su **nuovo calcolo** hello barra dei comandi e scegliere **Azure Batch.** Dovrebbe essere hello script JSON per la creazione di un Batch di Azure il servizio nell'editor di hello collegato.
2. In hello script JSON:

   1. Sostituire **nome account** con nome hello dell'account di Azure Batch.
   2. Sostituire **chiave di accesso** con la chiave di accesso hello di hello account Azure Batch.
   3. Immettere l'ID di hello del pool di hello per hello **poolName** proprietà**.** Per questa proprietà è possibile specificare il nome del pool o del pool di ID.
   4. Immettere il batch di hello URI per hello **batchUri** proprietà JSON.

      > [!IMPORTANT]
      > Hello **URL** da hello **pannello account Azure Batch** in hello seguente formato: \<accountname\>.\< area\>. batch.azure.com. Per hello **batchUri** proprietà hello JSON, è necessario troppo**rimuovere "accountname".** dall'URL hello. Esempio: `"batchUri": "https://eastus.batch.azure.com"`.
      >
      >

      ![](./media/data-factory-data-processing-using-batch/image9.png)

      Per hello **poolName** proprietà, è inoltre possibile specificare l'ID di hello del pool di hello anziché il nome di hello del pool di hello.

      > [!NOTE]
      > Hello servizio Data Factory non supporta un'opzione su richiesta per il Batch di Azure a quanto accade per HDInsight. È possibile usare solo il proprio pool di Batch di Azure in una data factory di Azure.
      >
      >
   5. Specificare **StorageLinkedService** per hello **linkedServiceName** proprietà. Il servizio collegato creato nel passaggio precedente di hello. Questo servizio di archiviazione viene usato come area di staging per file e log.
3. Fare clic su **Distribuisci** sul comando hello barra toodeploy hello collegato servizio.

#### <a name="step-3-create-datasets"></a>Passaggio 3: Creare set di dati
In questo passaggio, creare set di dati toorepresent input e i dati di output.

#### <a name="create-input-dataset"></a>Creare set di dati di input
1. In hello **Editor** per hello Data Factory, fare clic su **nuovo set di dati** pulsante sulla barra degli strumenti hello e fare clic su **archiviazione Blob di Azure** dal menu a discesa hello.
2. Sostituire hello JSON nel riquadro di destra hello con hello frammento di codice JSON seguente:

    ```json
    {
       "name": "InputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
               "format": {
                   "type": "TextFormat"
               },
               "partitionedBy": [
                   {
                       "name": "Year",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy"
                       }
                   },
                   {
                       "name": "Month",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "MM"
                       }
                   },
                   {
                       "name": "Day",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "dd"
                       }
                   },
                   {
                       "name": "Hour",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "HH"
                       }
                   }
               ]
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

    Più avanti in questa procedura dettagliata viene creata una pipeline con ora di inizio: 2015-11-16T00:00:00Z e ora di fine: 2015-11-16T05:00:00Z. Si tratta di dati pianificati tooproduce **oraria**, pertanto vi sono 5 sezioni di input/output (tra **00**: 00:00 -\> **05**: 00:00).

    Hello **frequenza** e **intervallo** per hello di un set di dati dell'input è troppo**ora** e **1**, il che significa che hello input sezione è disponibile ogni ora.

    Di seguito sono ora di inizio di hello per ogni sezione, rappresentato da **SliceStart** variabile di sistema in hello sopra il frammento JSON.

    | **Sezione** | **Ora di inizio**          |
    |-----------|-------------------------|
    | 1         | 2015-11-16T**00**:00:00 |
    | 2         | 2015-11-16T**01**:00:00 |
    | 3         | 2015-11-16T**02**:00:00 |
    | 4         | 2015-11-16T**03**:00:00 |
    | 5         | 2015-11-16T**04**:00:00 |

    Hello **folderPath** viene calcolato utilizzando hello di anno, mese, giorno e ora parte dell'ora di inizio sezione hello (**SliceStart**). Di conseguenza, ecco come una cartella di input è l'intervallo di tooa mappato.

    | **Sezione** | **Ora di inizio**          | **Cartella di input**  |
    |-----------|-------------------------|-------------------|
    | 1         | 2015-11-16T**00**:00:00 | 2015-11-16-**00** |
    | 2         | 2015-11-16T**01**:00:00 | 2015-11-16-**01** |
    | 3         | 2015-11-16T**02**:00:00 | 2015-11-16-**02** |
    | 4         | 2015-11-16T**03**:00:00 | 2015-11-16-**03** |
    | 5         | 2015-11-16T**04**:00:00 | 2015-11-16-**04** |

1. Fare clic su **Distribuisci** hello toocreate barra degli strumenti e distribuire hello **InputDataset** tabella.

#### <a name="create-output-dataset"></a>Creare il set di dati di output
In questo passaggio si crea un altro set di dati di tipo di dati di output di hello toorepresent AzureBlob.

1. In hello **Editor** per hello Data Factory, fare clic su **nuovo set di dati** pulsante sulla barra degli strumenti hello e fare clic su **archiviazione Blob di Azure** dal menu a discesa hello.
2. Sostituire hello JSON nel riquadro di destra hello con hello frammento di codice JSON seguente:

    ```json
    {
       "name": "OutputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "fileName": "{slice}.txt",
               "folderPath": "mycontainer/outputfolder",
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

    Un BLOB o file di output viene generato per ogni sezione di input. Ecco come viene denominato il file di output per ogni sezione. Tutti i file di output di hello vengono generati in una cartella di output: `mycontainer\\outputfolder`.

    | **Sezione** | **Ora di inizio**          | **File di output**       |
    |-----------|-------------------------|-----------------------|
    | 1         | 2015-11-16T**00**:00:00 | 2015-11-16-**00.txt** |
    | 2         | 2015-11-16T**01**:00:00 | 2015-11-16-**01.txt** |
    | 3         | 2015-11-16T**02**:00:00 | 2015-11-16-**02.txt** |
    | 4         | 2015-11-16T**03**:00:00 | 2015-11-16-**03.txt** |
    | 5         | 2015-11-16T**04**:00:00 | 2015-11-16-**04.txt** |

    Tenere presente che tutti i file in una cartella di input di hello (ad esempio: 2015-11-16-00) fanno parte di una sezione con ora di inizio hello: 2015-11-16-00. Durante l'elaborazione di questa sezione, attività personalizzata hello esamina ogni file e produce una riga nel file di output di hello con numero di hello di occorrenze del termine di ricerca ("Microsoft"). Se sono presenti tre file nella cartella hello 2015-11-16-00, sono presenti tre righe nel file di output di hello: 2015-11-16-00.txt.

1. Fare clic su **Distribuisci** hello toocreate barra degli strumenti e distribuire hello **OutputDataset**.

#### <a name="step-4-create-and-run-hello-pipeline-with-custom-activity"></a>Passaggio 4: Creare ed eseguire pipeline hello con attività personalizzata
In questo passaggio creare una pipeline con un'attività, attività personalizzata hello creato in precedenza.

> [!IMPORTANT]
> Se si non sono stati caricati hello **file.txt** tooinput cartelle nel contenitore blob hello, eseguire questa operazione prima di creare pipeline hello. Hello **isPaused** proprietà è impostata toofalse nella pipeline hello JSON, pertanto viene eseguita immediatamente pipeline hello come hello **avviare** la data è hello precedente.
>
>

1. Nell'Editor delle Data Factory hello, fare clic su **nuova pipeline** hello barra dei comandi. Se il comando hello non viene visualizzata, fare clic su **... (Puntini di sospensione)**  toosee è.
2. Sostituire hello JSON nel riquadro di destra hello con hello lo script JSON seguente:

    ```json
    {
       "name": "PipelineCustom",
       "properties": {
           "description": "Use custom activity",
           "activities": [
               {
                   "type": "DotNetActivity",
                   "typeProperties": {
                       "assemblyName": "MyDotNetActivity.dll",
                       "entryPoint": "MyDotNetActivityNS.MyDotNetActivity",
                       "packageLinkedService": "AzureStorageLinkedService",
                       "packageFile": "customactivitycontainer/MyDotNetActivity.zip"
                   },
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
                   "policy": {
                       "timeout": "00:30:00",
                       "concurrency": 5,
                       "retry": 3
                   },
                   "scheduler": {
                       "frequency": "Hour",
                       "interval": 1
                   },
                   "name": "MyDotNetActivity",
                   "linkedServiceName": "AzureBatchLinkedService"
               }
           ],
           "start": "2015-11-16T00:00:00Z",
           "end": "2015-11-16T05:00:00Z",
           "isPaused": false
      }
    }
    ```
   Si noti hello seguenti punti:

   * È presente una sola attività nella pipeline hello e che è di tipo: **DotNetActivity**.
   * **AssemblyName** è impostato il nome toohello di hello DLL: **MyDotNetActivity.dll**.
   * **Punto di ingresso** è troppo**MyDotNetActivityNS.MyDotNetActivity**. Si tratta in sostanza di \<spazio dei nomi\>.\<nome classe\> nel codice.
   * **PackageLinkedService** è troppo**StorageLinkedService** che punta toohello archiviazione di blob che contiene i file zip di attività personalizzata hello. Se si utilizza diversi account di archiviazione di Azure per i file di input/output e i file zip di attività personalizzata hello, è necessario toocreate un altro servizio di archiviazione Azure il servizio collegato. Questo articolo si presuppone che si sta utilizzando hello stesso account di archiviazione di Azure.
   * **PackageFile** è troppo**customactivitycontainer/MyDotNetActivity.zip**. È in formato hello: \<containerforthezip\>/\<nameofthezip.zip\>.
   * attività personalizzata Hello accetta **InputDataset** come input e **OutputDataset** come output.
   * Hello **linkedServiceName** proprietà dell'attività personalizzata hello punta toohello **AzureBatchLinkedService**, che indica Data Factory di Azure, tale attività personalizzata hello deve toorun nel Batch di Azure.
   * Hello **concorrenza** impostazione è importante. Se si utilizza il valore predefinito hello, ovvero 1, anche se si dispone di 2 o più nodi di calcolo nel pool di Azure Batch hello, sezioni hello vengono elaborate una dopo l'altra. Pertanto, non si potrà usufruire della funzionalità di elaborazione parallela hello di Batch di Azure. Se si imposta **concorrenza** tooa più alto valore, ad esempio 2, significa che due sezioni (corrisponde tootwo operazioni in Batch di Azure) possono essere elaborate in hello stesso tempo, in questo caso, entrambe le macchine virtuali di hello in hello Azure Batch vengono utilizzati pool. Pertanto, impostare proprietà di concorrenza hello in modo appropriato.
   * Per impostazione predefinita, viene eseguita solo un'attività (sezione) in una VM in qualsiasi momento. Hello motivo è che, per impostazione predefinita, hello **massimo attività per ogni macchina virtuale** è impostato too1 per un pool di Batch di Azure. Come parte dei prerequisiti, è stato creato un pool con too2 questo set di proprietà, in modo da due intervalli di Data Factory possono essere eseguito su una macchina virtuale in hello contemporaneamente.

    -   **isPaused** proprietà è impostata toofalse per impostazione predefinita. pipeline Hello verrà eseguito immediatamente in questo esempio perché l'inizio delle sezioni hello in hello precedente. È possibile impostare la pipeline di hello toopause tootrue proprietà e impostarla toorestart toofalse indietro.

    -   Hello **avviare** tempo e **fine** tempi sono distanza di cinque ore e le sezioni vengono generate ogni ora, in modo da cinque sezioni vengono generate dalla pipeline di hello.

1. Fare clic su **Distribuisci** sul comando hello barra pipeline hello toodeploy.

#### <a name="step-5-test-hello-pipeline"></a>Passaggio 5: Testare la pipeline hello
In questo passaggio si verifica pipeline hello eliminazione file nelle cartelle di input hello. Iniziamo con pipeline hello test con un file per una cartella di input.

1. Nel Pannello di Data Factory hello in hello portale di Azure, fare clic su **diagramma**.

   ![](./media/data-factory-data-processing-using-batch/image10.png)
2. Nella vista diagramma hello, fare doppio clic sul set di dati input: **InputDataset**.

   ![](./media/data-factory-data-processing-using-batch/image11.png)
3. Dovrebbe essere hello **InputDataset** pannello con tutti e cinque sezioni pronto. Hello preavviso **ora di inizio sezione** e **ora di fine sezione** per ogni sezione.

   ![](./media/data-factory-data-processing-using-batch/image12.png)
4. In hello **vista diagramma**, fare clic su **OutputDataset**.
5. Dovrebbe essere che le sezioni di output cinque hello sono nello stato Ready hello se sono già stati elaborati.

   ![](./media/data-factory-data-processing-using-batch/image13.png)
6. Hello tooview portale Azure usare **attività** associato hello **sezioni** e vedere quali macchine Virtuali di ogni sezione è stata eseguita. Per altre informazioni, vedere la sezione [Integrazione di Data Factory e Batch](#data-factory-and-batch-integration) .
7. Si noterà che i file di output di hello in hello `outputfolder` di `mycontainer` nell'archiviazione di Azure blob.

   ![](./media/data-factory-data-processing-using-batch/image15.png)

   Saranno presenti cinque file di output, uno per ogni sezione di input. Ognuno di hello l'output del file deve essere contenuto toohello simile seguente output:

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
    ```
   Hello diagramma seguente illustra il mapping tra sezioni Data Factory hello tootasks in Batch di Azure. In questo esempio a una sezione è associata una sola esecuzione.

   ![](./media/data-factory-data-processing-using-batch/image16.png)
8. Si proverà ora con più file in una cartella. Creazione di file: **file2.txt**, **file3.txt**, **file4.txt**, e **file5.txt** con hello stesso contenuto come file. txt nella cartella hello: **2015-11-06-01**.
9. Nella cartella di output di hello, **eliminare** file di output di hello: **2015-11-16-01.txt**.
10. A questo punto, in hello **OutputDataset** blade, sezione hello pulsante destro del mouse con **ora di inizio sezione** impostare troppo**16/11/2015 01:00:00 AM**, fare clic su **eseguire**sezione hello toorerun/rinviati-process. A questo punto, sezione hello ha cinque file anziché un file.

    ![](./media/data-factory-data-processing-using-batch/image17.png)
11. Dopo l'esecuzione di sezione hello e il suo stato sia **pronto**, verificare il contenuto di hello nel file di output di hello per questa sezione (**2015-11-16-01.txt**) in hello `outputfolder` di `mycontainer` nell'archiviazione blob. Deve essere presente una riga per ogni file della sezione hello.

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file2.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file3.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file4.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file5.txt.
    ```

> [!NOTE]
> Se non è stato eliminato hello output file 2015-11-16-01.txt prima di tentare con cinque file di input, viene visualizzata una riga da eseguire la sezione precedente hello e cinque righe dall'intervallo corrente di hello eseguire. Per impostazione predefinita, il contenuto di hello è accodato toooutput file se esiste già.
>
>

#### <a name="data-factory-and-batch-integration"></a>Integrazione di Data Factory e Batch
Hello servizio Data Factory crea un processo in Batch di Azure con nome hello: `adf-poolname:job-xxx`.

![Azure Data Factory: processi di Batch](media/data-factory-data-processing-using-batch/data-factory-batch-jobs.png)

Per ogni esecuzione di attività di una sezione viene creata un'attività nel processo di hello. Se sono presenti toobe pronto 10 sezioni elaborate, vengono create 10 attività nel processo di hello. È possibile avere più di una sezione in esecuzione in parallelo, se si dispone di più nodi di calcolo nel pool di hello. Se del numero massimo di attività hello per calcola i set di nodi sono troppo > 1, possono essere presenti più di una sezione in esecuzione su hello calcolo stesso.

In questo esempio ci sono cinque sezioni, quindi cinque attività in Azure Batch. Con hello **concorrenza** impostare troppo**5** in hello pipeline JSON in Azure Data Factory e **massimo attività per ogni macchina virtuale** impostare troppo**2** in Batch di Azure pool di applicazioni con **2** le macchine virtuali, hello attività esecuzione veloce (ora di inizio e fine per le attività di controllo).

Utilizzare procedura batch hello tooview portale hello e le relative attività associate a hello **sezioni** e vedere quali macchine Virtuali di ogni sezione è stata eseguita.

![Azure Data Factory: attività processi di Batch](media/data-factory-data-processing-using-batch/data-factory-batch-job-tasks.png)

### <a name="debug-hello-pipeline"></a>Eseguire il debug di pipeline hello
Il debug è costituito da alcune tecniche di base:

1. Se non è troppo impostata sezione input hello**pronto**, verificare che hello struttura di cartella di input sia corretto e file. txt presente nelle cartelle di input hello.

   ![](./media/data-factory-data-processing-using-batch/image3.png)
2. In hello **Execute** metodo dell'attività personalizzata, utilizzare hello **IActivityLogger** informazioni toolog oggetto che consente di risolvere i problemi. messaggi Hello registrato visualizzata all'utente di hello\_file di log di 0.

   In hello **OutputDataset** pannello, fare clic su hello toosee di sezione hello **sezione dati** pannello per tale sezione. Verranno visualizzate le **esecuzioni di attività** per quella sezione. Verrà visualizzata un'attività eseguire per sezione hello. Se si fa clic **eseguire** nella barra dei comandi di hello, è possibile avviare un'altra attività eseguita per hello stessa sezione.

   Quando si sceglie di eseguire attività di hello, vedrai hello **Dettagli esecuzione attività** pannello con un elenco di file di log. Vedere i messaggi registrati in hello **utente\_0 log** file. Quando si verifica un errore, vengono visualizzati tre esecuzioni di attività perché il numero di tentativi di hello è too3 nella pipeline/attività hello JSON. Quando si sceglie di eseguire attività di hello, vedrai che è possibile esaminare l'errore hello tootroubleshoot i file di log hello.

   ![](./media/data-factory-data-processing-using-batch/image18.png)

   Nell'elenco di hello dei file di log, fare clic su hello **utente 0.log**. Nel riquadro di destra hello sono risultati hello dell'utilizzo di hello **IActivityLogger.Write** metodo.

   ![](./media/data-factory-data-processing-using-batch/image19.png)

   È consigliabile cercare anche nel file system-0.log eventuali messaggi di errore di sistema ed eccezioni.

    ```
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Loading assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Creating an instance of MyDotNetActivityNS.MyDotNetActivity from assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Executing Module
    
    Trace\_T\_D\_12/6/2015 1:43:38 AM\_T\_D\_\_T\_D\_Information\_T\_D\_0\_T\_D\_Activity e3817da0-d843-4c5c-85c6-40ba7424dce2 finished successfully
    ```
3. Includere hello **PDB** file nel file zip hello in modo che i dettagli dell'errore hello presentano informazioni ad esempio **stack di chiamate** quando si verifica un errore.
4. Tutti hello file nel file zip hello per attività personalizzata hello deve essere in hello **livello principale** senza sottocartelle.

   ![](./media/data-factory-data-processing-using-batch/image20.png)
5. Verificare che hello **assemblyName** (MyDotNetActivity.dll), **entryPoint** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer / MyDotNetActivity.zip) e **packageLinkedService** (deve toohello punto Azure nell'archiviazione blob che contiene i file zip hello) sono impostate toocorrect valori.
6. Se è stata corretta una sezione di hello tooreprocess errore e si desidera, fare doppio clic su sezione hello hello **OutputDataset** pannello e fare clic su **eseguire**.

   ![](./media/data-factory-data-processing-using-batch/image21.png)

   > [!NOTE]
   > Nell'archiviazione BLOB di Azure verrà visualizzato un **contenitore** denominato `adfjobs`. Questo contenitore non viene eliminato automaticamente, ma è possibile eliminare senza problemi dopo aver completato la soluzione di hello test. Analogamente, hello soluzioni di Data Factory crea un Batch di Azure **processo** denominato: `adf-\<pool ID/name\>:job-0000000001`. Dopo avere testato soluzione hello se lo si desidera, è possibile eliminare il processo.
   >
   >
7. attività personalizzata Hello non utilizza hello **app** file dal pacchetto. Pertanto, se il codice legge tutte le stringhe di connessione dal file di configurazione di hello, non funziona in fase di esecuzione. Hello consigliata quando si utilizza Azure Batch è toohold tutti i segreti in un **KeyVault Azure**, utilizzare un keyvault hello tooprotect principale di servizio basato sul certificato e la distribuzione di pool di hello certificato tooAzure Batch. attività personalizzate .NET Hello quindi possono accedere i segreti in hello KeyVault in fase di esecuzione. Questa soluzione è generica e può essere ridimensionato tooany tipo di chiave privata, non solo stringa di connessione.

    È una soluzione più semplice (ma non consigliata): è possibile creare un **servizio collegato SQL Azure** con le impostazioni della stringa di connessione, creare un set di dati che utilizza hello servizio collegato e catena hello dataset come un set di dati di input fittizio attività di .NET toohello personalizzata. È possibile quindi hello accesso collegato stringa di connessione del servizio nel codice di attività personalizzata hello e dovrebbe funzionare correttamente in fase di esecuzione.  

#### <a name="extend-hello-sample"></a>Estendere l'esempio hello
È possibile estendere questo esempio toolearn ulteriori informazioni sulle funzionalità di Data Factory di Azure e Azure Batch. Tooprocess sezioni in un intervallo di tempo diversi, ad esempio, hello alla procedura seguente:

1. Aggiungere hello seguendo le sottocartelle in hello `inputfolder`: 2015-11-16-05, 2015-11-16-06 201-11-16-07, 2011-11-16-08, 09 2015-11-16 e inserire file di input in tali cartelle. Modificare l'ora di fine hello pipeline hello `2015-11-16T05:00:00Z` troppo`2015-11-16T10:00:00Z`. In hello **vista diagramma**, fare doppio clic su hello **InputDataset**e verificare che le sezioni di input hello sono pronte. Fare doppio clic su **OuptutDataset** stato hello toosee delle sezioni di output. Se sono in stato pronto, controllare la cartella di output hello per i file di output di hello.
2. Aumentare o diminuire hello **concorrenza** toounderstand impostazione come influisce sulle prestazioni di hello della soluzione, in particolare hello elaborazione che si verifica nel Batch di Azure. (Vedere il passaggio 4: creare ed eseguire pipeline hello per ulteriori informazioni su hello **concorrenza** impostazione.)
3. Creare un pool con un **numero massimo di attività per ogni VM**più alto o più basso. toouse hello nuovo pool è stato creato, hello aggiornamento servizio collegato Azure Batch nella soluzione di Data Factory hello. (Vedere il passaggio 4: creare ed eseguire pipeline hello per ulteriori informazioni su hello **massimo attività per ogni macchina virtuale** impostazione.)
4. Creare un pool di Azure Batch con la funzionalità **Scalabilità automatica** . Nodi di calcolo in un pool di Azure Batch di scalabilità automatica è regolazione dinamica dei hello della potenza utilizzata dall'applicazione di elaborazione. 

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
5. Nella soluzione di esempio hello hello **Execute** metodo richiama hello **Calculate** metodo che elabora un tooproduce porzioni di dati di input una sezione di dati di output. È possibile scrivere la propria tooprocess metodo dati di input e sostituire chiamata al metodo hello Calculate nel metodo Execute hello con un metodo di chiamata tooyour.

### <a name="next-steps-consume-hello-data"></a>Passaggi successivi: utilizzare i dati di hello
Dopo l'elaborazione dei dati, è possibile usarli con strumenti online come **Microsoft Power BI**. Di seguito sono collegamenti toohelp comprendere Power BI e come toouse in Azure:

* [Esplorare un set di dati in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-data/)
* [Introduzione a Power BI Desktop hello](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)
* [Aggiornamento dei dati in Power BI](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/)
* [Azure e Power BI - Panoramica di base](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

## <a name="references"></a>Riferimenti
* [Data factory di Azure](https://azure.microsoft.com/documentation/services/data-factory/)

  * [Introduzione tooAzure servizio Data Factory](data-factory-introduction.md)
  * [Introduzione a Data factory di Azure](data-factory-build-your-first-pipeline.md)
  * [Usare attività personalizzate in una pipeline di Data factory di Azure](data-factory-use-custom-activities.md)
* [Azure Batch](https://azure.microsoft.com/documentation/services/batch/)

  * [Nozioni di base su Azure Batch](../batch/batch-technical-overview.md)
  * [Cenni preliminari sulle funzionalità di Azure Batch](../batch/batch-api-basics.md)
  * [Creare e gestire account Azure Batch nel portale di Azure hello](../batch/batch-account-create-portal.md)
  * [Introduzione alla libreria di Azure Batch per .NET](../batch/batch-dotnet-get-started.md)

[batch-explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch-explorer-walkthrough]: http://blogs.technet.com/b/windowshpc/archive/2015/01/20/azure-batch-explorer-sample-walkthrough.aspx
