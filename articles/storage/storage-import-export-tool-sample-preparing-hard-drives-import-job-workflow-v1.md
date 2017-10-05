---
title: Flusso di lavoro di esempio per la preparazione dei dischi rigidi per un processo di importazione in Importazione/Esportazione di Azure - versione 1 | Documentazione Microsoft
description: "Viene illustrata una procedura dettagliata e completa per la preparazione delle unità per un processo di importazione nel servizio Importazione/Esportazione di Azure."
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
ms.openlocfilehash: 313f8c1f3962a943b4c98c530c324ff28aa84c10
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="sample-workflow-to-prepare-hard-drives-for-an-import-job"></a><span data-ttu-id="5e171-103">Flusso di lavoro campione per preparare i dischi rigidi per un processo di importazione</span><span class="sxs-lookup"><span data-stu-id="5e171-103">Sample workflow to prepare hard drives for an import job</span></span>
<span data-ttu-id="5e171-104">In questo argomento viene illustrato il processo completo di preparazione delle unità per un processo di importazione.</span><span class="sxs-lookup"><span data-stu-id="5e171-104">This topic walks you through the complete process of preparing drives for an import job.</span></span>  
  
<span data-ttu-id="5e171-105">In questo esempio verranno importati i seguenti dati di un account di archiviazione Windows Azure denominato `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="5e171-105">This example imports the following data into a Window Azure storage account named `mystorageaccount`:</span></span>  
  
|<span data-ttu-id="5e171-106">Percorso</span><span class="sxs-lookup"><span data-stu-id="5e171-106">Location</span></span>|<span data-ttu-id="5e171-107">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5e171-107">Description</span></span>|  
|--------------|-----------------|  
|<span data-ttu-id="5e171-108">H:\Video</span><span class="sxs-lookup"><span data-stu-id="5e171-108">H:\Video</span></span>|<span data-ttu-id="5e171-109">Una raccolta di video, 5 TB in totale.</span><span class="sxs-lookup"><span data-stu-id="5e171-109">A collection of videos, 5 TB in total.</span></span>|  
|<span data-ttu-id="5e171-110">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="5e171-110">H:\Photo</span></span>|<span data-ttu-id="5e171-111">Una raccolta di foto, 30 GB in totale.</span><span class="sxs-lookup"><span data-stu-id="5e171-111">A collection of photos, 30 GB in total.</span></span>|  
|<span data-ttu-id="5e171-112">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="5e171-112">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="5e171-113">Un'immagine di disco Blu-ray™, 25 GB.</span><span class="sxs-lookup"><span data-stu-id="5e171-113">A Blu-Ray™ disk image, 25 GB.</span></span>|  
|<span data-ttu-id="5e171-114">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="5e171-114">\\\bigshare\john\music</span></span>|<span data-ttu-id="5e171-115">Una raccolta di file musicali in una condivisione di rete, 10 GB in totale.</span><span class="sxs-lookup"><span data-stu-id="5e171-115">A collection of music files on a network share, 10 GB in total.</span></span>|  
  
<span data-ttu-id="5e171-116">Il processo importerà questi dati nelle seguenti destinazioni nell'account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="5e171-116">The import job will import this data into the following destinations in the storage account:</span></span>  
  
|<span data-ttu-id="5e171-117">Sorgente</span><span class="sxs-lookup"><span data-stu-id="5e171-117">Source</span></span>|<span data-ttu-id="5e171-118">BLOB o directory virtuale di destinazione</span><span class="sxs-lookup"><span data-stu-id="5e171-118">Destination virtual directory or blob</span></span>|  
|------------|-------------------------------------------|  
|<span data-ttu-id="5e171-119">H:\Video</span><span class="sxs-lookup"><span data-stu-id="5e171-119">H:\Video</span></span>|<span data-ttu-id="5e171-120">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="5e171-120">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="5e171-121">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="5e171-121">H:\Photo</span></span>|<span data-ttu-id="5e171-122">https://mystorageaccount.blob.core.windows.net/photo</span><span class="sxs-lookup"><span data-stu-id="5e171-122">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="5e171-123">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="5e171-123">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="5e171-124">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="5e171-124">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="5e171-125">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="5e171-125">\\\bigshare\john\music</span></span>|<span data-ttu-id="5e171-126">https://mystorageaccount.blob.core.windows.net/music</span><span class="sxs-lookup"><span data-stu-id="5e171-126">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
<span data-ttu-id="5e171-127">Con questo mapping, il file `H:\Video\Drama\GreatMovie.mov` verrà importato nel BLOB `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span><span class="sxs-lookup"><span data-stu-id="5e171-127">With this mapping, the file `H:\Video\Drama\GreatMovie.mov` will be imported to the blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>  
  
