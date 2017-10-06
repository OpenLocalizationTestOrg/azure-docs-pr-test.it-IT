---
title: "aaa \"evento di completamento di attività di Azure Batch | Documenti di Microsoft\""
description: "Riferimento per l'evento di completamento dell'attività batch."
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
ms.openlocfilehash: c126bf897071c008be3d24190cf77bba5878b807
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="task-complete-event"></a>Evento di completamento attività

 Questo evento viene generato quando un'attività viene completata, indipendentemente dal codice di uscita hello. Questo evento può essere utilizzato toodetermine hello durata di un'attività, di esecuzione delle attività hello e se è stato eseguito un nuovo tentativo.


 Hello esempio seguente viene illustrato hello corpo di un evento di completamento attività.

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
        "startTime": "2016-09-08T16:32:23.799Z",
        "endTime": "2016-09-08T16:34:00.666Z",
        "exitCode": 0,
        "retryCount": 0,
        "requeueCount": 0
    }
}
```

|Nome dell'elemento|Tipo|Note|
|------------------|----------|-----------|
|jobId|String|id di Hello del processo di hello contenente attività hello.|
|id|String|id di Hello dell'attività hello.|
|taskType|String|tipo di Hello dell'attività hello. Il valore può essere "JobManager" per indicare che si tratta di un'attività del gestore di processi oppure 'User' per indicare che non si tratta di un'attività del gestore di processi. Questo evento non viene generato per le attività di preparazione del processo, le attività di rilascio del processo o le attività di avvio.|
|systemTaskVersion|Int32|Si tratta di contatore dei tentativi interni hello in un'attività. Servizio Batch hello internamente possibile riprovare a eseguire un tooaccount di attività per errori temporanei. Questi problemi possono includere interno pianificazione errori o tentativi toorecover da nodi di calcolo in uno stato non valido.|
|[nodeInfo](#nodeInfo)|Tipo complesso|Contiene informazioni sul nodo di calcolo hello in cui hello attività è stata eseguita.|
|[multiInstanceSettings](#multiInstanceSettings)|Tipo complesso|Specifica che l'attività hello è un'attività di multi-istanza che richiedono più nodi di calcolo.  Per informazioni dettagliate, vedere [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task).|
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
|numberOfInstances|Int32|numero di Hello dei nodi di calcolo richiesto da attività hello.|

###  <a name="constraints"></a> constraints

|Nome dell'elemento|Tipo|Note|
|------------------|----------|-----------|
|maxTaskRetryCount|Int32|numero massimo di tentativi di esecuzione attività hello può essere di Hello. servizio Batch Hello Riprova a eseguire un'attività se il codice di uscita è diverso da zero.<br /><br /> Si noti che questo valore controlla in particolare il numero di hello di tentativi. servizio Batch Hello tenterà attività hello una sola volta e può quindi ripetere di toothis limite. Ad esempio, se il numero massimo di tentativi di hello è 3, Batch tenta un'operazione di backup too4 volte (tentativo iniziale di uno e 3 tentativi).<br /><br /> Se il numero massimo di tentativi di hello è 0, hello servizio Batch non ripetere l'attività.<br /><br /> Se il numero massimo di tentativi di hello è -1, il servizio Batch hello tentativi attività senza limiti.<br /><br /> valore predefinito di Hello è 0 (nessun tentativo).|

###  <a name="executionInfo"></a> executionInfo

|Nome dell'elemento|Tipo|Note|
|------------------|----------|-----------|
|startTime|DateTime|ora di Hello in quale attività hello avviato. 'In esecuzione' corrisponde toohello **esecuzione** stato se l'attività hello specifica i file di risorse o pacchetti di applicazioni, ora di inizio hello riflette ora hello in hello avviato il download o distribuzione di tali attività.  Se l'attività hello è stato riavviato o ripetuta, si tratta di hello ora più recente in cui attività hello avviato.|
|endTime|DateTime|ora di Hello in quali attività hello è stata completata.|
|exitCode|Int32|codice di uscita Hello dell'attività hello.|
|retryCount|Int32|numero di volte in cui è stato ripetuto attività hello dal servizio Batch hello di Hello. attività di Hello viene ritentata se si conclude con un codice di uscita diverso da zero, configurare toohello MaxTaskRetryCount è definita.|
|requeueCount|Int32|Hello numero di volte in cui attività hello è stata riaccodata dal servizio di Batch hello come risultato di hello di una richiesta dell'utente.<br /><br /> Quando si rimuove utente hello nodi da un pool (per il ridimensionamento o la compattazione del pool di hello) o quando il processo di hello viene disabilitato, l'utente hello è possono specificare che le attività in esecuzione nei nodi hello reinserite nella coda per l'esecuzione. Questo conteggio tiene traccia di quante volte è stato reinserito nella coda di attività hello per questi motivi.|
