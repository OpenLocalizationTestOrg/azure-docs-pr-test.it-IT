---
title: Elementi interni delle raccolte Reliable Collections e di Reliable State Manager in Azure Service Fabric | Microsoft Docs
description: Approfondimento dei concetti e della progettazione delle raccolte Reliable Collections in Azure Service Fabric.
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: mcoskun
ms.openlocfilehash: d607449a16e886337ab1bd96213fbb4231124353
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-service-fabric-reliable-state-manager-and-reliable-collection-internals"></a><span data-ttu-id="6afed-103">Elementi interni delle raccolte Reliable Collections e di Reliable State Manager in Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6afed-103">Azure Service Fabric Reliable State Manager and Reliable Collection internals</span></span>
<span data-ttu-id="6afed-104">Questo articolo tratta in modo approfondito Reliable State Manager e le raccolte Reliable Collections per spiegare il funzionamento in background dei componenti di base.</span><span class="sxs-lookup"><span data-stu-id="6afed-104">This document delves inside Reliable State Manager and Reliable Collections to see how core components work behind the scenes.</span></span>

> [!NOTE]
> <span data-ttu-id="6afed-105">Il documento è in continua evoluzione</span><span class="sxs-lookup"><span data-stu-id="6afed-105">This document is work in-progress.</span></span> <span data-ttu-id="6afed-106">ed è possibile aggiungere commenti all'articolo per indicare gli argomenti per cui si richiedono maggiori informazioni.</span><span class="sxs-lookup"><span data-stu-id="6afed-106">Add comments to this article to tell us what topic you would like to learn more about.</span></span>
>

##  <a name="local-persistence-model-log-and-checkpoint"></a><span data-ttu-id="6afed-107">Modello di persistenza locale: log e checkpoint</span><span class="sxs-lookup"><span data-stu-id="6afed-107">Local persistence model: log and checkpoint</span></span>
<span data-ttu-id="6afed-108">Reliable State Manager e le raccolte Reliable Collections seguono un modello di persistenza basato su log e checkpoint.</span><span class="sxs-lookup"><span data-stu-id="6afed-108">The Reliable State Manager and Reliable Collections follow a persistence model that is called Log and Checkpoint.</span></span>
<span data-ttu-id="6afed-109">In questo modello ogni cambiamento di stato viene registrato per prima cosa sul disco e quindi applicato in memoria.</span><span class="sxs-lookup"><span data-stu-id="6afed-109">In this model, each state change is logged on disk first and then applied in memory.</span></span>
<span data-ttu-id="6afed-110">Lo stesso stato completo viene reso persistente solo occasionalmente (noto anche come</span><span class="sxs-lookup"><span data-stu-id="6afed-110">The complete state itself is persisted only occasionally (a.k.a.</span></span> <span data-ttu-id="6afed-111">Checkpoint).</span><span class="sxs-lookup"><span data-stu-id="6afed-111">Checkpoint).</span></span>
<span data-ttu-id="6afed-112">Il vantaggio è che per migliorare le prestazioni, le differenze vengono trasformate in operazioni di scrittura sequenziali di solo accodamento sul disco.</span><span class="sxs-lookup"><span data-stu-id="6afed-112">The benefit is that deltas are turned into sequential append-only writes on disk for improved performance.</span></span>

<span data-ttu-id="6afed-113">Per comprendere meglio il modello basato su log e checkpoint, considerare prima di tutto lo scenario con disco infinito.</span><span class="sxs-lookup"><span data-stu-id="6afed-113">To better understand the Log and Checkpoint model, let’s first look at the infinite disk scenario.</span></span>
<span data-ttu-id="6afed-114">Reliable State Manager registra ogni operazione prima che venga replicata.</span><span class="sxs-lookup"><span data-stu-id="6afed-114">The Reliable State Manager logs every operation before it is replicated.</span></span>
<span data-ttu-id="6afed-115">La registrazione consente alla raccolta Reliable Collections di applicare l'operazione solo in memoria.</span><span class="sxs-lookup"><span data-stu-id="6afed-115">Logging allows the Reliable Collections to apply the operation only in memory.</span></span>
<span data-ttu-id="6afed-116">Dal momento che i log sono persistenti, anche se la replica ha esito negativo e deve essere riavviata, Reliable State Manager dispone di informazioni sufficienti per riprodurre tutte le operazioni perse dalla replica.</span><span class="sxs-lookup"><span data-stu-id="6afed-116">Since logs are persisted, even when the replica fails and needs to be restarted, the Reliable State Manager has enough information in its log to replay all the operations the replica has lost.</span></span>
<span data-ttu-id="6afed-117">Poiché il disco è infinito, non è mai necessario rimuovere i record del log e Reliable Collections deve gestire solo lo stato in memoria.</span><span class="sxs-lookup"><span data-stu-id="6afed-117">As the disk is infinite, log records never need to be removed and the Reliable Collection needs to manage only the in-memory state.</span></span>

