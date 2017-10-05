---
title: "Che cos'è l'Utilità di pianificazione di Azure? | Documentazione di Microsoft"
description: "L'Utilità di pianificazione di Azure consente di descrivere in modo dichiarativo le azioni da eseguire nel cloud e quindi pianifica ed esegue tali azioni automaticamente."
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
ms.openlocfilehash: a3bf1aacd6978499d7ef77cbcb451a06b857ac38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-azure-scheduler"></a><span data-ttu-id="e234e-105">Che cos'è l'Utilità di pianificazione di Azure?</span><span class="sxs-lookup"><span data-stu-id="e234e-105">What is Azure Scheduler?</span></span>
<span data-ttu-id="e234e-106">L'Utilità di pianificazione di Azure consente di descrivere in modo dichiarativo le azioni da eseguire nel cloud</span><span class="sxs-lookup"><span data-stu-id="e234e-106">Azure Scheduler allows you to declaratively describe actions to run in the cloud.</span></span> <span data-ttu-id="e234e-107">e quindi pianifica ed esegue tali azioni automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e234e-107">It then schedules and runs those actions automatically.</span></span>  <span data-ttu-id="e234e-108">A tale scopo, l'utilità di pianificazione di Azure utilizza il [portale di Azure](scheduler-get-started-portal.md), il codice, l'[API REST](https://msdn.microsoft.com/library/mt629143.aspx) o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e234e-108">Scheduler does this by using [the Azure portal](scheduler-get-started-portal.md), code, [REST API](https://msdn.microsoft.com/library/mt629143.aspx), or Azure PowerShell.</span></span>

<span data-ttu-id="e234e-109">L’Utilità di pianificazione crea, gestisce e richiama il lavoro programmato.</span><span class="sxs-lookup"><span data-stu-id="e234e-109">Scheduler creates, maintains, and invokes scheduled work.</span></span>  <span data-ttu-id="e234e-110">L’Utilità di pianificazione non ospita carichi di lavoro, né esegue codice.</span><span class="sxs-lookup"><span data-stu-id="e234e-110">Scheduler does not host any workloads or run any code.</span></span> <span data-ttu-id="e234e-111">*Richiama* soltanto codice ospitato altrove, ad esempio in Azure, in locale o presso un altro provider.</span><span class="sxs-lookup"><span data-stu-id="e234e-111">It only *invokes* code hosted elsewhere—in Azure, on-premises, or with another provider.</span></span> <span data-ttu-id="e234e-112">Richiama tramite HTTP, HTTPS, una coda di archiviazione, una coda del bus di servizio o un argomento del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="e234e-112">It invokes via HTTP, HTTPS, a storage queue, a service bus queue, or a service bus topic.</span></span>

<span data-ttu-id="e234e-113">L'Utilità di pianificazione pianifica i [processi](scheduler-concepts-terms.md), mantiene una cronologia dei risultati dell'esecuzione dei processi che è possibile esaminare e pianifica in modo deterministico e attendibile i carichi di lavoro da eseguire.</span><span class="sxs-lookup"><span data-stu-id="e234e-113">Scheduler schedules [jobs](scheduler-concepts-terms.md), keeps a history of job execution results that one can review, and deterministically and reliably schedules workloads to be run.</span></span> <span data-ttu-id="e234e-114">Azure WebJobs (parte della funzionalità App Web in Servizio app di Azure) e altre funzionalità di programmazione di Azure utilizzano l’Utilità di pianificazione in background.</span><span class="sxs-lookup"><span data-stu-id="e234e-114">Azure WebJobs (part of the Web Apps feature in Azure App Service) and other Azure scheduling capabilities use Scheduler in the background.</span></span> <span data-ttu-id="e234e-115">L' [API REST dell'Utilità di pianificazione](https://msdn.microsoft.com/library/mt629143.aspx) consente di gestire le comunicazioni per queste azioni.</span><span class="sxs-lookup"><span data-stu-id="e234e-115">The [Scheduler REST API](https://msdn.microsoft.com/library/mt629143.aspx) helps manage the communication for these actions.</span></span> <span data-ttu-id="e234e-116">Quindi, l’Utilità di pianificazione supporta facilmente [pianificazioni complesse e operazioni ricorrenti avanzate](scheduler-advanced-complexity.md) .</span><span class="sxs-lookup"><span data-stu-id="e234e-116">As such, Scheduler supports [complex schedules and advanced recurrence](scheduler-advanced-complexity.md) easily.</span></span>

<span data-ttu-id="e234e-117">L'Utilità di pianificazione può essere usata in diversi scenari.</span><span class="sxs-lookup"><span data-stu-id="e234e-117">There are several scenarios that lend themselves to the usage of Scheduler.</span></span> <span data-ttu-id="e234e-118">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e234e-118">For example:</span></span>

* <span data-ttu-id="e234e-119">*Azioni ricorrenti delle applicazioni*: raccolta periodica di dati da Twitter in un feed.</span><span class="sxs-lookup"><span data-stu-id="e234e-119">*Recurring application actions:* Periodically gathering data from Twitter into a feed.</span></span>
* <span data-ttu-id="e234e-120">*Manutenzione quotidiana*: eliminazione giornaliera dei registri, esecuzione di backup e altre attività di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="e234e-120">*Daily maintenance:* Daily pruning of logs, performing backups, and other maintenance tasks.</span></span> <span data-ttu-id="e234e-121">Ad esempio, un amministratore può scegliere di eseguire il backup del database alle ore 01:00</span><span class="sxs-lookup"><span data-stu-id="e234e-121">For example, an administrator may choose to back up the database at 1:00 A.M.</span></span> <span data-ttu-id="e234e-122">ogni giorno per i nove mesi successivi.</span><span class="sxs-lookup"><span data-stu-id="e234e-122">every day for the next nine months.</span></span>

<span data-ttu-id="e234e-123">Con l'Utilità di pianificazione è possibile creare, aggiornare, eliminare, visualizzare e gestire processi e [raccolte di processi](scheduler-concepts-terms.md) a livello di codice, tramite script e nel portale.</span><span class="sxs-lookup"><span data-stu-id="e234e-123">Scheduler allows you to create, update, delete, view, and manage jobs and [job collections](scheduler-concepts-terms.md) programmatically, by using scripts, and in the portal.</span></span>

## <a name="see-also"></a><span data-ttu-id="e234e-124">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="e234e-124">See also</span></span>
 [<span data-ttu-id="e234e-125">Concetti, terminologia e gerarchia di entità dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e234e-125">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="e234e-126">Introduzione all'uso dell'Utilità di pianificazione di Azure nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e234e-126">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="e234e-127">Piani e fatturazione nell'utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e234e-127">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="e234e-128">Come creare pianificazioni complesse e operazioni ricorrenti avanzate con l'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e234e-128">How to build complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="e234e-129">Informazioni di riferimento sull'API REST dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e234e-129">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="e234e-130">Informazioni di riferimento sui cmdlet PowerShell dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e234e-130">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="e234e-131">Livelli elevati di disponibilità e affidabilità dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e234e-131">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="e234e-132">Limiti, valori predefiniti e codici di errore dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e234e-132">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="e234e-133">Autenticazione in uscita dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e234e-133">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

