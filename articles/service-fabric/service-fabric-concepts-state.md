---
title: Definire e gestire lo stato nei microservizi di Azure | Documentazione Microsoft
description: Come definire e gestire lo stato di un servizio in Service Fabric
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
ms.openlocfilehash: 2f7835fab175bdb7ef7ce3894cab9e09a39457f3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="service-state"></a><span data-ttu-id="4aee2-103">Stato del servizio</span><span class="sxs-lookup"><span data-stu-id="4aee2-103">Service state</span></span>
<span data-ttu-id="4aee2-104">**Stato del servizio** si riferisce ai dati in memoria o su disco di cui un servizio necessita per funzionare.</span><span class="sxs-lookup"><span data-stu-id="4aee2-104">**Service state** refers to the in-memory or on disk data that a service requires to function.</span></span> <span data-ttu-id="4aee2-105">Si tratta ad esempio delle strutture di dati e delle variabili membro che vengono lette e scritte dal servizio per il funzionamento.</span><span class="sxs-lookup"><span data-stu-id="4aee2-105">It includes, for example, the data structures and member variables that the service reads and writes to do work.</span></span> <span data-ttu-id="4aee2-106">A seconda di come è progettato il servizio, può anche includere file o altre risorse archiviati su disco.</span><span class="sxs-lookup"><span data-stu-id="4aee2-106">Depending on how the service is architected, it could also include files or other resources that are stored on disk.</span></span> <span data-ttu-id="4aee2-107">I file ad esempio che un database userebbe per archiviare log delle transazioni e dati.</span><span class="sxs-lookup"><span data-stu-id="4aee2-107">For example, the files a database would use to store data and transaction logs.</span></span>

<span data-ttu-id="4aee2-108">Come un servizio di esempio, si consideri una calcolatrice.</span><span class="sxs-lookup"><span data-stu-id="4aee2-108">As an example service, let's consider a calculator.</span></span> <span data-ttu-id="4aee2-109">Questo servizio di calcolatrice di base accetta due numeri per restituirne la somma.</span><span class="sxs-lookup"><span data-stu-id="4aee2-109">A basic calculator service takes two numbers and returns their sum.</span></span> <span data-ttu-id="4aee2-110">L'esecuzione di questo calcolo non implica alcuna variabile membro o altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="4aee2-110">Performing this calculation involves no member variables or other information.</span></span>

<span data-ttu-id="4aee2-111">Si consideri ora la stessa calcolatrice, ma con un metodo aggiuntivo di memorizzazione e restituzione dell'ultima somma calcolata.</span><span class="sxs-lookup"><span data-stu-id="4aee2-111">Now consider the same calculator, but with an additional method for storing and returning the last sum it has computed.</span></span> <span data-ttu-id="4aee2-112">Il servizio è ora con stato.</span><span class="sxs-lookup"><span data-stu-id="4aee2-112">This service is now stateful.</span></span> <span data-ttu-id="4aee2-113">Con stato significa che contiene uno stato in cui scrive quando calcola una nuova somma e da cui legge quando viene richiesto di restituire l'ultima somma calcolata.</span><span class="sxs-lookup"><span data-stu-id="4aee2-113">Stateful means it contains some state that it writes to when it computes a new sum and reads from when you ask it to return the last computed sum.</span></span>

<span data-ttu-id="4aee2-114">In Service Fabric di Azure il primo servizio è denominato servizio senza stato.</span><span class="sxs-lookup"><span data-stu-id="4aee2-114">In Azure Service Fabric, the first service is called a stateless service.</span></span> <span data-ttu-id="4aee2-115">Il secondo invece è denominato servizio con stato.</span><span class="sxs-lookup"><span data-stu-id="4aee2-115">The second service is called a stateful service.</span></span>

## <a name="storing-service-state"></a><span data-ttu-id="4aee2-116">Archiviazione dello stato del servizio</span><span class="sxs-lookup"><span data-stu-id="4aee2-116">Storing service state</span></span>
<span data-ttu-id="4aee2-117">Lo stato può essere archiviato all'esterno oppure condividere la posizione con il codice che modifica lo stato.</span><span class="sxs-lookup"><span data-stu-id="4aee2-117">State can be either externalized or co-located with the code that is manipulating the state.</span></span> <span data-ttu-id="4aee2-118">L'esternalizzazione dello stato viene in genere eseguita usando un database esterno o un altro archivio dati eseguito in altri computer sulla rete o all'esterno del processo nello stesso computer.</span><span class="sxs-lookup"><span data-stu-id="4aee2-118">Externalization of state is typically done by using an external database or other data store that runs on different machines over the network or out of process on the same machine.</span></span> <span data-ttu-id="4aee2-119">In questo esempio di calcolatrice, l'archivio dati potrebbe essere un database SQL o un'istanza dell'archivio tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="4aee2-119">In our calculator example, the data store could be a SQL database or instance of Azure Table Store.</span></span> <span data-ttu-id="4aee2-120">Ogni richiesta per calcolare la somma esegue un aggiornamento di questi dati e richiede al servizio di restituire il risultato nel valore corrente recuperato dall'archivio.</span><span class="sxs-lookup"><span data-stu-id="4aee2-120">Every request to compute the sum performs an update on this data, and requests to the service to return the value result in the current value being fetched from the store.</span></span> 

<span data-ttu-id="4aee2-121">Lo stato può anche condividere la posizione con il codice che modifica lo stato.</span><span class="sxs-lookup"><span data-stu-id="4aee2-121">State can also be co-located with the code that manipulates the state.</span></span> <span data-ttu-id="4aee2-122">I servizi con stato in Service Fabric vengono in genere creati usando questo modello.</span><span class="sxs-lookup"><span data-stu-id="4aee2-122">Stateful services in Service Fabric are typically built using this model.</span></span> <span data-ttu-id="4aee2-123">Service Fabric fornisce l'infrastruttura per assicurare che questo stato sia con disponibilità elevata, coerente e durevole e che i servizi creati in questo modo possano essere facilmente scalabili.</span><span class="sxs-lookup"><span data-stu-id="4aee2-123">Service Fabric provides the infrastructure to ensure that this state is highly available, consistent, and durable, and that the services built this way can easily scale.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4aee2-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4aee2-124">Next steps</span></span>
<span data-ttu-id="4aee2-125">Per altre informazioni sui concetti relativi a Service Fabric, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="4aee2-125">For more information on Service Fabric concepts, see the following articles:</span></span>

* [<span data-ttu-id="4aee2-126">Disponibilità dei servizi di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4aee2-126">Availability of Service Fabric services</span></span>](service-fabric-availability-services.md)
* [<span data-ttu-id="4aee2-127">Scalabilità dei servizi di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4aee2-127">Scalability of Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
* [<span data-ttu-id="4aee2-128">Partizionamento dei servizi di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4aee2-128">Partitioning Service Fabric services</span></span>](service-fabric-concepts-partitioning.md)
* [<span data-ttu-id="4aee2-129">Reliable Services di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4aee2-129">Service Fabric Reliable Services</span></span>](service-fabric-reliable-services-introduction.md)
