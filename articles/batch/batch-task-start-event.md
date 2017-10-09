---
title: "aaa \"eventi di avvio attività di Azure Batch | Documenti di Microsoft\""
description: "Riferimento per l'evento di avvio dell'attività batch."
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
ms.openlocfilehash: 2cb066be1578741125e9081a84a2b7c74dc8356a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="task-start-event"></a>Evento di avvio attività

 Questo evento viene generato quando un'attività è stata pianificata toostart su un nodo di calcolo dall'utilità di pianificazione hello. Si noti che se l'attività hello viene ritentata o reinserito nella coda questo evento viene emesso nuovamente per hello stessa attività, ma hello numero di tentativi e versione dell'attività del sistema verrà aggiornato di conseguenza.


 Hello esempio seguente viene illustrato hello corpo di un evento di inizio delle attività.

```
{
    "jobId": "job-0000000001",
    "id": "task-5",
    "taskType": "User",
    "systemTaskVersion": 0,
    "nodeInfo": {
        "poolId": "pool-001",
        "nodeId": "tvm-257509324_1-20160908t162728z"
    },
    "multiInstanceSettings": {
        "numberOfInstances": 1
    },
    "constraints": {
        "maxTaskRetryCount": 2
    },
    "executionInfo": {
        "retryCount": 0
    }
}
```

|Nome dell'elemento|Tipo|Note|
|------------------|----------|-----------|
|jobId|String|id di Hello del processo di hello contenente attività hello.|
|id|String|id di Hello dell'attività hello.|
|taskType|String|tipo di Hello dell'attività hello. Il valore può essere "JobManager" per indicare che si tratta di un'attività del gestore di processi oppure 'User' per indicare che non si tratta di un'attività del gestore di processi.|
|systemTaskVersion|Int32|Si tratta di contatore dei tentativi interni hello in un'attività. Servizio Batch hello internamente possibile riprovare a eseguire un tooaccount di attività per errori temporanei. Questi problemi possono includere interno pianificazione errori o tentativi toorecover da nodi di calcolo in uno stato non valido.|
|[nodeInfo](#nodeInfo)|Tipo complesso|Contiene informazioni sul nodo di calcolo hello in cui hello attività è stata eseguita.|
|[multiInstanceSettings](#multiInstanceSettings)|Tipo complesso|Specifica che l'attività hello è multi-istanza attività che richiedono più nodi di calcolo.  Per informazioni dettagliate, vedere [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task).|
|[constraints](#constraints)|Tipo complesso|vincoli di esecuzione Hello che si applicano toothis attività.|
|[executionInfo](#executionInfo)|Tipo complesso|Contiene informazioni sull'esecuzione di hello dell'attività hello.|

###  <a name="nodeInfo"></a> nodeInfo

|Nome dell'elemento|Tipo|Note|
|------------------|----------|-----------|
|poolId|String|Hello l'id del pool di hello in cui hello attività è stata eseguita.|
|nodeId|String|Hello l'id del nodo di hello in cui hello attività è stata eseguita.|

###  <a name="multiInstanceSettings"></a> multiInstanceSettings

|Nome dell'elemento|Tipo|Note|
|------------------|----------|-----------|
|numberOfInstances|int|numero di Hello dei nodi di calcolo richiesto da attività hello.|

###  <a name="constraints"></a> constraints

|Nome dell'elemento|Tipo|Note|
|------------------|----------|-----------|
|maxTaskRetryCount|Int32|numero massimo di tentativi di esecuzione attività hello può essere di Hello. servizio Batch Hello Riprova a eseguire un'attività se il codice di uscita è diverso da zero.<br /><br /> Si noti che questo valore controlla in particolare il numero di hello di tentativi. servizio Batch Hello tenterà attività hello una sola volta e può quindi ripetere di toothis limite. Ad esempio, se il numero massimo di tentativi di hello è 3, Batch tenta un'operazione di backup too4 volte (tentativo iniziale di uno e 3 tentativi).<br /><br /> Se il numero massimo di tentativi di hello è 0, hello servizio Batch non ripetere l'attività.<br /><br /> Se il numero massimo di tentativi di hello è -1, il servizio Batch hello tentativi attività senza limiti.<br /><br /> valore predefinito di Hello è 0 (nessun tentativo).|

###  <a name="executionInfo"></a> executionInfo

|Nome dell'elemento|Tipo|Note|
|------------------|----------|-----------|
|retryCount|Int32|numero di volte in cui è stato ripetuto attività hello dal servizio Batch hello di Hello. attività di Hello viene ritentata se si conclude con un codice di uscita diverso da zero, backup toohello specificato MaxTaskRetryCount|
