---
title: Esercitazione sul servizio contenitore di Azure - Preparare il Registro contenitori di Azure | Microsoft Docs
description: Esercitazione sul servizio contenitore di Azure - Preparare il Registro contenitori di Azure
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, contenitori, Micro-Service, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 3e1f7617bf2fc52ee4c15598f51a46276f4dc57d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-and-use-azure-container-registry"></a><span data-ttu-id="b3830-104">Distribuire e usare il Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="b3830-104">Deploy and use Azure Container Registry</span></span>

<span data-ttu-id="b3830-105">Il Registro contenitori di Azure è un registro privato basato su Azure per le immagini del contenitore Docker.</span><span class="sxs-lookup"><span data-stu-id="b3830-105">Azure Container Registry (ACR) is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="b3830-106">Questa esercitazione, parte due di sette, illustra la distribuzione di un'istanza di Registro contenitori di Azure e il push di un'immagine del contenitore al suo interno.</span><span class="sxs-lookup"><span data-stu-id="b3830-106">This tutorial, part two of seven, walks through deploying an Azure Container Registry instance, and pushing a container image to it.</span></span> <span data-ttu-id="b3830-107">I passaggi completati comprendono:</span><span class="sxs-lookup"><span data-stu-id="b3830-107">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b3830-108">Distribuzione di un'istanza di Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="b3830-108">Deploying an Azure Container Registry (ACR) instance</span></span>
> * <span data-ttu-id="b3830-109">Assegnazione di tag a un'immagine del contenitore per Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="b3830-109">Tagging a container image for ACR</span></span>
> * <span data-ttu-id="b3830-110">Caricamento dell'immagine in Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="b3830-110">Uploading the image to ACR</span></span>

<span data-ttu-id="b3830-111">Nelle esercitazioni successive, questa istanza del registro contenitori di Azure viene integrata con un cluster Kubernetes del servizio contenitore di Azure, per eseguire in modo sicuro le immagini del contenitore.</span><span class="sxs-lookup"><span data-stu-id="b3830-111">In subsequent tutorials, this ACR instance is integrated with an Azure Container Service Kubernetes cluster, for securely running container images.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="b3830-112">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="b3830-112">Before you begin</span></span>

