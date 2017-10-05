---
title: Esercitazione di Istanze di contenitore di Azure - Distribuire un'app | Microsoft Docs
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
ms.openlocfilehash: 54151a5c1850ab7120fe666a46dc5dc99c0f5157
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-container-to-azure-container-instances"></a><span data-ttu-id="e90af-103">Distribuire un contenitore in Istanze di contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="e90af-103">Deploy a container to Azure Container Instances</span></span>

<span data-ttu-id="e90af-104">Questa è l'ultima di un'esercitazione in tre parti.</span><span class="sxs-lookup"><span data-stu-id="e90af-104">This is the last of a three-part tutorial.</span></span> <span data-ttu-id="e90af-105">Nelle sezioni precedenti, [un'immagine del contenitore è stata creata](container-instances-tutorial-prepare-app.md) e [inserita in un'istanza di Registro contenitori di Azure](container-instances-tutorial-prepare-acr.md).</span><span class="sxs-lookup"><span data-stu-id="e90af-105">In previous sections, [a container image was created](container-instances-tutorial-prepare-app.md) and [pushed to an Azure Container Registry](container-instances-tutorial-prepare-acr.md).</span></span> <span data-ttu-id="e90af-106">Questa sezione completa l'esercitazione distribuendo il contenitore in Istanze di contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="e90af-106">This section completes the tutorial by deploying the container to Azure Container Instances.</span></span> <span data-ttu-id="e90af-107">I passaggi completati comprendono:</span><span class="sxs-lookup"><span data-stu-id="e90af-107">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e90af-108">Definizione di un gruppo di contenitori usando un modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e90af-108">Defining a container group using an Azure Resource Manager template</span></span>
> * <span data-ttu-id="e90af-109">Distribuzione del gruppo di contenitori tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="e90af-109">Deploying the container group using the Azure CLI</span></span>
> * <span data-ttu-id="e90af-110">Visualizzare i log dei contenitori</span><span class="sxs-lookup"><span data-stu-id="e90af-110">Viewing container logs</span></span>

## <a name="deploy-the-container-using-the-azure-cli"></a><span data-ttu-id="e90af-111">Distribuire il contenitore tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="e90af-111">Deploy the container using the Azure CLI</span></span>

<span data-ttu-id="e90af-112">L'interfaccia della riga di comando di Azure consente di distribuire un contenitore in Istanze di contenitore di Azure con un unico comando.</span><span class="sxs-lookup"><span data-stu-id="e90af-112">The Azure CLI enables deployment of a container to Azure Container Instances in a single command.</span></span> <span data-ttu-id="e90af-113">L'immagine del contenitore è ospitata nell'istanza privata di Registro contenitori di Azure, quindi è necessario includere le credenziali necessarie per l'accesso.</span><span class="sxs-lookup"><span data-stu-id="e90af-113">Since the container image is hosted in the private Azure Container Registry, you must include the credentials required to access it.</span></span> <span data-ttu-id="e90af-114">Se necessario, è possibile trovarle con una query come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="e90af-114">If necessary, you can query them as shown below.</span></span>

<span data-ttu-id="e90af-115">Server di accesso del registro contenitori (sostituire con il nome del registro):</span><span class="sxs-lookup"><span data-stu-id="e90af-115">Container registry login server (update with your registry name):</span></span>

```azurecli-interactive
az acr show --name <acrName> --query loginServer
```

<span data-ttu-id="e90af-116">Password del registro contenitori:</span><span class="sxs-lookup"><span data-stu-id="e90af-116">Container registry password:</span></span>

```azurecli-interactive
az acr credential show --name <acrName> --query "passwords[0].value"
```

<span data-ttu-id="e90af-117">Per distribuire l'immagine del contenitore dal registro contenitori con una richiesta di risorse di 1 core CPU e 1 GB di memoria, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="e90af-117">To deploy your container image from the container registry with a resource request of 1 CPU core and 1GB of memory, run the following command:</span></span>

```azurecli-interactive
az container create --name aci-tutorial-app --image <acrLoginServer>/aci-tutorial-app:v1 --cpu 1 --memory 1 --registry-password <acrPassword> --ip-address public -g myResourceGroup
```

<span data-ttu-id="e90af-118">Entro pochi secondi si riceverà una risposta iniziale da Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e90af-118">Within a few seconds, you will receive an initial response from Azure Resource Manager.</span></span> <span data-ttu-id="e90af-119">Per visualizzare lo stato della distribuzione, usare:</span><span class="sxs-lookup"><span data-stu-id="e90af-119">To view the state of the deployment, use:</span></span>

```azurecli-interactive
az container show --name aci-tutorial-app --resource-group myResourceGroup --query state
```

<span data-ttu-id="e90af-120">È possibile continuare a eseguire questo comando finché lo stato non passa da *pending* a *running*.</span><span class="sxs-lookup"><span data-stu-id="e90af-120">We can continue running this command until the state changes from *pending* to *running*.</span></span> <span data-ttu-id="e90af-121">Sarà quindi possibile procedere.</span><span class="sxs-lookup"><span data-stu-id="e90af-121">Then we can proceed.</span></span>

## <a name="view-the-application-and-container-logs"></a><span data-ttu-id="e90af-122">Visualizzare l'applicazione e i log dei contenitori</span><span class="sxs-lookup"><span data-stu-id="e90af-122">View the application and container logs</span></span>

<span data-ttu-id="e90af-123">Dopo avere completato la distribuzione, aprire il browser all'indirizzo IP indicato nell'output del comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e90af-123">Once the deployment succeeds, open your browser to the IP address shown in the output of the following command:</span></span>

```bash
az container show --name aci-tutorial-app --resource-group myResourceGroup --query ipAddress.ip
```

```json
"13.88.176.27"
```

![App Hello World nel browser][aci-app-browser]

<span data-ttu-id="e90af-125">È anche possibile visualizzare l'output del log del contenitore:</span><span class="sxs-lookup"><span data-stu-id="e90af-125">You can also view the log output of the container:</span></span>

```azurecli-interactive
az container logs --name aci-tutorial-app -g myResourceGroup
```

<span data-ttu-id="e90af-126">Output:</span><span class="sxs-lookup"><span data-stu-id="e90af-126">Output:</span></span>

```bash
listening on port 80
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://13.88.176.27/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="next-steps"></a><span data-ttu-id="e90af-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e90af-127">Next steps</span></span>

<span data-ttu-id="e90af-128">In questa esercitazione sono stati distribuiti contenitori in Istanze di contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="e90af-128">In this tutorial, you completed the process of deploying your containers to Azure Container Instances.</span></span> <span data-ttu-id="e90af-129">Sono stati completati i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e90af-129">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e90af-130">Distribuzione del contenitore da Registro contenitori di Azure tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="e90af-130">Deploying the container from the Azure Container Registry using the Azure CLI</span></span>
> * <span data-ttu-id="e90af-131">Visualizzazione dell'applicazione nel browser</span><span class="sxs-lookup"><span data-stu-id="e90af-131">Viewing the application in the browser</span></span>
> * <span data-ttu-id="e90af-132">Visualizzare i log dei contenitori</span><span class="sxs-lookup"><span data-stu-id="e90af-132">Viewing the container logs</span></span>

<!-- LINKS -->
[prepare-app]: ./container-instances-tutorial-prepare-app.md

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png
