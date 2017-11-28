---
title: processo - v1 di importazione aaaSample del flusso di lavoro tooprep dischi rigidi per un'importazione/esportazione di Azure | Documenti Microsoft
description: "Una procedura dettagliata per il processo completo di hello la preparazione dell'unità per un processo di importazione in hello servizio importazione/esportazione di Azure, vedere."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 6eb1b1b7-c69f-4365-b5ef-3cd5e05eb72a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: f836fc6104d8b4ad5660cb110a62f61b40b0b7ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a><span data-ttu-id="3d98e-103">Unità disco rigido tooprepare del flusso di lavoro di esempio per un processo di importazione</span><span class="sxs-lookup"><span data-stu-id="3d98e-103">Sample workflow tooprepare hard drives for an import job</span></span>
<span data-ttu-id="3d98e-104">In questo argomento illustra hello processo completo di preparazione delle unità per un processo di importazione.</span><span class="sxs-lookup"><span data-stu-id="3d98e-104">This topic walks you through hello complete process of preparing drives for an import job.</span></span>  
  
<span data-ttu-id="3d98e-105">Questo esempio vengono importati dati seguenti in un account di archiviazione Windows Azure denominato hello `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="3d98e-105">This example imports hello following data into a Window Azure storage account named `mystorageaccount`:</span></span>  
  
|<span data-ttu-id="3d98e-106">Percorso</span><span class="sxs-lookup"><span data-stu-id="3d98e-106">Location</span></span>|<span data-ttu-id="3d98e-107">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3d98e-107">Description</span></span>|  
|--------------|-----------------|  
|<span data-ttu-id="3d98e-108">H:\Video</span><span class="sxs-lookup"><span data-stu-id="3d98e-108">H:\Video</span></span>|<span data-ttu-id="3d98e-109">Una raccolta di video, 5 TB in totale.</span><span class="sxs-lookup"><span data-stu-id="3d98e-109">A collection of videos, 5 TB in total.</span></span>|  
|<span data-ttu-id="3d98e-110">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="3d98e-110">H:\Photo</span></span>|<span data-ttu-id="3d98e-111">Una raccolta di foto, 30 GB in totale.</span><span class="sxs-lookup"><span data-stu-id="3d98e-111">A collection of photos, 30 GB in total.</span></span>|  
|<span data-ttu-id="3d98e-112">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="3d98e-112">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="3d98e-113">Un'immagine di disco Blu-ray™, 25 GB.</span><span class="sxs-lookup"><span data-stu-id="3d98e-113">A Blu-Ray™ disk image, 25 GB.</span></span>|  
|<span data-ttu-id="3d98e-114">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="3d98e-114">\\\bigshare\john\music</span></span>|<span data-ttu-id="3d98e-115">Una raccolta di file musicali in una condivisione di rete, 10 GB in totale.</span><span class="sxs-lookup"><span data-stu-id="3d98e-115">A collection of music files on a network share, 10 GB in total.</span></span>|  
  
<span data-ttu-id="3d98e-116">Questi dati verrà importati il processo di importazione Hello in seguito le destinazioni nell'account di archiviazione hello hello:</span><span class="sxs-lookup"><span data-stu-id="3d98e-116">hello import job will import this data into hello following destinations in hello storage account:</span></span>  
  
|<span data-ttu-id="3d98e-117">Sorgente</span><span class="sxs-lookup"><span data-stu-id="3d98e-117">Source</span></span>|<span data-ttu-id="3d98e-118">BLOB o directory virtuale di destinazione</span><span class="sxs-lookup"><span data-stu-id="3d98e-118">Destination virtual directory or blob</span></span>|  
|------------|-------------------------------------------|  
|<span data-ttu-id="3d98e-119">H:\Video</span><span class="sxs-lookup"><span data-stu-id="3d98e-119">H:\Video</span></span>|<span data-ttu-id="3d98e-120">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="3d98e-120">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="3d98e-121">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="3d98e-121">H:\Photo</span></span>|<span data-ttu-id="3d98e-122">https://mystorageaccount.blob.core.windows.net/photo</span><span class="sxs-lookup"><span data-stu-id="3d98e-122">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="3d98e-123">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="3d98e-123">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="3d98e-124">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="3d98e-124">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="3d98e-125">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="3d98e-125">\\\bigshare\john\music</span></span>|<span data-ttu-id="3d98e-126">https://mystorageaccount.blob.core.windows.net/music</span><span class="sxs-lookup"><span data-stu-id="3d98e-126">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
<span data-ttu-id="3d98e-127">Con questo mapping, hello file `H:\Video\Drama\GreatMovie.mov` sarà blob importati toohello `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span><span class="sxs-lookup"><span data-stu-id="3d98e-127">With this mapping, hello file `H:\Video\Drama\GreatMovie.mov` will be imported toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>  
  
