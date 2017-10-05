---
title: Distribuzione continua con App Web di Azure in Linux | Microsoft Docs
description: Come configurare la distribuzione continua in App Web di Azure in Linux.
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
ms.openlocfilehash: f8f7d51003f8a55b7f51e8cc2cea838e8e5a6196
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="continuous-deployment-with-azure-web-app-on-linux"></a><span data-ttu-id="a77e7-104">Distribuzione continua con App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="a77e7-104">Continuous deployment with Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="a77e7-105">In questa esercitazione si configura la distribuzione continua per un'immagine personalizzata del contenitore da repository del [Registro contenitori di Azure](https://azure.microsoft.com/en-us/services/container-registry/) o dall'[hub Docker](https://hub.docker.com).</span><span class="sxs-lookup"><span data-stu-id="a77e7-105">In this tutorial, you configure continuous deployment for a custom container image from Managed [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/) repositories or [Docker Hub](https://hub.docker.com).</span></span>

## <a name="step-1---sign-in-to-azure"></a><span data-ttu-id="a77e7-106">Passaggio 1 - Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="a77e7-106">Step 1 - Sign in to Azure</span></span>

<span data-ttu-id="a77e7-107">Accedere al portale di Azure all'indirizzo http://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="a77e7-107">Sign in to the Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---enable-container-continuous-deployment-feature"></a><span data-ttu-id="a77e7-108">Passaggio 2: Abilitare la funzionalità di distribuzione continua del contenitore</span><span class="sxs-lookup"><span data-stu-id="a77e7-108">Step 2 - Enable container continuous deployment feature</span></span>

<span data-ttu-id="a77e7-109">È possibile abilitare la funzionalità di distribuzione continua tramite l'[interfaccia della riga di comando di Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) ed eseguendo il comando seguente</span><span class="sxs-lookup"><span data-stu-id="a77e7-109">You can enable the continuous deployment feature using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing the following command</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

<span data-ttu-id="a77e7-110">Nel **[portale di Azure](https://portal.azure.com/)** fare clic sull'opzione **Servizio app** a sinistra nella pagina.</span><span class="sxs-lookup"><span data-stu-id="a77e7-110">In the **[Azure portal](https://portal.azure.com/)**, click the **App Service** option on the left of the page.</span></span>

<span data-ttu-id="a77e7-111">Fare clic sul nome dell'app per cui si desidera configurare la distribuzione continua dell'hub Docker.</span><span class="sxs-lookup"><span data-stu-id="a77e7-111">Click on the name of your app that you want to configure Docker Hub continuous deployment for.</span></span>

<span data-ttu-id="a77e7-112">In **Impostazioni app** aggiungere un'app denominata `DOCKER_ENABLE_CI` con il valore `true`.</span><span class="sxs-lookup"><span data-stu-id="a77e7-112">In the **App settings**, add an app setting called `DOCKER_ENABLE_CI` with the value `true`.</span></span>

![inserire l'immagine dell'impostazione dell'app](./media/app-service-webapp-service-linux-ci-cd/step2.png)

## <a name="step-3---prepare-webhook-url"></a><span data-ttu-id="a77e7-114">Passaggio 3 - Preparare l'URL webhook</span><span class="sxs-lookup"><span data-stu-id="a77e7-114">Step 3 - Prepare Webhook URL</span></span>

<span data-ttu-id="a77e7-115">È possibile ottenere l'URL Webhook tramite l'[interfaccia della riga di comando di Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) ed eseguendo il comando seguente</span><span class="sxs-lookup"><span data-stu-id="a77e7-115">You can obtain the Webhook URL using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing the following command</span></span>

```azurecli-interactive
az webapp deployment container -n sname1 -g rgname -e true --show-cd-url
``` 

<span data-ttu-id="a77e7-116">Per l'URL del Webhook, è necessario avere l'endpoint seguente: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span><span class="sxs-lookup"><span data-stu-id="a77e7-116">For the Webhook URL, you need to have the following endpoint: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span></span>

<span data-ttu-id="a77e7-117">È possibile ottenere `publishingusername` e `publishingpwd` scaricando il profilo di pubblicazione dell'app Web tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a77e7-117">You can obtain your `publishingusername` and `publishingpwd` by downloading the web app publish profile using the Azure portal.</span></span>

![inserire l'immagine dell'aggiunta del webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-3.png)

## <a name="step-4---add-a-web-hook"></a><span data-ttu-id="a77e7-119">Passaggio 4 - Aggiungere un webhook</span><span class="sxs-lookup"><span data-stu-id="a77e7-119">Step 4 - Add a web hook</span></span>

### <a name="azure-container-registry"></a><span data-ttu-id="a77e7-120">Registro di sistema del contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="a77e7-120">Azure Container Registry</span></span>

<span data-ttu-id="a77e7-121">Nel pannello del portale del registro fare clic su **Webhook** e creare un nuovo webhook facendo clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="a77e7-121">In your registry portal blade, click **Webhooks**, create a new webhook by clicking **Add**.</span></span> <span data-ttu-id="a77e7-122">Nel pannello **Create webhook** (Crea webhook) assegnare un nome al webhook.</span><span class="sxs-lookup"><span data-stu-id="a77e7-122">In the **Create webhook** blade, give your webhook a name.</span></span> <span data-ttu-id="a77e7-123">Per l'URI del webhook è necessario specificare l'URL ottenuto dal **passaggio 3**</span><span class="sxs-lookup"><span data-stu-id="a77e7-123">For the Webhook URI, you need to provide the URL obtained from **Step 3**</span></span>

<span data-ttu-id="a77e7-124">Assicurarsi di definire come ambito il repository che contiene l'immagine del contenitore.</span><span class="sxs-lookup"><span data-stu-id="a77e7-124">Make sure that you define the scope as the repo that contains your container image.</span></span>

![inserimento dell'immagine del webhhok](./media/app-service-webapp-service-linux-ci-cd/step3ACRWebhook-1.png)

<span data-ttu-id="a77e7-126">Quando l'immagine viene aggiornata, l'app Web viene aggiornata automaticamente con la nuova immagine.</span><span class="sxs-lookup"><span data-stu-id="a77e7-126">When the image gets updated, the web app get updated automatically with the new image.</span></span>

### <a name="docker-hub"></a><span data-ttu-id="a77e7-127">Hub Docker</span><span class="sxs-lookup"><span data-stu-id="a77e7-127">Docker Hub</span></span>

<span data-ttu-id="a77e7-128">Nella pagina Hub Docker, fare clic su **Webhook**, quindi **CREATE A WEBHOOK** (CREA UN WEBHOOK).</span><span class="sxs-lookup"><span data-stu-id="a77e7-128">In your Docker Hub page, click **Webhooks**, then **CREATE A WEBHOOK**.</span></span>

![inserire l'immagine dell'aggiunta del webhook 1](./media/app-service-webapp-service-linux-ci-cd/step3-1.png)

<span data-ttu-id="a77e7-130">Per l'URL del webhook è necessario specificare l'URL ottenuto dal **passaggio 3**</span><span class="sxs-lookup"><span data-stu-id="a77e7-130">For the Webhook URL, you need to provide the URL obtained from **Step 3**</span></span>

![inserire l'immagine dell'aggiunta del webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-2.png)

<span data-ttu-id="a77e7-132">Quando l'immagine viene aggiornata, l'app Web viene aggiornata automaticamente con la nuova immagine.</span><span class="sxs-lookup"><span data-stu-id="a77e7-132">When the image gets updated, the web app get updated automatically with the new image.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a77e7-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a77e7-133">Next steps</span></span>
* [<span data-ttu-id="a77e7-134">Definizione di App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="a77e7-134">What is Azure Web App on Linux?</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="a77e7-135">Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="a77e7-135">Azure Container Registry</span></span>](https://azure.microsoft.com/en-us/services/container-registry/)
* [<span data-ttu-id="a77e7-136">Uso della configurazione PM2 per Node.js in App Web su Linux</span><span class="sxs-lookup"><span data-stu-id="a77e7-136">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="a77e7-137">Uso di .NET Core in App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="a77e7-137">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="a77e7-138">Uso di Ruby in App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="a77e7-138">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="a77e7-139">Come usare un'immagine Docker personalizzata per App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="a77e7-139">How to use a custom Docker image for Azure Web App on Linux</span></span>](./app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="a77e7-140">Domande frequenti su App Web del Servizio app di Azure su Linux</span><span class="sxs-lookup"><span data-stu-id="a77e7-140">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md) 
* [<span data-ttu-id="a77e7-141">Gestire App Web in Linux tramite interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="a77e7-141">Manage Web App on Linux using Azure CLI 2.0</span></span>](./app-service-linux-cli.md)



