---
title: aaaCI/CD con il servizio contenitore di Azure e sciame | Documenti Microsoft
description: Utilizzare il servizio contenitore di Azure con Docker Swarm un registro di sistema contenitore di Azure e Visual Studio Team Services toodeliver continuamente un'applicazione .NET Core multi-contenitore
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
ms.openlocfilehash: 35348800aa620469fb62ab3e5a02b33834359446
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-docker-swarm-using-visual-studio-team-services"></a><span data-ttu-id="9a89f-104">CI/CD completo della pipeline toodeploy un'applicazione multi-contenitore nel servizio di Azure contenitore con Docker Swarm con Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="9a89f-104">Full CI/CD pipeline toodeploy a multi-container application on Azure Container Service with Docker Swarm using Visual Studio Team Services</span></span>

<span data-ttu-id="9a89f-105">Uno dei hello maggiori sfide durante lo sviluppo di applicazioni moderne per cloud hello toodeliver in grado di queste applicazioni in modo continuo.</span><span class="sxs-lookup"><span data-stu-id="9a89f-105">One of hello biggest challenges when developing modern applications for hello cloud is being able toodeliver these applications continuously.</span></span> <span data-ttu-id="9a89f-106">In questo articolo informazioni su come creare un'integrazione completa continua tooimplement e pipeline di distribuzione (CI/CD) utilizzando il servizio contenitore di Azure con Visual Studio Team Services, Azure del Registro di sistema contenitore e Docker Swarm e gestione del rilascio.</span><span class="sxs-lookup"><span data-stu-id="9a89f-106">In this article, you learn how tooimplement a full continuous integration and deployment (CI/CD) pipeline using Azure Container Service with Docker Swarm, Azure Container Registry, and Visual Studio Team Services build and release management.</span></span>

<span data-ttu-id="9a89f-107">Questo articolo si basa su una semplice applicazione, disponibile in [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs) e sviluppata con ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="9a89f-107">This article is based on a simple application, available on [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs), developed with ASP.NET Core.</span></span> <span data-ttu-id="9a89f-108">un'applicazione Hello è composta da quattro diversi servizi: tre web API e un solo web front-end:</span><span class="sxs-lookup"><span data-stu-id="9a89f-108">hello application is composed of four different services: three web APIs and one web front end:</span></span>

![Applicazione MyShop di esempio](./media/container-service-docker-swarm-setup-ci-cd/myshop-application.png)

<span data-ttu-id="9a89f-110">obiettivo di Hello è toodeliver questa applicazione in modo continuo in un cluster di Docker Swarm, tramite Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="9a89f-110">hello objective is toodeliver this application continuously in a Docker Swarm cluster, using Visual Studio Team Services.</span></span> <span data-ttu-id="9a89f-111">Hello figura riportata di seguito i dettagli questa pipeline il recapito continuo:</span><span class="sxs-lookup"><span data-stu-id="9a89f-111">hello following figure details this continuous delivery pipeline:</span></span>

![Applicazione MyShop di esempio](./media/container-service-docker-swarm-setup-ci-cd/full-ci-cd-pipeline.png)

<span data-ttu-id="9a89f-113">Di seguito è riportata una breve spiegazione dei passaggi di hello:</span><span class="sxs-lookup"><span data-stu-id="9a89f-113">Here is a brief explanation of hello steps:</span></span>

1. <span data-ttu-id="9a89f-114">Le modifiche al codice sono repository di codice sorgente toohello commit (in questo esempio GitHub)</span><span class="sxs-lookup"><span data-stu-id="9a89f-114">Code changes are committed toohello source code repository (here, GitHub)</span></span> 
2. <span data-ttu-id="9a89f-115">GitHub attiva una compilazione in Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="9a89f-115">GitHub triggers a build in Visual Studio Team Services</span></span> 
3. <span data-ttu-id="9a89f-116">Visual Studio Team Services Ottiene hello la versione più recente di origini di hello e compila tutte le immagini di hello che compongono un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="9a89f-116">Visual Studio Team Services gets hello latest version of hello sources and builds all hello images that compose hello application</span></span> 
4. <span data-ttu-id="9a89f-117">Visual Studio Team Services inserisce ogni immagine tooa Docker del Registro di sistema creato con il servizio di Azure del Registro di sistema contenitore hello</span><span class="sxs-lookup"><span data-stu-id="9a89f-117">Visual Studio Team Services pushes each image tooa Docker registry created using hello Azure Container Registry service</span></span> 
5. <span data-ttu-id="9a89f-118">Visual Studio Team Services attiva un nuovo rilascio</span><span class="sxs-lookup"><span data-stu-id="9a89f-118">Visual Studio Team Services triggers a new release</span></span> 
6. <span data-ttu-id="9a89f-119">versione di Hello esegue alcuni comandi tramite SSH nel nodo principale di hello Azure contenitore del servizio cluster</span><span class="sxs-lookup"><span data-stu-id="9a89f-119">hello release runs some commands using SSH on hello Azure container service cluster master node</span></span> 
7. <span data-ttu-id="9a89f-120">Docker sciame hello cluster esegue il pull hello versione più recente di immagini hello</span><span class="sxs-lookup"><span data-stu-id="9a89f-120">Docker Swarm on hello cluster pulls hello latest version of hello images</span></span> 
8. <span data-ttu-id="9a89f-121">nuova versione di Hello di un'applicazione hello viene distribuito tramite Docker Compose</span><span class="sxs-lookup"><span data-stu-id="9a89f-121">hello new version of hello application is deployed using Docker Compose</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9a89f-122">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9a89f-122">Prerequisites</span></span>

