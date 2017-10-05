---
title: CI/CD con il servizio contenitore di Azure e Swarm | Microsoft Docs
description: Usare il servizio contenitore di Azure con Docker Swarm, un Registro di sistema del contenitore di Azure e Visual Studio Team Services per distribuire un'applicazione .NET Core multi-contenitore in modo continuativo
services: container-service
documentationcenter: " "
author: jcorioland
manager: pierlag
tags: acs, azure-container-service
keywords: Docker, contenitori, microservizi, Swarm, Azure, Visual Studio Team Services, DevOps
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/08/2016
ms.author: jucoriol
ms.custom: mvc
ms.openlocfilehash: 99c27c37218a35d2a3416d6edd5e0a871cd5c011
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="full-cicd-pipeline-to-deploy-a-multi-container-application-on-azure-container-service-with-docker-swarm-using-visual-studio-team-services"></a><span data-ttu-id="12e89-104">Pipeline CI/CD completa per distribuire un'applicazione multi-contenitore nel servizio contenitore di Azure con Docker Swarm tramite Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="12e89-104">Full CI/CD pipeline to deploy a multi-container application on Azure Container Service with Docker Swarm using Visual Studio Team Services</span></span>

<span data-ttu-id="12e89-105">Una delle sfide principali quando si sviluppano applicazioni moderne per il cloud è quella di riuscire a distribuire le applicazioni in modo continuativo.</span><span class="sxs-lookup"><span data-stu-id="12e89-105">One of the biggest challenges when developing modern applications for the cloud is being able to deliver these applications continuously.</span></span> <span data-ttu-id="12e89-106">In questo articolo vengono offerte informazioni su come implementare una pipeline (CI/CD) completa di distribuzione e integrazione continuativa attraverso la gestione di compilazione e rilascio del servizio contenitore di Azure di Docker Swarm, Registro di sistema del contenitore di Azure e Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="12e89-106">In this article, you learn how to implement a full continuous integration and deployment (CI/CD) pipeline using Azure Container Service with Docker Swarm, Azure Container Registry, and Visual Studio Team Services build and release management.</span></span>

<span data-ttu-id="12e89-107">Questo articolo si basa su una semplice applicazione, disponibile in [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs) e sviluppata con ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="12e89-107">This article is based on a simple application, available on [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs), developed with ASP.NET Core.</span></span> <span data-ttu-id="12e89-108">L'applicazione è composta da quattro servizi diversi: tre API Web e un Web front-end:</span><span class="sxs-lookup"><span data-stu-id="12e89-108">The application is composed of four different services: three web APIs and one web front end:</span></span>

![Applicazione MyShop di esempio](./media/container-service-docker-swarm-setup-ci-cd/myshop-application.png)

<span data-ttu-id="12e89-110">L'obiettivo consiste nell'assicurare l'applicazione in modo continuativo in un cluster Docker Swarm attraverso Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="12e89-110">The objective is to deliver this application continuously in a Docker Swarm cluster, using Visual Studio Team Services.</span></span> <span data-ttu-id="12e89-111">Nell'immagine seguente sono illustrati i dettagli della pipeline di distribuzione continuativa:</span><span class="sxs-lookup"><span data-stu-id="12e89-111">The following figure details this continuous delivery pipeline:</span></span>

![Applicazione MyShop di esempio](./media/container-service-docker-swarm-setup-ci-cd/full-ci-cd-pipeline.png)

<span data-ttu-id="12e89-113">Una breve spiegazione dei passaggi:</span><span class="sxs-lookup"><span data-stu-id="12e89-113">Here is a brief explanation of the steps:</span></span>

1. <span data-ttu-id="12e89-114">Viene eseguito il commit delle modifiche al codice nel repository del codice sorgente (in questo caso GitHub)</span><span class="sxs-lookup"><span data-stu-id="12e89-114">Code changes are committed to the source code repository (here, GitHub)</span></span> 
2. <span data-ttu-id="12e89-115">GitHub attiva una compilazione in Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="12e89-115">GitHub triggers a build in Visual Studio Team Services</span></span> 
3. <span data-ttu-id="12e89-116">Visual Studio Team Services recupera la versione più recente delle origini e compila tutte le immagini che compongono l'applicazione</span><span class="sxs-lookup"><span data-stu-id="12e89-116">Visual Studio Team Services gets the latest version of the sources and builds all the images that compose the application</span></span> 
4. <span data-ttu-id="12e89-117">Visual Studio Team Services effettua il push di ogni immagine a un Registro di sistema Docker creato tramite il servizio Registro di sistema del contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="12e89-117">Visual Studio Team Services pushes each image to a Docker registry created using the Azure Container Registry service</span></span> 
5. <span data-ttu-id="12e89-118">Visual Studio Team Services attiva un nuovo rilascio</span><span class="sxs-lookup"><span data-stu-id="12e89-118">Visual Studio Team Services triggers a new release</span></span> 
6. <span data-ttu-id="12e89-119">Il rilascio esegue alcuni comandi tramite SSH nel nodo principale del cluster del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="12e89-119">The release runs some commands using SSH on the Azure container service cluster master node</span></span> 
7. <span data-ttu-id="12e89-120">Docker Swarm nel cluster effettua il pull della versione più recente delle immagini</span><span class="sxs-lookup"><span data-stu-id="12e89-120">Docker Swarm on the cluster pulls the latest version of the images</span></span> 
8. <span data-ttu-id="12e89-121">La nuova versione dell'applicazione viene distribuita mediante Docker Compose</span><span class="sxs-lookup"><span data-stu-id="12e89-121">The new version of the application is deployed using Docker Compose</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="12e89-122">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="12e89-122">Prerequisites</span></span>