<span data-ttu-id="6afed-118">Si prenda ora in considerazione lo scenario con disco finito.</span><span class="sxs-lookup"><span data-stu-id="6afed-118">Now let’s look at the finite disk scenario.</span></span>
<span data-ttu-id="6afed-119">Mano a mano che si accumulano i record di log, Reliable State Manager non avrà più spazio su disco a disposizione.</span><span class="sxs-lookup"><span data-stu-id="6afed-119">As log records accumulate, the Reliable State Manager will run out of disk space.</span></span>
<span data-ttu-id="6afed-120">Prima che questo accada, Reliable State Manager deve troncare il proprio log per fare spazio ai record più recenti.</span><span class="sxs-lookup"><span data-stu-id="6afed-120">Before that happens, the Reliable State Manager needs to truncate its log to make room for the newer records.</span></span>
<span data-ttu-id="6afed-121">Reliable State Manager richiede quindi alle raccolte Reliable Collections di inserire un checkpoint del proprio stato in memoria sul disco.</span><span class="sxs-lookup"><span data-stu-id="6afed-121">Reliable State Manager requests the Reliable Collections to checkpoint their in-memory state to disk.</span></span>
<span data-ttu-id="6afed-122">A questo punto, le raccolte Reliable Collections rendono persistente il proprio stato in memoria.</span><span class="sxs-lookup"><span data-stu-id="6afed-122">At this point, the Reliable Collections' would persist its in-memory state.</span></span>
<span data-ttu-id="6afed-123">Dopo che le raccolte Reliable Collections hanno completato i propri checkpoint, Reliable State Manager può troncare il log per liberare spazio su disco.</span><span class="sxs-lookup"><span data-stu-id="6afed-123">Once the Reliable Collections complete their checkpoints, the Reliable State Manager can truncate the log to free up disk space.</span></span>
<span data-ttu-id="6afed-124">Quando è necessario riavviare la replica, le raccolte Reliable Collections ripristinano il proprio stato in corrispondenza del checkpoint e Reliable State Manager ripristina e riproduce tutte le modifiche apportate allo stato dall'ultimo checkpoint.</span><span class="sxs-lookup"><span data-stu-id="6afed-124">When the replica needs to be restarted, Reliable Collections recover their checkpointed state, and the Reliable State Manager recovers and plays back all the state changes that occurred since the last checkpoint.</span></span>

<span data-ttu-id="6afed-125">L'aggiunta di un altro valore di checkpoint migliora i tempi di ripristino negli scenari comuni.</span><span class="sxs-lookup"><span data-stu-id="6afed-125">Another value add of checkpointing is that it improves recovery times in common scenarios.</span></span> <span data-ttu-id="6afed-126">Il log contiene tutte le operazioni che si sono verificate dall'ultimo checkpoint.</span><span class="sxs-lookup"><span data-stu-id="6afed-126">Log contains all operations that have happened since the last checkpoint.</span></span>
<span data-ttu-id="6afed-127">Pertanto, può includere più versioni di un elemento come più valori per una determinata riga in Reliable Dictionary.</span><span class="sxs-lookup"><span data-stu-id="6afed-127">So it may include multiple versions of an item like multiple values for a given row in Reliable Dictionary.</span></span>
<span data-ttu-id="6afed-128">Al contrario, una raccolta Reliable Collection inserisce un checkpoint solo della versione più recente di ogni valore per una chiave.</span><span class="sxs-lookup"><span data-stu-id="6afed-128">In contrast, a Reliable Collection checkpoints only the latest version of each value for a key.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6afed-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6afed-129">Next steps</span></span>
* [<span data-ttu-id="6afed-130">Transazioni e blocchi</span><span class="sxs-lookup"><span data-stu-id="6afed-130">Transactions and Locks</span></span>](service-fabric-reliable-services-reliable-collections-transactions-locks.md)

