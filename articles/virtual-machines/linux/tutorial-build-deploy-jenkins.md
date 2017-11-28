---
title: CI/CD da Jenkins in macchine virtuali di Azure con Team Services | Microsoft Docs
description: Configurare l'integrazione continua (CI) e la distribuzione continua (CD) di un'app Node.js usando Jenkins in macchine virtuali di Azure da Release Management in Visual Studio Team Services (VSTS) o Microsoft Team Foundation Server (TFS)
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
ms.openlocfilehash: a40e26a8681df31fad664e4d1df4c1513311900d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-your-app-to-linux-vms-using-jenkins-and-team-services"></a><span data-ttu-id="4fb3c-103">Distribuire l'app in macchine virtuali Linux usando Jenkins e Team Services</span><span class="sxs-lookup"><span data-stu-id="4fb3c-103">Deploy your app to Linux VMs using Jenkins and Team Services</span></span>

<span data-ttu-id="4fb3c-104">Integrazione continua (CI) e distribuzione continua (CD) sono una pipeline con cui è possibile compilare, rilasciare e distribuire codice.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-104">Continuous integration (CI) and continuous deployment (CD) is a pipeline by which you can build, release, and deploy your code.</span></span> <span data-ttu-id="4fb3c-105">Team Services offre un set di strumenti di automazione CI/CD completo per la distribuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-105">Team Services provides a complete, fully featured set of CI/CD automation tools for deployment to Azure.</span></span> <span data-ttu-id="4fb3c-106">Jenkins è uno strumento di terze parti diffuso basato su server per CI/CD che offre anche l'automazione CI/CD.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-106">Jenkins is a popular 3rd-party CI/CD server-based tool that also provides CI/CD automation.</span></span> <span data-ttu-id="4fb3c-107">È possibile usare insieme entrambi gli strumenti per personalizzare la fornitura dell'app o del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-107">You can use both together to customize how you deliver your cloud app or service.</span></span>

<span data-ttu-id="4fb3c-108">In questa esercitazione si userà Jenkins per creare un'**app Web Node.js** e Visual Studio Team Services per distribuirla in un [gruppo di distribuzione](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) contenente macchine virtuali Linux.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-108">In this tutorial, you use Jenkins to build a **Node.js web app**, and Visual Studio Team Services to deploy it to a [deployment group](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) containing Linux virtual machines.</span></span>

<span data-ttu-id="4fb3c-109">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="4fb3c-109">You will:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4fb3c-110">Creare l'app in Jenkins</span><span class="sxs-lookup"><span data-stu-id="4fb3c-110">Build your app in Jenkins</span></span>
> * <span data-ttu-id="4fb3c-111">Configurare Jenkins per l'integrazione con Team Services</span><span class="sxs-lookup"><span data-stu-id="4fb3c-111">Configure Jenkins for Team Services integration</span></span>
> * <span data-ttu-id="4fb3c-112">Creare un gruppo di distribuzione per le macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="4fb3c-112">Create a deployment group for the Azure virtual machines</span></span>
> * <span data-ttu-id="4fb3c-113">Creare una definizione di versione che configuri le macchine virtuali e distribuisca l'app</span><span class="sxs-lookup"><span data-stu-id="4fb3c-113">Create a release definition that configures the VMs and deploys the app</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4fb3c-114">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="4fb3c-114">Before you begin</span></span>

* <span data-ttu-id="4fb3c-115">È necessario l'accesso a un account Jenkins.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-115">You need access to a Jenkins account.</span></span> <span data-ttu-id="4fb3c-116">Se non è ancora stato creato un server Jenkins, vedere la [documentazione di Jenkins](https://jenkins.io/doc/).</span><span class="sxs-lookup"><span data-stu-id="4fb3c-116">If you have not yet created a Jenkins server, see [Jenkins Documentation](https://jenkins.io/doc/).</span></span> 

* <span data-ttu-id="4fb3c-117">Accedere al proprio account di Team Services (`https://{youraccount}.visualstudio.com`).</span><span class="sxs-lookup"><span data-stu-id="4fb3c-117">Sign in to your Team Services account (`https://{youraccount}.visualstudio.com`).</span></span> 
  <span data-ttu-id="4fb3c-118">È possibile ottenere un [account di Team Services gratuito](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).</span><span class="sxs-lookup"><span data-stu-id="4fb3c-118">You can get a [free Team Services account](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).</span></span>

  > [!NOTE]
  > <span data-ttu-id="4fb3c-119">Per altre informazioni, vedere [Connettersi a Team Services](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).</span><span class="sxs-lookup"><span data-stu-id="4fb3c-119">For more information, see [Connect to Team Services](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).</span></span>

