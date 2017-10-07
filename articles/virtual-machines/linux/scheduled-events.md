---
title: gli eventi per le macchine virtuali Linux in Azure aaaScheduled | Documenti Microsoft
description: Eventi pianificati tramite il servizio Azure metadati hello per nelle macchine virtuali Linux.
services: virtual-machines-windows, virtual-machines-linux, cloud-services
documentationcenter: 
author: zivraf
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: zivr
ms.openlocfilehash: e153c8854725330acefd67d0ef542f6149170a7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-metadata-service-scheduled-events-preview-for-linux-vms"></a><span data-ttu-id="5d38c-103">Servizio metadati di Azure: eventi pianificati (anteprima) per VM Linux</span><span class="sxs-lookup"><span data-stu-id="5d38c-103">Azure Metadata Service: Scheduled Events (Preview) for Linux VMs</span></span>

> [!NOTE] 
> <span data-ttu-id="5d38c-104">Le anteprime vengono apportate tooyou disponibili nella condizione hello che accetti toohello condizioni di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="5d38c-104">Previews are made available tooyou on hello condition that you agree toohello terms of use.</span></span> <span data-ttu-id="5d38c-105">Per altre informazioni, vedere [Condizioni Supplementari di Microsoft Azure le Anteprime di Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span><span class="sxs-lookup"><span data-stu-id="5d38c-105">For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span></span>
>

<span data-ttu-id="5d38c-106">Gli eventi pianificati è uno dei servizi secondari hello in hello servizio metadati di Azure.</span><span class="sxs-lookup"><span data-stu-id="5d38c-106">Scheduled Events is one of hello subservices under hello Azure Metadata Service.</span></span> <span data-ttu-id="5d38c-107">Presenta informazioni sugli eventi imminenti, ad esempio i riavvii, in modo che l'applicazione possa prepararsi di conseguenza e limitare le interruzioni.</span><span class="sxs-lookup"><span data-stu-id="5d38c-107">It is responsible for surfacing information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span> <span data-ttu-id="5d38c-108">Il servizio è disponibile per tutti i tipi di macchine virtuali di Azure, inclusi PaaS e IaaS.</span><span class="sxs-lookup"><span data-stu-id="5d38c-108">It is available for all Azure Virtual Machine types including PaaS and IaaS.</span></span> <span data-ttu-id="5d38c-109">Gli eventi pianificati offre le attività di prevenzione di macchina virtuale ora tooperform effetto hello toominimize di un evento.</span><span class="sxs-lookup"><span data-stu-id="5d38c-109">Scheduled Events gives your Virtual Machine time tooperform preventive tasks toominimize hello effect of an event.</span></span> 

<span data-ttu-id="5d38c-110">Eventi pianificati è disponibile per VM sia Windows che Linux.</span><span class="sxs-lookup"><span data-stu-id="5d38c-110">Scheduled Events is available for both Windows and Linux VMs.</span></span> <span data-ttu-id="5d38c-111">Per informazioni su Eventi pianificati in Windows, vedere [Eventi pianificati per macchine virtuali Windows](../windows/scheduled-events.md).</span><span class="sxs-lookup"><span data-stu-id="5d38c-111">For information about Scheduled Events on Windows, see [Scheduled Events for Windows VMs](../windows/scheduled-events.md).</span></span>

## <a name="why-scheduled-events"></a><span data-ttu-id="5d38c-112">Perché usare gli eventi pianificati</span><span class="sxs-lookup"><span data-stu-id="5d38c-112">Why Scheduled Events?</span></span>

<span data-ttu-id="5d38c-113">Con agli eventi pianificati, è possibile eseguire passaggi impatto hello toolimit di piattaforma intiated manutenzione o le azioni avviate dall'utente nel servizio.</span><span class="sxs-lookup"><span data-stu-id="5d38c-113">With Scheduled Events, you can take steps toolimit hello impact of platform-intiated maintenance or user-initiated actions on your service.</span></span> 

<span data-ttu-id="5d38c-114">Carichi di lavoro multi-istanza, che utilizza lo stato di replica tecniche toomaintain, potrebbe essere vulnerabile toooutages tra più istanze in corso.</span><span class="sxs-lookup"><span data-stu-id="5d38c-114">Multi-instance workloads, which use replication techniques toomaintain state, may be vulnerable toooutages happening across multiple instances.</span></span> <span data-ttu-id="5d38c-115">Tali interruzioni potrebbero comportare attività costose, ad esempio, la ricompilazione degli indici, o addirittura una perdita di replica.</span><span class="sxs-lookup"><span data-stu-id="5d38c-115">Such outages may result in expensive tasks (for example, rebuilding indexes) or even a replica loss.</span></span> 

<span data-ttu-id="5d38c-116">In molti altri casi, hello complessiva disponibilità del servizio può essere migliorata eseguendo la sequenza di arresto, ad esempio completamento (o annullamento) pertanto le transazioni, la riassegnazione attività tooother macchine virtuali in cluster hello (failover manuale), o la rimozione di hello Macchina virtuale da un pool di bilanciamento del carico di rete.</span><span class="sxs-lookup"><span data-stu-id="5d38c-116">In many other cases, hello overall service availability may be improved by performing a graceful shutdown sequence such as completing (or canceling) in-flight transactions, reassigning tasks tooother VMs in hello cluster (manual failover), or removing hello Virtual Machine from a network load balancer pool.</span></span> 

<span data-ttu-id="5d38c-117">Vi sono casi in cui informando un amministratore su un evento futuro o registrazione dell'evento contribuire a migliorare l'efficienza hello di applicazioni ospitate nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="5d38c-117">There are cases where notifying an administrator about an upcoming event or logging such an event help improving hello serviceability of applications hosted in hello cloud.</span></span>

<span data-ttu-id="5d38c-118">Casi d'uso di Azure Metadata Service superfici agli eventi pianificati seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="5d38c-118">Azure Metadata Service surfaces Scheduled Events in hello following use cases:</span></span>
-   <span data-ttu-id="5d38c-119">Manutenzione avviata dalla piattaforma, ad esempio implementazione del sistema operativo host</span><span class="sxs-lookup"><span data-stu-id="5d38c-119">Platform initiated maintenance (for example, Host OS rollout)</span></span>
-   <span data-ttu-id="5d38c-120">Chiamate avviate dall'utente, ad esempio riavvii iniziati dall'utente o ridistribuzione di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="5d38c-120">User-initiated calls (for example, user restarts or redeploys a VM)</span></span>


## <a name="hello-basics"></a><span data-ttu-id="5d38c-121">Nozioni di base Hello</span><span class="sxs-lookup"><span data-stu-id="5d38c-121">hello basics</span></span>  

<span data-ttu-id="5d38c-122">Servizio di metadati di Azure espone informazioni sull'esecuzione di macchine virtuali tramite un Endpoint REST accessibile dall'interno di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5d38c-122">Azure Metadata service exposes information about running Virtual Machines using a REST Endpoint accessible from within hello VM.</span></span> <span data-ttu-id="5d38c-123">informazioni Hello sono disponibile tramite un indirizzo IP non instradabile, in modo che non è esposta all'esterno di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5d38c-123">hello information is available via a non-routable IP so that it is not exposed outside hello VM.</span></span>

### <a name="scope"></a><span data-ttu-id="5d38c-124">Scope</span><span class="sxs-lookup"><span data-stu-id="5d38c-124">Scope</span></span>
<span data-ttu-id="5d38c-125">Gli eventi pianificati sono tooall esposto macchine virtuali in un servizio cloud o tooall macchine virtuali in un Set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="5d38c-125">Scheduled events are surfaced tooall Virtual Machines in a cloud service or tooall Virtual Machines in an Availability Set.</span></span> <span data-ttu-id="5d38c-126">Di conseguenza, è consigliabile controllare hello `Resources` campo hello evento tooidentify che le macchine virtuali verranno toobe interessati.</span><span class="sxs-lookup"><span data-stu-id="5d38c-126">As a result, you should check hello `Resources` field in hello event tooidentify which VMs are going toobe impacted.</span></span> 

### <a name="discovering-hello-endpoint"></a><span data-ttu-id="5d38c-127">Individuazione di endpoint hello</span><span class="sxs-lookup"><span data-stu-id="5d38c-127">Discovering hello endpoint</span></span>
<span data-ttu-id="5d38c-128">In caso di hello in cui viene creata una macchina virtuale in una rete virtuale (VNet), è disponibile da un IP statico non instradabile, servizio metadati hello `169.254.169.254`.</span><span class="sxs-lookup"><span data-stu-id="5d38c-128">In hello case where a Virtual Machine is created within a Virtual Network (VNet), hello metadata service is available from a static non-routable IP, `169.254.169.254`.</span></span>
<span data-ttu-id="5d38c-129">Se hello macchina virtuale non è stato creato in una rete virtuale, il case predefinito hello per servizi cloud e le macchine virtuali classiche, logica aggiuntiva è necessario toodiscover hello endpoint toouse.</span><span class="sxs-lookup"><span data-stu-id="5d38c-129">If hello Virtual Machine is not created within a Virtual Network, hello default cases for cloud services and classic VMs, additional logic is required toodiscover hello endpoint toouse.</span></span> <span data-ttu-id="5d38c-130">Vedere come troppo toothis esempio toolearn[individua endpoint host hello](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span><span class="sxs-lookup"><span data-stu-id="5d38c-130">Refer toothis sample toolearn how too[discover hello host endpoint](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span></span>

### <a name="versioning"></a><span data-ttu-id="5d38c-131">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="5d38c-131">Versioning</span></span> 
<span data-ttu-id="5d38c-132">Hello servizio metadati dell'istanza viene creata.</span><span class="sxs-lookup"><span data-stu-id="5d38c-132">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="5d38c-133">Le versioni sono obbligatorie e la versione corrente di hello è `2017-03-01`.</span><span class="sxs-lookup"><span data-stu-id="5d38c-133">Versions are mandatory and hello current version is `2017-03-01`.</span></span>

> [!NOTE] 
> <span data-ttu-id="5d38c-134">Versioni precedenti di anteprima di eventi pianificati supportati {più recente} come hello. api-version.</span><span class="sxs-lookup"><span data-stu-id="5d38c-134">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="5d38c-135">Questo formato non è più supportato e verrà rimossa in futuro hello.</span><span class="sxs-lookup"><span data-stu-id="5d38c-135">This format is no longer supported and will be deprecated in hello future.</span></span>

### <a name="using-headers"></a><span data-ttu-id="5d38c-136">Uso delle intestazioni</span><span class="sxs-lookup"><span data-stu-id="5d38c-136">Using headers</span></span>
<span data-ttu-id="5d38c-137">Quando si eseguono query hello Metadata Service, è necessario specificare l'intestazione di hello `Metadata: true` tooensure hello richiesta non è stata reindirizzata accidentalmente.</span><span class="sxs-lookup"><span data-stu-id="5d38c-137">When you query hello Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="enabling-scheduled-events"></a><span data-ttu-id="5d38c-138">Attivazione degli eventi pianificati</span><span class="sxs-lookup"><span data-stu-id="5d38c-138">Enabling Scheduled Events</span></span>
<span data-ttu-id="5d38c-139">Hello prima volta che si effettua una richiesta per gli eventi pianificati, Azure consente implicitamente funzionalità hello sulla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5d38c-139">hello first time you make a request for scheduled events, Azure implicitly enables hello feature on your Virtual Machine.</span></span> <span data-ttu-id="5d38c-140">Di conseguenza, è possibile aspettarsi una risposta ritardata nella prima chiamata di backup tootwo minuti.</span><span class="sxs-lookup"><span data-stu-id="5d38c-140">As a result, you should expect a delayed response in your first call of up tootwo minutes.</span></span>

### <a name="user-initiated-maintenance"></a><span data-ttu-id="5d38c-141">Manutenzione avviata dall'utente</span><span class="sxs-lookup"><span data-stu-id="5d38c-141">User initiated maintenance</span></span>
<span data-ttu-id="5d38c-142">Manutenzione delle macchine virtuali tramite il portale di Azure, hello API, CLI, avviata dall'utente o PowerShell genera un evento pianificato.</span><span class="sxs-lookup"><span data-stu-id="5d38c-142">User initiated virtual machine maintenance via hello Azure portal, API, CLI, or PowerShell results in a scheduled event.</span></span> <span data-ttu-id="5d38c-143">Questo consente la logica di preparazione tootest hello manutenzione dell'applicazione e tooprepare l'applicazione per la manutenzione avviata dall'utente.</span><span class="sxs-lookup"><span data-stu-id="5d38c-143">This allows you tootest hello maintenance preparation logic in your application and allows your application tooprepare for user initiated maintenance.</span></span>

<span data-ttu-id="5d38c-144">Il riavvio di una macchina virtuale pianifica un evento di tipo `Reboot`.</span><span class="sxs-lookup"><span data-stu-id="5d38c-144">Restarting a virtual machine schedules an event with type `Reboot`.</span></span> <span data-ttu-id="5d38c-145">La ridistribuzione di una macchina virtuale pianifica un evento di tipo `Redeploy`.</span><span class="sxs-lookup"><span data-stu-id="5d38c-145">Redeploying a virtual machine schedules an event with type `Redeploy`.</span></span>

> [!NOTE] 
> <span data-ttu-id="5d38c-146">Attualmente è possibile pianificare un massimo di 10 operazioni di manutenzione avviata dall'utente.</span><span class="sxs-lookup"><span data-stu-id="5d38c-146">Currently a maximum of 10 user initiated maintenance operations can be simultaneously scheduled.</span></span> <span data-ttu-id="5d38c-147">Questo limite viene aumentato prima della disponibilità generale di eventi pianificati.</span><span class="sxs-lookup"><span data-stu-id="5d38c-147">This limit will be relaxed before Scheduled Events general availability.</span></span>

> [!NOTE] 
> <span data-ttu-id="5d38c-148">Attualmente la manutenzione avviata dall'utente che dà luogo a eventi pianificati non è configurabile.</span><span class="sxs-lookup"><span data-stu-id="5d38c-148">Currently user initiated maintenance resulting in Scheduled Events is not configurable.</span></span> <span data-ttu-id="5d38c-149">Questa funzionalità è pianificata per una versione successiva.</span><span class="sxs-lookup"><span data-stu-id="5d38c-149">Configurability is planned for a future release.</span></span>

## <a name="using-hello-api"></a><span data-ttu-id="5d38c-150">Tramite l'API di hello</span><span class="sxs-lookup"><span data-stu-id="5d38c-150">Using hello API</span></span>

### <a name="query-for-events"></a><span data-ttu-id="5d38c-151">Query per gli eventi</span><span class="sxs-lookup"><span data-stu-id="5d38c-151">Query for events</span></span>
<span data-ttu-id="5d38c-152">È possibile eseguire una query per gli eventi pianificati sufficiente chiamata hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="5d38c-152">You can query for Scheduled Events simply by making hello following call:</span></span>

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

<span data-ttu-id="5d38c-153">Una risposta contiene una serie di eventi pianificati.</span><span class="sxs-lookup"><span data-stu-id="5d38c-153">A response contains an array of scheduled events.</span></span> <span data-ttu-id="5d38c-154">Una serie vuota indica che al momento non sono presenti eventi pianificati.</span><span class="sxs-lookup"><span data-stu-id="5d38c-154">An empty array means that there are currently no events scheduled.</span></span>
<span data-ttu-id="5d38c-155">In caso di hello in cui sono presenti eventi pianificati, risposta hello contiene una matrice di eventi:</span><span class="sxs-lookup"><span data-stu-id="5d38c-155">In hello case where there are scheduled events, hello response contains an array of events:</span></span> 
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

### <a name="event-properties"></a><span data-ttu-id="5d38c-156">Proprietà degli eventi</span><span class="sxs-lookup"><span data-stu-id="5d38c-156">Event properties</span></span>
|<span data-ttu-id="5d38c-157">Proprietà</span><span class="sxs-lookup"><span data-stu-id="5d38c-157">Property</span></span>  |  <span data-ttu-id="5d38c-158">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5d38c-158">Description</span></span> |
| - | - |
| <span data-ttu-id="5d38c-159">EventId</span><span class="sxs-lookup"><span data-stu-id="5d38c-159">EventId</span></span> | <span data-ttu-id="5d38c-160">Identificatore globalmente univoco per l'evento.</span><span class="sxs-lookup"><span data-stu-id="5d38c-160">Globally unique identifier for this event.</span></span> <br><br> <span data-ttu-id="5d38c-161">Esempio:</span><span class="sxs-lookup"><span data-stu-id="5d38c-161">Example:</span></span> <br><ul><li><span data-ttu-id="5d38c-162">602d9444-d2cd-49c7-8624-8643e7171297</span><span class="sxs-lookup"><span data-stu-id="5d38c-162">602d9444-d2cd-49c7-8624-8643e7171297</span></span>  |
| <span data-ttu-id="5d38c-163">EventType</span><span class="sxs-lookup"><span data-stu-id="5d38c-163">EventType</span></span> | <span data-ttu-id="5d38c-164">Impatto che l'evento causa.</span><span class="sxs-lookup"><span data-stu-id="5d38c-164">Impact this event causes.</span></span> <br><br> <span data-ttu-id="5d38c-165">Valori:</span><span class="sxs-lookup"><span data-stu-id="5d38c-165">Values:</span></span> <br><ul><li> <span data-ttu-id="5d38c-166">`Freeze`: hello macchina virtuale è pianificato toopause per alcuni secondi.</span><span class="sxs-lookup"><span data-stu-id="5d38c-166">`Freeze`: hello Virtual Machine is scheduled toopause for few seconds.</span></span> <span data-ttu-id="5d38c-167">Hello della CPU è sospesa, ma non ha alcun impatto su memoria, i file aperti o connessioni di rete.</span><span class="sxs-lookup"><span data-stu-id="5d38c-167">hello CPU is suspended, but there is no impact on memory, open files, or network connections.</span></span> <li><span data-ttu-id="5d38c-168">`Reboot`: hello macchina virtuale è pianificata per riavviare il sistema (memoria non persistente viene persa).</span><span class="sxs-lookup"><span data-stu-id="5d38c-168">`Reboot`: hello Virtual Machine is scheduled for reboot (non-persistent memory is lost).</span></span> <li><span data-ttu-id="5d38c-169">`Redeploy`: hello macchina virtuale è pianificato toomove tooanother nodo (dischi temporanei andranno persi).</span><span class="sxs-lookup"><span data-stu-id="5d38c-169">`Redeploy`: hello Virtual Machine is scheduled toomove tooanother node (ephemeral disks are lost).</span></span> |
| <span data-ttu-id="5d38c-170">ResourceType</span><span class="sxs-lookup"><span data-stu-id="5d38c-170">ResourceType</span></span> | <span data-ttu-id="5d38c-171">Tipo di risorsa su cui l'evento influisce.</span><span class="sxs-lookup"><span data-stu-id="5d38c-171">Type of resource this event impacts.</span></span> <br><br> <span data-ttu-id="5d38c-172">Valori:</span><span class="sxs-lookup"><span data-stu-id="5d38c-172">Values:</span></span> <ul><li>`VirtualMachine`|
| <span data-ttu-id="5d38c-173">Risorse</span><span class="sxs-lookup"><span data-stu-id="5d38c-173">Resources</span></span>| <span data-ttu-id="5d38c-174">Elenco delle risorse su cui l'evento influisce.</span><span class="sxs-lookup"><span data-stu-id="5d38c-174">List of resources this event impacts.</span></span> <span data-ttu-id="5d38c-175">Questo è garantito macchine toocontain da almeno uno [dominio di aggiornamento](manage-availability.md), ma non può contenere tutti i computer hello UD.</span><span class="sxs-lookup"><span data-stu-id="5d38c-175">This is guaranteed toocontain machines from at most one [Update Domain](manage-availability.md), but may not contain all machines in hello UD.</span></span> <br><br> <span data-ttu-id="5d38c-176">Esempio:</span><span class="sxs-lookup"><span data-stu-id="5d38c-176">Example:</span></span> <br><ul><li> <span data-ttu-id="5d38c-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span><span class="sxs-lookup"><span data-stu-id="5d38c-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span></span> |
| <span data-ttu-id="5d38c-178">Event Status</span><span class="sxs-lookup"><span data-stu-id="5d38c-178">Event Status</span></span> | <span data-ttu-id="5d38c-179">Stato dell'evento.</span><span class="sxs-lookup"><span data-stu-id="5d38c-179">Status of this event.</span></span> <br><br> <span data-ttu-id="5d38c-180">Valori:</span><span class="sxs-lookup"><span data-stu-id="5d38c-180">Values:</span></span> <ul><li><span data-ttu-id="5d38c-181">`Scheduled`: Questo evento è pianificato toostart dopo il tempo di hello specificato hello `NotBefore` proprietà.</span><span class="sxs-lookup"><span data-stu-id="5d38c-181">`Scheduled`: This event is scheduled toostart after hello time specified in hello `NotBefore` property.</span></span><li><span data-ttu-id="5d38c-182">`Started`: l'evento si è avviato.</span><span class="sxs-lookup"><span data-stu-id="5d38c-182">`Started`: This event has started.</span></span></ul> <span data-ttu-id="5d38c-183">Non `Completed` o simile viene sempre fornito; evento hello non verrà restituito al termine dell'evento hello.</span><span class="sxs-lookup"><span data-stu-id="5d38c-183">No `Completed` or similar status is ever provided; hello event will no longer be returned when hello event is completed.</span></span>
| <span data-ttu-id="5d38c-184">NotBefore</span><span class="sxs-lookup"><span data-stu-id="5d38c-184">NotBefore</span></span>| <span data-ttu-id="5d38c-185">Tempo dopo il quale l'evento può essere avviato.</span><span class="sxs-lookup"><span data-stu-id="5d38c-185">Time after which this event may start.</span></span> <br><br> <span data-ttu-id="5d38c-186">Esempio:</span><span class="sxs-lookup"><span data-stu-id="5d38c-186">Example:</span></span> <br><ul><li> <span data-ttu-id="5d38c-187">2016-09-19T18:29:47Z</span><span class="sxs-lookup"><span data-stu-id="5d38c-187">2016-09-19T18:29:47Z</span></span>  |

### <a name="event-scheduling"></a><span data-ttu-id="5d38c-188">Pianificazione degli eventi</span><span class="sxs-lookup"><span data-stu-id="5d38c-188">Event scheduling</span></span>
<span data-ttu-id="5d38c-189">Ogni evento è pianificata una quantità minima di tempo in futuro hello dipende dal tipo di evento.</span><span class="sxs-lookup"><span data-stu-id="5d38c-189">Each event is scheduled a minimum amount of time in hello future based on event type.</span></span> <span data-ttu-id="5d38c-190">Questo tempo si riflette in una proprietà `NotBefore` dell'evento.</span><span class="sxs-lookup"><span data-stu-id="5d38c-190">This time is reflected in an event's `NotBefore` property.</span></span> 

|<span data-ttu-id="5d38c-191">EventType</span><span class="sxs-lookup"><span data-stu-id="5d38c-191">EventType</span></span>  | <span data-ttu-id="5d38c-192">Minimum Notice</span><span class="sxs-lookup"><span data-stu-id="5d38c-192">Minimum Notice</span></span> |
| - | - |
| <span data-ttu-id="5d38c-193">Freeze</span><span class="sxs-lookup"><span data-stu-id="5d38c-193">Freeze</span></span>| <span data-ttu-id="5d38c-194">15 minuti</span><span class="sxs-lookup"><span data-stu-id="5d38c-194">15 minutes</span></span> |
| <span data-ttu-id="5d38c-195">Reboot</span><span class="sxs-lookup"><span data-stu-id="5d38c-195">Reboot</span></span> | <span data-ttu-id="5d38c-196">15 minuti</span><span class="sxs-lookup"><span data-stu-id="5d38c-196">15 minutes</span></span> |
| <span data-ttu-id="5d38c-197">Ripetere la distribuzione</span><span class="sxs-lookup"><span data-stu-id="5d38c-197">Redeploy</span></span> | <span data-ttu-id="5d38c-198">10 minuti</span><span class="sxs-lookup"><span data-stu-id="5d38c-198">10 minutes</span></span> |

### <a name="starting-an-event"></a><span data-ttu-id="5d38c-199">Avvio di un evento</span><span class="sxs-lookup"><span data-stu-id="5d38c-199">Starting an event</span></span> 

<span data-ttu-id="5d38c-200">Dopo aver appreso di un imminente evento e completato la logica per l'arresto normale, è possibile approvare eventi in attesa di hello effettuando un `POST` chiamare il servizio metadati toohello con hello `EventId`.</span><span class="sxs-lookup"><span data-stu-id="5d38c-200">Once you have learned of an upcoming event and completed your logic for graceful shutdown, you can approve hello outstanding event by making a `POST` call toohello metadata service with hello `EventId`.</span></span> <span data-ttu-id="5d38c-201">Ciò indica che è possibile abbreviare notifica minimo hello tooAzure ora (sempre).</span><span class="sxs-lookup"><span data-stu-id="5d38c-201">This indicates tooAzure that it can shorten hello minimum notification time (when possible).</span></span> 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> <span data-ttu-id="5d38c-202">Riconoscimento di un evento consente hello evento tooproceed per tutti i `Resources` nell'evento hello, non solo hello macchina virtuale che riconosce l'evento hello.</span><span class="sxs-lookup"><span data-stu-id="5d38c-202">Acknowledging an event allows hello event tooproceed for all `Resources` in hello event, not just hello virtual machine that acknowledges hello event.</span></span> <span data-ttu-id="5d38c-203">È pertanto possibile tooelect un acknowledgement leader toocoordinate hello, che può essere semplice come macchina di prima hello in hello `Resources` campo.</span><span class="sxs-lookup"><span data-stu-id="5d38c-203">You may therefore choose tooelect a leader toocoordinate hello acknowledgement, which may be as simple as hello first machine in hello `Resources` field.</span></span>




## <a name="python-sample"></a><span data-ttu-id="5d38c-204">Esempio Python</span><span class="sxs-lookup"><span data-stu-id="5d38c-204">Python sample</span></span> 

<span data-ttu-id="5d38c-205">Hello seguenti query di esempio hello servizio metadati per gli eventi pianificati e approva ogni evento in sospeso.</span><span class="sxs-lookup"><span data-stu-id="5d38c-205">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="5d38c-206">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5d38c-206">Next steps</span></span> 

- <span data-ttu-id="5d38c-207">Altre informazioni sulle API disponibili in hello hello [servizio metadati dell'istanza](instance-metadata-service.md).</span><span class="sxs-lookup"><span data-stu-id="5d38c-207">Read more about hello APIs available in hello [Instance Metadata service](instance-metadata-service.md).</span></span>
- <span data-ttu-id="5d38c-208">Informazioni sulla [manutenzione pianificata per le macchine virtuali Linux in Azure](planned-maintenance.md).</span><span class="sxs-lookup"><span data-stu-id="5d38c-208">Learn about [planned maintenance for Linux virtual machines in Azure](planned-maintenance.md).</span></span>
