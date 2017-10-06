---
title: aaa "evento di completamento di ridimensionamento del pool di Azure Batch | Documenti di Microsoft"
description: "Riferimento per l’evento di completamento ridimensionamento del pool di batch."
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
ms.openlocfilehash: dc64711a01aa4cf6192edba1a2c4cad56f953766
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="pool-resize-complete-event"></a>Evento di completamento ridimensionamento pool

 Questo evento viene generato quando il ridimensionamento di un pool è stato completato o non è riuscito.

 Hello esempio seguente viene illustrato hello corpo di un evento di completamento di ridimensionamento pool per un pool di aumenta le dimensioni e completata correttamente.

```
{
    "id": "p_1_0_01503750-252d-4e57-bd96-d6aa05601ad8",
    "nodeDeallocationOption": "invalid",
    "currentDedicated": 4,
    "targetDedicated": 4,
    "enableAutoScale": false,
    "isAutoPool": false,
    "startTime": "2016-09-09T22:13:06.573Z",
    "endTime": "2016-09-09T22:14:01.727Z",
    "result": "Success",
    "resizeError": "hello operation succeeded"
}
```

|Elemento|Tipo|Note|
|-------------|----------|-----------|
|id|String|id di Hello del pool di hello.|
|nodeDeallocationOption|String|Se quando i nodi potrebbero essere rimosse dal pool di hello, dimensioni del pool di hello sono decrescente.<br /><br /> I valori possibili sono:<br /><br /> **requeue**: termina le attività in esecuzione e le reinserisce nella coda. attività Hello verrà eseguito nuovamente durante il processo di hello è abilitato. I nodi vengono rimossi non appena le attività sono state terminate.<br /><br /> **terminate**: termina le attività in esecuzione. attività Hello non verranno più eseguite. I nodi vengono rimossi non appena le attività sono state terminate.<br /><br /> **taskcompletion** : Consenti toocomplete attività in corso. Non viene pianificata alcuna nuova attività durante l'attesa. I nodi vengono rimossi al completamento di tutte le attività.<br /><br /> **Retaineddata** : attualmente in esecuzione attività toocomplete, quindi attendere tutte tooexpire periodi di conservazione dei dati di attività. Non viene pianificata alcuna nuova attività durante l'attesa. I nodi vengono rimossi alla scadenza di tutti i periodi di conservazione dati delle attività.<br /><br /> valore predefinito di Hello è riaccodamento.<br /><br /> Se l'aumentano di dimensioni del pool di hello, hello è impostato troppo**valido**.|
|currentDedicated|Int32|numero di nodi di calcolo di Hello attualmente assegnati toohello pool.|
|targetDedicated|Int32|numero di Hello di nodi di calcolo che sono richieste per il pool di hello.|
|enableAutoScale|Booleano|Specifica se le dimensioni del pool di hello viene ridimensionato automaticamente nel corso del tempo.|
|isAutoPool|Booleano|Specifica se il pool di hello è stato creato tramite il meccanismo di pool automatico di un processo.|
|startTime|DateTime|Hello di ridimensionamento del pool di hello avvio.|
|endTime|DateTime|Hello tempo di ridimensionamento del pool di hello completata.|
|resultCode|String|risultato Hello di hello ridimensionare.|
|resultMessage|String|Errore di ridimensionamento Hello include i dettagli di hello del risultato hello.<br /><br /> Se Ridimensiona hello completata correttamente, gli Stati che hello operazione ha avuto esito positivo.|