<span data-ttu-id="3d98e-128">Successivamente, toodetermine il numero di dischi rigido necessari, calcolo hello dimensioni dei dati hello:</span><span class="sxs-lookup"><span data-stu-id="3d98e-128">Next, toodetermine how many hard drives are needed, compute hello size of hello data:</span></span>  
  
`5TB + 30GB + 25GB + 10GB = 5TB + 65GB`  
  
<span data-ttu-id="3d98e-129">Per questo esempio, dovrebbero essere sufficienti due dischi rigidi da 3 TB.</span><span class="sxs-lookup"><span data-stu-id="3d98e-129">For this example, two 3TB hard drives should be sufficient.</span></span> <span data-ttu-id="3d98e-130">Tuttavia, poiché la directory di origine hello `H:\Video` include 5TB di dati e la capacità del disco rigido è di soli 3TB, è necessario toobreak `H:\Video` in due directory di dimensioni minori prima di eseguire lo strumento di importazione/esportazione di Microsoft Azure di hello: `H:\Video1` e `H:\Video2`.</span><span class="sxs-lookup"><span data-stu-id="3d98e-130">However, since hello source directory `H:\Video` has 5TB of data and your single hard drive's capacity is only 3TB, it's necessary toobreak `H:\Video` into two smaller directories before running hello Microsoft Azure Import/Export Tool: `H:\Video1` and `H:\Video2`.</span></span> <span data-ttu-id="3d98e-131">Questo passaggio vengono generate hello seguenti directory di origine:</span><span class="sxs-lookup"><span data-stu-id="3d98e-131">This step yields hello following source directories:</span></span>  
  
|<span data-ttu-id="3d98e-132">Percorso</span><span class="sxs-lookup"><span data-stu-id="3d98e-132">Location</span></span>|<span data-ttu-id="3d98e-133">Dimensione</span><span class="sxs-lookup"><span data-stu-id="3d98e-133">Size</span></span>|<span data-ttu-id="3d98e-134">BLOB o directory virtuale di destinazione</span><span class="sxs-lookup"><span data-stu-id="3d98e-134">Destination virtual directory or blob</span></span>|  
|--------------|----------|-------------------------------------------|  
|<span data-ttu-id="3d98e-135">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="3d98e-135">H:\Video1</span></span>|<span data-ttu-id="3d98e-136">2,5 TB</span><span class="sxs-lookup"><span data-stu-id="3d98e-136">2.5TB</span></span>|<span data-ttu-id="3d98e-137">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="3d98e-137">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="3d98e-138">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="3d98e-138">H:\Video2</span></span>|<span data-ttu-id="3d98e-139">2,5 TB</span><span class="sxs-lookup"><span data-stu-id="3d98e-139">2.5TB</span></span>|<span data-ttu-id="3d98e-140">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="3d98e-140">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="3d98e-141">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="3d98e-141">H:\Photo</span></span>|<span data-ttu-id="3d98e-142">30 GB</span><span class="sxs-lookup"><span data-stu-id="3d98e-142">30GB</span></span>|<span data-ttu-id="3d98e-143">https://mystorageaccount.blob.core.windows.net/photo</span><span class="sxs-lookup"><span data-stu-id="3d98e-143">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="3d98e-144">K:\Temp\FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="3d98e-144">K:\Temp\FavoriteMovies.ISO</span></span>|<span data-ttu-id="3d98e-145">25 GB</span><span class="sxs-lookup"><span data-stu-id="3d98e-145">25GB</span></span>|<span data-ttu-id="3d98e-146">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="3d98e-146">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="3d98e-147">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="3d98e-147">\\\bigshare\john\music</span></span>|<span data-ttu-id="3d98e-148">10 GB</span><span class="sxs-lookup"><span data-stu-id="3d98e-148">10GB</span></span>|<span data-ttu-id="3d98e-149">https://mystorageaccount.blob.core.windows.net/music</span><span class="sxs-lookup"><span data-stu-id="3d98e-149">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
 <span data-ttu-id="3d98e-150">Si noti che anche se hello `H:\Video`directory è stata divisa directory tootwo, puntano toohello stessa directory virtuale di destinazione nell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="3d98e-150">Note that even though hello `H:\Video`directory has been split tootwo directories, they point toohello same destination virtual directory in hello storage account.</span></span> <span data-ttu-id="3d98e-151">In questo modo, tutti i file video sono conservati in un unico `video` contenitore nell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="3d98e-151">This way, all video files are maintained under a single `video` container in hello storage account.</span></span>  
  
 <span data-ttu-id="3d98e-152">Successivamente, hello sopra origine directory sono uniformemente distribuite toohello due dischi rigidi:</span><span class="sxs-lookup"><span data-stu-id="3d98e-152">Next, hello above source directories are evenly distributed toohello two hard drives:</span></span>  
  
