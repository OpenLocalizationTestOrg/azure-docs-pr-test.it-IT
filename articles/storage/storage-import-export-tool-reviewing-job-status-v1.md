---
title: Esame dello stato del processo di importazione/esportazione di Azure - versione 1 | Documentazione Microsoft
description: "Informazioni su come usare i file di log creati quando il processo di importazione o esportazione è stato eseguito per visualizzare lo stato del processo di importazione/esportazione."
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
ms.openlocfilehash: 621e41df127fded6ec6fe1f71e86cb8630965a70
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="reviewing-azure-importexport-job-status-with-copy-log-files"></a><span data-ttu-id="a8e3c-103">Esame dello stato del processo di Importazione/Esportazione di Azure con i file di log di copia</span><span class="sxs-lookup"><span data-stu-id="a8e3c-103">Reviewing Azure Import/Export job status with copy log files</span></span>
<span data-ttu-id="a8e3c-104">Quando il servizio Importazione/Esportazione di Microsoft Azure elabora unità associate a un processo di importazione o esportazione, scrive file di log di copia per l'account di archiviazione verso cui o da cui si importano o si esportano BLOB.</span><span class="sxs-lookup"><span data-stu-id="a8e3c-104">When the Microsoft Azure Import/Export service processes drives associated with an import or export job, it writes copy log files to the storage account to or from which you are importing or exporting blobs.</span></span> <span data-ttu-id="a8e3c-105">Il file di log contiene lo stato dettagliato di ogni file importato o esportato.</span><span class="sxs-lookup"><span data-stu-id="a8e3c-105">The log file contains detailed status about each file that was imported or exported.</span></span> <span data-ttu-id="a8e3c-106">L'URL ad ogni file di log di copia viene restituito quando si esegue una query sullo stato di un processo completato. Per ulteriori informazioni, vedere [Get Job](/rest/api/storageservices/Get-Job3).</span><span class="sxs-lookup"><span data-stu-id="a8e3c-106">The URL to each copy log file is returned when you query the status of a completed job; see [Get Job](/rest/api/storageservices/Get-Job3) for more information.</span></span>  

## <a name="example-urls"></a><span data-ttu-id="a8e3c-107">URL di esempio</span><span class="sxs-lookup"><span data-stu-id="a8e3c-107">Example URLs</span></span>

<span data-ttu-id="a8e3c-108">Di seguito sono mostrati URL di esempio per i file di log di copia per un processo di importazione con due unità:</span><span class="sxs-lookup"><span data-stu-id="a8e3c-108">The following are example URLs for copy log files for an import job with two drives:</span></span>  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  
  
 <span data-ttu-id="a8e3c-109">Per informazioni sul formato dei log di copia e l'elenco completo dei codici di stato, vedere [Formato dei file di log del servizio Importazione/Esportazione di Azure](storage-import-export-file-format-log.md).</span><span class="sxs-lookup"><span data-stu-id="a8e3c-109">See [Import/Export service Log File Format](storage-import-export-file-format-log.md) for the format of copy logs and the full list of status codes.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="a8e3c-110">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a8e3c-110">Next steps</span></span>
 
 * [<span data-ttu-id="a8e3c-111">Configurazione dello strumento Importazione/Esportazione di Azure</span><span class="sxs-lookup"><span data-stu-id="a8e3c-111">Setting Up the Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
 * <span data-ttu-id="a8e3c-112">[Preparing hard drives for an import job](storage-import-export-tool-preparing-hard-drives-import-v1.md) (Preparazione dei dischi rigidi per un processo di importazione)</span><span class="sxs-lookup"><span data-stu-id="a8e3c-112">[Preparing hard drives for an import job](storage-import-export-tool-preparing-hard-drives-import-v1.md)</span></span>   
 * <span data-ttu-id="a8e3c-113">[Repairing an import job](storage-import-export-tool-repairing-an-import-job-v1.md) (Riparazione di un processo di importazione)</span><span class="sxs-lookup"><span data-stu-id="a8e3c-113">[Repairing an import job](storage-import-export-tool-repairing-an-import-job-v1.md)</span></span>   
 * <span data-ttu-id="a8e3c-114">[Repairing an export job](storage-import-export-tool-repairing-an-export-job-v1.md) (Riparazione di un processo di esportazione)</span><span class="sxs-lookup"><span data-stu-id="a8e3c-114">[Repairing an export job](storage-import-export-tool-repairing-an-export-job-v1.md)</span></span>   
 * [<span data-ttu-id="a8e3c-115">Risoluzione dei problemi relativi allo strumento Importazione/Esportazione di Azure</span><span class="sxs-lookup"><span data-stu-id="a8e3c-115">Troubleshooting the Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
