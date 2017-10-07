---
title: esercitazione per istanze di contenitori aaaAzure - distribuire app | Documenti Microsoft
description: Esercitazione di Istanze di contenitore di Azure - Distribuire un'app
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: b9fb098d9491e1073f0be4b14a0b9b1a18f16095
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-container-tooazure-container-instances"></a><span data-ttu-id="b3e73-103">Distribuire un tooAzure contenitore istanze di contenitori</span><span class="sxs-lookup"><span data-stu-id="b3e73-103">Deploy a container tooAzure Container Instances</span></span>

<span data-ttu-id="b3e73-104">Si tratta di hello ultimo di un'esercitazione in tre parti.</span><span class="sxs-lookup"><span data-stu-id="b3e73-104">This is hello last of a three-part tutorial.</span></span> <span data-ttu-id="b3e73-105">Nelle sezioni precedenti, [è stata creata un'immagine contenitore](container-instances-tutorial-prepare-app.md) e [inserito tooan del Registro di sistema di Azure contenitore](container-instances-tutorial-prepare-acr.md).</span><span class="sxs-lookup"><span data-stu-id="b3e73-105">In previous sections, [a container image was created](container-instances-tutorial-prepare-app.md) and [pushed tooan Azure Container Registry](container-instances-tutorial-prepare-acr.md).</span></span> <span data-ttu-id="b3e73-106">In questa sezione viene completata l'esercitazione hello distribuendo hello contenitore tooAzure istanze di contenitori.</span><span class="sxs-lookup"><span data-stu-id="b3e73-106">This section completes hello tutorial by deploying hello container tooAzure Container Instances.</span></span> <span data-ttu-id="b3e73-107">I passaggi completati comprendono:</span><span class="sxs-lookup"><span data-stu-id="b3e73-107">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b3e73-108">Definizione di un gruppo di contenitori usando un modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b3e73-108">Defining a container group using an Azure Resource Manager template</span></span>
> * <span data-ttu-id="b3e73-109">Distribuzione di gruppo contenitore hello utilizzando hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="b3e73-109">Deploying hello container group using hello Azure CLI</span></span>
> * <span data-ttu-id="b3e73-110">Visualizzare i log dei contenitori</span><span class="sxs-lookup"><span data-stu-id="b3e73-110">Viewing container logs</span></span>

## <a name="deploy-hello-container-using-hello-azure-cli"></a><span data-ttu-id="b3e73-111">Distribuire il contenitore di hello utilizzando hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="b3e73-111">Deploy hello container using hello Azure CLI</span></span>

<span data-ttu-id="b3e73-112">Hello CLI di Azure consente la distribuzione di un contenitore tooAzure istanze di contenitori, in un unico comando.</span><span class="sxs-lookup"><span data-stu-id="b3e73-112">hello Azure CLI enables deployment of a container tooAzure Container Instances in a single command.</span></span> <span data-ttu-id="b3e73-113">Poiché l'immagine contenitore hello è ospitato in hello privato del Registro di sistema contenitore di Azure, è necessario includere tooaccess necessarie le credenziali di hello è.</span><span class="sxs-lookup"><span data-stu-id="b3e73-113">Since hello container image is hosted in hello private Azure Container Registry, you must include hello credentials required tooaccess it.</span></span> <span data-ttu-id="b3e73-114">Se necessario, è possibile trovarle con una query come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="b3e73-114">If necessary, you can query them as shown below.</span></span>

<span data-ttu-id="b3e73-115">Server di accesso del registro contenitori (sostituire con il nome del registro):</span><span class="sxs-lookup"><span data-stu-id="b3e73-115">Container registry login server (update with your registry name):</span></span>

```azurecli-interactive
az acr show --name <acrName> --query loginServer
```

<span data-ttu-id="b3e73-116">Password del registro contenitori:</span><span class="sxs-lookup"><span data-stu-id="b3e73-116">Container registry password:</span></span>

```azurecli-interactive
az acr credential show --name <acrName> --query "passwords[0].value"
```

