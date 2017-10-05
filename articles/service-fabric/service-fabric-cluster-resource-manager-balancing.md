---
title: Bilanciare il carico del cluster di Azure Service Fabric | Documentazione Microsoft
description: Introduzione al bilanciamento del carico del cluster con Cluster Resource Manager di Service Fabric.
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
ms.openlocfilehash: 34eacb29f324025c1d2803c9690600227d3ec457
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="balancing-your-service-fabric-cluster"></a><span data-ttu-id="25d7c-103">Bilanciamento del carico nel cluster di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="25d7c-103">Balancing your service fabric cluster</span></span>
<span data-ttu-id="25d7c-104">Cluster Resource Manager di Service Fabric supporta le modifiche al carico dinamico, reagisce all'aggiunta o alla rimozione di nodi o servizi.</span><span class="sxs-lookup"><span data-stu-id="25d7c-104">The Service Fabric Cluster Resource Manager supports dynamic load changes, reacting to additions or removals of nodes or services.</span></span> <span data-ttu-id="25d7c-105">Corregge anche automaticamente le violazioni dei vincoli ed esegue in modo proattivo il ribilanciamento del cluster.</span><span class="sxs-lookup"><span data-stu-id="25d7c-105">It also automatically corrects constraint violations, and proactively rebalances the cluster.</span></span> <span data-ttu-id="25d7c-106">Ma con quale frequenza vengono eseguite queste azioni, e che cosa le attiva?</span><span class="sxs-lookup"><span data-stu-id="25d7c-106">But how often are these actions taken, and what triggers them?</span></span>

<span data-ttu-id="25d7c-107">Sono disponibili tre diverse categorie di lavoro eseguite da Cluster. Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="25d7c-107">There are three different categories of work that the Cluster Resource Manager performs.</span></span> <span data-ttu-id="25d7c-108">Sono:</span><span class="sxs-lookup"><span data-stu-id="25d7c-108">They are:</span></span>

1. <span data-ttu-id="25d7c-109">Posizionamento: questa fase riguarda l'inserimento di repliche con stato o istanze senza stato mancanti.</span><span class="sxs-lookup"><span data-stu-id="25d7c-109">Placement – this stage deals with placing any stateful replicas or stateless instances that are missing.</span></span> <span data-ttu-id="25d7c-110">Il posizionamento include sia i nuovi servizi sia la gestione di repliche con stato o istanze senza stato non riuscite.</span><span class="sxs-lookup"><span data-stu-id="25d7c-110">Placement includes both new services and handling stateful replicas or stateless instances that have failed.</span></span> <span data-ttu-id="25d7c-111">In questa fase viene gestita l'eliminazione di istanze e repliche.</span><span class="sxs-lookup"><span data-stu-id="25d7c-111">Deleting and dropping replicas or instances are handled here.</span></span>
2. <span data-ttu-id="25d7c-112">Verifiche dei vincoli: in questa fase vengono controllate e corrette le violazioni dei vincoli (regole) di posizionamento all'interno del sistema.</span><span class="sxs-lookup"><span data-stu-id="25d7c-112">Constraint Checks – this stage checks for and corrects violations of the different placement constraints (rules) within the system.</span></span> <span data-ttu-id="25d7c-113">Le regole servono, ad esempio, per controllare che i nodi non superino la capacità o che i vincoli di posizionamento di un servizio vengano rispettati.</span><span class="sxs-lookup"><span data-stu-id="25d7c-113">Examples of rules are things like ensuring that nodes are not over capacity and that a service’s placement constraints are met.</span></span>
3. <span data-ttu-id="25d7c-114">Bilanciamento del carico: in questa fase viene verificata la necessità di applicare il ribilanciamento sulla base del livello di bilanciamento configurato per le diverse metriche.</span><span class="sxs-lookup"><span data-stu-id="25d7c-114">Balancing – this stage checks to see if rebalancing is necessary based on the configured desired level of balance for different metrics.</span></span> <span data-ttu-id="25d7c-115">In tal caso, viene eseguito il tentativo di trovare una disposizione più bilanciata nel cluster.</span><span class="sxs-lookup"><span data-stu-id="25d7c-115">If so it attempts to find an arrangement in the cluster that is more balanced.</span></span>

## <a name="configuring-cluster-resource-manager-timers"></a><span data-ttu-id="25d7c-116">Configurazione dei timer di Cluster Resource Manager</span><span class="sxs-lookup"><span data-stu-id="25d7c-116">Configuring Cluster Resource Manager Timers</span></span>
<span data-ttu-id="25d7c-117">Il primo set di controlli sul bilanciamento del carico sono un set di timer.</span><span class="sxs-lookup"><span data-stu-id="25d7c-117">The first set of controls around balancing are a set of timers.</span></span> <span data-ttu-id="25d7c-118">Questi timer controllano la frequenza con cui Cluster Resource Manager esamina il cluster e intraprende le azioni correttive.</span><span class="sxs-lookup"><span data-stu-id="25d7c-118">These timers govern how often the Cluster Resource Manager examines the cluster and takes corrective actions.</span></span>

