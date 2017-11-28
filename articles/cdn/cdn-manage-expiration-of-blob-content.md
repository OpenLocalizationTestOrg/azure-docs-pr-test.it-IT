---
title: scadenza aaaManage di BLOB di archiviazione di Azure nella rete CDN di Azure | Documenti Microsoft
description: Informazioni sulle opzioni di hello per il controllo time-to-live per BLOB nella rete CDN di Azure la memorizzazione nella cache.
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
ms.openlocfilehash: 9fecae9639deb28977da7f851e1da4a823ddc4e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-expiration-of-azure-storage-blobs-in-azure-cdn"></a><span data-ttu-id="c6d0f-103">Gestire la scadenza di BLOB del servizio di archiviazione di Azure nella rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="c6d0f-103">Manage expiration of Azure Storage blobs in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c6d0f-104">App Web/Servizi cloud di Azure, ASP.NET o IIS</span><span class="sxs-lookup"><span data-stu-id="c6d0f-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="c6d0f-105">Servizio BLOB del servizio di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="c6d0f-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="c6d0f-106">Hello [servizio blob](../storage/common/storage-introduction.md#blob-storage) in [di archiviazione di Azure](../storage/common/storage-introduction.md) una delle diverse origini basato su Azure è integrata con la rete CDN Azure.</span><span class="sxs-lookup"><span data-stu-id="c6d0f-106">hello [blob service](../storage/common/storage-introduction.md#blob-storage) in [Azure Storage](../storage/common/storage-introduction.md) is one of several Azure-based origins integrated with Azure CDN.</span></span>  <span data-ttu-id="c6d0f-107">Qualsiasi contenuto BLOB accessibile pubblicamente può essere memorizzato nella cache della rete CDN di Azure fino allo scadere della relativa durata (TTL).</span><span class="sxs-lookup"><span data-stu-id="c6d0f-107">Any publicly accessible blob content can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="c6d0f-108">Hello durata (TTL) è determinato dal hello [ *Cache-Control* intestazione](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) nella risposta HTTP hello dall'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c6d0f-108">hello TTL is determined by hello [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in hello HTTP response from Azure Storage.</span></span>

> [!TIP]
> <span data-ttu-id="c6d0f-109">È non possibile scegliere tooset alcuna durata (TTL) su un blob.</span><span class="sxs-lookup"><span data-stu-id="c6d0f-109">You may choose tooset no TTL on a blob.</span></span>  <span data-ttu-id="c6d0f-110">In tal caso, la rete CDN di Azure applica automaticamente una durata (TTL) predefinita di sette giorni.</span><span class="sxs-lookup"><span data-stu-id="c6d0f-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="c6d0f-111">Per ulteriori informazioni sul funzionamento di toospeed tooblobs di accesso e altri file di rete CDN di Azure, vedere hello [Panoramica della rete CDN di Azure](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c6d0f-111">For more information about how Azure CDN works toospeed up access tooblobs and other files, see hello [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> <span data-ttu-id="c6d0f-112">Per ulteriori informazioni su hello servizio blob di archiviazione di Azure, vedere [concetti relativi al servizio Blob](https://msdn.microsoft.com/library/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="c6d0f-112">For more details on hello Azure Storage blob service, see [Blob Service Concepts](https://msdn.microsoft.com/library/dd179376.aspx).</span></span> 
> 
> 

<span data-ttu-id="c6d0f-113">Questa esercitazione illustra diversi modi, che è possibile impostare hello durata (TTL) su un blob in archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c6d0f-113">This tutorial demonstrates several ways that you can set hello TTL on a blob in Azure Storage.</span></span>  

## <a name="azure-powershell"></a><span data-ttu-id="c6d0f-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6d0f-114">Azure PowerShell</span></span>
<span data-ttu-id="c6d0f-115">[Azure PowerShell](/powershell/azure/overview) è uno dei hello modi più rapido ed efficiente tooadminister i servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="c6d0f-115">[Azure PowerShell](/powershell/azure/overview) is one of hello quickest, most powerful ways tooadminister your Azure services.</span></span>  <span data-ttu-id="c6d0f-116">Hello utilizzare `Get-AzureStorageBlob` tooget cmdlet un blob toohello di riferimento, quindi impostare hello `.ICloudBlob.Properties.CacheControl` proprietà.</span><span class="sxs-lookup"><span data-stu-id="c6d0f-116">Use hello `Get-AzureStorageBlob` cmdlet tooget a reference toohello blob, then set hello `.ICloudBlob.Properties.CacheControl` property.</span></span> 

```powershell
# Create a storage context
$context = New-AzureStorageContext -StorageAccountName "<storage account name>" -StorageAccountKey "<storage account key>"

# Get a reference toohello blob
$blob = Get-AzureStorageBlob -Context $context -Container "<container name>" -Blob "<blob name>"

# Set hello CacheControl property tooexpire in 1 hour (3600 seconds)
$blob.ICloudBlob.Properties.CacheControl = "public, max-age=3600"

# Send hello update toohello cloud
$blob.ICloudBlob.SetProperties()
```

> [!TIP]
> <span data-ttu-id="c6d0f-117">È inoltre possibile utilizzare PowerShell troppo[gestire i profili di rete CDN e l'endpoint](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c6d0f-117">You can also use PowerShell too[manage your CDN profiles and endpoints](cdn-manage-powershell.md).</span></span>
> 
> 

## <a name="azure-storage-client-library-for-net"></a><span data-ttu-id="c6d0f-118">Libreria client di archiviazione di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="c6d0f-118">Azure Storage Client Library for .NET</span></span>
<span data-ttu-id="c6d0f-119">tooset un blob di durata (TTL) utilizzando .NET, usare hello [Azure Storage Client Library per .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) tooset hello [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) proprietà.</span><span class="sxs-lookup"><span data-stu-id="c6d0f-119">tooset a blob's TTL using .NET, use hello [Azure Storage Client Library for .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) tooset hello [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) property.</span></span>

```csharp
class Program
{
    const string connectionString = "<storage connection string>";
    static void Main()
    {
        // Retrieve storage account information from connection string
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);

        // Create a blob client for interacting with hello blob service.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

        // Create a reference toohello container
        CloudBlobContainer container = blobClient.GetContainerReference("<container name>");

        // Create a reference toohello blob
        CloudBlob blob = container.GetBlobReference("<blob name>");

        // Set hello CacheControl property tooexpire in 1 hour (3600 seconds)
        blob.Properties.CacheControl = "public, max-age=3600";

        // Update hello blob's properties in hello cloud
        blob.SetProperties();
    }
}
```

> [!TIP]
> <span data-ttu-id="c6d0f-120">Sono disponibili molti altri esempi di codice .NET in hello [esempi di archiviazione Blob di Azure per .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="c6d0f-120">There are many more .NET code samples available in hello [Azure Blob Storage Samples for .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span></span>
> 
> 

## <a name="other-methods"></a><span data-ttu-id="c6d0f-121">Altri metodi</span><span class="sxs-lookup"><span data-stu-id="c6d0f-121">Other methods</span></span>
* [<span data-ttu-id="c6d0f-122">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="c6d0f-122">Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)
  
    <span data-ttu-id="c6d0f-123">Quando si carica blob hello, impostare hello *cacheControl* proprietà utilizzando hello `-p` passare.</span><span class="sxs-lookup"><span data-stu-id="c6d0f-123">When uploading hello blob, set hello *cacheControl* property using hello `-p` switch.</span></span>  <span data-ttu-id="c6d0f-124">In questo esempio hello TTL tooone ora (3600 secondi).</span><span class="sxs-lookup"><span data-stu-id="c6d0f-124">This example sets hello TTL tooone hour (3600 seconds).</span></span>
  
    ```text
    azure storage blob upload -c <connectionstring> -p cacheControl="public, max-age=3600" .\test.txt myContainer test.txt
    ```
* [<span data-ttu-id="c6d0f-125">API REST dei servizi di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="c6d0f-125">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
  
    <span data-ttu-id="c6d0f-126">In modo esplicito il set di hello *x-ms-blob-cache-control* proprietà in un [Put Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [inserire elenco Blocca](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), o [Set Blob Properties](https://msdn.microsoft.com/library/azure/ee691966.aspx) richiesta.</span><span class="sxs-lookup"><span data-stu-id="c6d0f-126">Explicitly set hello *x-ms-blob-cache-control* property on a [Put Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [Put Block List](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), or [Set Blob Properties](https://msdn.microsoft.com/library/azure/ee691966.aspx) request.</span></span>
* <span data-ttu-id="c6d0f-127">Strumenti di gestione dell'archiviazione di terze parti</span><span class="sxs-lookup"><span data-stu-id="c6d0f-127">Third-party storage management tools</span></span>
  
    <span data-ttu-id="c6d0f-128">Alcuni strumenti di gestione archiviazione di Azure di terze parti consentono di hello tooset *CacheControl* proprietà BLOB.</span><span class="sxs-lookup"><span data-stu-id="c6d0f-128">Some third-party Azure Storage management tools allow you tooset hello *CacheControl* property on blobs.</span></span> 

## <a name="testing-hello-cache-control-header"></a><span data-ttu-id="c6d0f-129">Test hello *Cache-Control* intestazione</span><span class="sxs-lookup"><span data-stu-id="c6d0f-129">Testing hello *Cache-Control* header</span></span>
<span data-ttu-id="c6d0f-130">È possibile verificare facilmente hello durata (TTL) del BLOB.</span><span class="sxs-lookup"><span data-stu-id="c6d0f-130">You can easily verify hello TTL of your blobs.</span></span>  <span data-ttu-id="c6d0f-131">Tramite il browser [gli strumenti di sviluppo](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), verificare che il blob è incluso hello *Cache-Control* intestazione della risposta.</span><span class="sxs-lookup"><span data-stu-id="c6d0f-131">Using your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), test that your blob is including hello *Cache-Control* response header.</span></span>  <span data-ttu-id="c6d0f-132">È inoltre possibile utilizzare uno strumento come **wget**, [Postman](https://www.getpostman.com/), o [Fiddler](http://www.telerik.com/fiddler) intestazioni di risposta tooexamine hello.</span><span class="sxs-lookup"><span data-stu-id="c6d0f-132">You can also use a tool like **wget**, [Postman](https://www.getpostman.com/), or [Fiddler](http://www.telerik.com/fiddler) tooexamine hello response headers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6d0f-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c6d0f-133">Next Steps</span></span>
* [<span data-ttu-id="c6d0f-134">Conoscenza hello *Cache-Control* intestazione</span><span class="sxs-lookup"><span data-stu-id="c6d0f-134">Read about hello *Cache-Control* header</span></span>](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)
* [<span data-ttu-id="c6d0f-135">Informazioni su come toomanage scadenza del contenuto del servizio Cloud nella rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="c6d0f-135">Learn how toomanage expiration of Cloud Service content in Azure CDN</span></span>](cdn-manage-expiration-of-cloud-service-content.md)