<span data-ttu-id="5e171-128">Successivamente, per determinare il numero di dischi rigidi necessari, calcolare la dimensione dei dati:</span><span class="sxs-lookup"><span data-stu-id="5e171-128">Next, to determine how many hard drives are needed, compute the size of the data:</span></span>  
  
`5TB + 30GB + 25GB + 10GB = 5TB + 65GB`  
  
<span data-ttu-id="5e171-129">Per questo esempio, dovrebbero essere sufficienti due dischi rigidi da 3 TB.</span><span class="sxs-lookup"><span data-stu-id="5e171-129">For this example, two 3TB hard drives should be sufficient.</span></span> <span data-ttu-id="5e171-130">Tuttavia, poiché la directory di origine `H:\Video` include 5 TB di dati e la capacità del singolo disco rigido è di soli 3 TB, è necessario suddividere `H:\Video` in due directory di dimensioni minori prima di eseguire lo strumento di importazione/esportazione di Microsoft Azure: `H:\Video1` e `H:\Video2`.</span><span class="sxs-lookup"><span data-stu-id="5e171-130">However, since the source directory `H:\Video` has 5TB of data and your single hard drive's capacity is only 3TB, it's necessary to break `H:\Video` into two smaller directories before running the Microsoft Azure Import/Export Tool: `H:\Video1` and `H:\Video2`.</span></span> <span data-ttu-id="5e171-131">Questo passaggio genera le seguenti directory di origine:</span><span class="sxs-lookup"><span data-stu-id="5e171-131">This step yields the following source directories:</span></span>  
  
|<span data-ttu-id="5e171-132">Percorso</span><span class="sxs-lookup"><span data-stu-id="5e171-132">Location</span></span>|<span data-ttu-id="5e171-133">Dimensione</span><span class="sxs-lookup"><span data-stu-id="5e171-133">Size</span></span>|<span data-ttu-id="5e171-134">BLOB o directory virtuale di destinazione</span><span class="sxs-lookup"><span data-stu-id="5e171-134">Destination virtual directory or blob</span></span>|  
|--------------|----------|-------------------------------------------|  
|<span data-ttu-id="5e171-135">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="5e171-135">H:\Video1</span></span>|<span data-ttu-id="5e171-136">2,5 TB</span><span class="sxs-lookup"><span data-stu-id="5e171-136">2.5TB</span></span>|<span data-ttu-id="5e171-137">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="5e171-137">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="5e171-138">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="5e171-138">H:\Video2</span></span>|<span data-ttu-id="5e171-139">2,5 TB</span><span class="sxs-lookup"><span data-stu-id="5e171-139">2.5TB</span></span>|<span data-ttu-id="5e171-140">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="5e171-140">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="5e171-141">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="5e171-141">H:\Photo</span></span>|<span data-ttu-id="5e171-142">30 GB</span><span class="sxs-lookup"><span data-stu-id="5e171-142">30GB</span></span>|<span data-ttu-id="5e171-143">https://mystorageaccount.blob.core.windows.net/photo</span><span class="sxs-lookup"><span data-stu-id="5e171-143">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="5e171-144">K:\Temp\FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="5e171-144">K:\Temp\FavoriteMovies.ISO</span></span>|<span data-ttu-id="5e171-145">25 GB</span><span class="sxs-lookup"><span data-stu-id="5e171-145">25GB</span></span>|<span data-ttu-id="5e171-146">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="5e171-146">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="5e171-147">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="5e171-147">\\\bigshare\john\music</span></span>|<span data-ttu-id="5e171-148">10 GB</span><span class="sxs-lookup"><span data-stu-id="5e171-148">10GB</span></span>|<span data-ttu-id="5e171-149">https://mystorageaccount.blob.core.windows.net/music</span><span class="sxs-lookup"><span data-stu-id="5e171-149">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
 <span data-ttu-id="5e171-150">Si noti che anche se la directory `H:\Video` è stata suddivisa in due, queste ultime puntano alla stessa directory virtuale di destinazione nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5e171-150">Note that even though the `H:\Video`directory has been split to two directories, they point to the same destination virtual directory in the storage account.</span></span> <span data-ttu-id="5e171-151">In questo modo, tutti i file video verranno conservati in un singolo contenitore `video` nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5e171-151">This way, all video files are maintained under a single `video` container in the storage account.</span></span>  
  
 <span data-ttu-id="5e171-152">Successivamente, le directory di origine indicate in precedenza vengono distribuite uniformemente nei due dischi rigidi:</span><span class="sxs-lookup"><span data-stu-id="5e171-152">Next, the above source directories are evenly distributed to the two hard drives:</span></span>  
  
