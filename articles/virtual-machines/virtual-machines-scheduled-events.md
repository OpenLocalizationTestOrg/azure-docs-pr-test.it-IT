---
title: aaaScheduled eventi con il servizio di metadati di Azure | Documenti Microsoft
description: Rispondere tooImpactful eventi sulla macchina virtuale prima che si verifichino.
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
ms.date: 12/10/2016
ms.author: zivr
ms.openlocfilehash: b5c0849958c3ab48fa9c2cbff7db62f2e9d7daf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-metadata-service---scheduled-events-preview"></a><span data-ttu-id="c40a4-103">Servizio metadati di Azure - Eventi pianificati (anteprima)</span><span class="sxs-lookup"><span data-stu-id="c40a4-103">Azure Metadata Service - Scheduled Events (Preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="c40a4-104">Le anteprime vengono apportate tooyou disponibili nella condizione hello che accetti toohello condizioni di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="c40a4-104">Previews are made available tooyou on hello condition that you agree toohello terms of use.</span></span> <span data-ttu-id="c40a4-105">Per altre informazioni, vedere [Condizioni Supplementari di Microsoft Azure le Anteprime di Microsoft Azure](https://azure.microsoft.com/en-us/support/legal/preview-supplemental-terms/).</span><span class="sxs-lookup"><span data-stu-id="c40a4-105">For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/en-us/support/legal/preview-supplemental-terms/).</span></span>
>

<span data-ttu-id="c40a4-106">Gli eventi pianificati è uno dei servizi secondari hello in hello servizio metadati di Azure.</span><span class="sxs-lookup"><span data-stu-id="c40a4-106">Scheduled Events is one of hello subservices under hello Azure Metadata Service.</span></span> <span data-ttu-id="c40a4-107">Presenta informazioni sugli eventi imminenti, ad esempio i riavvii, in modo che l'applicazione possa prepararsi di conseguenza e limitare le interruzioni.</span><span class="sxs-lookup"><span data-stu-id="c40a4-107">It is responsible for surfacing information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span> <span data-ttu-id="c40a4-108">Il servizio è disponibile per tutti i tipi di macchine virtuali di Azure, inclusi PaaS e IaaS.</span><span class="sxs-lookup"><span data-stu-id="c40a4-108">It is available for all Azure Virtual Machine types including PaaS and IaaS.</span></span> <span data-ttu-id="c40a4-109">Gli eventi pianificati offre le attività di prevenzione di macchina virtuale ora tooperform effetto hello toominimize di un evento.</span><span class="sxs-lookup"><span data-stu-id="c40a4-109">Scheduled Events gives your Virtual Machine time tooperform preventive tasks toominimize hello effect of an event.</span></span> 

## <a name="introduction---why-scheduled-events"></a><span data-ttu-id="c40a4-110">Introduzione: perché scegliere gli eventi pianificati?</span><span class="sxs-lookup"><span data-stu-id="c40a4-110">Introduction - Why Scheduled Events?</span></span>

<span data-ttu-id="c40a4-111">Con agli eventi pianificati, è possibile eseguire passaggi impatto hello toolimit di piattaforma intiated manutenzione o le azioni avviate dall'utente nel servizio.</span><span class="sxs-lookup"><span data-stu-id="c40a4-111">With Scheduled Events, you can take steps toolimit hello impact of platform-intiated maintenance or user-initiated actions on your service.</span></span> 

<span data-ttu-id="c40a4-112">Carichi di lavoro multi-istanza, che utilizza lo stato di replica tecniche toomaintain, potrebbe essere vulnerabile toooutages tra più istanze in corso.</span><span class="sxs-lookup"><span data-stu-id="c40a4-112">Multi-instance workloads, which use replication techniques toomaintain state, may be vulnerable toooutages happening across multiple instances.</span></span> <span data-ttu-id="c40a4-113">Tali interruzioni potrebbero comportare attività costose, ad esempio, la ricompilazione degli indici, o addirittura una perdita di replica.</span><span class="sxs-lookup"><span data-stu-id="c40a4-113">Such outages may result in expensive tasks (for example, rebuilding indexes) or even a replica loss.</span></span> 