<span data-ttu-id="9a89f-123">Prima di iniziare questa esercitazione, è necessario hello toocomplete seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="9a89f-123">Before starting this tutorial, you need toocomplete hello following tasks:</span></span>

- [<span data-ttu-id="9a89f-124">Creare un cluster Swarm nel servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="9a89f-124">Create a Swarm cluster in Azure Container Service</span></span>](container-service-deployment.md)
- [<span data-ttu-id="9a89f-125">Connettersi con cluster sciame hello contenitore nel servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="9a89f-125">Connect with hello Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)
- [<span data-ttu-id="9a89f-126">Creare un Registro di sistema del contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="9a89f-126">Create an Azure container registry</span></span>](../../container-registry/container-registry-get-started-portal.md)
- [<span data-ttu-id="9a89f-127">Disporre di un account Visual Studio Team Services e aver creato un progetto di team</span><span class="sxs-lookup"><span data-stu-id="9a89f-127">Have a Visual Studio Team Services account and team project created</span></span>](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [<span data-ttu-id="9a89f-128">Fork hello GitHub repository tooyour account GitHub</span><span class="sxs-lookup"><span data-stu-id="9a89f-128">Fork hello GitHub repository tooyour GitHub account</span></span>](https://github.com/jcorioland/MyShop/)

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

<span data-ttu-id="9a89f-129">È inoltre necessario disporre di un computer Ubuntu (14.04 o 16.04) con Docker.</span><span class="sxs-lookup"><span data-stu-id="9a89f-129">You also need an Ubuntu (14.04 or 16.04) machine with Docker installed.</span></span> <span data-ttu-id="9a89f-130">Il computer è usato da Visual Studio Team Services hello durante la compilazione e versione processi.</span><span class="sxs-lookup"><span data-stu-id="9a89f-130">This machine is used by Visual Studio Team Services during hello build and release processes.</span></span> <span data-ttu-id="9a89f-131">Un modo toocreate questo computer è un immagine hello toouse disponibile in hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/).</span><span class="sxs-lookup"><span data-stu-id="9a89f-131">One way toocreate this machine is toouse hello image available in hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/).</span></span> 

## <a name="step-1-configure-your-visual-studio-team-services-account"></a><span data-ttu-id="9a89f-132">Passaggio 1: Configurare l'account di Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="9a89f-132">Step 1: Configure your Visual Studio Team Services account</span></span> 

<span data-ttu-id="9a89f-133">In questa sezione viene configurato l'account di Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="9a89f-133">In this section, you configure your Visual Studio Team Services account.</span></span>

### <a name="configure-a-visual-studio-team-services-linux-build-agent"></a><span data-ttu-id="9a89f-134">Configurare un agente di compilazione Linux di Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="9a89f-134">Configure a Visual Studio Team Services Linux build agent</span></span>

<span data-ttu-id="9a89f-135">immagini Docker toocreate e push che compilare queste immagini in un registro di sistema di contenitore di Azure da Visual Studio Team Services, è necessario un agente Linux tooregister.</span><span class="sxs-lookup"><span data-stu-id="9a89f-135">toocreate Docker images and push these images into an Azure container registry from a Visual Studio Team Services build, you need tooregister a Linux agent.</span></span> <span data-ttu-id="9a89f-136">Sono disponibili queste opzioni di installazione:</span><span class="sxs-lookup"><span data-stu-id="9a89f-136">You have these installation options:</span></span>

