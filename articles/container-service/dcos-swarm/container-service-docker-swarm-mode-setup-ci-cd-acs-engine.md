---
title: "CI/CD con il motore del servizio contenitore di Azure e la modalità Swarm | Microsoft Docs"
description: "Usare il motore del servizio contenitore di Azure con la modalità Docker Swarm, un Registro contenitori di Azure e Visual Studio Team Services per distribuire un'applicazione .NET Core multi-contenitore in modo continuativo"
services: container-service
documentationcenter: " "
author: diegomrtnzg
manager: esterdnb
tags: acs, azure-container-service, acs-engine
keywords: Docker, contenitori, microservizi, Swarm, Azure, Visual Studio Team Services, DevOps, motore del servizio contenitore di Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/27/2017
ms.author: diegomrtnzg
ms.custom: mvc
ms.openlocfilehash: 2c0e5fe4f60738fcc1aa67a78674e6f3c62e5628
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="full-cicd-pipeline-to-deploy-a-multi-container-application-on-azure-container-service-with-acs-engine-and-docker-swarm-mode-using-visual-studio-team-services"></a><span data-ttu-id="533d2-104">Pipeline CI/CD completa per distribuire un'applicazione multi-contenitore nel servizio contenitore di Azure con il motore del servizio contenitore di Azure e la modalità Docker Swarm tramite Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="533d2-104">Full CI/CD pipeline to deploy a multi-container application on Azure Container Service with ACS Engine and Docker Swarm Mode using Visual Studio Team Services</span></span>

