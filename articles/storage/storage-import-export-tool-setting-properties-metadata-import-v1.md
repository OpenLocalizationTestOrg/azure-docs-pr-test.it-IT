---
title: "Impostazione delle proprietà e dei metadati usando Importazione/Esportazione di Azure - versione 1 | Documentazione Microsoft"
description: "Informazioni su come specificare le proprietà e i metadati da impostare nei BLOB di destinazione quando si esegue lo strumento Importazione/Esportazione di Azure per preparare le unità. Si riferisce alla versione 1 dello strumento Importazione/Esportazione."
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
ms.openlocfilehash: 6455ce57572f9ec36d0ebae88c1ddd9f40f237bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="setting-properties-and-metadata-during-the-import-process"></a><span data-ttu-id="7c885-104">Impostazione di proprietà e metadati durante il processo di importazione</span><span class="sxs-lookup"><span data-stu-id="7c885-104">Setting properties and metadata during the import process</span></span>
<span data-ttu-id="7c885-105">Quando si esegue lo strumento Importazione/Esportazione di Microsoft Azure per preparare le unità, è possibile specificare le proprietà e i metadati da impostare nei BLOB di destinazione.</span><span class="sxs-lookup"><span data-stu-id="7c885-105">When you run the Microsoft Azure Import/Export Tool to prepare your drives, you can specify properties and metadata to be set on the destination blobs.</span></span> <span data-ttu-id="7c885-106">A tale scopo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="7c885-106">Follow these steps:</span></span>  
  
1.  <span data-ttu-id="7c885-107">Per impostare le proprietà dei BLOB, creare nel computer locale un file di testo che specifichi i nomi e i valori delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="7c885-107">To set blob properties, create a text file on your local computer that specifies property names and values.</span></span>  
  
2.  <span data-ttu-id="7c885-108">Per impostare i metadati dei BLOB, creare nel computer locale un file di testo che specifichi i nomi e i valori dei metadati.</span><span class="sxs-lookup"><span data-stu-id="7c885-108">To set blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>  
  
3.  <span data-ttu-id="7c885-109">Passare il percorso completo di uno di questi file o di entrambi allo strumento Importazione/Esportazione di Azure durante l'operazione `PrepImport`.</span><span class="sxs-lookup"><span data-stu-id="7c885-109">Pass the full path to one or both of these files to the Azure Import/Export Tool as part of the `PrepImport` operation.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="7c885-110">Quando si specifica un file di proprietà o di metadati durante una sessione di copia, tali proprietà o metadati vengono impostati per ogni BLOB importato durante tale sessione di copia.</span><span class="sxs-lookup"><span data-stu-id="7c885-110">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="7c885-111">Per specificare un set diverso di proprietà o metadati per alcuni dei BLOB da importare, sarà necessario creare una sessione di copia separata con file di proprietà o metadati diversi.</span><span class="sxs-lookup"><span data-stu-id="7c885-111">If you want to specify a different set of properties or metadata for some of the blobs being imported, you'll need to create a separate copy session with different properties or metadata files.</span></span>  
  
## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="7c885-112">Specificare le proprietà dei BLOB in un file di testo</span><span class="sxs-lookup"><span data-stu-id="7c885-112">Specify Blob Properties in a Text File</span></span>  
<span data-ttu-id="7c885-113">Per specificare le proprietà dei BLOB, creare un file di testo locale e includere un codice XML che specifichi i nomi delle proprietà come elementi e i valori delle proprietà come valori.</span><span class="sxs-lookup"><span data-stu-id="7c885-113">To specify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="7c885-114">Ecco un esempio che specifica alcuni valori delle proprietà:</span><span class="sxs-lookup"><span data-stu-id="7c885-114">Here's an example that specifies some property values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="7c885-115">Salvare il file in un percorso locale, ad esempio `C:\WAImportExport\ImportProperties.txt`.</span><span class="sxs-lookup"><span data-stu-id="7c885-115">Save the file to a local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>  
  
## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="7c885-116">Specificare i metadati dei BLOB in un file di testo</span><span class="sxs-lookup"><span data-stu-id="7c885-116">Specify Blob Metadata in a Text File</span></span>  
<span data-ttu-id="7c885-117">Allo stesso modo, per specificare i metadati dei BLOB, creare un file di testo locale che specifichi i nomi dei metadati come elementi e i valori dei metadati come valori.</span><span class="sxs-lookup"><span data-stu-id="7c885-117">Similarly, to specify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="7c885-118">Ecco un esempio che specifica alcuni valori dei metadati:</span><span class="sxs-lookup"><span data-stu-id="7c885-118">Here's an example that specifies some metadata values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="7c885-119">Salvare il file in un percorso locale, ad esempio `C:\WAImportExport\ImportMetadata.txt`.</span><span class="sxs-lookup"><span data-stu-id="7c885-119">Save the file to a local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>  
  
## <a name="create-a-copy-session-including-the-properties-or-metadata-files"></a><span data-ttu-id="7c885-120">Creare una sessione di copia che includa i file delle proprietà o dei metadati</span><span class="sxs-lookup"><span data-stu-id="7c885-120">Create a Copy Session Including the Properties or Metadata Files</span></span>  
<span data-ttu-id="7c885-121">Quando si esegue lo strumento Importazione/Esportazione di Azure per preparare il processo di importazione, specificare il file delle proprietà nella riga di comando tramite il parametro `PropertyFile`.</span><span class="sxs-lookup"><span data-stu-id="7c885-121">When you run the Azure Import/Export Tool to prepare the import job, specify the properties file on the command line using the `PropertyFile` parameter.</span></span> <span data-ttu-id="7c885-122">Specificare il file dei metadati nella riga di comando tramite il parametro `/MetadataFile`.</span><span class="sxs-lookup"><span data-stu-id="7c885-122">Specify the metadata file on the command line using the `/MetadataFile` parameter.</span></span> <span data-ttu-id="7c885-123">Ecco un esempio che consente di specificare entrambi i file:</span><span class="sxs-lookup"><span data-stu-id="7c885-123">Here's an example that specifies both files:</span></span>  
  
```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```
  
## <a name="next-steps"></a><span data-ttu-id="7c885-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7c885-124">Next steps</span></span>

* <span data-ttu-id="7c885-125">[Import/Export service metadata and properties file format](storage-import-export-file-format-metadata-and-properties.md) (Formato dei file di metadati e delle proprietà del servizio Importazione/Esportazione)</span><span class="sxs-lookup"><span data-stu-id="7c885-125">[Import/Export service metadata and properties file format](storage-import-export-file-format-metadata-and-properties.md)</span></span>
