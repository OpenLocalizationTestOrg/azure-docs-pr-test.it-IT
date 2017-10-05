---
title: Creare un'app Web PHP in Azure | Microsoft Docs
description: Distribuire la prima app PHP Hello World in un'app Web del servizio app di Azure in pochi minuti.
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 07/21/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 3a78e0b485046ad6228bf4819d3908042c298d1a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-php-web-app-in-azure"></a><span data-ttu-id="1cba8-103">Creare un'app Web PHP in Azure</span><span class="sxs-lookup"><span data-stu-id="1cba8-103">Create a PHP web app in Azure</span></span>

<span data-ttu-id="1cba8-104">Le [app Web di Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) forniscono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione.</span><span class="sxs-lookup"><span data-stu-id="1cba8-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="1cba8-105">Questa guida introduttiva illustra come distribuire un'app PHP in un'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="1cba8-105">This quickstart tutorial shows how to deploy a PHP app to Azure Web Apps.</span></span> <span data-ttu-id="1cba8-106">Si creerà l'app Web usando l'[interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) in Cloud Shell e si userà Git per distribuire il codice PHP di esempio nell'app Web.</span><span class="sxs-lookup"><span data-stu-id="1cba8-106">You create the web app using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) in Cloud Shell, and you use Git to deploy sample PHP code to the web app.</span></span>

<span data-ttu-id="1cba8-107">![App di esempio in esecuzione in Azure]](media/app-service-web-get-started-php/hello-world-in-browser.png)</span><span class="sxs-lookup"><span data-stu-id="1cba8-107">![Sample app running in Azure]](media/app-service-web-get-started-php/hello-world-in-browser.png)</span></span>

<span data-ttu-id="1cba8-108">È possibile eseguire queste procedure con un computer Mac, Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="1cba8-108">You can follow the steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="1cba8-109">Una volta installati i prerequisiti, sono necessari circa cinque minuti per completare la procedura.</span><span class="sxs-lookup"><span data-stu-id="1cba8-109">Once the prerequisites are installed, it takes about five minutes to complete the steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1cba8-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1cba8-110">Prerequisites</span></span>

<span data-ttu-id="1cba8-111">Per completare questa guida introduttiva:</span><span class="sxs-lookup"><span data-stu-id="1cba8-111">To complete this quickstart:</span></span>

* [<span data-ttu-id="1cba8-112">Installare Git</span><span class="sxs-lookup"><span data-stu-id="1cba8-112">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="1cba8-113">Installare PHP</span><span class="sxs-lookup"><span data-stu-id="1cba8-113">Install PHP</span></span>](https://php.net)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-the-sample-locally"></a><span data-ttu-id="1cba8-114">Scaricare l'esempio in locale</span><span class="sxs-lookup"><span data-stu-id="1cba8-114">Download the sample locally</span></span>

<span data-ttu-id="1cba8-115">Eseguire i comandi seguenti in una finestra del terminale.</span><span class="sxs-lookup"><span data-stu-id="1cba8-115">In a terminal window, run the following commands.</span></span> <span data-ttu-id="1cba8-116">L'applicazione di esempio verrà clonata nel computer locale e verrà visualizzata la directory contenente il codice di esempio.</span><span class="sxs-lookup"><span data-stu-id="1cba8-116">This will clone the sample application to your local machine, and navigate to the directory containing the sample code.</span></span>

```bash
git clone https://github.com/Azure-Samples/php-docs-hello-world
cd php-docs-hello-world
```

## <a name="run-the-app-locally"></a><span data-ttu-id="1cba8-117">Eseguire l'app in locale</span><span class="sxs-lookup"><span data-stu-id="1cba8-117">Run the app locally</span></span>

<span data-ttu-id="1cba8-118">Per eseguire l'applicazione in locale, aprire una finestra del terminale e usare il comando `php` per avviare il server Web PHP predefinito.</span><span class="sxs-lookup"><span data-stu-id="1cba8-118">Run the application locally by opening a terminal window and using the `php` command to launch the built-in PHP web server.</span></span>

```bash
php -S localhost:8080
```

<span data-ttu-id="1cba8-119">Aprire un Web browser e passare all'app di esempio all'indirizzo http://localhost:8080.</span><span class="sxs-lookup"><span data-stu-id="1cba8-119">Open a web browser, and navigate to the sample app at http://localhost:8080.</span></span>

<span data-ttu-id="1cba8-120">Nella pagina verrà visualizzato il messaggio **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="1cba8-120">You see the **Hello World!**</span></span> <span data-ttu-id="1cba8-121">dell'app di esempio.</span><span class="sxs-lookup"><span data-stu-id="1cba8-121">message from the sample app displayed in the page.</span></span>

![App di esempio in esecuzione in locale](media/app-service-web-get-started-php/localhost-hello-world-in-browser.png)

<span data-ttu-id="1cba8-123">Nella finestra del terminale premere **CTRL+C** per uscire dal server Web.</span><span class="sxs-lookup"><span data-stu-id="1cba8-123">In your terminal window, press **Ctrl+C** to exit the web server.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)]

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)]

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)]

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)]

