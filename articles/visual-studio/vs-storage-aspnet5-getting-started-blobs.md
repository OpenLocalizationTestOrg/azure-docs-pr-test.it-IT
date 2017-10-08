---
title: aaaGet generali di archiviazione blob e Visual Studio (ASP.NET Core) di servizi connessi | Documenti Microsoft
description: "La modalità di avvio utilizzando l'archiviazione Blob di Azure in un progetto di Visual Studio ASP.NET Core dopo aver creato un account di archiviazione usando Visual Studio tooget servizi connessi"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 094b596a-c92c-40c4-a0f5-86407ae79672
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 8eedf331896b21658c7b30a68a4391d8d60cd729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a>Introduzione all'archiviazione BLOB di Azure e ai relativi servizi di Visual Studio (ASP.NET Core)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Panoramica
Questo articolo descrive la modalità di avvio con archiviazione Blob di Azure in Visual Studio dopo aver creato o a cui fa riferimento a un account di archiviazione di Azure in un progetto ASP.NET Core utilizzando la finestra di Visual Studio aggiungere servizi connessi hello tooget.

Archiviazione Blob di Azure è un servizio per l'archiviazione di grandi quantità di dati non strutturati che è possibile accedere da qualsiasi in HelloWorld tramite HTTP o HTTPS. Un singolo BLOB può avere qualsiasi dimensione. I BLOB possono essere costituiti da immagini, file audio e video, dati non elaborati e file di documento. Questo articolo descrive la modalità di avvio tooget con archiviazione blob dopo aver creato un account di archiviazione di Azure tramite Visual Studio hello **aggiungere servizi connessi** finestra di dialogo in un progetto ASP.NET Core.

I BLOB di archiviazione si trovano nei contenitori esattamente come i file si trovano nelle cartelle. Dopo aver creato uno spazio di archiviazione, creare uno o più contenitori in archiviazione hello. Ad esempio, nell'archiviazione chiamato "Raccoglitore", è possibile creare contenitori nel servizio di archiviazione hello chiamato immagini toostore "immagini" e un altro denominato "audio" toostore file audio. Dopo aver creato i contenitori di hello, è possibile caricare blob singoli file toothem. Per altre informazioni sulla modifica dei BLOB a livello di codice, vedere [Introduzione all'archiviazione BLOB di Azure con .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) .

## <a name="access-blob-containers-in-code"></a>Accesso ai contenitori BLOB nel codice
tooprogrammatically Accedi ai BLOB in progetti ASP.NET Core, è necessario hello tooadd elementi, se non sono già presenti.

1. Aggiungere hello seguente di codice lo spazio dei nomi dichiarazioni toohello superiore di qualsiasi file c# in cui si desidera tooprogrammatically archiviazione di Azure.
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. Ottenere un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione. Utilizzare hello tooget di codice seguente la stringa di connessione di archiviazione e informazioni sull'account di archiviazione dalla configurazione del servizio Azure hello.
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    **Nota:** utilizzare tutti hello sopra codice codice hello in hello le sezioni seguenti.
3. Utilizzare un **CloudBlobClient** oggetto tooget un **CloudBlobContainer** contenitore esistente tooan di riferimento nell'account di archiviazione.
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a>Creazione di un contenitore nel codice
È inoltre possibile utilizzare hello **CloudBlobClient** toocreate un contenitore nell'account di archiviazione. È sufficiente toodo è una chiamata tooadd troppo**CreateIfNotExistsAsync** come hello seguente codice:

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference tooa container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


**Nota:** hello API che eseguono chiamate tooAzure archiviazione in ASP.NET Core sono asincrone. Per ulteriori informazioni, vedere [Programmazione asincrona con Async e Await](http://msdn.microsoft.com/library/hh191443.aspx) . codice Hello riportato di seguito si presuppone che vengono utilizzati i metodi di programmazione asincrono.

toomake hello i file all'interno hello contenitore disponibili tooeveryone, è possibile impostare hello contenitore toobe pubblica utilizzando hello seguente codice.

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a>Caricare un BLOB in un contenitore
tooupload un file blob in un contenitore, ottenere un riferimento a un contenitore e usarlo tooget un riferimento di blob. Dopo aver ottenuto un riferimento di blob, è possibile caricare qualsiasi flusso di dati tooit dal chiamante hello **UploadFromStreamAsync** metodo. Questa operazione crea blob hello se è già presente, o lo sovrascrive se esiste. Hello seguente esempio viene illustrato come tooupload un blob in un contenitore e si presuppone che il contenitore hello è già stato creato.

    // Get a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with hello contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a>Elenco di BLOB hello in un contenitore
BLOB di hello toolist in un contenitore, prima di ottenere un riferimento di contenitore. È quindi possibile chiamare del contenitore hello **ListBlobsSegmentedAsync** BLOB hello tooretrieve di metodo e/o directory all'interno di esso. set completo di proprietà e metodi per un tipo restituito di hello tooaccess **IListBlobItem**, è necessario eseguirne il cast tooa **CloudBlockBlob**, **CloudPageBlob**, o  **CloudBlobDirectory** oggetto. Se non si conosce blob hello tipo, è possibile utilizzare un toodetermine di controllo di tipo cui toocast in. Hello di codice seguente viene illustrato come tooretrieve e output di hello URI di ogni elemento in un contenitore.

    BlobContinuationToken token = null;
    do
    {
        BlobResultSegment resultSegment = await container.ListBlobsSegmentedAsync(token);
        token = resultSegment.ContinuationToken;

        foreach (IListBlobItem item in resultSegment.Results)
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
    } while (token != null);

Esistono altri modi toolist hello contenuto un contenitore blob. Per altre informazioni, vedere [Introduzione all'archiviazione BLOB di Azure con .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) .

## <a name="download-a-blob"></a>Scaricare un BLOB
ottenere innanzitutto un blob di riferimento toohello toodownload un blob e quindi chiamare hello **DownloadToStreamAsync** metodo. esempio Hello utilizza hello **DownloadToStreamAsync** metodo tootransfer hello blob contenuto tooa oggetto flusso che è quindi possibile salvare come file locale.

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save hello blob contents tooa file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

Esistono altri modi toosave BLOB come file. Per altre informazioni, vedere [Introduzione all'archiviazione BLOB di Azure con .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) .

## <a name="delete-a-blob"></a>Eliminare un BLOB
ottenere innanzitutto un blob di riferimento toohello toodelete un blob e quindi chiamare hello **DeleteAsync** metodo su di esso.

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

