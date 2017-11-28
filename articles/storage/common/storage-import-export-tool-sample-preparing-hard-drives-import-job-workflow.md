---
title: processo di importazione aaaSample del flusso di lavoro tooprep dischi rigidi per un'importazione/esportazione di Azure | Documenti Microsoft
description: "Una procedura dettagliata per il processo completo di hello la preparazione dell'unità per un processo di importazione in hello servizio importazione/esportazione di Azure, vedere."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: muralikk
ms.openlocfilehash: fa7f36300b35b81757523de4960fd583bd4bf305
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a><span data-ttu-id="edb6c-103">Unità disco rigido tooprepare del flusso di lavoro di esempio per un processo di importazione</span><span class="sxs-lookup"><span data-stu-id="edb6c-103">Sample workflow tooprepare hard drives for an import job</span></span>

<span data-ttu-id="edb6c-104">In questo articolo illustra hello processo completo di preparazione delle unità per un processo di importazione.</span><span class="sxs-lookup"><span data-stu-id="edb6c-104">This article walks you through hello complete process of preparing drives for an import job.</span></span>

## <a name="sample-data"></a><span data-ttu-id="edb6c-105">Dati di esempio</span><span class="sxs-lookup"><span data-stu-id="edb6c-105">Sample data</span></span>

<span data-ttu-id="edb6c-106">Questo esempio vengono importati dati seguenti in un account di archiviazione di Azure denominato hello `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="edb6c-106">This example imports hello following data into an Azure storage account named `mystorageaccount`:</span></span>

|<span data-ttu-id="edb6c-107">Percorso</span><span class="sxs-lookup"><span data-stu-id="edb6c-107">Location</span></span>|<span data-ttu-id="edb6c-108">Descrizione</span><span class="sxs-lookup"><span data-stu-id="edb6c-108">Description</span></span>|<span data-ttu-id="edb6c-109">Dimensioni dei dati</span><span class="sxs-lookup"><span data-stu-id="edb6c-109">Data size</span></span>|
|--------------|-----------------|-----|
|<span data-ttu-id="edb6c-110">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="edb6c-110">H:\Video\\</span></span> |<span data-ttu-id="edb6c-111">Una raccolta di video</span><span class="sxs-lookup"><span data-stu-id="edb6c-111">A collection of videos</span></span>|<span data-ttu-id="edb6c-112">12 TB</span><span class="sxs-lookup"><span data-stu-id="edb6c-112">12 TB</span></span>|
|<span data-ttu-id="edb6c-113">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="edb6c-113">H:\Photo\\</span></span> |<span data-ttu-id="edb6c-114">Una raccolta di foto</span><span class="sxs-lookup"><span data-stu-id="edb6c-114">A collection of photos</span></span>|<span data-ttu-id="edb6c-115">30 GB</span><span class="sxs-lookup"><span data-stu-id="edb6c-115">30 GB</span></span>|
|<span data-ttu-id="edb6c-116">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="edb6c-116">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="edb6c-117">Un'immagine di disco Blu-ray™</span><span class="sxs-lookup"><span data-stu-id="edb6c-117">A Blu-Ray™ disk image</span></span>|<span data-ttu-id="edb6c-118">25 GB</span><span class="sxs-lookup"><span data-stu-id="edb6c-118">25 GB</span></span>|
|<span data-ttu-id="edb6c-119">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="edb6c-119">\\\bigshare\john\music\\</span></span>|<span data-ttu-id="edb6c-120">Una raccolta di file musicali in una condivisione di rete</span><span class="sxs-lookup"><span data-stu-id="edb6c-120">A collection of music files on a network share</span></span>|<span data-ttu-id="edb6c-121">10 GB</span><span class="sxs-lookup"><span data-stu-id="edb6c-121">10 GB</span></span>|

## <a name="storage-account-destinations"></a><span data-ttu-id="edb6c-122">Destinazioni degli account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="edb6c-122">Storage account destinations</span></span>

<span data-ttu-id="edb6c-123">il processo di importazione Hello verrà importati i dati di hello in seguito le destinazioni nell'account di archiviazione hello hello:</span><span class="sxs-lookup"><span data-stu-id="edb6c-123">hello import job will import hello data into hello following destinations in hello storage account:</span></span>

|<span data-ttu-id="edb6c-124">Sorgente</span><span class="sxs-lookup"><span data-stu-id="edb6c-124">Source</span></span>|<span data-ttu-id="edb6c-125">BLOB o directory virtuale di destinazione</span><span class="sxs-lookup"><span data-stu-id="edb6c-125">Destination virtual directory or blob</span></span>|
|------------|-------------------------------------------|
|<span data-ttu-id="edb6c-126">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="edb6c-126">H:\Video\\</span></span> |<span data-ttu-id="edb6c-127">video/</span><span class="sxs-lookup"><span data-stu-id="edb6c-127">video/</span></span>|
|<span data-ttu-id="edb6c-128">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="edb6c-128">H:\Photo\\</span></span> |<span data-ttu-id="edb6c-129">photo/</span><span class="sxs-lookup"><span data-stu-id="edb6c-129">photo/</span></span>|
|<span data-ttu-id="edb6c-130">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="edb6c-130">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="edb6c-131">favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="edb6c-131">favorite/FavoriteMovies.ISO</span></span>|
|<span data-ttu-id="edb6c-132">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="edb6c-132">\\\bigshare\john\music\\</span></span> |<span data-ttu-id="edb6c-133">music</span><span class="sxs-lookup"><span data-stu-id="edb6c-133">music</span></span>|

<span data-ttu-id="edb6c-134">Con questo mapping, hello file `H:\Video\Drama\GreatMovie.mov` sarà blob importati toohello `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span><span class="sxs-lookup"><span data-stu-id="edb6c-134">With this mapping, hello file `H:\Video\Drama\GreatMovie.mov` will be imported toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>

