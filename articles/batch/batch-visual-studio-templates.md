---
title: compilazione di soluzioni di Batch con modelli di progetto di Visual Studio - Azure aaaStart | Documenti Microsoft
description: Informazioni su come questi modelli di progetto di Visual Studio consentono di implementare ed eseguire carichi di lavoro a elevato utilizzo di calcolo in Azure Batch.
services: batch
documentationcenter: .net
author: fayora
manager: timlt
editor: 
ms.assetid: 5e041ae2-25af-4882-a79e-3aa63c4bfb20
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a61c480ddc4dffd66c01220a137a3e852e39c338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-visual-studio-project-templates-toojump-start-batch-solutions"></a>Utilizzare soluzioni di Visual Studio project modelli toojump avvio Batch

Hello **il gestore di processi** e **modelli di Visual Studio di attività del processore** per Batch fornire codice toohelp è tooimplement ed eseguire i carichi di lavoro con utilizzo intensivo di calcolo in Batch con hello meno impegnativo. Questo documento vengono descritti questi modelli e fornisce indicazioni per il toouse li.

> [!IMPORTANT]
> In questo articolo vengono illustrati solo i modelli applicabili toothese due informazioni e si presuppone che si ha familiarità con il servizio di Batch hello e concetti chiave correlati tooit: pool, calcolare i nodi, processi e attività, attività di processo di gestione, le variabili di ambiente e altri informazioni rilevanti. È possibile trovare altre informazioni, vedere [nozioni di base di Azure Batch](batch-technical-overview.md), [Cenni preliminari sulla funzionalità di Batch per gli sviluppatori](batch-api-basics.md), e [Introduzione alla libreria di Azure Batch hello per .NET](batch-dotnet-get-started.md).
> 
> 

## <a name="high-level-overview"></a>Panoramica generale
modelli di gestore di processi e attività processore Hello possono essere utilizzato toocreate due componenti utili:

* Un'attività del gestore di processi che implementa un componente di suddivisione dei processi per suddividere un processo in più attività eseguibili in modo indipendente e parallelo.
* Un processore di attività che può essere utilizzati tooperform pre-elaborazione e post-elaborazione intorno a una riga di comando dell'applicazione.

Ad esempio, in uno scenario per il rendering di film, barra di divisione processo hello sarebbe trasformare un processo unico filmato in centinaia o migliaia di attività separate che elabora singoli frame separatamente. Di conseguenza, processore task hello sarebbe richiamare hello il rendering dell'applicazione e tutti i processi di dipendenti che sono necessari toorender ogni frame, nonché eseguire azioni aggiuntive (ad esempio, la copia hello rendering frame tooa percorso di archiviazione).

> [!NOTE]
> modelli di gestore di processi e attività processore Hello sono indipendenti tra loro, quindi è possibile scegliere toouse entrambi o solo uno di essi, a seconda dei requisiti di hello del processo di calcolo e alle preferenze.
> 
> 

Come illustrato nel diagramma hello riportato di seguito, un processo di calcolo che utilizza questi modelli passa attraverso tre fasi:

1. il codice client Hello (ad esempio, applicazione, il servizio web, e così via) Invia toohello un processo del servizio Batch in Azure, che specifica come il programma di gestione processo Gestione attività hello processo.
2. servizio Batch Hello esegue attività di gestione di processi hello in un nodo di calcolo e hello hello avvia barra di divisione di processo specificato numero di attività del processore di attività, alle molti nodi di calcolo in base alle esigenze, in base alle specifiche nel codice di divisione processo hello e parametri hello.
3. attività del processore di Hello attività eseguire in modo indipendente, in parallelo, tooprocess dati di input hello e generare dati di output di hello.

![Diagramma che illustra come il codice client interagisce con il servizio Batch hello][diagram01]

## <a name="prerequisites"></a>Prerequisiti
modelli di Batch hello toouse, sarà necessario seguente hello:

* Un computer in cui è installato Visual Studio 2015. I modelli di Batch sono attualmente supportati solo per Visual Studio 2015.
* modelli di Batch Hello, che sono disponibili da hello [Visual Studio Gallery] [ vs_gallery] come estensioni di Visual Studio. Esistono due modi tooget hello modelli:
  
  * Installare i modelli di hello utilizzando hello **estensioni e aggiornamenti** la finestra di dialogo in Visual Studio (per ulteriori informazioni, vedere [ricerca e uso delle estensioni di Visual Studio][vs_find_use_ext]). In hello **estensioni e aggiornamenti** della finestra di dialogo ricerca e download hello due estensioni seguenti:
    
    * Azure Batch Job Manager with Job Splitter (Gestore di processi di Azure Batch con componente di suddivisione dei processi)
    * Azure Batch Task Processor (Elaboratore di attività di Azure Batch)
  * Scaricare i modelli di hello dalla raccolta online hello per Visual Studio: [modelli di progetto di Microsoft Azure Batch][vs_gallery_templates]
