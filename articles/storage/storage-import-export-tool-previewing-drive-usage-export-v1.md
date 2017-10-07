---
title: "utilizzo dell'unità di aaaPreviewing per un processo di esportazione di importazione/esportazione di Azure - v1 | Documenti Microsoft"
description: "Informazioni su come elenco hello toopreview di BLOB è stato selezionato per un processo di esportazione nel servizio di importazione/esportazione di Azure hello."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 7707d744-7ec7-4de8-ac9b-93a18608dc9a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 88495f921371458c0451da6878fd7cc9a45d20cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="previewing-drive-usage-for-an-export-job"></a><span data-ttu-id="25d96-103">Anteprima dell'uso del disco per un processo di esportazione</span><span class="sxs-lookup"><span data-stu-id="25d96-103">Previewing drive usage for an export job</span></span>
<span data-ttu-id="25d96-104">Prima di creare un processo di esportazione, è necessario esportata un set di BLOB toobe toochoose.</span><span class="sxs-lookup"><span data-stu-id="25d96-104">Before you create an export job, you need toochoose a set of blobs toobe exported.</span></span> <span data-ttu-id="25d96-105">servizio di importazione/esportazione di Microsoft Azure Hello consente toouse un elenco di percorsi blob o blob prefissi BLOB hello toorepresent selezionata.</span><span class="sxs-lookup"><span data-stu-id="25d96-105">hello Microsoft Azure Import/Export service allows you toouse a list of blob paths or blob prefixes toorepresent hello blobs you've selected.</span></span>  
  
<span data-ttu-id="25d96-106">Successivamente, è necessario toodetermine il numero di unità è necessario toosend.</span><span class="sxs-lookup"><span data-stu-id="25d96-106">Next, you need toodetermine how many drives you need toosend.</span></span> <span data-ttu-id="25d96-107">Strumento di importazione/esportazione Hello fornisce hello `PreviewExport` sintassi del comando toopreview unità per i BLOB hello è selezionata, in base alle dimensioni di hello di hello unità verrà toouse.</span><span class="sxs-lookup"><span data-stu-id="25d96-107">hello Import/Export Tool provides hello `PreviewExport` command toopreview drive usage for hello blobs you selected, based on hello size of hello drives you are going toouse.</span></span>

## <a name="command-line-parameters"></a><span data-ttu-id="25d96-108">Parametri della riga di comando</span><span class="sxs-lookup"><span data-stu-id="25d96-108">Command-line parameters</span></span>

<span data-ttu-id="25d96-109">È possibile utilizzare i seguenti parametri quando si utilizza hello hello `PreviewExport` comando di hello strumento di importazione/esportazione.</span><span class="sxs-lookup"><span data-stu-id="25d96-109">You can use hello following parameters when using hello `PreviewExport` command of hello Import/Export Tool.</span></span>

|<span data-ttu-id="25d96-110">Parametro della riga di comando</span><span class="sxs-lookup"><span data-stu-id="25d96-110">Command-line parameter</span></span>|<span data-ttu-id="25d96-111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="25d96-111">Description</span></span>|  
|--------------------------|-----------------|  
|<span data-ttu-id="25d96-112">**/logdir:**&lt;DirectoryLog\></span><span class="sxs-lookup"><span data-stu-id="25d96-112">**/logdir:**<LogDirectory\></span></span>|<span data-ttu-id="25d96-113">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="25d96-113">Optional.</span></span> <span data-ttu-id="25d96-114">directory dei log Hello.</span><span class="sxs-lookup"><span data-stu-id="25d96-114">hello log directory.</span></span> <span data-ttu-id="25d96-115">File di log dettagliati verranno scritti toothis directory.</span><span class="sxs-lookup"><span data-stu-id="25d96-115">Verbose log files will be written toothis directory.</span></span> <span data-ttu-id="25d96-116">Se non viene specificata alcuna directory di log, la directory corrente hello da utilizzare come directory dei log hello.</span><span class="sxs-lookup"><span data-stu-id="25d96-116">If no log directory is specified, hello current directory will be used as hello log directory.</span></span>|  
|<span data-ttu-id="25d96-117">**/sn:**<NomeAccountArchiviazione\></span><span class="sxs-lookup"><span data-stu-id="25d96-117">**/sn:**<StorageAccountName\></span></span>|<span data-ttu-id="25d96-118">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="25d96-118">Required.</span></span> <span data-ttu-id="25d96-119">processo di esportazione nome Hello hello dell'account di archiviazione per hello.</span><span class="sxs-lookup"><span data-stu-id="25d96-119">hello name of hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="25d96-120">**/sk:**&lt;ChiaveAccountArchiviazione\></span><span class="sxs-lookup"><span data-stu-id="25d96-120">**/sk:**<StorageAccountKey\></span></span>|<span data-ttu-id="25d96-121">Obbligatorio solo se non è specificata una firma di accesso condiviso del contenitore.</span><span class="sxs-lookup"><span data-stu-id="25d96-121">Required if and only if a container SAS is not specified.</span></span> <span data-ttu-id="25d96-122">processo di esportazione chiave Hello per l'account di archiviazione hello per hello.</span><span class="sxs-lookup"><span data-stu-id="25d96-122">hello account key for hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="25d96-123">**/csas:**&lt;ContainerSas\></span><span class="sxs-lookup"><span data-stu-id="25d96-123">**/csas:**<ContainerSas\></span></span>|<span data-ttu-id="25d96-124">Obbligatorio solo se non è specificata una chiave dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="25d96-124">Required if and only if a storage account key is not specified.</span></span> <span data-ttu-id="25d96-125">il contenitore di Hello SAS per elenco hello BLOB toobe esportati nel processo di esportazione hello.</span><span class="sxs-lookup"><span data-stu-id="25d96-125">hello container SAS for listing hello blobs toobe exported in hello export job.</span></span>|  
|<span data-ttu-id="25d96-126">**/ExportBlobListFile:**&lt;FileElencoBlobEsportazione\></span><span class="sxs-lookup"><span data-stu-id="25d96-126">**/ExportBlobListFile:**<ExportBlobListFile\></span></span>|<span data-ttu-id="25d96-127">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="25d96-127">Required.</span></span> <span data-ttu-id="25d96-128">Toohello percorso XML del file contenente l'elenco dei percorsi blob o prefissi di percorso per toobe BLOB hello esportata blob.</span><span class="sxs-lookup"><span data-stu-id="25d96-128">Path toohello XML file containing list of blob paths or blob path prefixes for hello blobs toobe exported.</span></span> <span data-ttu-id="25d96-129">formato di file Hello usato in hello `BlobListBlobPath` elemento hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operazione di hello API REST del servizio importazione/esportazione.</span><span class="sxs-lookup"><span data-stu-id="25d96-129">hello file format used in hello `BlobListBlobPath` element in hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation of hello Import/Export service REST API.</span></span>|  
|<span data-ttu-id="25d96-130">**/DriveSize:**&lt;DimensioneUnità\></span><span class="sxs-lookup"><span data-stu-id="25d96-130">**/DriveSize:**<DriveSize\></span></span>|<span data-ttu-id="25d96-131">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="25d96-131">Required.</span></span> <span data-ttu-id="25d96-132">dimensioni dell'unità toouse per un processo di esportazione, Hello *ad esempio*, 500 GB o 1,5 TB.</span><span class="sxs-lookup"><span data-stu-id="25d96-132">hello size of drives toouse for an export job, *e.g.*, 500GB, 1.5TB.</span></span>|  