## <a name="determine-hard-drive-requirements"></a><span data-ttu-id="edb6c-135">Determinare i requisiti del disco rigido</span><span class="sxs-lookup"><span data-stu-id="edb6c-135">Determine hard drive requirements</span></span>

<span data-ttu-id="edb6c-136">Successivamente, toodetermine il numero di dischi rigido necessari, calcolo hello dimensioni dei dati hello:</span><span class="sxs-lookup"><span data-stu-id="edb6c-136">Next, toodetermine how many hard drives are needed, compute hello size of hello data:</span></span>

`12TB + 30GB + 25GB + 10GB = 12TB + 65GB`

<span data-ttu-id="edb6c-137">Per questo esempio, dovrebbero essere sufficienti due dischi rigidi da 8 TB.</span><span class="sxs-lookup"><span data-stu-id="edb6c-137">For this example, two 8TB hard drives should be sufficient.</span></span> <span data-ttu-id="edb6c-138">Tuttavia, poiché la directory di origine hello `H:\Video` include 12TB di dati e la capacità del disco rigido singolo è solo 8TB, si sarà in grado di toospecify in hello seguenti modalità di hello **driveset.csv** file:</span><span class="sxs-lookup"><span data-stu-id="edb6c-138">However, since hello source directory `H:\Video` has 12TB of data and your single hard drive's capacity is only 8TB, you will be able toospecify this in hello following way in hello **driveset.csv** file:</span></span>

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
X,Format,SilentMode,Encrypt,
Y,Format,SilentMode,Encrypt,
```
<span data-ttu-id="edb6c-139">strumento Hello distribuirà dati tra due dischi rigidi in modo ottimizzato.</span><span class="sxs-lookup"><span data-stu-id="edb6c-139">hello tool will distribute data across two hard drives in an optimized way.</span></span>

## <a name="attach-drives-and-configure-hello-job"></a><span data-ttu-id="edb6c-140">Collegare l'unità e configurare il processo di hello</span><span class="sxs-lookup"><span data-stu-id="edb6c-140">Attach drives and configure hello job</span></span>
<span data-ttu-id="edb6c-141">Verrà collegare entrambi macchina toohello dischi e volumi creati.</span><span class="sxs-lookup"><span data-stu-id="edb6c-141">You will attach both disks toohello machine and create volumes.</span></span> <span data-ttu-id="edb6c-142">Creare quindi il file **dataset.csv**:</span><span class="sxs-lookup"><span data-stu-id="edb6c-142">Then author **dataset.csv** file:</span></span>
```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

<span data-ttu-id="edb6c-143">Inoltre, è possibile impostare hello i metadati per tutti i file seguenti:</span><span class="sxs-lookup"><span data-stu-id="edb6c-143">In addition, you can set hello following metadata for all files:</span></span>