||||  
|-|-|-|  
|<span data-ttu-id="5e171-153">Disco rigido</span><span class="sxs-lookup"><span data-stu-id="5e171-153">Hard drive</span></span>|<span data-ttu-id="5e171-154">Directory di origine</span><span class="sxs-lookup"><span data-stu-id="5e171-154">Source directories</span></span>|<span data-ttu-id="5e171-155">Dimensioni totali</span><span class="sxs-lookup"><span data-stu-id="5e171-155">Total size</span></span>|  
|<span data-ttu-id="5e171-156">Prima unità</span><span class="sxs-lookup"><span data-stu-id="5e171-156">First Drive</span></span>|<span data-ttu-id="5e171-157">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="5e171-157">H:\Video1</span></span>|<span data-ttu-id="5e171-158">2,5 TB + 30 GB</span><span class="sxs-lookup"><span data-stu-id="5e171-158">2.5TB + 30GB</span></span>|  
||<span data-ttu-id="5e171-159">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="5e171-159">H:\Photo</span></span>||  
|<span data-ttu-id="5e171-160">Seconda unità</span><span class="sxs-lookup"><span data-stu-id="5e171-160">Second Drive</span></span>|<span data-ttu-id="5e171-161">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="5e171-161">H:\Video2</span></span>|<span data-ttu-id="5e171-162">2,5 TB + 35 GB</span><span class="sxs-lookup"><span data-stu-id="5e171-162">2.5TB + 35GB</span></span>|  
||<span data-ttu-id="5e171-163">K:\Temp\BlueRay.ISO</span><span class="sxs-lookup"><span data-stu-id="5e171-163">K:\Temp\BlueRay.ISO</span></span>||  
||<span data-ttu-id="5e171-164">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="5e171-164">\\\bigshare\john\music</span></span>||  
  
<span data-ttu-id="5e171-165">Inoltre, è possibile impostare i metadati seguenti per tutti i file:</span><span class="sxs-lookup"><span data-stu-id="5e171-165">In addition, you can set the following metadata for all files:</span></span>  
  
-   <span data-ttu-id="5e171-166">**UploadMethod:** servizio Importazione/Esportazione di Windows Azure</span><span class="sxs-lookup"><span data-stu-id="5e171-166">**UploadMethod:** Windows Azure Import/Export service</span></span>  
  
-   <span data-ttu-id="5e171-167">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="5e171-167">**DataSetName:** SampleData</span></span>  
  
-   <span data-ttu-id="5e171-168">**CreationDate:** 10/1/2013</span><span class="sxs-lookup"><span data-stu-id="5e171-168">**CreationDate:** 10/1/2013</span></span>  
  
<span data-ttu-id="5e171-169">Per impostare i metadati per i file importati, creare un file di testo, `c:\WAImportExport\SampleMetadata.txt`, con il contenuto seguente:</span><span class="sxs-lookup"><span data-stu-id="5e171-169">To set metadata for the imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with the following content:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="5e171-170">È inoltre possibile impostare alcune proprietà per il BLOB `FavoriteMovie.ISO`:</span><span class="sxs-lookup"><span data-stu-id="5e171-170">You can also set some properties for the `FavoriteMovie.ISO` blob:</span></span>  
  