<span data-ttu-id="533d2-105">*Questo articolo si basa sulla documentazione disponibile in [Full CI/CD pipeline to deploy a multi-container application on Azure Container Service with Docker Swarm using Visual Studio Team Services (Pipeline CI/CD completa per distribuire un'applicazione multi-contenitore nel servizio contenitore di Azure con Docker Swarm tramite Visual Studio Team Services)](container-service-docker-swarm-setup-ci-cd.md)*</span><span class="sxs-lookup"><span data-stu-id="533d2-105">*This article is based on [Full CI/CD pipeline to deploy a multi-container application on Azure Container Service with Docker Swarm using Visual Studio Team Services](container-service-docker-swarm-setup-ci-cd.md) documentation*</span></span>

<span data-ttu-id="533d2-106">Una delle sfide principali quando si sviluppano applicazioni moderne per il cloud è quella di riuscire a distribuire le applicazioni in modo continuativo.</span><span class="sxs-lookup"><span data-stu-id="533d2-106">Nowadays, One of the biggest challenges when developing modern applications for the cloud is being able to deliver these applications continuously.</span></span> <span data-ttu-id="533d2-107">Questo articolo illustra come implementare una pipeline completa di integrazione e distribuzione continua (CI/CD) tramite:</span><span class="sxs-lookup"><span data-stu-id="533d2-107">In this article, you learn how to implement a full continuous integration and deployment (CI/CD) pipeline using:</span></span> 
* <span data-ttu-id="533d2-108">Motore del servizio contenitore di Azure con la modalità Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="533d2-108">Azure Container Service Engine with Docker Swarm Mode</span></span>
* <span data-ttu-id="533d2-109">Registro di sistema del contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="533d2-109">Azure Container Registry</span></span>
* <span data-ttu-id="533d2-110">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="533d2-110">Visual Studio Team Services</span></span>

<span data-ttu-id="533d2-111">Questo articolo si basa su una semplice applicazione, disponibile in [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux) e sviluppata con ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="533d2-111">This article is based on a simple application, available on [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux), developed with ASP.NET Core.</span></span> <span data-ttu-id="533d2-112">L'applicazione è composta da quattro servizi diversi: tre API Web e un Web front-end:</span><span class="sxs-lookup"><span data-stu-id="533d2-112">The application is composed of four different services: three web APIs and one web front end:</span></span>

![Applicazione MyShop di esempio](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/myshop-application.png)

<span data-ttu-id="533d2-114">L'obiettivo è distribuire l'applicazione in modo continuativo in un cluster in modalità Docker Swarm attraverso Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="533d2-114">The objective is to deliver this application continuously in a Docker Swarm Mode cluster, using Visual Studio Team Services.</span></span> <span data-ttu-id="533d2-115">Nell'immagine seguente sono illustrati i dettagli della pipeline di distribuzione continuativa:</span><span class="sxs-lookup"><span data-stu-id="533d2-115">The following figure details this continuous delivery pipeline:</span></span>

![Applicazione MyShop di esempio](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/full-ci-cd-pipeline.png)

<span data-ttu-id="533d2-117">Una breve spiegazione dei passaggi:</span><span class="sxs-lookup"><span data-stu-id="533d2-117">Here is a brief explanation of the steps:</span></span>

1. <span data-ttu-id="533d2-118">Viene eseguito il commit delle modifiche al codice nel repository del codice sorgente (in questo caso GitHub)</span><span class="sxs-lookup"><span data-stu-id="533d2-118">Code changes are committed to the source code repository (here, GitHub)</span></span> 
2. <span data-ttu-id="533d2-119">GitHub attiva una compilazione in Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="533d2-119">GitHub triggers a build in Visual Studio Team Services</span></span> 
3. <span data-ttu-id="533d2-120">Visual Studio Team Services recupera la versione più recente delle origini e compila tutte le immagini che compongono l'applicazione</span><span class="sxs-lookup"><span data-stu-id="533d2-120">Visual Studio Team Services gets the latest version of the sources and builds all the images that compose the application</span></span> 
4. <span data-ttu-id="533d2-121">Visual Studio Team Services effettua il push di ogni immagine a un Registro di sistema Docker creato tramite il servizio Registro di sistema del contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="533d2-121">Visual Studio Team Services pushes each image to a Docker registry created using the Azure Container Registry service</span></span> 
5. <span data-ttu-id="533d2-122">Visual Studio Team Services attiva un nuovo rilascio</span><span class="sxs-lookup"><span data-stu-id="533d2-122">Visual Studio Team Services triggers a new release</span></span> 
6. <span data-ttu-id="533d2-123">Il rilascio esegue alcuni comandi tramite SSH nel nodo principale del cluster del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="533d2-123">The release runs some commands using SSH on the Azure container service cluster master node</span></span> 
7. <span data-ttu-id="533d2-124">La modalità Docker Swarm nel cluster effettua il pull della versione più recente delle immagini</span><span class="sxs-lookup"><span data-stu-id="533d2-124">Docker Swarm Mode on the cluster pulls the latest version of the images</span></span> 
8. <span data-ttu-id="533d2-125">La nuova versione dell'applicazione viene distribuita con Docker Stack</span><span class="sxs-lookup"><span data-stu-id="533d2-125">The new version of the application is deployed using Docker Stack</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="533d2-126">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="533d2-126">Prerequisites</span></span>

<span data-ttu-id="533d2-127">Prima di iniziare questa esercitazione, è necessario soddisfare i requisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="533d2-127">Before starting this tutorial, you need to complete the following tasks:</span></span>

- [<span data-ttu-id="533d2-128">Creare un cluster in modalità Swarm nel servizio contenitore di Azure con il motore del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="533d2-128">Create a Swarm Mode cluster in Azure Container Service with ACS Engine</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acsengine-swarmmode)
- [<span data-ttu-id="533d2-129">Connettersi a un cluster Swarm nel servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="533d2-129">Connect with the Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)
- [<span data-ttu-id="533d2-130">Creare un Registro di sistema del contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="533d2-130">Create an Azure container registry</span></span>](../../container-registry/container-registry-get-started-portal.md)
- [<span data-ttu-id="533d2-131">Disporre di un account Visual Studio Team Services e aver creato un progetto di team</span><span class="sxs-lookup"><span data-stu-id="533d2-131">Have a Visual Studio Team Services account and team project created</span></span>](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [<span data-ttu-id="533d2-132">Creare una fork del repository GitHub nell'account GitHub</span><span class="sxs-lookup"><span data-stu-id="533d2-132">Fork the GitHub repository to your GitHub account</span></span>](https://github.com/jcorioland/MyShop/tree/docker-linux)

>[!NOTE]
> <span data-ttu-id="533d2-133">L'agente di orchestrazione Docker Swarm nel servizio contenitore di Azure usa Swarm autonomo legacy.</span><span class="sxs-lookup"><span data-stu-id="533d2-133">The Docker Swarm orchestrator in Azure Container Service uses legacy standalone Swarm.</span></span> <span data-ttu-id="533d2-134">La [modalità Swarm](https://docs.docker.com/engine/swarm/) integrata (in Docker 1.12 e versioni successive) attualmente non è un agente di orchestrazione supportato nel servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="533d2-134">Currently, the integrated [Swarm mode](https://docs.docker.com/engine/swarm/) (in Docker 1.12 and higher) is not a supported orchestrator in Azure Container Service.</span></span> <span data-ttu-id="533d2-135">Per questo motivo viene usato il [motore del servizio contenitore di Azure](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), un [modello di avvio rapido](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/) realizzato con il contributo della community o una soluzione Docker in [Azure Marketplace](https://azuremarketplace.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="533d2-135">For this reason, we are using [ACS Engine](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), a community-contributed [quickstart template](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), or a Docker solution in the [Azure Marketplace](https://azuremarketplace.microsoft.com).</span></span>
>

## <a name="step-1-configure-your-visual-studio-team-services-account"></a><span data-ttu-id="533d2-136">Passaggio 1: Configurare l'account di Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="533d2-136">Step 1: Configure your Visual Studio Team Services account</span></span> 

<span data-ttu-id="533d2-137">In questa sezione viene configurato l'account di Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="533d2-137">In this section, you configure your Visual Studio Team Services account.</span></span> <span data-ttu-id="533d2-138">Per configurare gli endpoint dei servizi VSTS, nel progetto di Visual Studio Team Services fare clic sull'icona **Impostazioni** nella barra degli strumenti e selezionare **Servizi**.</span><span class="sxs-lookup"><span data-stu-id="533d2-138">To configure VSTS Services Endpoints, in your Visual Studio Team Services project, click the **Settings** icon in the toolbar, and select **Services**.</span></span>

![Aprire l'endpoint dei servizi](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/services-vsts.PNG)

### <a name="connect-visual-studio-team-services-and-azure-account"></a><span data-ttu-id="533d2-140">Connettere Visual Studio Team Services e l'account Azure</span><span class="sxs-lookup"><span data-stu-id="533d2-140">Connect Visual Studio Team Services and Azure account</span></span>

<span data-ttu-id="533d2-141">Impostare una connessione tra il progetto VSTS e l'account Azure.</span><span class="sxs-lookup"><span data-stu-id="533d2-141">Set up a connection between your VSTS project and your Azure account.</span></span>

1. <span data-ttu-id="533d2-142">A sinistra fare clic su **Nuovo endpoint del servizio** > **Azure Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="533d2-142">On the left, click **New Service Endpoint** > **Azure Resource Manager**.</span></span>
2. <span data-ttu-id="533d2-143">Per autorizzare VSTS al funzionamento con l'account Azure, selezionare la **Sottoscrizione** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="533d2-143">To authorize VSTS to work with your Azure account, select your **Subscription** and click **OK**.</span></span>

    ![Visual Studio Team Services - Autorizzazione di Azure](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-azure.PNG)

### <a name="connect-visual-studio-team-services-and-github"></a><span data-ttu-id="533d2-145">Connettere Visual Studio Team Services e GitHub</span><span class="sxs-lookup"><span data-stu-id="533d2-145">Connect Visual Studio Team Services and GitHub</span></span>

<span data-ttu-id="533d2-146">Impostare una connessione tra il progetto VSTS e l'account GitHub.</span><span class="sxs-lookup"><span data-stu-id="533d2-146">Set up a connection between your VSTS project and your GitHub account.</span></span>

1. <span data-ttu-id="533d2-147">A sinistra fare clic su **Nuovo endpoint del servizio** > **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="533d2-147">On the left, click **New Service Endpoint** > **GitHub**.</span></span>
2. <span data-ttu-id="533d2-148">Per autorizzare VSTS a lavorare con il proprio account GitHub, fare clic su **Autorizza** e attenersi alla procedura nella finestra visualizzata.</span><span class="sxs-lookup"><span data-stu-id="533d2-148">To authorize VSTS to work with your GitHub account, click **Authorize** and follow the procedure in the window that opens.</span></span>

    ![Visual Studio Team Services - Autorizzazione GitHub](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github.png)

### <a name="connect-vsts-to-your-azure-container-service-cluster"></a><span data-ttu-id="533d2-150">Connettere VSTS al cluster del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="533d2-150">Connect VSTS to your Azure Container Service cluster</span></span>

<span data-ttu-id="533d2-151">Prima di passare alla pipeline CI/CD occorre configurare le connessioni esterne al cluster Docker Swarm in Azure.</span><span class="sxs-lookup"><span data-stu-id="533d2-151">The last steps before getting into the CI/CD pipeline are to configure external connections to your Docker Swarm cluster in Azure.</span></span> 

1. <span data-ttu-id="533d2-152">Per il cluster Docker Swarm, aggiungere un endpoint di tipo **SSH**.</span><span class="sxs-lookup"><span data-stu-id="533d2-152">For the Docker Swarm cluster, add an endpoint of type **SSH**.</span></span> <span data-ttu-id="533d2-153">Successivamente, immettere le informazioni di connessione SSH del cluster Swarm (nodo master).</span><span class="sxs-lookup"><span data-stu-id="533d2-153">Then enter the SSH connection information of your Swarm cluster (master node).</span></span>

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-ssh.png)

<span data-ttu-id="533d2-155">Tutti i passaggi di configurazione vengono eseguiti ora.</span><span class="sxs-lookup"><span data-stu-id="533d2-155">All the configuration is done now.</span></span> <span data-ttu-id="533d2-156">Nei passaggi successivi viene creata la pipeline CI/CD che compila e distribuisce l'applicazione al cluster Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="533d2-156">In the next steps, you create the CI/CD pipeline that builds and deploys the application to the Docker Swarm cluster.</span></span> 

## <a name="step-2-create-the-build-definition"></a><span data-ttu-id="533d2-157">Passaggio 2: creare la definizione di compilazione</span><span class="sxs-lookup"><span data-stu-id="533d2-157">Step 2: Create the build definition</span></span>

<span data-ttu-id="533d2-158">In questo passaggio viene configurata una definizione di compilazione per il progetto VSTS e viene definito il flusso di lavoro di compilazione per le immagini contenitore</span><span class="sxs-lookup"><span data-stu-id="533d2-158">In this step, you set up a build definition for your VSTS project and define the build workflow for your container images</span></span>

### <a name="initial-definition-setup"></a><span data-ttu-id="533d2-159">Configurazione iniziale della definizione</span><span class="sxs-lookup"><span data-stu-id="533d2-159">Initial definition setup</span></span>

1. <span data-ttu-id="533d2-160">Per creare una definizione di compilazione, connettersi al progetto di Visual Studio Team Services e fare clic su **Build & Release** (Compilazione e rilascio).</span><span class="sxs-lookup"><span data-stu-id="533d2-160">To create a build definition, connect to your Visual Studio Team Services project and click **Build & Release**.</span></span> <span data-ttu-id="533d2-161">Nella sezione **Definizione di compilazione** fare clic su **+ New** (+Nuova).</span><span class="sxs-lookup"><span data-stu-id="533d2-161">In the **Build definitions** section, click **+ New**.</span></span> 

    ![Visual Studio Team Services - Nuova definizione di compilazione](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-build-vsts.PNG)

2. <span data-ttu-id="533d2-163">Selezionare il **processo vuoto**.</span><span class="sxs-lookup"><span data-stu-id="533d2-163">Select the **Empty process**.</span></span>

    ![Visual Studio Team Services - Nuova definizione di compilazione vuota](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-empty-build-vsts.PNG)

4. <span data-ttu-id="533d2-165">Fare clic sulla scheda **Variabili** e creare due nuove variabili: **RegistryURL** e **AgentURL**.</span><span class="sxs-lookup"><span data-stu-id="533d2-165">Then, click the **Variables** tab and create two new variables: **RegistryURL** and **AgentURL**.</span></span> <span data-ttu-id="533d2-166">Incollare i valori del registro contenitori e del DNS degli agenti cluster.</span><span class="sxs-lookup"><span data-stu-id="533d2-166">Paste the values of your Registry and Cluster Agents DNS.</span></span>

    ![Visual Studio Team Services - Configurazione variabili di compilazione](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-variables.png)

5. <span data-ttu-id="533d2-168">Nella pagina **Definizioni di compilazione** aprire prima di tutto la scheda **Trigger** e configurare la compilazione in modo che venga usata l'integrazione continua con il fork del progetto MyShop creato nei prerequisiti.</span><span class="sxs-lookup"><span data-stu-id="533d2-168">On the **Build Definitions** page, open the **Triggers** tab and configure the build to use continuous integration with the fork of the MyShop project that you created in the prerequisites.</span></span> <span data-ttu-id="533d2-169">Selezionare quindi **Modifiche batch**.</span><span class="sxs-lookup"><span data-stu-id="533d2-169">Then, select **Batch changes**.</span></span> <span data-ttu-id="533d2-170">Assicurarsi di selezionare *docker-linux* come **Specifica rami**.</span><span class="sxs-lookup"><span data-stu-id="533d2-170">Make sure that you select *docker-linux* as the **Branch specification**.</span></span>

    ![Visual Studio Team Services - Configurazione repository di compilazione](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github-repo-conf.PNG)


6. <span data-ttu-id="533d2-172">Infine, fare clic sulla scheda **Opzioni** e configurare la coda dell'agente predefinito come **anteprima Linux ospitata**.</span><span class="sxs-lookup"><span data-stu-id="533d2-172">Finally, click the **Options** tab and configure the Default agent queue to **Hosted Linux Preview**.</span></span>

    ![Visual Studio Team Services - Configurazione agente host](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-agent.png)

### <a name="define-the-build-workflow"></a><span data-ttu-id="533d2-174">Definire il flusso di lavoro di compilazione</span><span class="sxs-lookup"><span data-stu-id="533d2-174">Define the build workflow</span></span>
<span data-ttu-id="533d2-175">Nei passaggi successivi viene definito il flusso di lavoro di compilazione.</span><span class="sxs-lookup"><span data-stu-id="533d2-175">The next steps define the build workflow.</span></span> <span data-ttu-id="533d2-176">In primo luogo, è necessario configurare l'origine del codice.</span><span class="sxs-lookup"><span data-stu-id="533d2-176">First, you need to configure the source of the code.</span></span> <span data-ttu-id="533d2-177">A tale scopo, selezionare **GitHub**, il **repository** e il **ramo** (docker-linux).</span><span class="sxs-lookup"><span data-stu-id="533d2-177">To do it, select **GitHub** and your **repository** and **branch** (docker-linux).</span></span>

![Visual Studio Team Services - Configurazione origine del codice](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-source-code.png)

<span data-ttu-id="533d2-179">Esistono cinque immagini contenitore per la compilazione dell'applicazione *MyShop*.</span><span class="sxs-lookup"><span data-stu-id="533d2-179">There are five container images to build for the *MyShop* application.</span></span> <span data-ttu-id="533d2-180">Ogni immagine viene compilata attraverso il file Docker che si trova nelle cartelle del progetto:</span><span class="sxs-lookup"><span data-stu-id="533d2-180">Each image is built using the Dockerfile located in the project folders:</span></span>

* <span data-ttu-id="533d2-181">ProductsApi</span><span class="sxs-lookup"><span data-stu-id="533d2-181">ProductsApi</span></span>
* <span data-ttu-id="533d2-182">Proxy</span><span class="sxs-lookup"><span data-stu-id="533d2-182">Proxy</span></span>
* <span data-ttu-id="533d2-183">RatingsApi</span><span class="sxs-lookup"><span data-stu-id="533d2-183">RatingsApi</span></span>
* <span data-ttu-id="533d2-184">RecommandationsApi</span><span class="sxs-lookup"><span data-stu-id="533d2-184">RecommandationsApi</span></span>
* <span data-ttu-id="533d2-185">ShopFront</span><span class="sxs-lookup"><span data-stu-id="533d2-185">ShopFront</span></span>

<span data-ttu-id="533d2-186">Sono necessari due passaggi di Docker per ogni immagine, uno per compilare l'immagine, l'altro per effettuare il push dell'immagine nel registro contenitori di Azure.</span><span class="sxs-lookup"><span data-stu-id="533d2-186">You need two Docker steps for each image, one to build the image, and one to push the image in the Azure container registry.</span></span> 

1. <span data-ttu-id="533d2-187">Per aggiungere un passaggio nel flusso di lavoro di compilazione fare clic su **+ Aggiungi istruzione di compilazione** e selezionare **Docker**.</span><span class="sxs-lookup"><span data-stu-id="533d2-187">To add a step in the build workflow, click **+ Add build step** and select **Docker**.</span></span>

    ![Visual Studio Team Services - Aggiunta passaggi di compilazione](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-add-task.png)

2. <span data-ttu-id="533d2-189">Per ogni immagine, configurare un passaggio che usi il comando `docker build`.</span><span class="sxs-lookup"><span data-stu-id="533d2-189">For each image, configure one step that uses the `docker build` command.</span></span>

    ![Visual Studio Team Services - Compilazione Docker](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-build.png)

    <span data-ttu-id="533d2-191">Per l'operazione di compilazione, selezionare il registro contenitori di Azure, l'azione **Build an image** (Compila un'immagine) e il file Docker che definisce ogni immagine.</span><span class="sxs-lookup"><span data-stu-id="533d2-191">For the build operation, select your Azure Container Registry, the **Build an image** action, and the Dockerfile that defines each image.</span></span> <span data-ttu-id="533d2-192">Impostare la **directory di lavoro** come directory radice di Dockerfile, definire il **nome dell'immagine** e selezionare **Include Latest Tag** (Includi tag più recente).</span><span class="sxs-lookup"><span data-stu-id="533d2-192">Set the **Working Directory** as the Dockerfile root directory, define the **Image Name**, and select **Include Latest Tag**.</span></span>
    
    <span data-ttu-id="533d2-193">Il nome dell'immagine deve essere nel formato: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```.</span><span class="sxs-lookup"><span data-stu-id="533d2-193">The Image Name has to be in this format: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```.</span></span> <span data-ttu-id="533d2-194">Sostituire **[NAME]** con il nome dell'immagine:</span><span class="sxs-lookup"><span data-stu-id="533d2-194">Replace **[NAME]** with the image name:</span></span>
    - ```proxy```
    - ```products-api```
    - ```ratings-api```
    - ```recommendations-api```
    - ```shopfront```

3. <span data-ttu-id="533d2-195">Per ogni immagine, configurare un secondo passaggio che usi il comando `docker push`.</span><span class="sxs-lookup"><span data-stu-id="533d2-195">For each image, configure a second step that uses the `docker push` command.</span></span>

    ![Visual Studio Team Services - Push Docker](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-push.png)

    <span data-ttu-id="533d2-197">Per l'operazione di push, selezionare il registro contenitori di Azure, l'azione **Push an image** (Push immagine), immettere il **nome dell'immagine** compilato nel passaggio precedente e selezionare **Include Latest Tag** (Includi tag più recente).</span><span class="sxs-lookup"><span data-stu-id="533d2-197">For the push operation, select your Azure container registry, the **Push an image** action, enter the **Image Name** that is built in the previous step and select **Include Latest Tag**.</span></span>

4. <span data-ttu-id="533d2-198">Dopo aver configurato i passaggi di compilazione e push per ognuna delle cinque immagini, aggiungere altri tre passaggi al flusso di lavoro di compilazione.</span><span class="sxs-lookup"><span data-stu-id="533d2-198">After you configure the build and push steps for each of the five images, add three more steps in the build workflow.</span></span>

   ![Visual Studio Team Services - Aggiunta di attività della riga di comando](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-command-task.png)

      1. <span data-ttu-id="533d2-200">Un'attività della riga di comando che usa uno script bash per sostituire l'occorrenza *RegistryURL* nel file docker-compose.yml con la variabile RegistryURL.</span><span class="sxs-lookup"><span data-stu-id="533d2-200">A command-line task that uses a bash script to replace the *RegistryURL* occurrence in the docker-compose.yml file with the RegistryURL variable.</span></span> 
    
          ```-c "sed -i 's/RegistryUrl/$(RegistryURL)/g' src/docker-compose-v3.yml"```

          ![Visual Studio Team Services - Aggiornamento file Compose con URL del registro](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-replace-registry.png)

      2. <span data-ttu-id="533d2-202">Un'attività della riga di comando che usa uno script bash per sostituire l'occorrenza *AgentURL* nel file docker-compose.yml con la variabile AgentURL.</span><span class="sxs-lookup"><span data-stu-id="533d2-202">A command-line task that uses a bash script to replace the *AgentURL* occurrence in the docker-compose.yml file with the AgentURL variable.</span></span>
  
          ```-c "sed -i 's/AgentUrl/$(AgentURL)/g' src/docker-compose-v3.yml"```

     3. <span data-ttu-id="533d2-203">Un'attività che rimuove il file Compose aggiornato come elemento di compilazione per poterlo usare nel rilascio.</span><span class="sxs-lookup"><span data-stu-id="533d2-203">A task that drops the updated Compose file as a build artifact so it can be used in the release.</span></span> <span data-ttu-id="533d2-204">Vedere i dettagli nella schermata di seguito.</span><span class="sxs-lookup"><span data-stu-id="533d2-204">See the following screen for details.</span></span>

         ![Visual Studio Team Services - Pubblicazione elemento](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish.png) 

         ![Visual Studio Team Services - Pubblicazione file Compose](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish-compose.png) 

5. <span data-ttu-id="533d2-207">Fare clic su **Salva e accoda** per testare la definizione di compilazione.</span><span class="sxs-lookup"><span data-stu-id="533d2-207">Click **Save & queue** to test your build definition.</span></span>

   ![Visual Studio Team Services - Salva e accoda](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-save.png) 

   ![Visual Studio Team Services - Nuova coda](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-queue.png) 

6. <span data-ttu-id="533d2-210">Se la **compilazione**  è corretta, viene visualizzata la schermata seguente:</span><span class="sxs-lookup"><span data-stu-id="533d2-210">If the **Build** is correct, you have to see this screen:</span></span>

  ![Visual Studio Team Services - Compilazione completata](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-succeeded.png) 

## <a name="step-3-create-the-release-definition"></a><span data-ttu-id="533d2-212">Passaggio 3: creare la definizione di versione</span><span class="sxs-lookup"><span data-stu-id="533d2-212">Step 3: Create the release definition</span></span>

<span data-ttu-id="533d2-213">Visual Studio Team Services consente di [gestire i rilasci nei vari ambienti](https://www.visualstudio.com/team-services/release-management/).</span><span class="sxs-lookup"><span data-stu-id="533d2-213">Visual Studio Team Services allows you to [manage releases across environments](https://www.visualstudio.com/team-services/release-management/).</span></span> <span data-ttu-id="533d2-214">È possibile abilitare la distribuzione continua per assicurarsi che l'applicazione venga distribuita in ambienti diversi (ad esempio sviluppo, test, preproduzione e produzione) in modo uniforme.</span><span class="sxs-lookup"><span data-stu-id="533d2-214">You can enable continuous deployment to make sure that your application is deployed on your different environments (such as dev, test, pre-production, and production) in a smooth way.</span></span> <span data-ttu-id="533d2-215">È possibile creare un ambiente che rappresenti il cluster della modalità Docker Swarm del servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="533d2-215">You can create an environment that represents your Azure Container Service Docker Swarm Mode cluster.</span></span>

![Visual Studio Team Services - Rilascio su ACS](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-acs.png) 

### <a name="initial-release-setup"></a><span data-ttu-id="533d2-217">Configurazione iniziale del rilascio</span><span class="sxs-lookup"><span data-stu-id="533d2-217">Initial release setup</span></span>

1. <span data-ttu-id="533d2-218">Per creare una definizione di rilascio, fare clic su **Rilascio** > **+ Rilascio**</span><span class="sxs-lookup"><span data-stu-id="533d2-218">To create a release definition, click **Releases** > **+ Release**</span></span>

2. <span data-ttu-id="533d2-219">Per configurare l'origine dell'elemento, fare clic su **Elementi** > **Collega un'origine elemento**.</span><span class="sxs-lookup"><span data-stu-id="533d2-219">To configure the artifact source, Click **Artifacts** > **Link an artifact source**.</span></span> <span data-ttu-id="533d2-220">Da qui collegare la nuova definizione di rilascio alla compilazione definita nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="533d2-220">Here, link this new release definition to the build that you defined in the previous step.</span></span> <span data-ttu-id="533d2-221">Successivamente, il file docker-compose.yml è disponibile nel processo di rilascio.</span><span class="sxs-lookup"><span data-stu-id="533d2-221">After that, the docker-compose.yml file is available in the release process.</span></span>

    ![Visual Studio Team Services - Rilascio elementi](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-artefacts.png) 

3. <span data-ttu-id="533d2-223">Per configurare il trigger di rilascio, fare clic su **Trigger** e selezionare **Distribuzione continua**.</span><span class="sxs-lookup"><span data-stu-id="533d2-223">To configure the release trigger, click **Triggers** and select **Continuous Deployment**.</span></span> <span data-ttu-id="533d2-224">Impostare il trigger sulla stessa origine dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="533d2-224">Set the trigger on the same artifact source.</span></span> <span data-ttu-id="533d2-225">Questa impostazione garantisce l'avvio di un nuovo rilascio quando la compilazione viene completata.</span><span class="sxs-lookup"><span data-stu-id="533d2-225">This setting ensures that a new release starts when the build completes successfully.</span></span>

    ![Visual Studio Team Services - Rilascio trigger](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-trigger.png) 

4. <span data-ttu-id="533d2-227">Per configurare le variabili di rilascio, fare clic su **Variables** (Variabili) e selezionare **+Variable** (+Variabile) per creare tre nuove variabili con le informazioni del registro: **docker.username**, **docker.password** e **docker.registry**.</span><span class="sxs-lookup"><span data-stu-id="533d2-227">To configure the release variables, click **Variables** and select **+Variable** to create three new variables with the info of the registry: **docker.username**, **docker.password**, and **docker.registry**.</span></span> <span data-ttu-id="533d2-228">Incollare i valori del registro contenitori e del DNS degli agenti cluster.</span><span class="sxs-lookup"><span data-stu-id="533d2-228">Paste the values of your Registry and Cluster Agents DNS.</span></span>

    ![Visual Studio Team Services - Configurazione repository di compilazione](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-variables.png)

    >[!IMPORTANT]
    > <span data-ttu-id="533d2-230">Come illustrato nella schermata precedente, fare clic sulla casella di controllo **Lock** (Blocco) in docker.password.</span><span class="sxs-lookup"><span data-stu-id="533d2-230">As shown on the previous screen, click the **Lock** checkbox in docker.password.</span></span> <span data-ttu-id="533d2-231">Questa impostazione è importante per limitare la password.</span><span class="sxs-lookup"><span data-stu-id="533d2-231">This setting is important to restrict the password.</span></span>
    >

### <a name="define-the-release-workflow"></a><span data-ttu-id="533d2-232">Definire il flusso di lavoro di rilascio</span><span class="sxs-lookup"><span data-stu-id="533d2-232">Define the release workflow</span></span>

<span data-ttu-id="533d2-233">Il flusso di lavoro di rilascio è composto da due attività che vengono aggiunte.</span><span class="sxs-lookup"><span data-stu-id="533d2-233">The release workflow is composed of two tasks that you add.</span></span>

1. <span data-ttu-id="533d2-234">Configurare un'attività per copiare in modo sicuro il file Compose in una cartella di *distribuzione* nel nodo master Docker Swarm, tramite la connessione SSH configurata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="533d2-234">Configure a task to securely copy the compose file to a *deploy* folder on the Docker Swarm master node, using the SSH connection you configured previously.</span></span> <span data-ttu-id="533d2-235">Vedere i dettagli nella schermata di seguito.</span><span class="sxs-lookup"><span data-stu-id="533d2-235">See the following screen for details.</span></span>
    
    <span data-ttu-id="533d2-236">Cartella di origine: ```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```</span><span class="sxs-lookup"><span data-stu-id="533d2-236">Source folder: ```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```</span></span>

    ![Visual Studio Team Services - Rilascio SCP](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-scp.png)

2. <span data-ttu-id="533d2-238">Configurare una seconda attività in modo che esegua un comando bash per i comandi `docker` e `docker stack deploy` nel nodo principale.</span><span class="sxs-lookup"><span data-stu-id="533d2-238">Configure a second task to execute a bash command to run `docker` and `docker stack deploy` commands on the master node.</span></span> <span data-ttu-id="533d2-239">Vedere i dettagli nella schermata di seguito.</span><span class="sxs-lookup"><span data-stu-id="533d2-239">See the following screen for details.</span></span>

    ```docker login -u $(docker.username) -p $(docker.password) $(docker.registry) && export DOCKER_HOST=:2375 && cd deploy && docker stack deploy --compose-file docker-compose-v3.yml myshop --with-registry-auth```

    ![Visual Studio Team Services - Rilascio bash](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-bash.png)

    <span data-ttu-id="533d2-241">Il comando eseguito nel nodo principale usa l'interfaccia della riga di comando di Docker e Docker-Compose per eseguire queste attività:</span><span class="sxs-lookup"><span data-stu-id="533d2-241">The command executed on the master uses the Docker CLI and the Docker-Compose CLI to do the following tasks:</span></span>

    - <span data-ttu-id="533d2-242">Accedere al registro contenitori di Azure, con tre variabili di compilazione definite nella scheda **Variabili**</span><span class="sxs-lookup"><span data-stu-id="533d2-242">Log in to the Azure container registry (it uses three build variables that are defined in the **Variables** tab)</span></span>
    - <span data-ttu-id="533d2-243">Definire la variabile **DOCKER_HOST** in modo che sia compatibile con l'endpoint Swarm (:2375)</span><span class="sxs-lookup"><span data-stu-id="533d2-243">Define the **DOCKER_HOST** variable to work with the Swarm endpoint (:2375)</span></span>
    - <span data-ttu-id="533d2-244">Accedere alla cartella di *distribuzione* che è stata creata dall'attività di copia sicura precedente e che contiene il file docker-compose.yml</span><span class="sxs-lookup"><span data-stu-id="533d2-244">Navigate to the *deploy* folder that was created by the preceding secure copy task and that contains the docker-compose.yml file</span></span> 
    - <span data-ttu-id="533d2-245">Eseguire comandi `docker stack deploy`, che effettuano il pull di nuove immagini e creano i contenitori.</span><span class="sxs-lookup"><span data-stu-id="533d2-245">Execute `docker stack deploy` commands that pull the new images and create the containers.</span></span>

    >[!IMPORTANT]
    > <span data-ttu-id="533d2-246">Come illustrato nella schermata precedente, lasciare deselezionata la casella **Interrompi in caso di STDERR**.</span><span class="sxs-lookup"><span data-stu-id="533d2-246">As shown on the previous screen, leave the **Fail on STDERR** checkbox unchecked.</span></span> <span data-ttu-id="533d2-247">Questa impostazione permette di completare il processo di rilascio, perché `docker-compose` stampa diversi messaggi di diagnostica, ad esempio in caso di contenitori arrestati o in fase di eliminazione, nell'output di errore standard.</span><span class="sxs-lookup"><span data-stu-id="533d2-247">This setting allows us to complete the release process due to `docker-compose` prints several diagnostic messages, such as containers are stopping or being deleted, on the standard error output.</span></span> <span data-ttu-id="533d2-248">Se si seleziona la casella di controllo, Visual Studio Team Services segnala che si sono verificati errori durante il rilascio, anche se tutto va bene.</span><span class="sxs-lookup"><span data-stu-id="533d2-248">If you check the checkbox, Visual Studio Team Services reports that errors occurred during the release, even if all goes well.</span></span>
    >
3. <span data-ttu-id="533d2-249">Salvare la nuova definizione di rilascio.</span><span class="sxs-lookup"><span data-stu-id="533d2-249">Save this new release definition.</span></span>

## <a name="step-4-test-the-cicd-pipeline"></a><span data-ttu-id="533d2-250">Passaggio 4: Testare la pipeline CI/CD</span><span class="sxs-lookup"><span data-stu-id="533d2-250">Step 4: Test the CI/CD pipeline</span></span>

<span data-ttu-id="533d2-251">Dopo aver completato la configurazione, è il momento di testare la nuova pipeline CI/CD.</span><span class="sxs-lookup"><span data-stu-id="533d2-251">Now that you are done with the configuration, it's time to test this new CI/CD pipeline.</span></span> <span data-ttu-id="533d2-252">Il modo più semplice per eseguire il test consiste nell'aggiornare il codice sorgente ed eseguire il commit delle modifiche nel repository GitHub.</span><span class="sxs-lookup"><span data-stu-id="533d2-252">The easiest way to test it is to update the source code and commit the changes into your GitHub repository.</span></span> <span data-ttu-id="533d2-253">Pochi secondi dopo il push del codice, verrà visualizzata una nuova compilazione in esecuzione in Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="533d2-253">A few seconds after you push the code, you will see a new build running in Visual Studio Team Services.</span></span> <span data-ttu-id="533d2-254">Dopo il suo completamento, viene attivato un nuovo rilascio e la nuova versione dell'applicazione viene distribuita nel cluster del servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="533d2-254">Once completed successfully, a new release is triggered and deployed the new version of the application on the Azure Container Service cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="533d2-255">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="533d2-255">Next steps</span></span>

* <span data-ttu-id="533d2-256">Per altre informazioni su CI/CD con Visual Studio Team Services, vedere la [panoramica sulla compilazione di VSTS](https://www.visualstudio.com/docs/build/overview).</span><span class="sxs-lookup"><span data-stu-id="533d2-256">For more information about CI/CD with Visual Studio Team Services, see the [VSTS Build overview](https://www.visualstudio.com/docs/build/overview).</span></span>
* <span data-ttu-id="533d2-257">Per altre informazioni sul motore del servizio contenitore di Azure, vedere il [repository di GitHub sul motore del servizio contenitore di Azure](https://github.com/Azure/acs-engine).</span><span class="sxs-lookup"><span data-stu-id="533d2-257">For more information about ACS Engine, see the [ACS Engine GitHub repo](https://github.com/Azure/acs-engine).</span></span>
* <span data-ttu-id="533d2-258">Per altre informazioni sulla modalità Docker Swarm, vedere [Docker Swarm mode overview](https://docs.docker.com/engine/swarm/) (Panoramica della modalità Docker Swarm).</span><span class="sxs-lookup"><span data-stu-id="533d2-258">For more information about Docker Swarm mode, see the [Docker Swarm mode overview](https://docs.docker.com/engine/swarm/).</span></span>
