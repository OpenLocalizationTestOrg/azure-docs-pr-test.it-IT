---
title: Cluster Resource Manager di Service Fabric - Gruppi di applicazioni | Microsoft Docs
description: "Informazioni generali sulla funzionalità dei gruppi di applicazioni in Cluster Resource Manager di Service Fabric "
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
ms.openlocfilehash: 7fc61731c8df2a0c3dc5b77ae718b41c240f9233
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="introduction-to-application-groups"></a><span data-ttu-id="a4fac-103">Introduzione ai gruppi di applicazioni</span><span class="sxs-lookup"><span data-stu-id="a4fac-103">Introduction to Application Groups</span></span>
<span data-ttu-id="a4fac-104">Cluster Resource Manager di Service Fabric generalmente gestisce le risorse del cluster distribuendo il carico (rappresentato tramite [Metriche](service-fabric-cluster-resource-manager-metrics.md)) in modo uniforme nell'intero cluster.</span><span class="sxs-lookup"><span data-stu-id="a4fac-104">Service Fabric's Cluster Resource Manager typically manages cluster resources by spreading the load (represented via [Metrics](service-fabric-cluster-resource-manager-metrics.md)) evenly throughout the cluster.</span></span> <span data-ttu-id="a4fac-105">Service Fabric gestisce la capacità dei nodi del cluster e il cluster nel suo complesso tramite la [capacità](service-fabric-cluster-resource-manager-cluster-description.md).</span><span class="sxs-lookup"><span data-stu-id="a4fac-105">Service Fabric manages the capacity of the nodes in the cluster and the cluster as a whole via [capacity](service-fabric-cluster-resource-manager-cluster-description.md).</span></span> <span data-ttu-id="a4fac-106">Metriche e capacità rappresentano un'ottima soluzione per molti tipi di carichi di lavoro, ma i modelli che fanno largo uso di diverse istanze di applicazione di Service Fabric comportano a volte requisiti aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="a4fac-106">Metrics and capacity work great for many workloads, but patterns that make heavy use of different Service Fabric Application Instances sometimes bring in additional requirements.</span></span> <span data-ttu-id="a4fac-107">Ad esempio, si può desiderare di:</span><span class="sxs-lookup"><span data-stu-id="a4fac-107">For example you may want to:</span></span>

- <span data-ttu-id="a4fac-108">Riservare alcune capacità sui nodi del cluster per i servizi all'interno di qualche istanza di applicazione denominata</span><span class="sxs-lookup"><span data-stu-id="a4fac-108">Reserve some capacity on the nodes in the cluster for the services within some named application instance</span></span>
- <span data-ttu-id="a4fac-109">Limitare il numero totale di nodi eseguiti dai servizi all'interno di un'istanza dell'applicazione denominata (anziché distribuirli tramite l'intero cluster)</span><span class="sxs-lookup"><span data-stu-id="a4fac-109">Limit the total number of nodes that the services within a named application instance run on (instead of spreading them out over the entire cluster)</span></span>
- <span data-ttu-id="a4fac-110">Definire le capacità nell'istanza di applicazione stessa denominata per limitare il numero di servizi o il consumo totale delle risorse dei servizi al suo interno</span><span class="sxs-lookup"><span data-stu-id="a4fac-110">Define capacities on the named application instance itself to limit the number of services or total resource consumption of the services inside it</span></span>

<span data-ttu-id="a4fac-111">Per soddisfare questi requisiti, Cluster Resource Manager di Service Fabric supporta una funzionalità chiamata Gruppi di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="a4fac-111">To meet these requirements, the Service Fabric Cluster Resource Manager supports a feature called Application Groups.</span></span>

## <a name="limiting-the-maximum-number-of-nodes"></a><span data-ttu-id="a4fac-112">Limitazione del numero massimo di nodi</span><span class="sxs-lookup"><span data-stu-id="a4fac-112">Limiting the maximum number of nodes</span></span>
<span data-ttu-id="a4fac-113">Il caso d'uso più semplice della capacità dell'applicazione è quando un'istanza di applicazione deve essere limitata a un numero massimo di nodi.</span><span class="sxs-lookup"><span data-stu-id="a4fac-113">The simplest use case for Application capacity is when an application instance needs to be limited to a certain maximum number of nodes.</span></span> <span data-ttu-id="a4fac-114">Consolida tutti i servizi all'interno di tale istanza dell'applicazione su un numero di set di macchine.</span><span class="sxs-lookup"><span data-stu-id="a4fac-114">This consolidates all services within that application instance onto a set number of machines.</span></span> <span data-ttu-id="a4fac-115">Il consolidamento è utile quando si sta cercando di stimare o limitare l'utilizzo delle risorse fisiche da parte dei servizi all'interno di tale istanza dell'applicazione denominata.</span><span class="sxs-lookup"><span data-stu-id="a4fac-115">Consolidation is useful when you're trying to predict or cap physical resource use by the services within that named application instance.</span></span> 

