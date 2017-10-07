---
title: aaaGet avviato con Visual Studio e di archiviazione blob di servizi connessi (servizi cloud) | Documenti Microsoft
description: "La modalità di avvio tooget utilizzo dell'archiviazione Blob di Azure in un progetto di servizio cloud in Visual Studio dopo la connessione di account di archiviazione tooa utilizzando Visual Studio di servizi connessi"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 1144a958-f75a-4466-bb21-320b7ae8f304
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 62fb7fcff0a90008859ebe23755f13ef0555e380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-cloud-services-projects"></a>Introduzione all’archiviazione BLOB di Azure e ai servizi connessi di Visual Studio (progetti servizi cloud)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Panoramica
Questo articolo descrive la modalità di avvio tooget con archiviazione Blob di Azure dopo aver creato o a cui fa riferimento a un account di archiviazione di Azure tramite Visual Studio hello **aggiungere servizi connessi** progetto di servizi di finestra di dialogo in un cloud di Visual Studio. Vi mostreremo come tooaccess e creare contenitori blob e come attività comuni tooperform caricamento, visualizzazione e il download di BLOB. Hello esempi sono scritti in C\# e utilizzare hello [Microsoft Azure Storage Client Library per .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).

Archiviazione Blob di Azure è un servizio per l'archiviazione di grandi quantità di dati non strutturati che è possibile accedere da qualsiasi in HelloWorld tramite HTTP o HTTPS. Un singolo BLOB può avere qualsiasi dimensione. I BLOB possono essere costituiti da immagini, file audio e video, dati non elaborati e file di documento.

I BLOB di archiviazione si trovano nei contenitori esattamente come i file si trovano nelle cartelle. Dopo aver creato uno spazio di archiviazione, creare uno o più contenitori in archiviazione hello. Ad esempio, nell'archiviazione chiamato "Raccoglitore", è possibile creare contenitori nel servizio di archiviazione hello chiamato immagini toostore "immagini" e un altro denominato "audio" toostore file audio. Dopo aver creato i contenitori di hello, è possibile caricare blob singoli file toothem.

