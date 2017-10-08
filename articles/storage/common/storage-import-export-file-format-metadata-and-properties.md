---
title: "formato file metadati e proprietà aaaAzure importazione/esportazione | Documenti Microsoft"
description: "Informazioni su come toospecify metadati e le proprietà per uno o più blob che fanno parte di un'importazione o esportazione di processo."
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
ms.openlocfilehash: bb13c1f1a27baea77298cb224970cd521d02d8c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-metadata-and-properties-file-format"></a><span data-ttu-id="241c4-103">Formato di file dei metadati e delle proprietà di Importazione/Esportazione di Azure</span><span class="sxs-lookup"><span data-stu-id="241c4-103">Azure Import/Export service metadata and properties file format</span></span>
<span data-ttu-id="241c4-104">È possibile specificare i metadati e le proprietà per uno o più BLOB nell'ambito di un processo di importazione o esportazione.</span><span class="sxs-lookup"><span data-stu-id="241c4-104">You can specify metadata and properties for one or more blobs as part of an import job or an export job.</span></span> <span data-ttu-id="241c4-105">tooset metadati o proprietà per il BLOB viene creato come parte di un processo di importazione, fornire un file di metadati o delle proprietà nel disco rigido hello contenente hello toobe di dati importati.</span><span class="sxs-lookup"><span data-stu-id="241c4-105">tooset metadata or properties for blobs being created as part of an import job, you provide a metadata or properties file on hello hard drive containing hello data toobe imported.</span></span> <span data-ttu-id="241c4-106">Per un processo di esportazione, proprietà e i metadati vengono scritti tooa file di metadati o delle proprietà che è incluso nel disco rigido hello restituito tooyou.</span><span class="sxs-lookup"><span data-stu-id="241c4-106">For an export job, metadata and properties are written tooa metadata or properties file that is included on hello hard drive returned tooyou.</span></span>  
  
## <a name="metadata-file-format"></a><span data-ttu-id="241c4-107">Formato del file di metadati</span><span class="sxs-lookup"><span data-stu-id="241c4-107">Metadata file format</span></span>  
<span data-ttu-id="241c4-108">formato Hello di un file di metadati è il seguente:</span><span class="sxs-lookup"><span data-stu-id="241c4-108">hello format of a metadata file is as follows:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
[<metadata-name-1>metadata-value-1</metadata-name-1>]  
[<metadata-name-2>metadata-value-2</metadata-name-2>]  
. . .  
</Metadata>  
```
  
|<span data-ttu-id="241c4-109">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="241c4-109">XML Element</span></span>|<span data-ttu-id="241c4-110">Tipo</span><span class="sxs-lookup"><span data-stu-id="241c4-110">Type</span></span>|<span data-ttu-id="241c4-111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="241c4-111">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Metadata`|<span data-ttu-id="241c4-112">Elemento radice</span><span class="sxs-lookup"><span data-stu-id="241c4-112">Root element</span></span>|<span data-ttu-id="241c4-113">elemento radice di Hello hello del file di metadati.</span><span class="sxs-lookup"><span data-stu-id="241c4-113">hello root element of hello metadata file.</span></span>|  
|`metadata-name`|<span data-ttu-id="241c4-114">String</span><span class="sxs-lookup"><span data-stu-id="241c4-114">String</span></span>|<span data-ttu-id="241c4-115">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="241c4-115">Optional.</span></span> <span data-ttu-id="241c4-116">elemento XML Hello specifica il nome di hello di hello metadati per il blob hello e il relativo valore specifica il valore di hello dell'impostazione dei metadati hello.</span><span class="sxs-lookup"><span data-stu-id="241c4-116">hello XML element specifies hello name of hello metadata for hello blob, and its value specifies hello value of hello metadata setting.</span></span>|  
  
## <a name="properties-file-format"></a><span data-ttu-id="241c4-117">Formato del file delle proprietà</span><span class="sxs-lookup"><span data-stu-id="241c4-117">Properties file format</span></span>  
<span data-ttu-id="241c4-118">formato Hello di un file di proprietà è il seguente:</span><span class="sxs-lookup"><span data-stu-id="241c4-118">hello format of a properties file is as follows:</span></span>  
  
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
  
