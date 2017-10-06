---
title: aaaDebug dell'applicazione in Visual Studio | Documenti Microsoft
description: "Migliorare hello affidabilità e prestazioni dei servizi, sviluppo e il debug in Visual Studio in un cluster di sviluppo locale."
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
ms.openlocfilehash: 8d08689e82195d09f57b462631ad04fd237bc4fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-service-fabric-application-by-using-visual-studio"></a><span data-ttu-id="83717-103">Debug dell'applicazione di Service Fabric mediante Visual Studio</span><span class="sxs-lookup"><span data-stu-id="83717-103">Debug your Service Fabric application by using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="83717-104">Visual Studio/CSharp</span><span class="sxs-lookup"><span data-stu-id="83717-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="83717-105">Eclipse/Java</span><span class="sxs-lookup"><span data-stu-id="83717-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
>


## <a name="debug-a-local-service-fabric-application"></a><span data-ttu-id="83717-106">Eseguire il debug di un'applicazione di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="83717-106">Debug a local Service Fabric application</span></span>
<span data-ttu-id="83717-107">Per risparmiare tempo e denaro, è possibile distribuire l'applicazione di Service Fabric ed eseguirne il debug in un cluster di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="83717-107">You can save time and money by deploying and debugging your Azure Service Fabric application in a local computer development cluster.</span></span> <span data-ttu-id="83717-108">Visual Studio 2017 o Visual Studio 2015 è possibile distribuire cluster locale di hello applicazione toohello e si connettono automaticamente le istanze di hello debugger tooall dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="83717-108">Visual Studio 2017 or Visual Studio 2015 can deploy hello application toohello local cluster and automatically connect hello debugger tooall instances of your application.</span></span>

