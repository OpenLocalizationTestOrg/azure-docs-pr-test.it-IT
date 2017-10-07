---
title: "aaaWhat è utilità di pianificazione di Azure? | Microsoft Docs"
description: Pianificazione di Azure consente toodeclaratively descrivono toorun azioni nel cloud hello. e quindi pianifica ed esegue tali azioni automaticamente.
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 52aa6ae1-4c3d-43fb-81b0-6792c84bcfae
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 062e25ae473510264dc0038198c05e7ac1e86210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-scheduler"></a><span data-ttu-id="65dd4-105">Che cos'è l'Utilità di pianificazione di Azure?</span><span class="sxs-lookup"><span data-stu-id="65dd4-105">What is Azure Scheduler?</span></span>
<span data-ttu-id="65dd4-106">Pianificazione di Azure consente toodeclaratively descrivono toorun azioni nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="65dd4-106">Azure Scheduler allows you toodeclaratively describe actions toorun in hello cloud.</span></span> <span data-ttu-id="65dd4-107">e quindi pianifica ed esegue tali azioni automaticamente.</span><span class="sxs-lookup"><span data-stu-id="65dd4-107">It then schedules and runs those actions automatically.</span></span>  <span data-ttu-id="65dd4-108">Utilità di pianificazione avviene usando [hello Azure portal](scheduler-get-started-portal.md), codice, [API REST](https://msdn.microsoft.com/library/mt629143.aspx), o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="65dd4-108">Scheduler does this by using [hello Azure portal](scheduler-get-started-portal.md), code, [REST API](https://msdn.microsoft.com/library/mt629143.aspx), or Azure PowerShell.</span></span>

<span data-ttu-id="65dd4-109">L’Utilità di pianificazione crea, gestisce e richiama il lavoro programmato.</span><span class="sxs-lookup"><span data-stu-id="65dd4-109">Scheduler creates, maintains, and invokes scheduled work.</span></span>  <span data-ttu-id="65dd4-110">L’Utilità di pianificazione non ospita carichi di lavoro, né esegue codice.</span><span class="sxs-lookup"><span data-stu-id="65dd4-110">Scheduler does not host any workloads or run any code.</span></span> <span data-ttu-id="65dd4-111">*Richiama* soltanto codice ospitato altrove, ad esempio in Azure, in locale o presso un altro provider.</span><span class="sxs-lookup"><span data-stu-id="65dd4-111">It only *invokes* code hosted elsewhere—in Azure, on-premises, or with another provider.</span></span> <span data-ttu-id="65dd4-112">Richiama tramite HTTP, HTTPS, una coda di archiviazione, una coda del bus di servizio o un argomento del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="65dd4-112">It invokes via HTTP, HTTPS, a storage queue, a service bus queue, or a service bus topic.</span></span>

<span data-ttu-id="65dd4-113">Le pianificazioni dell'utilità di pianificazione [processi](scheduler-concepts-terms.md), mantiene una cronologia dei risultati di esecuzione processo che uno è possibile esaminare e in modo deterministico e affidabile le pianificazioni dei carichi di lavoro toobe eseguire.</span><span class="sxs-lookup"><span data-stu-id="65dd4-113">Scheduler schedules [jobs](scheduler-concepts-terms.md), keeps a history of job execution results that one can review, and deterministically and reliably schedules workloads toobe run.</span></span> <span data-ttu-id="65dd4-114">Processi Web di Azure (parte della funzionalità di App Web hello in Azure App Service) e altre funzionalità di pianificazione di Azure è possibile utilizzare utilità di pianificazione in background hello.</span><span class="sxs-lookup"><span data-stu-id="65dd4-114">Azure WebJobs (part of hello Web Apps feature in Azure App Service) and other Azure scheduling capabilities use Scheduler in hello background.</span></span> <span data-ttu-id="65dd4-115">Hello [API REST dell'utilità di pianificazione](https://msdn.microsoft.com/library/mt629143.aspx) consente di gestiscono le comunicazioni hello per le azioni.</span><span class="sxs-lookup"><span data-stu-id="65dd4-115">hello [Scheduler REST API](https://msdn.microsoft.com/library/mt629143.aspx) helps manage hello communication for these actions.</span></span> <span data-ttu-id="65dd4-116">Quindi, l’Utilità di pianificazione supporta facilmente [pianificazioni complesse e operazioni ricorrenti avanzate](scheduler-advanced-complexity.md) .</span><span class="sxs-lookup"><span data-stu-id="65dd4-116">As such, Scheduler supports [complex schedules and advanced recurrence](scheduler-advanced-complexity.md) easily.</span></span>

<span data-ttu-id="65dd4-117">Esistono diversi scenari che si prestano toohello utilizzo dell'utilità di pianificazione.</span><span class="sxs-lookup"><span data-stu-id="65dd4-117">There are several scenarios that lend themselves toohello usage of Scheduler.</span></span> <span data-ttu-id="65dd4-118">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="65dd4-118">For example:</span></span>

* <span data-ttu-id="65dd4-119">*Azioni ricorrenti delle applicazioni*: raccolta periodica di dati da Twitter in un feed.</span><span class="sxs-lookup"><span data-stu-id="65dd4-119">*Recurring application actions:* Periodically gathering data from Twitter into a feed.</span></span>
* <span data-ttu-id="65dd4-120">*Manutenzione quotidiana*: eliminazione giornaliera dei registri, esecuzione di backup e altre attività di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="65dd4-120">*Daily maintenance:* Daily pruning of logs, performing backups, and other maintenance tasks.</span></span> <span data-ttu-id="65dd4-121">Ad esempio, un amministratore può scegliere tooback backup database hello alle ore 01:00</span><span class="sxs-lookup"><span data-stu-id="65dd4-121">For example, an administrator may choose tooback up hello database at 1:00 A.M.</span></span> <span data-ttu-id="65dd4-122">ogni giorno per hello nove mesi successivi.</span><span class="sxs-lookup"><span data-stu-id="65dd4-122">every day for hello next nine months.</span></span>

<span data-ttu-id="65dd4-123">Utilità di pianificazione consente toocreate, aggiornare, eliminare, visualizzare e gestire i processi e [le raccolte di processi](scheduler-concepts-terms.md) a livello di programmazione, utilizzando gli script e nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="65dd4-123">Scheduler allows you toocreate, update, delete, view, and manage jobs and [job collections](scheduler-concepts-terms.md) programmatically, by using scripts, and in hello portal.</span></span>

## <a name="see-also"></a><span data-ttu-id="65dd4-124">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="65dd4-124">See also</span></span>
 [<span data-ttu-id="65dd4-125">Concetti, terminologia e gerarchia di entità dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="65dd4-125">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="65dd4-126">Introduzione all'uso dell'utilità di pianificazione nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="65dd4-126">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="65dd4-127">Piani e fatturazione nell'utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="65dd4-127">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="65dd4-128">Come toobuild complesso pianifica e ricorrenza avanzata con utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="65dd4-128">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="65dd4-129">Informazioni di riferimento sull'API REST dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="65dd4-129">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="65dd4-130">Informazioni di riferimento sui cmdlet PowerShell dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="65dd4-130">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="65dd4-131">Livelli elevati di disponibilità e affidabilità dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="65dd4-131">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="65dd4-132">Limiti, valori predefiniti e codici di errore dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="65dd4-132">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="65dd4-133">Autenticazione in uscita dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="65dd4-133">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