|<span data-ttu-id="241c4-119">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="241c4-119">XML Element</span></span>|<span data-ttu-id="241c4-120">Tipo</span><span class="sxs-lookup"><span data-stu-id="241c4-120">Type</span></span>|<span data-ttu-id="241c4-121">Descrizione</span><span class="sxs-lookup"><span data-stu-id="241c4-121">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Properties`|<span data-ttu-id="241c4-122">Elemento radice</span><span class="sxs-lookup"><span data-stu-id="241c4-122">Root element</span></span>|<span data-ttu-id="241c4-123">elemento radice di Hello del file delle proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="241c4-123">hello root element of hello properties file.</span></span>|  
|`Last-Modified`|<span data-ttu-id="241c4-124">String</span><span class="sxs-lookup"><span data-stu-id="241c4-124">String</span></span>|<span data-ttu-id="241c4-125">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="241c4-125">Optional.</span></span> <span data-ttu-id="241c4-126">ora ultima modifica Hello per blob hello.</span><span class="sxs-lookup"><span data-stu-id="241c4-126">hello last-modified time for hello blob.</span></span> <span data-ttu-id="241c4-127">Solo per i processi di esportazione.</span><span class="sxs-lookup"><span data-stu-id="241c4-127">For export jobs only.</span></span>|  
|`Etag`|<span data-ttu-id="241c4-128">String</span><span class="sxs-lookup"><span data-stu-id="241c4-128">String</span></span>|<span data-ttu-id="241c4-129">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="241c4-129">Optional.</span></span> <span data-ttu-id="241c4-130">Hello valore ETag del blob.</span><span class="sxs-lookup"><span data-stu-id="241c4-130">hello blob's ETag value.</span></span> <span data-ttu-id="241c4-131">Solo per i processi di esportazione.</span><span class="sxs-lookup"><span data-stu-id="241c4-131">For export jobs only.</span></span>|  
|`Content-Length`|<span data-ttu-id="241c4-132">String</span><span class="sxs-lookup"><span data-stu-id="241c4-132">String</span></span>|<span data-ttu-id="241c4-133">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="241c4-133">Optional.</span></span> <span data-ttu-id="241c4-134">dimensioni di Hello di hello blob in byte.</span><span class="sxs-lookup"><span data-stu-id="241c4-134">hello size of hello blob in bytes.</span></span> <span data-ttu-id="241c4-135">Solo per i processi di esportazione.</span><span class="sxs-lookup"><span data-stu-id="241c4-135">For export jobs only.</span></span>|  
|`Content-Type`|<span data-ttu-id="241c4-136">String</span><span class="sxs-lookup"><span data-stu-id="241c4-136">String</span></span>|<span data-ttu-id="241c4-137">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="241c4-137">Optional.</span></span> <span data-ttu-id="241c4-138">tipo di contenuto Hello del blob hello.</span><span class="sxs-lookup"><span data-stu-id="241c4-138">hello content type of hello blob.</span></span>|  
|`Content-MD5`|<span data-ttu-id="241c4-139">String</span><span class="sxs-lookup"><span data-stu-id="241c4-139">String</span></span>|<span data-ttu-id="241c4-140">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="241c4-140">Optional.</span></span> <span data-ttu-id="241c4-141">Hello hash MD5 del blob.</span><span class="sxs-lookup"><span data-stu-id="241c4-141">hello blob's MD5 hash.</span></span>|  
|`Content-Encoding`|<span data-ttu-id="241c4-142">String</span><span class="sxs-lookup"><span data-stu-id="241c4-142">String</span></span>|<span data-ttu-id="241c4-143">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="241c4-143">Optional.</span></span> <span data-ttu-id="241c4-144">contenuto del blob Hello codifica.</span><span class="sxs-lookup"><span data-stu-id="241c4-144">hello blob's content encoding.</span></span>|  
|`Content-Language`|<span data-ttu-id="241c4-145">String</span><span class="sxs-lookup"><span data-stu-id="241c4-145">String</span></span>|<span data-ttu-id="241c4-146">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="241c4-146">Optional.</span></span> <span data-ttu-id="241c4-147">Hello linguaggio del contenuto del blob.</span><span class="sxs-lookup"><span data-stu-id="241c4-147">hello blob's content language.</span></span>|  
|`Cache-Control`|<span data-ttu-id="241c4-148">String</span><span class="sxs-lookup"><span data-stu-id="241c4-148">String</span></span>|<span data-ttu-id="241c4-149">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="241c4-149">Optional.</span></span> <span data-ttu-id="241c4-150">stringa di controllo della cache Hello per blob hello.</span><span class="sxs-lookup"><span data-stu-id="241c4-150">hello cache control string for hello blob.</span></span>|  

## <a name="next-steps"></a><span data-ttu-id="241c4-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="241c4-151">Next steps</span></span>

<span data-ttu-id="241c4-152">Per le regole dettagliate sull'impostazione dei metadati e delle proprietà di un BLOB, vedere [Set blob properties](/rest/api/storageservices/set-blob-properties) (Impostare le proprietà di un BLOB), [Set Blob Metadata](/rest/api/storageservices/set-blob-metadata) (Impostare i metadati di un BLOB) e [Setting and retrieving properties and metadata for blob resources](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) (Impostazione e recupero di proprietà e metadati per le risorse BLOB).</span><span class="sxs-lookup"><span data-stu-id="241c4-152">See [Set blob properties](/rest/api/storageservices/set-blob-properties), [Set Blob Metadata](/rest/api/storageservices/set-blob-metadata), and [Setting and retrieving properties and metadata for blob resources](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) for detailed rules about setting blob metadata and properties.</span></span>
