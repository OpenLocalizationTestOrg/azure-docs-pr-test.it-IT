---
title: Creare un'app Ruby con le App Web in Linux | Microsoft Docs
description: Informazioni su come creare app Ruby con app web in Linux.
keywords: servizio app di azure, linux, oss, ruby
services: app-service
documentationcenter: 
author: wesmc7777
manager: erikre
editor: 
ms.assetid: 6d00c73c-13cb-446f-8926-923db4101afa
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: wesmc;rachelap
ms.openlocfilehash: 17f3f1a2122c508501134a0c43ab6abce412fb44
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-ruby-app-with-web-apps-on-linux"></a><span data-ttu-id="a8f97-104">Creare un'app Ruby con le App Web in Linux</span><span class="sxs-lookup"><span data-stu-id="a8f97-104">Create a Ruby App with Web Apps on Linux</span></span> 

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="a8f97-105">Le [app Web di Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) forniscono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione.</span><span class="sxs-lookup"><span data-stu-id="a8f97-105">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="a8f97-106">In questa guida introduttiva viene illustrato come creare un'applicazione Ruby on Rails di base e quindi distribuirla in App Web di Azure in Linux.</span><span class="sxs-lookup"><span data-stu-id="a8f97-106">This quickstart shows you how to create a basic Ruby on Rails application you then deploy it to Azure as a Web App on Linux.</span></span>

