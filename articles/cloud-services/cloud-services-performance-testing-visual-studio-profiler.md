---
title: Profilatura di un servizio cloud in locale nell'emulatore di calcolo | Documentazione Microsoft
services: cloud-services
description: Analizzare i problemi di prestazioni nei servizi cloud con il profiler di Visual Studio
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
ms.openlocfilehash: 51c8192d8312dc5cf546b4c357aeecf6f19d56b8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="testing-the-performance-of-a-cloud-service-locally-in-the-azure-compute-emulator-using-the-visual-studio-profiler"></a><span data-ttu-id="ce2c6-103">Test locale delle prestazioni di un servizio cloud nell'emulatore di calcolo di Azure mediante il profiler di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ce2c6-103">Testing the Performance of a Cloud Service Locally in the Azure Compute Emulator Using the Visual Studio Profiler</span></span>
<span data-ttu-id="ce2c6-104">È possibile usare diversi strumenti e tecniche per il test delle prestazioni di servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-104">A variety of tools and techniques are available for testing the performance of cloud services.</span></span>
<span data-ttu-id="ce2c6-105">Quando si pubblica un servizio cloud in Azure, è possibile impostare Visual Studio per la raccolta di dati di profilatura e quindi per l'analisi locale di tali dati, come illustrato in [Profilatura di un'applicazione di Azure][1].</span><span class="sxs-lookup"><span data-stu-id="ce2c6-105">When you publish a cloud service to Azure, you can have Visual Studio collect profiling data and then analyze it locally, as described in [Profiling an Azure Application][1].</span></span>
<span data-ttu-id="ce2c6-106">È anche possibile usare gli strumenti di diagnostica per tenere traccia di diversi contatori delle prestazioni, come illustrato in [Uso dei contatori delle prestazioni in Azure][2].</span><span class="sxs-lookup"><span data-stu-id="ce2c6-106">You can also use diagnostics to track a variety of performance counters, as described in [Using performance counters in Azure][2].</span></span>
<span data-ttu-id="ce2c6-107">È inoltre consigliabile eseguire localmente la profilatura dell'applicazione nell'emulatore di calcolo prima di distribuirla nel cloud.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-107">You might also want to profile your application locally in the compute emulator before deploying it to the cloud.</span></span>

<span data-ttu-id="ce2c6-108">In questo articolo viene illustrato il metodo Campionamento CPU per la profilatura, che può essere eseguito localmente nell'emulatore.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-108">This article covers the CPU Sampling method of profiling, which can be done locally in the emulator.</span></span> <span data-ttu-id="ce2c6-109">Si tratta di un metodo di profilatura non eccessivamente invasivo.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-109">CPU sampling is a method of profiling that is not very intrusive.</span></span> <span data-ttu-id="ce2c6-110">Il profiler salva uno snapshot dello stack di chiamate in base a intervalli di campionamento specificati.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-110">At a designated sampling interval, the profiler takes a snapshot of the call stack.</span></span> <span data-ttu-id="ce2c6-111">I dati vengono raccolti per un determinato periodo di tempo e vengono visualizzati in un rapporto.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-111">The data is collected over a period of time, and shown in a report.</span></span> <span data-ttu-id="ce2c6-112">Questo metodo di profilatura tende a indicare la posizione in cui viene eseguita la maggior parte del lavoro della CPU in un'applicazione a elevato utilizzo di calcolo.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-112">This method of profiling tends to indicate where in a computationally intensive application most of the CPU work is being done.</span></span>  <span data-ttu-id="ce2c6-113">Ciò consente di focalizzare l'attenzione sul "percorso critico" in cui l'applicazione trascorre la maggior parte del tempo.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-113">This gives you the opportunity to focus on the "hot path" where your application is spending the most time.</span></span>

