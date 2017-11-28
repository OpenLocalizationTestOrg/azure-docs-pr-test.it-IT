---
title: aaaAzure Analitica Batch | Documenti Microsoft
description: Riferimento per le analisi di Azure Batch.
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: 462fbad1ac522b485ae18c1e8891b9d2cabd45e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="batch-analytics"></a><span data-ttu-id="ed070-103">Batch Analytics</span><span class="sxs-lookup"><span data-stu-id="ed070-103">Batch Analytics</span></span>
<span data-ttu-id="ed070-104">Negli argomenti di Hello Analitica Batch contengono informazioni di riferimento per gli eventi di hello e gli avvisi disponibili per le risorse del servizio Batch.</span><span class="sxs-lookup"><span data-stu-id="ed070-104">hello topics in Batch Analytics contain reference information for hello events and alerts available for Batch service resources.</span></span>

<span data-ttu-id="ed070-105">Per altre informazioni sull'abilitazione e sull'uso di log di diagnostica di Batch, vedere [Registrazione diagnostica di Azure Batch](https://azure.microsoft.com/documentation/articles/batch-diagnostics/).</span><span class="sxs-lookup"><span data-stu-id="ed070-105">See [Azure Batch diagnostic logging](https://azure.microsoft.com/documentation/articles/batch-diagnostics/) for more information on enabling and consuming Batch diagnostic logs.</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="ed070-106">Log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="ed070-106">Diagnostic logs</span></span>

<span data-ttu-id="ed070-107">servizio Azure Batch Hello genera hello dopo gli eventi di log di diagnostica nel corso della durata hello di alcune risorse di Batch.</span><span class="sxs-lookup"><span data-stu-id="ed070-107">hello Azure Batch service emits hello following diagnostic log events during hello lifetime of certain Batch resources.</span></span>

<span data-ttu-id="ed070-108">**Eventi del log del servizio**</span><span class="sxs-lookup"><span data-stu-id="ed070-108">**Service Log events**</span></span>
* [<span data-ttu-id="ed070-109">Creazione di pool</span><span class="sxs-lookup"><span data-stu-id="ed070-109">Pool create</span></span>](batch-pool-create-event.md)
* [<span data-ttu-id="ed070-110">Avvio dell'eliminazione di pool</span><span class="sxs-lookup"><span data-stu-id="ed070-110">Pool delete start</span></span>](batch-pool-delete-start-event.md)
* [<span data-ttu-id="ed070-111">Completamento dell'eliminazione di pool</span><span class="sxs-lookup"><span data-stu-id="ed070-111">Pool delete complete</span></span>](batch-pool-delete-complete-event.md)
* [<span data-ttu-id="ed070-112">Avvio del ridimensionamento di pool</span><span class="sxs-lookup"><span data-stu-id="ed070-112">Pool resize start</span></span>](batch-pool-resize-start-event.md)
* [<span data-ttu-id="ed070-113">Completamento del ridimensionamento di pool</span><span class="sxs-lookup"><span data-stu-id="ed070-113">Pool resize complete</span></span>](batch-pool-resize-complete-event.md)
* [<span data-ttu-id="ed070-114">Avvio dell'attività</span><span class="sxs-lookup"><span data-stu-id="ed070-114">Task start</span></span>](batch-task-start-event.md)
* [<span data-ttu-id="ed070-115">Attività completata</span><span class="sxs-lookup"><span data-stu-id="ed070-115">Task complete</span></span>](batch-task-complete-event.md)
* [<span data-ttu-id="ed070-116">Errore dell'attività</span><span class="sxs-lookup"><span data-stu-id="ed070-116">Task fail</span></span>](batch-task-fail-event.md)