---
title: "aaaCreate attività tooprepare processi e completa sui nodi di calcolo - Azure Batch | Documenti Microsoft"
description: "Dati di utilizzo a livello di processo di preparazione attività toominimize trasferire tooAzure nodi di calcolo di Batch e rilasciare l'attività per la pulizia del nodo al completamento del processo."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 63d9d4f1-8521-4bbb-b95a-c4cad73692d3
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fd5fb47ae6700281e63048c49a1241f4e935baba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-job-preparation-and-job-release-tasks-on-batch-compute-nodes"></a>Eseguire attività di preparazione e rilascio del processo in nodi di calcolo di Batch

 Un processo di Azure Batch richiede spesso alcune operazioni di configurazione prima dell'esecuzione delle attività e di manutenzione post-processo dopo il completamento delle attività. È possibile necessario toodownload comuni attività dati di input tooyour calcolo nodi o caricare attività output dati tooAzure archiviazione dopo completamento del processo di hello. È possibile utilizzare **processo preparazione** e **processo versione** attività tooperform queste operazioni.

## <a name="what-are-job-preparation-and-release-tasks"></a>Quali sono le attività di preparazione e rilascio dei processi
Prima di eseguire attività di un processo, l'attività di preparazione processo hello viene eseguito su tutti toorun di pianificata di nodi di calcolo almeno un'attività. Una volta completato il processo di hello, attività di rilascio di hello processo viene eseguito su ogni nodo nel pool di hello eseguita almeno un'attività. Come con le normale attività di Batch, è possibile specificare toobe una riga di comando viene richiamato ogni volta una preparazione del processo o attività di rilascio viene eseguito.

Le attività di preparazione e rilascio del processo offrono funzionalità familiari per le attività di Batch, quali download di file ([file di risorse][net_job_prep_resourcefiles]), esecuzione con privilegi elevati, variabili di ambiente personalizzate, durata massima di esecuzione, numero di tentativi e periodo di conservazione dei file.

Nella seguenti sezioni di hello, si apprenderà come hello toouse [JobPreparationTask] [ net_job_prep] e [JobReleaseTask] [ net_job_release] classi contenute nello hello [.NET per batch] [ api_net] libreria.

> [!TIP]
> Le attività di preparazione e rilascio del processo sono particolarmente utili in ambienti con "pool condivisi", in cui un pool di nodi di calcolo viene mantenuto durante l'esecuzione di un processo e viene usato da più processi.
> 
> 

## <a name="when-toouse-job-preparation-and-release-tasks"></a>Quando toouse preparazione del processo e rilasciare l'attività
Preparazione del processo e le attività di rilascio di processo sono ideali per hello seguenti situazioni:

**Download dei dati delle attività comuni**

I processi batch richiedono spesso un set comune di dati come input per l'attività del processo di hello. Ad esempio, nei calcoli di analisi dei rischi giornaliera, dati di mercato sono specifici ancora comuni attività tooall hello processo. Questi dati di mercato, dimensioni, spesso diversi gigabyte devono essere solo una volta scaricato tooeach del nodo di calcolo in modo che qualsiasi attività che viene eseguita nel nodo hello possibile utilizzarlo. Utilizzare un **attività di preparazione del processo** toodownload questo nodo tooeach dati prima che esecuzione hello del processo di hello altre attività.

**Eliminazione dell'output di processi e attività**

In un ambiente "shared pool", in cui i nodi di calcolo di un pool non sono rimossi tra processi, potrebbe essere dati del processo toodelete tra le esecuzioni. Potrebbe essere necessario tooconserve spazio sui nodi hello, o che soddisfano i criteri di sicurezza dell'organizzazione. Utilizzare un **versione mansione** toodelete dati che è stati scaricati da un'attività di preparazione del processo o generati durante l'esecuzione dell'attività.

**Conservazione dei log**

È possibile tookeep una copia del file di log che generano le attività, o forse i file di dump di arresto anomalo del sistema possono essere generati da errori nelle applicazioni. Utilizzare un **versione mansione** in tali casi di toocompress e caricare questo tooan dati [di archiviazione di Azure] [ azure_storage] account.

> [!TIP]
> Un altro modo toopersist log, l'attività e altri processi di output dei dati sono hello toouse [convenzioni File Batch di Azure](batch-task-output.md) libreria.
> 
> 

## <a name="job-preparation-task"></a>attività di preparazione del processo
Prima dell'esecuzione di attività di un processo, Batch esegue l'attività di preparazione processo hello in ogni nodo di calcolo è toorun pianificata un'attività. Per impostazione predefinita, il servizio Batch hello attende hello processo preparazione attività toobe completato prima di eseguire hello attività pianificate tooexecute nel nodo hello. Tuttavia, è possibile configurare il servizio di hello non toowait. Se si riavvia il nodo di hello, viene eseguito di nuovo l'attività di preparazione processo hello, ma è anche possibile disabilitare questo comportamento.

