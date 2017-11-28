---
title: aaaBalance il cluster di Azure Service Fabric | Documenti Microsoft
description: Toobalancing un'introduzione del cluster con hello servizio di gestione delle risorse Cluster dell'infrastruttura.
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 030b1465-6616-4c0b-8bc7-24ed47d054c0
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 5f7ad2f5cf4cfb3751a860f5293b03d2d5266d99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="balancing-your-service-fabric-cluster"></a><span data-ttu-id="9d49c-103">Bilanciamento del carico nel cluster di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9d49c-103">Balancing your service fabric cluster</span></span>
<span data-ttu-id="9d49c-104">Hello gestione delle risorse Cluster di Service Fabric supporta modifiche al caricamento dinamico, reazione tooadditions o la rimozione di nodi o servizi.</span><span class="sxs-lookup"><span data-stu-id="9d49c-104">hello Service Fabric Cluster Resource Manager supports dynamic load changes, reacting tooadditions or removals of nodes or services.</span></span> <span data-ttu-id="9d49c-105">Corregge automaticamente anche le violazioni dei vincoli ed eseguito in modo proattivo il ribilanciamento cluster hello.</span><span class="sxs-lookup"><span data-stu-id="9d49c-105">It also automatically corrects constraint violations, and proactively rebalances hello cluster.</span></span> <span data-ttu-id="9d49c-106">Ma con quale frequenza vengono eseguite queste azioni, e che cosa le attiva?</span><span class="sxs-lookup"><span data-stu-id="9d49c-106">But how often are these actions taken, and what triggers them?</span></span>

<span data-ttu-id="9d49c-107">Sono disponibili tre diverse categorie di lavoro che hello esegue Gestione risorse di Cluster.</span><span class="sxs-lookup"><span data-stu-id="9d49c-107">There are three different categories of work that hello Cluster Resource Manager performs.</span></span> <span data-ttu-id="9d49c-108">Sono:</span><span class="sxs-lookup"><span data-stu-id="9d49c-108">They are:</span></span>

1. <span data-ttu-id="9d49c-109">Posizionamento: questa fase riguarda l'inserimento di repliche con stato o istanze senza stato mancanti.</span><span class="sxs-lookup"><span data-stu-id="9d49c-109">Placement – this stage deals with placing any stateful replicas or stateless instances that are missing.</span></span> <span data-ttu-id="9d49c-110">Il posizionamento include sia i nuovi servizi sia la gestione di repliche con stato o istanze senza stato non riuscite.</span><span class="sxs-lookup"><span data-stu-id="9d49c-110">Placement includes both new services and handling stateful replicas or stateless instances that have failed.</span></span> <span data-ttu-id="9d49c-111">In questa fase viene gestita l'eliminazione di istanze e repliche.</span><span class="sxs-lookup"><span data-stu-id="9d49c-111">Deleting and dropping replicas or instances are handled here.</span></span>
2. <span data-ttu-id="9d49c-112">Vincolo di verifica: questa fase controllate e corrette le violazioni dei vincoli di posizionamento diverse hello (regole) all'interno del sistema hello.</span><span class="sxs-lookup"><span data-stu-id="9d49c-112">Constraint Checks – this stage checks for and corrects violations of hello different placement constraints (rules) within hello system.</span></span> <span data-ttu-id="9d49c-113">Le regole servono, ad esempio, per controllare che i nodi non superino la capacità o che i vincoli di posizionamento di un servizio vengano rispettati.</span><span class="sxs-lookup"><span data-stu-id="9d49c-113">Examples of rules are things like ensuring that nodes are not over capacity and that a service’s placement constraints are met.</span></span>
3. <span data-ttu-id="9d49c-114">Bilanciamento del carico: questa fase controlla toosee se ribilanciamento è necessario in base a hello configurato desiderato a livello di bilanciamento per metriche.</span><span class="sxs-lookup"><span data-stu-id="9d49c-114">Balancing – this stage checks toosee if rebalancing is necessary based on hello configured desired level of balance for different metrics.</span></span> <span data-ttu-id="9d49c-115">In tal caso tenta toofind una disposizione in hello del cluster che è più bilanciato.</span><span class="sxs-lookup"><span data-stu-id="9d49c-115">If so it attempts toofind an arrangement in hello cluster that is more balanced.</span></span>

## <a name="configuring-cluster-resource-manager-timers"></a><span data-ttu-id="9d49c-116">Configurazione dei timer di Cluster Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9d49c-116">Configuring Cluster Resource Manager Timers</span></span>
<span data-ttu-id="9d49c-117">Hello primi dei controlli intorno a bilanciamento del carico sono un set di timer.</span><span class="sxs-lookup"><span data-stu-id="9d49c-117">hello first set of controls around balancing are a set of timers.</span></span> <span data-ttu-id="9d49c-118">Questi timer determinano la frequenza con cui hello gestione delle risorse Cluster esamina cluster hello e accetta le azioni correttive.</span><span class="sxs-lookup"><span data-stu-id="9d49c-118">These timers govern how often hello Cluster Resource Manager examines hello cluster and takes corrective actions.</span></span>

