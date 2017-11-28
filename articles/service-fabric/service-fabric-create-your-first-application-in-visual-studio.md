---
title: aaaCreate un servizio affidabile di Azure Service Fabric con c#
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
ms.openlocfilehash: 740c866da6e639219b529fe92ed63cbeaa702a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-c-service-fabric-stateful-reliable-services-application"></a><span data-ttu-id="bb9f1-103">Creare la prima applicazione Reliable Services con stato C# di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="bb9f1-103">Create your first C# Service Fabric stateful reliable services application</span></span>

<span data-ttu-id="bb9f1-104">Informazioni su come toodeploy della prima applicazione di Service Fabric per .NET su Windows in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-104">Learn how toodeploy your first Service Fabric application for .NET on Windows in just a few minutes.</span></span> <span data-ttu-id="bb9f1-105">Al termine, si avrà un cluster locale in esecuzione con un'applicazione Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-105">When you're finished, you'll have a local cluster running with a reliable service application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb9f1-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bb9f1-106">Prerequisites</span></span>

<span data-ttu-id="bb9f1-107">Prima di iniziare, assicurarsi di avere [configurato l'ambiente di sviluppo](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bb9f1-107">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span></span> <span data-ttu-id="bb9f1-108">Questo include l'installazione di Service Fabric SDK hello e Visual Studio 2017 o 2015.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-108">This includes installing hello Service Fabric SDK and Visual Studio 2017 or 2015.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="bb9f1-109">Creare un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="bb9f1-109">Create hello application</span></span>

<span data-ttu-id="bb9f1-110">Avviare Visual Studio come **amministratore**.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-110">Launch Visual Studio as an **administrator**.</span></span>

<span data-ttu-id="bb9f1-111">Creare un progetto con `CTRL`+`SHIFT`+`N`.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-111">Create a project with `CTRL`+`SHIFT`+`N`</span></span>

<span data-ttu-id="bb9f1-112">In hello **nuovo progetto** finestra di dialogo, scegliere **Cloud > applicazione di Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-112">In hello **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

<span data-ttu-id="bb9f1-113">Nome di un'applicazione hello **MyApplication** e premere **OK**.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-113">Name hello application **MyApplication** and press **OK**.</span></span>

   
![Finestra di dialogo Nuovo progetto in Visual Studio][1]

<span data-ttu-id="bb9f1-115">È possibile creare qualsiasi tipo di applicazione di Service Fabric dalla finestra di dialogo successiva hello.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-115">You can create any type of Service Fabric application from hello next dialog.</span></span> <span data-ttu-id="bb9f1-116">Per questa guida introduttiva scegliere **Servizio con stato**.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-116">For this Quickstart, choose **Stateful Service**.</span></span>

<span data-ttu-id="bb9f1-117">Nome servizio hello **MyStatefulService** e premere **OK**.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-117">Name hello service **MyStatefulService** and press **OK**.</span></span>

![Finestra di dialogo Nuovo servizio in Visual Studio][2]


<span data-ttu-id="bb9f1-119">Visual Studio crea il progetto di applicazione hello e il progetto di servizio con stato hello e li visualizza in Esplora soluzioni.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-119">Visual Studio creates hello application project and hello stateful service project and displays them in Solution Explorer.</span></span>

![Esplora soluzioni dopo la creazione dell'applicazione con servizio con stato][3]

<span data-ttu-id="bb9f1-121">progetto di applicazione Hello (**MyApplication**) non contiene il codice direttamente.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-121">hello application project (**MyApplication**) does not contain any code directly.</span></span> <span data-ttu-id="bb9f1-122">Fa invece riferimento a un set di progetti di servizio.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-122">Instead, it references a set of service projects.</span></span> <span data-ttu-id="bb9f1-123">Include inoltre altri tre tipi di contenuto:</span><span class="sxs-lookup"><span data-stu-id="bb9f1-123">In addition, it contains three other types of content:</span></span>

* <span data-ttu-id="bb9f1-124">**Profili di pubblicazione**</span><span class="sxs-lookup"><span data-stu-id="bb9f1-124">**Publish profiles**</span></span>  
<span data-ttu-id="bb9f1-125">Profili per la distribuzione di ambienti toodifferent.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-125">Profiles for deploying toodifferent environments.</span></span>

* <span data-ttu-id="bb9f1-126">**Script**</span><span class="sxs-lookup"><span data-stu-id="bb9f1-126">**Scripts**</span></span>  
<span data-ttu-id="bb9f1-127">Script di PowerShell per distribuire o aggiornare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-127">PowerShell script for deploying/upgrading your application.</span></span>

* <span data-ttu-id="bb9f1-128">**Definizione di applicazione**</span><span class="sxs-lookup"><span data-stu-id="bb9f1-128">**Application definition**</span></span>  
<span data-ttu-id="bb9f1-129">Include file ApplicationManifest XML hello in *ApplicationPackageRoot* che descrive la composizione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-129">Includes hello ApplicationManifest.xml file under *ApplicationPackageRoot* which describes your application's composition.</span></span> <span data-ttu-id="bb9f1-130">I file dei parametri dell'applicazione associati sono in *ApplicationParameters*, che può essere utilizzato toospecify parametri specifici dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-130">Associated application parameter files are under *ApplicationParameters*, which can be used toospecify environment-specific parameters.</span></span> <span data-ttu-id="bb9f1-131">Istruzioni SELECT di Visual Studio associato a un file di parametro dell'applicazione specificato nel hello profilo di pubblicazione durante l'ambiente di distribuzione tooa specifico.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-131">Visual Studio selects an application parameter file that's specified in hello associated publish profile during deployment tooa specific environment.</span></span>
    
<span data-ttu-id="bb9f1-132">Per una panoramica del contenuto di hello hello del progetto di servizio, vedere [Introduzione a servizi affidabili](service-fabric-reliable-services-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="bb9f1-132">For an overview of hello contents of hello service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="deploy-and-debug-hello-application"></a><span data-ttu-id="bb9f1-133">Distribuire ed eseguire il debug di un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="bb9f1-133">Deploy and debug hello application</span></span>

<span data-ttu-id="bb9f1-134">A questo punto, eseguire l'applicazione creata.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-134">Now that you have an application, run it.</span></span>

<span data-ttu-id="bb9f1-135">In Visual Studio, premere `F5` toodeploy per il debug di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-135">In Visual Studio, press `F5` toodeploy hello application for debugging.</span></span>

>[!NOTE]
><span data-ttu-id="bb9f1-136">Hello prima eseguire e distribuire un'applicazione hello in locale, Visual Studio crea un cluster locale per il debug.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-136">hello first time you run and deploy hello application locally, Visual Studio creates a local cluster for debugging.</span></span> <span data-ttu-id="bb9f1-137">Questa operazione potrebbe richiedere tempo.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-137">This may take some time.</span></span> <span data-ttu-id="bb9f1-138">lo stato di creazione di cluster Hello viene visualizzato nella finestra di output di hello Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-138">hello cluster creation status is displayed in hello Visual Studio output window.</span></span>

<span data-ttu-id="bb9f1-139">Quando il cluster hello è pronto, si riceve una notifica di hello cluster locale Gestione applicazione area di notifica inclusa hello SDK.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-139">When hello cluster is ready, you get a notification from hello local cluster system tray manager application included with hello SDK.</span></span>
   
![Notifica della barra delle applicazioni per il cluster locale][4]

<span data-ttu-id="bb9f1-141">Una volta viene avviata l'applicazione hello, Visual Studio automaticamente apparirà hello **Visualizzatore eventi di diagnostica**, in cui è possibile visualizzare l'output di traccia dai servizi.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-141">Once hello application starts, Visual Studio automatically brings up hello **Diagnostics Event Viewer**, where you can see trace output from your services.</span></span>
   
![Visualizzatore eventi di diagnostica][5]

<span data-ttu-id="bb9f1-143">Hello modello di servizio con stato utilizzassimo mostra semplicemente un valore di contatore incremento in hello `RunAsync` metodo **MyStatefulService.cs**.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-143">hello stateful service template we used simply shows a counter value incrementing in hello `RunAsync` method of **MyStatefulService.cs**.</span></span>

<span data-ttu-id="bb9f1-144">Espandere una delle hello eventi toosee ulteriori dettagli, incluso il nodo hello in cui è in esecuzione codice hello.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-144">Expand one of hello events toosee more details, including hello node where hello code is running.</span></span> <span data-ttu-id="bb9f1-145">In questo caso è \_Node\_2, anche se nel computer locale potrebbe essere diverso.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-145">In this case, it is \_Node\_2, though it may differ on your machine.</span></span>
   
![Dettaglio del visualizzatore eventi di diagnostica][6]

<span data-ttu-id="bb9f1-147">cluster locale Hello contiene cinque nodi ospitati in un singolo computer.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-147">hello local cluster contains five nodes hosted on a single machine.</span></span> <span data-ttu-id="bb9f1-148">In un ambiente di produzione, ogni nodo è ospitato in una macchina virtuale o un computer fisico distinto.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-148">In a production environment, each node is hosted on a distinct physical or virtual machine.</span></span> <span data-ttu-id="bb9f1-149">perdita di hello toosimulate di una macchina durante lo eserciterebbe hello Visual Studio del debugger in hello stessa ora e diamo un'occhiata a uno dei nodi cluster locale hello hello.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-149">toosimulate hello loss of a machine while exercising hello Visual Studio debugger at hello same time, let's take down one of hello nodes on hello local cluster.</span></span>

<span data-ttu-id="bb9f1-150">In hello **Esplora** finestra, aprire **MyStatefulService.cs**.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-150">In hello **Solution Explorer** window, open **MyStatefulService.cs**.</span></span> 

<span data-ttu-id="bb9f1-151">Trovare hello `RunAsync` metodo e impostare un punto di interruzione della prima riga hello del metodo hello.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-151">Find hello `RunAsync` method and set a breakpoint on hello first line of hello method.</span></span>

![Punto di interruzione nel metodo RunAsync del servizio con stato][7]

<span data-ttu-id="bb9f1-153">Avviare hello **Service Fabric Explorer** strumento facendo clic su hello **gestione Cluster locale** applicazione area di notifica e scegliere **gestire Cluster locale**.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-153">Launch hello **Service Fabric Explorer** tool by right-clicking on hello **Local Cluster Manager** system tray application and choose **Manage Local Cluster**.</span></span>

![Avviare Service Fabric Explorer da hello gestione Cluster locale][systray-launch-sfx]

<span data-ttu-id="bb9f1-155">[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) offre una rappresentazione visiva del cluster,</span><span class="sxs-lookup"><span data-stu-id="bb9f1-155">[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) offers a visual representation of a cluster.</span></span> <span data-ttu-id="bb9f1-156">Include set hello di applicazioni distribuite tooit e nodi fisici che compongono il set di hello.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-156">It includes hello set of applications deployed tooit and hello set of physical nodes that make it up.</span></span>

<span data-ttu-id="bb9f1-157">Nel riquadro sinistro hello espandere **Cluster > nodi** e trova hello nodo in cui viene eseguito il codice.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-157">In hello left pane, expand **Cluster > Nodes** and find hello node where your code is running.</span></span>

<span data-ttu-id="bb9f1-158">Fare clic su **azioni > Disattiva (riavvio)** toosimulate un riavvio del computer.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-158">Click **Actions > Deactivate (Restart)** toosimulate a machine restarting.</span></span>

![Arresto di un nodo in Service Fabric Explorer][sfx-stop-node]

<span data-ttu-id="bb9f1-160">Temporaneamente, verrà visualizzato il punto di interruzione raggiunto in Visual Studio come calcolo hello stavi facendo facilmente in un nodo viene eseguito il failover tooanother.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-160">Momentarily, you should see your breakpoint hit in Visual Studio as hello computation you were doing on one node seamlessly fails over tooanother.</span></span>


<span data-ttu-id="bb9f1-161">Successivamente, restituire toohello Visualizzatore eventi di diagnostica e osservare i messaggi hello.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-161">Next, return toohello Diagnostic Events Viewer and observe hello messages.</span></span> <span data-ttu-id="bb9f1-162">contatore Hello continua incremento, anche se gli eventi di hello effettivamente derivano da un nodo diverso.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-162">hello counter has continued incrementing, even though hello events are actually coming from a different node.</span></span>

![Visualizzatore eventi di diagnostica dopo il failover][diagnostic-events-viewer-detail-post-failover]

## <a name="cleaning-up-hello-local-cluster-optional"></a><span data-ttu-id="bb9f1-164">Pulizia dei cluster locale hello (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="bb9f1-164">Cleaning up hello local cluster (optional)</span></span>

<span data-ttu-id="bb9f1-165">Tenere presente che il cluster locale è reale.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-165">Remember, this local cluster is real.</span></span> <span data-ttu-id="bb9f1-166">Arrestare il debugger hello rimuove l'istanza dell'applicazione e Annulla la registrazione di tipo di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-166">Stopping hello debugger removes your application instance and unregisters hello application type.</span></span> <span data-ttu-id="bb9f1-167">Tuttavia, i cluster hello continua toorun in background hello.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-167">However, hello cluster continues toorun in hello background.</span></span> <span data-ttu-id="bb9f1-168">Quando sarai pronto toostop cluster locale di hello, sono disponibili due opzioni.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-168">When you're ready toostop hello local cluster, there are a couple options.</span></span>

### <a name="keep-application-and-trace-data"></a><span data-ttu-id="bb9f1-169">Mantenere i dati applicazione e di traccia</span><span class="sxs-lookup"><span data-stu-id="bb9f1-169">Keep application and trace data</span></span>

<span data-ttu-id="bb9f1-170">Arrestare il cluster di hello facendo clic su hello **gestione Cluster locale** applicazione area di notifica e quindi scegliere **arrestare Cluster locale**.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-170">Shut down hello cluster by right-clicking on hello **Local Cluster Manager** system tray application and then choose **Stop Local Cluster**.</span></span>

### <a name="delete-hello-cluster-and-all-data"></a><span data-ttu-id="bb9f1-171">Eliminare il cluster hello e tutti i dati</span><span class="sxs-lookup"><span data-stu-id="bb9f1-171">Delete hello cluster and all data</span></span>

<span data-ttu-id="bb9f1-172">Rimuovere il cluster di hello facendo clic su hello **gestione Cluster locale** applicazione area di notifica e quindi scegliere **rimuovere Cluster locale**.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-172">Remove hello cluster by right-clicking on hello **Local Cluster Manager** system tray application and then choose **Remove Local Cluster**.</span></span> 

<span data-ttu-id="bb9f1-173">Se si sceglie questa opzione, Visual Studio verrà distribuito nuovamente hello cluster hello successivo hello di eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-173">If you choose this option, Visual Studio will redeploy hello cluster hello next time your run hello application.</span></span> <span data-ttu-id="bb9f1-174">Scegliere questa opzione se non si prevede di cluster locale di hello toouse per un certo tempo o se è necessario tooreclaim risorse.</span><span class="sxs-lookup"><span data-stu-id="bb9f1-174">Choose this option if you don't intend toouse hello local cluster for some time or if you need tooreclaim resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb9f1-175">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bb9f1-175">Next steps</span></span>
<span data-ttu-id="bb9f1-176">Altre informazioni su [Reliable Services](service-fabric-reliable-services-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bb9f1-176">Read more about [reliable services](service-fabric-reliable-services-introduction.md).</span></span>
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