* <span data-ttu-id="4fb3c-120">Se non si dispone di un token di accesso personale nell'account di Team Services, crearne uno.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-120">Create a personal access token (PAT) in your Team Services account if you don't already have one.</span></span> <span data-ttu-id="4fb3c-121">Jenkins richiede questa informazione per accedere all'account di Team Services.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-121">Jenkins requires this information to access your Team Services account.</span></span>
  <span data-ttu-id="4fb3c-122">Leggere [Come creare un token di accesso personale per Team Services e TFS](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) per informazioni su come generarne uno.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-122">Read [How do I create a personal access token for Team Services and TFS](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) to learn how to generate one.</span></span>

## <a name="get-the-sample-app"></a><span data-ttu-id="4fb3c-123">Ottenere l'app di esempio</span><span class="sxs-lookup"><span data-stu-id="4fb3c-123">Get the sample app</span></span>

<span data-ttu-id="4fb3c-124">È necessario disporre di un'app da distribuire archiviata in un repository Git.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-124">You need an app to deploy stored in a Git repository.</span></span>
<span data-ttu-id="4fb3c-125">Per questa esercitazione, si consiglia di usare [questa app di esempio disponibile da GitHub](https://github.com/azooinmyluggage/fabrikam-node).</span><span class="sxs-lookup"><span data-stu-id="4fb3c-125">For this tutorial, we recommend you use [this sample app available from GitHub](https://github.com/azooinmyluggage/fabrikam-node).</span></span>

1. <span data-ttu-id="4fb3c-126">Creare un fork di questa app e prendere nota del percorso (URL) per l'uso nei passaggi successivi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-126">Create a fork of this app and take note of the location (URL) for use in later steps of this tutorial.</span></span>

1. <span data-ttu-id="4fb3c-127">Rendere il fork **pubblico** per semplificare la connessione a GitHub in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-127">Make the fork **public** to simplify connecting to GitHub later.</span></span>

> [!NOTE]
> <span data-ttu-id="4fb3c-128">Per ulteriori informazioni, vedere [Fork a repo](https://help.github.com/articles/fork-a-repo/) (Biforcazione di un repository) e [Making a private repository public](https://help.github.com/articles/making-a-private-repository-public/) (Rendere pubblico un repository privato).</span><span class="sxs-lookup"><span data-stu-id="4fb3c-128">For more information, see [Fork a repo](https://help.github.com/articles/fork-a-repo/) and [Making a private repository public](https://help.github.com/articles/making-a-private-repository-public/).</span></span>

> [!NOTE]
> <span data-ttu-id="4fb3c-129">L'app è stata creata con [Yeoman](http://yeoman.io/learning/index.html), usa **Express**, **Bower** e **Grunt**, e ha alcuni pacchetti **npm** come dipendenze.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-129">The app was built using [Yeoman](http://yeoman.io/learning/index.html); it uses **Express**, **bower**, and **grunt**; and it has some **npm** packages as dependencies.</span></span>
> <span data-ttu-id="4fb3c-130">L'app di esempio contiene un set di [modelli di Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) usati per creare in modo dinamico le macchine virtuali per la distribuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-130">The sample app contains a set of [Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) that are used to dynamically create the virtual machines for deployment on Azure.</span></span> <span data-ttu-id="4fb3c-131">Questi modelli vengono usati dalle attività nella [definizione di versione di Team Services](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).</span><span class="sxs-lookup"><span data-stu-id="4fb3c-131">These templates are used by tasks in the [Team Services release definition](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).</span></span>
> <span data-ttu-id="4fb3c-132">Il modello principale crea un gruppo di sicurezza di rete, una macchina virtuale e una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-132">The main template creates a network security group, a virtual machine, and a virtual network.</span></span> <span data-ttu-id="4fb3c-133">Assegna un indirizzo IP pubblico e apre la porta 80 in ingresso.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-133">It assigns a public IP address and opens inbound port 80.</span></span> <span data-ttu-id="4fb3c-134">Aggiunge anche un tag che viene usato dal gruppo di distribuzione per selezionare le macchine virtuali che ricevono la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-134">It also adds a tag that is used by the deployment group to select the machines to receive the deployment.</span></span>
>
> <span data-ttu-id="4fb3c-135">L'esempio contiene anche uno script che configura Nginx e distribuisce l'app.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-135">The sample also contains a script that sets up Nginx and deploys the app.</span></span> <span data-ttu-id="4fb3c-136">Viene eseguito su tutte le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-136">It is executed on each of the virtual machines.</span></span> <span data-ttu-id="4fb3c-137">In particolare, lo script installa Noe, Nginx e PM2, configura Nginx e PM2 e quindi avvia l'app Node.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-137">Specifically, the script installs Node, Nginx, and PM2; configures Nginx and PM2; then starts the Node app.</span></span>

## <a name="configure-jenkins-plugins"></a><span data-ttu-id="4fb3c-138">Configurare i plug-in di Jenkins</span><span class="sxs-lookup"><span data-stu-id="4fb3c-138">Configure Jenkins plugins</span></span>

<span data-ttu-id="4fb3c-139">In primo luogo è necessario configurare due plug-in di Jenkins per **NodeJS** e l'**integrazione con Team Services**.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-139">First, you must configure two Jenkins plugins for **NodeJS** and **Integration with Team Services**.</span></span>

1. <span data-ttu-id="4fb3c-140">Aprire l'account di Jenkins e scegliere **Manage Jenkins** (Gestisci Jenkins).</span><span class="sxs-lookup"><span data-stu-id="4fb3c-140">Open your Jenkins account and choose **Manage Jenkins**.</span></span>

1. <span data-ttu-id="4fb3c-141">Nella pagina **Manage Jenkins** fare clic su **Manage Plugins** (Gestisci plug-in).</span><span class="sxs-lookup"><span data-stu-id="4fb3c-141">In the **Manage Jenkins** page, choose **Manage Plugins**.</span></span>

1. <span data-ttu-id="4fb3c-142">Filtrare l'elenco per individuare il plug-in **NodeJS** e installarlo senza riavvio.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-142">Filter the list to locate the **NodeJS** plugin and install it without restart.</span></span>

   ![Aggiunta del plug-in NodeJS a Jenkins](media/tutorial-build-deploy-jenkins/jenkins-nodejs-plugin.png)

1. <span data-ttu-id="4fb3c-144">Filtrare l'elenco per trovare il plug-in **Team Foundation Server** e installarlo</span><span class="sxs-lookup"><span data-stu-id="4fb3c-144">Filter the list to find the **Team Foundation Server** plugin and install it.</span></span> <span data-ttu-id="4fb3c-145">(questo plug-in funziona sia con Team Services che con Team Foundation Server). Il riavvio di Jenkins non è necessario.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-145">(This plug-in works for both Team Services and Team Foundation Server.) Restarting Jenkins is not necessary.</span></span>

## <a name="configure-jenkins-build-for-nodejs"></a><span data-ttu-id="4fb3c-146">Configurare la compilazione di Jenkins per Node.js</span><span class="sxs-lookup"><span data-stu-id="4fb3c-146">Configure Jenkins build for Node.js</span></span>

<span data-ttu-id="4fb3c-147">In Jenkins creare un nuovo progetto di compilazione e configurarlo come segue:</span><span class="sxs-lookup"><span data-stu-id="4fb3c-147">In Jenkins, create a new build project and configure it as follows:</span></span>

1. <span data-ttu-id="4fb3c-148">Nella scheda **General** (Generale) immettere un nome per il progetto di compilazione.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-148">In the **General** tab, enter a name for your build project.</span></span>

1. <span data-ttu-id="4fb3c-149">Nella scheda **Source Code Managament** (Gestione codice sorgente) selezionare **Git** e immettere i dettagli del repository e del ramo contenenti il codice dell'app.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-149">In the **Source Code Management** tab, select **Git** and enter the details of the repository and the branch containing your app code.</span></span>

   ![Aggiungere un repository alla build](media/tutorial-build-deploy-jenkins/jenkins-git.png)

   > [!NOTE]
   > <span data-ttu-id="4fb3c-151">Se il repository non è pubblico, scegliere **Add** (Aggiungi) e fornire le credenziali per la connessione.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-151">If your repository is not public, choose **Add** and provide credentials to connect to it.</span></span>

1. <span data-ttu-id="4fb3c-152">Nella scheda **Build Triggers** (Trigger build) selezionare **Poll SCM** (Polling SCM) e immettere la pianificazione `H/03 * * * *` per il polling delle modifiche al repository Git ogni tre minuti.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-152">In the **Build Triggers** tab, select **Poll SCM** and enter the schedule `H/03 * * * *` to poll the Git repository for changes every three minutes.</span></span> 

1. <span data-ttu-id="4fb3c-153">Nella scheda **Build Environment** (Ambiente build) selezionare **Provide Node &amp; npm bin/ folder PATH** e immettere `NodeJS` per il valore Node JS Installation (Installazione Node JS).</span><span class="sxs-lookup"><span data-stu-id="4fb3c-153">In the **Build Environment** tab, select **Provide Node &amp; npm bin/ folder PATH** and enter `NodeJS` for the Node JS Installation value.</span></span> <span data-ttu-id="4fb3c-154">Lasciare **npmrc file** impostato su "use system default" (usa impostazioni predefinite di sistema).</span><span class="sxs-lookup"><span data-stu-id="4fb3c-154">Leave **npmrc file** set to "use system default."</span></span>

1. <span data-ttu-id="4fb3c-155">Nella scheda **Build** (Compila) immettere il comando `npm install` per assicurarsi che tutte le dipendenze siano aggiornate.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-155">In the **Build** tab, enter the command `npm install` to ensure all dependencies are updated.</span></span>

## <a name="configure-jenkins-for-team-services-integration"></a><span data-ttu-id="4fb3c-156">Configurare Jenkins per l'integrazione con Team Services</span><span class="sxs-lookup"><span data-stu-id="4fb3c-156">Configure Jenkins for Team Services integration</span></span>

1. <span data-ttu-id="4fb3c-157">Nella scheda **Post-build Actions** (Azioni post-compilazione) per **Files to archive** (File da archiviare) immettere `**/*` per includere tutti i file.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-157">In the **Post-build Actions** tab, for **Files to archive**, enter `**/*` to include all files.</span></span>

1. <span data-ttu-id="4fb3c-158">Per **Trigger release in TFS/Team Services** (Attiva versione in TFS/Team Services), immettere l'URL completo dell'account, ad esempio `https://your-account-name.visualstudio.com`, il nome del progetto, un nome per la definizione di versione che verrà creata in un secondo momento e le credenziali per connettersi all'account.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-158">For **Trigger release in TFS/Team Services**, enter the full URL of your account (such as `https://your-account-name.visualstudio.com`), the project name, a name for the release definition (created later), and the credentials to connect to your account.</span></span>
   <span data-ttu-id="4fb3c-159">Sono necessari il nome utente e il token di accesso personale creati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-159">You need your user name and the PAT you created earlier.</span></span> 

   ![Configurazione delle azioni di post-compilazione in Jenkins](media/tutorial-build-deploy-jenkins/trigger-release-from-jenkins.png)

1. <span data-ttu-id="4fb3c-161">Salvare il progetto di compilazione.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-161">Save the build project.</span></span>

## <a name="create-a-jenkins-service-endpoint"></a><span data-ttu-id="4fb3c-162">Creare un endpoint servizio di Jenkins</span><span class="sxs-lookup"><span data-stu-id="4fb3c-162">Create a Jenkins service endpoint</span></span>

<span data-ttu-id="4fb3c-163">Un endpoint servizio consente a Team Services di connettersi a Jenkins.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-163">A service endpoint allows Team Services to connect to Jenkins.</span></span>

1. <span data-ttu-id="4fb3c-164">Aprire la pagina **Servizi** in Team Services, aprire l'elenco **Nuovo endpoint servizio** e scegliere **Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-164">Open the **Services** page in Team Services, open the **New Service Endpoint** list, and choose **Jenkins**.</span></span>

   ![Aggiungere un endpoint di Jenkins](media/tutorial-build-deploy-jenkins/add-jenkins-endpoint.png)

1. <span data-ttu-id="4fb3c-166">Immettere un nome da usare come riferimento per questa connessione.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-166">Enter a name you will use to refer to this connection.</span></span>

1. <span data-ttu-id="4fb3c-167">Immettere l'URL del server Jenkins e contrassegnare l'opzione **Accetta i certificati SSL non attendibili**.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-167">Enter the URL of your Jenkins server, and tick the **Accept untrusted SSL certificates** option.</span></span>

1. <span data-ttu-id="4fb3c-168">Immettere il nome utente e la password per l'account di Jenkins.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-168">Enter the user name and password for your Jenkins account.</span></span>

1. <span data-ttu-id="4fb3c-169">Scegliere **Verifica connessione** per assicurarsi che le informazioni siano corrette.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-169">Choose **Verify connection** to check that the information is correct.</span></span>

1. <span data-ttu-id="4fb3c-170">Scegliere **OK** per creare l'endpoint servizio.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-170">Choose **OK** to create the service endpoint.</span></span>

## <a name="create-a-deployment-group"></a><span data-ttu-id="4fb3c-171">Creare un gruppo di distribuzione</span><span class="sxs-lookup"><span data-stu-id="4fb3c-171">Create a deployment group</span></span>

<span data-ttu-id="4fb3c-172">È necessario un [gruppo di distribuzione](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) per contenere le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-172">You need a [deployment group](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) to  contain the virtual machines.</span></span>

1. <span data-ttu-id="4fb3c-173">Aprire la scheda **Versioni** nell'hub **Compilazione &amp; versione**, quindi aprire la scheda **Gruppi di distribuzione** e scegliere **+ Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-173">Open the **Releases** tab of the **Build &amp; Release** hub, then open the **Deployment groups** tab, and choose **+ New**.</span></span>

1. <span data-ttu-id="4fb3c-174">Immettere un nome per il gruppo di distribuzione e una descrizione facoltativa,</span><span class="sxs-lookup"><span data-stu-id="4fb3c-174">Enter a name for the deployment group, and an optional description.</span></span>
   <span data-ttu-id="4fb3c-175">quindi scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-175">Then choose **Create**.</span></span>

<span data-ttu-id="4fb3c-176">L'attività di distribuzione di un gruppo di risorse di Azure crea e registra le macchine virtuali quando viene eseguita con il modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-176">The Azure Resource Group Deployment task creates and registers the VMs when it runs using the Azure Resource Manager template.</span></span>
<span data-ttu-id="4fb3c-177">Non è necessario creare e registrare manualmente le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-177">You don't need to create and register the virtual machines yourself.</span></span>

## <a name="create-a-release-definition"></a><span data-ttu-id="4fb3c-178">Creare una definizione di versione</span><span class="sxs-lookup"><span data-stu-id="4fb3c-178">Create a release definition</span></span>

<span data-ttu-id="4fb3c-179">Una definizione di versione specifica il processo eseguito da Team Services per distribuire l'app.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-179">A release definition specifies the process Team Services will execute to deploy the app.</span></span>
<span data-ttu-id="4fb3c-180">Per creare una definizione di versione in Team Services:</span><span class="sxs-lookup"><span data-stu-id="4fb3c-180">To create the release definition in Team Services:</span></span>

1. <span data-ttu-id="4fb3c-181">Aprire la scheda **Versioni** nell'hub **Compilazione &amp; versione**, aprire l'elenco a discesa **+** di definizioni di versione e scegliere **Crea definizione di versione**.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-181">Open the **Releases** tab of the **Build &amp; Release** hub, open the **+** drop-down in the list of release definitions, and choose the **Create release definition**.</span></span> 

1. <span data-ttu-id="4fb3c-182">Selezionare il modello **Vuoto** e scegliere **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-182">Select the **Empty** template and choose **Next**.</span></span>

1. <span data-ttu-id="4fb3c-183">Nella sezione **Elementi** fare clic su **Collega un elemento** e scegliere **Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-183">In the **Artifacts** section, click on **Link an Artifact** and choose **Jenkins**.</span></span> <span data-ttu-id="4fb3c-184">Selezionare la connessione all'endpoint servizio Jenkins,</span><span class="sxs-lookup"><span data-stu-id="4fb3c-184">Select your Jenkins service endpoint connection.</span></span> <span data-ttu-id="4fb3c-185">quindi selezionare il processo di origine Jenkins e scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-185">Then select the Jenkins source job and choose **Create**.</span></span> 

1. <span data-ttu-id="4fb3c-186">Nella nuova definizione di versione scegliere **+ Aggiungi attività** e aggiungere un'attività **Distribuzione gruppo di risorse di Azure** per l'ambiente predefinito.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-186">In the new release definition, choose **+ Add tasks** and add an **Azure Resource Group Deployment** task to the default environment.</span></span>

1. <span data-ttu-id="4fb3c-187">Scegliere la freccia a discesa accanto al collegamento **+ Aggiungi attività** e aggiungere una fase di gruppo di distribuzione alla definizione.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-187">Choose the drop down arrow next to the **+ Add tasks** link and add a deployment group phase to the definition.</span></span>

   ![Aggiunta di una fase di gruppo di distribuzione](media/tutorial-build-deploy-jenkins/deployment-group-phase-in-release-definition.png) 

1. <span data-ttu-id="4fb3c-189">Nel catalogo delle attività aprire la sezione **Utilità** e aggiungere un'istanza dell'attività **Script della Shell**.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-189">In the Task catalog, open the **Utility** section and add an instance of the **Shell Script** task.</span></span>

1. <span data-ttu-id="4fb3c-190">Il modello di parametri usato nell'attività Distribuzione gruppo di risorse di Azure imposta la password amministratore usata per connettersi alle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-190">The parameters template used in the Azure Resource Group Deployment task sets the admin password used to connect to the VMs.</span></span>
   <span data-ttu-id="4fb3c-191">Fornire la password con la variabile **$(adminpassword)**:</span><span class="sxs-lookup"><span data-stu-id="4fb3c-191">You provide this password with the variable **$(adminpassword)**:</span></span>
   
   - <span data-ttu-id="4fb3c-192">Aprire la scheda **Variabili** e, nella sezione **Variabili**, immettere il nome `adminpassword`.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-192">Open the **Variables** tab and, in the **Variables** section, enter the name `adminpassword`.</span></span>

   - <span data-ttu-id="4fb3c-193">Immettere la password amministratore.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-193">Enter the administrator password.</span></span>

   - <span data-ttu-id="4fb3c-194">Scegliere l'icona "lucchetto" accanto alla casella di testo del valore per proteggere la password.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-194">Choose the "padlock" icon next to the value textbox to protect the password.</span></span> 

## <a name="configure-the-azure-resource-group-deployment-task"></a><span data-ttu-id="4fb3c-195">Configurare l'attività Distribuzione gruppo di risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="4fb3c-195">Configure the Azure Resource Group Deployment task</span></span>

<span data-ttu-id="4fb3c-196">L'attività **Distribuzione gruppo di risorse di Azure** viene usata per creare il gruppo di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-196">The **Azure Resource Group Deployment** task is used to create the deployment group.</span></span> <span data-ttu-id="4fb3c-197">Configurare l'app come segue:</span><span class="sxs-lookup"><span data-stu-id="4fb3c-197">Configure it as follows:</span></span>

* <span data-ttu-id="4fb3c-198">**Sottoscrizione di Azure:** selezionare una connessione dall'elenco in **Connessioni ai servizi di Azure disponibili**.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-198">**Azure Subscription:** Select a connection from the list under **Available Azure Service Connections**.</span></span> 
  <span data-ttu-id="4fb3c-199">Se non viene visualizzata alcuna connessione, scegliere **Gestisci**, selezionare **Nuovo endpoint servizio**, quindi **Azure Resource Manager** e seguire le istruzioni.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-199">If no connections appear, choose **Manage**, select **New Service Endpoint** then **Azure Resource Manager**, and follow the prompts.</span></span>
  <span data-ttu-id="4fb3c-200">Tornare alla definizione di versione, aggiornare l'elenco **Sottoscrizione di AzureRM** e selezionare la connessione creata.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-200">Return to your release definition, refresh the **AzureRM Subscription** list, and select the connection you created.</span></span>

* <span data-ttu-id="4fb3c-201">**Gruppo di risorse**: immettere un nome per il gruppo di risorse creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-201">**Resource group**: Enter a name of the resource group you created earlier.</span></span>

* <span data-ttu-id="4fb3c-202">**Posizione**: selezionare un'area per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-202">**Location**: Select a region for the deployment.</span></span>

  ![Creare un nuovo gruppo di risorse](media/tutorial-build-deploy-jenkins/provision-web-server.png)

* <span data-ttu-id="4fb3c-204">**Percorso del modelli**:`URL of the file`</span><span class="sxs-lookup"><span data-stu-id="4fb3c-204">**Template location**: `URL of the file`</span></span>

* <span data-ttu-id="4fb3c-205">**Collegamento al modello**:`{your-git-repo}/ARM-Templates/UbuntuWeb1.json`</span><span class="sxs-lookup"><span data-stu-id="4fb3c-205">**Template link**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.json`</span></span>

* <span data-ttu-id="4fb3c-206">**Collegamento ai parametri del modello**:`{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`</span><span class="sxs-lookup"><span data-stu-id="4fb3c-206">**Template parameters link**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`</span></span>

* <span data-ttu-id="4fb3c-207">**Esegui override dei parametri del modello**: un elenco dei valori di override, ad esempio: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-207">**Override template parameters**: A list of the override values, for example: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.</span></span><br /><span data-ttu-id="4fb3c-208">Inserire i valori specifici per i {segnaposto}.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-208">Insert your own specific values for the {placeholders}.</span></span> 

* <span data-ttu-id="4fb3c-209">**Abilita i prerequisiti**: `Configure with Deployment Group agent`</span><span class="sxs-lookup"><span data-stu-id="4fb3c-209">**Enable prerequisites**: `Configure with Deployment Group agent`</span></span>

* <span data-ttu-id="4fb3c-210">**Endpoint TFS/VSTS**: scegliere **Aggiungi** e, nella finestra di dialogo "Aggiungi nuova connessione Team Foundation Server/Team Services", selezionare **Autenticazione basata su token**.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-210">**TFS/VSTS endpoint**: Choose **Add** and, in the "Add new Team Foundation Server/Team Services Connection" dialog, select **Token Based Authentication**.</span></span> <span data-ttu-id="4fb3c-211">Immettere un nome per la connessione e l'URL del progetto team.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-211">Enter a name of the connection and the URL of your team project.</span></span> <span data-ttu-id="4fb3c-212">Quindi generare e immettere un [token di accesso personale]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) per autenticare la connessione al progetto team.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-212">Then generate and enter a [Personal Access Token (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) to authenticate the connection to your team project.</span></span>

  ![Creare un token di accesso personale](media/tutorial-build-deploy-jenkins/create-a-pat.png)

* <span data-ttu-id="4fb3c-214">**Progetto team**: selezionare il progetto corrente.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-214">**Team project**: Select your current project.</span></span>

* <span data-ttu-id="4fb3c-215">**Gruppo di distribuzione**: immettere lo stesso nome del gruppo di distribuzione usato per il parametro **Gruppo di risorse**.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-215">**Deployment Group**: Enter the same deployment group name as you used for the **Resource group** parameter.</span></span>

<span data-ttu-id="4fb3c-216">Le impostazioni predefinite per l'attività Distribuzione gruppo di risorse di Azure creano o aggiornano una risorsa in modo incrementale.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-216">The default settings for the Azure Resource Group Deployment task are to create or update a resource, and to do so incrementally.</span></span> <span data-ttu-id="4fb3c-217">L'attività crea le macchine virtuali la prima volta che viene eseguita. In seguito, si limita ad aggiornarle.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-217">The task creates the VMs the first time it runs, and subsequently just update them.</span></span>

## <a name="configure-the-shell-script-task"></a><span data-ttu-id="4fb3c-218">Configurare l'attività Script della Shell</span><span class="sxs-lookup"><span data-stu-id="4fb3c-218">Configure the Shell Script task</span></span>

<span data-ttu-id="4fb3c-219">L'attività **Script della Shell** viene usata per fornire la configurazione di esecuzione di uno script in ogni server, al fine di installare Node.js e avviare l'app.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-219">The **Shell Script** task is used to provide the configuration for a script to run on each server to install Node.js and start the app.</span></span> <span data-ttu-id="4fb3c-220">Configurare l'app come segue:</span><span class="sxs-lookup"><span data-stu-id="4fb3c-220">Configure it as follows:</span></span>

* <span data-ttu-id="4fb3c-221">**Percorso script**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`</span><span class="sxs-lookup"><span data-stu-id="4fb3c-221">**Script Path**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`</span></span>

* <span data-ttu-id="4fb3c-222">**Specifica directory di lavoro**: `Checked`</span><span class="sxs-lookup"><span data-stu-id="4fb3c-222">**Specify Working Directory**: `Checked`</span></span>

* <span data-ttu-id="4fb3c-223">**Directory di lavoro**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node`</span><span class="sxs-lookup"><span data-stu-id="4fb3c-223">**Working Directory**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node`</span></span>
   
## <a name="rename-and-save-the-release-definition"></a><span data-ttu-id="4fb3c-224">Rinominare e salvare la definizione di versione</span><span class="sxs-lookup"><span data-stu-id="4fb3c-224">Rename and save the release definition</span></span>

1. <span data-ttu-id="4fb3c-225">Modificare il nome della definizione di versione in quello specificato nella scheda **Post-build Actions** (Azioni post-compilazione) nella build in Jenkins.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-225">Edit the name of the release definition to the name you specified in the **Post-build Actions** tab of the build in Jenkins.</span></span> <span data-ttu-id="4fb3c-226">Jenkins richiede questo nome per poter attivare una nuova versione quando vengono aggiornati gli elementi di origine.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-226">Jenkins requires this name to be able to trigger a new release when the source artifacts are updated.</span></span>

1. <span data-ttu-id="4fb3c-227">Facoltativamente, modificare il nome dell'ambiente facendo clic sul nome.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-227">Optionally, change the name of the environment by clicking on the name.</span></span> 

1. <span data-ttu-id="4fb3c-228">Scegliere **Salva** e quindi **OK**.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-228">Choose **Save**, and choose **OK**.</span></span>

## <a name="start-a-manual-deployment"></a><span data-ttu-id="4fb3c-229">Avviare una distribuzione manuale</span><span class="sxs-lookup"><span data-stu-id="4fb3c-229">Start a manual deployment</span></span>

1. <span data-ttu-id="4fb3c-230">Scegliere **+ Versione** e selezionare **Crea versione**.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-230">Choose **+ Release** and select **Create Release**.</span></span>

1. <span data-ttu-id="4fb3c-231">Selezionare la build completata nell'elenco a discesa evidenziato e scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-231">Select the build you completed in the highlighted drop-down list and choose **Create**.</span></span>

1. <span data-ttu-id="4fb3c-232">Scegliere il collegamento di versione nel messaggio popup.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-232">Choose the release link in the popup message.</span></span> <span data-ttu-id="4fb3c-233">Ad esempio: "Versione **Versione-1** creata."</span><span class="sxs-lookup"><span data-stu-id="4fb3c-233">For example: "Release **Release-1** has been created."</span></span>

1. <span data-ttu-id="4fb3c-234">Aprire la scheda **Log** per osservare l'output della console della versione.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-234">Open the **Logs** tab to watch the release console output.</span></span>

1. <span data-ttu-id="4fb3c-235">Nel browser aprire l'URL di uno dei server aggiunti al gruppo di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-235">In your browser, open the URL of one of the servers you added to your deployment group.</span></span> <span data-ttu-id="4fb3c-236">Ad esempio, immettere `http://{your-server-ip-address}`</span><span class="sxs-lookup"><span data-stu-id="4fb3c-236">For example, enter `http://{your-server-ip-address}`</span></span>

## <a name="start-a-cicd-deployment"></a><span data-ttu-id="4fb3c-237">Avviare una distribuzione CI/CD</span><span class="sxs-lookup"><span data-stu-id="4fb3c-237">Start a CI/CD deployment</span></span>

1. <span data-ttu-id="4fb3c-238">Nella definizione di versione deselezionare la casella di controllo **Abilitato** nella sezione **Opzioni di controllo** delle impostazioni dell'attività Distribuzione gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-238">In the release definition, uncheck the **Enabled** checkbox in the **Control Options** section of the settings for the Azure Resource Group Deployment task.</span></span>
   <span data-ttu-id="4fb3c-239">Per le distribuzioni future al gruppo di distribuzione esistente non è necessario eseguire nuovamente questa attività.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-239">For future deployments to the existing deployment group, you do not need to re-execute this task.</span></span>

1. <span data-ttu-id="4fb3c-240">Passare al repository Git di origine e di modificare il contenuto del titolo **h1** nel file [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).</span><span class="sxs-lookup"><span data-stu-id="4fb3c-240">Go to the source Git repository and modify the contents of the **h1** heading in the file [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).</span></span>

1. <span data-ttu-id="4fb3c-241">Eseguire il commit delle modifiche.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-241">Commit your change.</span></span>

1. <span data-ttu-id="4fb3c-242">Dopo alcuni minuti, si noterà una nuova versione creata nella pagina **Versioni** di Team Services o TFS.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-242">After a few minutes, you will see a new release created in the **Releases** page of Team Services or TFS.</span></span> <span data-ttu-id="4fb3c-243">Aprire la versione per visualizzare la distribuzione in corso.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-243">Open the release to see the deployment taking place.</span></span> <span data-ttu-id="4fb3c-244">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-244">Congratulations!</span></span>

## <a name="next-steps"></a><span data-ttu-id="4fb3c-245">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4fb3c-245">Next Steps</span></span>

<span data-ttu-id="4fb3c-246">In questa esercitazione è stata automatizzata la distribuzione di un'app in Azure tramite la compilazione in Jenkins e Team Services per il rilascio.</span><span class="sxs-lookup"><span data-stu-id="4fb3c-246">In this tutorial, you automated the deployment of an app to Azure using Jenkins build and Team Services for release.</span></span> <span data-ttu-id="4fb3c-247">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="4fb3c-247">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4fb3c-248">Creare l'app in Jenkins</span><span class="sxs-lookup"><span data-stu-id="4fb3c-248">Build your app in Jenkins</span></span>
> * <span data-ttu-id="4fb3c-249">Configurare Jenkins per l'integrazione con Team Services</span><span class="sxs-lookup"><span data-stu-id="4fb3c-249">Configure Jenkins for Team Services integration</span></span>
> * <span data-ttu-id="4fb3c-250">Creare un gruppo di distribuzione per le macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="4fb3c-250">Create a deployment group for the Azure virtual machines</span></span>
> * <span data-ttu-id="4fb3c-251">Creare una definizione di versione che configuri le macchine virtuali e distribuisca l'app</span><span class="sxs-lookup"><span data-stu-id="4fb3c-251">Create a release definition that configures the VMs and deploys the app</span></span>

<span data-ttu-id="4fb3c-252">Passare all'esercitazione successiva per ottenere altre informazioni su come distribuire uno stack LAMP (Linux, Apache, MySQL e PHP).</span><span class="sxs-lookup"><span data-stu-id="4fb3c-252">Advance to the next tutorial to learn more about how to deploy a LAMP (Linux, Apache, MySQL, and PHP) stack.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4fb3c-253">Distribuire lo stack LAMP</span><span class="sxs-lookup"><span data-stu-id="4fb3c-253">Deploy LAMP stack</span></span>](tutorial-lamp-stack.md)