l'attività di preparazione processo Hello viene eseguita solo per i nodi che vengono pianificati toorun un'attività. Ciò impedisce l'esecuzione non necessari di hello di un'attività di preparazione nel caso in cui un nodo non viene assegnata un'attività. Ciò può verificarsi quando il numero di hello di attività per un processo è minore di numero hello di nodi in un pool. Si applica anche quando [esecuzione di attività simultanee](batch-parallel-node-tasks.md) è abilitato, che lascia alcuni nodi inattiva se il numero di attività hello è inferiore a hello totale possibili le attività simultanee. Da non in esecuzione l'attività di preparazione processo hello nei nodi di inattività, è possibile spesa sugli addebiti di trasferimento dati.

> [!NOTE]
> [JobPreparationTask] [ net_job_prep_cloudjob] è diverso da [CloudPool.StartTask] [ pool_starttask] in JobPreparationTask viene eseguita all'avvio di hello di ogni processo, mentre StartTask viene eseguita solo quando un nodo di calcolo prima viene aggiunto a un pool o riavvio.
> 
> 

## <a name="job-release-task"></a>attività di rilascio del processo
Quando un processo è stato contrassegnato come completato, attività di rilascio di hello processo viene eseguito su ogni nodo nel pool di hello eseguita almeno un'attività. Un processo viene contrassegnato come completato generando una richiesta di interruzione. Hello servizio Batch, quindi imposta hello lo stato del processo troppo*terminazione*, interrompe tutte le attività attive o in esecuzione associate al processo hello ed esegue attività di rilascio processo hello. il processo di Hello passa quindi toohello *completato* stato.

> [!NOTE]
> L'eliminazione di processo anche l'esecuzione di attività di rilascio processo hello. Tuttavia, se un processo è già stato terminato, attività di rilascio hello non viene eseguito una seconda volta se il processo di hello viene eliminato in un secondo momento.
> 
> 

## <a name="job-prep-and-release-tasks-with-batch-net"></a>Attività di preparazione e di rilascio del processo con Batch .NET
toouse un'attività di preparazione del processo, assegnare un [JobPreparationTask] [ net_job_prep] processo tooyour oggetti [CloudJob.JobPreparationTask] [ net_job_prep_cloudjob] proprietà . Analogamente, inizializzare un [JobReleaseTask] [ net_job_release] e assegnarlo del processo tooyour [CloudJob.JobReleaseTask] [ net_job_prep_cloudjob] hello tooset proprietà attività di rilascio del processo.

In questo frammento di codice, `myBatchClient` è un'istanza di [BatchClient][net_batch_client], e `myPool` è un pool esistente all'interno di hello account Batch.

```csharp
// Create hello CloudJob for CloudPool "myPool"
CloudJob myJob =
    myBatchClient.JobOperations.CreateJob(
        "JobPrepReleaseSampleJob",
        new PoolInformation() { PoolId = "myPool" });

// Specify hello command lines for hello job preparation and release tasks
string jobPrepCmdLine =
    "cmd /c echo %AZ_BATCH_NODE_ID% > %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";
string jobReleaseCmdLine =
    "cmd /c del %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";

// Assign hello job preparation task toohello job
myJob.JobPreparationTask =
    new JobPreparationTask { CommandLine = jobPrepCmdLine };

// Assign hello job release task toohello job
myJob.JobReleaseTask =
    new JobPreparationTask { CommandLine = jobReleaseCmdLine };

await myJob.CommitAsync();
```

Come accennato in precedenza, attività di rilascio hello viene eseguito quando un processo viene terminato o eliminato. Terminare un processo con [JobOperations.TerminateJobAsync][net_job_terminate]. Eliminare un processo con [JobOperations.DeleteJobAsync][net_job_delete]. In genere si termina o si elimina un processo quando le attività vengono completate o quando si raggiunge un timeout definito dall'utente.

```csharp
// Terminate hello job toomark it as Completed; this will initiate the
// Job Release Task on any node that executed job tasks. Note that the
// Job Release Task is also executed when a job is deleted, thus you
// need not call Terminate if you typically delete jobs after task completion.
await myBatchClient.JobOperations.TerminateJobAsy("JobPrepReleaseSampleJob");
```

## <a name="code-sample-on-github"></a>Esempio di codice in GitHub
attività toosee processo di preparazione e rilascio in azione, estrarre hello [JobPrepRelease] [ job_prep_release_sample] progetto di esempio su GitHub. Questa applicazione console hello seguenti:

1. Crea un pool con due nodi "small".
2. Crea un processo con attività di preparazione e rilascio di processi e attività standard.
3. Esecuzioni hello attività di preparazione processo, che scrive i file di testo tooa ID nodo hello innanzitutto nella directory "condiviso" un nodo.
4. Esegue un'attività in ogni nodo che scrive il toohello ID attività file di testo stesso.
5. Una volta che vengono completate tutte le attività (o viene raggiunto il timeout di hello), stampa il contenuto di hello della console toohello file testo di ciascun nodo.
6. Al termine dell'esecuzione processo hello, per eseguire hello processo versione attività toodelete hello file dal nodo hello.
7. Hello stampe codici di preparazione del processo hello di uscita e rilasciare le attività per ogni nodo in cui è stato eseguito.
8. Mette in pausa esecuzione tooallow conferma dell'eliminazione di processo e/o pool.