<span data-ttu-id="c40a4-114">In molti altri casi, hello complessiva disponibilità del servizio può essere migliorata eseguendo la sequenza di arresto, ad esempio completamento (o annullamento) pertanto le transazioni, la riassegnazione attività tooother macchine virtuali in cluster hello (failover manuale), o la rimozione di hello Macchina virtuale da un pool di bilanciamento del carico di rete.</span><span class="sxs-lookup"><span data-stu-id="c40a4-114">In many other cases, hello overall service availability may be improved by performing a graceful shutdown sequence such as completing (or canceling) in-flight transactions, reassigning tasks tooother VMs in hello cluster (manual failover), or removing hello Virtual Machine from a network load balancer pool.</span></span> 

<span data-ttu-id="c40a4-115">Vi sono casi in cui informando un amministratore su un evento futuro o registrazione dell'evento contribuire a migliorare l'efficienza hello di applicazioni ospitate nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="c40a4-115">There are cases where notifying an administrator about an upcoming event or logging such an event help improving hello serviceability of applications hosted in hello cloud.</span></span>

<span data-ttu-id="c40a4-116">Casi d'uso di Azure Metadata Service superfici agli eventi pianificati seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="c40a4-116">Azure Metadata Service surfaces Scheduled Events in hello following use cases:</span></span>
-   <span data-ttu-id="c40a4-117">Manutenzione avviata dalla piattaforma, ad esempio implementazione del sistema operativo host</span><span class="sxs-lookup"><span data-stu-id="c40a4-117">Platform initiated maintenance (for example, Host OS rollout)</span></span>
-   <span data-ttu-id="c40a4-118">Chiamate avviate dall'utente, ad esempio riavvii iniziati dall'utente o ridistribuzione di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="c40a4-118">User-initiated calls (for example, user restarts or redeploys a VM)</span></span>


## <a name="scheduled-events---hello-basics"></a><span data-ttu-id="c40a4-119">Eventi pianificati - hello nozioni di base</span><span class="sxs-lookup"><span data-stu-id="c40a4-119">Scheduled Events - hello Basics</span></span>  

<span data-ttu-id="c40a4-120">Servizio di metadati di Azure espone informazioni sull'esecuzione di macchine virtuali tramite un Endpoint REST accessibile dall'interno di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c40a4-120">Azure Metadata service exposes information about running Virtual Machines using a REST Endpoint accessible from within hello VM.</span></span> <span data-ttu-id="c40a4-121">informazioni Hello sono disponibile tramite un indirizzo IP non instradabile, in modo che non è esposta all'esterno di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c40a4-121">hello information is available via a non-routable IP so that it is not exposed outside hello VM.</span></span>

### <a name="scope"></a><span data-ttu-id="c40a4-122">Scope</span><span class="sxs-lookup"><span data-stu-id="c40a4-122">Scope</span></span>
<span data-ttu-id="c40a4-123">Gli eventi pianificati sono tooall esposto macchine virtuali in un servizio cloud o tooall macchine virtuali in un Set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="c40a4-123">Scheduled events are surfaced tooall Virtual Machines in a cloud service or tooall Virtual Machines in an Availability Set.</span></span> <span data-ttu-id="c40a4-124">Di conseguenza, è consigliabile controllare hello `Resources` campo hello evento tooidentify che le macchine virtuali verranno toobe interessati.</span><span class="sxs-lookup"><span data-stu-id="c40a4-124">As a result, you should check hello `Resources` field in hello event tooidentify which VMs are going toobe impacted.</span></span> 

