---
title: "multi-istanza aaaUse attività applicazioni MPI toorun - Azure Batch | Documenti Microsoft"
description: "Informazioni su come le applicazioni di interfaccia MPI (Message Passing) tooexecute utilizzando hello multi-istanza attività digitano in Batch di Azure."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 83e34bd7-a027-4b1b-8314-759384719327
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: 5/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b0e3295a6aeb76267c26d5504bcff59de3dc5e22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-multi-instance-tasks-toorun-message-passing-interface-mpi-applications-in-batch"></a>Utilizzare le applicazioni multi-istanza attività toorun interfaccia MPI (Message Passing) in Batch

Attività di multi-istanza consentono toorun un'attività di Azure Batch in più nodi di calcolo contemporaneamente. e di abilitare scenari high performance computing, ad esempio le applicazioni MPI (Message Passing Interface) in Batch. In questo articolo viene illustrato come attività di multi-istanza tooexecute utilizzando hello [.NET per Batch] [ api_net] libreria.

> [!NOTE]
> Mentre hello esempi in questo articolo illustrano .NET per Batch, MS-MPI, nodi di calcolo di Windows, concetti di attività di multi-istanza hello descritti di seguito sono applicabili tooother piattaforme e tecnologie (Python e Intel MPI in nodi di Linux, ad esempio).
>
>

## <a name="multi-instance-task-overview"></a>Panoramica sulle attività a istanze multiple
Nel Batch, ogni attività sono in genere eseguita in un singolo nodo di calcolo, si invia più attività tooa processo e hello servizio Batch Pianifica ogni attività per l'esecuzione in un nodo. Tuttavia, tramite la configurazione di un'attività **le impostazioni di multi-istanza**, richiedere a Batch tooinstead creare un'attività principale e diverse sottoattività che vengono quindi eseguite su più nodi.

![Panoramica sulle attività a istanze multiple][1]

Quando si invia un'attività con il processo di multi-istanza impostazioni tooa, Batch vengono eseguite diverse attività toomulti-istanza univoca di passaggi:

1. Hello servizio Batch crea uno **primario** e diversi **sottoattività** in base alle impostazioni di multi-istanza hello. numero totale di Hello di attività (primaria e tutte le sottoattività) corrisponde a svariati hello **istanze** (nodi di calcolo) specificato nelle impostazioni di multi-istanza hello.
2. Batch consente di definire uno dei hello nodi di calcolo come hello **master**, e le pianificazioni hello tooexecute attività principale sul master hello. Consente di pianificare hello sottoattività tooexecute nel resto di hello dell'attività multi-istanza toohello allocato di nodi di calcolo di hello, uno sottoattività per ogni nodo.
3. scaricare Hello primaria e tutte le attività **file di risorse comuni** specificati nelle impostazioni di multi-istanza hello.
4. Dopo aver scaricato il file di risorse comuni hello, hello primaria e le sottoattività eseguire hello **comando coordinamento** specificati nelle impostazioni di multi-istanza hello. comando di coordinamento Hello è nodi tooprepare in genere utilizzate per l'esecuzione di attività hello. Può trattarsi di avvio di servizi in background (ad esempio [Microsoft MPI][msmpi_msdn]del `smpd.exe`) e verificare che i nodi di hello siano pronti tooprocess i messaggi tra i nodi.
5. attività principale Hello esegue hello **comando applicazione** sul nodo principale hello *dopo* comando coordinamento hello è stata completata correttamente hello primaria e tutte le sottoattività. comando applicazione Hello è hello riga di comando hello multi-istanza attività stessa e viene eseguito solo da attività principale hello. In una soluzione basata su [MS-MPI][msmpi_msdn], qui viene eseguita l'applicazione abilitata per MPI tramite `mpiexec.exe`.

> [!NOTE]
> Se è funzionalmente distinto, hello "attività di multi-istanza" non è un tipo di attività univoco come hello [StartTask] [ net_starttask] o [JobPreparationTask] [ net_jobprep]. attività di multi-istanza Hello è semplicemente un'attività di Batch standard ([CloudTask] [ net_task] in .NET per Batch) sono state configurate le cui impostazioni di multi-istanza. In questo articolo verrà fatto riferimento toothis come hello **attività multi-istanza**.
>
>

