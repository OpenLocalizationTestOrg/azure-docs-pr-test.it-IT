---
title: hello aaaUsing API REST del servizio importazione/esportazione di Azure | Documenti Microsoft
description: Informazioni su dove del servizio API REST, inclusi entrambi materiale di riferimento come tooand toofind risorse per l'utilizzo di hello importazione/esportazione di Azure.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 233f80e9-2e7f-48e0-9639-5c7785e7d743
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: a01c170b1bc9c2b2ce9086d39de78a39fafb2c8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-importexport-service-rest-api"></a><span data-ttu-id="baa42-103">Tramite l'API REST del servizio importazione/esportazione di Azure hello</span><span class="sxs-lookup"><span data-stu-id="baa42-103">Using hello Azure Import/Export service REST API</span></span>

<span data-ttu-id="baa42-104">Hello servizio importazione/esportazione di Microsoft Azure espone un controllo a livello di codice tooenable di API REST dei processi di importazione/esportazione.</span><span class="sxs-lookup"><span data-stu-id="baa42-104">hello Microsoft Azure Import/Export service exposes a REST API tooenable programmatic control of import/export jobs.</span></span> <span data-ttu-id="baa42-105">È possibile utilizzare l'API REST di hello tooperform tutti hello importazione/esportazione di operazioni che è possibile eseguire con hello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="baa42-105">You can use hello REST API tooperform all of hello import/export operations that you can perform with hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="baa42-106">Inoltre, è possibile utilizzare hello API REST tooperform determinate operazioni granulari, ad esempio hello percentuale di completamento di un processo, l'esecuzione di query che non sono attualmente disponibili nel portale classico hello.</span><span class="sxs-lookup"><span data-stu-id="baa42-106">Additionally, you can use hello REST API tooperform certain granular operations, such as querying hello percentage completion of a job, which are not currently available in hello classic portal.</span></span>

<span data-ttu-id="baa42-107">Vedere [tramite servizio di importazione/esportazione di Microsoft Azure hello, dati tooTransfer tooBlob archiviazione](storage-import-export-service.md) per una panoramica del servizio di importazione/esportazione hello e un'esercitazione che illustra come toouse hello toocreate portale classico e gestire l'importazione e i processi di esportazione.</span><span class="sxs-lookup"><span data-stu-id="baa42-107">See [Using hello Microsoft Azure Import/Export service tooTransfer Data tooBlob Storage](storage-import-export-service.md) for an overview of hello Import/Export service and a tutorial that demonstrates how toouse hello classic portal toocreate and manage import and export jobs.</span></span>

## <a name="service-endpoints"></a><span data-ttu-id="baa42-108">Endpoint di servizio</span><span class="sxs-lookup"><span data-stu-id="baa42-108">Service endpoints</span></span>

<span data-ttu-id="baa42-109">Hello servizio importazione/esportazione di Azure è un provider di risorse per Gestione risorse di Azure e fornisce un set di API REST a hello endpoint HTTPS per la gestione dei processi di importazione/esportazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="baa42-109">hello Azure Import/Export service is a resource provider for Azure Resource Manager and provides a set of REST APIs at hello following HTTPS endpoint for managing import/export jobs:</span></span>

```
https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.ImportExport/jobs/<job-name>
```

## <a name="versioning"></a><span data-ttu-id="baa42-110">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="baa42-110">Versioning</span></span>

<span data-ttu-id="baa42-111">Le richieste di servizio di importazione/esportazione toohello deve specificare hello `api-version` parametro e impostarne il valore troppo`2016-11-01`.</span><span class="sxs-lookup"><span data-stu-id="baa42-111">Requests toohello Import/Export service must specify hello `api-version` parameter and set its value too`2016-11-01`.</span></span>

## <a name="importexport-service-operations"></a><span data-ttu-id="baa42-112">Operazioni del servizio Importazione/Esportazione</span><span class="sxs-lookup"><span data-stu-id="baa42-112">Import/Export service operations</span></span>

<span data-ttu-id="baa42-113">[Creating an import job](storage-import-export-creating-an-import-job.md) (Creazione di un processo di importazione)</span><span class="sxs-lookup"><span data-stu-id="baa42-113">[Creating an import job](storage-import-export-creating-an-import-job.md)</span></span>

<span data-ttu-id="baa42-114">[Creating an export job](storage-import-export-creating-an-export-job.md) (Creazione di un processo di esportazione)</span><span class="sxs-lookup"><span data-stu-id="baa42-114">[Creating an export job](storage-import-export-creating-an-export-job.md)</span></span>

<span data-ttu-id="baa42-115">[Retrieving state information for a job](storage-import-export-retrieving-state-info-for-a-job.md) (Recupero delle informazioni sullo stato per un processo)</span><span class="sxs-lookup"><span data-stu-id="baa42-115">[Retrieving state information for a job](storage-import-export-retrieving-state-info-for-a-job.md)</span></span>

<span data-ttu-id="baa42-116">[Enumerating jobs](storage-import-export-enumerating-jobs.md) (Enumerazione dei processi)</span><span class="sxs-lookup"><span data-stu-id="baa42-116">[Enumerating jobs](storage-import-export-enumerating-jobs.md)</span></span>

<span data-ttu-id="baa42-117">[Cancelling and deleting jobs](storage-import-export-cancelling-and-deleting-jobs.md) (Annullamento ed eliminazione dei processi)</span><span class="sxs-lookup"><span data-stu-id="baa42-117">[Cancelling and deleting jobs](storage-import-export-cancelling-and-deleting-jobs.md)</span></span>

[<span data-ttu-id="baa42-118">Backup dei manifesti delle unità</span><span class="sxs-lookup"><span data-stu-id="baa42-118">Backing Up drive manifests</span></span>](storage-import-export-backing-up-drive-manifests.md)

[<span data-ttu-id="baa42-119">Diagnostica e ripristino dagli errori per i processi di Importazione/Esportazione</span><span class="sxs-lookup"><span data-stu-id="baa42-119">Diagnostics and error recovery for Import/Export jobs</span></span>](storage-import-export-diagnostics-and-error-recovery.md)

## <a name="next-steps"></a><span data-ttu-id="baa42-120">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="baa42-120">Next steps</span></span>

* [<span data-ttu-id="baa42-121">REST di importazione/esportazione dell'archiviazione</span><span class="sxs-lookup"><span data-stu-id="baa42-121">Storage Import/Export REST</span></span>](/rest/api/storageimportexport)