<span data-ttu-id="25d7c-119">Ognuno dei tipi diversi di correzioni che Cluster Resource Manager può apportare è controllato da un timer diverso che ne determina la frequenza.</span><span class="sxs-lookup"><span data-stu-id="25d7c-119">Each of these different types of corrections the Cluster Resource Manager can make is controlled by a different timer that governs its frequency.</span></span> <span data-ttu-id="25d7c-120">Quando viene attivato ogni timer, l'attività viene pianificata.</span><span class="sxs-lookup"><span data-stu-id="25d7c-120">When each timer fires, the task is scheduled.</span></span> <span data-ttu-id="25d7c-121">Per impostazione predefinita, Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="25d7c-121">By default the Resource Manager:</span></span>

* <span data-ttu-id="25d7c-122">Analizza lo stato e applica gli aggiornamenti, ad esempio la registrazione di un nodo inattivo, ogni decimo di secondo.</span><span class="sxs-lookup"><span data-stu-id="25d7c-122">scans its state and applies updates (like recording that a node is down) every 1/10th of a second</span></span>
* <span data-ttu-id="25d7c-123">imposta il flag di controllo di selezione</span><span class="sxs-lookup"><span data-stu-id="25d7c-123">sets the placement check flag</span></span> 
* <span data-ttu-id="25d7c-124">imposta il flag di controllo del vincolo ogni secondo</span><span class="sxs-lookup"><span data-stu-id="25d7c-124">sets the constraint check flag every second</span></span>
* <span data-ttu-id="25d7c-125">Imposta il flag di bilanciamento ogni cinque secondi.</span><span class="sxs-lookup"><span data-stu-id="25d7c-125">sets the balancing flag every five seconds.</span></span>

<span data-ttu-id="25d7c-126">Di seguito sono riportati alcuni esempi di configurazione che controllano i timer:</span><span class="sxs-lookup"><span data-stu-id="25d7c-126">Examples of the configuration governing these timers are below:</span></span>

<span data-ttu-id="25d7c-127">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="25d7c-127">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PLBRefreshGap" Value="0.1" />
            <Parameter Name="MinPlacementInterval" Value="1.0" />
            <Parameter Name="MinConstraintCheckInterval" Value="1.0" />
            <Parameter Name="MinLoadBalancingInterval" Value="5.0" />
        </Section>