* Se si prevede di hello toouse [pacchetti di applicazioni](batch-application-packages.md) il gestore di processi hello toodeploy di funzionalità e attività del processore toohello Batch nodi di calcolo, è necessario toolink un tooyour di account di archiviazione account Batch.

## <a name="preparation"></a>Operazioni preliminari
È consigliabile creare una soluzione destinata a contenga il gestore di processi, nonché il processore di attività, perché ciò può rendere più semplice codice tooshare tra il gestore di processi e i programmi di attività del processore. toocreate questa soluzione, seguire questi passaggi:

1. Aprire Visual Studio e selezionare **File** > **Nuovo** > **Progetto**.
2. In **Modelli** espandere **Altri tipi di progetti**, fare clic su **Soluzioni di Visual Studio** e selezionare **Soluzione vuota**.
3. Digitare un nome che descriva lo scopo dell'applicazione e hello di questa soluzione (ad esempio, "LitwareBatchTaskPrograms").
4. toocreate hello nuova soluzione, fare clic su **OK**.

## <a name="job-manager-template"></a>Modello Job Manager (Gestore di processi)
modello di processo Manager Hello consente si tooimplement un'attività di gestione di processo eseguibili hello seguenti azioni:

* Dividere un processo in più attività.
* Inviare toorun tali attività nel Batch.

