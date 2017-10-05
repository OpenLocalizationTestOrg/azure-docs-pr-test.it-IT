---
title: Partizionamento dei servizi di Service Fabric | Microsoft Docs
description: Illustra come partizionare i servizi con stato di Service Fabric. Le partizioni consentono di archiviare i dati nei computer locali, in modo da poter ridimensionare dati e calcolo allo stesso tempo.
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
ms.openlocfilehash: 3c1e80305cb65f41a6981b99f69e8b87f89599ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="partition-service-fabric-reliable-services"></a><span data-ttu-id="c5a82-104">Partizionare Reliable Services di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c5a82-104">Partition Service Fabric reliable services</span></span>
<span data-ttu-id="c5a82-105">Questo articolo offre un'introduzione ai concetti di base del partizionamento di Reliable Services di Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c5a82-105">This article provides an introduction to the basic concepts of partitioning Azure Service Fabric reliable services.</span></span> <span data-ttu-id="c5a82-106">Il codice sorgente usato nell'articolo è disponibile anche in [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span><span class="sxs-lookup"><span data-stu-id="c5a82-106">The source code used in the article is also available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span></span>

## <a name="partitioning"></a><span data-ttu-id="c5a82-107">Partizionamento</span><span class="sxs-lookup"><span data-stu-id="c5a82-107">Partitioning</span></span>
<span data-ttu-id="c5a82-108">Il partizionamento non è una procedura specifica di Service Fabric,</span><span class="sxs-lookup"><span data-stu-id="c5a82-108">Partitioning is not unique to Service Fabric.</span></span> <span data-ttu-id="c5a82-109">bensì si tratta di un modello di base per la creazione di servizi scalabili.</span><span class="sxs-lookup"><span data-stu-id="c5a82-109">In fact, it is a core pattern of building scalable services.</span></span> <span data-ttu-id="c5a82-110">Più in generale, si può pensare al partizionamento come alla divisione dello stato (dati) e del calcolo in unità accessibili più piccole per migliorare la scalabilità e le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="c5a82-110">In a broader sense, we can think about partitioning as a concept of dividing state (data) and compute into smaller accessible units to improve scalability and performance.</span></span> <span data-ttu-id="c5a82-111">Una forma molto conosciuta di partizionamento è il [partizionamento dei dati][wikipartition], noto anche come partizionamento orizzontale.</span><span class="sxs-lookup"><span data-stu-id="c5a82-111">A well-known form of partitioning is [data partitioning][wikipartition], also known as sharding.</span></span>

### <a name="partition-service-fabric-stateless-services"></a><span data-ttu-id="c5a82-112">Partizionamento dei servizi senza stato di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c5a82-112">Partition Service Fabric stateless services</span></span>
<span data-ttu-id="c5a82-113">Per i servizi senza stato un partizionamento può essere considerato un'unità logica contenente una o più istanze di un servizio.</span><span class="sxs-lookup"><span data-stu-id="c5a82-113">For stateless services, you can think about a partition being a logical unit that contains one or more instances of a service.</span></span> <span data-ttu-id="c5a82-114">La figura 1 illustra un servizio senza stato con cinque istanze distribuite in un cluster usando una partizione.</span><span class="sxs-lookup"><span data-stu-id="c5a82-114">Figure 1 shows a stateless service with five instances distributed across a cluster using one partition.</span></span>

![Servizio senza stato](./media/service-fabric-concepts-partitioning/statelessinstances.png)

<span data-ttu-id="c5a82-116">Sono disponibili due tipi di soluzioni di servizio senza stato.</span><span class="sxs-lookup"><span data-stu-id="c5a82-116">There are really two types of stateless service solutions.</span></span> <span data-ttu-id="c5a82-117">La prima è un servizio che rende persistente lo stato esternamente, ad esempio in un database SQL di Azure (come un sito Web che archivia informazioni e dati sulle sessioni),</span><span class="sxs-lookup"><span data-stu-id="c5a82-117">The first one is a service that persists its state externally, for example in an Azure SQL database (like a website that stores the session information and data).</span></span> <span data-ttu-id="c5a82-118">e la seconda include servizi solo di calcolo (ad esempio, una calcolatrice o l'anteprima di un'immagine) che non gestiscono alcuno stato persistente.</span><span class="sxs-lookup"><span data-stu-id="c5a82-118">The second one is computation-only services (like a calculator or image thumbnailing) that do not manage any persistent state.</span></span>

<span data-ttu-id="c5a82-119">In entrambi i casi, il partizionamento di un servizio senza stato è uno scenario molto raro e la scalabilità e la disponibilità in genere si ottengono aggiungendo altre istanze.</span><span class="sxs-lookup"><span data-stu-id="c5a82-119">In either case, partitioning a stateless service is a very rare scenario--scalability and availability are normally achieved by adding more instances.</span></span> <span data-ttu-id="c5a82-120">I soli casi in cui è opportuno considerare più partizioni per le istanze di un servizio senza stato sono quelli in cui è necessario soddisfare speciali richieste di routing,</span><span class="sxs-lookup"><span data-stu-id="c5a82-120">The only time you want to consider multiple partitions for stateless service instances is when you need to meet special routing requests.</span></span>

<span data-ttu-id="c5a82-121">ad esempio, quando gli utenti con ID compresi in un determinato intervallo devono essere gestiti solo da una particolare istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="c5a82-121">As an example, consider a case where users with IDs in a certain range should only be served by a particular service instance.</span></span> <span data-ttu-id="c5a82-122">È possibile partizionare un servizio senza stato anche quando, ad esempio, è presente un back-end molto partizionato, come un database SQL partizionato, e si vuole controllare quale istanza del servizio deve scrivere nella partizione di database oppure eseguire altre operazioni di preparazione nel servizio senza stato che richiedono le stesse informazioni sul partizionamento usate nel back-end.</span><span class="sxs-lookup"><span data-stu-id="c5a82-122">Another example of when you could partition a stateless service is when you have a truly partitioned backend (e.g. a sharded SQL database) and you want to control which service instance should write to the database shard--or perform other preparation work within the stateless service that requires the same partitioning information as is used in the backend.</span></span> <span data-ttu-id="c5a82-123">Tali tipi di scenario possono essere risolti anche in modo diverso e non richiedono necessariamente il partizionamento del servizio.</span><span class="sxs-lookup"><span data-stu-id="c5a82-123">Those types of scenarios can also be solved in different ways and do not necessarily require service partitioning.</span></span>

<span data-ttu-id="c5a82-124">La parte restante di questa procedura dettagliata riguarda i servizi con stato.</span><span class="sxs-lookup"><span data-stu-id="c5a82-124">The remainder of this walkthrough focuses on stateful services.</span></span>

### <a name="partition-service-fabric-stateful-services"></a><span data-ttu-id="c5a82-125">Partizionamento dei servizi con stato di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c5a82-125">Partition Service Fabric stateful services</span></span>
<span data-ttu-id="c5a82-126">L'infrastruttura di servizi facilita lo sviluppo di servizi con stato scalabili offrendo un modo straordinario per partizionare lo stato (dati).</span><span class="sxs-lookup"><span data-stu-id="c5a82-126">Service Fabric makes it easy to develop scalable stateful services by offering a first-class way to partition state (data).</span></span> <span data-ttu-id="c5a82-127">Concettualmente, si può pensare al partizionamento di un servizio con stato come a un'unità di scala estremamente affidabile nelle [repliche](service-fabric-availability-services.md) distribuite e bilanciate nei nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="c5a82-127">Conceptually, you can think about a partition of a stateful service as a scale unit that is highly reliable through [replicas](service-fabric-availability-services.md) that are distributed and balanced across the nodes in a cluster.</span></span>

<span data-ttu-id="c5a82-128">Il partizionamento, nell'ambito dei servizi con stato di Service Fabric, fa riferimento al processo che determina come una particolare partizione del servizio sia responsabile di una parte dello stato completo del servizio.</span><span class="sxs-lookup"><span data-stu-id="c5a82-128">Partitioning in the context of Service Fabric stateful services refers to the process of determining that a particular service partition is responsible for a portion of the complete state of the service.</span></span> <span data-ttu-id="c5a82-129">Come accennato in precedenza, la partizione è un set di [repliche](service-fabric-availability-services.md).</span><span class="sxs-lookup"><span data-stu-id="c5a82-129">(As mentioned before, a partition is a set of [replicas](service-fabric-availability-services.md)).</span></span> <span data-ttu-id="c5a82-130">Un'importante caratteristica dell'infrastruttura di servizi è che inserisce le partizioni in nodi diversi,</span><span class="sxs-lookup"><span data-stu-id="c5a82-130">A great thing about Service Fabric is that it places the partitions on different nodes.</span></span> <span data-ttu-id="c5a82-131">consentendo loro di crescere fino al limite di risorse di un nodo.</span><span class="sxs-lookup"><span data-stu-id="c5a82-131">This allows them to grow to a node's resource limit.</span></span> <span data-ttu-id="c5a82-132">Quando i dati richiedono uno spazio maggiore, le partizioni crescono e Service Fabric le ribilancia tra i nodi</span><span class="sxs-lookup"><span data-stu-id="c5a82-132">As the data needs grow, partitions grow, and Service Fabric rebalances partitions across nodes.</span></span> <span data-ttu-id="c5a82-133">assicurando un uso continuo ed efficiente delle risorse hardware.</span><span class="sxs-lookup"><span data-stu-id="c5a82-133">This ensures the continued efficient use of hardware resources.</span></span>

<span data-ttu-id="c5a82-134">Si supponga, ad esempio, di iniziare con un cluster a 5 nodi e un servizio configurato per includere 10 partizioni e una destinazione di tre repliche.</span><span class="sxs-lookup"><span data-stu-id="c5a82-134">To give you an example, say you start with a 5-node cluster and a service that is configured to have 10 partitions and a target of three replicas.</span></span> <span data-ttu-id="c5a82-135">In questo caso, Service Fabric bilancerebbe e distribuirebbe le repliche nel cluster e risulterebbero due [repliche](service-fabric-availability-services.md) primarie per nodo.</span><span class="sxs-lookup"><span data-stu-id="c5a82-135">In this case, Service Fabric would balance and distribute the replicas across the cluster--and you would end up with two primary [replicas](service-fabric-availability-services.md) per node.</span></span>
<span data-ttu-id="c5a82-136">Se poi fosse necessario scalare orizzontalmente il cluster fino a 10 nodi, Service Fabric ribilancerebbe le [repliche](service-fabric-availability-services.md) primarie tra tutti i 10 nodi.</span><span class="sxs-lookup"><span data-stu-id="c5a82-136">If you now need to scale out the cluster to 10 nodes, Service Fabric would rebalance the primary [replicas](service-fabric-availability-services.md) across all 10 nodes.</span></span> <span data-ttu-id="c5a82-137">Analogamente, se si tornasse a 5 nodi, Service Fabric ribilancerebbe tutte le repliche tra i 5 nodi.</span><span class="sxs-lookup"><span data-stu-id="c5a82-137">Likewise, if you scaled back to 5 nodes, Service Fabric would rebalance all the replicas across the 5 nodes.</span></span>  

<span data-ttu-id="c5a82-138">La figura 2 illustra la distribuzione di 10 partizioni prima e dopo il ridimensionamento del cluster.</span><span class="sxs-lookup"><span data-stu-id="c5a82-138">Figure 2 shows the distribution of 10 partitions before and after scaling the cluster.</span></span>

![Servizio con stato](./media/service-fabric-concepts-partitioning/partitions.png)

<span data-ttu-id="c5a82-140">La scalabilità orizzontale è quindi garantita perché le richieste dei client vengono distribuite tra i computer, le prestazioni generali dell'applicazione vengono migliorate e la contesa in caso di accesso a blocchi di dati viene ridotta.</span><span class="sxs-lookup"><span data-stu-id="c5a82-140">As a result, the scale-out is achieved since requests from clients are distributed across computers, overall performance of the application is improved, and contention on access to chunks of data is reduced.</span></span>

## <a name="plan-for-partitioning"></a><span data-ttu-id="c5a82-141">Pianificazione del partizionamento</span><span class="sxs-lookup"><span data-stu-id="c5a82-141">Plan for partitioning</span></span>
<span data-ttu-id="c5a82-142">Prima di implementare un servizio, è sempre consigliabile considerare la strategia di partizionamento richiesta dalla scalabilità orizzontale.</span><span class="sxs-lookup"><span data-stu-id="c5a82-142">Before implementing a service, you should always consider the partitioning strategy that is required to scale out.</span></span> <span data-ttu-id="c5a82-143">Esistono diversi modi, ma tutti si concentrano sugli scopi dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c5a82-143">There are different ways, but all of them focus on what the application needs to achieve.</span></span> <span data-ttu-id="c5a82-144">Nell'ambito di questo articolo verranno illustrati alcuni degli aspetti più importanti.</span><span class="sxs-lookup"><span data-stu-id="c5a82-144">For the context of this article, let's consider some of the more important aspects.</span></span>

<span data-ttu-id="c5a82-145">Un valido approccio consiste nel considerare la struttura dello stato che deve essere partizionato come primo passaggio.</span><span class="sxs-lookup"><span data-stu-id="c5a82-145">A good approach is to think about the structure of the state that needs to be partitioned, as the first step.</span></span>

<span data-ttu-id="c5a82-146">Un semplice esempio viene riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="c5a82-146">Let's take a simple example.</span></span> <span data-ttu-id="c5a82-147">Per compilare un servizio per un sondaggio a livello di stato, è possibile creare una partizione per ogni città dello stato</span><span class="sxs-lookup"><span data-stu-id="c5a82-147">If you were to build a service for a countywide poll, you could create a partition for each city in the county.</span></span> <span data-ttu-id="c5a82-148">e quindi archiviare i voti per ogni persona della città nella partizione corrispondente a tale città.</span><span class="sxs-lookup"><span data-stu-id="c5a82-148">Then, you could store the votes for every person in the city in the partition that corresponds to that city.</span></span> <span data-ttu-id="c5a82-149">La figura 3 illustra un gruppo di persone e la città in cui risiedono.</span><span class="sxs-lookup"><span data-stu-id="c5a82-149">Figure 3 illustrates a set of people and the city in which they reside.</span></span>

![Partizione semplice](./media/service-fabric-concepts-partitioning/cities.png)

<span data-ttu-id="c5a82-151">Poiché la popolazione delle città varia considerevolmente, si potrebbero avere alcune partizioni contenenti una grande quantità di dati (ad esempio, Seattle) e altre con dati in quantità molto piccole (ad esempio, Kirkland).</span><span class="sxs-lookup"><span data-stu-id="c5a82-151">As the population of cities varies widely, you may end up with some partitions that contain a lot of data (e.g. Seattle) and other partitions with very little state (e.g. Kirkland).</span></span> <span data-ttu-id="c5a82-152">Quale impatto hanno quindi partizioni con quantità di dati non uniformi?</span><span class="sxs-lookup"><span data-stu-id="c5a82-152">So what is the impact of having partitions with uneven amounts of state?</span></span>

<span data-ttu-id="c5a82-153">Tornando all'esempio, si può osservare facilmente che la partizione con i voti per Seattle avrà più traffico di quella di Kirkland.</span><span class="sxs-lookup"><span data-stu-id="c5a82-153">If you think about the example again, you can easily see that the partition that holds the votes for Seattle will get more traffic than the Kirkland one.</span></span> <span data-ttu-id="c5a82-154">Per impostazione predefinita, Service Fabric assicura che in ogni nodo sia presente all'incirca lo stesso numero di repliche primarie e secondarie,</span><span class="sxs-lookup"><span data-stu-id="c5a82-154">By default, Service Fabric makes sure that there is about the same number of primary and secondary replicas on each node.</span></span> <span data-ttu-id="c5a82-155">perciò si potrebbero avere nodi contenenti repliche che gestiscono più traffico e altre che gestiscono meno traffico.</span><span class="sxs-lookup"><span data-stu-id="c5a82-155">So you may end up with nodes that hold replicas that serve more traffic and others that serve less traffic.</span></span> <span data-ttu-id="c5a82-156">In un cluster è preferibile evitare le aree sensibili e non sensibili di questo genere.</span><span class="sxs-lookup"><span data-stu-id="c5a82-156">You would preferably want to avoid hot and cold spots like this in a cluster.</span></span>

<span data-ttu-id="c5a82-157">Per evitarle, si consiglia di effettuare due azioni nell'ambito del partizionamento:</span><span class="sxs-lookup"><span data-stu-id="c5a82-157">In order to avoid this, you should do two things, from a partitioning point of view:</span></span>

* <span data-ttu-id="c5a82-158">Cercare di partizionare lo stato in modo che venga distribuito uniformemente tra tutte le partizioni.</span><span class="sxs-lookup"><span data-stu-id="c5a82-158">Try to partition the state so that it is evenly distributed across all partitions.</span></span>
* <span data-ttu-id="c5a82-159">Segnalare il carico da ognuna delle repliche per il servizio.</span><span class="sxs-lookup"><span data-stu-id="c5a82-159">Report load from each of the replicas for the service.</span></span> <span data-ttu-id="c5a82-160">Per informazioni su come fare, vedere l'articolo relativo a [metriche e carico](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="c5a82-160">(For information on how, check out this article on [Metrics and Load](service-fabric-cluster-resource-manager-metrics.md)).</span></span> <span data-ttu-id="c5a82-161">Service Fabric consente di segnalare il carico utilizzato dai servizi, ad esempio la quantità di memoria o il numero di record.</span><span class="sxs-lookup"><span data-stu-id="c5a82-161">Service Fabric provides the capability to report load consumed by services, such as amount of memory or number of records.</span></span> <span data-ttu-id="c5a82-162">In base alle metriche segnalate, Service Fabric rileva che alcune partizioni gestiscono carichi maggiori di altre e ribilancia il cluster spostando le repliche in nodi più adatti, per evitare il sovraccarico dei nodi in generale.</span><span class="sxs-lookup"><span data-stu-id="c5a82-162">Based on the metrics reported, Service Fabric detects that some partitions are serving higher loads than others and rebalances the cluster by moving replicas to more suitable nodes, so that overall no node is overloaded.</span></span>

<span data-ttu-id="c5a82-163">A volte non è possibile sapere quanti dati saranno presenti in una determinata partizione</span><span class="sxs-lookup"><span data-stu-id="c5a82-163">Sometimes, you cannot know how much data will be in a given partition.</span></span> <span data-ttu-id="c5a82-164">e quindi si consiglia di eseguire entrambe le operazioni, adottando prima una strategia di partizionamento che distribuisca i dati in modo uniforme nelle partizioni e poi creando un report del carico.</span><span class="sxs-lookup"><span data-stu-id="c5a82-164">So a general recommendation is to do both--first, by adopting a partitioning strategy that spreads the data evenly across the partitions and second, by reporting load.</span></span>  <span data-ttu-id="c5a82-165">Il primo metodo consente di evitare le situazioni descritte nell'esempio delle votazioni, il secondo invece di ridurre le differenze temporanee nell'accesso o nel carico nel corso del tempo.</span><span class="sxs-lookup"><span data-stu-id="c5a82-165">The first method prevents situations described in the voting example, while the second helps smooth out temporary differences in access or load over time.</span></span>

<span data-ttu-id="c5a82-166">Un altro aspetto della pianificazione delle partizioni è la scelta del numero corretto di partizioni con cui iniziare.</span><span class="sxs-lookup"><span data-stu-id="c5a82-166">Another aspect of partition planning is to choose the correct number of partitions to begin with.</span></span>
<span data-ttu-id="c5a82-167">Dal punto di vista di Service Fabric, nulla impedisce di iniziare con un numero di partizioni maggiore di quello anticipato per lo scenario.</span><span class="sxs-lookup"><span data-stu-id="c5a82-167">From a Service Fabric perspective, there is nothing that prevents you from starting out with a higher number of partitions than anticipated for your scenario.</span></span>
<span data-ttu-id="c5a82-168">Infatti ipotizzare il numero massimo di partizioni è un valido approccio.</span><span class="sxs-lookup"><span data-stu-id="c5a82-168">In fact, assuming the maximum number of partitions is a valid approach.</span></span>

<span data-ttu-id="c5a82-169">Raramente saranno necessarie più partizioni di quelle scelte inizialmente.</span><span class="sxs-lookup"><span data-stu-id="c5a82-169">In rare cases, you may end up needing more partitions than you have initially chosen.</span></span> <span data-ttu-id="c5a82-170">Poiché non sarà più possibile modificare in seguito il conteggio delle partizioni, sarà necessario adottare alcuni approcci avanzati, ad esempio la creazione di una nuova istanza del servizio dello stesso tipo di servizio,</span><span class="sxs-lookup"><span data-stu-id="c5a82-170">As you cannot change the partition count after the fact, you would need to apply some advanced partition approaches, such as creating a new service instance of the same service type.</span></span> <span data-ttu-id="c5a82-171">e implementare una logica lato client che instradi le richieste all'istanza del servizio corretta in base alle conoscenze lato client che il codice client deve avere.</span><span class="sxs-lookup"><span data-stu-id="c5a82-171">You would also need to implement some client-side logic that routes the requests to the correct service instance, based on client-side knowledge that your client code must maintain.</span></span>

<span data-ttu-id="c5a82-172">Un altro aspetto da considerare per la pianificazione del partizionamento sono le risorse del computer disponibili.</span><span class="sxs-lookup"><span data-stu-id="c5a82-172">Another consideration for partitioning planning is the available computer resources.</span></span> <span data-ttu-id="c5a82-173">Poiché lo stato deve essere accessibile e archiviato, è necessario rispettare i limiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="c5a82-173">As the state needs to be accessed and stored, you are bound to follow:</span></span>

* <span data-ttu-id="c5a82-174">Larghezza di banda della rete</span><span class="sxs-lookup"><span data-stu-id="c5a82-174">Network bandwidth limits</span></span>
* <span data-ttu-id="c5a82-175">Memoria di sistema</span><span class="sxs-lookup"><span data-stu-id="c5a82-175">System memory limits</span></span>
* <span data-ttu-id="c5a82-176">Archiviazione su disco</span><span class="sxs-lookup"><span data-stu-id="c5a82-176">Disk storage limits</span></span>

<span data-ttu-id="c5a82-177">Cosa accade quindi se si presentano vincoli relativi alle risorse in un cluster in esecuzione?</span><span class="sxs-lookup"><span data-stu-id="c5a82-177">So what happens if you run into resource constraints in a running cluster?</span></span> <span data-ttu-id="c5a82-178">Per soddisfare i nuovi requisiti, sarà sufficiente scalare orizzontalmente il cluster.</span><span class="sxs-lookup"><span data-stu-id="c5a82-178">The answer is that you can simply scale out the cluster to accommodate the new requirements.</span></span>

<span data-ttu-id="c5a82-179">[La guida alla pianificazione della capacità](service-fabric-capacity-planning.md) contiene indicazioni per determinare quanti nodi sono necessari al cluster.</span><span class="sxs-lookup"><span data-stu-id="c5a82-179">[The capacity planning guide](service-fabric-capacity-planning.md) offers guidance for how to determine how many nodes your cluster needs.</span></span>

## <a name="get-started-with-partitioning"></a><span data-ttu-id="c5a82-180">Introduzione al partizionamento</span><span class="sxs-lookup"><span data-stu-id="c5a82-180">Get started with partitioning</span></span>
<span data-ttu-id="c5a82-181">Questa sezione descrive come iniziare a partizionare il servizio.</span><span class="sxs-lookup"><span data-stu-id="c5a82-181">This section describes how to get started with partitioning your service.</span></span>

<span data-ttu-id="c5a82-182">In primo luogo Service Fabric consente di scegliere tra tre schemi di partizione:</span><span class="sxs-lookup"><span data-stu-id="c5a82-182">Service Fabric offers a choice of three partition schemes:</span></span>

* <span data-ttu-id="c5a82-183">Partizionamento con intervallo (noto anche come UniformInt64Partition).</span><span class="sxs-lookup"><span data-stu-id="c5a82-183">Ranged partitioning (otherwise known as UniformInt64Partition).</span></span>
* <span data-ttu-id="c5a82-184">Partizionamento denominato.</span><span class="sxs-lookup"><span data-stu-id="c5a82-184">Named partitioning.</span></span> <span data-ttu-id="c5a82-185">Le applicazioni che usano questo modello in genere hanno dati che possono essere inseriti in un bucket, in un set associato.</span><span class="sxs-lookup"><span data-stu-id="c5a82-185">Applications using this model usually have data that can be bucketed, within a bounded set.</span></span> <span data-ttu-id="c5a82-186">Aree, codici postali, gruppi di clienti o altri limiti aziendali sono alcuni esempi comuni di campi dati usati come chiavi di partizione denominata.</span><span class="sxs-lookup"><span data-stu-id="c5a82-186">Some common examples of data fields used as named partition keys would be regions, postal codes, customer groups, or other business boundaries.</span></span>
* <span data-ttu-id="c5a82-187">Partizionamento singleton.</span><span class="sxs-lookup"><span data-stu-id="c5a82-187">Singleton partitioning.</span></span> <span data-ttu-id="c5a82-188">Le partizioni singleton in genere vengono usate quando il servizio non richiede alcun routing aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="c5a82-188">Singleton partitions are typically used when the service does not require any additional routing.</span></span> <span data-ttu-id="c5a82-189">I servizi senza stato, ad esempio, usano questo schema di partizionamento per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="c5a82-189">For example, stateless services use this partitioning scheme by default.</span></span>

<span data-ttu-id="c5a82-190">Gli schemi di partizionamento denominato e singleton sono forme particolari di partizioni con intervalli.</span><span class="sxs-lookup"><span data-stu-id="c5a82-190">Named and Singleton partitioning schemes are special forms of ranged partitions.</span></span> <span data-ttu-id="c5a82-191">Per impostazione predefinita, i modelli di Visual Studio per Service Fabric usano il partizionamento con intervallo perché è quello più comune e utile.</span><span class="sxs-lookup"><span data-stu-id="c5a82-191">By default, the Visual Studio templates for Service Fabric use ranged partitioning, as it is the most common and useful one.</span></span> <span data-ttu-id="c5a82-192">La parte restante di questo articolo riguarda lo schema di partizionamento con intervallo.</span><span class="sxs-lookup"><span data-stu-id="c5a82-192">The remainder of this article focuses on the ranged partitioning scheme.</span></span>

### <a name="ranged-partitioning-scheme"></a><span data-ttu-id="c5a82-193">Schema di partizionamento con intervallo</span><span class="sxs-lookup"><span data-stu-id="c5a82-193">Ranged partitioning scheme</span></span>
<span data-ttu-id="c5a82-194">Viene usato per specificare un intervallo di numeri interi (identificato da una chiave minima e una chiave massima) e un numero di partizioni (n).</span><span class="sxs-lookup"><span data-stu-id="c5a82-194">This is used to specify an integer range (identified by a low key and high key) and a number of partitions (n).</span></span> <span data-ttu-id="c5a82-195">Crea n partizioni, ognuna responsabile di un intervallo secondario non sovrapposto dell'intervallo di chiavi di partizione generale.</span><span class="sxs-lookup"><span data-stu-id="c5a82-195">It creates n partitions, each responsible for a non-overlapping subrange of the overall partition key range.</span></span> <span data-ttu-id="c5a82-196">Ad esempio, uno schema di partizionamento con intervallo con una chiave minima 0, una chiave massima 99 e un conteggio pari a 4 creerà quattro partizioni come mostrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="c5a82-196">For example, a ranged partitioning scheme with a low key of 0, a high key of 99, and a count of 4 would create four partitions, as shown below.</span></span>

![Partizionamento per intervalli](./media/service-fabric-concepts-partitioning/range-partitioning.png)

<span data-ttu-id="c5a82-198">Un approccio comune consiste nel creare un hash basato su una chiave univoca nel set di dati.</span><span class="sxs-lookup"><span data-stu-id="c5a82-198">A common approach is to create a hash based on a unique key within the data set.</span></span> <span data-ttu-id="c5a82-199">Sono esempi comuni di chiavi un Vehicle Identification Number (VIN), l'ID di un dipendente o una stringa univoca.</span><span class="sxs-lookup"><span data-stu-id="c5a82-199">Some common examples of keys would be a vehicle identification number (VIN), an employee ID, or a unique string.</span></span> <span data-ttu-id="c5a82-200">Usando questa chiave univoca è possibile quindi generare un codice hash, modulo dell'intervallo di chiavi, da usare come chiave.</span><span class="sxs-lookup"><span data-stu-id="c5a82-200">By using this unique key, you would then generate a hash code, modulus the key range, to use as your key.</span></span> <span data-ttu-id="c5a82-201">È possibile specificare limiti massimi e minimi dell'intervallo di chiavi consentite.</span><span class="sxs-lookup"><span data-stu-id="c5a82-201">You can specify the upper and lower bounds of the allowed key range.</span></span>

### <a name="select-a-hash-algorithm"></a><span data-ttu-id="c5a82-202">Selezionare un algoritmo di hash</span><span class="sxs-lookup"><span data-stu-id="c5a82-202">Select a hash algorithm</span></span>
<span data-ttu-id="c5a82-203">Una parte importante della generazione di un hash è rappresentata dalla selezione dell'algoritmo di hash.</span><span class="sxs-lookup"><span data-stu-id="c5a82-203">An important part of hashing is selecting your hash algorithm.</span></span> <span data-ttu-id="c5a82-204">È necessario valutare se l'obiettivo sia raggruppare chiavi simili una accanto all'altra (hash sensibile alla località) o se l'attività debba essere distribuita su larga scala su tutte le partizioni (hash di distribuzione), che è l'obiettivo più comune.</span><span class="sxs-lookup"><span data-stu-id="c5a82-204">A consideration is whether the goal is to group similar keys near each other (locality sensitive hashing)--or if activity should be distributed broadly across all partitions (distribution hashing), which is more common.</span></span>

<span data-ttu-id="c5a82-205">Un valido algoritmo di hash di distribuzione si distingue perché è facile da elaborare, presenta pochi conflitti e distribuisce le chiavi in modo uniforme.</span><span class="sxs-lookup"><span data-stu-id="c5a82-205">The characteristics of a good distribution hashing algorithm are that it is easy to compute, it has few collisions, and it distributes the keys evenly.</span></span> <span data-ttu-id="c5a82-206">[FNV-1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) è un valido esempio di algoritmo di hash efficiente.</span><span class="sxs-lookup"><span data-stu-id="c5a82-206">A good example of an efficient hash algorithm is the [FNV-1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) hash algorithm.</span></span>

<span data-ttu-id="c5a82-207">Un'ottima risorsa per le scelte di algoritmi di codice di hash generali è rappresentata dalla [pagina Wikipedia sulle funzioni hash](http://en.wikipedia.org/wiki/Hash_function).</span><span class="sxs-lookup"><span data-stu-id="c5a82-207">A good resource for general hash code algorithm choices is the [Wikipedia page on hash functions](http://en.wikipedia.org/wiki/Hash_function).</span></span>

## <a name="build-a-stateful-service-with-multiple-partitions"></a><span data-ttu-id="c5a82-208">Compilare un servizio con stato con più partizioni</span><span class="sxs-lookup"><span data-stu-id="c5a82-208">Build a stateful service with multiple partitions</span></span>
<span data-ttu-id="c5a82-209">Ora verrà creato il primo servizio con stato affidabile con più partizioni.</span><span class="sxs-lookup"><span data-stu-id="c5a82-209">Let's create your first reliable stateful service with multiple partitions.</span></span> <span data-ttu-id="c5a82-210">In questo esempio si compilerà un'applicazione molto semplice in cui archiviare tutti i cognomi che iniziano con la stessa lettera nella stessa partizione.</span><span class="sxs-lookup"><span data-stu-id="c5a82-210">In this example, you will build a very simple application where you want to store all last names that start with the same letter in the same partition.</span></span>

<span data-ttu-id="c5a82-211">Prima di scrivere il codice, considerare le partizioni e le chiavi di partizione.</span><span class="sxs-lookup"><span data-stu-id="c5a82-211">Before you write any code, you need to think about the partitions and partition keys.</span></span> <span data-ttu-id="c5a82-212">Sono necessarie 26 partizioni, una per ogni lettera dell'alfabeto, ma per quanto riguarda le chiavi minime e massime?</span><span class="sxs-lookup"><span data-stu-id="c5a82-212">You need 26 partitions (one for each letter in the alphabet), but what about the low and high keys?</span></span>
<span data-ttu-id="c5a82-213">Poiché è necessaria esattamente una partizione per ogni lettera, è possibile usare 0 come chiave minima e 25 come chiave massima, perché ogni lettera corrisponde alla propria chiave.</span><span class="sxs-lookup"><span data-stu-id="c5a82-213">As we literally want to have one partition per letter, we can use 0 as the low key and 25 as the high key, as each letter is its own key.</span></span>

> [!NOTE]
> <span data-ttu-id="c5a82-214">Questo è uno scenario semplificato, perché nella realtà la distribuzione non sarebbe uniforme.</span><span class="sxs-lookup"><span data-stu-id="c5a82-214">This is a simplified scenario, as in reality the distribution would be uneven.</span></span> <span data-ttu-id="c5a82-215">I cognomi che iniziano con la lettera "S" o "M" sono più comuni di quelli che iniziano con "X" o "Y".</span><span class="sxs-lookup"><span data-stu-id="c5a82-215">Last names starting with the letters "S" or "M" are more common than the ones starting with "X" or "Y".</span></span>
> 
> 

1. <span data-ttu-id="c5a82-216">Aprire **Visual Studio** > **File** > **Nuovo** > **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="c5a82-216">Open **Visual Studio** > **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="c5a82-217">Nella finestra di dialogo **Nuovo progetto** scegliere l'applicazione Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c5a82-217">In the **New Project** dialog box, choose the Service Fabric application.</span></span>
3. <span data-ttu-id="c5a82-218">Assegnare al progetto il nome "AlphabetPartitions".</span><span class="sxs-lookup"><span data-stu-id="c5a82-218">Call the project "AlphabetPartitions".</span></span>
4. <span data-ttu-id="c5a82-219">Nella finestra di dialogo **Create a Service** (Crea un servizio) scegliere il servizio **con stato** e assegnargli il nome "Alphabet.Processing", come nell'immagine seguente.</span><span class="sxs-lookup"><span data-stu-id="c5a82-219">In the **Create a Service** dialog box, choose **Stateful** service and call it "Alphabet.Processing" as shown in the image below.</span></span>
       <span data-ttu-id="c5a82-220">![Finestra di dialogo Nuovo servizio in Visual Studio][1]</span><span class="sxs-lookup"><span data-stu-id="c5a82-220">![New service dialog in Visual Studio][1]</span></span>

  <!--  ![Stateful service screenshot](./media/service-fabric-concepts-partitioning/createstateful.png)-->

5. <span data-ttu-id="c5a82-221">Impostare il numero di partizioni.</span><span class="sxs-lookup"><span data-stu-id="c5a82-221">Set the number of partitions.</span></span> <span data-ttu-id="c5a82-222">Aprire il file Applicationmanifest.xml che si trova nella cartella ApplicationPackageRoot del progetto AlphabetPartitions e impostare il parametro Processing_PartitionCount su 26, come mostrato sotto.</span><span class="sxs-lookup"><span data-stu-id="c5a82-222">Open the Applicationmanifest.xml file located in the ApplicationPackageRoot folder of the AlphabetPartitions project and update the parameter Processing_PartitionCount to 26 as shown below.</span></span>
   
    ```xml
    <Parameter Name="Processing_PartitionCount" DefaultValue="26" />
    ```
   
    <span data-ttu-id="c5a82-223">È anche necessario aggiornare le proprietà LowKey e HighKey dell'elemento StatefulService in ApplicationManifest.xml come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="c5a82-223">You also need to update the LowKey and HighKey properties of the StatefulService element in the ApplicationManifest.xml as shown below.</span></span>
   
    ```xml
    <Service Name="Processing">
      <StatefulService ServiceTypeName="ProcessingType" TargetReplicaSetSize="[Processing_TargetReplicaSetSize]" MinReplicaSetSize="[Processing_MinReplicaSetSize]">
        <UniformInt64Partition PartitionCount="[Processing_PartitionCount]" LowKey="0" HighKey="25" />
      </StatefulService>
    </Service>
    ```
6. <span data-ttu-id="c5a82-224">Per rendere accessibile il servizio, aprire un endpoint su una porta aggiungendo l'elemento endpoint di ServiceManifest.xml (nella cartella PackageRoot) per il servizio Alphabet.Processing, come mostrato sotto:</span><span class="sxs-lookup"><span data-stu-id="c5a82-224">For the service to be accessible, open up an endpoint on a port by adding the endpoint element of ServiceManifest.xml (located in the PackageRoot folder) for the Alphabet.Processing service as shown below:</span></span>
   
    ```xml
    <Endpoint Name="ProcessingServiceEndpoint" Port="8089" Protocol="http" Type="Internal" />
    ```
   
    <span data-ttu-id="c5a82-225">Il servizio ora è configurato per l'ascolto di un endpoint interno con 26 partizioni.</span><span class="sxs-lookup"><span data-stu-id="c5a82-225">Now the service is configured to listen to an internal endpoint with 26 partitions.</span></span>
7. <span data-ttu-id="c5a82-226">In seguito è necessario eseguire l'override del metodo `CreateServiceReplicaListeners()` della classe Processing.</span><span class="sxs-lookup"><span data-stu-id="c5a82-226">Next, you need to override the `CreateServiceReplicaListeners()` method of the Processing class.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c5a82-227">Per questo esempio, si presume che venga usato un semplice oggetto HttpCommunicationListener.</span><span class="sxs-lookup"><span data-stu-id="c5a82-227">For this sample, we assume that you are using a simple HttpCommunicationListener.</span></span> <span data-ttu-id="c5a82-228">Per ulteriori informazioni sulla comunicazione Reliable Service, vedere [Modello di comunicazione Reliable Service](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="c5a82-228">For more information on reliable service communication, see [The Reliable Service communication model](service-fabric-reliable-services-communication.md).</span></span>
   > 
   > 
8. <span data-ttu-id="c5a82-229">Un modello consigliato per l'URL su cui è in ascolto una replica è il formato seguente: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`,</span><span class="sxs-lookup"><span data-stu-id="c5a82-229">A recommended pattern for the URL that a replica listens on is the following format: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.</span></span>
    <span data-ttu-id="c5a82-230">che consente di configurare il listener di comunicazione perché rimanga in ascolto degli endpoint corretti e con questo modello.</span><span class="sxs-lookup"><span data-stu-id="c5a82-230">So you want to configure your communication listener to listen on the correct endpoints and with this pattern.</span></span>
   
    <span data-ttu-id="c5a82-231">Poiché è possibile che più repliche di questo servizio siano ospitate sullo stesso computer, questo indirizzo deve essere univoco per la replica</span><span class="sxs-lookup"><span data-stu-id="c5a82-231">Multiple replicas of this service may be hosted on the same computer, so this address needs to be unique to the replica.</span></span> <span data-ttu-id="c5a82-232">ed è per questo motivo che nell'URL sono presenti un ID partizione e un ID replica.</span><span class="sxs-lookup"><span data-stu-id="c5a82-232">This is why   partition ID + replica ID are in the URL.</span></span> <span data-ttu-id="c5a82-233">HttpListener può essere in ascolto di più indirizzi sulla stessa porta, purché il prefisso dell'URL sia univoco.</span><span class="sxs-lookup"><span data-stu-id="c5a82-233">HttpListener can listen on multiple addresses on the same port as long as the URL prefix    is unique.</span></span>
   
    <span data-ttu-id="c5a82-234">Il GUID aggiuntivo è presente per un caso avanzato in cui anche le repliche secondarie sono in ascolto delle richieste di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="c5a82-234">The extra GUID is there for an advanced case where secondary replicas also listen for read-only requests.</span></span> <span data-ttu-id="c5a82-235">In questo caso, è opportuno assicurarsi che venga usato un nuovo indirizzo univoco quando si passa dalla replica primaria a quelle secondarie per obbligare i client a risolvere nuovamente l'indirizzo.</span><span class="sxs-lookup"><span data-stu-id="c5a82-235">When that's the case, you want to make sure that a new unique address is used when transitioning from primary to secondary to force clients to re-resolve the address.</span></span> <span data-ttu-id="c5a82-236">In questo caso viene usato '+' come indirizzo per fare in modo che la replica sia in ascolto in tutti gli host disponibili (IP, FQDM, localhost, e così via) Il codice seguente mostra un esempio.</span><span class="sxs-lookup"><span data-stu-id="c5a82-236">'+' is used as the address here so that the replica listens on all available hosts (IP, FQDM, localhost, etc.) The code below shows an example.</span></span>
   
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
   
    <span data-ttu-id="c5a82-237">È anche importante notare che l'URL pubblicato è leggermente diverso dal prefisso dell'URL di ascolto.</span><span class="sxs-lookup"><span data-stu-id="c5a82-237">It's also worth noting that the published URL is slightly different from the listening URL prefix.</span></span>
    <span data-ttu-id="c5a82-238">L'URL in ascolto viene assegnato a HttpListener.</span><span class="sxs-lookup"><span data-stu-id="c5a82-238">The listening URL is given to HttpListener.</span></span> <span data-ttu-id="c5a82-239">L'URL pubblicato è l'URL che viene pubblicato nel servizio Naming dell'infrastruttura di servizi, usato per l'individuazione dei servizi.</span><span class="sxs-lookup"><span data-stu-id="c5a82-239">The published URL is the URL that is published to the Service Fabric Naming Service, which is used for service discovery.</span></span> <span data-ttu-id="c5a82-240">I client richiederanno questo indirizzo con questo servizio di individuazione.</span><span class="sxs-lookup"><span data-stu-id="c5a82-240">Clients will ask for this address through that discovery service.</span></span> <span data-ttu-id="c5a82-241">Poiché l'indirizzo ottenuto dai client deve avere l'IP o il nome FQDN effettivo del nodo per connettersi,</span><span class="sxs-lookup"><span data-stu-id="c5a82-241">The address that clients get needs to have the actual IP or FQDN of the node in order to connect.</span></span> <span data-ttu-id="c5a82-242">è necessario sostituire "+" con l'IP o il nome FQDN del nodo, come mostrato sotto.</span><span class="sxs-lookup"><span data-stu-id="c5a82-242">So you need to replace '+' with the node's IP or FQDN as shown above.</span></span>
9. <span data-ttu-id="c5a82-243">L'ultimo passaggio consiste nell'aggiungere la logica di elaborazione al servizio, come mostrato sotto.</span><span class="sxs-lookup"><span data-stu-id="c5a82-243">The last step is to add the processing logic to the service as shown below.</span></span>
   
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
   
    <span data-ttu-id="c5a82-244">`ProcessInternalRequest` legge i valori del parametro della stringa di query usato per chiamare la partizione e chiama `AddUserAsync` per aggiungere il cognome al dizionario attendibile `dictionary`.</span><span class="sxs-lookup"><span data-stu-id="c5a82-244">`ProcessInternalRequest` reads the values of the query string parameter used to call the partition and calls `AddUserAsync` to add the lastname to the reliable dictionary `dictionary`.</span></span>
10. <span data-ttu-id="c5a82-245">Ora si aggiungerà un servizio senza stato al progetto per verificare se sia possibile chiamare una determinata partizione.</span><span class="sxs-lookup"><span data-stu-id="c5a82-245">Let's add a stateless service to the project to see how you can call a particular partition.</span></span>
    
    <span data-ttu-id="c5a82-246">Questo servizio viene usato come semplice interfaccia Web che accetta il cognome come parametro della stringa di query, determina la chiave di partizione e la invia al servizio Alphabet.Processing per l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="c5a82-246">This service serves as a simple web interface that accepts the lastname as a query string parameter, determines the partition key, and sends it to the Alphabet.Processing service for processing.</span></span>
11. <span data-ttu-id="c5a82-247">Nella finestra di dialogo **Create a Service** (Crea un servizio) scegliere il servizio **senza stato** e assegnargli il nome "Alphabet.Web", come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="c5a82-247">In the **Create a Service** dialog box, choose **Stateless** service and call it "Alphabet.Web" as shown below.</span></span>
    
    ![Schermata di servizio senza stato](./media/service-fabric-concepts-partitioning/createnewstateless.png)<span data-ttu-id="c5a82-249">.</span><span class="sxs-lookup"><span data-stu-id="c5a82-249">.</span></span>
12. <span data-ttu-id="c5a82-250">Aggiornare le informazioni sull'endpoint nel file ServiceManifest.xml del servizio Alphabet.WebApi per aprire una porta, come mostrato sotto.</span><span class="sxs-lookup"><span data-stu-id="c5a82-250">Update the endpoint information in the ServiceManifest.xml of the Alphabet.WebApi service to open up a port as shown below.</span></span>
    
    ```xml
    <Endpoint Name="WebApiServiceEndpoint" Protocol="http" Port="8081"/>
    ```
13. <span data-ttu-id="c5a82-251">È necessario restituire una raccolta di ServiceInstanceListener nella classe Web.</span><span class="sxs-lookup"><span data-stu-id="c5a82-251">You need to return a collection of ServiceInstanceListeners in the class Web.</span></span> <span data-ttu-id="c5a82-252">Anche in questo caso è possibile scegliere di implementare un semplice HttpCommunicationListener.</span><span class="sxs-lookup"><span data-stu-id="c5a82-252">Again, you can choose to implement a simple HttpCommunicationListener.</span></span>
    
    ```CSharp
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] {new ServiceInstanceListener(context => this.CreateInputListener(context))};
    }
    private ICommunicationListener CreateInputListener(ServiceContext context)
    {
        // Service instance's URL is the node's IP & desired port
        EndpointResourceDescription inputEndpoint = context.CodePackageActivationContext.GetEndpoint("WebApiServiceEndpoint")
        string uriPrefix = String.Format("{0}://+:{1}/alphabetpartitions/", inputEndpoint.Protocol, inputEndpoint.Port);
        var uriPublished = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
        return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInputRequest);
    }
    ```
14. <span data-ttu-id="c5a82-253">Ora è necessario implementare la logica di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="c5a82-253">Now you need to implement the processing logic.</span></span> <span data-ttu-id="c5a82-254">HttpCommunicationListener chiama `ProcessInputRequest` quando arriva una richiesta.</span><span class="sxs-lookup"><span data-stu-id="c5a82-254">The HttpCommunicationListener calls `ProcessInputRequest` when a request comes in.</span></span> <span data-ttu-id="c5a82-255">Ora aggiungere il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="c5a82-255">So let's go ahead and add the code below.</span></span>
    
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
                    "Result: {0}. <p>Partition key: '{1}' generated from the first letter '{2}' of input value '{3}'. <br>Processing service partition ID: {4}. <br>Processing service replica address: {5}",
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
                output = output + "added to Partition: " + primaryReplicaAddress;
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    ```
    
    <span data-ttu-id="c5a82-256">Analisi dettagliata:</span><span class="sxs-lookup"><span data-stu-id="c5a82-256">Let's walk through it step by step.</span></span> <span data-ttu-id="c5a82-257">il codice legge la prima lettera del parametro della stringa di query `lastname` in un char.</span><span class="sxs-lookup"><span data-stu-id="c5a82-257">The code reads the first letter of the query string parameter `lastname` into a char.</span></span> <span data-ttu-id="c5a82-258">Quindi determina la chiave di partizione di questa lettera sottraendo il valore esadecimale di `A` dal valore esadecimale della prima lettera dei cognomi.</span><span class="sxs-lookup"><span data-stu-id="c5a82-258">Then, it determines the partition key for this letter by subtracting the hexadecimal value of `A` from the hexadecimal value of the last names' first letter.</span></span>
    
    ```CSharp
    string lastname = context.Request.QueryString["lastname"];
    char firstLetterOfLastName = lastname.First();
    ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    ```
    
    <span data-ttu-id="c5a82-259">Si ricordi che in questo esempio si usano 26 partizioni con una chiave per ogni partizione.</span><span class="sxs-lookup"><span data-stu-id="c5a82-259">Remember, for this example, we are using 26 partitions with one partition key per partition.</span></span>
    <span data-ttu-id="c5a82-260">A questo punto è necessario ottenere la partizione del servizio `partition` per la chiave usando il metodo `ResolveAsync` nell'oggetto `servicePartitionResolver`.</span><span class="sxs-lookup"><span data-stu-id="c5a82-260">Next, we obtain the service partition `partition` for this key by using the `ResolveAsync` method on the `servicePartitionResolver` object.</span></span> <span data-ttu-id="c5a82-261">`servicePartitionResolver` viene definito come mostrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="c5a82-261">`servicePartitionResolver` is defined as</span></span>
    
    ```CSharp
    private readonly ServicePartitionResolver servicePartitionResolver = ServicePartitionResolver.GetDefault();
    ```
    
    <span data-ttu-id="c5a82-262">Il metodo `ResolveAsync` accetta l'URI del servizio, la chiave di partizione e un token di annullamento come parametri.</span><span class="sxs-lookup"><span data-stu-id="c5a82-262">The `ResolveAsync` method takes the service URI, the partition key, and a cancellation token as parameters.</span></span> <span data-ttu-id="c5a82-263">L'URI del servizio di elaborazione è `fabric:/AlphabetPartitions/Processing`.</span><span class="sxs-lookup"><span data-stu-id="c5a82-263">The service URI for the processing service is `fabric:/AlphabetPartitions/Processing`.</span></span> <span data-ttu-id="c5a82-264">A questo punto è necessario ottenere l'endpoint della partizione.</span><span class="sxs-lookup"><span data-stu-id="c5a82-264">Next, we get the endpoint of the partition.</span></span>
    
    ```CSharp
    ResolvedServiceEndpoint ep = partition.GetEndpoint()
    ```
    
    <span data-ttu-id="c5a82-265">Infine si compilano l'URL dell'endpoint e la stringa di query e si chiama il servizio di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="c5a82-265">Finally, we build the endpoint URL plus the querystring and call the processing service.</span></span>
    
    ```CSharp
    JObject addresses = JObject.Parse(ep.Address);
    string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
    UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
    primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
    string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    ```
    
    <span data-ttu-id="c5a82-266">Una volta completata l'elaborazione, si scrive l'output.</span><span class="sxs-lookup"><span data-stu-id="c5a82-266">Once the processing is done, we write the output back.</span></span>
15. <span data-ttu-id="c5a82-267">L'ultimo passaggio consiste nel testare il servizio.</span><span class="sxs-lookup"><span data-stu-id="c5a82-267">The last step is to test the service.</span></span> <span data-ttu-id="c5a82-268">Visual Studio usa i parametri dell'applicazione per la distribuzione locale e cloud.</span><span class="sxs-lookup"><span data-stu-id="c5a82-268">Visual Studio uses application parameters for local and cloud deployment.</span></span> <span data-ttu-id="c5a82-269">Per testare il servizio in locale con 26 partizioni, è necessario aggiornare il file `Local.xml` nella cartella ApplicationParameters del progetto AlphabetPartitions, come mostrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="c5a82-269">To test the service with 26 partitions locally, you need to update the `Local.xml` file in the ApplicationParameters folder of the AlphabetPartitions project as shown below:</span></span>
    
    ```xml
    <Parameters>
      <Parameter Name="Processing_PartitionCount" Value="26" />
      <Parameter Name="WebApi_InstanceCount" Value="1" />
    </Parameters>
    ```
16. <span data-ttu-id="c5a82-270">Al termine del processo di distribuzione, è possibile controllare il servizio e tutte le partizioni in Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="c5a82-270">Once you finish deployment, you can check the service and all of its partitions in the Service Fabric Explorer.</span></span>
    
    ![Schermata di Service Fabric Explorer](./media/service-fabric-concepts-partitioning/sfxpartitions.png)
17. <span data-ttu-id="c5a82-272">Per testare la logica di partizionamento, immettere `http://localhost:8081/?lastname=somename`in un browser.</span><span class="sxs-lookup"><span data-stu-id="c5a82-272">In a browser, you can test the partitioning logic by entering `http://localhost:8081/?lastname=somename`.</span></span> <span data-ttu-id="c5a82-273">Ogni cognome che inizia con la stessa lettera risulta archiviato nella stessa partizione.</span><span class="sxs-lookup"><span data-stu-id="c5a82-273">You will see that each last name that starts with the same letter is being stored in the same partition.</span></span>
    
    ![Schermata del browser](./media/service-fabric-concepts-partitioning/samplerunning.png)

<span data-ttu-id="c5a82-275">L'intero codice sorgente dell'esempio è disponibile in [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span><span class="sxs-lookup"><span data-stu-id="c5a82-275">The entire source code of the sample is available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5a82-276">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c5a82-276">Next steps</span></span>
<span data-ttu-id="c5a82-277">Per informazioni sui concetti relativi a Service Fabric, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="c5a82-277">For information on Service Fabric concepts, see the following:</span></span>

* [<span data-ttu-id="c5a82-278">Disponibilità dei servizi di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c5a82-278">Availability of Service Fabric services</span></span>](service-fabric-availability-services.md)
* [<span data-ttu-id="c5a82-279">Scalabilità dei servizi di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c5a82-279">Scalability of Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
* [<span data-ttu-id="c5a82-280">Pianificazione della capacità per le applicazioni Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c5a82-280">Capacity planning for Service Fabric applications</span></span>](service-fabric-capacity-planning.md)

[wikipartition]: https://en.wikipedia.org/wiki/Partition_(database)

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png