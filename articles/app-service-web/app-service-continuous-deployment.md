---
title: aaaContinuous tooAzure distribuzione servizio App | Documenti Microsoft
description: Informazioni su come la distribuzione continua di tooenable tooAzure servizio App.
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 6adb5c84-6cf3-424e-a336-c554f23b4000
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 62a22cbda354fd5b0a1b9729c8c375408e75049f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-tooazure-app-service"></a><span data-ttu-id="752ac-103">TooAzure distribuzione continua servizio App</span><span class="sxs-lookup"><span data-stu-id="752ac-103">Continuous Deployment tooAzure App Service</span></span>
<span data-ttu-id="752ac-104">In questa esercitazione illustra come tooconfigure un flusso di lavoro di distribuzione continua per il [Azure App Service] app.</span><span class="sxs-lookup"><span data-stu-id="752ac-104">This tutorial shows you how tooconfigure a continuous deployment workflow for your [Azure App Service] app.</span></span> <span data-ttu-id="752ac-105">Integrazione del servizio App con BitBucket, GitHub, e [Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) consente un continuo del flusso di lavoro di distribuzione in Azure esegue il pull degli aggiornamenti più recenti di hello dal progetto pubblicati tooone di questi servizi.</span><span class="sxs-lookup"><span data-stu-id="752ac-105">App Service integration with BitBucket, GitHub, and [Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) enables a continuous deployment workflow where Azure pulls in hello most recent updates from your project published tooone of these services.</span></span> <span data-ttu-id="752ac-106">La distribuzione continua è un'ottima opzione per i progetti in cui vengono integrati contributi numerosi e frequenti.</span><span class="sxs-lookup"><span data-stu-id="752ac-106">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span>

