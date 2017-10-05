---
title: "Formato di file dei metadati e delle proprietà del servizio Importazione/Esportazione di Azure | Documentazione Microsoft"
description: "Informazioni su come specificare i metadati e le proprietà per uno o più BLOB nell'ambito di un processo di importazione o esportazione."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 840364c6-d9a8-4b43-a9f3-f7441c625069
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 3f728ad94cdcbd32092b677f11a737ae91376720
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-importexport-service-metadata-and-properties-file-format"></a><span data-ttu-id="71136-103">Formato di file dei metadati e delle proprietà di Importazione/Esportazione di Azure</span><span class="sxs-lookup"><span data-stu-id="71136-103">Azure Import/Export service metadata and properties file format</span></span>
<span data-ttu-id="71136-104">È possibile specificare i metadati e le proprietà per uno o più BLOB nell'ambito di un processo di importazione o esportazione.</span><span class="sxs-lookup"><span data-stu-id="71136-104">You can specify metadata and properties for one or more blobs as part of an import job or an export job.</span></span> <span data-ttu-id="71136-105">Per impostare i metadati o le proprietà per i BLOB che vengono creati nell'ambito di un processo di importazione, occorre fornire un file di metadati o delle proprietà nel disco rigido contenente i dati da importare.</span><span class="sxs-lookup"><span data-stu-id="71136-105">To set metadata or properties for blobs being created as part of an import job, you provide a metadata or properties file on the hard drive containing the data to be imported.</span></span> <span data-ttu-id="71136-106">In un processo di esportazione, i metadati e le proprietà vengono scritti in un file di metadati o delle proprietà che viene incluso nel disco rigido restituito all'utente.</span><span class="sxs-lookup"><span data-stu-id="71136-106">For an export job, metadata and properties are written to a metadata or properties file that is included on the hard drive returned to you.</span></span>  
  
## <a name="metadata-file-format"></a><span data-ttu-id="71136-107">Formato del file di metadati</span><span class="sxs-lookup"><span data-stu-id="71136-107">Metadata file format</span></span>  
<span data-ttu-id="71136-108">Il formato del file di metadati è indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="71136-108">The format of a metadata file is as follows:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
[<metadata-name-1>metadata-value-1</metadata-name-1>]  
[<metadata-name-2>metadata-value-2</metadata-name-2>]  
. . .  
</Metadata>  
```
  
|<span data-ttu-id="71136-109">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="71136-109">XML Element</span></span>|<span data-ttu-id="71136-110">Tipo</span><span class="sxs-lookup"><span data-stu-id="71136-110">Type</span></span>|<span data-ttu-id="71136-111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="71136-111">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Metadata`|<span data-ttu-id="71136-112">Elemento radice</span><span class="sxs-lookup"><span data-stu-id="71136-112">Root element</span></span>|<span data-ttu-id="71136-113">L'elemento radice del file di metadati.</span><span class="sxs-lookup"><span data-stu-id="71136-113">The root element of the metadata file.</span></span>|  
|`metadata-name`|<span data-ttu-id="71136-114">string</span><span class="sxs-lookup"><span data-stu-id="71136-114">String</span></span>|<span data-ttu-id="71136-115">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="71136-115">Optional.</span></span> <span data-ttu-id="71136-116">L'elemento XML specifica il nome dei metadati per il BLOB e il relativo valore specifica il valore dell'impostazione dei metadati.</span><span class="sxs-lookup"><span data-stu-id="71136-116">The XML element specifies the name of the metadata for the blob, and its value specifies the value of the metadata setting.</span></span>|  
  
