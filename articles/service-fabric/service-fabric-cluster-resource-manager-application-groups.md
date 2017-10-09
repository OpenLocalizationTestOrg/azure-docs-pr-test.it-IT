---
title: aaaService gestione delle risorse dell'infrastruttura Cluster - gruppi di applicazioni | Documenti Microsoft
description: "Panoramica delle funzionalità gruppo di applicazioni nel servizio di gestione delle risorse Cluster dell'infrastruttura di hello hello"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 4cae2370-77b3-49ce-bf40-030400c4260d
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: b4f068862d962b53a0b3ea813b89bb13ee395681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapplication-groups"></a><span data-ttu-id="c883c-103">Introduzione tooApplication gruppi</span><span class="sxs-lookup"><span data-stu-id="c883c-103">Introduction tooApplication Groups</span></span>
<span data-ttu-id="c883c-104">Gestione delle risorse dell'infrastruttura servizio Cluster gestisce in genere le risorse cluster distribuendo il carico hello (rappresentato tramite [metriche](service-fabric-cluster-resource-manager-metrics.md)) in modo uniforme in tutto il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="c883c-104">Service Fabric's Cluster Resource Manager typically manages cluster resources by spreading hello load (represented via [Metrics](service-fabric-cluster-resource-manager-metrics.md)) evenly throughout hello cluster.</span></span> <span data-ttu-id="c883c-105">Service Fabric gestisce la capacità di hello dei nodi hello hello e hello cluster nel suo complesso tramite [capacità](service-fabric-cluster-resource-manager-cluster-description.md).</span><span class="sxs-lookup"><span data-stu-id="c883c-105">Service Fabric manages hello capacity of hello nodes in hello cluster and hello cluster as a whole via [capacity](service-fabric-cluster-resource-manager-cluster-description.md).</span></span> <span data-ttu-id="c883c-106">Metriche e capacità rappresentano un'ottima soluzione per molti tipi di carichi di lavoro, ma i modelli che fanno largo uso di diverse istanze di applicazione di Service Fabric comportano a volte requisiti aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="c883c-106">Metrics and capacity work great for many workloads, but patterns that make heavy use of different Service Fabric Application Instances sometimes bring in additional requirements.</span></span> <span data-ttu-id="c883c-107">Ad esempio, si può desiderare di:</span><span class="sxs-lookup"><span data-stu-id="c883c-107">For example you may want to:</span></span>

- <span data-ttu-id="c883c-108">Alcune capacità in nodi hello hello cluster per i servizi all'interno di un'istanza di applicazione denominata hello di riserva</span><span class="sxs-lookup"><span data-stu-id="c883c-108">Reserve some capacity on hello nodes in hello cluster for hello services within some named application instance</span></span>
- <span data-ttu-id="c883c-109">Limitare hello il numero totale di nodi che hello all'interno di un'istanza dell'applicazione denominata vengono eseguiti i servizi (anziché distribuirli tramite l'intero cluster hello)</span><span class="sxs-lookup"><span data-stu-id="c883c-109">Limit hello total number of nodes that hello services within a named application instance run on (instead of spreading them out over hello entire cluster)</span></span>
- <span data-ttu-id="c883c-110">Definire le capacità nell'istanza di applicazione denominata hello stesso numero di hello toolimit servizi o totale del consumo della risorsa dei servizi di hello all'interno</span><span class="sxs-lookup"><span data-stu-id="c883c-110">Define capacities on hello named application instance itself toolimit hello number of services or total resource consumption of hello services inside it</span></span>

<span data-ttu-id="c883c-111">toomeet questi requisiti, hello gestione delle risorse Cluster di Service Fabric supporta una funzionalità denominata gruppi di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="c883c-111">toomeet these requirements, hello Service Fabric Cluster Resource Manager supports a feature called Application Groups.</span></span>