||||  
|-|-|-|  
|<span data-ttu-id="3d98e-153">Disco rigido</span><span class="sxs-lookup"><span data-stu-id="3d98e-153">Hard drive</span></span>|<span data-ttu-id="3d98e-154">Directory di origine</span><span class="sxs-lookup"><span data-stu-id="3d98e-154">Source directories</span></span>|<span data-ttu-id="3d98e-155">Dimensioni totali</span><span class="sxs-lookup"><span data-stu-id="3d98e-155">Total size</span></span>|  
|<span data-ttu-id="3d98e-156">Prima unità</span><span class="sxs-lookup"><span data-stu-id="3d98e-156">First Drive</span></span>|<span data-ttu-id="3d98e-157">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="3d98e-157">H:\Video1</span></span>|<span data-ttu-id="3d98e-158">2,5 TB + 30 GB</span><span class="sxs-lookup"><span data-stu-id="3d98e-158">2.5TB + 30GB</span></span>|  
||<span data-ttu-id="3d98e-159">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="3d98e-159">H:\Photo</span></span>||  
|<span data-ttu-id="3d98e-160">Seconda unità</span><span class="sxs-lookup"><span data-stu-id="3d98e-160">Second Drive</span></span>|<span data-ttu-id="3d98e-161">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="3d98e-161">H:\Video2</span></span>|<span data-ttu-id="3d98e-162">2,5 TB + 35 GB</span><span class="sxs-lookup"><span data-stu-id="3d98e-162">2.5TB + 35GB</span></span>|  
||<span data-ttu-id="3d98e-163">K:\Temp\BlueRay.ISO</span><span class="sxs-lookup"><span data-stu-id="3d98e-163">K:\Temp\BlueRay.ISO</span></span>||  
||<span data-ttu-id="3d98e-164">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="3d98e-164">\\\bigshare\john\music</span></span>||  
  
<span data-ttu-id="3d98e-165">Inoltre, è possibile impostare hello i metadati per tutti i file seguenti:</span><span class="sxs-lookup"><span data-stu-id="3d98e-165">In addition, you can set hello following metadata for all files:</span></span>  
  
-   <span data-ttu-id="3d98e-166">**UploadMethod:** servizio Importazione/Esportazione di Windows Azure</span><span class="sxs-lookup"><span data-stu-id="3d98e-166">**UploadMethod:** Windows Azure Import/Export service</span></span>  
  
-   <span data-ttu-id="3d98e-167">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="3d98e-167">**DataSetName:** SampleData</span></span>  
  
-   <span data-ttu-id="3d98e-168">**CreationDate:** 10/1/2013</span><span class="sxs-lookup"><span data-stu-id="3d98e-168">**CreationDate:** 10/1/2013</span></span>  
  
<span data-ttu-id="3d98e-169">tooset metadati per i file hello importato, creare un file di testo, `c:\WAImportExport\SampleMetadata.txt`, con hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="3d98e-169">tooset metadata for hello imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with hello following content:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="3d98e-170">È inoltre possibile impostare alcune proprietà per hello `FavoriteMovie.ISO` blob:</span><span class="sxs-lookup"><span data-stu-id="3d98e-170">You can also set some properties for hello `FavoriteMovie.ISO` blob:</span></span>  
  