## <a name="properties-file-format"></a><span data-ttu-id="71136-117">Formato del file delle proprietà</span><span class="sxs-lookup"><span data-stu-id="71136-117">Properties file format</span></span>  
<span data-ttu-id="71136-118">Il formato di un file delle proprietà è indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="71136-118">The format of a properties file is as follows:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
[<Last-Modified>date-time-value</Last-Modified>]  
[<Etag>etag</Etag>]  
[<Content-Length>size-in-bytes<Content-Length>]  
[<Content-Type>content-type</Content-Type>]  
[<Content-MD5>content-md5</Content-MD5>]  
[<Content-Encoding>content-encoding</Content-Encoding>]  
[<Content-Language>content-language</Content-Language>]  
[<Cache-Control>cache-control</Cache-Control>]  
</Properties>  
```
  
|<span data-ttu-id="71136-119">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="71136-119">XML Element</span></span>|<span data-ttu-id="71136-120">Tipo</span><span class="sxs-lookup"><span data-stu-id="71136-120">Type</span></span>|<span data-ttu-id="71136-121">Descrizione</span><span class="sxs-lookup"><span data-stu-id="71136-121">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Properties`|<span data-ttu-id="71136-122">Elemento radice</span><span class="sxs-lookup"><span data-stu-id="71136-122">Root element</span></span>|<span data-ttu-id="71136-123">L'elemento radice del file delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="71136-123">The root element of the properties file.</span></span>|  
|`Last-Modified`|<span data-ttu-id="71136-124">String</span><span class="sxs-lookup"><span data-stu-id="71136-124">String</span></span>|<span data-ttu-id="71136-125">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="71136-125">Optional.</span></span> <span data-ttu-id="71136-126">L'ora dell'ultima modifica per il BLOB.</span><span class="sxs-lookup"><span data-stu-id="71136-126">The last-modified time for the blob.</span></span> <span data-ttu-id="71136-127">Solo per i processi di esportazione.</span><span class="sxs-lookup"><span data-stu-id="71136-127">For export jobs only.</span></span>|  
|`Etag`|<span data-ttu-id="71136-128">String</span><span class="sxs-lookup"><span data-stu-id="71136-128">String</span></span>|<span data-ttu-id="71136-129">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="71136-129">Optional.</span></span> <span data-ttu-id="71136-130">Il valore ETag del BLOB.</span><span class="sxs-lookup"><span data-stu-id="71136-130">The blob's ETag value.</span></span> <span data-ttu-id="71136-131">Solo per i processi di esportazione.</span><span class="sxs-lookup"><span data-stu-id="71136-131">For export jobs only.</span></span>|  
|`Content-Length`|<span data-ttu-id="71136-132">String</span><span class="sxs-lookup"><span data-stu-id="71136-132">String</span></span>|<span data-ttu-id="71136-133">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="71136-133">Optional.</span></span> <span data-ttu-id="71136-134">La dimensione del BLOB in byte.</span><span class="sxs-lookup"><span data-stu-id="71136-134">The size of the blob in bytes.</span></span> <span data-ttu-id="71136-135">Solo per i processi di esportazione.</span><span class="sxs-lookup"><span data-stu-id="71136-135">For export jobs only.</span></span>|  
|`Content-Type`|<span data-ttu-id="71136-136">String</span><span class="sxs-lookup"><span data-stu-id="71136-136">String</span></span>|<span data-ttu-id="71136-137">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="71136-137">Optional.</span></span> <span data-ttu-id="71136-138">Il tipo di contenuto del BLOB.</span><span class="sxs-lookup"><span data-stu-id="71136-138">The content type of the blob.</span></span>|  
|`Content-MD5`|<span data-ttu-id="71136-139">String</span><span class="sxs-lookup"><span data-stu-id="71136-139">String</span></span>|<span data-ttu-id="71136-140">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="71136-140">Optional.</span></span> <span data-ttu-id="71136-141">L'hash MD5 del BLOB.</span><span class="sxs-lookup"><span data-stu-id="71136-141">The blob's MD5 hash.</span></span>|  
|`Content-Encoding`|<span data-ttu-id="71136-142">String</span><span class="sxs-lookup"><span data-stu-id="71136-142">String</span></span>|<span data-ttu-id="71136-143">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="71136-143">Optional.</span></span> <span data-ttu-id="71136-144">La codifica del contenuto del BLOB.</span><span class="sxs-lookup"><span data-stu-id="71136-144">The blob's content encoding.</span></span>|  
|`Content-Language`|<span data-ttu-id="71136-145">String</span><span class="sxs-lookup"><span data-stu-id="71136-145">String</span></span>|<span data-ttu-id="71136-146">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="71136-146">Optional.</span></span> <span data-ttu-id="71136-147">La lingua del contenuto del BLOB.</span><span class="sxs-lookup"><span data-stu-id="71136-147">The blob's content language.</span></span>|  
|`Cache-Control`|<span data-ttu-id="71136-148">String</span><span class="sxs-lookup"><span data-stu-id="71136-148">String</span></span>|<span data-ttu-id="71136-149">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="71136-149">Optional.</span></span> <span data-ttu-id="71136-150">La stringa di controllo della cache per il BLOB.</span><span class="sxs-lookup"><span data-stu-id="71136-150">The cache control string for the blob.</span></span>|  

## <a name="next-steps"></a><span data-ttu-id="71136-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="71136-151">Next steps</span></span>

<span data-ttu-id="71136-152">Per le regole dettagliate sull'impostazione dei metadati e delle proprietà di un BLOB, vedere [Set blob properties](/rest/api/storageservices/set-blob-properties) (Impostare le proprietà di un BLOB), [Set Blob Metadata](/rest/api/storageservices/set-blob-metadata) (Impostare i metadati di un BLOB) e [Setting and retrieving properties and metadata for blob resources](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) (Impostazione e recupero di proprietà e metadati per le risorse BLOB).</span><span class="sxs-lookup"><span data-stu-id="71136-152">See [Set blob properties](/rest/api/storageservices/set-blob-properties), [Set Blob Metadata](/rest/api/storageservices/set-blob-metadata), and [Setting and retrieving properties and metadata for blob resources](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) for detailed rules about setting blob metadata and properties.</span></span>
