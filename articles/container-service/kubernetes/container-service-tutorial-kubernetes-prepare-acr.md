---
title: esercitazione per il servizio contenitore aaaAzure - preparare ACR | Documenti Microsoft
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
ms.openlocfilehash: 3980e5ce4eb9836f83c761a2f76c944bb3f13060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-use-azure-container-registry"></a><span data-ttu-id="cc6cd-104">Distribuire e usare il Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="cc6cd-104">Deploy and use Azure Container Registry</span></span>

<span data-ttu-id="cc6cd-105">Il Registro contenitori di Azure è un registro privato basato su Azure per le immagini del contenitore Docker.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-105">Azure Container Registry (ACR) is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="cc6cd-106">Questa esercitazione, la seconda parte della sette, illustra la distribuzione di un'istanza del Registro di sistema di Azure contenitore e inserendo un tooit immagine contenitore.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-106">This tutorial, part two of seven, walks through deploying an Azure Container Registry instance, and pushing a container image tooit.</span></span> <span data-ttu-id="cc6cd-107">I passaggi completati comprendono:</span><span class="sxs-lookup"><span data-stu-id="cc6cd-107">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cc6cd-108">Distribuzione di un'istanza di Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="cc6cd-108">Deploying an Azure Container Registry (ACR) instance</span></span>
> * <span data-ttu-id="cc6cd-109">Assegnazione di tag a un'immagine del contenitore per Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="cc6cd-109">Tagging a container image for ACR</span></span>
> * <span data-ttu-id="cc6cd-110">Caricamento hello immagine tooACR</span><span class="sxs-lookup"><span data-stu-id="cc6cd-110">Uploading hello image tooACR</span></span>

<span data-ttu-id="cc6cd-111">Nelle esercitazioni successive, questa istanza del registro contenitori di Azure viene integrata con un cluster Kubernetes del servizio contenitore di Azure, per eseguire in modo sicuro le immagini del contenitore.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-111">In subsequent tutorials, this ACR instance is integrated with an Azure Container Service Kubernetes cluster, for securely running container images.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="cc6cd-112">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="cc6cd-112">Before you begin</span></span>

