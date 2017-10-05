---
title: "Distribuire un'applicazione di Azure Service Fabric in un cluster di entità | Microsoft Docs"
description: "Informazioni su come distribuire un'applicazione in un cluster di entità."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: msfussell
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: mikhegn
ms.openlocfilehash: 6624d683edb548a65d07ab4012c599faaf940ed0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-an-application-to-a-party-cluster-in-azure"></a><span data-ttu-id="bd03f-103">Distribuire un'applicazione in un cluster di entità in Azure</span><span class="sxs-lookup"><span data-stu-id="bd03f-103">Deploy an application to a Party Cluster in Azure</span></span>
<span data-ttu-id="bd03f-104">Questa esercitazione è la seconda parte di una serie e illustra come distribuire un'applicazione di Azure Service Fabric in un cluster di entità in Azure.</span><span class="sxs-lookup"><span data-stu-id="bd03f-104">This tutorial is part two of a series and shows you how to deploy an Azure Service Fabric application to a Party Cluster in Azure.</span></span>

<span data-ttu-id="bd03f-105">Nella seconda parte della serie di esercitazioni si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="bd03f-105">In part two of the tutorial series, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="bd03f-106">Distribuire un'applicazione in un cluster remoto usando Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bd03f-106">Deploy an application to a remote cluster using Visual Studio</span></span>
> * <span data-ttu-id="bd03f-107">Rimuovere un'applicazione da un cluster usando Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="bd03f-107">Remove an application from a cluster using Service Fabric Explorer</span></span>