## <a name="limiting-hello-maximum-number-of-nodes"></a><span data-ttu-id="c883c-112">Limitando hello il numero massimo di nodi</span><span class="sxs-lookup"><span data-stu-id="c883c-112">Limiting hello maximum number of nodes</span></span>
<span data-ttu-id="c883c-113">Hello più semplice per la capacità dell'applicazione viene usata quando un'istanza di applicazione deve toobe limitato tooa determinato numero massimo di nodi.</span><span class="sxs-lookup"><span data-stu-id="c883c-113">hello simplest use case for Application capacity is when an application instance needs toobe limited tooa certain maximum number of nodes.</span></span> <span data-ttu-id="c883c-114">Consolida tutti i servizi all'interno di tale istanza dell'applicazione su un numero di set di macchine.</span><span class="sxs-lookup"><span data-stu-id="c883c-114">This consolidates all services within that application instance onto a set number of machines.</span></span> <span data-ttu-id="c883c-115">Consolidamento è utile quando si sta tentando di toopredict o limitare l'utilizzo delle risorse fisiche da servizi di hello all'interno di tale istanza dell'applicazione denominata.</span><span class="sxs-lookup"><span data-stu-id="c883c-115">Consolidation is useful when you're trying toopredict or cap physical resource use by hello services within that named application instance.</span></span> 

<span data-ttu-id="c883c-116">Hello immagine seguente mostra un'istanza dell'applicazione con e senza un numero massimo di nodi definiti:</span><span class="sxs-lookup"><span data-stu-id="c883c-116">hello following image shows an application instance with and without a maximum number of nodes defined:</span></span>