<span data-ttu-id="9d49c-119">Ognuno di questi tipi diversi di hello correzioni consentono di gestione delle risorse Cluster è controllato da un diverso timer che determina la frequenza.</span><span class="sxs-lookup"><span data-stu-id="9d49c-119">Each of these different types of corrections hello Cluster Resource Manager can make is controlled by a different timer that governs its frequency.</span></span> <span data-ttu-id="9d49c-120">Quando viene generato ogni timer, i hello è pianificata.</span><span class="sxs-lookup"><span data-stu-id="9d49c-120">When each timer fires, hello task is scheduled.</span></span> <span data-ttu-id="9d49c-121">Per impostazione predefinita hello Gestione risorse:</span><span class="sxs-lookup"><span data-stu-id="9d49c-121">By default hello Resource Manager:</span></span>

* <span data-ttu-id="9d49c-122">Analizza lo stato e applica gli aggiornamenti, ad esempio la registrazione di un nodo inattivo, ogni decimo di secondo.</span><span class="sxs-lookup"><span data-stu-id="9d49c-122">scans its state and applies updates (like recording that a node is down) every 1/10th of a second</span></span>
* <span data-ttu-id="9d49c-123">Imposta flag di controllo di selezione host hello</span><span class="sxs-lookup"><span data-stu-id="9d49c-123">sets hello placement check flag</span></span> 
* <span data-ttu-id="9d49c-124">Imposta flag di controllo di vincolo hello ogni secondo</span><span class="sxs-lookup"><span data-stu-id="9d49c-124">sets hello constraint check flag every second</span></span>
* <span data-ttu-id="9d49c-125">Imposta hello bilanciamento del carico flag ogni cinque secondi.</span><span class="sxs-lookup"><span data-stu-id="9d49c-125">sets hello balancing flag every five seconds.</span></span>

<span data-ttu-id="9d49c-126">Di seguito sono riportati esempi di configurazione di hello che governano questi timer:</span><span class="sxs-lookup"><span data-stu-id="9d49c-126">Examples of hello configuration governing these timers are below:</span></span>

<span data-ttu-id="9d49c-127">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="9d49c-127">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PLBRefreshGap" Value="0.1" />
            <Parameter Name="MinPlacementInterval" Value="1.0" />
            <Parameter Name="MinConstraintCheckInterval" Value="1.0" />
            <Parameter Name="MinLoadBalancingInterval" Value="5.0" />
        </Section>
```

<span data-ttu-id="9d49c-128">mediante ClusterConfig.json per le distribuzioni autonome o Template.json per i cluster ospitati in Azure:</span><span class="sxs-lookup"><span data-stu-id="9d49c-128">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "PLBRefreshGap",
          "value": "0.10"
      },
      {
          "name": "MinPlacementInterval",
          "value": "1.0"
      },
      {
          "name": "MinConstraintCheckInterval",
          "value": "1.0"
      },
      {
          "name": "MinLoadBalancingInterval",
          "value": "5.0"
      }
    ]
  }
]
```

<span data-ttu-id="9d49c-129">Oggi hello gestione delle risorse Cluster esegue solo una di queste azioni contemporaneamente, in modo sequenziale.</span><span class="sxs-lookup"><span data-stu-id="9d49c-129">Today hello Cluster Resource Manager only performs one of these actions at a time, sequentially.</span></span> <span data-ttu-id="9d49c-130">È per questo motivo è vedere timer toothese come "intervalli minimi" e hello azioni eseguite quando il timer di hello si trovi in come "impostazione flag" ottengano.</span><span class="sxs-lookup"><span data-stu-id="9d49c-130">This is why we refer toothese timers as “minimum intervals” and hello actions that get taken when hello timers go off as "setting flags".</span></span> <span data-ttu-id="9d49c-131">Hello occupa gestione delle risorse Cluster in sospeso, ad esempio, richiede i servizi di toocreate prima hello cluster di bilanciamento.</span><span class="sxs-lookup"><span data-stu-id="9d49c-131">For example, hello Cluster Resource Manager takes care of pending requests toocreate services before balancing hello cluster.</span></span> <span data-ttu-id="9d49c-132">Come si può notare da intervalli di tempo predefinito hello specificati, hello gestione delle risorse Cluster per qualsiasi elemento viene analizzato toodo esigenze di frequente.</span><span class="sxs-lookup"><span data-stu-id="9d49c-132">As you can see by hello default time intervals specified, hello Cluster Resource Manager scans for anything it needs toodo frequently.</span></span> <span data-ttu-id="9d49c-133">In genere, ciò significa che il set di hello delle modifiche apportate durante ogni passaggio è piccolo.</span><span class="sxs-lookup"><span data-stu-id="9d49c-133">Normally this means that hello set of changes made during each step is small.</span></span> <span data-ttu-id="9d49c-134">Apportare piccole modifiche spesso consente hello toobe di gestione delle risorse Cluster risponde quando si verificano eventi in cluster hello.</span><span class="sxs-lookup"><span data-stu-id="9d49c-134">Making small changes frequently allows hello Cluster Resource Manager toobe responsive when things happen in hello cluster.</span></span> <span data-ttu-id="9d49c-135">Hello timer predefiniti forniscono alcuni batch poiché molte delle hello stessi tipi di eventi tendono toooccur contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="9d49c-135">hello default timers provide some batching since many of hello same types of events tend toooccur simultaneously.</span></span> 

