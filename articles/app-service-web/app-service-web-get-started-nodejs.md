---
title: Creare un'app Web Node.js in Azure | Microsoft Docs
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
ms.openlocfilehash: ce845da09a7c088b8a2ba29b818a46a3b41aa4e7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-nodejs-web-app-in-azure"></a><span data-ttu-id="73b04-103">Creare un'app Web Node.js in Azure</span><span class="sxs-lookup"><span data-stu-id="73b04-103">Create a Node.js web app in Azure</span></span>

<span data-ttu-id="73b04-104">Le [app Web di Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) forniscono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione.</span><span class="sxs-lookup"><span data-stu-id="73b04-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="73b04-105">Questa guida introduttiva illustra come distribuire un'app Node.js in un'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="73b04-105">This quickstart shows how to deploy a Node.js app to Azure Web Apps.</span></span> <span data-ttu-id="73b04-106">Si creerà l'app Web usando l'[interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) e si userà Git per distribuire il codice Node.js di esempio nell'app Web.</span><span class="sxs-lookup"><span data-stu-id="73b04-106">You create the web app using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git to deploy sample Node.js code to the web app.</span></span>

![App di esempio in esecuzione in Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="73b04-108">È possibile eseguire queste procedure con un computer Mac, Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="73b04-108">You can follow the steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="73b04-109">Una volta installati i prerequisiti, sono necessari circa cinque minuti per completare la procedura.</span><span class="sxs-lookup"><span data-stu-id="73b04-109">Once the prerequisites are installed, it takes about five minutes to complete the steps.</span></span>   

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-Node-Developers/Create-a-Nodejs-app-in-Azure-Quickstart/player]   


## <a name="prerequisites"></a><span data-ttu-id="73b04-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="73b04-110">Prerequisites</span></span>

<span data-ttu-id="73b04-111">Per completare questa guida introduttiva:</span><span class="sxs-lookup"><span data-stu-id="73b04-111">To complete this quickstart:</span></span>

