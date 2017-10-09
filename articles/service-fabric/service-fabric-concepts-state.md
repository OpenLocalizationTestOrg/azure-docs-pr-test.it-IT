---
title: aaaDefinine e gestire lo stato in Azure microservizi | Documenti Microsoft
description: Come toodefine e gestire lo stato del servizio in Service Fabric
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f5e618a5-3ea3-4404-94af-122278f91652
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 4a24696da71753d0f343a86df3556b5b7c964834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-state"></a><span data-ttu-id="f6bf6-103">Stato del servizio</span><span class="sxs-lookup"><span data-stu-id="f6bf6-103">Service state</span></span>
<span data-ttu-id="f6bf6-104">**Stato del servizio** fa riferimento toohello in memoria o su dati su disco che un servizio richiede toofunction.</span><span class="sxs-lookup"><span data-stu-id="f6bf6-104">**Service state** refers toohello in-memory or on disk data that a service requires toofunction.</span></span> <span data-ttu-id="f6bf6-105">Include, ad esempio, le strutture di dati hello e le variabili membro servizio hello legge e scrive toodo lavoro.</span><span class="sxs-lookup"><span data-stu-id="f6bf6-105">It includes, for example, hello data structures and member variables that hello service reads and writes toodo work.</span></span> <span data-ttu-id="f6bf6-106">A seconda della modalità progettazione di un servizio hello, può anche includere file o altre risorse che sono archiviati su disco.</span><span class="sxs-lookup"><span data-stu-id="f6bf6-106">Depending on how hello service is architected, it could also include files or other resources that are stored on disk.</span></span> <span data-ttu-id="f6bf6-107">File di un database, ad esempio, hello utilizzerebbe toostore registri delle transazioni e di dati.</span><span class="sxs-lookup"><span data-stu-id="f6bf6-107">For example, hello files a database would use toostore data and transaction logs.</span></span>

<span data-ttu-id="f6bf6-108">Come un servizio di esempio, si consideri una calcolatrice.</span><span class="sxs-lookup"><span data-stu-id="f6bf6-108">As an example service, let's consider a calculator.</span></span> <span data-ttu-id="f6bf6-109">Questo servizio di calcolatrice di base accetta due numeri per restituirne la somma.</span><span class="sxs-lookup"><span data-stu-id="f6bf6-109">A basic calculator service takes two numbers and returns their sum.</span></span> <span data-ttu-id="f6bf6-110">L'esecuzione di questo calcolo non implica alcuna variabile membro o altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="f6bf6-110">Performing this calculation involves no member variables or other information.</span></span>

<span data-ttu-id="f6bf6-111">Si consideri ora hello calcolatrice stessa, ma con un metodo aggiuntivo per l'archiviazione e la restituzione ultima somma di hello è calcolato.</span><span class="sxs-lookup"><span data-stu-id="f6bf6-111">Now consider hello same calculator, but with an additional method for storing and returning hello last sum it has computed.</span></span> <span data-ttu-id="f6bf6-112">Il servizio è ora con stato.</span><span class="sxs-lookup"><span data-stu-id="f6bf6-112">This service is now stateful.</span></span> <span data-ttu-id="f6bf6-113">Informazioni sullo stato significa che contiene uno stato che scrive toowhen calcola la somma di nuovo e legge da quando si chiede somma calcolata di tooreturn hello ultimo.</span><span class="sxs-lookup"><span data-stu-id="f6bf6-113">Stateful means it contains some state that it writes toowhen it computes a new sum and reads from when you ask it tooreturn hello last computed sum.</span></span>

<span data-ttu-id="f6bf6-114">In Azure Service Fabric, primo servizio hello viene chiamato un servizio senza stato.</span><span class="sxs-lookup"><span data-stu-id="f6bf6-114">In Azure Service Fabric, hello first service is called a stateless service.</span></span> <span data-ttu-id="f6bf6-115">secondo servizio Hello viene chiamato un servizio con stato.</span><span class="sxs-lookup"><span data-stu-id="f6bf6-115">hello second service is called a stateful service.</span></span>

## <a name="storing-service-state"></a><span data-ttu-id="f6bf6-116">Archiviazione dello stato del servizio</span><span class="sxs-lookup"><span data-stu-id="f6bf6-116">Storing service state</span></span>
<span data-ttu-id="f6bf6-117">Lo stato può essere esternalizzato o con percorso condiviso con codice di hello che sta modificando lo stato di hello.</span><span class="sxs-lookup"><span data-stu-id="f6bf6-117">State can be either externalized or co-located with hello code that is manipulating hello state.</span></span> <span data-ttu-id="f6bf6-118">Esternalizzazione di stato è in genere eseguita con un database esterno o altri dati di archiviano che viene eseguito in computer diversi tramite rete hello o fuori del processo su hello nello stesso computer.</span><span class="sxs-lookup"><span data-stu-id="f6bf6-118">Externalization of state is typically done by using an external database or other data store that runs on different machines over hello network or out of process on hello same machine.</span></span> <span data-ttu-id="f6bf6-119">In questo esempio, la calcolatrice archivio dati hello potrebbe essere un database SQL o un'istanza dell'archivio tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="f6bf6-119">In our calculator example, hello data store could be a SQL database or instance of Azure Table Store.</span></span> <span data-ttu-id="f6bf6-120">Somma di hello toocompute ogni richiesta esegue un aggiornamento per i dati e richieste toohello servizio tooreturn hello valore generano valore corrente di hello recuperati dall'archivio hello.</span><span class="sxs-lookup"><span data-stu-id="f6bf6-120">Every request toocompute hello sum performs an update on this data, and requests toohello service tooreturn hello value result in hello current value being fetched from hello store.</span></span> 

<span data-ttu-id="f6bf6-121">Lo stato può anche essere condiviso con codice hello che modifica lo stato di hello.</span><span class="sxs-lookup"><span data-stu-id="f6bf6-121">State can also be co-located with hello code that manipulates hello state.</span></span> <span data-ttu-id="f6bf6-122">I servizi con stato in Service Fabric vengono in genere creati usando questo modello.</span><span class="sxs-lookup"><span data-stu-id="f6bf6-122">Stateful services in Service Fabric are typically built using this model.</span></span> <span data-ttu-id="f6bf6-123">Service Fabric fornisce hello infrastruttura tooensure che questo stato è altamente disponibile, coerente e durevole e che i servizi di hello creati in questo modo può essere facilmente scalato.</span><span class="sxs-lookup"><span data-stu-id="f6bf6-123">Service Fabric provides hello infrastructure tooensure that this state is highly available, consistent, and durable, and that hello services built this way can easily scale.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6bf6-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f6bf6-124">Next steps</span></span>
<span data-ttu-id="f6bf6-125">Per ulteriori informazioni sui concetti di Service Fabric, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="f6bf6-125">For more information on Service Fabric concepts, see hello following articles:</span></span>

* [<span data-ttu-id="f6bf6-126">Disponibilità dei servizi di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f6bf6-126">Availability of Service Fabric services</span></span>](service-fabric-availability-services.md)
* [<span data-ttu-id="f6bf6-127">Scalabilità dei servizi di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f6bf6-127">Scalability of Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
* [<span data-ttu-id="f6bf6-128">Partizionamento dei servizi di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f6bf6-128">Partitioning Service Fabric services</span></span>](service-fabric-concepts-partitioning.md)
* [<span data-ttu-id="f6bf6-129">Reliable Services di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f6bf6-129">Service Fabric Reliable Services</span></span>](service-fabric-reliable-services-introduction.md)