<span data-ttu-id="9d49c-136">Ad esempio, quando i nodi presentano errori possono procedere con interi domini di errore alla volta.</span><span class="sxs-lookup"><span data-stu-id="9d49c-136">For example, when nodes fail they can do so entire fault domains at a time.</span></span> <span data-ttu-id="9d49c-137">Tutti questi errori vengono acquisiti durante il successivo stato hello aggiornamento dopo hello *PLBRefreshGap*.</span><span class="sxs-lookup"><span data-stu-id="9d49c-137">All these failures are captured during hello next state update after hello *PLBRefreshGap*.</span></span> <span data-ttu-id="9d49c-138">correzioni di Hello vengono determinate durante hello dopo la selezione, controllo del vincolo e bilanciamento del carico viene eseguito.</span><span class="sxs-lookup"><span data-stu-id="9d49c-138">hello corrections are determined during hello following placement, constraint check, and balancing runs.</span></span> <span data-ttu-id="9d49c-139">Per hello predefinito gestione delle risorse Cluster è non l'analisi di ore di modifiche in cluster hello e tentativo tooaddress tutte le modifiche in una sola volta.</span><span class="sxs-lookup"><span data-stu-id="9d49c-139">By default hello Cluster Resource Manager is not scanning through hours of changes in hello cluster and trying tooaddress all changes at once.</span></span> <span data-ttu-id="9d49c-140">In questo modo potrebbe causare toobursts di varianza.</span><span class="sxs-lookup"><span data-stu-id="9d49c-140">Doing so would lead toobursts of churn.</span></span>

<span data-ttu-id="9d49c-141">Gestione delle risorse Cluster Hello deve inoltre toodetermine alcune informazioni aggiuntive se hello cluster sbilanciata.</span><span class="sxs-lookup"><span data-stu-id="9d49c-141">hello Cluster Resource Manager also needs some additional information toodetermine if hello cluster imbalanced.</span></span> <span data-ttu-id="9d49c-142">Per gestire questi aspetti sono disponibili due controlli di configurazione: le *soglie di bilanciamento* e le *soglie di attività*.</span><span class="sxs-lookup"><span data-stu-id="9d49c-142">For that we have two other pieces of configuration: *BalancingThresholds* and *ActivityThresholds*.</span></span>

## <a name="balancing-thresholds"></a><span data-ttu-id="9d49c-143">Soglie di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="9d49c-143">Balancing thresholds</span></span>
<span data-ttu-id="9d49c-144">Una soglia di bilanciamento del carico è controllo principale di hello per l'attivazione di ribilanciamento.</span><span class="sxs-lookup"><span data-stu-id="9d49c-144">A Balancing Threshold is hello main control for triggering rebalancing.</span></span> <span data-ttu-id="9d49c-145">Hello bilanciamento del carico di soglia per una metrica è un _rapporto_.</span><span class="sxs-lookup"><span data-stu-id="9d49c-145">hello Balancing Threshold for a metric is a _ratio_.</span></span> <span data-ttu-id="9d49c-146">Se il carico hello per una misurazione in hello caricato più nodo divisa per la quantità di hello di carico nel minor caricata hello nodo supera tale metrica *BalancingThreshold*, quindi cluster hello è bilanciato.</span><span class="sxs-lookup"><span data-stu-id="9d49c-146">If hello load for a metric on hello most loaded node divided by hello amount of load on hello least loaded node exceeds that metric's *BalancingThreshold*, then hello cluster is imbalanced.</span></span> <span data-ttu-id="9d49c-147">Di conseguenza bilanciamento del carico è hello ora successiva hello trigger Controlla gestione delle risorse Cluster.</span><span class="sxs-lookup"><span data-stu-id="9d49c-147">As a result balancing is triggered hello next time hello Cluster Resource Manager checks.</span></span> <span data-ttu-id="9d49c-148">Hello *MinLoadBalancingInterval* timer definisce con quale frequenza hello gestione delle risorse Cluster deve verificare se il ribilanciamento è necessario.</span><span class="sxs-lookup"><span data-stu-id="9d49c-148">hello *MinLoadBalancingInterval* timer defines how often hello Cluster Resource Manager should check if rebalancing is necessary.</span></span> <span data-ttu-id="9d49c-149">Controllare non comporta che venga eseguita un'operazione.</span><span class="sxs-lookup"><span data-stu-id="9d49c-149">Checking doesn't mean that anything happens.</span></span> 