```

<span data-ttu-id="25d7c-128">mediante ClusterConfig.json per le distribuzioni autonome o Template.json per i cluster ospitati in Azure:</span><span class="sxs-lookup"><span data-stu-id="25d7c-128">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="25d7c-129">Oggi Cluster Resource Manager esegue solo una di queste azioni alla volta, in sequenza.</span><span class="sxs-lookup"><span data-stu-id="25d7c-129">Today the Cluster Resource Manager only performs one of these actions at a time, sequentially.</span></span> <span data-ttu-id="25d7c-130">Questo è il motivo per cui si fa riferimento a questi timer come "intervalli minimi" e le azioni che vengono eseguite quando il timer viene spente come "flag di impostazione".</span><span class="sxs-lookup"><span data-stu-id="25d7c-130">This is why we refer to these timers as “minimum intervals” and the actions that get taken when the timers go off as "setting flags".</span></span> <span data-ttu-id="25d7c-131">Ad esempio, Cluster Resource Manager si occupa delle richieste di creazione di servizi in sospeso prima di bilanciare il carico del cluster.</span><span class="sxs-lookup"><span data-stu-id="25d7c-131">For example, the Cluster Resource Manager takes care of pending requests to create services before balancing the cluster.</span></span> <span data-ttu-id="25d7c-132">Come si nota dagli intervalli di tempo predefiniti specificati, Cluster Resource Manager analizza di frequente tutte le attività.</span><span class="sxs-lookup"><span data-stu-id="25d7c-132">As you can see by the default time intervals specified, the Cluster Resource Manager scans for anything it needs to do frequently.</span></span> <span data-ttu-id="25d7c-133">In genere, ciò significa che il set di modifiche apportate durante ogni passaggio è piccolo.</span><span class="sxs-lookup"><span data-stu-id="25d7c-133">Normally this means that the set of changes made during each step is small.</span></span> <span data-ttu-id="25d7c-134">Le modifiche piccole e frequenti consentono a Cluster Resource Manager di essere sensibile quando ciò si verifica nel cluster.</span><span class="sxs-lookup"><span data-stu-id="25d7c-134">Making small changes frequently allows the Cluster Resource Manager to be responsive when things happen in the cluster.</span></span> <span data-ttu-id="25d7c-135">I timer predefiniti eseguono una sorta di divisione in batch, dato che molti degli eventi dello stesso tipo tendono a verificarsi simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="25d7c-135">The default timers provide some batching since many of the same types of events tend to occur simultaneously.</span></span> 

<span data-ttu-id="25d7c-136">Ad esempio, quando i nodi presentano errori possono procedere con interi domini di errore alla volta.</span><span class="sxs-lookup"><span data-stu-id="25d7c-136">For example, when nodes fail they can do so entire fault domains at a time.</span></span> <span data-ttu-id="25d7c-137">Tutti questi errori vengono acquisiti durante il successivo aggiornamento dopo il *PLBRefreshGap*.</span><span class="sxs-lookup"><span data-stu-id="25d7c-137">All these failures are captured during the next state update after the *PLBRefreshGap*.</span></span> <span data-ttu-id="25d7c-138">Le correzioni vengono determinate durante il posizionamento seguente del controllo del vincolo, e bilanciamento del carico viene eseguito.</span><span class="sxs-lookup"><span data-stu-id="25d7c-138">The corrections are determined during the following placement, constraint check, and balancing runs.</span></span> <span data-ttu-id="25d7c-139">Per impostazione predefinita, Cluster Resource Manager non analizza ore di modifiche nel cluster e non tenta di risolvere tutte le modifiche in una sola volta.</span><span class="sxs-lookup"><span data-stu-id="25d7c-139">By default the Cluster Resource Manager is not scanning through hours of changes in the cluster and trying to address all changes at once.</span></span> <span data-ttu-id="25d7c-140">Questo potrebbe generare burst di varianza.</span><span class="sxs-lookup"><span data-stu-id="25d7c-140">Doing so would lead to bursts of churn.</span></span>

<span data-ttu-id="25d7c-141">Cluster Resource Manager necessita di informazioni aggiuntive per determinare se il cluster è sbilanciato.</span><span class="sxs-lookup"><span data-stu-id="25d7c-141">The Cluster Resource Manager also needs some additional information to determine if the cluster imbalanced.</span></span> <span data-ttu-id="25d7c-142">Per gestire questi aspetti sono disponibili due controlli di configurazione: le *soglie di bilanciamento* e le *soglie di attività*.</span><span class="sxs-lookup"><span data-stu-id="25d7c-142">For that we have two other pieces of configuration: *BalancingThresholds* and *ActivityThresholds*.</span></span>

## <a name="balancing-thresholds"></a><span data-ttu-id="25d7c-143">Soglie di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="25d7c-143">Balancing thresholds</span></span>
<span data-ttu-id="25d7c-144">Una soglia di bilanciamento del carico è il controllo principale per attivare il ribilanciamento.</span><span class="sxs-lookup"><span data-stu-id="25d7c-144">A Balancing Threshold is the main control for triggering rebalancing.</span></span> <span data-ttu-id="25d7c-145">La soglia di bilanciamento del carico per una metrica è espressa con un _rapporto_.</span><span class="sxs-lookup"><span data-stu-id="25d7c-145">The Balancing Threshold for a metric is a _ratio_.</span></span> <span data-ttu-id="25d7c-146">Se il volume di carico sul nodo più carico diviso per il volume di carico sul nodo meno carico supera il *BalancingThreshold*della metrica, il cluster viene considerato sbilanciato.</span><span class="sxs-lookup"><span data-stu-id="25d7c-146">If the load for a metric on the most loaded node divided by the amount of load on the least loaded node exceeds that metric's *BalancingThreshold*, then the cluster is imbalanced.</span></span> <span data-ttu-id="25d7c-147">In tal caso, al successivo controllo di Cluster Resource Manager viene attivato il bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="25d7c-147">As a result balancing is triggered the next time the Cluster Resource Manager checks.</span></span> <span data-ttu-id="25d7c-148">Il timer *MinLoadBalancingInterval* definisce la frequenza dei controlli eseguiti da Cluster Resource Manager se è necessario il ribilanciamento.</span><span class="sxs-lookup"><span data-stu-id="25d7c-148">The *MinLoadBalancingInterval* timer defines how often the Cluster Resource Manager should check if rebalancing is necessary.</span></span> <span data-ttu-id="25d7c-149">Controllare non comporta che venga eseguita un'operazione.</span><span class="sxs-lookup"><span data-stu-id="25d7c-149">Checking doesn't mean that anything happens.</span></span> 

<span data-ttu-id="25d7c-150">Le soglie di bilanciamento del carico sono definite sulla base delle singole metriche nell'ambito della definizione del cluster.</span><span class="sxs-lookup"><span data-stu-id="25d7c-150">Balancing Thresholds are defined on a per-metric basis as a part of the cluster definition.</span></span> <span data-ttu-id="25d7c-151">Per altre informazioni sulle metriche, vedere [questo articolo](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="25d7c-151">For more information on metrics, check out [this article](service-fabric-cluster-resource-manager-metrics.md).</span></span>

<span data-ttu-id="25d7c-152">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="25d7c-152">ClusterManifest.xml</span></span>

```xml
    <Section Name="MetricBalancingThresholds">
      <Parameter Name="MetricName1" Value="2"/>
      <Parameter Name="MetricName2" Value="3.5"/>
    </Section>