## <a name="requirements-for-multi-instance-tasks"></a>Requisiti delle attività a istanze multiple
Per le attività a istanze multiple è necessario un pool in cui sia **abilitata la comunicazione tra i nodi** e **disabilitata l'esecuzione di attività simultanee**. esecuzione di attività simultanee toodisable, hello set [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) too1 di proprietà.

Questo frammento di codice viene illustrato come le attività utilizzando una libreria .NET di Batch di hello toocreate un pool per multi-istanza.

```csharp
CloudPool myCloudPool =
    myBatchClient.PoolOperations.CreatePool(
        poolId: "MultiInstanceSamplePool",
        targetDedicatedComputeNodes: 3
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Multi-instance tasks require inter-node communication, and those nodes
// must run only one task at a time.
myCloudPool.InterComputeNodeCommunicationEnabled = true;
myCloudPool.MaxTasksPerComputeNode = 1;
```

> [!NOTE]
> Se si tenta di toorun disabilitata un'attività a più istanze in un pool con le comunicazioni, o con un *maxTasksPerNode* valore maggiore di 1, l'attività hello non è pianificata come mai - all'infinito rimane nello stato "attivo" hello. 
>
> Le attività a istanze multiple possono essere eseguite solo in nodi di pool creati dopo il 14 dicembre 2015.
>
>

### <a name="use-a-starttask-tooinstall-mpi"></a>Utilizzare un tooinstall StartTask MPI
toorun di applicazioni MPI con un'attività a più istanze, è necessario innanzitutto tooinstall un'implementazione MPI (MS-MPI o MPI Intel, ad esempio) sui nodi di calcolo hello nel pool di hello. Si tratta di un toouse tempestivamente un [StartTask][net_starttask], che viene eseguito ogni volta che un nodo viene aggiunto un pool o viene riavviato. Questo frammento di codice crea un StartTask che specifica il pacchetto di installazione hello MS-MPI come un [file di risorse][net_resourcefile]. riga di comando dell'attività di avvio Hello viene eseguita dopo che il file di risorse di hello è scaricato toohello nodo. In questo caso, la riga di comando hello esegue un'installazione automatica di MS-MPI.

```csharp
// Create a StartTask for hello pool which we use for installing MS-MPI on
// hello nodes as they join hello pool (or when they are restarted).
StartTask startTask = new StartTask
{
    CommandLine = "cmd /c MSMpiSetup.exe -unattend -force",
    ResourceFiles = new List<ResourceFile> { new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MSMpiSetup.exe", "MSMpiSetup.exe") },
    UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin)),
    WaitForSuccess = true
};
myCloudPool.StartTask = startTask;

// Commit hello fully configured pool toohello Batch service tooactually create
// hello pool and its compute nodes.
await myCloudPool.CommitAsync();
```

### <a name="remote-direct-memory-access-rdma"></a>Accesso diretto a memoria remota (RDMA)
Quando si sceglie un [dimensioni che supportano RDMA](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) , ad esempio A9 per hello nodi di calcolo nel pool di Batch, l'applicazione MPI può usufruire di prestazioni elevate, bassa latenza diretto a memoria remota (RDMA) di accesso di rete di Azure.

Cercare le dimensioni di hello specificate come "Che supporta RDMA" in hello seguenti articoli:

* Pool **CloudServiceConfiguration**

  * [Dimensioni dei servizi cloud](../cloud-services/cloud-services-sizes-specs.md) (solo Windows)
* Pool **VirtualMachineConfiguration**

  * [Dimensioni delle macchine virtuali in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)
  * [Dimensioni delle macchine virtuali in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)

