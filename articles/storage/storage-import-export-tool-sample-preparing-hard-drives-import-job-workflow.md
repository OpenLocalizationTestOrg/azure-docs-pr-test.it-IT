---
title: Flusso di lavoro di esempio per la preparazione dei dischi rigidi per un processo di importazione in Importazione/Esportazione di Azure | Documentazione Microsoft
description: "Viene illustrata una procedura dettagliata e completa per la preparazione delle unità per un processo di importazione nel servizio Importazione/Esportazione di Azure."
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
ms.openlocfilehash: 78d7ce3bbd3205fd995ba331af08d830097c8156
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="sample-workflow-to-prepare-hard-drives-for-an-import-job"></a><span data-ttu-id="9528e-103">Flusso di lavoro campione per preparare i dischi rigidi per un processo di importazione</span><span class="sxs-lookup"><span data-stu-id="9528e-103">Sample workflow to prepare hard drives for an import job</span></span>

<span data-ttu-id="9528e-104">In questo articolo viene illustrato il processo completo di preparazione delle unità per un processo di importazione.</span><span class="sxs-lookup"><span data-stu-id="9528e-104">This article walks you through the complete process of preparing drives for an import job.</span></span>

## <a name="sample-data"></a><span data-ttu-id="9528e-105">Dati di esempio</span><span class="sxs-lookup"><span data-stu-id="9528e-105">Sample data</span></span>

<span data-ttu-id="9528e-106">In questo esempio verranno importati i seguenti dati di un account di archiviazione Azure denominato `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="9528e-106">This example imports the following data into an Azure storage account named `mystorageaccount`:</span></span>

|<span data-ttu-id="9528e-107">Percorso</span><span class="sxs-lookup"><span data-stu-id="9528e-107">Location</span></span>|<span data-ttu-id="9528e-108">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9528e-108">Description</span></span>|<span data-ttu-id="9528e-109">Dimensioni dei dati</span><span class="sxs-lookup"><span data-stu-id="9528e-109">Data size</span></span>|
|--------------|-----------------|-----|
|<span data-ttu-id="9528e-110">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="9528e-110">H:\Video\\</span></span> |<span data-ttu-id="9528e-111">Una raccolta di video</span><span class="sxs-lookup"><span data-stu-id="9528e-111">A collection of videos</span></span>|<span data-ttu-id="9528e-112">12 TB</span><span class="sxs-lookup"><span data-stu-id="9528e-112">12 TB</span></span>|
|<span data-ttu-id="9528e-113">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="9528e-113">H:\Photo\\</span></span> |<span data-ttu-id="9528e-114">Una raccolta di foto</span><span class="sxs-lookup"><span data-stu-id="9528e-114">A collection of photos</span></span>|<span data-ttu-id="9528e-115">30 GB</span><span class="sxs-lookup"><span data-stu-id="9528e-115">30 GB</span></span>|
|<span data-ttu-id="9528e-116">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="9528e-116">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="9528e-117">Un'immagine di disco Blu-ray™</span><span class="sxs-lookup"><span data-stu-id="9528e-117">A Blu-Ray™ disk image</span></span>|<span data-ttu-id="9528e-118">25 GB</span><span class="sxs-lookup"><span data-stu-id="9528e-118">25 GB</span></span>|
|<span data-ttu-id="9528e-119">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="9528e-119">\\\bigshare\john\music\\</span></span>|<span data-ttu-id="9528e-120">Una raccolta di file musicali in una condivisione di rete</span><span class="sxs-lookup"><span data-stu-id="9528e-120">A collection of music files on a network share</span></span>|<span data-ttu-id="9528e-121">10 GB</span><span class="sxs-lookup"><span data-stu-id="9528e-121">10 GB</span></span>|

## <a name="storage-account-destinations"></a><span data-ttu-id="9528e-122">Destinazioni degli account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="9528e-122">Storage account destinations</span></span>

<span data-ttu-id="9528e-123">Il processo importerà i dati nelle seguenti destinazioni nell'account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="9528e-123">The import job will import the data into the following destinations in the storage account:</span></span>

|<span data-ttu-id="9528e-124">Sorgente</span><span class="sxs-lookup"><span data-stu-id="9528e-124">Source</span></span>|<span data-ttu-id="9528e-125">BLOB o directory virtuale di destinazione</span><span class="sxs-lookup"><span data-stu-id="9528e-125">Destination virtual directory or blob</span></span>|
|------------|-------------------------------------------|
|<span data-ttu-id="9528e-126">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="9528e-126">H:\Video\\</span></span> |<span data-ttu-id="9528e-127">video/</span><span class="sxs-lookup"><span data-stu-id="9528e-127">video/</span></span>|
|<span data-ttu-id="9528e-128">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="9528e-128">H:\Photo\\</span></span> |<span data-ttu-id="9528e-129">photo/</span><span class="sxs-lookup"><span data-stu-id="9528e-129">photo/</span></span>|
|<span data-ttu-id="9528e-130">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="9528e-130">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="9528e-131">favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="9528e-131">favorite/FavoriteMovies.ISO</span></span>|
|<span data-ttu-id="9528e-132">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="9528e-132">\\\bigshare\john\music\\</span></span> |<span data-ttu-id="9528e-133">music</span><span class="sxs-lookup"><span data-stu-id="9528e-133">music</span></span>|

<span data-ttu-id="9528e-134">Con questo mapping, il file `H:\Video\Drama\GreatMovie.mov` verrà importato nel BLOB `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span><span class="sxs-lookup"><span data-stu-id="9528e-134">With this mapping, the file `H:\Video\Drama\GreatMovie.mov` will be imported to the blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>