### <a name="discovering-hello-endpoint"></a><span data-ttu-id="c40a4-125">Individuazione hello Endpoint</span><span class="sxs-lookup"><span data-stu-id="c40a4-125">Discovering hello Endpoint</span></span>
<span data-ttu-id="c40a4-126">In caso di hello in cui viene creata una macchina virtuale in una rete virtuale (VNet), è disponibile da un IP statico non instradabile, servizio metadati hello `169.254.169.254`.</span><span class="sxs-lookup"><span data-stu-id="c40a4-126">In hello case where a Virtual Machine is created within a Virtual Network (VNet), hello metadata service is available from a static non-routable IP, `169.254.169.254`.</span></span>
<span data-ttu-id="c40a4-127">Se hello macchina virtuale non è stato creato in una rete virtuale, il case predefinito hello per servizi cloud e le macchine virtuali classiche, logica aggiuntiva è necessario toodiscover hello endpoint toouse.</span><span class="sxs-lookup"><span data-stu-id="c40a4-127">If hello Virtual Machine is not created within a Virtual Network, hello default cases for cloud services and classic VMs, additional logic is required toodiscover hello endpoint toouse.</span></span> <span data-ttu-id="c40a4-128">Vedere come troppo toothis esempio toolearn[individua endpoint host hello](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span><span class="sxs-lookup"><span data-stu-id="c40a4-128">Refer toothis sample toolearn how too[discover hello host endpoint](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span></span>

### <a name="versioning"></a><span data-ttu-id="c40a4-129">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="c40a4-129">Versioning</span></span> 
<span data-ttu-id="c40a4-130">Hello servizio metadati dell'istanza viene creata.</span><span class="sxs-lookup"><span data-stu-id="c40a4-130">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="c40a4-131">Le versioni sono obbligatorie e la versione corrente di hello è `2017-03-01`.</span><span class="sxs-lookup"><span data-stu-id="c40a4-131">Versions are mandatory and hello current version is `2017-03-01`.</span></span>

> [!NOTE] 
> <span data-ttu-id="c40a4-132">Versioni precedenti di anteprima di eventi pianificati supportati {più recente} come hello. api-version.</span><span class="sxs-lookup"><span data-stu-id="c40a4-132">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="c40a4-133">Questo formato non è più supportato e verrà rimossa in futuro hello.</span><span class="sxs-lookup"><span data-stu-id="c40a4-133">This format is no longer supported and will be deprecated in hello future.</span></span>

### <a name="using-headers"></a><span data-ttu-id="c40a4-134">Uso delle intestazioni</span><span class="sxs-lookup"><span data-stu-id="c40a4-134">Using Headers</span></span>
<span data-ttu-id="c40a4-135">Quando si eseguono query hello Metadata Service, è necessario specificare l'intestazione di hello `Metadata: true` tooensure hello richiesta non è stata reindirizzata accidentalmente.</span><span class="sxs-lookup"><span data-stu-id="c40a4-135">When you query hello Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="enabling-scheduled-events"></a><span data-ttu-id="c40a4-136">Attivazione degli eventi pianificati</span><span class="sxs-lookup"><span data-stu-id="c40a4-136">Enabling Scheduled Events</span></span>
<span data-ttu-id="c40a4-137">Hello prima volta che si effettua una richiesta per gli eventi pianificati, Azure consente implicitamente funzionalità hello sulla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c40a4-137">hello first time you make a request for scheduled events, Azure implicitly enables hello feature on your Virtual Machine.</span></span> <span data-ttu-id="c40a4-138">Di conseguenza, è possibile aspettarsi una risposta ritardata nella prima chiamata di backup tootwo minuti.</span><span class="sxs-lookup"><span data-stu-id="c40a4-138">As a result, you should expect a delayed response in your first call of up tootwo minutes.</span></span>

### <a name="user-initiated-maintenance"></a><span data-ttu-id="c40a4-139">Manutenzione avviata dall'utente</span><span class="sxs-lookup"><span data-stu-id="c40a4-139">User Initiated Maintenance</span></span>
<span data-ttu-id="c40a4-140">Manutenzione delle macchine virtuali tramite il portale di Azure, hello API, CLI, avviata dall'utente o PowerShell comporterà agli eventi pianificati.</span><span class="sxs-lookup"><span data-stu-id="c40a4-140">User initiated virtual machine maintenance via hello Azure portal, API, CLI, or PowerShell will result in Scheduled Events.</span></span> <span data-ttu-id="c40a4-141">Questo consente la logica di preparazione tootest hello manutenzione dell'applicazione e tooprepare l'applicazione per la manutenzione avviata dall'utente.</span><span class="sxs-lookup"><span data-stu-id="c40a4-141">This allows you tootest hello maintenance preparation logic in your application and allows your application tooprepare for user initiated maintenance.</span></span>

<span data-ttu-id="c40a4-142">Il riavvio di una macchina virtuale pianificherà un evento di tipo `Reboot`.</span><span class="sxs-lookup"><span data-stu-id="c40a4-142">Restarting a virtual machine will schedule an event with type `Reboot`.</span></span> <span data-ttu-id="c40a4-143">La ridistribuzione di una macchina virtuale pianificherà un evento di tipo `Redeploy`.</span><span class="sxs-lookup"><span data-stu-id="c40a4-143">Redeploying a virtual machine will schedule an event with type `Redeploy`.</span></span>

> [!NOTE] 
> <span data-ttu-id="c40a4-144">Attualmente è possibile pianificare un massimo di 10 operazioni di manutenzione avviata dall'utente.</span><span class="sxs-lookup"><span data-stu-id="c40a4-144">Currently a maximum of 10 user initiated maintenance operations can be simultaneously scheduled.</span></span> <span data-ttu-id="c40a4-145">Questo limite viene aumentato prima della disponibilità generale di eventi pianificati.</span><span class="sxs-lookup"><span data-stu-id="c40a4-145">This limit will be relaxed before Scheduled Events General Availability.</span></span>

> [!NOTE] 
> <span data-ttu-id="c40a4-146">Attualmente la manutenzione avviata dall'utente che dà luogo a eventi pianificati non è configurabile.</span><span class="sxs-lookup"><span data-stu-id="c40a4-146">Currently user initiated maintenance resulting in Scheduled Events is not configurable.</span></span> <span data-ttu-id="c40a4-147">Questa funzionalità è pianificata per una versione successiva.</span><span class="sxs-lookup"><span data-stu-id="c40a4-147">Configurability is planned for a future release.</span></span>

## <a name="using-hello-api"></a><span data-ttu-id="c40a4-148">Tramite l'API di hello</span><span class="sxs-lookup"><span data-stu-id="c40a4-148">Using hello API</span></span>

### <a name="query-for-events"></a><span data-ttu-id="c40a4-149">Query per gli eventi</span><span class="sxs-lookup"><span data-stu-id="c40a4-149">Query for events</span></span>
<span data-ttu-id="c40a4-150">È possibile eseguire una query per gli eventi pianificati sufficiente chiamata hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="c40a4-150">You can query for Scheduled Events simply by making hello following call:</span></span>

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

<span data-ttu-id="c40a4-151">Una risposta contiene una serie di eventi pianificati.</span><span class="sxs-lookup"><span data-stu-id="c40a4-151">A response contains an array of scheduled events.</span></span> <span data-ttu-id="c40a4-152">Una serie vuota indica che al momento non sono presenti eventi pianificati.</span><span class="sxs-lookup"><span data-stu-id="c40a4-152">An empty array means that there are currently no events scheduled.</span></span>
<span data-ttu-id="c40a4-153">In caso di hello in cui sono presenti eventi pianificati, risposta hello contiene una matrice di eventi:</span><span class="sxs-lookup"><span data-stu-id="c40a4-153">In hello case where there are scheduled events, hello response contains an array of events:</span></span> 
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

### <a name="event-properties"></a><span data-ttu-id="c40a4-154">Proprietà dell'evento</span><span class="sxs-lookup"><span data-stu-id="c40a4-154">Event Properties</span></span>
|<span data-ttu-id="c40a4-155">Proprietà</span><span class="sxs-lookup"><span data-stu-id="c40a4-155">Property</span></span>  |  <span data-ttu-id="c40a4-156">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c40a4-156">Description</span></span> |
| - | - |
| <span data-ttu-id="c40a4-157">EventId</span><span class="sxs-lookup"><span data-stu-id="c40a4-157">EventId</span></span> | <span data-ttu-id="c40a4-158">Identificatore globalmente univoco per l'evento.</span><span class="sxs-lookup"><span data-stu-id="c40a4-158">Globally unique identifier for this event.</span></span> <br><br> <span data-ttu-id="c40a4-159">Esempio:</span><span class="sxs-lookup"><span data-stu-id="c40a4-159">Example:</span></span> <br><ul><li><span data-ttu-id="c40a4-160">602d9444-d2cd-49c7-8624-8643e7171297</span><span class="sxs-lookup"><span data-stu-id="c40a4-160">602d9444-d2cd-49c7-8624-8643e7171297</span></span>  |
| <span data-ttu-id="c40a4-161">EventType</span><span class="sxs-lookup"><span data-stu-id="c40a4-161">EventType</span></span> | <span data-ttu-id="c40a4-162">Impatto che l'evento causa.</span><span class="sxs-lookup"><span data-stu-id="c40a4-162">Impact this event causes.</span></span> <br><br> <span data-ttu-id="c40a4-163">Valori:</span><span class="sxs-lookup"><span data-stu-id="c40a4-163">Values:</span></span> <br><ul><li> <span data-ttu-id="c40a4-164">`Freeze`: hello macchina virtuale è pianificato toopause per alcuni secondi.</span><span class="sxs-lookup"><span data-stu-id="c40a4-164">`Freeze`: hello Virtual Machine is scheduled toopause for few seconds.</span></span> <span data-ttu-id="c40a4-165">Hello CPU verrà sospeso, ma non ha alcun impatto su memoria, i file aperti o connessioni di rete.</span><span class="sxs-lookup"><span data-stu-id="c40a4-165">hello CPU will be suspended, but there is no impact on memory, open files, or network connections.</span></span> <li><span data-ttu-id="c40a4-166">`Reboot`: hello macchina virtuale è pianificata per riavviare il sistema (memoria non persistente viene persa).</span><span class="sxs-lookup"><span data-stu-id="c40a4-166">`Reboot`: hello Virtual Machine is scheduled for reboot (non-persistent memory is lost).</span></span> <li><span data-ttu-id="c40a4-167">`Redeploy`: hello macchina virtuale è pianificato toomove tooanother nodo (dischi temporanei andranno persi).</span><span class="sxs-lookup"><span data-stu-id="c40a4-167">`Redeploy`: hello Virtual Machine is scheduled toomove tooanother node (ephemeral disks are lost).</span></span> |
| <span data-ttu-id="c40a4-168">ResourceType</span><span class="sxs-lookup"><span data-stu-id="c40a4-168">ResourceType</span></span> | <span data-ttu-id="c40a4-169">Tipo di risorsa su cui l'evento influisce.</span><span class="sxs-lookup"><span data-stu-id="c40a4-169">Type of resource this event impacts.</span></span> <br><br> <span data-ttu-id="c40a4-170">Valori:</span><span class="sxs-lookup"><span data-stu-id="c40a4-170">Values:</span></span> <ul><li>`VirtualMachine`|
| <span data-ttu-id="c40a4-171">Risorse</span><span class="sxs-lookup"><span data-stu-id="c40a4-171">Resources</span></span>| <span data-ttu-id="c40a4-172">Elenco delle risorse su cui l'evento influisce.</span><span class="sxs-lookup"><span data-stu-id="c40a4-172">List of resources this event impacts.</span></span> <span data-ttu-id="c40a4-173">Questo è garantito macchine toocontain da almeno uno [dominio di aggiornamento](windows/manage-availability.md), ma non può contenere tutti i computer hello UD.</span><span class="sxs-lookup"><span data-stu-id="c40a4-173">This is guaranteed toocontain machines from at most one [Update Domain](windows/manage-availability.md), but may not contain all machines in hello UD.</span></span> <br><br> <span data-ttu-id="c40a4-174">Esempio:</span><span class="sxs-lookup"><span data-stu-id="c40a4-174">Example:</span></span> <br><ul><li> <span data-ttu-id="c40a4-175">["FrontEnd_IN_0", "BackEnd_IN_0"]</span><span class="sxs-lookup"><span data-stu-id="c40a4-175">["FrontEnd_IN_0", "BackEnd_IN_0"]</span></span> |
| <span data-ttu-id="c40a4-176">Event Status</span><span class="sxs-lookup"><span data-stu-id="c40a4-176">Event Status</span></span> | <span data-ttu-id="c40a4-177">Stato dell'evento.</span><span class="sxs-lookup"><span data-stu-id="c40a4-177">Status of this event.</span></span> <br><br> <span data-ttu-id="c40a4-178">Valori:</span><span class="sxs-lookup"><span data-stu-id="c40a4-178">Values:</span></span> <ul><li><span data-ttu-id="c40a4-179">`Scheduled`: Questo evento è pianificato toostart dopo il tempo di hello specificato hello `NotBefore` proprietà.</span><span class="sxs-lookup"><span data-stu-id="c40a4-179">`Scheduled`: This event is scheduled toostart after hello time specified in hello `NotBefore` property.</span></span><li><span data-ttu-id="c40a4-180">`Started`: l'evento si è avviato.</span><span class="sxs-lookup"><span data-stu-id="c40a4-180">`Started`: This event has started.</span></span></ul> <span data-ttu-id="c40a4-181">Non `Completed` o simile viene sempre fornito; evento hello non verrà restituito al termine dell'evento hello.</span><span class="sxs-lookup"><span data-stu-id="c40a4-181">No `Completed` or similar status is ever provided; hello event will no longer be returned when hello event is completed.</span></span>
| <span data-ttu-id="c40a4-182">NotBefore</span><span class="sxs-lookup"><span data-stu-id="c40a4-182">NotBefore</span></span>| <span data-ttu-id="c40a4-183">Tempo dopo il quale l'evento può essere avviato.</span><span class="sxs-lookup"><span data-stu-id="c40a4-183">Time after which this event may start.</span></span> <br><br> <span data-ttu-id="c40a4-184">Esempio:</span><span class="sxs-lookup"><span data-stu-id="c40a4-184">Example:</span></span> <br><ul><li> <span data-ttu-id="c40a4-185">2016-09-19T18:29:47Z</span><span class="sxs-lookup"><span data-stu-id="c40a4-185">2016-09-19T18:29:47Z</span></span>  |

### <a name="event-scheduling"></a><span data-ttu-id="c40a4-186">Event Scheduling</span><span class="sxs-lookup"><span data-stu-id="c40a4-186">Event Scheduling</span></span>
<span data-ttu-id="c40a4-187">Ogni evento è pianificata una quantità minima di tempo in futuro hello dipende dal tipo di evento.</span><span class="sxs-lookup"><span data-stu-id="c40a4-187">Each event is scheduled a minimum amount of time in hello future based on event type.</span></span> <span data-ttu-id="c40a4-188">Questo tempo si riflette in una proprietà `NotBefore` dell'evento.</span><span class="sxs-lookup"><span data-stu-id="c40a4-188">This time is reflected in an event's `NotBefore` property.</span></span> 

|<span data-ttu-id="c40a4-189">EventType</span><span class="sxs-lookup"><span data-stu-id="c40a4-189">EventType</span></span>  | <span data-ttu-id="c40a4-190">Minimum Notice</span><span class="sxs-lookup"><span data-stu-id="c40a4-190">Minimum Notice</span></span> |
| - | - |
| <span data-ttu-id="c40a4-191">Freeze</span><span class="sxs-lookup"><span data-stu-id="c40a4-191">Freeze</span></span>| <span data-ttu-id="c40a4-192">15 minuti</span><span class="sxs-lookup"><span data-stu-id="c40a4-192">15 minutes</span></span> |
| <span data-ttu-id="c40a4-193">Reboot</span><span class="sxs-lookup"><span data-stu-id="c40a4-193">Reboot</span></span> | <span data-ttu-id="c40a4-194">15 minuti</span><span class="sxs-lookup"><span data-stu-id="c40a4-194">15 minutes</span></span> |
| <span data-ttu-id="c40a4-195">Ripetere la distribuzione</span><span class="sxs-lookup"><span data-stu-id="c40a4-195">Redeploy</span></span> | <span data-ttu-id="c40a4-196">10 minuti</span><span class="sxs-lookup"><span data-stu-id="c40a4-196">10 minutes</span></span> |

### <a name="starting-an-event-expedite"></a><span data-ttu-id="c40a4-197">Avvio di un evento (urgente)</span><span class="sxs-lookup"><span data-stu-id="c40a4-197">Starting an event (expedite)</span></span>

<span data-ttu-id="c40a4-198">Dopo aver appreso di un imminente evento e completato la logica per l'arresto normale, è possibile approvare eventi in attesa di hello effettuando un `POST` chiamare il servizio metadati toohello con hello `EventId`.</span><span class="sxs-lookup"><span data-stu-id="c40a4-198">Once you have learned of an upcoming event and completed your logic for graceful shutdown, you can approve hello outstanding event by making a `POST` call toohello metadata service with hello `EventId`.</span></span> <span data-ttu-id="c40a4-199">Ciò indica che è possibile abbreviare notifica minimo hello tooAzure ora (sempre).</span><span class="sxs-lookup"><span data-stu-id="c40a4-199">This indicates tooAzure that it can shorten hello minimum notification time (when possible).</span></span> 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> <span data-ttu-id="c40a4-200">Riconoscimento di un evento consentirà hello evento tooproceed tutti `Resources` nell'evento hello, non solo hello macchina virtuale che riconosce l'evento hello.</span><span class="sxs-lookup"><span data-stu-id="c40a4-200">Acknowledging a event will allow hello event tooproceed for all `Resources` in hello event, not just hello virtual machine that acknowledges hello event.</span></span> <span data-ttu-id="c40a4-201">È pertanto possibile tooelect un acknowledgement leader toocoordinate hello, che può essere semplice come macchina di prima hello in hello `Resources` campo.</span><span class="sxs-lookup"><span data-stu-id="c40a4-201">You may therefore choose tooelect a leader toocoordinate hello acknowledgement, which may be as simple as hello first machine in hello `Resources` field.</span></span>

## <a name="samples"></a><span data-ttu-id="c40a4-202">Esempi</span><span class="sxs-lookup"><span data-stu-id="c40a4-202">Samples</span></span>

### <a name="powershell-sample"></a><span data-ttu-id="c40a4-203">Esempio PowerShell</span><span class="sxs-lookup"><span data-stu-id="c40a4-203">PowerShell Sample</span></span> 

<span data-ttu-id="c40a4-204">Hello seguenti query di esempio hello servizio metadati per gli eventi pianificati e approva ogni evento in sospeso.</span><span class="sxs-lookup"><span data-stu-id="c40a4-204">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

```PowerShell
# How tooget scheduled events 
function GetScheduledEvents($uri)
{
    $scheduledEvents = Invoke-RestMethod -Headers @{"Metadata"="true"} -URI $uri -Method get
    $json = ConvertTo-Json $scheduledEvents
    Write-Host "Received following events: `n" $json
    return $scheduledEvents
}

# How tooapprove a scheduled event
function ApproveScheduledEvent($eventId, $docIncarnation, $uri)
{    
    # Create hello Scheduled Events Approval Document
    $startRequests = [array]@{"EventId" = $eventId}
    $scheduledEventsApproval = @{"StartRequests" = $startRequests; "DocumentIncarnation" = $docIncarnation} 
    
    # Convert tooJSON string
    $approvalString = ConvertTo-Json $scheduledEventsApproval

    Write-Host "Approving with hello following: `n" $approvalString

    # Post approval string tooscheduled events endpoint
    Invoke-RestMethod -Uri $uri -Headers @{"Metadata"="true"} -Method POST -Body $approvalString
}

function HandleScheduledEvents($scheduledEvents)
{
    # Add logic for handling events here
}

######### Sample Scheduled Events Interaction #########

# Set up hello scheduled events URI for a VNET-enabled VM
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


### <a name="c-sample"></a><span data-ttu-id="c40a4-205">Esempio C\#</span><span class="sxs-lookup"><span data-stu-id="c40a4-205">C\# Sample</span></span> 

<span data-ttu-id="c40a4-206">Hello esempio seguente è un semplice client che comunica con il servizio di metadati hello.</span><span class="sxs-lookup"><span data-stu-id="c40a4-206">hello following sample is of a simple client that communicates with hello metadata service.</span></span>

```csharp
public class ScheduledEventsClient
{
    private readonly string scheduledEventsEndpoint;
    private readonly string defaultIpAddress = "169.254.169.254"; 

    // Set up hello scheduled events URI for a VNET-enabled VM
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

<span data-ttu-id="c40a4-207">Gli eventi pianificati possono essere rappresentati mediante hello strutture di dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="c40a4-207">Scheduled Events can be represented using hello following data structures:</span></span>

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

<span data-ttu-id="c40a4-208">Hello seguenti query di esempio hello servizio metadati per gli eventi pianificati e approva ogni evento in sospeso.</span><span class="sxs-lookup"><span data-stu-id="c40a4-208">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

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
            Console.WriteLine("Press Enter tooapprove executing events\n");
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

            Console.WriteLine("Complete. Press enter toorepeat\n\n");
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

### <a name="python-sample"></a><span data-ttu-id="c40a4-209">Esempio Python</span><span class="sxs-lookup"><span data-stu-id="c40a4-209">Python Sample</span></span> 

<span data-ttu-id="c40a4-210">Hello seguenti query di esempio hello servizio metadati per gli eventi pianificati e approva ogni evento in sospeso.</span><span class="sxs-lookup"><span data-stu-id="c40a4-210">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="c40a4-211">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c40a4-211">Next Steps</span></span> 

- <span data-ttu-id="c40a4-212">Altre informazioni sulle API disponibili in hello hello [servizio metadati dell'istanza](virtual-machines-instancemetadataservice-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c40a4-212">Read more about hello APIs available in hello [instance metadata service](virtual-machines-instancemetadataservice-overview.md).</span></span>
- <span data-ttu-id="c40a4-213">Informazioni sulla [manutenzione pianificata per le macchine virtuali Windows in Azure](windows/planned-maintenance.md).</span><span class="sxs-lookup"><span data-stu-id="c40a4-213">Learn about [planned maintenance for Windows virtual machines in Azure](windows/planned-maintenance.md).</span></span>
- <span data-ttu-id="c40a4-214">Informazioni sulla [manutenzione pianificata per le macchine virtuali Linux in Azure](linux/planned-maintenance.md).</span><span class="sxs-lookup"><span data-stu-id="c40a4-214">Learn about [planned maintenance for Linux virtual machines in Azure](linux/planned-maintenance.md).</span></span>
