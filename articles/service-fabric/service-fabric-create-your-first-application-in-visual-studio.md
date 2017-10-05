---
title: Creare un servizio Reliable Services di Azure Service Fabric con C#
description: Creare e distribuire un'applicazione Reliable Services basata su Azure Service Fabric ed eseguirne il debug con Visual Studio.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: c3655b7b-de78-4eac-99eb-012f8e042109
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: f93298e6483fd8c9dfda835964aeebd1a430af69
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-your-first-c-service-fabric-stateful-reliable-services-application"></a><span data-ttu-id="61c26-103">Creare la prima applicazione Reliable Services con stato C# di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="61c26-103">Create your first C# Service Fabric stateful reliable services application</span></span>

<span data-ttu-id="61c26-104">Questo articolo illustra come distribuire la prima applicazione di Service Fabric per .NET in Windows in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="61c26-104">Learn how to deploy your first Service Fabric application for .NET on Windows in just a few minutes.</span></span> <span data-ttu-id="61c26-105">Al termine, si avrà un cluster locale in esecuzione con un'applicazione Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="61c26-105">When you're finished, you'll have a local cluster running with a reliable service application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61c26-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="61c26-106">Prerequisites</span></span>

<span data-ttu-id="61c26-107">Prima di iniziare, assicurarsi di avere [configurato l'ambiente di sviluppo](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="61c26-107">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span></span> <span data-ttu-id="61c26-108">Ciò include l'installazione di Service Fabric SDK e Visual Studio 2017 o 2015.</span><span class="sxs-lookup"><span data-stu-id="61c26-108">This includes installing the Service Fabric SDK and Visual Studio 2017 or 2015.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="61c26-109">Creazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="61c26-109">Create the application</span></span>

<span data-ttu-id="61c26-110">Avviare Visual Studio come **amministratore**.</span><span class="sxs-lookup"><span data-stu-id="61c26-110">Launch Visual Studio as an **administrator**.</span></span>

<span data-ttu-id="61c26-111">Creare un progetto con `CTRL`+`SHIFT`+`N`.</span><span class="sxs-lookup"><span data-stu-id="61c26-111">Create a project with `CTRL`+`SHIFT`+`N`</span></span>

<span data-ttu-id="61c26-112">Nella finestra di dialogo **Nuovo progetto** scegliere **Cloud > Applicazione di Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="61c26-112">In the **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

<span data-ttu-id="61c26-113">Assegnare all'applicazione il nome **MyApplication** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="61c26-113">Name the application **MyApplication** and press **OK**.</span></span>

   
![Finestra di dialogo Nuovo progetto in Visual Studio][1]

<span data-ttu-id="61c26-115">Nella finestra di dialogo successiva è possibile creare qualsiasi tipo di applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="61c26-115">You can create any type of Service Fabric application from the next dialog.</span></span> <span data-ttu-id="61c26-116">Per questa guida introduttiva scegliere **Servizio con stato**.</span><span class="sxs-lookup"><span data-stu-id="61c26-116">For this Quickstart, choose **Stateful Service**.</span></span>

<span data-ttu-id="61c26-117">Assegnare al servizio il nome **MyStatefulService** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="61c26-117">Name the service **MyStatefulService** and press **OK**.</span></span>

![Finestra di dialogo Nuovo servizio in Visual Studio][2]


<span data-ttu-id="61c26-119">Visual studio crea il progetto di applicazione e il progetto di servizio con stato e li visualizza in Esplora soluzioni.</span><span class="sxs-lookup"><span data-stu-id="61c26-119">Visual Studio creates the application project and the stateful service project and displays them in Solution Explorer.</span></span>

![Esplora soluzioni dopo la creazione dell'applicazione con servizio con stato][3]

<span data-ttu-id="61c26-121">Il progetto di applicazione (**MyApplication**) non contiene direttamente codice,</span><span class="sxs-lookup"><span data-stu-id="61c26-121">The application project (**MyApplication**) does not contain any code directly.</span></span> <span data-ttu-id="61c26-122">ma fa riferimento a un set di progetti di servizio.</span><span class="sxs-lookup"><span data-stu-id="61c26-122">Instead, it references a set of service projects.</span></span> <span data-ttu-id="61c26-123">Include inoltre altri tre tipi di contenuto:</span><span class="sxs-lookup"><span data-stu-id="61c26-123">In addition, it contains three other types of content:</span></span>

* <span data-ttu-id="61c26-124">**Profili di pubblicazione**</span><span class="sxs-lookup"><span data-stu-id="61c26-124">**Publish profiles**</span></span>  
<span data-ttu-id="61c26-125">Profili per la distribuzione in diversi ambienti.</span><span class="sxs-lookup"><span data-stu-id="61c26-125">Profiles for deploying to different environments.</span></span>

* <span data-ttu-id="61c26-126">**Script**</span><span class="sxs-lookup"><span data-stu-id="61c26-126">**Scripts**</span></span>  
<span data-ttu-id="61c26-127">Script di PowerShell per distribuire o aggiornare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="61c26-127">PowerShell script for deploying/upgrading your application.</span></span>

* <span data-ttu-id="61c26-128">**Definizione di applicazione**</span><span class="sxs-lookup"><span data-stu-id="61c26-128">**Application definition**</span></span>  
<span data-ttu-id="61c26-129">Include il file ApplicationManifest.xml in *ApplicationPackageRoot*, che descrive la composizione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="61c26-129">Includes the ApplicationManifest.xml file under *ApplicationPackageRoot* which describes your application's composition.</span></span> <span data-ttu-id="61c26-130">I file di parametri dell'applicazione associati sono disponibili in *ApplicationParameters* e possono essere usati per fornire parametri specifici dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="61c26-130">Associated application parameter files are under *ApplicationParameters*, which can be used to specify environment-specific parameters.</span></span> <span data-ttu-id="61c26-131">Visual Studio seleziona un file di parametri dell'applicazione specificato nel profilo di pubblicazione associato durante la distribuzione in un ambiente specifico.</span><span class="sxs-lookup"><span data-stu-id="61c26-131">Visual Studio selects an application parameter file that's specified in the associated publish profile during deployment to a specific environment.</span></span>
    
<span data-ttu-id="61c26-132">Per una panoramica del contenuto del progetto di servizio, vedere la [Guida introduttiva a Reliable Services](service-fabric-reliable-services-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="61c26-132">For an overview of the contents of the service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="deploy-and-debug-the-application"></a><span data-ttu-id="61c26-133">Distribuire ed eseguire il debug dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="61c26-133">Deploy and debug the application</span></span>

<span data-ttu-id="61c26-134">A questo punto, eseguire l'applicazione creata.</span><span class="sxs-lookup"><span data-stu-id="61c26-134">Now that you have an application, run it.</span></span>

<span data-ttu-id="61c26-135">In Visual Studio premere `F5` per distribuire l'applicazione per il debug.</span><span class="sxs-lookup"><span data-stu-id="61c26-135">In Visual Studio, press `F5` to deploy the application for debugging.</span></span>

>[!NOTE]
><span data-ttu-id="61c26-136">La prima volta che si esegue e si distribuisce l'applicazione in locale, Visual Studio crea un cluster locale per il debug.</span><span class="sxs-lookup"><span data-stu-id="61c26-136">The first time you run and deploy the application locally, Visual Studio creates a local cluster for debugging.</span></span> <span data-ttu-id="61c26-137">Questa operazione potrebbe richiedere tempo.</span><span class="sxs-lookup"><span data-stu-id="61c26-137">This may take some time.</span></span> <span data-ttu-id="61c26-138">Lo stato della creazione del cluster verrà visualizzato nella finestra di output di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="61c26-138">The cluster creation status is displayed in the Visual Studio output window.</span></span>

<span data-ttu-id="61c26-139">Quando il cluster è pronto, si riceverà una notifica dall'applicazione di gestione della barra delle applicazioni inclusa nell'SDK.</span><span class="sxs-lookup"><span data-stu-id="61c26-139">When the cluster is ready, you get a notification from the local cluster system tray manager application included with the SDK.</span></span>
   
![Notifica della barra delle applicazioni per il cluster locale][4]

<span data-ttu-id="61c26-141">All'avvio dell'applicazione, Visual Studio apre automaticamente il **visualizzatore eventi di diagnostica**, in cui viene visualizzato l'output di traccia dei servizi.</span><span class="sxs-lookup"><span data-stu-id="61c26-141">Once the application starts, Visual Studio automatically brings up the **Diagnostics Event Viewer**, where you can see trace output from your services.</span></span>
   
![Visualizzatore eventi di diagnostica][5]

<span data-ttu-id="61c26-143">Il modello di servizio con stato usato mostra semplicemente l'incremento del valore del contatore nel metodo `RunAsync` di **MyStatefulService.cs**.</span><span class="sxs-lookup"><span data-stu-id="61c26-143">The stateful service template we used simply shows a counter value incrementing in the `RunAsync` method of **MyStatefulService.cs**.</span></span>

<span data-ttu-id="61c26-144">Espandere uno degli eventi per visualizzare altri dettagli, incluso il nodo in cui viene eseguito il codice.</span><span class="sxs-lookup"><span data-stu-id="61c26-144">Expand one of the events to see more details, including the node where the code is running.</span></span> <span data-ttu-id="61c26-145">In questo caso è \_Node\_2, anche se nel computer locale potrebbe essere diverso.</span><span class="sxs-lookup"><span data-stu-id="61c26-145">In this case, it is \_Node\_2, though it may differ on your machine.</span></span>
   
![Dettaglio del visualizzatore eventi di diagnostica][6]

<span data-ttu-id="61c26-147">Il cluster locale include cinque nodi ospitati in un singolo computer.</span><span class="sxs-lookup"><span data-stu-id="61c26-147">The local cluster contains five nodes hosted on a single machine.</span></span> <span data-ttu-id="61c26-148">In un ambiente di produzione, ogni nodo è ospitato in una macchina virtuale o un computer fisico distinto.</span><span class="sxs-lookup"><span data-stu-id="61c26-148">In a production environment, each node is hosted on a distinct physical or virtual machine.</span></span> <span data-ttu-id="61c26-149">Per simulare la perdita di un computer durante l'esecuzione del debugger di Visual Studio, portare offline uno dei nodi del cluster locale.</span><span class="sxs-lookup"><span data-stu-id="61c26-149">To simulate the loss of a machine while exercising the Visual Studio debugger at the same time, let's take down one of the nodes on the local cluster.</span></span>

<span data-ttu-id="61c26-150">Nella finestra **Esplora soluzioni** aprire **MyStatefulService.cs**.</span><span class="sxs-lookup"><span data-stu-id="61c26-150">In the **Solution Explorer** window, open **MyStatefulService.cs**.</span></span> 

<span data-ttu-id="61c26-151">Trovare il metodo `RunAsync` e impostare un punto di interruzione nella prima riga del metodo.</span><span class="sxs-lookup"><span data-stu-id="61c26-151">Find the `RunAsync` method and set a breakpoint on the first line of the method.</span></span>

![Punto di interruzione nel metodo RunAsync del servizio con stato][7]

<span data-ttu-id="61c26-153">Avviare lo strumento **Service Fabric Explorer** facendo clic con il pulsante destro del mouse sull'applicazione dell'area di notifica **Local Cluster Manager** (Gestione cluster locale) e scegliendo **Manage Local Cluster** (Gestisci cluster locale).</span><span class="sxs-lookup"><span data-stu-id="61c26-153">Launch the **Service Fabric Explorer** tool by right-clicking on the **Local Cluster Manager** system tray application and choose **Manage Local Cluster**.</span></span>

![Avvio di Service Fabric Explorer da Local Cluster Manager][systray-launch-sfx]

<span data-ttu-id="61c26-155">[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) offre una rappresentazione visiva del cluster,</span><span class="sxs-lookup"><span data-stu-id="61c26-155">[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) offers a visual representation of a cluster.</span></span> <span data-ttu-id="61c26-156">che include il set di applicazioni distribuite al suo interno e il set di nodi fisici da cui è costituito.</span><span class="sxs-lookup"><span data-stu-id="61c26-156">It includes the set of applications deployed to it and the set of physical nodes that make it up.</span></span>

<span data-ttu-id="61c26-157">Nel riquadro sinistro espandere **Cluster > Nodi** e individuare il nodo in cui è in esecuzione il codice.</span><span class="sxs-lookup"><span data-stu-id="61c26-157">In the left pane, expand **Cluster > Nodes** and find the node where your code is running.</span></span>

<span data-ttu-id="61c26-158">Fare clic su **Azioni > Disattiva (riavvio)** per simulare il riavvio di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="61c26-158">Click **Actions > Deactivate (Restart)** to simulate a machine restarting.</span></span>

![Arresto di un nodo in Service Fabric Explorer][sfx-stop-node]

<span data-ttu-id="61c26-160">Verrà visualizzato il raggiungimento del punto di interruzione in Visual Studio mentre viene effettuato il failover del calcolo eseguito su un nodo in un altro nodo.</span><span class="sxs-lookup"><span data-stu-id="61c26-160">Momentarily, you should see your breakpoint hit in Visual Studio as the computation you were doing on one node seamlessly fails over to another.</span></span>


<span data-ttu-id="61c26-161">Tornare quindi al visualizzatore eventi di diagnostica e osservare i messaggi.</span><span class="sxs-lookup"><span data-stu-id="61c26-161">Next, return to the Diagnostic Events Viewer and observe the messages.</span></span> <span data-ttu-id="61c26-162">Il contatore ha continuato ad aumentare anche se gli eventi provengono in effetti da un nodo diverso.</span><span class="sxs-lookup"><span data-stu-id="61c26-162">The counter has continued incrementing, even though the events are actually coming from a different node.</span></span>

![Visualizzatore eventi di diagnostica dopo il failover][diagnostic-events-viewer-detail-post-failover]

## <a name="cleaning-up-the-local-cluster-optional"></a><span data-ttu-id="61c26-164">Pulizia del cluster locale (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="61c26-164">Cleaning up the local cluster (optional)</span></span>

<span data-ttu-id="61c26-165">Tenere presente che il cluster locale è reale.</span><span class="sxs-lookup"><span data-stu-id="61c26-165">Remember, this local cluster is real.</span></span> <span data-ttu-id="61c26-166">L'arresto del debugger rimuove l'istanza dell'applicazione e annulla la registrazione del tipo di applicazione.</span><span class="sxs-lookup"><span data-stu-id="61c26-166">Stopping the debugger removes your application instance and unregisters the application type.</span></span> <span data-ttu-id="61c26-167">L'esecuzione del cluster, tuttavia, continua in background.</span><span class="sxs-lookup"><span data-stu-id="61c26-167">However, the cluster continues to run in the background.</span></span> <span data-ttu-id="61c26-168">Quando si è pronti per arrestare il cluster locale, è possibile procedere in due modi.</span><span class="sxs-lookup"><span data-stu-id="61c26-168">When you're ready to stop the local cluster, there are a couple options.</span></span>

### <a name="keep-application-and-trace-data"></a><span data-ttu-id="61c26-169">Mantenere i dati applicazione e di traccia</span><span class="sxs-lookup"><span data-stu-id="61c26-169">Keep application and trace data</span></span>

<span data-ttu-id="61c26-170">Arrestare il cluster facendo clic con il pulsante destro del mouse sull'applicazione dell'area di notifica **Local Cluster Manager** (Gestione cluster locale) e quindi scegliendo **Stop Local Cluster** (Arresta cluster locale).</span><span class="sxs-lookup"><span data-stu-id="61c26-170">Shut down the cluster by right-clicking on the **Local Cluster Manager** system tray application and then choose **Stop Local Cluster**.</span></span>

### <a name="delete-the-cluster-and-all-data"></a><span data-ttu-id="61c26-171">Eliminare il cluster e tutti i dati</span><span class="sxs-lookup"><span data-stu-id="61c26-171">Delete the cluster and all data</span></span>

<span data-ttu-id="61c26-172">Rimuovere il cluster facendo clic con il pulsante destro del mouse sull'applicazione dell'area di notifica **Local Cluster Manager** (Gestione cluster locale) e quindi scegliendo **Remove Local Cluster** (Rimuovi cluster locale).</span><span class="sxs-lookup"><span data-stu-id="61c26-172">Remove the cluster by right-clicking on the **Local Cluster Manager** system tray application and then choose **Remove Local Cluster**.</span></span> 

<span data-ttu-id="61c26-173">Se si sceglie questa opzione, Visual Studio ridistribuirà il cluster alla successiva esecuzione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="61c26-173">If you choose this option, Visual Studio will redeploy the cluster the next time your run the application.</span></span> <span data-ttu-id="61c26-174">Scegliere questa opzione se non si prevede di usare il cluster locale per un certo periodo o se è necessario recuperare risorse.</span><span class="sxs-lookup"><span data-stu-id="61c26-174">Choose this option if you don't intend to use the local cluster for some time or if you need to reclaim resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="61c26-175">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="61c26-175">Next steps</span></span>
<span data-ttu-id="61c26-176">Altre informazioni su [Reliable Services](service-fabric-reliable-services-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="61c26-176">Read more about [reliable services](service-fabric-reliable-services-introduction.md).</span></span>
<!-- Image References -->

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog.png
[2]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png
[3]: ./media/service-fabric-create-your-first-application-in-visual-studio/solution-explorer-stateful-service-template.png
[4]: ./media/service-fabric-create-your-first-application-in-visual-studio/local-cluster-manager-notification.png
[5]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer.png
[6]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail.png
[7]: ./media/service-fabric-create-your-first-application-in-visual-studio/runasync-breakpoint.png
[sfx-stop-node]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-deactivate-node.png
[systray-launch-sfx]: ./media/service-fabric-create-your-first-application-in-visual-studio/launch-sfx.png
[diagnostic-events-viewer-detail-post-failover]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail-post-failover.png
[sfe-delete-application]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-delete-application.png
[switch-cluster-mode]: ./media/service-fabric-create-your-first-application-in-visual-studio/switch-cluster-mode.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
