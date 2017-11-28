---
title: stato del processo di importazione/esportazione di Azure - v1 aaaReviewing | Documenti Microsoft
description: "Informazioni su come file di log di hello toouse creati quando hello importazione o Esporta processo è stato eseguito il processo di importazione/esportazione di hello stato hello toosee."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: c69d1d69-6403-4eee-9949-0185faeecfa1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: muralikk
ms.openlocfilehash: 378bc9a7ef6bfe65209413c8c4134f313a2c0d79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reviewing-azure-importexport-job-status-with-copy-log-files"></a><span data-ttu-id="d75fa-103">Esame dello stato del processo di Importazione/Esportazione di Azure con i file di log di copia</span><span class="sxs-lookup"><span data-stu-id="d75fa-103">Reviewing Azure Import/Export job status with copy log files</span></span>
<span data-ttu-id="d75fa-104">Quando hello servizio importazione/esportazione di Microsoft Azure elabora unità associate a un processo di importazione o esportazione, viene scritta copia log file toohello storage account tooor da cui si importano o esportano i BLOB.</span><span class="sxs-lookup"><span data-stu-id="d75fa-104">When hello Microsoft Azure Import/Export service processes drives associated with an import or export job, it writes copy log files toohello storage account tooor from which you are importing or exporting blobs.</span></span> <span data-ttu-id="d75fa-105">file di log Hello contiene lo stato dettagliato di ogni file importato o esportato.</span><span class="sxs-lookup"><span data-stu-id="d75fa-105">hello log file contains detailed status about each file that was imported or exported.</span></span> <span data-ttu-id="d75fa-106">file di log di copia di Hello URL tooeach viene restituito quando si esegue una query sullo stato di hello di un processo completato. vedere [recupero del processo](/rest/api/storageservices/Get-Job3) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="d75fa-106">hello URL tooeach copy log file is returned when you query hello status of a completed job; see [Get Job](/rest/api/storageservices/Get-Job3) for more information.</span></span>  

## <a name="example-urls"></a><span data-ttu-id="d75fa-107">URL di esempio</span><span class="sxs-lookup"><span data-stu-id="d75fa-107">Example URLs</span></span>

<span data-ttu-id="d75fa-108">di seguito Hello sono gli URL di esempio per i file di log di copia per un processo di importazione con due unità:</span><span class="sxs-lookup"><span data-stu-id="d75fa-108">hello following are example URLs for copy log files for an import job with two drives:</span></span>  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  
  
 <span data-ttu-id="d75fa-109">Vedere [il servizio di importazione/esportazione il formato di File di Log](storage-import-export-file-format-log.md) formato hello dei log di copia e l'elenco completo di hello dei codici di stato.</span><span class="sxs-lookup"><span data-stu-id="d75fa-109">See [Import/Export service Log File Format](storage-import-export-file-format-log.md) for hello format of copy logs and hello full list of status codes.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="d75fa-110">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d75fa-110">Next steps</span></span>
 
 * [<span data-ttu-id="d75fa-111">Impostazione hello strumento di importazione/esportazione di Azure</span><span class="sxs-lookup"><span data-stu-id="d75fa-111">Setting Up hello Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
 * <span data-ttu-id="d75fa-112">[Preparing hard drives for an import job](storage-import-export-tool-preparing-hard-drives-import-v1.md) (Preparazione dei dischi rigidi per un processo di importazione)</span><span class="sxs-lookup"><span data-stu-id="d75fa-112">[Preparing hard drives for an import job](storage-import-export-tool-preparing-hard-drives-import-v1.md)</span></span>   
 * <span data-ttu-id="d75fa-113">[Repairing an import job](storage-import-export-tool-repairing-an-import-job-v1.md) (Riparazione di un processo di importazione)</span><span class="sxs-lookup"><span data-stu-id="d75fa-113">[Repairing an import job](storage-import-export-tool-repairing-an-import-job-v1.md)</span></span>   
 * <span data-ttu-id="d75fa-114">[Repairing an export job](storage-import-export-tool-repairing-an-export-job-v1.md) (Riparazione di un processo di esportazione)</span><span class="sxs-lookup"><span data-stu-id="d75fa-114">[Repairing an export job](storage-import-export-tool-repairing-an-export-job-v1.md)</span></span>   
 * [<span data-ttu-id="d75fa-115">Risoluzione dei problemi hello strumento di importazione/esportazione di Azure</span><span class="sxs-lookup"><span data-stu-id="d75fa-115">Troubleshooting hello Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
