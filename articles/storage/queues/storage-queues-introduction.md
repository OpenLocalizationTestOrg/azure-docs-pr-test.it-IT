---
title: Introduzione all'archiviazione code di Azure | Microsoft Docs
description: Introduzione all'archiviazione code di Azure
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
ms.openlocfilehash: 4db7552a1b76c89151405c55c8682abbb5326bb6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-queues"></a><span data-ttu-id="8d77f-103">Introduzione alle code</span><span class="sxs-lookup"><span data-stu-id="8d77f-103">Introduction to Queues</span></span>

<span data-ttu-id="8d77f-104">Il servizio di archiviazione di accodamento di Azure consente di archiviare grandi quantità di messaggi ai quali è possibile accedere da qualsiasi parte del mondo mediante chiamate autenticate tramite HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="8d77f-104">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="8d77f-105">La dimensione massima di un singolo messaggio della coda è di 64 KB e una coda può contenere milioni di messaggi, nei limiti della capacità complessiva di un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="8d77f-105">A single queue message can be up to 64 KB in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span></span>

## <a name="common-uses"></a><span data-ttu-id="8d77f-106">Utilizzi comuni</span><span class="sxs-lookup"><span data-stu-id="8d77f-106">Common uses</span></span>

<span data-ttu-id="8d77f-107">Di seguito sono riportati gli utilizzi più comuni per il servizio di archiviazione di accodamento.</span><span class="sxs-lookup"><span data-stu-id="8d77f-107">Common uses of Queue storage include:</span></span>

* <span data-ttu-id="8d77f-108">Creazione di un backlog di lavoro da elaborare in modo asincrono</span><span class="sxs-lookup"><span data-stu-id="8d77f-108">Creating a backlog of work to process asynchronously</span></span>
* <span data-ttu-id="8d77f-109">Passaggio di messaggi da un ruolo Web di Azure a un ruolo di lavoro di Azure</span><span class="sxs-lookup"><span data-stu-id="8d77f-109">Passing messages from an Azure web role to an Azure worker role</span></span>

## <a name="queue-service-concepts"></a><span data-ttu-id="8d77f-110">Concetti del servizio di accodamento</span><span class="sxs-lookup"><span data-stu-id="8d77f-110">Queue service concepts</span></span>

<span data-ttu-id="8d77f-111">Il servizio di accodamento contiene i componenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="8d77f-111">The Queue service contains the following components:</span></span>

![Concetti delle code](./media/storage-queues-introduction/queue1.png)

* <span data-ttu-id="8d77f-113">**Formato dell'URL**: è possibile fare riferimento alle code usando il formato di URL seguente:</span><span class="sxs-lookup"><span data-stu-id="8d77f-113">**URL format:** Queues are addressable using the following URL format:</span></span>   
    <span data-ttu-id="8d77f-114">http://`<storage account>`.queue.core.windows.net/`<queue>`</span><span class="sxs-lookup"><span data-stu-id="8d77f-114">http://`<storage account>`.queue.core.windows.net/`<queue>`</span></span> 
  
    <span data-ttu-id="8d77f-115">L'URL seguente fa riferimento a una delle code nel diagramma: </span><span class="sxs-lookup"><span data-stu-id="8d77f-115">The following URL addresses a queue in the diagram:</span></span>  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* <span data-ttu-id="8d77f-116">**Account di archiviazione:** tutti gli accessi ad Archiviazione di Azure vengono eseguiti tramite un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="8d77f-116">**Storage account:** All access to Azure Storage is done through a storage account.</span></span> <span data-ttu-id="8d77f-117">Per informazioni sulla capacità dell'account di archiviazione, vedere [Obiettivi di scalabilità e prestazioni per Archiviazione di Azure](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) .</span><span class="sxs-lookup"><span data-stu-id="8d77f-117">See [Azure Storage Scalability and Performance Targets](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) for details about storage account capacity.</span></span>

* <span data-ttu-id="8d77f-118">**Coda:** una coda contiene un set di messaggi.</span><span class="sxs-lookup"><span data-stu-id="8d77f-118">**Queue:** A queue contains a set of messages.</span></span> <span data-ttu-id="8d77f-119">Tutti i messaggi devono essere inclusi in una coda.</span><span class="sxs-lookup"><span data-stu-id="8d77f-119">All messages must be in a queue.</span></span> <span data-ttu-id="8d77f-120">Si noti che il nome della coda deve essere in lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="8d77f-120">Note that the queue name must be all lowercase.</span></span> <span data-ttu-id="8d77f-121">Per altre informazioni, vedere [Denominazione di code e metadati](https://msdn.microsoft.com/library/azure/dd179349.aspx).</span><span class="sxs-lookup"><span data-stu-id="8d77f-121">For information on naming queues, see [Naming Queues and Metadata](https://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

* <span data-ttu-id="8d77f-122">**Messaggio:** un messaggio, in qualsiasi formato, con dimensioni massime di 64 KB.</span><span class="sxs-lookup"><span data-stu-id="8d77f-122">**Message:** A message, in any format, of up to 64 KB.</span></span> <span data-ttu-id="8d77f-123">Il tempo massimo che un messaggio può rimanere nella coda è di sette giorni.</span><span class="sxs-lookup"><span data-stu-id="8d77f-123">The maximum time that a message can remain in the queue is seven days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d77f-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8d77f-124">Next steps</span></span>

* [<span data-ttu-id="8d77f-125">Creare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="8d77f-125">Create a storage account</span></span>](../storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [<span data-ttu-id="8d77f-126">Introduzione alle code con .NET</span><span class="sxs-lookup"><span data-stu-id="8d77f-126">Getting started with Queues using .NET</span></span>](storage-dotnet-how-to-use-queues.md)
