---
title: aaa "pool di Azure Batch eliminare evento completo | Documenti di Microsoft"
description: "Riferimento per l’evento di completamento eliminazione del pool di batch."
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
ms.openlocfilehash: 494c371e48ebfb1bf3d2973a7401829a939ba141
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="pool-delete-complete-event"></a><span data-ttu-id="7a265-103">Evento di completamento eliminazione pool</span><span class="sxs-lookup"><span data-stu-id="7a265-103">Pool delete complete event</span></span>

 <span data-ttu-id="7a265-104">Questo evento viene generato quando un'operazione di eliminazione pool è stata completata.</span><span class="sxs-lookup"><span data-stu-id="7a265-104">This event is emitted when a pool delete operation has completed.</span></span>

 <span data-ttu-id="7a265-105">Hello esempio seguente viene illustrato hello corpo di un evento di completamento Elimina pool.</span><span class="sxs-lookup"><span data-stu-id="7a265-105">hello following example shows hello body of a pool delete complete event.</span></span>

```
{
    "id": "myPool1",
    "startTime": "2016-09-09T22:13:48.579Z",
    "endTime": "2016-09-09T22:14:08.836Z"
}
```

|<span data-ttu-id="7a265-106">Elemento</span><span class="sxs-lookup"><span data-stu-id="7a265-106">Element</span></span>|<span data-ttu-id="7a265-107">Tipo</span><span class="sxs-lookup"><span data-stu-id="7a265-107">Type</span></span>|<span data-ttu-id="7a265-108">Note</span><span class="sxs-lookup"><span data-stu-id="7a265-108">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="7a265-109">id</span><span class="sxs-lookup"><span data-stu-id="7a265-109">id</span></span>|<span data-ttu-id="7a265-110">String</span><span class="sxs-lookup"><span data-stu-id="7a265-110">String</span></span>|<span data-ttu-id="7a265-111">id di Hello del pool di hello.</span><span class="sxs-lookup"><span data-stu-id="7a265-111">hello id of hello pool.</span></span>|
|<span data-ttu-id="7a265-112">startTime</span><span class="sxs-lookup"><span data-stu-id="7a265-112">startTime</span></span>|<span data-ttu-id="7a265-113">DateTime</span><span class="sxs-lookup"><span data-stu-id="7a265-113">DateTime</span></span>|<span data-ttu-id="7a265-114">Hello eliminare pool hello avvio.</span><span class="sxs-lookup"><span data-stu-id="7a265-114">hello time hello pool delete started.</span></span>|
|<span data-ttu-id="7a265-115">endTime</span><span class="sxs-lookup"><span data-stu-id="7a265-115">endTime</span></span>|<span data-ttu-id="7a265-116">DateTime</span><span class="sxs-lookup"><span data-stu-id="7a265-116">DateTime</span></span>|<span data-ttu-id="7a265-117">Hello tempo eliminare pool hello completata.</span><span class="sxs-lookup"><span data-stu-id="7a265-117">hello time hello pool delete completed.</span></span>|

## <a name="remarks"></a><span data-ttu-id="7a265-118">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="7a265-118">Remarks</span></span>
<span data-ttu-id="7a265-119">Per altre informazioni sugli stati e sui codici di errore per l'operazione di ridimensionamento pool, vedere [Delete a pool from an account](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account) (Eliminare un pool da un account).</span><span class="sxs-lookup"><span data-stu-id="7a265-119">For more information about states and error codes for pool resize operation, see [Delete a pool from an account](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span></span>