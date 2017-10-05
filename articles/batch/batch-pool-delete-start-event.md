---
title: Evento di avvio eliminazione pool di Azure Batch | Microsoft Docs
description: "Riferimento per l’evento di avvio eliminazione del pool di batch."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: f8a5241dce422e5c826ab428da6d7bc93284a1cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="pool-delete-start-event"></a><span data-ttu-id="6b44a-103">Evento di avvio eliminazione pool</span><span class="sxs-lookup"><span data-stu-id="6b44a-103">Pool delete start event</span></span>

 <span data-ttu-id="6b44a-104">Questo evento viene generato quando un'operazione di eliminazione pool è stata avviata.</span><span class="sxs-lookup"><span data-stu-id="6b44a-104">This event is emitted when a pool delete operation has started.</span></span> <span data-ttu-id="6b44a-105">Poiché l'eliminazione pool è un evento asincrono, è possibile prevedere l'emissione di un evento di completamento eliminazione pool una volta completata l'operazione di eliminazione.</span><span class="sxs-lookup"><span data-stu-id="6b44a-105">Since the pool delete is an asynchronous event, you can expect a pool delete complete event to be emitted once the delete operation completes.</span></span>

 <span data-ttu-id="6b44a-106">L'esempio seguente illustra il corpo di un evento di avvio eliminazione pool.</span><span class="sxs-lookup"><span data-stu-id="6b44a-106">The following example shows the body of a pool delete start event.</span></span>

```
{
    "id": "myPool1"
}
```

|<span data-ttu-id="6b44a-107">Elemento</span><span class="sxs-lookup"><span data-stu-id="6b44a-107">Element</span></span>|<span data-ttu-id="6b44a-108">Tipo</span><span class="sxs-lookup"><span data-stu-id="6b44a-108">Type</span></span>|<span data-ttu-id="6b44a-109">Note</span><span class="sxs-lookup"><span data-stu-id="6b44a-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="6b44a-110">id</span><span class="sxs-lookup"><span data-stu-id="6b44a-110">id</span></span>|<span data-ttu-id="6b44a-111">String</span><span class="sxs-lookup"><span data-stu-id="6b44a-111">String</span></span>|<span data-ttu-id="6b44a-112">ID del pool.</span><span class="sxs-lookup"><span data-stu-id="6b44a-112">The id of the pool.</span></span>|