![Hello-world](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

## <a name="prerequisites"></a><span data-ttu-id="a8f97-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a8f97-108">Prerequisites</span></span>

* <span data-ttu-id="a8f97-109">[Ruby 2.4.1 o versione successiva](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).</span><span class="sxs-lookup"><span data-stu-id="a8f97-109">[Ruby 2.4.1 or higher](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).</span></span>
* <span data-ttu-id="a8f97-110">[Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="a8f97-110">[Git](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="a8f97-111">Una [sottoscrizione di Azure attiva](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a8f97-111">An [active Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-the-sample"></a><span data-ttu-id="a8f97-112">Scaricare l'esempio</span><span class="sxs-lookup"><span data-stu-id="a8f97-112">Download the sample</span></span>

<span data-ttu-id="a8f97-113">In una finestra del terminale eseguire il comando seguente per clonare il repository dell'app di esempio nel computer locale:</span><span class="sxs-lookup"><span data-stu-id="a8f97-113">In a terminal window, run the following command to clone the sample app repository to your local machine:</span></span>

```bash
git clone https://github.com/Azure-Samples/ruby-docs-hello-world
```

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="run-the-application-locally"></a><span data-ttu-id="a8f97-114">Eseguire l'applicazione in locale</span><span class="sxs-lookup"><span data-stu-id="a8f97-114">Run the application locally</span></span>

<span data-ttu-id="a8f97-115">Eseguire il server della barra di scorrimento per il funzionamento dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a8f97-115">Run the rails server in order for the application to work.</span></span> <span data-ttu-id="a8f97-116">Passare alla directory *hello-world* e il comando `rails server` avvia il server.</span><span class="sxs-lookup"><span data-stu-id="a8f97-116">Change to the *hello-world* directory, and the `rails server` command starts the server.</span></span>

```bash
cd hello-world\bin
rails server
```
    
<span data-ttu-id="a8f97-117">Tramite il Web browser, passare a `http://localhost:3000` per testare l'app in locale.</span><span class="sxs-lookup"><span data-stu-id="a8f97-117">Using your web browser, navigate to `http://localhost:3000` to test the app locally.</span></span>    

![Hello-world](./media/app-service-linux-ruby-get-started/hello-world.png)

## <a name="modify-app-to-display-welcome-message"></a><span data-ttu-id="a8f97-119">Modificare l'app per visualizzare il messaggio di benvenuto</span><span class="sxs-lookup"><span data-stu-id="a8f97-119">Modify app to display welcome message</span></span>

<span data-ttu-id="a8f97-120">Modificare l'applicazione in modo da visualizzare un messaggio di benvenuto.</span><span class="sxs-lookup"><span data-stu-id="a8f97-120">Modify the application so it displays a welcome message.</span></span> <span data-ttu-id="a8f97-121">Modificare il controller dell'applicazione in modo che restituisca il messaggio in formato HTML nel browser.</span><span class="sxs-lookup"><span data-stu-id="a8f97-121">Change the application's controller so it returns the message as HTML to the browser.</span></span> 

<span data-ttu-id="a8f97-122">Aprire *~/workspace/hello-world/app/controllers/application_controller.rb* per la modifica.</span><span class="sxs-lookup"><span data-stu-id="a8f97-122">Open *~/workspace/hello-world/app/controllers/application_controller.rb* for editing.</span></span> <span data-ttu-id="a8f97-123">Modificare la classe `ApplicationController` per avere l'aspetto dell'esempio di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="a8f97-123">Modify the `ApplicationController` class to look like the following code sample:</span></span>

  ```ruby
  class ApplicationController > ActionController :: base
    protect_from_forgery with: :exception 
    def hello
      render html: "Hello, world from Azure Web App on Linux!"
    end
  end
  ```

<span data-ttu-id="a8f97-124">Ora l'app è configurata.</span><span class="sxs-lookup"><span data-stu-id="a8f97-124">Your app is now configured.</span></span> <span data-ttu-id="a8f97-125">Tramite il Web browser, passare a `http://localhost:3000` per confermare la pagina di destinazione principale.</span><span class="sxs-lookup"><span data-stu-id="a8f97-125">Using your web browser, navigate to `http://localhost:3000` to confirm the root landing page.</span></span>

![Hello World configurato](./media/app-service-linux-ruby-get-started/hello-world-configured.png)

[!INCLUDE [Try Cloud Shell](../../includes/cloud-shell-try-it.md)]

## <a name="create-a-ruby-web-app-on-azure"></a><span data-ttu-id="a8f97-127">Creare una app web Ruby in Azure</span><span class="sxs-lookup"><span data-stu-id="a8f97-127">Create a Ruby web app on Azure</span></span>

<span data-ttu-id="a8f97-128">Usare il comando [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) per creare un piano di servizio app per l'app web.</span><span class="sxs-lookup"><span data-stu-id="a8f97-128">Use the [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) command to create an app service plan for your web app.</span></span> 
 
```azurecli-interactive
  az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --is-linux
```

<span data-ttu-id="a8f97-129">Eseguire quindi il comando [az webapp create](https://docs.microsoft.com/cli/azure/webapp) per creare l'app web che usa il piano di servizio appena creato.</span><span class="sxs-lookup"><span data-stu-id="a8f97-129">Next, issue the [az webapp create](https://docs.microsoft.com/cli/azure/webapp) command to create the web app that uses the newly created service plan.</span></span> <span data-ttu-id="a8f97-130">Si noti che il runtime è impostato su `ruby|2.3`.</span><span class="sxs-lookup"><span data-stu-id="a8f97-130">Notice that the runtime is set to `ruby|2.3`.</span></span> <span data-ttu-id="a8f97-131">Non dimenticare di sostituire `<app name>` con un nome univoco dell'app.</span><span class="sxs-lookup"><span data-stu-id="a8f97-131">Don't forget to replace `<app name>` with a unique app name.</span></span>

```azurecli-interactive
  az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app name> --runtime "ruby|2.3" --deployment-local-git
```

<span data-ttu-id="a8f97-132">Una volta creato l'app web, è disponibile una pagina **Panoramica** per la visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="a8f97-132">Once the web app is created, an **Overview** page is available to view.</span></span> <span data-ttu-id="a8f97-133">Passare ad essa.</span><span class="sxs-lookup"><span data-stu-id="a8f97-133">Navigate to it.</span></span> <span data-ttu-id="a8f97-134">Viene visualizzata la pagina iniziale seguente:</span><span class="sxs-lookup"><span data-stu-id="a8f97-134">The following splash page is displayed:</span></span>

![Pagina iniziale](./media/app-service-linux-ruby-get-started/splash-page.png)


## <a name="deploy-your-application"></a><span data-ttu-id="a8f97-136">Distribuire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="a8f97-136">Deploy your application</span></span>

<span data-ttu-id="a8f97-137">Usare Git per distribuire l'applicazione Ruby in Azure.</span><span class="sxs-lookup"><span data-stu-id="a8f97-137">Use Git to deploy the Ruby application to Azure.</span></span> <span data-ttu-id="a8f97-138">La app web ha già una distribuzione Git configurata.</span><span class="sxs-lookup"><span data-stu-id="a8f97-138">The web app already has a Git deployment configured.</span></span> <span data-ttu-id="a8f97-139">È possibile recuperare l'URL di distribuzione tramite l'emissione di un comando [az webapp deployment](https://docs.microsoft.com/cli/azure/webapp/deployment).</span><span class="sxs-lookup"><span data-stu-id="a8f97-139">You can retrieve the deployment URL by issuing an [az webapp deployment](https://docs.microsoft.com/cli/azure/webapp/deployment) command.</span></span>  

```bash
az webapp deployment source show --name <app name> --resource-group myResourceGroup
```

<span data-ttu-id="a8f97-140">Si noti che l'URL Git ha il formato seguente, in base al nome dell'app Web:</span><span class="sxs-lookup"><span data-stu-id="a8f97-140">Notice that the Git URL has the following form based on your web app name:</span></span>

```bash
https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
```

[!INCLUDE [Clean-up section](../../includes/configure-deployment-user-no-h.md)]

<span data-ttu-id="a8f97-141">Eseguire i comandi seguenti per distribuire l'applicazione locale al sito Web di Azure:</span><span class="sxs-lookup"><span data-stu-id="a8f97-141">Run the following commands to deploy the local application to your Azure website:</span></span>

```bash
git remote add azure <Git deployment URL from above>
git add -A
git commit -m "Initial deployment commit"
git push azure master
```

<span data-ttu-id="a8f97-142">Verificare che per le operazioni di distribuzione in remoto venga segnalato l'esito positivo.</span><span class="sxs-lookup"><span data-stu-id="a8f97-142">Confirm that the remote deployment operations report success.</span></span> <span data-ttu-id="a8f97-143">I comandi generano un output simile al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="a8f97-143">The commands produce output similar to the following text:</span></span>

```bash
remote: Using sass-rails 5.0.6
remote: Updating files in vendor/cache
remote: Bundle gems are installed into ./vendor/bundle
remote: Updating files in vendor/cache
remote: ~site/repository
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
To https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
  579ccb....2ca5f31  master -> master
myuser@ubuntu1234:~workspace/<app name>$
```

<span data-ttu-id="a8f97-144">Dopo aver completato la distribuzione, riavviare l'app Web affinché la distribuzione venga applicata tramite il comando [az webapp restart](https://docs.microsoft.com/cli/azure/webapp#restart), come mostrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="a8f97-144">Once the deployment has completed, restart your web app for the deployment to take effect by using the [az webapp restart](https://docs.microsoft.com/cli/azure/webapp#restart) command, as shown here:</span></span>

```azurecli-interactive 
az webapp restart --name <app name> --resource-group myResourceGroup
```

<span data-ttu-id="a8f97-145">Passare al sito e verificare i risultati.</span><span class="sxs-lookup"><span data-stu-id="a8f97-145">Navigate to your site and verify the results.</span></span>

```bash
http://<your web app name>.azurewebsites.net
```
![app Web aggiornata](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

> [!NOTE]
> <span data-ttu-id="a8f97-147">Mentre l'app viene riavviata, il tentativo di aprire il sito genera un codice di stato HTTP `Error 503 Server unavailable`.</span><span class="sxs-lookup"><span data-stu-id="a8f97-147">While the app is restarting, attempting to browse the site results in an HTTP status code `Error 503 Server unavailable`.</span></span> <span data-ttu-id="a8f97-148">Il completamento del riavvio potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="a8f97-148">It may take a few minutes to fully restart.</span></span>
>

[!INCLUDE [Clean-up section](../../includes/cli-script-clean-up.md)]


## <a name="next-steps"></a><span data-ttu-id="a8f97-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a8f97-149">Next steps</span></span>

[<span data-ttu-id="a8f97-150">Domande frequenti su App Web del Servizio app di Azure su Linux</span><span class="sxs-lookup"><span data-stu-id="a8f97-150">Azure App Service Web App on Linux FAQ</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-linux-faq.md)