```

<span data-ttu-id="25d7c-153">mediante ClusterConfig.json per le distribuzioni autonome o Template.json per i cluster ospitati in Azure:</span><span class="sxs-lookup"><span data-stu-id="25d7c-153">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="25d7c-154"><center>
![Esempio di soglia di bilanciamento][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="25d7c-154"><center>
![Balancing Threshold Example][Image1]
</center></span></span>

<span data-ttu-id="25d7c-155">In questo esempio ogni servizio usa una unità di una metrica.</span><span class="sxs-lookup"><span data-stu-id="25d7c-155">In this example, each service is consuming one unit of some metric.</span></span> <span data-ttu-id="25d7c-156">Nell'esempio in alto il carico massimo su un nodo è cinque e il carico minimo è due.</span><span class="sxs-lookup"><span data-stu-id="25d7c-156">In the top example, the maximum load on a node is five and the minimum is two.</span></span> <span data-ttu-id="25d7c-157">Si supponga che la soglia di bilanciamento del carico per questa metrica sia tre.</span><span class="sxs-lookup"><span data-stu-id="25d7c-157">Let’s say that the balancing threshold for this metric is three.</span></span> <span data-ttu-id="25d7c-158">Dato che il rapporto nel cluster è 5/2 = 2,5 e che tale cifra è inferiore al valore tre della soglia di bilanciamento, il cluster è bilanciato.</span><span class="sxs-lookup"><span data-stu-id="25d7c-158">Since the ratio in the cluster is 5/2 = 2.5 and that is less than the specified balancing threshold of three, the cluster is balanced.</span></span> <span data-ttu-id="25d7c-159">In tal caso, al successivo controllo di Cluster Resource Manager non viene attivato alcun bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="25d7c-159">No balancing is triggered when the Cluster Resource Manager checks.</span></span>

<span data-ttu-id="25d7c-160">Nell'esempio in basso il carico massimo su un nodo è 10, mentre il carico minimo è due. Il rapporto è quindi pari a cinque.</span><span class="sxs-lookup"><span data-stu-id="25d7c-160">In the bottom example, the maximum load on a node is 10, while the minimum is two, resulting in a ratio of five.</span></span> <span data-ttu-id="25d7c-161">Cinque è superiore alla soglia di bilanciamento del carico designata di tre per tale metrica.</span><span class="sxs-lookup"><span data-stu-id="25d7c-161">Five is greater than the designated balancing threshold of three for that metric.</span></span> <span data-ttu-id="25d7c-162">Di conseguenza, all'attivazione successiva del timer di bilanciamento del carico verrà pianificato un ribilanciamento.</span><span class="sxs-lookup"><span data-stu-id="25d7c-162">As a result, a rebalancing run will be scheduled next time the balancing timer fires.</span></span> <span data-ttu-id="25d7c-163">In una situazione come questa, parte del carico viene in genere distribuito nel nodo 3.</span><span class="sxs-lookup"><span data-stu-id="25d7c-163">In a situation like this some load is usually distributed to Node3.</span></span> <span data-ttu-id="25d7c-164">Poiché Cluster Resource Manager di Service Fabric non usa un approccio greedy, parte del carico potrebbe essere distribuita anche nel nodo 2.</span><span class="sxs-lookup"><span data-stu-id="25d7c-164">Because the Service Fabric Cluster Resource Manager doesn't use a greedy approach, some load could also be distributed to Node2.</span></span> 

<span data-ttu-id="25d7c-165"><center>
![Azioni sull'esempio di soglia di bilanciamento][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="25d7c-165"><center>
![Balancing Threshold Example Actions][Image2]
</center></span></span>

> [!NOTE]
> <span data-ttu-id="25d7c-166">Il "Bilanciamento" gestisce due diverse strategie per gestire il carico nel cluster.</span><span class="sxs-lookup"><span data-stu-id="25d7c-166">"Balancing" handles two different strategies for managing load in your cluster.</span></span> <span data-ttu-id="25d7c-167">La strategia predefinita usata da Cluster Resource Manager consiste nel distribuire il carico tra i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="25d7c-167">The default strategy that the Cluster Resource Manager uses is to distribute load across the nodes in the cluster.</span></span> <span data-ttu-id="25d7c-168">L'altra strategia è la [deframmentazione](service-fabric-cluster-resource-manager-defragmentation-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="25d7c-168">The other strategy is [defragmentation](service-fabric-cluster-resource-manager-defragmentation-metrics.md).</span></span> <span data-ttu-id="25d7c-169">La deframmentazione viene eseguita durante l'esecuzione dello stesso bilanciamento.</span><span class="sxs-lookup"><span data-stu-id="25d7c-169">Defragmentation is performed during the same balancing run.</span></span> <span data-ttu-id="25d7c-170">Le strategie di bilanciamento e deframmentazione possono essere usate per metriche diverse all'interno dello stesso cluster.</span><span class="sxs-lookup"><span data-stu-id="25d7c-170">The balancing and defragmentation strategies can be used for different metrics within the same cluster.</span></span> <span data-ttu-id="25d7c-171">Un servizio può disporre di metriche di bilanciamento e di deframmentazione.</span><span class="sxs-lookup"><span data-stu-id="25d7c-171">A service can have both balancing and defragmentation metrics.</span></span> <span data-ttu-id="25d7c-172">Per la metrica di deframmentazione, il rapporto dei carichi nel cluster attiva in questo caso il ribilanciamento quando è _al di sotto_ della soglia di bilanciamento.</span><span class="sxs-lookup"><span data-stu-id="25d7c-172">For defragmentation metrics, the ratio of the loads in the cluster triggers rebalancing when it is _below_ the balancing threshold.</span></span> 
>

<span data-ttu-id="25d7c-173">Rimanere sotto la soglia di bilanciamento del carico non è un obiettivo esplicito.</span><span class="sxs-lookup"><span data-stu-id="25d7c-173">Getting below the balancing threshold is not an explicit goal.</span></span> <span data-ttu-id="25d7c-174">Le soglie di bilanciamento sono semplicemente un *trigger*.</span><span class="sxs-lookup"><span data-stu-id="25d7c-174">Balancing Thresholds are just a *trigger*.</span></span> <span data-ttu-id="25d7c-175">Quando viene eseguito il bilanciamento, Cluster Resource Manager determina quali miglioramenti può apportare, se ve ne sono.</span><span class="sxs-lookup"><span data-stu-id="25d7c-175">When balancing runs, the Cluster Resource Manager determines what improvements it can make, if any.</span></span> <span data-ttu-id="25d7c-176">Il fatto che venga avviata una ricerca di bilanciamento non significa che vengano spostati degli elementi.</span><span class="sxs-lookup"><span data-stu-id="25d7c-176">Just because a balancing search is kicked off doesn't mean anything moves.</span></span> <span data-ttu-id="25d7c-177">A volte il cluster non è bilanciato ma è troppo limitato per essere corretto.</span><span class="sxs-lookup"><span data-stu-id="25d7c-177">Sometimes the cluster is imbalanced but too constrained to correct.</span></span> <span data-ttu-id="25d7c-178">In alternativa, i miglioramenti richiedono dei movimenti che sono troppo [costosi](service-fabric-cluster-resource-manager-movement-cost.md)).</span><span class="sxs-lookup"><span data-stu-id="25d7c-178">Alternatively, the improvements require movements that are too [costly](service-fabric-cluster-resource-manager-movement-cost.md)).</span></span>

## <a name="activity-thresholds"></a><span data-ttu-id="25d7c-179">soglie di attività</span><span class="sxs-lookup"><span data-stu-id="25d7c-179">Activity thresholds</span></span>
<span data-ttu-id="25d7c-180">A volte, sebbene i nodi siano relativamente sbilanciati, la quantità *totale* di carico nel cluster è bassa.</span><span class="sxs-lookup"><span data-stu-id="25d7c-180">Sometimes, although nodes are relatively imbalanced, the *total* amount of load in the cluster is low.</span></span> <span data-ttu-id="25d7c-181">La mancanza di carico può essere dovuta a un calo temporaneo o al fatto che il cluster è nuovo ed è stato avviato da poco.</span><span class="sxs-lookup"><span data-stu-id="25d7c-181">The lack of load could be a transient dip, or because the cluster is new and just getting bootstrapped.</span></span> <span data-ttu-id="25d7c-182">In entrambi i casi non è consigliabile perdere tempo con il bilanciamento del carico del cluster perché i risultati non sarebbero soddisfacenti.</span><span class="sxs-lookup"><span data-stu-id="25d7c-182">In either case, you may not want to spend time balancing the cluster because there’s little to be gained.</span></span> <span data-ttu-id="25d7c-183">Se il carico del cluster è stato bilanciato, si perderebbero risorse di rete e di calcolo per spostamenti che *non* farebbero grandi differenze.</span><span class="sxs-lookup"><span data-stu-id="25d7c-183">If the cluster underwent balancing, you’d spend network and compute resources to move things around without making any large *absolute* difference.</span></span> <span data-ttu-id="25d7c-184">Per evitare movimenti non necessari, è disponibile un altro controllo noto come Soglie di attività.</span><span class="sxs-lookup"><span data-stu-id="25d7c-184">To avoid unnecessary moves, there’s another control known as Activity Thresholds.</span></span> <span data-ttu-id="25d7c-185">Le soglie di attività consentono di specificare un limite inferiore assoluto per l'attività.</span><span class="sxs-lookup"><span data-stu-id="25d7c-185">Activity Thresholds allows you to specify some absolute lower bound for activity.</span></span> <span data-ttu-id="25d7c-186">Se nessun nodo supera tale soglia, il bilanciamento del carico non viene attivato neanche se viene raggiunta la soglia di bilanciamento.</span><span class="sxs-lookup"><span data-stu-id="25d7c-186">If no node is over this threshold, balancing isn't triggered even if the Balancing Threshold is met.</span></span>

<span data-ttu-id="25d7c-187">Si supponga che abbiamo mantenuto la soglia di bilanciamento su tre per questa metrica.</span><span class="sxs-lookup"><span data-stu-id="25d7c-187">Let’s say that we retain our Balancing Threshold of three for this metric.</span></span> <span data-ttu-id="25d7c-188">Si supponga anche che sia disponibile una Soglia di attività di 1536.</span><span class="sxs-lookup"><span data-stu-id="25d7c-188">Let's also say we have an Activity Threshold of 1536.</span></span> <span data-ttu-id="25d7c-189">Nel primo caso il cluster è sbilanciato in base alla soglia di bilanciamento, ma nessun nodo raggiunge la soglia di attività, quindi non viene eseguita alcuna azione.</span><span class="sxs-lookup"><span data-stu-id="25d7c-189">In the first case, while the cluster is imbalanced per the Balancing Threshold there's no node meets that Activity Threshold, so nothing happens.</span></span> <span data-ttu-id="25d7c-190">Nell'esempio in basso il nodo 1 supera la Soglia di attività.</span><span class="sxs-lookup"><span data-stu-id="25d7c-190">In the bottom example, Node1 is over the Activity Threshold.</span></span> <span data-ttu-id="25d7c-191">Dato che vengono superate sia la soglia di bilanciamento che la soglia di attività per la metrica, viene pianificato un bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="25d7c-191">Since both the Balancing Threshold and the Activity Threshold for the metric are exceeded, balancing is scheduled.</span></span> <span data-ttu-id="25d7c-192">Ad esempio, si veda il diagramma seguente:</span><span class="sxs-lookup"><span data-stu-id="25d7c-192">As an example, let's look at the following diagram:</span></span> 

<span data-ttu-id="25d7c-193"><center>
![Esempio di soglia di attività][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="25d7c-193"><center>
![Activity Threshold Example][Image3]
</center></span></span>

<span data-ttu-id="25d7c-194">Proprio come le soglie di bilanciamento del carico, le soglie di attività sono definite sulla base di singoli metriche tramite la definizione del cluster:</span><span class="sxs-lookup"><span data-stu-id="25d7c-194">Just like Balancing Thresholds, Activity Thresholds are defined per-metric via the cluster definition:</span></span>

<span data-ttu-id="25d7c-195">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="25d7c-195">ClusterManifest.xml</span></span>

``` xml
    <Section Name="MetricActivityThresholds">
      <Parameter Name="Memory" Value="1536"/>
    </Section>
