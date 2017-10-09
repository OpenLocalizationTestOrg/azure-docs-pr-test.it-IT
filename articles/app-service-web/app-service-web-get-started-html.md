---
title: app web aaaCreate HTML statico in Azure | Documenti Microsoft
description: Informazioni su come le app web toorun in Azure App Service distribuendo un HTML statico app di esempio.
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
ms.openlocfilehash: efd8c8189a3aa1ac35602b688eeb31bff6f5a373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-static-html-web-app-in-azure"></a><span data-ttu-id="c9b9e-103">Creare un'app Web HTML statica in Azure</span><span class="sxs-lookup"><span data-stu-id="c9b9e-103">Create a static HTML web app in Azure</span></span>

<span data-ttu-id="c9b9e-104">Le [app Web di Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) forniscono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione.</span><span class="sxs-lookup"><span data-stu-id="c9b9e-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="c9b9e-105">Questa Guida rapida illustra toodeploy HTML + CSS base dei siti tooAzure Web App.</span><span class="sxs-lookup"><span data-stu-id="c9b9e-105">This quickstart shows how toodeploy a basic HTML+CSS site tooAzure Web Apps.</span></span> <span data-ttu-id="c9b9e-106">Si crea app web hello utilizzando hello [CLI di Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), e si utilizza Git toodeploy app web di esempio HTML toohello contenuto.</span><span class="sxs-lookup"><span data-stu-id="c9b9e-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git toodeploy sample HTML content toohello web app.</span></span>

