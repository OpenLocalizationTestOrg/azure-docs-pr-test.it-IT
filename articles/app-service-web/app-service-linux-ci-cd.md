---
title: Distribuzione con App Web di Azure in Linux aaaContinuous | Documenti Microsoft
description: Come la distribuzione continua toosetup nell'App Web di Azure in Linux.
keywords: servizio app di azure, linux, oss, acr
services: app-service
documentationcenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: a47fb43a-bbbd-4751-bdc1-cd382eae49f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: f94d837e27605da58428f507ab2b0eb3af3297e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-with-azure-web-app-on-linux"></a><span data-ttu-id="67418-104">Distribuzione continua con App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="67418-104">Continuous deployment with Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="67418-105">In questa esercitazione si configura la distribuzione continua per un'immagine personalizzata del contenitore da repository del [Registro contenitori di Azure](https://azure.microsoft.com/en-us/services/container-registry/) o dall'[hub Docker](https://hub.docker.com).</span><span class="sxs-lookup"><span data-stu-id="67418-105">In this tutorial, you configure continuous deployment for a custom container image from Managed [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/) repositories or [Docker Hub](https://hub.docker.com).</span></span>

## <a name="step-1---sign-in-tooazure"></a><span data-ttu-id="67418-106">Passaggio 1 - Sign in tooAzure</span><span class="sxs-lookup"><span data-stu-id="67418-106">Step 1 - Sign in tooAzure</span></span>

<span data-ttu-id="67418-107">Accedi toohello portale di Azure all'indirizzo http://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="67418-107">Sign in toohello Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---enable-container-continuous-deployment-feature"></a><span data-ttu-id="67418-108">Passaggio 2: Abilitare la funzionalità di distribuzione continua del contenitore</span><span class="sxs-lookup"><span data-stu-id="67418-108">Step 2 - Enable container continuous deployment feature</span></span>

<span data-ttu-id="67418-109">È possibile abilitare funzionalità di distribuzione continua hello mediante [CLI di Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) e l'esecuzione di hello comando seguente</span><span class="sxs-lookup"><span data-stu-id="67418-109">You can enable hello continuous deployment feature using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing hello following command</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