<span data-ttu-id="752ac-107">toofind out come la distribuzione continua tooconfigure manualmente da un repository di cloud non elencata hello portale di Azure (ad esempio [GitLab](https://gitlab.com/)), vedere [configurazione di distribuzione continua tramite i passaggi manuali](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).</span><span class="sxs-lookup"><span data-stu-id="752ac-107">toofind out how tooconfigure continuous deployment manually from a cloud repository not listed by hello Azure Portal (such as [GitLab](https://gitlab.com/)), see [Setting up continuous deployment using manual steps](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).</span></span>

## <span data-ttu-id="752ac-108"><a name="overview"></a>Abilitare la distribuzione continua</span><span class="sxs-lookup"><span data-stu-id="752ac-108"><a name="overview"></a>Enable continuous deployment</span></span>
<span data-ttu-id="752ac-109">distribuzione continua tooenable,</span><span class="sxs-lookup"><span data-stu-id="752ac-109">tooenable continuous deployment,</span></span>

1. <span data-ttu-id="752ac-110">Pubblicare il repository di contenuto toohello app che verrà utilizzato per la distribuzione continua.</span><span class="sxs-lookup"><span data-stu-id="752ac-110">Publish your app content toohello repository that will be used for continuous deployment.</span></span>  
    <span data-ttu-id="752ac-111">Per ulteriori informazioni sulla pubblicazione di servizi toothese progetto, vedere [creare un repository (GitHub)], [creare un repository (BitBucket)], e [Introduzione a Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="752ac-111">For more information on publishing your project toothese services, see [Create a repo (GitHub)], [Create a repo (BitBucket)], and [Get started with VSTS].</span></span>
2. <span data-ttu-id="752ac-112">Nel Pannello di menu dell'applicazione in hello [portale di Azure], fare clic su **distribuzione dell'APP > Opzioni di distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="752ac-112">In your app's menu blade in hello [Azure portal], click **APP DEPLOYMENT > Deployment options**.</span></span> <span data-ttu-id="752ac-113">Fare clic su **Scegli origine**, quindi selezionare origine distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="752ac-113">Click **Choose Source**, then select hello deployment source.</span></span>  
   
    ![](./media/app-service-continuous-deployment/cd_options.png)
   
   > [!NOTE]
   > <span data-ttu-id="752ac-114">tooconfigure un account di Visual Studio Team Services per la distribuzione di servizio App, vedere [esercitazione](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).</span><span class="sxs-lookup"><span data-stu-id="752ac-114">tooconfigure a VSTS account for App Service deployment please see this [tutorial](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).</span></span>
   > 
   > 
3. <span data-ttu-id="752ac-115">Completamento del flusso di lavoro di hello autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="752ac-115">Complete hello authorization workflow.</span></span>
4. <span data-ttu-id="752ac-116">In hello **origine distribuzione** pannello, scegliere il progetto hello e creare rami toodeploy da.</span><span class="sxs-lookup"><span data-stu-id="752ac-116">In hello **Deployment source** blade, choose hello project and branch toodeploy from.</span></span> <span data-ttu-id="752ac-117">Al termine, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="752ac-117">When you're done, click **OK**.</span></span>
   
    ![](./media/app-service-continuous-deployment/github_option.png)
   
   > [!NOTE]
   > <span data-ttu-id="752ac-118">Se si abilita la distribuzione continua con GitHub o BitBucket, verranno visualizzati progetti sia pubblici che privati.</span><span class="sxs-lookup"><span data-stu-id="752ac-118">When enabling continuous deployment with GitHub or BitBucket, both public and private projects will be displayed.</span></span>
   > 
   > 
   
    <span data-ttu-id="752ac-119">Servizio App crea un'associazione con repository selezionato hello, inserisce nel file hello dal ramo specificato hello e mantiene un clone del repository per l'applicazione di servizio App.</span><span class="sxs-lookup"><span data-stu-id="752ac-119">App Service creates an association with hello selected repository, pulls in hello files from hello specified branch, and maintains a clone of your repository for your App Service app.</span></span> <span data-ttu-id="752ac-120">Quando si configura una distribuzione continua VSTS dal portale di Azure hello, integrazione di hello utilizza hello servizio App [motore di distribuzione Kudu](https://github.com/projectkudu/kudu/wiki), che già automatizza le attività di compilazione e distribuzione con ogni `git push`.</span><span class="sxs-lookup"><span data-stu-id="752ac-120">When you configure VSTS continuous deployment from hello Azure portal, hello integration uses hello App Service [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki), which already automates build and deployment tasks with every `git push`.</span></span> <span data-ttu-id="752ac-121">Tooseparately non è necessario impostare la distribuzione continua in Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="752ac-121">You do not need tooseparately set up continuous deployment in VSTS.</span></span> <span data-ttu-id="752ac-122">Dopo il completamento del processo, hello **opzioni di distribuzione** pannello app verrà visualizzata una distribuzione attiva che indica la distribuzione ha avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="752ac-122">After this process completes, hello **Deployment options** app blade will show an active deployment that indicates deployment has succeeded.</span></span>
5. <span data-ttu-id="752ac-123">è stata distribuita correttamente tooverify hello app, fare clic su hello **URL** nella parte superiore di hello del pannello dell'applicazione hello in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="752ac-123">tooverify hello app is successfully deployed, click hello **URL** at hello top of hello app's blade in hello Azure portal.</span></span>
6. <span data-ttu-id="752ac-124">tooverify in corso la distribuzione continua dal repository hello di propria scelta, push di un repository toohello di modifica.</span><span class="sxs-lookup"><span data-stu-id="752ac-124">tooverify that continuous deployment is occurring from hello repository of your choice, push a change toohello repository.</span></span> <span data-ttu-id="752ac-125">L'app deve aggiornare le modifiche di hello tooreflect a breve termine repository toohello di hello push.</span><span class="sxs-lookup"><span data-stu-id="752ac-125">Your app should update tooreflect hello changes shortly after hello push toohello repository completes.</span></span> <span data-ttu-id="752ac-126">È possibile verificare che è estratta nell'aggiornamento hello in hello **opzioni di distribuzione** pannello dell'app.</span><span class="sxs-lookup"><span data-stu-id="752ac-126">You can verify that it has pulled in hello update in hello **Deployment options** blade of your app.</span></span>

## <span data-ttu-id="752ac-127"><a name="VSsolution"></a>Distribuzione continua di una soluzione di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="752ac-127"><a name="VSsolution"></a>Continuous deployment of a Visual Studio solution</span></span>
<span data-ttu-id="752ac-128">Inserendo un tooAzure di soluzioni di Visual Studio servizio App è semplice come l'inserimento di un file index.html semplice.</span><span class="sxs-lookup"><span data-stu-id="752ac-128">Pushing a Visual Studio solution tooAzure App Service is just as easy as pushing a simple index.html file.</span></span> <span data-ttu-id="752ac-129">il processo di distribuzione di servizio App Hello semplifica tutti i dettagli di hello, incluso il ripristino NuGet dipendenze e la creazione di file binari dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="752ac-129">hello App Service deployment process streamlines all hello details, including restoring NuGet dependencies and building hello application binaries.</span></span> <span data-ttu-id="752ac-130">È possibile seguire hello origine controllo procedure consigliate di gestione del codice solo nel repository Git e fare in modo che la distribuzione del servizio App rest hello.</span><span class="sxs-lookup"><span data-stu-id="752ac-130">You can follow hello source control best practices of maintaining code only in your Git repository, and let App Service deployment take care of hello rest.</span></span>

<span data-ttu-id="752ac-131">Hello passaggi per l'inserimento del tooApp soluzione Visual Studio sono servizio hello stesso come hello [precedente sezione](#overview), a condizione che si configura la soluzione e il repository come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="752ac-131">hello steps for pushing your Visual Studio solution tooApp Service are hello same as in hello [previous section](#overview), provided that you configure your solution and repository as follows:</span></span>

* <span data-ttu-id="752ac-132">Utilizzare hello Visual Studio origine controllo opzione toogenerate un `.gitignore` file, ad esempio l'immagine di hello seguente o aggiungere manualmente un `.gitignore` file nella radice del repository con contenuto toothis simile [esempio con estensione gitignore](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span><span class="sxs-lookup"><span data-stu-id="752ac-132">Use hello Visual Studio source control option toogenerate a `.gitignore` file such as hello image below or manually add a `.gitignore` file in your repository root with content similar toothis [.gitignore sample](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>
  
  ![](./media/app-service-continuous-deployment/VS_source_control.png)
* <span data-ttu-id="752ac-133">Aggiungi repository di tooyour struttura ad albero di directory hello intera soluzione, con il file con estensione sln hello nella radice del repository hello.</span><span class="sxs-lookup"><span data-stu-id="752ac-133">Add hello entire solution's directory tree tooyour repository, with hello .sln file in hello repository root.</span></span>

<span data-ttu-id="752ac-134">Dopo aver impostato il repository come descritto e configurata l'app in Azure per la pubblicazione continua da uno dei repository Git online hello, è possibile sviluppare l'applicazione ASP.NET in locale in Visual Studio e in modo continuo di semplicemente da distribuire il codice inserendo il repository Git in linea del tooyour le modifiche.</span><span class="sxs-lookup"><span data-stu-id="752ac-134">Once you have set up your repository as described, and configured your app in Azure for continuous publishing from one of hello online Git repositories, you can develop your ASP.NET application locally in Visual Studio and continuously deploy your code simply by pushing your changes tooyour online Git repository.</span></span>

## <span data-ttu-id="752ac-135"><a name="disableCD"></a>Disabilitare la distribuzione continua</span><span class="sxs-lookup"><span data-stu-id="752ac-135"><a name="disableCD"></a>Disable continuous deployment</span></span>
<span data-ttu-id="752ac-136">distribuzione continua toodisable,</span><span class="sxs-lookup"><span data-stu-id="752ac-136">toodisable continuous deployment,</span></span>

1. <span data-ttu-id="752ac-137">Nel Pannello di menu dell'applicazione in hello [portale di Azure], fare clic su **distribuzione dell'APP > Opzioni di distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="752ac-137">In your app's menu blade in hello [Azure portal], click **APP DEPLOYMENT > Deployment options**.</span></span> <span data-ttu-id="752ac-138">Quindi fare clic su **Disconnect** in hello **opzioni di distribuzione** blade.</span><span class="sxs-lookup"><span data-stu-id="752ac-138">Then click **Disconnect** in hello **Deployment options** blade.</span></span>
   
    ![](./media/app-service-continuous-deployment/cd_disconnect.png)
2. <span data-ttu-id="752ac-139">Dopo la risposta **Sì** toohello messaggio di conferma, è possibile restituire pannello tooyour dell'app e fare clic su **distribuzione dell'APP > Opzioni di distribuzione** se si desidera tooset la pubblicazione da un'altra origine.</span><span class="sxs-lookup"><span data-stu-id="752ac-139">After answering **Yes** toohello confirmation message, you can return tooyour app's blade and click **APP DEPLOYMENT > Deployment options** if you would like tooset up publishing from another source.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="752ac-140">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="752ac-140">Additional Resources</span></span>
* [<span data-ttu-id="752ac-141">La modalità di problemi comuni di tooinvestigate con una distribuzione continua</span><span class="sxs-lookup"><span data-stu-id="752ac-141">How tooinvestigate common issues with continuous deployment</span></span>](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment)
* <span data-ttu-id="752ac-142">[Come toouse PowerShell per Azure]</span><span class="sxs-lookup"><span data-stu-id="752ac-142">[How toouse PowerShell for Azure]</span></span>
* <span data-ttu-id="752ac-143">[Come toouse hello strumenti da riga di comando di Azure per Mac e Linux]</span><span class="sxs-lookup"><span data-stu-id="752ac-143">[How toouse hello Azure Command-Line Tools for Mac and Linux]</span></span>
* <span data-ttu-id="752ac-144">[Documentazione su Git]</span><span class="sxs-lookup"><span data-stu-id="752ac-144">[Git documentation]</span></span>
* [<span data-ttu-id="752ac-145">Progetto Kudu</span><span class="sxs-lookup"><span data-stu-id="752ac-145">Project Kudu</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="752ac-146">Usare Azure tooautomatically genera un'app di CI/CD pipeline toodeploy un ASP.NET 4</span><span class="sxs-lookup"><span data-stu-id="752ac-146">Use Azure tooautomatically generate a CI/CD pipeline toodeploy an ASP.NET 4 app</span></span>](https://www.visualstudio.com/docs/build/get-started/aspnet-4-ci-cd-azure-automatic)

> [!NOTE]
> <span data-ttu-id="752ac-147">Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="752ac-147">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="752ac-148">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="752ac-148">No credit cards required; no commitments.</span></span>
> 
> 

[Azure App Service]: https://azure.microsoft.com/en-us/documentation/articles/app-service-changes-existing-services/
[portale di Azure]: https://portal.azure.com
[VSTS Portal]: https://www.visualstudio.com/en-us/products/visual-studio-team-services-vs.aspx
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[Come toouse PowerShell per Azure]: /powershell/azureps-cmdlets-docs
[Come toouse hello strumenti da riga di comando di Azure per Mac e Linux]:../cli-install-nodejs.md
[Documentazione su Git]: http://git-scm.com/documentation

[creare un repository (GitHub)]: https://help.github.com/articles/create-a-repo
[creare un repository (BitBucket)]: https://confluence.atlassian.com/display/BITBUCKET/Create+an+Account+and+a+Git+Repo
[Introduzione a Visual Studio Team Services]: https://www.visualstudio.com/docs/vsts-tfs-overview
