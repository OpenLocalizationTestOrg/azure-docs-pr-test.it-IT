---
title: "aaaSetting proprietà e i metadati utilizzando Importazione/esportazione di Azure - v1 | Documenti Microsoft"
description: "Informazioni su come imposta toospecify toobe di proprietà e metadati per il BLOB di destinazione hello durante l'esecuzione di hello strumento di importazione/esportazione di Azure tooprepare le unità. Si riferisce toov1 di hello strumento di importazione/esportazione."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: e8541695-bcfb-4bf0-84d9-72c9de32a0a8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 66e55c2076fbcda9b78302f17b5ff2cf96bb24e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="setting-properties-and-metadata-during-hello-import-process"></a><span data-ttu-id="065be-104">Impostazione delle proprietà e metadati hello durante il processo di importazione</span><span class="sxs-lookup"><span data-stu-id="065be-104">Setting properties and metadata during hello import process</span></span>
<span data-ttu-id="065be-105">Quando si eseguono hello dello strumento di importazione/esportazione di Microsoft Azure tooprepare le unità, è possibile specificare le proprietà e metadati toobe impostato per il BLOB di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="065be-105">When you run hello Microsoft Azure Import/Export Tool tooprepare your drives, you can specify properties and metadata toobe set on hello destination blobs.</span></span> <span data-ttu-id="065be-106">A tale scopo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="065be-106">Follow these steps:</span></span>  
  
1.  <span data-ttu-id="065be-107">proprietà blob tooset, creare un file di testo nel computer locale che specifica i nomi delle proprietà e valori.</span><span class="sxs-lookup"><span data-stu-id="065be-107">tooset blob properties, create a text file on your local computer that specifies property names and values.</span></span>  
  
2.  <span data-ttu-id="065be-108">tooset i metadati del blob, creare un file di testo nel computer locale che specifica i nomi dei metadati e i valori.</span><span class="sxs-lookup"><span data-stu-id="065be-108">tooset blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>  
  
3.  <span data-ttu-id="065be-109">Passare tooone percorso completo di hello o entrambi questi toohello file dello strumento di importazione/esportazione di Azure come parte di hello `PrepImport` operazione.</span><span class="sxs-lookup"><span data-stu-id="065be-109">Pass hello full path tooone or both of these files toohello Azure Import/Export Tool as part of hello `PrepImport` operation.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="065be-110">Quando si specifica un file di proprietà o di metadati durante una sessione di copia, tali proprietà o metadati vengono impostati per ogni BLOB importato durante tale sessione di copia.</span><span class="sxs-lookup"><span data-stu-id="065be-110">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="065be-111">Se si desidera toospecify un diverso set di proprietà o metadati per alcuni BLOB hello importati, è necessario toocreate separato copiare sessione con proprietà diverse o file di metadati.</span><span class="sxs-lookup"><span data-stu-id="065be-111">If you want toospecify a different set of properties or metadata for some of hello blobs being imported, you'll need toocreate a separate copy session with different properties or metadata files.</span></span>  
  
## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="065be-112">Specificare le proprietà dei BLOB in un file di testo</span><span class="sxs-lookup"><span data-stu-id="065be-112">Specify Blob Properties in a Text File</span></span>  
<span data-ttu-id="065be-113">proprietà blob toospecify, creare un file di testo locale e includere il XML che specifica i nomi delle proprietà come elementi e i valori delle proprietà come valori.</span><span class="sxs-lookup"><span data-stu-id="065be-113">toospecify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="065be-114">Ecco un esempio che specifica alcuni valori delle proprietà:</span><span class="sxs-lookup"><span data-stu-id="065be-114">Here's an example that specifies some property values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="065be-115">Salvare hello tooa locale percorso del file come `C:\WAImportExport\ImportProperties.txt`.</span><span class="sxs-lookup"><span data-stu-id="065be-115">Save hello file tooa local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>  
  
## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="065be-116">Specificare i metadati dei BLOB in un file di testo</span><span class="sxs-lookup"><span data-stu-id="065be-116">Specify Blob Metadata in a Text File</span></span>  
<span data-ttu-id="065be-117">Analogamente, toospecify i metadati del blob, creare un file di testo locale che specifica i nomi dei metadati come elementi e i valori dei metadati come valori.</span><span class="sxs-lookup"><span data-stu-id="065be-117">Similarly, toospecify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="065be-118">Ecco un esempio che specifica alcuni valori dei metadati:</span><span class="sxs-lookup"><span data-stu-id="065be-118">Here's an example that specifies some metadata values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="065be-119">Salvare hello tooa locale percorso del file come `C:\WAImportExport\ImportMetadata.txt`.</span><span class="sxs-lookup"><span data-stu-id="065be-119">Save hello file tooa local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>  
  
## <a name="create-a-copy-session-including-hello-properties-or-metadata-files"></a><span data-ttu-id="065be-120">Creare un hello sessione di copia tra le proprietà o i file di metadati</span><span class="sxs-lookup"><span data-stu-id="065be-120">Create a Copy Session Including hello Properties or Metadata Files</span></span>  
<span data-ttu-id="065be-121">Quando si esegue processo di importazione hello tooprepare hello strumento di importazione/esportazione di Azure, specificare il file delle proprietà hello nella riga di comando hello utilizzando hello `PropertyFile` parametro.</span><span class="sxs-lookup"><span data-stu-id="065be-121">When you run hello Azure Import/Export Tool tooprepare hello import job, specify hello properties file on hello command line using hello `PropertyFile` parameter.</span></span> <span data-ttu-id="065be-122">Specificare il file di metadati hello nella riga di comando hello utilizzando hello `/MetadataFile` parametro.</span><span class="sxs-lookup"><span data-stu-id="065be-122">Specify hello metadata file on hello command line using hello `/MetadataFile` parameter.</span></span> <span data-ttu-id="065be-123">Ecco un esempio che consente di specificare entrambi i file:</span><span class="sxs-lookup"><span data-stu-id="065be-123">Here's an example that specifies both files:</span></span>  
  
```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```
  
## <a name="next-steps"></a><span data-ttu-id="065be-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="065be-124">Next steps</span></span>

* <span data-ttu-id="065be-125">[Import/Export service metadata and properties file format](storage-import-export-file-format-metadata-and-properties.md) (Formato dei file di metadati e delle proprietà del servizio Importazione/Esportazione)</span><span class="sxs-lookup"><span data-stu-id="065be-125">[Import/Export service metadata and properties file format](storage-import-export-file-format-metadata-and-properties.md)</span></span>