<span data-ttu-id="bd03f-108">In questa serie di esercitazioni si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="bd03f-108">In this tutorial series you learn how to:</span></span>
> [!div class="checklist"]
> * [<span data-ttu-id="bd03f-109">Creare un'applicazione di Service Fabric .NET</span><span class="sxs-lookup"><span data-stu-id="bd03f-109">Build a .NET Service Fabric application</span></span>](service-fabric-tutorial-create-dotnet-app.md)
> * <span data-ttu-id="bd03f-110">Distribuire l'applicazione in un cluster remoto</span><span class="sxs-lookup"><span data-stu-id="bd03f-110">Deploy the application to a remote cluster</span></span>
> * [<span data-ttu-id="bd03f-111">Configurare l'integrazione continua e la distribuzione continua usando Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="bd03f-111">Configure CI/CD using Visual Studio Team Services</span></span>](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a><span data-ttu-id="bd03f-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bd03f-112">Prerequisites</span></span>
<span data-ttu-id="bd03f-113">Prima di iniziare questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="bd03f-113">Before you begin this tutorial:</span></span>
- <span data-ttu-id="bd03f-114">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span><span class="sxs-lookup"><span data-stu-id="bd03f-114">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="bd03f-115">[Installare Visual Studio 2017](https://www.visualstudio.com/) e installare i carichi di lavoro **Sviluppo di Azure** e **Sviluppo ASP.NET e Web**.</span><span class="sxs-lookup"><span data-stu-id="bd03f-115">[Install Visual Studio 2017](https://www.visualstudio.com/) and install the **Azure development** and **ASP.NET and web development** workloads.</span></span>
- [<span data-ttu-id="bd03f-116">Installare Service Fabric SDK</span><span class="sxs-lookup"><span data-stu-id="bd03f-116">Install the Service Fabric SDK</span></span>](service-fabric-get-started.md)

## <a name="download-the-voting-sample-application"></a><span data-ttu-id="bd03f-117">Scaricare l'applicazione di voto di esempio</span><span class="sxs-lookup"><span data-stu-id="bd03f-117">Download the Voting sample application</span></span>
<span data-ttu-id="bd03f-118">Se l'applicazione di voto di esempio non è stata compilata nella [parte 1 di questa serie di esercitazioni](service-fabric-tutorial-create-dotnet-app.md), è possibile scaricarla.</span><span class="sxs-lookup"><span data-stu-id="bd03f-118">If you did not build the Voting sample application in [part one of this tutorial series](service-fabric-tutorial-create-dotnet-app.md), you can download it.</span></span> <span data-ttu-id="bd03f-119">In una finestra di comando eseguire il comando seguente per clonare il repository dell'app di esempio nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="bd03f-119">In a command window, run the following command to clone the sample app repository to your local machine.</span></span>

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="set-up-a-party-cluster"></a><span data-ttu-id="bd03f-120">Configurare un cluster di entità</span><span class="sxs-lookup"><span data-stu-id="bd03f-120">Set up a Party Cluster</span></span>
<span data-ttu-id="bd03f-121">I cluster di entità sono cluster Service Fabric gratuiti e disponibili per un periodo di tempo limitato ospitati in Azure e gestiti dal team di Service Fabric, in cui chiunque può distribuire applicazioni e ottenere informazioni sulla piattaforma.</span><span class="sxs-lookup"><span data-stu-id="bd03f-121">Party clusters are free, limited-time Service Fabric clusters hosted on Azure and run by the Service Fabric team where anyone can deploy applications and learn about the platform.</span></span> <span data-ttu-id="bd03f-122">Gratuitamente.</span><span class="sxs-lookup"><span data-stu-id="bd03f-122">For free!</span></span>

<span data-ttu-id="bd03f-123">Per accedere a un cluster di entità, passare a questo sito: http://aka.ms/tryservicefabric e seguire le istruzioni per ottenere l'accesso a un cluster.</span><span class="sxs-lookup"><span data-stu-id="bd03f-123">To get access to a Party Cluster, browse to this site: http://aka.ms/tryservicefabric and follow the instructions to get access to a cluster.</span></span> <span data-ttu-id="bd03f-124">È necessario un account Facebook o GitHub per ottenere l'accesso a un cluster di entità.</span><span class="sxs-lookup"><span data-stu-id="bd03f-124">You need a Facebook or GitHub account to get access to a Party Cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="bd03f-125">I cluster di entità non sono protetti, quindi le applicazioni e tutti i dati inseriti negli stessi possono essere visibili ad altri utenti.</span><span class="sxs-lookup"><span data-stu-id="bd03f-125">Party clusters are not secured, so your applications and any data you put in them may be visible to others.</span></span> <span data-ttu-id="bd03f-126">Non distribuire elementi che gli altri utenti non devono vedere.</span><span class="sxs-lookup"><span data-stu-id="bd03f-126">Don't deploy anything you don't want others to see.</span></span> <span data-ttu-id="bd03f-127">Assicurarsi di leggere tutti i dettagli nelle Condizioni per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="bd03f-127">Be sure to read over our Terms of Use for all the details.</span></span>

## <a name="configure-the-listening-port"></a><span data-ttu-id="bd03f-128">Configurare la porta di ascolto</span><span class="sxs-lookup"><span data-stu-id="bd03f-128">Configure the listening port</span></span>
<span data-ttu-id="bd03f-129">Quando viene creato il servizio front-end VotingWeb, Visual Studio seleziona casualmente una porta su cui il servizio resterà in ascolto.</span><span class="sxs-lookup"><span data-stu-id="bd03f-129">When the VotingWeb front-end service is created, Visual Studio randomly selects a port for the service to listen on.</span></span>  <span data-ttu-id="bd03f-130">Poiché il servizio VotingWeb agisce come front-end per l'applicazione e accetta traffico esterno, è opportuno associare il servizio a una porta fissa e conosciuta.</span><span class="sxs-lookup"><span data-stu-id="bd03f-130">The VotingWeb service acts as the front-end for this application and accepts external traffic, so let's bind that service to a fixed and well-know port.</span></span> <span data-ttu-id="bd03f-131">In Esplora soluzioni aprire *VotingWeb/PackageRoot/ServiceManifest.xml*.</span><span class="sxs-lookup"><span data-stu-id="bd03f-131">In Solution Explorer, open  *VotingWeb/PackageRoot/ServiceManifest.xml*.</span></span>  <span data-ttu-id="bd03f-132">Trovare la risorsa **Endpoint** nella sezione **Risorse** e modificare il valore della **Porta** su 80.</span><span class="sxs-lookup"><span data-stu-id="bd03f-132">Find the **Endpoint** resource in the **Resources** section and change the **Port** value to 80.</span></span>

```xml
<Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port on which to 
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" Port="80" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="bd03f-133">Aggiornare inoltre il valore della proprietà URL applicazione nel progetto Voting in modo che, quando si esegue il debug con il tasto F5, un Web browser si apra sulla porta corretta.</span><span class="sxs-lookup"><span data-stu-id="bd03f-133">Also update the Application URL property value in the Voting project so a web browser opens to the correct port when you debug using 'F5'.</span></span>  <span data-ttu-id="bd03f-134">In Esplora soluzioni selezionare il progetto **Voting** e aggiornare la proprietà **URL applicazione**.</span><span class="sxs-lookup"><span data-stu-id="bd03f-134">In Solution Explorer, select the **Voting** project and update the **Application URL** property.</span></span>

![URL applicazione](./media/service-fabric-tutorial-deploy-app-to-party-cluster/application-url.png)

## <a name="deploy-the-app-to-the-azure"></a><span data-ttu-id="bd03f-136">Distribuire l'app in Azure</span><span class="sxs-lookup"><span data-stu-id="bd03f-136">Deploy the app to the Azure</span></span>
<span data-ttu-id="bd03f-137">Ora che l'applicazione è pronta, è possibile distribuirla nel cluster di entità direttamente da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bd03f-137">Now that the application is ready, you can deploy it to the Party Cluster direct from Visual Studio.</span></span>

1. <span data-ttu-id="bd03f-138">Fare clic con il pulsante destro del mouse su **Voting** in Esplora soluzioni e scegliere **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="bd03f-138">Right-click **Voting** in the Solution Explorer and choose **Publish**.</span></span>

    ![Finestra di dialogo Pubblica](./media/service-fabric-tutorial-deploy-app-to-party-cluster/publish-app.png)

2. <span data-ttu-id="bd03f-140">Digitare l'endpoint della connessione del cluster di entità nel campo **Endpoint connessione** e fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="bd03f-140">Type in the Connection Endpoint of the Party Cluster in the **Connection Endpoint** field and click **Publish**.</span></span>

    <span data-ttu-id="bd03f-141">Completata la pubblicazione, dovrebbe essere possibile inviare una richiesta all'applicazione usando un browser.</span><span class="sxs-lookup"><span data-stu-id="bd03f-141">Once the publish has finished, you should be able to send a request to the application via a browser.</span></span>

3. <span data-ttu-id="bd03f-142">Aprire il browser preferito, digitare l'indirizzo del cluster (l'endpoint di connessione senza le informazioni sulla porta, ad esempio win1kw5649s.westus.cloudapp.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bd03f-142">Open you preferred browser and type in the cluster address (the connection endpoint without the port information - for example, win1kw5649s.westus.cloudapp.azure.com).</span></span>

    <span data-ttu-id="bd03f-143">Deve apparire lo stesso risultato visualizzato quando si esegue l'applicazione in locale.</span><span class="sxs-lookup"><span data-stu-id="bd03f-143">You should now see the same result as you saw when running the application locally.</span></span>

    ![Risposta API dal cluster](./media/service-fabric-tutorial-deploy-app-to-party-cluster/response-from-cluster.png)

## <a name="remove-the-application-from-a-cluster-using-service-fabric-explorer"></a><span data-ttu-id="bd03f-145">Rimuovere l'applicazione da un cluster usando Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="bd03f-145">Remove the application from a cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="bd03f-146">Service Fabric Explorer è un'interfaccia utente grafica che consente di esplorare e gestire le applicazioni in un cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="bd03f-146">Service Fabric Explorer is a graphical user interface to explore and manage applications in a Service Fabric cluster.</span></span>

<span data-ttu-id="bd03f-147">Per rimuovere l'applicazione dal cluster di entità:</span><span class="sxs-lookup"><span data-stu-id="bd03f-147">To remove the application from the Party Cluster:</span></span>

1. <span data-ttu-id="bd03f-148">Passare a Service Fabric Explorer usando il collegamento indicato nella pagina di iscrizione al cluster di entità.</span><span class="sxs-lookup"><span data-stu-id="bd03f-148">Browse to the Service Fabric Explorer, using the link provided by the Party Cluster sign-up page.</span></span> <span data-ttu-id="bd03f-149">Ad esempio, http://win1kw5649s.westus.cloudapp.azure.com:19080/Explorer/index.html.</span><span class="sxs-lookup"><span data-stu-id="bd03f-149">For example, http://win1kw5649s.westus.cloudapp.azure.com:19080/Explorer/index.html.</span></span>

2. <span data-ttu-id="bd03f-150">In Service Fabric Explorer passare al nodo **fabric://Voting** nella visualizzazione struttura ad albero sul lato sinistro.</span><span class="sxs-lookup"><span data-stu-id="bd03f-150">In Service Fabric Explorer, navigate to the **fabric://Voting** node in the treeview on the left-hand side.</span></span>

3. <span data-ttu-id="bd03f-151">Fare clic sul pulsante **Azione** nel riquadro **Informazioni di base** a destra e scegliere **Elimina applicazione**.</span><span class="sxs-lookup"><span data-stu-id="bd03f-151">Click the **Action** button in the right-hand **Essentials** pane, and choose **Delete Application**.</span></span> <span data-ttu-id="bd03f-152">Confermare l'eliminazione dell'istanza di applicazione per rimuovere l'istanza dell'applicazione in esecuzione nel cluster.</span><span class="sxs-lookup"><span data-stu-id="bd03f-152">Confirm deleting the application instance, which removes the instance of our application running in the cluster.</span></span>

![Eliminare un'applicazione in Service Fabric Explorer](./media/service-fabric-tutorial-deploy-app-to-party-cluster/delete-application.png)

## <a name="remove-the-application-type-from-a-cluster-using-service-fabric-explorer"></a><span data-ttu-id="bd03f-154">Rimuovere il tipo di applicazione da un cluster usando Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="bd03f-154">Remove the application type from a cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="bd03f-155">Le applicazioni vengono distribuite come tipi di applicazioni in un cluster Service Fabric, che consente di avere più istanze e versioni dell'applicazione in esecuzione nel cluster.</span><span class="sxs-lookup"><span data-stu-id="bd03f-155">Applications are deployed as application types in a Service Fabric cluster, which enables you to have multiple instances and versions of the application running within the cluster.</span></span> <span data-ttu-id="bd03f-156">Dopo avere rimosso l'istanza dell'applicazione in esecuzione, è anche possibile rimuovere il tipo, per completare la pulizia della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="bd03f-156">After having removed the running instance of our application, we can also remove the type, to complete the cleanup of the deployment.</span></span>

<span data-ttu-id="bd03f-157">Per altre informazioni sul modello di applicazione in Service Fabric, vedere [Modellare un'applicazione in Service Fabric](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="bd03f-157">For more information about the application model in Service Fabric, see [Model an application in Service Fabric](service-fabric-application-model.md).</span></span>

1. <span data-ttu-id="bd03f-158">Passare al nodo **VotingType** nella visualizzazione struttura ad albero.</span><span class="sxs-lookup"><span data-stu-id="bd03f-158">Navigate to the **VotingType** node in the treeview.</span></span>

2. <span data-ttu-id="bd03f-159">Fare clic sul pulsante **Azione** nel riquadro **Informazioni di base** a destra e scegliere **Unprovision Type** (Annulla provisioning tipo).</span><span class="sxs-lookup"><span data-stu-id="bd03f-159">Click the **Action** button in the right-hand **Essentials** pane, and choose **Unprovision Type**.</span></span> <span data-ttu-id="bd03f-160">Confermare l'annullamento del provisioning del tipo di applicazione.</span><span class="sxs-lookup"><span data-stu-id="bd03f-160">Confirm unprovisioning the application type.</span></span>

![Annullare il provisioning del tipo di applicazione in Service Fabric Explorer](./media/service-fabric-tutorial-deploy-app-to-party-cluster/unprovision-type.png)

<span data-ttu-id="bd03f-162">L'esercitazione è terminata.</span><span class="sxs-lookup"><span data-stu-id="bd03f-162">This concludes the tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd03f-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bd03f-163">Next steps</span></span>
<span data-ttu-id="bd03f-164">In questa esercitazione si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="bd03f-164">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bd03f-165">Distribuire un'applicazione in un cluster remoto usando Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bd03f-165">Deploy an application to a remote cluster using Visual Studio</span></span>
> * <span data-ttu-id="bd03f-166">Rimuovere un'applicazione da un cluster usando Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="bd03f-166">Remove an application from a cluster using Service Fabric Explorer</span></span>

<span data-ttu-id="bd03f-167">Passare all'esercitazione successiva:</span><span class="sxs-lookup"><span data-stu-id="bd03f-167">Advance to the next tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="bd03f-168">Impostare l'integrazione continua usando Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="bd03f-168">Set up continuous integration using Visual Studio Team Services</span></span>](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)