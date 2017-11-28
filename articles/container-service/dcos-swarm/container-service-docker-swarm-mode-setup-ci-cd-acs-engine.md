---
title: "aaaCI/CD con motore del servizio contenitore di Azure e la modalità Swarm | Documenti Microsoft"
description: "Utilizzare il motore del servizio contenitore di Azure con Docker Swarm modalità, un registro di sistema contenitore di Azure e Visual Studio Team Services toodeliver continuamente un'applicazione .NET Core multi-contenitore"
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
ms.openlocfilehash: 040522c452f7ea0ce3c92f2fe57b1c141b97e380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-acs-engine-and-docker-swarm-mode-using-visual-studio-team-services"></a><span data-ttu-id="6a5d2-104">CI/CD completo della pipeline toodeploy un'applicazione multi-contenitore nel servizio contenitore di Azure con il motore di ACS e Docker Swarm modalità utilizzando Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="6a5d2-104">Full CI/CD pipeline toodeploy a multi-container application on Azure Container Service with ACS Engine and Docker Swarm Mode using Visual Studio Team Services</span></span>

<span data-ttu-id="6a5d2-105">*Questo articolo si basa su [CI/CD completo della pipeline toodeploy un'applicazione multi-contenitore nel servizio di Azure contenitore con Docker Swarm con Visual Studio Team Services](container-service-docker-swarm-setup-ci-cd.md) documentazione*</span><span class="sxs-lookup"><span data-stu-id="6a5d2-105">*This article is based on [Full CI/CD pipeline toodeploy a multi-container application on Azure Container Service with Docker Swarm using Visual Studio Team Services](container-service-docker-swarm-setup-ci-cd.md) documentation*</span></span>

<span data-ttu-id="6a5d2-106">Oggi, uno di hello maggiori sfide durante lo sviluppo di applicazioni moderne per cloud hello toodeliver in grado di queste applicazioni in modo continuo.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-106">Nowadays, One of hello biggest challenges when developing modern applications for hello cloud is being able toodeliver these applications continuously.</span></span> <span data-ttu-id="6a5d2-107">In questo articolo è illustrato come tooimplement un'integrazione completa continua e distribuzione (CI/CD) di pipeline utilizzando:</span><span class="sxs-lookup"><span data-stu-id="6a5d2-107">In this article, you learn how tooimplement a full continuous integration and deployment (CI/CD) pipeline using:</span></span> 
* <span data-ttu-id="6a5d2-108">Motore del servizio contenitore di Azure con la modalità Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="6a5d2-108">Azure Container Service Engine with Docker Swarm Mode</span></span>
* <span data-ttu-id="6a5d2-109">Registro di sistema del contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="6a5d2-109">Azure Container Registry</span></span>
* <span data-ttu-id="6a5d2-110">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="6a5d2-110">Visual Studio Team Services</span></span>

<span data-ttu-id="6a5d2-111">Questo articolo si basa su una semplice applicazione, disponibile in [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux) e sviluppata con ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-111">This article is based on a simple application, available on [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux), developed with ASP.NET Core.</span></span> <span data-ttu-id="6a5d2-112">un'applicazione Hello è composta da quattro diversi servizi: tre web API e un solo web front-end:</span><span class="sxs-lookup"><span data-stu-id="6a5d2-112">hello application is composed of four different services: three web APIs and one web front end:</span></span>

![Applicazione MyShop di esempio](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/myshop-application.png)

<span data-ttu-id="6a5d2-114">obiettivo di Hello è toodeliver questa applicazione in modo continuo in un cluster di Docker Swarm modalità, tramite Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-114">hello objective is toodeliver this application continuously in a Docker Swarm Mode cluster, using Visual Studio Team Services.</span></span> <span data-ttu-id="6a5d2-115">Hello figura riportata di seguito i dettagli questa pipeline il recapito continuo:</span><span class="sxs-lookup"><span data-stu-id="6a5d2-115">hello following figure details this continuous delivery pipeline:</span></span>

![Applicazione MyShop di esempio](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/full-ci-cd-pipeline.png)

<span data-ttu-id="6a5d2-117">Di seguito è riportata una breve spiegazione dei passaggi di hello:</span><span class="sxs-lookup"><span data-stu-id="6a5d2-117">Here is a brief explanation of hello steps:</span></span>

1. <span data-ttu-id="6a5d2-118">Le modifiche al codice sono repository di codice sorgente toohello commit (in questo esempio GitHub)</span><span class="sxs-lookup"><span data-stu-id="6a5d2-118">Code changes are committed toohello source code repository (here, GitHub)</span></span> 
2. <span data-ttu-id="6a5d2-119">GitHub attiva una compilazione in Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="6a5d2-119">GitHub triggers a build in Visual Studio Team Services</span></span> 
3. <span data-ttu-id="6a5d2-120">Visual Studio Team Services Ottiene hello la versione più recente di origini di hello e compila tutte le immagini di hello che compongono un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="6a5d2-120">Visual Studio Team Services gets hello latest version of hello sources and builds all hello images that compose hello application</span></span> 
4. <span data-ttu-id="6a5d2-121">Visual Studio Team Services inserisce ogni immagine tooa Docker del Registro di sistema creato con il servizio di Azure del Registro di sistema contenitore hello</span><span class="sxs-lookup"><span data-stu-id="6a5d2-121">Visual Studio Team Services pushes each image tooa Docker registry created using hello Azure Container Registry service</span></span> 
5. <span data-ttu-id="6a5d2-122">Visual Studio Team Services attiva un nuovo rilascio</span><span class="sxs-lookup"><span data-stu-id="6a5d2-122">Visual Studio Team Services triggers a new release</span></span> 
6. <span data-ttu-id="6a5d2-123">versione di Hello esegue alcuni comandi tramite SSH nel nodo principale di hello Azure contenitore del servizio cluster</span><span class="sxs-lookup"><span data-stu-id="6a5d2-123">hello release runs some commands using SSH on hello Azure container service cluster master node</span></span> 
7. <span data-ttu-id="6a5d2-124">Docker Swarm modalità cluster hello estrae hello versione immagini hello</span><span class="sxs-lookup"><span data-stu-id="6a5d2-124">Docker Swarm Mode on hello cluster pulls hello latest version of hello images</span></span> 
8. <span data-ttu-id="6a5d2-125">nuova versione di Hello di un'applicazione hello viene distribuito con Stack di Docker</span><span class="sxs-lookup"><span data-stu-id="6a5d2-125">hello new version of hello application is deployed using Docker Stack</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6a5d2-126">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6a5d2-126">Prerequisites</span></span>

<span data-ttu-id="6a5d2-127">Prima di iniziare questa esercitazione, è necessario hello toocomplete seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="6a5d2-127">Before starting this tutorial, you need toocomplete hello following tasks:</span></span>

- [<span data-ttu-id="6a5d2-128">Creare un cluster in modalità Swarm nel servizio contenitore di Azure con il motore del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="6a5d2-128">Create a Swarm Mode cluster in Azure Container Service with ACS Engine</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acsengine-swarmmode)
- [<span data-ttu-id="6a5d2-129">Connettersi con cluster sciame hello contenitore nel servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="6a5d2-129">Connect with hello Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)
- [<span data-ttu-id="6a5d2-130">Creare un Registro di sistema del contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="6a5d2-130">Create an Azure container registry</span></span>](../../container-registry/container-registry-get-started-portal.md)
- [<span data-ttu-id="6a5d2-131">Disporre di un account Visual Studio Team Services e aver creato un progetto di team</span><span class="sxs-lookup"><span data-stu-id="6a5d2-131">Have a Visual Studio Team Services account and team project created</span></span>](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [<span data-ttu-id="6a5d2-132">Fork hello GitHub repository tooyour account GitHub</span><span class="sxs-lookup"><span data-stu-id="6a5d2-132">Fork hello GitHub repository tooyour GitHub account</span></span>](https://github.com/jcorioland/MyShop/tree/docker-linux)

>[!NOTE]
> <span data-ttu-id="6a5d2-133">orchestrator Docker Swarm Hello contenitore nel servizio di Azure Usa autonomo legacy sciame.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-133">hello Docker Swarm orchestrator in Azure Container Service uses legacy standalone Swarm.</span></span> <span data-ttu-id="6a5d2-134">Attualmente, hello integrato [modalità sciame](https://docs.docker.com/engine/swarm/) (in Docker 1.12 e versione successiva) non è un agente di orchestrazione supportati nel servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-134">Currently, hello integrated [Swarm mode](https://docs.docker.com/engine/swarm/) (in Docker 1.12 and higher) is not a supported orchestrator in Azure Container Service.</span></span> <span data-ttu-id="6a5d2-135">Per questo motivo, si sta usando [motore ACS](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), contributo della community [modello delle Guide rapide](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), o una soluzione di Docker in hello [Azure Marketplace](https://azuremarketplace.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="6a5d2-135">For this reason, we are using [ACS Engine](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), a community-contributed [quickstart template](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), or a Docker solution in hello [Azure Marketplace](https://azuremarketplace.microsoft.com).</span></span>
>

## <a name="step-1-configure-your-visual-studio-team-services-account"></a><span data-ttu-id="6a5d2-136">Passaggio 1: Configurare l'account di Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="6a5d2-136">Step 1: Configure your Visual Studio Team Services account</span></span> 

<span data-ttu-id="6a5d2-137">In questa sezione viene configurato l'account di Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-137">In this section, you configure your Visual Studio Team Services account.</span></span> <span data-ttu-id="6a5d2-138">gli endpoint di servizi di VSTS tooconfigure, nel progetto di Visual Studio Team Services, fare clic su hello **impostazioni** icona nella barra degli strumenti hello e selezionare **servizi**.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-138">tooconfigure VSTS Services Endpoints, in your Visual Studio Team Services project, click hello **Settings** icon in hello toolbar, and select **Services**.</span></span>

![Aprire l'endpoint dei servizi](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/services-vsts.PNG)

### <a name="connect-visual-studio-team-services-and-azure-account"></a><span data-ttu-id="6a5d2-140">Connettere Visual Studio Team Services e l'account Azure</span><span class="sxs-lookup"><span data-stu-id="6a5d2-140">Connect Visual Studio Team Services and Azure account</span></span>

<span data-ttu-id="6a5d2-141">Impostare una connessione tra il progetto VSTS e l'account Azure.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-141">Set up a connection between your VSTS project and your Azure account.</span></span>

1. <span data-ttu-id="6a5d2-142">A sinistra di hello, fare clic su **nuovo Endpoint del servizio** > **Azure Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-142">On hello left, click **New Service Endpoint** > **Azure Resource Manager**.</span></span>
2. <span data-ttu-id="6a5d2-143">tooauthorize VSTS toowork con un account Azure, selezionare il **sottoscrizione** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-143">tooauthorize VSTS toowork with your Azure account, select your **Subscription** and click **OK**.</span></span>

    ![Visual Studio Team Services - Autorizzazione di Azure](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-azure.PNG)

### <a name="connect-visual-studio-team-services-and-github"></a><span data-ttu-id="6a5d2-145">Connettere Visual Studio Team Services e GitHub</span><span class="sxs-lookup"><span data-stu-id="6a5d2-145">Connect Visual Studio Team Services and GitHub</span></span>

<span data-ttu-id="6a5d2-146">Impostare una connessione tra il progetto VSTS e l'account GitHub.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-146">Set up a connection between your VSTS project and your GitHub account.</span></span>

1. <span data-ttu-id="6a5d2-147">A sinistra di hello, fare clic su **nuovo Endpoint del servizio** > **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-147">On hello left, click **New Service Endpoint** > **GitHub**.</span></span>
2. <span data-ttu-id="6a5d2-148">Fare clic su tooauthorize VSTS toowork con l'account GitHub, **Authorize** e seguire la procedura di hello nella finestra di hello visualizzata.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-148">tooauthorize VSTS toowork with your GitHub account, click **Authorize** and follow hello procedure in hello window that opens.</span></span>

    ![Visual Studio Team Services - Autorizzazione GitHub](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github.png)

### <a name="connect-vsts-tooyour-azure-container-service-cluster"></a><span data-ttu-id="6a5d2-150">Connettere VSTS tooyour Azure contenitore Servizio cluster</span><span class="sxs-lookup"><span data-stu-id="6a5d2-150">Connect VSTS tooyour Azure Container Service cluster</span></span>

<span data-ttu-id="6a5d2-151">ultimi passaggi di Hello prima di ottenere nella pipeline CI/CD hello sono tooconfigure cluster di Docker Swarm connessioni esterne tooyour in Azure.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-151">hello last steps before getting into hello CI/CD pipeline are tooconfigure external connections tooyour Docker Swarm cluster in Azure.</span></span> 

1. <span data-ttu-id="6a5d2-152">Per cluster di Docker Swarm hello, aggiungere un endpoint di tipo **SSH**.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-152">For hello Docker Swarm cluster, add an endpoint of type **SSH**.</span></span> <span data-ttu-id="6a5d2-153">Immettere le informazioni di connessione SSH hello del cluster sciame (nodo principale).</span><span class="sxs-lookup"><span data-stu-id="6a5d2-153">Then enter hello SSH connection information of your Swarm cluster (master node).</span></span>

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-ssh.png)

<span data-ttu-id="6a5d2-155">Le configurazioni di hello vengono effettuate a questo punto.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-155">All hello configuration is done now.</span></span> <span data-ttu-id="6a5d2-156">Nei passaggi successivi hello creare pipeline di CI/CD hello che crea e distribuisce hello applicazione toohello Docker Swarm cluster.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-156">In hello next steps, you create hello CI/CD pipeline that builds and deploys hello application toohello Docker Swarm cluster.</span></span> 

## <a name="step-2-create-hello-build-definition"></a><span data-ttu-id="6a5d2-157">Passaggio 2: Creare una definizione di compilazione hello</span><span class="sxs-lookup"><span data-stu-id="6a5d2-157">Step 2: Create hello build definition</span></span>

<span data-ttu-id="6a5d2-158">In questo passaggio, si imposta una definizione di compilazione per il progetto di Visual Studio Team Services e definisce il flusso di lavoro di hello compilazione per le immagini contenitore</span><span class="sxs-lookup"><span data-stu-id="6a5d2-158">In this step, you set up a build definition for your VSTS project and define hello build workflow for your container images</span></span>

### <a name="initial-definition-setup"></a><span data-ttu-id="6a5d2-159">Configurazione iniziale della definizione</span><span class="sxs-lookup"><span data-stu-id="6a5d2-159">Initial definition setup</span></span>

1. <span data-ttu-id="6a5d2-160">toocreate una definizione di compilazione, collegare tooyour progetto di Visual Studio Team Services e fare clic su **compilazione & versione**.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-160">toocreate a build definition, connect tooyour Visual Studio Team Services project and click **Build & Release**.</span></span> <span data-ttu-id="6a5d2-161">In hello **le definizioni di compilazione** fare clic su **+ nuovo**.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-161">In hello **Build definitions** section, click **+ New**.</span></span> 

    ![Visual Studio Team Services - Nuova definizione di compilazione](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-build-vsts.PNG)

2. <span data-ttu-id="6a5d2-163">Seleziona hello **processo vuoto**.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-163">Select hello **Empty process**.</span></span>

    ![Visual Studio Team Services - Nuova definizione di compilazione vuota](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-empty-build-vsts.PNG)

4. <span data-ttu-id="6a5d2-165">Quindi, fare clic su hello **variabili** scheda e creare due nuove variabili: **RegistryURL** e **AgentURL**.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-165">Then, click hello **Variables** tab and create two new variables: **RegistryURL** and **AgentURL**.</span></span> <span data-ttu-id="6a5d2-166">Incollare i valori hello del Registro di sistema e DNS di agenti di Cluster.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-166">Paste hello values of your Registry and Cluster Agents DNS.</span></span>

    ![Visual Studio Team Services - Configurazione variabili di compilazione](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-variables.png)

5. <span data-ttu-id="6a5d2-168">In hello **le definizioni di compilazione** pagina, aprire hello **trigger** scheda e configurare l'integrazione continua di hello compilazione toouse con biforcazione hello del progetto MyShop hello creato nei prerequisiti hello.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-168">On hello **Build Definitions** page, open hello **Triggers** tab and configure hello build toouse continuous integration with hello fork of hello MyShop project that you created in hello prerequisites.</span></span> <span data-ttu-id="6a5d2-169">Selezionare quindi **Modifiche batch**.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-169">Then, select **Batch changes**.</span></span> <span data-ttu-id="6a5d2-170">Assicurarsi di selezionare *docker linux* come hello **ramo specifica**.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-170">Make sure that you select *docker-linux* as hello **Branch specification**.</span></span>

    ![Visual Studio Team Services - Configurazione repository di compilazione](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github-repo-conf.PNG)


6. <span data-ttu-id="6a5d2-172">Infine, fare clic su hello **opzioni** scheda e configurare coda dell'agente di hello predefinito troppo**ospitato anteprima Linux**.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-172">Finally, click hello **Options** tab and configure hello Default agent queue too**Hosted Linux Preview**.</span></span>

    ![Visual Studio Team Services - Configurazione agente host](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-agent.png)

### <a name="define-hello-build-workflow"></a><span data-ttu-id="6a5d2-174">Definire il flusso di lavoro di hello compilazione</span><span class="sxs-lookup"><span data-stu-id="6a5d2-174">Define hello build workflow</span></span>
<span data-ttu-id="6a5d2-175">passaggi successivi Hello definiscono il flusso di lavoro di hello compilazione.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-175">hello next steps define hello build workflow.</span></span> <span data-ttu-id="6a5d2-176">In primo luogo, è necessario origine hello tooconfigure di codice hello.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-176">First, you need tooconfigure hello source of hello code.</span></span> <span data-ttu-id="6a5d2-177">toodo esso, selezionare **GitHub** e **repository** e **ramo** (docker linux).</span><span class="sxs-lookup"><span data-stu-id="6a5d2-177">toodo it, select **GitHub** and your **repository** and **branch** (docker-linux).</span></span>

![Visual Studio Team Services - Configurazione origine del codice](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-source-code.png)

<span data-ttu-id="6a5d2-179">Esistono cinque toobuild di immagini contenitore per hello *MyShop* dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-179">There are five container images toobuild for hello *MyShop* application.</span></span> <span data-ttu-id="6a5d2-180">Ogni immagine viene creata con Dockerfile si trova in cartelle di progetto hello hello:</span><span class="sxs-lookup"><span data-stu-id="6a5d2-180">Each image is built using hello Dockerfile located in hello project folders:</span></span>

* <span data-ttu-id="6a5d2-181">ProductsApi</span><span class="sxs-lookup"><span data-stu-id="6a5d2-181">ProductsApi</span></span>
* <span data-ttu-id="6a5d2-182">Proxy</span><span class="sxs-lookup"><span data-stu-id="6a5d2-182">Proxy</span></span>
* <span data-ttu-id="6a5d2-183">RatingsApi</span><span class="sxs-lookup"><span data-stu-id="6a5d2-183">RatingsApi</span></span>
* <span data-ttu-id="6a5d2-184">RecommandationsApi</span><span class="sxs-lookup"><span data-stu-id="6a5d2-184">RecommandationsApi</span></span>
* <span data-ttu-id="6a5d2-185">ShopFront</span><span class="sxs-lookup"><span data-stu-id="6a5d2-185">ShopFront</span></span>

<span data-ttu-id="6a5d2-186">Sono necessari due passaggi di Docker per ogni immagine, un'immagine di hello toobuild e un'immagine di hello toopush nel Registro di sistema di hello contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-186">You need two Docker steps for each image, one toobuild hello image, and one toopush hello image in hello Azure container registry.</span></span> 

1. <span data-ttu-id="6a5d2-187">Fare clic su un passaggio nel flusso di lavoro compilazione hello tooadd **+ Aggiungi istruzione di compilazione** e selezionare **Docker**.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-187">tooadd a step in hello build workflow, click **+ Add build step** and select **Docker**.</span></span>

    ![Visual Studio Team Services - Aggiunta passaggi di compilazione](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-add-task.png)

2. <span data-ttu-id="6a5d2-189">Per ogni immagine, configurare un unico passaggio che utilizza hello `docker build` comando.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-189">For each image, configure one step that uses hello `docker build` command.</span></span>

    ![Visual Studio Team Services - Compilazione Docker](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-build.png)

    <span data-ttu-id="6a5d2-191">Operazione di compilazione hello, selezionare il Registro di sistema di contenitore di Azure, hello **compilare un'immagine** azione e hello Dockerfile che definisce ogni immagine.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-191">For hello build operation, select your Azure Container Registry, hello **Build an image** action, and hello Dockerfile that defines each image.</span></span> <span data-ttu-id="6a5d2-192">Set hello **la Directory di lavoro** come directory radice di hello Dockerfile, definire hello **nome immagine**e selezionare **includere Tag più recente**.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-192">Set hello **Working Directory** as hello Dockerfile root directory, define hello **Image Name**, and select **Include Latest Tag**.</span></span>
    
    <span data-ttu-id="6a5d2-193">Nome dell'immagine di Hello è toobe nel formato: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-193">hello Image Name has toobe in this format: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```.</span></span> <span data-ttu-id="6a5d2-194">Sostituire **[nome]** con nome immagine hello:</span><span class="sxs-lookup"><span data-stu-id="6a5d2-194">Replace **[NAME]** with hello image name:</span></span>
    - ```proxy```
    - ```products-api```
    - ```ratings-api```
    - ```recommendations-api```
    - ```shopfront```

3. <span data-ttu-id="6a5d2-195">Per ogni immagine, configurare un secondo passaggio che utilizza hello `docker push` comando.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-195">For each image, configure a second step that uses hello `docker push` command.</span></span>

    ![Visual Studio Team Services - Push Docker](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-push.png)

    <span data-ttu-id="6a5d2-197">Per l'operazione di push hello, selezionare il Registro di sistema di contenitore di Azure, hello **Push un'immagine** azione, immettere hello **nome immagine** che viene compilato nel passaggio precedente hello e scegliere **includere Tag più recente** .</span><span class="sxs-lookup"><span data-stu-id="6a5d2-197">For hello push operation, select your Azure container registry, hello **Push an image** action, enter hello **Image Name** that is built in hello previous step and select **Include Latest Tag**.</span></span>

4. <span data-ttu-id="6a5d2-198">Dopo aver configurato la compilazione hello e push passaggi per ognuna delle cinque immagini hello, aggiungere che tre ulteriori passaggi hello del flusso di lavoro di compilazione.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-198">After you configure hello build and push steps for each of hello five images, add three more steps in hello build workflow.</span></span>

   ![Visual Studio Team Services - Aggiunta di attività della riga di comando](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-command-task.png)

      1. <span data-ttu-id="6a5d2-200">Un'attività da riga di comando che utilizza un hello tooreplace di script bash *RegistryURL* occorrenza nel file di docker compose.yml hello con variabile RegistryURL hello.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-200">A command-line task that uses a bash script tooreplace hello *RegistryURL* occurrence in hello docker-compose.yml file with hello RegistryURL variable.</span></span> 
    
          ```-c "sed -i 's/RegistryUrl/$(RegistryURL)/g' src/docker-compose-v3.yml"```

          ![Visual Studio Team Services - Aggiornamento file Compose con URL del registro](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-replace-registry.png)

      2. <span data-ttu-id="6a5d2-202">Un'attività da riga di comando che utilizza un hello tooreplace di script bash *AgentURL* occorrenza nel file di docker compose.yml hello con variabile AgentURL hello.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-202">A command-line task that uses a bash script tooreplace hello *AgentURL* occurrence in hello docker-compose.yml file with hello AgentURL variable.</span></span>
  
          ```-c "sed -i 's/AgentUrl/$(AgentURL)/g' src/docker-compose-v3.yml"```

     3. <span data-ttu-id="6a5d2-203">Un'attività che elimina hello aggiornato Scrivi file come un elemento di compilazione, pertanto può essere utilizzato in versione di hello.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-203">A task that drops hello updated Compose file as a build artifact so it can be used in hello release.</span></span> <span data-ttu-id="6a5d2-204">Hello seguente schermata per informazioni dettagliate, vedere.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-204">See hello following screen for details.</span></span>

         ![Visual Studio Team Services - Pubblicazione elemento](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish.png) 

         ![Visual Studio Team Services - Pubblicazione file Compose](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish-compose.png) 

5. <span data-ttu-id="6a5d2-207">Fare clic su **Salva e coda** tootest la definizione di compilazione.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-207">Click **Save & queue** tootest your build definition.</span></span>

   ![Visual Studio Team Services - Salva e accoda](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-save.png) 

   ![Visual Studio Team Services - Nuova coda](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-queue.png) 

6. <span data-ttu-id="6a5d2-210">Se hello **compilare** sia corretto, si dispone di toosee questa schermata:</span><span class="sxs-lookup"><span data-stu-id="6a5d2-210">If hello **Build** is correct, you have toosee this screen:</span></span>

  ![Visual Studio Team Services - Compilazione completata](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-succeeded.png) 

## <a name="step-3-create-hello-release-definition"></a><span data-ttu-id="6a5d2-212">Passaggio 3: Creare una definizione di versione di hello</span><span class="sxs-lookup"><span data-stu-id="6a5d2-212">Step 3: Create hello release definition</span></span>

<span data-ttu-id="6a5d2-213">Visual Studio Team Services consente troppo[gestire i rilasci in ambienti](https://www.visualstudio.com/team-services/release-management/).</span><span class="sxs-lookup"><span data-stu-id="6a5d2-213">Visual Studio Team Services allows you too[manage releases across environments](https://www.visualstudio.com/team-services/release-management/).</span></span> <span data-ttu-id="6a5d2-214">È possibile abilitare la distribuzione continua toomake assicurarsi che l'applicazione viene distribuita in diversi ambienti (ad esempio sviluppo, test, pre-produzione e produzione) in modo uniforme.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-214">You can enable continuous deployment toomake sure that your application is deployed on your different environments (such as dev, test, pre-production, and production) in a smooth way.</span></span> <span data-ttu-id="6a5d2-215">È possibile creare un ambiente che rappresenti il cluster della modalità Docker Swarm del servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-215">You can create an environment that represents your Azure Container Service Docker Swarm Mode cluster.</span></span>

![Visual Studio Team Services - versione tooACS](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-acs.png) 

### <a name="initial-release-setup"></a><span data-ttu-id="6a5d2-217">Configurazione iniziale del rilascio</span><span class="sxs-lookup"><span data-stu-id="6a5d2-217">Initial release setup</span></span>

1. <span data-ttu-id="6a5d2-218">Fare clic su una definizione di versione, toocreate **versioni** > **+ versione**</span><span class="sxs-lookup"><span data-stu-id="6a5d2-218">toocreate a release definition, click **Releases** > **+ Release**</span></span>

2. <span data-ttu-id="6a5d2-219">origine dell'artefatto hello tooconfigure, fare clic su **elementi** > **collega un'origine artefatto**.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-219">tooconfigure hello artifact source, Click **Artifacts** > **Link an artifact source**.</span></span> <span data-ttu-id="6a5d2-220">In questo caso, collegare il nuovo toohello build di rilascio definizione definito nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-220">Here, link this new release definition toohello build that you defined in hello previous step.</span></span> <span data-ttu-id="6a5d2-221">Successivamente, è disponibile nel processo di rilascio hello file docker compose.yml hello.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-221">After that, hello docker-compose.yml file is available in hello release process.</span></span>

    ![Visual Studio Team Services - Rilascio elementi](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-artefacts.png) 

3. <span data-ttu-id="6a5d2-223">trigger di rilascio hello tooconfigure, fare clic su **trigger** e selezionare **distribuzione continua**.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-223">tooconfigure hello release trigger, click **Triggers** and select **Continuous Deployment**.</span></span> <span data-ttu-id="6a5d2-224">Imposta il trigger hello sull'hello stessa origine artefatto.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-224">Set hello trigger on hello same artifact source.</span></span> <span data-ttu-id="6a5d2-225">Questa impostazione assicura che una nuova versione viene avviata quando hello compilazione viene completata correttamente.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-225">This setting ensures that a new release starts when hello build completes successfully.</span></span>

    ![Visual Studio Team Services - Rilascio trigger](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-trigger.png) 

4. <span data-ttu-id="6a5d2-227">Fare clic su variabili di versione di hello tooconfigure, **variabili** e selezionare **+ variabile** toocreate tre nuove variabili con informazioni hello del Registro di sistema hello: **docker.username**, **docker.password**, e **docker.registry**.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-227">tooconfigure hello release variables, click **Variables** and select **+Variable** toocreate three new variables with hello info of hello registry: **docker.username**, **docker.password**, and **docker.registry**.</span></span> <span data-ttu-id="6a5d2-228">Incollare i valori hello del Registro di sistema e DNS di agenti di Cluster.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-228">Paste hello values of your Registry and Cluster Agents DNS.</span></span>

    ![Visual Studio Team Services - Configurazione repository di compilazione](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-variables.png)

    >[!IMPORTANT]
    > <span data-ttu-id="6a5d2-230">Come illustrato nella schermata precedente hello, fare clic su hello **blocco** docker.password casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-230">As shown on hello previous screen, click hello **Lock** checkbox in docker.password.</span></span> <span data-ttu-id="6a5d2-231">Questa impostazione è la password di hello toorestrict importanti.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-231">This setting is important toorestrict hello password.</span></span>
    >

### <a name="define-hello-release-workflow"></a><span data-ttu-id="6a5d2-232">Definizione del flusso di lavoro di hello versione</span><span class="sxs-lookup"><span data-stu-id="6a5d2-232">Define hello release workflow</span></span>

<span data-ttu-id="6a5d2-233">flusso di lavoro versione Hello è composta da due attività da aggiungere.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-233">hello release workflow is composed of two tasks that you add.</span></span>

1. <span data-ttu-id="6a5d2-234">Configurare un hello di copia toosecurely attività comporre file tooa *distribuire* cartella hello Docker Swarm nodo principale, utilizzando una connessione SSH hello configurate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-234">Configure a task toosecurely copy hello compose file tooa *deploy* folder on hello Docker Swarm master node, using hello SSH connection you configured previously.</span></span> <span data-ttu-id="6a5d2-235">Hello seguente schermata per informazioni dettagliate, vedere.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-235">See hello following screen for details.</span></span>
    
    <span data-ttu-id="6a5d2-236">Cartella di origine: ```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```</span><span class="sxs-lookup"><span data-stu-id="6a5d2-236">Source folder: ```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```</span></span>

    ![Visual Studio Team Services - Rilascio SCP](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-scp.png)

2. <span data-ttu-id="6a5d2-238">Configurare un secondo tooexecute attività un toorun comando bash `docker` e `docker stack deploy` comandi sul nodo principale hello.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-238">Configure a second task tooexecute a bash command toorun `docker` and `docker stack deploy` commands on hello master node.</span></span> <span data-ttu-id="6a5d2-239">Hello seguente schermata per informazioni dettagliate, vedere.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-239">See hello following screen for details.</span></span>

    ```docker login -u $(docker.username) -p $(docker.password) $(docker.registry) && export DOCKER_HOST=:2375 && cd deploy && docker stack deploy --compose-file docker-compose-v3.yml myshop --with-registry-auth```

    ![Visual Studio Team Services - Rilascio bash](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-bash.png)

    <span data-ttu-id="6a5d2-241">comando Hello eseguito sul master hello utilizza hello Docker CLI e hello toodo di Docker Compose CLI hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="6a5d2-241">hello command executed on hello master uses hello Docker CLI and hello Docker-Compose CLI toodo hello following tasks:</span></span>

    - <span data-ttu-id="6a5d2-242">Accedi al Registro di sistema toohello contenitore di Azure (Usa tre variabili di compilazione che sono definite nel hello **variabili** scheda)</span><span class="sxs-lookup"><span data-stu-id="6a5d2-242">Log in toohello Azure container registry (it uses three build variables that are defined in hello **Variables** tab)</span></span>
    - <span data-ttu-id="6a5d2-243">Definire hello **DOCKER_HOST** toowork variabile con endpoint sciame hello (: 2375)</span><span class="sxs-lookup"><span data-stu-id="6a5d2-243">Define hello **DOCKER_HOST** variable toowork with hello Swarm endpoint (:2375)</span></span>
    - <span data-ttu-id="6a5d2-244">Passare toohello *distribuire* cartella che è stato creato da hello precedenti attività di copia sicuro e che contiene i file di docker compose.yml hello</span><span class="sxs-lookup"><span data-stu-id="6a5d2-244">Navigate toohello *deploy* folder that was created by hello preceding secure copy task and that contains hello docker-compose.yml file</span></span> 
    - <span data-ttu-id="6a5d2-245">Eseguire `docker stack deploy` comandi pull nuove immagini hello e creare contenitori hello.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-245">Execute `docker stack deploy` commands that pull hello new images and create hello containers.</span></span>

    >[!IMPORTANT]
    > <span data-ttu-id="6a5d2-246">Come illustrato nella schermata precedente hello, lasciare hello **esito negativo in STDERR** casella di controllo deselezionata.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-246">As shown on hello previous screen, leave hello **Fail on STDERR** checkbox unchecked.</span></span> <span data-ttu-id="6a5d2-247">Questa impostazione consente toocomplete del processo di rilascio hello scadenza troppo`docker-compose` stampa i messaggi di diagnostica diversi, ad esempio i contenitori sono arresto o eliminato, nell'output di errore standard hello.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-247">This setting allows us toocomplete hello release process due too`docker-compose` prints several diagnostic messages, such as containers are stopping or being deleted, on hello standard error output.</span></span> <span data-ttu-id="6a5d2-248">Se si seleziona la casella di controllo di hello, Visual Studio Team Services indica che si sono verificati errori durante il rilascio di hello, anche se tutto va bene.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-248">If you check hello checkbox, Visual Studio Team Services reports that errors occurred during hello release, even if all goes well.</span></span>
    >
3. <span data-ttu-id="6a5d2-249">Salvare la nuova definizione di rilascio.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-249">Save this new release definition.</span></span>

## <a name="step-4-test-hello-cicd-pipeline"></a><span data-ttu-id="6a5d2-250">Passaggio 4: Testare pipeline CI/CD hello</span><span class="sxs-lookup"><span data-stu-id="6a5d2-250">Step 4: Test hello CI/CD pipeline</span></span>

<span data-ttu-id="6a5d2-251">Dopo avere con configurazione hello, è ora tootest questa nuova pipeline CI/CD-ROM.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-251">Now that you are done with hello configuration, it's time tootest this new CI/CD pipeline.</span></span> <span data-ttu-id="6a5d2-252">tootest modo più semplice Hello è tooupdate hello origine codice e il commit hello modifiche nel repository GitHub.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-252">hello easiest way tootest it is tooupdate hello source code and commit hello changes into your GitHub repository.</span></span> <span data-ttu-id="6a5d2-253">Pochi secondi dopo che si esegue il push codice hello, si noterà una nuova compilazione in esecuzione in Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-253">A few seconds after you push hello code, you will see a new build running in Visual Studio Team Services.</span></span> <span data-ttu-id="6a5d2-254">Una volta completata, una nuova versione viene attivata e distribuito una nuova versione di hello di un'applicazione hello in cluster del servizio di contenitore di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="6a5d2-254">Once completed successfully, a new release is triggered and deployed hello new version of hello application on hello Azure Container Service cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a5d2-255">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6a5d2-255">Next steps</span></span>

* <span data-ttu-id="6a5d2-256">Per ulteriori informazioni sull'elemento di configurazione/CD con Visual Studio Team Services, vedere hello [Panoramica di compilazione VSTS](https://www.visualstudio.com/docs/build/overview).</span><span class="sxs-lookup"><span data-stu-id="6a5d2-256">For more information about CI/CD with Visual Studio Team Services, see hello [VSTS Build overview](https://www.visualstudio.com/docs/build/overview).</span></span>
* <span data-ttu-id="6a5d2-257">Per ulteriori informazioni sul motore di ACS, vedere hello [repository GitHub motore ACS](https://github.com/Azure/acs-engine).</span><span class="sxs-lookup"><span data-stu-id="6a5d2-257">For more information about ACS Engine, see hello [ACS Engine GitHub repo](https://github.com/Azure/acs-engine).</span></span>
* <span data-ttu-id="6a5d2-258">Per ulteriori informazioni sulla modalità di Docker Swarm, vedere hello [Panoramica sulla modalità di Docker Swarm](https://docs.docker.com/engine/swarm/).</span><span class="sxs-lookup"><span data-stu-id="6a5d2-258">For more information about Docker Swarm mode, see hello [Docker Swarm mode overview](https://docs.docker.com/engine/swarm/).</span></span>
