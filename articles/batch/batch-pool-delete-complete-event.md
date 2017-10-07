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
# <a name="pool-delete-complete-event"></a>Evento di completamento eliminazione pool

 Questo evento viene generato quando un'operazione di eliminazione pool è stata completata.

 Hello esempio seguente viene illustrato hello corpo di un evento di completamento Elimina pool.

```
{
    "id": "myPool1",
    "startTime": "2016-09-09T22:13:48.579Z",
    "endTime": "2016-09-09T22:14:08.836Z"
}
```

|Elemento|Tipo|Note|
|-------------|----------|-----------|
|id|String|id di Hello del pool di hello.|
|startTime|DateTime|Hello eliminare pool hello avvio.|
|endTime|DateTime|Hello tempo eliminare pool hello completata.|

## <a name="remarks"></a>Osservazioni
Per altre informazioni sugli stati e sui codici di errore per l'operazione di ridimensionamento pool, vedere [Delete a pool from an account](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account) (Eliminare un pool da un account).