<span data-ttu-id="9d49c-150">Soglie di bilanciamento del carico sono definite con cadenza per metriche come parte della definizione di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="9d49c-150">Balancing Thresholds are defined on a per-metric basis as a part of hello cluster definition.</span></span> <span data-ttu-id="9d49c-151">Per altre informazioni sulle metriche, vedere [questo articolo](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="9d49c-151">For more information on metrics, check out [this article](service-fabric-cluster-resource-manager-metrics.md).</span></span>

<span data-ttu-id="9d49c-152">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="9d49c-152">ClusterManifest.xml</span></span>

```xml
    <Section Name="MetricBalancingThresholds">
      <Parameter Name="MetricName1" Value="2"/>
      <Parameter Name="MetricName2" Value="3.5"/>
    </Section>
```

<span data-ttu-id="9d49c-153">mediante ClusterConfig.json per le distribuzioni autonome o Template.json per i cluster ospitati in Azure:</span><span class="sxs-lookup"><span data-stu-id="9d49c-153">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "MetricBalancingThresholds",
    "parameters": [
      {
          "name": "MetricName1",
          "value": "2"
      },
      {
          "name": "MetricName2",
          "value": "3.5"
      }
    ]
  }
]
```

<span data-ttu-id="9d49c-154"><center>
![Esempio di soglia di bilanciamento][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="9d49c-154"><center>
![Balancing Threshold Example][Image1]
</center></span></span>

<span data-ttu-id="9d49c-155">In questo esempio ogni servizio usa una unità di una metrica.</span><span class="sxs-lookup"><span data-stu-id="9d49c-155">In this example, each service is consuming one unit of some metric.</span></span> <span data-ttu-id="9d49c-156">Nell'esempio hello superiore hello del carico massimo in un nodo è cinque e minimo hello è due.</span><span class="sxs-lookup"><span data-stu-id="9d49c-156">In hello top example, hello maximum load on a node is five and hello minimum is two.</span></span> <span data-ttu-id="9d49c-157">Si supponga che hello bilanciamento del carico di soglia per questa metrica è tre.</span><span class="sxs-lookup"><span data-stu-id="9d49c-157">Let’s say that hello balancing threshold for this metric is three.</span></span> <span data-ttu-id="9d49c-158">Poiché il rapporto di hello cluster hello è 5/2 = 2.5 e che è inferiore a quello hello specificato soglia del cluster di tre, hello di bilanciamento del carico viene bilanciato.</span><span class="sxs-lookup"><span data-stu-id="9d49c-158">Since hello ratio in hello cluster is 5/2 = 2.5 and that is less than hello specified balancing threshold of three, hello cluster is balanced.</span></span> <span data-ttu-id="9d49c-159">Nessun bilanciamento del carico viene attivata quando verifica la gestione delle risorse Cluster hello.</span><span class="sxs-lookup"><span data-stu-id="9d49c-159">No balancing is triggered when hello Cluster Resource Manager checks.</span></span>

<span data-ttu-id="9d49c-160">Nell'esempio hello basso carico massimo di hello in un nodo è 10, mentre hello minimo è due, risultante in un rapporto di cinque.</span><span class="sxs-lookup"><span data-stu-id="9d49c-160">In hello bottom example, hello maximum load on a node is 10, while hello minimum is two, resulting in a ratio of five.</span></span> <span data-ttu-id="9d49c-161">Cinque è maggiore del valore soglia di bilanciamento del carico designato hello di tre per tale metrica.</span><span class="sxs-lookup"><span data-stu-id="9d49c-161">Five is greater than hello designated balancing threshold of three for that metric.</span></span> <span data-ttu-id="9d49c-162">Di conseguenza, esecuzione di un ribilanciamento sarà pianificato hello ora successiva bilanciamento del carico generato timer.</span><span class="sxs-lookup"><span data-stu-id="9d49c-162">As a result, a rebalancing run will be scheduled next time hello balancing timer fires.</span></span> <span data-ttu-id="9d49c-163">In una situazione simile al seguente parte del carico è in genere distribuite tooNode3.</span><span class="sxs-lookup"><span data-stu-id="9d49c-163">In a situation like this some load is usually distributed tooNode3.</span></span> <span data-ttu-id="9d49c-164">Perché hello servizio di gestione delle risorse Cluster dell'infrastruttura non utilizza un approccio greedy, potrebbe essere anche un carico tooNode2 distribuita.</span><span class="sxs-lookup"><span data-stu-id="9d49c-164">Because hello Service Fabric Cluster Resource Manager doesn't use a greedy approach, some load could also be distributed tooNode2.</span></span> 

<span data-ttu-id="9d49c-165"><center>
![Azioni sull'esempio di soglia di bilanciamento][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="9d49c-165"><center>
![Balancing Threshold Example Actions][Image2]
</center></span></span>

> [!NOTE]
> <span data-ttu-id="9d49c-166">Il "Bilanciamento" gestisce due diverse strategie per gestire il carico nel cluster.</span><span class="sxs-lookup"><span data-stu-id="9d49c-166">"Balancing" handles two different strategies for managing load in your cluster.</span></span> <span data-ttu-id="9d49c-167">strategia predefinita Hello hello Usa Gestione risorse di Cluster è toodistribute carico tra i nodi del cluster hello hello.</span><span class="sxs-lookup"><span data-stu-id="9d49c-167">hello default strategy that hello Cluster Resource Manager uses is toodistribute load across hello nodes in hello cluster.</span></span> <span data-ttu-id="9d49c-168">Hello altri strategia è [deframmentazione](service-fabric-cluster-resource-manager-defragmentation-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="9d49c-168">hello other strategy is [defragmentation](service-fabric-cluster-resource-manager-defragmentation-metrics.md).</span></span> <span data-ttu-id="9d49c-169">La deframmentazione viene eseguita durante hello stesso bilanciamento del carico di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="9d49c-169">Defragmentation is performed during hello same balancing run.</span></span> <span data-ttu-id="9d49c-170">Hello strategie di bilanciamento del carico e deframmentazione in linea possono essere utilizzate per le metriche diversi all'interno di hello dello stesso cluster.</span><span class="sxs-lookup"><span data-stu-id="9d49c-170">hello balancing and defragmentation strategies can be used for different metrics within hello same cluster.</span></span> <span data-ttu-id="9d49c-171">Un servizio può disporre di metriche di bilanciamento e di deframmentazione.</span><span class="sxs-lookup"><span data-stu-id="9d49c-171">A service can have both balancing and defragmentation metrics.</span></span> <span data-ttu-id="9d49c-172">Per la metrica di deframmentazione in linea, rapporto hello di hello carica nei trigger cluster hello in questo caso il ribilanciamento _seguito_ hello soglia di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="9d49c-172">For defragmentation metrics, hello ratio of hello loads in hello cluster triggers rebalancing when it is _below_ hello balancing threshold.</span></span> 
>

<span data-ttu-id="9d49c-173">Recupero seguito hello soglia di bilanciamento del carico non è un obiettivo esplicito.</span><span class="sxs-lookup"><span data-stu-id="9d49c-173">Getting below hello balancing threshold is not an explicit goal.</span></span> <span data-ttu-id="9d49c-174">Le soglie di bilanciamento sono semplicemente un *trigger*.</span><span class="sxs-lookup"><span data-stu-id="9d49c-174">Balancing Thresholds are just a *trigger*.</span></span> <span data-ttu-id="9d49c-175">Quando Bilanciamento del carico viene eseguito, hello gestione delle risorse Cluster determina quali miglioramenti rendere, se presente.</span><span class="sxs-lookup"><span data-stu-id="9d49c-175">When balancing runs, hello Cluster Resource Manager determines what improvements it can make, if any.</span></span> <span data-ttu-id="9d49c-176">Il fatto che venga avviata una ricerca di bilanciamento non significa che vengano spostati degli elementi.</span><span class="sxs-lookup"><span data-stu-id="9d49c-176">Just because a balancing search is kicked off doesn't mean anything moves.</span></span> <span data-ttu-id="9d49c-177">A volte hello cluster è toocorrect sbilanciata ma troppo limitata.</span><span class="sxs-lookup"><span data-stu-id="9d49c-177">Sometimes hello cluster is imbalanced but too constrained toocorrect.</span></span> <span data-ttu-id="9d49c-178">In alternativa, miglioramenti di hello richiedono i movimenti che sono troppo [costosi](service-fabric-cluster-resource-manager-movement-cost.md)).</span><span class="sxs-lookup"><span data-stu-id="9d49c-178">Alternatively, hello improvements require movements that are too [costly](service-fabric-cluster-resource-manager-movement-cost.md)).</span></span>

## <a name="activity-thresholds"></a><span data-ttu-id="9d49c-179">soglie di attività</span><span class="sxs-lookup"><span data-stu-id="9d49c-179">Activity thresholds</span></span>
<span data-ttu-id="9d49c-180">In alcuni casi, anche se i nodi sono relativamente sbilanciati, hello *totale* quantità di carico nel cluster hello è bassa.</span><span class="sxs-lookup"><span data-stu-id="9d49c-180">Sometimes, although nodes are relatively imbalanced, hello *total* amount of load in hello cluster is low.</span></span> <span data-ttu-id="9d49c-181">mancanza di Hello di carico può essere un dip temporaneo o perché cluster hello è nuovo e recupero appena avviato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="9d49c-181">hello lack of load could be a transient dip, or because hello cluster is new and just getting bootstrapped.</span></span> <span data-ttu-id="9d49c-182">In entrambi i casi, è opportuno non ora toospend hello cluster di bilanciamento perché è poco toobe acquisita.</span><span class="sxs-lookup"><span data-stu-id="9d49c-182">In either case, you may not want toospend time balancing hello cluster because there’s little toobe gained.</span></span> <span data-ttu-id="9d49c-183">Se il cluster hello sottoposti a bilanciamento del carico, si sarebbe spesa rete e risorse toomove diversi elementi di calcolo senza apportare qualsiasi grande *assoluto* differenza.</span><span class="sxs-lookup"><span data-stu-id="9d49c-183">If hello cluster underwent balancing, you’d spend network and compute resources toomove things around without making any large *absolute* difference.</span></span> <span data-ttu-id="9d49c-184">Sposta tooavoid non necessari, è noto come soglie di attività di un altro controllo.</span><span class="sxs-lookup"><span data-stu-id="9d49c-184">tooavoid unnecessary moves, there’s another control known as Activity Thresholds.</span></span> <span data-ttu-id="9d49c-185">Soglie di attività consente toospecify limite alcuni inferiore assoluto per l'attività.</span><span class="sxs-lookup"><span data-stu-id="9d49c-185">Activity Thresholds allows you toospecify some absolute lower bound for activity.</span></span> <span data-ttu-id="9d49c-186">Se nessun nodo oltre questa soglia, bilanciamento del carico non viene attivato anche se hello bilanciamento del carico viene raggiunta la soglia.</span><span class="sxs-lookup"><span data-stu-id="9d49c-186">If no node is over this threshold, balancing isn't triggered even if hello Balancing Threshold is met.</span></span>

<span data-ttu-id="9d49c-187">Si supponga che abbiamo mantenuto la soglia di bilanciamento su tre per questa metrica.</span><span class="sxs-lookup"><span data-stu-id="9d49c-187">Let’s say that we retain our Balancing Threshold of three for this metric.</span></span> <span data-ttu-id="9d49c-188">Si supponga anche che sia disponibile una Soglia di attività di 1536.</span><span class="sxs-lookup"><span data-stu-id="9d49c-188">Let's also say we have an Activity Threshold of 1536.</span></span> <span data-ttu-id="9d49c-189">Nel primo caso hello, mentre il cluster hello è bilanciato per hello bilanciamento del carico di soglia sono soddisfa alcun nodo tale soglia di attività è avviene quindi alcuna operazione.</span><span class="sxs-lookup"><span data-stu-id="9d49c-189">In hello first case, while hello cluster is imbalanced per hello Balancing Threshold there's no node meets that Activity Threshold, so nothing happens.</span></span> <span data-ttu-id="9d49c-190">Nell'esempio hello inferiore Node1 è su hello soglia di attività.</span><span class="sxs-lookup"><span data-stu-id="9d49c-190">In hello bottom example, Node1 is over hello Activity Threshold.</span></span> <span data-ttu-id="9d49c-191">Poiché entrambi hello soglia di bilanciamento del carico e hello soglia di attività per la metrica hello vengono superate, bilanciamento del carico è pianificata.</span><span class="sxs-lookup"><span data-stu-id="9d49c-191">Since both hello Balancing Threshold and hello Activity Threshold for hello metric are exceeded, balancing is scheduled.</span></span> <span data-ttu-id="9d49c-192">Ad esempio, si esaminerà hello seguente diagramma:</span><span class="sxs-lookup"><span data-stu-id="9d49c-192">As an example, let's look at hello following diagram:</span></span> 

<span data-ttu-id="9d49c-193"><center>
![Esempio di soglia di attività][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="9d49c-193"><center>
![Activity Threshold Example][Image3]
</center></span></span>

<span data-ttu-id="9d49c-194">Analogamente alle soglie di bilanciamento del carico, le soglie di attività sono definiti per ogni metrica tramite la definizione del cluster di hello:</span><span class="sxs-lookup"><span data-stu-id="9d49c-194">Just like Balancing Thresholds, Activity Thresholds are defined per-metric via hello cluster definition:</span></span>

<span data-ttu-id="9d49c-195">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="9d49c-195">ClusterManifest.xml</span></span>

``` xml
    <Section Name="MetricActivityThresholds">
      <Parameter Name="Memory" Value="1536"/>
    </Section>
