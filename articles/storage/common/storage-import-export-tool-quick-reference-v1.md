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
ms.openlocfilehash: 945eb4f9eff28c92ec963585d27cba73a7eb59bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="5c8ff-104">Informazioni di riferimento rapido sui comandi di uso frequente per i processi di importazione</span><span class="sxs-lookup"><span data-stu-id="5c8ff-104">Quick reference for frequently used commands for import jobs</span></span>
<span data-ttu-id="5c8ff-105">Questa sezione contiene informazioni di riferimento rapido su alcuni comandi di uso frequente.</span><span class="sxs-lookup"><span data-stu-id="5c8ff-105">This section provides a quick reference for some frequently used commands.</span></span> <span data-ttu-id="5c8ff-106">Per informazioni dettagliate sull'uso, vedere [Preparazione dei dischi rigidi per un processo di importazione](../storage-import-export-tool-preparing-hard-drives-import-v1.md).</span><span class="sxs-lookup"><span data-stu-id="5c8ff-106">For detailed usage, see [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import-v1.md).</span></span>  

## <a name="prepare-a-hard-drive-when-data-has-already-been-copied-toohello-hard-drive"></a><span data-ttu-id="5c8ff-107">Preparare un disco rigido quando i dati sono già stati copiati toohello disco rigido</span><span class="sxs-lookup"><span data-stu-id="5c8ff-107">Prepare a hard drive when data has already been copied toohello hard drive</span></span>
 <span data-ttu-id="5c8ff-108">Hello comando seguente consente di preparare un disco rigido quando sono già stato copiato tooit di dati, ma non sono ancora stati crittografati con BitLocker:</span><span class="sxs-lookup"><span data-stu-id="5c8ff-108">hello following command prepares a hard drive when data has already been copied tooit, but has not yet been encrypted with BitLocker:</span></span>  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-tooa-hard-drive"></a><span data-ttu-id="5c8ff-109">Copiare un singola directory tooa disco rigido</span><span class="sxs-lookup"><span data-stu-id="5c8ff-109">Copy a single directory tooa hard drive</span></span>  
 <span data-ttu-id="5c8ff-110">Hello comando seguente consente di copiare un singola origine directory tooa disco rigido che non è ancora stato crittografato con BitLocker:</span><span class="sxs-lookup"><span data-stu-id="5c8ff-110">hello following command copies a single source directory tooa hard drive that has not yet been encrypted with BitLocker:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-two-directories-tooa-hard-drive"></a><span data-ttu-id="5c8ff-111">Copiare due directory tooa disco rigido</span><span class="sxs-lookup"><span data-stu-id="5c8ff-111">Copy two directories tooa hard drive</span></span>  
 <span data-ttu-id="5c8ff-112">unità di tooa directory origine toocopy due, hello di utilizzare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="5c8ff-112">toocopy two source directories tooa drive, use hello following commands:</span></span>  
  
 <span data-ttu-id="5c8ff-113">Hello primo comando specifica directory log hello, chiave dell'account di archiviazione, lettera di unità di destinazione, `format/encrypt` , requisiti e i parametri comuni:</span><span class="sxs-lookup"><span data-stu-id="5c8ff-113">hello first command specifies hello log directory, storage account key, target drive letter, `format/encrypt` requirements, and common parameters:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 <span data-ttu-id="5c8ff-114">comando secondo Hello specifica file journal hello, un nuovo ID sessione e i percorsi di origine e destinazione di hello:</span><span class="sxs-lookup"><span data-stu-id="5c8ff-114">hello second command specifies hello journal file, a new session ID, and hello source and destination locations:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-tooa-hard-drive-in-a-second-copy-session"></a><span data-ttu-id="5c8ff-115">Copiare un file di grandi dimensioni tooa disco rigido in una seconda sessione di copia</span><span class="sxs-lookup"><span data-stu-id="5c8ff-115">Copy a large file tooa hard drive in a second copy session</span></span>  
 <span data-ttu-id="5c8ff-116">Hello comando seguente copia un file di grandi dimensioni tooa disco rigido preparato in una sessione di copia precedente:</span><span class="sxs-lookup"><span data-stu-id="5c8ff-116">hello following command copies a single large file tooa hard drive that was prepared in a previous copy session:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a><span data-ttu-id="5c8ff-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5c8ff-117">Next steps</span></span>

* [<span data-ttu-id="5c8ff-118">Unità disco rigido tooprepare del flusso di lavoro di esempio per un processo di importazione</span><span class="sxs-lookup"><span data-stu-id="5c8ff-118">Sample workflow tooprepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
