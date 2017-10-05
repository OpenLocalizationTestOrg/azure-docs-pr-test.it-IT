---
title: "Impostazione delle proprietà e dei metadati usando Importazione/Esportazione di Azure | Documentazione Microsoft"
description: "Informazioni su come specificare le proprietà e i metadati da impostare nei BLOB di destinazione quando si esegue lo strumento Importazione/Esportazione di Azure per preparare le unità."
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
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: bdc7a53f82d1fbbb726e2b1bd5d96678a8563566
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="setting-properties-and-metadata-during-the-import-process"></a><span data-ttu-id="c6e04-103">Impostazione di proprietà e metadati durante il processo di importazione</span><span class="sxs-lookup"><span data-stu-id="c6e04-103">Setting properties and metadata during the import process</span></span>

<span data-ttu-id="c6e04-104">Quando si esegue lo strumento Importazione/Esportazione di Microsoft Azure per preparare le unità, è possibile specificare le proprietà e i metadati da impostare nei BLOB di destinazione.</span><span class="sxs-lookup"><span data-stu-id="c6e04-104">When you run the Microsoft Azure Import/Export Tool to prepare your drives, you can specify properties and metadata to be set on the destination blobs.</span></span> <span data-ttu-id="c6e04-105">A tale scopo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c6e04-105">Follow these steps:</span></span>

1.  <span data-ttu-id="c6e04-106">Per impostare le proprietà dei BLOB, creare nel computer locale un file di testo che specifichi i nomi e i valori delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="c6e04-106">To set blob properties, create a text file on your local computer that specifies property names and values.</span></span>
2.  <span data-ttu-id="c6e04-107">Per impostare i metadati dei BLOB, creare nel computer locale un file di testo che specifichi i nomi e i valori dei metadati.</span><span class="sxs-lookup"><span data-stu-id="c6e04-107">To set blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>
3.  <span data-ttu-id="c6e04-108">Passare il percorso completo di uno di questi file o di entrambi allo strumento Importazione/Esportazione di Azure durante l'operazione `PrepImport`.</span><span class="sxs-lookup"><span data-stu-id="c6e04-108">Pass the full path to one or both of these files to the Azure Import/Export Tool as part of the `PrepImport` operation.</span></span>

> [!NOTE]
>  <span data-ttu-id="c6e04-109">Quando si specifica un file di proprietà o di metadati durante una sessione di copia, tali proprietà o metadati vengono impostati per ogni BLOB importato durante tale sessione di copia.</span><span class="sxs-lookup"><span data-stu-id="c6e04-109">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="c6e04-110">Per specificare un set diverso di proprietà o metadati per alcuni dei BLOB da importare, sarà necessario creare una sessione di copia separata con file di proprietà o metadati diversi.</span><span class="sxs-lookup"><span data-stu-id="c6e04-110">If you want to specify a different set of properties or metadata for some of the blobs being imported, you'll need to create a separate copy session with different properties or metadata files.</span></span>

## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="c6e04-111">Specificare le proprietà dei BLOB in un file di testo</span><span class="sxs-lookup"><span data-stu-id="c6e04-111">Specify blob properties in a text file</span></span>

<span data-ttu-id="c6e04-112">Per specificare le proprietà dei BLOB, creare un file di testo locale e includere un codice XML che specifichi i nomi delle proprietà come elementi e i valori delle proprietà come valori.</span><span class="sxs-lookup"><span data-stu-id="c6e04-112">To specify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="c6e04-113">Ecco un esempio che specifica alcuni valori delle proprietà:</span><span class="sxs-lookup"><span data-stu-id="c6e04-113">Here's an example that specifies some property values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

<span data-ttu-id="c6e04-114">Salvare il file in un percorso locale, ad esempio `C:\WAImportExport\ImportProperties.txt`.</span><span class="sxs-lookup"><span data-stu-id="c6e04-114">Save the file to a local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>

## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="c6e04-115">Specificare i metadati dei BLOB in un file di testo</span><span class="sxs-lookup"><span data-stu-id="c6e04-115">Specify blob metadata in a text file</span></span>

<span data-ttu-id="c6e04-116">Allo stesso modo, per specificare i metadati dei BLOB, creare un file di testo locale che specifichi i nomi dei metadati come elementi e i valori dei metadati come valori.</span><span class="sxs-lookup"><span data-stu-id="c6e04-116">Similarly, to specify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="c6e04-117">Ecco un esempio che specifica alcuni valori dei metadati:</span><span class="sxs-lookup"><span data-stu-id="c6e04-117">Here's an example that specifies some metadata values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="c6e04-118">Salvare il file in un percorso locale, ad esempio `C:\WAImportExport\ImportMetadata.txt`.</span><span class="sxs-lookup"><span data-stu-id="c6e04-118">Save the file to a local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>

## <a name="add-the-path-to-properties-and-metadata-files-in-datasetcsv"></a><span data-ttu-id="c6e04-119">Aggiungere il percorso dei file di proprietà e di metadati in dataset.csv</span><span class="sxs-lookup"><span data-stu-id="c6e04-119">Add the path to properties and metadata files in dataset.csv</span></span>

```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,https://mystorageaccount.blob.core.windows.net/video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,https://mystorageaccount.blob.core.windows.net/photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,https://mystorageaccount.blob.core.windows.net/music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

## <a name="next-steps"></a><span data-ttu-id="c6e04-120">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c6e04-120">Next steps</span></span>

* <span data-ttu-id="c6e04-121">[Import/Export service metadata and properties file format](storage-import-export-file-format-metadata-and-properties.md) (Formato dei file di metadati e delle proprietà del servizio Importazione/Esportazione)</span><span class="sxs-lookup"><span data-stu-id="c6e04-121">[Import/Export service metadata and properties file format](storage-import-export-file-format-metadata-and-properties.md)</span></span>
