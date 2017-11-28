---
title: esercitazione per istanze di contenitori aaaAzure - preparare Registro di sistema contenitore di Azure | Documenti Microsoft
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
ms.openlocfilehash: 2525626125740c3c861fad36aad207d0b587ff54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-use-azure-container-registry"></a><span data-ttu-id="c8bd1-104">Distribuire e usare il Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="c8bd1-104">Deploy and use Azure Container Registry</span></span>

<span data-ttu-id="c8bd1-105">Questa è la parte due di un'esercitazione in tre parti.</span><span class="sxs-lookup"><span data-stu-id="c8bd1-105">This is part two of a three-part tutorial.</span></span> <span data-ttu-id="c8bd1-106">In hello [passaggio precedente](./container-instances-tutorial-prepare-app.md), un'immagine contenitore è stata creata per un'applicazione web semplice scritta in [Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="c8bd1-106">In hello [previous step](./container-instances-tutorial-prepare-app.md), a container image was created for a simple web application written in [Node.js](http://nodejs.org).</span></span> <span data-ttu-id="c8bd1-107">In questa esercitazione, questa immagine viene inserita tooan del Registro di sistema contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="c8bd1-107">In this tutorial, this image is pushed tooan Azure Container Registry.</span></span> <span data-ttu-id="c8bd1-108">Se non è stato creato immagine contenitore hello, restituire troppo[esercitazione 1: immagine contenitore crea](./container-instances-tutorial-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="c8bd1-108">If you have not created hello container image, return too[Tutorial 1 – Create container image](./container-instances-tutorial-prepare-app.md).</span></span> 

<span data-ttu-id="c8bd1-109">Hello del Registro di sistema di Azure contenitore è un registro basato su Azure e privato, per le immagini contenitore Docker.</span><span class="sxs-lookup"><span data-stu-id="c8bd1-109">hello Azure Container Registry is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="c8bd1-110">In questa esercitazione vengono illustrati l'implementazione di un'istanza del Registro di sistema di Azure contenitore e inserendo un tooit immagine contenitore.</span><span class="sxs-lookup"><span data-stu-id="c8bd1-110">This tutorial walks through deploying an Azure Container Registry instance, and pushing a container image tooit.</span></span> <span data-ttu-id="c8bd1-111">I passaggi completati comprendono:</span><span class="sxs-lookup"><span data-stu-id="c8bd1-111">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c8bd1-112">Distribuzione di un'istanza del Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="c8bd1-112">Deploying an Azure Container Registry instance</span></span>
> * <span data-ttu-id="c8bd1-113">Assegnazione di un tag all'immagine del contenitore per Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="c8bd1-113">Tagging container image for Azure Container Registry</span></span>
> * <span data-ttu-id="c8bd1-114">Caricamento tooAzure immagine contenitore del Registro di sistema</span><span class="sxs-lookup"><span data-stu-id="c8bd1-114">Uploading image tooAzure Container Registry</span></span>

<span data-ttu-id="c8bd1-115">Nelle esercitazioni successive, distribuire contenitore hello dal tooAzure del Registro di sistema privata istanze di contenitori.</span><span class="sxs-lookup"><span data-stu-id="c8bd1-115">In subsequent tutorials, you deploy hello container from your private registry tooAzure Container Instances.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c8bd1-116">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="c8bd1-116">Before you begin</span></span>

<span data-ttu-id="c8bd1-117">Questa esercitazione, è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="c8bd1-117">This tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="c8bd1-118">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="c8bd1-118">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="c8bd1-119">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c8bd1-119">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="c8bd1-120">Distribuire il Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="c8bd1-120">Deploy Azure Container Registry</span></span>