<span data-ttu-id="67418-110">In hello  **[portale di Azure](https://portal.azure.com/)**, fare clic su hello **servizio App** opzione a sinistra di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="67418-110">In hello **[Azure portal](https://portal.azure.com/)**, click hello **App Service** option on hello left of hello page.</span></span>

<span data-ttu-id="67418-111">Fare clic sul nome hello dell'app che si desidera tooconfigure Hub Docker la distribuzione continua per.</span><span class="sxs-lookup"><span data-stu-id="67418-111">Click on hello name of your app that you want tooconfigure Docker Hub continuous deployment for.</span></span>

<span data-ttu-id="67418-112">In hello **impostazioni App**, aggiungere un'app denominata `DOCKER_ENABLE_CI` con valore hello `true`.</span><span class="sxs-lookup"><span data-stu-id="67418-112">In hello **App settings**, add an app setting called `DOCKER_ENABLE_CI` with hello value `true`.</span></span>

![inserire l'immagine dell'impostazione dell'app](./media/app-service-webapp-service-linux-ci-cd/step2.png)

## <a name="step-3---prepare-webhook-url"></a><span data-ttu-id="67418-114">Passaggio 3 - Preparare l'URL webhook</span><span class="sxs-lookup"><span data-stu-id="67418-114">Step 3 - Prepare Webhook URL</span></span>

<span data-ttu-id="67418-115">È possibile ottenere utilizzando URL del Webhook hello [CLI di Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) e l'esecuzione di hello comando seguente</span><span class="sxs-lookup"><span data-stu-id="67418-115">You can obtain hello Webhook URL using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing hello following command</span></span>

```azurecli-interactive
az webapp deployment container -n sname1 -g rgname -e true --show-cd-url
``` 

<span data-ttu-id="67418-116">Per l'URL del Webhook hello, è necessario hello toohave seguenti endpoint: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span><span class="sxs-lookup"><span data-stu-id="67418-116">For hello Webhook URL, you need toohave hello following endpoint: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span></span>

<span data-ttu-id="67418-117">È possibile ottenere il `publishingusername` e `publishingpwd` scaricando hello web app pubblicare profilo utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="67418-117">You can obtain your `publishingusername` and `publishingpwd` by downloading hello web app publish profile using hello Azure portal.</span></span>

![inserire l'immagine dell'aggiunta del webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-3.png)

## <a name="step-4---add-a-web-hook"></a><span data-ttu-id="67418-119">Passaggio 4 - Aggiungere un webhook</span><span class="sxs-lookup"><span data-stu-id="67418-119">Step 4 - Add a web hook</span></span>

### <a name="azure-container-registry"></a><span data-ttu-id="67418-120">Registro di sistema del contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="67418-120">Azure Container Registry</span></span>

<span data-ttu-id="67418-121">Nel pannello del portale del registro fare clic su **Webhook** e creare un nuovo webhook facendo clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="67418-121">In your registry portal blade, click **Webhooks**, create a new webhook by clicking **Add**.</span></span> <span data-ttu-id="67418-122">In hello **creare webhook** pannello, denominare il webhook.</span><span class="sxs-lookup"><span data-stu-id="67418-122">In hello **Create webhook** blade, give your webhook a name.</span></span> <span data-ttu-id="67418-123">Per hello Webhook URI, è necessario tooprovide hello URL ottenuto dal **passaggio 3**</span><span class="sxs-lookup"><span data-stu-id="67418-123">For hello Webhook URI, you need tooprovide hello URL obtained from **Step 3**</span></span>

<span data-ttu-id="67418-124">Assicurarsi che ambito hello è definito come hello repository che contiene l'immagine del contenitore.</span><span class="sxs-lookup"><span data-stu-id="67418-124">Make sure that you define hello scope as hello repo that contains your container image.</span></span>

![inserimento dell'immagine del webhhok](./media/app-service-webapp-service-linux-ci-cd/step3ACRWebhook-1.png)

<span data-ttu-id="67418-126">Quando viene aggiornata l'immagine di hello, hello web app aggiornata automaticamente con una nuova immagine hello.</span><span class="sxs-lookup"><span data-stu-id="67418-126">When hello image gets updated, hello web app get updated automatically with hello new image.</span></span>

### <a name="docker-hub"></a><span data-ttu-id="67418-127">Hub Docker</span><span class="sxs-lookup"><span data-stu-id="67418-127">Docker Hub</span></span>

<span data-ttu-id="67418-128">Nella pagina Hub Docker, fare clic su **Webhook**, quindi **CREATE A WEBHOOK** (CREA UN WEBHOOK).</span><span class="sxs-lookup"><span data-stu-id="67418-128">In your Docker Hub page, click **Webhooks**, then **CREATE A WEBHOOK**.</span></span>

![inserire l'immagine dell'aggiunta del webhook 1](./media/app-service-webapp-service-linux-ci-cd/step3-1.png)

<span data-ttu-id="67418-130">Per l'URL del Webhook hello, è necessario tooprovide hello URL ottenuto dal **passaggio 3**</span><span class="sxs-lookup"><span data-stu-id="67418-130">For hello Webhook URL, you need tooprovide hello URL obtained from **Step 3**</span></span>

![inserire l'immagine dell'aggiunta del webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-2.png)

<span data-ttu-id="67418-132">Quando viene aggiornata l'immagine di hello, hello web app aggiornata automaticamente con una nuova immagine hello.</span><span class="sxs-lookup"><span data-stu-id="67418-132">When hello image gets updated, hello web app get updated automatically with hello new image.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67418-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="67418-133">Next steps</span></span>
* [<span data-ttu-id="67418-134">Definizione di App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="67418-134">What is Azure Web App on Linux?</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="67418-135">Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="67418-135">Azure Container Registry</span></span>](https://azure.microsoft.com/en-us/services/container-registry/)
* [<span data-ttu-id="67418-136">Uso della configurazione PM2 per Node.js in App Web su Linux</span><span class="sxs-lookup"><span data-stu-id="67418-136">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="67418-137">Uso di .NET Core in App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="67418-137">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="67418-138">Uso di Ruby in App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="67418-138">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="67418-139">Come immagine di toouse una Docker personalizzata per l'App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="67418-139">How toouse a custom Docker image for Azure Web App on Linux</span></span>](./app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="67418-140">Domande frequenti su App Web del Servizio app di Azure su Linux</span><span class="sxs-lookup"><span data-stu-id="67418-140">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md) 
* [<span data-ttu-id="67418-141">Gestire App Web in Linux tramite interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="67418-141">Manage Web App on Linux using Azure CLI 2.0</span></span>](./app-service-linux-cli.md)