-   <span data-ttu-id="3d98e-171">**Content-Type:** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="3d98e-171">**Content-Type:** application/octet-stream</span></span>  
  
-   <span data-ttu-id="3d98e-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span><span class="sxs-lookup"><span data-stu-id="3d98e-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>  
  
-   <span data-ttu-id="3d98e-173">**Cache-Control:** no-cache</span><span class="sxs-lookup"><span data-stu-id="3d98e-173">**Cache-Control:** no-cache</span></span>  
  
<span data-ttu-id="3d98e-174">tooset queste proprietà, creare un file di testo, `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="3d98e-174">tooset these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="3d98e-175">Si è ora pronto toorun hello strumento di importazione/esportazione di Azure tooprepare hello due unità disco rigido.</span><span class="sxs-lookup"><span data-stu-id="3d98e-175">Now you are ready toorun hello Azure Import/Export Tool tooprepare hello two hard drives.</span></span> <span data-ttu-id="3d98e-176">Si noti che:</span><span class="sxs-lookup"><span data-stu-id="3d98e-176">Note that:</span></span>  
  
-   <span data-ttu-id="3d98e-177">Hello prima unità viene montata come unità X.</span><span class="sxs-lookup"><span data-stu-id="3d98e-177">hello first drive is mounted as drive X.</span></span>  
  
-   <span data-ttu-id="3d98e-178">Hello seconda unità viene montata come unità Y.</span><span class="sxs-lookup"><span data-stu-id="3d98e-178">hello second drive is mounted as drive Y.</span></span>  
  
-   <span data-ttu-id="3d98e-179">chiave di Hello per l'account di archiviazione hello `mystorageaccount` è `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span><span class="sxs-lookup"><span data-stu-id="3d98e-179">hello key for hello storage account `mystorageaccount` is `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span></span>  

## <a name="preparing-disk-for-import-when-data-is-pre-loaded"></a><span data-ttu-id="3d98e-180">Preparazione del disco per l'importazione con dati precaricati</span><span class="sxs-lookup"><span data-stu-id="3d98e-180">Preparing disk for import when data is pre-loaded</span></span>
 
 <span data-ttu-id="3d98e-181">Se toobe dati hello importato è già presente nel disco hello, utilizzare /skipwrite flag hello.</span><span class="sxs-lookup"><span data-stu-id="3d98e-181">If hello data toobe imported is already present on hello disk, use hello flag /skipwrite.</span></span> <span data-ttu-id="3d98e-182">Valore di /t e /srcdir deve puntare toohello disco viene preparato per l'importazione.</span><span class="sxs-lookup"><span data-stu-id="3d98e-182">Value of /t and /srcdir both should point toohello disk being prepared for import.</span></span> <span data-ttu-id="3d98e-183">Se non tutti hello dati su disco hello deve toogo toohello stessa directory virtuale di destinazione o alla radice dell'account di archiviazione hello, esecuzione hello stesso comando per ogni directory separatamente mantenere il valore di hello del /id lo stesso in tutte le esecuzioni.</span><span class="sxs-lookup"><span data-stu-id="3d98e-183">If not all hello data on hello disk needs toogo toohello same destination virtual directory or root of hello storage account, run hello same command for each directory separately keeping hello value of /id same across all runs.</span></span>

>[!NOTE] 
><span data-ttu-id="3d98e-184">Non specificare /format come che verrà cancellare i dati di hello sul disco hello.</span><span class="sxs-lookup"><span data-stu-id="3d98e-184">Do not specify /format as it will wipe hello data on hello disk.</span></span> <span data-ttu-id="3d98e-185">È possibile specificare / crittografare o /bk a seconda se il disco di hello è già crittografato o meno.</span><span class="sxs-lookup"><span data-stu-id="3d98e-185">You can specify /encrypt or /bk depending on whether hello disk is already encrypted or not.</span></span> 
>

```
    When data is already present on hello disk for each drive run hello following command.
    WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:x:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt /skipwrite
