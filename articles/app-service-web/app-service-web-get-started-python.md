---
title: Creare un'app Web Python in Azure | Microsoft Docs
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
ms.openlocfilehash: 119f9770097c010cc360e0e204d06a307a268814
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-python-web-app-in-azure"></a><span data-ttu-id="59859-103">Creare un'app Web Python in Azure</span><span class="sxs-lookup"><span data-stu-id="59859-103">Create a Python web app in Azure</span></span>

<span data-ttu-id="59859-104">Le [app Web di Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) forniscono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione.</span><span class="sxs-lookup"><span data-stu-id="59859-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="59859-105">Questa guida introduttiva illustra come sviluppare e distribuire un'app Python in un'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="59859-105">This quickstart walks through how to develop and deploy a Python app to Azure Web Apps.</span></span> <span data-ttu-id="59859-106">Si creerà l'app Web usando l'[interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) e si userà Git per distribuire il codice Python di esempio nell'app Web.</span><span class="sxs-lookup"><span data-stu-id="59859-106">You create the web app using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git to deploy sample Python code to the web app.</span></span>

![App di esempio in esecuzione in Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

<span data-ttu-id="59859-108">È possibile eseguire queste procedure con un computer Mac, Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="59859-108">You can follow the steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="59859-109">Una volta installati i prerequisiti, sono necessari circa cinque minuti per completare la procedura.</span><span class="sxs-lookup"><span data-stu-id="59859-109">Once the prerequisites are installed, it takes about five minutes to complete the steps.</span></span>
## <a name="prerequisites"></a><span data-ttu-id="59859-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="59859-110">Prerequisites</span></span>

<span data-ttu-id="59859-111">Per completare questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="59859-111">To complete this tutorial:</span></span>

1. [<span data-ttu-id="59859-112">Installare Git</span><span class="sxs-lookup"><span data-stu-id="59859-112">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="59859-113">Installare Python</span><span class="sxs-lookup"><span data-stu-id="59859-113">Install Python</span></span>](https://www.python.org/downloads/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="59859-114">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="59859-114">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="59859-115">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="59859-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="59859-116">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="59859-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-the-sample"></a><span data-ttu-id="59859-117">Scaricare l'esempio</span><span class="sxs-lookup"><span data-stu-id="59859-117">Download the sample</span></span>

<span data-ttu-id="59859-118">In una finestra del terminale eseguire il comando seguente per clonare il repository dell'app di esempio nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="59859-118">In a terminal window, run the following command to clone the sample app repository to your local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/python-docs-hello-world
```

<span data-ttu-id="59859-119">Questa finestra del terminale dovrà essere usata per eseguire tutti i comandi presenti in questa guida introduttiva.</span><span class="sxs-lookup"><span data-stu-id="59859-119">You use this terminal window to run all the commands in this quickstart.</span></span>

<span data-ttu-id="59859-120">Passare alla directory contenente il codice di esempio.</span><span class="sxs-lookup"><span data-stu-id="59859-120">Change to the directory that contains the sample code.</span></span>

```bash
cd Python-docs-hello-world
```

## <a name="run-the-app-locally"></a><span data-ttu-id="59859-121">Eseguire l'app in locale</span><span class="sxs-lookup"><span data-stu-id="59859-121">Run the app locally</span></span>

<span data-ttu-id="59859-122">Installare i pacchetti necessari tramite `pip`.</span><span class="sxs-lookup"><span data-stu-id="59859-122">Install the required packages using `pip`.</span></span>

```bash
pip install -r requirements.txt
```

<span data-ttu-id="59859-123">Per eseguire l'applicazione in locale, aprire una finestra del terminale e usare il comando `Python` per avviare il server Web Python predefinito.</span><span class="sxs-lookup"><span data-stu-id="59859-123">Run the application locally by opening a terminal window and using the `Python` command to launch the built-in Python web server.</span></span>

```bash
python main.py
```

<span data-ttu-id="59859-124">Aprire un Web browser e passare all'app di esempio all'indirizzo http://localhost:5000.</span><span class="sxs-lookup"><span data-stu-id="59859-124">Open a web browser, and navigate to the sample app at http://localhost:5000.</span></span>

<span data-ttu-id="59859-125">Nella pagina verrà visualizzato il messaggio **Hello World** dell'app di esempio.</span><span class="sxs-lookup"><span data-stu-id="59859-125">You can see the **Hello World** message from the sample app displayed in the page.</span></span>

![App di esempio in esecuzione in locale](media/app-service-web-get-started-python/localhost-hello-world-in-browser.png)

<span data-ttu-id="59859-127">Nella finestra del terminale premere **CTRL+C** per uscire dal server Web.</span><span class="sxs-lookup"><span data-stu-id="59859-127">In your terminal window, press **Ctrl+C** to exit the web server.</span></span>

[!INCLUDE [Log in to Azure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Pagina dell'app Web vuota](media/app-service-web-get-started-python/app-service-web-service-created.png)

<span data-ttu-id="59859-129">È stata creata una nuova app Web vuota in Azure.</span><span class="sxs-lookup"><span data-stu-id="59859-129">You’ve created an empty new web app in Azure.</span></span>

## <a name="configure-to-use-python"></a><span data-ttu-id="59859-130">Eseguire la configurazione per usare Python</span><span class="sxs-lookup"><span data-stu-id="59859-130">Configure to use Python</span></span>

<span data-ttu-id="59859-131">Usare il comando [az webapp config set](/cli/azure/webapp/config#set) per configurare l'app Web per l'uso di Python versione `3.4`.</span><span class="sxs-lookup"><span data-stu-id="59859-131">Use the [az webapp config set](/cli/azure/webapp/config#set) command to configure the web app to use Python version `3.4`.</span></span>

```azurecli-interactive
az webapp config set --python-version 3.4 --name <app_name> --resource-group myResourceGroup
```


<span data-ttu-id="59859-132">Per impostare la versione Python in questo modo viene usato un contenitore predefinito fornito dalla piattaforma.</span><span class="sxs-lookup"><span data-stu-id="59859-132">Setting the Python version this way uses a default container provided by the platform.</span></span> <span data-ttu-id="59859-133">Per usare un contenitore personalizzato, vedere il riferimento sull'interfaccia della riga di comando per il comando [az webapp config container set](/cli/azure/webapp/config/container#set).</span><span class="sxs-lookup"><span data-stu-id="59859-133">To use your own container, see the CLI reference for the [az webapp config container set](/cli/azure/webapp/config/container#set) command.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push to Azure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 18, done.
Delta compression using up to 4 threads.
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
To https://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-to-the-app"></a><span data-ttu-id="59859-134">Passare all'app</span><span class="sxs-lookup"><span data-stu-id="59859-134">Browse to the app</span></span>

<span data-ttu-id="59859-135">Passare all'applicazione distribuita con il Web browser.</span><span class="sxs-lookup"><span data-stu-id="59859-135">Browse to the deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="59859-136">Il codice di esempio Python è in esecuzione in un'app Web del servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="59859-136">The Python sample code is running in an Azure App Service web app.</span></span>

![App di esempio in esecuzione in Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

<span data-ttu-id="59859-138">**Congratulazioni.**</span><span class="sxs-lookup"><span data-stu-id="59859-138">**Congratulations!**</span></span> <span data-ttu-id="59859-139">La distribuzione della prima app Python nel servizio app è stata completata.</span><span class="sxs-lookup"><span data-stu-id="59859-139">You've deployed your first Python app to App Service.</span></span>

## <a name="update-and-redeploy-the-code"></a><span data-ttu-id="59859-140">Aggiornare e ridistribuire il codice</span><span class="sxs-lookup"><span data-stu-id="59859-140">Update and redeploy the code</span></span>

<span data-ttu-id="59859-141">Usando un editor di testo locale, aprire il file `main.py` nell'app Python e apportare una piccola modifica al testo accanto all'istruzione `return`:</span><span class="sxs-lookup"><span data-stu-id="59859-141">Using a local text editor, open the `main.py` file in the Python app, and make a small change to the text next to the `return` statement:</span></span>

```python
return 'Hello, Azure!'
```

<span data-ttu-id="59859-142">Eseguire il commit delle modifiche in Git e quindi effettuare il push delle modifiche al codice in Azure.</span><span class="sxs-lookup"><span data-stu-id="59859-142">Commit your changes in Git, and then push the code changes to Azure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="59859-143">Al termine della distribuzione, tornare alla finestra del browser aperta nel passaggio [Passare all'app](#browse-to-the-app) e aggiornare la pagina.</span><span class="sxs-lookup"><span data-stu-id="59859-143">Once deployment has completed, switch back to the browser window that opened in the [Browse to the app](#browse-to-the-app) step, and refresh the page.</span></span>

![App di esempio aggiornata in esecuzione in Azure](media/app-service-web-get-started-python/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="59859-145">Gestire la nuova app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="59859-145">Manage your new Azure web app</span></span>

<span data-ttu-id="59859-146">Accedere al <a href="https://portal.azure.com" target="_blank">portale di Azure</a> per gestire l'app Web creata.</span><span class="sxs-lookup"><span data-stu-id="59859-146">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span></span>

<span data-ttu-id="59859-147">Nel menu a sinistra fare clic su **Servizi app** e quindi sul nome dell'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="59859-147">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Passare all'app Web di Azure nel portale](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="59859-149">Verrà visualizzata la pagina di panoramica dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="59859-149">You see your web app's Overview page.</span></span> <span data-ttu-id="59859-150">Qui è possibile eseguire attività di gestione di base come l'esplorazione, l'arresto, l'avvio, il riavvio e l'eliminazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="59859-150">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Pannello del servizio app nel portale di Azure](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="59859-152">Il menu a sinistra fornisce varie pagine per la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="59859-152">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="59859-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="59859-153">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="59859-154">Python con PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="59859-154">Python with PostgreSQL</span></span>](app-service-web-tutorial-docker-python-postgresql-app.md)
