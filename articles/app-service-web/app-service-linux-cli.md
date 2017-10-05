---
title: Gestire App Web in Linux tramite interfaccia della riga di comando di Azure 2.0| Microsoft Docs
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
ms.openlocfilehash: 04aceecf0cb4cad5c838b7254bf7079a36bbd0d8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="manage-web-app-on-linux-using-azure-cli"></a><span data-ttu-id="1c243-104">Gestire App Web in Linux tramite interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="1c243-104">Manage Web App on Linux using Azure CLI</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="1c243-105">Utilizzando i comandi in questo articolo si è in grado di creare e gestire un'App Web in Linux con interfaccia della riga di comando di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="1c243-105">Using the commands in this article you are able to create and manage a Web App on Linux using Azure CLI 2.0.</span></span>
<span data-ttu-id="1c243-106">È possibile iniziare a usare la nuova versione dell'interfaccia della riga di comando in due modi:</span><span class="sxs-lookup"><span data-stu-id="1c243-106">You can start using the new version of the CLI in two ways:</span></span>

* <span data-ttu-id="1c243-107">[Installare l'interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) sul computer.</span><span class="sxs-lookup"><span data-stu-id="1c243-107">[Installing Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span>
* <span data-ttu-id="1c243-108">Utilizzare [Azure Cloud Shell (anteprima)](../cloud-shell/overview.md)</span><span class="sxs-lookup"><span data-stu-id="1c243-108">Using [Azure Cloud Shell (Preview)](../cloud-shell/overview.md)</span></span>


## <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="1c243-109">Creare un nuovo piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="1c243-109">Create a Linux App Service Plan</span></span>

<span data-ttu-id="1c243-110">Per creare un piano di servizio app Linux, è possibile utilizzare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1c243-110">To create a Linux App Service Plan, you can use the following command:</span></span>

```azurecli-interactive
az appservice plan create -n appname -g rgname --islinux -l "South Central US" --sku S1 --number-of-workers 1
``` 

## <a name="create-a-custom-docker-container-web-app"></a><span data-ttu-id="1c243-111">Creare un contenitore Docker personalizzato App Web</span><span class="sxs-lookup"><span data-stu-id="1c243-111">Create a custom Docker container Web App</span></span>

<span data-ttu-id="1c243-112">Per creare un'app Web e configurarla per l'esecuzione di un contenitore Docker personalizzato, è possibile utilizzare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1c243-112">To create a web app and configuring it to run a custom Docker container, you can use the following command:</span></span>

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -i elnably/dockerimagetest
```
 
## <a name="activate-the-docker-container-logging"></a><span data-ttu-id="1c243-113">Attivare la registrazione del contenitore Docker</span><span class="sxs-lookup"><span data-stu-id="1c243-113">Activate the Docker container logging</span></span>

<span data-ttu-id="1c243-114">Per attivare la registrazione del contenitore Docker è possibile usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1c243-114">To activate the Docker container logging, you can use the following command:</span></span>

```azurecli-interactive
az webapp log config -n sname -g rgname --web-server-logging filesystem
```
 
## <a name="change-the-custom-docker-container-for-an-existing-web-app-on-linux-app"></a><span data-ttu-id="1c243-115">Modificare il contenitore Docker personalizzato per un'App Web esistente in App di Linux</span><span class="sxs-lookup"><span data-stu-id="1c243-115">Change the custom Docker container for an existing Web App on Linux App</span></span>

<span data-ttu-id="1c243-116">Per modificare un'app creata in precedenza, dall'immagine del Docker attuale a una nuova immagine, è possibile utilizzare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1c243-116">To change a previously created app, from the current Docker image to a new image, you can use the following command:</span></span>

```azurecli-interactive
az webapp config container set -n sname -g rgname -c apurvajo/mariohtml5
``` 

## <a name="using-docker-images-from-a-private-registry"></a><span data-ttu-id="1c243-117">Utilizzo di immagini Docker da un registro privato</span><span class="sxs-lookup"><span data-stu-id="1c243-117">Using Docker images from a private registry</span></span>

<span data-ttu-id="1c243-118">È possibile configurare l'app per utilizzare le immagini da un registro di sistema privato.</span><span class="sxs-lookup"><span data-stu-id="1c243-118">You can configure your app to use images from a private registry.</span></span> <span data-ttu-id="1c243-119">È necessario specificare l'url per il Registro di sistema, nome utente e password.</span><span class="sxs-lookup"><span data-stu-id="1c243-119">You need to provide the url for your registry, user name, and password.</span></span> <span data-ttu-id="1c243-120">È possibile fare ciò utilizzando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1c243-120">This can be achieved using the following command:</span></span>

```azurecli-interactive
az webapp config container set -n sname1 -g rgname -c <container name> -r <server url> -u <username> -p <password>
``` 

## <a name="enable-continuous-deployments-for-custom-docker-images"></a><span data-ttu-id="1c243-121">Abilitare la distribuzione continua per le immagini Docker personalizzate</span><span class="sxs-lookup"><span data-stu-id="1c243-121">Enable continuous deployments for custom Docker images</span></span>

<span data-ttu-id="1c243-122">Con il comando seguente è possibile abilitare la funzionalità CD e ottenere l'url del webhook.</span><span class="sxs-lookup"><span data-stu-id="1c243-122">With the following command you can enable the CD functionality, and get the webhook url.</span></span> <span data-ttu-id="1c243-123">Questo url consente di configurare il repository DockerHub o del Registro contenitori di Azure.</span><span class="sxs-lookup"><span data-stu-id="1c243-123">This url can be used to configure you DockerHub or Azure Container Registry repos.</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

## <a name="create-a-web-app-on-linux-app-using-one-of-our-built-in-runtime-frameworks"></a><span data-ttu-id="1c243-124">Creare un'App Web in App di Linux usando uno dei nostri Framework di runtime integrati</span><span class="sxs-lookup"><span data-stu-id="1c243-124">Create a Web App on Linux App using one of our built-in runtime frameworks</span></span>

<span data-ttu-id="1c243-125">Per creare un'App Web di PHP 5.6 sull'App di Linux, è possibile utilizzare il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="1c243-125">To create a PHP 5.6 Web App on Linux App that, you can use the following command.</span></span>

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -r "php|5.6"
``` 

## <a name="change-framework-version-for-an-existing-web-app-on-linux-app"></a><span data-ttu-id="1c243-126">Modificare la versione del framework per un'App Web esistente in App di Linux</span><span class="sxs-lookup"><span data-stu-id="1c243-126">Change framework version for an existing Web App on Linux App</span></span>

<span data-ttu-id="1c243-127">Per modificare un'applicazione creata in precedenza, dalla versione del framework corrente a Node.js 6.11, è possibile utilizzare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1c243-127">To change a previously created app, from the current framework version to Node.js 6.11, you can use the following command:</span></span>

```azurecli-interactive
az webapp config set -n sname -g rgname --linux-fx-version "node|6.11"
``` 

## <a name="set-up-git-deployments-for-your-web-app"></a><span data-ttu-id="1c243-128">Configurare le distribuzioni Git per l'App Web</span><span class="sxs-lookup"><span data-stu-id="1c243-128">Set up Git deployments for your Web App</span></span>

<span data-ttu-id="1c243-129">Per configurare le distribuzioni Git per l'app, è possibile utilizzare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1c243-129">To set up Git deployments for your app, you can use the following command:</span></span>

```azurecli-interactive
az webapp deployment source config -n sname -g rgname --repo-url <gitrepo url> --branch <branch>
``` 


## <a name="next-steps"></a><span data-ttu-id="1c243-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1c243-130">Next steps</span></span>
* [<span data-ttu-id="1c243-131">Definizione di App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="1c243-131">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="1c243-132">Installare l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="1c243-132">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
* [<span data-ttu-id="1c243-133">Azure Cloud Shell (anteprima)</span><span class="sxs-lookup"><span data-stu-id="1c243-133">Azure Cloud Shell (Preview)</span></span>](../cloud-shell/overview.md)
* [<span data-ttu-id="1c243-134">Configurare gli ambienti di gestione temporanea nel Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="1c243-134">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="1c243-135">Distribuzione continua con App Web di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="1c243-135">Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)
