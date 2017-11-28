---
title: aaa "evento di avvio di Azure Batch pool delete | Documenti di Microsoft"
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
ms.openlocfilehash: 79bb28bffc760a49cc0a95062f5086dc96c6a795
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="pool-delete-start-event"></a><span data-ttu-id="b9409-103">Evento di avvio eliminazione pool</span><span class="sxs-lookup"><span data-stu-id="b9409-103">Pool delete start event</span></span>

 <span data-ttu-id="b9409-104">Questo evento viene generato quando un'operazione di eliminazione pool è stata avviata.</span><span class="sxs-lookup"><span data-stu-id="b9409-104">This event is emitted when a pool delete operation has started.</span></span> <span data-ttu-id="b9409-105">Poiché hello eliminare un pool è un evento asincrono, è possibile prevedere un toobe di evento completo Elimina pool generato dopo l'operazione di eliminazione hello viene completata.</span><span class="sxs-lookup"><span data-stu-id="b9409-105">Since hello pool delete is an asynchronous event, you can expect a pool delete complete event toobe emitted once hello delete operation completes.</span></span>

 <span data-ttu-id="b9409-106">Hello esempio seguente viene illustrato hello corpo di un evento di inizio di eliminazione del pool.</span><span class="sxs-lookup"><span data-stu-id="b9409-106">hello following example shows hello body of a pool delete start event.</span></span>

```
{
    "id": "myPool1"
}
```

|<span data-ttu-id="b9409-107">Elemento</span><span class="sxs-lookup"><span data-stu-id="b9409-107">Element</span></span>|<span data-ttu-id="b9409-108">Tipo</span><span class="sxs-lookup"><span data-stu-id="b9409-108">Type</span></span>|<span data-ttu-id="b9409-109">Note</span><span class="sxs-lookup"><span data-stu-id="b9409-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="b9409-110">id</span><span class="sxs-lookup"><span data-stu-id="b9409-110">id</span></span>|<span data-ttu-id="b9409-111">String</span><span class="sxs-lookup"><span data-stu-id="b9409-111">String</span></span>|<span data-ttu-id="b9409-112">id di Hello del pool di hello.</span><span class="sxs-lookup"><span data-stu-id="b9409-112">hello id of hello pool.</span></span>|