<span data-ttu-id="c8bd1-121">Prima di distribuire un Registro contenitori di Azure, è necessario che esista un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="c8bd1-121">When deploying an Azure Container Registry, you first need a resource group.</span></span> <span data-ttu-id="c8bd1-122">Un gruppo di risorse di Azure è una raccolta logica in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="c8bd1-122">An Azure resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="c8bd1-123">Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="c8bd1-123">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="c8bd1-124">In questo esempio, un gruppo di risorse denominato *myResourceGroup* viene creato in hello *eastus* area.</span><span class="sxs-lookup"><span data-stu-id="c8bd1-124">In this example, a resource group named *myResourceGroup* is created in hello *eastus* region.</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="c8bd1-125">Creare un registro di sistema del contenitore di Azure con hello [az acr creare](/cli/azure/acr#create) comando.</span><span class="sxs-lookup"><span data-stu-id="c8bd1-125">Create an Azure Container registry with hello [az acr create](/cli/azure/acr#create) command.</span></span> <span data-ttu-id="c8bd1-126">nome di un contenitore del Registro di sistema di Hello **deve essere univoco**.</span><span class="sxs-lookup"><span data-stu-id="c8bd1-126">hello name of a Container Registry **must be unique**.</span></span> <span data-ttu-id="c8bd1-127">Nel seguente esempio di hello, utilizziamo nome hello *mycontainerregistry082*.</span><span class="sxs-lookup"><span data-stu-id="c8bd1-127">In hello following example, we use hello name *mycontainerregistry082*.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name mycontainerregistry082 --sku Basic --admin-enabled true
```

<span data-ttu-id="c8bd1-128">Tutta hello di questa esercitazione, utilizziamo `<acrname>` come segnaposto per nome del Registro di sistema del contenitore hello scelto.</span><span class="sxs-lookup"><span data-stu-id="c8bd1-128">Throughout hello rest of this tutorial, we use `<acrname>` as a placeholder for hello container registry name that you chose.</span></span>

## <a name="container-registry-login"></a><span data-ttu-id="c8bd1-129">Accesso al registro contenitori</span><span class="sxs-lookup"><span data-stu-id="c8bd1-129">Container registry login</span></span>

<span data-ttu-id="c8bd1-130">È necessario accedere in istanza ACR tooyour prima push tooit immagini.</span><span class="sxs-lookup"><span data-stu-id="c8bd1-130">You must log in tooyour ACR instance before pushing images tooit.</span></span> <span data-ttu-id="c8bd1-131">Hello utilizzare [accesso acr az](https://docs.microsoft.com/en-us/cli/azure/acr#login) operazione hello toocomplete di comando.</span><span class="sxs-lookup"><span data-stu-id="c8bd1-131">Use hello [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) command toocomplete hello operation.</span></span> <span data-ttu-id="c8bd1-132">È necessario il nome univoco di tooprovide hello assegnato del Registro di sistema di toohello contenitore al momento della creazione.</span><span class="sxs-lookup"><span data-stu-id="c8bd1-132">You need tooprovide hello unique name given toohello container registry when it was created.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="c8bd1-133">comando Hello restituisce un messaggio 'Accesso riuscito' una volta completato.</span><span class="sxs-lookup"><span data-stu-id="c8bd1-133">hello command returns a 'Login Succeeded’ message once completed.</span></span>

## <a name="tag-container-image"></a><span data-ttu-id="c8bd1-134">Assegnare tag all'immagine del contenitore</span><span class="sxs-lookup"><span data-stu-id="c8bd1-134">Tag container image</span></span>

<span data-ttu-id="c8bd1-135">toodeploy un'immagine contenitore da un registro di sistema privato, l'immagine di hello deve essere contrassegnato con hello toobe `loginServer` nome del Registro di sistema hello.</span><span class="sxs-lookup"><span data-stu-id="c8bd1-135">toodeploy a container image from a private registry, hello image needs toobe tagged with hello `loginServer` name of hello registry.</span></span>

<span data-ttu-id="c8bd1-136">un elenco di immagini corrente, utilizzare hello toosee `docker images` comando.</span><span class="sxs-lookup"><span data-stu-id="c8bd1-136">toosee a list of current images, use hello `docker images` command.</span></span>

```bash
docker images
```

<span data-ttu-id="c8bd1-137">Output:</span><span class="sxs-lookup"><span data-stu-id="c8bd1-137">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

<span data-ttu-id="c8bd1-138">tooget hello loginServer nome eseguire hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="c8bd1-138">tooget hello loginServer name, run hello following command.</span></span>

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

<span data-ttu-id="c8bd1-139">Hello tag *aci-esercitazione-app* immagine con loginServer hello del Registro di sistema di hello contenitore.</span><span class="sxs-lookup"><span data-stu-id="c8bd1-139">Tag hello *aci-tutorial-app* image with hello loginServer of hello container registry.</span></span> <span data-ttu-id="c8bd1-140">Inoltre, aggiungere `:v1` toohello fine del nome dell'immagine hello.</span><span class="sxs-lookup"><span data-stu-id="c8bd1-140">Also, add `:v1` toohello end of hello image name.</span></span> <span data-ttu-id="c8bd1-141">Questo tag indica numero di versione di hello immagine.</span><span class="sxs-lookup"><span data-stu-id="c8bd1-141">This tag indicates hello image version number.</span></span>

```bash
docker tag aci-tutorial-app <acrLoginServer>/aci-tutorial-app:v1
```

<span data-ttu-id="c8bd1-142">Una volta contrassegnate, eseguire `docker images` operazione hello tooverify.</span><span class="sxs-lookup"><span data-stu-id="c8bd1-142">Once tagged, run `docker images` tooverify hello operation.</span></span>

```bash
docker images
```

<span data-ttu-id="c8bd1-143">Output:</span><span class="sxs-lookup"><span data-stu-id="c8bd1-143">Output:</span></span>

```bash
REPOSITORY                                                TAG                 IMAGE ID            CREATED             SIZE
aci-tutorial-app                                          latest              5c745774dfa9        39 seconds ago      68.1 MB
mycontainerregistry082.azurecr.io/aci-tutorial-app        v1                  a9dace4e1a17        7 minutes ago       68.1 MB
```

## <a name="push-image-tooazure-container-registry"></a><span data-ttu-id="c8bd1-144">Push tooAzure immagine contenitore del Registro di sistema</span><span class="sxs-lookup"><span data-stu-id="c8bd1-144">Push image tooAzure Container Registry</span></span>

<span data-ttu-id="c8bd1-145">Push hello *aci-esercitazione-app* registro toohello di immagini.</span><span class="sxs-lookup"><span data-stu-id="c8bd1-145">Push hello *aci-tutorial-app* image toohello registry.</span></span>

<span data-ttu-id="c8bd1-146">Utilizza hello di esempio seguente, sostituire hello contenitore del Registro di sistema loginServer name con loginServer hello dall'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="c8bd1-146">Using hello following example, replace hello container registry loginServer name with hello loginServer from your environment.</span></span>

```bash
docker push <acrLoginServer>/aci-tutorial-app:v1
```

## <a name="list-images-in-azure-container-registry"></a><span data-ttu-id="c8bd1-147">Elencare le immagini in Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="c8bd1-147">List images in Azure Container Registry</span></span>

<span data-ttu-id="c8bd1-148">un elenco di immagini che sono stati inseriti tooyour Azure contenitore del Registro di sistema, hello utente tooreturn [elenco repository di az acr](/cli/azure/acr/repository#list) comando.</span><span class="sxs-lookup"><span data-stu-id="c8bd1-148">tooreturn a list of images that have been pushed tooyour Azure Container registry, user hello [az acr repository list](/cli/azure/acr/repository#list) command.</span></span> <span data-ttu-id="c8bd1-149">Aggiornare il comando hello con il nome del Registro di sistema di hello contenitore.</span><span class="sxs-lookup"><span data-stu-id="c8bd1-149">Update hello command with hello container registry name.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="c8bd1-150">Output:</span><span class="sxs-lookup"><span data-stu-id="c8bd1-150">Output:</span></span>

```azurecli
Result
----------------
aci-tutorial-app
```

<span data-ttu-id="c8bd1-151">Quindi tag hello toosee per un'immagine specifica, utilizzare hello [az acr repository Mostra-tag](/cli/azure/acr/repository#show-tags) comando.</span><span class="sxs-lookup"><span data-stu-id="c8bd1-151">And then toosee hello tags for a specific image, use hello [az acr repository show-tags](/cli/azure/acr/repository#show-tags) command.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository aci-tutorial-app --output table
```

<span data-ttu-id="c8bd1-152">Output:</span><span class="sxs-lookup"><span data-stu-id="c8bd1-152">Output:</span></span>

```azurecli
Result
--------
v1
```

## <a name="next-steps"></a><span data-ttu-id="c8bd1-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c8bd1-153">Next steps</span></span>

<span data-ttu-id="c8bd1-154">In questa esercitazione, un registro di sistema di contenitore di Azure è stata preparata per l'uso con istanze di contenitori di Azure e immagine contenitore hello è stato inserito.</span><span class="sxs-lookup"><span data-stu-id="c8bd1-154">In this tutorial, an Azure Container Registry was prepared for use with Azure Container Instances, and hello container image was pushed.</span></span> <span data-ttu-id="c8bd1-155">sono stata completata Hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="c8bd1-155">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c8bd1-156">Distribuzione di un'istanza del Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="c8bd1-156">Deploying an Azure Container Registry instance</span></span>
> * <span data-ttu-id="c8bd1-157">Assegnazione di un tag all'immagine del contenitore per Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="c8bd1-157">Tagging container image for Azure Container Registry</span></span>
> * <span data-ttu-id="c8bd1-158">Caricamento tooAzure immagine contenitore del Registro di sistema</span><span class="sxs-lookup"><span data-stu-id="c8bd1-158">Uploading image tooAzure Container Registry</span></span>

<span data-ttu-id="c8bd1-159">Spostare toohello Avanti toolearn esercitazione sulla distribuzione di hello contenitore tooAzure utilizzando istanze di contenitori di Azure.</span><span class="sxs-lookup"><span data-stu-id="c8bd1-159">Advance toohello next tutorial toolearn about deploying hello container tooAzure using Azure Container Instances.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c8bd1-160">Distribuire i contenitori tooAzure istanze di contenitori</span><span class="sxs-lookup"><span data-stu-id="c8bd1-160">Deploy containers tooAzure Container Instances</span></span>](./container-instances-tutorial-deploy-app.md)
