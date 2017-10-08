---
title: "lo stato di avanzamento di un processo contando le attività dallo stato - Azure Batch aaaMonitor | Documenti Microsoft"
description: "Monitorare lo stato di hello di un processo chiamando operazione Ottieni conteggio attività hello toocount attività per un processo. È possibile ottenere un conteggio delle attività attive, in esecuzione e completate e delle attività riuscite o non riuscite."
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: article
ms.date: 08/02/2017
ms.author: tamram
ms.openlocfilehash: 03957d8a3d678bf44587f3bc7f988a76885c2af0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="count-tasks-by-state-toomonitor-a-jobs-progress-preview"></a>Conteggio attività toomonitor stato avanzamento di un processo (anteprima)

Azure Batch offre un modo efficiente toomonitor hello lo stato di avanzamento di un processo durante l'esecuzione delle relative attività. È possibile chiamare hello [Ottieni conteggio attività] [ rest_get_task_counts] toofind operazione quante attività sono in uno stato attivo, in esecuzione o completato e quanti hanno esito positivo o negativo. Contando il numero di hello di attività in ogni stato, è più facilmente possibile visualizzare utente tooa di stato di avanzamento del processo di hello o rilevare ritardi imprevisti o errori che possono influire sul processo hello.

> [!IMPORTANT]
> Ciao operazione Ottieni conteggio attività è attualmente in anteprima e non è ancora disponibile in Azure per enti pubblici, Cina di Azure e Azure in Germania. 
>
>

## <a name="how-tasks-are-counted"></a>Come vengono conteggiate le attività

operazione Ottieni conteggio attività Hello conta le attività dallo stato, come indicato di seguito:

