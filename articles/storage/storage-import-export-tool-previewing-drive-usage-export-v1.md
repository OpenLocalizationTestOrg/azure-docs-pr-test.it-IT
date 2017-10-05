---
title: Anteprima dell'uso del disco per un processo di esportazione in Importazione/Esportazione di Azure - versione 1 | Documentazione Microsoft
description: Informazioni su come visualizzare in anteprima l'elenco dei BLOB selezionati per un processo di esportazione nel servizio Importazione/Esportazione di Azure.
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
ms.openlocfilehash: 7bf74247090f91e17f81a9bc98ebfa78334c8c10
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="previewing-drive-usage-for-an-export-job"></a><span data-ttu-id="8074e-103">Anteprima dell'uso del disco per un processo di esportazione</span><span class="sxs-lookup"><span data-stu-id="8074e-103">Previewing drive usage for an export job</span></span>
<span data-ttu-id="8074e-104">Prima di creare un processo di esportazione, è necessario scegliere un set di BLOB da esportare.</span><span class="sxs-lookup"><span data-stu-id="8074e-104">Before you create an export job, you need to choose a set of blobs to be exported.</span></span> <span data-ttu-id="8074e-105">Il servizio Importazione/Esportazione di Microsoft Azure consente di usare un elenco di percorsi o prefissi BLOB per rappresentare i BLOB selezionati.</span><span class="sxs-lookup"><span data-stu-id="8074e-105">The Microsoft Azure Import/Export service allows you to use a list of blob paths or blob prefixes to represent the blobs you've selected.</span></span>  
  
<span data-ttu-id="8074e-106">È poi necessario determinare il numero di unità necessarie per l'invio.</span><span class="sxs-lookup"><span data-stu-id="8074e-106">Next, you need to determine how many drives you need to send.</span></span> <span data-ttu-id="8074e-107">Lo strumento Importazione/Esportazione consente di usare il comando `PreviewExport` per visualizzare in anteprima l'uso delle unità per i BLOB selezionati, in base alla dimensione delle unità che si intende usare.</span><span class="sxs-lookup"><span data-stu-id="8074e-107">The Import/Export Tool provides the `PreviewExport` command to preview drive usage for the blobs you selected, based on the size of the drives you are going to use.</span></span>

## <a name="command-line-parameters"></a><span data-ttu-id="8074e-108">Parametri della riga di comando</span><span class="sxs-lookup"><span data-stu-id="8074e-108">Command-line parameters</span></span>

<span data-ttu-id="8074e-109">Quando si usa il comando `PreviewExport` dello strumento Importazione/Esportazione, è possibile usare i parametri seguenti.</span><span class="sxs-lookup"><span data-stu-id="8074e-109">You can use the following parameters when using the `PreviewExport` command of the Import/Export Tool.</span></span>

