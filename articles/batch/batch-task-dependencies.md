---
title: "attività di aaaUse toorun di dipendenze in base hello completamento di altre attività - Azure Batch | Documenti Microsoft"
description: "Creare le attività che dipendono dal completamento hello di altre attività per l'elaborazione di stile MapReduce e i dati di grandi dimensioni simili carichi di lavoro nel Batch di Azure."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: b8d12db5-ca30-4c7d-993a-a05af9257210
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: faf08ec38cb30b1f66acd51e256c31aea6215c62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-task-dependencies-toorun-tasks-that-depend-on-other-tasks"></a>Creare relazioni tra attività attività toorun che dipendono da altre attività

È possibile definire attività dipendenze toorun un'attività o un set di attività solo dopo che un'attività padre è stata completata. Ecco alcuni degli scenari in cui le dipendenze delle attività sono utili:

* Stile MapReduce i carichi di lavoro nel cloud hello.
* Processi le cui attività di elaborazione dati può essere espressa come grafo aciclico diretto (DAG).
* Dopo il rendering e il pre-rendering di elabora, in cui ogni attività è necessario completare prima di poter iniziare l'attività successiva hello.
* Qualsiasi altro processo in cui attività downstream dipendono dall'output di hello delle attività a monte.

Con le relazioni tra attività Batch, è possibile creare attività pianificate per l'esecuzione in nodi di calcolo dopo il completamento di hello di uno o più attività padre. Ad esempio, è possibile creare un processo che esegue il rendering di ogni fotogramma di un film 3D con le attività parallele separate. attività finale Hello - hello "attività merge" - unioni hello fotogrammi sottoposti a rendering in film completo di hello solo dopo che tutti i frame è stato correttamente eseguito il rendering.

Per impostazione predefinita, le attività dipendenti pianificate per l'esecuzione solo dopo che l'attività padre hello è stata completata. È possibile specificare un dipendenza azione toooverride hello il comportamento predefinito ed eseguire attività quando l'attività padre hello ha esito negativo. Vedere hello [azioni dipendenza](#dependency-actions) sezione per informazioni dettagliate.  

È possibile creare attività che dipendono da altre attività in una relazione uno-a-uno o uno-a-molti. È inoltre possibile creare una dipendenza di intervallo in cui un'attività dipende dal completamento di hello di un gruppo di attività all'interno di un intervallo di ID attività specificato. È possibile combinare queste tre relazioni molti-a-molti toocreate di scenari di base.