```

## <a name="copy-sessions---first-drive"></a><span data-ttu-id="3d98e-186">Copiare le sessioni - prima unità</span><span class="sxs-lookup"><span data-stu-id="3d98e-186">Copy sessions - first drive</span></span>

<span data-ttu-id="3d98e-187">Per la prima unità hello, eseguire lo strumento di importazione/esportazione di Azure due volte i hello toocopy due origine hello directory:</span><span class="sxs-lookup"><span data-stu-id="3d98e-187">For hello first drive, run hello Azure Import/Export Tool twice toocopy hello two source directories:</span></span>  

<span data-ttu-id="3d98e-188">**Prima sessione di copia**</span><span class="sxs-lookup"><span data-stu-id="3d98e-188">**First copy session**</span></span>
  
```
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:H:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```

<span data-ttu-id="3d98e-189">**Seconda sessione di copia**</span><span class="sxs-lookup"><span data-stu-id="3d98e-189">**Second copy session**</span></span>

```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Photo /srcdir:H:\Photo /dstdir:photo/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt
```

## <a name="copy-sessions---second-drive"></a><span data-ttu-id="3d98e-190">Copiare le sessioni - seconda unità</span><span class="sxs-lookup"><span data-stu-id="3d98e-190">Copy sessions - second drive</span></span>
 
<span data-ttu-id="3d98e-191">Per hello seconda unità, eseguire hello strumento di importazione/esportazione di Azure tre volte, una volta per hello ogni directory di origine e una volta per hello autonoma Blu-Ray™ file di immagine):</span><span class="sxs-lookup"><span data-stu-id="3d98e-191">For hello second drive, run hello Azure Import/Export Tool three times, once each for hello source directories, and once for hello standalone Blu-Ray™ image file):</span></span>  
  
<span data-ttu-id="3d98e-192">**Prima sessione di copia**</span><span class="sxs-lookup"><span data-stu-id="3d98e-192">**First copy session**</span></span> 

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Video2 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:y /format /encrypt /srcdir:H:\Video2 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```
  
<span data-ttu-id="3d98e-193">**Seconda sessione di copia**</span><span class="sxs-lookup"><span data-stu-id="3d98e-193">**Second copy session**</span></span>

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Music /srcdir:\\bigshare\john\music /dstdir:music/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```  
  
<span data-ttu-id="3d98e-194">**Terza sessione di copia**</span><span class="sxs-lookup"><span data-stu-id="3d98e-194">**Third copy session**</span></span>  

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```

## <a name="copy-session-completion"></a><span data-ttu-id="3d98e-195">Completamento della sessione di copia</span><span class="sxs-lookup"><span data-stu-id="3d98e-195">Copy session completion</span></span>

<span data-ttu-id="3d98e-196">Dopo aver completato le sessioni di copia hello, è possibile disconnettere hello due unità dal computer di hello copia e spedirle toohello appropriato centro dati di Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="3d98e-196">Once hello copy sessions have completed, you can disconnect hello two drives from hello copy computer and ship them toohello appropriate Windows Azure data center.</span></span> <span data-ttu-id="3d98e-197">Carica file journal hello due, `FirstDrive.jrn` e `SecondDrive.jrn`, quando si crea il processo di importazione hello in hello [il portale di gestione di Windows Azure](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="3d98e-197">You'll upload hello two journal files, `FirstDrive.jrn` and `SecondDrive.jrn`, when you create hello import job in hello [Windows Azure Management Portal](https://manage.windowsazure.com/).</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="3d98e-198">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3d98e-198">Next steps</span></span>

* <span data-ttu-id="3d98e-199">[Preparing hard drives for an import job](storage-import-export-tool-preparing-hard-drives-import-v1.md) (Preparazione dei dischi rigidi per un processo di importazione)</span><span class="sxs-lookup"><span data-stu-id="3d98e-199">[Preparing hard drives for an import job](storage-import-export-tool-preparing-hard-drives-import-v1.md)</span></span>   
* <span data-ttu-id="3d98e-200">[Quick reference for frequently used commands](storage-import-export-tool-quick-reference-v1.md) (Riferimento rapido per i comandi usati più di frequente)</span><span class="sxs-lookup"><span data-stu-id="3d98e-200">[Quick reference for frequently used commands](storage-import-export-tool-quick-reference-v1.md)</span></span> 