<span data-ttu-id="a4fac-116">Nell'immagine seguente è mostrata un'istanza di applicazione con e senza un numero massimo di nodi definiti.</span><span class="sxs-lookup"><span data-stu-id="a4fac-116">The following image shows an application instance with and without a maximum number of nodes defined:</span></span>

<span data-ttu-id="a4fac-117"><center>
![Istanza di applicazione che definisce il numero massimo di nodi][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="a4fac-117"><center>
![Application Instance Defining Maximum Number of Nodes][Image1]
</center></span></span>

<span data-ttu-id="a4fac-118">Nell'esempio a sinistra, l'applicazione non ha un numero massimo di nodi definito, e ha tre servizi.</span><span class="sxs-lookup"><span data-stu-id="a4fac-118">In the left example, the application doesn’t have a maximum number of nodes defined, and it has three services.</span></span> <span data-ttu-id="a4fac-119">Cluster Resource Manager ha distribuito tutte le repliche tra sei nodi disponibili per ottenere il bilanciamento ottimale nel cluster (il comportamento predefinito).</span><span class="sxs-lookup"><span data-stu-id="a4fac-119">The Cluster Resource Manager has spread out all replicas across six available nodes to achieve the best balance in the cluster (the default behavior).</span></span> <span data-ttu-id="a4fac-120">Nell'esempio a destra, notiamo la stessa applicazione limitata a tre nodi.</span><span class="sxs-lookup"><span data-stu-id="a4fac-120">In the right example, we see the same application limited to three nodes.</span></span>

<span data-ttu-id="a4fac-121">Il parametro che gestisce questo comportamento è denominato MaximumNodes.</span><span class="sxs-lookup"><span data-stu-id="a4fac-121">The parameter that controls this behavior is called MaximumNodes.</span></span> <span data-ttu-id="a4fac-122">Questo parametro può essere impostato durante la creazione dell'applicazione oppure può essere aggiornato per un'istanza di applicazione già in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a4fac-122">This parameter can be set during application creation, or updated for an application instance that was already running.</span></span>

<span data-ttu-id="a4fac-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4fac-123">Powershell</span></span>

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MaximumNodes 3
Update-ServiceFabricApplication –Name fabric:/AppName –MaximumNodes 5
```

<span data-ttu-id="a4fac-124">C#</span><span class="sxs-lookup"><span data-stu-id="a4fac-124">C#</span></span>

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

<span data-ttu-id="a4fac-125">All'interno del set di nodi, Cluster Resource Manager non garantisce quali oggetti di servizio si posizionano insieme o quali nodi vengono usati.</span><span class="sxs-lookup"><span data-stu-id="a4fac-125">Within the set of nodes, the Cluster Resource Manager doesn't guarantee which service objects get placed together or which nodes get used.</span></span>

## <a name="application-metrics-load-and-capacity"></a><span data-ttu-id="a4fac-126">Metriche, carico e capacità dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="a4fac-126">Application Metrics, Load, and Capacity</span></span>
<span data-ttu-id="a4fac-127">I gruppi di applicazioni consentono anche di definire le metriche associate a una determinata istanza di applicazione denominata, nonché la capacità di quell'istanza dell'applicazione in relazione a tali metriche.</span><span class="sxs-lookup"><span data-stu-id="a4fac-127">Application Groups also allow you to define metrics associated with a given named application instance, and that application instance's capacity for those metrics.</span></span> <span data-ttu-id="a4fac-128">Le metriche dell'applicazione consentono di tener traccia del consumo di risorse da parte dei servizi all'interno dell'istanza di applicazione, di riservarlo e di limitarlo.</span><span class="sxs-lookup"><span data-stu-id="a4fac-128">Application metrics allow you to track, reserve, and limit the resource consumption of the services inside that application instance.</span></span>

<span data-ttu-id="a4fac-129">Per ogni metrica di applicazione, è possibile impostare due valori:</span><span class="sxs-lookup"><span data-stu-id="a4fac-129">For each application metric, there are two values that can be set:</span></span>

- <span data-ttu-id="a4fac-130">**Capacità totale dell'applicazione**: rappresenta la capacità totale dell'applicazione per una particolare metrica.</span><span class="sxs-lookup"><span data-stu-id="a4fac-130">**Total Application Capacity** – This setting represents the total capacity of the application for a particular metric.</span></span> <span data-ttu-id="a4fac-131">Cluster Resource Manager impedisce di creare nuovi servizi all'interno dell'istanza di applicazione che farebbero superare questo valore di carico totale.</span><span class="sxs-lookup"><span data-stu-id="a4fac-131">The Cluster Resource Manager disallows the creation of any new services within this application instance that would cause total load to exceed this value.</span></span> <span data-ttu-id="a4fac-132">Si supponga, ad esempio, che l'istanza di applicazione abbia una capacità pari a 10 e il carico sia già pari a cinque.</span><span class="sxs-lookup"><span data-stu-id="a4fac-132">For example, let's say the application instance had a capacity of 10 and already had load of five.</span></span> <span data-ttu-id="a4fac-133">La creazione di un servizio con un carico totale predefinito di 10 non verrebbe consentita.</span><span class="sxs-lookup"><span data-stu-id="a4fac-133">The creation of a service with a total default load of 10 would be disallowed.</span></span>
- <span data-ttu-id="a4fac-134">**Capacità massima del nodo**: specifica il carico totale massimo per l'applicazione in un singolo nodo.</span><span class="sxs-lookup"><span data-stu-id="a4fac-134">**Maximum Node Capacity** – This setting specifies the maximum total load for the application on a single node.</span></span> <span data-ttu-id="a4fac-135">Se il carico supera questa capacità, Cluster Resource Manager sposta le repliche in altri nodi in modo che il carico diminuisca.</span><span class="sxs-lookup"><span data-stu-id="a4fac-135">If load goes over this capacity, the Cluster Resource Manager moves replicas to other nodes so that the load decreases.</span></span>


<span data-ttu-id="a4fac-136">Powershell:</span><span class="sxs-lookup"><span data-stu-id="a4fac-136">Powershell:</span></span>

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -Metrics @("MetricName:Metric1,MaximumNodeCapacity:100,MaximumApplicationCapacity:1000")
```

<span data-ttu-id="a4fac-137">C#:</span><span class="sxs-lookup"><span data-stu-id="a4fac-137">C#:</span></span>

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

## <a name="reserving-capacity"></a><span data-ttu-id="a4fac-138">Riserva della capacità</span><span class="sxs-lookup"><span data-stu-id="a4fac-138">Reserving Capacity</span></span>
<span data-ttu-id="a4fac-139">I gruppi di applicazioni vengono comunemente usati anche per garantire che le risorse all'interno del cluster siano riservate per una determinata istanza di applicazione.</span><span class="sxs-lookup"><span data-stu-id="a4fac-139">Another common use for application groups is to ensure that resources within the cluster are reserved for a given application instance.</span></span> <span data-ttu-id="a4fac-140">Lo spazio viene riservato sempre quando viene creata l'istanza dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a4fac-140">The space is always reserved when the application instance is created.</span></span>

<span data-ttu-id="a4fac-141">La riserva dello spazio nel cluster per l'applicazione si verifica immediatamente, anche se:</span><span class="sxs-lookup"><span data-stu-id="a4fac-141">Reserving space in the cluster for the application happens immediately even when:</span></span>
- <span data-ttu-id="a4fac-142">l'istanza dell'applicazione viene creata ma non dispone ancora di tutti i servizi all'interno di essa</span><span class="sxs-lookup"><span data-stu-id="a4fac-142">the application instance is created but doesn't have any services within it yet</span></span>
- <span data-ttu-id="a4fac-143">il numero di servizi all'interno dell'istanza dell'applicazione cambia ogni volta</span><span class="sxs-lookup"><span data-stu-id="a4fac-143">the number of services within the application instance changes every time</span></span> 
- <span data-ttu-id="a4fac-144">i servizi esistono ma non usano le risorse</span><span class="sxs-lookup"><span data-stu-id="a4fac-144">the services exist but aren't consuming the resources</span></span> 

<span data-ttu-id="a4fac-145">Per prenotare le risorse per un'istanza dell'applicazione è necessario definire due parametri aggiuntivi: *MinimumNodes* e *NodeReservationCapacity*</span><span class="sxs-lookup"><span data-stu-id="a4fac-145">Reserving resources for an application instance requires specifying two additional parameters: *MinimumNodes* and *NodeReservationCapacity*</span></span>

- <span data-ttu-id="a4fac-146">**MinimumNodes**: definisce il numero minimo di nodi con cui l'istanza dell'applicazione deve essere eseguita.</span><span class="sxs-lookup"><span data-stu-id="a4fac-146">**MinimumNodes** - Defines the minimum number of nodes that the application instance should run on.</span></span>  
- <span data-ttu-id="a4fac-147">**NodeReservationCapacity**: questa impostazione è per ogni metrica per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a4fac-147">**NodeReservationCapacity** - This setting is per metric for the application.</span></span> <span data-ttu-id="a4fac-148">Il valore è la quantità di tale metrica riservata per l'applicazione su ogni nodo in cui si eseguono i servizi dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a4fac-148">The value is the amount of that metric reserved for the application on any node where that the services in that application run.</span></span>

<span data-ttu-id="a4fac-149">La combinazione di **MinimumNodes** e **NodeReservationCapacity** garantisce una riserva minima del carico per l'applicazione all'interno del cluster.</span><span class="sxs-lookup"><span data-stu-id="a4fac-149">Combining **MinimumNodes** and **NodeReservationCapacity** guarantees a minimum load reservation for the application within the cluster.</span></span> <span data-ttu-id="a4fac-150">Se si ha meno capacità rimanente nel cluster rispetto al totale della riserva richiesta, la creazione dell'applicazione ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="a4fac-150">If there's less remaining capacity in the cluster than the total reservation required, creation of the application fails.</span></span> 

<span data-ttu-id="a4fac-151">Di seguito viene illustrato un esempio di come viene riservata la capacità:</span><span class="sxs-lookup"><span data-stu-id="a4fac-151">Let's look at an example of capacity reservation:</span></span>

<span data-ttu-id="a4fac-152"><center>
![Istanze di applicazione che definiscono la capacità riservata][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="a4fac-152"><center>
![Application Instances Defining Reserved Capacity][Image2]
</center></span></span>

<span data-ttu-id="a4fac-153">Nell'esempio a sinistra, le applicazioni non hanno una capacità definita.</span><span class="sxs-lookup"><span data-stu-id="a4fac-153">In the left example, applications do not have any Application Capacity defined.</span></span> <span data-ttu-id="a4fac-154">Cluster Resource Manager bilancia tutti gli elementi in base alle normali regole.</span><span class="sxs-lookup"><span data-stu-id="a4fac-154">The Cluster Resource Manager balances everything according to normal rules.</span></span>

<span data-ttu-id="a4fac-155">Nell'esempio a destra, si supponga che Applicazione1 sia stata creata con le impostazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a4fac-155">In the example on the right, let's say that Application1 was created with the following settings:</span></span>

- <span data-ttu-id="a4fac-156">MinimumNodes impostato su due</span><span class="sxs-lookup"><span data-stu-id="a4fac-156">MinimumNodes set to two</span></span>
- <span data-ttu-id="a4fac-157">Una metrica dell'applicazione definita con le impostazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a4fac-157">An application Metric defined with</span></span>
  - <span data-ttu-id="a4fac-158">NodeReservationCapacity pari a 20</span><span class="sxs-lookup"><span data-stu-id="a4fac-158">NodeReservationCapacity of 20</span></span>

<span data-ttu-id="a4fac-159">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4fac-159">Powershell</span></span>

 ``` posh
 New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MinimumNodes 2 -Metrics @("MetricName:Metric1,NodeReservationCapacity:20")
 ```

<span data-ttu-id="a4fac-160">C#</span><span class="sxs-lookup"><span data-stu-id="a4fac-160">C#</span></span>

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

<span data-ttu-id="a4fac-161">Service Fabric riserva la capacità in due nodi per Applicazione1 e non consente ai servizi da Applicazione2 di usare tale capacità, anche se non sono presenti carichi usati dai servizi all'interno di Applicazione1 al momento.</span><span class="sxs-lookup"><span data-stu-id="a4fac-161">Service Fabric reserves capacity on two nodes for Application1, and doesn't allow services from Application2 to consume that capacity even if there are no load is being consumed by the services inside Application1 at the time.</span></span> <span data-ttu-id="a4fac-162">Questa capacità riservata dell'applicazione viene considerata usata e conta a fronte della capacità residua del nodo e del cluster.</span><span class="sxs-lookup"><span data-stu-id="a4fac-162">This reserved application capacity is considered consumed  and counts against the remaining capacity on that node and within the cluster.</span></span>  <span data-ttu-id="a4fac-163">La riserva viene sottratta immediatamente dalla capacità del cluster rimanente, tuttavia il consumo riservato viene sottratto dalla capacità di un nodo specifico solo quando almeno un oggetto del servizio viene posizionato su di esso.</span><span class="sxs-lookup"><span data-stu-id="a4fac-163">The reservation is deducted from the remaining cluster capacity immediately, however the reserved consumption is deducted from the capacity of a specific node only when at least one service object is placed on it.</span></span> <span data-ttu-id="a4fac-164">Questa prenotazione successiva consente un utilizzo ottimale delle risorse e flessibilità, dal momento che le risorse sono riservate nei nodi solo quando necessario.</span><span class="sxs-lookup"><span data-stu-id="a4fac-164">This later reservation allows for flexibility and better resource utilization since resources are only reserved on nodes when needed.</span></span>

## <a name="obtaining-the-application-load-information"></a><span data-ttu-id="a4fac-165">Ottenimento delle informazioni sul carico dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="a4fac-165">Obtaining the application load information</span></span>
<span data-ttu-id="a4fac-166">Per ogni applicazione con una Capacità dell'applicazione definita per una o più metriche è possibile ottenere le informazioni relative al carico aggregato segnalato dalle repliche dei suoi servizi.</span><span class="sxs-lookup"><span data-stu-id="a4fac-166">For each application that has an Application Capacity defined for one or more metrics you can obtain the information about the aggregate load reported by replicas of its services.</span></span>

<span data-ttu-id="a4fac-167">Powershell:</span><span class="sxs-lookup"><span data-stu-id="a4fac-167">Powershell:</span></span>

``` posh
Get-ServiceFabricApplicationLoad –ApplicationName fabric:/MyApplication1
```

<span data-ttu-id="a4fac-168">C#</span><span class="sxs-lookup"><span data-stu-id="a4fac-168">C#</span></span>

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

<span data-ttu-id="a4fac-169">La query ApplicationLoad restituisce le informazioni di base sulla capacità dell'applicazione che è stata specificata.</span><span class="sxs-lookup"><span data-stu-id="a4fac-169">The ApplicationLoad query returns the basic information about Application Capacity that was specified for the application.</span></span> <span data-ttu-id="a4fac-170">Queste informazioni includono le informazioni sul numero minimo e massimo di nodi e sul numero attualmente occupato dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a4fac-170">This information includes the Minimum Nodes and Maximum Nodes info, and the number that the application is currently occupying.</span></span> <span data-ttu-id="a4fac-171">Sono inoltre incluse informazioni su ogni metrica di carico dell'applicazione, tra cui:</span><span class="sxs-lookup"><span data-stu-id="a4fac-171">It also includes information about each application load metric, including:</span></span>

* <span data-ttu-id="a4fac-172">Nome della metrica: nome della metrica.</span><span class="sxs-lookup"><span data-stu-id="a4fac-172">Metric Name: Name of the metric.</span></span>
* <span data-ttu-id="a4fac-173">Capacità di prenotazione: capacità riservata nel cluster per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="a4fac-173">Reservation Capacity: Cluster Capacity that is reserved in the cluster for this Application.</span></span>
* <span data-ttu-id="a4fac-174">Carico dell'applicazione: carico totale delle repliche figlio dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a4fac-174">Application Load: Total Load of this Application’s child replicas.</span></span>
* <span data-ttu-id="a4fac-175">Capacità dell'applicazione: valore massimo consentito di carico dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a4fac-175">Application Capacity: Maximum permitted value of Application Load.</span></span>

## <a name="removing-application-capacity"></a><span data-ttu-id="a4fac-176">Rimozione della capacità dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="a4fac-176">Removing Application Capacity</span></span>
<span data-ttu-id="a4fac-177">Dopo aver impostato i parametri di capacità per un'applicazione, questi parametri possono essere rimossi usando le API di aggiornamento dell'applicazione o i cmdlet PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a4fac-177">Once the Application Capacity parameters are set for an application, they can be removed using Update Application APIs or PowerShell cmdlets.</span></span> <span data-ttu-id="a4fac-178">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="a4fac-178">For example:</span></span>

``` posh
Update-ServiceFabricApplication –Name fabric:/MyApplication1 –RemoveApplicationCapacity

```

<span data-ttu-id="a4fac-179">Questo comando rimuove tutti i parametri di gestione della capacità dall'istanza dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a4fac-179">This command removes all Application capacity management parameters from the application instance.</span></span> <span data-ttu-id="a4fac-180">Ciò include MinimumNodes, MaximumNodes e le metriche dell'applicazione, se presenti.</span><span class="sxs-lookup"><span data-stu-id="a4fac-180">This includes MinimumNodes, MaximumNodes, and the Application's metrics, if any.</span></span> <span data-ttu-id="a4fac-181">L'effetto del comando è immediato.</span><span class="sxs-lookup"><span data-stu-id="a4fac-181">The effect of the command is immediate.</span></span> <span data-ttu-id="a4fac-182">Una volta eseguito il comando, Cluster Resource Manager usa il comportamento predefinito per la gestione delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="a4fac-182">After this command completes, the Cluster Resource Manager uses the default behavior for managing applications.</span></span> <span data-ttu-id="a4fac-183">I parametri di capacità dell'applicazione possono essere specificati nuovamente tramite `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.</span><span class="sxs-lookup"><span data-stu-id="a4fac-183">Application Capacity parameters can be specified again via `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.</span></span>

### <a name="restrictions-on-application-capacity"></a><span data-ttu-id="a4fac-184">Restrizioni relative alla capacità dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="a4fac-184">Restrictions on Application Capacity</span></span>
<span data-ttu-id="a4fac-185">Esistono diverse restrizioni da rispettare per i parametri di capacità dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a4fac-185">There are several restrictions on Application Capacity parameters that must be respected.</span></span> <span data-ttu-id="a4fac-186">Se sono presenti errori di convalida non viene apportata alcuna modifica.</span><span class="sxs-lookup"><span data-stu-id="a4fac-186">If there are validation errors no changes take place.</span></span>

- <span data-ttu-id="a4fac-187">Tutti i parametri di tipo integer devono essere numeri non negativi.</span><span class="sxs-lookup"><span data-stu-id="a4fac-187">All integer parameters must be non-negative numbers.</span></span>
- <span data-ttu-id="a4fac-188">MinimumNodes non deve essere mai maggiore di MaximumNodes.</span><span class="sxs-lookup"><span data-stu-id="a4fac-188">MinimumNodes must never be greater than MaximumNodes.</span></span>
- <span data-ttu-id="a4fac-189">Se definite, le capacità per una metrica di carico devono rispettare queste regole:</span><span class="sxs-lookup"><span data-stu-id="a4fac-189">If capacities for a load metric are defined, then they must follow these rules:</span></span>
  - <span data-ttu-id="a4fac-190">La capacità di prenotazione del nodo non deve essere maggiore della capacità massima del nodo.</span><span class="sxs-lookup"><span data-stu-id="a4fac-190">Node Reservation Capacity must not be greater than Maximum Node Capacity.</span></span> <span data-ttu-id="a4fac-191">Ad esempio, non è possibile limitare la capacità per la metrica "CPU" nel nodo a due unità e provare a prenotare tre unità in ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="a4fac-191">For example, you cannot limit the capacity for the metric “CPU” on the node to two units and try to reserve three units on each node.</span></span>
  - <span data-ttu-id="a4fac-192">Se viene specificato MaximumNodes, il prodotto di MaximumNodes e della capacità massima del nodo non deve essere maggiore della capacità totale dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a4fac-192">If MaximumNodes is specified, then the product of MaximumNodes and Maximum Node Capacity must not be greater than Total Application Capacity.</span></span> <span data-ttu-id="a4fac-193">Si supponga, ad esempio, che la capacità massima del nodo per la metrica di carico "CPU" sia impostata su 8.</span><span class="sxs-lookup"><span data-stu-id="a4fac-193">For example, let's say the Maximum Node Capacity for load metric “CPU” is set to eight.</span></span> <span data-ttu-id="a4fac-194">Si supponga anche che il numero massimo di nodi sia impostato su 10.</span><span class="sxs-lookup"><span data-stu-id="a4fac-194">Let's also say you set the Maximum Nodes to 10.</span></span> <span data-ttu-id="a4fac-195">In questo caso, la capacità totale dell'applicazione deve essere superiore a 80 per la metrica di carico.</span><span class="sxs-lookup"><span data-stu-id="a4fac-195">In this case, Total Application Capacity must be greater than 80 for this load metric.</span></span>

<span data-ttu-id="a4fac-196">Le restrizioni vengono applicate sia durante la creazione dell'applicazione sia durante i suoi aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="a4fac-196">The restrictions are enforced both during application creation and updates.</span></span>

## <a name="how-not-to-use-application-capacity"></a><span data-ttu-id="a4fac-197">Come usare la capacità dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="a4fac-197">How not to use Application Capacity</span></span>
- <span data-ttu-id="a4fac-198">Non tentare di usare le funzionalità dei gruppi di applicazioni per vincolare l'applicazione a uno _specifico_ subset di nodi.</span><span class="sxs-lookup"><span data-stu-id="a4fac-198">Do not try to use the Application Group features to constrain the application to a _specific_ subset of nodes.</span></span> <span data-ttu-id="a4fac-199">In altre parole, è possibile specificare che l'applicazione venga eseguita su un massimo di cinque nodi, ma non indicare i cinque nodi del cluster specifici.</span><span class="sxs-lookup"><span data-stu-id="a4fac-199">In other words, you can specify that the application runs on at most five nodes, but not which specific five nodes in the cluster.</span></span> <span data-ttu-id="a4fac-200">È possibile vincolare un'applicazione a nodi specifici usando i vincoli di posizionamento per i servizi.</span><span class="sxs-lookup"><span data-stu-id="a4fac-200">Constraining an application to specific nodes can be achieved using placement constraints for services.</span></span>
- <span data-ttu-id="a4fac-201">Non usare la capacità dell'applicazione per garantire che due servizi della stessa applicazione vengano sempre posizionati sugli stessi nodi.</span><span class="sxs-lookup"><span data-stu-id="a4fac-201">Do not try to use the Application Capacity to ensure that two services from the same application are placed on the same nodes.</span></span> <span data-ttu-id="a4fac-202">Usare invece [affinità](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) o [vincoli di posizionamento](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).</span><span class="sxs-lookup"><span data-stu-id="a4fac-202">Instead use [affinity](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) or [placement constraints](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4fac-203">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a4fac-203">Next steps</span></span>
- <span data-ttu-id="a4fac-204">Per altre informazioni sulla configurazione dei servizi, [Informazioni sulla configurazione dei servizi](service-fabric-cluster-resource-manager-configure-services.md)</span><span class="sxs-lookup"><span data-stu-id="a4fac-204">For more information on configuring services, [Learn about configuring Services](service-fabric-cluster-resource-manager-configure-services.md)</span></span>
- <span data-ttu-id="a4fac-205">Per informazioni sul modo in cui Cluster Resource Manager gestisce e bilancia il carico nel cluster, vedere l'articolo relativo al [bilanciamento del carico](service-fabric-cluster-resource-manager-balancing.md)</span><span class="sxs-lookup"><span data-stu-id="a4fac-205">To find out about how the Cluster Resource Manager manages and balances load in the cluster, check out the article on [balancing load](service-fabric-cluster-resource-manager-balancing.md)</span></span>
- <span data-ttu-id="a4fac-206">Partire dall'inizio e vedere l' [introduzione a Cluster Resource Manager di Service Fabric](service-fabric-cluster-resource-manager-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="a4fac-206">Start from the beginning and [get an Introduction to the Service Fabric Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)</span></span>
- <span data-ttu-id="a4fac-207">Per altre informazioni sul funzionamento generale delle metriche, vedere l'articolo sulle [metriche di carico di Service Fabric](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="a4fac-207">For more information on how metrics work generally, read up on [Service Fabric Load Metrics](service-fabric-cluster-resource-manager-metrics.md)</span></span>
- <span data-ttu-id="a4fac-208">Cluster Resource Manager dispone di varie opzioni per descrivere il cluster.</span><span class="sxs-lookup"><span data-stu-id="a4fac-208">The Cluster Resource Manager has many options for describing the cluster.</span></span> <span data-ttu-id="a4fac-209">Per altre informazioni a riguardo vedere l'articolo [Descrivere un cluster di Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md)</span><span class="sxs-lookup"><span data-stu-id="a4fac-209">To find out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-max-nodes.png
[Image2]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-reserved-capacity.png
