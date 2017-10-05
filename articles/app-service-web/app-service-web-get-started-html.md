---
title: Creare un'app Web HTML statica in Azure | Microsoft Docs
description: Informazioni su come eseguire app Web nel servizio app di Azure mediante la distribuzione di un'app HTML statica di esempio.
services: app-service\web
documentationcenter: 
author: rick-anderson
manager: wpickett
editor: 
ms.assetid: 60495cc5-6963-4bf0-8174-52786d226c26
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 05/26/2017
ms.author: riande
ms.custom: mvc
ms.openlocfilehash: 42af5b08b8d2ff0c75fd73dcfa61c861647fd2c9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-static-html-web-app-in-azure"></a><span data-ttu-id="a4f95-103">Creare un'app Web HTML statica in Azure</span><span class="sxs-lookup"><span data-stu-id="a4f95-103">Create a static HTML web app in Azure</span></span>

<span data-ttu-id="a4f95-104">Le [app Web di Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) forniscono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione.</span><span class="sxs-lookup"><span data-stu-id="a4f95-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="a4f95-105">Questa guida introduttiva illustra come distribuire un sito HTML e CSS di base in un'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="a4f95-105">This quickstart shows how to deploy a basic HTML+CSS site to Azure Web Apps.</span></span> <span data-ttu-id="a4f95-106">Si creerà l'app Web usando l'[interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) e si userà Git per distribuire il contenuto HTML di esempio nell'app Web.</span><span class="sxs-lookup"><span data-stu-id="a4f95-106">You create the web app using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git to deploy sample HTML content to the web app.</span></span>

