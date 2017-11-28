---
title: un Cloud servizio localmente nell'emulatore di calcolo hello aaaProfiling | Documenti Microsoft
services: cloud-services
description: Analizzare i problemi di prestazioni nei servizi cloud con il profiler di Visual Studio hello
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
tags: 
ms.assetid: 25e40bf3-eea0-4b0b-9f4a-91ffe797f6c3
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: fc37c85dad4db4cc0310f73afad56fc0fe5f3963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="testing-hello-performance-of-a-cloud-service-locally-in-hello-azure-compute-emulator-using-hello-visual-studio-profiler"></a><span data-ttu-id="6d3d8-103">Test delle prestazioni di locale di un servizio Cloud hello in hello Azure Compute Emulator tramite hello Profiler di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6d3d8-103">Testing hello Performance of a Cloud Service Locally in hello Azure Compute Emulator Using hello Visual Studio Profiler</span></span>
<span data-ttu-id="6d3d8-104">Un'ampia gamma di strumenti e tecniche sono disponibili per il test delle prestazioni di hello dei servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-104">A variety of tools and techniques are available for testing hello performance of cloud services.</span></span>
<span data-ttu-id="6d3d8-105">Quando si pubblica un tooAzure servizio cloud, è possibile impostare Visual Studio raccogliere dati di profilatura e analizzarli in locale, come descritto in [profilatura di un'applicazione Azure][1].</span><span class="sxs-lookup"><span data-stu-id="6d3d8-105">When you publish a cloud service tooAzure, you can have Visual Studio collect profiling data and then analyze it locally, as described in [Profiling an Azure Application][1].</span></span>
<span data-ttu-id="6d3d8-106">È inoltre possibile utilizzare diagnostica tootrack contatori delle prestazioni diverse, come descritto in [mediante i contatori delle prestazioni in Azure][2].</span><span class="sxs-lookup"><span data-stu-id="6d3d8-106">You can also use diagnostics tootrack a variety of performance counters, as described in [Using performance counters in Azure][2].</span></span>
<span data-ttu-id="6d3d8-107">È inoltre possibile tooprofile l'applicazione localmente nell'emulatore di calcolo hello prima della distribuzione cloud toohello.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-107">You might also want tooprofile your application locally in hello compute emulator before deploying it toohello cloud.</span></span>

<span data-ttu-id="6d3d8-108">Questo articolo descrive il metodo di campionamento CPU di hello di profilatura, che può essere eseguito localmente nell'emulatore hello.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-108">This article covers hello CPU Sampling method of profiling, which can be done locally in hello emulator.</span></span> <span data-ttu-id="6d3d8-109">Si tratta di un metodo di profilatura non eccessivamente invasivo.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-109">CPU sampling is a method of profiling that is not very intrusive.</span></span> <span data-ttu-id="6d3d8-110">In un intervallo di campionamento designato, il profiler hello accetta uno snapshot dello stack di chiamate hello.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-110">At a designated sampling interval, hello profiler takes a snapshot of hello call stack.</span></span> <span data-ttu-id="6d3d8-111">dati Hello vengono raccolti in un periodo di tempo e presenti in un report.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-111">hello data is collected over a period of time, and shown in a report.</span></span> <span data-ttu-id="6d3d8-112">Questo metodo di profilatura tende tooindicate in cui in un'applicazione con calcoli complessi la maggior parte del lavoro hello CPU viene eseguita.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-112">This method of profiling tends tooindicate where in a computationally intensive application most of hello CPU work is being done.</span></span>  <span data-ttu-id="6d3d8-113">In questo modo si hello toofocus opportunità tracciato hello"attivo" in cui l'applicazione sta impiegando hello la maggior parte di tempo.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-113">This gives you hello opportunity toofocus on hello "hot path" where your application is spending hello most time.</span></span>

## <a name="1-configure-visual-studio-for-profiling"></a><span data-ttu-id="6d3d8-114">1: Configurare Visual Studio per la profilatura</span><span class="sxs-lookup"><span data-stu-id="6d3d8-114">1: Configure Visual Studio for profiling</span></span>
<span data-ttu-id="6d3d8-115">Visual Studio include alcune opzioni di configurazione che possono risultare utili per la profilatura.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-115">First, there are a few Visual Studio configuration options that might be helpful when profiling.</span></span> <span data-ttu-id="6d3d8-116">senso toomake di hello i rapporti di profilatura, è necessario simboli (PDB) per l'applicazione e anche i simboli per le librerie di sistema.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-116">toomake sense of hello profiling reports, you'll need symbols (.pdb files) for your application and also symbols for system libraries.</span></span> <span data-ttu-id="6d3d8-117">È opportuno assicurarsi di fare riferimento a server dei simboli disponibili hello toomake.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-117">You'll want toomake sure that you reference hello available symbol servers.</span></span> <span data-ttu-id="6d3d8-118">toodo questo su hello **strumenti** menu in Visual Studio, scegliere **opzioni**, quindi scegliere **debug**, quindi **simboli**.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-118">toodo this, on hello **Tools** menu in Visual Studio, choose **Options**, then choose **Debugging**, then **Symbols**.</span></span> <span data-ttu-id="6d3d8-119">Verificare che Server dei simboli Microsoft sia elencato in **Percorsi dei file di simboli (pdb)**.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-119">Make sure that Microsoft Symbol Servers is listed under **Symbol file (.pdb) locations**.</span></span>  <span data-ttu-id="6d3d8-120">È inoltre possibile fare riferimento a http://referencesource.microsoft.com/symbols, dove potrebbero essere disponibili file di simboli aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-120">You can also reference http://referencesource.microsoft.com/symbols, which might have additional symbol files.</span></span>

![Opzioni dei simboli][4]

<span data-ttu-id="6d3d8-122">Se si desidera, è possibile semplificare hello segnala che il profiler hello genera impostando Just My Code.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-122">If desired, you can simplify hello reports that hello profiler generates by setting Just My Code.</span></span> <span data-ttu-id="6d3d8-123">Con Just My Code attivata, gli stack di chiamate di funzione sono stati semplificati in modo che chiama toolibraries completamente interno e hello .NET Framework sono nascosti da report hello.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-123">With Just My Code enabled, function call stacks are simplified so that calls entirely internal toolibraries and hello .NET Framework are hidden from hello reports.</span></span> <span data-ttu-id="6d3d8-124">In hello **strumenti** menu, scegliere **opzioni**.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-124">On hello **Tools** menu, choose **Options**.</span></span> <span data-ttu-id="6d3d8-125">Espandere quindi hello **strumenti di prestazioni** nodo e scegliere **generale**.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-125">Then expand hello **Performance Tools** node, and choose **General**.</span></span> <span data-ttu-id="6d3d8-126">Selezionare una casella di controllo hello **Abilita Just My Code per i rapporti del profiler**.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-126">Select hello checkbox for **Enable Just My Code for profiler reports**.</span></span>

![Opzioni di Just My Code][17]

<span data-ttu-id="6d3d8-128">Queste istruzioni sono applicabili a un progetto esistente o a un nuovo progetto.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-128">You can use these instructions with an existing project or with a new project.</span></span>  <span data-ttu-id="6d3d8-129">Se si crea un nuovo hello tootry progetto tecniche descritte di seguito, scegliere c# **servizio Cloud di Azure** del progetto e selezionare un **ruolo Web** e un **ruolo di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-129">If you create a new project tootry hello techniques described below, choose a C# **Azure Cloud Service** project, and select a **Web Role** and a **Worker Role**.</span></span>

![Ruoli del progetto Servizi cloud di Azure][5]

<span data-ttu-id="6d3d8-131">Scopi, ad esempio aggiungere un progetto di codice tooyour che richiede molto tempo e illustra alcuni problemi di prestazioni ovvio.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-131">For example purposes, add some code tooyour project that takes a lot of time and demonstrates some obvious performance problem.</span></span> <span data-ttu-id="6d3d8-132">Ad esempio, aggiungere hello progetto ruolo di lavoro tooa di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="6d3d8-132">For example, add hello following code tooa worker role project:</span></span>

    public class Concatenator
    {
        public static string Concatenate(int number)
        {
            int count;
            string s = "";
            for (count = 0; count < number; count++)
            {
                s += "\n" + count.ToString();
            }
            return s;
        }
    }

<span data-ttu-id="6d3d8-133">Chiamare il codice da hello RunAsync metodo nella classe derivata da RoleEntryPoint del ruolo di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-133">Call this code from hello RunAsync method in hello worker role's RoleEntryPoint-derived class.</span></span> <span data-ttu-id="6d3d8-134">(Ignora avviso hello sul metodo hello in esecuzione in modo sincrono).</span><span class="sxs-lookup"><span data-stu-id="6d3d8-134">(Ignore hello warning about hello method running synchronously.)</span></span>

        private async Task RunAsync(CancellationToken cancellationToken)
        {
            // TODO: Replace hello following with your own logic.
            while (!cancellationToken.IsCancellationRequested)
            {
                Trace.TraceInformation("Working");
                Concatenator.Concatenate(10000);
            }
        }

<span data-ttu-id="6d3d8-135">Compilare ed eseguire il servizio cloud in locale senza eseguire debug (Ctrl + F5), con la configurazione della soluzione hello impostato troppo**versione**.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-135">Build and run your cloud service locally without debugging (Ctrl+F5), with hello solution configuration set too**Release**.</span></span> <span data-ttu-id="6d3d8-136">Ciò garantisce che tutti i file e cartelle vengono create per l'esecuzione di un'applicazione hello in locale e assicura che tutti gli emulatori di hello siano avviati.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-136">This ensures that all files and folders are created for running hello application locally, and ensures that all hello emulators are started.</span></span> <span data-ttu-id="6d3d8-137">Avviare hello interfaccia utente dell'emulatore di calcolo da hello barra delle applicazioni tooverify che esegue il ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-137">Start hello Compute Emulator UI from hello taskbar tooverify that your worker role is running.</span></span>

## <a name="2-attach-tooa-process"></a><span data-ttu-id="6d3d8-138">2: connessione del processo tooa</span><span class="sxs-lookup"><span data-stu-id="6d3d8-138">2: Attach tooa process</span></span>
<span data-ttu-id="6d3d8-139">Anziché un'applicazione hello avviandolo hello IDE di Visual Studio 2010, è necessario collegare hello profiler tooa esecuzione processo.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-139">Instead of profiling hello application by starting it from hello Visual Studio 2010 IDE, you must attach hello profiler tooa running process.</span></span> 

<span data-ttu-id="6d3d8-140">tooattach hello profiler tooa processo, di hello **Analizza** menu, scegliere **Profiler** e **collegamento/scollegamento**.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-140">tooattach hello profiler tooa process, on hello **Analyze** menu, choose **Profiler** and **Attach/Detach**.</span></span>

![Opzione per il collegamento del profilo][6]

<span data-ttu-id="6d3d8-142">Per un ruolo di lavoro, trovare il processo di WaWorkerHost.exe hello.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-142">For a worker role, find hello WaWorkerHost.exe process.</span></span>

![Processo WaWorkerHost][7]

<span data-ttu-id="6d3d8-144">Se la cartella di progetto è un'unità di rete, il profiler hello chiederà tooprovide hello di toosave percorso un altro report per la profilatura.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-144">If your project folder is on a network drive, hello profiler will ask you tooprovide another location toosave hello profiling reports.</span></span>

 <span data-ttu-id="6d3d8-145">È inoltre possibile allegare il ruolo web tooa collegando tooWaIISHost.exe.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-145">You can also attach tooa web role by attaching tooWaIISHost.exe.</span></span>
<span data-ttu-id="6d3d8-146">Se sono presenti più processi di ruolo di lavoro nell'applicazione, è necessario toouse hello processID toodistinguish li.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-146">If there are multiple worker role processes in your application, you need toouse hello processID toodistinguish them.</span></span> <span data-ttu-id="6d3d8-147">È possibile eseguire query a livello di codice hello processID accedendo all'oggetto processo hello.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-147">You can query hello processID programmatically by accessing hello Process object.</span></span> <span data-ttu-id="6d3d8-148">Ad esempio, se si aggiunge questo metodo di esecuzione di codice toohello della classe derivata RoleEntryPoint hello in un ruolo, è possibile esaminare il log hello tooknow di interfaccia utente dell'emulatore di calcolo tooconnect il processo di.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-148">For example, if you add this code toohello Run method of hello RoleEntryPoint-derived class in a role, you can look at the log in hello Compute Emulator UI tooknow what process tooconnect to.</span></span>

    var process = System.Diagnostics.Process.GetCurrentProcess();
    var message = String.Format("Process ID: {0}", process.Id);
    Trace.WriteLine(message, "Information");

<span data-ttu-id="6d3d8-149">log di hello tooview, hello avvio dell'interfaccia utente emulatore di calcolo.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-149">tooview hello log, start hello Compute Emulator UI.</span></span>

![Avviare hello interfaccia utente dell'emulatore di calcolo][8]

<span data-ttu-id="6d3d8-151">Aprire la finestra console hello lavoro ruolo log in hello interfaccia utente dell'emulatore di calcolo facendo clic sulla barra del titolo della finestra di console hello.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-151">Open hello worker role log console window in hello Compute Emulator UI by clicking on hello console window's title bar.</span></span> <span data-ttu-id="6d3d8-152">È possibile visualizzare l'ID del processo nel registro hello hello.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-152">You can see hello process ID in hello log.</span></span>

![Visualizzare l'ID processo][9]

<span data-ttu-id="6d3d8-154">È stata associata, una procedura hello nello scenario di hello tooreproduce dell'interfaccia utente (se necessario) dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-154">One you've attached, perform hello steps in your application's UI (if needed) tooreproduce hello scenario.</span></span>

<span data-ttu-id="6d3d8-155">Quando si desidera toostop profilatura, scegliere hello **arrestare profilatura** collegamento.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-155">When you want toostop profiling, choose hello **Stop Profiling** link.</span></span>

![Opzione Arresta profilatura][10]

## <a name="3-view-performance-reports"></a><span data-ttu-id="6d3d8-157">3: Visualizzare i rapporti relativi alle prestazioni</span><span class="sxs-lookup"><span data-stu-id="6d3d8-157">3: View performance reports</span></span>
<span data-ttu-id="6d3d8-158">report prestazioni Hello per l'applicazione viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-158">hello performance report for your application is displayed.</span></span>

<span data-ttu-id="6d3d8-159">A questo punto, hello profiler interrompe l'esecuzione, Salva i dati in un file con estensione vsp e consente di visualizzare un report contenente un'analisi dei dati.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-159">At this point, hello profiler stops executing, saves data in a .vsp file, and displays a report that shows an analysis of this data.</span></span>

![Report del profiler][11]

<span data-ttu-id="6d3d8-161">Se viene visualizzato String.wstrcpy in hello percorso ricorrente, fare clic su hello toochange Just My Code consente di visualizzare tooshow solo codice utente.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-161">If you see String.wstrcpy in hello Hot Path, click on Just My Code toochange hello view tooshow user code only.</span></span>  <span data-ttu-id="6d3d8-162">Se String. Concat, provare a pulsante Mostra tutto il codice hello.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-162">If you see String.Concat, try pressing hello Show All Code button.</span></span>

<span data-ttu-id="6d3d8-163">Si dovrebbe essere metodo Concatenate hello e String. Concat occupando gran parte del tempo di esecuzione hello.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-163">You should see hello Concatenate method and String.Concat taking up a large portion of hello execution time.</span></span>

![Analisi del report][12]

<span data-ttu-id="6d3d8-165">Se è stato aggiunto codice concatenazione di stringa hello in questo articolo, si verrà visualizzato un avviso in hello elenco attività per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-165">If you added hello string concatenation code in this article, you should see a warning in hello Task List for this.</span></span> <span data-ttu-id="6d3d8-166">È inoltre possibile visualizzare un avviso che vi sia una quantità eccessiva di garbage collection, ovvero a causa di toohello numero di stringhe che vengono creati ed eliminato.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-166">You may also see a warning that there is an excessive amount of garbage collection, which is due toohello number of strings that are created and disposed.</span></span>

![Avvisi di prestazioni][14]

## <a name="4-make-changes-and-compare-performance"></a><span data-ttu-id="6d3d8-168">4: Apportare modifiche e confrontare le prestazioni</span><span class="sxs-lookup"><span data-stu-id="6d3d8-168">4: Make changes and compare performance</span></span>
<span data-ttu-id="6d3d8-169">È inoltre possibile confrontare le prestazioni di hello prima e dopo una modifica del codice.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-169">You can also compare hello performance before and after a code change.</span></span>  <span data-ttu-id="6d3d8-170">Arresta esecuzione processo hello e modificare hello codice tooreplace hello stringa operazione di concatenazione con utilizzo hello di StringBuilder:</span><span class="sxs-lookup"><span data-stu-id="6d3d8-170">Stop hello running process, and edit hello code tooreplace hello string concatenation operation with hello use of StringBuilder:</span></span>

    public static string Concatenate(int number)
    {
        int count;
        System.Text.StringBuilder builder = new System.Text.StringBuilder("");
        for (count = 0; count < number; count++)
        {
             builder.Append("\n" + count.ToString());
        }
        return builder.ToString();
    }

<span data-ttu-id="6d3d8-171">Eseguire un'altra esecuzione sulle prestazioni e quindi confrontare le prestazioni di hello.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-171">Do another performance run, and then compare hello performance.</span></span> <span data-ttu-id="6d3d8-172">In Esplora prestazioni hello, se hello esecuzioni sono in hello stessa sessione, è solo possibile selezionare entrambi i report, aprire il menu di scelta rapida hello e scegliere **Confronta report di prestazioni**.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-172">In hello Performance Explorer, if hello runs are in hello same session, you can just select both reports, open hello shortcut menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="6d3d8-173">Se si desidera toocompare con un'esecuzione in un'altra sessione di prestazioni, aprire hello **Analizza** menu, scegliere **Confronta report di prestazioni**.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-173">If you want toocompare with a run in another performance session, open hello **Analyze** menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="6d3d8-174">Specificare entrambi i file nella finestra di dialogo hello visualizzata.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-174">Specify both files in hello dialog box that appears.</span></span>

![Opzione Confronta report di prestazioni][15]

<span data-ttu-id="6d3d8-176">i report di Hello evidenziare le differenze tra due esecuzioni hello.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-176">hello reports highlight differences between hello two runs.</span></span>

![Report di confronto][16]

<span data-ttu-id="6d3d8-178">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-178">Congratulations!</span></span> <span data-ttu-id="6d3d8-179">È stato avviato con il profiler di hello.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-179">You've gotten started with hello profiler.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="6d3d8-180">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="6d3d8-180">Troubleshooting</span></span>
* <span data-ttu-id="6d3d8-181">Assicurarsi di eseguire la profilatura di una compilazione di rilascio e avviarla senza eseguire il debug.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-181">Make sure you are profiling a Release build and start without debugging.</span></span>
* <span data-ttu-id="6d3d8-182">Se l'opzione di collegamento/scollegamento hello non è abilitato nel menu di Profiler hello, eseguire hello procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-182">If hello Attach/Detach option is not enabled on hello Profiler menu, run hello Performance Wizard.</span></span>
* <span data-ttu-id="6d3d8-183">Utilizzare hello interfaccia utente dell'emulatore di calcolo tooview hello lo stato dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-183">Use hello Compute Emulator UI tooview hello status of your application.</span></span> 
* <span data-ttu-id="6d3d8-184">Se si verificano problemi durante l'avvio delle applicazioni nell'emulatore hello o associare hello profiler, arrestare l'emulatore di calcolo hello e riavviarlo.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-184">If you have problems starting applications in hello emulator, or attaching hello profiler, shut down hello compute emulator and restart it.</span></span> <span data-ttu-id="6d3d8-185">Se non viene risolto il problema di hello, provare a riavviare.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-185">If that doesn't solve hello problem, try rebooting.</span></span> <span data-ttu-id="6d3d8-186">Questo problema può verificarsi se si utilizza toosuspend emulatore di calcolo hello e rimuovere le distribuzioni in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-186">This problem can occur if you use hello Compute Emulator toosuspend and remove running deployments.</span></span>
* <span data-ttu-id="6d3d8-187">Se è stato utilizzato uno dei comandi dalla riga di comando di profilatura hello, soprattutto hello impostazioni globali, assicurarsi che sia stato chiamato VSPerfClrEnv /globaloff e che VsPerfMon.exe è stato arrestato.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-187">If you have used any of hello profiling commands from the command line, especially hello global settings, make sure that VSPerfClrEnv /globaloff has been called and that VsPerfMon.exe has been shut down.</span></span>
* <span data-ttu-id="6d3d8-188">Se durante il campionamento, viene visualizzato il messaggio hello "PRF0025: è stato raccolto alcun dato," verificare che hello processo allegato attività toohas della CPU.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-188">If when sampling, you see hello message "PRF0025: No data was collected," check that hello process you attached toohas CPU activity.</span></span> <span data-ttu-id="6d3d8-189">È possibile che le applicazioni che non eseguono attività di calcolo non producano dati di campionamento.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-189">Applications that are not doing any computational work might not produce any sampling data.</span></span>  <span data-ttu-id="6d3d8-190">È anche possibile hello terminata prima che qualsiasi campionamento è stato eseguito.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-190">It's also possible that hello process exited before any sampling was done.</span></span> <span data-ttu-id="6d3d8-191">Controllare toosee che non termina il metodo Run hello per un ruolo che si esegue la profilatura.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-191">Check toosee that hello Run method for a role that you are profiling does not terminate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d3d8-192">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6d3d8-192">Next Steps</span></span>
<span data-ttu-id="6d3d8-193">Strumentazione di binari Azure nell'emulatore hello non è supportata nel profiler di Visual Studio hello, ma se si desidera tootest l'allocazione della memoria, è possibile selezionare l'opzione durante l'analisi.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-193">Instrumenting Azure binaries in hello emulator is not supported in hello Visual Studio profiler, but if you want tootest memory allocation, you can choose that option when profiling.</span></span> <span data-ttu-id="6d3d8-194">È anche possibile scegliere la profilatura della concorrenza, che consente di determinare se sono un inutile consumo di thread concorrenti ora per i blocchi o profilatura di interazione tra livelli consente di tenere traccia dei problemi di prestazioni durante l'interazione tra livelli di un'applicazione, più spesso tra il livello di dati hello e un ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-194">You can also choose concurrency profiling, which helps you determine whether threads are wasting time competing for locks, or tier interaction profiling, which helps you track down performance problems when interacting between tiers of an application, most frequently between hello data tier and a worker role.</span></span>  <span data-ttu-id="6d3d8-195">È possibile visualizzare le query di database hello che genera l'app e usare hello l'utilizzo del database hello tooimprove dati di profilatura.</span><span class="sxs-lookup"><span data-stu-id="6d3d8-195">You can view hello database queries that your app generates and use hello profiling data tooimprove your use of hello database.</span></span> <span data-ttu-id="6d3d8-196">Per informazioni sulla profilatura interazione tra livelli, vedere hello post di blog [procedura dettagliata: utilizzo di Profiler di interazione tra livelli in Visual Studio Team System 2010 hello][3].</span><span class="sxs-lookup"><span data-stu-id="6d3d8-196">For information about tier interaction profiling, see hello blog post [Walkthrough: Using hello Tier Interaction Profiler in Visual Studio Team System 2010][3].</span></span>

[1]: http://msdn.microsoft.com/library/azure/hh369930.aspx
[2]: http://msdn.microsoft.com/library/azure/hh411542.aspx
[3]: http://blogs.msdn.com/b/habibh/archive/2009/06/30/walkthrough-using-the-tier-interaction-profiler-in-visual-studio-team-system-2010.aspx
[4]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally09.png
[5]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally10.png
[6]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally02.png
[7]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally05.png
[8]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally010.png
[9]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally07.png
[10]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally06.png
[11]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally03.png
[12]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally011.png
[14]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally04.png 
[15]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally013.png
[16]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally012.png
[17]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally08.png