-   <span data-ttu-id="5e171-171">**Content-Type:** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="5e171-171">**Content-Type:** application/octet-stream</span></span>  
  
-   <span data-ttu-id="5e171-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span><span class="sxs-lookup"><span data-stu-id="5e171-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>  
  
-   <span data-ttu-id="5e171-173">**Cache-Control:** no-cache</span><span class="sxs-lookup"><span data-stu-id="5e171-173">**Cache-Control:** no-cache</span></span>  
  
<span data-ttu-id="5e171-174">Per impostare queste proprietà, creare un file di testo, `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="5e171-174">To set these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="5e171-175">A questo punto è possibile eseguire lo strumento di importazione/esportazione di Azure per preparare i due dischi rigidi.</span><span class="sxs-lookup"><span data-stu-id="5e171-175">Now you are ready to run the Azure Import/Export Tool to prepare the two hard drives.</span></span> <span data-ttu-id="5e171-176">Si noti che:</span><span class="sxs-lookup"><span data-stu-id="5e171-176">Note that:</span></span>  
  
-   <span data-ttu-id="5e171-177">La prima unità viene montata come unità X.</span><span class="sxs-lookup"><span data-stu-id="5e171-177">The first drive is mounted as drive X.</span></span>  
  
-   <span data-ttu-id="5e171-178">La seconda unità viene montata come unità Y.</span><span class="sxs-lookup"><span data-stu-id="5e171-178">The second drive is mounted as drive Y.</span></span>  
  
-   <span data-ttu-id="5e171-179">La chiave per l'account di archiviazione `mystorageaccount` è `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span><span class="sxs-lookup"><span data-stu-id="5e171-179">The key for the storage account `mystorageaccount` is `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span></span>  

## <a name="preparing-disk-for-import-when-data-is-pre-loaded"></a><span data-ttu-id="5e171-180">Preparazione del disco per l'importazione con dati precaricati</span><span class="sxs-lookup"><span data-stu-id="5e171-180">Preparing disk for import when data is pre-loaded</span></span>
 
 <span data-ttu-id="5e171-181">Se i dati da importare sono già presenti sul disco, usare il flag /skipwrite.</span><span class="sxs-lookup"><span data-stu-id="5e171-181">If the data to be imported is already present on the disk, use the flag /skipwrite.</span></span> <span data-ttu-id="5e171-182">I valori di /t e /srcdir devono puntare entrambi al disco in preparazione per l'importazione.</span><span class="sxs-lookup"><span data-stu-id="5e171-182">Value of /t and /srcdir both should point to the disk being prepared for import.</span></span> <span data-ttu-id="5e171-183">Se non tutti i dati su disco devono essere trasferiti nella stessa directory virtuale di destinazione o root dell'account di archiviazione, eseguire il medesimo comando separatamente per ciascuna directory, mantenendo identico il valore di /id nelle varie esecuzioni.</span><span class="sxs-lookup"><span data-stu-id="5e171-183">If not all the data on the disk needs to go to the same destination virtual directory or root of the storage account, run the same command for each directory separately keeping the value of /id same across all runs.</span></span>

>[!NOTE] 
><span data-ttu-id="5e171-184">Non specificare /format in quanto comporterà l'eliminazione dei dati su disco.</span><span class="sxs-lookup"><span data-stu-id="5e171-184">Do not specify /format as it will wipe the data on the disk.</span></span> <span data-ttu-id="5e171-185">È possibile specificare /encrypt o /bk a seconda che il disco sia già crittografato o meno.</span><span class="sxs-lookup"><span data-stu-id="5e171-185">You can specify /encrypt or /bk depending on whether the disk is already encrypted or not.</span></span> 
>

```
    When data is already present on the disk for each drive run the following command.
    WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:x:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt /skipwrite