Output di applicazione di esempio hello è simile toohello seguenti:

```
Attempting toocreate pool: JobPrepReleaseSamplePool
Created pool JobPrepReleaseSamplePool with 2 small nodes
Checking for existing job JobPrepReleaseSampleJob...
Job JobPrepReleaseSampleJob not found, creating...
Submitting tasks and awaiting completion...
All tasks completed.

Contents of shared\job_prep_and_release.txt on tvm-2434664350_1-20160623t173951z:
-------------------------------------------
tvm-2434664350_1-20160623t173951z tasks:
  task001
  task004
  task005
  task006

Contents of shared\job_prep_and_release.txt on tvm-2434664350_2-20160623t173951z:
-------------------------------------------
tvm-2434664350_2-20160623t173951z tasks:
  task008
  task002
  task003
  task007

Waiting for job JobPrepReleaseSampleJob tooreach state Completed
...

tvm-2434664350_1-20160623t173951z:
  Prep task exit code:    0
  Release task exit code: 0

tvm-2434664350_2-20160623t173951z:
  Prep task exit code:    0
  Release task exit code: 0

Delete job? [yes] no
yes
Delete pool? [yes] no
yes

Sample complete, hit ENTER tooexit...
```

> [!NOTE]
> A causa di toohello variabile creazione e ora di inizio nodi in un nuovo pool (alcuni nodi sono pronti per l'attività prima degli altri), verrà visualizzato un output diverso. In particolare, in quanto attività hello completato rapidamente, uno dei nodi del pool di hello può eseguire tutte le attività del processo di hello. In questo caso, si noterà che hello preparazione del processo e rilasciare l'attività non esistono per il nodo hello non eseguita alcuna attività.
> 
> 

### <a name="inspect-job-preparation-and-release-tasks-in-hello-azure-portal"></a>Controllare l'attività di rilascio nel portale di Azure hello e preparazione del processo
Quando si esegue l'applicazione di esempio hello, è possibile utilizzare hello [portale di Azure] [ portal] tooview hello proprietà del processo di hello e le relative attività, o anche scaricare i file di testo condivisa hello modificata dall'attività del processo di hello.

schermata di Hello riportata di seguito viene illustrato hello **Pannello attività di preparazione** nel portale di Azure dopo l'esecuzione dell'applicazione di esempio hello hello. Passare toohello *JobPrepReleaseSampleJob* proprietà dopo aver completato le attività, ma prima di eliminare il processo e il pool, fare clic su **attività di preparazione** o **leattivitàdirilascio** tooview le relative proprietà.

![Proprietà di preparazione del processo nel portale di Azure][1]

## <a name="next-steps"></a>Passaggi successivi
### <a name="application-packages"></a>Pacchetti dell'applicazione
Nell'attività di preparazione processo toohello aggiunta, è inoltre possibile utilizzare hello [pacchetti di applicazioni](batch-application-packages.md) funzionalità di Batch tooprepare nodi per l'esecuzione dell'attività di calcolo. Questa funzionalità è particolarmente utile per la distribuzione di applicazioni che non richiedono l'esecuzione di un programma di installazione, applicazioni che contengono molti file (100+) o applicazioni che richiedono un controllo delle versioni rigoroso.

### <a name="installing-applications-and-staging-data"></a>Installazione delle applicazioni e staging dei dati
Questo post del forum MSDN offre una panoramica di diversi metodi di preparazione dei nodi per l'esecuzione di attività:

[Installing applications and staging data on Batch compute nodes][forum_post] (Installazione delle applicazioni e staging dei dati nei nodi di calcolo di Batch)

Scritti da uno dei membri del team di Azure Batch hello, vengono illustrate diverse tecniche che è possibile utilizzare i nodi di toocompute toodeploy applicazioni e dati.

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_listjobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[azure_storage]: https://azure.microsoft.com/services/storage/
[portal]: https://portal.azure.com
[job_prep_release_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/JobPrepRelease
[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[net_batch_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]:https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_prep]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.aspx
[net_job_prep_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_job_prep_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.resourcefiles.aspx
[net_job_delete]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.deletejobasync.aspx
[net_job_terminate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_job_release]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobreleasetask.aspx
[net_job_release_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx

[net_list_certs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.listcertificates.aspx
[net_list_compute_nodes]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listcomputenodes.aspx
[net_list_job_schedules]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobschedules.aspx
[net_list_jobprep_status]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobpreparationandreleasetaskstatus.aspx
[net_list_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[net_list_nodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listnodefiles.aspx
[net_list_pools]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listpools.aspx
[net_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobs.aspx
[net_list_task_files]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[net_list_tasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listtasks.aspx

[1]: ./media/batch-job-prep-release/portal-jobprep-01.png
