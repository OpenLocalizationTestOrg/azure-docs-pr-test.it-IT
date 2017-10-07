---
title: aaa "evento di avvio del ridimensionamento del pool di Azure Batch | Documenti di Microsoft"
description: "Riferimento per l’evento di avvio ridimensionamento del pool di batch."
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
ms.openlocfilehash: 2ca2a4f1195c3f785ae5b051b63340f70eecbc22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="pool-resize-start-event"></a>Evento di avvio ridimensionamento pool

 Questo evento viene generato quando un ridimensionamento pool è stato avviato. Poiché ridimensionamento pool hello è un evento asincrono, è possibile prevedere un toobe evento di completamento del ridimensionamento pool generato dopo l'operazione di ridimensionamento hello viene completata.

 Ridimensiona Hello Mostra hello corpo di un evento di avvio di ridimensionamento del pool per il ridimensionamento del pool da 0 too2 nodi con un manuale di esempio seguente.

```
{
    "poolId": "myPool1",
    "nodeDeallocationOption": "invalid",
    "currentDedicated": 0,
    "targetDedicated": 2,
    "enableAutoScale": false,
    "isAutoPool": false
}
```

|Elemento|Tipo|Note|
|-------------|----------|-----------|
|poolId|String|id di Hello del pool di hello.|
|nodeDeallocationOption|String|Se quando i nodi potrebbero essere rimosse dal pool di hello, dimensioni del pool di hello sono decrescente.<br /><br /> I valori possibili sono:<br /><br /> **requeue**: termina le attività in esecuzione e le reinserisce nella coda. attività Hello verrà eseguito nuovamente durante il processo di hello è abilitato. I nodi vengono rimossi non appena le attività sono state terminate.<br /><br /> **terminate**: termina le attività in esecuzione. attività Hello non verranno più eseguite. I nodi vengono rimossi non appena le attività sono state terminate.<br /><br /> **taskcompletion** : Consenti toocomplete attività in corso. Non viene pianificata alcuna nuova attività durante l'attesa. I nodi vengono rimossi al completamento di tutte le attività.<br /><br /> **Retaineddata** : attualmente in esecuzione attività toocomplete, quindi attendere tutte tooexpire periodi di conservazione dei dati di attività. Non viene pianificata alcuna nuova attività durante l'attesa. I nodi vengono rimossi alla scadenza di tutti i periodi di conservazione dati delle attività.<br /><br /> valore predefinito di Hello è riaccodamento.<br /><br /> Se l'aumentano di dimensioni del pool di hello, hello è impostato troppo**valido**.|
|currentDedicated|Int32|numero di nodi di calcolo di Hello attualmente assegnati toohello pool.|
|targetDedicated|Int32|numero di Hello di nodi di calcolo che sono richieste per il pool di hello.|
|enableAutoScale|Booleano|Specifica se le dimensioni del pool di hello viene ridimensionato automaticamente nel corso del tempo.|
|isAutoPool|Booleano|Specifica se il pool di hello è stato creato tramite il meccanismo di pool automatico di un processo.|