## <a name="1-configure-visual-studio-for-profiling"></a><span data-ttu-id="ce2c6-114">1: Configurare Visual Studio per la profilatura</span><span class="sxs-lookup"><span data-stu-id="ce2c6-114">1: Configure Visual Studio for profiling</span></span>
<span data-ttu-id="ce2c6-115">Visual Studio include alcune opzioni di configurazione che possono risultare utili per la profilatura.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-115">First, there are a few Visual Studio configuration options that might be helpful when profiling.</span></span> <span data-ttu-id="ce2c6-116">Per rendere comprensibili i rapporti di profilatura, saranno necessari simboli (file con estensione pdb) per l'applicazione, oltre a simboli per le librerie di sistema.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-116">To make sense of the profiling reports, you'll need symbols (.pdb files) for your application and also symbols for system libraries.</span></span> <span data-ttu-id="ce2c6-117">È necessario assicurarsi di fare riferimento ai server dei simboli disponibili.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-117">You'll want to make sure that you reference the available symbol servers.</span></span> <span data-ttu-id="ce2c6-118">A tale scopo, dal menu **Strumenti** in Visual Studio scegliere **Opzioni**, quindi **Debug** e infine **Simboli**.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-118">To do this, on the **Tools** menu in Visual Studio, choose **Options**, then choose **Debugging**, then **Symbols**.</span></span> <span data-ttu-id="ce2c6-119">Verificare che Server dei simboli Microsoft sia elencato in **Percorsi dei file di simboli (pdb)**.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-119">Make sure that Microsoft Symbol Servers is listed under **Symbol file (.pdb) locations**.</span></span>  <span data-ttu-id="ce2c6-120">È inoltre possibile fare riferimento a http://referencesource.microsoft.com/symbols, dove potrebbero essere disponibili file di simboli aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-120">You can also reference http://referencesource.microsoft.com/symbols, which might have additional symbol files.</span></span>

![Opzioni dei simboli][4]

<span data-ttu-id="ce2c6-122">Se lo si desidera, è possibile semplificare i rapporti generati dal profiler impostando Just My Code.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-122">If desired, you can simplify the reports that the profiler generates by setting Just My Code.</span></span> <span data-ttu-id="ce2c6-123">Se Just My Code è abilitato, gli stack di chiamate funzione vengono semplificati, in modo che le chiamate interamente interne alle librerie e a .NET Framework non vengano visualizzate nei rapporti.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-123">With Just My Code enabled, function call stacks are simplified so that calls entirely internal to libraries and the .NET Framework are hidden from the reports.</span></span> <span data-ttu-id="ce2c6-124">Scegliere **Opzioni** dal menu **Strumenti**.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-124">On the **Tools** menu, choose **Options**.</span></span> <span data-ttu-id="ce2c6-125">Espandere quindi il nodo **Strumenti per le prestazioni** e scegliere **Generale**.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-125">Then expand the **Performance Tools** node, and choose **General**.</span></span> <span data-ttu-id="ce2c6-126">Selezionare la casella di controllo **Abilita Just My Code per i rapporti del profiler**.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-126">Select the checkbox for **Enable Just My Code for profiler reports**.</span></span>

![Opzioni di Just My Code][17]

<span data-ttu-id="ce2c6-128">Queste istruzioni sono applicabili a un progetto esistente o a un nuovo progetto.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-128">You can use these instructions with an existing project or with a new project.</span></span>  <span data-ttu-id="ce2c6-129">Se si crea un nuovo progetto per provare ad applicare le tecniche illustrate di seguito, scegliere un progetto **Servizio cloud di Azure** in C# e quindi selezionare un **ruolo Web** e un **ruolo di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-129">If you create a new project to try the techniques described below, choose a C# **Azure Cloud Service** project, and select a **Web Role** and a **Worker Role**.</span></span>

![Ruoli del progetto Servizi cloud di Azure][5]