<span data-ttu-id="12e89-123">Prima di iniziare questa esercitazione, è necessario soddisfare i requisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="12e89-123">Before starting this tutorial, you need to complete the following tasks:</span></span>

- [<span data-ttu-id="12e89-124">Creare un cluster Swarm nel servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="12e89-124">Create a Swarm cluster in Azure Container Service</span></span>](container-service-deployment.md)
- [<span data-ttu-id="12e89-125">Connettersi a un cluster Swarm nel servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="12e89-125">Connect with the Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)
- [<span data-ttu-id="12e89-126">Creare un Registro di sistema del contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="12e89-126">Create an Azure container registry</span></span>](../../container-registry/container-registry-get-started-portal.md)
- [<span data-ttu-id="12e89-127">Disporre di un account Visual Studio Team Services e aver creato un progetto di team</span><span class="sxs-lookup"><span data-stu-id="12e89-127">Have a Visual Studio Team Services account and team project created</span></span>](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [<span data-ttu-id="12e89-128">Creare una fork del repository GitHub nell'account GitHub</span><span class="sxs-lookup"><span data-stu-id="12e89-128">Fork the GitHub repository to your GitHub account</span></span>](https://github.com/jcorioland/MyShop/)

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

<span data-ttu-id="12e89-129">È inoltre necessario disporre di un computer Ubuntu (14.04 o 16.04) con Docker.</span><span class="sxs-lookup"><span data-stu-id="12e89-129">You also need an Ubuntu (14.04 or 16.04) machine with Docker installed.</span></span> <span data-ttu-id="12e89-130">Questo computer viene usato da Visual Studio Team Services durante i processi di compilazione e rilascio.</span><span class="sxs-lookup"><span data-stu-id="12e89-130">This machine is used by Visual Studio Team Services during the build and release processes.</span></span> <span data-ttu-id="12e89-131">Un modo per creare questo computer consiste nell'usare l'immagine disponibile in [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/).</span><span class="sxs-lookup"><span data-stu-id="12e89-131">One way to create this machine is to use the image available in the [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/).</span></span> 

## <a name="step-1-configure-your-visual-studio-team-services-account"></a><span data-ttu-id="12e89-132">Passaggio 1: Configurare l'account di Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="12e89-132">Step 1: Configure your Visual Studio Team Services account</span></span> 

<span data-ttu-id="12e89-133">In questa sezione viene configurato l'account di Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="12e89-133">In this section, you configure your Visual Studio Team Services account.</span></span>

### <a name="configure-a-visual-studio-team-services-linux-build-agent"></a><span data-ttu-id="12e89-134">Configurare un agente di compilazione Linux di Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="12e89-134">Configure a Visual Studio Team Services Linux build agent</span></span>

<span data-ttu-id="12e89-135">Per creare immagini Docker ed effettuare il push in un Registro di sistema del contenitore di Azure da una compilazione di Visual Studio Team Services, è necessario registrare un agente Linux.</span><span class="sxs-lookup"><span data-stu-id="12e89-135">To create Docker images and push these images into an Azure container registry from a Visual Studio Team Services build, you need to register a Linux agent.</span></span> <span data-ttu-id="12e89-136">Sono disponibili queste opzioni di installazione:</span><span class="sxs-lookup"><span data-stu-id="12e89-136">You have these installation options:</span></span>

* [<span data-ttu-id="12e89-137">Distribuire un agente in Linux</span><span class="sxs-lookup"><span data-stu-id="12e89-137">Deploy an agent on Linux</span></span>](https://www.visualstudio.com/docs/build/admin/agents/v2-linux)

* [<span data-ttu-id="12e89-138">Usare Docker per eseguire l'agente VSTS</span><span class="sxs-lookup"><span data-stu-id="12e89-138">Use Docker to run the VSTS agent</span></span>](https://hub.docker.com/r/microsoft/vsts-agent)

### <a name="install-the-docker-integration-vsts-extension"></a><span data-ttu-id="12e89-139">Installare l'estensione VSTS di Docker Integration</span><span class="sxs-lookup"><span data-stu-id="12e89-139">Install the Docker Integration VSTS extension</span></span>

<span data-ttu-id="12e89-140">Microsoft offre un'estensione di VSTS per lavorare con Docker nei processi di compilazione e rilascio.</span><span class="sxs-lookup"><span data-stu-id="12e89-140">Microsoft provides a VSTS extension to work with Docker in build and release processes.</span></span> <span data-ttu-id="12e89-141">Questa estensione è disponibile nel [marketplace di VSTS](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker).</span><span class="sxs-lookup"><span data-stu-id="12e89-141">This extension is available in the [VSTS Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker).</span></span> <span data-ttu-id="12e89-142">Fare clic su **Installa** per aggiungere l'estensione all'account VSTS:</span><span class="sxs-lookup"><span data-stu-id="12e89-142">Click **Install** to add this extension to your VSTS account:</span></span>

![Installare Docker Integration](./media/container-service-docker-swarm-setup-ci-cd/install-docker-vsts.png)

<span data-ttu-id="12e89-144">È necessario connettersi all'account VSTS usando le credenziali.</span><span class="sxs-lookup"><span data-stu-id="12e89-144">You are asked to connect to your VSTS account using your credentials.</span></span> 

### <a name="connect-visual-studio-team-services-and-github"></a><span data-ttu-id="12e89-145">Connettere Visual Studio Team Services e GitHub</span><span class="sxs-lookup"><span data-stu-id="12e89-145">Connect Visual Studio Team Services and GitHub</span></span>

<span data-ttu-id="12e89-146">Impostare una connessione tra il progetto VSTS e l'account GitHub.</span><span class="sxs-lookup"><span data-stu-id="12e89-146">Set up a connection between your VSTS project and your GitHub account.</span></span>

1. <span data-ttu-id="12e89-147">Nel progetto di Visual Studio Team Services fare clic sull'icona **Impostazioni** nella barra degli strumenti e selezionare **Servizi**.</span><span class="sxs-lookup"><span data-stu-id="12e89-147">In your Visual Studio Team Services project, click the **Settings** icon in the toolbar, and select **Services**.</span></span>

    ![Visual Studio Team Services - Connessione esterna](./media/container-service-docker-swarm-setup-ci-cd/vsts-services-menu.png)

2. <span data-ttu-id="12e89-149">A sinistra fare clic su **Nuovo endpoint del servizio** > **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="12e89-149">On the left, click **New Service Endpoint** > **GitHub**.</span></span>

    ![Visual Studio Team Services - GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github.png)

3. <span data-ttu-id="12e89-151">Per autorizzare VSTS a lavorare con il proprio account GitHub, fare clic su **Autorizza** e attenersi alla procedura nella finestra visualizzata.</span><span class="sxs-lookup"><span data-stu-id="12e89-151">To authorize VSTS to work with your GitHub account, click **Authorize** and follow the procedure in the window that opens.</span></span>

    ![Visual Studio Team Services - Autorizzazione GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-authorize.png)

### <a name="connect-vsts-to-your-azure-container-registry-and-azure-container-service-cluster"></a><span data-ttu-id="12e89-153">Connettere VSTS al Registro di sistema del contenitore di Azure e al cluster del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="12e89-153">Connect VSTS to your Azure container registry and Azure Container Service cluster</span></span>

<span data-ttu-id="12e89-154">Gli ultimi passaggi prima di approfondire la pipeline CI/CD consistono nel configurare le connessioni esterne nel Registro di sistema del contenitore e nel cluster Docker Swarm in Azure.</span><span class="sxs-lookup"><span data-stu-id="12e89-154">The last steps before getting into the CI/CD pipeline are to configure external connections to your container registry and your Docker Swarm cluster in Azure.</span></span> 

1. <span data-ttu-id="12e89-155">Nelle impostazioni **Servizi** del progetto Visual Studio Team Services aggiungere un endpoint di servizio di tipo **Docker Registry**.</span><span class="sxs-lookup"><span data-stu-id="12e89-155">In the **Services** settings of your Visual Studio Team Services project, add a service endpoint of type **Docker Registry**.</span></span> 

2. <span data-ttu-id="12e89-156">Nel popup che viene visualizzato immettere l'URL e le credenziali del Registro di sistema del contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="12e89-156">In the popup that opens, enter the URL and the credentials of your Azure container registry.</span></span>

    ![Visual Studio Team Services - Docker Registry](./media/container-service-docker-swarm-setup-ci-cd/vsts-registry.png)

3. <span data-ttu-id="12e89-158">Per il cluster Docker Swarm, aggiungere un endpoint di tipo **SSH**.</span><span class="sxs-lookup"><span data-stu-id="12e89-158">For the Docker Swarm cluster, add an endpoint of type **SSH**.</span></span> <span data-ttu-id="12e89-159">Successivamente, immettere le informazioni di connessione SSH del cluster Swarm.</span><span class="sxs-lookup"><span data-stu-id="12e89-159">Then enter the SSH connection information of your Swarm cluster.</span></span>

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-setup-ci-cd/vsts-ssh.png)

<span data-ttu-id="12e89-161">Tutti i passaggi di configurazione vengono eseguiti ora.</span><span class="sxs-lookup"><span data-stu-id="12e89-161">All the configuration is done now.</span></span> <span data-ttu-id="12e89-162">Nei passaggi successivi viene creata la pipeline CI/CD che compila e distribuisce l'applicazione al cluster Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="12e89-162">In the next steps, you create the CI/CD pipeline that builds and deploys the application to the Docker Swarm cluster.</span></span> 

## <a name="step-2-create-the-build-definition"></a><span data-ttu-id="12e89-163">Passaggio 2: creare la definizione di compilazione</span><span class="sxs-lookup"><span data-stu-id="12e89-163">Step 2: Create the build definition</span></span>

<span data-ttu-id="12e89-164">In questo passaggio viene configurata una definizione di compilazione per il progetto VSTS e viene definito il flusso di lavoro di compilazione per le immagini contenitore</span><span class="sxs-lookup"><span data-stu-id="12e89-164">In this step, you set up a build definitionfor your VSTS project and define the build workflow for your container images</span></span>

### <a name="initial-definition-setup"></a><span data-ttu-id="12e89-165">Configurazione iniziale della definizione</span><span class="sxs-lookup"><span data-stu-id="12e89-165">Initial definition setup</span></span>

1. <span data-ttu-id="12e89-166">Per creare una definizione di compilazione, connettersi al progetto di Visual Studio Team Services e fare clic su **Build & Release** (Compilazione e rilascio).</span><span class="sxs-lookup"><span data-stu-id="12e89-166">To create a build definition, connect to your Visual Studio Team Services project and click **Build & Release**.</span></span> 

2. <span data-ttu-id="12e89-167">Nella sezione **Definizione di compilazione** fare clic su **+ New** (+Nuova).</span><span class="sxs-lookup"><span data-stu-id="12e89-167">In the **Build definitions** section, click **+ New**.</span></span> <span data-ttu-id="12e89-168">Selezionare il modello **Vuoto**.</span><span class="sxs-lookup"><span data-stu-id="12e89-168">Select the **Empty** template.</span></span>

    ![Visual Studio Team Services - Nuova definizione di compilazione](./media/container-service-docker-swarm-setup-ci-cd/create-build-vsts.png)

3. <span data-ttu-id="12e89-170">Configurare la nuova compilazione con un'origine di repository GitHub, selezionare **Integrazione continua**, quindi scegliere la coda dell'agente in cui è registrato l'agente Linux.</span><span class="sxs-lookup"><span data-stu-id="12e89-170">Configure the new build with a GitHub repository source, check **Continuous integration**, and select the agent queue where you registered your Linux agent.</span></span> <span data-ttu-id="12e89-171">Fare clic su **Crea** per creare la definizione di compilazione.</span><span class="sxs-lookup"><span data-stu-id="12e89-171">Click **Create** to create the build definition.</span></span>

    ![Visual Studio Team Services - Creazione definizione di compilazione](./media/container-service-docker-swarm-setup-ci-cd/vsts-create-build-github.png)

4. <span data-ttu-id="12e89-173">Nella pagina **Definizioni di compilazione** innanzitutto aprire la scheda **Repository** e configurare la compilazione in modo che usi la fork del progetto MyShop creata nei prerequisiti.</span><span class="sxs-lookup"><span data-stu-id="12e89-173">On the **Build Definitions** page, first open the **Repository** tab and configure the build to use the fork of the MyShop project that you created in the prerequisites.</span></span> <span data-ttu-id="12e89-174">Assicurarsi di selezionare *acs-docs* come **ramo predefinito**.</span><span class="sxs-lookup"><span data-stu-id="12e89-174">Make sure that you select *acs-docs* as the **Default branch**.</span></span>

    ![Visual Studio Team Services - Configurazione repository di compilazione](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-repo-conf.png)

5. <span data-ttu-id="12e89-176">Nella scheda **Trigger** configurare la compilazione in modo che venga attivata dopo ciascun commit.</span><span class="sxs-lookup"><span data-stu-id="12e89-176">On the **Triggers** tab, configure the build to be triggered after each commit.</span></span> <span data-ttu-id="12e89-177">Selezionare **Integrazione continua** e **Modifiche bacth**.</span><span class="sxs-lookup"><span data-stu-id="12e89-177">Select **Continuous integration** and **Batch changes**.</span></span>

    ![Visual Studio Team Services - Configurazione trigger di compilazione](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-trigger-conf.png)

### <a name="define-the-build-workflow"></a><span data-ttu-id="12e89-179">Definire il flusso di lavoro di compilazione</span><span class="sxs-lookup"><span data-stu-id="12e89-179">Define the build workflow</span></span>
<span data-ttu-id="12e89-180">Nei passaggi successivi viene definito il flusso di lavoro di compilazione.</span><span class="sxs-lookup"><span data-stu-id="12e89-180">The next steps define the build workflow.</span></span> <span data-ttu-id="12e89-181">Esistono cinque immagini contenitore per la compilazione dell'applicazione *MyShop*.</span><span class="sxs-lookup"><span data-stu-id="12e89-181">There are five container images to build for the *MyShop* application.</span></span> <span data-ttu-id="12e89-182">Ogni immagine viene compilata attraverso il file Docker che si trova nelle cartelle del progetto:</span><span class="sxs-lookup"><span data-stu-id="12e89-182">Each image is built using the Dockerfile located in the project folders:</span></span>

* <span data-ttu-id="12e89-183">ProductsApi</span><span class="sxs-lookup"><span data-stu-id="12e89-183">ProductsApi</span></span>
* <span data-ttu-id="12e89-184">Proxy</span><span class="sxs-lookup"><span data-stu-id="12e89-184">Proxy</span></span>
* <span data-ttu-id="12e89-185">RatingsApi</span><span class="sxs-lookup"><span data-stu-id="12e89-185">RatingsApi</span></span>
* <span data-ttu-id="12e89-186">RecommandationsApi</span><span class="sxs-lookup"><span data-stu-id="12e89-186">RecommandationsApi</span></span>
* <span data-ttu-id="12e89-187">ShopFront</span><span class="sxs-lookup"><span data-stu-id="12e89-187">ShopFront</span></span>

<span data-ttu-id="12e89-188">È necessario aggiungere due passaggi di Docker per ogni immagine, uno per compilare l'immagine, l'altro per effettuare il push dell'immagine nel Registro di sistema del contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="12e89-188">You need to add two Docker steps for each image, one to build the image, and one to push the image in the Azure container registry.</span></span> 

1. <span data-ttu-id="12e89-189">Per aggiungere un passaggio nel flusso di lavoro di compilazione fare clic su **+ Aggiungi istruzione di compilazione** e selezionare **Docker**.</span><span class="sxs-lookup"><span data-stu-id="12e89-189">To add a step in the build workflow, click **+ Add build step** and select **Docker**.</span></span>

    ![Visual Studio Team Services - Aggiunta passaggi di compilazione](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-add-task.png)

2. <span data-ttu-id="12e89-191">Per ogni immagine, configurare un passaggio che usi il comando `docker build`.</span><span class="sxs-lookup"><span data-stu-id="12e89-191">For each image, configure one step that uses the `docker build` command.</span></span>

    ![Visual Studio Team Services - Compilazione Docker](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-build.png)

    <span data-ttu-id="12e89-193">Per l'operazione di compilazione, selezionare il Registro di sistema del contenitore di Azure, l'azione **Build an image** (Compila un'immagine) e il file Docker che definisce ogni immagine.</span><span class="sxs-lookup"><span data-stu-id="12e89-193">For the build operation, select your Azure container registry, the **Build an image** action, and the Dockerfile that defines each image.</span></span> <span data-ttu-id="12e89-194">Impostare **Build context** (Contesto compilazione) come directory radice del file Docker e definire **Nome immagine**.</span><span class="sxs-lookup"><span data-stu-id="12e89-194">Set the **Build context** as the Dockerfile root directory, and define the **Image Name**.</span></span> 
    
    <span data-ttu-id="12e89-195">Come mostrato nella schermata precedente, il nome dell'immagine deve iniziare con l'URI del Registro di sistema del contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="12e89-195">As shown on the preceding screen, start the image name with the URI of your Azure container registry.</span></span> <span data-ttu-id="12e89-196">È anche possibile usare una variabile di compilazione per assegnare parametri al tag dell'immagine, in questo esempio l'identificatore di compilazione.</span><span class="sxs-lookup"><span data-stu-id="12e89-196">(You can also use a build variable to parameterize the tag of the image, such as the build identifier in this example.)</span></span>

3. <span data-ttu-id="12e89-197">Per ogni immagine, configurare un secondo passaggio che usi il comando `docker push`.</span><span class="sxs-lookup"><span data-stu-id="12e89-197">For each image, configure a second step that uses the `docker push` command.</span></span>

    ![Visual Studio Team Services - Push Docker](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-push.png)

    <span data-ttu-id="12e89-199">Per l'operazione di push, selezionare il Registro di sistema del contenitore di Azure, l'azione **Push an image** (Push immagine) e immettere il **nome dell'immagine** compilato nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="12e89-199">For the push operation, select your Azure container registry, the **Push an image** action, and enter the **Image Name** that is built in the previous step.</span></span>

4. <span data-ttu-id="12e89-200">Dopo aver configurato i passaggi di compilazione e push per ognuna delle cinque immagini, aggiungere altri due passaggi nel flusso di lavoro di compilazione.</span><span class="sxs-lookup"><span data-stu-id="12e89-200">After you configure the build and push steps for each of the five images, add two more steps in the build workflow.</span></span>

    <span data-ttu-id="12e89-201">a.</span><span class="sxs-lookup"><span data-stu-id="12e89-201">a.</span></span> <span data-ttu-id="12e89-202">Un'attività della riga di comando che usi uno script bash per sostituire l'occorrenza *BuildNumber* nel file docker-compose.yml con l'ID di compilazione corrente. Vedere i dettagli nella schermata di seguito.</span><span class="sxs-lookup"><span data-stu-id="12e89-202">A command-line task that uses a bash script to replace the *BuildNumber* occurrence in the docker-compose.yml file with the current build Id. See the following screen for details.</span></span>

    ![Visual Studio Team Services - Aggiornamento file Compose](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-replace-build-number.png)

    <span data-ttu-id="12e89-204">b.</span><span class="sxs-lookup"><span data-stu-id="12e89-204">b.</span></span> <span data-ttu-id="12e89-205">Un'attività che rimuove il file Compose aggiornato come elemento di compilazione per poterlo usare nel rilascio.</span><span class="sxs-lookup"><span data-stu-id="12e89-205">A task that drops the updated Compose file as a build artifact so it can be used in the release.</span></span> <span data-ttu-id="12e89-206">Vedere i dettagli nella schermata di seguito.</span><span class="sxs-lookup"><span data-stu-id="12e89-206">See the following screen for details.</span></span>

    ![Visual Studio Team Services - Pubblicazione file Compose](./media/container-service-docker-swarm-setup-ci-cd/vsts-publish-compose.png) 

5. <span data-ttu-id="12e89-208">Fare clic su **Salva** e assegnare un nome alla definizione di compilazione.</span><span class="sxs-lookup"><span data-stu-id="12e89-208">Click **Save** and name your build definition.</span></span>

## <a name="step-3-create-the-release-definition"></a><span data-ttu-id="12e89-209">Passaggio 3: creare la definizione di versione</span><span class="sxs-lookup"><span data-stu-id="12e89-209">Step 3: Create the release definition</span></span>

<span data-ttu-id="12e89-210">Visual Studio Team Services consente di [gestire i rilasci nei vari ambienti](https://www.visualstudio.com/team-services/release-management/).</span><span class="sxs-lookup"><span data-stu-id="12e89-210">Visual Studio Team Services allows you to [manage releases across environments](https://www.visualstudio.com/team-services/release-management/).</span></span> <span data-ttu-id="12e89-211">È possibile abilitare la distribuzione continua per assicurarsi che l'applicazione venga distribuita in ambienti diversi (ad esempio sviluppo, test, preproduzione e produzione) in modo uniforme.</span><span class="sxs-lookup"><span data-stu-id="12e89-211">You can enable continuous deployment to make sure that your application is deployed on your different environments (such as dev, test, pre-production, and production) in a smooth way.</span></span> <span data-ttu-id="12e89-212">È possibile creare un nuovo ambiente che rappresenti il cluster Docker Swarm del servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="12e89-212">You can create a new environment that represents your Azure Container Service Docker Swarm cluster.</span></span>

![Visual Studio Team Services - Rilascio su ACS](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-acs.png) 

### <a name="initial-release-setup"></a><span data-ttu-id="12e89-214">Configurazione iniziale del rilascio</span><span class="sxs-lookup"><span data-stu-id="12e89-214">Initial release setup</span></span>

1. <span data-ttu-id="12e89-215">Per creare una definizione di rilascio, fare clic su **Rilascio** > **+ Rilascio**</span><span class="sxs-lookup"><span data-stu-id="12e89-215">To create a release definition, click **Releases** > **+ Release**</span></span>

2. <span data-ttu-id="12e89-216">Per configurare l'origine dell'elemento, fare clic su **Elementi** > **Collega un'origine elemento**.</span><span class="sxs-lookup"><span data-stu-id="12e89-216">To configure the artifact source, Click **Artifacts** > **Link an artifact source**.</span></span> <span data-ttu-id="12e89-217">Da qui collegare la nuova definizione di rilascio alla compilazione definita nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="12e89-217">Here, link this new release definition to the build that you defined in the previous step.</span></span> <span data-ttu-id="12e89-218">In questo modo, il file docker-compose.yml è disponibile nel processo di rilascio.</span><span class="sxs-lookup"><span data-stu-id="12e89-218">By doing this, the docker-compose.yml file is available in the release process.</span></span>

    ![Visual Studio Team Services - Rilascio elementi](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-artefacts.png) 

3. <span data-ttu-id="12e89-220">Per configurare il trigger di rilascio, fare clic su **Trigger** e selezionare **Distribuzione continua**.</span><span class="sxs-lookup"><span data-stu-id="12e89-220">To configure the release trigger, click **Triggers** and select **Continuous Deployment**.</span></span> <span data-ttu-id="12e89-221">Impostare il trigger sulla stessa origine dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="12e89-221">Set the trigger on the same artifact source.</span></span> <span data-ttu-id="12e89-222">Questa impostazione garantisce che un nuovo rilascio venga avviato non appena la compilazione viene completata correttamente.</span><span class="sxs-lookup"><span data-stu-id="12e89-222">This setting ensures that a new release starts as soon as the build completes successfully.</span></span>

    ![Visual Studio Team Services - Rilascio trigger](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-trigger.png) 

### <a name="define-the-release-workflow"></a><span data-ttu-id="12e89-224">Definire il flusso di lavoro di rilascio</span><span class="sxs-lookup"><span data-stu-id="12e89-224">Define the release workflow</span></span>

<span data-ttu-id="12e89-225">Il flusso di lavoro di rilascio è composto da due attività che vengono aggiunte.</span><span class="sxs-lookup"><span data-stu-id="12e89-225">The release workflow is composed of two tasks that you add.</span></span>

1. <span data-ttu-id="12e89-226">Configurare un'attività per copiare in modo sicuro il file Compose in una cartella di *distribuzione* nel nodo master Docker Swarm, tramite la connessione SSH configurata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="12e89-226">Configure a task to securely copy the compose file to a *deploy* folder on the Docker Swarm master node, using the SSH connection you configured previously.</span></span> <span data-ttu-id="12e89-227">Vedere i dettagli nella schermata di seguito.</span><span class="sxs-lookup"><span data-stu-id="12e89-227">See the following screen for details.</span></span>

    ![Visual Studio Team Services - Rilascio SCP](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-scp.png)

2. <span data-ttu-id="12e89-229">Configurare una seconda attività in modo che esegua un comando bash per i comandi `docker` e `docker-compose` nel nodo principale.</span><span class="sxs-lookup"><span data-stu-id="12e89-229">Configure a second task to execute a bash command to run `docker` and `docker-compose` commands on the master node.</span></span> <span data-ttu-id="12e89-230">Vedere i dettagli nella schermata di seguito.</span><span class="sxs-lookup"><span data-stu-id="12e89-230">See the following screen for details.</span></span>

    ![Visual Studio Team Services - Rilascio bash](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-bash.png)

    <span data-ttu-id="12e89-232">Il comando eseguito nel nodo principale usa l'interfaccia della riga di comando di Docker e Docker-Compose per eseguire le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="12e89-232">The command executed on the master use the Docker CLI and the Docker-Compose CLI to do the following tasks:</span></span>

    - <span data-ttu-id="12e89-233">Accedere al Registro di sistema del contenitore di Azure (usa tre variabili di compilazione definite nella scheda **Variabili**)</span><span class="sxs-lookup"><span data-stu-id="12e89-233">Login to the Azure container registry (it uses three build variab\`les that are defined in the **Variables** tab)</span></span>
    - <span data-ttu-id="12e89-234">Definire la variabile **DOCKER_HOST** in modo che sia compatibile con l'endpoint Swarm (:2375)</span><span class="sxs-lookup"><span data-stu-id="12e89-234">Define the **DOCKER_HOST** variable to work with the Swarm endpoint (:2375)</span></span>
    - <span data-ttu-id="12e89-235">Accedere alla cartella di *distribuzione* che è stata creata dall'attività di copia sicura precedente e che contiene il file docker-compose.yml</span><span class="sxs-lookup"><span data-stu-id="12e89-235">Navigate to the *deploy* folder that was created by the preceding secure copy task and that contains the docker-compose.yml file</span></span> 
    - <span data-ttu-id="12e89-236">Eseguire i comandi `docker-compose` che effettuano il pull di nuove immagini, interrompono e rimuovono i servizi e creano i contenitori.</span><span class="sxs-lookup"><span data-stu-id="12e89-236">Execute `docker-compose` commands that pull the new images, stop the services, remove the services, and create the containers.</span></span>

    >[!IMPORTANT]
    > <span data-ttu-id="12e89-237">Come illustrato nella schermata precedente, lasciare deselezionata la casella **Interrompi in caso di STDERR**.</span><span class="sxs-lookup"><span data-stu-id="12e89-237">As shown on the preceding screen, leave the **Fail on STDERR** checkbox unchecked.</span></span> <span data-ttu-id="12e89-238">Questa è un'impostazione importante, perché `docker-compose` stampa diversi messaggi di diagnostica, ad esempio in caso di contenitori arrestati o in fase di eliminazione, nell'output di errore standard.</span><span class="sxs-lookup"><span data-stu-id="12e89-238">This is an important setting, because `docker-compose` prints several diagnostic messages, such as containers are stopping or being deleted, on the standard error output.</span></span> <span data-ttu-id="12e89-239">Se si seleziona la casella di controllo, Visual Studio Team Services segnala che si sono verificati errori durante il rilascio, anche se tutto va bene.</span><span class="sxs-lookup"><span data-stu-id="12e89-239">If you check the checkbox, Visual Studio Team Services reports that errors occurred during the release, even if all goes well.</span></span>
    >
3. <span data-ttu-id="12e89-240">Salvare la nuova definizione di rilascio.</span><span class="sxs-lookup"><span data-stu-id="12e89-240">Save this new release definition.</span></span>


>[!NOTE]
><span data-ttu-id="12e89-241">Questa distribuzione include tempi di inattività perché vengono interrotti i servizi precedenti per eseguire quello nuovo.</span><span class="sxs-lookup"><span data-stu-id="12e89-241">This deployment includes some downtime because we are stopping the old services and running the new one.</span></span> <span data-ttu-id="12e89-242">È possibile evitare il problema effettuando una distribuzione di tipo blu-verde.</span><span class="sxs-lookup"><span data-stu-id="12e89-242">It is possible to avoid this by doing a blue-green deployment.</span></span>
>

## <a name="step-4-test-the-cicd-pipeline"></a><span data-ttu-id="12e89-243">Passaggio 4.</span><span class="sxs-lookup"><span data-stu-id="12e89-243">Step 4.</span></span> <span data-ttu-id="12e89-244">Testare la pipeline CI/CD</span><span class="sxs-lookup"><span data-stu-id="12e89-244">Test the CI/CD pipeline</span></span>

<span data-ttu-id="12e89-245">Dopo aver completato la configurazione, è il momento di testare la nuova pipeline CI/CD.</span><span class="sxs-lookup"><span data-stu-id="12e89-245">Now that you are done with the configuration, it's time to test this new CI/CD pipeline.</span></span> <span data-ttu-id="12e89-246">Il modo più semplice per eseguire il test consiste nell'aggiornare il codice sorgente ed eseguire il commit delle modifiche nel repository GitHub.</span><span class="sxs-lookup"><span data-stu-id="12e89-246">The easiest way to test it is to update the source code and commit the changes into your GitHub repository.</span></span> <span data-ttu-id="12e89-247">Pochi secondi dopo il push del codice, verrà visualizzata una nuova compilazione in esecuzione in Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="12e89-247">A few seconds after you push the code, you will see a new build running in Visual Studio Team Services.</span></span> <span data-ttu-id="12e89-248">Dopo il suo completamento, verrà attivato un nuovo rilascio, che distribuirà la nuova versione dell'applicazione nel cluster del servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="12e89-248">Once completed successfully, a new release will be triggered and will deploy the new version of the application on the Azure Container Service cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12e89-249">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="12e89-249">Next Steps</span></span>

* <span data-ttu-id="12e89-250">Per altre informazioni su CI/CD con Visual Studio Team Services, vedere la [panoramica sulla compilazione di VSTS](https://www.visualstudio.com/docs/build/overview).</span><span class="sxs-lookup"><span data-stu-id="12e89-250">For more information about CI/CD with Visual Studio Team Services, see the [VSTS Build overview](https://www.visualstudio.com/docs/build/overview).</span></span>