> [!NOTE]
> vantaggio tootake RDMA in [nodi di calcolo Linux](batch-linux-nodes.md), è necessario utilizzare **Intel MPI** nei nodi hello. Per ulteriori informazioni sui pool CloudServiceConfiguration e VirtualMachineConfiguration, vedere la sezione Pool di hello hello [Cenni preliminari sulle funzionalità di Batch](batch-api-basics.md).
>
>

## <a name="create-a-multi-instance-task-with-batch-net"></a>Creare un'attività a istanze multiple con Batch .NET
Ora che abbiamo trattato requisiti pool hello e installazione del pacchetto MPI, creare attività di multi-istanza hello. In questo frammento di codice viene creato un oggetto [CloudTask][net_task] standard e viene quindi configurata la relativa proprietà [MultiInstanceSettings][net_multiinstance_prop]. Come accennato in precedenza, hello multi-istanza attività non è un tipo di attività distinto, ma un'attività Batch standard configurato con le impostazioni di multi-istanza.

```csharp
// Create hello multi-instance task. Its command line is hello "application command"
// and will be executed *only* by hello primary, and only after hello primary and
// subtasks execute hello CoordinationCommandLine.
CloudTask myMultiInstanceTask = new CloudTask(id: "mymultiinstancetask",
    commandline: "cmd /c mpiexec.exe -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe");

// Configure hello task's MultiInstanceSettings. hello CoordinationCommandLine will be executed by
// hello primary and all subtasks.
myMultiInstanceTask.MultiInstanceSettings =
    new MultiInstanceSettings(numberOfNodes) {
    CoordinationCommandLine = @"cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d",
    CommonResourceFiles = new List<ResourceFile> {
    new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MyMPIApplication.exe",
                     "MyMPIApplication.exe")
    }
};

// Submit hello task toohello job. Batch will take care of splitting it into subtasks and
// scheduling them for execution on hello nodes.
await myBatchClient.JobOperations.AddTaskAsync("mybatchjob", myMultiInstanceTask);
```

## <a name="primary-task-and-subtasks"></a>Attività primaria e sottoattività
Quando si crea hello le impostazioni di multi-istanza per un'attività, viene specificato il numero di hello dei nodi di calcolo che sono attività hello tooexecute. Quando si inviano processi di tooa attività hello, hello servizio Batch crea uno **primario** attività e sufficiente **sottoattività** che insieme corrispondente hello al numero di nodi specificato.

Queste attività vengono assegnate un id di tipo integer nell'intervallo di hello 0 troppo*numberOfInstances* - 1. Hello attività con id 0 è hello primario e tutti gli altri ID sono sottoattività. Ad esempio, se si crea hello seguendo le impostazioni di multi-istanza per un'attività, attività principale hello avrebbe un id pari a 0 e hello sottoattività avrebbe ID 1 a 9.

```csharp
int numberOfNodes = 10;
myMultiInstanceTask.MultiInstanceSettings = new MultiInstanceSettings(numberOfNodes);
```

### <a name="master-node"></a>Nodo master
Quando si invia un'attività a più istanze, hello servizio Batch ne definisce uno di hello nodi di calcolo come nodo "master" hello e pianificazioni hello tooexecute attività principale nel nodo principale hello. Hello sottoattività sono pianificati tooexecute nel resto di hello dei nodi di hello allocata toohello attività di multi-istanza.

## <a name="coordination-command"></a>comando di coordinamento
Hello **comando coordinamento** viene eseguito sia hello primaria e le sottoattività.

chiamata di Hello del comando di coordinamento hello sta bloccando - Batch non viene eseguito il comando dell'applicazione hello fino a quando il comando di coordinamento hello ha restituito correttamente per tutte le sottoattività. comando coordinamento Hello deve pertanto avviare tutti i servizi in background necessarie, verificare che siano pronti per l'utilizzo e uscire. Questo comando di coordinamento per una soluzione utilizzando la versione 7 MS-MPI, ad esempio, avvia il servizio SMPD hello nel nodo di hello, quindi viene chiuso:

```
cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d
```

