---
title: Gestire la scadenza di BLOB del servizio di archiviazione di Azure nella rete CDN di Azure | Documentazione Microsoft
description: Informazioni sulle opzioni per il controllo della durata per i BLOB nel caching della rete CDN di Azure.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: ad4801e9-d09a-49bf-b35c-efdc4e6034e8
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: d4741921806e443d92c385a04b781cec296c2ae8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="manage-expiration-of-azure-storage-blobs-in-azure-cdn"></a><span data-ttu-id="286db-103">Gestire la scadenza di BLOB del servizio di archiviazione di Azure nella rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="286db-103">Manage expiration of Azure Storage blobs in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="286db-104">App Web/Servizi cloud di Azure, ASP.NET o IIS</span><span class="sxs-lookup"><span data-stu-id="286db-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="286db-105">Servizio BLOB del servizio di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="286db-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="286db-106">Il [servizio BLOB](../storage/common/storage-introduction.md#blob-storage) di [Archiviazione di Azure](../storage/common/storage-introduction.md) è una delle diverse origini basate su Azure integrate nella rete CDN di Azure.</span><span class="sxs-lookup"><span data-stu-id="286db-106">The [blob service](../storage/common/storage-introduction.md#blob-storage) in [Azure Storage](../storage/common/storage-introduction.md) is one of several Azure-based origins integrated with Azure CDN.</span></span>  <span data-ttu-id="286db-107">Qualsiasi contenuto BLOB accessibile pubblicamente può essere memorizzato nella cache della rete CDN di Azure fino allo scadere della relativa durata (TTL).</span><span class="sxs-lookup"><span data-stu-id="286db-107">Any publicly accessible blob content can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="286db-108">La durata (TTL) è determinata dall' [*Cache-Control* ](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) nella risposta HTTP di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="286db-108">The TTL is determined by the [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in the HTTP response from Azure Storage.</span></span>

> [!TIP]
> <span data-ttu-id="286db-109">È possibile scegliere di non impostare alcuna durata (TTL) per un BLOB.</span><span class="sxs-lookup"><span data-stu-id="286db-109">You may choose to set no TTL on a blob.</span></span>  <span data-ttu-id="286db-110">In tal caso, la rete CDN di Azure applica automaticamente una durata (TTL) predefinita di sette giorni.</span><span class="sxs-lookup"><span data-stu-id="286db-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="286db-111">Per altre informazioni sull'uso della rete CDN di Azure per velocizzare l'accesso a BLOB e altri file, vedere la [panoramica della rete CDN di Azure](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="286db-111">For more information about how Azure CDN works to speed up access to blobs and other files, see the [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> <span data-ttu-id="286db-112">Per informazioni dettagliate sul servizio BLOB del servizio di Archiviazione di Azure, vedere [Concetti relativi al servizio BLOB](https://msdn.microsoft.com/library/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="286db-112">For more details on the Azure Storage blob service, see [Blob Service Concepts](https://msdn.microsoft.com/library/dd179376.aspx).</span></span> 
> 
> 

<span data-ttu-id="286db-113">Questa esercitazione illustra vari modi in cui è possibile impostare la durata (TTL) per un BLOB in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="286db-113">This tutorial demonstrates several ways that you can set the TTL on a blob in Azure Storage.</span></span>  

## <a name="azure-powershell"></a><span data-ttu-id="286db-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="286db-114">Azure PowerShell</span></span>
<span data-ttu-id="286db-115">[Azure PowerShell](/powershell/azure/overview) è uno dei modi più rapidi ed efficaci per amministrare i servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="286db-115">[Azure PowerShell](/powershell/azure/overview) is one of the quickest, most powerful ways to administer your Azure services.</span></span>  <span data-ttu-id="286db-116">Usare il cmdlet `Get-AzureStorageBlob` per ottenere un riferimento al BLOB, quindi impostare la proprietà `.ICloudBlob.Properties.CacheControl`.</span><span class="sxs-lookup"><span data-stu-id="286db-116">Use the `Get-AzureStorageBlob` cmdlet to get a reference to the blob, then set the `.ICloudBlob.Properties.CacheControl` property.</span></span> 

```powershell
# Create a storage context
$context = New-AzureStorageContext -StorageAccountName "<storage account name>" -StorageAccountKey "<storage account key>"

# Get a reference to the blob
$blob = Get-AzureStorageBlob -Context $context -Container "<container name>" -Blob "<blob name>"

# Set the CacheControl property to expire in 1 hour (3600 seconds)
$blob.ICloudBlob.Properties.CacheControl = "public, max-age=3600"

# Send the update to the cloud
$blob.ICloudBlob.SetProperties()
```

> [!TIP]
> <span data-ttu-id="286db-117">È anche possibile usare PowerShell per [gestire i profili e gli endpoint della rete CDN](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="286db-117">You can also use PowerShell to [manage your CDN profiles and endpoints](cdn-manage-powershell.md).</span></span>
> 
> 

## <a name="azure-storage-client-library-for-net"></a><span data-ttu-id="286db-118">Libreria client di archiviazione di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="286db-118">Azure Storage Client Library for .NET</span></span>
<span data-ttu-id="286db-119">Per impostare la durata (TTL) di un BLOB con .NET, usare la [libreria client di archiviazione di Azure per .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) per impostare la proprietà [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx).</span><span class="sxs-lookup"><span data-stu-id="286db-119">To set a blob's TTL using .NET, use the [Azure Storage Client Library for .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) to set the [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) property.</span></span>

```csharp
class Program
{
    const string connectionString = "<storage connection string>";
    static void Main()
    {
        // Retrieve storage account information from connection string
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);

        // Create a blob client for interacting with the blob service.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

        // Create a reference to the container
        CloudBlobContainer container = blobClient.GetContainerReference("<container name>");

        // Create a reference to the blob
        CloudBlob blob = container.GetBlobReference("<blob name>");

        // Set the CacheControl property to expire in 1 hour (3600 seconds)
        blob.Properties.CacheControl = "public, max-age=3600";

        // Update the blob's properties in the cloud
        blob.SetProperties();
    }
}
```

> [!TIP]
> <span data-ttu-id="286db-120">Molti altri esempi di codice .NET sono disponibili in [Azure Blob Storage Samples for .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)(Esempi di archivio BLOB di Azure per .NET).</span><span class="sxs-lookup"><span data-stu-id="286db-120">There are many more .NET code samples available in the [Azure Blob Storage Samples for .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span></span>
> 
> 

## <a name="other-methods"></a><span data-ttu-id="286db-121">Altri metodi</span><span class="sxs-lookup"><span data-stu-id="286db-121">Other methods</span></span>
* [<span data-ttu-id="286db-122">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="286db-122">Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)
  
    <span data-ttu-id="286db-123">Quando si carica il BLOB, impostare la proprietà *cacheControl* usando l'opzione `-p`.</span><span class="sxs-lookup"><span data-stu-id="286db-123">When uploading the blob, set the *cacheControl* property using the `-p` switch.</span></span>  <span data-ttu-id="286db-124">Questo esempio imposta la durata (TTL) su un'ora, ovvero 3.600 secondi.</span><span class="sxs-lookup"><span data-stu-id="286db-124">This example sets the TTL to one hour (3600 seconds).</span></span>
  
    ```text
    azure storage blob upload -c <connectionstring> -p cacheControl="public, max-age=3600" .\test.txt myContainer test.txt
    ```
* [<span data-ttu-id="286db-125">API REST dei servizi di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="286db-125">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
  
    <span data-ttu-id="286db-126">Impostare in modo esplicito la proprietà *x-ms-blob-cache-control* su una richiesta [Put Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [Put Block List](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx) o [Set Blob Properties](https://msdn.microsoft.com/library/azure/ee691966.aspx).</span><span class="sxs-lookup"><span data-stu-id="286db-126">Explicitly set the *x-ms-blob-cache-control* property on a [Put Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [Put Block List](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), or [Set Blob Properties](https://msdn.microsoft.com/library/azure/ee691966.aspx) request.</span></span>
* <span data-ttu-id="286db-127">Strumenti di gestione dell'archiviazione di terze parti</span><span class="sxs-lookup"><span data-stu-id="286db-127">Third-party storage management tools</span></span>
  
    <span data-ttu-id="286db-128">Alcuni strumenti di gestione di Archiviazione di Azure di terze parti consentono di impostare la proprietà *CacheControl* per i BLOB.</span><span class="sxs-lookup"><span data-stu-id="286db-128">Some third-party Azure Storage management tools allow you to set the *CacheControl* property on blobs.</span></span> 

## <a name="testing-the-cache-control-header"></a><span data-ttu-id="286db-129">Test dell'intestazione *Cache-Control*</span><span class="sxs-lookup"><span data-stu-id="286db-129">Testing the *Cache-Control* header</span></span>
<span data-ttu-id="286db-130">È possibile verificare facilmente la durata (TTL) dei BLOB.</span><span class="sxs-lookup"><span data-stu-id="286db-130">You can easily verify the TTL of your blobs.</span></span>  <span data-ttu-id="286db-131">Usare gli [strumenti di sviluppo](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/)del browser per verificare che il BLOB includa l'intestazione della risposta *Cache-Control* .</span><span class="sxs-lookup"><span data-stu-id="286db-131">Using your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), test that your blob is including the *Cache-Control* response header.</span></span>  <span data-ttu-id="286db-132">È anche possibile usare uno strumento come **wget**, [Postman](https://www.getpostman.com/) o [Fiddler](http://www.telerik.com/fiddler) per esaminare le intestazioni della risposta.</span><span class="sxs-lookup"><span data-stu-id="286db-132">You can also use a tool like **wget**, [Postman](https://www.getpostman.com/), or [Fiddler](http://www.telerik.com/fiddler) to examine the response headers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="286db-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="286db-133">Next Steps</span></span>
* [<span data-ttu-id="286db-134">Informazioni sull'intestazione *Cache-Control*</span><span class="sxs-lookup"><span data-stu-id="286db-134">Read about the *Cache-Control* header</span></span>](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)
* [<span data-ttu-id="286db-135">Informazioni su come gestire la scadenza del contenuto di Servizi cloud nella rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="286db-135">Learn how to manage expiration of Cloud Service content in Azure CDN</span></span>](cdn-manage-expiration-of-cloud-service-content.md)

