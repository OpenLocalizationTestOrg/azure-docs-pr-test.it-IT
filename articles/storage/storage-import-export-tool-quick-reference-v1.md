---
title: riferimento aaaQuick per i comandi di processo di importazione dello strumento di importazione/esportazione di Azure - v1 | Documenti Microsoft
description: Guida di riferimento per i comandi dello strumento Importazione/Esportazione di Azure usati di frequente per i processi di importazione. Si riferisce toov1 di hello strumento di importazione/esportazione.
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
ms.openlocfilehash: e36f065e5d23268758cf6b6db9428fe8a8e1056d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="d0675-104">Informazioni di riferimento rapido sui comandi di uso frequente per i processi di importazione</span><span class="sxs-lookup"><span data-stu-id="d0675-104">Quick reference for frequently used commands for import jobs</span></span>
<span data-ttu-id="d0675-105">In questa sezione vengono forniti riferimenti rapidi per alcuni comandi usati di frequente.</span><span class="sxs-lookup"><span data-stu-id="d0675-105">This section provides a quick references for some frequently used commands.</span></span> <span data-ttu-id="d0675-106">Per informazioni dettagliate sull'uso, vedere [Preparazione dei dischi rigidi per un processo di importazione](storage-import-export-tool-preparing-hard-drives-import-v1.md).</span><span class="sxs-lookup"><span data-stu-id="d0675-106">For detailed usage, see [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import-v1.md).</span></span>  

## <a name="prepare-hello-disks-when-data-already-copied-toohello-disks"></a><span data-ttu-id="d0675-107">Preparare i dischi di hello quando i dati copiati già toohello dischi</span><span class="sxs-lookup"><span data-stu-id="d0675-107">Prepare hello disks when data already copied toohello disks</span></span>
 <span data-ttu-id="d0675-108">Ecco un tooprepare di comando di esempio un dischi quando i dati copiati già toohello disco rigido che non ancora crittografato con BitLocker:</span><span class="sxs-lookup"><span data-stu-id="d0675-108">Here is a sample command tooprepare a disks when data already copied toohello hard drive that hasn't been yet been encrypted with BitLocker:</span></span>  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-tooa-hard-drive"></a><span data-ttu-id="d0675-109">Copiare un singola directory tooa disco rigido</span><span class="sxs-lookup"><span data-stu-id="d0675-109">Copy a single directory tooa hard drive</span></span>  
 <span data-ttu-id="d0675-110">Ecco un toocopy di comando di esempio una singola origine directory tooa unità disco rigido non ancora crittografato con BitLocker:</span><span class="sxs-lookup"><span data-stu-id="d0675-110">Here is a sample command toocopy a single source directory tooa hard drive that hasn't been yet been encrypted with BitLocker:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-wwo-directories-tooa-hard-drive"></a><span data-ttu-id="d0675-111">Copiare wwo directory tooa disco rigido</span><span class="sxs-lookup"><span data-stu-id="d0675-111">Copy wwo directories tooa hard drive</span></span>  
 <span data-ttu-id="d0675-112">toocopy due directory tooa unità di origine, sono necessari due comandi.</span><span class="sxs-lookup"><span data-stu-id="d0675-112">toocopy two source directories tooa drive, you will need two commands.</span></span>  
  
 <span data-ttu-id="d0675-113">Hello primo comando specifica directory log hello, chiave dell'account di archiviazione, lettera di unità di destinazione e `format/encrypt` requisiti, in parametri comuni di addizione toohello:</span><span class="sxs-lookup"><span data-stu-id="d0675-113">hello first command specifies hello log directory, storage account key, target drive letter and `format/encrypt` requirements, in addition toohello common parameters:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 <span data-ttu-id="d0675-114">comando secondo Hello specifica file journal hello, un nuovo ID sessione e i percorsi di origine e destinazione di hello:</span><span class="sxs-lookup"><span data-stu-id="d0675-114">hello second command specifies hello journal file, a new session ID, and hello source and destination locations:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-tooa-hard-drive-in-a-second-copy-session"></a><span data-ttu-id="d0675-115">Copiare un file di grandi dimensioni tooa disco rigido in una seconda sessione di copia</span><span class="sxs-lookup"><span data-stu-id="d0675-115">Copy a large file tooa hard drive in a second copy session</span></span>  
 <span data-ttu-id="d0675-116">Di seguito è riportato un esempio del comando che consente di copiare un'unità tooa singolo file di grandi dimensioni che è stata preparata in una sessione di copia precedente:</span><span class="sxs-lookup"><span data-stu-id="d0675-116">Here is a sample command that copies a single large file tooa drive that has been prepared in a previous copy session:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a><span data-ttu-id="d0675-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d0675-117">Next steps</span></span>

* [<span data-ttu-id="d0675-118">Unità disco rigido tooprepare del flusso di lavoro di esempio per un processo di importazione</span><span class="sxs-lookup"><span data-stu-id="d0675-118">Sample workflow tooprepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