* <span data-ttu-id="edb6c-144">**UploadMethod:** servizio Importazione/Esportazione di Windows Azure</span><span class="sxs-lookup"><span data-stu-id="edb6c-144">**UploadMethod:** Windows Azure Import/Export service</span></span>
* <span data-ttu-id="edb6c-145">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="edb6c-145">**DataSetName:** SampleData</span></span>
* <span data-ttu-id="edb6c-146">**CreationDate:** 10/1/2013</span><span class="sxs-lookup"><span data-stu-id="edb6c-146">**CreationDate:** 10/1/2013</span></span>

<span data-ttu-id="edb6c-147">tooset metadati per i file hello importato, creare un file di testo, `c:\WAImportExport\SampleMetadata.txt`, con hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="edb6c-147">tooset metadata for hello imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with hello following content:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="edb6c-148">È inoltre possibile impostare alcune proprietà per hello `FavoriteMovie.ISO` blob:</span><span class="sxs-lookup"><span data-stu-id="edb6c-148">You can also set some properties for hello `FavoriteMovie.ISO` blob:</span></span>

* <span data-ttu-id="edb6c-149">**Content-Type:** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="edb6c-149">**Content-Type:** application/octet-stream</span></span>
* <span data-ttu-id="edb6c-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span><span class="sxs-lookup"><span data-stu-id="edb6c-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>
* <span data-ttu-id="edb6c-151">**Cache-Control:** no-cache</span><span class="sxs-lookup"><span data-stu-id="edb6c-151">**Cache-Control:** no-cache</span></span>

<span data-ttu-id="edb6c-152">tooset queste proprietà, creare un file di testo, `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="edb6c-152">tooset these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

## <a name="run-hello-azure-importexport-tool-waimportexportexe"></a><span data-ttu-id="edb6c-153">Hello esecuzione dello strumento di importazione/esportazione di Azure (WAImportExport.exe)</span><span class="sxs-lookup"><span data-stu-id="edb6c-153">Run hello Azure Import/Export Tool (WAImportExport.exe)</span></span>

<span data-ttu-id="edb6c-154">Si è ora pronto toorun hello strumento di importazione/esportazione di Azure tooprepare hello due unità disco rigido.</span><span class="sxs-lookup"><span data-stu-id="edb6c-154">Now you are ready toorun hello Azure Import/Export Tool tooprepare hello two hard drives.</span></span>

<span data-ttu-id="edb6c-155">**Per la prima sessione hello:**</span><span class="sxs-lookup"><span data-stu-id="edb6c-155">**For hello first session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

<span data-ttu-id="edb6c-156">Se tutti i dati più devono toobe aggiunto, creare un altro file di set di dati (stesso formato Initialdataset).</span><span class="sxs-lookup"><span data-stu-id="edb6c-156">If any more data needs toobe added, create another dataset file (same format as Initialdataset).</span></span>

<span data-ttu-id="edb6c-157">**Per una seconda sessione hello:**</span><span class="sxs-lookup"><span data-stu-id="edb6c-157">**For hello second session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

<span data-ttu-id="edb6c-158">Dopo aver completato le sessioni di copia hello, è possibile disconnettere hello due unità dal computer di hello copia e spedirle toohello data center Azure appropriato.</span><span class="sxs-lookup"><span data-stu-id="edb6c-158">Once hello copy sessions have completed, you can disconnect hello two drives from hello copy computer and ship them toohello appropriate Azure data center.</span></span> <span data-ttu-id="edb6c-159">Carica file journal hello due, `<FirstDriveSerialNumber>.xml` e `<SecondDriveSerialNumber>.xml`, quando si crea il processo di importazione hello in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="edb6c-159">You'll upload hello two journal files, `<FirstDriveSerialNumber>.xml` and `<SecondDriveSerialNumber>.xml`, when you create hello import job in hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="edb6c-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="edb6c-160">Next steps</span></span>

* <span data-ttu-id="edb6c-161">[Preparing hard drives for an import job](../storage-import-export-tool-preparing-hard-drives-import.md) (Preparazione dei dischi rigidi per un processo di importazione)</span><span class="sxs-lookup"><span data-stu-id="edb6c-161">[Preparing hard drives for an import job](../storage-import-export-tool-preparing-hard-drives-import.md)</span></span>
* <span data-ttu-id="edb6c-162">[Quick reference for frequently used commands](../storage-import-export-tool-quick-reference.md) (Riferimento rapido per i comandi usati più di frequente)</span><span class="sxs-lookup"><span data-stu-id="edb6c-162">[Quick reference for frequently used commands](../storage-import-export-tool-quick-reference.md)</span></span>