## <a name="determine-hard-drive-requirements"></a><span data-ttu-id="9528e-135">Determinare i requisiti del disco rigido</span><span class="sxs-lookup"><span data-stu-id="9528e-135">Determine hard drive requirements</span></span>

<span data-ttu-id="9528e-136">Successivamente, per determinare il numero di dischi rigidi necessari, calcolare la dimensione dei dati:</span><span class="sxs-lookup"><span data-stu-id="9528e-136">Next, to determine how many hard drives are needed, compute the size of the data:</span></span>

`12TB + 30GB + 25GB + 10GB = 12TB + 65GB`

<span data-ttu-id="9528e-137">Per questo esempio, dovrebbero essere sufficienti due dischi rigidi da 8 TB.</span><span class="sxs-lookup"><span data-stu-id="9528e-137">For this example, two 8TB hard drives should be sufficient.</span></span> <span data-ttu-id="9528e-138">Poiché tuttavia la directory di origine `H:\Video` contiene 12 TB di dati e la capacità del singolo disco rigido è di soli 8 TB, sarà possibile specificarlo nel modo seguente nel file **driveset.csv**:</span><span class="sxs-lookup"><span data-stu-id="9528e-138">However, since the source directory `H:\Video` has 12TB of data and your single hard drive's capacity is only 8TB, you will be able to specify this in the following way in the **driveset.csv** file:</span></span>

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
X,Format,SilentMode,Encrypt,
Y,Format,SilentMode,Encrypt,
```
<span data-ttu-id="9528e-139">Lo strumento distribuirà dati nei due dischi rigidi in modo ottimizzato.</span><span class="sxs-lookup"><span data-stu-id="9528e-139">The tool will distribute data across two hard drives in an optimized way.</span></span>

## <a name="attach-drives-and-configure-the-job"></a><span data-ttu-id="9528e-140">Collegare le unità e configurare il processo</span><span class="sxs-lookup"><span data-stu-id="9528e-140">Attach drives and configure the job</span></span>
<span data-ttu-id="9528e-141">Si collegheranno entrambi i dischi alla macchina e si creeranno i volumi.</span><span class="sxs-lookup"><span data-stu-id="9528e-141">You will attach both disks to the machine and create volumes.</span></span> <span data-ttu-id="9528e-142">Creare quindi il file **dataset.csv**:</span><span class="sxs-lookup"><span data-stu-id="9528e-142">Then author **dataset.csv** file:</span></span>
```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

<span data-ttu-id="9528e-143">Inoltre, è possibile impostare i metadati seguenti per tutti i file:</span><span class="sxs-lookup"><span data-stu-id="9528e-143">In addition, you can set the following metadata for all files:</span></span>