1. <span data-ttu-id="83717-109">Avviare un cluster di sviluppo locale seguendo i passaggi di hello in [impostazione dell'ambiente di sviluppo di Service Fabric](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="83717-109">Start a local development cluster by following hello steps in [Setting up your Service Fabric development environment](service-fabric-get-started.md).</span></span>
2. <span data-ttu-id="83717-110">Premere **F5** oppure fare clic su **Debug** > **Avvia debug**.</span><span class="sxs-lookup"><span data-stu-id="83717-110">Press **F5** or click **Debug** > **Start Debugging**.</span></span>
   
    ![Avviare il debug di un'applicazione][startdebugging]
3. <span data-ttu-id="83717-112">Impostare i punti di interruzione nel codice ed esaminare l'applicazione hello tramite i comandi in hello **Debug** menu.</span><span class="sxs-lookup"><span data-stu-id="83717-112">Set breakpoints in your code and step through hello application by clicking commands in hello **Debug** menu.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="83717-113">Visual Studio collega tooall istanze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="83717-113">Visual Studio attaches tooall instances of your application.</span></span> <span data-ttu-id="83717-114">Mentre il codice viene eseguito un'istruzione alla volta, i punti di interruzione possono essere raggiunti da più processi, dando luogo a sessioni simultanee.</span><span class="sxs-lookup"><span data-stu-id="83717-114">While you're stepping through code, breakpoints may get hit by multiple processes resulting in concurrent sessions.</span></span> <span data-ttu-id="83717-115">Provare a disabilitare i punti di interruzione hello dopo che è raggiunto apportando ogni punto di interruzione condizionale sull'ID di thread hello o usando gli eventi di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="83717-115">Try disabling hello breakpoints after they're hit, by making each breakpoint conditional on hello thread ID or by using diagnostic events.</span></span>
   > 
   > 
4. <span data-ttu-id="83717-116">Hello **gli eventi di diagnostica** finestra verrà aperta automaticamente in modo da visualizzare gli eventi di diagnostica in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="83717-116">hello **Diagnostic Events** window will automatically open so you can view diagnostic events in real time.</span></span>
   
    ![Visualizzare gli eventi diagnostici in tempo reale][diagnosticevents]
5. <span data-ttu-id="83717-118">È inoltre possibile aprire hello **gli eventi di diagnostica** finestra in Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="83717-118">You can also open hello **Diagnostic Events** window in Cloud Explorer.</span></span>  <span data-ttu-id="83717-119">In **Service Fabric** fare clic con il pulsante destro del mouse e scegliere **Visualizza tracce streaming**.</span><span class="sxs-lookup"><span data-stu-id="83717-119">Under **Service Fabric**, right-click any node and choose **View Streaming Traces**.</span></span>
   
    ![Finestra di eventi di diagnostica hello aperto][viewdiagnosticevents]
   
    <span data-ttu-id="83717-121">Se si desidera toofilter il servizio specifico di tracce tooa o l'applicazione, semplicemente abilitando le tracce di streaming su tale applicazione o un servizio specifico.</span><span class="sxs-lookup"><span data-stu-id="83717-121">If you want toofilter your traces tooa specific service or application, simply enable streaming traces on that specific service or application.</span></span>
6. <span data-ttu-id="83717-122">eventi di diagnostica Hello possono essere visualizzati in hello generato automaticamente **ServiceEventSource.cs** file e vengono chiamati dal codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="83717-122">hello diagnostic events can be seen in hello automatically generated **ServiceEventSource.cs** file and are called from application code.</span></span>
   
    ```csharp
    ServiceEventSource.Current.ServiceMessage(this, "My ServiceMessage with a parameter {0}", result.Value.ToString());
    ```
7. <span data-ttu-id="83717-123">Hello **gli eventi di diagnostica** finestra supporta il filtro, la sospensione e controllando gli eventi in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="83717-123">hello **Diagnostic Events** window supports filtering, pausing, and inspecting events in real time.</span></span>  <span data-ttu-id="83717-124">filtro di Hello è una ricerca semplice stringa di messaggio di evento hello, incluso il relativo contenuto.</span><span class="sxs-lookup"><span data-stu-id="83717-124">hello filter is a simple string search of hello event message, including its contents.</span></span>
   
    ![Filtrare, sospendere e riprendere o esaminare eventi in tempo reale][diagnosticeventsactions]
8. <span data-ttu-id="83717-126">Il debug dei servizi è come il debug di qualsiasi altra applicazione.</span><span class="sxs-lookup"><span data-stu-id="83717-126">Debugging services is like debugging any other application.</span></span> <span data-ttu-id="83717-127">In genere i punti di interruzione vengono impostati tramite Visual Studio per semplificare il debug.</span><span class="sxs-lookup"><span data-stu-id="83717-127">You will normally set Breakpoints through Visual Studio for easy debugging.</span></span> <span data-ttu-id="83717-128">Anche se le raccolte Reliable Collections vengono replicate in più nodi, implementano comunque IEnumerable.</span><span class="sxs-lookup"><span data-stu-id="83717-128">Even though Reliable Collections replicate across multiple nodes, they still implement IEnumerable.</span></span> <span data-ttu-id="83717-129">Ciò significa che è possibile utilizzare hello visualizzazione dei risultati in Visual Studio durante il debug toosee è memorizzato all'interno.</span><span class="sxs-lookup"><span data-stu-id="83717-129">This means that you can use hello Results View in Visual Studio while debugging toosee what you've stored inside.</span></span> <span data-ttu-id="83717-130">È sufficiente impostare un punto di interruzione in qualsiasi posizione all'interno del codice.</span><span class="sxs-lookup"><span data-stu-id="83717-130">Simply set a breakpoint anywhere in your code.</span></span>
   
    ![Avviare il debug di un'applicazione][breakpoint]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="debug-a-remote-service-fabric-application"></a><span data-ttu-id="83717-132">Eseguire il debug di un'applicazione remota di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="83717-132">Debug a remote Service Fabric application</span></span>
<span data-ttu-id="83717-133">Se le applicazioni di Service Fabric sono in esecuzione in un cluster di Service Fabric in Azure, si è in grado di eseguire il debug tooremotely questi, direttamente da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="83717-133">If your Service Fabric applications are running on a Service Fabric cluster in Azure, you are able tooremotely debug these, directly from Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="83717-134">funzionalità di Hello richiede [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) e [Azure SDK per .NET 2.9](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="83717-134">hello feature requires [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) and [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/).</span></span>    
> 
> 

<!-- -->
> [!WARNING]
> <span data-ttu-id="83717-135">Debug remoto è destinato agli scenari di sviluppo e test e non toobe utilizzato negli ambienti di produzione a causa dell'impatto hello in hello applicazioni in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="83717-135">Remote debugging is meant for dev/test scenarios and not toobe used in production environments, because of hello impact on hello running applications.</span></span>
> 
> 

1. <span data-ttu-id="83717-136">Passare il cluster tooyour in **Cloud Explorer**destro del mouse e scegliere **attivare il debug**</span><span class="sxs-lookup"><span data-stu-id="83717-136">Navigate tooyour cluster in **Cloud Explorer**, right-click and choose **Enable Debugging**</span></span>
   
    ![Abilitare il debug remoto][enableremotedebugging]
   
    <span data-ttu-id="83717-138">Ciò consente di avviare il processo di hello di abilitazione hello estensione nei nodi del cluster del debug remoto, nonché le configurazioni di rete necessarie.</span><span class="sxs-lookup"><span data-stu-id="83717-138">This will kick off hello process of enabling hello remote debugging extension on your cluster nodes, as well as required network configurations.</span></span>
2. <span data-ttu-id="83717-139">Nodo del cluster rapida hello in **Cloud Explorer**e scegliere **collega Debugger**</span><span class="sxs-lookup"><span data-stu-id="83717-139">Right-click hello cluster node in **Cloud Explorer**, and choose **Attach Debugger**</span></span>
   
    ![Collega debugger][attachdebugger]
3. <span data-ttu-id="83717-141">In hello **allegare tooprocess** finestra di dialogo, scegliere il processo di hello toodebug desiderato e fare clic su **Connetti**</span><span class="sxs-lookup"><span data-stu-id="83717-141">In hello **Attach tooprocess** dialog, choose hello process you want toodebug, and click **Attach**</span></span>
   
    ![Scegliere il processo][chooseprocess]
   
    <span data-ttu-id="83717-143">nome Hello del processo di hello desiderate tooattach a, uguale a hello nome del nome di assembly del progetto di servizio.</span><span class="sxs-lookup"><span data-stu-id="83717-143">hello name of hello process you want tooattach to, equals hello name of your service project assembly name.</span></span>
   
    <span data-ttu-id="83717-144">debugger Hello collegherà tooall nodi in esecuzione il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="83717-144">hello debugger will attach tooall nodes running hello process.</span></span>
   
   * <span data-ttu-id="83717-145">In caso di hello in cui si esegue il debug di un servizio senza stato, tutte le istanze del servizio hello in tutti i nodi fanno parte della sessione di debug hello.</span><span class="sxs-lookup"><span data-stu-id="83717-145">In hello case where you are debugging a stateless service, all instances of hello service on all nodes are part of hello debug session.</span></span>
   * <span data-ttu-id="83717-146">Se si esegue il debug di un servizio con stato, solo hello replica primaria di ogni partizione sarà attiva e pertanto rilevata dal debugger hello.</span><span class="sxs-lookup"><span data-stu-id="83717-146">If you are debugging a stateful service, only hello primary replica of any partition will be active and therefore caught by hello debugger.</span></span> <span data-ttu-id="83717-147">Se la replica primaria hello viene spostata durante una sessione di debug di hello, l'elaborazione di hello di tale replica sarà ancora parte della sessione di debug hello.</span><span class="sxs-lookup"><span data-stu-id="83717-147">If hello primary replica moves during hello debug session, hello processing of that replica will still be part of hello debug session.</span></span>
   * <span data-ttu-id="83717-148">Le partizioni rilevanti ordine tooonly catch o istanze di un determinato servizio, è possibile utilizzare i punti di interruzione condizionali tooonly interruzione una partizione specifica o istanza.</span><span class="sxs-lookup"><span data-stu-id="83717-148">In order tooonly catch relevant partitions or instances of a given service, you can use conditional breakpoints tooonly break a specific partition or instance.</span></span>
     
     ![Punto di interruzione condizionale][conditionalbreakpoint]
     
     > [!NOTE]
     > <span data-ttu-id="83717-150">Attualmente non è supportato il debug di un cluster di Service Fabric con più istanze di hello nome eseguibile del servizio stesso.</span><span class="sxs-lookup"><span data-stu-id="83717-150">Currently we do not support debugging a Service Fabric cluster with multiple instances of hello same service executable name.</span></span>
     > 
     > 
4. <span data-ttu-id="83717-151">Dopo aver completato il debug dell'applicazione, è possibile disabilitare l'estensione di debug remoto hello facendo clic con il cluster hello in **Cloud Explorer** e scegliere **disabilitare il debug**</span><span class="sxs-lookup"><span data-stu-id="83717-151">Once you finish debugging your application, you can disable hello remote debugging extension by right-clicking hello cluster in **Cloud Explorer** and choose **Disable Debugging**</span></span>
   
    ![Disabilitare il debug remoto][disableremotedebugging]

## <a name="streaming-traces-from-a-remote-cluster-node"></a><span data-ttu-id="83717-153">Streaming delle tracce da un nodo del cluster remoto</span><span class="sxs-lookup"><span data-stu-id="83717-153">Streaming traces from a remote cluster node</span></span>
<span data-ttu-id="83717-154">Inoltre in grado di toostream tracce sono direttamente da un tooVisual nodo cluster remoto Studio.</span><span class="sxs-lookup"><span data-stu-id="83717-154">You are also able toostream traces directly from a remote cluster node tooVisual Studio.</span></span> <span data-ttu-id="83717-155">Questa funzionalità permette di eventi di traccia ETW toostream, generati in un nodo di cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="83717-155">This feature allows you toostream ETW trace events, produced on a Service Fabric cluster node.</span></span>

> [!NOTE]
> <span data-ttu-id="83717-156">La funzionalità richiede [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) e [Azure SDK per .NET 2.9](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="83717-156">This feature requires [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) and [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/).</span></span>
> <span data-ttu-id="83717-157">Questa funzionalità supporta solo i cluster in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="83717-157">This feature only supports clusters running in Azure.</span></span>
> 
> 

<!-- -->
> [!WARNING]
> <span data-ttu-id="83717-158">Il flusso di tracce è progettato per scenari di sviluppo e test e non toobe utilizzato negli ambienti di produzione a causa dell'impatto hello in hello applicazioni in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="83717-158">Streaming traces is meant for dev/test scenarios and not toobe used in production environments, because of hello impact on hello running applications.</span></span>
> <span data-ttu-id="83717-159">In uno scenario di produzione è consigliabile basarsi sugli eventi di inoltro usando Diagnostica di Azure.</span><span class="sxs-lookup"><span data-stu-id="83717-159">In a production scenario, you should rely on forwarding events using Azure Diagnostics.</span></span>
> 
> 

1. <span data-ttu-id="83717-160">Passare il cluster tooyour in **Cloud Explorer**destro del mouse e scegliere **abilitare lo Streaming di tracce**</span><span class="sxs-lookup"><span data-stu-id="83717-160">Navigate tooyour cluster in **Cloud Explorer**, right-click and choose **Enable Streaming Traces**</span></span>
   
    ![Abilitare le tracce di streaming remote][enablestreamingtraces]
   
    <span data-ttu-id="83717-162">Ciò consente di avviare il processo di hello di abilitazione hello streaming estensione tracce nei nodi del cluster, nonché le configurazioni di rete necessarie.</span><span class="sxs-lookup"><span data-stu-id="83717-162">This will kick off hello process of enabling hello streaming traces extension on your cluster nodes, as well as required network configurations.</span></span>
2. <span data-ttu-id="83717-163">Espandere hello **nodi** elemento **Cloud Explorer**, il nodo hello rapida toostream tracce da desiderato e scegliere **visualizzazione tracce di Streaming**</span><span class="sxs-lookup"><span data-stu-id="83717-163">Expand hello **Nodes** element in **Cloud Explorer**, right-click hello node you want toostream traces from and choose **View Streaming Traces**</span></span>
   
    ![Visualizzare le tracce di streaming remote][viewremotestreamingtraces]
   
    <span data-ttu-id="83717-165">Ripetere il passaggio 2 per qualsiasi numero di nodi che si desidera toosee tracce da.</span><span class="sxs-lookup"><span data-stu-id="83717-165">Repeat step 2 for as many nodes as you want toosee traces from.</span></span> <span data-ttu-id="83717-166">Il flusso di ogni nodo verrà visualizzato in una finestra dedicata.</span><span class="sxs-lookup"><span data-stu-id="83717-166">Each nodes stream will show up in a dedicated window.</span></span>
   
    <span data-ttu-id="83717-167">Ora in grado di toosee hello tracce sono generate dall'infrastruttura di servizio e i servizi.</span><span class="sxs-lookup"><span data-stu-id="83717-167">You are now able toosee hello traces emitted by Service Fabric, and your services.</span></span> <span data-ttu-id="83717-168">Se si desidera toofilter hello eventi tooonly Mostra un'applicazione specifica, è sufficiente digitare hello nome dell'applicazione hello nel filtro hello.</span><span class="sxs-lookup"><span data-stu-id="83717-168">If you want toofilter hello events tooonly show a specific application, simply type in hello name of hello application in hello filter.</span></span>
   
    ![Visualizzazione delle tracce di streaming][viewingstreamingtraces]
3. <span data-ttu-id="83717-170">Dopo aver eseguito le tracce di streaming dal cluster, è possibile disabilitare le tracce di flusso remote, facendo clic con il cluster hello in **Cloud Explorer** e scegliere **disabilitare tracce di Streaming**</span><span class="sxs-lookup"><span data-stu-id="83717-170">Once you are done streaming traces from your cluster, you can disable remote streaming traces, by right-clicking hello cluster in **Cloud Explorer** and choose **Disable Streaming Traces**</span></span>
   
    ![Disabilitare le tracce di streaming remote][disablestreamingtraces]

## <a name="next-steps"></a><span data-ttu-id="83717-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="83717-172">Next steps</span></span>
* <span data-ttu-id="83717-173">[Testare un servizio di Service Fabric](service-fabric-testability-overview.md)</span><span class="sxs-lookup"><span data-stu-id="83717-173">[Test a Service Fabric service](service-fabric-testability-overview.md).</span></span>
* <span data-ttu-id="83717-174">[Gestione delle applicazioni di Service Fabric in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="83717-174">[Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

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
