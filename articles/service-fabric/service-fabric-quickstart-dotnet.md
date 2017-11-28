---
title: un'applicazione .NET Service Fabric in Azure aaaCreate | Documenti Microsoft
description: Creare un'applicazione .NET per Azure utilizzando l'esempio di Guida introduttiva di Service Fabric hello.
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: msfussell
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: mikhegn
ms.openlocfilehash: 20ef88dbf9fb0def31234ef05679a19009b9b529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-net-service-fabric-application-in-azure"></a><span data-ttu-id="ebe32-103">Creare un'applicazione .NET Service Fabric in Azure</span><span class="sxs-lookup"><span data-stu-id="ebe32-103">Create a .NET Service Fabric application in Azure</span></span>
<span data-ttu-id="ebe32-104">Azure Service Fabric è una piattaforma di sistemi distribuiti per la distribuzione e la gestione di microservizi e contenitori scalabili e affidabili.</span><span class="sxs-lookup"><span data-stu-id="ebe32-104">Azure Service Fabric is a distributed systems platform for deploying and managing scalable and reliable microservices and containers.</span></span> 

<span data-ttu-id="ebe32-105">Questa Guida introduttiva viene illustrato come toodeploy il primo tooService di applicazioni .NET dell'infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="ebe32-105">This quickstart shows how toodeploy your first .NET application tooService Fabric.</span></span> <span data-ttu-id="ebe32-106">Al termine, si dispone di un'applicazione voto con un front-end che salva i risultati di voto in un servizio back-end con stato cluster hello web di ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="ebe32-106">When you're finished, you have a voting application with an ASP.NET Core web front-end that saves voting results in a stateful back-end service in hello cluster.</span></span>