- Un'attività viene considerata **active** quando è in coda e in grado di toorun, ma non è attualmente assegnato tooa del nodo di calcolo. Un'attività viene conteggiata come **attiva** anche se dipende da un'attività padre non ancora completata. Per ulteriori informazioni sulle dipendenze delle attività, vedere [creare relazioni tra attività attività toorun che dipendono da altre attività](batch-task-dependencies.md). 
- Un'attività viene considerata **esecuzione** quando è stato assegnato il nodo di calcolo tooa, ma non è ancora stata completata. Un'attività viene considerata **esecuzione** quando lo stato è `preparing` o `running`, come indicato dal hello [ottenere informazioni su un'attività] [ rest_get_task] operazione.
- Un'attività viene considerata **completato** quando non è più idoneo toorun. Un'attività conteggiata come **completata** è stata in genere completata correttamente o non è riuscita e ha anche superato il limite di nuovi tentativi. 

Hello operazione Ottieni conteggio attività indica inoltre il numero di attività hanno esito positivo o negativo. Batch determina se un'attività è riuscita o meno controllando hello **risultato** proprietà di hello [executionInfo] [https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task#executionInfo] proprietà:

    - Un'attività viene considerata **ha avuto esito positivo** se hello risultato dell'esecuzione dell'attività è `success`.
    - Un'attività viene considerata **Impossibile** se hello risultato dell'esecuzione dell'attività è `failure`.

Per altre informazioni sugli stati delle attività, vedere [Get information about a task][rest_get_task] (Ottenere informazioni su un'attività).

Hello .NET esempio seguente viene illustrato come attività tooretrieve conta dallo stato: 

```csharp
var taskCounts = await batchClient.JobOperations.GetTaskCountsAsync("job-1");

Console.WriteLine("Task count in active state: {0}", taskCounts.Active);
Console.WriteLine("Task count in preparing or running state: {0}", taskCounts.Running);
Console.WriteLine("Task count in completed state: {0}", taskCounts.Completed);
Console.WriteLine("Succeeded task count: {0}", taskCounts.Succeeded);
Console.WriteLine("Failed task count: {0}", taskCounts.Failed);
Console.WriteLine("ValidationStatus: {0}", taskCounts.ValidationStatus);
```

> [!NOTE]
> È possibile utilizzare un modello simile per REST e altri linguaggi supportati tooget attività i conteggi per un processo. 
> 
> 

## <a name="consistency-checking-for-task-counts"></a>Verifica della coerenza per i conteggi delle attività

servizio Batch Hello aggrega i conteggi di attività per la raccolta dati da più parti di un sistema distribuito asincrono. tooensure attività conteggi sono corretti, Batch fornisce la convalida aggiuntiva per il conteggio di stato mediante l'esecuzione di verifiche di coerenza su più componenti di sistema hello. Batch esegue queste verifiche di coerenza, purché vi sono meno di 200.000 attività nel processo di hello. In hello improbabile che il controllo di coerenza hello rileva errori, Batch corregge risultato hello dell'operazione Ottieni conteggio attività hello in base ai risultati di hello di verifica di coerenza hello. Hello verifica di coerenza è un'ulteriore misura tooensure che i clienti che si basano su hello operazione Ottieni conteggio attività ottenere informazioni corrette di hello che necessarie per la soluzione.

Hello **validationStatus** proprietà in risposta hello indica se i Batch ha eseguito il controllo di coerenza hello. Se il Batch non è stato toocheck in grado di conteggi di stato con gli stati di hello effettivo mantenuti nel sistema hello, hello **validationStatus** impostata troppo`unvalidated`. Per motivi di prestazioni Batch non eseguirà hello verifica di coerenza se hello processo include più di 200.000 attività, pertanto hello **validationStatus** proprietà può essere impostata troppo`unvalidated` in questo caso. Tuttavia, hello attività conteggio non è necessariamente in questo caso, è altamente improbabile anche una perdita di dati molto limitato. 

Quando un'attività di modifica stato, pipeline di aggregazione hello elabora modifica hello entro pochi secondi. operazione Ottieni conteggio attività Hello riflette i conteggi delle attività hello aggiornato entro tale periodo. Tuttavia, se pipeline aggregazione hello mancati riscontri una modifica in uno stato di attività, quindi che modifica non è registrato fino al successivo passaggio di convalida hello. Durante questo periodo, i conteggi delle attività potrebbero essere leggermente imprecisi a causa di eventi non toohello, ma essi vengono corretti nel passaggio di convalida hello successivo.

## <a name="best-practices-for-counting-a-jobs-tasks"></a>Procedure consigliate per il conteggio della attività di un processo

La chiamata di operazione Ottieni conteggio attività hello è tooreturn modo più efficiente di hello un conteggio delle attività di un processo per stato di base. Se si utilizza una versione del servizio Batch 2017-06-01.5.1, si consiglia di scrittura o aggiornamento del codice toouse Ottieni conteggio attività.

in precedenza 2017-06-01.5.1 Hello operazione Ottieni conteggio attività non è disponibile nelle versioni del servizio Batch. Se si utilizza una versione precedente del servizio di hello, quindi utilizzare un'attività di toocount query di elenco in un processo. Per ulteriori informazioni, vedere [creare query in modo efficiente le risorse di Batch toolist](batch-efficient-list-queries.md).

## <a name="next-steps"></a>Passaggi successivi

* Vedere hello [Cenni preliminari sulle funzionalità di Batch](batch-api-basics.md) toolearn ulteriori informazioni sulle funzionalità e concetti relativi al servizio Batch. articolo Hello illustra risorse Batch primarie hello come pool, nodi di calcolo, i processi e attività e fornisce una panoramica delle funzionalità del servizio hello.
* Nozioni di base hello dello sviluppo di un'applicazione abilitata per Batch utilizzando hello [libreria client .NET per Batch](batch-dotnet-get-started.md) o [Python](batch-python-tutorial.md). Questi articoli introduttivi consentono di eseguire un'applicazione funzionante che utilizza hello Batch servizio tooexecute un carico di lavoro su più nodi di calcolo.


[rest_get_task_counts]: https://docs.microsoft.com/rest/api/batchservice/get-the-task-counts-for-a-job
[rest_get_task]: https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task
[rest_list_tasks]: https://docs.microsoft.com/rest/api/batchservice/list-the-tasks-associated-with-a-job
