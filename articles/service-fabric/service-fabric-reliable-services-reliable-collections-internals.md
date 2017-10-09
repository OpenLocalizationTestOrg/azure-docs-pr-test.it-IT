---
title: elementi interni affidabile stato gestione di servizi dell'infrastruttura e un insieme affidabile aaaAzure | Documenti Microsoft
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
ms.openlocfilehash: 651bfb52785a2475e4840cd471e87220d1936391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-reliable-state-manager-and-reliable-collection-internals"></a><span data-ttu-id="2ed63-103">Elementi interni delle raccolte Reliable Collections e di Reliable State Manager in Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2ed63-103">Azure Service Fabric Reliable State Manager and Reliable Collection internals</span></span>
<span data-ttu-id="2ed63-104">Questo documento affronta all'interno di raccolte affidabile e affidabile di gestione dello stato toosee funzionano dei componenti di base di background hello.</span><span class="sxs-lookup"><span data-stu-id="2ed63-104">This document delves inside Reliable State Manager and Reliable Collections toosee how core components work behind hello scenes.</span></span>

> [!NOTE]
> <span data-ttu-id="2ed63-105">Il documento è in continua evoluzione</span><span class="sxs-lookup"><span data-stu-id="2ed63-105">This document is work in-progress.</span></span> <span data-ttu-id="2ed63-106">Aggiungere commenti toothis articolo tootell us l'argomento desiderato toolearn ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="2ed63-106">Add comments toothis article tootell us what topic you would like toolearn more about.</span></span>
>

##  <a name="local-persistence-model-log-and-checkpoint"></a><span data-ttu-id="2ed63-107">Modello di persistenza locale: log e checkpoint</span><span class="sxs-lookup"><span data-stu-id="2ed63-107">Local persistence model: log and checkpoint</span></span>
<span data-ttu-id="2ed63-108">Hello affidabile di gestione dello stato e le raccolte affidabile seguono un modello di persistenza che viene chiamato Log e dei Checkpoint.</span><span class="sxs-lookup"><span data-stu-id="2ed63-108">hello Reliable State Manager and Reliable Collections follow a persistence model that is called Log and Checkpoint.</span></span>
<span data-ttu-id="2ed63-109">In questo modello ogni cambiamento di stato viene registrato per prima cosa sul disco e quindi applicato in memoria.</span><span class="sxs-lookup"><span data-stu-id="2ed63-109">In this model, each state change is logged on disk first and then applied in memory.</span></span>
<span data-ttu-id="2ed63-110">Hello completo dallo stato viene mantenuto solo occasionalmente (anche noto come</span><span class="sxs-lookup"><span data-stu-id="2ed63-110">hello complete state itself is persisted only occasionally (a.k.a.</span></span> <span data-ttu-id="2ed63-111">Checkpoint).</span><span class="sxs-lookup"><span data-stu-id="2ed63-111">Checkpoint).</span></span>
<span data-ttu-id="2ed63-112">Il vantaggio di Hello è che delta viene convertiti in solo di Accodamento scritture sequenziali su disco per migliorare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="2ed63-112">hello benefit is that deltas are turned into sequential append-only writes on disk for improved performance.</span></span>

<span data-ttu-id="2ed63-113">toobetter comprendere hello Log e il modello di Checkpoint, esaminiamo innanzitutto scenario disco infinito hello.</span><span class="sxs-lookup"><span data-stu-id="2ed63-113">toobetter understand hello Log and Checkpoint model, let’s first look at hello infinite disk scenario.</span></span>
<span data-ttu-id="2ed63-114">prima viene replicato, Hello affidabile di gestione dello stato registra ogni operazione.</span><span class="sxs-lookup"><span data-stu-id="2ed63-114">hello Reliable State Manager logs every operation before it is replicated.</span></span>
<span data-ttu-id="2ed63-115">La registrazione consente hello raccolte affidabile tooapply hello operazione solo in memoria.</span><span class="sxs-lookup"><span data-stu-id="2ed63-115">Logging allows hello Reliable Collections tooapply hello operation only in memory.</span></span>
<span data-ttu-id="2ed63-116">Poiché i registri sono persistenti, anche quando si verifica un errore di replica hello e toobe riavviato, è necessario hello affidabile di gestione dello stato ha informazioni sufficienti nel relativo tooreplay log tutte le operazioni di hello ha perso la replica hello.</span><span class="sxs-lookup"><span data-stu-id="2ed63-116">Since logs are persisted, even when hello replica fails and needs toobe restarted, hello Reliable State Manager has enough information in its log tooreplay all hello operations hello replica has lost.</span></span>
<span data-ttu-id="2ed63-117">Come disco di hello è infinito, i record del log non necessario mai toobe rimosso e la raccolta affidabile hello deve toomanage solo lo stato di hello in memoria.</span><span class="sxs-lookup"><span data-stu-id="2ed63-117">As hello disk is infinite, log records never need toobe removed and hello Reliable Collection needs toomanage only hello in-memory state.</span></span>