* Per altre informazioni sulla modifica dei BLOB a livello di codice, vedere [Introduzione all'archiviazione BLOB di Azure con .NET](storage-dotnet-how-to-use-blobs.md).
* Per informazioni generali sull'Archiviazione di Azure, vedere [la documentazione relativa all'archiviazione](https://azure.microsoft.com/documentation/services/storage/).
* Per informazioni generali sui servizi cloud di Azure, vedere [la documentazione sui servizi cloud](https://azure.microsoft.com/documentation/services/cloud-services/).
* Per altre informazioni sulla programmazione delle applicazioni ASP.NET, vedere [ASP.NET](http://www.asp.net).

## <a name="access-blob-containers-in-code"></a>Accesso ai contenitori BLOB nel codice
tooprogrammatically Accedi ai BLOB in progetti di servizi cloud, è necessario hello tooadd seguenti elementi, se non sono già presenti.

1. Aggiungere hello seguente di codice lo spazio dei nomi dichiarazioni toohello superiore di qualsiasi file c# in cui si desidera tooprogrammatically accesso di archiviazione di Azure.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. Ottenere un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione. Hello utilizzare seguente tooget codice hello la stringa di connessione di archiviazione e informazioni sull'account di archiviazione dalla configurazione del servizio Azure hello.
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        CloudConfigurationManager.GetSetting("<storage account name>_AzureStorageConnectionString"));
3. Ottenere un **CloudBlobClient** tooreference un contenitore esistente nell'account di archiviazione dell'oggetto.
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
4. Ottenere un **CloudBlobContainer** tooreference un contenitore di blob specifico dell'oggetto.
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

> [!NOTE]
> Utilizzare tutto il codice hello illustrato nella procedura precedente di hello davanti codice hello di hello le sezioni seguenti.
> 
> 

## <a name="create-a-container-in-code"></a>Creazione di un contenitore nel codice
> [!NOTE]
> Alcune API che eseguono chiamate tooAzure archiviazione in ASP.NET sono asincrone. Per ulteriori informazioni, vedere [Programmazione asincrona con Async e Await](http://msdn.microsoft.com/library/hh191443.aspx) . codice Hello in hello di esempio seguente si presuppone che si utilizzano i metodi di programmazione asincrono.
> 
> 

toocreate un contenitore nell'account di archiviazione, è sufficiente toodo è aggiungere una chiamata troppo**CreateIfNotExistsAsync** come hello seguente codice:

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


toomake hello i file all'interno hello contenitore disponibili tooeveryone, è possibile impostare hello contenitore toobe pubblica utilizzando hello seguente codice.

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });


Chiunque sia connesso a Internet hello possa vedere i BLOB in un contenitore pubblico, ma è possibile modificarli o eliminarli solo se si dispone di hello chiave di accesso appropriati.

## <a name="upload-a-blob-into-a-container"></a>Caricare un BLOB in un contenitore
Archiviazione di Azure supporta BLOB in blocchi e BLOB di pagine. Nella maggior parte delle hello blob in blocchi è consigliata toouse tipo hello.

tooupload un blob in blocchi file tooa, ottenere un riferimento a un contenitore e usarlo tooget un riferimento di blob di blocco. Dopo aver creato un riferimento di blob, è possibile caricare qualsiasi flusso di dati tooit dal chiamante hello **UploadFromStream** metodo. Questa operazione crea blob hello se non esiste in precedenza o sovrascritto se esiste. Hello seguente esempio viene illustrato come tooupload un blob in un contenitore e si presuppone che il contenitore hello è già stato creato.

    // Retrieve a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with contents from a local file.
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        blockBlob.UploadFromStream(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a>Elenco di BLOB hello in un contenitore
BLOB di hello toolist in un contenitore, prima di ottenere un riferimento di contenitore. È quindi possibile utilizzare del contenitore hello **ListBlobs** BLOB hello tooretrieve di metodo e/o directory all'interno di esso. set completo di proprietà e metodi per un tipo restituito di hello tooaccess **IListBlobItem**, è necessario eseguirne il cast tooa **CloudBlockBlob**, **CloudPageBlob**, o  **CloudBlobDirectory** oggetto. Se il tipo di hello è sconosciuto, è possibile utilizzare un toodetermine di controllo di tipo quali toocast a. Hello codice seguente viene illustrato come tooretrieve e output di hello URI di ogni elemento nel hello **foto** contenitore:

    // Loop over items within hello container and output hello length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, false))
    {
        if (item.GetType() == typeof(CloudBlockBlob))
        {
            CloudBlockBlob blob = (CloudBlockBlob)item;

            Console.WriteLine("Block blob of length {0}: {1}", blob.Properties.Length, blob.Uri);

        }
        else if (item.GetType() == typeof(CloudPageBlob))
        {
            CloudPageBlob pageBlob = (CloudPageBlob)item;

            Console.WriteLine("Page blob of length {0}: {1}", pageBlob.Properties.Length, pageBlob.Uri);

        }
        else if (item.GetType() == typeof(CloudBlobDirectory))
        {
            CloudBlobDirectory directory = (CloudBlobDirectory)item;

            Console.WriteLine("Directory: {0}", directory.Uri);
        }
    }

Come illustrato nell'esempio di codice hello precedente, il concetto di hello di directory all'interno di contenitori, servizio blob hello. È quindi possibile organizzare i BLOB in una struttura più simile a quella delle cartelle. Si consideri ad esempio hello seguente set di BLOB in blocchi in un contenitore denominato **foto**:

    photo1.jpg
    2010/architecture/description.txt
    2010/architecture/photo3.jpg
    2010/architecture/photo4.jpg
    2011/architecture/photo5.jpg
    2011/architecture/photo6.jpg
    2011/architecture/description.txt
    2011/photo7.jpg

Quando si chiama **ListBlobs** nel contenitore di hello (come nell'esempio precedente del hello), raccolta hello restituita contiene **CloudBlobDirectory** e **CloudBlockBlob** oggetti che rappresenta la directory hello e BLOB contenuti al livello superiore di hello. Di seguito è riportato l'output risultante hello:

    Directory: https://<accountname>.blob.core.windows.net/photos/2010/
    Directory: https://<accountname>.blob.core.windows.net/photos/2011/
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg


Facoltativamente, è possibile impostare hello **UseFlatBlobListing** parametro di hello **ListBlobs** metodo **true**. In questo modo tutti i BLOB verranno restituiti come **CloudBlockBlob**, indipendentemente dalla directory. Ecco la chiamata di hello troppo**ListBlobs**:

    // Loop over items within hello container and output hello length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, true))
    {
       ...
    }

e di seguito sono riportati i risultati di hello:

    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
    Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
    Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
    Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
    Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
    Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg

Per altre informazioni, vedere [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).

## <a name="download-blobs"></a>Scaricare BLOB
BLOB toodownload, recuperare innanzitutto un riferimento di blob e quindi chiamare hello **metodi DownloadToStream** metodo. esempio Hello utilizza hello **metodi DownloadToStream** metodo tootransfer hello blob contenuto tooa oggetto flusso che può quindi rendere persistente tooa file locale.

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save blob contents tooa file.
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        blockBlob.DownloadToStream(fileStream);
    }

È inoltre possibile utilizzare hello **metodi DownloadToStream** contenuto hello toodownload di metodo di un blob come una stringa di testo.

    // Get a reference tooa blob named "myblob.txt"
    CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

    string text;
    using (var memoryStream = new MemoryStream())
    {
        blockBlob2.DownloadToStream(memoryStream);
        text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
    }

## <a name="delete-blobs"></a>Eliminare BLOB
un blob, toodelete innanzitutto ottenere un riferimento di blob e quindi chiamare il **eliminare** metodo.

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    blockBlob.Delete();


## <a name="list-blobs-in-pages-asynchronously"></a>Elencare BLOB nelle pagine in modalità asincrona
Elencare un numero elevato di BLOB, se si desidera toocontrol hello numero di risultati che restituito in un'unica operazione di elenco, è possibile elencare i BLOB di pagine di risultati. Questo esempio mostra la vista tooreturn dei risultati nelle pagine in modo asincrono, in modo che non l'esecuzione viene bloccata durante l'attesa tooreturn un ampio set di risultati.

Questo esempio viene illustrato un semplice elenco di blob, ma è anche possibile eseguire un elenco gerarchico, impostazione hello **useFlatBlobListing** parametro di hello **ListBlobsSegmentedAsync** metodo troppo **false**.

Poiché l'esempio hello chiama un metodo asincrono, devono essere preceduto da hello **async** (parola chiave) e deve restituire un **attività** oggetto. Hello await (parola chiave) specificato per hello **ListBlobsSegmentedAsync** metodo sospende l'esecuzione del metodo di esempio hello fino al completamento hello elenco attività.

    async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
    {
        // List blobs toohello console window, with paging.
        Console.WriteLine("List blobs in pages:");

        int i = 0;
        BlobContinuationToken continuationToken = null;
        BlobResultSegment resultSegment = null;

        // Call ListBlobsSegmentedAsync and enumerate hello result segment returned, while hello continuation token is non-null.
        // When hello continuation token is null, hello last page has been returned and execution can exit hello loop.
        do
        {
            // This overload allows control of hello page size. You can return all remaining results by passing null for hello maxResults parameter,
            // or by calling a different overload.
            resultSegment = await container.ListBlobsSegmentedAsync("", true, BlobListingDetails.All, 10, continuationToken, null, null);
            if (resultSegment.Results.Count<IListBlobItem>() > 0) { Console.WriteLine("Page {0}:", ++i); }
            foreach (var blobItem in resultSegment.Results)
            {
                Console.WriteLine("\t{0}", blobItem.StorageUri.PrimaryUri);
            }
            Console.WriteLine();

            //Get hello continuation token.
            continuationToken = resultSegment.ContinuationToken;
        }
        while (continuationToken != null);
    }

## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