* [<span data-ttu-id="9a89f-137">Distribuire un agente in Linux</span><span class="sxs-lookup"><span data-stu-id="9a89f-137">Deploy an agent on Linux</span></span>](https://www.visualstudio.com/docs/build/admin/agents/v2-linux)

* [<span data-ttu-id="9a89f-138">Usare l'agente di VSTS hello toorun Docker</span><span class="sxs-lookup"><span data-stu-id="9a89f-138">Use Docker toorun hello VSTS agent</span></span>](https://hub.docker.com/r/microsoft/vsts-agent)

### <a name="install-hello-docker-integration-vsts-extension"></a><span data-ttu-id="9a89f-139">Installare l'estensione Docker integrazione VSTS hello</span><span class="sxs-lookup"><span data-stu-id="9a89f-139">Install hello Docker Integration VSTS extension</span></span>

<span data-ttu-id="9a89f-140">Microsoft fornisce un toowork estensione di Visual Studio Team Services con Docker in compilazione e i processi di rilascio.</span><span class="sxs-lookup"><span data-stu-id="9a89f-140">Microsoft provides a VSTS extension toowork with Docker in build and release processes.</span></span> <span data-ttu-id="9a89f-141">Questa estensione è disponibile in hello [VSTS Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker).</span><span class="sxs-lookup"><span data-stu-id="9a89f-141">This extension is available in hello [VSTS Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker).</span></span> <span data-ttu-id="9a89f-142">Fare clic su **installare** tooadd questo account VSTS tooyour estensione:</span><span class="sxs-lookup"><span data-stu-id="9a89f-142">Click **Install** tooadd this extension tooyour VSTS account:</span></span>

![Installare hello integrazione di Docker](./media/container-service-docker-swarm-setup-ci-cd/install-docker-vsts.png)

<span data-ttu-id="9a89f-144">Verrà chiesto di account VSTS tooyour tooconnect utilizzando le credenziali.</span><span class="sxs-lookup"><span data-stu-id="9a89f-144">You are asked tooconnect tooyour VSTS account using your credentials.</span></span> 

### <a name="connect-visual-studio-team-services-and-github"></a><span data-ttu-id="9a89f-145">Connettere Visual Studio Team Services e GitHub</span><span class="sxs-lookup"><span data-stu-id="9a89f-145">Connect Visual Studio Team Services and GitHub</span></span>

<span data-ttu-id="9a89f-146">Impostare una connessione tra il progetto VSTS e l'account GitHub.</span><span class="sxs-lookup"><span data-stu-id="9a89f-146">Set up a connection between your VSTS project and your GitHub account.</span></span>

1. <span data-ttu-id="9a89f-147">Nel progetto di Visual Studio Team Services, fare clic su hello **impostazioni** icona nella barra degli strumenti hello e selezionare **servizi**.</span><span class="sxs-lookup"><span data-stu-id="9a89f-147">In your Visual Studio Team Services project, click hello **Settings** icon in hello toolbar, and select **Services**.</span></span>

    ![Visual Studio Team Services - Connessione esterna](./media/container-service-docker-swarm-setup-ci-cd/vsts-services-menu.png)

2. <span data-ttu-id="9a89f-149">A sinistra di hello, fare clic su **nuovo Endpoint del servizio** > **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="9a89f-149">On hello left, click **New Service Endpoint** > **GitHub**.</span></span>

    ![Visual Studio Team Services - GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github.png)

3. <span data-ttu-id="9a89f-151">Fare clic su tooauthorize VSTS toowork con l'account GitHub, **Authorize** e seguire la procedura di hello nella finestra di hello visualizzata.</span><span class="sxs-lookup"><span data-stu-id="9a89f-151">tooauthorize VSTS toowork with your GitHub account, click **Authorize** and follow hello procedure in hello window that opens.</span></span>

    ![Visual Studio Team Services - Autorizzazione GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-authorize.png)

### <a name="connect-vsts-tooyour-azure-container-registry-and-azure-container-service-cluster"></a><span data-ttu-id="9a89f-153">Connettersi al Registro di sistema VSTS tooyour contenitore di Azure e i cluster del servizio di contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="9a89f-153">Connect VSTS tooyour Azure container registry and Azure Container Service cluster</span></span>

<span data-ttu-id="9a89f-154">ultimi passaggi di Hello prima di ottenere nella pipeline CI/CD hello sono del Registro di sistema di tooconfigure connessioni esterne tooyour contenitore e il cluster Docker Swarm in Azure.</span><span class="sxs-lookup"><span data-stu-id="9a89f-154">hello last steps before getting into hello CI/CD pipeline are tooconfigure external connections tooyour container registry and your Docker Swarm cluster in Azure.</span></span> 

1. <span data-ttu-id="9a89f-155">In hello **servizi** impostazioni del progetto di Visual Studio Team Services, aggiungere un endpoint del servizio di tipo **Registro di sistema Docker**.</span><span class="sxs-lookup"><span data-stu-id="9a89f-155">In hello **Services** settings of your Visual Studio Team Services project, add a service endpoint of type **Docker Registry**.</span></span> 

2. <span data-ttu-id="9a89f-156">Nella finestra popup di hello che viene visualizzata, immettere hello URL e le credenziali di hello Azure contenitore del Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="9a89f-156">In hello popup that opens, enter hello URL and hello credentials of your Azure container registry.</span></span>

    ![Visual Studio Team Services - Docker Registry](./media/container-service-docker-swarm-setup-ci-cd/vsts-registry.png)

3. <span data-ttu-id="9a89f-158">Per cluster di Docker Swarm hello, aggiungere un endpoint di tipo **SSH**.</span><span class="sxs-lookup"><span data-stu-id="9a89f-158">For hello Docker Swarm cluster, add an endpoint of type **SSH**.</span></span> <span data-ttu-id="9a89f-159">Immettere le informazioni sulla connessione del cluster sciame hello SSH.</span><span class="sxs-lookup"><span data-stu-id="9a89f-159">Then enter hello SSH connection information of your Swarm cluster.</span></span>

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-setup-ci-cd/vsts-ssh.png)

<span data-ttu-id="9a89f-161">Le configurazioni di hello vengono effettuate a questo punto.</span><span class="sxs-lookup"><span data-stu-id="9a89f-161">All hello configuration is done now.</span></span> <span data-ttu-id="9a89f-162">Nei passaggi successivi hello creare pipeline di CI/CD hello che crea e distribuisce hello applicazione toohello Docker Swarm cluster.</span><span class="sxs-lookup"><span data-stu-id="9a89f-162">In hello next steps, you create hello CI/CD pipeline that builds and deploys hello application toohello Docker Swarm cluster.</span></span> 

## <a name="step-2-create-hello-build-definition"></a><span data-ttu-id="9a89f-163">Passaggio 2: Creare una definizione di compilazione hello</span><span class="sxs-lookup"><span data-stu-id="9a89f-163">Step 2: Create hello build definition</span></span>

<span data-ttu-id="9a89f-164">In questo passaggio, si imposta definitionfor una compilazione del progetto di Visual Studio Team Services e definisce il flusso di lavoro di hello compilazione per le immagini contenitore</span><span class="sxs-lookup"><span data-stu-id="9a89f-164">In this step, you set up a build definitionfor your VSTS project and define hello build workflow for your container images</span></span>

### <a name="initial-definition-setup"></a><span data-ttu-id="9a89f-165">Configurazione iniziale della definizione</span><span class="sxs-lookup"><span data-stu-id="9a89f-165">Initial definition setup</span></span>

1. <span data-ttu-id="9a89f-166">toocreate una definizione di compilazione, collegare tooyour progetto di Visual Studio Team Services e fare clic su **compilazione & versione**.</span><span class="sxs-lookup"><span data-stu-id="9a89f-166">toocreate a build definition, connect tooyour Visual Studio Team Services project and click **Build & Release**.</span></span> 

2. <span data-ttu-id="9a89f-167">In hello **le definizioni di compilazione** fare clic su **+ nuovo**.</span><span class="sxs-lookup"><span data-stu-id="9a89f-167">In hello **Build definitions** section, click **+ New**.</span></span> <span data-ttu-id="9a89f-168">Seleziona hello **vuoto** modello.</span><span class="sxs-lookup"><span data-stu-id="9a89f-168">Select hello **Empty** template.</span></span>

    ![Visual Studio Team Services - Nuova definizione di compilazione](./media/container-service-docker-swarm-setup-ci-cd/create-build-vsts.png)

3. <span data-ttu-id="9a89f-170">Configurare una nuova compilazione hello con un'origine di repository GitHub, controllo **integrazione continua**e coda dell'agente selezionare hello in cui è stato registrato l'agente Linux.</span><span class="sxs-lookup"><span data-stu-id="9a89f-170">Configure hello new build with a GitHub repository source, check **Continuous integration**, and select hello agent queue where you registered your Linux agent.</span></span> <span data-ttu-id="9a89f-171">Fare clic su **crea** toocreate hello definizione di compilazione.</span><span class="sxs-lookup"><span data-stu-id="9a89f-171">Click **Create** toocreate hello build definition.</span></span>

    ![Visual Studio Team Services - Creazione definizione di compilazione](./media/container-service-docker-swarm-setup-ci-cd/vsts-create-build-github.png)

4. <span data-ttu-id="9a89f-173">In hello **le definizioni di compilazione** pagina, aprire innanzitutto hello **Repository** scheda e configurare hello compilazione toouse hello la biforcazione del progetto MyShop hello creato nei prerequisiti hello.</span><span class="sxs-lookup"><span data-stu-id="9a89f-173">On hello **Build Definitions** page, first open hello **Repository** tab and configure hello build toouse hello fork of hello MyShop project that you created in hello prerequisites.</span></span> <span data-ttu-id="9a89f-174">Assicurarsi di selezionare *acs docs* come hello **ramo predefinito**.</span><span class="sxs-lookup"><span data-stu-id="9a89f-174">Make sure that you select *acs-docs* as hello **Default branch**.</span></span>

    ![Visual Studio Team Services - Configurazione repository di compilazione](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-repo-conf.png)

5. <span data-ttu-id="9a89f-176">In hello **trigger** , configurare hello compilazione toobe attivata dopo ciascun commit.</span><span class="sxs-lookup"><span data-stu-id="9a89f-176">On hello **Triggers** tab, configure hello build toobe triggered after each commit.</span></span> <span data-ttu-id="9a89f-177">Selezionare **Integrazione continua** e **Modifiche bacth**.</span><span class="sxs-lookup"><span data-stu-id="9a89f-177">Select **Continuous integration** and **Batch changes**.</span></span>

    ![Visual Studio Team Services - Configurazione trigger di compilazione](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-trigger-conf.png)

### <a name="define-hello-build-workflow"></a><span data-ttu-id="9a89f-179">Definire il flusso di lavoro di hello compilazione</span><span class="sxs-lookup"><span data-stu-id="9a89f-179">Define hello build workflow</span></span>
<span data-ttu-id="9a89f-180">passaggi successivi Hello definiscono il flusso di lavoro di hello compilazione.</span><span class="sxs-lookup"><span data-stu-id="9a89f-180">hello next steps define hello build workflow.</span></span> <span data-ttu-id="9a89f-181">Esistono cinque toobuild di immagini contenitore per hello *MyShop* dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9a89f-181">There are five container images toobuild for hello *MyShop* application.</span></span> <span data-ttu-id="9a89f-182">Ogni immagine viene creata con Dockerfile si trova in cartelle di progetto hello hello:</span><span class="sxs-lookup"><span data-stu-id="9a89f-182">Each image is built using hello Dockerfile located in hello project folders:</span></span>

* <span data-ttu-id="9a89f-183">ProductsApi</span><span class="sxs-lookup"><span data-stu-id="9a89f-183">ProductsApi</span></span>
* <span data-ttu-id="9a89f-184">Proxy</span><span class="sxs-lookup"><span data-stu-id="9a89f-184">Proxy</span></span>
* <span data-ttu-id="9a89f-185">RatingsApi</span><span class="sxs-lookup"><span data-stu-id="9a89f-185">RatingsApi</span></span>
* <span data-ttu-id="9a89f-186">RecommandationsApi</span><span class="sxs-lookup"><span data-stu-id="9a89f-186">RecommandationsApi</span></span>
* <span data-ttu-id="9a89f-187">ShopFront</span><span class="sxs-lookup"><span data-stu-id="9a89f-187">ShopFront</span></span>

<span data-ttu-id="9a89f-188">Sono necessari due passaggi Docker tooadd per ogni immagine, un'immagine di hello toobuild e un'immagine di hello toopush nel Registro di sistema di hello contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="9a89f-188">You need tooadd two Docker steps for each image, one toobuild hello image, and one toopush hello image in hello Azure container registry.</span></span> 

1. <span data-ttu-id="9a89f-189">Fare clic su un passaggio nel flusso di lavoro compilazione hello tooadd **+ Aggiungi istruzione di compilazione** e selezionare **Docker**.</span><span class="sxs-lookup"><span data-stu-id="9a89f-189">tooadd a step in hello build workflow, click **+ Add build step** and select **Docker**.</span></span>

    ![Visual Studio Team Services - Aggiunta passaggi di compilazione](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-add-task.png)

2. <span data-ttu-id="9a89f-191">Per ogni immagine, configurare un unico passaggio che utilizza hello `docker build` comando.</span><span class="sxs-lookup"><span data-stu-id="9a89f-191">For each image, configure one step that uses hello `docker build` command.</span></span>

    ![Visual Studio Team Services - Compilazione Docker](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-build.png)

    <span data-ttu-id="9a89f-193">Operazione di compilazione hello, selezionare il Registro di sistema di contenitore di Azure, hello **compilare un'immagine** azione e hello Dockerfile che definisce ogni immagine.</span><span class="sxs-lookup"><span data-stu-id="9a89f-193">For hello build operation, select your Azure container registry, hello **Build an image** action, and hello Dockerfile that defines each image.</span></span> <span data-ttu-id="9a89f-194">Set hello **contesto di compilazione** come hello Dockerfile directory radice e definire hello **nome immagine**.</span><span class="sxs-lookup"><span data-stu-id="9a89f-194">Set hello **Build context** as hello Dockerfile root directory, and define hello **Image Name**.</span></span> 
    
    <span data-ttu-id="9a89f-195">Come mostrato nella precedente schermata hello, il nome di immagine hello deve iniziare con hello URI Azure contenitore del Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="9a89f-195">As shown on hello preceding screen, start hello image name with hello URI of your Azure container registry.</span></span> <span data-ttu-id="9a89f-196">(È anche possibile utilizzare un tag di hello tooparameterize variabili di compilazione dell'immagine di hello, ad esempio ID build hello in questo esempio.)</span><span class="sxs-lookup"><span data-stu-id="9a89f-196">(You can also use a build variable tooparameterize hello tag of hello image, such as hello build identifier in this example.)</span></span>

3. <span data-ttu-id="9a89f-197">Per ogni immagine, configurare un secondo passaggio che utilizza hello `docker push` comando.</span><span class="sxs-lookup"><span data-stu-id="9a89f-197">For each image, configure a second step that uses hello `docker push` command.</span></span>

    ![Visual Studio Team Services - Push Docker](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-push.png)

    <span data-ttu-id="9a89f-199">Per l'operazione di push hello, selezionare il Registro di sistema di contenitore di Azure, hello **Push un'immagine** action e immettere hello **nome immagine** che viene compilato nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="9a89f-199">For hello push operation, select your Azure container registry, hello **Push an image** action, and enter hello **Image Name** that is built in hello previous step.</span></span>

4. <span data-ttu-id="9a89f-200">Dopo aver configurato la compilazione hello e push passaggi per ognuna delle cinque immagini hello, aggiungere che altri due passaggi hello del flusso di lavoro di compilazione.</span><span class="sxs-lookup"><span data-stu-id="9a89f-200">After you configure hello build and push steps for each of hello five images, add two more steps in hello build workflow.</span></span>

    <span data-ttu-id="9a89f-201">a.</span><span class="sxs-lookup"><span data-stu-id="9a89f-201">a.</span></span> <span data-ttu-id="9a89f-202">Un'attività da riga di comando che utilizza un hello tooreplace di script bash *BuildNumber* occorrenza nel file di docker compose.yml hello con hello corrente compilare ID. Hello seguente schermata per informazioni dettagliate, vedere.</span><span class="sxs-lookup"><span data-stu-id="9a89f-202">A command-line task that uses a bash script tooreplace hello *BuildNumber* occurrence in hello docker-compose.yml file with hello current build Id. See hello following screen for details.</span></span>

    ![Visual Studio Team Services - Aggiornamento file Compose](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-replace-build-number.png)

    <span data-ttu-id="9a89f-204">b.</span><span class="sxs-lookup"><span data-stu-id="9a89f-204">b.</span></span> <span data-ttu-id="9a89f-205">Un'attività che elimina hello aggiornato Scrivi file come un elemento di compilazione, pertanto può essere utilizzato in versione di hello.</span><span class="sxs-lookup"><span data-stu-id="9a89f-205">A task that drops hello updated Compose file as a build artifact so it can be used in hello release.</span></span> <span data-ttu-id="9a89f-206">Hello seguente schermata per informazioni dettagliate, vedere.</span><span class="sxs-lookup"><span data-stu-id="9a89f-206">See hello following screen for details.</span></span>

    ![Visual Studio Team Services - Pubblicazione file Compose](./media/container-service-docker-swarm-setup-ci-cd/vsts-publish-compose.png) 

5. <span data-ttu-id="9a89f-208">Fare clic su **Salva** e assegnare un nome alla definizione di compilazione.</span><span class="sxs-lookup"><span data-stu-id="9a89f-208">Click **Save** and name your build definition.</span></span>

## <a name="step-3-create-hello-release-definition"></a><span data-ttu-id="9a89f-209">Passaggio 3: Creare una definizione di versione di hello</span><span class="sxs-lookup"><span data-stu-id="9a89f-209">Step 3: Create hello release definition</span></span>

<span data-ttu-id="9a89f-210">Visual Studio Team Services consente troppo[gestire i rilasci in ambienti](https://www.visualstudio.com/team-services/release-management/).</span><span class="sxs-lookup"><span data-stu-id="9a89f-210">Visual Studio Team Services allows you too[manage releases across environments](https://www.visualstudio.com/team-services/release-management/).</span></span> <span data-ttu-id="9a89f-211">È possibile abilitare la distribuzione continua toomake assicurarsi che l'applicazione viene distribuita in diversi ambienti (ad esempio sviluppo, test, pre-produzione e produzione) in modo uniforme.</span><span class="sxs-lookup"><span data-stu-id="9a89f-211">You can enable continuous deployment toomake sure that your application is deployed on your different environments (such as dev, test, pre-production, and production) in a smooth way.</span></span> <span data-ttu-id="9a89f-212">È possibile creare un nuovo ambiente che rappresenti il cluster Docker Swarm del servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="9a89f-212">You can create a new environment that represents your Azure Container Service Docker Swarm cluster.</span></span>

![Visual Studio Team Services - versione tooACS](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-acs.png) 

### <a name="initial-release-setup"></a><span data-ttu-id="9a89f-214">Configurazione iniziale del rilascio</span><span class="sxs-lookup"><span data-stu-id="9a89f-214">Initial release setup</span></span>

1. <span data-ttu-id="9a89f-215">Fare clic su una definizione di versione, toocreate **versioni** > **+ versione**</span><span class="sxs-lookup"><span data-stu-id="9a89f-215">toocreate a release definition, click **Releases** > **+ Release**</span></span>

2. <span data-ttu-id="9a89f-216">origine dell'artefatto hello tooconfigure, fare clic su **elementi** > **collega un'origine artefatto**.</span><span class="sxs-lookup"><span data-stu-id="9a89f-216">tooconfigure hello artifact source, Click **Artifacts** > **Link an artifact source**.</span></span> <span data-ttu-id="9a89f-217">In questo caso, collegare il nuovo toohello build di rilascio definizione definito nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="9a89f-217">Here, link this new release definition toohello build that you defined in hello previous step.</span></span> <span data-ttu-id="9a89f-218">In questo modo, i file di docker compose.yml hello è disponibili nel processo di rilascio hello.</span><span class="sxs-lookup"><span data-stu-id="9a89f-218">By doing this, hello docker-compose.yml file is available in hello release process.</span></span>

    ![Visual Studio Team Services - Rilascio elementi](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-artefacts.png) 

3. <span data-ttu-id="9a89f-220">trigger di rilascio hello tooconfigure, fare clic su **trigger** e selezionare **distribuzione continua**.</span><span class="sxs-lookup"><span data-stu-id="9a89f-220">tooconfigure hello release trigger, click **Triggers** and select **Continuous Deployment**.</span></span> <span data-ttu-id="9a89f-221">Imposta il trigger hello sull'hello stessa origine artefatto.</span><span class="sxs-lookup"><span data-stu-id="9a89f-221">Set hello trigger on hello same artifact source.</span></span> <span data-ttu-id="9a89f-222">Questa impostazione assicura che una nuova versione viene avviata non appena hello compilazione viene completata correttamente.</span><span class="sxs-lookup"><span data-stu-id="9a89f-222">This setting ensures that a new release starts as soon as hello build completes successfully.</span></span>

    ![Visual Studio Team Services - Rilascio trigger](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-trigger.png) 

### <a name="define-hello-release-workflow"></a><span data-ttu-id="9a89f-224">Definizione del flusso di lavoro di hello versione</span><span class="sxs-lookup"><span data-stu-id="9a89f-224">Define hello release workflow</span></span>

<span data-ttu-id="9a89f-225">flusso di lavoro versione Hello è composta da due attività da aggiungere.</span><span class="sxs-lookup"><span data-stu-id="9a89f-225">hello release workflow is composed of two tasks that you add.</span></span>

1. <span data-ttu-id="9a89f-226">Configurare un hello di copia toosecurely attività comporre file tooa *distribuire* cartella hello Docker Swarm nodo principale, utilizzando una connessione SSH hello configurate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9a89f-226">Configure a task toosecurely copy hello compose file tooa *deploy* folder on hello Docker Swarm master node, using hello SSH connection you configured previously.</span></span> <span data-ttu-id="9a89f-227">Hello seguente schermata per informazioni dettagliate, vedere.</span><span class="sxs-lookup"><span data-stu-id="9a89f-227">See hello following screen for details.</span></span>

    ![Visual Studio Team Services - Rilascio SCP](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-scp.png)

2. <span data-ttu-id="9a89f-229">Configurare un secondo tooexecute attività un toorun comando bash `docker` e `docker-compose` comandi sul nodo principale hello.</span><span class="sxs-lookup"><span data-stu-id="9a89f-229">Configure a second task tooexecute a bash command toorun `docker` and `docker-compose` commands on hello master node.</span></span> <span data-ttu-id="9a89f-230">Hello seguente schermata per informazioni dettagliate, vedere.</span><span class="sxs-lookup"><span data-stu-id="9a89f-230">See hello following screen for details.</span></span>

    ![Visual Studio Team Services - Rilascio bash](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-bash.png)

    <span data-ttu-id="9a89f-232">comando Hello eseguito hello utilizzare master hello Docker CLI e hello toodo di Docker Compose CLI hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="9a89f-232">hello command executed on hello master use hello Docker CLI and hello Docker-Compose CLI toodo hello following tasks:</span></span>

    - <span data-ttu-id="9a89f-233">Registro di sistema di account di accesso toohello contenitore di Azure (Usa tre variab'les di compilazione che sono definiti nel hello **variabili** scheda)</span><span class="sxs-lookup"><span data-stu-id="9a89f-233">Login toohello Azure container registry (it uses three build variab\`les that are defined in hello **Variables** tab)</span></span>
    - <span data-ttu-id="9a89f-234">Definire hello **DOCKER_HOST** toowork variabile con endpoint sciame hello (: 2375)</span><span class="sxs-lookup"><span data-stu-id="9a89f-234">Define hello **DOCKER_HOST** variable toowork with hello Swarm endpoint (:2375)</span></span>
    - <span data-ttu-id="9a89f-235">Passare toohello *distribuire* cartella che è stato creato da hello precedenti attività di copia sicuro e che contiene i file di docker compose.yml hello</span><span class="sxs-lookup"><span data-stu-id="9a89f-235">Navigate toohello *deploy* folder that was created by hello preceding secure copy task and that contains hello docker-compose.yml file</span></span> 
    - <span data-ttu-id="9a89f-236">Eseguire `docker-compose` comandi che recuperano nuove immagini hello, arrestare i servizi di hello, rimuovere servizi hello e creare contenitori hello.</span><span class="sxs-lookup"><span data-stu-id="9a89f-236">Execute `docker-compose` commands that pull hello new images, stop hello services, remove hello services, and create hello containers.</span></span>

    >[!IMPORTANT]
    > <span data-ttu-id="9a89f-237">Come mostrato nella precedente schermata hello, lasciare hello **esito negativo in STDERR** casella di controllo deselezionata.</span><span class="sxs-lookup"><span data-stu-id="9a89f-237">As shown on hello preceding screen, leave hello **Fail on STDERR** checkbox unchecked.</span></span> <span data-ttu-id="9a89f-238">Questa è un'impostazione importante, perché `docker-compose` stampa i messaggi di diagnostica diversi, ad esempio i contenitori sono arresto o eliminato, nell'output di errore standard hello.</span><span class="sxs-lookup"><span data-stu-id="9a89f-238">This is an important setting, because `docker-compose` prints several diagnostic messages, such as containers are stopping or being deleted, on hello standard error output.</span></span> <span data-ttu-id="9a89f-239">Se si seleziona la casella di controllo di hello, Visual Studio Team Services indica che si sono verificati errori durante il rilascio di hello, anche se tutto va bene.</span><span class="sxs-lookup"><span data-stu-id="9a89f-239">If you check hello checkbox, Visual Studio Team Services reports that errors occurred during hello release, even if all goes well.</span></span>
    >
3. <span data-ttu-id="9a89f-240">Salvare la nuova definizione di rilascio.</span><span class="sxs-lookup"><span data-stu-id="9a89f-240">Save this new release definition.</span></span>


>[!NOTE]
><span data-ttu-id="9a89f-241">Questa distribuzione include i tempi di inattività Poiché stiamo l'arresto dei servizi precedente hello e in esecuzione hello uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="9a89f-241">This deployment includes some downtime because we are stopping hello old services and running hello new one.</span></span> <span data-ttu-id="9a89f-242">Si tratta tooavoid possibili effettuando una distribuzione verde-blu.</span><span class="sxs-lookup"><span data-stu-id="9a89f-242">It is possible tooavoid this by doing a blue-green deployment.</span></span>
>

## <a name="step-4-test-hello-cicd-pipeline"></a><span data-ttu-id="9a89f-243">Passaggio 4.</span><span class="sxs-lookup"><span data-stu-id="9a89f-243">Step 4.</span></span> <span data-ttu-id="9a89f-244">Testare hello CI/CD pipeline</span><span class="sxs-lookup"><span data-stu-id="9a89f-244">Test hello CI/CD pipeline</span></span>

<span data-ttu-id="9a89f-245">Dopo avere con configurazione hello, è ora tootest questa nuova pipeline CI/CD-ROM.</span><span class="sxs-lookup"><span data-stu-id="9a89f-245">Now that you are done with hello configuration, it's time tootest this new CI/CD pipeline.</span></span> <span data-ttu-id="9a89f-246">tootest modo più semplice Hello è tooupdate hello origine codice e il commit hello modifiche nel repository GitHub.</span><span class="sxs-lookup"><span data-stu-id="9a89f-246">hello easiest way tootest it is tooupdate hello source code and commit hello changes into your GitHub repository.</span></span> <span data-ttu-id="9a89f-247">Pochi secondi dopo che si esegue il push codice hello, si noterà una nuova compilazione in esecuzione in Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="9a89f-247">A few seconds after you push hello code, you will see a new build running in Visual Studio Team Services.</span></span> <span data-ttu-id="9a89f-248">Una volta completata, una nuova versione verrà attivata e verrà distribuita hello nuova versione dell'applicazione hello in cluster del servizio di contenitore di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9a89f-248">Once completed successfully, a new release will be triggered and will deploy hello new version of hello application on hello Azure Container Service cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a89f-249">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9a89f-249">Next Steps</span></span>

* <span data-ttu-id="9a89f-250">Per ulteriori informazioni sull'elemento di configurazione/CD con Visual Studio Team Services, vedere hello [Panoramica di compilazione VSTS](https://www.visualstudio.com/docs/build/overview).</span><span class="sxs-lookup"><span data-stu-id="9a89f-250">For more information about CI/CD with Visual Studio Team Services, see hello [VSTS Build overview](https://www.visualstudio.com/docs/build/overview).</span></span>
