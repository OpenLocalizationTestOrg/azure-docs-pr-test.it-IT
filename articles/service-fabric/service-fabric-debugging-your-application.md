---
title: Debug dell'applicazione in Visual Studio | Documentazione Microsoft
description: "Migliorare l'affidabilità e le prestazioni dei servizi sviluppandoli ed eseguendone il debug in Visual Studio all'interno di un cluster di sviluppo locale."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: cb888532-bcdb-4e47-95e4-bfbb1f644da4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: 2459025899a7f5ffebf44fa104ed112c0eb99dfa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="debug-your-service-fabric-application-by-using-visual-studio"></a><span data-ttu-id="2ea09-103">Debug dell'applicazione di Service Fabric mediante Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2ea09-103">Debug your Service Fabric application by using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2ea09-104">Visual Studio/CSharp</span><span class="sxs-lookup"><span data-stu-id="2ea09-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="2ea09-105">Eclipse/Java</span><span class="sxs-lookup"><span data-stu-id="2ea09-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
>


## <a name="debug-a-local-service-fabric-application"></a><span data-ttu-id="2ea09-106">Eseguire il debug di un'applicazione di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2ea09-106">Debug a local Service Fabric application</span></span>
<span data-ttu-id="2ea09-107">Per risparmiare tempo e denaro, è possibile distribuire l'applicazione di Service Fabric ed eseguirne il debug in un cluster di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="2ea09-107">You can save time and money by deploying and debugging your Azure Service Fabric application in a local computer development cluster.</span></span> <span data-ttu-id="2ea09-108">Visual Studio 2017 o Visual Studio 2015 può distribuire l'applicazione nel cluster locale e connettere automaticamente il debugger a tutte le istanze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2ea09-108">Visual Studio 2017 or Visual Studio 2015 can deploy the application to the local cluster and automatically connect the debugger to all instances of your application.</span></span>

