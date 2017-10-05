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
ms.openlocfilehash: 370cf6fae7ae106e8341f65086c8b8187d335746
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="33cce-104">Informazioni di riferimento rapido sui comandi di uso frequente per i processi di importazione</span><span class="sxs-lookup"><span data-stu-id="33cce-104">Quick reference for frequently used commands for import jobs</span></span>
<span data-ttu-id="33cce-105">Questa sezione contiene informazioni di riferimento rapido su alcuni comandi di uso frequente.</span><span class="sxs-lookup"><span data-stu-id="33cce-105">This section provides a quick reference for some frequently used commands.</span></span> <span data-ttu-id="33cce-106">Per informazioni dettagliate sull'uso, vedere [Preparazione dei dischi rigidi per un processo di importazione](../storage-import-export-tool-preparing-hard-drives-import-v1.md).</span><span class="sxs-lookup"><span data-stu-id="33cce-106">For detailed usage, see [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import-v1.md).</span></span>  

## <a name="prepare-a-hard-drive-when-data-has-already-been-copied-to-the-hard-drive"></a><span data-ttu-id="33cce-107">Preparare un disco rigido quando i dati sono già stati copiati nel disco rigido</span><span class="sxs-lookup"><span data-stu-id="33cce-107">Prepare a hard drive when data has already been copied to the hard drive</span></span>
 <span data-ttu-id="33cce-108">Il comando seguente consente di preparare un disco rigido quando i dati sono già stati copiati al suo interno ma non sono ancora stati crittografati con BitLocker:</span><span class="sxs-lookup"><span data-stu-id="33cce-108">The following command prepares a hard drive when data has already been copied to it, but has not yet been encrypted with BitLocker:</span></span>  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-to-a-hard-drive"></a><span data-ttu-id="33cce-109">Copiare una singola directory in un disco rigido</span><span class="sxs-lookup"><span data-stu-id="33cce-109">Copy a single directory to a hard drive</span></span>  
 <span data-ttu-id="33cce-110">Il comando seguente consente di copiare una singola directory di origine in un disco rigido non ancora crittografato con BitLocker:</span><span class="sxs-lookup"><span data-stu-id="33cce-110">The following command copies a single source directory to a hard drive that has not yet been encrypted with BitLocker:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-two-directories-to-a-hard-drive"></a><span data-ttu-id="33cce-111">Copiare due directory in un disco rigido</span><span class="sxs-lookup"><span data-stu-id="33cce-111">Copy two directories to a hard drive</span></span>  
 <span data-ttu-id="33cce-112">Per copiare due directory di origine in un'unità, usare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="33cce-112">To copy two source directories to a drive, use the following commands:</span></span>  
  
 <span data-ttu-id="33cce-113">Il primo comando specifica la directory di log, la chiave dell'account di archiviazione, la lettera dell'unità di destinazione e i requisiti `format/encrypt`, oltre ai parametri comuni:</span><span class="sxs-lookup"><span data-stu-id="33cce-113">The first command specifies the log directory, storage account key, target drive letter, `format/encrypt` requirements, and common parameters:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 <span data-ttu-id="33cce-114">Il secondo comando specifica il file journal, un nuovo ID di sessione e i percorsi di origine e di destinazione:</span><span class="sxs-lookup"><span data-stu-id="33cce-114">The second command specifies the journal file, a new session ID, and the source and destination locations:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-to-a-hard-drive-in-a-second-copy-session"></a><span data-ttu-id="33cce-115">Copiare un file di grandi dimensioni in un disco rigido in una seconda sessione di copia</span><span class="sxs-lookup"><span data-stu-id="33cce-115">Copy a large file to a hard drive in a second copy session</span></span>  
 <span data-ttu-id="33cce-116">Il comando seguente consente di copiare un singolo file di grandi dimensioni in un'unità preparata in una sessione di copia precedente:</span><span class="sxs-lookup"><span data-stu-id="33cce-116">The following command copies a single large file to a hard drive that was prepared in a previous copy session:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a><span data-ttu-id="33cce-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="33cce-117">Next steps</span></span>

* <span data-ttu-id="33cce-118">[Sample workflow to prepare hard drives for an import job](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md) (Flusso di lavoro campione per preparare i dischi rigidi per un processo di importazione)</span><span class="sxs-lookup"><span data-stu-id="33cce-118">[Sample workflow to prepare hard drives for an import job](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)</span></span>