```

<span data-ttu-id="9d49c-196">mediante ClusterConfig.json per le distribuzioni autonome o Template.json per i cluster ospitati in Azure:</span><span class="sxs-lookup"><span data-stu-id="9d49c-196">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "MetricActivityThresholds",
    "parameters": [
      {
          "name": "Memory",
          "value": "1536"
      }
    ]
  }
]
```

<span data-ttu-id="9d49c-197">Soglie di bilanciamento carico di rete e attività sono entrambi legati tooa metrica specifica - bilanciamento del carico viene generato solo se entrambi hello soglia di bilanciamento del carico e viene superata la soglia di attività per hello stessa metrica.</span><span class="sxs-lookup"><span data-stu-id="9d49c-197">Balancing and activity thresholds are both tied tooa specific metric - balancing is triggered only if both hello Balancing Threshold and Activity Threshold is exceeded for hello same metric.</span></span>

## <a name="balancing-services-together"></a><span data-ttu-id="9d49c-198">Bilanciamento composto dei servizi</span><span class="sxs-lookup"><span data-stu-id="9d49c-198">Balancing services together</span></span>
<span data-ttu-id="9d49c-199">Se non è bilanciato cluster hello o non è una decisione a livello di cluster.</span><span class="sxs-lookup"><span data-stu-id="9d49c-199">Whether hello cluster is imbalanced or not is a cluster-wide decision.</span></span> <span data-ttu-id="9d49c-200">È tuttavia modo hello passiamo su correggerlo lo spostamento repliche singolo servizio e le istanze.</span><span class="sxs-lookup"><span data-stu-id="9d49c-200">However, hello way we go about fixing it is moving individual service replicas and instances around.</span></span> <span data-ttu-id="9d49c-201">Questo approccio ha senso, giusto?</span><span class="sxs-lookup"><span data-stu-id="9d49c-201">This makes sense, right?</span></span> <span data-ttu-id="9d49c-202">Se aggiunti allo stack memoria in un nodo, più repliche o istanze potrebbero contribuire tooit.</span><span class="sxs-lookup"><span data-stu-id="9d49c-202">If memory is stacked up on one node, multiple replicas or instances could be contributing tooit.</span></span> <span data-ttu-id="9d49c-203">Correzione sbilanciamento hello potrebbe richiedere lo spostamento di una delle repliche con stato hello o istanze senza state che utilizzano metrica sbilanciata hello.</span><span class="sxs-lookup"><span data-stu-id="9d49c-203">Fixing hello imbalance could require moving any of hello stateful replicas or stateless instances that use hello imbalanced metric.</span></span>