![Home page dell'app di esempio](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

<span data-ttu-id="c9b9e-108">È possibile eseguire operazioni di hello seguenti utilizzando un computer Mac, Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="c9b9e-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="c9b9e-109">Una volta installati i prerequisiti di hello, sono necessari circa cinque minuti toocomplete passaggi hello.</span><span class="sxs-lookup"><span data-stu-id="c9b9e-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9b9e-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c9b9e-110">Prerequisites</span></span>

<span data-ttu-id="c9b9e-111">toocomplete questa Guida rapida:</span><span class="sxs-lookup"><span data-stu-id="c9b9e-111">toocomplete this quickstart:</span></span>

- <span data-ttu-id="c9b9e-112">[Installare Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]</span><span class="sxs-lookup"><span data-stu-id="c9b9e-112">[Install Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c9b9e-113">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="c9b9e-113">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="c9b9e-114">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="c9b9e-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="c9b9e-115">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c9b9e-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-hello-sample"></a><span data-ttu-id="c9b9e-116">Scaricare l'esempio hello</span><span class="sxs-lookup"><span data-stu-id="c9b9e-116">Download hello sample</span></span>

<span data-ttu-id="c9b9e-117">In una finestra terminale, eseguire hello successivo comando tooclone hello esempio app repository tooyour computer locale.</span><span class="sxs-lookup"><span data-stu-id="c9b9e-117">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/html-docs-hello-world.git
```

<span data-ttu-id="c9b9e-118">Utilizzare questo toorun finestra terminale tutti i comandi di hello in questa Guida rapida.</span><span class="sxs-lookup"><span data-stu-id="c9b9e-118">You use this terminal window toorun all hello commands in this quickstart.</span></span>

## <a name="view-hello-html"></a><span data-ttu-id="c9b9e-119">Visualizzare hello HTML</span><span class="sxs-lookup"><span data-stu-id="c9b9e-119">View hello HTML</span></span>

<span data-ttu-id="c9b9e-120">Passare toohello directory che contiene l'esempio hello HTML.</span><span class="sxs-lookup"><span data-stu-id="c9b9e-120">Navigate toohello directory that contains hello sample HTML.</span></span> <span data-ttu-id="c9b9e-121">Aprire hello *index.html* file nel browser.</span><span class="sxs-lookup"><span data-stu-id="c9b9e-121">Open hello *index.html* file in your browser.</span></span>

![Home page dell'app di esempio](media/app-service-web-get-started-html/hello-world-in-browser.png)

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Pagina dell'app Web vuota](media/app-service-web-get-started-html/app-service-web-service-created.png)

<span data-ttu-id="c9b9e-124">È stata creata una nuova app Web vuota in Azure.</span><span class="sxs-lookup"><span data-stu-id="c9b9e-124">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 13, done.
Delta compression using up too4 threads.
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
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a><span data-ttu-id="c9b9e-125">Esplorare app toohello</span><span class="sxs-lookup"><span data-stu-id="c9b9e-125">Browse toohello app</span></span>

<span data-ttu-id="c9b9e-126">In un browser, passare l'URL dell'app web di Azure toohello:</span><span class="sxs-lookup"><span data-stu-id="c9b9e-126">In a browser, go toohello Azure web app URL:</span></span>

```
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="c9b9e-127">pagina Hello è in esecuzione come un'app web di servizio App di Azure.</span><span class="sxs-lookup"><span data-stu-id="c9b9e-127">hello page is running as an Azure App Service web app.</span></span>

![Home page dell'app di esempio](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

<span data-ttu-id="c9b9e-129">**Congratulazioni.**</span><span class="sxs-lookup"><span data-stu-id="c9b9e-129">**Congratulations!**</span></span> <span data-ttu-id="c9b9e-130">È stato distribuito il primo tooApp di app HTML del servizio.</span><span class="sxs-lookup"><span data-stu-id="c9b9e-130">You've deployed your first HTML app tooApp Service.</span></span>

## <a name="update-and-redeploy-hello-app"></a><span data-ttu-id="c9b9e-131">Aggiornare e ridistribuire l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="c9b9e-131">Update and redeploy hello app</span></span>

<span data-ttu-id="c9b9e-132">Aprire hello *index.html* file in un editor di testo e verificare un markup toohello di modifica.</span><span class="sxs-lookup"><span data-stu-id="c9b9e-132">Open hello *index.html* file in a text editor, and make a change toohello markup.</span></span> <span data-ttu-id="c9b9e-133">Ad esempio, modificare l'intestazione H1 hello da "Azure App Service – esempio sito HTML statico" toojust "servizio App di Azure'.</span><span class="sxs-lookup"><span data-stu-id="c9b9e-133">For example, change hello H1 heading from "Azure App Service - Sample Static HTML Site" toojust "Azure App Service\`.</span></span>

<span data-ttu-id="c9b9e-134">Eseguire il commit delle modifiche in Git e quindi push tooAzure modifiche di codice hello.</span><span class="sxs-lookup"><span data-stu-id="c9b9e-134">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated HTML"
git push azure master
```

<span data-ttu-id="c9b9e-135">Una volta completata la distribuzione, aggiornare le modifiche di hello toosee browser.</span><span class="sxs-lookup"><span data-stu-id="c9b9e-135">Once deployment has completed, refresh your browser toosee hello changes.</span></span>

![Home page dell'app di esempio aggiornata](media/app-service-web-get-started-html/hello-azure-in-browser-az.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="c9b9e-137">Gestire la nuova app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="c9b9e-137">Manage your new Azure web app</span></span>

<span data-ttu-id="c9b9e-138">Passare toohello <a href="https://portal.azure.com" target="_blank">portale di Azure</a> toomanage hello web app è stato creato.</span><span class="sxs-lookup"><span data-stu-id="c9b9e-138">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="c9b9e-139">Scegliere dal menu a sinistra hello **servizi App**, quindi fare clic su nome hello dell'app web di Azure.</span><span class="sxs-lookup"><span data-stu-id="c9b9e-139">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Spostamento del portale tooAzure web app](./media/app-service-web-get-started-html/portal1.png)

<span data-ttu-id="c9b9e-141">Verrà visualizzata la pagina di panoramica dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="c9b9e-141">You see your web app's Overview page.</span></span> <span data-ttu-id="c9b9e-142">Qui è possibile eseguire attività di gestione di base come l'esplorazione, l'arresto, l'avvio, il riavvio e l'eliminazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="c9b9e-142">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Pannello del servizio app nel portale di Azure](./media/app-service-web-get-started-html/portal2.png)

<span data-ttu-id="c9b9e-144">menu a sinistra di Hello fornisce diverse pagine di configurazione app.</span><span class="sxs-lookup"><span data-stu-id="c9b9e-144">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="c9b9e-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c9b9e-145">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c9b9e-146">Eseguire il mapping di un dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="c9b9e-146">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
