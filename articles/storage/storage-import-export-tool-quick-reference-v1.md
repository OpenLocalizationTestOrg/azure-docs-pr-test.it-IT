---
title: Informazioni di riferimento rapido sui comandi per i processi di importazione dello strumento Importazione/Esportazione di Azure - versione 1 | Documentazione Microsoft
description: Guida di riferimento per i comandi dello strumento Importazione/Esportazione di Azure usati di frequente per i processi di importazione. Si riferisce alla versione 1 dello strumento Importazione/Esportazione.
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
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 47f450ee87dac3db2ccf7659928d52a6330a5697
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="37e1e-104">Informazioni di riferimento rapido sui comandi di uso frequente per i processi di importazione</span><span class="sxs-lookup"><span data-stu-id="37e1e-104">Quick reference for frequently used commands for import jobs</span></span>
<span data-ttu-id="37e1e-105">In questa sezione vengono forniti riferimenti rapidi per alcuni comandi usati di frequente.</span><span class="sxs-lookup"><span data-stu-id="37e1e-105">This section provides a quick references for some frequently used commands.</span></span> <span data-ttu-id="37e1e-106">Per informazioni dettagliate sull'uso, vedere [Preparazione dei dischi rigidi per un processo di importazione](storage-import-export-tool-preparing-hard-drives-import-v1.md).</span><span class="sxs-lookup"><span data-stu-id="37e1e-106">For detailed usage, see [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import-v1.md).</span></span>  

## <a name="prepare-the-disks-when-data-already-copied-to-the-disks"></a><span data-ttu-id="37e1e-107">Preparare i dischi quando i dati sono già copiati nei dischi</span><span class="sxs-lookup"><span data-stu-id="37e1e-107">Prepare the disks when data already copied to the disks</span></span>
 <span data-ttu-id="37e1e-108">Ecco un comando di esempio per preparare un disco quando i dati sono già copiati nel disco rigido non ancora crittografato con BitLocker:</span><span class="sxs-lookup"><span data-stu-id="37e1e-108">Here is a sample command to prepare a disks when data already copied to the hard drive that hasn't been yet been encrypted with BitLocker:</span></span>  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-to-a-hard-drive"></a><span data-ttu-id="37e1e-109">Copiare una singola directory in un disco rigido</span><span class="sxs-lookup"><span data-stu-id="37e1e-109">Copy a single directory to a hard drive</span></span>  
 <span data-ttu-id="37e1e-110">Ecco un comando di esempio per copiare una singola directory di origine in un disco rigido non ancora crittografato con BitLocker:</span><span class="sxs-lookup"><span data-stu-id="37e1e-110">Here is a sample command to copy a single source directory to a hard drive that hasn't been yet been encrypted with BitLocker:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-wwo-directories-to-a-hard-drive"></a><span data-ttu-id="37e1e-111">Copiare due directory in un disco rigido</span><span class="sxs-lookup"><span data-stu-id="37e1e-111">Copy wwo directories to a hard drive</span></span>  
 <span data-ttu-id="37e1e-112">Per copiare due directory di origine in un'unità, sarà necessario usare due comandi.</span><span class="sxs-lookup"><span data-stu-id="37e1e-112">To copy two source directories to a drive, you will need two commands.</span></span>  
  
 <span data-ttu-id="37e1e-113">Il primo comando specifica la directory di log, la chiave dell'account di archiviazione, la lettera dell'unità di destinazione e i requisiti `format/encrypt`, oltre ai parametri comuni:</span><span class="sxs-lookup"><span data-stu-id="37e1e-113">The first command specifies the log directory, storage account key, target drive letter and `format/encrypt` requirements, in addition to the common parameters:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 <span data-ttu-id="37e1e-114">Il secondo comando specifica il file journal, un nuovo ID di sessione e i percorsi di origine e di destinazione:</span><span class="sxs-lookup"><span data-stu-id="37e1e-114">The second command specifies the journal file, a new session ID, and the source and destination locations:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-to-a-hard-drive-in-a-second-copy-session"></a><span data-ttu-id="37e1e-115">Copiare un file di grandi dimensioni in un disco rigido in una seconda sessione di copia</span><span class="sxs-lookup"><span data-stu-id="37e1e-115">Copy a large file to a hard drive in a second copy session</span></span>  
 <span data-ttu-id="37e1e-116">Ecco un comando di esempio che copia un singolo file di grandi dimensioni in un'unità che è stata preparata in una sessione di copia precedente:</span><span class="sxs-lookup"><span data-stu-id="37e1e-116">Here is a sample command that copies a single large file to a drive that has been prepared in a previous copy session:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a><span data-ttu-id="37e1e-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="37e1e-117">Next steps</span></span>

* <span data-ttu-id="37e1e-118">[Sample workflow to prepare hard drives for an import job](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md) (Flusso di lavoro campione per preparare i dischi rigidi per un processo di importazione)</span><span class="sxs-lookup"><span data-stu-id="37e1e-118">[Sample workflow to prepare hard drives for an import job](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)</span></span>
