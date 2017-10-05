---
title: "Impostare e recuperare proprietà e metadati degli oggetti in Archiviazione di Azure | Microsoft Docs"
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
ms.openlocfilehash: 6af66607478c58874f00bcf017a35abfc37888df
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="set-and-retrieve-properties-and-metadata"></a><span data-ttu-id="5223b-103">Impostare e recuperare proprietà e metadati</span><span class="sxs-lookup"><span data-stu-id="5223b-103">Set and retrieve properties and metadata</span></span>

<span data-ttu-id="5223b-104">Oggetti nelle proprietà di sistema di supporto di Archiviazione di Azure e metadati definiti dall'utente, oltre ai dati che contengono.</span><span class="sxs-lookup"><span data-stu-id="5223b-104">Objects in Azure Storage support system properties and user-defined metadata, in addition to the data they contain.</span></span> <span data-ttu-id="5223b-105">Questo articolo illustra la gestione delle proprietà di sistema e i metadati definiti dall'utente con la [Libreria client di archiviazione di Azure per .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span><span class="sxs-lookup"><span data-stu-id="5223b-105">This article discusses managing system properties and user-defined metadata with the [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span>

* <span data-ttu-id="5223b-106">**Proprietà di sistema**: proprietà di sistema su ogni risorsa di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5223b-106">**System properties**: System properties exist on each storage resource.</span></span> <span data-ttu-id="5223b-107">Alcune di esse possono essere lette o impostate, mentre altre sono di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="5223b-107">Some of them can be read or set, while others are read-only.</span></span> <span data-ttu-id="5223b-108">Anche se in modo non esplicito, alcune proprietà di sistema corrispondono a specifiche intestazioni HTTP standard.</span><span class="sxs-lookup"><span data-stu-id="5223b-108">Under the covers, some system properties correspond to certain standard HTTP headers.</span></span> <span data-ttu-id="5223b-109">La libreria client di archiviazione di Azure gestisce tale funzionalità.</span><span class="sxs-lookup"><span data-stu-id="5223b-109">The Azure storage client library maintains these for you.</span></span>

* <span data-ttu-id="5223b-110">**Metadati definiti dall'utente**: i metadati definiti dall'utente sono metadati specificati in una determinata risorsa, sotto forma di coppia nome-valore.</span><span class="sxs-lookup"><span data-stu-id="5223b-110">**User-defined metadata**: User-defined metadata is metadata that you specify on a given resource in the form of a name-value pair.</span></span> <span data-ttu-id="5223b-111">È possibile usare i metadati per archiviare valori aggiuntivi con una risorsa di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5223b-111">You can use metadata to store additional values with a storage resource.</span></span> <span data-ttu-id="5223b-112">Questi valori di metadati aggiuntivi sono solo per le proprie esigenze e non influiscono sul comportamento della risorsa.</span><span class="sxs-lookup"><span data-stu-id="5223b-112">These additional metadata values are for your own purposes only, and do not affect how the resource behaves.</span></span>

<span data-ttu-id="5223b-113">Il recupero dei valori di proprietà e dei metadati per una risorsa è un processo in due fasi.</span><span class="sxs-lookup"><span data-stu-id="5223b-113">Retrieving property and metadata values for a storage resource is a two-step process.</span></span> <span data-ttu-id="5223b-114">Prima di leggere questi valori, è necessario recuperarli in modo esplicito chiamando il metodo **FetchAttributes** .</span><span class="sxs-lookup"><span data-stu-id="5223b-114">Before you can read these values, you must explicitly fetch them by calling the **FetchAttributes** method.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5223b-115">I valori di proprietà e i metadati per una risorsa di archiviazione non vengono popolati a meno che non si chiami uno dei metodi **FetchAttributes** .</span><span class="sxs-lookup"><span data-stu-id="5223b-115">Property and metadata values for a storage resource are not populated unless you call one of the **FetchAttributes** methods.</span></span>
>
> <span data-ttu-id="5223b-116">Verrà visualizzato un messaggio `400 Bad Request`, se una qualsiasi coppia nome/valore contiene caratteri non ASCII.</span><span class="sxs-lookup"><span data-stu-id="5223b-116">You will receive a `400 Bad Request` if any name/value pairs contain non-ASCII characters.</span></span> <span data-ttu-id="5223b-117">Le coppie nome/valore di metadati sono intestazioni HTTP valide e devono essere conformi alle restrizioni imposte sulle intestazioni HTTP.</span><span class="sxs-lookup"><span data-stu-id="5223b-117">Metadata name/value pairs are valid HTTP headers, and so must adhere to all restrictions governing HTTP headers.</span></span> <span data-ttu-id="5223b-118">È quindi consigliabile usare la codifica URL o la codifica Base64 per i nomi e i valori contenenti caratteri non ASCII.</span><span class="sxs-lookup"><span data-stu-id="5223b-118">It is therefore recommended that you use URL encoding or Base64 encoding for names and values containing non-ASCII characters.</span></span>
>

## <a name="setting-and-retrieving-properties"></a><span data-ttu-id="5223b-119">Impostazione e recupero di proprietà</span><span class="sxs-lookup"><span data-stu-id="5223b-119">Setting and retrieving properties</span></span>
<span data-ttu-id="5223b-120">Per recuperare i valori della proprietà, chiamare il metodo **FetchAttributes** sul BLOB o sul contenitore per popolare le proprietà, quindi leggere i valori.</span><span class="sxs-lookup"><span data-stu-id="5223b-120">To retrieve property values, call the **FetchAttributes** method on your blob or container to populate the properties, then read the values.</span></span>

<span data-ttu-id="5223b-121">Per impostare le proprietà di un oggetto, specificare il valore della proprietà, quindi chiamare il metodo **SetProperties** .</span><span class="sxs-lookup"><span data-stu-id="5223b-121">To set properties on an object, specify the property value, then call the **SetProperties** method.</span></span>

<span data-ttu-id="5223b-122">L'esempio di codice seguente crea un contenitore e scrive alcuni dei valori delle proprietà in una finestra della console.</span><span class="sxs-lookup"><span data-stu-id="5223b-122">The following code example creates a container, then writes some of its property values to a console window.</span></span>

```csharp
//Parse the connection string for the storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

//Create the service client object for credentialed access to the Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference to a container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create the container if it does not already exist.
container.CreateIfNotExists();

// Fetch container properties and write out their values.
container.FetchAttributes();
Console.WriteLine("Properties for container {0}", container.StorageUri.PrimaryUri.ToString());
Console.WriteLine("LastModifiedUTC: {0}", container.Properties.LastModified.ToString());
Console.WriteLine("ETag: {0}", container.Properties.ETag);
Console.WriteLine();
```

## <a name="setting-and-retrieving-metadata"></a><span data-ttu-id="5223b-123">Impostazione e recupero dei metadati</span><span class="sxs-lookup"><span data-stu-id="5223b-123">Setting and retrieving metadata</span></span>
<span data-ttu-id="5223b-124">È possibile specificare i metadati come uno o più coppie nome-valore in una risorsa BLOB o contenitore.</span><span class="sxs-lookup"><span data-stu-id="5223b-124">You can specify metadata as one or more name-value pairs on a blob or container resource.</span></span> <span data-ttu-id="5223b-125">Per impostare i metadati, aggiungere coppie nome-valore alla raccolta **Metadati** nella risorsa, quindi chiamare il metodo **SetMetadata** per salvare i valori nel servizio.</span><span class="sxs-lookup"><span data-stu-id="5223b-125">To set metadata, add name-value pairs to the **Metadata** collection on the resource, then call the **SetMetadata** method to save the values to the service.</span></span>

> [!NOTE]
> <span data-ttu-id="5223b-126">Il nome dei metadati deve essere conforme alle convenzioni di denominazione degli identificatori C#.</span><span class="sxs-lookup"><span data-stu-id="5223b-126">The name of your metadata must conform to the naming conventions for C# identifiers.</span></span>
>
>

<span data-ttu-id="5223b-127">Il seguente codice di esempio imposta i metadati in un contenitore.</span><span class="sxs-lookup"><span data-stu-id="5223b-127">The following code example sets metadata on a container.</span></span> <span data-ttu-id="5223b-128">Un valore è impostato mediante l'utilizzo del metodo di raccolta **Aggiungi** .</span><span class="sxs-lookup"><span data-stu-id="5223b-128">One value is set using the collection's **Add** method.</span></span> <span data-ttu-id="5223b-129">L'altro valore è impostato utilizzando la sintassi implicita chiave/valore.</span><span class="sxs-lookup"><span data-stu-id="5223b-129">The other value is set using implicit key/value syntax.</span></span> <span data-ttu-id="5223b-130">Entrambi sono validi.</span><span class="sxs-lookup"><span data-stu-id="5223b-130">Both are valid.</span></span>

```csharp
public static void AddContainerMetadata(CloudBlobContainer container)
{
    //Add some metadata to the container.
    container.Metadata.Add("docType", "textDocuments");
    container.Metadata["category"] = "guidance";

    //Set the container's metadata.
    container.SetMetadata();
}
```

<span data-ttu-id="5223b-131">Per recuperare i metadati, chiamare il metodo **FetchAttributes** nel BLOB o nel contenitore per popolare la raccolta **Metadati**, quindi leggere i valori, come nell'esempio mostrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="5223b-131">To retrieve metadata, call the **FetchAttributes** method on your blob or container to populate the **Metadata** collection, then read the values, as shown in the example below.</span></span>

```csharp
public static void ListContainerMetadata(CloudBlobContainer container)
{
    //Fetch container attributes in order to populate the container's properties and metadata.
    container.FetchAttributes();

    //Enumerate the container's metadata.
    Console.WriteLine("Container metadata:");
    foreach (var metadataItem in container.Metadata)
    {
        Console.WriteLine("\tKey: {0}", metadataItem.Key);
        Console.WriteLine("\tValue: {0}", metadataItem.Value);
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="5223b-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5223b-132">Next steps</span></span>
* [<span data-ttu-id="5223b-133">Informazioni di riferimento sulla libreria client di archiviazione di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="5223b-133">Azure Storage Client Library for .NET reference</span></span>](/dotnet/api/?term=Microsoft.WindowsAzure.Storage)
* [<span data-ttu-id="5223b-134">Pacchetto NuGet per la libreria client di Archiviazione di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="5223b-134">Azure Storage Client Library for .NET NuGet package</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
