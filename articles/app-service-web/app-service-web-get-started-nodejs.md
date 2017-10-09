---
title: aaaCreate un'app web Node.js in Azure | Documenti Microsoft
description: Distribuire la prima app Node.js Hello World in un'app Web del servizio app di Azure in pochi minuti.
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 582bb3c2-164b-42f5-b081-95bfcb7a502a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 05/05/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 163edf83b2353755fc9fa2d75aed489038cf7c81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-nodejs-web-app-in-azure"></a><span data-ttu-id="d890b-103">Creare un'app Web Node.js in Azure</span><span class="sxs-lookup"><span data-stu-id="d890b-103">Create a Node.js web app in Azure</span></span>

<span data-ttu-id="d890b-104">Le [app Web di Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) forniscono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione.</span><span class="sxs-lookup"><span data-stu-id="d890b-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="d890b-105">Questa Guida introduttiva viene illustrato come toodeploy un tooAzure app Node.js App Web.</span><span class="sxs-lookup"><span data-stu-id="d890b-105">This quickstart shows how toodeploy a Node.js app tooAzure Web Apps.</span></span> <span data-ttu-id="d890b-106">Si crea app web hello utilizzando hello [CLI di Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), e si usa Git toodeploy esempio Node.js codice toohello web app.</span><span class="sxs-lookup"><span data-stu-id="d890b-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git toodeploy sample Node.js code toohello web app.</span></span>

![App di esempio in esecuzione in Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="d890b-108">È possibile eseguire operazioni di hello seguenti utilizzando un computer Mac, Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="d890b-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="d890b-109">Una volta installati i prerequisiti di hello, sono necessari circa cinque minuti toocomplete passaggi hello.</span><span class="sxs-lookup"><span data-stu-id="d890b-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>   

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-Node-Developers/Create-a-Nodejs-app-in-Azure-Quickstart/player]   


## <a name="prerequisites"></a><span data-ttu-id="d890b-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d890b-110">Prerequisites</span></span>

<span data-ttu-id="d890b-111">toocomplete questa Guida rapida:</span><span class="sxs-lookup"><span data-stu-id="d890b-111">toocomplete this quickstart:</span></span>

