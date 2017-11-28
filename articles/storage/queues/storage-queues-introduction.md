---
title: aaaIntroduction tooAzure l'archiviazione delle code | Documenti Microsoft
description: Introduzione tooAzure l'archiviazione delle code
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: robinsh
ms.openlocfilehash: 669effedff7beedde8a119c350a2a70edafedcf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooqueues"></a><span data-ttu-id="06190-103">Introduzione tooQueues</span><span class="sxs-lookup"><span data-stu-id="06190-103">Introduction tooQueues</span></span>

<span data-ttu-id="06190-104">Archiviazione delle code di Azure è un servizio per l'archiviazione di un numero elevato di messaggi che è possibile accedere da qualsiasi in HelloWorld tramite chiamate autenticate tramite HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="06190-104">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="06190-105">Può essere un messaggio nella coda singola too64 KB di dimensioni e una coda può contenere milioni di messaggi, il limite di capacità totale toohello di un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="06190-105">A single queue message can be up too64 KB in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span>

## <a name="common-uses"></a><span data-ttu-id="06190-106">Utilizzi comuni</span><span class="sxs-lookup"><span data-stu-id="06190-106">Common uses</span></span>

<span data-ttu-id="06190-107">Di seguito sono riportati gli utilizzi più comuni per il servizio di archiviazione di accodamento.</span><span class="sxs-lookup"><span data-stu-id="06190-107">Common uses of Queue storage include:</span></span>

* <span data-ttu-id="06190-108">Creazione di un backlog di lavoro tooprocess in modo asincrono</span><span class="sxs-lookup"><span data-stu-id="06190-108">Creating a backlog of work tooprocess asynchronously</span></span>
* <span data-ttu-id="06190-109">Passaggio di messaggi da un ruolo di lavoro di Azure tooan ruolo web di Azure</span><span class="sxs-lookup"><span data-stu-id="06190-109">Passing messages from an Azure web role tooan Azure worker role</span></span>

## <a name="queue-service-concepts"></a><span data-ttu-id="06190-110">Concetti del servizio di accodamento</span><span class="sxs-lookup"><span data-stu-id="06190-110">Queue service concepts</span></span>

<span data-ttu-id="06190-111">servizio di Accodamento Hello contiene hello seguenti componenti:</span><span class="sxs-lookup"><span data-stu-id="06190-111">hello Queue service contains hello following components:</span></span>

![Concetti delle code](./media/storage-queues-introduction/queue1.png)

* <span data-ttu-id="06190-113">**Formato URL:** le code sono indirizzabili mediante hello seguendo il formato di URL:</span><span class="sxs-lookup"><span data-stu-id="06190-113">**URL format:** Queues are addressable using hello following URL format:</span></span>   
    <span data-ttu-id="06190-114">http://`<storage account>`.queue.core.windows.net/`<queue>`</span><span class="sxs-lookup"><span data-stu-id="06190-114">http://`<storage account>`.queue.core.windows.net/`<queue>`</span></span> 
  
    <span data-ttu-id="06190-115">una coda nel diagramma hello è concepito Hello URL seguente:</span><span class="sxs-lookup"><span data-stu-id="06190-115">hello following URL addresses a queue in hello diagram:</span></span>  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* <span data-ttu-id="06190-116">**Account di archiviazione:** tutti gli accessi tooAzure archiviazione viene eseguita tramite un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="06190-116">**Storage account:** All access tooAzure Storage is done through a storage account.</span></span> <span data-ttu-id="06190-117">Per informazioni sulla capacità dell'account di archiviazione, vedere [Obiettivi di scalabilità e prestazioni per Archiviazione di Azure](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) .</span><span class="sxs-lookup"><span data-stu-id="06190-117">See [Azure Storage Scalability and Performance Targets](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) for details about storage account capacity.</span></span>

* <span data-ttu-id="06190-118">**Coda:** una coda contiene un set di messaggi.</span><span class="sxs-lookup"><span data-stu-id="06190-118">**Queue:** A queue contains a set of messages.</span></span> <span data-ttu-id="06190-119">Tutti i messaggi devono essere inclusi in una coda.</span><span class="sxs-lookup"><span data-stu-id="06190-119">All messages must be in a queue.</span></span> <span data-ttu-id="06190-120">Il che nome della coda hello debba essere tutti in lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="06190-120">Note that hello queue name must be all lowercase.</span></span> <span data-ttu-id="06190-121">Per altre informazioni, vedere [Denominazione di code e metadati](https://msdn.microsoft.com/library/azure/dd179349.aspx).</span><span class="sxs-lookup"><span data-stu-id="06190-121">For information on naming queues, see [Naming Queues and Metadata](https://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

* <span data-ttu-id="06190-122">**Messaggio:** un messaggio, in qualsiasi formato, di too64 KB.</span><span class="sxs-lookup"><span data-stu-id="06190-122">**Message:** A message, in any format, of up too64 KB.</span></span> <span data-ttu-id="06190-123">tempo massimo di Hello che un messaggio può rimanere nella coda di hello è sette giorni.</span><span class="sxs-lookup"><span data-stu-id="06190-123">hello maximum time that a message can remain in hello queue is seven days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="06190-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="06190-124">Next steps</span></span>

* [<span data-ttu-id="06190-125">Creare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="06190-125">Create a storage account</span></span>](../storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [<span data-ttu-id="06190-126">Introduzione alle code con .NET</span><span class="sxs-lookup"><span data-stu-id="06190-126">Getting started with Queues using .NET</span></span>](storage-dotnet-how-to-use-queues.md)
