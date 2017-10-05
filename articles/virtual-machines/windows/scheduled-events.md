---
title: Eventi pianificati per macchine virtuali Windows in Azure | Microsoft Docs
description: Eventi pianificati usando il servizio metadati di Azure per le macchine virtuali Windows.
services: virtual-machines-windows, virtual-machines-linux, cloud-services
documentationcenter: 
author: zivraf
manager: timlt
editor: 
tags: 
ms.assetid: 28d8e1f2-8e61-4fbe-bfe8-80a68443baba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: zivr
ms.openlocfilehash: 7198fa8d1a512d10ca7022078aa2ea7bde3a4c02
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-metadata-service-scheduled-events-preview-for-windows-vms"></a><span data-ttu-id="f7d97-103">Servizio metadati di Azure: eventi pianificati (anteprima) per VM Windows</span><span class="sxs-lookup"><span data-stu-id="f7d97-103">Azure Metadata Service: Scheduled Events (Preview) for Windows VMs</span></span>

> [!NOTE] 
> <span data-ttu-id="f7d97-104">Le anteprime vengono rese disponibili per l'utente a condizione che si accettino le condizioni d'uso.</span><span class="sxs-lookup"><span data-stu-id="f7d97-104">Previews are made available to you on the condition that you agree to the terms of use.</span></span> <span data-ttu-id="f7d97-105">Per altre informazioni, vedere [Condizioni Supplementari di Microsoft Azure le Anteprime di Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span><span class="sxs-lookup"><span data-stu-id="f7d97-105">For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span></span>
>

<span data-ttu-id="f7d97-106">Eventi pianificati è uno dei servizi secondari del Servizio metadati di Azure.</span><span class="sxs-lookup"><span data-stu-id="f7d97-106">Scheduled Events is one of the subservices under the Azure Metadata Service.</span></span> <span data-ttu-id="f7d97-107">Presenta informazioni sugli eventi imminenti, ad esempio i riavvii, in modo che l'applicazione possa prepararsi di conseguenza e limitare le interruzioni.</span><span class="sxs-lookup"><span data-stu-id="f7d97-107">It is responsible for surfacing information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span> <span data-ttu-id="f7d97-108">Il servizio è disponibile per tutti i tipi di macchine virtuali di Azure, inclusi PaaS e IaaS.</span><span class="sxs-lookup"><span data-stu-id="f7d97-108">It is available for all Azure Virtual Machine types including PaaS and IaaS.</span></span> <span data-ttu-id="f7d97-109">Il servizio dà alla macchina virtuale il tempo sufficiente per eseguire attività preventive e ridurre al minimo l'effetto di un evento.</span><span class="sxs-lookup"><span data-stu-id="f7d97-109">Scheduled Events gives your Virtual Machine time to perform preventive tasks to minimize the effect of an event.</span></span> 

<span data-ttu-id="f7d97-110">Eventi pianificati è disponibile per VM sia Linux che Windows.</span><span class="sxs-lookup"><span data-stu-id="f7d97-110">Scheduled Events is available for both Linux and Windows VMs.</span></span> <span data-ttu-id="f7d97-111">Per informazioni su Eventi pianificati in Linux, vedere [Eventi pianificati per macchine virtuali Linux](../windows/scheduled-events.md).</span><span class="sxs-lookup"><span data-stu-id="f7d97-111">For information about Scheduled Events on Linux, see [Scheduled Events for Linux VMs](../windows/scheduled-events.md).</span></span>

## <a name="why-scheduled-events"></a><span data-ttu-id="f7d97-112">Perché usare gli eventi pianificati</span><span class="sxs-lookup"><span data-stu-id="f7d97-112">Why Scheduled Events?</span></span>

<span data-ttu-id="f7d97-113">Con Eventi pianificati, è possibile eseguire la procedura per ridurre l'impatto della manutenzione avviata dalla piattaforma o delle azioni avviate dall'utente nel servizio.</span><span class="sxs-lookup"><span data-stu-id="f7d97-113">With Scheduled Events, you can take steps to limit the impact of platform-intiated maintenance or user-initiated actions on your service.</span></span> 

<span data-ttu-id="f7d97-114">I carichi di lavoro a più istanze, che usano tecniche di replica per mantenere lo stato, potrebbero essere soggetti a interruzioni tra più istanze.</span><span class="sxs-lookup"><span data-stu-id="f7d97-114">Multi-instance workloads, which use replication techniques to maintain state, may be vulnerable to outages happening across multiple instances.</span></span> <span data-ttu-id="f7d97-115">Tali interruzioni potrebbero comportare attività costose, ad esempio, la ricompilazione degli indici, o addirittura una perdita di replica.</span><span class="sxs-lookup"><span data-stu-id="f7d97-115">Such outages may result in expensive tasks (for example, rebuilding indexes) or even a replica loss.</span></span> 

<span data-ttu-id="f7d97-116">In molti altri casi, la disponibilità generale del servizio può essere migliorata eseguendo la normale sequenza di arresto, ad esempio il completamento o l'annullamento della transazioni in corso, la riassegnazione delle attività ad altre macchine virtuali nel cluster, ovvero il failover manuale, o la rimozione della macchina virtuale da un pool di bilanciamento del carico della rete.</span><span class="sxs-lookup"><span data-stu-id="f7d97-116">In many other cases, the overall service availability may be improved by performing a graceful shutdown sequence such as completing (or canceling) in-flight transactions, reassigning tasks to other VMs in the cluster (manual failover), or removing the Virtual Machine from a network load balancer pool.</span></span> 

<span data-ttu-id="f7d97-117">Ci sono casi in cui è possibile migliorare l'utilità delle applicazioni ospitate nel cloud avvisando un amministratore della presenza di un evento imminente o registrando tale evento.</span><span class="sxs-lookup"><span data-stu-id="f7d97-117">There are cases where notifying an administrator about an upcoming event or logging such an event help improving the serviceability of applications hosted in the cloud.</span></span>

<span data-ttu-id="f7d97-118">Il Servizio metadati di Azure presenta gli eventi pianificati nei seguenti casi d'uso:</span><span class="sxs-lookup"><span data-stu-id="f7d97-118">Azure Metadata Service surfaces Scheduled Events in the following use cases:</span></span>
-   <span data-ttu-id="f7d97-119">Manutenzione avviata dalla piattaforma, ad esempio implementazione del sistema operativo host</span><span class="sxs-lookup"><span data-stu-id="f7d97-119">Platform initiated maintenance (for example, Host OS rollout)</span></span>
-   <span data-ttu-id="f7d97-120">Chiamate avviate dall'utente, ad esempio riavvii iniziati dall'utente o ridistribuzione di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="f7d97-120">User-initiated calls (for example, user restarts or redeploys a VM)</span></span>


## <a name="the-basics"></a><span data-ttu-id="f7d97-121">Nozioni di base</span><span class="sxs-lookup"><span data-stu-id="f7d97-121">The basics</span></span>  

<span data-ttu-id="f7d97-122">Il Servizio metadati di Azure presenta informazioni sulle macchine virtuali in esecuzione usando un endpoint REST accessibile dall'interno della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f7d97-122">Azure Metadata service exposes information about running Virtual Machines using a REST Endpoint accessible from within the VM.</span></span> <span data-ttu-id="f7d97-123">Le informazioni sono disponibili tramite un indirizzo IP non instradabile, in modo da non essere esposte al di fuori della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f7d97-123">The information is available via a non-routable IP so that it is not exposed outside the VM.</span></span>

### <a name="scope"></a><span data-ttu-id="f7d97-124">Scope</span><span class="sxs-lookup"><span data-stu-id="f7d97-124">Scope</span></span>
<span data-ttu-id="f7d97-125">Gli eventi pianificati vengono presentati per tutte le macchine virtuali in un servizio cloud o per tutte le macchine virtuali in un set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="f7d97-125">Scheduled events are surfaced to all Virtual Machines in a cloud service or to all Virtual Machines in an Availability Set.</span></span> <span data-ttu-id="f7d97-126">Pertanto, è consigliabile controllare il campo `Resources` nell'evento per individuare le macchine virtuali che ne saranno interessate.</span><span class="sxs-lookup"><span data-stu-id="f7d97-126">As a result, you should check the `Resources` field in the event to identify which VMs are going to be impacted.</span></span> 

### <a name="discovering-the-endpoint"></a><span data-ttu-id="f7d97-127">Individuazione dell'endpoint</span><span class="sxs-lookup"><span data-stu-id="f7d97-127">Discovering the endpoint</span></span>
<span data-ttu-id="f7d97-128">Nel caso in cui venga creata una macchina virtuale in una rete virtuale, il servizio di metadati è disponibile all'indirizzo IP statico non instradabile, `169.254.169.254`.</span><span class="sxs-lookup"><span data-stu-id="f7d97-128">In the case where a Virtual Machine is created within a Virtual Network (VNet), the metadata service is available from a static non-routable IP, `169.254.169.254`.</span></span>
<span data-ttu-id="f7d97-129">Se la macchina virtuale non viene creata all'interno di una rete virtuale, i casi predefiniti per i servizi cloud e le macchine virtuali classiche, sarà necessaria una logica aggiuntiva per individuare l'endpoint da usare.</span><span class="sxs-lookup"><span data-stu-id="f7d97-129">If the Virtual Machine is not created within a Virtual Network, the default cases for cloud services and classic VMs, additional logic is required to discover the endpoint to use.</span></span> <span data-ttu-id="f7d97-130">Fare riferimento a questo esempio per informazioni su come [individuare l'endpoint dell'host](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span><span class="sxs-lookup"><span data-stu-id="f7d97-130">Refer to this sample to learn how to [discover the host endpoint](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span></span>

### <a name="versioning"></a><span data-ttu-id="f7d97-131">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="f7d97-131">Versioning</span></span> 
<span data-ttu-id="f7d97-132">Il Servizio metadati dell'istanza è con versione.</span><span class="sxs-lookup"><span data-stu-id="f7d97-132">The Instance Metadata Service is versioned.</span></span> <span data-ttu-id="f7d97-133">Le versioni sono obbligatorie e la versione corrente è `2017-03-01`.</span><span class="sxs-lookup"><span data-stu-id="f7d97-133">Versions are mandatory and the current version is `2017-03-01`.</span></span>

> [!NOTE] 
> <span data-ttu-id="f7d97-134">Le versioni precedenti di anteprima di eventi pianificati {ultima} sono supportate come versione dell'API.</span><span class="sxs-lookup"><span data-stu-id="f7d97-134">Previous preview releases of scheduled events supported {latest} as the api-version.</span></span> <span data-ttu-id="f7d97-135">Questo formato non è più supportato e verrà rimosso in futuro.</span><span class="sxs-lookup"><span data-stu-id="f7d97-135">This format is no longer supported and will be deprecated in the future.</span></span>

### <a name="using-headers"></a><span data-ttu-id="f7d97-136">Uso delle intestazioni</span><span class="sxs-lookup"><span data-stu-id="f7d97-136">Using headers</span></span>
<span data-ttu-id="f7d97-137">Quando si eseguono query sul Servizio metadati, è necessario specificare l'intestazione `Metadata: true` per garantire che la richiesta non sia stata reindirizzata accidentalmente.</span><span class="sxs-lookup"><span data-stu-id="f7d97-137">When you query the Metadata Service, you must provide the header `Metadata: true` to ensure the request was not unintentionally redirected.</span></span>

### <a name="enabling-scheduled-events"></a><span data-ttu-id="f7d97-138">Attivazione degli eventi pianificati</span><span class="sxs-lookup"><span data-stu-id="f7d97-138">Enabling Scheduled Events</span></span>
<span data-ttu-id="f7d97-139">La prima volta che si emette una richiesta per gli eventi pianificati, Azure abilita in modo implicito la funzionalità nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f7d97-139">The first time you make a request for scheduled events, Azure implicitly enables the feature on your Virtual Machine.</span></span> <span data-ttu-id="f7d97-140">Di conseguenza la prima chiamata potrebbe ricevere una risposta con un ritardo massimo di due minuti.</span><span class="sxs-lookup"><span data-stu-id="f7d97-140">As a result, you should expect a delayed response in your first call of up to two minutes.</span></span>

### <a name="user-initiated-maintenance"></a><span data-ttu-id="f7d97-141">Manutenzione avviata dall'utente</span><span class="sxs-lookup"><span data-stu-id="f7d97-141">User initiated maintenance</span></span>
<span data-ttu-id="f7d97-142">La manutenzione delle macchine virtuali avviata dall'utente tramite il portale, l'API o l'interfaccia della riga di comando di Azure oppure tramite PowerShell restituisce un evento pianificato.</span><span class="sxs-lookup"><span data-stu-id="f7d97-142">User initiated virtual machine maintenance via the Azure portal, API, CLI, or PowerShell results in a scheduled event.</span></span> <span data-ttu-id="f7d97-143">In questo modo è possibile testare la logica di preparazione della manutenzione dell'applicazione e permettere all'applicazione di prepararsi per la manutenzione avviata dall'utente.</span><span class="sxs-lookup"><span data-stu-id="f7d97-143">This allows you to test the maintenance preparation logic in your application and allows your application to prepare for user initiated maintenance.</span></span>

<span data-ttu-id="f7d97-144">Il riavvio di una macchina virtuale pianifica un evento di tipo `Reboot`.</span><span class="sxs-lookup"><span data-stu-id="f7d97-144">Restarting a virtual machine schedules an event with type `Reboot`.</span></span> <span data-ttu-id="f7d97-145">La ridistribuzione di una macchina virtuale pianifica un evento di tipo `Redeploy`.</span><span class="sxs-lookup"><span data-stu-id="f7d97-145">Redeploying a virtual machine schedules an event with type `Redeploy`.</span></span>

> [!NOTE] 
> <span data-ttu-id="f7d97-146">Attualmente è possibile pianificare un massimo di 10 operazioni di manutenzione avviata dall'utente.</span><span class="sxs-lookup"><span data-stu-id="f7d97-146">Currently a maximum of 10 user initiated maintenance operations can be simultaneously scheduled.</span></span> <span data-ttu-id="f7d97-147">Questo limite viene aumentato prima della disponibilità generale di eventi pianificati.</span><span class="sxs-lookup"><span data-stu-id="f7d97-147">This limit will be relaxed before Scheduled Events general availability.</span></span>

> [!NOTE] 
> <span data-ttu-id="f7d97-148">Attualmente la manutenzione avviata dall'utente che dà luogo a eventi pianificati non è configurabile.</span><span class="sxs-lookup"><span data-stu-id="f7d97-148">Currently user initiated maintenance resulting in Scheduled Events is not configurable.</span></span> <span data-ttu-id="f7d97-149">Questa funzionalità è pianificata per una versione successiva.</span><span class="sxs-lookup"><span data-stu-id="f7d97-149">Configurability is planned for a future release.</span></span>

## <a name="using-the-api"></a><span data-ttu-id="f7d97-150">Uso dell'API</span><span class="sxs-lookup"><span data-stu-id="f7d97-150">Using the API</span></span>

### <a name="query-for-events"></a><span data-ttu-id="f7d97-151">Query per gli eventi</span><span class="sxs-lookup"><span data-stu-id="f7d97-151">Query for events</span></span>
<span data-ttu-id="f7d97-152">È possibile eseguire query per gli eventi pianificati semplicemente eseguendo la chiamata seguente:</span><span class="sxs-lookup"><span data-stu-id="f7d97-152">You can query for Scheduled Events simply by making the following call:</span></span>

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

<span data-ttu-id="f7d97-153">Una risposta contiene una serie di eventi pianificati.</span><span class="sxs-lookup"><span data-stu-id="f7d97-153">A response contains an array of scheduled events.</span></span> <span data-ttu-id="f7d97-154">Una serie vuota indica che al momento non sono presenti eventi pianificati.</span><span class="sxs-lookup"><span data-stu-id="f7d97-154">An empty array means that there are currently no events scheduled.</span></span>
<span data-ttu-id="f7d97-155">Nel caso in cui siano presenti eventi pianificati, la risposta contiene una serie di eventi:</span><span class="sxs-lookup"><span data-stu-id="f7d97-155">In the case where there are scheduled events, the response contains an array of events:</span></span> 
```
{
    "DocumentIncarnation": {IncarnationID},
    "Events": [
        {
            "EventId": {eventID},
            "EventType": "Reboot" | "Redeploy" | "Freeze",
            "ResourceType": "VirtualMachine",
            "Resources": [{resourceName}],
            "EventStatus": "Scheduled" | "Started",
            "NotBefore": {timeInUTC},              
        }
    ]
}
```

### <a name="event-properties"></a><span data-ttu-id="f7d97-156">Proprietà degli eventi</span><span class="sxs-lookup"><span data-stu-id="f7d97-156">Event properties</span></span>
|<span data-ttu-id="f7d97-157">Proprietà</span><span class="sxs-lookup"><span data-stu-id="f7d97-157">Property</span></span>  |  <span data-ttu-id="f7d97-158">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7d97-158">Description</span></span> |
| - | - |
| <span data-ttu-id="f7d97-159">EventId</span><span class="sxs-lookup"><span data-stu-id="f7d97-159">EventId</span></span> | <span data-ttu-id="f7d97-160">Identificatore globalmente univoco per l'evento.</span><span class="sxs-lookup"><span data-stu-id="f7d97-160">Globally unique identifier for this event.</span></span> <br><br> <span data-ttu-id="f7d97-161">Esempio:</span><span class="sxs-lookup"><span data-stu-id="f7d97-161">Example:</span></span> <br><ul><li><span data-ttu-id="f7d97-162">602d9444-d2cd-49c7-8624-8643e7171297</span><span class="sxs-lookup"><span data-stu-id="f7d97-162">602d9444-d2cd-49c7-8624-8643e7171297</span></span>  |
| <span data-ttu-id="f7d97-163">EventType</span><span class="sxs-lookup"><span data-stu-id="f7d97-163">EventType</span></span> | <span data-ttu-id="f7d97-164">Impatto che l'evento causa.</span><span class="sxs-lookup"><span data-stu-id="f7d97-164">Impact this event causes.</span></span> <br><br> <span data-ttu-id="f7d97-165">Valori:</span><span class="sxs-lookup"><span data-stu-id="f7d97-165">Values:</span></span> <br><ul><li> <span data-ttu-id="f7d97-166">`Freeze`: è pianificata una sospensione della macchina virtuale per alcuni secondi.</span><span class="sxs-lookup"><span data-stu-id="f7d97-166">`Freeze`: The Virtual Machine is scheduled to pause for few seconds.</span></span> <span data-ttu-id="f7d97-167">La CPU viene sospesa, ma la memoria, i file aperti o le connessioni di rete non subiranno conseguenze.</span><span class="sxs-lookup"><span data-stu-id="f7d97-167">The CPU is suspended, but there is no impact on memory, open files, or network connections.</span></span> <li><span data-ttu-id="f7d97-168">`Reboot`: è pianificato un riavvio della macchina virtuale. La memoria non permanente andrà persa.</span><span class="sxs-lookup"><span data-stu-id="f7d97-168">`Reboot`: The Virtual Machine is scheduled for reboot (non-persistent memory is lost).</span></span> <li><span data-ttu-id="f7d97-169">`Redeploy`: è pianificato uno spostamento della macchina virtuale in un altro nodo. I dischi temporanei andranno persi.</span><span class="sxs-lookup"><span data-stu-id="f7d97-169">`Redeploy`: The Virtual Machine is scheduled to move to another node (ephemeral disks are lost).</span></span> |
| <span data-ttu-id="f7d97-170">ResourceType</span><span class="sxs-lookup"><span data-stu-id="f7d97-170">ResourceType</span></span> | <span data-ttu-id="f7d97-171">Tipo di risorsa su cui l'evento influisce.</span><span class="sxs-lookup"><span data-stu-id="f7d97-171">Type of resource this event impacts.</span></span> <br><br> <span data-ttu-id="f7d97-172">Valori:</span><span class="sxs-lookup"><span data-stu-id="f7d97-172">Values:</span></span> <ul><li>`VirtualMachine`|
| <span data-ttu-id="f7d97-173">Risorse</span><span class="sxs-lookup"><span data-stu-id="f7d97-173">Resources</span></span>| <span data-ttu-id="f7d97-174">Elenco delle risorse su cui l'evento influisce.</span><span class="sxs-lookup"><span data-stu-id="f7d97-174">List of resources this event impacts.</span></span> <span data-ttu-id="f7d97-175">Contiene sicuramente i computer per al massimo un [Dominio di aggiornamento](manage-availability.md), ma non può contenere tutti i computer nel dominio di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="f7d97-175">This is guaranteed to contain machines from at most one [Update Domain](manage-availability.md), but may not contain all machines in the UD.</span></span> <br><br> <span data-ttu-id="f7d97-176">Esempio:</span><span class="sxs-lookup"><span data-stu-id="f7d97-176">Example:</span></span> <br><ul><li> <span data-ttu-id="f7d97-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span><span class="sxs-lookup"><span data-stu-id="f7d97-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span></span> |
| <span data-ttu-id="f7d97-178">Event Status</span><span class="sxs-lookup"><span data-stu-id="f7d97-178">Event Status</span></span> | <span data-ttu-id="f7d97-179">Stato dell'evento.</span><span class="sxs-lookup"><span data-stu-id="f7d97-179">Status of this event.</span></span> <br><br> <span data-ttu-id="f7d97-180">Valori:</span><span class="sxs-lookup"><span data-stu-id="f7d97-180">Values:</span></span> <ul><li><span data-ttu-id="f7d97-181">`Scheduled`: l'avvio dell'evento è pianificato in seguito al tempo specificato nella proprietà `NotBefore`.</span><span class="sxs-lookup"><span data-stu-id="f7d97-181">`Scheduled`: This event is scheduled to start after the time specified in the `NotBefore` property.</span></span><li><span data-ttu-id="f7d97-182">`Started`: l'evento si è avviato.</span><span class="sxs-lookup"><span data-stu-id="f7d97-182">`Started`: This event has started.</span></span></ul> <span data-ttu-id="f7d97-183">Non viene indicato `Completed` o uno stato simile; l'evento non verrà più restituito al suo completamento.</span><span class="sxs-lookup"><span data-stu-id="f7d97-183">No `Completed` or similar status is ever provided; the event will no longer be returned when the event is completed.</span></span>
| <span data-ttu-id="f7d97-184">NotBefore</span><span class="sxs-lookup"><span data-stu-id="f7d97-184">NotBefore</span></span>| <span data-ttu-id="f7d97-185">Tempo dopo il quale l'evento può essere avviato.</span><span class="sxs-lookup"><span data-stu-id="f7d97-185">Time after which this event may start.</span></span> <br><br> <span data-ttu-id="f7d97-186">Esempio:</span><span class="sxs-lookup"><span data-stu-id="f7d97-186">Example:</span></span> <br><ul><li> <span data-ttu-id="f7d97-187">2016-09-19T18:29:47Z</span><span class="sxs-lookup"><span data-stu-id="f7d97-187">2016-09-19T18:29:47Z</span></span>  |

### <a name="event-scheduling"></a><span data-ttu-id="f7d97-188">Pianificazione degli eventi</span><span class="sxs-lookup"><span data-stu-id="f7d97-188">Event scheduling</span></span>
<span data-ttu-id="f7d97-189">Ogni evento è pianificato con un ritardo minimo che dipende dal tipo di evento.</span><span class="sxs-lookup"><span data-stu-id="f7d97-189">Each event is scheduled a minimum amount of time in the future based on event type.</span></span> <span data-ttu-id="f7d97-190">Questo tempo si riflette in una proprietà `NotBefore` dell'evento.</span><span class="sxs-lookup"><span data-stu-id="f7d97-190">This time is reflected in an event's `NotBefore` property.</span></span> 

|<span data-ttu-id="f7d97-191">EventType</span><span class="sxs-lookup"><span data-stu-id="f7d97-191">EventType</span></span>  | <span data-ttu-id="f7d97-192">Minimum Notice</span><span class="sxs-lookup"><span data-stu-id="f7d97-192">Minimum Notice</span></span> |
| - | - |
| <span data-ttu-id="f7d97-193">Freeze</span><span class="sxs-lookup"><span data-stu-id="f7d97-193">Freeze</span></span>| <span data-ttu-id="f7d97-194">15 minuti</span><span class="sxs-lookup"><span data-stu-id="f7d97-194">15 minutes</span></span> |
| <span data-ttu-id="f7d97-195">Reboot</span><span class="sxs-lookup"><span data-stu-id="f7d97-195">Reboot</span></span> | <span data-ttu-id="f7d97-196">15 minuti</span><span class="sxs-lookup"><span data-stu-id="f7d97-196">15 minutes</span></span> |
| <span data-ttu-id="f7d97-197">Ripetere la distribuzione</span><span class="sxs-lookup"><span data-stu-id="f7d97-197">Redeploy</span></span> | <span data-ttu-id="f7d97-198">10 minuti</span><span class="sxs-lookup"><span data-stu-id="f7d97-198">10 minutes</span></span> |

### <a name="starting-an-event"></a><span data-ttu-id="f7d97-199">Avvio di un evento</span><span class="sxs-lookup"><span data-stu-id="f7d97-199">Starting an event</span></span> 

<span data-ttu-id="f7d97-200">Dopo aver appreso informazioni su un evento imminente e aver completato la logica per l'arresto normale, è possibile approvare l'evento in sospeso facendo una chiamata `POST` al servizio metadati con `EventId`.</span><span class="sxs-lookup"><span data-stu-id="f7d97-200">Once you have learned of an upcoming event and completed your logic for graceful shutdown, you can approve the outstanding event by making a `POST` call to the metadata service with the `EventId`.</span></span> <span data-ttu-id="f7d97-201">Ciò indica ad Azure che si può ridurre il tempo di notifica minimo, quando possibile.</span><span class="sxs-lookup"><span data-stu-id="f7d97-201">This indicates to Azure that it can shorten the minimum notification time (when possible).</span></span> 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> <span data-ttu-id="f7d97-202">Il riconoscimento di un evento consente all'evento di procedere per tutti gli elementi `Resources` nell'evento, non solo per la macchina virtuale che riconosce l'evento.</span><span class="sxs-lookup"><span data-stu-id="f7d97-202">Acknowledging an event allows the event to proceed for all `Resources` in the event, not just the virtual machine that acknowledges the event.</span></span> <span data-ttu-id="f7d97-203">Pertanto è possibile scegliere un coordinatore che si occupi del riconoscimento, che potrebbe essere semplicemente il primo nel campo `Resources`.</span><span class="sxs-lookup"><span data-stu-id="f7d97-203">You may therefore choose to elect a leader to coordinate the acknowledgement, which may be as simple as the first machine in the `Resources` field.</span></span>


## <a name="powershell-sample"></a><span data-ttu-id="f7d97-204">Esempio PowerShell</span><span class="sxs-lookup"><span data-stu-id="f7d97-204">PowerShell sample</span></span> 

<span data-ttu-id="f7d97-205">L'esempio seguente esegue query sul servizio metadati per gli eventi pianificati e quindi approva gli eventi in sospeso.</span><span class="sxs-lookup"><span data-stu-id="f7d97-205">The following sample queries the metadata service for scheduled events and approves each outstanding event.</span></span>

```PowerShell
# How to get scheduled events 
function GetScheduledEvents($uri)
{
    $scheduledEvents = Invoke-RestMethod -Headers @{"Metadata"="true"} -URI $uri -Method get
    $json = ConvertTo-Json $scheduledEvents
    Write-Host "Received following events: `n" $json
    return $scheduledEvents
}

# How to approve a scheduled event
function ApproveScheduledEvent($eventId, $docIncarnation, $uri)
{    
    # Create the Scheduled Events Approval Document
    $startRequests = [array]@{"EventId" = $eventId}
    $scheduledEventsApproval = @{"StartRequests" = $startRequests; "DocumentIncarnation" = $docIncarnation} 
    
    # Convert to JSON string
    $approvalString = ConvertTo-Json $scheduledEventsApproval

    Write-Host "Approving with the following: `n" $approvalString

    # Post approval string to scheduled events endpoint
    Invoke-RestMethod -Uri $uri -Headers @{"Metadata"="true"} -Method POST -Body $approvalString
}

function HandleScheduledEvents($scheduledEvents)
{
    # Add logic for handling events here
}

######### Sample Scheduled Events Interaction #########

# Set up the scheduled events URI for a VNET-enabled VM
$localHostIP = "169.254.169.254"
$scheduledEventURI = 'http://{0}/metadata/scheduledevents?api-version=2017-03-01' -f $localHostIP 

# Get events
$scheduledEvents = GetScheduledEvents $scheduledEventURI

# Handle events however is best for your service
HandleScheduledEvents $scheduledEvents

# Approve events when ready (optional)
foreach($event in $scheduledEvents.Events)
{
    Write-Host "Current Event: `n" $event
    $entry = Read-Host "`nApprove event? Y/N"
    if($entry -eq "Y" -or $entry -eq "y")
    {
        ApproveScheduledEvent $event.EventId $scheduledEvents.DocumentIncarnation $scheduledEventURI 
    }
}
``` 


## <a name="c-sample"></a><span data-ttu-id="f7d97-206">Esempio C\#</span><span class="sxs-lookup"><span data-stu-id="f7d97-206">C\# sample</span></span> 

<span data-ttu-id="f7d97-207">L'esempio seguente si riferisce a un client semplice che comunica con il Servizio metadati.</span><span class="sxs-lookup"><span data-stu-id="f7d97-207">The following sample is of a simple client that communicates with the metadata service.</span></span>

```csharp
public class ScheduledEventsClient
{
    private readonly string scheduledEventsEndpoint;
    private readonly string defaultIpAddress = "169.254.169.254"; 

    // Set up the scheduled events URI for a VNET-enabled VM
    public ScheduledEventsClient()
    {
        scheduledEventsEndpoint = string.Format("http://{0}/metadata/scheduledevents?api-version=2017-03-01", defaultIpAddress);
    }

    // Get events
    public string GetScheduledEvents()
    {
        Uri cloudControlUri = new Uri(scheduledEventsEndpoint);
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Metadata", "true");
            return webClient.DownloadString(cloudControlUri);
        }   
    }

    // Approve events
    public void ApproveScheduledEvents(string jsonPost)
    {
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Content-Type", "application/json");
            webClient.UploadString(scheduledEventsEndpoint, jsonPost);
        }
    }
}
```

<span data-ttu-id="f7d97-208">È possibile rappresentare gli eventi pianificati usando le seguenti strutture di dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="f7d97-208">Scheduled Events can be represented using the following data structures:</span></span>

```csharp
public class ScheduledEventsDocument
{
    public string DocumentIncarnation;
    public List<CloudControlEvent> Events { get; set; }
}