> [!NOTE]
> Per altre informazioni sulle attività del gestore di processi, vedere [Panoramica delle funzionalità di Batch per sviluppatori](batch-api-basics.md#job-manager-task).
> 
> 

### <a name="create-a-job-manager-using-hello-template"></a>Creare un gestore di processi utilizzando il modello di hello
tooadd una soluzione di toohello manager processo creato in precedenza, seguire questi passaggi:

1. Aprire la soluzione esistente in Visual Studio.
2. In Esplora soluzioni, Esplora hello pulsante destro del mouse, fare clic su **Aggiungi** > **nuovo progetto**.
3. In **Visual C#** fare clic su **Cloud** e su **Azure Batch Job Manager with Job Splitter** (Gestore di processi di Azure Batch con componente di suddivisione dei processi).
4. Digitare un nome che descrive l'applicazione e identifica il progetto come gestore di processi hello (ad esempio "GestoreProcessiLitware".
5. progetto hello toocreate, fare clic su **OK**.
6. Infine, compilazione hello progetto tooforce Visual Studio tooload tutti i pacchetti NuGet a cui viene fatto riferimento e tooverify che hello progetto sia valido prima di iniziare la modifica.

### <a name="job-manager-template-files-and-their-purpose"></a>File del modello Job Manager (Gestore di processi) e relativo scopo
Quando si crea un progetto usando il modello di processo Manager hello, genera tre gruppi di file di codice:

* file di programma principale Hello (Program.cs). Che contiene il punto di ingresso programma hello e la gestione delle eccezioni di livello superiore. Non deve in genere necessario toomodify.
* directory del Framework Hello. Contiene file hello responsabili di lavoro 'standard' hello eseguita dal programma di gestione processo hello: installazione del pacchetto di parametri, aggiunta di processo Batch toohello di attività e così via. Non deve in genere toomodify i file necessari.
* file di divisione del processo Hello (JobSplitter.cs). in cui si inserirà la logica specifica dell'applicazione per suddividere un processo in attività.

Naturalmente è possibile aggiungere ulteriori file come obbligatorio toosupport codice processo barra di divisione, a seconda della complessità hello del processo di hello suddivisione logica.

modello di Hello genera anche i file di progetto .NET standard, ad esempio un file con estensione csproj app. config, Packages, e così via.

resto Hello di questa sezione vengono descritti diversi file hello e la relativa struttura di codice e le operazioni eseguite da ogni classe.

![Esplora soluzioni Visual Studio con una soluzione di modello di processo Manager hello][solution_explorer01]

**File di Framework**

* `Configuration.cs`: Incapsula il caricamento di hello processo dati di configurazione, ad esempio i dettagli dell'account Batch, le credenziali dell'account di archiviazione collegati, informazioni di processo e attività e i parametri del processo. Fornisce inoltre l'accesso delle variabili di ambiente definita tooBatch (vedere le impostazioni di ambiente per le attività, nella documentazione di Batch hello) tramite la classe Configuration.EnvironmentVariable hello.
* `IConfiguration.cs`: Riassunto hello implementazione della classe di configurazione di hello, in modo che sia possibile unit test divisione del processo utilizzando un oggetto di configurazione fittizi o.
* `JobManager.cs`: Coordina i componenti del programma di gestione processo di hello hello. Ed è responsabile per l'inizializzazione di divisione processo hello, chiamata divisione processo hello, hello e invio attività hello restituito dal mittente dell'attività toohello di hello processo barra di divisione.
* `JobManagerException.cs`: Rappresenta un errore che richiede hello processo manager tooterminate. JobManagerException è usato toowrap 'previsto' errori in cui le informazioni di diagnostica specifiche possono essere fornite come parte della terminazione.
* `TaskSubmitter.cs`: Questa classe è responsabile tooadding attività restituita dal processo Batch toohello di hello processo barra di divisione. classe JobManager Hello aggrega sequenza hello delle operazioni in batch per il processo di aggiunta efficiente ma tempestiva toohello, quindi chiama TaskSubmitter.SubmitTasks su un thread in background per ogni batch.

**Componente di suddivisione dei processi**

`JobSplitter.cs`: Questa classe contiene la logica specifica dell'applicazione per suddividere il processo di hello in attività. framework Hello richiama hello JobSplitter.Split metodo tooobtain una sequenza di attività, che viene aggiunto il processo di toohello come metodo hello li restituisce. Si tratta di classe hello in cui si inserirà logica hello del processo. Implementare hello Split metodo tooreturn una sequenza di istanze di CloudTask che rappresentano attività hello in cui si desidera che toopartition hello.

**File di progetto della riga di comando .NET standard**

* `App.config`: file di configurazione dell'applicazione .NET standard.
* `Packages.config`: file di dipendenza del pacchetto NuGet standard.
* `Program.cs`: Contiene il punto di ingresso programma hello e la gestione delle eccezioni di livello superiore.

### <a name="implementing-hello-job-splitter"></a>Implementazione della barra di divisione processo hello
Quando si apre il progetto di modello il gestore di processi di hello, progetto hello avrà file JobSplitter.cs hello aperta per impostazione predefinita. È possibile implementare hello suddividere la logica per le attività di hello nel carico di lavoro utilizzando Mostra di metodo Split () hello riportato di seguito:

```csharp
/// <summary>
/// Gets hello tasks into which toosplit hello job. This is where you inject
/// your application-specific logic for decomposing hello job into tasks.
///
/// hello job manager framework invokes hello Split method for you; you need
/// only tooimplement it, not toocall it yourself. Typically, your
/// implementation should return tasks lazily, for example using a C#
/// iterator and hello "yield return" statement; this allows tasks toobe added
/// and toostart running while splitting is still in progress.
/// </summary>
/// <returns>hello tasks toobe added toohello job. Tasks are added automatically
/// by hello job manager framework as they are returned by this method.</returns>
public IEnumerable<CloudTask> Split()
{
    // Your code for hello split logic goes here.
    int startFrame = Convert.ToInt32(_parameters["StartFrame"]);
    int endFrame = Convert.ToInt32(_parameters["EndFrame"]);

    for (int i = startFrame; i <= endFrame; i++)
    {
        yield return new CloudTask("myTask" + i, "cmd /c dir");
    }
}
```

> [!NOTE]
> Hello annotato sezione hello `Split()` metodo è hello sezione solo hello codice del modello di gestore di processi destinato a si toomodify aggiungendo hello logica toosplit i processi in attività diverse. Se si desidera toomodify un'altra sezione del modello di hello, verificare il funzionamento di Batch, è sono a conoscenza e provare a utilizzare alcune delle hello [Batch esempi di codice][github_samples].
> 
> 

L'implementazione di Split() ha accesso a:

* parametri del processo, tramite hello Hello `_parameters` campo.
* Hello CloudJob dell'oggetto che rappresenta i processi di hello, tramite hello `_job` campo.
* Hello CloudTask dell'oggetto che rappresenta hello manager mansione, tramite hello `_jobManagerTask` campo.

Il `Split()` non è necessario implementazione processo toohello di attività tooadd direttamente. Al contrario, il codice deve restituire una sequenza di oggetti CloudTask e verranno aggiunte toohello processo automaticamente dalle classi framework hello che richiamano la barra di divisione processo hello. È comune toouse # iteratore (`yield return`) funzionalità tooimplement separatori di processo, come in questo modo toostart attività hello più breve possibile anziché attendere che tutte le attività toobe calcolato.

**Errore del componente di suddivisione dei processi**

Se il componente di suddivisione dei processi rileva un errore, deve eseguire una di queste due operazioni:

* Terminare hello sequenza utilizzando hello c# `yield break` istruzione, in cui il gestore di processi hello case verrà considerato come esito positivo; o
* Genera un'eccezione, in cui il gestore di processi hello case verrà considerato come non riuscita e può essere ripetuto a seconda di come è configurato il client hello).

In entrambi i casi, tutte le attività non ha restituito da una barra di divisione processo hello e processo Batch toohello aggiunto saranno toorun idoneo. Se non si desidera questo toohappen, quindi è possibile:

* Terminare il processo di hello prima della restituzione da una barra di divisione processo hello
* Formulare raccolta intera attività hello prima di restituirlo (ovvero viene restituito un `ICollection<CloudTask>` o `IList<CloudTask>` anziché implementare la divisione di processo mediante un iteratore in c#)
* Utilizzare l'attività dipendenze toomake che tutte le attività dipendono dal completamento hello del gestore di processi hello

**Tentativi del gestore di processi**

Se il gestore di processi hello non riesce, può essere ripetuto dal servizio Batch hello a seconda delle impostazioni relative ai tentativi hello client. In generale, questa operazione è sicura, perché quando il framework di hello aggiunge processo toohello attività, ignora tutte le attività che esistono già. Tuttavia, se il calcolo delle attività è costoso, si può chiamare non costo hello tooincur di calcolo delle attività che sono già stati aggiunti toohello processo. al contrario, se hello esegue di nuovo è toogenerate non garantita hello stesso ID attività, quindi non consente di avviare il comportamento di 'Ignora i duplicati' hello in. In questi casi è consigliabile progettare il lavoro processo divisione toodetect hello che sia già stato eseguito e non ripeterla, ad esempio eseguendo un CloudJob.ListTasks prima di avviare attività tooyield.

### <a name="exit-codes-and-exceptions-in-hello-job-manager-template"></a>Uscire da codici e le eccezioni nel modello di processo Manager hello
Codici di uscita e le eccezioni forniscono un meccanismo toodetermine hello risultato esegue un programma e tooidentify possono consentire eventuali problemi con l'esecuzione di hello del programma hello. modello di processo Manager Hello implementa i codici di uscita hello e le eccezioni descritte in questa sezione.

Un'attività di gestione processo che viene implementata con modello di processo Manager hello può restituire tre codici di uscita possibili:

| Codice | Descrizione |
| --- | --- |
| 0 |gestore di processi Hello completato. Il codice della barra di divisione processo eseguito toocompletion e tutte le attività sono state aggiunte toohello processo. |
| 1 |attività di gestione di Hello processo non riuscito con un'eccezione in una parte del programma hello 'prevista'. eccezione Hello è stato tradotto tooa JobManagerException con informazioni di diagnostica e, se possibile, suggerimenti per la risoluzione hello errore. |
| 2 |attività del gestore Hello processi non riuscito con eccezione 'imprevista'. Hello eccezione era registrati toostandard output, ma il gestore di processi hello tooadd Impossibile le informazioni di diagnostica o di monitoraggio e aggiornamento. |

In caso di hello processo manager esito negativo dell'attività, alcune attività possono ancora essere stati aggiunti toohello servizio prima dell'errore di hello. Queste attività verranno eseguite normalmente. Per informazioni su questo percorso del codice, vedere sopra "Errore del componente di suddivisione dei processi".

Tutte le informazioni restituite da eccezioni hello vengono scritti nel file stdout.txt e stderr.txt. Per altre informazioni, vedere [Gestione degli errori](batch-api-basics.md#error-handling).

### <a name="client-considerations"></a>Considerazioni sul client
Questa sezione illustra alcuni requisiti dell'implementazione client quando si richiama un gestore di processi basato su questo modello. Vedere [come toopass parametri e variabili di ambiente da hello codice client](#pass-environment-settings) per ulteriori informazioni sul passaggio di parametri e le impostazioni di ambiente.

**Credenziali obbligatorie**

In tooadd attività toohello Azure batch ordine, attività del gestore processi hello richiede una chiave e l'URL dell'account Azure Batch. È necessario passarli nelle variabili di ambiente denominate YOUR_BATCH_URL e YOUR_BATCH_KEY. È possibile impostare nel gestore di processi hello impostazioni ambiente di attività. Ad esempio, in un client C#:

```csharp
job.JobManagerTask.EnvironmentSettings = new [] {
    new EnvironmentSetting("YOUR_BATCH_URL", "https://account.region.batch.azure.com"),
    new EnvironmentSetting("YOUR_BATCH_KEY", "{your_base64_encoded_account_key}"),
};
```
**Credenziali di archiviazione**

In genere, hello client non deve tooprovide hello archiviazione collegati account credenziali toohello attività del gestore processi perché (a) la maggior parte dei gestori di processo non è necessario l'account di archiviazione collegato hello accesso tooexplicitly e (b) hello account di archiviazione collegato viene spesso fornita attività tooall come un'impostazione di ambiente comuni per il processo di hello. Se non si desidera fornire hello collegato l'account di archiviazione tramite impostazioni di ambiente hello comuni, il gestore di processi hello richiede accesso toolinked archiviazione, quindi è necessario fornire le credenziali di archiviazione hello collegato come segue:

```csharp
job.JobManagerTask.EnvironmentSettings = new [] {
    /* other environment settings */
    new EnvironmentSetting("LINKED_STORAGE_ACCOUNT", "{storageAccountName}"),
    new EnvironmentSetting("LINKED_STORAGE_KEY", "{storageAccountKey}"),
};
```

**Impostazioni dell'attività del gestore di processi**

client Hello deve impostare il gestore di processi hello *killJobOnCompletion* flag troppo**false**.

È in genere sicura per hello client tooset *runExclusive* troppo**false**.

client di Hello deve utilizzare hello *resourceFiles* o *applicationPackageReferences* raccolta toohave hello il gestore di processi eseguibile (e relativa DLL necessarie) distribuito toohello del nodo di calcolo.

Per impostazione predefinita, il gestore di processi hello non verrà ritentato in caso di errore. A seconda la logica di gestione del processo, il client hello può essere tooenable tentativi tramite *vincoli*/*maxTaskRetryCount*.

**Impostazioni del processo**

Se il separatore di processo hello genera attività con dipendenze, il client di hello deve impostare tootrue usesTaskDependencies del processo di hello.

Nel modello di divisione hello processo, è insolito per i client toowish tooadd attività toojobs oltre il separatore di processo hello crea. client Hello dovrebbe pertanto impostato del processo di hello *onAllTasksComplete* troppo**terminatejob**.

## <a name="task-processor-template"></a>Modello Task Processor (Elaboratore di attività)
Un modello di processore Task consente tooimplement un processore di attività eseguibili hello seguenti azioni:

* Impostare le informazioni di hello richieste da ogni toorun attività Batch.
* Eseguire tutte le azioni necessarie per ogni attività batch.
* Salvare l'output di un'attività toopersistent archiviazione.

Anche se un processore di attività non è necessario toorun attività nel Batch, hello dei principali vantaggi dell'utilizzo di un processore di attività è che fornisce un wrapper tooimplement tutte le azioni di esecuzione di attività in un'unica posizione. Ad esempio, se è necessario toorun diverse applicazioni nel contesto di hello di ogni attività o se è necessario toocopy archiviazione toopersistent dei dati dopo il completamento di ogni attività.

azioni Hello eseguite dal processore task hello possono essere semplice o complesso e il numero o minor, come richiesto dal carico di lavoro. Inoltre, implementando tutte le azioni di attività in un processore di attività, è possibile facilmente aggiornare o aggiungere azioni in base ai requisiti di carico di lavoro o tooapplications le modifiche. Tuttavia, in alcuni casi un processore di attività potrebbe non essere hello ottimale soluzione per l'implementazione come è possibile aggiungere un'inutile complessità, ad esempio quando si esegue i processi che è possibile avviare rapidamente da una semplice riga di comando.

### <a name="create-a-task-processor-using-hello-template"></a>Creare un processore di attività utilizzando il modello di hello
tooadd una soluzione di toohello processore attività creata in precedenza, seguire questi passaggi:

1. Aprire la soluzione esistente in Visual Studio.
2. In Esplora soluzioni, Esplora hello pulsante destro del mouse, fare clic su **Aggiungi**, quindi fare clic su **nuovo progetto**.
3. In **Visual C#** fare clic su **Cloud** e su **Azure Batch Task Processor** (Elaboratore di attività di Azure Batch).
4. Digitare un nome che descrive l'applicazione e identifica il progetto come hello (ad esempio, il processore di attività "ElaboratoreAttivitàLitware".
5. progetto hello toocreate, fare clic su **OK**.
6. Infine, compilazione hello progetto tooforce Visual Studio tooload tutti i pacchetti NuGet a cui viene fatto riferimento e tooverify che hello progetto sia valido prima di iniziare la modifica.

### <a name="task-processor-template-files-and-their-purpose"></a>File del modello Task Processor (Elaboratore di attività) e relativo scopo
Quando si crea un progetto modello di processore attività hello, genera tre gruppi di file di codice:

* file di programma principale Hello (Program.cs). Che contiene il punto di ingresso programma hello e la gestione delle eccezioni di livello superiore. Non deve in genere necessario toomodify.
* directory del Framework Hello. Contiene file hello responsabili di lavoro 'standard' hello eseguita dal programma di gestione processo hello: installazione del pacchetto di parametri, aggiunta di processo Batch toohello di attività e così via. Non deve in genere toomodify i file necessari.
* file del processore Hello attività (TaskProcessor.cs). Si tratta in cui si inserirà la logica specifica dell'applicazione per l'esecuzione di un'attività (in genere da una chiamata in uscita eseguibile esistente tooan). Anche il codice di pre-elaborazione e post-elaborazione, ad esempio per il download di dati aggiuntivi o il caricamento dei file dei risultati, viene inserito qui.

Naturalmente è possibile aggiungere ulteriori file come toosupport richiesto il codice di attività del processore, a seconda della complessità hello del processo di hello suddivisione logica.

modello di Hello genera anche i file di progetto .NET standard, ad esempio un file con estensione csproj app. config, Packages, e così via.

resto Hello di questa sezione vengono descritti diversi file hello e la relativa struttura di codice e le operazioni eseguite da ogni classe.

![Esplora soluzioni Visual Studio con una soluzione di modello attività processore hello][solution_explorer02]

**File di Framework**

* `Configuration.cs`: Incapsula il caricamento di hello processo dati di configurazione, ad esempio i dettagli dell'account Batch, le credenziali dell'account di archiviazione collegati, informazioni di processo e attività e i parametri del processo. Fornisce inoltre l'accesso delle variabili di ambiente definita tooBatch (vedere le impostazioni di ambiente per le attività, nella documentazione di Batch hello) tramite la classe Configuration.EnvironmentVariable hello.
* `IConfiguration.cs`: Riassunto hello implementazione della classe di configurazione di hello, in modo che sia possibile unit test divisione del processo utilizzando un oggetto di configurazione fittizi o.
* `TaskProcessorException.cs`: Rappresenta un errore che richiede hello processo manager tooterminate. TaskProcessorException è usato toowrap 'previsto' errori in cui le informazioni di diagnostica specifiche possono essere fornite come parte della terminazione.

**Elaboratore di attività**

* `TaskProcessor.cs`: Esegue l'attività di hello. framework Hello richiama il metodo TaskProcessor.Run hello. Si tratta di classe hello in cui si inserirà logica specifica dell'applicazione hello dell'attività. Implementare il metodo Run hello per:
  * Analizzare e convalidare i parametri delle attività
  * Comporre hello della riga di comando per qualsiasi programma esterno, si desidera tooinvoke
  * Registrare le informazioni di diagnostica che potrebbero essere necessarie a scopo di debug
  * Avviare un processo usando tale riga di comando
  * Attendere hello processo tooexit
  * Acquisire il codice di uscita hello di hello processo toodetermine se ha avuto esito positivo o non è riuscita
  * Salvare i file di output desiderato tookeep toopersistent archiviazione

**File di progetto della riga di comando .NET standard**

* `App.config`: file di configurazione dell'applicazione .NET standard.
* `Packages.config`: file di dipendenza del pacchetto NuGet standard.
* `Program.cs`: Contiene il punto di ingresso programma hello e la gestione delle eccezioni di livello superiore.

## <a name="implementing-hello-task-processor"></a>Implementazione del processore attività hello
Quando si apre il progetto di modello di hello processore Task, progetto hello avrà file TaskProcessor.cs hello aperta per impostazione predefinita. È possibile implementare la logica di eseguire hello per le attività di hello nel carico di lavoro con metodo Run () hello illustrato di seguito:

```csharp
/// <summary>
/// Runs hello task processing logic. This is where you inject
/// your application-specific logic for decomposing hello job into tasks.
///
/// hello task processor framework invokes hello Run method for you; you need
/// only tooimplement it, not toocall it yourself. Typically, your
/// implementation will execute an external program (from resource files or
/// an application package), check hello exit code of that program and
/// save output files toopersistent storage.
/// </summary>
public async Task<int> Run()

{
    try
    {
        //Your code for hello task processor goes here.
        var command = $"compare {_parameters["Frame1"]} {_parameters["Frame2"]} compare.gif";
        using (var process = Process.Start($"cmd /c {command}"))
        {
            process.WaitForExit();
            var taskOutputStorage = new TaskOutputStorage(
            _configuration.StorageAccount,
            _configuration.JobId,
            _configuration.TaskId
            );
            await taskOutputStorage.SaveAsync(
            TaskOutputKind.TaskOutput,
            @"..\stdout.txt",
            @"stdout.txt"
            );
            return process.ExitCode;
        }
    }
    catch (Exception ex)
    {
        throw new TaskProcessorException(
        $"{ex.GetType().Name} exception in run task processor: {ex.Message}",
        ex
        );
    }
}
```
> [!NOTE]
> Hello annotato nel hello metodo Run () è hello solo sezione di codice del modello attività processore hello destinato si toomodify mediante l'aggiunta di logica eseguire hello per le attività di hello nel carico di lavoro. Se si desidera toomodify un'altra sezione del modello di hello,. prima di tutto acquisire familiarità con la modalità Batch funziona esaminare la documentazione di Batch hello e provare alcuni degli esempi di codice hello Batch.
> 
> 

Hello metodo Run () è responsabile dell'avvio della riga di comando hello, avvio di uno o più processi, in attesa di toocomplete processo tutti, salvataggio dei risultati di hello e infine restituzione con un codice di uscita. Hello metodo Run () è in cui viene implementata hello logica per le attività di elaborazione. framework processore delle attività Hello Richiama metodo Run () hello. non è necessario toocall è manualmente.

L'implementazione di Run() ha accesso a:

* i parametri di attività, tramite hello Hello `_parameters` campo.
* ID attività e processi, tramite hello Hello `_jobId` e `_taskId` campi.
* configurazione dell'attività Hello, tramite hello `_configuration` campo.

**Errore dell'attività**

In caso di errore, è possibile uscire dal metodo Run () hello generando un'eccezione, ma in questo modo, il gestore di eccezioni di livello superiore di hello nel controllo del codice di uscita attività hello. Se è necessario codice di uscita toocontrol hello in modo che sia possibile distinguere i diversi tipi di errore, ad esempio per motivi di diagnostica o perché alcune modalità di errore deve terminare processi hello e altri utenti non dovrebbero, quindi è necessario uscire metodo Run () hello restituendo un codice di uscita diverso da zero. Questo valore diventa codice di uscita attività hello.

### <a name="exit-codes-and-exceptions-in-hello-task-processor-template"></a>Uscire da codici e le eccezioni nel modello di attività processore hello
Codici di uscita e le eccezioni forniscono un meccanismo toodetermine hello risultato esegue un programma e consentono di identificare eventuali problemi con l'esecuzione di hello del programma hello. modello di attività processore Hello implementa i codici di uscita hello e le eccezioni descritte in questa sezione.

Un'attività del processore attività che viene implementata con modello di attività processore hello può restituire tre codici di uscita possibili:

| Codice | Descrizione |
| --- | --- |
| [Process.ExitCode][process_exitcode] |processore task Hello eseguito toocompletion. Si noti che ciò non implica tale programma hello che è stata completata, solo hello attività processore ha eseguito correttamente ed eseguita post-elaborazione senza eccezioni. Hello significato del codice di uscita hello dipende dal programma richiamato hello – codice di uscita 0 significa in genere programma hello ha avuto esito positivo e qualsiasi altro codice di uscita significa hello programma non è riuscito. |
| 1 |processore task Hello non riuscita con un'eccezione in una parte del programma hello 'prevista'. Hello eccezione è stata tradotta tooa `TaskProcessorException` con informazioni di diagnostica e, se possibile, suggerimenti per la risoluzione hello errore. |
| 2 |processore task Hello non riuscito con eccezione 'imprevista'. Hello eccezione era registrati toostandard output, ma processore task hello tooadd Impossibile le informazioni di diagnostica o di monitoraggio e aggiornamento. |

> [!NOTE]
> Se il programma di hello che richiami utilizza modalità di errore specifico di uscita codici 1 e 2 tooindicate, quindi utilizzare i codici di uscita 1 e 2 per gli errori delle attività del processore è ambiguo. È possibile modificare questi codici di uscita attività processore errore codici toodistinctive modificando i casi di eccezione hello nel file Program.cs hello.
> 
> 

Tutte le informazioni restituite da eccezioni hello vengono scritti nel file stdout.txt e stderr.txt. Per ulteriori informazioni, vedere Gestione di errori, nella documentazione di Batch hello.

### <a name="client-considerations"></a>Considerazioni sul client
**Credenziali di archiviazione**

Se il processore di attività Usa l'output di toopersist archiviazione blob di Azure, ad esempio l'utilizzo della libreria helper di convenzioni file hello, quindi è richiesto l'accesso troppo*entrambi* hello le credenziali dell'account di archiviazione cloud *o* URL del contenitore blob che include una firma di accesso condiviso (SAS). modello Hello include il supporto per fornire le credenziali tramite variabili di ambiente comuni. Il client può passare le credenziali di archiviazione hello come indicato di seguito:

```csharp
job.CommonEnvironmentSettings = new [] {
    new EnvironmentSetting("LINKED_STORAGE_ACCOUNT", "{storageAccountName}"),
    new EnvironmentSetting("LINKED_STORAGE_KEY", "{storageAccountKey}"),
};
```

account di archiviazione Hello diventa quindi disponibile nella classe TaskProcessor tramite hello hello `_configuration.StorageAccount` proprietà.

Se si preferisce toouse un URL del contenitore con firma di accesso condiviso, è anche possibile passare questo tramite un'impostazione di ambiente comuni di processo, ma modello attività hello attualmente non include supporto incorporato per questo.

**Configurazione dell'archiviazione**

È consigliabile hello client o del processo di Gestione attività creare tutti i contenitori necessari per le attività prima dell'aggiunta di hello attività toohello processo. Questo campo è obbligatorio che se si utilizza un URL del contenitore con firma di accesso condiviso, di conseguenza un URL non include autorizzazioni toocreate hello contenitore. Anche se si passa le credenziali dell'account di archiviazione, è consigliabile come Salva tutte le attività con toocall CloudBlobContainer.CreateIfNotExistsAsync nel contenitore hello.

## <a name="pass-parameters-and-environment-variables"></a>Passare i parametri e le variabili di ambiente
### <a name="pass-environment-settings"></a>Passare le impostazioni di ambiente
Un client può passare l'attività del gestore processi toohello informazioni sotto forma di hello di impostazioni di ambiente. Queste informazioni possono quindi utilizzabile da attività del gestore processi hello quando il processo di calcolo di generazione hello processore attività che verrà eseguita come parte di hello. Sono esempi di hello informazioni che è possibile passare alle impostazioni di ambiente:

* Nome dell'account di archiviazione e chiavi dell'account
* URL dell'account Batch
* Chiave dell'account Batch

Hello servizio Batch è un'attività di gestione di un meccanismo semplice toopass ambiente impostazioni tooa processi utilizzando hello `EnvironmentSettings` proprietà [Microsoft.Azure.Batch.JobManagerTask][net_jobmanagertask].

Ad esempio, tooget hello `BatchClient` istanza per un account di Batch, è possibile passare come variabili di ambiente da client hello codice hello URL e credenziali di chiave per l'account Batch hello condivise. Analogamente, account di archiviazione di hello tooaccess è collegato l'account Batch toohello, è possibile passare nome account di archiviazione hello e chiave dell'account di archiviazione hello come variabili di ambiente.

### <a name="pass-parameters-toohello-job-manager-template"></a>Passare parametri toohello processo Gestione modello
In molti casi, è utile toopass per processo parametri toohello processo Gestione attività, entrambi processo hello toocontrol suddivisione processo o attività hello tooconfigure per hello processo. È possibile farlo caricando un file JSON denominato parameters.json come file di risorse per attività di gestione di processi hello. i parametri di Hello possono poi diventare disponibili in hello `JobSplitter._parameters` campo nel modello di processo Manager hello.

> [!NOTE]
> il gestore di parametri predefiniti di Hello supporta solo i dizionari per stringa-stringa. Se si desidera valori JSON complessi toopass come valori di parametro, verrà necessità toopass queste informazioni come stringhe e analizzarli nella barra di divisione processo hello o modifica del framework di hello `Configuration.GetJobParameters` metodo.
> 
> 

### <a name="pass-parameters-toohello-task-processor-template"></a>Passare parametri toohello processore attività modello
È inoltre possibile passare parametri attività tooindividual implementato utilizzando il modello di attività processore hello. Proprio come con modello di gestione processo di hello, hello attività processore modello cerca un file di risorse denominato

Parameters.JSON e se lo trova, viene caricato in formato dizionario di parametri hello. Sono disponibili due opzioni per la modalità toopass parametri toohello attività attività del processore:

* Riutilizzare i parametri del processo hello JSON. Ciò funziona perfettamente se hello unici parametri sono quelli a livello di processo (ad esempio, un rendering altezza e larghezza). toodo, quando si crea un CloudTask nella barra di divisione processo hello, aggiungere un oggetto file di risorse di riferimento toohello parameters.json da ResourceFiles hello processo Gestione attività (`JobSplitter._jobManagerTask.ResourceFiles`) insieme ResourceFiles del CloudTask toohello.
* Generare e caricare un documento parameters.json specifici dell'attività come parte dell'esecuzione del processo con separatore, fare riferimento a tale blob nella raccolta di file di risorse dell'attività hello. Ciò è necessario se i parametri sono diversi per ogni attività. Un esempio potrebbe essere uno scenario di rendering 3D in indice dei fotogrammi hello è toohello attività passata come parametro.

> [!NOTE]
> il gestore di parametri predefiniti di Hello supporta solo i dizionari per stringa-stringa. Se si desidera valori JSON complessi toopass come valori di parametro, si verrà necessarie toopass come stringhe e analizzarli in processore task hello o modificare del framework hello `Configuration.GetTaskParameters` metodo.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
### <a name="persist-job-and-task-output-tooazure-storage"></a>Processo di persistenza e attività output tooAzure archiviazione
Un altro strumento utile nello sviluppo di soluzioni Batch è [Azure Batch File Conventions][nuget_package]. Utilizzare questa libreria di classi .NET (attualmente in anteprima) nell'archivio tooeasily applicazioni .NET per Batch e recuperare tooand output attività dall'archiviazione di Azure. [Output di attività e processi Batch di Azure di mantenere](batch-task-output.md) contiene una descrizione completa della libreria hello e sul relativo utilizzo.

### <a name="batch-forum"></a>Forum di Batch
Hello [Forum di Azure Batch] [ forum] su MSDN è un ottimo posizionare toodiscuss Batch e porre domande sul servizio hello. Leggere i post contrassegnati e inviare domande durante le procedure di sviluppo delle soluzioni Batch.

[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[net_jobmanagertask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobmanagertask.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[process_exitcode]: https://msdn.microsoft.com/library/system.diagnostics.process.exitcode.aspx
[vs_gallery]: https://visualstudiogallery.msdn.microsoft.com/
[vs_gallery_templates]: https://go.microsoft.com/fwlink/?linkid=820714
[vs_find_use_ext]: https://msdn.microsoft.com/library/dd293638.aspx

[diagram01]: ./media/batch-visual-studio-templates/diagram01.png
[solution_explorer01]: ./media/batch-visual-studio-templates/solution_explorer01.png
[solution_explorer02]: ./media/batch-visual-studio-templates/solution_explorer02.png