<span data-ttu-id="b3e73-117">toodeploy immagine contenitore dal Registro di sistema di hello contenitore con una risorsa richiesta di 1 core CPU e 1GB di memoria, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b3e73-117">toodeploy your container image from hello container registry with a resource request of 1 CPU core and 1GB of memory, run hello following command:</span></span>

```azurecli-interactive
az container create --name aci-tutorial-app --image <acrLoginServer>/aci-tutorial-app:v1 --cpu 1 --memory 1 --registry-password <acrPassword> --ip-address public -g myResourceGroup
```

<span data-ttu-id="b3e73-118">Entro pochi secondi si riceverà una risposta iniziale da Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b3e73-118">Within a few seconds, you will receive an initial response from Azure Resource Manager.</span></span> <span data-ttu-id="b3e73-119">stato di hello tooview hello della distribuzione di, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="b3e73-119">tooview hello state of hello deployment, use:</span></span>

```azurecli-interactive
az container show --name aci-tutorial-app --resource-group myResourceGroup --query state
```

<span data-ttu-id="b3e73-120">È possibile continuare a eseguire questo comando fino a quando non hello stato cambia da *in sospeso* troppo*esecuzione*.</span><span class="sxs-lookup"><span data-stu-id="b3e73-120">We can continue running this command until hello state changes from *pending* too*running*.</span></span> <span data-ttu-id="b3e73-121">Sarà quindi possibile procedere.</span><span class="sxs-lookup"><span data-stu-id="b3e73-121">Then we can proceed.</span></span>

## <a name="view-hello-application-and-container-logs"></a><span data-ttu-id="b3e73-122">Visualizzare i log dell'applicazione e il contenitore di hello</span><span class="sxs-lookup"><span data-stu-id="b3e73-122">View hello application and container logs</span></span>

<span data-ttu-id="b3e73-123">Al termine della distribuzione di hello, aprire l'indirizzo IP di toohello browser illustrato nell'output di hello di hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b3e73-123">Once hello deployment succeeds, open your browser toohello IP address shown in hello output of hello following command:</span></span>

```bash
az container show --name aci-tutorial-app --resource-group myResourceGroup --query ipAddress.ip
```

```json
"13.88.176.27"
```

![Hello world app nel browser hello][aci-app-browser]

<span data-ttu-id="b3e73-125">È inoltre possibile visualizzare l'output del log del contenitore hello hello:</span><span class="sxs-lookup"><span data-stu-id="b3e73-125">You can also view hello log output of hello container:</span></span>

```azurecli-interactive
az container logs --name aci-tutorial-app -g myResourceGroup
```

<span data-ttu-id="b3e73-126">Output:</span><span class="sxs-lookup"><span data-stu-id="b3e73-126">Output:</span></span>

```bash
listening on port 80
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://13.88.176.27/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="next-steps"></a><span data-ttu-id="b3e73-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b3e73-127">Next steps</span></span>

<span data-ttu-id="b3e73-128">In questa esercitazione, il processo di hello distribuire le istanze di contenitori di tooAzure contenitori è completato.</span><span class="sxs-lookup"><span data-stu-id="b3e73-128">In this tutorial, you completed hello process of deploying your containers tooAzure Container Instances.</span></span> <span data-ttu-id="b3e73-129">sono stata completata Hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="b3e73-129">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b3e73-130">Distribuzione di contenitore hello dall'utilizzo del Registro di sistema di Azure contenitore hello hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="b3e73-130">Deploying hello container from hello Azure Container Registry using hello Azure CLI</span></span>
> * <span data-ttu-id="b3e73-131">Visualizzazione di un'applicazione hello in browser hello</span><span class="sxs-lookup"><span data-stu-id="b3e73-131">Viewing hello application in hello browser</span></span>
> * <span data-ttu-id="b3e73-132">Visualizzazione dei log di contenitore hello</span><span class="sxs-lookup"><span data-stu-id="b3e73-132">Viewing hello container logs</span></span>

<!-- LINKS -->
[prepare-app]: ./container-instances-tutorial-prepare-app.md

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png
