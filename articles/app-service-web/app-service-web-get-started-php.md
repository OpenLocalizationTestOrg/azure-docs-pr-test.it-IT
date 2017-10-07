---
title: aaaCreate PHP web app in Azure | Documenti Microsoft
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
ms.openlocfilehash: 8e1022889ca162f8f15ce7435cc9393cc6efef06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-web-app-in-azure"></a><span data-ttu-id="7cd79-103">Creare un'app Web PHP in Azure</span><span class="sxs-lookup"><span data-stu-id="7cd79-103">Create a PHP web app in Azure</span></span>

<span data-ttu-id="7cd79-104">Le [app Web di Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) forniscono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione.</span><span class="sxs-lookup"><span data-stu-id="7cd79-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="7cd79-105">Questa esercitazione Guida introduttiva viene illustrato come toodeploy un tooAzure app PHP App Web.</span><span class="sxs-lookup"><span data-stu-id="7cd79-105">This quickstart tutorial shows how toodeploy a PHP app tooAzure Web Apps.</span></span> <span data-ttu-id="7cd79-106">Si crea app web hello utilizzando hello [CLI di Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) nella Shell di Cloud e si usa Git toodeploy esempio PHP codice toohello web app.</span><span class="sxs-lookup"><span data-stu-id="7cd79-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) in Cloud Shell, and you use Git toodeploy sample PHP code toohello web app.</span></span>

<span data-ttu-id="7cd79-107">![App di esempio in esecuzione in Azure]](media/app-service-web-get-started-php/hello-world-in-browser.png)</span><span class="sxs-lookup"><span data-stu-id="7cd79-107">![Sample app running in Azure]](media/app-service-web-get-started-php/hello-world-in-browser.png)</span></span>

<span data-ttu-id="7cd79-108">È possibile eseguire operazioni di hello seguenti utilizzando un computer Mac, Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="7cd79-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="7cd79-109">Una volta installati i prerequisiti di hello, sono necessari circa cinque minuti toocomplete passaggi hello.</span><span class="sxs-lookup"><span data-stu-id="7cd79-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7cd79-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7cd79-110">Prerequisites</span></span>

<span data-ttu-id="7cd79-111">toocomplete questa Guida rapida:</span><span class="sxs-lookup"><span data-stu-id="7cd79-111">toocomplete this quickstart:</span></span>

* [<span data-ttu-id="7cd79-112">Installare Git</span><span class="sxs-lookup"><span data-stu-id="7cd79-112">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="7cd79-113">Installare PHP</span><span class="sxs-lookup"><span data-stu-id="7cd79-113">Install PHP</span></span>](https://php.net)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample-locally"></a><span data-ttu-id="7cd79-114">Scaricare l'esempio hello in locale</span><span class="sxs-lookup"><span data-stu-id="7cd79-114">Download hello sample locally</span></span>

<span data-ttu-id="7cd79-115">In una finestra terminale, eseguire hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="7cd79-115">In a terminal window, run hello following commands.</span></span> <span data-ttu-id="7cd79-116">Verrà Clona macchina locale tooyour hello esempio applicazione e spostarsi nel codice di esempio di toohello directory contenitore hello.</span><span class="sxs-lookup"><span data-stu-id="7cd79-116">This will clone hello sample application tooyour local machine, and navigate toohello directory containing hello sample code.</span></span>

```bash
git clone https://github.com/Azure-Samples/php-docs-hello-world
cd php-docs-hello-world
```

## <a name="run-hello-app-locally"></a><span data-ttu-id="7cd79-117">Eseguire app hello in locale</span><span class="sxs-lookup"><span data-stu-id="7cd79-117">Run hello app locally</span></span>

<span data-ttu-id="7cd79-118">Eseguire un'applicazione hello in locale, aprire una finestra terminale e utilizzare hello `php` comando toolaunch hello PHP server web predefinito.</span><span class="sxs-lookup"><span data-stu-id="7cd79-118">Run hello application locally by opening a terminal window and using hello `php` command toolaunch hello built-in PHP web server.</span></span>

```bash
php -S localhost:8080
```

<span data-ttu-id="7cd79-119">Aprire un web browser e passare l'app di esempio toohello in http://localhost:8080.</span><span class="sxs-lookup"><span data-stu-id="7cd79-119">Open a web browser, and navigate toohello sample app at http://localhost:8080.</span></span>

<span data-ttu-id="7cd79-120">Vedrai hello **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="7cd79-120">You see hello **Hello World!**</span></span> <span data-ttu-id="7cd79-121">messaggio dall'applicazione di esempio hello visualizzato nella pagina hello.</span><span class="sxs-lookup"><span data-stu-id="7cd79-121">message from hello sample app displayed in hello page.</span></span>

![App di esempio in esecuzione in locale](media/app-service-web-get-started-php/localhost-hello-world-in-browser.png)

<span data-ttu-id="7cd79-123">Nella finestra del terminale, premere **Ctrl + C** server web di tooexit hello.</span><span class="sxs-lookup"><span data-stu-id="7cd79-123">In your terminal window, press **Ctrl+C** tooexit hello web server.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)]

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)]

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)]

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)]

