---
title: aaaCreate un'app web Python in Azure | Documenti Microsoft
description: Distribuire la prima app Python Hello World in un'app Web del servizio app di Azure in pochi minuti.
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 928ee2e5-6143-4c0c-8546-366f5a3d80ce
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 03/17/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 42178d490d8aa8eaf93710667aad598794c62c8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-python-web-app-in-azure"></a><span data-ttu-id="1ee64-103">Creare un'app Web Python in Azure</span><span class="sxs-lookup"><span data-stu-id="1ee64-103">Create a Python web app in Azure</span></span>

<span data-ttu-id="1ee64-104">Le [app Web di Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) forniscono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione.</span><span class="sxs-lookup"><span data-stu-id="1ee64-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="1ee64-105">Questa Guida rapida illustra in dettaglio come toodevelop e distribuire un tooAzure app Python App Web.</span><span class="sxs-lookup"><span data-stu-id="1ee64-105">This quickstart walks through how toodevelop and deploy a Python app tooAzure Web Apps.</span></span> <span data-ttu-id="1ee64-106">Si crea app web hello utilizzando hello [CLI di Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), e si usa Git toodeploy esempio Python codice toohello web app.</span><span class="sxs-lookup"><span data-stu-id="1ee64-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git toodeploy sample Python code toohello web app.</span></span>

