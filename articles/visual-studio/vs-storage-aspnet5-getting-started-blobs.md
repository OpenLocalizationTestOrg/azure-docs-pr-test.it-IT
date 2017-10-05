---
title: Introduzione all'archiviazione BLOB e ai servizi connessi di Visual Studio (ASP.NET Core) | Microsoft Docs
description: Informazioni su come iniziare a usare l'archiviazione BLOB di Azure in un progetto ASP.NET Core in Visual Studio dopo aver creato un account di archiviazione con i servizi connessi di Visual Studio
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
ms.openlocfilehash: 2e8060b44c395ad7c24e7778c0ef65148a3a45de
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a>Introduzione all'archiviazione BLOB di Azure e ai relativi servizi di Visual Studio (ASP.NET Core)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Panoramica
Questo articolo descrive come iniziare a usare l'archiviazione BLOB di Azure in Visual Studio dopo aver creato o fatto riferimento a un account di archiviazione di Azure in un progetto ASP.NET Core usando la finestra di dialogo Aggiungi servizi connessi di Visual Studio.

L'archiviazione BLOB di Azure è un servizio per l'archiviazione di quantità elevate di dati non strutturati a cui è possibile accedere da qualsiasi parte del mondo tramite HTTP o HTTPS. Un singolo BLOB può avere qualsiasi dimensione. I BLOB possono essere costituiti da immagini, file audio e video, dati non elaborati e file di documento. Questo articolo descrive come iniziare a usare l'archiviazione BLOB dopo la creazione di un account di archiviazione di Azure usando la finestra di dialogo **Aggiungi servizi connessi** di Visual Studio in un progetto ASP.NET Core.

I BLOB di archiviazione si trovano nei contenitori esattamente come i file si trovano nelle cartelle. Dopo aver creato una risorsa di archiviazione, è possibile creare uno o più contenitori nello spazio di archiviazione. Ad esempio, in una risorsa di archiviazione denominata "Raccoglitore" è possibile creare contenitori denominati "immagini" per archiviare immagini e un altro contenitore denominato "audio" per archiviare file audio. Dopo la creazione dei contenitori, sarà possibile caricarvi singoli file BLOB. Per altre informazioni sulla modifica dei BLOB a livello di codice, vedere [Introduzione all'archiviazione BLOB di Azure con .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) .

## <a name="access-blob-containers-in-code"></a>Accesso ai contenitori BLOB nel codice
Per accedere ai BLOB a livello di codice nei progetti ASP.NET Core, è necessario aggiungere gli elementi seguenti, se non sono già presenti.

1. Aggiungere le dichiarazioni dello spazio dei nomi del codice seguenti all'inizio del file C# in cui si desidera accedere ad Archiviazione di Azure a livello di codice:
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. Ottenere un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione. Usare il codice seguente per ottenere la stringa di connessione di archiviazione e le informazioni sull'account di archiviazione dalla configurazione del servizio di Azure.
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    **NOTA:** utilizzare tutto il codice riportato in precedenza prima del codice indicato nelle sezioni seguenti.
3. Usare un oggetto **CloudBlobClient** per ottenere un riferimento **CloudBlobContainer** a un contenitore esistente nell'account di archiviazione.
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference to a container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a>Creazione di un contenitore nel codice
È inoltre possibile utilizzare **CloudBlobClient** per creare un contenitore nell'account di archiviazione. È sufficiente aggiungere un richiamo a **CreateIfNotExistsAsync** come nel codice seguente:

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference to a container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


**NOTA:** le API che eseguono chiamate ad Archiviazione di Azure in ASP.NET Core sono asincrone. Per ulteriori informazioni, vedere [Programmazione asincrona con Async e Await](http://msdn.microsoft.com/library/hh191443.aspx) . Nel codice riportato di seguito si presuppone vengano utilizzati i metodi di programmazione asincrona.

Per rendere i file all'interno del contenitore disponibili a tutti, è possibile impostare il contenitore come pubblico utilizzando il codice seguente.

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a>Caricare un BLOB in un contenitore
Per caricare un file BLOB in un contenitore, ottenere un riferimento a un contenitore e usarlo per ottenere un riferimento a un BLOB. Dopo aver ottenuto un riferimento al BLOB, sarà possibile caricarvi qualsiasi flusso di dati chiamando il metodo **UploadFromStreamAsync** . Questa operazione crea il BLOB, se non esiste già, oppure lo sovrascrive se esiste già. Nell'esempio seguente viene illustrato come caricare un BLOB in un contenitore e si presuppone che il contenitore sia già stato creato.

    // Get a reference to a blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite the "myblob" blob with the contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-the-blobs-in-a-container"></a>Elencare i BLOB in un contenitore
Per elencare i BLOB in un contenitore, ottenere prima un riferimento al contenitore. Sarà quindi possibile chiamare il metodo **ListBlobsSegmentedAsync** del contenitore per recuperare i BLOB e/o le directory disponibili. Per accedere all'insieme avanzato di proprietà e metodi per un oggetto **IListBlobItem** restituito, è necessario eseguirne il cast in un oggetto **CloudBlockBlob**, **CloudPageBlob** o **CloudBlobDirectory**. Se il tipo del BLOB non è noto, è possibile usare un controllo del tipo per determinare quello in cui viene eseguito il cast. Nel codice seguente viene illustrato come recuperare e visualizzare l'URI di ogni elemento in un contenitore.

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

È possibile elencare i contenuti di un contenitore BLOB in altri modi. Per altre informazioni, vedere [Introduzione all'archiviazione BLOB di Azure con .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) .

## <a name="download-a-blob"></a>Scaricare un BLOB
Per scaricare un BLOB, ottenere prima di tutto un riferimento al BLOB, quindi chiamare il metodo **DownloadToStreamAsync** . Nell'esempio seguente viene utilizzato il metodo **DownloadToStreamAsync** per trasferire i contenuti del BLOB a un oggetto stream che è quindi possibile salvare come file locale.

    // Get a reference to a blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save the blob contents to a file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

È possibile salvare i BLOB come file in altri modi. Per altre informazioni, vedere [Introduzione all'archiviazione BLOB di Azure con .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) .

## <a name="delete-a-blob"></a>Eliminare un BLOB
Per eliminare un BLOB, ottenere prima di tutto un riferimento al BLOB, quindi chiamare il metodo **DeleteAsync** .

    // Get a reference to a blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete the blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