public class CloudControlEvent
{
    public string EventId { get; set; }
    public string EventStatus { get; set; }
    public string EventType { get; set; }
    public string ResourceType { get; set; }
    public List<string> Resources { get; set; }
    public DateTime? NotBefore { get; set; }
}

public class ScheduledEventsApproval
{
    public string DocumentIncarnation;
    public List<StartRequest> StartRequests = new List<StartRequest>();
}

public class StartRequest
{
    [JsonProperty("EventId")]
    private string eventId;

    public StartRequest(string eventId)
    {
        this.eventId = eventId;
    }
}
```

<span data-ttu-id="f7d97-209">L'esempio seguente esegue query sul servizio metadati per gli eventi pianificati e quindi approva gli eventi in sospeso.</span><span class="sxs-lookup"><span data-stu-id="f7d97-209">The following sample queries the metadata service for scheduled events and approves each outstanding event.</span></span>

```csharp
public class Program
{
    static ScheduledEventsClient client;

    static void Main(string[] args)
    {
        client = new ScheduledEventsClient();

        while (true)
        {
            string json = client.GetDocument();
            ScheduledEventsDocument scheduledEventsDocument = JsonConvert.DeserializeObject<ScheduledEventsDocument>(json);

            HandleEvents(scheduledEventsDocument.Events);

            // Wait for user response
            Console.WriteLine("Press Enter to approve executing events\n");
            Console.ReadLine();

            // Approve events
            ScheduledEventsApproval scheduledEventsApprovalDocument = new ScheduledEventsApproval()
            {
                DocumentIncarnation = scheduledEventsDocument.DocumentIncarnation
            };
        
            foreach (CloudControlEvent event in scheduledEventsDocument.Events)
            {
                scheduledEventsApprovalDocument.StartRequests.Add(new StartRequest(event.EventId));
            }

            if (scheduledEventsApprovalDocument.StartRequests.Count > 0)
            {
                // Serialize using Newtonsoft.Json
                string approveEventsJsonDocument =
                    JsonConvert.SerializeObject(scheduledEventsApprovalDocument);

                Console.WriteLine($"Approving events with json: {approveEventsJsonDocument}\n");
                client.ApproveScheduledEvents(approveEventsJsonDocument);
            }

            Console.WriteLine("Complete. Press enter to repeat\n\n");
            Console.ReadLine();
            Console.Clear();
        }
    }