![App di esempio in esecuzione in Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

<span data-ttu-id="1ee64-108">È possibile eseguire operazioni di hello seguenti utilizzando un computer Mac, Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="1ee64-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="1ee64-109">Una volta installati i prerequisiti di hello, sono necessari circa cinque minuti toocomplete passaggi hello.</span><span class="sxs-lookup"><span data-stu-id="1ee64-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>
## <a name="prerequisites"></a><span data-ttu-id="1ee64-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1ee64-110">Prerequisites</span></span>

<span data-ttu-id="1ee64-111">toocomplete questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="1ee64-111">toocomplete this tutorial:</span></span>

1. [<span data-ttu-id="1ee64-112">Installare Git</span><span class="sxs-lookup"><span data-stu-id="1ee64-112">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="1ee64-113">Installare Python</span><span class="sxs-lookup"><span data-stu-id="1ee64-113">Install Python</span></span>](https://www.python.org/downloads/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="1ee64-114">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="1ee64-114">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="1ee64-115">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="1ee64-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="1ee64-116">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1ee64-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-hello-sample"></a><span data-ttu-id="1ee64-117">Scaricare l'esempio hello</span><span class="sxs-lookup"><span data-stu-id="1ee64-117">Download hello sample</span></span>

<span data-ttu-id="1ee64-118">In una finestra terminale, eseguire hello successivo comando tooclone hello esempio app repository tooyour computer locale.</span><span class="sxs-lookup"><span data-stu-id="1ee64-118">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/python-docs-hello-world
```

<span data-ttu-id="1ee64-119">Utilizzare questo toorun finestra terminale tutti i comandi di hello in questa Guida rapida.</span><span class="sxs-lookup"><span data-stu-id="1ee64-119">You use this terminal window toorun all hello commands in this quickstart.</span></span>

<span data-ttu-id="1ee64-120">Spostarsi nella directory toohello che contiene il codice di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="1ee64-120">Change toohello directory that contains hello sample code.</span></span>

```bash
cd Python-docs-hello-world
```

## <a name="run-hello-app-locally"></a><span data-ttu-id="1ee64-121">Eseguire app hello in locale</span><span class="sxs-lookup"><span data-stu-id="1ee64-121">Run hello app locally</span></span>

<span data-ttu-id="1ee64-122">Installare i pacchetti hello necessario utilizzando `pip`.</span><span class="sxs-lookup"><span data-stu-id="1ee64-122">Install hello required packages using `pip`.</span></span>

```bash
pip install -r requirements.txt
```

<span data-ttu-id="1ee64-123">Eseguire un'applicazione hello in locale, aprire una finestra terminale e utilizzare hello `Python` comando toolaunch hello Python server web predefinito.</span><span class="sxs-lookup"><span data-stu-id="1ee64-123">Run hello application locally by opening a terminal window and using hello `Python` command toolaunch hello built-in Python web server.</span></span>

```bash
python main.py
```

<span data-ttu-id="1ee64-124">Aprire un web browser e passare l'app di esempio toohello all'indirizzo http://localhost:5000/.</span><span class="sxs-lookup"><span data-stu-id="1ee64-124">Open a web browser, and navigate toohello sample app at http://localhost:5000.</span></span>

<span data-ttu-id="1ee64-125">È possibile visualizzare hello **Hello World** messaggio dall'applicazione di esempio hello visualizzato nella pagina hello.</span><span class="sxs-lookup"><span data-stu-id="1ee64-125">You can see hello **Hello World** message from hello sample app displayed in hello page.</span></span>

![App di esempio in esecuzione in locale](media/app-service-web-get-started-python/localhost-hello-world-in-browser.png)

<span data-ttu-id="1ee64-127">Nella finestra del terminale, premere **Ctrl + C** server web di tooexit hello.</span><span class="sxs-lookup"><span data-stu-id="1ee64-127">In your terminal window, press **Ctrl+C** tooexit hello web server.</span></span>

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Pagina dell'app Web vuota](media/app-service-web-get-started-python/app-service-web-service-created.png)

<span data-ttu-id="1ee64-129">È stata creata una nuova app Web vuota in Azure.</span><span class="sxs-lookup"><span data-stu-id="1ee64-129">You’ve created an empty new web app in Azure.</span></span>

## <a name="configure-toouse-python"></a><span data-ttu-id="1ee64-130">Configurare toouse Python</span><span class="sxs-lookup"><span data-stu-id="1ee64-130">Configure toouse Python</span></span>

<span data-ttu-id="1ee64-131">Hello utilizzare [az webapp config set](/cli/azure/webapp/config#set) versione di Python di comando tooconfigure hello web app toouse `3.4`.</span><span class="sxs-lookup"><span data-stu-id="1ee64-131">Use hello [az webapp config set](/cli/azure/webapp/config#set) command tooconfigure hello web app toouse Python version `3.4`.</span></span>

```azurecli-interactive
az webapp config set --python-version 3.4 --name <app_name> --resource-group myResourceGroup
```


<span data-ttu-id="1ee64-132">L'impostazione di tale versione di Python hello utilizza un contenitore predefinito fornito dalla piattaforma hello.</span><span class="sxs-lookup"><span data-stu-id="1ee64-132">Setting hello Python version this way uses a default container provided by hello platform.</span></span> <span data-ttu-id="1ee64-133">toouse contenitore, vedere hello riferimento CLI per hello [az webapp configurazione contenitore set](/cli/azure/webapp/config/container#set) comando.</span><span class="sxs-lookup"><span data-stu-id="1ee64-133">toouse your own container, see hello CLI reference for hello [az webapp config container set](/cli/azure/webapp/config/container#set) command.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 18, done.
Delta compression using up too4 threads.
Compressing objects: 100% (16/16), done.
Writing objects: 100% (18/18), 4.31 KiB | 0 bytes/s, done.
Total 18 (delta 4), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '44e74fe7dd'.
remote: Generating deployment script.
remote: Generating deployment script for python Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling python deployment.
remote: KuduSync.NET from: 'D:\home\site\repository' to: 'D:\home\site\wwwroot'
remote: Deleting file: 'hostingstart.html'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'main.py'
remote: Copying file: 'README.md'
remote: Copying file: 'requirements.txt'
remote: Copying file: 'virtualenv_proxy.py'
remote: Copying file: 'web.2.7.config'
remote: Copying file: 'web.3.4.config'
remote: Detected requirements.txt.  You can skip Python specific steps with a .skipPythonDeployment file.
remote: Detecting Python runtime from site configuration
remote: Detected python-3.4
remote: Creating python-3.4 virtual environment.
remote: .................................
remote: Pip install requirements.
remote: Successfully installed Flask click itsdangerous Jinja2 Werkzeug MarkupSafe
remote: Cleaning up...
remote: .
remote: Overwriting web.config with web.3.4.config
remote:         1 file(s) copied.
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a><span data-ttu-id="1ee64-134">Esplorare app toohello</span><span class="sxs-lookup"><span data-stu-id="1ee64-134">Browse toohello app</span></span>

<span data-ttu-id="1ee64-135">Sfoglia toohello distribuito l'applicazione tramite il web browser.</span><span class="sxs-lookup"><span data-stu-id="1ee64-135">Browse toohello deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="1ee64-136">esempio di codice Python Hello è in esecuzione in un'applicazione web di servizio App di Azure.</span><span class="sxs-lookup"><span data-stu-id="1ee64-136">hello Python sample code is running in an Azure App Service web app.</span></span>

![App di esempio in esecuzione in Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

<span data-ttu-id="1ee64-138">**Congratulazioni.**</span><span class="sxs-lookup"><span data-stu-id="1ee64-138">**Congratulations!**</span></span> <span data-ttu-id="1ee64-139">Il primo tooApp di app Python servizio distribuiti.</span><span class="sxs-lookup"><span data-stu-id="1ee64-139">You've deployed your first Python app tooApp Service.</span></span>

## <a name="update-and-redeploy-hello-code"></a><span data-ttu-id="1ee64-140">Aggiornare e ridistribuire codice hello</span><span class="sxs-lookup"><span data-stu-id="1ee64-140">Update and redeploy hello code</span></span>

<span data-ttu-id="1ee64-141">Utilizzare un editor di testo locale, aprire hello `main.py` file nell'app Python hello e verificare un toohello di modifica di piccole dimensioni toohello testo successivo `return` istruzione:</span><span class="sxs-lookup"><span data-stu-id="1ee64-141">Using a local text editor, open hello `main.py` file in hello Python app, and make a small change toohello text next toohello `return` statement:</span></span>

```python
return 'Hello, Azure!'
```

<span data-ttu-id="1ee64-142">Eseguire il commit delle modifiche in Git e quindi push tooAzure modifiche di codice hello.</span><span class="sxs-lookup"><span data-stu-id="1ee64-142">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="1ee64-143">Una volta completata la distribuzione, passare toohello indietro finestra del browser aperto in hello [Sfoglia toohello app](#browse-to-the-app) passaggio e aggiornare la pagina hello.</span><span class="sxs-lookup"><span data-stu-id="1ee64-143">Once deployment has completed, switch back toohello browser window that opened in hello [Browse toohello app](#browse-to-the-app) step, and refresh hello page.</span></span>

![App di esempio aggiornata in esecuzione in Azure](media/app-service-web-get-started-python/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="1ee64-145">Gestire la nuova app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="1ee64-145">Manage your new Azure web app</span></span>

<span data-ttu-id="1ee64-146">Passare toohello <a href="https://portal.azure.com" target="_blank">portale di Azure</a> toomanage hello web app è stato creato.</span><span class="sxs-lookup"><span data-stu-id="1ee64-146">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="1ee64-147">Scegliere dal menu a sinistra hello **servizi App**, quindi fare clic su nome hello dell'app web di Azure.</span><span class="sxs-lookup"><span data-stu-id="1ee64-147">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Spostamento del portale tooAzure web app](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="1ee64-149">Verrà visualizzata la pagina di panoramica dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="1ee64-149">You see your web app's Overview page.</span></span> <span data-ttu-id="1ee64-150">Qui è possibile eseguire attività di gestione di base come l'esplorazione, l'arresto, l'avvio, il riavvio e l'eliminazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="1ee64-150">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Pannello del servizio app nel portale di Azure](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="1ee64-152">menu a sinistra di Hello fornisce diverse pagine di configurazione app.</span><span class="sxs-lookup"><span data-stu-id="1ee64-152">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="1ee64-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1ee64-153">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1ee64-154">Python con PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="1ee64-154">Python with PostgreSQL</span></span>](app-service-web-tutorial-docker-python-postgresql-app.md)
