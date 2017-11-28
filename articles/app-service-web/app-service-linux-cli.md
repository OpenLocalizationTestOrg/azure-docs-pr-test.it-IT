---
title: App Web in Linux con Azure CLI 2.0 aaaManage | Documenti Microsoft
description: Gestire App Web in Linux tramite interfaccia della riga di comando di Azure.
keywords: servizio app di Azure, app Web, interfaccia della riga di comando, domande frequenti, linux, oss
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: aelnably
ms.openlocfilehash: 5e8e0da8a362450c56d2e87e087f77598ec874ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-web-app-on-linux-using-azure-cli"></a><span data-ttu-id="1d835-104">Gestire App Web in Linux tramite interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="1d835-104">Manage Web App on Linux using Azure CLI</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="1d835-105">Utilizzando i comandi di hello in questo articolo sono in grado di toocreate e gestire un'App Web in Linux con CLI di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="1d835-105">Using hello commands in this article you are able toocreate and manage a Web App on Linux using Azure CLI 2.0.</span></span>
<span data-ttu-id="1d835-106">È possibile iniziare a utilizzare hello nuova versione di hello CLI in due modi:</span><span class="sxs-lookup"><span data-stu-id="1d835-106">You can start using hello new version of hello CLI in two ways:</span></span>

* <span data-ttu-id="1d835-107">[Installare l'interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) sul computer.</span><span class="sxs-lookup"><span data-stu-id="1d835-107">[Installing Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span>
* <span data-ttu-id="1d835-108">Utilizzare [Azure Cloud Shell (anteprima)](../cloud-shell/overview.md)</span><span class="sxs-lookup"><span data-stu-id="1d835-108">Using [Azure Cloud Shell (Preview)](../cloud-shell/overview.md)</span></span>


## <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="1d835-109">Creare un nuovo piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="1d835-109">Create a Linux App Service Plan</span></span>

<span data-ttu-id="1d835-110">toocreate un piano di servizio a Linux App, è possibile utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1d835-110">toocreate a Linux App Service Plan, you can use hello following command:</span></span>

```azurecli-interactive
az appservice plan create -n appname -g rgname --islinux -l "South Central US" --sku S1 --number-of-workers 1
``` 

## <a name="create-a-custom-docker-container-web-app"></a><span data-ttu-id="1d835-111">Creare un contenitore Docker personalizzato App Web</span><span class="sxs-lookup"><span data-stu-id="1d835-111">Create a custom Docker container Web App</span></span>

<span data-ttu-id="1d835-112">toocreate un'app web e configurarlo toorun contenitore Docker personalizzato, è possibile utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1d835-112">toocreate a web app and configuring it toorun a custom Docker container, you can use hello following command:</span></span>

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -i elnably/dockerimagetest
```
 
## <a name="activate-hello-docker-container-logging"></a><span data-ttu-id="1d835-113">Attivare la registrazione di contenitore Docker hello</span><span class="sxs-lookup"><span data-stu-id="1d835-113">Activate hello Docker container logging</span></span>

<span data-ttu-id="1d835-114">tooactivate hello registrazione contenitore Docker, è possibile usare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1d835-114">tooactivate hello Docker container logging, you can use hello following command:</span></span>

```azurecli-interactive
az webapp log config -n sname -g rgname --web-server-logging filesystem
```
 
## <a name="change-hello-custom-docker-container-for-an-existing-web-app-on-linux-app"></a><span data-ttu-id="1d835-115">Modifica contenitore Docker personalizzata hello per un'App Web esistente in App di Linux</span><span class="sxs-lookup"><span data-stu-id="1d835-115">Change hello custom Docker container for an existing Web App on Linux App</span></span>

<span data-ttu-id="1d835-116">toochange un'app creata in precedenza, da hello corrente Docker immagine tooa nuova immagine, è possibile utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1d835-116">toochange a previously created app, from hello current Docker image tooa new image, you can use hello following command:</span></span>

```azurecli-interactive
az webapp config container set -n sname -g rgname -c apurvajo/mariohtml5
``` 

## <a name="using-docker-images-from-a-private-registry"></a><span data-ttu-id="1d835-117">Utilizzo di immagini Docker da un registro privato</span><span class="sxs-lookup"><span data-stu-id="1d835-117">Using Docker images from a private registry</span></span>

<span data-ttu-id="1d835-118">È possibile configurare delle immagini dell'app toouse un registro di sistema privato.</span><span class="sxs-lookup"><span data-stu-id="1d835-118">You can configure your app toouse images from a private registry.</span></span> <span data-ttu-id="1d835-119">È necessario tooprovide hello url per il Registro di sistema, un nome utente e password.</span><span class="sxs-lookup"><span data-stu-id="1d835-119">You need tooprovide hello url for your registry, user name, and password.</span></span> <span data-ttu-id="1d835-120">Questa operazione può essere eseguita mediante hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1d835-120">This can be achieved using hello following command:</span></span>

```azurecli-interactive
az webapp config container set -n sname1 -g rgname -c <container name> -r <server url> -u <username> -p <password>
``` 

## <a name="enable-continuous-deployments-for-custom-docker-images"></a><span data-ttu-id="1d835-121">Abilitare la distribuzione continua per le immagini Docker personalizzate</span><span class="sxs-lookup"><span data-stu-id="1d835-121">Enable continuous deployments for custom Docker images</span></span>

<span data-ttu-id="1d835-122">Con hello comando seguente è possibile abilitare la funzionalità CD hello e ottenere l'url del webhook hello.</span><span class="sxs-lookup"><span data-stu-id="1d835-122">With hello following command you can enable hello CD functionality, and get hello webhook url.</span></span> <span data-ttu-id="1d835-123">Questo url può essere utilizzato tooconfigure si repository DockerHub o del Registro di sistema contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="1d835-123">This url can be used tooconfigure you DockerHub or Azure Container Registry repos.</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

## <a name="create-a-web-app-on-linux-app-using-one-of-our-built-in-runtime-frameworks"></a><span data-ttu-id="1d835-124">Creare un'App Web in App di Linux usando uno dei nostri Framework di runtime integrati</span><span class="sxs-lookup"><span data-stu-id="1d835-124">Create a Web App on Linux App using one of our built-in runtime frameworks</span></span>

<span data-ttu-id="1d835-125">toocreate un'App Web di PHP 5.6 sull'App di Linux, è possibile utilizzare hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="1d835-125">toocreate a PHP 5.6 Web App on Linux App that, you can use hello following command.</span></span>

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -r "php|5.6"
``` 

## <a name="change-framework-version-for-an-existing-web-app-on-linux-app"></a><span data-ttu-id="1d835-126">Modificare la versione del framework per un'App Web esistente in App di Linux</span><span class="sxs-lookup"><span data-stu-id="1d835-126">Change framework version for an existing Web App on Linux App</span></span>

<span data-ttu-id="1d835-127">toochange un'app creata in precedenza, da hello corrente framework versione tooNode.js 6.11, è possibile utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1d835-127">toochange a previously created app, from hello current framework version tooNode.js 6.11, you can use hello following command:</span></span>

```azurecli-interactive
az webapp config set -n sname -g rgname --linux-fx-version "node|6.11"
``` 

## <a name="set-up-git-deployments-for-your-web-app"></a><span data-ttu-id="1d835-128">Configurare le distribuzioni Git per l'App Web</span><span class="sxs-lookup"><span data-stu-id="1d835-128">Set up Git deployments for your Web App</span></span>

<span data-ttu-id="1d835-129">tooset le distribuzioni Git per l'app, è possibile utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1d835-129">tooset up Git deployments for your app, you can use hello following command:</span></span>

```azurecli-interactive
az webapp deployment source config -n sname -g rgname --repo-url <gitrepo url> --branch <branch>
``` 


## <a name="next-steps"></a><span data-ttu-id="1d835-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1d835-130">Next steps</span></span>
* [<span data-ttu-id="1d835-131">Definizione di App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="1d835-131">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="1d835-132">Installare l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="1d835-132">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
* [<span data-ttu-id="1d835-133">Azure Cloud Shell (anteprima)</span><span class="sxs-lookup"><span data-stu-id="1d835-133">Azure Cloud Shell (Preview)</span></span>](../cloud-shell/overview.md)
* [<span data-ttu-id="1d835-134">Configurare gli ambienti di gestione temporanea nel Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="1d835-134">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="1d835-135">Distribuzione continua con App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="1d835-135">Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)