Si noti hello utilizzo di `start` in questo comando di coordinamento. Questa operazione è necessaria perché hello `smpd.exe` applicazione non viene restituito immediatamente dopo l'esecuzione. Senza usare hello hello [avviare] [ cmd_start] dei comandi, non verrà restituito da questo comando di coordinamento e pertanto bloccano hello applicazione esecuzione comando.

## <a name="application-command"></a>Comando applicazione
Una volta attività principale hello e tutte le attività terminata l'esecuzione di comandi di coordinamento hello, riga di comando dell'attività di hello multi-istanza viene eseguita dall'attività primaria hello *solo*. Viene chiamato questo hello **comando applicazione** toodistinguish dal comando di coordinamento hello.

Per le applicazioni di MS-MPI, utilizzare hello tooexecute comando applicazione dell'applicazione abilitata MPI con `mpiexec.exe`. Di seguito è riportato, a titolo di esempio, il comando applicazione per una soluzione con MS-MPI versione 7:

```
cmd /c ""%MSMPI_BIN%\mpiexec.exe"" -c 1 -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe
```

> [!NOTE]
> Poiché MS-MPI `mpiexec.exe` utilizza hello `CCP_NODES` variabile per impostazione predefinita (vedere [le variabili di ambiente](#environment-variables)) esempio hello esclusa applicazione riga di comando riportata in precedenza.
>
>

## <a name="environment-variables"></a>Variabili di ambiente
Crea più batch [le variabili di ambiente] [ msdn_env_var] attività istanza toomulti specifica hello nodi allocata tooa attività di più istanze di calcolo. Le righe di comando di coordinamento e l'applicazione può fare riferimento a queste variabili di ambiente, possono hello script e programmi che vengono eseguiti.

Hello seguenti variabili di ambiente vengono create dal servizio Batch hello per l'utilizzo dalle attività di multi-istanza:

* `CCP_NODES`
* `AZ_BATCH_NODE_LIST`
* `AZ_BATCH_HOST_LIST`
* `AZ_BATCH_MASTER_NODE`
* `AZ_BATCH_TASK_SHARED_DIR`
* `AZ_BATCH_IS_CURRENT_NODE_MASTER`

Per i dettagli completi su questi e hello altri Batch calcolo nodo variabili di ambiente, inclusi i contenuti e la visibilità, vedere [le variabili di ambiente nodo di calcolo][msdn_env_var].

> [!TIP]
> Nell'esempio di codice Hello MPI Linux Batch contiene un esempio di come è possibile usare alcune di queste variabili di ambiente. Hello [coordinamento cmd] [ coord_cmd_example] Bash script Scarica i file di input e di applicazione comune da archiviazione di Azure, consente a una condivisione di File System NFS (Network) nel nodo principale hello e configura hello altri nodi allocato attività multi-istanza toohello come i client NFS.
>
>

## <a name="resource-files"></a>File di risorse
Esistono due set di tooconsider i file di risorse per le attività di multi-istanza: **file di risorse comuni** che *tutti* attività scaricare (principali e sottoattività), hello e **ifiledirisorse** specificato per hello multi-istanza dell'attività stessa, che *solo hello primario* attività di download.

È possibile specificare uno o più **file di risorse comuni** nelle impostazioni di multi-istanza hello per un'attività. Questi file di risorse comuni vengono scaricati da [di archiviazione di Azure](../storage/common/storage-introduction.md) in ogni nodo **directory condivisa attività** hello primaria e tutte le sottoattività. È possibile accedere directory condivisa di hello attività dalle righe di comando dell'applicazione e coordinamento tramite hello `AZ_BATCH_TASK_SHARED_DIR` variabile di ambiente. Hello `AZ_BATCH_TASK_SHARED_DIR` percorso è identico in ogni attività di multi-istanza nodo toohello allocato, pertanto è possibile condividere un comando singolo coordinamento tra hello primaria e tutte le attività. Batch "condividono" hello directory in senso di accesso remoto, ma è possibile utilizzarlo come un montaggio o punto come indicato in precedenza in suggerimento hello sulle variabili di ambiente di condivisione.

File di risorse che specificano per hello attività multi-istanza stessa directory di lavoro dell'attività toohello scaricato, `AZ_BATCH_TASK_WORKING_DIR`, per impostazione predefinita. Come accennato, invece toocommon file di risorse, unica attività primaria hello Scarica i file di risorse specificati per l'attività di hello multi-istanza stessa.

> [!IMPORTANT]
> Utilizzare sempre le variabili di ambiente hello `AZ_BATCH_TASK_SHARED_DIR` e `AZ_BATCH_TASK_WORKING_DIR` directory toothese toorefer le righe di comando. Non tentare percorsi hello tooconstruct manualmente.
>
>

## <a name="task-lifetime"></a>Durata dell'attività
durata Hello di hello attività principale controlli hello intera durata di hello multi-istanza intera attività. Quando si chiude hello primario, vengono terminate tutte hello sottoattività. codice di uscita Hello di hello primario è il codice di uscita hello dell'attività hello, pertanto riuscita di hello toodetermine utilizzato o meno delle attività hello per scopi di tentativi.

Se una delle sottoattività hello hanno esito negativo, chiusura con codice restituito diverso da zero, ad esempio, hello multi-istanza intera attività ha esito negativo. attività di multi-istanza Hello viene quindi terminata e ritentata, backup tooits limite di tentativi.

Quando si elimina un'attività a più istanze, hello primaria e tutte le attività vengono eliminate anche dal servizio Batch hello. Tutti sottoattività directory e i relativi file vengono eliminati dai nodi di calcolo hello, come per un'attività standard.

[TaskConstraints] [ net_taskconstraints] per un'attività di multi-istanza, ad esempio hello [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime] [ net_taskconstraint_maxwallclock], e [RetentionTime] [ net_taskconstraint_retention] vengono rispettate le proprietà, in quanto sono per un'attività standard e applicare toohello primario e tutte le sottoattività. Tuttavia, se si modifica hello [RetentionTime] [ net_taskconstraint_retention] proprietà dopo l'aggiunta di hello multi-istanza attività toohello processo, questa modifica è l'attività principale toohello solo applicato. Tutte le sottoattività hello continuare toouse hello originale [RetentionTime][net_taskconstraint_retention].

Elenco attività recenti del nodo di calcolo riflette id hello di una sottoattività se attività recente hello faceva parte di un'attività di multi-istanza.

## <a name="obtain-information-about-subtasks"></a>Ottenere informazioni sulle sottoattività
informazioni tooobtain su sottoattività tramite la libreria .NET di Batch di hello, chiamata hello [CloudTask.ListSubtasks] [ net_task_listsubtasks] metodo. Questo metodo restituisce informazioni su tutte le attività e informazioni su hello calcolo nodo hello attività eseguite. Tali informazioni, è possibile determinare directory radice del ciascuna sottoattività id del pool di hello, lo stato corrente, codice di uscita e più. È possibile utilizzare queste informazioni in combinazione con hello [PoolOperations.GetNodeFile] [ poolops_getnodefile] i file della sottoattività di metodo tooobtain hello. Si noti che questo metodo non restituisce informazioni per l'attività principale hello (id 0).

> [!NOTE]
> Se non diversamente specificato, i metodi .NET per Batch che operano su hello multi-istanza [CloudTask] [ net_task] stesso applicare *solo* toohello di attività principale. Ad esempio, quando si chiama hello [CloudTask.ListNodeFiles] [ net_task_listnodefiles] metodo su un'attività a più istanze, vengono restituiti solo i file dell'attività di hello primario.
>
>

Hello frammento di codice seguente viene illustrato come tooobtain sottoattività informazioni e come richiedere il contenuto del file da nodi hello in cui è stato eseguito.

```csharp
// Obtain hello job and hello multi-instance task from hello Batch service
CloudJob boundJob = batchClient.JobOperations.GetJob("mybatchjob");
CloudTask myMultiInstanceTask = boundJob.GetTask("mymultiinstancetask");

// Now obtain hello list of subtasks for hello task
IPagedEnumerable<SubtaskInformation> subtasks = myMultiInstanceTask.ListSubtasks();

// Asynchronously iterate over hello subtasks and print their stdout and stderr
// output if hello subtask has completed
await subtasks.ForEachAsync(async (subtask) =>
{
    Console.WriteLine("subtask: {0}", subtask.Id);
    Console.WriteLine("exit code: {0}", subtask.ExitCode);

    if (subtask.State == SubtaskState.Completed)
    {
        ComputeNode node =
            await batchClient.PoolOperations.GetComputeNodeAsync(subtask.ComputeNodeInformation.PoolId,
                                                                 subtask.ComputeNodeInformation.ComputeNodeId);

        NodeFile stdOutFile = await node.GetNodeFileAsync(subtask.ComputeNodeInformation.TaskRootDirectory + "\\" + Constants.StandardOutFileName);
        NodeFile stdErrFile = await node.GetNodeFileAsync(subtask.ComputeNodeInformation.TaskRootDirectory + "\\" + Constants.StandardErrorFileName);
        stdOut = await stdOutFile.ReadAsStringAsync();
        stdErr = await stdErrFile.ReadAsStringAsync();

        Console.WriteLine("node: {0}:", node.Id);
        Console.WriteLine("stdout.txt: {0}", stdOut);
        Console.WriteLine("stderr.txt: {0}", stdErr);
    }
    else
    {
        Console.WriteLine("\tSubtask {0} is in state {1}", subtask.Id, subtask.State);
    }
});
```

## <a name="code-sample"></a>Esempio di codice
Hello [MultiInstanceTasks] [ github_mpi] nell'esempio di codice su GitHub viene illustrato come una multi-istanza toouse attività toorun un [MS-MPI] [ msmpi_msdn] applicazione sui nodi di calcolo di Batch. Seguire i passaggi di hello in [preparazione](#preparation) e [esecuzione](#execution) toorun: esempio hello.

### <a name="preparation"></a>Operazioni preliminari
1. Seguire i primi due passaggi di hello in [come toocompile ed eseguire un semplice programma MS-MPI][msmpi_howto]. Questo soddisfa prerequesites hello per hello seguente passaggio.
2. Compilare un *versione* versione di hello [MPIHelloWorld] [ helloworld_proj] programma di esempio MPI. Si tratta di programma hello che verrà eseguita dall'attività di multi-istanza hello sui nodi di calcolo.
3. Creare un file zip contenente `MPIHelloWorld.exe` (compilato per il passaggio 2) e `MSMpiSetup.exe` (scaricato al passaggio 1). Carica il file zip come un pacchetto di applicazione nel passaggio successivo hello.
4. Hello utilizzare [portale di Azure] [ portal] toocreate un Batch [applicazione](batch-application-packages.md) chiamato "MPIHelloWorld" e specificare i file zip hello creato nel passaggio precedente hello come la versione "1.0" pacchetto di applicazione Hello. Vedere [Caricare e gestire le applicazioni](batch-application-packages.md#upload-and-manage-applications) per maggiori informazioni.

> [!TIP]
> Compilare un *versione* versione `MPIHelloWorld.exe` in modo che non è tooinclude eventuali dipendenze aggiuntive (ad esempio, `msvcp140d.dll` o `vcruntime140d.dll`) nel pacchetto dell'applicazione.
>
>

### <a name="execution"></a>Esecuzione
1. Scaricare hello [esempi di azure batch] [ github_samples_zip] da GitHub.
2. Aprire hello MultiInstanceTasks **soluzione** in Visual Studio 2015 o versione successiva. Hello `MultiInstanceTasks.sln` file della soluzione si trova:

    `azure-batch-samples\CSharp\ArticleProjects\MultiInstanceTasks\`
3. Immettere le credenziali dell'account Batch e l'archiviazione in `AccountSettings.settings` in hello **Microsoft.Azure.Batch.Samples.Common** progetto.
4. **Compilare ed eseguire** hello MultiInstanceTasks soluzione tooexecute hello esempio applicazione MPI in nodi di calcolo in un pool di Batch.
5. *Facoltativo*: hello utilizzare [portale di Azure] [ portal] o hello [Explorer Batch] [ batch_explorer] tooexamine pool esempio hello, processi, e attività ("MultiInstanceSamplePool", "MultiInstanceSampleJob", "MultiInstanceSampleTask") prima di eliminare le risorse di hello.

> [!TIP]
> È possibile scaricare [Visual Studio Community][visual_studio] gratuitamente se non si dispone di Visual Studio.
>
>

L'output di `MultiInstanceTasks.exe` è simile toohello seguente:

```
Creating pool [MultiInstanceSamplePool]...
Creating job [MultiInstanceSampleJob]...
Adding task [MultiInstanceSampleTask] toojob [MultiInstanceSampleJob]...
Awaiting task completion, timeout in 00:30:00...

Main task [MultiInstanceSampleTask] is in state [Completed] and ran on compute node [tvm-1219235766_1-20161017t162002z]:
---- stdout.txt ----
Rank 2 received string "Hello world" from Rank 0
Rank 1 received string "Hello world" from Rank 0

---- stderr.txt ----

Main task completed, waiting 00:00:10 for subtasks toocomplete...

---- Subtask information ----
subtask: 1
        exit code: 0
        node: tvm-1219235766_3-20161017t162002z
        stdout.txt:
        stderr.txt:
subtask: 2
        exit code: 0
        node: tvm-1219235766_2-20161017t162002z
        stdout.txt:
        stderr.txt:

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER tooexit...
```

## <a name="next-steps"></a>Passaggi successivi
* blog del Team di Batch di Azure e Microsoft HPC Hello illustra [MPI il supporto per Linux su Azure Batch][blog_mpi_linux]e include informazioni sull'uso [OpenFOAM] [ openfoam] con Batch. È possibile trovare esempi di codice Python per hello [esempio OpenFOAM su GitHub][github_mpi].
* Informazioni su come troppo[creare pool di nodi di calcolo Linux](batch-linux-nodes.md) per utilizzare nelle soluzioni di Azure Batch MPI.

[helloworld_proj]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/MultiInstanceTasks/MPIHelloWorld

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[blog_mpi_linux]: https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/
[cmd_start]: https://technet.microsoft.com/library/cc770297.aspx
[coord_cmd_example]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/article_samples/mpi/data/linux/openfoam/coordination-cmd
[github_mpi]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/MultiInstanceTasks
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[msdn_env_var]: https://msdn.microsoft.com/library/azure/mt743623.aspx
[msmpi_msdn]: https://msdn.microsoft.com/library/bb524831.aspx
[msmpi_sdk]: http://go.microsoft.com/FWLink/p/?LinkID=389556
[msmpi_howto]: http://blogs.technet.com/b/windowshpc/archive/2015/02/02/how-to-compile-and-run-a-simple-ms-mpi-program.aspx
[openfoam]: http://www.openfoam.com/
[visual_studio]: https://www.visualstudio.com/vs/community/

[net_jobprep]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.aspx
[net_multiinstance_class]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.aspx
[net_multiinstance_prop]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.multiinstancesettings.aspx
[net_multiinsance_commonresfiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.commonresourcefiles.aspx
[net_multiinstance_coordcmdline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.coordinationcommandline.aspx
[net_multiinstance_numinstances]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.numberofinstances.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_pool_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[net_pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_resourcefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.aspx
[net_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.aspx
[net_starttask_cmdline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.commandline.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_taskconstraints]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.aspx
[net_taskconstraint_maxretry]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.maxtaskretrycount.aspx
[net_taskconstraint_maxwallclock]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.maxwallclocktime.aspx
[net_taskconstraint_retention]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.retentiontime.aspx
[net_task_listsubtasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listsubtasks.aspx
[net_task_listnodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[poolops_getnodefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getnodefile.aspx

[portal]: https://portal.azure.com
[rest_multiinstance]: https://msdn.microsoft.com/library/azure/mt637905.aspx

[1]: ./media/batch-mpi/batch_mpi_01.png "Panoramica sulle istanze multiple"