1. <span data-ttu-id="2ea09-109">Avviare un cluster di sviluppo locale seguendo la procedura descritta nell'articolo [Configurazione dell'ambiente di sviluppo di Service Fabric](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2ea09-109">Start a local development cluster by following the steps in [Setting up your Service Fabric development environment](service-fabric-get-started.md).</span></span>
2. <span data-ttu-id="2ea09-110">Premere **F5** oppure fare clic su **Debug** > **Avvia debug**.</span><span class="sxs-lookup"><span data-stu-id="2ea09-110">Press **F5** or click **Debug** > **Start Debugging**.</span></span>
   
    ![Avviare il debug di un'applicazione][startdebugging]
3. <span data-ttu-id="2ea09-112">Impostare i punti di interruzione nel codice ed eseguire l'applicazione un'istruzione alla volta scegliendo i comandi dal menu **Debug** .</span><span class="sxs-lookup"><span data-stu-id="2ea09-112">Set breakpoints in your code and step through the application by clicking commands in the **Debug** menu.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2ea09-113">Visual Studio si connette a tutte le istanze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2ea09-113">Visual Studio attaches to all instances of your application.</span></span> <span data-ttu-id="2ea09-114">Mentre il codice viene eseguito un'istruzione alla volta, i punti di interruzione possono essere raggiunti da più processi, dando luogo a sessioni simultanee.</span><span class="sxs-lookup"><span data-stu-id="2ea09-114">While you're stepping through code, breakpoints may get hit by multiple processes resulting in concurrent sessions.</span></span> <span data-ttu-id="2ea09-115">Provare a disabilitare i punti di interruzione dopo che sono stati raggiunti rendendoli condizionali in base all'ID del thread, oppure usando gli eventi di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="2ea09-115">Try disabling the breakpoints after they're hit, by making each breakpoint conditional on the thread ID or by using diagnostic events.</span></span>
   > 
   > 
4. <span data-ttu-id="2ea09-116">La finestra degli **eventi di diagnostica** si aprirà automaticamente per visualizzare gli eventi diagnostici in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="2ea09-116">The **Diagnostic Events** window will automatically open so you can view diagnostic events in real time.</span></span>
   
    ![Visualizzare gli eventi diagnostici in tempo reale][diagnosticevents]
5. <span data-ttu-id="2ea09-118">È possibile aprire la finestra **degli** eventi di diagnostica anche in Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="2ea09-118">You can also open the **Diagnostic Events** window in Cloud Explorer.</span></span>  <span data-ttu-id="2ea09-119">In **Service Fabric** fare clic con il pulsante destro del mouse e scegliere **Visualizza tracce streaming**.</span><span class="sxs-lookup"><span data-stu-id="2ea09-119">Under **Service Fabric**, right-click any node and choose **View Streaming Traces**.</span></span>
   
    ![Aprire la finestra degli eventi di diagnostica][viewdiagnosticevents]
   
    <span data-ttu-id="2ea09-121">Se si vuole filtrare le tracce in un'applicazione o in un servizio, è sufficiente abilitare le tracce di streaming in tale applicazione o servizio.</span><span class="sxs-lookup"><span data-stu-id="2ea09-121">If you want to filter your traces to a specific service or application, simply enable streaming traces on that specific service or application.</span></span>
6. <span data-ttu-id="2ea09-122">Gli eventi diagnostici possono essere visualizzati nel file **ServiceEventSource.cs** generato automaticamente e vengono chiamati dal codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2ea09-122">The diagnostic events can be seen in the automatically generated **ServiceEventSource.cs** file and are called from application code.</span></span>
   
    ```csharp
    ServiceEventSource.Current.ServiceMessage(this, "My ServiceMessage with a parameter {0}", result.Value.ToString());
    ```
7. <span data-ttu-id="2ea09-123">Nella finestra **degli**eventi di diagnostica è possibile filtrare, sospendere ed esaminare eventi in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="2ea09-123">The **Diagnostic Events** window supports filtering, pausing, and inspecting events in real time.</span></span>  <span data-ttu-id="2ea09-124">Il filtro è una semplice ricerca di stringhe del messaggio dell'evento, incluso il relativo contenuto.</span><span class="sxs-lookup"><span data-stu-id="2ea09-124">The filter is a simple string search of the event message, including its contents.</span></span>
   
    ![Filtrare, sospendere e riprendere o esaminare eventi in tempo reale][diagnosticeventsactions]
8. <span data-ttu-id="2ea09-126">Il debug dei servizi è come il debug di qualsiasi altra applicazione.</span><span class="sxs-lookup"><span data-stu-id="2ea09-126">Debugging services is like debugging any other application.</span></span> <span data-ttu-id="2ea09-127">In genere i punti di interruzione vengono impostati tramite Visual Studio per semplificare il debug.</span><span class="sxs-lookup"><span data-stu-id="2ea09-127">You will normally set Breakpoints through Visual Studio for easy debugging.</span></span> <span data-ttu-id="2ea09-128">Anche se le raccolte Reliable Collections vengono replicate in più nodi, implementano comunque IEnumerable.</span><span class="sxs-lookup"><span data-stu-id="2ea09-128">Even though Reliable Collections replicate across multiple nodes, they still implement IEnumerable.</span></span> <span data-ttu-id="2ea09-129">Ciò significa che è possibile utilizzare la visualizzazione dei risultati in Visual Studio durante il debug per vedere cosa è stato memorizzato all'interno.</span><span class="sxs-lookup"><span data-stu-id="2ea09-129">This means that you can use the Results View in Visual Studio while debugging to see what you've stored inside.</span></span> <span data-ttu-id="2ea09-130">È sufficiente impostare un punto di interruzione in qualsiasi posizione all'interno del codice.</span><span class="sxs-lookup"><span data-stu-id="2ea09-130">Simply set a breakpoint anywhere in your code.</span></span>
   
    ![Avviare il debug di un'applicazione][breakpoint]

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->

## <a name="debug-a-remote-service-fabric-application"></a><span data-ttu-id="2ea09-132">Eseguire il debug di un'applicazione remota di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2ea09-132">Debug a remote Service Fabric application</span></span>
<span data-ttu-id="2ea09-133">Se le applicazioni di Service Fabric sono in esecuzione in un cluster di Service Fabric in Azure, è possibile eseguirne il debug remoto direttamente da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2ea09-133">If your Service Fabric applications are running on a Service Fabric cluster in Azure, you are able to remotely debug these, directly from Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="2ea09-134">La funzionalità richiede [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) e [Azure SDK per .NET 2.9](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="2ea09-134">The feature requires [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) and [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/).</span></span>    
> 
> 

<!-- -->
> [!WARNING]
> <span data-ttu-id="2ea09-135">Il debug remoto è progettato per scenari di sviluppo e test e non deve essere usato in ambienti di produzione a causa dell'impatto sulle applicazioni in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2ea09-135">Remote debugging is meant for dev/test scenarios and not to be used in production environments, because of the impact on the running applications.</span></span>
> 
> 

1. <span data-ttu-id="2ea09-136">Passare al cluster in **Cloud Explorer**, fare clic con il pulsante destro del mouse e scegliere **Abilita debug**</span><span class="sxs-lookup"><span data-stu-id="2ea09-136">Navigate to your cluster in **Cloud Explorer**, right-click and choose **Enable Debugging**</span></span>
   
    ![Abilitare il debug remoto][enableremotedebugging]
   
    <span data-ttu-id="2ea09-138">Verrà avviato il processo di abilitazione dell'estensione di debug remoto nei nodi del cluster e delle configurazioni di rete necessarie.</span><span class="sxs-lookup"><span data-stu-id="2ea09-138">This will kick off the process of enabling the remote debugging extension on your cluster nodes, as well as required network configurations.</span></span>
2. <span data-ttu-id="2ea09-139">Fare clic con il pulsante destro del mouse sul nodo del cluster in **Cloud Explorer** e scegliere **Associa debugger**</span><span class="sxs-lookup"><span data-stu-id="2ea09-139">Right-click the cluster node in **Cloud Explorer**, and choose **Attach Debugger**</span></span>
   
    ![Collega debugger][attachdebugger]
3. <span data-ttu-id="2ea09-141">Nella finestra di dialogo **Associa a processo** scegliere il processo di cui si vuole eseguire il debug e fare clic su **Collega**</span><span class="sxs-lookup"><span data-stu-id="2ea09-141">In the **Attach to process** dialog, choose the process you want to debug, and click **Attach**</span></span>
   
    ![Scegliere il processo][chooseprocess]
   
    <span data-ttu-id="2ea09-143">Il nome del processo a cui connettersi corrisponde al nome dell'assembly del progetto del servizio.</span><span class="sxs-lookup"><span data-stu-id="2ea09-143">The name of the process you want to attach to, equals the name of your service project assembly name.</span></span>
   
    <span data-ttu-id="2ea09-144">Il debugger si connetterà a tutti i nodi che eseguono il processo.</span><span class="sxs-lookup"><span data-stu-id="2ea09-144">The debugger will attach to all nodes running the process.</span></span>
   
   * <span data-ttu-id="2ea09-145">Se si esegue il debug di un servizio senza stato, tutte le istanze del servizio in tutti i nodi fanno parte della sessione di debug.</span><span class="sxs-lookup"><span data-stu-id="2ea09-145">In the case where you are debugging a stateless service, all instances of the service on all nodes are part of the debug session.</span></span>
   * <span data-ttu-id="2ea09-146">Se si esegue il debug di un servizio con stato, solo la replica primaria di qualsiasi partizione sarà attiva e quindi rilevata dal debugger.</span><span class="sxs-lookup"><span data-stu-id="2ea09-146">If you are debugging a stateful service, only the primary replica of any partition will be active and therefore caught by the debugger.</span></span> <span data-ttu-id="2ea09-147">Se la replica primaria viene spostata durante la sessione di debug, l'elaborazione di quella replica farà ancora parte della sessione di debug.</span><span class="sxs-lookup"><span data-stu-id="2ea09-147">If the primary replica moves during the debug session, the processing of that replica will still be part of the debug session.</span></span>
   * <span data-ttu-id="2ea09-148">Per rilevare solo le partizioni o istanze pertinenti di un determinato servizio, è possibile usare punti di interruzione condizionali per interrompere solo una specifica istanza o partizione.</span><span class="sxs-lookup"><span data-stu-id="2ea09-148">In order to only catch relevant partitions or instances of a given service, you can use conditional breakpoints to only break a specific partition or instance.</span></span>
     
     ![Punto di interruzione condizionale][conditionalbreakpoint]
     
     > [!NOTE]
     > <span data-ttu-id="2ea09-150">Attualmente non è supportato il debug di un cluster di Service Fabric con più istanze dello stesso nome di eseguibile del servizio.</span><span class="sxs-lookup"><span data-stu-id="2ea09-150">Currently we do not support debugging a Service Fabric cluster with multiple instances of the same service executable name.</span></span>
     > 
     > 
4. <span data-ttu-id="2ea09-151">Al termine del debug dell'applicazione è possibile disabilitare l'estensione di debug remoto facendo clic con il pulsante destro del mouse sul cluster in **Cloud Explorer** e scegliendo **Disabilita debug**</span><span class="sxs-lookup"><span data-stu-id="2ea09-151">Once you finish debugging your application, you can disable the remote debugging extension by right-clicking the cluster in **Cloud Explorer** and choose **Disable Debugging**</span></span>
   
    ![Disabilitare il debug remoto][disableremotedebugging]

## <a name="streaming-traces-from-a-remote-cluster-node"></a><span data-ttu-id="2ea09-153">Streaming delle tracce da un nodo del cluster remoto</span><span class="sxs-lookup"><span data-stu-id="2ea09-153">Streaming traces from a remote cluster node</span></span>
<span data-ttu-id="2ea09-154">Si può anche eseguire lo streaming delle tracce direttamente da un nodo del cluster remoto a Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2ea09-154">You are also able to stream traces directly from a remote cluster node to Visual Studio.</span></span> <span data-ttu-id="2ea09-155">Questa funzionalità consente di eseguire lo streaming degli eventi di traccia ETW, generati su un nodo del cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2ea09-155">This feature allows you to stream ETW trace events, produced on a Service Fabric cluster node.</span></span>

> [!NOTE]
> <span data-ttu-id="2ea09-156">La funzionalità richiede [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) e [Azure SDK per .NET 2.9](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="2ea09-156">This feature requires [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) and [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/).</span></span>
> <span data-ttu-id="2ea09-157">Questa funzionalità supporta solo i cluster in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="2ea09-157">This feature only supports clusters running in Azure.</span></span>
> 
> 

<!-- -->
> [!WARNING]
> <span data-ttu-id="2ea09-158">Lo streaming delle tracce è progettato per scenari di sviluppo e test e non deve essere usato in ambienti di produzione a causa dell'impatto sulle applicazioni in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2ea09-158">Streaming traces is meant for dev/test scenarios and not to be used in production environments, because of the impact on the running applications.</span></span>
> <span data-ttu-id="2ea09-159">In uno scenario di produzione è consigliabile basarsi sugli eventi di inoltro usando Diagnostica di Azure.</span><span class="sxs-lookup"><span data-stu-id="2ea09-159">In a production scenario, you should rely on forwarding events using Azure Diagnostics.</span></span>
> 
> 

1. <span data-ttu-id="2ea09-160">Passare al cluster in **Cloud Explorer**, fare clic con il pulsante destro del mouse e scegliere **Abilita tracce streaming**</span><span class="sxs-lookup"><span data-stu-id="2ea09-160">Navigate to your cluster in **Cloud Explorer**, right-click and choose **Enable Streaming Traces**</span></span>
   
    ![Abilitare le tracce di streaming remote][enablestreamingtraces]
   
    <span data-ttu-id="2ea09-162">Verrà avviato il processo di abilitazione dell'estensione di streaming delle tracce nei nodi del cluster e delle configurazioni di rete necessarie.</span><span class="sxs-lookup"><span data-stu-id="2ea09-162">This will kick off the process of enabling the streaming traces extension on your cluster nodes, as well as required network configurations.</span></span>
2. <span data-ttu-id="2ea09-163">Espandere l'elemento **Nodi** in **Cloud Explorer**, fare clic con il pulsante destro del mouse sul nodo da cui trasmettere le tracce e scegliere **Visualizza tracce streaming**</span><span class="sxs-lookup"><span data-stu-id="2ea09-163">Expand the **Nodes** element in **Cloud Explorer**, right-click the node you want to stream traces from and choose **View Streaming Traces**</span></span>
   
    ![Visualizzare le tracce di streaming remote][viewremotestreamingtraces]
   
    <span data-ttu-id="2ea09-165">Ripetere il passaggio 2 per tutti i nodi da cui visualizzare le tracce.</span><span class="sxs-lookup"><span data-stu-id="2ea09-165">Repeat step 2 for as many nodes as you want to see traces from.</span></span> <span data-ttu-id="2ea09-166">Il flusso di ogni nodo verrà visualizzato in una finestra dedicata.</span><span class="sxs-lookup"><span data-stu-id="2ea09-166">Each nodes stream will show up in a dedicated window.</span></span>
   
    <span data-ttu-id="2ea09-167">A questo punto è possibile vedere le tracce emesse da Service Fabrice e dai propri servizi.</span><span class="sxs-lookup"><span data-stu-id="2ea09-167">You are now able to see the traces emitted by Service Fabric, and your services.</span></span> <span data-ttu-id="2ea09-168">Per filtrare gli eventi in modo da visualizzare solo una specifica applicazione, è sufficiente immettere il nome dell'applicazione nel filtro.</span><span class="sxs-lookup"><span data-stu-id="2ea09-168">If you want to filter the events to only show a specific application, simply type in the name of the application in the filter.</span></span>
   
    ![Visualizzazione delle tracce di streaming][viewingstreamingtraces]
3. <span data-ttu-id="2ea09-170">Al termine dello streaming delle tracce dal cluster, è possibile disabilitare le tracce di streaming remote facendo clic con il pulsante destro del mouse sul cluster in **Cloud Explorer** e scegliere **Disabilita tracce streaming**</span><span class="sxs-lookup"><span data-stu-id="2ea09-170">Once you are done streaming traces from your cluster, you can disable remote streaming traces, by right-clicking the cluster in **Cloud Explorer** and choose **Disable Streaming Traces**</span></span>
   
    ![Disabilitare le tracce di streaming remote][disablestreamingtraces]

## <a name="next-steps"></a><span data-ttu-id="2ea09-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2ea09-172">Next steps</span></span>
* <span data-ttu-id="2ea09-173">[Testare un servizio di Service Fabric](service-fabric-testability-overview.md)</span><span class="sxs-lookup"><span data-stu-id="2ea09-173">[Test a Service Fabric service](service-fabric-testability-overview.md).</span></span>
* <span data-ttu-id="2ea09-174">[Gestione delle applicazioni di Service Fabric in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="2ea09-174">[Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

<!--Image references-->
[startdebugging]: ./media/service-fabric-debugging-your-application/startdebugging.png
[diagnosticevents]: ./media/service-fabric-debugging-your-application/diagnosticevents.png
[viewdiagnosticevents]: ./media/service-fabric-debugging-your-application/viewdiagnosticevents.png
[diagnosticeventsactions]: ./media/service-fabric-debugging-your-application/diagnosticeventsactions.png
[breakpoint]: ./media/service-fabric-debugging-your-application/breakpoint.png
[enableremotedebugging]: ./media/service-fabric-debugging-your-application/enableremotedebugging.png
[attachdebugger]: ./media/service-fabric-debugging-your-application/attachdebugger.png
[chooseprocess]: ./media/service-fabric-debugging-your-application/chooseprocess.png
[conditionalbreakpoint]: ./media/service-fabric-debugging-your-application/conditionalbreakpoint.png
[disableremotedebugging]: ./media/service-fabric-debugging-your-application/disableremotedebugging.png
[enablestreamingtraces]: ./media/service-fabric-debugging-your-application/enablestreamingtraces.png
[viewingstreamingtraces]: ./media/service-fabric-debugging-your-application/viewingstreamingtraces.png
[viewremotestreamingtraces]: ./media/service-fabric-debugging-your-application/viewremotestreamingtraces.png
[disablestreamingtraces]: ./media/service-fabric-debugging-your-application/disablestreamingtraces.png