<span data-ttu-id="c883c-117"><center>
![Istanza di applicazione che definisce il numero massimo di nodi][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="c883c-117"><center>
![Application Instance Defining Maximum Number of Nodes][Image1]
</center></span></span>

<span data-ttu-id="c883c-118">Nell'esempio di sinistra hello, un'applicazione hello non dispone di un numero massimo di nodi definiti e dispone di tre servizi.</span><span class="sxs-lookup"><span data-stu-id="c883c-118">In hello left example, hello application doesn’t have a maximum number of nodes defined, and it has three services.</span></span> <span data-ttu-id="c883c-119">Gestione delle risorse Cluster Hello è diffondere tutte le repliche tra sei nodi disponibili tooachieve hello equilibrio migliore in cluster hello (comportamento predefinito di hello).</span><span class="sxs-lookup"><span data-stu-id="c883c-119">hello Cluster Resource Manager has spread out all replicas across six available nodes tooachieve hello best balance in hello cluster (hello default behavior).</span></span> <span data-ttu-id="c883c-120">Nell'esempio di destra hello, vediamo hello stessa applicazione limitata toothree nodi.</span><span class="sxs-lookup"><span data-stu-id="c883c-120">In hello right example, we see hello same application limited toothree nodes.</span></span>

<span data-ttu-id="c883c-121">il parametro Hello che controlla questo comportamento viene chiamato numero massimo di nodi.</span><span class="sxs-lookup"><span data-stu-id="c883c-121">hello parameter that controls this behavior is called MaximumNodes.</span></span> <span data-ttu-id="c883c-122">Questo parametro può essere impostato durante la creazione dell'applicazione oppure può essere aggiornato per un'istanza di applicazione già in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c883c-122">This parameter can be set during application creation, or updated for an application instance that was already running.</span></span>

<span data-ttu-id="c883c-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c883c-123">Powershell</span></span>

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MaximumNodes 3
Update-ServiceFabricApplication –Name fabric:/AppName –MaximumNodes 5
```

<span data-ttu-id="c883c-124">C#</span><span class="sxs-lookup"><span data-stu-id="c883c-124">C#</span></span>

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MaximumNodes = 3;
await fc.ApplicationManager.CreateApplicationAsync(ad);

ApplicationUpdateDescription adUpdate = new ApplicationUpdateDescription(new Uri("fabric:/AppName"));
adUpdate.MaximumNodes = 5;
await fc.ApplicationManager.UpdateApplicationAsync(adUpdate);

```

<span data-ttu-id="c883c-125">In set di nodi hello hello gestione delle risorse Cluster non garantisce gli oggetti per cui ottengano posizionati o ottengano utilizzati i nodi.</span><span class="sxs-lookup"><span data-stu-id="c883c-125">Within hello set of nodes, hello Cluster Resource Manager doesn't guarantee which service objects get placed together or which nodes get used.</span></span>

## <a name="application-metrics-load-and-capacity"></a><span data-ttu-id="c883c-126">Metriche, carico e capacità dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="c883c-126">Application Metrics, Load, and Capacity</span></span>
<span data-ttu-id="c883c-127">Gruppi di applicazioni consentono anche metriche toodefine associate a un'istanza dell'applicazione denominata specificato e la capacità del tale istanza applicazione per tali metriche.</span><span class="sxs-lookup"><span data-stu-id="c883c-127">Application Groups also allow you toodefine metrics associated with a given named application instance, and that application instance's capacity for those metrics.</span></span> <span data-ttu-id="c883c-128">Le metriche dell'applicazione consentono di tootrack riserva e limitare il consumo di risorse hello dei servizi di hello all'interno di tale istanza dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c883c-128">Application metrics allow you tootrack, reserve, and limit hello resource consumption of hello services inside that application instance.</span></span>

<span data-ttu-id="c883c-129">Per ogni metrica di applicazione, è possibile impostare due valori:</span><span class="sxs-lookup"><span data-stu-id="c883c-129">For each application metric, there are two values that can be set:</span></span>

- <span data-ttu-id="c883c-130">**Applicazione capacità totale** : questa impostazione rappresenta la capacità totale hello dell'applicazione hello per una determinata metrica.</span><span class="sxs-lookup"><span data-stu-id="c883c-130">**Total Application Capacity** – This setting represents hello total capacity of hello application for a particular metric.</span></span> <span data-ttu-id="c883c-131">Hello gestione delle risorse Cluster non consente la creazione di hello di eventuali nuovi servizi all'interno di questa istanza di applicazione che fa sì che il carico totale tooexceed questo valore.</span><span class="sxs-lookup"><span data-stu-id="c883c-131">hello Cluster Resource Manager disallows hello creation of any new services within this application instance that would cause total load tooexceed this value.</span></span> <span data-ttu-id="c883c-132">Si supponga, ad esempio, ha una capacità pari a 10 di istanza dell'applicazione hello e dispone già di carico di cinque.</span><span class="sxs-lookup"><span data-stu-id="c883c-132">For example, let's say hello application instance had a capacity of 10 and already had load of five.</span></span> <span data-ttu-id="c883c-133">creazione di Hello di un servizio con un carico totale predefinito di 10 sarebbe non consentita.</span><span class="sxs-lookup"><span data-stu-id="c883c-133">hello creation of a service with a total default load of 10 would be disallowed.</span></span>
- <span data-ttu-id="c883c-134">**Capacità massima del nodo** : questa impostazione specifica carico totale massimo di hello per un'applicazione hello in un singolo nodo.</span><span class="sxs-lookup"><span data-stu-id="c883c-134">**Maximum Node Capacity** – This setting specifies hello maximum total load for hello application on a single node.</span></span> <span data-ttu-id="c883c-135">Se il carico passa in questa capacità, hello gestione delle risorse Cluster consente di spostare i nodi tooother repliche hello carico diminuisce.</span><span class="sxs-lookup"><span data-stu-id="c883c-135">If load goes over this capacity, hello Cluster Resource Manager moves replicas tooother nodes so that hello load decreases.</span></span>


<span data-ttu-id="c883c-136">Powershell:</span><span class="sxs-lookup"><span data-stu-id="c883c-136">Powershell:</span></span>

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -Metrics @("MetricName:Metric1,MaximumNodeCapacity:100,MaximumApplicationCapacity:1000")
```

<span data-ttu-id="c883c-137">C#:</span><span class="sxs-lookup"><span data-stu-id="c883c-137">C#:</span></span>

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.TotalApplicationCapacity = 1000;
appMetric.MaximumNodeCapacity = 100;
ad.Metrics.Add(appMetric);
await fc.ApplicationManager.CreateApplicationAsync(ad);
```

## <a name="reserving-capacity"></a><span data-ttu-id="c883c-138">Riserva della capacità</span><span class="sxs-lookup"><span data-stu-id="c883c-138">Reserving Capacity</span></span>
<span data-ttu-id="c883c-139">Un altro utilizzo comune per gruppi di applicazioni è che le risorse all'interno di hello cluster tooensure sono riservati per un'istanza dell'applicazione specificato.</span><span class="sxs-lookup"><span data-stu-id="c883c-139">Another common use for application groups is tooensure that resources within hello cluster are reserved for a given application instance.</span></span> <span data-ttu-id="c883c-140">Quando viene creata l'istanza dell'applicazione hello, è sempre riservato Hello uno spazio.</span><span class="sxs-lookup"><span data-stu-id="c883c-140">hello space is always reserved when hello application instance is created.</span></span>

<span data-ttu-id="c883c-141">Riserva spazio nel cluster hello per un'applicazione hello avviene immediatamente, anche se:</span><span class="sxs-lookup"><span data-stu-id="c883c-141">Reserving space in hello cluster for hello application happens immediately even when:</span></span>
- <span data-ttu-id="c883c-142">istanza dell'applicazione Hello viene creato ma non dispone ancora di tutti i servizi all'interno di essa</span><span class="sxs-lookup"><span data-stu-id="c883c-142">hello application instance is created but doesn't have any services within it yet</span></span>
- <span data-ttu-id="c883c-143">numero di Hello dei servizi all'interno di istanza dell'applicazione hello cambia ogni volta</span><span class="sxs-lookup"><span data-stu-id="c883c-143">hello number of services within hello application instance changes every time</span></span> 
- <span data-ttu-id="c883c-144">servizi di Hello esistano ma non utilizzano risorse di hello</span><span class="sxs-lookup"><span data-stu-id="c883c-144">hello services exist but aren't consuming hello resources</span></span> 

<span data-ttu-id="c883c-145">Per prenotare le risorse per un'istanza dell'applicazione è necessario definire due parametri aggiuntivi: *MinimumNodes* e *NodeReservationCapacity*</span><span class="sxs-lookup"><span data-stu-id="c883c-145">Reserving resources for an application instance requires specifying two additional parameters: *MinimumNodes* and *NodeReservationCapacity*</span></span>

- <span data-ttu-id="c883c-146">**Numero minimo di nodi** -definisce il numero minimo di hello di nodi che hello applicazione istanza deve essere eseguita.</span><span class="sxs-lookup"><span data-stu-id="c883c-146">**MinimumNodes** - Defines hello minimum number of nodes that hello application instance should run on.</span></span>  
- <span data-ttu-id="c883c-147">**NodeReservationCapacity** -questa impostazione è per ogni metrica per un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="c883c-147">**NodeReservationCapacity** - This setting is per metric for hello application.</span></span> <span data-ttu-id="c883c-148">il valore di Hello è quantità hello di tale metrica riservato per un'applicazione hello su qualsiasi nodo in cui che hello servizi in esecuzione tale applicazione.</span><span class="sxs-lookup"><span data-stu-id="c883c-148">hello value is hello amount of that metric reserved for hello application on any node where that hello services in that application run.</span></span>

<span data-ttu-id="c883c-149">La combinazione di **nodi** e **NodeReservationCapacity** garantisce una prenotazione di un carico minimo per un'applicazione hello all'interno di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="c883c-149">Combining **MinimumNodes** and **NodeReservationCapacity** guarantees a minimum load reservation for hello application within hello cluster.</span></span> <span data-ttu-id="c883c-150">Se si verifica meno rimanenti del cluster di prenotazione di hello totale necessaria capacità di hello, si verifica un errore di creazione di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="c883c-150">If there's less remaining capacity in hello cluster than hello total reservation required, creation of hello application fails.</span></span> 

<span data-ttu-id="c883c-151">Di seguito viene illustrato un esempio di come viene riservata la capacità:</span><span class="sxs-lookup"><span data-stu-id="c883c-151">Let's look at an example of capacity reservation:</span></span>

<span data-ttu-id="c883c-152"><center>
![Istanze di applicazione che definiscono la capacità riservata][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="c883c-152"><center>
![Application Instances Defining Reserved Capacity][Image2]
</center></span></span>

<span data-ttu-id="c883c-153">Nell'esempio di sinistra hello, le applicazioni non dispone capacità qualsiasi applicazione definito.</span><span class="sxs-lookup"><span data-stu-id="c883c-153">In hello left example, applications do not have any Application Capacity defined.</span></span> <span data-ttu-id="c883c-154">Gestione delle risorse Cluster Hello saldi tutti gli elementi in base a regole toonormal.</span><span class="sxs-lookup"><span data-stu-id="c883c-154">hello Cluster Resource Manager balances everything according toonormal rules.</span></span>

<span data-ttu-id="c883c-155">Nell'esempio hello hello destra, si supponga che Application1 sia stato creato con hello seguenti impostazioni:</span><span class="sxs-lookup"><span data-stu-id="c883c-155">In hello example on hello right, let's say that Application1 was created with hello following settings:</span></span>

- <span data-ttu-id="c883c-156">Numero minimo di nodi set tootwo</span><span class="sxs-lookup"><span data-stu-id="c883c-156">MinimumNodes set tootwo</span></span>
- <span data-ttu-id="c883c-157">Una metrica dell'applicazione definita con le impostazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="c883c-157">An application Metric defined with</span></span>
  - <span data-ttu-id="c883c-158">NodeReservationCapacity pari a 20</span><span class="sxs-lookup"><span data-stu-id="c883c-158">NodeReservationCapacity of 20</span></span>

<span data-ttu-id="c883c-159">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c883c-159">Powershell</span></span>

 ``` posh
 New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MinimumNodes 2 -Metrics @("MetricName:Metric1,NodeReservationCapacity:20")
 ```

<span data-ttu-id="c883c-160">C#</span><span class="sxs-lookup"><span data-stu-id="c883c-160">C#</span></span>

 ``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MinimumNodes = 2;

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.NodeReservationCapacity = 20;

ad.Metrics.Add(appMetric);

await fc.ApplicationManager.CreateApplicationAsync(ad);
```

<span data-ttu-id="c883c-161">Service Fabric riserva capacità in due nodi per /Application1 e non consentono di servizi da Application2 tooconsume tale capacità anche se sono presenti che senza alcun carico non viene consumato da servizi di hello all'interno di Application1 in fase di hello.</span><span class="sxs-lookup"><span data-stu-id="c883c-161">Service Fabric reserves capacity on two nodes for Application1, and doesn't allow services from Application2 tooconsume that capacity even if there are no load is being consumed by hello services inside Application1 at hello time.</span></span> <span data-ttu-id="c883c-162">Questa capacità riservata applicazione è considerata utilizzata e concorre hello residua in tale nodo e all'interno di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="c883c-162">This reserved application capacity is considered consumed  and counts against hello remaining capacity on that node and within hello cluster.</span></span>  <span data-ttu-id="c883c-163">prenotazione Hello viene sottratto dal hello residua di cluster immediatamente, ma hello riservato consumo viene sottratto dalla capacità di hello di un nodo specifico solo quando almeno un servizio oggetto viene posizionato su di esso.</span><span class="sxs-lookup"><span data-stu-id="c883c-163">hello reservation is deducted from hello remaining cluster capacity immediately, however hello reserved consumption is deducted from hello capacity of a specific node only when at least one service object is placed on it.</span></span> <span data-ttu-id="c883c-164">Questa prenotazione successiva consente un utilizzo ottimale delle risorse e flessibilità, dal momento che le risorse sono riservate nei nodi solo quando necessario.</span><span class="sxs-lookup"><span data-stu-id="c883c-164">This later reservation allows for flexibility and better resource utilization since resources are only reserved on nodes when needed.</span></span>

## <a name="obtaining-hello-application-load-information"></a><span data-ttu-id="c883c-165">Ottenere informazioni sul caricamento di applicazione hello</span><span class="sxs-lookup"><span data-stu-id="c883c-165">Obtaining hello application load information</span></span>
<span data-ttu-id="c883c-166">Per ogni applicazione che ha una capacità di applicazioni definito per una o più metriche è possibile ottenere informazioni di hello sul carico di aggregazione hello segnalato da repliche dei relativi servizi.</span><span class="sxs-lookup"><span data-stu-id="c883c-166">For each application that has an Application Capacity defined for one or more metrics you can obtain hello information about hello aggregate load reported by replicas of its services.</span></span>

<span data-ttu-id="c883c-167">Powershell:</span><span class="sxs-lookup"><span data-stu-id="c883c-167">Powershell:</span></span>

``` posh
Get-ServiceFabricApplicationLoad –ApplicationName fabric:/MyApplication1
```

<span data-ttu-id="c883c-168">C#</span><span class="sxs-lookup"><span data-stu-id="c883c-168">C#</span></span>

``` csharp
var v = await fc.QueryManager.GetApplicationLoadInformationAsync("fabric:/MyApplication1");
var metrics = v.ApplicationLoadMetricInformation;
foreach (ApplicationLoadMetricInformation metric in metrics)
{
    Console.WriteLine(metric.ApplicationCapacity);  //total capacity for this metric in this application instance
    Console.WriteLine(metric.ReservationCapacity);  //reserved capacity for this metric in this application instance
    Console.WriteLine(metric.ApplicationLoad);  //current load for this metric in this application instance
}
```

<span data-ttu-id="c883c-169">query ApplicationLoad Hello restituisce informazioni di base sulla capacità di applicazione che è stato specificato per un'applicazione hello hello.</span><span class="sxs-lookup"><span data-stu-id="c883c-169">hello ApplicationLoad query returns hello basic information about Application Capacity that was specified for hello application.</span></span> <span data-ttu-id="c883c-170">Queste informazioni includono le informazioni di nodi di minimo e massimo hello e numero hello che un'applicazione hello è attualmente occupata.</span><span class="sxs-lookup"><span data-stu-id="c883c-170">This information includes hello Minimum Nodes and Maximum Nodes info, and hello number that hello application is currently occupying.</span></span> <span data-ttu-id="c883c-171">Sono inoltre incluse informazioni su ogni metrica di carico dell'applicazione, tra cui:</span><span class="sxs-lookup"><span data-stu-id="c883c-171">It also includes information about each application load metric, including:</span></span>

* <span data-ttu-id="c883c-172">Il nome della metrica: Nome della metrica hello.</span><span class="sxs-lookup"><span data-stu-id="c883c-172">Metric Name: Name of hello metric.</span></span>
* <span data-ttu-id="c883c-173">Capacità di prenotazione: La capacità Cluster nel cluster hello viene riservata per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c883c-173">Reservation Capacity: Cluster Capacity that is reserved in hello cluster for this Application.</span></span>
* <span data-ttu-id="c883c-174">Carico dell'applicazione: carico totale delle repliche figlio dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c883c-174">Application Load: Total Load of this Application’s child replicas.</span></span>
* <span data-ttu-id="c883c-175">Capacità dell'applicazione: valore massimo consentito di carico dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c883c-175">Application Capacity: Maximum permitted value of Application Load.</span></span>

## <a name="removing-application-capacity"></a><span data-ttu-id="c883c-176">Rimozione della capacità dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="c883c-176">Removing Application Capacity</span></span>
<span data-ttu-id="c883c-177">Dopo aver impostati i parametri di capacità dell'applicazione hello per un'applicazione, può essere rimosso utilizzando le API di aggiornamento dell'applicazione o i cmdlet PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c883c-177">Once hello Application Capacity parameters are set for an application, they can be removed using Update Application APIs or PowerShell cmdlets.</span></span> <span data-ttu-id="c883c-178">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c883c-178">For example:</span></span>

``` posh
Update-ServiceFabricApplication –Name fabric:/MyApplication1 –RemoveApplicationCapacity

```

<span data-ttu-id="c883c-179">Questo comando rimuove tutti i parametri di gestione della capacità dell'applicazione dall'istanza di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="c883c-179">This command removes all Application capacity management parameters from hello application instance.</span></span> <span data-ttu-id="c883c-180">Sono inclusi nodi, numero massimo di nodi e le metriche dell'applicazione hello, se presente.</span><span class="sxs-lookup"><span data-stu-id="c883c-180">This includes MinimumNodes, MaximumNodes, and hello Application's metrics, if any.</span></span> <span data-ttu-id="c883c-181">effetto di Hello del comando hello è immediato.</span><span class="sxs-lookup"><span data-stu-id="c883c-181">hello effect of hello command is immediate.</span></span> <span data-ttu-id="c883c-182">Dopo il completamento del comando, hello gestione delle risorse Cluster utilizza il comportamento predefinito di hello per la gestione delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="c883c-182">After this command completes, hello Cluster Resource Manager uses hello default behavior for managing applications.</span></span> <span data-ttu-id="c883c-183">I parametri di capacità dell'applicazione possono essere specificati nuovamente tramite `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.</span><span class="sxs-lookup"><span data-stu-id="c883c-183">Application Capacity parameters can be specified again via `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.</span></span>

### <a name="restrictions-on-application-capacity"></a><span data-ttu-id="c883c-184">Restrizioni relative alla capacità dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="c883c-184">Restrictions on Application Capacity</span></span>
<span data-ttu-id="c883c-185">Esistono diverse restrizioni da rispettare per i parametri di capacità dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c883c-185">There are several restrictions on Application Capacity parameters that must be respected.</span></span> <span data-ttu-id="c883c-186">Se sono presenti errori di convalida non viene apportata alcuna modifica.</span><span class="sxs-lookup"><span data-stu-id="c883c-186">If there are validation errors no changes take place.</span></span>

- <span data-ttu-id="c883c-187">Tutti i parametri di tipo integer devono essere numeri non negativi.</span><span class="sxs-lookup"><span data-stu-id="c883c-187">All integer parameters must be non-negative numbers.</span></span>
- <span data-ttu-id="c883c-188">MinimumNodes non deve essere mai maggiore di MaximumNodes.</span><span class="sxs-lookup"><span data-stu-id="c883c-188">MinimumNodes must never be greater than MaximumNodes.</span></span>
- <span data-ttu-id="c883c-189">Se definite, le capacità per una metrica di carico devono rispettare queste regole:</span><span class="sxs-lookup"><span data-stu-id="c883c-189">If capacities for a load metric are defined, then they must follow these rules:</span></span>
  - <span data-ttu-id="c883c-190">La capacità di prenotazione del nodo non deve essere maggiore della capacità massima del nodo.</span><span class="sxs-lookup"><span data-stu-id="c883c-190">Node Reservation Capacity must not be greater than Maximum Node Capacity.</span></span> <span data-ttu-id="c883c-191">Ad esempio, non è possibile limitare la capacità di hello per la metrica di hello "CPU" in unità di hello nodo tootwo si cerca tooreserve tre unità su ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="c883c-191">For example, you cannot limit hello capacity for hello metric “CPU” on hello node tootwo units and try tooreserve three units on each node.</span></span>
  - <span data-ttu-id="c883c-192">Se il numero massimo di nodi viene specificato, il prodotto di hello del numero massimo di nodi e capacità massima del nodo non deve essere maggiore rispetto alla capacità totale di applicazione.</span><span class="sxs-lookup"><span data-stu-id="c883c-192">If MaximumNodes is specified, then hello product of MaximumNodes and Maximum Node Capacity must not be greater than Total Application Capacity.</span></span> <span data-ttu-id="c883c-193">Si supponga, ad esempio, hello capacità massima di nodo per la metrica di caricamento "CPU" è impostata tooeight.</span><span class="sxs-lookup"><span data-stu-id="c883c-193">For example, let's say hello Maximum Node Capacity for load metric “CPU” is set tooeight.</span></span> <span data-ttu-id="c883c-194">Si supponga inoltre che impostare hello too10 numero massimo di nodi.</span><span class="sxs-lookup"><span data-stu-id="c883c-194">Let's also say you set hello Maximum Nodes too10.</span></span> <span data-ttu-id="c883c-195">In questo caso, la capacità totale dell'applicazione deve essere superiore a 80 per la metrica di carico.</span><span class="sxs-lookup"><span data-stu-id="c883c-195">In this case, Total Application Capacity must be greater than 80 for this load metric.</span></span>

<span data-ttu-id="c883c-196">Hello restrizioni vengono applicate sia durante la creazione di applicazioni e aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="c883c-196">hello restrictions are enforced both during application creation and updates.</span></span>

## <a name="how-not-toouse-application-capacity"></a><span data-ttu-id="c883c-197">La modalità non toouse capacità di applicazione</span><span class="sxs-lookup"><span data-stu-id="c883c-197">How not toouse Application Capacity</span></span>
- <span data-ttu-id="c883c-198">Non tentare toouse hello gruppo di applicazioni funzionalità tooconstrain hello applicazione tooa _specifico_ subset di nodi.</span><span class="sxs-lookup"><span data-stu-id="c883c-198">Do not try toouse hello Application Group features tooconstrain hello application tooa _specific_ subset of nodes.</span></span> <span data-ttu-id="c883c-199">In altre parole, è possibile specificare che un'applicazione hello viene eseguito su al massimo cinque nodi, ma non le cinque nodi specifici cluster hello.</span><span class="sxs-lookup"><span data-stu-id="c883c-199">In other words, you can specify that hello application runs on at most five nodes, but not which specific five nodes in hello cluster.</span></span> <span data-ttu-id="c883c-200">Vincolare un toospecific applicazione nodi possono essere ottenuti utilizzando vincoli di posizionamento per i servizi.</span><span class="sxs-lookup"><span data-stu-id="c883c-200">Constraining an application toospecific nodes can be achieved using placement constraints for services.</span></span>
- <span data-ttu-id="c883c-201">Non tentare toouse hello applicazione capacità tooensure che due servizi dalla stessa applicazione si trovano in hello hello stessi nodi.</span><span class="sxs-lookup"><span data-stu-id="c883c-201">Do not try toouse hello Application Capacity tooensure that two services from hello same application are placed on hello same nodes.</span></span> <span data-ttu-id="c883c-202">Usare invece [affinità](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) o [vincoli di posizionamento](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).</span><span class="sxs-lookup"><span data-stu-id="c883c-202">Instead use [affinity](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) or [placement constraints](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c883c-203">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c883c-203">Next steps</span></span>
- <span data-ttu-id="c883c-204">Per altre informazioni sulla configurazione dei servizi, [Informazioni sulla configurazione dei servizi](service-fabric-cluster-resource-manager-configure-services.md)</span><span class="sxs-lookup"><span data-stu-id="c883c-204">For more information on configuring services, [Learn about configuring Services](service-fabric-cluster-resource-manager-configure-services.md)</span></span>
- <span data-ttu-id="c883c-205">toofind out sulla modalità di gestione delle risorse Cluster hello gestisce e bilancia il carico nel cluster hello, controllare l'articolo hello [bilanciamento del carico](service-fabric-cluster-resource-manager-balancing.md)</span><span class="sxs-lookup"><span data-stu-id="c883c-205">toofind out about how hello Cluster Resource Manager manages and balances load in hello cluster, check out hello article on [balancing load](service-fabric-cluster-resource-manager-balancing.md)</span></span>
- <span data-ttu-id="c883c-206">Iniziare dall'inizio hello e [ottenere un servizio di gestione delle risorse Cluster dell'infrastruttura di toohello introduzione](service-fabric-cluster-resource-manager-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="c883c-206">Start from hello beginning and [get an Introduction toohello Service Fabric Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)</span></span>
- <span data-ttu-id="c883c-207">Per altre informazioni sul funzionamento generale delle metriche, vedere l'articolo sulle [metriche di carico di Service Fabric](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="c883c-207">For more information on how metrics work generally, read up on [Service Fabric Load Metrics](service-fabric-cluster-resource-manager-metrics.md)</span></span>
- <span data-ttu-id="c883c-208">Hello gestione delle risorse Cluster dispone di numerose opzioni per la descrizione del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="c883c-208">hello Cluster Resource Manager has many options for describing hello cluster.</span></span> <span data-ttu-id="c883c-209">toofind ulteriori informazioni, consultare questo articolo in [che descrive un cluster di Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md)</span><span class="sxs-lookup"><span data-stu-id="c883c-209">toofind out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-max-nodes.png
[Image2]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-reserved-capacity.png