* [<span data-ttu-id="d890b-112">Installare Git</span><span class="sxs-lookup"><span data-stu-id="d890b-112">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="d890b-113">Installare Node.js e NPM</span><span class="sxs-lookup"><span data-stu-id="d890b-113">Install Node.js and NPM</span></span>](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d890b-114">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="d890b-114">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="d890b-115">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="d890b-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="d890b-116">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d890b-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-hello-sample"></a><span data-ttu-id="d890b-117">Scaricare l'esempio hello</span><span class="sxs-lookup"><span data-stu-id="d890b-117">Download hello sample</span></span>

<span data-ttu-id="d890b-118">In una finestra terminale, eseguire hello successivo comando tooclone hello esempio app repository tooyour computer locale.</span><span class="sxs-lookup"><span data-stu-id="d890b-118">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/nodejs-docs-hello-world
```

<span data-ttu-id="d890b-119">Utilizzare questo toorun finestra terminale tutti i comandi di hello in questa Guida rapida.</span><span class="sxs-lookup"><span data-stu-id="d890b-119">You use this terminal window toorun all hello commands in this quickstart.</span></span>

<span data-ttu-id="d890b-120">Spostarsi nella directory toohello che contiene il codice di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="d890b-120">Change toohello directory that contains hello sample code.</span></span>

```bash
cd nodejs-docs-hello-world
```

## <a name="run-hello-app-locally"></a><span data-ttu-id="d890b-121">Eseguire app hello in locale</span><span class="sxs-lookup"><span data-stu-id="d890b-121">Run hello app locally</span></span>

<span data-ttu-id="d890b-122">Eseguire un'applicazione hello in locale, aprire una finestra terminale e utilizzare hello `npm start` hello toolaunch script compilato nel server Node.js HTTP.</span><span class="sxs-lookup"><span data-stu-id="d890b-122">Run hello application locally by opening a terminal window and using hello `npm start` script toolaunch hello built in Node.js HTTP server.</span></span>

```bash
npm start
```

<span data-ttu-id="d890b-123">Aprire un web browser e passare l'app di esempio toohello in http://localhost:1337.</span><span class="sxs-lookup"><span data-stu-id="d890b-123">Open a web browser, and navigate toohello sample app at http://localhost:1337.</span></span>

<span data-ttu-id="d890b-124">Vedrai hello **Hello World** messaggio dall'applicazione di esempio hello visualizzato nella pagina hello.</span><span class="sxs-lookup"><span data-stu-id="d890b-124">You see hello **Hello World** message from hello sample app displayed in hello page.</span></span>

![App di esempio in esecuzione in locale](media/app-service-web-get-started-nodejs-poc/localhost-hello-world-in-browser.png)

<span data-ttu-id="d890b-126">Nella finestra del terminale, premere **Ctrl + C** server web di tooexit hello.</span><span class="sxs-lookup"><span data-stu-id="d890b-126">In your terminal window, press **Ctrl+C** tooexit hello web server.</span></span>

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Pagina dell'app Web vuota](media/app-service-web-get-started-php/app-service-web-service-created.png)

<span data-ttu-id="d890b-128">È stata creata una nuova app Web vuota in Azure.</span><span class="sxs-lookup"><span data-stu-id="d890b-128">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 23, done.
Delta compression using up too4 threads.
Compressing objects: 100% (21/21), done.
Writing objects: 100% (23/23), 3.71 KiB | 0 bytes/s, done.
Total 23 (delta 8), reused 7 (delta 1)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'bf114df591'.
remote: Generating deployment script.
remote: Generating deployment script for node.js Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling node.js deployment.
remote: Kudu sync from: '/home/site/repository' to: '/home/site/wwwroot'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Copying file: 'index.js'
remote: Copying file: 'package.json'
remote: Copying file: 'process.json'
remote: Deleting file: 'hostingstart.html'
remote: Ignoring: .git
remote: Using start-up script index.js from package.json.
remote: Node.js versions available on hello platform are: 4.4.7, 4.5.0, 6.2.2, 6.6.0, 6.9.1.
remote: Selected node.js version 6.9.1. Use package.json file toochoose a different version.
remote: Selected npm version 3.10.8
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net:443/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a><span data-ttu-id="d890b-129">Esplorare app toohello</span><span class="sxs-lookup"><span data-stu-id="d890b-129">Browse toohello app</span></span>

<span data-ttu-id="d890b-130">Sfoglia toohello distribuito l'applicazione tramite il web browser.</span><span class="sxs-lookup"><span data-stu-id="d890b-130">Browse toohello deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="d890b-131">codice di esempio Node.js Hello è in esecuzione in un'applicazione web di servizio App di Azure.</span><span class="sxs-lookup"><span data-stu-id="d890b-131">hello Node.js sample code is running in an Azure App Service web app.</span></span>

![App di esempio in esecuzione in Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="d890b-133">**Congratulazioni.**</span><span class="sxs-lookup"><span data-stu-id="d890b-133">**Congratulations!**</span></span> <span data-ttu-id="d890b-134">Il primo tooApp di app Node.js servizio distribuiti.</span><span class="sxs-lookup"><span data-stu-id="d890b-134">You've deployed your first Node.js app tooApp Service.</span></span>

## <a name="update-and-redeploy-hello-code"></a><span data-ttu-id="d890b-135">Aggiornare e ridistribuire codice hello</span><span class="sxs-lookup"><span data-stu-id="d890b-135">Update and redeploy hello code</span></span>

<span data-ttu-id="d890b-136">Utilizzando un editor di testo, aprire hello `index.js` file nell'app Node.js hello e consente di applicare una piccola modifica toohello testo nella chiamata di hello troppo`response.end`:</span><span class="sxs-lookup"><span data-stu-id="d890b-136">Using a text editor, open hello `index.js` file in hello Node.js app, and make a small change toohello text in hello call too`response.end`:</span></span>

```nodejs
response.end("Hello Azure!");
```

<span data-ttu-id="d890b-137">Eseguire il commit delle modifiche in Git e quindi push tooAzure modifiche di codice hello.</span><span class="sxs-lookup"><span data-stu-id="d890b-137">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="d890b-138">Una volta completata la distribuzione, passare toohello indietro finestra del browser aperto in hello **Sfoglia toohello app** passaggio e fare clic su Aggiorna.</span><span class="sxs-lookup"><span data-stu-id="d890b-138">Once deployment has completed, switch back toohello browser window that opened in hello **Browse toohello app** step, and hit refresh.</span></span>

![App di esempio aggiornata in esecuzione in Azure](media/app-service-web-get-started-nodejs-poc/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="d890b-140">Gestire la nuova app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="d890b-140">Manage your new Azure web app</span></span>

<span data-ttu-id="d890b-141">Passare toohello <a href="https://portal.azure.com" target="_blank">portale di Azure</a> toomanage hello web app è stato creato.</span><span class="sxs-lookup"><span data-stu-id="d890b-141">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="d890b-142">Scegliere dal menu a sinistra hello **servizi App**, quindi fare clic su nome hello dell'app web di Azure.</span><span class="sxs-lookup"><span data-stu-id="d890b-142">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Spostamento del portale tooAzure web app](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="d890b-144">Verrà visualizzata la pagina di panoramica dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="d890b-144">You see your web app's Overview page.</span></span> <span data-ttu-id="d890b-145">Qui è possibile eseguire attività di gestione di base come l'esplorazione, l'arresto, l'avvio, il riavvio e l'eliminazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="d890b-145">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Pannello del servizio app nel portale di Azure](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="d890b-147">menu a sinistra di Hello fornisce diverse pagine di configurazione app.</span><span class="sxs-lookup"><span data-stu-id="d890b-147">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="d890b-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d890b-148">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d890b-149">Node.js con MongoDB</span><span class="sxs-lookup"><span data-stu-id="d890b-149">Node.js with MongoDB</span></span>](app-service-web-tutorial-nodejs-mongodb-app.md)