|<span data-ttu-id="8074e-110">Parametro della riga di comando</span><span class="sxs-lookup"><span data-stu-id="8074e-110">Command-line parameter</span></span>|<span data-ttu-id="8074e-111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8074e-111">Description</span></span>|  
|--------------------------|-----------------|  
|<span data-ttu-id="8074e-112">**/logdir:**<DirectoryLog\></span><span class="sxs-lookup"><span data-stu-id="8074e-112">**/logdir:**<LogDirectory\></span></span>|<span data-ttu-id="8074e-113">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="8074e-113">Optional.</span></span> <span data-ttu-id="8074e-114">Directory dei log.</span><span class="sxs-lookup"><span data-stu-id="8074e-114">The log directory.</span></span> <span data-ttu-id="8074e-115">in cui verranno scritti file di log dettagliati.</span><span class="sxs-lookup"><span data-stu-id="8074e-115">Verbose log files will be written to this directory.</span></span> <span data-ttu-id="8074e-116">Se non è specificata alcuna directory dei log, verrà usata la directory corrente.</span><span class="sxs-lookup"><span data-stu-id="8074e-116">If no log directory is specified, the current directory will be used as the log directory.</span></span>|  
|<span data-ttu-id="8074e-117">**/sn:**<NomeAccountArchiviazione\></span><span class="sxs-lookup"><span data-stu-id="8074e-117">**/sn:**<StorageAccountName\></span></span>|<span data-ttu-id="8074e-118">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="8074e-118">Required.</span></span> <span data-ttu-id="8074e-119">Nome dell'account di archiviazione per il processo di esportazione.</span><span class="sxs-lookup"><span data-stu-id="8074e-119">The name of the storage account for the export job.</span></span>|  
|<span data-ttu-id="8074e-120">**/sk:**<ChiaveAccountArchiviazione\></span><span class="sxs-lookup"><span data-stu-id="8074e-120">**/sk:**<StorageAccountKey\></span></span>|<span data-ttu-id="8074e-121">Obbligatorio solo se non è specificata una firma di accesso condiviso del contenitore.</span><span class="sxs-lookup"><span data-stu-id="8074e-121">Required if and only if a container SAS is not specified.</span></span> <span data-ttu-id="8074e-122">Chiave dell'account per l'account di archiviazione per il processo di esportazione.</span><span class="sxs-lookup"><span data-stu-id="8074e-122">The account key for the storage account for the export job.</span></span>|  
|<span data-ttu-id="8074e-123">**/csas:**<FirmaAccessoCondivisoContenitore\></span><span class="sxs-lookup"><span data-stu-id="8074e-123">**/csas:**<ContainerSas\></span></span>|<span data-ttu-id="8074e-124">Obbligatorio solo se non è specificata una chiave dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="8074e-124">Required if and only if a storage account key is not specified.</span></span> <span data-ttu-id="8074e-125">Firma di accesso condiviso del contenitore per l'elenco dei BLOB da esportare nel processo di esportazione.</span><span class="sxs-lookup"><span data-stu-id="8074e-125">The container SAS for listing the blobs to be exported in the export job.</span></span>|  
|<span data-ttu-id="8074e-126">**/ExportBlobListFile:**<FileElencoBlobEsportazione\></span><span class="sxs-lookup"><span data-stu-id="8074e-126">**/ExportBlobListFile:**<ExportBlobListFile\></span></span>|<span data-ttu-id="8074e-127">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="8074e-127">Required.</span></span> <span data-ttu-id="8074e-128">Percorso del file XML contenente l'elenco dei percorsi o dei prefissi dei percorsi BLOB per i BLOB da esportare.</span><span class="sxs-lookup"><span data-stu-id="8074e-128">Path to the XML file containing list of blob paths or blob path prefixes for the blobs to be exported.</span></span> <span data-ttu-id="8074e-129">Formato di file usato nell'elemento `BlobListBlobPath` nell'operazione [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) dell'API REST del servizio Importazione/Esportazione.</span><span class="sxs-lookup"><span data-stu-id="8074e-129">The file format used in the `BlobListBlobPath` element in the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation of the Import/Export service REST API.</span></span>|  
|<span data-ttu-id="8074e-130">**/DriveSize:**<DimensioneUnità\></span><span class="sxs-lookup"><span data-stu-id="8074e-130">**/DriveSize:**<DriveSize\></span></span>|<span data-ttu-id="8074e-131">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="8074e-131">Required.</span></span> <span data-ttu-id="8074e-132">Dimensione delle unità da usare per un processo di esportazione, *ad es.* 500 GB, 1,5 TB.</span><span class="sxs-lookup"><span data-stu-id="8074e-132">The size of drives to use for an export job, *e.g.*, 500GB, 1.5TB.</span></span>|  

## <a name="command-line-example"></a><span data-ttu-id="8074e-133">Esempio di riga di comando</span><span class="sxs-lookup"><span data-stu-id="8074e-133">Command-line example</span></span>

<span data-ttu-id="8074e-134">L'esempio seguente illustra il comando `PreviewExport`:</span><span class="sxs-lookup"><span data-stu-id="8074e-134">The following example demonstrates the `PreviewExport` command:</span></span>  
  
```  
WAImportExport.exe PreviewExport /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\WAImportExport\mybloblist.xml /DriveSize:500GB    
```  
  
<span data-ttu-id="8074e-135">Il file dell'elenco del BLOB di esportazione può contenere nomi e prefissi BLOB, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="8074e-135">The export blob list file may contain blob names and blob prefixes, as shown here:</span></span>  
  
```xml 
<?xml version="1.0" encoding="utf-8"?>  
<BlobList>  
<BlobPath>pictures/animals/koala.jpg</BlobPath>  
<BlobPathPrefix>/vhds/</BlobPathPrefix>  
<BlobPathPrefix>/movies/</BlobPathPrefix>  
</BlobList>  
```

<span data-ttu-id="8074e-136">Lo strumento Importazione/Esportazione di Azure elenca tutti i BLOB da esportare e calcola come comprimerli in unità della dimensione specificata, tenendo conto dell'eventuale sovraccarico necessario, quindi stima il numero di unità richieste per contenere i BLOB e le informazioni sull'uso delle unità.</span><span class="sxs-lookup"><span data-stu-id="8074e-136">The Azure Import/Export Tool lists all blobs to be exported and calculates how to pack them into drives of the specified size, taking into account any necessary overhead, then estimates the number of drives needed to hold the blobs and drive usage information.</span></span>  
  
<span data-ttu-id="8074e-137">Di seguito è riportato un esempio dell'output, senza log informativi:</span><span class="sxs-lookup"><span data-stu-id="8074e-137">Here is an example of the output, with informational logs omitted:</span></span>  
  
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
  
## <a name="next-steps"></a><span data-ttu-id="8074e-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8074e-138">Next steps</span></span>

* <span data-ttu-id="8074e-139">[Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) (Informazioni di riferimento sullo strumento Importazione/Esportazione di Azure)</span><span class="sxs-lookup"><span data-stu-id="8074e-139">[Azure Import/Export Tool reference](storage-import-export-tool-how-to-v1.md)</span></span>