![Home page dell'app di esempio](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

<span data-ttu-id="a4f95-108">È possibile eseguire queste procedure con un computer Mac, Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="a4f95-108">You can follow the steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="a4f95-109">Una volta installati i prerequisiti, sono necessari circa cinque minuti per completare la procedura.</span><span class="sxs-lookup"><span data-stu-id="a4f95-109">Once the prerequisites are installed, it takes about five minutes to complete the steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4f95-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a4f95-110">Prerequisites</span></span>

<span data-ttu-id="a4f95-111">Per completare questa guida introduttiva:</span><span class="sxs-lookup"><span data-stu-id="a4f95-111">To complete this quickstart:</span></span>

- <span data-ttu-id="a4f95-112">[Installare Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]</span><span class="sxs-lookup"><span data-stu-id="a4f95-112">[Install Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a4f95-113">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="a4f95-113">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a4f95-114">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="a4f95-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="a4f95-115">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a4f95-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-the-sample"></a><span data-ttu-id="a4f95-116">Scaricare l'esempio</span><span class="sxs-lookup"><span data-stu-id="a4f95-116">Download the sample</span></span>

<span data-ttu-id="a4f95-117">In una finestra del terminale eseguire il comando seguente per clonare il repository dell'app di esempio nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="a4f95-117">In a terminal window, run the following command to clone the sample app repository to your local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/html-docs-hello-world.git
```

<span data-ttu-id="a4f95-118">Questa finestra del terminale dovrà essere usata per eseguire tutti i comandi presenti in questa guida introduttiva.</span><span class="sxs-lookup"><span data-stu-id="a4f95-118">You use this terminal window to run all the commands in this quickstart.</span></span>

## <a name="view-the-html"></a><span data-ttu-id="a4f95-119">Visualizzare il codice HTML</span><span class="sxs-lookup"><span data-stu-id="a4f95-119">View the HTML</span></span>

<span data-ttu-id="a4f95-120">Passare alla directory contenente il codice HTML di esempio.</span><span class="sxs-lookup"><span data-stu-id="a4f95-120">Navigate to the directory that contains the sample HTML.</span></span> <span data-ttu-id="a4f95-121">Aprire il file *index.html* nel browser.</span><span class="sxs-lookup"><span data-stu-id="a4f95-121">Open the *index.html* file in your browser.</span></span>

![Home page dell'app di esempio](media/app-service-web-get-started-html/hello-world-in-browser.png)

[!INCLUDE [Log in to Azure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Pagina dell'app Web vuota](media/app-service-web-get-started-html/app-service-web-service-created.png)

<span data-ttu-id="a4f95-124">È stata creata una nuova app Web vuota in Azure.</span><span class="sxs-lookup"><span data-stu-id="a4f95-124">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push to Azure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 13, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (11/11), done.
Writing objects: 100% (13/13), 2.07 KiB | 0 bytes/s, done.
Total 13 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'cc39b1e4cb'.
remote: Generating deployment script.
remote: Generating deployment script for Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling Basic Web Site deployment.
remote: KuduSync.NET from: 'D:\home\site\repository' to: 'D:\home\site\wwwroot'
remote: Deleting file: 'hostingstart.html'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
To https://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-to-the-app"></a><span data-ttu-id="a4f95-125">Passare all'app</span><span class="sxs-lookup"><span data-stu-id="a4f95-125">Browse to the app</span></span>

<span data-ttu-id="a4f95-126">In un browser passare all'URL dell'app Web di Azure:</span><span class="sxs-lookup"><span data-stu-id="a4f95-126">In a browser, go to the Azure web app URL:</span></span>

```
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="a4f95-127">La pagina è in esecuzione come un'app Web del servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="a4f95-127">The page is running as an Azure App Service web app.</span></span>

![Home page dell'app di esempio](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

<span data-ttu-id="a4f95-129">**Congratulazioni.**</span><span class="sxs-lookup"><span data-stu-id="a4f95-129">**Congratulations!**</span></span> <span data-ttu-id="a4f95-130">La distribuzione della prima app HTML nel Servizio app è stata completata.</span><span class="sxs-lookup"><span data-stu-id="a4f95-130">You've deployed your first HTML app to App Service.</span></span>

## <a name="update-and-redeploy-the-app"></a><span data-ttu-id="a4f95-131">Aggiornare e ridistribuire l'app</span><span class="sxs-lookup"><span data-stu-id="a4f95-131">Update and redeploy the app</span></span>

<span data-ttu-id="a4f95-132">Aprire il file *index.html* in un editor di testo e apportare una modifica al markup.</span><span class="sxs-lookup"><span data-stu-id="a4f95-132">Open the *index.html* file in a text editor, and make a change to the markup.</span></span> <span data-ttu-id="a4f95-133">Modificare ad esempio l'intestazione H1 da "Servizio app di Azure - Sito HTML statico di esempio" a "Servizio app di Azure".</span><span class="sxs-lookup"><span data-stu-id="a4f95-133">For example, change the H1 heading from "Azure App Service - Sample Static HTML Site" to just "Azure App Service\`.</span></span>

<span data-ttu-id="a4f95-134">Eseguire il commit delle modifiche in Git e quindi effettuare il push delle modifiche al codice in Azure.</span><span class="sxs-lookup"><span data-stu-id="a4f95-134">Commit your changes in Git, and then push the code changes to Azure.</span></span>

```bash
git commit -am "updated HTML"
git push azure master
```

<span data-ttu-id="a4f95-135">Al termine della distribuzione, aggiornare il browser per visualizzare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="a4f95-135">Once deployment has completed, refresh your browser to see the changes.</span></span>

![Home page dell'app di esempio aggiornata](media/app-service-web-get-started-html/hello-azure-in-browser-az.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="a4f95-137">Gestire la nuova app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="a4f95-137">Manage your new Azure web app</span></span>

<span data-ttu-id="a4f95-138">Accedere al <a href="https://portal.azure.com" target="_blank">portale di Azure</a> per gestire l'app Web creata.</span><span class="sxs-lookup"><span data-stu-id="a4f95-138">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span></span>

<span data-ttu-id="a4f95-139">Nel menu a sinistra fare clic su **Servizi app** e quindi sul nome dell'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="a4f95-139">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Passare all'app Web di Azure nel portale](./media/app-service-web-get-started-html/portal1.png)

<span data-ttu-id="a4f95-141">Verrà visualizzata la pagina di panoramica dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="a4f95-141">You see your web app's Overview page.</span></span> <span data-ttu-id="a4f95-142">Qui è possibile eseguire attività di gestione di base come l'esplorazione, l'arresto, l'avvio, il riavvio e l'eliminazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="a4f95-142">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Pannello del servizio app nel portale di Azure](./media/app-service-web-get-started-html/portal2.png)

<span data-ttu-id="a4f95-144">Il menu a sinistra fornisce varie pagine per la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="a4f95-144">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="a4f95-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a4f95-145">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a4f95-146">Eseguire il mapping di un dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="a4f95-146">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