![Pagina dell'app Web vuota](media/app-service-web-get-started-php/app-service-web-service-created.png)

<span data-ttu-id="1cba8-125">È stata creata una nuova app Web vuota in Azure.</span><span class="sxs-lookup"><span data-stu-id="1cba8-125">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push to Azure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 2, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 352 bytes | 0 bytes/s, done.
Total 2 (delta 1), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '25f18051e9'.
remote: Generating deployment script.
remote: Running deployment command...
remote: Handling Basic Web Site deployment.
remote: Kudu sync from: '/home/site/repository' to: '/home/site/wwwroot'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Copying file: 'index.php'
remote: Ignoring: .git
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
To https://<app_name>.scm.azurewebsites.net/<app_name>.git
   cc39b1e..25f1805  master -> master
```

## <a name="browse-to-the-app-locally"></a><span data-ttu-id="1cba8-126">Passare all'app in locale</span><span class="sxs-lookup"><span data-stu-id="1cba8-126">Browse to the app locally</span></span>

<span data-ttu-id="1cba8-127">Passare all'applicazione distribuita con il Web browser.</span><span class="sxs-lookup"><span data-stu-id="1cba8-127">Browse to the deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="1cba8-128">Il codice di esempio PHP è in esecuzione in un'app Web del servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="1cba8-128">The PHP sample code is running in an Azure App Service web app.</span></span>

![App di esempio in esecuzione in Azure](media/app-service-web-get-started-php/hello-world-in-browser.png)

<span data-ttu-id="1cba8-130">**Congratulazioni.**</span><span class="sxs-lookup"><span data-stu-id="1cba8-130">**Congratulations!**</span></span> <span data-ttu-id="1cba8-131">La distribuzione della prima app PHP nel servizio app è stata completata.</span><span class="sxs-lookup"><span data-stu-id="1cba8-131">You've deployed your first PHP app to App Service.</span></span>

## <a name="update-locally-and-redeploy-the-code"></a><span data-ttu-id="1cba8-132">Aggiornare e ridistribuire il codice in locale</span><span class="sxs-lookup"><span data-stu-id="1cba8-132">Update locally and redeploy the code</span></span>

<span data-ttu-id="1cba8-133">Usando un editor di testo locale, aprire il file `index.php` nell'app PHP e apportare una piccola modifica al testo nella stringa accanto a `echo`:</span><span class="sxs-lookup"><span data-stu-id="1cba8-133">Using a local text editor, open the `index.php` file within the PHP app, and make a small change to the text within the string next to `echo`:</span></span>

```php
echo "Hello Azure!";
```

<span data-ttu-id="1cba8-134">Eseguire il commit delle modifiche in Git e quindi effettuare il push delle modifiche al codice in Azure.</span><span class="sxs-lookup"><span data-stu-id="1cba8-134">Commit your changes in Git, and then push the code changes to Azure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="1cba8-135">Al termine della distribuzione, tornare alla finestra del browser aperta nel passaggio **Passare all'app** e aggiornare la pagina.</span><span class="sxs-lookup"><span data-stu-id="1cba8-135">Once deployment has completed, switch back to the browser window that opened in the **Browse to the app** step, and refresh the page.</span></span>

![App di esempio aggiornata in esecuzione in Azure](media/app-service-web-get-started-php/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="1cba8-137">Gestire la nuova app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="1cba8-137">Manage your new Azure web app</span></span>

<span data-ttu-id="1cba8-138">Accedere al <a href="https://portal.azure.com" target="_blank">portale di Azure</a> per gestire l'app Web creata.</span><span class="sxs-lookup"><span data-stu-id="1cba8-138">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span></span>

<span data-ttu-id="1cba8-139">Nel menu a sinistra fare clic su **Servizi app** e quindi sul nome dell'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="1cba8-139">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Passare all'app Web di Azure nel portale](./media/app-service-web-get-started-php/php-docs-hello-world-app-service-list.png)

<span data-ttu-id="1cba8-141">Verrà visualizzata la pagina di panoramica dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="1cba8-141">You see your web app's Overview page.</span></span> <span data-ttu-id="1cba8-142">Qui è possibile eseguire attività di gestione di base come l'esplorazione, l'arresto, l'avvio, il riavvio e l'eliminazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="1cba8-142">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span>

![Pannello del servizio app nel portale di Azure](media/app-service-web-get-started-php/php-docs-hello-world-app-service-detail.png)

<span data-ttu-id="1cba8-144">Il menu a sinistra fornisce varie pagine per la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="1cba8-144">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="1cba8-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1cba8-145">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1cba8-146">PHP con MySQL</span><span class="sxs-lookup"><span data-stu-id="1cba8-146">PHP with MySQL</span></span>](app-service-web-tutorial-php-mysql.md)
