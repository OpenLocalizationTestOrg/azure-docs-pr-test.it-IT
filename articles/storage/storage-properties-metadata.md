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
# <a name="set-and-retrieve-properties-and-metadata"></a><span data-ttu-id="daf48-103">Impostare e recuperare proprietà e metadati</span><span class="sxs-lookup"><span data-stu-id="daf48-103">Set and retrieve properties and metadata</span></span>

<span data-ttu-id="daf48-104">Oggetti nella proprietà di sistema di supporto di archiviazione di Azure e i metadati definiti dall'utente, inoltre toohello dati in che essi contenuti.</span><span class="sxs-lookup"><span data-stu-id="daf48-104">Objects in Azure Storage support system properties and user-defined metadata, in addition toohello data they contain.</span></span> <span data-ttu-id="daf48-105">Questo articolo illustra la gestione delle proprietà di sistema e i metadati definiti dall'utente con hello [Azure Storage Client Library per .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span><span class="sxs-lookup"><span data-stu-id="daf48-105">This article discusses managing system properties and user-defined metadata with hello [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span>

* <span data-ttu-id="daf48-106">**Proprietà di sistema**: proprietà di sistema su ogni risorsa di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="daf48-106">**System properties**: System properties exist on each storage resource.</span></span> <span data-ttu-id="daf48-107">Alcune di esse possono essere lette o impostate, mentre altre sono di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="daf48-107">Some of them can be read or set, while others are read-only.</span></span> <span data-ttu-id="daf48-108">In realtà hello, alcune proprietà di sistema corrispondono a intestazioni HTTP standard toocertain.</span><span class="sxs-lookup"><span data-stu-id="daf48-108">Under hello covers, some system properties correspond toocertain standard HTTP headers.</span></span> <span data-ttu-id="daf48-109">libreria client di archiviazione di Azure Hello gestisce tale funzionalità.</span><span class="sxs-lookup"><span data-stu-id="daf48-109">hello Azure storage client library maintains these for you.</span></span>

* <span data-ttu-id="daf48-110">**I metadati definiti dall'utente**: i metadati definiti dall'utente sono i metadati specificati in una determinata risorsa in forma di hello di una coppia nome-valore.</span><span class="sxs-lookup"><span data-stu-id="daf48-110">**User-defined metadata**: User-defined metadata is metadata that you specify on a given resource in hello form of a name-value pair.</span></span> <span data-ttu-id="daf48-111">È possibile utilizzare i valori dei metadati toostore aggiuntivi con una risorsa di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="daf48-111">You can use metadata toostore additional values with a storage resource.</span></span> <span data-ttu-id="daf48-112">Questi valori di metadati aggiuntivi sono per solo le proprie esigenze e non influiscono sul comportamento delle risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="daf48-112">These additional metadata values are for your own purposes only, and do not affect how hello resource behaves.</span></span>

<span data-ttu-id="daf48-113">Il recupero dei valori di proprietà e dei metadati per una risorsa è un processo in due fasi.</span><span class="sxs-lookup"><span data-stu-id="daf48-113">Retrieving property and metadata values for a storage resource is a two-step process.</span></span> <span data-ttu-id="daf48-114">Prima di leggere questi valori, è necessario recuperarli in modo esplicito dal chiamante hello **FetchAttributes** metodo.</span><span class="sxs-lookup"><span data-stu-id="daf48-114">Before you can read these values, you must explicitly fetch them by calling hello **FetchAttributes** method.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="daf48-115">I valori di proprietà e i metadati per una risorsa di archiviazione non vengono popolati a meno che non si chiama uno dei hello **FetchAttributes** metodi.</span><span class="sxs-lookup"><span data-stu-id="daf48-115">Property and metadata values for a storage resource are not populated unless you call one of hello **FetchAttributes** methods.</span></span>
>
> <span data-ttu-id="daf48-116">Verrà visualizzato un messaggio `400 Bad Request`, se una qualsiasi coppia nome/valore contiene caratteri non ASCII.</span><span class="sxs-lookup"><span data-stu-id="daf48-116">You will receive a `400 Bad Request` if any name/value pairs contain non-ASCII characters.</span></span> <span data-ttu-id="daf48-117">Coppie nome/valore dei metadati sono intestazioni HTTP valide e pertanto devono essere conformi tooall restrizioni imposte sulle intestazioni HTTP.</span><span class="sxs-lookup"><span data-stu-id="daf48-117">Metadata name/value pairs are valid HTTP headers, and so must adhere tooall restrictions governing HTTP headers.</span></span> <span data-ttu-id="daf48-118">È quindi consigliabile usare la codifica URL o la codifica Base64 per i nomi e i valori contenenti caratteri non ASCII.</span><span class="sxs-lookup"><span data-stu-id="daf48-118">It is therefore recommended that you use URL encoding or Base64 encoding for names and values containing non-ASCII characters.</span></span>
>

## <a name="setting-and-retrieving-properties"></a><span data-ttu-id="daf48-119">Impostazione e recupero di proprietà</span><span class="sxs-lookup"><span data-stu-id="daf48-119">Setting and retrieving properties</span></span>
<span data-ttu-id="daf48-120">i valori delle proprietà tooretrieve, chiamata hello **FetchAttributes** metodo le proprietà di hello toopopulate blob o contenitore, quindi leggere i valori hello.</span><span class="sxs-lookup"><span data-stu-id="daf48-120">tooretrieve property values, call hello **FetchAttributes** method on your blob or container toopopulate hello properties, then read hello values.</span></span>

<span data-ttu-id="daf48-121">proprietà tooset su un oggetto, specificare il valore di proprietà hello, quindi chiamare hello **SetProperties** metodo.</span><span class="sxs-lookup"><span data-stu-id="daf48-121">tooset properties on an object, specify hello property value, then call hello **SetProperties** method.</span></span>

<span data-ttu-id="daf48-122">Hello esempio di codice seguente crea un contenitore, quindi scrive alcuni della relativa finestra della console tooa valori proprietà.</span><span class="sxs-lookup"><span data-stu-id="daf48-122">hello following code example creates a container, then writes some of its property values tooa console window.</span></span>

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

## <a name="setting-and-retrieving-metadata"></a><span data-ttu-id="daf48-123">Impostazione e recupero dei metadati</span><span class="sxs-lookup"><span data-stu-id="daf48-123">Setting and retrieving metadata</span></span>
<span data-ttu-id="daf48-124">È possibile specificare i metadati come uno o più coppie nome-valore in una risorsa BLOB o contenitore.</span><span class="sxs-lookup"><span data-stu-id="daf48-124">You can specify metadata as one or more name-value pairs on a blob or container resource.</span></span> <span data-ttu-id="daf48-125">i metadati tooset, aggiungere coppie nome-valore toohello **metadati** raccolta sulla risorsa hello, quindi chiamare hello **SetMetadata** hello toosave metodo valori toohello servizio.</span><span class="sxs-lookup"><span data-stu-id="daf48-125">tooset metadata, add name-value pairs toohello **Metadata** collection on hello resource, then call hello **SetMetadata** method toosave hello values toohello service.</span></span>

> [!NOTE]
> <span data-ttu-id="daf48-126">nome Hello dei metadati deve essere conforme toohello convenzioni di denominazione per gli identificatori c#.</span><span class="sxs-lookup"><span data-stu-id="daf48-126">hello name of your metadata must conform toohello naming conventions for C# identifiers.</span></span>
>
>

<span data-ttu-id="daf48-127">Hello esempio di codice seguente imposta i metadati in un contenitore.</span><span class="sxs-lookup"><span data-stu-id="daf48-127">hello following code example sets metadata on a container.</span></span> <span data-ttu-id="daf48-128">Un valore è impostato l'utilizzo dell'insieme di hello **Aggiungi** metodo.</span><span class="sxs-lookup"><span data-stu-id="daf48-128">One value is set using hello collection's **Add** method.</span></span> <span data-ttu-id="daf48-129">Hello altro valore viene impostato utilizzando la sintassi implicita chiave/valore.</span><span class="sxs-lookup"><span data-stu-id="daf48-129">hello other value is set using implicit key/value syntax.</span></span> <span data-ttu-id="daf48-130">Entrambi sono validi.</span><span class="sxs-lookup"><span data-stu-id="daf48-130">Both are valid.</span></span>

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

<span data-ttu-id="daf48-131">i metadati tooretrieve, chiamata hello **FetchAttributes** metodo hello il toopopulate blob o contenitore **metadati** raccolta, quindi leggere i valori hello, come illustrato nel seguente esempio hello.</span><span class="sxs-lookup"><span data-stu-id="daf48-131">tooretrieve metadata, call hello **FetchAttributes** method on your blob or container toopopulate hello **Metadata** collection, then read hello values, as shown in hello example below.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="daf48-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="daf48-132">Next steps</span></span>
* [<span data-ttu-id="daf48-133">Informazioni di riferimento sulla libreria client di archiviazione di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="daf48-133">Azure Storage Client Library for .NET reference</span></span>](/dotnet/api/?term=Microsoft.WindowsAzure.Storage)
* [<span data-ttu-id="daf48-134">Pacchetto NuGet per la libreria client di Archiviazione di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="daf48-134">Azure Storage Client Library for .NET NuGet package</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
