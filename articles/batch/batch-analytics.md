---
title: Analisi di Azure Batch | Microsoft Docs
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
ms.openlocfilehash: 7d634e1bb595a84b8af339e5bc5a483a7849e7f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="batch-analytics"></a><span data-ttu-id="373d3-103">Batch Analytics</span><span class="sxs-lookup"><span data-stu-id="373d3-103">Batch Analytics</span></span>
<span data-ttu-id="373d3-104">Gli argomenti di Batch Analytics includono informazioni di riferimento per gli eventi e gli avvisi disponibili per le risorse del servizio Batch.</span><span class="sxs-lookup"><span data-stu-id="373d3-104">The topics in Batch Analytics contain reference information for the events and alerts available for Batch service resources.</span></span>

<span data-ttu-id="373d3-105">Per altre informazioni sull'abilitazione e sull'uso di log di diagnostica di Batch, vedere [Registrazione diagnostica di Azure Batch](https://azure.microsoft.com/documentation/articles/batch-diagnostics/).</span><span class="sxs-lookup"><span data-stu-id="373d3-105">See [Azure Batch diagnostic logging](https://azure.microsoft.com/documentation/articles/batch-diagnostics/) for more information on enabling and consuming Batch diagnostic logs.</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="373d3-106">Log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="373d3-106">Diagnostic logs</span></span>

<span data-ttu-id="373d3-107">Il servizio Azure Batch produce i seguenti eventi di registro di diagnostica nel corso della durata di determinate risorse Batch.</span><span class="sxs-lookup"><span data-stu-id="373d3-107">The Azure Batch service emits the following diagnostic log events during the lifetime of certain Batch resources.</span></span>

<span data-ttu-id="373d3-108">**Eventi del log del servizio**</span><span class="sxs-lookup"><span data-stu-id="373d3-108">**Service Log events**</span></span>
* [<span data-ttu-id="373d3-109">Creazione di pool</span><span class="sxs-lookup"><span data-stu-id="373d3-109">Pool create</span></span>](batch-pool-create-event.md)
* [<span data-ttu-id="373d3-110">Avvio dell'eliminazione di pool</span><span class="sxs-lookup"><span data-stu-id="373d3-110">Pool delete start</span></span>](batch-pool-delete-start-event.md)
* [<span data-ttu-id="373d3-111">Completamento dell'eliminazione di pool</span><span class="sxs-lookup"><span data-stu-id="373d3-111">Pool delete complete</span></span>](batch-pool-delete-complete-event.md)
* [<span data-ttu-id="373d3-112">Avvio del ridimensionamento di pool</span><span class="sxs-lookup"><span data-stu-id="373d3-112">Pool resize start</span></span>](batch-pool-resize-start-event.md)
* [<span data-ttu-id="373d3-113">Completamento del ridimensionamento di pool</span><span class="sxs-lookup"><span data-stu-id="373d3-113">Pool resize complete</span></span>](batch-pool-resize-complete-event.md)
* [<span data-ttu-id="373d3-114">Avvio dell'attività</span><span class="sxs-lookup"><span data-stu-id="373d3-114">Task start</span></span>](batch-task-start-event.md)
* [<span data-ttu-id="373d3-115">Attività completata</span><span class="sxs-lookup"><span data-stu-id="373d3-115">Task complete</span></span>](batch-task-complete-event.md)
* [<span data-ttu-id="373d3-116">Errore dell'attività</span><span class="sxs-lookup"><span data-stu-id="373d3-116">Task fail</span></span>](batch-task-fail-event.md)