<span data-ttu-id="b3830-113">Nell'[esercitazione precedente](./container-service-tutorial-kubernetes-prepare-app.md) è stata creta un'immagine del contenitore per una semplice applicazione Azure Voting.</span><span class="sxs-lookup"><span data-stu-id="b3830-113">In the [previous tutorial](./container-service-tutorial-kubernetes-prepare-app.md), a container image was created for a simple Azure Voting application.</span></span> <span data-ttu-id="b3830-114">In questa esercitazione viene eseguito il push di questa immagine in un'istanza di Registro contenitori di Azure.</span><span class="sxs-lookup"><span data-stu-id="b3830-114">In this tutorial, this image is pushed to an Azure Container Registry.</span></span> <span data-ttu-id="b3830-115">Se l'immagine dell'app Azure Vote non è stata creata, tornare all'[Esercitazione 1 - Creare immagini del contenitore](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="b3830-115">If you have not created the Azure Voting app image, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> <span data-ttu-id="b3830-116">In alternativa, la procedura illustrata di seguito funziona con qualsiasi immagine del contenitore.</span><span class="sxs-lookup"><span data-stu-id="b3830-116">Alternatively, the steps detailed here work with any container image.</span></span>

<span data-ttu-id="b3830-117">Questa esercitazione richiede l'interfaccia della riga di comando di Azure 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="b3830-117">This tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="b3830-118">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="b3830-118">Run `az --version` to find the version.</span></span> <span data-ttu-id="b3830-119">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b3830-119">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="b3830-120">Distribuire il Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="b3830-120">Deploy Azure Container Registry</span></span>

<span data-ttu-id="b3830-121">Prima di distribuire un Registro contenitori di Azure, è necessario che esista un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="b3830-121">When deploying an Azure Container Registry, you first need a resource group.</span></span> <span data-ttu-id="b3830-122">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="b3830-122">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="b3830-123">Creare un gruppo di risorse con il comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="b3830-123">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="b3830-124">In questo esempio viene creato un gruppo di risorse denominato *myResourceGroup* nell'area *westeurope*.</span><span class="sxs-lookup"><span data-stu-id="b3830-124">In this example, a resource group named *myResourceGroup* is created in the *westeurope* region.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="b3830-125">Creare un Registro contenitori di Azure con il comando [az acr create](/cli/azure/acr#create).</span><span class="sxs-lookup"><span data-stu-id="b3830-125">Create an Azure Container registry with the [az acr create](/cli/azure/acr#create) command.</span></span> <span data-ttu-id="b3830-126">Il nome di un registro contenitori **deve essere univoco**.</span><span class="sxs-lookup"><span data-stu-id="b3830-126">The name of a Container Registry **must be unique**.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Basic --admin-enabled true
```

<span data-ttu-id="b3830-127">Nella parte restante di questa esercitazione si usa "acrname" come segnaposto per il nome del registro contenitori scelto.</span><span class="sxs-lookup"><span data-stu-id="b3830-127">Throughout the rest of this tutorial, we use "acrname" as a placeholder for the container registry name that you chose.</span></span>

## <a name="container-registry-login"></a><span data-ttu-id="b3830-128">Accesso al registro contenitori</span><span class="sxs-lookup"><span data-stu-id="b3830-128">Container registry login</span></span>

<span data-ttu-id="b3830-129">È necessario accedere all'istanza del Registro contenitori di Azure prima di eseguire il push di immagini in essa.</span><span class="sxs-lookup"><span data-stu-id="b3830-129">You must log in to your ACR instance before pushing images to it.</span></span> <span data-ttu-id="b3830-130">Usare il comando [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) per completare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="b3830-130">Use the [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) command to complete the operation.</span></span> <span data-ttu-id="b3830-131">È necessario specificare il nome univoco assegnato al registro contenitori al momento della creazione.</span><span class="sxs-lookup"><span data-stu-id="b3830-131">You need to provide the unique name given to the container registry when it was created.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="b3830-132">Al termine, il comando restituisce un messaggio di accesso riuscito.</span><span class="sxs-lookup"><span data-stu-id="b3830-132">The command returns a 'Login Succeeded’ message once completed.</span></span>

## <a name="tag-container-images"></a><span data-ttu-id="b3830-133">Assegnare tag alle immagini del contenitore</span><span class="sxs-lookup"><span data-stu-id="b3830-133">Tag container images</span></span>

<span data-ttu-id="b3830-134">Ogni immagine del contenitore deve essere contrassegnata con il nome del server di accesso del registro.</span><span class="sxs-lookup"><span data-stu-id="b3830-134">Each container image needs to be tagged with the loginServer name of the registry.</span></span> <span data-ttu-id="b3830-135">Questo tag viene usato per il routing quando si esegue il push delle immagini del contenitore nel registro delle immagini.</span><span class="sxs-lookup"><span data-stu-id="b3830-135">This tag is used for routing when pushing container images to an image registry.</span></span>

<span data-ttu-id="b3830-136">Per visualizzare un elenco di immagini correnti, usare il comando [docker images](https://docs.docker.com/engine/reference/commandline/images/).</span><span class="sxs-lookup"><span data-stu-id="b3830-136">To see a list of current images, use the [docker images](https://docs.docker.com/engine/reference/commandline/images/) command.</span></span>

```bash
docker images
```

<span data-ttu-id="b3830-137">Output:</span><span class="sxs-lookup"><span data-stu-id="b3830-137">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front             latest              4675398c9172        13 minutes ago      694MB
redis                        latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask               788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="b3830-138">Per ottenere il nome loginServer, eseguire questo comando.</span><span class="sxs-lookup"><span data-stu-id="b3830-138">To get the loginServer name, run the following command.</span></span>

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

<span data-ttu-id="b3830-139">Applicare ora all'immagine *azure-vote-front* il tag loginServer del registro contenitori.</span><span class="sxs-lookup"><span data-stu-id="b3830-139">Now, tag the *azure-vote-front* image with the loginServer of the container registry.</span></span> <span data-ttu-id="b3830-140">Aggiungere anche `:redis-v1` alla fine del nome dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="b3830-140">Also, add `:redis-v1` to the end of the image name.</span></span> <span data-ttu-id="b3830-141">Questo tag indica la versione dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="b3830-141">This tag indicates the image version.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v1
```

<span data-ttu-id="b3830-142">Dopo aver assegnato il tag, eseguire [docker images] (https://docs.docker.com/engine/reference/commandline/images/) per verificare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="b3830-142">Once tagged, run [docker images] (https://docs.docker.com/engine/reference/commandline/images/) to verify the operation.</span></span>

```bash
docker images
```

<span data-ttu-id="b3830-143">Output:</span><span class="sxs-lookup"><span data-stu-id="b3830-143">Output:</span></span>

```bash
REPOSITORY                                           TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front                                     latest              eaf2b9c57e5e        8 minutes ago       716 MB
mycontainerregistry082.azurecr.io/azure-vote-front   redis-v1            eaf2b9c57e5e        8 minutes ago       716 MB
redis                                                latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask                           flask               788ca94b2313        8 months ago        694 MB
```

## <a name="push-images-to-registry"></a><span data-ttu-id="b3830-144">Eseguire il push delle immagini nel registro</span><span class="sxs-lookup"><span data-stu-id="b3830-144">Push images to registry</span></span>

<span data-ttu-id="b3830-145">Eseguire il push dell'immagine *azure-vote-front* nel registro.</span><span class="sxs-lookup"><span data-stu-id="b3830-145">Push the *azure-vote-front* image to the registry.</span></span> 

<span data-ttu-id="b3830-146">Nell'esempio seguente sostituire il nome del loginServer del Registro contenitori di Azure con il loginServer dell'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="b3830-146">Using the following example, replace the ACR loginServer name with the loginServer from your environment.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v1
```

<span data-ttu-id="b3830-147">Il completamento dell'operazione richiede alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="b3830-147">This takes a couple of minutes to complete.</span></span>

## <a name="list-images-in-registry"></a><span data-ttu-id="b3830-148">Elencare le immagini nel registro</span><span class="sxs-lookup"><span data-stu-id="b3830-148">List images in registry</span></span>

<span data-ttu-id="b3830-149">Per restituire un elenco di immagini di cui è stato eseguito il push nel Registro contenitori di Azure, usare il comando [az acr repository list](/cli/azure/acr/repository#list).</span><span class="sxs-lookup"><span data-stu-id="b3830-149">To return a list of images that have been pushed to your Azure Container registry, user the [az acr repository list](/cli/azure/acr/repository#list) command.</span></span> <span data-ttu-id="b3830-150">Aggiornare il comando con il nome dell'istanza del Registro contenitori di Azure.</span><span class="sxs-lookup"><span data-stu-id="b3830-150">Update the command with the ACR instance name.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="b3830-151">Output:</span><span class="sxs-lookup"><span data-stu-id="b3830-151">Output:</span></span>

```azurecli
Result
----------------
azure-vote-front
```

<span data-ttu-id="b3830-152">Per visualizzare i tag per un'immagine specifica, usare il comando [az acr repository show-tags](/cli/azure/acr/repository#show-tags).</span><span class="sxs-lookup"><span data-stu-id="b3830-152">And then to see the tags for a specific image, use the [az acr repository show-tags](/cli/azure/acr/repository#show-tags) command.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository azure-vote-front --output table
```

<span data-ttu-id="b3830-153">Output:</span><span class="sxs-lookup"><span data-stu-id="b3830-153">Output:</span></span>

```azurecli
Result
--------
redis-v1
```

<span data-ttu-id="b3830-154">Al termine dell'esercitazione, l'immagine del contenitore sarà stata archiviata in un'istanza privata di Registro contenitori di Azure.</span><span class="sxs-lookup"><span data-stu-id="b3830-154">At tutorial completion, the container image has been stored in a private Azure Container Registry instance.</span></span> <span data-ttu-id="b3830-155">Questa immagine verrà distribuita da Registro contenitori di Azure a un cluster Kubernetes nelle esercitazioni successive.</span><span class="sxs-lookup"><span data-stu-id="b3830-155">This image is deployed from ACR to a Kubernetes cluster in subsequent tutorials.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3830-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b3830-156">Next steps</span></span>

<span data-ttu-id="b3830-157">In questa esercitazione un Registro contenitori di Azure è stato preparato per l'uso in un cluster Kubernetes del servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="b3830-157">In this tutorial, an Azure Container Registry was prepared for use in an ACS Kubernetes cluster.</span></span> <span data-ttu-id="b3830-158">Sono stati completati i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b3830-158">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b3830-159">Distribuzione di un'istanza di Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="b3830-159">Deployed an Azure Container Registry instance</span></span>
> * <span data-ttu-id="b3830-160">Assegnazione di tag a un'immagine del contenitore per Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="b3830-160">Tagged a container image for ACR</span></span>
> * <span data-ttu-id="b3830-161">Caricamento dell'immagine in Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="b3830-161">Uploaded the image to ACR</span></span>

<span data-ttu-id="b3830-162">Passare all'esercitazione successiva per informazioni sulla distribuzione di un cluster Kubernetes in Azure.</span><span class="sxs-lookup"><span data-stu-id="b3830-162">Advance to the next tutorial to learn about deploying a Kubernetes cluster in Azure.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="b3830-163">[Distribuire un cluster Kubernetes](./container-service-tutorial-kubernetes-deploy-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="b3830-163">[Deploy Kubernetes cluster](./container-service-tutorial-kubernetes-deploy-cluster.md)</span></span>