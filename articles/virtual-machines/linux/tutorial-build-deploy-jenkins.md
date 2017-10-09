---
title: aaaCI/CD da Jenkins tooAzure le macchine virtuali con Team Services | Documenti Microsoft
description: Configurare l'integrazione continua (CI) e la distribuzione continua (CD) di un'app Node.js tramite Jenkins tooAzure VM da Release Management in Visual Studio Team Services (VSTS) o Microsoft Team Foundation Server (TFS)
author: ahomer
manager: douge
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/15/2017
ms.author: ahomer
ms.custom: mvc
ms.openlocfilehash: 400ae34cbdf45da65351811c0ff6ff5d61ef862c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-toolinux-vms-using-jenkins-and-team-services"></a><span data-ttu-id="7eca9-103">Distribuire le macchine virtuali di tooLinux app con Jenkins e Team Services</span><span class="sxs-lookup"><span data-stu-id="7eca9-103">Deploy your app tooLinux VMs using Jenkins and Team Services</span></span>

<span data-ttu-id="7eca9-104">Integrazione continua (CI) e distribuzione continua (CD) sono una pipeline con cui è possibile compilare, rilasciare e distribuire codice.</span><span class="sxs-lookup"><span data-stu-id="7eca9-104">Continuous integration (CI) and continuous deployment (CD) is a pipeline by which you can build, release, and deploy your code.</span></span> <span data-ttu-id="7eca9-105">Team Services fornisce un set completo, completo di strumenti di automazione CI/CD-ROM per tooAzure di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="7eca9-105">Team Services provides a complete, fully featured set of CI/CD automation tools for deployment tooAzure.</span></span> <span data-ttu-id="7eca9-106">Jenkins è uno strumento di terze parti diffuso basato su server per CI/CD che offre anche l'automazione CI/CD.</span><span class="sxs-lookup"><span data-stu-id="7eca9-106">Jenkins is a popular 3rd-party CI/CD server-based tool that also provides CI/CD automation.</span></span> <span data-ttu-id="7eca9-107">È possibile utilizzare entrambi toocustomize contemporaneamente la modalità di recapito di applicazione cloud o nel servizio.</span><span class="sxs-lookup"><span data-stu-id="7eca9-107">You can use both together toocustomize how you deliver your cloud app or service.</span></span>

<span data-ttu-id="7eca9-108">In questa esercitazione è utilizzare Jenkins toobuild un **app web Node. js**, toodeploy di Visual Studio Team Services e si tooa [gruppo distribuzione](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) contenente macchine virtuali Linux.</span><span class="sxs-lookup"><span data-stu-id="7eca9-108">In this tutorial, you use Jenkins toobuild a **Node.js web app**, and Visual Studio Team Services toodeploy it tooa [deployment group](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) containing Linux virtual machines.</span></span>

<span data-ttu-id="7eca9-109">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="7eca9-109">You will:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7eca9-110">Creare l'app in Jenkins</span><span class="sxs-lookup"><span data-stu-id="7eca9-110">Build your app in Jenkins</span></span>
> * <span data-ttu-id="7eca9-111">Configurare Jenkins per l'integrazione con Team Services</span><span class="sxs-lookup"><span data-stu-id="7eca9-111">Configure Jenkins for Team Services integration</span></span>
> * <span data-ttu-id="7eca9-112">Creare un gruppo di distribuzione per hello macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="7eca9-112">Create a deployment group for hello Azure virtual machines</span></span>
> * <span data-ttu-id="7eca9-113">Creare una definizione di versione che consente di configurare le macchine virtuali hello e distribuisce l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="7eca9-113">Create a release definition that configures hello VMs and deploys hello app</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7eca9-114">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="7eca9-114">Before you begin</span></span>

* <span data-ttu-id="7eca9-115">È necessario l'account di accesso tooa Jenkins.</span><span class="sxs-lookup"><span data-stu-id="7eca9-115">You need access tooa Jenkins account.</span></span> <span data-ttu-id="7eca9-116">Se non è ancora stato creato un server Jenkins, vedere la [documentazione di Jenkins](https://jenkins.io/doc/).</span><span class="sxs-lookup"><span data-stu-id="7eca9-116">If you have not yet created a Jenkins server, see [Jenkins Documentation](https://jenkins.io/doc/).</span></span> 

* <span data-ttu-id="7eca9-117">Accedi tooyour account Team Services (`https://{youraccount}.visualstudio.com`).</span><span class="sxs-lookup"><span data-stu-id="7eca9-117">Sign in tooyour Team Services account (`https://{youraccount}.visualstudio.com`).</span></span> 
  <span data-ttu-id="7eca9-118">È possibile ottenere un [account di Team Services gratuito](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).</span><span class="sxs-lookup"><span data-stu-id="7eca9-118">You can get a [free Team Services account](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).</span></span>

  > [!NOTE]
  > <span data-ttu-id="7eca9-119">Per ulteriori informazioni, vedere [connettere servizi tooTeam](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).</span><span class="sxs-lookup"><span data-stu-id="7eca9-119">For more information, see [Connect tooTeam Services](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).</span></span>