<span data-ttu-id="9d49c-204">In alcuni casi però viene spostato un servizio che non era stesso sbilanciata (a questo proposito hello locale e globale pesi in precedenza).</span><span class="sxs-lookup"><span data-stu-id="9d49c-204">Occasionally though, a service that wasn’t itself imbalanced gets moved (remember hello discussion of local and global weights earlier).</span></span> <span data-ttu-id="9d49c-205">Per quale motivo si dovrebbe spostare un servizio quando tutte le metriche di quel servizio sono state bilanciate?</span><span class="sxs-lookup"><span data-stu-id="9d49c-205">Why would a service get moved when all that service’s metrics were balanced?</span></span> <span data-ttu-id="9d49c-206">Di seguito viene illustrato un esempio:</span><span class="sxs-lookup"><span data-stu-id="9d49c-206">Let’s see an example:</span></span>

- <span data-ttu-id="9d49c-207">Si supponga di avere quattro servizi: Service1, Service2, Service3 e Service4.</span><span class="sxs-lookup"><span data-stu-id="9d49c-207">Let's say there are four services, Service1, Service2, Service3, and Service4.</span></span> 
- <span data-ttu-id="9d49c-208">Service1 riporta le metriche Metric1 e Metric2.</span><span class="sxs-lookup"><span data-stu-id="9d49c-208">Service1 reports metrics Metric1 and Metric2.</span></span> 
- <span data-ttu-id="9d49c-209">Service2 riporta le metriche Metric2 e Metric3.</span><span class="sxs-lookup"><span data-stu-id="9d49c-209">Service2 reports metrics Metric2 and Metric3.</span></span> 
- <span data-ttu-id="9d49c-210">Service3 riporta le metriche Metric3 e Metric4.</span><span class="sxs-lookup"><span data-stu-id="9d49c-210">Service3 reports metrics Metric3 and Metric4.</span></span>
- <span data-ttu-id="9d49c-211">Service4 riporta la metrica Metric99.</span><span class="sxs-lookup"><span data-stu-id="9d49c-211">Service4 reports metric Metric99.</span></span> 