```

## <a name="copy-sessions---first-drive"></a><span data-ttu-id="5e171-186">Copiare le sessioni - prima unità</span><span class="sxs-lookup"><span data-stu-id="5e171-186">Copy sessions - first drive</span></span>

<span data-ttu-id="5e171-187">Per la prima unità, eseguire due volte lo strumento di importazione/esportazione di Azure per copiare le due directory di origine:</span><span class="sxs-lookup"><span data-stu-id="5e171-187">For the first drive, run the Azure Import/Export Tool twice to copy the two source directories:</span></span>  

<span data-ttu-id="5e171-188">**Prima sessione di copia**</span><span class="sxs-lookup"><span data-stu-id="5e171-188">**First copy session**</span></span>
  
```
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:H:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```

<span data-ttu-id="5e171-189">**Seconda sessione di copia**</span><span class="sxs-lookup"><span data-stu-id="5e171-189">**Second copy session**</span></span>

```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Photo /srcdir:H:\Photo /dstdir:photo/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt
```

## <a name="copy-sessions---second-drive"></a><span data-ttu-id="5e171-190">Copiare le sessioni - seconda unità</span><span class="sxs-lookup"><span data-stu-id="5e171-190">Copy sessions - second drive</span></span>
 
<span data-ttu-id="5e171-191">Per la seconda unità, eseguire tre volte lo strumento di importazione/esportazione di Azure, una volta per ciascuna delle due directory di origine e una volta per il file di immagine Blu-Ray™ autonomo:</span><span class="sxs-lookup"><span data-stu-id="5e171-191">For the second drive, run the Azure Import/Export Tool three times, once each for the source directories, and once for the standalone Blu-Ray™ image file):</span></span>  
  
<span data-ttu-id="5e171-192">**Prima sessione di copia**</span><span class="sxs-lookup"><span data-stu-id="5e171-192">**First copy session**</span></span> 

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Video2 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:y /format /encrypt /srcdir:H:\Video2 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```
  
<span data-ttu-id="5e171-193">**Seconda sessione di copia**</span><span class="sxs-lookup"><span data-stu-id="5e171-193">**Second copy session**</span></span>

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Music /srcdir:\\bigshare\john\music /dstdir:music/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```  
  
<span data-ttu-id="5e171-194">**Terza sessione di copia**</span><span class="sxs-lookup"><span data-stu-id="5e171-194">**Third copy session**</span></span>  

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```

## <a name="copy-session-completion"></a><span data-ttu-id="5e171-195">Completamento della sessione di copia</span><span class="sxs-lookup"><span data-stu-id="5e171-195">Copy session completion</span></span>

<span data-ttu-id="5e171-196">Dopo aver completato le sessioni di copia, è possibile disconnettere le due unità dal computer di copia e spedirle al data center di Windows Azure appropriato.</span><span class="sxs-lookup"><span data-stu-id="5e171-196">Once the copy sessions have completed, you can disconnect the two drives from the copy computer and ship them to the appropriate Windows Azure data center.</span></span> <span data-ttu-id="5e171-197">I due file journal, `FirstDrive.jrn` e `SecondDrive.jrn`, dovranno essere caricati durante la creazione del processo di importazione nel [portale di gestione di Windows Azure](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="5e171-197">You'll upload the two journal files, `FirstDrive.jrn` and `SecondDrive.jrn`, when you create the import job in the [Windows Azure Management Portal](https://manage.windowsazure.com/).</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="5e171-198">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5e171-198">Next steps</span></span>

* <span data-ttu-id="5e171-199">[Preparing hard drives for an import job](storage-import-export-tool-preparing-hard-drives-import-v1.md) (Preparazione dei dischi rigidi per un processo di importazione)</span><span class="sxs-lookup"><span data-stu-id="5e171-199">[Preparing hard drives for an import job](storage-import-export-tool-preparing-hard-drives-import-v1.md)</span></span>   
* <span data-ttu-id="5e171-200">[Quick reference for frequently used commands](storage-import-export-tool-quick-reference-v1.md) (Riferimento rapido per i comandi usati più di frequente)</span><span class="sxs-lookup"><span data-stu-id="5e171-200">[Quick reference for frequently used commands](storage-import-export-tool-quick-reference-v1.md)</span></span> 