## <a name="command-line-example"></a><span data-ttu-id="25d96-133">Esempio di riga di comando</span><span class="sxs-lookup"><span data-stu-id="25d96-133">Command-line example</span></span>

<span data-ttu-id="25d96-134">esempio Hello illustra hello `PreviewExport` comando:</span><span class="sxs-lookup"><span data-stu-id="25d96-134">hello following example demonstrates hello `PreviewExport` command:</span></span>  
  
```  
WAImportExport.exe PreviewExport /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\WAImportExport\mybloblist.xml /DriveSize:500GB    
```  
  
<span data-ttu-id="25d96-135">Hello blob elenco file di esportazione può contenere nomi blob e prefissi blob, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="25d96-135">hello export blob list file may contain blob names and blob prefixes, as shown here:</span></span>  
  
```xml 
<?xml version="1.0" encoding="utf-8"?>  
<BlobList>  
<BlobPath>pictures/animals/koala.jpg</BlobPath>  
<BlobPathPrefix>/vhds/</BlobPathPrefix>  
<BlobPathPrefix>/movies/</BlobPathPrefix>  
</BlobList>  
```

<span data-ttu-id="25d96-136">Hello strumento di importazione/esportazione di Azure Elenca tutti i BLOB toobe esportato e calcola come toopack in unità di hello specificato di dimensioni, prendendo in considerazione l'eventuale overhead necessario, quindi stima il numero di hello di unità necessarie BLOB hello toohold e utilizzo dell'unità informazioni.</span><span class="sxs-lookup"><span data-stu-id="25d96-136">hello Azure Import/Export Tool lists all blobs toobe exported and calculates how toopack them into drives of hello specified size, taking into account any necessary overhead, then estimates hello number of drives needed toohold hello blobs and drive usage information.</span></span>  
  
<span data-ttu-id="25d96-137">Di seguito è riportato un esempio di output di hello, senza log informativi:</span><span class="sxs-lookup"><span data-stu-id="25d96-137">Here is an example of hello output, with informational logs omitted:</span></span>  
  
```  
Number of unique blob paths/prefixes:   3  
Number of duplicate blob paths/prefixes:        0  
Number of nonexistent blob paths/prefixes:      1  
  
Drive size:     500.00 GB  
Number of blobs that can be exported:   6  
Number of blobs that cannot be exported:        2  
Number of drives needed:        3  
        Drive #1:       blobs = 1, occupied space = 454.74 GB  
        Drive #2:       blobs = 3, occupied space = 441.37 GB  
        Drive #3:       blobs = 2, occupied space = 131.28 GB    
```  
  
## <a name="next-steps"></a><span data-ttu-id="25d96-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="25d96-138">Next steps</span></span>

* <span data-ttu-id="25d96-139">[Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) (Informazioni di riferimento sullo strumento Importazione/Esportazione di Azure)</span><span class="sxs-lookup"><span data-stu-id="25d96-139">[Azure Import/Export Tool reference](storage-import-export-tool-how-to-v1.md)</span></span>
