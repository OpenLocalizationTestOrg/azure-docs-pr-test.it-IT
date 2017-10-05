---
title: Esercitazione di Istanze di contenitore di Azure - Preparare Registro contenitori di Azure | Microsoft Docs
description: Esercitazione di Istanze di contenitore di Azure - Preparare Registro contenitori di Azure
services: container-instances
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, contenitori, Micro-Service, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: cc96ba9f5abd45a7503ba3327b30e1f809391384
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-and-use-azure-container-registry"></a><span data-ttu-id="9f6e7-104">Distribuire e usare il Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="9f6e7-104">Deploy and use Azure Container Registry</span></span>

<span data-ttu-id="9f6e7-105">Questa è la parte due di un'esercitazione in tre parti.</span><span class="sxs-lookup"><span data-stu-id="9f6e7-105">This is part two of a three-part tutorial.</span></span> <span data-ttu-id="9f6e7-106">Nel [passaggio precedente](./container-instances-tutorial-prepare-app.md) è stata creta un'immagine del contenitore per una semplice applicazione Web scritta in [Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="9f6e7-106">In the [previous step](./container-instances-tutorial-prepare-app.md), a container image was created for a simple web application written in [Node.js](http://nodejs.org).</span></span> <span data-ttu-id="9f6e7-107">In questa esercitazione viene eseguito il push di questa immagine in un'istanza di Registro contenitori di Azure.</span><span class="sxs-lookup"><span data-stu-id="9f6e7-107">In this tutorial, this image is pushed to an Azure Container Registry.</span></span> <span data-ttu-id="9f6e7-108">Se l'immagine del contenitore non è stata creata, tornare all'[Esercitazione 1 - Creare l'immagine del contenitore](./container-instances-tutorial-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="9f6e7-108">If you have not created the container image, return to [Tutorial 1 – Create container image](./container-instances-tutorial-prepare-app.md).</span></span> 

<span data-ttu-id="9f6e7-109">Registro contenitori di Azure è un registro privato basato su Azure per le immagini del contenitore Docker.</span><span class="sxs-lookup"><span data-stu-id="9f6e7-109">The Azure Container Registry is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="9f6e7-110">Questa esercitazione illustra la distribuzione di un'istanza di Registro contenitori di Azure e il push di un'immagine del contenitore in essa.</span><span class="sxs-lookup"><span data-stu-id="9f6e7-110">This tutorial walks through deploying an Azure Container Registry instance, and pushing a container image to it.</span></span> <span data-ttu-id="9f6e7-111">I passaggi completati comprendono:</span><span class="sxs-lookup"><span data-stu-id="9f6e7-111">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9f6e7-112">Distribuzione di un'istanza del Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="9f6e7-112">Deploying an Azure Container Registry instance</span></span>
> * <span data-ttu-id="9f6e7-113">Assegnazione di un tag all'immagine del contenitore per Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="9f6e7-113">Tagging container image for Azure Container Registry</span></span>
> * <span data-ttu-id="9f6e7-114">Caricamento dell'immagine in Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="9f6e7-114">Uploading image to Azure Container Registry</span></span>

<span data-ttu-id="9f6e7-115">Nelle esercitazioni successive si distribuirà il contenitore dal registro privato a Istanze di contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="9f6e7-115">In subsequent tutorials, you deploy the container from your private registry to Azure Container Instances.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9f6e7-116">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="9f6e7-116">Before you begin</span></span>

<span data-ttu-id="9f6e7-117">Questa esercitazione richiede l'interfaccia della riga di comando di Azure 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="9f6e7-117">This tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="9f6e7-118">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="9f6e7-118">Run `az --version` to find the version.</span></span> <span data-ttu-id="9f6e7-119">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9f6e7-119">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="9f6e7-120">Distribuire il Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="9f6e7-120">Deploy Azure Container Registry</span></span>

<span data-ttu-id="9f6e7-121">Prima di distribuire un Registro contenitori di Azure, è necessario che esista un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="9f6e7-121">When deploying an Azure Container Registry, you first need a resource group.</span></span> <span data-ttu-id="9f6e7-122">Un gruppo di risorse di Azure è una raccolta logica in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="9f6e7-122">An Azure resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="9f6e7-123">Creare un gruppo di risorse con il comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="9f6e7-123">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="9f6e7-124">In questo esempio viene creato un gruppo di risorse denominato *myResourceGroup* nell'area *eastus*.</span><span class="sxs-lookup"><span data-stu-id="9f6e7-124">In this example, a resource group named *myResourceGroup* is created in the *eastus* region.</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="9f6e7-125">Creare un Registro contenitori di Azure con il comando [az acr create](/cli/azure/acr#create).</span><span class="sxs-lookup"><span data-stu-id="9f6e7-125">Create an Azure Container registry with the [az acr create](/cli/azure/acr#create) command.</span></span> <span data-ttu-id="9f6e7-126">Il nome di un registro contenitori **deve essere univoco**.</span><span class="sxs-lookup"><span data-stu-id="9f6e7-126">The name of a Container Registry **must be unique**.</span></span> <span data-ttu-id="9f6e7-127">Nell'esempio seguente si usa il nome *mycontainerregistry082*.</span><span class="sxs-lookup"><span data-stu-id="9f6e7-127">In the following example, we use the name *mycontainerregistry082*.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name mycontainerregistry082 --sku Basic --admin-enabled true
```

<span data-ttu-id="9f6e7-128">Nella parte restante di questa esercitazione si usa `<acrname>` come segnaposto per il nome del registro contenitori scelto.</span><span class="sxs-lookup"><span data-stu-id="9f6e7-128">Throughout the rest of this tutorial, we use `<acrname>` as a placeholder for the container registry name that you chose.</span></span>

## <a name="container-registry-login"></a><span data-ttu-id="9f6e7-129">Accesso al registro contenitori</span><span class="sxs-lookup"><span data-stu-id="9f6e7-129">Container registry login</span></span>

<span data-ttu-id="9f6e7-130">È necessario accedere all'istanza del Registro contenitori di Azure prima di eseguire il push di immagini in essa.</span><span class="sxs-lookup"><span data-stu-id="9f6e7-130">You must log in to your ACR instance before pushing images to it.</span></span> <span data-ttu-id="9f6e7-131">Usare il comando [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) per completare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="9f6e7-131">Use the [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) command to complete the operation.</span></span> <span data-ttu-id="9f6e7-132">È necessario specificare il nome univoco assegnato al registro contenitori al momento della creazione.</span><span class="sxs-lookup"><span data-stu-id="9f6e7-132">You need to provide the unique name given to the container registry when it was created.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="9f6e7-133">Al termine, il comando restituisce un messaggio di accesso riuscito.</span><span class="sxs-lookup"><span data-stu-id="9f6e7-133">The command returns a 'Login Succeeded’ message once completed.</span></span>

## <a name="tag-container-image"></a><span data-ttu-id="9f6e7-134">Assegnare tag all'immagine del contenitore</span><span class="sxs-lookup"><span data-stu-id="9f6e7-134">Tag container image</span></span>

<span data-ttu-id="9f6e7-135">Per distribuire un'immagine del contenitore da un registro privato, all'immagine deve essere assegnato un tag con il nome `loginServer` del registro.</span><span class="sxs-lookup"><span data-stu-id="9f6e7-135">To deploy a container image from a private registry, the image needs to be tagged with the `loginServer` name of the registry.</span></span>

<span data-ttu-id="9f6e7-136">Per visualizzare un elenco di immagini correnti, usare il comando `docker images`.</span><span class="sxs-lookup"><span data-stu-id="9f6e7-136">To see a list of current images, use the `docker images` command.</span></span>

```bash
docker images
```

<span data-ttu-id="9f6e7-137">Output:</span><span class="sxs-lookup"><span data-stu-id="9f6e7-137">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

<span data-ttu-id="9f6e7-138">Per ottenere il nome loginServer, eseguire questo comando.</span><span class="sxs-lookup"><span data-stu-id="9f6e7-138">To get the loginServer name, run the following command.</span></span>

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

<span data-ttu-id="9f6e7-139">Applicare all'immagine *aci-tutorial-app* il tag del server di accesso del registro contenitori.</span><span class="sxs-lookup"><span data-stu-id="9f6e7-139">Tag the *aci-tutorial-app* image with the loginServer of the container registry.</span></span> <span data-ttu-id="9f6e7-140">Aggiungere anche `:v1` alla fine del nome dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="9f6e7-140">Also, add `:v1` to the end of the image name.</span></span> <span data-ttu-id="9f6e7-141">Questo tag indica il numero di versione dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="9f6e7-141">This tag indicates the image version number.</span></span>

```bash
docker tag aci-tutorial-app <acrLoginServer>/aci-tutorial-app:v1
```

<span data-ttu-id="9f6e7-142">Una volta applicato il tag, eseguire `docker images` per verificare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="9f6e7-142">Once tagged, run `docker images` to verify the operation.</span></span>

```bash
docker images
```

<span data-ttu-id="9f6e7-143">Output:</span><span class="sxs-lookup"><span data-stu-id="9f6e7-143">Output:</span></span>

```bash
REPOSITORY                                                TAG                 IMAGE ID            CREATED             SIZE
aci-tutorial-app                                          latest              5c745774dfa9        39 seconds ago      68.1 MB
mycontainerregistry082.azurecr.io/aci-tutorial-app        v1                  a9dace4e1a17        7 minutes ago       68.1 MB
```

## <a name="push-image-to-azure-container-registry"></a><span data-ttu-id="9f6e7-144">Eseguire il push dell'immagine in Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="9f6e7-144">Push image to Azure Container Registry</span></span>

<span data-ttu-id="9f6e7-145">Eseguire il push dell'immagine *aci-tutorial-app* nel registro.</span><span class="sxs-lookup"><span data-stu-id="9f6e7-145">Push the *aci-tutorial-app* image to the registry.</span></span>

<span data-ttu-id="9f6e7-146">Usando l'esempio seguente, sostituire il nome del server di accesso del registro contenitori con il nome del server di accesso dell'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="9f6e7-146">Using the following example, replace the container registry loginServer name with the loginServer from your environment.</span></span>

```bash
docker push <acrLoginServer>/aci-tutorial-app:v1
```

## <a name="list-images-in-azure-container-registry"></a><span data-ttu-id="9f6e7-147">Elencare le immagini in Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="9f6e7-147">List images in Azure Container Registry</span></span>

<span data-ttu-id="9f6e7-148">Per restituire un elenco di immagini di cui è stato eseguito il push nel Registro contenitori di Azure, usare il comando [az acr repository list](/cli/azure/acr/repository#list).</span><span class="sxs-lookup"><span data-stu-id="9f6e7-148">To return a list of images that have been pushed to your Azure Container registry, user the [az acr repository list](/cli/azure/acr/repository#list) command.</span></span> <span data-ttu-id="9f6e7-149">Aggiornare il comando con il nome del registro contenitori.</span><span class="sxs-lookup"><span data-stu-id="9f6e7-149">Update the command with the container registry name.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="9f6e7-150">Output:</span><span class="sxs-lookup"><span data-stu-id="9f6e7-150">Output:</span></span>

```azurecli
Result
----------------
aci-tutorial-app
```

<span data-ttu-id="9f6e7-151">Per visualizzare i tag per un'immagine specifica, usare il comando [az acr repository show-tags](/cli/azure/acr/repository#show-tags).</span><span class="sxs-lookup"><span data-stu-id="9f6e7-151">And then to see the tags for a specific image, use the [az acr repository show-tags](/cli/azure/acr/repository#show-tags) command.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository aci-tutorial-app --output table
```

<span data-ttu-id="9f6e7-152">Output:</span><span class="sxs-lookup"><span data-stu-id="9f6e7-152">Output:</span></span>

```azurecli
Result
--------
v1
```

## <a name="next-steps"></a><span data-ttu-id="9f6e7-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9f6e7-153">Next steps</span></span>

<span data-ttu-id="9f6e7-154">In questa esercitazione è stata preparata un'istanza di Registro contenitori di Azure da usare con Istanze di contenitore di Azure. È stato inoltre eseguito il push dell'immagine del contenitore.</span><span class="sxs-lookup"><span data-stu-id="9f6e7-154">In this tutorial, an Azure Container Registry was prepared for use with Azure Container Instances, and the container image was pushed.</span></span> <span data-ttu-id="9f6e7-155">Sono stati completati i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="9f6e7-155">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9f6e7-156">Distribuzione di un'istanza del Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="9f6e7-156">Deploying an Azure Container Registry instance</span></span>
> * <span data-ttu-id="9f6e7-157">Assegnazione di un tag all'immagine del contenitore per Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="9f6e7-157">Tagging container image for Azure Container Registry</span></span>
> * <span data-ttu-id="9f6e7-158">Caricamento dell'immagine in Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="9f6e7-158">Uploading image to Azure Container Registry</span></span>

<span data-ttu-id="9f6e7-159">Passare alla prossima esercitazione per informazioni sulla distribuzione del contenitore in Azure con Istanze di contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="9f6e7-159">Advance to the next tutorial to learn about deploying the container to Azure using Azure Container Instances.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9f6e7-160">Distribuire contenitori in Istanze di contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="9f6e7-160">Deploy containers to Azure Container Instances</span></span>](./container-instances-tutorial-deploy-app.md)