<span data-ttu-id="9d49c-212">Sicuramente è già possibile intravedere una spiegazione: la catena.</span><span class="sxs-lookup"><span data-stu-id="9d49c-212">Surely you can see where we’re going here: There's a chain!</span></span> <span data-ttu-id="9d49c-213">Non ci sono quattro servizi indipendenti, ma tre servizi correlati tra loro e uno autonomo.</span><span class="sxs-lookup"><span data-stu-id="9d49c-213">We don’t really have four independent services, we have three services that are related and one that is off on its own.</span></span>

<span data-ttu-id="9d49c-214"><center>
![Bilanciamento composto dei servizi][Image4]
</center></span><span class="sxs-lookup"><span data-stu-id="9d49c-214"><center>
![Balancing Services Together][Image4]
</center></span></span>

<span data-ttu-id="9d49c-215">A causa di questa catena, è possibile che uno squilibrio nelle metriche 1-4 può causare le repliche o le istanze appartenenti tooservices 1-3 toomove intorno.</span><span class="sxs-lookup"><span data-stu-id="9d49c-215">Because of this chain, it's possible that an imbalance in metrics 1-4 can cause replicas or instances belonging tooservices 1-3 toomove around.</span></span> <span data-ttu-id="9d49c-216">Sappiamo anche che uno sbilanciamento delle metriche 1, 2 o 3 non può comportare movimenti in Service4.</span><span class="sxs-lookup"><span data-stu-id="9d49c-216">We also know that an imbalance in Metrics 1, 2, or 3 can't cause movements in Service4.</span></span> <span data-ttu-id="9d49c-217">Non vi sarà alcun punto dopo lo spostamento le repliche hello o le istanze appartenenti tooService4 intorno può assolutamente nessun saldo hello tooimpact delle metriche 1-3.</span><span class="sxs-lookup"><span data-stu-id="9d49c-217">There would be no point since moving hello replicas or instances belonging tooService4 around can do absolutely nothing tooimpact hello balance of Metrics 1-3.</span></span>