<span data-ttu-id="ce2c6-131">A scopo esemplificativo, aggiungere al progetto codice la cui esecuzione richiede molto tempo e che illustri alcuni problemi ovvi relativi alle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-131">For example purposes, add some code to your project that takes a lot of time and demonstrates some obvious performance problem.</span></span> <span data-ttu-id="ce2c6-132">Aggiungere ad esempio il codice seguente a un progetto di tipo ruolo di lavoro:</span><span class="sxs-lookup"><span data-stu-id="ce2c6-132">For example, add the following code to a worker role project:</span></span>

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

<span data-ttu-id="ce2c6-133">Chiamare tale codice dal metodo RunAsync nella classe del ruolo di lavoro derivata da RoleEntryPoint.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-133">Call this code from the RunAsync method in the worker role's RoleEntryPoint-derived class.</span></span> <span data-ttu-id="ce2c6-134">(Ignorare l'avviso relativo al metodo eseguito in modalità sincrona).</span><span class="sxs-lookup"><span data-stu-id="ce2c6-134">(Ignore the warning about the method running synchronously.)</span></span>

        private async Task RunAsync(CancellationToken cancellationToken)
        {
            // TODO: Replace the following with your own logic.
            while (!cancellationToken.IsCancellationRequested)
            {
                Trace.TraceInformation("Working");
                Concatenator.Concatenate(10000);
            }
        }

<span data-ttu-id="ce2c6-135">Compilare ed eseguire localmente il servizio cloud senza eseguire il debug (CTRL+F5) con la configurazione della soluzione impostata su **Release**.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-135">Build and run your cloud service locally without debugging (Ctrl+F5), with the solution configuration set to **Release**.</span></span> <span data-ttu-id="ce2c6-136">In tale modo, tutti i file e le cartelle verranno creati per l'esecuzione locale dell'applicazione e tutti gli emulatori verranno avviati.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-136">This ensures that all files and folders are created for running the application locally, and ensures that all the emulators are started.</span></span> <span data-ttu-id="ce2c6-137">Avviare l'interfaccia utente dell'emulatore di calcolo dalla barra delle applicazioni per verificare che il ruolo di lavoro sia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-137">Start the Compute Emulator UI from the taskbar to verify that your worker role is running.</span></span>

## <a name="2-attach-to-a-process"></a><span data-ttu-id="ce2c6-138">2: Connettersi a un processo</span><span class="sxs-lookup"><span data-stu-id="ce2c6-138">2: Attach to a process</span></span>
<span data-ttu-id="ce2c6-139">Invece di eseguire la profilatura dell'applicazione avviandola dall'IDE di Visual Studio 2010, è necessario connettere il profiler a un processo in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-139">Instead of profiling the application by starting it from the Visual Studio 2010 IDE, you must attach the profiler to a running process.</span></span> 

<span data-ttu-id="ce2c6-140">A tale scopo, scegliere **Profiler** dal menu **Analizza**, quindi fare clic su **Connetti/Disconnetti**.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-140">To attach the profiler to a process, on the **Analyze** menu, choose **Profiler** and **Attach/Detach**.</span></span>

![Opzione per il collegamento del profilo][6]

<span data-ttu-id="ce2c6-142">Per un ruolo di lavoro individuare il processo WaWorkerHost.exe.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-142">For a worker role, find the WaWorkerHost.exe process.</span></span>

![Processo WaWorkerHost][7]

<span data-ttu-id="ce2c6-144">Se la cartella del progetto si trova su un'unità di rete, il profiler richiederà di specificare un percorso diverso per il salvataggio dei rapporti di profilatura.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-144">If your project folder is on a network drive, the profiler will ask you to provide another location to save the profiling reports.</span></span>

 <span data-ttu-id="ce2c6-145">È anche possibile connettersi a un ruolo Web mediante la connessione a WaIISHost.exe.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-145">You can also attach to a web role by attaching to WaIISHost.exe.</span></span>