* <span data-ttu-id="7eca9-120">Se non si dispone di un token di accesso personale nell'account di Team Services, crearne uno.</span><span class="sxs-lookup"><span data-stu-id="7eca9-120">Create a personal access token (PAT) in your Team Services account if you don't already have one.</span></span> <span data-ttu-id="7eca9-121">Jenkins richiede questa tooaccess informazioni dell'account Team Services.</span><span class="sxs-lookup"><span data-stu-id="7eca9-121">Jenkins requires this information tooaccess your Team Services account.</span></span>
  <span data-ttu-id="7eca9-122">Lettura [come creare un token di accesso personale per Team Services e TFS](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) toolearn come toogenerate uno.</span><span class="sxs-lookup"><span data-stu-id="7eca9-122">Read [How do I create a personal access token for Team Services and TFS](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) toolearn how toogenerate one.</span></span>

## <a name="get-hello-sample-app"></a><span data-ttu-id="7eca9-123">Ottenere app di esempio hello</span><span class="sxs-lookup"><span data-stu-id="7eca9-123">Get hello sample app</span></span>

<span data-ttu-id="7eca9-124">È necessario un toodeploy app archiviati in un repository Git.</span><span class="sxs-lookup"><span data-stu-id="7eca9-124">You need an app toodeploy stored in a Git repository.</span></span>
<span data-ttu-id="7eca9-125">Per questa esercitazione, si consiglia di usare [questa app di esempio disponibile da GitHub](https://github.com/azooinmyluggage/fabrikam-node).</span><span class="sxs-lookup"><span data-stu-id="7eca9-125">For this tutorial, we recommend you use [this sample app available from GitHub](https://github.com/azooinmyluggage/fabrikam-node).</span></span>

1. <span data-ttu-id="7eca9-126">Creare un fork di questa app e prendere nota del percorso di hello (URL) per l'utilizzo nei passaggi successivi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="7eca9-126">Create a fork of this app and take note of hello location (URL) for use in later steps of this tutorial.</span></span>

1. <span data-ttu-id="7eca9-127">Rendere fork hello **pubblica** toosimplify connessione tooGitHub in seguito.</span><span class="sxs-lookup"><span data-stu-id="7eca9-127">Make hello fork **public** toosimplify connecting tooGitHub later.</span></span>

> [!NOTE]
> <span data-ttu-id="7eca9-128">Per ulteriori informazioni, vedere [Fork a repo](https://help.github.com/articles/fork-a-repo/) (Biforcazione di un repository) e [Making a private repository public](https://help.github.com/articles/making-a-private-repository-public/) (Rendere pubblico un repository privato).</span><span class="sxs-lookup"><span data-stu-id="7eca9-128">For more information, see [Fork a repo](https://help.github.com/articles/fork-a-repo/) and [Making a private repository public](https://help.github.com/articles/making-a-private-repository-public/).</span></span>

> [!NOTE]
> <span data-ttu-id="7eca9-129">app Hello è stato compilato utilizzando [Yeoman](http://yeoman.io/learning/index.html); Usa **Express**, **bower**, e **grunt**; e ha alcuni **npm**pacchetti come dipendenze.</span><span class="sxs-lookup"><span data-stu-id="7eca9-129">hello app was built using [Yeoman](http://yeoman.io/learning/index.html); it uses **Express**, **bower**, and **grunt**; and it has some **npm** packages as dependencies.</span></span>
> <span data-ttu-id="7eca9-130">app di esempio Hello contiene un set di [modelli di gestione risorse di Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) che vengono utilizzati toodynamically creare hello macchine virtuali per la distribuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="7eca9-130">hello sample app contains a set of [Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) that are used toodynamically create hello virtual machines for deployment on Azure.</span></span> <span data-ttu-id="7eca9-131">Questi modelli vengono utilizzati dalle attività di hello [definizione di versione di Team Services](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).</span><span class="sxs-lookup"><span data-stu-id="7eca9-131">These templates are used by tasks in hello [Team Services release definition](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).</span></span>
> <span data-ttu-id="7eca9-132">modello principale Hello consente di creare un gruppo di sicurezza di rete, una macchina virtuale e una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="7eca9-132">hello main template creates a network security group, a virtual machine, and a virtual network.</span></span> <span data-ttu-id="7eca9-133">Assegna un indirizzo IP pubblico e apre la porta 80 in ingresso.</span><span class="sxs-lookup"><span data-stu-id="7eca9-133">It assigns a public IP address and opens inbound port 80.</span></span> <span data-ttu-id="7eca9-134">Verrà inoltre aggiunto un tag che viene utilizzato dalla distribuzione di hello distribuzione gruppo hello troppo selezionare macchine tooreceive hello.</span><span class="sxs-lookup"><span data-stu-id="7eca9-134">It also adds a tag that is used by hello deployment group too select hello machines tooreceive hello deployment.</span></span>
>
> <span data-ttu-id="7eca9-135">esempio Hello contiene anche uno script che configura Nginx e distribuisce l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="7eca9-135">hello sample also contains a script that sets up Nginx and deploys hello app.</span></span> <span data-ttu-id="7eca9-136">Viene eseguita in ognuna delle macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="7eca9-136">It is executed on each of hello virtual machines.</span></span> <span data-ttu-id="7eca9-137">In particolare, script hello installa nodo, Nginx e PM2; Configura Nginx e PM2; Avvia quindi hello nodo app.</span><span class="sxs-lookup"><span data-stu-id="7eca9-137">Specifically, hello script installs Node, Nginx, and PM2; configures Nginx and PM2; then starts hello Node app.</span></span>

## <a name="configure-jenkins-plugins"></a><span data-ttu-id="7eca9-138">Configurare i plug-in di Jenkins</span><span class="sxs-lookup"><span data-stu-id="7eca9-138">Configure Jenkins plugins</span></span>

<span data-ttu-id="7eca9-139">In primo luogo è necessario configurare due plug-in di Jenkins per **NodeJS** e l'**integrazione con Team Services**.</span><span class="sxs-lookup"><span data-stu-id="7eca9-139">First, you must configure two Jenkins plugins for **NodeJS** and **Integration with Team Services**.</span></span>

1. <span data-ttu-id="7eca9-140">Aprire l'account di Jenkins e scegliere **Manage Jenkins** (Gestisci Jenkins).</span><span class="sxs-lookup"><span data-stu-id="7eca9-140">Open your Jenkins account and choose **Manage Jenkins**.</span></span>

1. <span data-ttu-id="7eca9-141">In hello **gestire Jenkins** pagina, scegliere **gestire plug-in**.</span><span class="sxs-lookup"><span data-stu-id="7eca9-141">In hello **Manage Jenkins** page, choose **Manage Plugins**.</span></span>

1. <span data-ttu-id="7eca9-142">Hello di filtro hello elenco toolocate **NodeJS** plug-in e l'installazione senza riavviare.</span><span class="sxs-lookup"><span data-stu-id="7eca9-142">Filter hello list toolocate hello **NodeJS** plugin and install it without restart.</span></span>

   ![Aggiunta di hello NodeJS plug-in tooJenkins](media/tutorial-build-deploy-jenkins/jenkins-nodejs-plugin.png)

1. <span data-ttu-id="7eca9-144">Hello di filtro hello elenco toofind **Team Foundation Server** plug-in e installarlo.</span><span class="sxs-lookup"><span data-stu-id="7eca9-144">Filter hello list toofind hello **Team Foundation Server** plugin and install it.</span></span> <span data-ttu-id="7eca9-145">(questo plug-in funziona sia con Team Services che con Team Foundation Server). Il riavvio di Jenkins non è necessario.</span><span class="sxs-lookup"><span data-stu-id="7eca9-145">(This plug-in works for both Team Services and Team Foundation Server.) Restarting Jenkins is not necessary.</span></span>

## <a name="configure-jenkins-build-for-nodejs"></a><span data-ttu-id="7eca9-146">Configurare la compilazione di Jenkins per Node.js</span><span class="sxs-lookup"><span data-stu-id="7eca9-146">Configure Jenkins build for Node.js</span></span>

<span data-ttu-id="7eca9-147">In Jenkins creare un nuovo progetto di compilazione e configurarlo come segue:</span><span class="sxs-lookup"><span data-stu-id="7eca9-147">In Jenkins, create a new build project and configure it as follows:</span></span>

1. <span data-ttu-id="7eca9-148">In hello **generale** , immettere un nome per il progetto di compilazione.</span><span class="sxs-lookup"><span data-stu-id="7eca9-148">In hello **General** tab, enter a name for your build project.</span></span>

1. <span data-ttu-id="7eca9-149">In hello **gestione del codice sorgente** , selezionare **Git** e immettere i dettagli di hello del repository di hello e ramo hello contenente il codice dell'app.</span><span class="sxs-lookup"><span data-stu-id="7eca9-149">In hello **Source Code Management** tab, select **Git** and enter hello details of hello repository and hello branch containing your app code.</span></span>

   ![Aggiungere una compilazione tooyour repository](media/tutorial-build-deploy-jenkins/jenkins-git.png)

   > [!NOTE]
   > <span data-ttu-id="7eca9-151">Se il repository non è pubblico, scegliere **Aggiungi** e fornire le credenziali tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="7eca9-151">If your repository is not public, choose **Add** and provide credentials tooconnect tooit.</span></span>

1. <span data-ttu-id="7eca9-152">In hello **trigger di compilazione** , selezionare **polling SCM** e immettere pianificazione hello `H/03 * * * *` repository Git di hello toopoll modifiche ogni tre minuti.</span><span class="sxs-lookup"><span data-stu-id="7eca9-152">In hello **Build Triggers** tab, select **Poll SCM** and enter hello schedule `H/03 * * * *` toopoll hello Git repository for changes every three minutes.</span></span> 

1. <span data-ttu-id="7eca9-153">In hello **ambiente Build** , selezionare **fornire nodo &amp; npm bin / percorso cartella** e immettere `NodeJS` per hello valore JS installazione del nodo.</span><span class="sxs-lookup"><span data-stu-id="7eca9-153">In hello **Build Environment** tab, select **Provide Node &amp; npm bin/ folder PATH** and enter `NodeJS` for hello Node JS Installation value.</span></span> <span data-ttu-id="7eca9-154">Lasciare **npmrc file** impostato su "use system default" (usa impostazioni predefinite di sistema).</span><span class="sxs-lookup"><span data-stu-id="7eca9-154">Leave **npmrc file** set to "use system default."</span></span>

1. <span data-ttu-id="7eca9-155">In hello **compilare** , immettere il comando hello `npm install` tooensure vengono aggiornate tutte le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="7eca9-155">In hello **Build** tab, enter hello command `npm install` tooensure all dependencies are updated.</span></span>

## <a name="configure-jenkins-for-team-services-integration"></a><span data-ttu-id="7eca9-156">Configurare Jenkins per l'integrazione con Team Services</span><span class="sxs-lookup"><span data-stu-id="7eca9-156">Configure Jenkins for Team Services integration</span></span>

1. <span data-ttu-id="7eca9-157">In hello **azioni post-compilazione** scheda per **file tooarchive**, immettere `**/*` tooinclude tutti i file.</span><span class="sxs-lookup"><span data-stu-id="7eca9-157">In hello **Post-build Actions** tab, for **Files tooarchive**, enter `**/*` tooinclude all files.</span></span>

1. <span data-ttu-id="7eca9-158">Per **attivare rilascio in TFS/Team Services**, immettere l'URL completo di hello del tuo account (ad esempio `https://your-account-name.visualstudio.com`), nome del progetto, un nome per la definizione di versione di hello (creato in un secondo momento), hello e hello account tooyour tooconnect di credenziali.</span><span class="sxs-lookup"><span data-stu-id="7eca9-158">For **Trigger release in TFS/Team Services**, enter hello full URL of your account (such as `https://your-account-name.visualstudio.com`), hello project name, a name for hello release definition (created later), and hello credentials tooconnect tooyour account.</span></span>
   <span data-ttu-id="7eca9-159">È necessario il nome utente e hello PAT creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="7eca9-159">You need your user name and hello PAT you created earlier.</span></span> 

   ![Configurazione delle azioni di post-compilazione in Jenkins](media/tutorial-build-deploy-jenkins/trigger-release-from-jenkins.png)

1. <span data-ttu-id="7eca9-161">Salvare il progetto di compilazione hello.</span><span class="sxs-lookup"><span data-stu-id="7eca9-161">Save hello build project.</span></span>

## <a name="create-a-jenkins-service-endpoint"></a><span data-ttu-id="7eca9-162">Creare un endpoint servizio di Jenkins</span><span class="sxs-lookup"><span data-stu-id="7eca9-162">Create a Jenkins service endpoint</span></span>

<span data-ttu-id="7eca9-163">Un endpoint del servizio consente tooJenkins tooconnect Team Services.</span><span class="sxs-lookup"><span data-stu-id="7eca9-163">A service endpoint allows Team Services tooconnect tooJenkins.</span></span>

1. <span data-ttu-id="7eca9-164">Aprire hello **servizi** pagina Team Services, aprire hello **nuovo Endpoint del servizio** elenco e scegliere **Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="7eca9-164">Open hello **Services** page in Team Services, open hello **New Service Endpoint** list, and choose **Jenkins**.</span></span>

   ![Aggiungere un endpoint di Jenkins](media/tutorial-build-deploy-jenkins/add-jenkins-endpoint.png)

1. <span data-ttu-id="7eca9-166">Immettere un nome che verrà utilizzato toorefer toothis connessione.</span><span class="sxs-lookup"><span data-stu-id="7eca9-166">Enter a name you will use toorefer toothis connection.</span></span>

1. <span data-ttu-id="7eca9-167">Immettere l'URL di hello del server Jenkins e segni di graduazione hello **accettare certificati SSL non attendibili** opzione.</span><span class="sxs-lookup"><span data-stu-id="7eca9-167">Enter hello URL of your Jenkins server, and tick hello **Accept untrusted SSL certificates** option.</span></span>

1. <span data-ttu-id="7eca9-168">Immettere nome utente hello e una password per l'account di Jenkins.</span><span class="sxs-lookup"><span data-stu-id="7eca9-168">Enter hello user name and password for your Jenkins account.</span></span>

1. <span data-ttu-id="7eca9-169">Scegliere **verificare connessione** toocheck che hello informazioni sia corretto.</span><span class="sxs-lookup"><span data-stu-id="7eca9-169">Choose **Verify connection** toocheck that hello information is correct.</span></span>

1. <span data-ttu-id="7eca9-170">Scegliere **OK** endpoint del servizio toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="7eca9-170">Choose **OK** toocreate hello service endpoint.</span></span>

## <a name="create-a-deployment-group"></a><span data-ttu-id="7eca9-171">Creare un gruppo di distribuzione</span><span class="sxs-lookup"><span data-stu-id="7eca9-171">Create a deployment group</span></span>

<span data-ttu-id="7eca9-172">È necessario un [gruppo distribuzione](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) troppo contengono le macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="7eca9-172">You need a [deployment group](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) too contain hello virtual machines.</span></span>

1. <span data-ttu-id="7eca9-173">Aprire hello **versioni** scheda di hello **compilare &amp; versione** hub, quindi aprire hello **gruppi di distribuzione** scheda e scegliere **+ nuovo**.</span><span class="sxs-lookup"><span data-stu-id="7eca9-173">Open hello **Releases** tab of hello **Build &amp; Release** hub, then open hello **Deployment groups** tab, and choose **+ New**.</span></span>

1. <span data-ttu-id="7eca9-174">Immettere un nome per il gruppo di distribuzione hello e una descrizione facoltativa.</span><span class="sxs-lookup"><span data-stu-id="7eca9-174">Enter a name for hello deployment group, and an optional description.</span></span>
   <span data-ttu-id="7eca9-175">quindi scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="7eca9-175">Then choose **Create**.</span></span>

<span data-ttu-id="7eca9-176">attività di distribuzione di gruppo di risorse di Azure Hello crea e registra le macchine virtuali hello quando viene eseguita utilizzando il modello di gestione risorse di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="7eca9-176">hello Azure Resource Group Deployment task creates and registers hello VMs when it runs using hello Azure Resource Manager template.</span></span>
<span data-ttu-id="7eca9-177">Non necessari toocreate e registrare le macchine virtuali hello manualmente.</span><span class="sxs-lookup"><span data-stu-id="7eca9-177">You don't need toocreate and register hello virtual machines yourself.</span></span>

## <a name="create-a-release-definition"></a><span data-ttu-id="7eca9-178">Creare una definizione di versione</span><span class="sxs-lookup"><span data-stu-id="7eca9-178">Create a release definition</span></span>

<span data-ttu-id="7eca9-179">Definizione di una versione specifica eseguirà l'applicazione hello toodeploy processo hello Team Services.</span><span class="sxs-lookup"><span data-stu-id="7eca9-179">A release definition specifies hello process Team Services will execute toodeploy hello app.</span></span>
<span data-ttu-id="7eca9-180">definizione di versione toocreate hello in Team Services:</span><span class="sxs-lookup"><span data-stu-id="7eca9-180">toocreate hello release definition in Team Services:</span></span>

1. <span data-ttu-id="7eca9-181">Aprire hello **versioni** scheda di hello **compilare &amp; versione** hub, aprire hello  **+**  giù nell'elenco di hello di definizioni di versione e scegliere Hello **Crea definizione di versione**.</span><span class="sxs-lookup"><span data-stu-id="7eca9-181">Open hello **Releases** tab of hello **Build &amp; Release** hub, open hello **+** drop-down in hello list of release definitions, and choose hello **Create release definition**.</span></span> 

1. <span data-ttu-id="7eca9-182">Seleziona hello **vuoto** modello e scegliere **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="7eca9-182">Select hello **Empty** template and choose **Next**.</span></span>

1. <span data-ttu-id="7eca9-183">In hello **elementi** sezione, fare clic su **collegare un elemento** e scegliere **Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="7eca9-183">In hello **Artifacts** section, click on **Link an Artifact** and choose **Jenkins**.</span></span> <span data-ttu-id="7eca9-184">Selezionare la connessione all'endpoint servizio Jenkins,</span><span class="sxs-lookup"><span data-stu-id="7eca9-184">Select your Jenkins service endpoint connection.</span></span> <span data-ttu-id="7eca9-185">Quindi selezionare hello Jenkins origine processo e scegliere **crea**.</span><span class="sxs-lookup"><span data-stu-id="7eca9-185">Then select hello Jenkins source job and choose **Create**.</span></span> 

1. <span data-ttu-id="7eca9-186">In hello nuova definizione di versione, scegliere **+ Aggiungi attività** e aggiungere un **distribuzione gruppo di risorse di Azure** ambiente predefinito toohello di attività.</span><span class="sxs-lookup"><span data-stu-id="7eca9-186">In hello new release definition, choose **+ Add tasks** and add an **Azure Resource Group Deployment** task toohello default environment.</span></span>

1. <span data-ttu-id="7eca9-187">Scegliere toohello avanti sulla freccia a discesa hello **+ Aggiungi attività** collegare e aggiungere una definizione di toohello fase di distribuzione gruppo.</span><span class="sxs-lookup"><span data-stu-id="7eca9-187">Choose hello drop down arrow next toohello **+ Add tasks** link and add a deployment group phase toohello definition.</span></span>

   ![Aggiunta di una fase di gruppo di distribuzione](media/tutorial-build-deploy-jenkins/deployment-group-phase-in-release-definition.png) 

1. <span data-ttu-id="7eca9-189">Nel catalogo di attività hello, aprire hello **utilità** sezione e aggiungere un'istanza di hello **Script della Shell** attività.</span><span class="sxs-lookup"><span data-stu-id="7eca9-189">In hello Task catalog, open hello **Utility** section and add an instance of hello **Shell Script** task.</span></span>

1. <span data-ttu-id="7eca9-190">set di modelli di parametri di Hello utilizzato nell'attività di distribuzione di gruppo di risorse di Azure hello hello admin password utilizzata tooconnect toohello macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="7eca9-190">hello parameters template used in hello Azure Resource Group Deployment task sets hello admin password used tooconnect toohello VMs.</span></span>
   <span data-ttu-id="7eca9-191">Fornire la password con variabile hello **$(adminpassword)**:</span><span class="sxs-lookup"><span data-stu-id="7eca9-191">You provide this password with hello variable **$(adminpassword)**:</span></span>
   
   - <span data-ttu-id="7eca9-192">Aprire hello **variabili** scheda e hello **variabili** sezione, immettere il nome di hello `adminpassword`.</span><span class="sxs-lookup"><span data-stu-id="7eca9-192">Open hello **Variables** tab and, in hello **Variables** section, enter hello name `adminpassword`.</span></span>

   - <span data-ttu-id="7eca9-193">Immettere la password dell'amministratore di hello.</span><span class="sxs-lookup"><span data-stu-id="7eca9-193">Enter hello administrator password.</span></span>

   - <span data-ttu-id="7eca9-194">Scegliere hello "lucchetto" icona Avanti toohello valore textbox tooprotect hello password.</span><span class="sxs-lookup"><span data-stu-id="7eca9-194">Choose hello "padlock" icon next toohello value textbox tooprotect hello password.</span></span> 

## <a name="configure-hello-azure-resource-group-deployment-task"></a><span data-ttu-id="7eca9-195">Configurare l'attività di distribuzione di gruppo di risorse di Azure hello</span><span class="sxs-lookup"><span data-stu-id="7eca9-195">Configure hello Azure Resource Group Deployment task</span></span>

<span data-ttu-id="7eca9-196">Hello **distribuzione gruppo di risorse di Azure** attività è gruppo di distribuzione utilizzato toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="7eca9-196">hello **Azure Resource Group Deployment** task is used toocreate hello deployment group.</span></span> <span data-ttu-id="7eca9-197">Configurare l'app come segue:</span><span class="sxs-lookup"><span data-stu-id="7eca9-197">Configure it as follows:</span></span>

* <span data-ttu-id="7eca9-198">**Sottoscrizione di Azure:** selezionare una connessione dall'elenco di hello in **connessioni del servizio di Azure disponibili**.</span><span class="sxs-lookup"><span data-stu-id="7eca9-198">**Azure Subscription:** Select a connection from hello list under **Available Azure Service Connections**.</span></span> 
  <span data-ttu-id="7eca9-199">Se viene visualizzata alcuna connessione, scegliere **Gestisci**selezionare **nuovo Endpoint del servizio** quindi **Azure Resource Manager**e seguire le istruzioni di hello.</span><span class="sxs-lookup"><span data-stu-id="7eca9-199">If no connections appear, choose **Manage**, select **New Service Endpoint** then **Azure Resource Manager**, and follow hello prompts.</span></span>
  <span data-ttu-id="7eca9-200">Restituire la definizione di tipo versione tooyour, hello aggiornamento **sottoscrizione di Azure Resource Manager** elenco hello selezionare la connessione e creato.</span><span class="sxs-lookup"><span data-stu-id="7eca9-200">Return tooyour release definition, refresh hello **AzureRM Subscription** list, and select hello connection you created.</span></span>

* <span data-ttu-id="7eca9-201">**Gruppo di risorse**: immettere un nome del gruppo di risorse hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="7eca9-201">**Resource group**: Enter a name of hello resource group you created earlier.</span></span>

* <span data-ttu-id="7eca9-202">**Percorso**: selezionare un'area per la distribuzione di hello.</span><span class="sxs-lookup"><span data-stu-id="7eca9-202">**Location**: Select a region for hello deployment.</span></span>

  ![Creare un nuovo gruppo di risorse](media/tutorial-build-deploy-jenkins/provision-web-server.png)

* <span data-ttu-id="7eca9-204">**Percorso del modelli**:`URL of hello file`</span><span class="sxs-lookup"><span data-stu-id="7eca9-204">**Template location**: `URL of hello file`</span></span>

* <span data-ttu-id="7eca9-205">**Collegamento al modello**:`{your-git-repo}/ARM-Templates/UbuntuWeb1.json`</span><span class="sxs-lookup"><span data-stu-id="7eca9-205">**Template link**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.json`</span></span>

* <span data-ttu-id="7eca9-206">**Collegamento ai parametri del modello**:`{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`</span><span class="sxs-lookup"><span data-stu-id="7eca9-206">**Template parameters link**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`</span></span>

* <span data-ttu-id="7eca9-207">**Eseguire l'override di parametri di modello**: un elenco di hello eseguire l'override di valori, ad esempio: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.</span><span class="sxs-lookup"><span data-stu-id="7eca9-207">**Override template parameters**: A list of hello override values, for example: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.</span></span><br /><span data-ttu-id="7eca9-208">Inserire i propri valori specifici per hello {segnaposto}.</span><span class="sxs-lookup"><span data-stu-id="7eca9-208">Insert your own specific values for hello {placeholders}.</span></span> 

* <span data-ttu-id="7eca9-209">**Abilita i prerequisiti**: `Configure with Deployment Group agent`</span><span class="sxs-lookup"><span data-stu-id="7eca9-209">**Enable prerequisites**: `Configure with Deployment Group agent`</span></span>

* <span data-ttu-id="7eca9-210">**Endpoint TFS/VSTS**: scegliere **Aggiungi** e, nella finestra di dialogo "Aggiungi nuova connessione a servizi/Team Server Team Foundation" hello, selezionare **autenticazione basata su Token**.</span><span class="sxs-lookup"><span data-stu-id="7eca9-210">**TFS/VSTS endpoint**: Choose **Add** and, in hello "Add new Team Foundation Server/Team Services Connection" dialog, select **Token Based Authentication**.</span></span> <span data-ttu-id="7eca9-211">Immettere un nome di connessione hello e l'URL di hello del progetto team.</span><span class="sxs-lookup"><span data-stu-id="7eca9-211">Enter a name of hello connection and hello URL of your team project.</span></span> <span data-ttu-id="7eca9-212">Quindi generare e immettere un [Personal Access Token (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) il progetto team tooyour di tooauthenticate hello connessione.</span><span class="sxs-lookup"><span data-stu-id="7eca9-212">Then generate and enter a [Personal Access Token (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) tooauthenticate hello connection tooyour team project.</span></span>

  ![Creare un token di accesso personale](media/tutorial-build-deploy-jenkins/create-a-pat.png)

* <span data-ttu-id="7eca9-214">**Progetto team**: selezionare il progetto corrente.</span><span class="sxs-lookup"><span data-stu-id="7eca9-214">**Team project**: Select your current project.</span></span>

* <span data-ttu-id="7eca9-215">**Gruppo di distribuzione**: immettere hello stesso nome del gruppo di distribuzione che si utilizzi per hello **gruppo di risorse** parametro.</span><span class="sxs-lookup"><span data-stu-id="7eca9-215">**Deployment Group**: Enter hello same deployment group name as you used for hello **Resource group** parameter.</span></span>

<span data-ttu-id="7eca9-216">le impostazioni predefinite di Hello per attività di distribuzione di gruppo di risorse di Azure hello sono toocreate o aggiorneranno una risorsa e toodo in modo incrementale.</span><span class="sxs-lookup"><span data-stu-id="7eca9-216">hello default settings for hello Azure Resource Group Deployment task are toocreate or update a resource, and toodo so incrementally.</span></span> <span data-ttu-id="7eca9-217">attività Hello crea hello macchine virtuali hello prima volta che viene eseguito e successivamente semplicemente aggiornarli.</span><span class="sxs-lookup"><span data-stu-id="7eca9-217">hello task creates hello VMs hello first time it runs, and subsequently just update them.</span></span>

## <a name="configure-hello-shell-script-task"></a><span data-ttu-id="7eca9-218">Configurare l'attività Script della Shell hello</span><span class="sxs-lookup"><span data-stu-id="7eca9-218">Configure hello Shell Script task</span></span>

<span data-ttu-id="7eca9-219">Hello **Script della Shell** attività è una configurazione di hello tooprovide utilizzati per un toorun di script in ogni server tooinstall Node.js e avviare hello App Windows.</span><span class="sxs-lookup"><span data-stu-id="7eca9-219">hello **Shell Script** task is used tooprovide hello configuration for a script toorun on each server tooinstall Node.js and start hello app.</span></span> <span data-ttu-id="7eca9-220">Configurare l'app come segue:</span><span class="sxs-lookup"><span data-stu-id="7eca9-220">Configure it as follows:</span></span>

* <span data-ttu-id="7eca9-221">**Percorso script**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`</span><span class="sxs-lookup"><span data-stu-id="7eca9-221">**Script Path**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`</span></span>

* <span data-ttu-id="7eca9-222">**Specifica directory di lavoro**: `Checked`</span><span class="sxs-lookup"><span data-stu-id="7eca9-222">**Specify Working Directory**: `Checked`</span></span>

* <span data-ttu-id="7eca9-223">**Directory di lavoro**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node`</span><span class="sxs-lookup"><span data-stu-id="7eca9-223">**Working Directory**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node`</span></span>
   
## <a name="rename-and-save-hello-release-definition"></a><span data-ttu-id="7eca9-224">Rinominare e salvare la definizione di versione hello</span><span class="sxs-lookup"><span data-stu-id="7eca9-224">Rename and save hello release definition</span></span>

1. <span data-ttu-id="7eca9-225">Modificare il nome di hello del nome di hello versione definizione toohello specificato nel **azioni post-compilazione** scheda della compilazione hello in Jenkins.</span><span class="sxs-lookup"><span data-stu-id="7eca9-225">Edit hello name of hello release definition toohello name you specified in the **Post-build Actions** tab of hello build in Jenkins.</span></span> <span data-ttu-id="7eca9-226">Quando vengono aggiornati gli elementi di origine hello, Jenkins richiede questo nome toobe in grado di tootrigger una nuova versione.</span><span class="sxs-lookup"><span data-stu-id="7eca9-226">Jenkins requires this name toobe able tootrigger a new release when hello source artifacts are updated.</span></span>

1. <span data-ttu-id="7eca9-227">Facoltativamente, modificare il nome di hello dell'ambiente di hello facendo clic sul nome hello.</span><span class="sxs-lookup"><span data-stu-id="7eca9-227">Optionally, change hello name of hello environment by clicking on hello name.</span></span> 

1. <span data-ttu-id="7eca9-228">Scegliere **Salva** e quindi **OK**.</span><span class="sxs-lookup"><span data-stu-id="7eca9-228">Choose **Save**, and choose **OK**.</span></span>

## <a name="start-a-manual-deployment"></a><span data-ttu-id="7eca9-229">Avviare una distribuzione manuale</span><span class="sxs-lookup"><span data-stu-id="7eca9-229">Start a manual deployment</span></span>

1. <span data-ttu-id="7eca9-230">Scegliere **+ Versione** e selezionare **Crea versione**.</span><span class="sxs-lookup"><span data-stu-id="7eca9-230">Choose **+ Release** and select **Create Release**.</span></span>

1. <span data-ttu-id="7eca9-231">Selezionare una compilazione hello è completato nell'elenco a discesa evidenziato hello e scegliere **crea**.</span><span class="sxs-lookup"><span data-stu-id="7eca9-231">Select hello build you completed in hello highlighted drop-down list and choose **Create**.</span></span>

1. <span data-ttu-id="7eca9-232">Scegliere il collegamento di rilascio hello nel messaggio popup di hello.</span><span class="sxs-lookup"><span data-stu-id="7eca9-232">Choose hello release link in hello popup message.</span></span> <span data-ttu-id="7eca9-233">Ad esempio: "Versione **Versione-1** creata."</span><span class="sxs-lookup"><span data-stu-id="7eca9-233">For example: "Release **Release-1** has been created."</span></span>

1. <span data-ttu-id="7eca9-234">Aprire hello **registri** scheda output della console toowatch hello versione.</span><span class="sxs-lookup"><span data-stu-id="7eca9-234">Open hello **Logs** tab toowatch hello release console output.</span></span>

1. <span data-ttu-id="7eca9-235">Nel browser aprire hello URL di uno dei server hello è stato aggiunto il gruppo di distribuzione tooyour.</span><span class="sxs-lookup"><span data-stu-id="7eca9-235">In your browser, open hello URL of one of hello servers you added tooyour deployment group.</span></span> <span data-ttu-id="7eca9-236">Ad esempio, immettere `http://{your-server-ip-address}`</span><span class="sxs-lookup"><span data-stu-id="7eca9-236">For example, enter `http://{your-server-ip-address}`</span></span>

## <a name="start-a-cicd-deployment"></a><span data-ttu-id="7eca9-237">Avviare una distribuzione CI/CD</span><span class="sxs-lookup"><span data-stu-id="7eca9-237">Start a CI/CD deployment</span></span>

1. <span data-ttu-id="7eca9-238">Definizione di versione di hello, deselezionare hello **abilitato** casella di controllo in hello **le opzioni di controllo** sezione delle impostazioni di hello per attività di distribuzione di gruppo di risorse di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="7eca9-238">In hello release definition, uncheck hello **Enabled** checkbox in hello **Control Options** section of hello settings for hello Azure Resource Group Deployment task.</span></span>
   <span data-ttu-id="7eca9-239">Per le distribuzioni future toohello distribuzione gruppo di esistente, non è necessario toore-eseguire questa attività.</span><span class="sxs-lookup"><span data-stu-id="7eca9-239">For future deployments toohello existing deployment group, you do not need toore-execute this task.</span></span>

1. <span data-ttu-id="7eca9-240">Passare repository Git di origine toohello e modificare contenuto hello di hello **h1** intestazione nel file hello [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).</span><span class="sxs-lookup"><span data-stu-id="7eca9-240">Go toohello source Git repository and modify hello contents of hello **h1** heading in hello file [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).</span></span>

1. <span data-ttu-id="7eca9-241">Eseguire il commit delle modifiche.</span><span class="sxs-lookup"><span data-stu-id="7eca9-241">Commit your change.</span></span>

1. <span data-ttu-id="7eca9-242">Dopo alcuni minuti, si noterà una nuova versione creata in hello **versioni** pagina di Team Services o TFS.</span><span class="sxs-lookup"><span data-stu-id="7eca9-242">After a few minutes, you will see a new release created in hello **Releases** page of Team Services or TFS.</span></span> <span data-ttu-id="7eca9-243">Aprire hello versione toosee hello distribuzione in corso.</span><span class="sxs-lookup"><span data-stu-id="7eca9-243">Open hello release toosee hello deployment taking place.</span></span> <span data-ttu-id="7eca9-244">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="7eca9-244">Congratulations!</span></span>

## <a name="next-steps"></a><span data-ttu-id="7eca9-245">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7eca9-245">Next Steps</span></span>

<span data-ttu-id="7eca9-246">In questa esercitazione si automatizzata hello di tooAzure un'app tramite servizi di Team per il rilascio e di compilazione Jenkins.</span><span class="sxs-lookup"><span data-stu-id="7eca9-246">In this tutorial, you automated hello deployment of an app tooAzure using Jenkins build and Team Services for release.</span></span> <span data-ttu-id="7eca9-247">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="7eca9-247">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7eca9-248">Creare l'app in Jenkins</span><span class="sxs-lookup"><span data-stu-id="7eca9-248">Build your app in Jenkins</span></span>
> * <span data-ttu-id="7eca9-249">Configurare Jenkins per l'integrazione con Team Services</span><span class="sxs-lookup"><span data-stu-id="7eca9-249">Configure Jenkins for Team Services integration</span></span>
> * <span data-ttu-id="7eca9-250">Creare un gruppo di distribuzione per hello macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="7eca9-250">Create a deployment group for hello Azure virtual machines</span></span>
> * <span data-ttu-id="7eca9-251">Creare una definizione di versione che consente di configurare le macchine virtuali hello e distribuisce l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="7eca9-251">Create a release definition that configures hello VMs and deploys hello app</span></span>

<span data-ttu-id="7eca9-252">Spostare toolearn esercitazione successiva toohello ulteriori informazioni su come dello stack toodeploy una luce (Linux Apache, MySQL e PHP).</span><span class="sxs-lookup"><span data-stu-id="7eca9-252">Advance toohello next tutorial toolearn more about how toodeploy a LAMP (Linux, Apache, MySQL, and PHP) stack.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7eca9-253">Distribuire lo stack LAMP</span><span class="sxs-lookup"><span data-stu-id="7eca9-253">Deploy LAMP stack</span></span>](tutorial-lamp-stack.md)