```

<span data-ttu-id="25d7c-196">Tramite ClusterConfig.json per le distribuzioni autonome o Template.json per cluster ospitati in Azure:</span><span class="sxs-lookup"><span data-stu-id="25d7c-196">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="25d7c-197">Si noti che le soglie di bilanciamento e di attività sono entrambe legate a una metrica specifica. Il bilanciamento del carico viene attivato solo se vengono superate entrambe le soglie di bilanciamento e di attività per la stessa metrica.</span><span class="sxs-lookup"><span data-stu-id="25d7c-197">Balancing and activity thresholds are both tied to a specific metric - balancing is triggered only if both the Balancing Threshold and Activity Threshold is exceeded for the same metric.</span></span>

## <a name="balancing-services-together"></a><span data-ttu-id="25d7c-198">Bilanciamento composto dei servizi</span><span class="sxs-lookup"><span data-stu-id="25d7c-198">Balancing services together</span></span>
<span data-ttu-id="25d7c-199">Che il cluster sia bilanciato o no è una decisione a livello di cluster.</span><span class="sxs-lookup"><span data-stu-id="25d7c-199">Whether the cluster is imbalanced or not is a cluster-wide decision.</span></span> <span data-ttu-id="25d7c-200">Viene, tuttavia, corretto spostando le singole repliche e le istanze dei servizi.</span><span class="sxs-lookup"><span data-stu-id="25d7c-200">However, the way we go about fixing it is moving individual service replicas and instances around.</span></span> <span data-ttu-id="25d7c-201">Questo approccio ha senso, giusto?</span><span class="sxs-lookup"><span data-stu-id="25d7c-201">This makes sense, right?</span></span> <span data-ttu-id="25d7c-202">Uno stack di memoria in un nodo può ricevere contributi da più repliche o istanze.</span><span class="sxs-lookup"><span data-stu-id="25d7c-202">If memory is stacked up on one node, multiple replicas or instances could be contributing to it.</span></span> <span data-ttu-id="25d7c-203">Per correggere lo sbilanciamento potrebbe essere necessario spostare una delle repliche con stato o delle istanze senza stato che usano la metrica sbilanciata.</span><span class="sxs-lookup"><span data-stu-id="25d7c-203">Fixing the imbalance could require moving any of the stateful replicas or stateless instances that use the imbalanced metric.</span></span>

<span data-ttu-id="25d7c-204">In alcuni casi però viene spostato un servizio che non era sbilanciato (ricordare la discussione precedente relativa ai pesi locali e globali).</span><span class="sxs-lookup"><span data-stu-id="25d7c-204">Occasionally though, a service that wasn’t itself imbalanced gets moved (remember the discussion of local and global weights earlier).</span></span> <span data-ttu-id="25d7c-205">Per quale motivo si dovrebbe spostare un servizio quando tutte le metriche di quel servizio sono state bilanciate?</span><span class="sxs-lookup"><span data-stu-id="25d7c-205">Why would a service get moved when all that service’s metrics were balanced?</span></span> <span data-ttu-id="25d7c-206">Di seguito viene illustrato un esempio:</span><span class="sxs-lookup"><span data-stu-id="25d7c-206">Let’s see an example:</span></span>

- <span data-ttu-id="25d7c-207">Si supponga di avere quattro servizi: Service1, Service2, Service3 e Service4.</span><span class="sxs-lookup"><span data-stu-id="25d7c-207">Let's say there are four services, Service1, Service2, Service3, and Service4.</span></span> 
- <span data-ttu-id="25d7c-208">Service1 riporta le metriche Metric1 e Metric2.</span><span class="sxs-lookup"><span data-stu-id="25d7c-208">Service1 reports metrics Metric1 and Metric2.</span></span> 
- <span data-ttu-id="25d7c-209">Service2 riporta le metriche Metric2 e Metric3.</span><span class="sxs-lookup"><span data-stu-id="25d7c-209">Service2 reports metrics Metric2 and Metric3.</span></span> 
- <span data-ttu-id="25d7c-210">Service3 riporta le metriche Metric3 e Metric4.</span><span class="sxs-lookup"><span data-stu-id="25d7c-210">Service3 reports metrics Metric3 and Metric4.</span></span>
- <span data-ttu-id="25d7c-211">Service4 riporta la metrica Metric99.</span><span class="sxs-lookup"><span data-stu-id="25d7c-211">Service4 reports metric Metric99.</span></span> 

<span data-ttu-id="25d7c-212">Sicuramente è già possibile intravedere una spiegazione: la catena.</span><span class="sxs-lookup"><span data-stu-id="25d7c-212">Surely you can see where we’re going here: There's a chain!</span></span> <span data-ttu-id="25d7c-213">Non ci sono quattro servizi indipendenti, ma tre servizi correlati tra loro e uno autonomo.</span><span class="sxs-lookup"><span data-stu-id="25d7c-213">We don’t really have four independent services, we have three services that are related and one that is off on its own.</span></span>

<span data-ttu-id="25d7c-214"><center>
![Bilanciamento composto dei servizi][Image4]
</center></span><span class="sxs-lookup"><span data-stu-id="25d7c-214"><center>
![Balancing Services Together][Image4]
</center></span></span>

<span data-ttu-id="25d7c-215">A causa di questa catena, è possibile che uno squilibrio nelle metriche 1-4 provochi lo spostamento di repliche o istanze appartenenti ai servizi 1-3.</span><span class="sxs-lookup"><span data-stu-id="25d7c-215">Because of this chain, it's possible that an imbalance in metrics 1-4 can cause replicas or instances belonging to services 1-3 to move around.</span></span> <span data-ttu-id="25d7c-216">Sappiamo anche che uno sbilanciamento delle metriche 1, 2 o 3 non può comportare movimenti in Service4.</span><span class="sxs-lookup"><span data-stu-id="25d7c-216">We also know that an imbalance in Metrics 1, 2, or 3 can't cause movements in Service4.</span></span> <span data-ttu-id="25d7c-217">Non sarebbero di alcuna utilità, dato che lo spostamento di repliche o istanze appartenenti a Service4 non influirebbe in alcun modo sul bilanciamento delle metriche 1-3.</span><span class="sxs-lookup"><span data-stu-id="25d7c-217">There would be no point since moving the replicas or instances belonging to Service4 around can do absolutely nothing to impact the balance of Metrics 1-3.</span></span>

<span data-ttu-id="25d7c-218">Cluster Resource Manager determina automaticamente i servizi correlati.</span><span class="sxs-lookup"><span data-stu-id="25d7c-218">The Cluster Resource Manager automatically figures out what services are related.</span></span> <span data-ttu-id="25d7c-219">Aggiungere, rimuovere o modificare le metriche per i servizi può influire sulle relative relazioni.</span><span class="sxs-lookup"><span data-stu-id="25d7c-219">Adding, removing, or changing the metrics for services can impact their relationships.</span></span> <span data-ttu-id="25d7c-220">Ad esempio, tra due esecuzioni di bilanciamento del carico, Service2 potrebbe essere stato aggiornato per rimuovere Metric2.</span><span class="sxs-lookup"><span data-stu-id="25d7c-220">For example, between two runs of balancing Service2 may have been updated to remove Metric2.</span></span> <span data-ttu-id="25d7c-221">Questa operazione interrompe la catena tra Service1 e Service2.</span><span class="sxs-lookup"><span data-stu-id="25d7c-221">This breaks the chain between Service1 and Service2.</span></span> <span data-ttu-id="25d7c-222">Ora, invece di due gruppi di servizi correlati ce ne sono tre:</span><span class="sxs-lookup"><span data-stu-id="25d7c-222">Now instead of two groups of related services, there are three:</span></span>

<span data-ttu-id="25d7c-223"><center>
![Bilanciamento composto dei servizi][Image5]
</center></span><span class="sxs-lookup"><span data-stu-id="25d7c-223"><center>
![Balancing Services Together][Image5]
</center></span></span>

## <a name="next-steps"></a><span data-ttu-id="25d7c-224">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="25d7c-224">Next steps</span></span>
* <span data-ttu-id="25d7c-225">Le metriche determinano il modo in cui Cluster Resource Manger di Service Fabric gestisce il consumo e la capacità del cluster.</span><span class="sxs-lookup"><span data-stu-id="25d7c-225">Metrics are how the Service Fabric Cluster Resource Manger manages consumption and capacity in the cluster.</span></span> <span data-ttu-id="25d7c-226">Per altre informazioni sulle metriche e su come configurarle, vedere [questo articolo](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="25d7c-226">To learn more about metrics and how to configure them, check out [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>
* <span data-ttu-id="25d7c-227">Il costo dello spostamento è un modo per segnalare a Cluster Resource Manager che alcuni servizi sono più costosi da spostare rispetto ad altri.</span><span class="sxs-lookup"><span data-stu-id="25d7c-227">Movement Cost is one way of signaling to the Cluster Resource Manager that certain services are more expensive to move than others.</span></span> <span data-ttu-id="25d7c-228">Per altre informazioni sui costi di spostamento, vedere [questo articolo](service-fabric-cluster-resource-manager-movement-cost.md).</span><span class="sxs-lookup"><span data-stu-id="25d7c-228">For more about movement cost, refer to [this article](service-fabric-cluster-resource-manager-movement-cost.md)</span></span>
* <span data-ttu-id="25d7c-229">Cluster Resource Manager dispone di diverse limitazioni da configurare per rallentare la varianza del cluster.</span><span class="sxs-lookup"><span data-stu-id="25d7c-229">The Cluster Resource Manager has several throttles that you can configure to slow down churn in the cluster.</span></span> <span data-ttu-id="25d7c-230">Queste limitazioni non sono in genere necessarie, ma sono eventualmente disponibili altre informazioni [qui](service-fabric-cluster-resource-manager-advanced-throttling.md)</span><span class="sxs-lookup"><span data-stu-id="25d7c-230">They're not normally necessary, but if you need them you can learn about them [here](service-fabric-cluster-resource-manager-advanced-throttling.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resrouce-manager-balancing-thresholds.png
[Image2]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-threshold-triggered-results.png
[Image3]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-activity-thresholds.png
[Image4]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together1.png
[Image5]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together2.png