<span data-ttu-id="9d49c-218">Hello gestione delle risorse Cluster determina automaticamente i servizi correlati.</span><span class="sxs-lookup"><span data-stu-id="9d49c-218">hello Cluster Resource Manager automatically figures out what services are related.</span></span> <span data-ttu-id="9d49c-219">Aggiunta, rimozione o modifica le metriche di hello per i servizi possono influire sulle relative relazioni.</span><span class="sxs-lookup"><span data-stu-id="9d49c-219">Adding, removing, or changing hello metrics for services can impact their relationships.</span></span> <span data-ttu-id="9d49c-220">Ad esempio, tra due esecuzioni del bilanciamento del carico Service2 potrebbe essere stato aggiornato tooremove Metric2.</span><span class="sxs-lookup"><span data-stu-id="9d49c-220">For example, between two runs of balancing Service2 may have been updated tooremove Metric2.</span></span> <span data-ttu-id="9d49c-221">Viene interrotta la catena di hello tra Service1 e Service2.</span><span class="sxs-lookup"><span data-stu-id="9d49c-221">This breaks hello chain between Service1 and Service2.</span></span> <span data-ttu-id="9d49c-222">Ora, invece di due gruppi di servizi correlati ce ne sono tre:</span><span class="sxs-lookup"><span data-stu-id="9d49c-222">Now instead of two groups of related services, there are three:</span></span>

<span data-ttu-id="9d49c-223"><center>
![Bilanciamento composto dei servizi][Image5]
</center></span><span class="sxs-lookup"><span data-stu-id="9d49c-223"><center>
![Balancing Services Together][Image5]
</center></span></span>

## <a name="next-steps"></a><span data-ttu-id="9d49c-224">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9d49c-224">Next steps</span></span>
* <span data-ttu-id="9d49c-225">Le metriche sono la modalità di gestione di consumo e la capacità in cluster hello in hello gestore di risorse Cluster dell'infrastruttura del servizio.</span><span class="sxs-lookup"><span data-stu-id="9d49c-225">Metrics are how hello Service Fabric Cluster Resource Manger manages consumption and capacity in hello cluster.</span></span> <span data-ttu-id="9d49c-226">ulteriori informazioni sulle metriche toolearn come tooconfigure, archiviazione ed estrazione [in questo articolo](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="9d49c-226">toolearn more about metrics and how tooconfigure them, check out [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>
* <span data-ttu-id="9d49c-227">Il costo dello spostamento è un modo di segnalazione toohello gestione delle risorse Cluster che alcuni servizi siano toomove più costosi rispetto ad altri.</span><span class="sxs-lookup"><span data-stu-id="9d49c-227">Movement Cost is one way of signaling toohello Cluster Resource Manager that certain services are more expensive toomove than others.</span></span> <span data-ttu-id="9d49c-228">Per ulteriori informazioni sul costo di spostamento, fare riferimento troppo[in questo articolo](service-fabric-cluster-resource-manager-movement-cost.md)</span><span class="sxs-lookup"><span data-stu-id="9d49c-228">For more about movement cost, refer too[this article](service-fabric-cluster-resource-manager-movement-cost.md)</span></span>
* <span data-ttu-id="9d49c-229">Hello gestione delle risorse Cluster ha le limitazioni diversi che è possibile configurare tooslow verso il basso la varianza del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="9d49c-229">hello Cluster Resource Manager has several throttles that you can configure tooslow down churn in hello cluster.</span></span> <span data-ttu-id="9d49c-230">Queste limitazioni non sono in genere necessarie, ma sono eventualmente disponibili altre informazioni [qui](service-fabric-cluster-resource-manager-advanced-throttling.md)</span><span class="sxs-lookup"><span data-stu-id="9d49c-230">They're not normally necessary, but if you need them you can learn about them [here](service-fabric-cluster-resource-manager-advanced-throttling.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resrouce-manager-balancing-thresholds.png
[Image2]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-threshold-triggered-results.png
[Image3]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-activity-thresholds.png
[Image4]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together1.png
[Image5]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together2.png