    private static void HandleEvents(List<CloudControlEvent> events)
    {
        // Add logic for handling events here
    }
}
```

## <a name="python-sample"></a><span data-ttu-id="f7d97-210">Esempio Python</span><span class="sxs-lookup"><span data-stu-id="f7d97-210">Python sample</span></span> 

<span data-ttu-id="f7d97-211">L'esempio seguente esegue query sul servizio metadati per gli eventi pianificati e quindi approva gli eventi in sospeso.</span><span class="sxs-lookup"><span data-stu-id="f7d97-211">The following sample queries the metadata service for scheduled events and approves each outstanding event.</span></span>

```python
#!/usr/bin/python

import json
import urllib2
import socket
import sys

metadata_url = "http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01"
headers = "{Metadata:true}"
this_host = socket.gethostname()

def get_scheduled_events():
   req = urllib2.Request(metadata_url)
   req.add_header('Metadata', 'true')
   resp = urllib2.urlopen(req)
   data = json.loads(resp.read())
   return data

def handle_scheduled_events(data):
    for evt in data['Events']:
        eventid = evt['EventId']
        status = evt['EventStatus']
        resources = evt['Resources']
        eventtype = evt['EventType']
        resourcetype = evt['ResourceType']
        notbefore = evt['NotBefore'].replace(" ","_")
        if this_host in resources:
            print "+ Scheduled Event. This host is scheduled for " + eventype + " not before " + notbefore
            # Add logic for handling events here

def main():
   data = get_scheduled_events()
   handle_scheduled_events(data)
   
if __name__ == '__main__':
  main()
  sys.exit(0)
```

## <a name="next-steps"></a><span data-ttu-id="f7d97-212">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f7d97-212">Next steps</span></span> 

- <span data-ttu-id="f7d97-213">Altre informazioni sulle API disponibili nel [servizio metadati dell'istanza](instance-metadata-service.md).</span><span class="sxs-lookup"><span data-stu-id="f7d97-213">Read more about the APIs available in the [Instance Metadata service](instance-metadata-service.md).</span></span>
- <span data-ttu-id="f7d97-214">Informazioni sulla [manutenzione pianificata per le macchine virtuali Windows in Azure](planned-maintenance.md).</span><span class="sxs-lookup"><span data-stu-id="f7d97-214">Learn about [planned maintenance for Windows virtual machines in Azure](planned-maintenance.md).</span></span>