![Screenshot dell'applicazione](./media/service-fabric-quickstart-dotnet/application-screenshot.png)

<span data-ttu-id="ebe32-108">Usando questa applicazione, si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="ebe32-108">Using this application you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="ebe32-109">Creare un'applicazione mediante .NET e Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ebe32-109">Create an application using .NET and Service Fabric</span></span>
> * <span data-ttu-id="ebe32-110">Usare ASP.NET Core come front-end Web</span><span class="sxs-lookup"><span data-stu-id="ebe32-110">Use ASP.NET core as a web front-end</span></span>
> * <span data-ttu-id="ebe32-111">Archiviare i dati dell'applicazione in un servizio con stato</span><span class="sxs-lookup"><span data-stu-id="ebe32-111">Store application data in a stateful service</span></span>
> * <span data-ttu-id="ebe32-112">Eseguire il debug dell'applicazione in locale</span><span class="sxs-lookup"><span data-stu-id="ebe32-112">Debug your application locally</span></span>
> * <span data-ttu-id="ebe32-113">Distribuire hello applicazione tooa cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="ebe32-113">Deploy hello application tooa cluster in Azure</span></span>
> * <span data-ttu-id="ebe32-114">Applicazione hello di scalabilità orizzontale in più nodi</span><span class="sxs-lookup"><span data-stu-id="ebe32-114">Scale-out hello application across multiple nodes</span></span>
> * <span data-ttu-id="ebe32-115">Eseguire un aggiornamento in sequenza delle applicazioni</span><span class="sxs-lookup"><span data-stu-id="ebe32-115">Perform a rolling application upgrade</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ebe32-116">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ebe32-116">Prerequisites</span></span>
<span data-ttu-id="ebe32-117">toocomplete questa Guida rapida:</span><span class="sxs-lookup"><span data-stu-id="ebe32-117">toocomplete this quickstart:</span></span>
1. <span data-ttu-id="ebe32-118">[Installare Visual Studio 2017](https://www.visualstudio.com/) con hello **lo sviluppo di Azure** e **sviluppo web ASP.NET e** i carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="ebe32-118">[Install Visual Studio 2017](https://www.visualstudio.com/) with hello **Azure development** and **ASP.NET and web development** workloads.</span></span>
2. [<span data-ttu-id="ebe32-119">Installare Git</span><span class="sxs-lookup"><span data-stu-id="ebe32-119">Install Git</span></span>](https://git-scm.com/)
3. [<span data-ttu-id="ebe32-120">Installare Microsoft Azure Service Fabric SDK hello</span><span class="sxs-lookup"><span data-stu-id="ebe32-120">Install hello Microsoft Azure Service Fabric SDK</span></span>](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK)
4. <span data-ttu-id="ebe32-121">Eseguire hello comando tooenable Visual Studio toodeploy toohello dell'infrastruttura del servizio cluster locale seguente:</span><span class="sxs-lookup"><span data-stu-id="ebe32-121">Run hello following command tooenable Visual Studio toodeploy toohello local Service Fabric cluster:</span></span>
    ```powershell
    Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
    ```

## <a name="download-hello-sample"></a><span data-ttu-id="ebe32-122">Scaricare l'esempio hello</span><span class="sxs-lookup"><span data-stu-id="ebe32-122">Download hello sample</span></span>
<span data-ttu-id="ebe32-123">In una finestra di comando, eseguire hello successivo comando tooclone hello esempio app repository tooyour computer locale.</span><span class="sxs-lookup"><span data-stu-id="ebe32-123">In a command window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>
```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="run-hello-application-locally"></a><span data-ttu-id="ebe32-124">Eseguire un'applicazione hello in locale</span><span class="sxs-lookup"><span data-stu-id="ebe32-124">Run hello application locally</span></span>
<span data-ttu-id="ebe32-125">Fare doppio clic sull'icona di Visual Studio hello in hello Menu Start e scegliere **Esegui come amministratore**.</span><span class="sxs-lookup"><span data-stu-id="ebe32-125">Right-click hello Visual Studio icon in hello Start Menu and choose **Run as administrator**.</span></span> <span data-ttu-id="ebe32-126">In servizi di tooyour debugger hello tooattach ordine, è necessario toorun Visual Studio come amministratore.</span><span class="sxs-lookup"><span data-stu-id="ebe32-126">In order tooattach hello debugger tooyour services, you need toorun Visual Studio as administrator.</span></span>

<span data-ttu-id="ebe32-127">Aprire hello **Voting.sln** soluzione di Visual Studio dal repository hello è stato clonato.</span><span class="sxs-lookup"><span data-stu-id="ebe32-127">Open hello **Voting.sln** Visual Studio solution from hello repository you cloned.</span></span>

<span data-ttu-id="ebe32-128">un'applicazione hello toodeploy, premere **F5**.</span><span class="sxs-lookup"><span data-stu-id="ebe32-128">toodeploy hello application, press **F5**.</span></span>

> [!NOTE]
> <span data-ttu-id="ebe32-129">Hello prima eseguire e distribuire un'applicazione hello, Visual Studio crea un cluster locale per il debug.</span><span class="sxs-lookup"><span data-stu-id="ebe32-129">hello first time you run and deploy hello application, Visual Studio creates a local cluster for debugging.</span></span> <span data-ttu-id="ebe32-130">Questa operazione può richiedere del tempo.</span><span class="sxs-lookup"><span data-stu-id="ebe32-130">This operation may take some time.</span></span> <span data-ttu-id="ebe32-131">lo stato di creazione di cluster Hello viene visualizzato nella finestra di output di hello Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ebe32-131">hello cluster creation status is displayed in hello Visual Studio output window.</span></span>

<span data-ttu-id="ebe32-132">Una volta completata la distribuzione di hello, avviare un browser e aprire questa pagina: `http://localhost:8080` -web hello front-end dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="ebe32-132">When hello deployment is complete, launch a browser and open this page: `http://localhost:8080` - hello web front-end of hello application.</span></span>

![Front-end dell'applicazione](./media/service-fabric-quickstart-dotnet/application-screenshot-new.png)

<span data-ttu-id="ebe32-134">È ora possibile aggiungere un set di opzioni per le votazioni e iniziare a raccogliere i voti.</span><span class="sxs-lookup"><span data-stu-id="ebe32-134">You can now add a set of voting options, and start taking votes.</span></span> <span data-ttu-id="ebe32-135">esecuzione dell'applicazione Hello e archivia tutti i dati del cluster di Service Fabric, senza necessità di hello di un database separato.</span><span class="sxs-lookup"><span data-stu-id="ebe32-135">hello application runs and stores all data in your Service Fabric cluster, without hello need for a separate database.</span></span>

## <a name="walk-through-hello-voting-sample-application"></a><span data-ttu-id="ebe32-136">Procedura dettagliata hello voto applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="ebe32-136">Walk through hello voting sample application</span></span>
<span data-ttu-id="ebe32-137">Hello voto applicazione è costituita da due servizi:</span><span class="sxs-lookup"><span data-stu-id="ebe32-137">hello voting application consists of two services:</span></span>
- <span data-ttu-id="ebe32-138">Il servizio front-end (VotingWeb) Web - An ASP.NET Core web front-end del servizio, che serve a pagina web hello ed espone web toocommunicate API con il servizio back-end hello.</span><span class="sxs-lookup"><span data-stu-id="ebe32-138">Web front-end service (VotingWeb)- An ASP.NET Core web front-end service, which serves hello web page and exposes web APIs toocommunicate with hello backend service.</span></span>
- <span data-ttu-id="ebe32-139">Il servizio back-end (VotingData)-servizio web di ASP.NET Core, che espone un voto di hello toostore API comporta un dizionario affidabile persistente su disco.</span><span class="sxs-lookup"><span data-stu-id="ebe32-139">Back-end service (VotingData)- An ASP.NET Core web service, which exposes an API toostore hello vote results in a reliable dictionary persisted on disk.</span></span>

![Diagramma dell'applicazione](./media/service-fabric-quickstart-dotnet/application-diagram.png)

<span data-ttu-id="ebe32-141">Quando voto hello applicazione hello seguenti si verificano eventi:</span><span class="sxs-lookup"><span data-stu-id="ebe32-141">When you vote in hello application hello following events occur:</span></span>
1. <span data-ttu-id="ebe32-142">JavaScript invia API web toohello richiesta di voto hello in servizio front-end web di hello come una richiesta HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="ebe32-142">A JavaScript sends hello vote request toohello web API in hello web front-end service as an HTTP PUT request.</span></span>

2. <span data-ttu-id="ebe32-143">servizio front-end web di Hello Usa un proxy toolocate e inoltrare un servizio back-end toohello di richiesta HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="ebe32-143">hello web front-end service uses a proxy toolocate and forward an HTTP PUT request toohello back-end service.</span></span>

3. <span data-ttu-id="ebe32-144">servizio back-end Hello accetta la richiesta in ingresso hello e archivi hello aggiornamento risultato in un dizionario affidabile, che ottiene i nodi toomultiple replicati all'interno di cluster hello e persistente su disco.</span><span class="sxs-lookup"><span data-stu-id="ebe32-144">hello back-end service takes hello incoming request, and stores hello updated result in a reliable dictionary, which gets replicated toomultiple nodes within hello cluster and persisted on disk.</span></span> <span data-ttu-id="ebe32-145">Dati dell'applicazione hello tutti archiviati in cluster hello, pertanto non è necessario alcun database.</span><span class="sxs-lookup"><span data-stu-id="ebe32-145">All hello application's data is stored in hello cluster, so no database is needed.</span></span>

## <a name="debug-in-visual-studio"></a><span data-ttu-id="ebe32-146">Eseguire il debug in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ebe32-146">Debug in Visual Studio</span></span>
<span data-ttu-id="ebe32-147">Durante il debug dell'applicazione in Visual Studio, viene usato un cluster di sviluppo locale di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ebe32-147">When debugging application in Visual Studio, you are using a local Service Fabric development cluster.</span></span> <span data-ttu-id="ebe32-148">È necessario hello opzione tooadjust lo scenario di tooyour esperienza di debug.</span><span class="sxs-lookup"><span data-stu-id="ebe32-148">You have hello option tooadjust your debugging experience tooyour scenario.</span></span> <span data-ttu-id="ebe32-149">In questa applicazione, i dati vengono archiviati nel servizio back-end tramite un oggetto Reliable Dictionary.</span><span class="sxs-lookup"><span data-stu-id="ebe32-149">In this application, we store data in our back-end service, using a reliable dictionary.</span></span> <span data-ttu-id="ebe32-150">Visual Studio rimuove un'applicazione hello per impostazione predefinita, quando si arresta il debugger hello.</span><span class="sxs-lookup"><span data-stu-id="ebe32-150">Visual Studio removes hello application per default when you stop hello debugger.</span></span> <span data-ttu-id="ebe32-151">Rimozione di un'applicazione hello comporta hello dati back-end hello tooalso servizio da rimuovere.</span><span class="sxs-lookup"><span data-stu-id="ebe32-151">Removing hello application causes hello data in hello back-end service tooalso be removed.</span></span> <span data-ttu-id="ebe32-152">dati di hello toopersist tra le sessioni di debug, è possibile modificare hello **modalità di Debug dell'applicazione** come proprietà nel hello **voto** progetto in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ebe32-152">toopersist hello data between debugging sessions, you can change hello **Application Debug Mode** as a property on hello **Voting** project in Visual Studio.</span></span>

<span data-ttu-id="ebe32-153">toolook cosa accade nel codice hello, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ebe32-153">toolook at what happens in hello code, complete hello following steps:</span></span>
1. <span data-ttu-id="ebe32-154">Aprire hello **VotesController.cs** file e impostare un punto di interruzione dell'API web hello **inserire** (metodo) (riga 47), è possibile cercare file hello in hello Esplora soluzioni in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ebe32-154">Open hello **VotesController.cs** file and set a breakpoint in hello web API's **Put** method (line 47) - You can search for hello file in hello Solution Explorer in Visual Studio.</span></span>

2. <span data-ttu-id="ebe32-155">Aprire hello **VoteDataController.cs** file e impostare un punto di interruzione in questa web API **inserire** (metodo) (riga 50).</span><span class="sxs-lookup"><span data-stu-id="ebe32-155">Open hello **VoteDataController.cs** file and set a breakpoint in this web API's **Put** method (line 50).</span></span>

3. <span data-ttu-id="ebe32-156">Tornare indietro del browser toohello e fare clic su un'opzione di voto oppure aggiungere una nuova opzione di voto.</span><span class="sxs-lookup"><span data-stu-id="ebe32-156">Go back toohello browser and click a voting option or add a new voting option.</span></span> <span data-ttu-id="ebe32-157">È stato raggiunto punto di interruzione prima hello nel controller api hello web front-end.</span><span class="sxs-lookup"><span data-stu-id="ebe32-157">You hit hello first breakpoint in hello web front-end's api controller.</span></span>
    - <span data-ttu-id="ebe32-158">Si tratta di dove hello JavaScript nel browser hello invia un controller di API web toohello richiesta nel servizio front-end hello.</span><span class="sxs-lookup"><span data-stu-id="ebe32-158">This is where hello JavaScript in hello browser sends a request toohello web API controller in hello front-end service.</span></span>
    
    ![Aggiungere il servizio front-end di voto](./media/service-fabric-quickstart-dotnet/addvote-frontend.png)

    - <span data-ttu-id="ebe32-160">Prima di tutto è costruire hello URL toohello ReverseProxy per il servizio back-end **(1)**.</span><span class="sxs-lookup"><span data-stu-id="ebe32-160">First we construct hello URL toohello ReverseProxy for our back-end service **(1)**.</span></span>
    - <span data-ttu-id="ebe32-161">Quindi inviare hello HTTP PUT richiesta toohello ReverseProxy **(2)**.</span><span class="sxs-lookup"><span data-stu-id="ebe32-161">Then we send hello HTTP PUT Request toohello ReverseProxy **(2)**.</span></span>
    - <span data-ttu-id="ebe32-162">Infine hello restituiamo risposta hello client toohello servizio back-end di hello **(3)**.</span><span class="sxs-lookup"><span data-stu-id="ebe32-162">Finally hello we return hello response from hello back-end service toohello client **(3)**.</span></span>

4. <span data-ttu-id="ebe32-163">Premere **F5** toocontinue</span><span class="sxs-lookup"><span data-stu-id="ebe32-163">Press **F5** toocontinue</span></span>
    - <span data-ttu-id="ebe32-164">Sono ora al punto di interruzione hello in servizio back-end hello.</span><span class="sxs-lookup"><span data-stu-id="ebe32-164">You are now at hello break point in hello back-end service.</span></span>
    
    ![Aggiungere il servizio back-end di voto](./media/service-fabric-quickstart-dotnet/addvote-backend.png)

    - <span data-ttu-id="ebe32-166">Nella prima riga di hello nel metodo hello **(1)** usiamo hello `StateManager` tooget o aggiungere un dizionario affidabile denominato `counts`.</span><span class="sxs-lookup"><span data-stu-id="ebe32-166">In hello first line in hello method **(1)** we are using hello `StateManager` tooget or add a reliable dictionary called `counts`.</span></span>
    - <span data-ttu-id="ebe32-167">Tutte le interazioni con i valori in un oggetto Reliable Dictionary richiedono una transazione, che viene creata dall'istruzione using **(2)**.</span><span class="sxs-lookup"><span data-stu-id="ebe32-167">All interactions with values in a reliable dictionary require a transaction, this using statement **(2)** creates that transaction.</span></span>
    - <span data-ttu-id="ebe32-168">Transazione hello, è stato quindi aggiornare il valore di hello della chiave pertinenti di hello per hello voto opzione e commit hello operazione **(3)**.</span><span class="sxs-lookup"><span data-stu-id="ebe32-168">In hello transaction, we then update hello value of hello relevant key for hello voting option and commits hello operation **(3)**.</span></span> <span data-ttu-id="ebe32-169">Dopo il commit di hello metodo viene restituito, hello dati viene aggiornati nel dizionario hello e replicati tooother nodi nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ebe32-169">Once hello commit method returns, hello data is updated in hello dictionary and replicated tooother nodes in hello cluster.</span></span> <span data-ttu-id="ebe32-170">dati Hello sono ora archiviati in modo sicuro in cluster hello e servizio back-end hello failover dei nodi tooother, persistono dati hello disponibili.</span><span class="sxs-lookup"><span data-stu-id="ebe32-170">hello data is now safely stored in hello cluster, and hello back-end service can fail over tooother nodes, still having hello data available.</span></span>
5. <span data-ttu-id="ebe32-171">Premere **F5** toocontinue</span><span class="sxs-lookup"><span data-stu-id="ebe32-171">Press **F5** toocontinue</span></span>

<span data-ttu-id="ebe32-172">hello toostop debug sessione, premere **MAIUSC + F5**.</span><span class="sxs-lookup"><span data-stu-id="ebe32-172">toostop hello debugging session, press **Shift+F5**.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="ebe32-173">Distribuire tooAzure applicazione hello</span><span class="sxs-lookup"><span data-stu-id="ebe32-173">Deploy hello application tooAzure</span></span>
<span data-ttu-id="ebe32-174">toodeploy cluster tooa hello applicazione in Azure, è possibile scegliere toocreate la propria cluster, oppure utilizzare un Cluster di terze parti.</span><span class="sxs-lookup"><span data-stu-id="ebe32-174">toodeploy hello application tooa cluster in Azure, you can either choose toocreate your own cluster, or use a Party Cluster.</span></span>

<span data-ttu-id="ebe32-175">Cluster di terze parti sono i cluster di Service Fabric gratuito, periodo di tempo limitato ospitati in Azure e vengono eseguiti dal team di Service Fabric hello in tutti gli utenti possono distribuire le applicazioni e informazioni sulla piattaforma hello.</span><span class="sxs-lookup"><span data-stu-id="ebe32-175">Party clusters are free, limited-time Service Fabric clusters hosted on Azure and run by hello Service Fabric team where anyone can deploy applications and learn about hello platform.</span></span> <span data-ttu-id="ebe32-176">tooget accesso tooa Cluster di terze parti, [istruzioni hello](http://aka.ms/tryservicefabric).</span><span class="sxs-lookup"><span data-stu-id="ebe32-176">tooget access tooa Party Cluster, [follow hello instructions](http://aka.ms/tryservicefabric).</span></span> 

<span data-ttu-id="ebe32-177">Per informazioni sulla creazione di un cluster, vedere [Creare il primo cluster di Service Fabric di Azure](service-fabric-get-started-azure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="ebe32-177">For information about creating your own cluster, see [Create your first Service Fabric cluster on Azure](service-fabric-get-started-azure-cluster.md).</span></span>

> [!Note]
> <span data-ttu-id="ebe32-178">il servizio front-end web di Hello è toolisten configurato sulla porta 8080 per il traffico in ingresso.</span><span class="sxs-lookup"><span data-stu-id="ebe32-178">hello web front-end service is configured toolisten on port 8080 for incoming traffic.</span></span> <span data-ttu-id="ebe32-179">Assicurarsi che tale porta sia aperta nel cluster.</span><span class="sxs-lookup"><span data-stu-id="ebe32-179">Make sure that port is open in your cluster.</span></span> <span data-ttu-id="ebe32-180">Se si utilizza hello Cluster di terze parti, questa porta è aperta.</span><span class="sxs-lookup"><span data-stu-id="ebe32-180">If you are using hello Party Cluster, this port is open.</span></span>
>

### <a name="deploy-hello-application-using-visual-studio"></a><span data-ttu-id="ebe32-181">Distribuire l'applicazione hello utilizzando Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ebe32-181">Deploy hello application using Visual Studio</span></span>
<span data-ttu-id="ebe32-182">Ora che un'applicazione hello è pronta, è possibile distribuire cluster tooa direttamente da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ebe32-182">Now that hello application is ready, you can deploy it tooa cluster directly from Visual Studio.</span></span>

1. <span data-ttu-id="ebe32-183">Fare doppio clic su **voto** in hello Esplora soluzioni e scegliere **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="ebe32-183">Right-click **Voting** in hello Solution Explorer and choose **Publish**.</span></span> <span data-ttu-id="ebe32-184">finestra di dialogo pubblicazione Hello viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="ebe32-184">hello Publish dialog appears.</span></span>

    ![Finestra di dialogo Pubblica](./media/service-fabric-quickstart-dotnet/publish-app.png)

2. <span data-ttu-id="ebe32-186">Tipo di Endpoint della connessione hello cluster hello in hello **Endpoint della connessione** campo e fare clic su **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="ebe32-186">Type in hello Connection Endpoint of hello cluster in hello **Connection Endpoint** field and click **Publish**.</span></span> <span data-ttu-id="ebe32-187">Se l'iscrizione per hello Cluster di terze parti, hello Endpoint della connessione viene fornito nel browser hello.</span><span class="sxs-lookup"><span data-stu-id="ebe32-187">When signing up for hello Party Cluster, hello Connection Endpoint is provided in hello browser.</span></span> <span data-ttu-id="ebe32-188">Ad esempio, `winh1x87d1d.westus.cloudapp.azure.com:19000`.</span><span class="sxs-lookup"><span data-stu-id="ebe32-188">- for example, `winh1x87d1d.westus.cloudapp.azure.com:19000`.</span></span>

3. <span data-ttu-id="ebe32-189">Aprire un browser e digitare, ad esempio, nell'indirizzo cluster hello - `http://winh1x87d1d.westus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="ebe32-189">Open a browser and type in hello cluster address - for example, `http://winh1x87d1d.westus.cloudapp.azure.com`.</span></span> <span data-ttu-id="ebe32-190">Dovrebbe essere un'applicazione hello in esecuzione in cluster hello in Azure.</span><span class="sxs-lookup"><span data-stu-id="ebe32-190">You should now see hello application running in hello cluster in Azure.</span></span>

![Front-end dell'applicazione](./media/service-fabric-quickstart-dotnet/application-screenshot-new-azure.png)

## <a name="scale-applications-and-services-in-a-cluster"></a><span data-ttu-id="ebe32-192">Ridimensionare applicazioni e servizi in un cluster</span><span class="sxs-lookup"><span data-stu-id="ebe32-192">Scale applications and services in a cluster</span></span>
<span data-ttu-id="ebe32-193">Servizi di Service Fabric possono essere scalati facilmente in un cluster di tooaccommodate per una modifica nel carico di hello nei servizi di hello.</span><span class="sxs-lookup"><span data-stu-id="ebe32-193">Service Fabric services can easily be scaled across a cluster tooaccommodate for a change in hello load on hello services.</span></span> <span data-ttu-id="ebe32-194">Scalabilità di un servizio modificando hello numero di istanze in esecuzione nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ebe32-194">You scale a service by changing hello number of instances running in hello cluster.</span></span> <span data-ttu-id="ebe32-195">Sono disponibili diversi sistemi per garantire la scalabilità dei servizi: è possibile usare gli script o i comandi di PowerShell oppure l'interfaccia della riga di comando di Service Fabric (sfctl).</span><span class="sxs-lookup"><span data-stu-id="ebe32-195">You have multiple ways of scaling your services, you can use scripts or commands from PowerShell or Service Fabric CLI (sfctl).</span></span> <span data-ttu-id="ebe32-196">In questo esempio verrà usato Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="ebe32-196">In this example, we are using Service Fabric Explorer.</span></span>

<span data-ttu-id="ebe32-197">Service Fabric Explorer viene eseguito in tutti i cluster di Service Fabric e sono accessibili da un browser, esplorando la porta di Gestione cluster HTTP toohello (19080), ad esempio, `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span><span class="sxs-lookup"><span data-stu-id="ebe32-197">Service Fabric Explorer runs in all Service Fabric clusters and can be accessed from a browser, by browsing toohello clusters HTTP management port (19080), for example, `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span></span>

<span data-ttu-id="ebe32-198">hello tooscale servizio front-end web, hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ebe32-198">tooscale hello web front-end service, do hello following steps:</span></span>

1. <span data-ttu-id="ebe32-199">Aprire Service Fabric Explorer nel cluster, ad esempio `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span><span class="sxs-lookup"><span data-stu-id="ebe32-199">Open Service Fabric Explorer in your cluster - for example,`http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span></span>
2. <span data-ttu-id="ebe32-200">Fare clic su Avanti toohello di hello puntini di sospensione (tre punti) **fabric: / voto/VotingWeb** nodo in treeview hello e scegliere **servizio scala**.</span><span class="sxs-lookup"><span data-stu-id="ebe32-200">Click on hello ellipsis (three dots) next toohello **fabric:/Voting/VotingWeb** node in hello treeview and choose **Scale Service**.</span></span>

    ![Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/service-fabric-explorer-scale.png)

    <span data-ttu-id="ebe32-202">È ora possibile scegliere numero hello tooscale istanze del servizio front-end web di hello.</span><span class="sxs-lookup"><span data-stu-id="ebe32-202">You can now choose tooscale hello number of instances of hello web front-end service.</span></span>

3. <span data-ttu-id="ebe32-203">Modificare il numero di hello troppo**2** e fare clic su **servizio scala**.</span><span class="sxs-lookup"><span data-stu-id="ebe32-203">Change hello number too**2** and click **Scale Service**.</span></span>
4. <span data-ttu-id="ebe32-204">Fare clic su hello **fabric: / voto/VotingWeb** nodo nella visualizzazione struttura ad albero di hello ed espandere il nodo di partizione hello (rappresentato da un GUID).</span><span class="sxs-lookup"><span data-stu-id="ebe32-204">Click on hello **fabric:/Voting/VotingWeb** node in hello tree-view and expand hello partition node (represented by a GUID).</span></span>

    ![Ridimensionamento dei servizi in Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/service-fabric-explorer-scaled-service.png)

    <span data-ttu-id="ebe32-206">Si noterà ora che hello servizio dispone di due istanze, e nella visualizzazione ad albero di hello vedere quali nodi eseguire istanze hello in.</span><span class="sxs-lookup"><span data-stu-id="ebe32-206">You can now see that hello service has two instances, and in hello tree view you see which nodes hello instances run on.</span></span>

<span data-ttu-id="ebe32-207">Da questa attività, gestione semplice è raddoppiato risorse hello disponibili per il carico utente tooprocess di servizio front-end.</span><span class="sxs-lookup"><span data-stu-id="ebe32-207">By this simple management task, we doubled hello resources available for our front-end service tooprocess user load.</span></span> <span data-ttu-id="ebe32-208">È importante toounderstand che non è necessario più istanze di un servizio di toohave eseguirlo in modo affidabile.</span><span class="sxs-lookup"><span data-stu-id="ebe32-208">It's important toounderstand that you do not need multiple instances of a service toohave it run reliably.</span></span> <span data-ttu-id="ebe32-209">Se non è un servizio, Service Fabric assicura che una nuova istanza del servizio viene eseguito nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ebe32-209">If a service fails, Service Fabric makes sure a new service instance runs in hello cluster.</span></span>

## <a name="perform-a-rolling-application-upgrade"></a><span data-ttu-id="ebe32-210">Eseguire un aggiornamento in sequenza delle applicazioni</span><span class="sxs-lookup"><span data-stu-id="ebe32-210">Perform a rolling application upgrade</span></span>
<span data-ttu-id="ebe32-211">Quando si distribuisce una nuova applicazione di tooyour gli aggiornamenti, Service Fabric esegue il rollup di aggiornamento hello in modo sicuro.</span><span class="sxs-lookup"><span data-stu-id="ebe32-211">When deploying new updates tooyour application, Service Fabric rolls out hello update in a safe way.</span></span> <span data-ttu-id="ebe32-212">Gli aggiornamenti in sequenza non comportano tempi di inattività durante l'aggiornamento e consentono il rollback automatico in caso di errori.</span><span class="sxs-lookup"><span data-stu-id="ebe32-212">Rolling upgrades gives you no downtime while upgrading as well as automated rollback should errors occur.</span></span>

<span data-ttu-id="ebe32-213">tooupgrade applicazione hello, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="ebe32-213">tooupgrade hello application, do hello following:</span></span>

1. <span data-ttu-id="ebe32-214">Aprire hello **cshtml** file in Visual Studio, è possibile cercare file hello in hello Esplora soluzioni in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ebe32-214">Open hello **Index.cshtml** file in Visual Studio - You can search for hello file in hello Solution Explorer in Visual Studio.</span></span>
2. <span data-ttu-id="ebe32-215">Tramite l'aggiunta di testo, ad esempio, modificare il titolo di hello nella pagina hello.</span><span class="sxs-lookup"><span data-stu-id="ebe32-215">Change hello heading on hello page by adding some text - for example.</span></span>
    ```html
        <div class="col-xs-8 col-xs-offset-2 text-center">
            <h2>Service Fabric Voting Sample v2</h2>
        </div>
    ```
3. <span data-ttu-id="ebe32-216">Salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="ebe32-216">Save hello file.</span></span>
4. <span data-ttu-id="ebe32-217">Fare doppio clic su **voto** in hello Esplora soluzioni e scegliere **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="ebe32-217">Right-click **Voting** in hello Solution Explorer and choose **Publish**.</span></span> <span data-ttu-id="ebe32-218">finestra di dialogo pubblicazione Hello viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="ebe32-218">hello Publish dialog appears.</span></span>
5. <span data-ttu-id="ebe32-219">Fare clic su hello **versione manifesto** pulsante toochange hello versione servizio hello e applicazione.</span><span class="sxs-lookup"><span data-stu-id="ebe32-219">Click hello **Manifest Version** button toochange hello version of hello service and application.</span></span>
6. <span data-ttu-id="ebe32-220">Modifica di versione di hello di hello **codice** elemento sotto **VotingWebPkg** troppo "2.0.0", ad esempio e fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="ebe32-220">Change hello version of hello **Code** element under **VotingWebPkg** too"2.0.0", for example, and click **Save**.</span></span>

    ![Finestra di dialogo Modifica versione](./media/service-fabric-quickstart-dotnet/change-version.png)
7. <span data-ttu-id="ebe32-222">In hello **pubblicare l'applicazione di Service Fabric** finestra di dialogo, la casella di controllo di controllo hello hello aggiornamento dell'applicazione e fare clic su **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="ebe32-222">In hello **Publish Service Fabric Application** dialog, check hello Upgrade hello Application checkbox, and click **Publish**.</span></span>

    ![Impostazione di aggiornamento nella finestra di dialogo Pubblica](./media/service-fabric-quickstart-dotnet/upgrade-app.png)
8. <span data-ttu-id="ebe32-224">Aprire il browser e passare ad esempio l'indirizzo del cluster toohello sulla porta 19080 - `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span><span class="sxs-lookup"><span data-stu-id="ebe32-224">Open your browser and browse toohello cluster address on port 19080 - for example, `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span></span>
9. <span data-ttu-id="ebe32-225">Fare clic su hello **applicazioni** nodo nella visualizzazione ad albero di hello e quindi **gli aggiornamenti in corso** nel riquadro di destra hello.</span><span class="sxs-lookup"><span data-stu-id="ebe32-225">Click on hello **Applications** node in hello tree view, and then **Upgrades in Progress** in hello right-hand pane.</span></span> <span data-ttu-id="ebe32-226">Viene visualizzato come aggiornamento hello transita attraverso domini di aggiornamento hello del cluster, assicurarsi che ogni dominio sia integro prima di procedere toohello accanto.</span><span class="sxs-lookup"><span data-stu-id="ebe32-226">You see how hello upgrade rolls through hello upgrade domains in your cluster, making sure each domain is healthy before proceeding toohello next.</span></span>
    <span data-ttu-id="ebe32-227">![Visualizzazione dell'aggiornamento in Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/upgrading.png)</span><span class="sxs-lookup"><span data-stu-id="ebe32-227">![Upgrade View in Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/upgrading.png)</span></span>

    <span data-ttu-id="ebe32-228">Service Fabric rende aggiornamenti sicuro in attesa di due minuti dopo l'aggiornamento del servizio hello in ogni nodo cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ebe32-228">Service Fabric makes upgrades safe by waiting two minutes after upgrading hello service on each node in hello cluster.</span></span> <span data-ttu-id="ebe32-229">Prevedere hello intero aggiornamento tootake circa 8 minuti.</span><span class="sxs-lookup"><span data-stu-id="ebe32-229">Expect hello entire update tootake approximately eight minutes.</span></span>

10. <span data-ttu-id="ebe32-230">Durante l'aggiornamento di hello è in esecuzione, è possibile utilizzare ancora un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="ebe32-230">While hello upgrade is running, you can still use hello application.</span></span> <span data-ttu-id="ebe32-231">Poiché si dispone di due istanze del servizio di hello in esecuzione nel cluster hello, alcune delle richieste può ottenere una versione aggiornata dell'applicazione hello, mentre altri potrebbero comunque essere la versione precedente di hello.</span><span class="sxs-lookup"><span data-stu-id="ebe32-231">Because you have two instances of hello service running in hello cluster, some of your requests may get an upgraded version of hello application, while others may still get hello old version.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ebe32-232">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ebe32-232">Next steps</span></span>
<span data-ttu-id="ebe32-233">In questa guida introduttiva si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="ebe32-233">In this quickstart, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ebe32-234">Creare un'applicazione mediante .NET e Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ebe32-234">Create an application using .NET and Service Fabric</span></span>
> * <span data-ttu-id="ebe32-235">Usare ASP.NET Core come front-end Web</span><span class="sxs-lookup"><span data-stu-id="ebe32-235">Use ASP.NET core as a web front-end</span></span>
> * <span data-ttu-id="ebe32-236">Archiviare i dati dell'applicazione in un servizio con stato</span><span class="sxs-lookup"><span data-stu-id="ebe32-236">Store application data in a stateful service</span></span>
> * <span data-ttu-id="ebe32-237">Eseguire il debug dell'applicazione in locale</span><span class="sxs-lookup"><span data-stu-id="ebe32-237">Debug your application locally</span></span>
> * <span data-ttu-id="ebe32-238">Distribuire hello applicazione tooa cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="ebe32-238">Deploy hello application tooa cluster in Azure</span></span>
> * <span data-ttu-id="ebe32-239">Applicazione hello di scalabilità orizzontale in più nodi</span><span class="sxs-lookup"><span data-stu-id="ebe32-239">Scale-out hello application across multiple nodes</span></span>
> * <span data-ttu-id="ebe32-240">Eseguire un aggiornamento in sequenza delle applicazioni</span><span class="sxs-lookup"><span data-stu-id="ebe32-240">Perform a rolling application upgrade</span></span>

<span data-ttu-id="ebe32-241">toolearn ulteriori informazioni su Service Fabric e .NET, esaminare in questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="ebe32-241">toolearn more about Service Fabric and .NET, take a look at this tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="ebe32-242">Applicazione .NET in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ebe32-242">.NET application on Service Fabric</span></span>](service-fabric-tutorial-create-dotnet-app.md)