## <a name="task-dependencies-with-batch-net"></a>Relazioni tra attività con Batch .NET
In questo articolo viene illustrato come dipendenze di attività tooconfigure utilizzando hello [.NET per Batch] [ net_msdn] libreria. Viene innanzitutto illustrata la modalità è troppo[abilitare la relazione tra attività](#enable-task-dependencies) nei processi e quindi illustra come troppo[configurare un'attività con le dipendenze](#create-dependent-tasks). È anche descrivere come toospecify un dipendenza azione toorun attività dipendente se padre hello ha esito negativo. Infine, approfondiremo hello [scenari dipendenza](#dependency-scenarios) che supporta Batch.

## <a name="enable-task-dependencies"></a>Abilitare le relazioni tra attività
dipendenze di attività toouse Batch nell'applicazione in uso, è necessario configurare le dipendenze di attività toouse di hello del processo. In .NET per Batch, abilitarlo nel [CloudJob] [ net_cloudjob] impostando il relativo [UsesTaskDependencies] [ net_usestaskdependencies] proprietà troppo`true`:

```csharp
CloudJob unboundJob = batchClient.JobOperations.CreateJob( "job001",
    new PoolInformation { PoolId = "pool001" });

// IMPORTANT: This is REQUIRED for using task dependencies.
unboundJob.UsesTaskDependencies = true;
```

Nel precedente frammento di codice di hello, "batchClient" è un'istanza di hello [BatchClient] [ net_batchclient] classe.

## <a name="create-dependent-tasks"></a>Creare attività dipendenti
toocreate un'attività che dipende dal completamento hello di uno o più attività padre, è possibile specificare l'attività "dipende" hello che hello altre attività. In .NET per Batch, configurare hello [CloudTask][net_cloudtask].[ DependsOn] [ net_dependson] proprietà con un'istanza di hello [TaskDependencies] [ net_taskdependencies] classe:

```csharp
// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
```

Questo frammento di codice crea un'attività dipendente con ID attività "Flowers". Hello "Fiori" attività dipende dalle attività "Ora" e "Sun". L'attività "Fiori" sarà toorun pianificato su un nodo di calcolo solo dopo l'attività "Ora" e "Sun" sono stati completati correttamente.

> [!NOTE]
> Un'attività viene considerata toobe completata correttamente quando è in hello **completato** stato e il relativo **codice di uscita** è `0`. In .NET per Batch, ciò significa un [CloudTask][net_cloudtask].[ Stato] [ net_taskstate] valore della proprietà `Completed` e hello del CloudTask [TaskExecutionInformation][net_taskexecutioninformation].[ Codice di uscita] [ net_exitcode] valore della proprietà è `0`.
> 
> 

## <a name="dependency-scenarios"></a>scenari delle relazione
In Azure Batch è possibile usare tre scenari di relazioni tra attività di base, ovvero uno-a-uno, uno-a-molti e la relazione tra intervalli di ID. Possono essere combinati tooprovide un quarto scenario, molti-a-molti.

| Scenario&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Esempio |  |
|:---:| --- | --- |
|  [Uno-a-uno](#one-to-one) |L'*attivitàB* dipende dall'*attivitàA* <p/> L'*attivitàB* sarà pianificata per l'esecuzione solo dopo il completamento corretto dell'*attivitàA* |![Diagramma: relazione uno-a-uno tra attività][1] |
|  [Uno-a-molti](#one-to-many) |L'*attivitàC* dipende sia dall'*attivitàA* che dall'*attivitàB*. <p/> L'*attivitàC* sarà pianificata per l'esecuzione solo dopo il completamento corretto dell'*attivitàA* e dell'*attivitàB* |![Diagramma: relazione uno-a-molti tra attività][2] |
|  [Intervallo di ID attività](#task-id-range) |L'*attivitàD* dipende da un intervallo di attività <p/> *taskD* non verrà pianificato per l'esecuzione fino a quando le attività con ID hello *1* tramite *10* sono stati completati correttamente |![Diagramma: relazione tra intervalli di ID attività][3] |

> [!TIP]
> È possibile creare **molti-a-molti** relazioni, ad esempio in cui attività C, D, E e F ogni dipende da attività A e B. Ciò è utile, ad esempio, negli scenari di pre-elaborazione parallelizzati in cui le attività downstream dipendono dall'output di hello di più attività upstream.
> 
> Negli esempi di hello in questa sezione, un'attività dipendente viene eseguito solo dopo che l'attività padre hello completata correttamente. Questo comportamento è hello predefinito per un'attività dipendente. Dopo che un'attività padre non riesce, specificando un comportamento predefinito di hello toooverride di azione di dipendenza, è possibile eseguire un'attività dipendente. Vedere hello [azioni dipendenza](#dependency-actions) sezione per informazioni dettagliate.

### <a name="one-to-one"></a>Uno-a-uno
In una relazione uno-a un'attività dipende dal completamento hello dell'attività padre. toocreate hello dipendenza, fornire un toohello ID singola attività [TaskDependencies][net_taskdependencies].[ OnId] [ net_onid] metodo statico quando si popola hello [DependsOn] [ net_dependson] proprietà di [CloudTask] [ net_cloudtask].

```csharp
// Task 'taskA' doesn't depend on any other tasks
new CloudTask("taskA", "cmd.exe /c echo taskA"),

// Task 'taskB' depends on completion of task 'taskA'
new CloudTask("taskB", "cmd.exe /c echo taskB")
{
    DependsOn = TaskDependencies.OnId("taskA")
},
```

### <a name="one-to-many"></a>Uno-a-molti
In una relazione uno-a-molti, un'attività dipende dal completamento di hello di più attività padre. toocreate hello dipendenza, offrono un insieme di attività ID toohello [TaskDependencies][net_taskdependencies].[ OnIds] [ net_onids] metodo statico quando si popola hello [DependsOn] [ net_dependson] proprietà di [CloudTask] [ net_cloudtask].

```csharp
// 'Rain' and 'Sun' don't depend on any other tasks
new CloudTask("Rain", "cmd.exe /c echo Rain"),
new CloudTask("Sun", "cmd.exe /c echo Sun"),

// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
``` 

### <a name="task-id-range"></a>Intervallo di ID attività
Una dipendenza su un intervallo di attività padre, un'attività dipende dal completamento di hello hello delle attività i cui ID sono situati all'interno di un intervallo.
dipendenza hello toocreate, fornire hello prima e ultima attività ID in hello intervallo toohello [TaskDependencies][net_taskdependencies].[ OnIdRange] [ net_onidrange] metodo statico quando si popola hello [DependsOn] [ net_dependson] proprietà di [CloudTask] [net_cloudtask].

> [!IMPORTANT]
> Quando si usano gli intervalli di ID attività per le dipendenze, hello ID attività nell'intervallo di hello *deve* da rappresentazioni di stringa di valori integer.
> 
> Ogni attività nell'intervallo di hello devono soddisfare dipendenza hello, completamento o completando con un errore che è mappata tooa dipendenza azione impostare troppo**Satisfies**. Vedere hello [azioni dipendenza](#dependency-actions) sezione per informazioni dettagliate.
>
>

```csharp
// Tasks 1, 2, and 3 don't depend on any other tasks. Because
// we will be using them for a task range dependency, we must
// specify string representations of integers as their ids.
new CloudTask("1", "cmd.exe /c echo 1"),
new CloudTask("2", "cmd.exe /c echo 2"),
new CloudTask("3", "cmd.exe /c echo 3"),

// Task 4 depends on a range of tasks, 1 through 3
new CloudTask("4", "cmd.exe /c echo 4")
{
    // toouse a range of tasks, their ids must be integer values.
    // Note that we pass integers as parameters tooTaskIdRange,
    // but their ids (above) are string representations of hello ids.
    DependsOn = TaskDependencies.OnIdRange(1, 3)
},
```

## <a name="dependency-actions"></a>Azioni di dipendenza

Per impostazione predefinita, un'attività o un set di attività dipendenti vengono eseguite solo dopo il corretto completamento di un'attività padre. In alcuni scenari, è consigliabile attività dipendenti toorun anche se l'attività padre hello ha esito negativo. È possibile eseguire l'override di comportamento predefinito di hello specificando un'azione di dipendenza. Un'azione di dipendenza specifica se un'attività dipendente è idoneo toorun, in base a hello riuscita o meno delle attività padre hello. 

Ad esempio, si supponga che un'attività dipendente è in attesa di dati dal completamento hello dell'attività upstream hello. Se attività upstream hello non riesce, l'attività dipendente hello potrebbe essere ancora in grado di toorun i dati obsoleti. In questo caso, un'azione di dipendenza è possibile specificare che tale attività dipendente hello è idoneo toorun nonostante l'errore hello dell'attività padre hello.

Un'azione di dipendenza si basa su una condizione di uscita per l'attività padre hello. È possibile specificare un'azione di dipendenza per una delle seguenti condizioni di uscita; hello per .NET, vedere hello [ExitConditions] [ net_exitconditions] classe per informazioni dettagliate:

- Quando si verifica un errore di pre-elaborazione.
- Quando si verifica un errore di caricamento dei file. Se l'attività hello viene terminata con un codice di uscita specificato tramite **exitCodes** o **exitCodeRanges**e quindi si verifica un errore di caricamento di file, l'azione hello specificata da hello uscita codice avrà la precedenza.
- Quando attività hello termina con un codice di uscita definito da hello **ExitCodes** proprietà.
- Quando attività hello termina con un codice di uscita che rientra in un intervallo specificato da hello **ExitCodeRanges** proprietà.
- Hello caso predefinito, se l'attività hello termina con un codice di uscita non è definito da **ExitCodes** o **ExitCodeRanges**, o se l'attività hello termina con un errore di pre-elaborazione e hello **PreProcessingError**  non è impostata, o se hello attività non riesce e genera un file di caricamento di errore e hello **FileUploadError** non è impostata. 

un'azione di dipendenza in .NET, hello set toospecify [ExitOptions][net_exitoptions].[ DependencyAction] [ net_dependencyaction] proprietà per la condizione di uscita hello. Hello **DependencyAction** proprietà prende uno dei due valori:

- Hello impostazione **DependencyAction** proprietà troppo**Satisfies** indica che le attività dipendenti sono idonei toorun se l'attività padre hello termina con un errore specificato.
- Hello impostazione **DependencyAction** proprietà troppo**blocco** indica che le attività dipendenti non sono idonee toorun.

impostazione predefinita per hello Hello **DependencyAction** proprietà **Satisfies** per il codice di uscita 0, e **blocco** per tutte le altre condizioni di uscita.

frammento di codice seguente Hello imposta hello **DependencyAction** proprietà per un'attività padre. Se l'attività padre hello termina con un errore di pre-elaborazione o con hello hello dipendenti codici di errore specificato, l'attività è bloccata. Se l'attività padre hello viene terminato con un altro errore diverso da zero, l'attività dipendente hello è toorun idonei.

```csharp
// Task A is hello parent task.
new CloudTask("A", "cmd.exe /c echo A")
{
    // Specify exit conditions for task A and their dependency actions.
    ExitConditions = new ExitConditions
    {
        // If task A exits with a pre-processing error, block any downstream tasks (in this example, task B).
        PreProcessingError = new ExitOptions
        {
            DependencyAction = DependencyAction.Block
        },
        // If task A exits with hello specified error codes, block any downstream tasks (in this example, task B).
        ExitCodes = new List<ExitCodeMapping>
        {
            new ExitCodeMapping(10, new ExitOptions() { DependencyAction = DependencyAction.Block }),
            new ExitCodeMapping(20, new ExitOptions() { DependencyAction = DependencyAction.Block })
        },
        // If task A succeeds or fails with any other error, any downstream tasks become eligible toorun 
        // (in this example, task B).
        Default = new ExitOptions
        {
            DependencyAction = DependencyAction.Satisfy
        }
    }
},
// Task B depends on task A. Whether it becomes eligible toorun depends on how task A exits.
new CloudTask("B", "cmd.exe /c echo B")
{
    DependsOn = TaskDependencies.OnId("A")
},
```

## <a name="code-sample"></a>Esempio di codice
Hello [TaskDependencies] [ github_taskdependencies] progetto di esempio è uno dei hello [esempi di codice di Azure Batch] [ github_samples] su GitHub. Questa soluzione di Visual Studio mostra:

- Come tooenable attività dipendenza su un processo
- Modalità toocreate attività da cui dipendono altre attività
- Modalità tooexecute quelli delle attività in un pool di nodi di calcolo.

## <a name="next-steps"></a>Passaggi successivi
### <a name="application-deployment"></a>Distribuzione dell'applicazione
Hello [pacchetti di applicazioni](batch-application-packages.md) funzionalità di Batch fornisce un modo semplice distribuire tooboth e la versione applicazioni hello le attività eseguite in nodi di calcolo.

### <a name="installing-applications-and-staging-data"></a>Installazione delle applicazioni e staging dei dati
Vedere [l'installazione di applicazioni e dati in Batch di gestione temporanea di nodi di calcolo] [ forum_post] nel forum di Azure Batch hello per una panoramica dei metodi per la preparazione dei nodi toorun attività. Scritti da uno dei membri del team hello Azure Batch, che questo post di è una buona panoramica sulle applicazioni di toocopy hello modi diversi, i dati di input attività e altri tooyour file nodi di calcolo.

[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[github_taskdependencies]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/TaskDependencies
[github_samples]: https://github.com/Azure/azure-batch-samples
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_dependson]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.dependson.aspx
[net_exitcode]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskexecutioninformation.exitcode.aspx
[net_exitconditions]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitconditions
[net_exitoptions]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitoptions
[net_dependencyaction]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitoptions#Microsoft_Azure_Batch_ExitOptions_DependencyAction
[net_msdn]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_onid]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onid.aspx
[net_onids]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onids.aspx
[net_onidrange]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onidrange.aspx
[net_taskexecutioninformation]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskexecutioninformation.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_usestaskdependencies]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.usestaskdependencies.aspx
[net_taskdependencies]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskdependencies.aspx

[1]: ./media/batch-task-dependency/01_one_to_one.png "Diagramma: relazione uno-a-uno"
[2]: ./media/batch-task-dependency/02_one_to_many.png "Diagramma: relazione uno-a-molti"
[3]: ./media/batch-task-dependency/03_task_id_range.png "Diagramma: relazione tra intervalli di ID attività"