<span data-ttu-id="ce2c6-146">Se l'applicazione include più processi di ruolo di lavoro, sarà necessario usare il valore processID per distinguerli.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-146">If there are multiple worker role processes in your application, you need to use the processID to distinguish them.</span></span> <span data-ttu-id="ce2c6-147">È possibile eseguire query relative ai valori processID a livello di codice, mediante l'accesso all'oggetto Process.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-147">You can query the processID programmatically by accessing the Process object.</span></span> <span data-ttu-id="ce2c6-148">Se, ad esempio, si aggiunge il codice seguente al metodo Run della classe derivata da RoleEntryPoint in un ruolo, sarà possibile esaminare il log nell'interfaccia utente dell'emulatore di calcolo per individuare i processi a cui connettersi.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-148">For example, if you add this code to the Run method of the RoleEntryPoint-derived class in a role, you can look at the log in the Compute Emulator UI to know what process to connect to.</span></span>

    var process = System.Diagnostics.Process.GetCurrentProcess();
    var message = String.Format("Process ID: {0}", process.Id);
    Trace.WriteLine(message, "Information");

<span data-ttu-id="ce2c6-149">Per visualizzare il log, avviare l'interfaccia utente dell'emulatore di calcolo.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-149">To view the log, start the Compute Emulator UI.</span></span>

![Avviare l'interfaccia utente dell'emulatore di calcolo][8]

<span data-ttu-id="ce2c6-151">Aprire la finestra della console del log del ruolo di lavoro nell'interfaccia utente dell'emulatore di calcolo, facendo clic sulla barra del titolo nella finestra della console.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-151">Open the worker role log console window in the Compute Emulator UI by clicking on the console window's title bar.</span></span> <span data-ttu-id="ce2c6-152">Nel log è possibile verificare l'ID dei processi.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-152">You can see the process ID in the log.</span></span>