* <span data-ttu-id="9528e-144">**UploadMethod:** servizio Importazione/Esportazione di Windows Azure</span><span class="sxs-lookup"><span data-stu-id="9528e-144">**UploadMethod:** Windows Azure Import/Export service</span></span>
* <span data-ttu-id="9528e-145">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="9528e-145">**DataSetName:** SampleData</span></span>
* <span data-ttu-id="9528e-146">**CreationDate:** 10/1/2013</span><span class="sxs-lookup"><span data-stu-id="9528e-146">**CreationDate:** 10/1/2013</span></span>

<span data-ttu-id="9528e-147">Per impostare i metadati per i file importati, creare un file di testo, `c:\WAImportExport\SampleMetadata.txt`, con il contenuto seguente:</span><span class="sxs-lookup"><span data-stu-id="9528e-147">To set metadata for the imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with the following content:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="9528e-148">È inoltre possibile impostare alcune proprietà per il BLOB `FavoriteMovie.ISO`:</span><span class="sxs-lookup"><span data-stu-id="9528e-148">You can also set some properties for the `FavoriteMovie.ISO` blob:</span></span>

* <span data-ttu-id="9528e-149">**Content-Type:** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="9528e-149">**Content-Type:** application/octet-stream</span></span>
* <span data-ttu-id="9528e-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span><span class="sxs-lookup"><span data-stu-id="9528e-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>
* <span data-ttu-id="9528e-151">**Cache-Control:** no-cache</span><span class="sxs-lookup"><span data-stu-id="9528e-151">**Cache-Control:** no-cache</span></span>

<span data-ttu-id="9528e-152">Per impostare queste proprietà, creare un file di testo, `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="9528e-152">To set these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

## <a name="run-the-azure-importexport-tool-waimportexportexe"></a><span data-ttu-id="9528e-153">Eseguire lo strumento di Importazione/Esportazione di Azure (WAImportExport.exe)</span><span class="sxs-lookup"><span data-stu-id="9528e-153">Run the Azure Import/Export Tool (WAImportExport.exe)</span></span>

<span data-ttu-id="9528e-154">A questo punto è possibile eseguire lo strumento di Importazione/Esportazione di Azure per preparare i due dischi rigidi.</span><span class="sxs-lookup"><span data-stu-id="9528e-154">Now you are ready to run the Azure Import/Export Tool to prepare the two hard drives.</span></span>

<span data-ttu-id="9528e-155">**Per la prima sessione:**</span><span class="sxs-lookup"><span data-stu-id="9528e-155">**For the first session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

<span data-ttu-id="9528e-156">Se è necessario aggiungere altri dati, creare un altro file di set di dati (stesso formato di Initialdataset).</span><span class="sxs-lookup"><span data-stu-id="9528e-156">If any more data needs to be added, create another dataset file (same format as Initialdataset).</span></span>

<span data-ttu-id="9528e-157">**Per la seconda sessione:**</span><span class="sxs-lookup"><span data-stu-id="9528e-157">**For the second session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

<span data-ttu-id="9528e-158">Dopo aver completato le sessioni di copia, è possibile disconnettere le due unità dal computer di copia e spedirle al data center di Azure appropriato.</span><span class="sxs-lookup"><span data-stu-id="9528e-158">Once the copy sessions have completed, you can disconnect the two drives from the copy computer and ship them to the appropriate Azure data center.</span></span> <span data-ttu-id="9528e-159">I due file journal, `<FirstDriveSerialNumber>.xml` e `<SecondDriveSerialNumber>.xml`, dovranno essere caricati durante la creazione del processo di importazione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9528e-159">You'll upload the two journal files, `<FirstDriveSerialNumber>.xml` and `<SecondDriveSerialNumber>.xml`, when you create the import job in the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9528e-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9528e-160">Next steps</span></span>

* <span data-ttu-id="9528e-161">[Preparing hard drives for an import job](storage-import-export-tool-preparing-hard-drives-import.md) (Preparazione dei dischi rigidi per un processo di importazione)</span><span class="sxs-lookup"><span data-stu-id="9528e-161">[Preparing hard drives for an import job](storage-import-export-tool-preparing-hard-drives-import.md)</span></span>
* <span data-ttu-id="9528e-162">[Quick reference for frequently used commands](storage-import-export-tool-quick-reference.md) (Riferimento rapido per i comandi usati più di frequente)</span><span class="sxs-lookup"><span data-stu-id="9528e-162">[Quick reference for frequently used commands](storage-import-export-tool-quick-reference.md)</span></span>
