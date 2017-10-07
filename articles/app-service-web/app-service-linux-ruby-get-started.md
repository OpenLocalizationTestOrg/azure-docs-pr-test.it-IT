---
title: un'App Ruby con le app Web in Linux aaaCreate | Documenti Microsoft
description: Informazioni su toocreate Ruby App con del sito web di Azure in Linux.
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
ms.openlocfilehash: 99ce3b5ee16703a147787387bb02973defce8190
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-ruby-app-with-web-apps-on-linux"></a><span data-ttu-id="f9e43-104">Creare un'app Ruby con le App Web in Linux</span><span class="sxs-lookup"><span data-stu-id="f9e43-104">Create a Ruby App with Web Apps on Linux</span></span> 

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="f9e43-105">Le [app Web di Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) forniscono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione.</span><span class="sxs-lookup"><span data-stu-id="f9e43-105">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="f9e43-106">Questa Guida introduttiva viene illustrato come una base Ruby sull'applicazione Guide toocreate quindi distribuirlo tooAzure come un'App Web in Linux.</span><span class="sxs-lookup"><span data-stu-id="f9e43-106">This quickstart shows you how toocreate a basic Ruby on Rails application you then deploy it tooAzure as a Web App on Linux.</span></span>

![Hello-world](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

## <a name="prerequisites"></a><span data-ttu-id="f9e43-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f9e43-108">Prerequisites</span></span>

* <span data-ttu-id="f9e43-109">[Ruby 2.4.1 o versione successiva](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).</span><span class="sxs-lookup"><span data-stu-id="f9e43-109">[Ruby 2.4.1 or higher](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).</span></span>
* <span data-ttu-id="f9e43-110">[Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="f9e43-110">[Git](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="f9e43-111">Una [sottoscrizione di Azure attiva](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f9e43-111">An [active Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a><span data-ttu-id="f9e43-112">Scaricare l'esempio hello</span><span class="sxs-lookup"><span data-stu-id="f9e43-112">Download hello sample</span></span>

<span data-ttu-id="f9e43-113">In una finestra terminale, eseguire hello successivo comando tooclone hello esempio app repository tooyour computer locale:</span><span class="sxs-lookup"><span data-stu-id="f9e43-113">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine:</span></span>

```bash
git clone https://github.com/Azure-Samples/ruby-docs-hello-world
```

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="run-hello-application-locally"></a><span data-ttu-id="f9e43-114">Eseguire un'applicazione hello in locale</span><span class="sxs-lookup"><span data-stu-id="f9e43-114">Run hello application locally</span></span>

<span data-ttu-id="f9e43-115">Eseguire il server di guide hello affinché toowork applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f9e43-115">Run hello rails server in order for hello application toowork.</span></span> <span data-ttu-id="f9e43-116">Modificare toohello *hello world* directory e hello `rails server` comando Avvia hello server.</span><span class="sxs-lookup"><span data-stu-id="f9e43-116">Change toohello *hello-world* directory, and hello `rails server` command starts hello server.</span></span>

```bash
cd hello-world\bin
rails server
```
    
<span data-ttu-id="f9e43-117">Tramite il browser, passare troppo`http://localhost:3000` app di hello tootest localmente.</span><span class="sxs-lookup"><span data-stu-id="f9e43-117">Using your web browser, navigate too`http://localhost:3000` tootest hello app locally.</span></span>  

![Hello-world](./media/app-service-linux-ruby-get-started/hello-world.png)

## <a name="modify-app-toodisplay-welcome-message"></a><span data-ttu-id="f9e43-119">Modifica messaggio di benvenuto toodisplay app</span><span class="sxs-lookup"><span data-stu-id="f9e43-119">Modify app toodisplay welcome message</span></span>

<span data-ttu-id="f9e43-120">Modificare un'applicazione hello in modo da visualizzare un messaggio di benvenuto.</span><span class="sxs-lookup"><span data-stu-id="f9e43-120">Modify hello application so it displays a welcome message.</span></span> <span data-ttu-id="f9e43-121">Modificare il controller dell'applicazione hello in modo che restituisca il messaggio hello come browser toohello HTML.</span><span class="sxs-lookup"><span data-stu-id="f9e43-121">Change hello application's controller so it returns hello message as HTML toohello browser.</span></span> 

<span data-ttu-id="f9e43-122">Aprire *~/workspace/hello-world/app/controllers/application_controller.rb* per la modifica.</span><span class="sxs-lookup"><span data-stu-id="f9e43-122">Open *~/workspace/hello-world/app/controllers/application_controller.rb* for editing.</span></span> <span data-ttu-id="f9e43-123">Modificare hello `ApplicationController` toolook classe come hello nell'esempio di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="f9e43-123">Modify hello `ApplicationController` class toolook like hello following code sample:</span></span>

  ```ruby
  class ApplicationController > ActionController :: base
    protect_from_forgery with: :exception 
    def hello
      render html: "Hello, world from Azure Web App on Linux!"
    end
  end
  ```

<span data-ttu-id="f9e43-124">Ora l'app è configurata.</span><span class="sxs-lookup"><span data-stu-id="f9e43-124">Your app is now configured.</span></span> <span data-ttu-id="f9e43-125">Tramite il browser, passare troppo`http://localhost:3000` pagina di destinazione tooconfirm hello radice.</span><span class="sxs-lookup"><span data-stu-id="f9e43-125">Using your web browser, navigate too`http://localhost:3000` tooconfirm hello root landing page.</span></span>

![Hello World configurato](./media/app-service-linux-ruby-get-started/hello-world-configured.png)

[!INCLUDE [Try Cloud Shell](../../includes/cloud-shell-try-it.md)]

## <a name="create-a-ruby-web-app-on-azure"></a><span data-ttu-id="f9e43-127">Creare una app web Ruby in Azure</span><span class="sxs-lookup"><span data-stu-id="f9e43-127">Create a Ruby web app on Azure</span></span>

<span data-ttu-id="f9e43-128">Hello utilizzare [crea piano di servizio App az](https://docs.microsoft.com/cli/azure/appservice/plan#create) comando toocreate un piano di servizio app per l'app web.</span><span class="sxs-lookup"><span data-stu-id="f9e43-128">Use hello [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) command toocreate an app service plan for your web app.</span></span> 
 
```azurecli-interactive
  az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --is-linux
```

<span data-ttu-id="f9e43-129">Eseguire quindi hello [az webapp creare](https://docs.microsoft.com/cli/azure/webapp) comando toocreate hello web app che utilizza il piano di servizio hello appena creato.</span><span class="sxs-lookup"><span data-stu-id="f9e43-129">Next, issue hello [az webapp create](https://docs.microsoft.com/cli/azure/webapp) command toocreate hello web app that uses hello newly created service plan.</span></span> <span data-ttu-id="f9e43-130">Si noti che runtime hello è impostato troppo`ruby|2.3`.</span><span class="sxs-lookup"><span data-stu-id="f9e43-130">Notice that hello runtime is set too`ruby|2.3`.</span></span> <span data-ttu-id="f9e43-131">Non dimenticare tooreplace `<app name>` con un nome univoco dell'app.</span><span class="sxs-lookup"><span data-stu-id="f9e43-131">Don't forget tooreplace `<app name>` with a unique app name.</span></span>

```azurecli-interactive
  az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app name> --runtime "ruby|2.3" --deployment-local-git
```

<span data-ttu-id="f9e43-132">Una volta creato l'app web hello, un **Panoramica** pagina è disponibile tooview.</span><span class="sxs-lookup"><span data-stu-id="f9e43-132">Once hello web app is created, an **Overview** page is available tooview.</span></span> <span data-ttu-id="f9e43-133">Passare tooit.</span><span class="sxs-lookup"><span data-stu-id="f9e43-133">Navigate tooit.</span></span> <span data-ttu-id="f9e43-134">viene visualizzato dopo la pagina iniziale di Hello:</span><span class="sxs-lookup"><span data-stu-id="f9e43-134">hello following splash page is displayed:</span></span>

![Pagina iniziale](./media/app-service-linux-ruby-get-started/splash-page.png)


## <a name="deploy-your-application"></a><span data-ttu-id="f9e43-136">Distribuire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="f9e43-136">Deploy your application</span></span>

<span data-ttu-id="f9e43-137">Usare Git toodeploy hello applicazione Ruby tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f9e43-137">Use Git toodeploy hello Ruby application tooAzure.</span></span> <span data-ttu-id="f9e43-138">app web Hello dispone già di una distribuzione Git configurata.</span><span class="sxs-lookup"><span data-stu-id="f9e43-138">hello web app already has a Git deployment configured.</span></span> <span data-ttu-id="f9e43-139">È possibile recuperare l'URL di distribuzione hello generando un [distribuzione webapp az](https://docs.microsoft.com/cli/azure/webapp/deployment) comando.</span><span class="sxs-lookup"><span data-stu-id="f9e43-139">You can retrieve hello deployment URL by issuing an [az webapp deployment](https://docs.microsoft.com/cli/azure/webapp/deployment) command.</span></span>  

```bash
az webapp deployment source show --name <app name> --resource-group myResourceGroup
```

<span data-ttu-id="f9e43-140">Si noti che l'URL Git hello sono hello modulo basato sul nome dell'app web seguenti:</span><span class="sxs-lookup"><span data-stu-id="f9e43-140">Notice that hello Git URL has hello following form based on your web app name:</span></span>

```bash
https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
```

[!INCLUDE [Clean-up section](../../includes/configure-deployment-user-no-h.md)]

<span data-ttu-id="f9e43-141">Eseguire hello seguenti comandi toodeploy hello applicazione locale tooyour sito Web di Azure:</span><span class="sxs-lookup"><span data-stu-id="f9e43-141">Run hello following commands toodeploy hello local application tooyour Azure website:</span></span>

```bash
git remote add azure <Git deployment URL from above>
git add -A
git commit -m "Initial deployment commit"
git push azure master
```

<span data-ttu-id="f9e43-142">Verificare che le operazioni di distribuzione remoto hello segnalano l'esito positivo.</span><span class="sxs-lookup"><span data-stu-id="f9e43-142">Confirm that hello remote deployment operations report success.</span></span> <span data-ttu-id="f9e43-143">Hello comandi producono output simili toohello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="f9e43-143">hello commands produce output similar toohello following text:</span></span>

```bash
remote: Using sass-rails 5.0.6
remote: Updating files in vendor/cache
remote: Bundle gems are installed into ./vendor/bundle
remote: Updating files in vendor/cache
remote: ~site/repository
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<your web app name>.scm.azurewebsites.net/<your web app name>.git
  579ccb....2ca5f31  master -> master
myuser@ubuntu1234:~workspace/<app name>$
```

<span data-ttu-id="f9e43-144">Una volta completata la distribuzione di hello, riavviare l'app web per effetto di hello distribuzione tootake utilizzando hello [riavvio webapp az](https://docs.microsoft.com/cli/azure/webapp#restart) comando, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="f9e43-144">Once hello deployment has completed, restart your web app for hello deployment tootake effect by using hello [az webapp restart](https://docs.microsoft.com/cli/azure/webapp#restart) command, as shown here:</span></span>

```azurecli-interactive 
az webapp restart --name <app name> --resource-group myResourceGroup
```

<span data-ttu-id="f9e43-145">Passare tooyour sito e verificare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="f9e43-145">Navigate tooyour site and verify hello results.</span></span>

```bash
http://<your web app name>.azurewebsites.net
```
![app Web aggiornata](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

> [!NOTE]
> <span data-ttu-id="f9e43-147">Durante l'applicazione hello è il riavvio, il tentativo di toobrowse hello del sito genera un codice di stato HTTP `Error 503 Server unavailable`.</span><span class="sxs-lookup"><span data-stu-id="f9e43-147">While hello app is restarting, attempting toobrowse hello site results in an HTTP status code `Error 503 Server unavailable`.</span></span> <span data-ttu-id="f9e43-148">Potrebbe richiedere alcuni minuti toofully riavvio.</span><span class="sxs-lookup"><span data-stu-id="f9e43-148">It may take a few minutes toofully restart.</span></span>
>

[!INCLUDE [Clean-up section](../../includes/cli-script-clean-up.md)]


## <a name="next-steps"></a><span data-ttu-id="f9e43-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f9e43-149">Next steps</span></span>

[<span data-ttu-id="f9e43-150">Domande frequenti su App Web del Servizio app di Azure su Linux</span><span class="sxs-lookup"><span data-stu-id="f9e43-150">Azure App Service Web App on Linux FAQ</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-linux-faq.md)