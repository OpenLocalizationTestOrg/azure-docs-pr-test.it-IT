---
title: Creare il primo contenitore di Istanze di contenitore di Azure | Azure Docs
description: Distribuire e iniziare a usare Istanze di contenitore di Azure
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 905f69e5e1e237a31d9bb1e326969ec83292c244
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-your-first-container-in-azure-container-instances"></a><span data-ttu-id="daf51-103">Creare il primo contenitore in Istanze di contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="daf51-103">Create your first container in Azure Container Instances</span></span>

<span data-ttu-id="daf51-104">Istanze di contenitore di Azure semplifica la creazione e la gestione dei contenitori in Azure.</span><span class="sxs-lookup"><span data-stu-id="daf51-104">Azure Container Instances makes it easy to create and manage containers in Azure.</span></span> <span data-ttu-id="daf51-105">In questa guida introduttiva si creerà un contenitore in Azure e lo si esporrà a Internet con un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="daf51-105">In this quick start, you will create a container in Azure and expose it to the internet with a public IP address.</span></span> <span data-ttu-id="daf51-106">Per completare questa operazione, è sufficiente un solo comando.</span><span class="sxs-lookup"><span data-stu-id="daf51-106">This operation is completed in a single command.</span></span> <span data-ttu-id="daf51-107">In pochi secondi, nel browser verrà visualizzato quanto segue:</span><span class="sxs-lookup"><span data-stu-id="daf51-107">Within just a few seconds, you will see this in your browser:</span></span>

![App distribuita usando Istanze di contenitore di Azure visualizzata nel browser][aci-app-browser]

<span data-ttu-id="daf51-109">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="daf51-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="daf51-110">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questa guida introduttiva è necessario eseguire l'interfaccia della riga di comando di Azure versione 2.0.12 o successiva.</span><span class="sxs-lookup"><span data-stu-id="daf51-110">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.12 or later.</span></span> <span data-ttu-id="daf51-111">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="daf51-111">Run `az --version` to find the version.</span></span> <span data-ttu-id="daf51-112">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="daf51-112">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="daf51-113">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="daf51-113">Create a resource group</span></span>

<span data-ttu-id="daf51-114">Le istanze di contenitore di Azure sono risorse di Azure e devono essere inserite in un gruppo di risorse di Azure, una raccolta logica in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="daf51-114">Azure Container Instances are Azure resources and must be placed in an Azure resource group, a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="daf51-115">Creare un gruppo di risorse con il comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="daf51-115">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="daf51-116">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroup* nella località *stati uniti orientali*.</span><span class="sxs-lookup"><span data-stu-id="daf51-116">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-container"></a><span data-ttu-id="daf51-117">Creare un contenitore</span><span class="sxs-lookup"><span data-stu-id="daf51-117">Create a container</span></span>

<span data-ttu-id="daf51-118">Per creare un contenitore, specificare un nome, un'immagine Docker e un gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="daf51-118">You can create a container by providing a name, a Docker image, and an Azure resource group.</span></span> <span data-ttu-id="daf51-119">È facoltativamente possibile esporre il contenitore a Internet con un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="daf51-119">You can optionally expose the container to the internet with a public IP address.</span></span> <span data-ttu-id="daf51-120">In questo caso, verrà usato un contenitore che ospita un'app Web molto semplice scritta in [Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="daf51-120">In this case, we'll use a container that hosts a very simple web app written in [Node.js](http://nodejs.org).</span></span>

```azurecli-interactive
az container create --name mycontainer --image microsoft/aci-helloworld --resource-group myResourceGroup --ip-address public 
```

<span data-ttu-id="daf51-121">In pochi secondi, verrà visualizzata una risposta alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="daf51-121">Within a few seconds, you should get a response to your request.</span></span> <span data-ttu-id="daf51-122">Il contenitore inizialmente presenterà lo stato **Creating**, ma verrà avviato entro alcuni secondi.</span><span class="sxs-lookup"><span data-stu-id="daf51-122">Initially, the container will be in a **Creating** state, but it should start within a few seconds.</span></span> <span data-ttu-id="daf51-123">È possibile controllare lo stato usando il comando `show`:</span><span class="sxs-lookup"><span data-stu-id="daf51-123">You can check the status using the `show` command:</span></span>

```azurecli-interactive
az container show --name mycontainer --resource-group myResourceGroup
```

<span data-ttu-id="daf51-124">Nella parte inferiore dell'output verranno visualizzati lo stato del provisioning e l'indirizzo IP del contenitore:</span><span class="sxs-lookup"><span data-stu-id="daf51-124">At the bottom of the output, you will see the container's provisioning state and its IP address:</span></span>

```json
...
"ipAddress": {
      "ip": "13.88.8.148",
      "ports": [
        {
          "port": 80,
          "protocol": "TCP"
        }
      ]
    },
    "osType": "Linux",
    "provisioningState": "Succeeded"
...
```

<span data-ttu-id="daf51-125">Dopo che lo stato del contenitore è diventato **Succeeded**, è possibile raggiungerlo nel browser usando l'indirizzo IP fornito.</span><span class="sxs-lookup"><span data-stu-id="daf51-125">Once the container moves to the **Succeeded** state, you can reach it in the browser using the IP address provided.</span></span> 

![App distribuita usando Istanze di contenitore di Azure visualizzata nel browser][aci-app-browser]

## <a name="pull-the-container-logs"></a><span data-ttu-id="daf51-127">Effettuare il pull dei log del contenitore</span><span class="sxs-lookup"><span data-stu-id="daf51-127">Pull the container logs</span></span>

<span data-ttu-id="daf51-128">È possibile effettuare il pull dei log per il contenitore creato usando il comando `logs`:</span><span class="sxs-lookup"><span data-stu-id="daf51-128">You can pull the logs for the container you created using the `logs` command:</span></span>

```azurecli-interactive
az container logs --name mycontainer --resource-group myResourceGroup
```

<span data-ttu-id="daf51-129">Output:</span><span class="sxs-lookup"><span data-stu-id="daf51-129">Output:</span></span>

```bash
listening on port 80
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://104.210.39.122/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="delete-the-container"></a><span data-ttu-id="daf51-130">Eliminare il contenitore</span><span class="sxs-lookup"><span data-stu-id="daf51-130">Delete the container</span></span>

<span data-ttu-id="daf51-131">Quando il contenitore non è più necessario, è possibile rimuoverlo usando il comando `delete`:</span><span class="sxs-lookup"><span data-stu-id="daf51-131">When you are done with the container, you can remove it using the `delete` command:</span></span>

```azurecli-interactive
az container delete --name mycontainer --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="daf51-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="daf51-132">Next steps</span></span>

<span data-ttu-id="daf51-133">Tutto il codice per il contenitore usato in questa guida introduttiva è disponibile [su GitHub][app-github-repo], con il documento Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="daf51-133">All of the code for the container used in this quick start is available [on GitHub][app-github-repo], along with its Dockerfile.</span></span> <span data-ttu-id="daf51-134">Per provare a compilarlo personalmente e a distribuirlo in Istanze di contenitore di Azure usando il Registro contenitori di Azure, passare all'esercitazione su Istanze di contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="daf51-134">If you'd like to try building it yourself and deploying it to Azure Container Instances using the Azure Container Registry, continue to the Azure Container Instances tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="daf51-135">Esercitazioni su Istanze di contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="daf51-135">Azure Container Instances tutorials</span></span>](./container-instances-tutorial-prepare-app.md)


<!-- LINKS -->
[app-github-repo]: https://github.com/Azure-Samples/aci-helloworld.git

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png