* [<span data-ttu-id="73b04-112">Installare Git</span><span class="sxs-lookup"><span data-stu-id="73b04-112">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="73b04-113">Installare Node.js e NPM</span><span class="sxs-lookup"><span data-stu-id="73b04-113">Install Node.js and NPM</span></span>](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="73b04-114">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="73b04-114">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="73b04-115">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="73b04-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="73b04-116">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="73b04-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-the-sample"></a><span data-ttu-id="73b04-117">Scaricare l'esempio</span><span class="sxs-lookup"><span data-stu-id="73b04-117">Download the sample</span></span>

<span data-ttu-id="73b04-118">In una finestra del terminale eseguire il comando seguente per clonare il repository dell'app di esempio nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="73b04-118">In a terminal window, run the following command to clone the sample app repository to your local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/nodejs-docs-hello-world
```

<span data-ttu-id="73b04-119">Questa finestra del terminale dovrà essere usata per eseguire tutti i comandi presenti in questa guida introduttiva.</span><span class="sxs-lookup"><span data-stu-id="73b04-119">You use this terminal window to run all the commands in this quickstart.</span></span>

<span data-ttu-id="73b04-120">Passare alla directory contenente il codice di esempio.</span><span class="sxs-lookup"><span data-stu-id="73b04-120">Change to the directory that contains the sample code.</span></span>

```bash
cd nodejs-docs-hello-world
```

## <a name="run-the-app-locally"></a><span data-ttu-id="73b04-121">Eseguire l'app in locale</span><span class="sxs-lookup"><span data-stu-id="73b04-121">Run the app locally</span></span>

<span data-ttu-id="73b04-122">Per eseguire l'applicazione in locale, aprire una finestra del terminale e usare lo script `npm start` per avviare il server HTTP Node.js predefinito.</span><span class="sxs-lookup"><span data-stu-id="73b04-122">Run the application locally by opening a terminal window and using the `npm start` script to launch the built in Node.js HTTP server.</span></span>

```bash
npm start
```

<span data-ttu-id="73b04-123">Aprire un Web browser e passare all'app di esempio all'indirizzo http://localhost:1337.</span><span class="sxs-lookup"><span data-stu-id="73b04-123">Open a web browser, and navigate to the sample app at http://localhost:1337.</span></span>

<span data-ttu-id="73b04-124">Nella pagina verrà visualizzato il messaggio **Hello World** dell'app di esempio.</span><span class="sxs-lookup"><span data-stu-id="73b04-124">You see the **Hello World** message from the sample app displayed in the page.</span></span>

![App di esempio in esecuzione in locale](media/app-service-web-get-started-nodejs-poc/localhost-hello-world-in-browser.png)

<span data-ttu-id="73b04-126">Nella finestra del terminale premere **CTRL+C** per uscire dal server Web.</span><span class="sxs-lookup"><span data-stu-id="73b04-126">In your terminal window, press **Ctrl+C** to exit the web server.</span></span>

[!INCLUDE [Log in to Azure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Pagina dell'app Web vuota](media/app-service-web-get-started-php/app-service-web-service-created.png)

<span data-ttu-id="73b04-128">È stata creata una nuova app Web vuota in Azure.</span><span class="sxs-lookup"><span data-stu-id="73b04-128">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push to Azure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 23, done.
Delta compression using up to 4 threads.
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
remote: Node.js versions available on the platform are: 4.4.7, 4.5.0, 6.2.2, 6.6.0, 6.9.1.
remote: Selected node.js version 6.9.1. Use package.json file to choose a different version.
remote: Selected npm version 3.10.8
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
To https://<app_name>.scm.azurewebsites.net:443/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-to-the-app"></a><span data-ttu-id="73b04-129">Passare all'app</span><span class="sxs-lookup"><span data-stu-id="73b04-129">Browse to the app</span></span>

<span data-ttu-id="73b04-130">Passare all'applicazione distribuita con il Web browser.</span><span class="sxs-lookup"><span data-stu-id="73b04-130">Browse to the deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="73b04-131">Il codice di esempio Node.js è in esecuzione in un'app Web del servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="73b04-131">The Node.js sample code is running in an Azure App Service web app.</span></span>

![App di esempio in esecuzione in Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="73b04-133">**Congratulazioni.**</span><span class="sxs-lookup"><span data-stu-id="73b04-133">**Congratulations!**</span></span> <span data-ttu-id="73b04-134">La distribuzione della prima app Node.js nel servizio app è stata completata.</span><span class="sxs-lookup"><span data-stu-id="73b04-134">You've deployed your first Node.js app to App Service.</span></span>

## <a name="update-and-redeploy-the-code"></a><span data-ttu-id="73b04-135">Aggiornare e ridistribuire il codice</span><span class="sxs-lookup"><span data-stu-id="73b04-135">Update and redeploy the code</span></span>

<span data-ttu-id="73b04-136">Usando un editor di testo, aprire il file `index.js` nell'app Node.js e apportare una piccola modifica al testo nella chiamata a `response.end`:</span><span class="sxs-lookup"><span data-stu-id="73b04-136">Using a text editor, open the `index.js` file in the Node.js app, and make a small change to the text in the call to `response.end`:</span></span>

```nodejs
response.end("Hello Azure!");
```

<span data-ttu-id="73b04-137">Eseguire il commit delle modifiche in Git e quindi effettuare il push delle modifiche al codice in Azure.</span><span class="sxs-lookup"><span data-stu-id="73b04-137">Commit your changes in Git, and then push the code changes to Azure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="73b04-138">Al termine della distribuzione, tornare alla finestra del browser aperta nel passaggio **Passare all'app** e fare clic su Aggiorna.</span><span class="sxs-lookup"><span data-stu-id="73b04-138">Once deployment has completed, switch back to the browser window that opened in the **Browse to the app** step, and hit refresh.</span></span>

![App di esempio aggiornata in esecuzione in Azure](media/app-service-web-get-started-nodejs-poc/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="73b04-140">Gestire la nuova app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="73b04-140">Manage your new Azure web app</span></span>

<span data-ttu-id="73b04-141">Accedere al <a href="https://portal.azure.com" target="_blank">portale di Azure</a> per gestire l'app Web creata.</span><span class="sxs-lookup"><span data-stu-id="73b04-141">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span></span>

<span data-ttu-id="73b04-142">Nel menu a sinistra fare clic su **Servizi app** e quindi sul nome dell'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="73b04-142">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Passare all'app Web di Azure nel portale](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="73b04-144">Verrà visualizzata la pagina di panoramica dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="73b04-144">You see your web app's Overview page.</span></span> <span data-ttu-id="73b04-145">Qui è possibile eseguire attività di gestione di base come l'esplorazione, l'arresto, l'avvio, il riavvio e l'eliminazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="73b04-145">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Pannello del servizio app nel portale di Azure](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="73b04-147">Il menu a sinistra fornisce varie pagine per la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="73b04-147">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="73b04-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="73b04-148">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="73b04-149">Node.js con MongoDB</span><span class="sxs-lookup"><span data-stu-id="73b04-149">Node.js with MongoDB</span></span>](app-service-web-tutorial-nodejs-mongodb-app.md)
