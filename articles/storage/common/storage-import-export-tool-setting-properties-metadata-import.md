---
title: "aaaSetting proprietà e i metadati utilizzando Importazione/esportazione di Azure | Documenti Microsoft"
description: "Informazioni su come imposta toospecify toobe di proprietà e metadati per il BLOB di destinazione hello durante l'esecuzione di hello strumento di importazione/esportazione di Azure tooprepare le unità."
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
ms.openlocfilehash: c763237160f0e4b72ce88fd31e2958994bfe8e50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="setting-properties-and-metadata-during-hello-import-process"></a><span data-ttu-id="1abc5-103">Impostazione delle proprietà e metadati hello durante il processo di importazione</span><span class="sxs-lookup"><span data-stu-id="1abc5-103">Setting properties and metadata during hello import process</span></span>

<span data-ttu-id="1abc5-104">Quando si eseguono hello dello strumento di importazione/esportazione di Microsoft Azure tooprepare le unità, è possibile specificare le proprietà e metadati toobe impostato per il BLOB di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="1abc5-104">When you run hello Microsoft Azure Import/Export Tool tooprepare your drives, you can specify properties and metadata toobe set on hello destination blobs.</span></span> <span data-ttu-id="1abc5-105">A tale scopo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1abc5-105">Follow these steps:</span></span>

1.  <span data-ttu-id="1abc5-106">proprietà blob tooset, creare un file di testo nel computer locale che specifica i nomi delle proprietà e valori.</span><span class="sxs-lookup"><span data-stu-id="1abc5-106">tooset blob properties, create a text file on your local computer that specifies property names and values.</span></span>
2.  <span data-ttu-id="1abc5-107">tooset i metadati del blob, creare un file di testo nel computer locale che specifica i nomi dei metadati e i valori.</span><span class="sxs-lookup"><span data-stu-id="1abc5-107">tooset blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>
3.  <span data-ttu-id="1abc5-108">Passare tooone percorso completo di hello o entrambi questi toohello file dello strumento di importazione/esportazione di Azure come parte di hello `PrepImport` operazione.</span><span class="sxs-lookup"><span data-stu-id="1abc5-108">Pass hello full path tooone or both of these files toohello Azure Import/Export Tool as part of hello `PrepImport` operation.</span></span>

> [!NOTE]
>  <span data-ttu-id="1abc5-109">Quando si specifica un file di proprietà o di metadati durante una sessione di copia, tali proprietà o metadati vengono impostati per ogni BLOB importato durante tale sessione di copia.</span><span class="sxs-lookup"><span data-stu-id="1abc5-109">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="1abc5-110">Se si desidera toospecify un diverso set di proprietà o metadati per alcuni BLOB hello importati, è necessario toocreate separato copiare sessione con proprietà diverse o file di metadati.</span><span class="sxs-lookup"><span data-stu-id="1abc5-110">If you want toospecify a different set of properties or metadata for some of hello blobs being imported, you'll need toocreate a separate copy session with different properties or metadata files.</span></span>

## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="1abc5-111">Specificare le proprietà dei BLOB in un file di testo</span><span class="sxs-lookup"><span data-stu-id="1abc5-111">Specify blob properties in a text file</span></span>

<span data-ttu-id="1abc5-112">proprietà blob toospecify, creare un file di testo locale e includere il XML che specifica i nomi delle proprietà come elementi e i valori delle proprietà come valori.</span><span class="sxs-lookup"><span data-stu-id="1abc5-112">toospecify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="1abc5-113">Ecco un esempio che specifica alcuni valori delle proprietà:</span><span class="sxs-lookup"><span data-stu-id="1abc5-113">Here's an example that specifies some property values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

<span data-ttu-id="1abc5-114">Salvare hello tooa locale percorso del file come `C:\WAImportExport\ImportProperties.txt`.</span><span class="sxs-lookup"><span data-stu-id="1abc5-114">Save hello file tooa local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>

## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="1abc5-115">Specificare i metadati dei BLOB in un file di testo</span><span class="sxs-lookup"><span data-stu-id="1abc5-115">Specify blob metadata in a text file</span></span>

<span data-ttu-id="1abc5-116">Analogamente, toospecify i metadati del blob, creare un file di testo locale che specifica i nomi dei metadati come elementi e i valori dei metadati come valori.</span><span class="sxs-lookup"><span data-stu-id="1abc5-116">Similarly, toospecify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="1abc5-117">Ecco un esempio che specifica alcuni valori dei metadati:</span><span class="sxs-lookup"><span data-stu-id="1abc5-117">Here's an example that specifies some metadata values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="1abc5-118">Salvare hello tooa locale percorso del file come `C:\WAImportExport\ImportMetadata.txt`.</span><span class="sxs-lookup"><span data-stu-id="1abc5-118">Save hello file tooa local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>

## <a name="add-hello-path-tooproperties-and-metadata-files-in-datasetcsv"></a><span data-ttu-id="1abc5-119">Aggiungere i file di metadati e tooproperties percorso hello in dataset.csv</span><span class="sxs-lookup"><span data-stu-id="1abc5-119">Add hello path tooproperties and metadata files in dataset.csv</span></span>

```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,https://mystorageaccount.blob.core.windows.net/video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,https://mystorageaccount.blob.core.windows.net/photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,https://mystorageaccount.blob.core.windows.net/music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

## <a name="next-steps"></a><span data-ttu-id="1abc5-120">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1abc5-120">Next steps</span></span>

* <span data-ttu-id="1abc5-121">[Import/Export service metadata and properties file format](../storage-import-export-file-format-metadata-and-properties.md) (Formato dei file di metadati e delle proprietà del servizio Importazione/Esportazione)</span><span class="sxs-lookup"><span data-stu-id="1abc5-121">[Import/Export service metadata and properties file format](../storage-import-export-file-format-metadata-and-properties.md)</span></span>