<span data-ttu-id="2ed63-118">Ora esaminiamo scenario disco finito hello.</span><span class="sxs-lookup"><span data-stu-id="2ed63-118">Now let’s look at hello finite disk scenario.</span></span>
<span data-ttu-id="2ed63-119">Come record di log si accumulano, verrà eseguita hello affidabile di gestione dello stato spazio su disco insufficiente.</span><span class="sxs-lookup"><span data-stu-id="2ed63-119">As log records accumulate, hello Reliable State Manager will run out of disk space.</span></span>
<span data-ttu-id="2ed63-120">Prima che si verifichi, hello affidabile di gestione dello stato deve tootruncate della sua room toomake log per i record più recenti di hello.</span><span class="sxs-lookup"><span data-stu-id="2ed63-120">Before that happens, hello Reliable State Manager needs tootruncate its log toomake room for hello newer records.</span></span>
<span data-ttu-id="2ed63-121">Le richieste di gestione dello stato di affidabile hello raccolte affidabile toocheckpoint toodisk loro stato in memoria.</span><span class="sxs-lookup"><span data-stu-id="2ed63-121">Reliable State Manager requests hello Reliable Collections toocheckpoint their in-memory state toodisk.</span></span>
<span data-ttu-id="2ed63-122">A questo punto, hello raccolte affidabile' verrebbe persistente lo stato di in memoria.</span><span class="sxs-lookup"><span data-stu-id="2ed63-122">At this point, hello Reliable Collections' would persist its in-memory state.</span></span>
<span data-ttu-id="2ed63-123">Una volta raccolte affidabile hello completare i checkpoint, hello affidabile di gestione dello stato possibile troncare hello log toofree spazio su disco.</span><span class="sxs-lookup"><span data-stu-id="2ed63-123">Once hello Reliable Collections complete their checkpoints, hello Reliable State Manager can truncate hello log toofree up disk space.</span></span>
<span data-ttu-id="2ed63-124">Quando replica hello deve toobe riavviato, raccolte affidabile ripristinare lo stato di Checkpoint e ripristina hello affidabile di gestione dello stato e tutte le modifiche di stato hello che si sono verificati dall'ultimo checkpoint hello viene riprodotto.</span><span class="sxs-lookup"><span data-stu-id="2ed63-124">When hello replica needs toobe restarted, Reliable Collections recover their checkpointed state, and hello Reliable State Manager recovers and plays back all hello state changes that occurred since hello last checkpoint.</span></span>

<span data-ttu-id="2ed63-125">L'aggiunta di un altro valore di checkpoint migliora i tempi di ripristino negli scenari comuni.</span><span class="sxs-lookup"><span data-stu-id="2ed63-125">Another value add of checkpointing is that it improves recovery times in common scenarios.</span></span> <span data-ttu-id="2ed63-126">Log contiene tutte le operazioni che si sono verificati dall'ultimo checkpoint hello.</span><span class="sxs-lookup"><span data-stu-id="2ed63-126">Log contains all operations that have happened since hello last checkpoint.</span></span>
<span data-ttu-id="2ed63-127">Pertanto, può includere più versioni di un elemento come più valori per una determinata riga in Reliable Dictionary.</span><span class="sxs-lookup"><span data-stu-id="2ed63-127">So it may include multiple versions of an item like multiple values for a given row in Reliable Dictionary.</span></span>
<span data-ttu-id="2ed63-128">Al contrario, un checkpoint insieme affidabile hello solo la versione più recente di ogni valore per una chiave.</span><span class="sxs-lookup"><span data-stu-id="2ed63-128">In contrast, a Reliable Collection checkpoints only hello latest version of each value for a key.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ed63-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2ed63-129">Next steps</span></span>
* [<span data-ttu-id="2ed63-130">Transazioni e blocchi</span><span class="sxs-lookup"><span data-stu-id="2ed63-130">Transactions and Locks</span></span>](service-fabric-reliable-services-reliable-collections-transactions-locks.md)