![Visualizzare l'ID processo][9]

<span data-ttu-id="ce2c6-154">Dopo la connessione, eseguire la procedura nell'interfaccia utente dell'applicazione, se necessario, per riprodurre lo scenario.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-154">One you've attached, perform the steps in your application's UI (if needed) to reproduce the scenario.</span></span>

<span data-ttu-id="ce2c6-155">Per interrompere la profilatura, scegliere il collegamento **Interrompi la profilatura** .</span><span class="sxs-lookup"><span data-stu-id="ce2c6-155">When you want to stop profiling, choose the **Stop Profiling** link.</span></span>

![Opzione Arresta profilatura][10]

## <a name="3-view-performance-reports"></a><span data-ttu-id="ce2c6-157">3: Visualizzare i rapporti relativi alle prestazioni</span><span class="sxs-lookup"><span data-stu-id="ce2c6-157">3: View performance reports</span></span>
<span data-ttu-id="ce2c6-158">Viene visualizzato il rapporto relativo alle prestazioni dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-158">The performance report for your application is displayed.</span></span>

<span data-ttu-id="ce2c6-159">A questo punto, l'esecuzione del profiler viene interrotta, i dati vengono salvati in un file con estensione vsp e viene visualizzato un rapporto che include un'analisi di tali dati.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-159">At this point, the profiler stops executing, saves data in a .vsp file, and displays a report that shows an analysis of this data.</span></span>

![Report del profiler][11]

<span data-ttu-id="ce2c6-161">Se nel percorso critico è visibile il file String.wstrcpy, fare clic su Just My Code per modificare la visualizzazione, in modo da mostrare solo il codice utente.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-161">If you see String.wstrcpy in the Hot Path, click on Just My Code to change the view to show user code only.</span></span>  <span data-ttu-id="ce2c6-162">Se è visualizzato String.Concat, provare a selezionare il pulsante Mostra tutto il codice.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-162">If you see String.Concat, try pressing the Show All Code button.</span></span>

<span data-ttu-id="ce2c6-163">Come si può notare, il metodo Concatenate e String.Concat richiedono una parte significativa del tempo di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-163">You should see the Concatenate method and String.Concat taking up a large portion of the execution time.</span></span>

![Analisi del report][12]

<span data-ttu-id="ce2c6-165">Se è stato aggiunto il codice di concatenazione di stringa disponibile in questo articolo, nell'Elenco attività dovrebbe essere visualizzato un avviso corrispondente.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-165">If you added the string concatenation code in this article, you should see a warning in the Task List for this.</span></span> <span data-ttu-id="ce2c6-166">È anche possibile che venga visualizzato un avviso relativo a una quantità eccessiva di Garbage Collection, dovuta al numero di stringhe eliminate.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-166">You may also see a warning that there is an excessive amount of garbage collection, which is due to the number of strings that are created and disposed.</span></span>

![Avvisi di prestazioni][14]

## <a name="4-make-changes-and-compare-performance"></a><span data-ttu-id="ce2c6-168">4: Apportare modifiche e confrontare le prestazioni</span><span class="sxs-lookup"><span data-stu-id="ce2c6-168">4: Make changes and compare performance</span></span>
<span data-ttu-id="ce2c6-169">È anche possibile confrontare le prestazioni prima e dopo la modifica del codice.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-169">You can also compare the performance before and after a code change.</span></span>  <span data-ttu-id="ce2c6-170">Arrestare il processo in esecuzione e modificare il codice per sostituire l'operazione di concatenazione di stringa usando StringBuilder:</span><span class="sxs-lookup"><span data-stu-id="ce2c6-170">Stop the running process, and edit the code to replace the string concatenation operation with the use of StringBuilder:</span></span>

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

<span data-ttu-id="ce2c6-171">Eseguire di nuovo la verifica delle prestazioni e quindi confrontare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-171">Do another performance run, and then compare the performance.</span></span> <span data-ttu-id="ce2c6-172">Se le esecuzioni si trovano nella stessa sessione, in Esplora prestazioni è possibile selezionare entrambi i rapporti, aprire il menu di scelta rapida e quindi scegliere **Confronta rapporto di prestazioni**.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-172">In the Performance Explorer, if the runs are in the same session, you can just select both reports, open the shortcut menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="ce2c6-173">Per effettuare un confronto con un'esecuzione in un'altra sessione relativa alle prestazioni, aprire il menu **Analizza** e quindi scegliere **Confronta rapporto di prestazioni**.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-173">If you want to compare with a run in another performance session, open the **Analyze** menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="ce2c6-174">Specificare entrambi i file nella casella della finestra di dialogo visualizzata.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-174">Specify both files in the dialog box that appears.</span></span>

![Opzione Confronta report di prestazioni][15]

<span data-ttu-id="ce2c6-176">Nei rapporti vengono evidenziate le differenze tra le due esecuzioni.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-176">The reports highlight differences between the two runs.</span></span>

![Report di confronto][16]

<span data-ttu-id="ce2c6-178">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-178">Congratulations!</span></span> <span data-ttu-id="ce2c6-179">sono state eseguite le operazioni preliminari con il profiler.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-179">You've gotten started with the profiler.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="ce2c6-180">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="ce2c6-180">Troubleshooting</span></span>
* <span data-ttu-id="ce2c6-181">Assicurarsi di eseguire la profilatura di una compilazione di rilascio e avviarla senza eseguire il debug.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-181">Make sure you are profiling a Release build and start without debugging.</span></span>
* <span data-ttu-id="ce2c6-182">Se l'opzione Connetti/Disconnetti non è abilitata nel menu Profiler, eseguire la Creazione guidata sessione di prestazioni.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-182">If the Attach/Detach option is not enabled on the Profiler menu, run the Performance Wizard.</span></span>
* <span data-ttu-id="ce2c6-183">Usare l'interfaccia utente dell'emulatore di calcolo per visualizzare lo stato dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-183">Use the Compute Emulator UI to view the status of your application.</span></span> 
* <span data-ttu-id="ce2c6-184">Se si verificano problemi di avvio delle applicazioni nell'emulatore o problemi di connessione del profiler, arrestare l'emulatore di calcolo e riavviarlo.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-184">If you have problems starting applications in the emulator, or attaching the profiler, shut down the compute emulator and restart it.</span></span> <span data-ttu-id="ce2c6-185">Se il problema persiste, provare a riavviare il sistema.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-185">If that doesn't solve the problem, try rebooting.</span></span> <span data-ttu-id="ce2c6-186">È possibile che questo problema si verifichi se si usa l'emulatore di calcolo per sospendere e rimuovere distribuzioni in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-186">This problem can occur if you use the Compute Emulator to suspend and remove running deployments.</span></span>
* <span data-ttu-id="ce2c6-187">Se sono stati usati comandi relativi alla profilatura dalla riga di comando, in particolare le impostazioni globali, assicurarsi che sia stata effettuata la chiamata a VSPerfClrEnv /globaloff e che VsPerfMon.exe sia stato arrestato.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-187">If you have used any of the profiling commands from the command line, especially the global settings, make sure that VSPerfClrEnv /globaloff has been called and that VsPerfMon.exe has been shut down.</span></span>
* <span data-ttu-id="ce2c6-188">Se durante il campionamento viene visualizzato il messaggio "PRF0025: Dati non raccolti", verificare che nel processo a cui ci si è connessi sia presente attività della CPU.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-188">If when sampling, you see the message "PRF0025: No data was collected," check that the process you attached to has CPU activity.</span></span> <span data-ttu-id="ce2c6-189">È possibile che le applicazioni che non eseguono attività di calcolo non producano dati di campionamento.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-189">Applications that are not doing any computational work might not produce any sampling data.</span></span>  <span data-ttu-id="ce2c6-190">È inoltre possibile che il processo sia stato chiuso prima dell'esecuzione del campionamento.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-190">It's also possible that the process exited before any sampling was done.</span></span> <span data-ttu-id="ce2c6-191">Verificare che il metodo Run di un ruolo da sottoporre a profilatura non preveda la terminazione.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-191">Check to see that the Run method for a role that you are profiling does not terminate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce2c6-192">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ce2c6-192">Next Steps</span></span>
<span data-ttu-id="ce2c6-193">La strumentazione dei file binari di Azure nell'emulatore non è supportata nel profiler di Visual Studio. Se tuttavia si desidera testare l'allocazione della memoria, è possibile scegliere tale opzione durante la profilatura.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-193">Instrumenting Azure binaries in the emulator is not supported in the Visual Studio profiler, but if you want to test memory allocation, you can choose that option when profiling.</span></span> <span data-ttu-id="ce2c6-194">È inoltre possibile scegliere la profilatura della concorrenza, che consente di determinare se i thread sprecano tempo nel tentativo di ottenere blocchi, oppure la profilatura di interazioni tra livelli, che consente di tenere traccia dei problemi di prestazioni durante l'interazione tra livelli di un'applicazione, nella maggior parte dei casi tra il livello dati e il ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-194">You can also choose concurrency profiling, which helps you determine whether threads are wasting time competing for locks, or tier interaction profiling, which helps you track down performance problems when interacting between tiers of an application, most frequently between the data tier and a worker role.</span></span>  <span data-ttu-id="ce2c6-195">È possibile visualizzare le query di database generate dall'applicazione e usare i dati di profilatura per ottimizzare l'uso del database.</span><span class="sxs-lookup"><span data-stu-id="ce2c6-195">You can view the database queries that your app generates and use the profiling data to improve your use of the database.</span></span> <span data-ttu-id="ce2c6-196">Per informazioni sulla profilatura dell'interazione tra livelli, vedere il post di blog [Walkthrough: Using the Tier Interaction Profiler in Visual Studio Team System 2010][3] (Procedura dettagliata: Uso del profiler relativo alle interazioni tra livelli in Visual Studio Team System 2010).</span><span class="sxs-lookup"><span data-stu-id="ce2c6-196">For information about tier interaction profiling, see the blog post [Walkthrough: Using the Tier Interaction Profiler in Visual Studio Team System 2010][3].</span></span>

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
