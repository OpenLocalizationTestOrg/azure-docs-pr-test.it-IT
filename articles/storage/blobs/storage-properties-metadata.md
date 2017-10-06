---
title: "aaaSet e recuperare l'oggetto proprietà e metadati in archiviazione di Azure | Documenti Microsoft"
description: "Archiviare i metadati personalizzati per oggetti di archiviazione di Azure, impostare e recuperare le proprietà di sistema."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 036f9006-273e-400b-844b-3329045e9e1f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: marsma
ms.openlocfilehash: 44f9243183014845964f337b476a6b0069dc0902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-and-retrieve-properties-and-metadata"></a>Impostare e recuperare proprietà e metadati

Oggetti nella proprietà di sistema di supporto di archiviazione di Azure e i metadati definiti dall'utente, inoltre toohello dati in che essi contenuti. Questo articolo illustra la gestione delle proprietà di sistema e i metadati definiti dall'utente con hello [Azure Storage Client Library per .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).

* **Proprietà di sistema**: proprietà di sistema su ogni risorsa di archiviazione. Alcune di esse possono essere lette o impostate, mentre altre sono di sola lettura. In realtà hello, alcune proprietà di sistema corrispondono a intestazioni HTTP standard toocertain. libreria client di archiviazione di Azure Hello gestisce tale funzionalità.

* **I metadati definiti dall'utente**: i metadati definiti dall'utente sono i metadati specificati in una determinata risorsa in forma di hello di una coppia nome-valore. È possibile utilizzare i valori dei metadati toostore aggiuntivi con una risorsa di archiviazione. Questi valori di metadati aggiuntivi sono per solo le proprie esigenze e non influiscono sul comportamento delle risorse di hello.

Il recupero dei valori di proprietà e dei metadati per una risorsa è un processo in due fasi. Prima di leggere questi valori, è necessario recuperarli in modo esplicito dal chiamante hello **FetchAttributes** metodo.

> [!IMPORTANT]
> I valori di proprietà e i metadati per una risorsa di archiviazione non vengono popolati a meno che non si chiama uno dei hello **FetchAttributes** metodi.
>
> Verrà visualizzato un messaggio `400 Bad Request`, se una qualsiasi coppia nome/valore contiene caratteri non ASCII. Coppie nome/valore dei metadati sono intestazioni HTTP valide e pertanto devono essere conformi tooall restrizioni imposte sulle intestazioni HTTP. È quindi consigliabile usare la codifica URL o la codifica Base64 per i nomi e i valori contenenti caratteri non ASCII.
>

## <a name="setting-and-retrieving-properties"></a>Impostazione e recupero di proprietà
i valori delle proprietà tooretrieve, chiamata hello **FetchAttributes** metodo le proprietà di hello toopopulate blob o contenitore, quindi leggere i valori hello.

proprietà tooset su un oggetto, specificare il valore di proprietà hello, quindi chiamare hello **SetProperties** metodo.

Hello esempio di codice seguente crea un contenitore, quindi scrive alcuni della relativa finestra della console tooa valori proprietà.

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

//Create hello service client object for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create hello container if it does not already exist.
container.CreateIfNotExists();

// Fetch container properties and write out their values.
container.FetchAttributes();
Console.WriteLine("Properties for container {0}", container.StorageUri.PrimaryUri.ToString());
Console.WriteLine("LastModifiedUTC: {0}", container.Properties.LastModified.ToString());
Console.WriteLine("ETag: {0}", container.Properties.ETag);
Console.WriteLine();
```

## <a name="setting-and-retrieving-metadata"></a>Impostazione e recupero dei metadati
È possibile specificare i metadati come uno o più coppie nome-valore in una risorsa BLOB o contenitore. i metadati tooset, aggiungere coppie nome-valore toohello **metadati** raccolta sulla risorsa hello, quindi chiamare hello **SetMetadata** hello toosave metodo valori toohello servizio.

> [!NOTE]
> nome Hello dei metadati deve essere conforme toohello convenzioni di denominazione per gli identificatori c#.
>
>

Hello esempio di codice seguente imposta i metadati in un contenitore. Un valore è impostato l'utilizzo dell'insieme di hello **Aggiungi** metodo. Hello altro valore viene impostato utilizzando la sintassi implicita chiave/valore. Entrambi sono validi.

```csharp
public static void AddContainerMetadata(CloudBlobContainer container)
{
    //Add some metadata toohello container.
    container.Metadata.Add("docType", "textDocuments");
    container.Metadata["category"] = "guidance";

    //Set hello container's metadata.
    container.SetMetadata();
}
```

i metadati tooretrieve, chiamata hello **FetchAttributes** metodo hello il toopopulate blob o contenitore **metadati** raccolta, quindi leggere i valori hello, come illustrato nel seguente esempio hello.

```csharp
public static void ListContainerMetadata(CloudBlobContainer container)
{
    //Fetch container attributes in order toopopulate hello container's properties and metadata.
    container.FetchAttributes();

    //Enumerate hello container's metadata.
    Console.WriteLine("Container metadata:");
    foreach (var metadataItem in container.Metadata)
    {
        Console.WriteLine("\tKey: {0}", metadataItem.Key);
        Console.WriteLine("\tValue: {0}", metadataItem.Value);
    }
}
```

## <a name="next-steps"></a>Passaggi successivi
* [Informazioni di riferimento sulla libreria client di archiviazione di Azure per .NET](/dotnet/api/?term=Microsoft.WindowsAzure.Storage)
* [Pacchetto NuGet per la libreria client di Archiviazione di Azure per .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)