![Pagina dell'app Web vuota](media/app-service-web-get-started-php/app-service-web-service-created.png)

<span data-ttu-id="7cd79-125">È stata creata una nuova app Web vuota in Azure.</span><span class="sxs-lookup"><span data-stu-id="7cd79-125">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 2, done.
Delta compression using up too4 threads.
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
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
   cc39b1e..25f1805  master -> master
```

## <a name="browse-toohello-app-locally"></a><span data-ttu-id="7cd79-126">Esplorare app toohello localmente</span><span class="sxs-lookup"><span data-stu-id="7cd79-126">Browse toohello app locally</span></span>

<span data-ttu-id="7cd79-127">Sfoglia toohello distribuito l'applicazione tramite il web browser.</span><span class="sxs-lookup"><span data-stu-id="7cd79-127">Browse toohello deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="7cd79-128">codice di esempio PHP Hello è in esecuzione in un'applicazione web di servizio App di Azure.</span><span class="sxs-lookup"><span data-stu-id="7cd79-128">hello PHP sample code is running in an Azure App Service web app.</span></span>

![App di esempio in esecuzione in Azure](media/app-service-web-get-started-php/hello-world-in-browser.png)

<span data-ttu-id="7cd79-130">**Congratulazioni.**</span><span class="sxs-lookup"><span data-stu-id="7cd79-130">**Congratulations!**</span></span> <span data-ttu-id="7cd79-131">Il primo tooApp di app PHP servizio distribuiti.</span><span class="sxs-lookup"><span data-stu-id="7cd79-131">You've deployed your first PHP app tooApp Service.</span></span>

## <a name="update-locally-and-redeploy-hello-code"></a><span data-ttu-id="7cd79-132">In locale e ridistribuire codice hello</span><span class="sxs-lookup"><span data-stu-id="7cd79-132">Update locally and redeploy hello code</span></span>

<span data-ttu-id="7cd79-133">Utilizzare un editor di testo locale, aprire hello `index.php` file all'interno di app PHP hello e consente di applicare un piccola modifica toohello testo all'interno di stringa hello accanto troppo`echo`:</span><span class="sxs-lookup"><span data-stu-id="7cd79-133">Using a local text editor, open hello `index.php` file within hello PHP app, and make a small change toohello text within hello string next too`echo`:</span></span>

```php
echo "Hello Azure!";
```

<span data-ttu-id="7cd79-134">Eseguire il commit delle modifiche in Git e quindi push tooAzure modifiche di codice hello.</span><span class="sxs-lookup"><span data-stu-id="7cd79-134">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="7cd79-135">Una volta completata la distribuzione, passare toohello indietro finestra del browser aperto in hello **Sfoglia toohello app** passaggio e aggiornare la pagina hello.</span><span class="sxs-lookup"><span data-stu-id="7cd79-135">Once deployment has completed, switch back toohello browser window that opened in hello **Browse toohello app** step, and refresh hello page.</span></span>

![App di esempio aggiornata in esecuzione in Azure](media/app-service-web-get-started-php/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="7cd79-137">Gestire la nuova app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="7cd79-137">Manage your new Azure web app</span></span>

<span data-ttu-id="7cd79-138">Passare toohello <a href="https://portal.azure.com" target="_blank">portale di Azure</a> toomanage hello web app è stato creato.</span><span class="sxs-lookup"><span data-stu-id="7cd79-138">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="7cd79-139">Scegliere dal menu a sinistra hello **servizi App**, quindi fare clic su nome hello dell'app web di Azure.</span><span class="sxs-lookup"><span data-stu-id="7cd79-139">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Spostamento del portale tooAzure web app](./media/app-service-web-get-started-php/php-docs-hello-world-app-service-list.png)

<span data-ttu-id="7cd79-141">Verrà visualizzata la pagina di panoramica dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="7cd79-141">You see your web app's Overview page.</span></span> <span data-ttu-id="7cd79-142">Qui è possibile eseguire attività di gestione di base come l'esplorazione, l'arresto, l'avvio, il riavvio e l'eliminazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="7cd79-142">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span>

![Pannello del servizio app nel portale di Azure](media/app-service-web-get-started-php/php-docs-hello-world-app-service-detail.png)

<span data-ttu-id="7cd79-144">menu a sinistra di Hello fornisce diverse pagine di configurazione app.</span><span class="sxs-lookup"><span data-stu-id="7cd79-144">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="7cd79-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7cd79-145">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7cd79-146">PHP con MySQL</span><span class="sxs-lookup"><span data-stu-id="7cd79-146">PHP with MySQL</span></span>](app-service-web-tutorial-php-mysql.md)
