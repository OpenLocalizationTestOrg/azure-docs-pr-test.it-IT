---
title: servizi di Service Fabric aaaPartitioning | Documenti Microsoft
description: Viene descritto come servizi con stati di toopartition Service Fabric. Partizioni consente l'archiviazione dei dati sul computer locale hello in modo da dati e calcolo possono essere ridimensionate, insieme.
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 3b7248c8-ea92-4964-85e7-6f1291b5cc7b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: msfussell
ms.openlocfilehash: 6ead48716c08f4212535202ee69d169067d5c6d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="partition-service-fabric-reliable-services"></a><span data-ttu-id="2f498-104">Partizionare Reliable Services di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2f498-104">Partition Service Fabric reliable services</span></span>
<span data-ttu-id="2f498-105">Questo articolo fornisce un'introduzione toohello concetti di base di servizi di Azure Service Fabric affidabili di partizionamento.</span><span class="sxs-lookup"><span data-stu-id="2f498-105">This article provides an introduction toohello basic concepts of partitioning Azure Service Fabric reliable services.</span></span> <span data-ttu-id="2f498-106">Hello codice sorgente utilizzato nell'articolo hello disponibile anche su [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span><span class="sxs-lookup"><span data-stu-id="2f498-106">hello source code used in hello article is also available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span></span>

## <a name="partitioning"></a><span data-ttu-id="2f498-107">Partizionamento</span><span class="sxs-lookup"><span data-stu-id="2f498-107">Partitioning</span></span>
<span data-ttu-id="2f498-108">Il partizionamento non è univoco tooService dell'infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="2f498-108">Partitioning is not unique tooService Fabric.</span></span> <span data-ttu-id="2f498-109">bensì si tratta di un modello di base per la creazione di servizi scalabili.</span><span class="sxs-lookup"><span data-stu-id="2f498-109">In fact, it is a core pattern of building scalable services.</span></span> <span data-ttu-id="2f498-110">In senso più ampio, è possibile considerare di partizionamento come concetto della divisione di stato (dati) e di calcolo di prestazioni e scalabilità di tooimprove accessibile unità più piccole.</span><span class="sxs-lookup"><span data-stu-id="2f498-110">In a broader sense, we can think about partitioning as a concept of dividing state (data) and compute into smaller accessible units tooimprove scalability and performance.</span></span> <span data-ttu-id="2f498-111">Una forma molto conosciuta di partizionamento è il [partizionamento dei dati][wikipartition], noto anche come partizionamento orizzontale.</span><span class="sxs-lookup"><span data-stu-id="2f498-111">A well-known form of partitioning is [data partitioning][wikipartition], also known as sharding.</span></span>

### <a name="partition-service-fabric-stateless-services"></a><span data-ttu-id="2f498-112">Partizionamento dei servizi senza stato di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2f498-112">Partition Service Fabric stateless services</span></span>
<span data-ttu-id="2f498-113">Per i servizi senza stato un partizionamento può essere considerato un'unità logica contenente una o più istanze di un servizio.</span><span class="sxs-lookup"><span data-stu-id="2f498-113">For stateless services, you can think about a partition being a logical unit that contains one or more instances of a service.</span></span> <span data-ttu-id="2f498-114">La figura 1 illustra un servizio senza stato con cinque istanze distribuite in un cluster usando una partizione.</span><span class="sxs-lookup"><span data-stu-id="2f498-114">Figure 1 shows a stateless service with five instances distributed across a cluster using one partition.</span></span>

![Servizio senza stato](./media/service-fabric-concepts-partitioning/statelessinstances.png)

<span data-ttu-id="2f498-116">Sono disponibili due tipi di soluzioni di servizio senza stato.</span><span class="sxs-lookup"><span data-stu-id="2f498-116">There are really two types of stateless service solutions.</span></span> <span data-ttu-id="2f498-117">Hello prima uno è un servizio che rende persistente lo stato esternamente, ad esempio in un database SQL di Azure (ad esempio, un sito Web che archivia i dati e le informazioni sulla sessione hello).</span><span class="sxs-lookup"><span data-stu-id="2f498-117">hello first one is a service that persists its state externally, for example in an Azure SQL database (like a website that stores hello session information and data).</span></span> <span data-ttu-id="2f498-118">Hello secondo è solo calcolo servizi (come anteprima una calcolatrice o immagine) che non si gestiscono qualsiasi stato persistente.</span><span class="sxs-lookup"><span data-stu-id="2f498-118">hello second one is computation-only services (like a calculator or image thumbnailing) that do not manage any persistent state.</span></span>

<span data-ttu-id="2f498-119">In entrambi i casi, il partizionamento di un servizio senza stato è uno scenario molto raro e la scalabilità e la disponibilità in genere si ottengono aggiungendo altre istanze.</span><span class="sxs-lookup"><span data-stu-id="2f498-119">In either case, partitioning a stateless service is a very rare scenario--scalability and availability are normally achieved by adding more instances.</span></span> <span data-ttu-id="2f498-120">Hello solo tempo tooconsider più partizioni per le istanze del servizio senza stato è quando è necessario toomeet speciali routing delle richieste.</span><span class="sxs-lookup"><span data-stu-id="2f498-120">hello only time you want tooconsider multiple partitions for stateless service instances is when you need toomeet special routing requests.</span></span>

<span data-ttu-id="2f498-121">ad esempio, quando gli utenti con ID compresi in un determinato intervallo devono essere gestiti solo da una particolare istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="2f498-121">As an example, consider a case where users with IDs in a certain range should only be served by a particular service instance.</span></span> <span data-ttu-id="2f498-122">Un altro esempio di quando è possibile partizionare un servizio senza stato è quando si dispone di un back-end realmente partizionato (ad esempio un database SQL partizionato) e si desidera toocontrol quale istanza del servizio deve scrivere toohello partizioni di database, o eseguire altre operazioni di preparazione all'interno di Hello servizio senza stato che richiede hello stesso le informazioni di partizionamento come viene utilizzato nel back-end hello.</span><span class="sxs-lookup"><span data-stu-id="2f498-122">Another example of when you could partition a stateless service is when you have a truly partitioned backend (e.g. a sharded SQL database) and you want toocontrol which service instance should write toohello database shard--or perform other preparation work within hello stateless service that requires hello same partitioning information as is used in hello backend.</span></span> <span data-ttu-id="2f498-123">Tali tipi di scenario possono essere risolti anche in modo diverso e non richiedono necessariamente il partizionamento del servizio.</span><span class="sxs-lookup"><span data-stu-id="2f498-123">Those types of scenarios can also be solved in different ways and do not necessarily require service partitioning.</span></span>

<span data-ttu-id="2f498-124">resto Hello di questa procedura dettagliata si concentra sui servizi con stato.</span><span class="sxs-lookup"><span data-stu-id="2f498-124">hello remainder of this walkthrough focuses on stateful services.</span></span>

### <a name="partition-service-fabric-stateful-services"></a><span data-ttu-id="2f498-125">Partizionamento dei servizi con stato di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2f498-125">Partition Service Fabric stateful services</span></span>
<span data-ttu-id="2f498-126">Service Fabric rende servizi con stato scalabili toodevelop facile offrendo un modo di prima classe toopartition stato (dati).</span><span class="sxs-lookup"><span data-stu-id="2f498-126">Service Fabric makes it easy toodevelop scalable stateful services by offering a first-class way toopartition state (data).</span></span> <span data-ttu-id="2f498-127">Concettualmente, si pensi a una partizione di un servizio con stato come unità di scala che è altamente affidabile tramite [repliche](service-fabric-availability-services.md) che vengono distribuiti e bilanciati tra i nodi di hello in un cluster.</span><span class="sxs-lookup"><span data-stu-id="2f498-127">Conceptually, you can think about a partition of a stateful service as a scale unit that is highly reliable through [replicas](service-fabric-availability-services.md) that are distributed and balanced across hello nodes in a cluster.</span></span>

<span data-ttu-id="2f498-128">Il partizionamento nel contesto di hello di servizi di Service Fabric con stati, si riferisce toohello processo di individuazione che una partizione specifica del servizio è responsabile di una parte di hello stato completo nello stato del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="2f498-128">Partitioning in hello context of Service Fabric stateful services refers toohello process of determining that a particular service partition is responsible for a portion of hello complete state of hello service.</span></span> <span data-ttu-id="2f498-129">Come accennato in precedenza, la partizione è un set di [repliche](service-fabric-availability-services.md).</span><span class="sxs-lookup"><span data-stu-id="2f498-129">(As mentioned before, a partition is a set of [replicas](service-fabric-availability-services.md)).</span></span> <span data-ttu-id="2f498-130">Un aspetto interessante di Service Fabric è che le partizioni hello viene inserito in nodi diversi.</span><span class="sxs-lookup"><span data-stu-id="2f498-130">A great thing about Service Fabric is that it places hello partitions on different nodes.</span></span> <span data-ttu-id="2f498-131">In questo modo il limite di risorse del nodo di toogrow tooa.</span><span class="sxs-lookup"><span data-stu-id="2f498-131">This allows them toogrow tooa node's resource limit.</span></span> <span data-ttu-id="2f498-132">Quando sono necessari dati hello aumento delle dimensioni, partizioni di aumento delle dimensioni e Service Fabric eseguito il ribilanciamento delle partizioni tra i nodi.</span><span class="sxs-lookup"><span data-stu-id="2f498-132">As hello data needs grow, partitions grow, and Service Fabric rebalances partitions across nodes.</span></span> <span data-ttu-id="2f498-133">In questo modo hello continua utilizzo efficiente delle risorse hardware.</span><span class="sxs-lookup"><span data-stu-id="2f498-133">This ensures hello continued efficient use of hardware resources.</span></span>

<span data-ttu-id="2f498-134">toogive ad esempio, affermare che iniziano con un cluster di 5 nodi e un servizio che viene configurato toohave 10 partizioni e una destinazione di tre repliche.</span><span class="sxs-lookup"><span data-stu-id="2f498-134">toogive you an example, say you start with a 5-node cluster and a service that is configured toohave 10 partitions and a target of three replicas.</span></span> <span data-ttu-id="2f498-135">In questo caso, Service Fabric potrebbe bilanciare repliche hello cluster hello - e distribuire alla fine si avrebbero primario due [repliche](service-fabric-availability-services.md) per ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="2f498-135">In this case, Service Fabric would balance and distribute hello replicas across hello cluster--and you would end up with two primary [replicas](service-fabric-availability-services.md) per node.</span></span>
<span data-ttu-id="2f498-136">Se è necessario ora tooscale out too10 i nodi del cluster di hello, Service Fabric sarebbe ribilanciare primario hello [repliche](service-fabric-availability-services.md) in tutti i nodi di 10.</span><span class="sxs-lookup"><span data-stu-id="2f498-136">If you now need tooscale out hello cluster too10 nodes, Service Fabric would rebalance hello primary [replicas](service-fabric-availability-services.md) across all 10 nodes.</span></span> <span data-ttu-id="2f498-137">Analogamente, se è ridimensionata nodi too5 indietro, Service Fabric sarebbe ribilanciare tutte le repliche di hello nei nodi hello 5.</span><span class="sxs-lookup"><span data-stu-id="2f498-137">Likewise, if you scaled back too5 nodes, Service Fabric would rebalance all hello replicas across hello 5 nodes.</span></span>  

<span data-ttu-id="2f498-138">Figura 2 mostra hello distribuzione 10 partizioni prima e dopo il ridimensionamento cluster hello.</span><span class="sxs-lookup"><span data-stu-id="2f498-138">Figure 2 shows hello distribution of 10 partitions before and after scaling hello cluster.</span></span>

![Servizio con stato](./media/service-fabric-concepts-partitioning/partitions.png)

<span data-ttu-id="2f498-140">Di conseguenza, hello scalabilità orizzontale è possibile ottenere poiché le richieste dai client vengono distribuite tra più computer, un miglioramento delle prestazioni complessive dell'applicazione hello e viene ridotto il conflitto su toochunks accesso dei dati.</span><span class="sxs-lookup"><span data-stu-id="2f498-140">As a result, hello scale-out is achieved since requests from clients are distributed across computers, overall performance of hello application is improved, and contention on access toochunks of data is reduced.</span></span>

## <a name="plan-for-partitioning"></a><span data-ttu-id="2f498-141">Pianificazione del partizionamento</span><span class="sxs-lookup"><span data-stu-id="2f498-141">Plan for partitioning</span></span>
<span data-ttu-id="2f498-142">Prima di implementare un servizio, è necessario considerare sempre hello strategia che è necessario tooscale out di partizionamento. Esistono diversi modi, ma tutti gli elementi concentrarsi su quale applicazione hello deve tooachieve.</span><span class="sxs-lookup"><span data-stu-id="2f498-142">Before implementing a service, you should always consider hello partitioning strategy that is required tooscale out. There are different ways, but all of them focus on what hello application needs tooachieve.</span></span> <span data-ttu-id="2f498-143">Per il contesto di hello di questo articolo, si prendano in considerazione alcune hello aspetti più importanti.</span><span class="sxs-lookup"><span data-stu-id="2f498-143">For hello context of this article, let's consider some of hello more important aspects.</span></span>

<span data-ttu-id="2f498-144">Un buon approccio è toothink sulla struttura hello dello stato di hello necessarie toobe partizionata, come primo passaggio hello.</span><span class="sxs-lookup"><span data-stu-id="2f498-144">A good approach is toothink about hello structure of hello state that needs toobe partitioned, as hello first step.</span></span>

<span data-ttu-id="2f498-145">Un semplice esempio viene riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="2f498-145">Let's take a simple example.</span></span> <span data-ttu-id="2f498-146">Se fosse un servizio per un sondaggio countywide toobuild, è possibile creare una partizione per ogni città regione hello.</span><span class="sxs-lookup"><span data-stu-id="2f498-146">If you were toobuild a service for a countywide poll, you could create a partition for each city in hello county.</span></span> <span data-ttu-id="2f498-147">Quindi, si potrebbe archiviare hello voti per ogni persona città hello nella partizione hello corrispondente toothat città.</span><span class="sxs-lookup"><span data-stu-id="2f498-147">Then, you could store hello votes for every person in hello city in hello partition that corresponds toothat city.</span></span> <span data-ttu-id="2f498-148">Figura 3 viene illustrato un set di utenti e hello città in cui risiedono.</span><span class="sxs-lookup"><span data-stu-id="2f498-148">Figure 3 illustrates a set of people and hello city in which they reside.</span></span>

![Partizione semplice](./media/service-fabric-concepts-partitioning/cities.png)

<span data-ttu-id="2f498-150">Come il popolamento di città hello varia notevolmente, si rischia di con alcune partizioni che contengono una grande quantità di dati (ad esempio, Seattle) e le altre partizioni con stato molto piccolo (ad esempio Kirkland).</span><span class="sxs-lookup"><span data-stu-id="2f498-150">As hello population of cities varies widely, you may end up with some partitions that contain a lot of data (e.g. Seattle) and other partitions with very little state (e.g. Kirkland).</span></span> <span data-ttu-id="2f498-151">Cos'è impatto hello della presenza di partizioni con una quantità non uniforme di stato?</span><span class="sxs-lookup"><span data-stu-id="2f498-151">So what is hello impact of having partitions with uneven amounts of state?</span></span>

<span data-ttu-id="2f498-152">Se si pensa esempio hello nuovamente, è possibile visualizzare facilmente che partizione hello contenente hello voti per Seattle consentirà di ottenere più traffico Kirkland hello uno.</span><span class="sxs-lookup"><span data-stu-id="2f498-152">If you think about hello example again, you can easily see that hello partition that holds hello votes for Seattle will get more traffic than hello Kirkland one.</span></span> <span data-ttu-id="2f498-153">Per impostazione predefinita, Service Fabric garantisce che sia presente su hello stesso numero di repliche primarie e secondarie in ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="2f498-153">By default, Service Fabric makes sure that there is about hello same number of primary and secondary replicas on each node.</span></span> <span data-ttu-id="2f498-154">perciò si potrebbero avere nodi contenenti repliche che gestiscono più traffico e altre che gestiscono meno traffico.</span><span class="sxs-lookup"><span data-stu-id="2f498-154">So you may end up with nodes that hold replicas that serve more traffic and others that serve less traffic.</span></span> <span data-ttu-id="2f498-155">Preferibilmente si tooavoid a caldo e freddi aree come segue in un cluster.</span><span class="sxs-lookup"><span data-stu-id="2f498-155">You would preferably want tooavoid hot and cold spots like this in a cluster.</span></span>

<span data-ttu-id="2f498-156">In ordine tooavoid questo, è necessario eseguire due operazioni, da un punto di vista di partizionamento:</span><span class="sxs-lookup"><span data-stu-id="2f498-156">In order tooavoid this, you should do two things, from a partitioning point of view:</span></span>

* <span data-ttu-id="2f498-157">Provare a stato hello toopartition in modo che viene distribuito uniformemente tra tutte le partizioni.</span><span class="sxs-lookup"><span data-stu-id="2f498-157">Try toopartition hello state so that it is evenly distributed across all partitions.</span></span>
* <span data-ttu-id="2f498-158">Caricamento di report da ognuna delle repliche hello per servizio hello.</span><span class="sxs-lookup"><span data-stu-id="2f498-158">Report load from each of hello replicas for hello service.</span></span> <span data-ttu-id="2f498-159">Per informazioni su come fare, vedere l'articolo relativo a [metriche e carico](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="2f498-159">(For information on how, check out this article on [Metrics and Load](service-fabric-cluster-resource-manager-metrics.md)).</span></span> <span data-ttu-id="2f498-160">Service Fabric fornisce hello. funzionalità il carico di tooreport utilizzato da servizi, ad esempio quantità di memoria o un numero di record.</span><span class="sxs-lookup"><span data-stu-id="2f498-160">Service Fabric provides hello capability tooreport load consumed by services, such as amount of memory or number of records.</span></span> <span data-ttu-id="2f498-161">In base alle metriche di hello segnalate, Service Fabric rileva che alcune partizioni servono carichi più elevati rispetto ad altri ed eseguito il ribilanciamento cluster hello mobile repliche toomore adatto nodi, in modo che complessivo non è sottoposto a overload alcun nodo.</span><span class="sxs-lookup"><span data-stu-id="2f498-161">Based on hello metrics reported, Service Fabric detects that some partitions are serving higher loads than others and rebalances hello cluster by moving replicas toomore suitable nodes, so that overall no node is overloaded.</span></span>

<span data-ttu-id="2f498-162">A volte non è possibile sapere quanti dati saranno presenti in una determinata partizione</span><span class="sxs-lookup"><span data-stu-id="2f498-162">Sometimes, you cannot know how much data will be in a given partition.</span></span> <span data-ttu-id="2f498-163">Pertanto una raccomandazione generale è toodo entrambi - prima di tutto, adottando una strategia di partizionamento che distribuisce hello dati in modo uniforme tra partizioni hello e i secondi, dal carico di report.</span><span class="sxs-lookup"><span data-stu-id="2f498-163">So a general recommendation is toodo both--first, by adopting a partitioning strategy that spreads hello data evenly across hello partitions and second, by reporting load.</span></span>  <span data-ttu-id="2f498-164">primo metodo Hello impedisce situazioni descritte hello voto di esempio, anche se hello secondo consente di arrotondare i temporanee differenze in access o di carico nel tempo.</span><span class="sxs-lookup"><span data-stu-id="2f498-164">hello first method prevents situations described in hello voting example, while hello second helps smooth out temporary differences in access or load over time.</span></span>

<span data-ttu-id="2f498-165">Un altro aspetto della pianificazione di partizione è numero corretto di hello toochoose di toobegin partizioni con.</span><span class="sxs-lookup"><span data-stu-id="2f498-165">Another aspect of partition planning is toochoose hello correct number of partitions toobegin with.</span></span>
<span data-ttu-id="2f498-166">Dal punto di vista di Service Fabric, nulla impedisce di iniziare con un numero di partizioni maggiore di quello anticipato per lo scenario.</span><span class="sxs-lookup"><span data-stu-id="2f498-166">From a Service Fabric perspective, there is nothing that prevents you from starting out with a higher number of partitions than anticipated for your scenario.</span></span>
<span data-ttu-id="2f498-167">In realtà, presupponendo che il numero massimo di hello di partizioni è un approccio valido.</span><span class="sxs-lookup"><span data-stu-id="2f498-167">In fact, assuming hello maximum number of partitions is a valid approach.</span></span>

<span data-ttu-id="2f498-168">Raramente saranno necessarie più partizioni di quelle scelte inizialmente.</span><span class="sxs-lookup"><span data-stu-id="2f498-168">In rare cases, you may end up needing more partitions than you have initially chosen.</span></span> <span data-ttu-id="2f498-169">Come è possibile modificare il numero di partizioni hello dopo hello, sarebbe necessario tooapply alcuni approcci partizione avanzate, ad esempio la creazione di una nuova istanza del servizio di hello stesso tipo di servizio.</span><span class="sxs-lookup"><span data-stu-id="2f498-169">As you cannot change hello partition count after hello fact, you would need tooapply some advanced partition approaches, such as creating a new service instance of hello same service type.</span></span> <span data-ttu-id="2f498-170">È inoltre necessario tooimplement logica sul lato client che indirizza hello richiede l'istanza del servizio corretto toohello, in base alle informazioni sul lato client che il codice client deve gestire.</span><span class="sxs-lookup"><span data-stu-id="2f498-170">You would also need tooimplement some client-side logic that routes hello requests toohello correct service instance, based on client-side knowledge that your client code must maintain.</span></span>

<span data-ttu-id="2f498-171">Un'altra considerazione per il partizionamento di pianificazione è risorse del computer disponibile hello.</span><span class="sxs-lookup"><span data-stu-id="2f498-171">Another consideration for partitioning planning is hello available computer resources.</span></span> <span data-ttu-id="2f498-172">Quando lo stato di hello esigenze toobe accessibili e archiviati, si sta toofollow associato:</span><span class="sxs-lookup"><span data-stu-id="2f498-172">As hello state needs toobe accessed and stored, you are bound toofollow:</span></span>

* <span data-ttu-id="2f498-173">Larghezza di banda della rete</span><span class="sxs-lookup"><span data-stu-id="2f498-173">Network bandwidth limits</span></span>
* <span data-ttu-id="2f498-174">Memoria di sistema</span><span class="sxs-lookup"><span data-stu-id="2f498-174">System memory limits</span></span>
* <span data-ttu-id="2f498-175">Archiviazione su disco</span><span class="sxs-lookup"><span data-stu-id="2f498-175">Disk storage limits</span></span>

<span data-ttu-id="2f498-176">Ma cosa accade se si verificano i vincoli di risorse in un cluster in esecuzione? risposte Hello sono che è semplicemente possibile scalare orizzontalmente hello cluster tooaccommodate hello nuovi requisiti.</span><span class="sxs-lookup"><span data-stu-id="2f498-176">So what happens if you run into resource constraints in a running cluster? hello answer is that you can simply scale out hello cluster tooaccommodate hello new requirements.</span></span>

<span data-ttu-id="2f498-177">[Guida alla pianificazione della capacità di Hello](service-fabric-capacity-planning.md) offre indicazioni per il toodetermine il numero di nodi del cluster è necessario.</span><span class="sxs-lookup"><span data-stu-id="2f498-177">[hello capacity planning guide](service-fabric-capacity-planning.md) offers guidance for how toodetermine how many nodes your cluster needs.</span></span>

## <a name="get-started-with-partitioning"></a><span data-ttu-id="2f498-178">Introduzione al partizionamento</span><span class="sxs-lookup"><span data-stu-id="2f498-178">Get started with partitioning</span></span>
<span data-ttu-id="2f498-179">In questa sezione viene descritto come tooget iniziare con il partizionamento del servizio.</span><span class="sxs-lookup"><span data-stu-id="2f498-179">This section describes how tooget started with partitioning your service.</span></span>

<span data-ttu-id="2f498-180">In primo luogo Service Fabric consente di scegliere tra tre schemi di partizione:</span><span class="sxs-lookup"><span data-stu-id="2f498-180">Service Fabric offers a choice of three partition schemes:</span></span>

* <span data-ttu-id="2f498-181">Partizionamento con intervallo (noto anche come UniformInt64Partition).</span><span class="sxs-lookup"><span data-stu-id="2f498-181">Ranged partitioning (otherwise known as UniformInt64Partition).</span></span>
* <span data-ttu-id="2f498-182">Partizionamento denominato.</span><span class="sxs-lookup"><span data-stu-id="2f498-182">Named partitioning.</span></span> <span data-ttu-id="2f498-183">Le applicazioni che usano questo modello in genere hanno dati che possono essere inseriti in un bucket, in un set associato.</span><span class="sxs-lookup"><span data-stu-id="2f498-183">Applications using this model usually have data that can be bucketed, within a bounded set.</span></span> <span data-ttu-id="2f498-184">Aree, codici postali, gruppi di clienti o altri limiti aziendali sono alcuni esempi comuni di campi dati usati come chiavi di partizione denominata.</span><span class="sxs-lookup"><span data-stu-id="2f498-184">Some common examples of data fields used as named partition keys would be regions, postal codes, customer groups, or other business boundaries.</span></span>
* <span data-ttu-id="2f498-185">Partizionamento singleton.</span><span class="sxs-lookup"><span data-stu-id="2f498-185">Singleton partitioning.</span></span> <span data-ttu-id="2f498-186">Partizioni singleton vengono utilizzate in genere quando il servizio di hello non richiede alcun aggiuntive di routing.</span><span class="sxs-lookup"><span data-stu-id="2f498-186">Singleton partitions are typically used when hello service does not require any additional routing.</span></span> <span data-ttu-id="2f498-187">I servizi senza stato, ad esempio, usano questo schema di partizionamento per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="2f498-187">For example, stateless services use this partitioning scheme by default.</span></span>

<span data-ttu-id="2f498-188">Gli schemi di partizionamento denominato e singleton sono forme particolari di partizioni con intervalli.</span><span class="sxs-lookup"><span data-stu-id="2f498-188">Named and Singleton partitioning schemes are special forms of ranged partitions.</span></span> <span data-ttu-id="2f498-189">Per impostazione predefinita, i modelli di Visual Studio hello per l'utilizzo di Service Fabric intervallo incluso il partizionamento, perché è hello uno più comune e utile.</span><span class="sxs-lookup"><span data-stu-id="2f498-189">By default, hello Visual Studio templates for Service Fabric use ranged partitioning, as it is hello most common and useful one.</span></span> <span data-ttu-id="2f498-190">resto Hello di questo articolo illustra lo schema di partizionamento nell'intervallo di hello.</span><span class="sxs-lookup"><span data-stu-id="2f498-190">hello remainder of this article focuses on hello ranged partitioning scheme.</span></span>

### <a name="ranged-partitioning-scheme"></a><span data-ttu-id="2f498-191">Schema di partizionamento con intervallo</span><span class="sxs-lookup"><span data-stu-id="2f498-191">Ranged partitioning scheme</span></span>
<span data-ttu-id="2f498-192">Si tratta di toospecify usato un numero intero intervalli (identificate da una chiave inferiore e chiave superiore) e un numero di partizioni (n).</span><span class="sxs-lookup"><span data-stu-id="2f498-192">This is used toospecify an integer range (identified by a low key and high key) and a number of partitions (n).</span></span> <span data-ttu-id="2f498-193">Crea partizioni n, ognuno responsabile di un intervallo secondario non sovrapposti di hello complessiva intervalli di chiavi di partizione.</span><span class="sxs-lookup"><span data-stu-id="2f498-193">It creates n partitions, each responsible for a non-overlapping subrange of hello overall partition key range.</span></span> <span data-ttu-id="2f498-194">Ad esempio, uno schema di partizionamento con intervallo con una chiave minima 0, una chiave massima 99 e un conteggio pari a 4 creerà quattro partizioni come mostrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="2f498-194">For example, a ranged partitioning scheme with a low key of 0, a high key of 99, and a count of 4 would create four partitions, as shown below.</span></span>

![Partizionamento per intervalli](./media/service-fabric-concepts-partitioning/range-partitioning.png)

<span data-ttu-id="2f498-196">Un approccio comune è un hash basato su una chiave univoca nel set di dati hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="2f498-196">A common approach is toocreate a hash based on a unique key within hello data set.</span></span> <span data-ttu-id="2f498-197">Sono esempi comuni di chiavi un Vehicle Identification Number (VIN), l'ID di un dipendente o una stringa univoca.</span><span class="sxs-lookup"><span data-stu-id="2f498-197">Some common examples of keys would be a vehicle identification number (VIN), an employee ID, or a unique string.</span></span> <span data-ttu-id="2f498-198">Usando questa chiave univoca, si potrebbe quindi generare un codice hash, l'intervallo di chiavi di modulo hello, toouse come chiave.</span><span class="sxs-lookup"><span data-stu-id="2f498-198">By using this unique key, you would then generate a hash code, modulus hello key range, toouse as your key.</span></span> <span data-ttu-id="2f498-199">È possibile specificare hello superiore e inferiore di hello chiave intervallo consentito.</span><span class="sxs-lookup"><span data-stu-id="2f498-199">You can specify hello upper and lower bounds of hello allowed key range.</span></span>

### <a name="select-a-hash-algorithm"></a><span data-ttu-id="2f498-200">Selezionare un algoritmo di hash</span><span class="sxs-lookup"><span data-stu-id="2f498-200">Select a hash algorithm</span></span>
<span data-ttu-id="2f498-201">Una parte importante della generazione di un hash è rappresentata dalla selezione dell'algoritmo di hash.</span><span class="sxs-lookup"><span data-stu-id="2f498-201">An important part of hashing is selecting your hash algorithm.</span></span> <span data-ttu-id="2f498-202">Una considerazione importante è se obiettivo hello toogroup chiavi simili vicini (sensibili hashing località), o se l'attività deve essere distribuito su vasta scala tra tutte le partizioni (distribuzione hash), che sono più comuni.</span><span class="sxs-lookup"><span data-stu-id="2f498-202">A consideration is whether hello goal is toogroup similar keys near each other (locality sensitive hashing)--or if activity should be distributed broadly across all partitions (distribution hashing), which is more common.</span></span>

<span data-ttu-id="2f498-203">sono riportate le caratteristiche di Hello di un algoritmo di hash di distribuzione valido che è facile toocompute dispone di alcuni conflitti e distribuisce chiavi di hello in modo uniforme.</span><span class="sxs-lookup"><span data-stu-id="2f498-203">hello characteristics of a good distribution hashing algorithm are that it is easy toocompute, it has few collisions, and it distributes hello keys evenly.</span></span> <span data-ttu-id="2f498-204">Un buon esempio di un algoritmo hash efficiente è hello [FNV 1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) algoritmo hash.</span><span class="sxs-lookup"><span data-stu-id="2f498-204">A good example of an efficient hash algorithm is hello [FNV-1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) hash algorithm.</span></span>

<span data-ttu-id="2f498-205">Un'ottima risorsa per le scelte di algoritmo di hash generale codice è hello [pagina di Wikipedia sulle funzioni hash](http://en.wikipedia.org/wiki/Hash_function).</span><span class="sxs-lookup"><span data-stu-id="2f498-205">A good resource for general hash code algorithm choices is hello [Wikipedia page on hash functions](http://en.wikipedia.org/wiki/Hash_function).</span></span>

## <a name="build-a-stateful-service-with-multiple-partitions"></a><span data-ttu-id="2f498-206">Compilare un servizio con stato con più partizioni</span><span class="sxs-lookup"><span data-stu-id="2f498-206">Build a stateful service with multiple partitions</span></span>
<span data-ttu-id="2f498-207">Ora verrà creato il primo servizio con stato affidabile con più partizioni.</span><span class="sxs-lookup"><span data-stu-id="2f498-207">Let's create your first reliable stateful service with multiple partitions.</span></span> <span data-ttu-id="2f498-208">In questo esempio, si creerà un'applicazione molto semplice in cui si desidera toostore tutti i cognomi che iniziano con hello stessa lettera di hello stessa partizione.</span><span class="sxs-lookup"><span data-stu-id="2f498-208">In this example, you will build a very simple application where you want toostore all last names that start with hello same letter in hello same partition.</span></span>

<span data-ttu-id="2f498-209">Prima di scrivere alcun codice, è necessario toothink sulle partizioni hello e le chiavi di partizione.</span><span class="sxs-lookup"><span data-stu-id="2f498-209">Before you write any code, you need toothink about hello partitions and partition keys.</span></span> <span data-ttu-id="2f498-210">È necessario 26 partizioni (uno per ogni lettera nell'alfabeto hello), ma su hello superiore e inferiore delle chiavi?</span><span class="sxs-lookup"><span data-stu-id="2f498-210">You need 26 partitions (one for each letter in hello alphabet), but what about hello low and high keys?</span></span>
<span data-ttu-id="2f498-211">Come si desidera letteralmente toohave una partizione per ogni lettera, è possibile usare 0 come chiave bassa hello e 25 come chiave alta hello, ogni lettera è la propria chiave.</span><span class="sxs-lookup"><span data-stu-id="2f498-211">As we literally want toohave one partition per letter, we can use 0 as hello low key and 25 as hello high key, as each letter is its own key.</span></span>

> [!NOTE]
> <span data-ttu-id="2f498-212">Si tratta di uno scenario semplificato, come in realtà distribuzione hello sarebbe non uniforme.</span><span class="sxs-lookup"><span data-stu-id="2f498-212">This is a simplified scenario, as in reality hello distribution would be uneven.</span></span> <span data-ttu-id="2f498-213">Cognome inizia con la lettera di hello "S" o "M" sono più comuni di quelli hello a partire da "X" o "Y".</span><span class="sxs-lookup"><span data-stu-id="2f498-213">Last names starting with hello letters "S" or "M" are more common than hello ones starting with "X" or "Y".</span></span>
> 
> 

1. <span data-ttu-id="2f498-214">Aprire **Visual Studio** > **File** > **Nuovo** > **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="2f498-214">Open **Visual Studio** > **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="2f498-215">In hello **nuovo progetto** finestra di dialogo, scegliere un'applicazione hello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2f498-215">In hello **New Project** dialog box, choose hello Service Fabric application.</span></span>
3. <span data-ttu-id="2f498-216">Denominare il progetto di hello "AlphabetPartitions".</span><span class="sxs-lookup"><span data-stu-id="2f498-216">Call hello project "AlphabetPartitions".</span></span>
4. <span data-ttu-id="2f498-217">In hello **creare un servizio** finestra di dialogo scegliere **Stateful** del servizio e chiamarlo "Alphabet.Processing", come illustrato nell'immagine di hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="2f498-217">In hello **Create a Service** dialog box, choose **Stateful** service and call it "Alphabet.Processing" as shown in hello image below.</span></span>
       <span data-ttu-id="2f498-218">![Finestra di dialogo Nuovo servizio in Visual Studio][1]</span><span class="sxs-lookup"><span data-stu-id="2f498-218">![New service dialog in Visual Studio][1]</span></span>

  <!--  ![Stateful service screenshot](./media/service-fabric-concepts-partitioning/createstateful.png)-->

5. <span data-ttu-id="2f498-219">Impostare il numero di hello di partizioni.</span><span class="sxs-lookup"><span data-stu-id="2f498-219">Set hello number of partitions.</span></span> <span data-ttu-id="2f498-220">File ApplicationManifest XML hello aprire si trova in hello cartella ApplicationPackageRoot parametro hello AlphabetPartitions progetto e aggiornare hello Processing_PartitionCount too26 come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="2f498-220">Open hello Applicationmanifest.xml file located in hello ApplicationPackageRoot folder of hello AlphabetPartitions project and update hello parameter Processing_PartitionCount too26 as shown below.</span></span>
   
    ```xml
    <Parameter Name="Processing_PartitionCount" DefaultValue="26" />
    ```
   
    <span data-ttu-id="2f498-221">È inoltre necessario hello tooupdate LowKey e le proprietà di HighKey elemento StatefulService hello in hello ApplicationManifest.xml come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="2f498-221">You also need tooupdate hello LowKey and HighKey properties of hello StatefulService element in hello ApplicationManifest.xml as shown below.</span></span>
   
    ```xml
    <Service Name="Processing">
      <StatefulService ServiceTypeName="ProcessingType" TargetReplicaSetSize="[Processing_TargetReplicaSetSize]" MinReplicaSetSize="[Processing_MinReplicaSetSize]">
        <UniformInt64Partition PartitionCount="[Processing_PartitionCount]" LowKey="0" HighKey="25" />
      </StatefulService>
    </Service>
    ```
6. <span data-ttu-id="2f498-222">Per toobe servizio hello accessibile, aprire un endpoint su una porta aggiungendo l'elemento dell'endpoint hello di ServiceManifest.xml (che si trova nella cartella PackageRoot hello) per hello Alphabet.Processing servizio come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="2f498-222">For hello service toobe accessible, open up an endpoint on a port by adding hello endpoint element of ServiceManifest.xml (located in hello PackageRoot folder) for hello Alphabet.Processing service as shown below:</span></span>
   
    ```xml
    <Endpoint Name="ProcessingServiceEndpoint" Port="8089" Protocol="http" Type="Internal" />
    ```
   
    <span data-ttu-id="2f498-223">Servizio hello è ora configurato toolisten tooan interno di endpoint con 26 partizioni.</span><span class="sxs-lookup"><span data-stu-id="2f498-223">Now hello service is configured toolisten tooan internal endpoint with 26 partitions.</span></span>
7. <span data-ttu-id="2f498-224">Successivamente, è necessario toooverride hello `CreateServiceReplicaListeners()` metodo della classe di elaborazione hello.</span><span class="sxs-lookup"><span data-stu-id="2f498-224">Next, you need toooverride hello `CreateServiceReplicaListeners()` method of hello Processing class.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2f498-225">Per questo esempio, si presume che venga usato un semplice oggetto HttpCommunicationListener.</span><span class="sxs-lookup"><span data-stu-id="2f498-225">For this sample, we assume that you are using a simple HttpCommunicationListener.</span></span> <span data-ttu-id="2f498-226">Per ulteriori informazioni sulla comunicazione affidabile di servizio, vedere [modello di comunicazione affidabile servizio hello](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="2f498-226">For more information on reliable service communication, see [hello Reliable Service communication model](service-fabric-reliable-services-communication.md).</span></span>
   > 
   > 
8. <span data-ttu-id="2f498-227">Un modello consigliato per l'URL di hello che una replica è in ascolto su è hello seguente formato: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.</span><span class="sxs-lookup"><span data-stu-id="2f498-227">A recommended pattern for hello URL that a replica listens on is hello following format: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.</span></span>
    <span data-ttu-id="2f498-228">Pertanto si desidera tooconfigure il listener di comunicazione toolisten sugli endpoint corretto hello e con questo modello.</span><span class="sxs-lookup"><span data-stu-id="2f498-228">So you want tooconfigure your communication listener toolisten on hello correct endpoints and with this pattern.</span></span>
   
    <span data-ttu-id="2f498-229">Più repliche di questo servizio possono essere ospitate su hello stesso computer, quindi questo indirizzo deve toobe toohello univoco replica.</span><span class="sxs-lookup"><span data-stu-id="2f498-229">Multiple replicas of this service may be hosted on hello same computer, so this address needs toobe unique toohello replica.</span></span> <span data-ttu-id="2f498-230">Ecco perché l'ID di partizione + ID replica si trovano hello URL.</span><span class="sxs-lookup"><span data-stu-id="2f498-230">This is why   partition ID + replica ID are in hello URL.</span></span> <span data-ttu-id="2f498-231">HttpListener può restare in ascolto su più indirizzi in hello che stessa porta come prefisso di URL hello è univoco.</span><span class="sxs-lookup"><span data-stu-id="2f498-231">HttpListener can listen on multiple addresses on hello same port as long as hello URL prefix    is unique.</span></span>
   
    <span data-ttu-id="2f498-232">Hello che GUID aggiuntiva è disponibile per un case avanzato in cui le repliche secondarie sono anche in attesa per le richieste di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="2f498-232">hello extra GUID is there for an advanced case where secondary replicas also listen for read-only requests.</span></span> <span data-ttu-id="2f498-233">Quando è il caso di hello, è opportuno che un nuovo indirizzo univoco viene utilizzato durante la transizione da indirizzo di toosecondary primaria tooforce client toore risoluzione hello toomake.</span><span class="sxs-lookup"><span data-stu-id="2f498-233">When that's hello case, you want toomake sure that a new unique address is used when transitioning from primary toosecondary tooforce clients toore-resolve hello address.</span></span> <span data-ttu-id="2f498-234">'+' viene utilizzato come indirizzo hello in modo che hello replica è in ascolto in tutto il codice hello (IP, FQDM, localhost e così via), gli host disponibili riportato di seguito viene illustrato un esempio.</span><span class="sxs-lookup"><span data-stu-id="2f498-234">'+' is used as hello address here so that hello replica listens on all available hosts (IP, FQDM, localhost, etc.) hello code below shows an example.</span></span>
   
    ```CSharp
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
         return new[] { new ServiceReplicaListener(context => this.CreateInternalListener(context))};
    }
    private ICommunicationListener CreateInternalListener(ServiceContext context)
    {
   
         EndpointResourceDescription internalEndpoint = context.CodePackageActivationContext.GetEndpoint("ProcessingServiceEndpoint");
         string uriPrefix = String.Format(
                "{0}://+:{1}/{2}/{3}-{4}/",
                internalEndpoint.Protocol,
                internalEndpoint.Port,
                context.PartitionId,
                context.ReplicaOrInstanceId,
                Guid.NewGuid());
   
         string nodeIP = FabricRuntime.GetNodeContext().IPAddressOrFQDN;
   
         string uriPublished = uriPrefix.Replace("+", nodeIP);
         return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInternalRequest);
    }
    ```
   
    <span data-ttu-id="2f498-235">È inoltre importante notare che hello pubblicati URL è leggermente diversa dal prefisso URL ascolto hello.</span><span class="sxs-lookup"><span data-stu-id="2f498-235">It's also worth noting that hello published URL is slightly different from hello listening URL prefix.</span></span>
    <span data-ttu-id="2f498-236">URL di ascolto Hello viene tooHttpListener.</span><span class="sxs-lookup"><span data-stu-id="2f498-236">hello listening URL is given tooHttpListener.</span></span> <span data-ttu-id="2f498-237">Hello che URL pubblicato è hello URL pubblicato toohello servizio Naming Service Fabric, che viene utilizzato per l'individuazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="2f498-237">hello published URL is hello URL that is published toohello Service Fabric Naming Service, which is used for service discovery.</span></span> <span data-ttu-id="2f498-238">I client richiederanno questo indirizzo con questo servizio di individuazione.</span><span class="sxs-lookup"><span data-stu-id="2f498-238">Clients will ask for this address through that discovery service.</span></span> <span data-ttu-id="2f498-239">indirizzo Hello che i client recuperano esigenze toohave hello effettivo IP o nome di dominio completo del nodo hello in ordine tooconnect.</span><span class="sxs-lookup"><span data-stu-id="2f498-239">hello address that clients get needs toohave hello actual IP or FQDN of hello node in order tooconnect.</span></span> <span data-ttu-id="2f498-240">Pertanto è necessario tooreplace '+' con hello del nodo IP o FQDN come illustrato sopra.</span><span class="sxs-lookup"><span data-stu-id="2f498-240">So you need tooreplace '+' with hello node's IP or FQDN as shown above.</span></span>
9. <span data-ttu-id="2f498-241">ultimo passaggio Hello è hello tooadd logica toohello servizio come illustrato di seguito di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="2f498-241">hello last step is tooadd hello processing logic toohello service as shown below.</span></span>
   
    ```CSharp
    private async Task ProcessInternalRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        string output = null;
        string user = context.Request.QueryString["lastname"].ToString();
   
        try
        {
            output = await this.AddUserAsync(user);
        }
        catch (Exception ex)
        {
            output = ex.Message;
        }
   
        using (HttpListenerResponse response = context.Response)
        {
            if (output != null)
            {
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    private async Task<string> AddUserAsync(string user)
    {
        IReliableDictionary<String, String> dictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<String, String>>("dictionary");
   
        using (ITransaction tx = this.StateManager.CreateTransaction())
        {
            bool addResult = await dictionary.TryAddAsync(tx, user.ToUpperInvariant(), user);
   
            await tx.CommitAsync();
   
            return String.Format(
                "User {0} {1}",
                user,
                addResult ? "sucessfully added" : "already exists");
        }
    }
    ```
   
    <span data-ttu-id="2f498-242">`ProcessInternalRequest`i valori hello query stringa parametro utilizzato toocall hello partizione e chiamate di hello letture `AddUserAsync` dizionario affidabile toohello tooadd hello lastname `dictionary`.</span><span class="sxs-lookup"><span data-stu-id="2f498-242">`ProcessInternalRequest` reads hello values of hello query string parameter used toocall hello partition and calls `AddUserAsync` tooadd hello lastname toohello reliable dictionary `dictionary`.</span></span>
10. <span data-ttu-id="2f498-243">Aggiungere un toosee di progetto di servizio senza stato toohello come chiamare una determinata partizione.</span><span class="sxs-lookup"><span data-stu-id="2f498-243">Let's add a stateless service toohello project toosee how you can call a particular partition.</span></span>
    
    <span data-ttu-id="2f498-244">Questo servizio funge da una semplice interfaccia web che accetta lastname hello come parametro di stringa di query, determina la chiave di partizione hello e invia toohello Alphabet.Processing servizio per l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="2f498-244">This service serves as a simple web interface that accepts hello lastname as a query string parameter, determines hello partition key, and sends it toohello Alphabet.Processing service for processing.</span></span>
11. <span data-ttu-id="2f498-245">In hello **creare un servizio** finestra di dialogo scegliere **Stateless** del servizio e chiamarlo "Alphabet.Web", come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="2f498-245">In hello **Create a Service** dialog box, choose **Stateless** service and call it "Alphabet.Web" as shown below.</span></span>
    
    ![Schermata di servizio senza stato](./media/service-fabric-concepts-partitioning/createnewstateless.png)<span data-ttu-id="2f498-247">.</span><span class="sxs-lookup"><span data-stu-id="2f498-247">.</span></span>
12. <span data-ttu-id="2f498-248">Aggiornare le informazioni di endpoint hello in ServiceManifest.xml hello di hello Alphabet.WebApi servizio tooopen di una porta, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="2f498-248">Update hello endpoint information in hello ServiceManifest.xml of hello Alphabet.WebApi service tooopen up a port as shown below.</span></span>
    
    ```xml
    <Endpoint Name="WebApiServiceEndpoint" Protocol="http" Port="8081"/>
    ```
13. <span data-ttu-id="2f498-249">È necessario un insieme di ServiceInstanceListeners classe hello Web tooreturn.</span><span class="sxs-lookup"><span data-stu-id="2f498-249">You need tooreturn a collection of ServiceInstanceListeners in hello class Web.</span></span> <span data-ttu-id="2f498-250">È possibile scegliere nuovamente tooimplement HttpCommunicationListener un semplice.</span><span class="sxs-lookup"><span data-stu-id="2f498-250">Again, you can choose tooimplement a simple HttpCommunicationListener.</span></span>
    
    ```CSharp
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] {new ServiceInstanceListener(context => this.CreateInputListener(context))};
    }
    private ICommunicationListener CreateInputListener(ServiceContext context)
    {
        // Service instance's URL is hello node's IP & desired port
        EndpointResourceDescription inputEndpoint = context.CodePackageActivationContext.GetEndpoint("WebApiServiceEndpoint")
        string uriPrefix = String.Format("{0}://+:{1}/alphabetpartitions/", inputEndpoint.Protocol, inputEndpoint.Port);
        var uriPublished = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
        return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInputRequest);
    }
    ```
14. <span data-ttu-id="2f498-251">È ora necessario logica di elaborazione tooimplement hello.</span><span class="sxs-lookup"><span data-stu-id="2f498-251">Now you need tooimplement hello processing logic.</span></span> <span data-ttu-id="2f498-252">Hello chiamate HttpCommunicationListener `ProcessInputRequest` quando arriva una richiesta.</span><span class="sxs-lookup"><span data-stu-id="2f498-252">hello HttpCommunicationListener calls `ProcessInputRequest` when a request comes in.</span></span> <span data-ttu-id="2f498-253">Pertanto proseguire e aggiungere codice hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="2f498-253">So let's go ahead and add hello code below.</span></span>
    
    ```CSharp
    private async Task ProcessInputRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        String output = null;
        try
        {
            string lastname = context.Request.QueryString["lastname"];
            char firstLetterOfLastName = lastname.First();
            ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    
            ResolvedServicePartition partition = await this.servicePartitionResolver.ResolveAsync(alphabetServiceUri, partitionKey, cancelRequest);
            ResolvedServiceEndpoint ep = partition.GetEndpoint();
    
            JObject addresses = JObject.Parse(ep.Address);
            string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
            UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
            primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
            string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    
            output = String.Format(
                    "Result: {0}. <p>Partition key: '{1}' generated from hello first letter '{2}' of input value '{3}'. <br>Processing service partition ID: {4}. <br>Processing service replica address: {5}",
                    result,
                    partitionKey,
                    firstLetterOfLastName,
                    lastname,
                    partition.Info.Id,
                    primaryReplicaAddress);
        }
        catch (Exception ex) { output = ex.Message; }
    
        using (var response = context.Response)
        {
            if (output != null)
            {
                output = output + "added tooPartition: " + primaryReplicaAddress;
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    ```
    
    <span data-ttu-id="2f498-254">Analisi dettagliata:</span><span class="sxs-lookup"><span data-stu-id="2f498-254">Let's walk through it step by step.</span></span> <span data-ttu-id="2f498-255">codice Hello legge prima lettera di hello del parametro di stringa di query hello `lastname` in char.</span><span class="sxs-lookup"><span data-stu-id="2f498-255">hello code reads hello first letter of hello query string parameter `lastname` into a char.</span></span> <span data-ttu-id="2f498-256">Quindi, determina la chiave di partizione hello per questa lettera sottraendo hello valore esadecimale `A` dal valore esadecimale hello prima lettera degli hello cognomi.</span><span class="sxs-lookup"><span data-stu-id="2f498-256">Then, it determines hello partition key for this letter by subtracting hello hexadecimal value of `A` from hello hexadecimal value of hello last names' first letter.</span></span>
    
    ```CSharp
    string lastname = context.Request.QueryString["lastname"];
    char firstLetterOfLastName = lastname.First();
    ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    ```
    
    <span data-ttu-id="2f498-257">Si ricordi che in questo esempio si usano 26 partizioni con una chiave per ogni partizione.</span><span class="sxs-lookup"><span data-stu-id="2f498-257">Remember, for this example, we are using 26 partitions with one partition key per partition.</span></span>
    <span data-ttu-id="2f498-258">Successivamente, si ottiene partizione del servizio hello `partition` per questa chiave utilizzando hello `ResolveAsync` metodo hello `servicePartitionResolver` oggetto.</span><span class="sxs-lookup"><span data-stu-id="2f498-258">Next, we obtain hello service partition `partition` for this key by using hello `ResolveAsync` method on hello `servicePartitionResolver` object.</span></span> <span data-ttu-id="2f498-259">`servicePartitionResolver` viene definito come mostrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="2f498-259">`servicePartitionResolver` is defined as</span></span>
    
    ```CSharp
    private readonly ServicePartitionResolver servicePartitionResolver = ServicePartitionResolver.GetDefault();
    ```
    
    <span data-ttu-id="2f498-260">Hello `ResolveAsync` metodo accetta hello URI del servizio, la chiave di partizione hello e un token di annullamento come parametri.</span><span class="sxs-lookup"><span data-stu-id="2f498-260">hello `ResolveAsync` method takes hello service URI, hello partition key, and a cancellation token as parameters.</span></span> <span data-ttu-id="2f498-261">Hello URI del servizio per il servizio di elaborazione hello è `fabric:/AlphabetPartitions/Processing`.</span><span class="sxs-lookup"><span data-stu-id="2f498-261">hello service URI for hello processing service is `fabric:/AlphabetPartitions/Processing`.</span></span> <span data-ttu-id="2f498-262">Quindi, ci occuperemo endpoint hello della partizione hello.</span><span class="sxs-lookup"><span data-stu-id="2f498-262">Next, we get hello endpoint of hello partition.</span></span>
    
    ```CSharp
    ResolvedServiceEndpoint ep = partition.GetEndpoint()
    ```
    
    <span data-ttu-id="2f498-263">Infine, è compilare l'URL dell'endpoint hello più querystring hello e chiamare hello servizio di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="2f498-263">Finally, we build hello endpoint URL plus hello querystring and call hello processing service.</span></span>
    
    ```CSharp
    JObject addresses = JObject.Parse(ep.Address);
    string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
    UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
    primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
    string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    ```
    
    <span data-ttu-id="2f498-264">Al termine dell'elaborazione di hello, output di hello è write-back.</span><span class="sxs-lookup"><span data-stu-id="2f498-264">Once hello processing is done, we write hello output back.</span></span>
15. <span data-ttu-id="2f498-265">ultimo passaggio Hello è servizio di hello tootest.</span><span class="sxs-lookup"><span data-stu-id="2f498-265">hello last step is tootest hello service.</span></span> <span data-ttu-id="2f498-266">Visual Studio usa i parametri dell'applicazione per la distribuzione locale e cloud.</span><span class="sxs-lookup"><span data-stu-id="2f498-266">Visual Studio uses application parameters for local and cloud deployment.</span></span> <span data-ttu-id="2f498-267">servizio di hello tootest con 26 partizioni in locale, è necessario hello tooupdate `Local.xml` file nella cartella ApplicationParameters hello del progetto AlphabetPartitions hello, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="2f498-267">tootest hello service with 26 partitions locally, you need tooupdate hello `Local.xml` file in hello ApplicationParameters folder of hello AlphabetPartitions project as shown below:</span></span>
    
    ```xml
    <Parameters>
      <Parameter Name="Processing_PartitionCount" Value="26" />
      <Parameter Name="WebApi_InstanceCount" Value="1" />
    </Parameters>
    ```
16. <span data-ttu-id="2f498-268">Una volta terminata la distribuzione, è possibile controllare il servizio di hello e tutte le relative partizioni in hello Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="2f498-268">Once you finish deployment, you can check hello service and all of its partitions in hello Service Fabric Explorer.</span></span>
    
    ![Schermata di Service Fabric Explorer](./media/service-fabric-concepts-partitioning/sfxpartitions.png)
17. <span data-ttu-id="2f498-270">In un browser, è possibile testare la logica di partizionamento immettendo hello `http://localhost:8081/?lastname=somename`.</span><span class="sxs-lookup"><span data-stu-id="2f498-270">In a browser, you can test hello partitioning logic by entering `http://localhost:8081/?lastname=somename`.</span></span> <span data-ttu-id="2f498-271">Si noterà che ciascun cognome che inizia con hello stessa lettera di vengono archiviato in hello stessa partizione.</span><span class="sxs-lookup"><span data-stu-id="2f498-271">You will see that each last name that starts with hello same letter is being stored in hello same partition.</span></span>
    
    ![Schermata del browser](./media/service-fabric-concepts-partitioning/samplerunning.png)

<span data-ttu-id="2f498-273">è disponibili sul Hello intero codice sorgente dell'esempio hello [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span><span class="sxs-lookup"><span data-stu-id="2f498-273">hello entire source code of hello sample is available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f498-274">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2f498-274">Next steps</span></span>
<span data-ttu-id="2f498-275">Per informazioni sui concetti di Service Fabric, vedere l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="2f498-275">For information on Service Fabric concepts, see hello following:</span></span>

* [<span data-ttu-id="2f498-276">Disponibilità dei servizi di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2f498-276">Availability of Service Fabric services</span></span>](service-fabric-availability-services.md)
* [<span data-ttu-id="2f498-277">Scalabilità dei servizi di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2f498-277">Scalability of Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
* [<span data-ttu-id="2f498-278">Pianificazione della capacità per le applicazioni Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2f498-278">Capacity planning for Service Fabric applications</span></span>](service-fabric-capacity-planning.md)

[wikipartition]: https://en.wikipedia.org/wiki/Partition_(database)

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png