<span data-ttu-id="cc6cd-113">In hello [esercitazione precedente](./container-service-tutorial-kubernetes-prepare-app.md), un'immagine contenitore è stata creata per una semplice applicazione di Azure di voto.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-113">In hello [previous tutorial](./container-service-tutorial-kubernetes-prepare-app.md), a container image was created for a simple Azure Voting application.</span></span> <span data-ttu-id="cc6cd-114">In questa esercitazione, questa immagine viene inserita tooan del Registro di sistema contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-114">In this tutorial, this image is pushed tooan Azure Container Registry.</span></span> <span data-ttu-id="cc6cd-115">Se non è stato creato immagine dell'app di Azure voto hello, restituire troppo[esercitazione 1: creare le immagini contenitore](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="cc6cd-115">If you have not created hello Azure Voting app image, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> <span data-ttu-id="cc6cd-116">In alternativa, passaggi hello descritto in questo punto utilizzare qualsiasi immagine contenitore.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-116">Alternatively, hello steps detailed here work with any container image.</span></span>

<span data-ttu-id="cc6cd-117">Questa esercitazione, è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-117">This tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="cc6cd-118">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-118">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="cc6cd-119">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="cc6cd-119">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="cc6cd-120">Distribuire il Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="cc6cd-120">Deploy Azure Container Registry</span></span>

<span data-ttu-id="cc6cd-121">Prima di distribuire un Registro contenitori di Azure, è necessario che esista un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-121">When deploying an Azure Container Registry, you first need a resource group.</span></span> <span data-ttu-id="cc6cd-122">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-122">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="cc6cd-123">Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-123">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="cc6cd-124">In questo esempio, un gruppo di risorse denominato *myResourceGroup* viene creato in hello *westeurope* area.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-124">In this example, a resource group named *myResourceGroup* is created in hello *westeurope* region.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="cc6cd-125">Creare un registro di sistema del contenitore di Azure con hello [az acr creare](/cli/azure/acr#create) comando.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-125">Create an Azure Container registry with hello [az acr create](/cli/azure/acr#create) command.</span></span> <span data-ttu-id="cc6cd-126">nome di un contenitore del Registro di sistema di Hello **deve essere univoco**.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-126">hello name of a Container Registry **must be unique**.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Basic --admin-enabled true
```

<span data-ttu-id="cc6cd-127">Tutta hello di questa esercitazione, utilizziamo "acrname" come segnaposto per nome del Registro di sistema del contenitore hello scelto.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-127">Throughout hello rest of this tutorial, we use "acrname" as a placeholder for hello container registry name that you chose.</span></span>

## <a name="container-registry-login"></a><span data-ttu-id="cc6cd-128">Accesso al registro contenitori</span><span class="sxs-lookup"><span data-stu-id="cc6cd-128">Container registry login</span></span>

<span data-ttu-id="cc6cd-129">È necessario accedere in istanza ACR tooyour prima push tooit immagini.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-129">You must log in tooyour ACR instance before pushing images tooit.</span></span> <span data-ttu-id="cc6cd-130">Hello utilizzare [accesso acr az](https://docs.microsoft.com/en-us/cli/azure/acr#login) operazione hello toocomplete di comando.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-130">Use hello [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) command toocomplete hello operation.</span></span> <span data-ttu-id="cc6cd-131">È necessario il nome univoco di tooprovide hello assegnato del Registro di sistema di toohello contenitore al momento della creazione.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-131">You need tooprovide hello unique name given toohello container registry when it was created.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="cc6cd-132">comando Hello restituisce un messaggio 'Accesso riuscito' una volta completato.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-132">hello command returns a 'Login Succeeded’ message once completed.</span></span>

## <a name="tag-container-images"></a><span data-ttu-id="cc6cd-133">Assegnare tag alle immagini del contenitore</span><span class="sxs-lookup"><span data-stu-id="cc6cd-133">Tag container images</span></span>

<span data-ttu-id="cc6cd-134">Ogni immagine di contenitore deve toobe contrassegnato con il nome loginServer hello del Registro di sistema hello.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-134">Each container image needs toobe tagged with hello loginServer name of hello registry.</span></span> <span data-ttu-id="cc6cd-135">Questo tag viene usato per il routing quando push del Registro di sistema di contenitore immagini tooan immagine.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-135">This tag is used for routing when pushing container images tooan image registry.</span></span>

<span data-ttu-id="cc6cd-136">un elenco di immagini corrente, utilizzare hello toosee [immagini docker](https://docs.docker.com/engine/reference/commandline/images/) comando.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-136">toosee a list of current images, use hello [docker images](https://docs.docker.com/engine/reference/commandline/images/) command.</span></span>

```bash
docker images
```

<span data-ttu-id="cc6cd-137">Output:</span><span class="sxs-lookup"><span data-stu-id="cc6cd-137">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front             latest              4675398c9172        13 minutes ago      694MB
redis                        latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask               788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="cc6cd-138">tooget hello loginServer nome eseguire hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-138">tooget hello loginServer name, run hello following command.</span></span>

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

<span data-ttu-id="cc6cd-139">A questo punto, hello di tag *azure voto-anteriore* immagine con loginServer hello del Registro di sistema di hello contenitore.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-139">Now, tag hello *azure-vote-front* image with hello loginServer of hello container registry.</span></span> <span data-ttu-id="cc6cd-140">Inoltre, aggiungere `:redis-v1` toohello fine del nome dell'immagine hello.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-140">Also, add `:redis-v1` toohello end of hello image name.</span></span> <span data-ttu-id="cc6cd-141">Questo tag indica una versione dell'immagine hello.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-141">This tag indicates hello image version.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v1
```

<span data-ttu-id="cc6cd-142">Una volta contrassegnate, eseguire [immagini docker] operazione di hello tooverify (https://docs.docker.com/engine/reference/commandline/images/).</span><span class="sxs-lookup"><span data-stu-id="cc6cd-142">Once tagged, run [docker images] (https://docs.docker.com/engine/reference/commandline/images/) tooverify hello operation.</span></span>

```bash
docker images
```

<span data-ttu-id="cc6cd-143">Output:</span><span class="sxs-lookup"><span data-stu-id="cc6cd-143">Output:</span></span>

```bash
REPOSITORY                                           TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front                                     latest              eaf2b9c57e5e        8 minutes ago       716 MB
mycontainerregistry082.azurecr.io/azure-vote-front   redis-v1            eaf2b9c57e5e        8 minutes ago       716 MB
redis                                                latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask                           flask               788ca94b2313        8 months ago        694 MB
```

## <a name="push-images-tooregistry"></a><span data-ttu-id="cc6cd-144">Push tooregistry immagini</span><span class="sxs-lookup"><span data-stu-id="cc6cd-144">Push images tooregistry</span></span>

<span data-ttu-id="cc6cd-145">Push hello *azure voto-anteriore* registro toohello di immagini.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-145">Push hello *azure-vote-front* image toohello registry.</span></span> 

<span data-ttu-id="cc6cd-146">Utilizzando hello di esempio seguente, sostituire nome loginServer di hello ACR con loginServer hello dall'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-146">Using hello following example, replace hello ACR loginServer name with hello loginServer from your environment.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v1
```

<span data-ttu-id="cc6cd-147">Questa operazione richiede un paio di minuti toocomplete.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-147">This takes a couple of minutes toocomplete.</span></span>

## <a name="list-images-in-registry"></a><span data-ttu-id="cc6cd-148">Elencare le immagini nel registro</span><span class="sxs-lookup"><span data-stu-id="cc6cd-148">List images in registry</span></span>

<span data-ttu-id="cc6cd-149">un elenco di immagini che sono stati inseriti tooyour Azure contenitore del Registro di sistema, hello utente tooreturn [elenco repository di az acr](/cli/azure/acr/repository#list) comando.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-149">tooreturn a list of images that have been pushed tooyour Azure Container registry, user hello [az acr repository list](/cli/azure/acr/repository#list) command.</span></span> <span data-ttu-id="cc6cd-150">Aggiornare il comando hello con il nome di istanza ACR hello.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-150">Update hello command with hello ACR instance name.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="cc6cd-151">Output:</span><span class="sxs-lookup"><span data-stu-id="cc6cd-151">Output:</span></span>

```azurecli
Result
----------------
azure-vote-front
```

<span data-ttu-id="cc6cd-152">Quindi tag hello toosee per un'immagine specifica, utilizzare hello [az acr repository Mostra-tag](/cli/azure/acr/repository#show-tags) comando.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-152">And then toosee hello tags for a specific image, use hello [az acr repository show-tags](/cli/azure/acr/repository#show-tags) command.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository azure-vote-front --output table
```

<span data-ttu-id="cc6cd-153">Output:</span><span class="sxs-lookup"><span data-stu-id="cc6cd-153">Output:</span></span>

```azurecli
Result
--------
redis-v1
```

<span data-ttu-id="cc6cd-154">Al termine dell'esercitazione, l'immagine contenitore hello è stato archiviato in un'istanza del Registro di sistema di Azure contenitore privata.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-154">At tutorial completion, hello container image has been stored in a private Azure Container Registry instance.</span></span> <span data-ttu-id="cc6cd-155">Questa immagine viene distribuita dal cluster di record tooa Kubernetes nelle esercitazioni successive.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-155">This image is deployed from ACR tooa Kubernetes cluster in subsequent tutorials.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc6cd-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cc6cd-156">Next steps</span></span>

<span data-ttu-id="cc6cd-157">In questa esercitazione un Registro contenitori di Azure è stato preparato per l'uso in un cluster Kubernetes del servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-157">In this tutorial, an Azure Container Registry was prepared for use in an ACS Kubernetes cluster.</span></span> <span data-ttu-id="cc6cd-158">sono stata completata Hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="cc6cd-158">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cc6cd-159">Distribuzione di un'istanza di Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="cc6cd-159">Deployed an Azure Container Registry instance</span></span>
> * <span data-ttu-id="cc6cd-160">Assegnazione di tag a un'immagine del contenitore per Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="cc6cd-160">Tagged a container image for ACR</span></span>
> * <span data-ttu-id="cc6cd-161">TooACR immagine hello caricato</span><span class="sxs-lookup"><span data-stu-id="cc6cd-161">Uploaded hello image tooACR</span></span>

<span data-ttu-id="cc6cd-162">Spostare toohello Avanti toolearn esercitazione sulla distribuzione di un cluster Kubernetes in Azure.</span><span class="sxs-lookup"><span data-stu-id="cc6cd-162">Advance toohello next tutorial toolearn about deploying a Kubernetes cluster in Azure.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="cc6cd-163">[Distribuire un cluster Kubernetes](./container-service-tutorial-kubernetes-deploy-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="cc6cd-163">[Deploy Kubernetes cluster](./container-service-tutorial-kubernetes-deploy-cluster.md)</span></span>