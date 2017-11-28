---
title: aaaCreate registro contenitore privato Docker - CLI di Azure | Documenti Microsoft
description: Iniziare a creare e gestire i registri contenitore Docker privati con hello Azure CLI 2.0
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: 2cadf42db0681a09c95486510f1e65c6f87c5280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-cli"></a><span data-ttu-id="d382c-103">Creare un registro di sistema di contenitore gestito mediante hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="d382c-103">Create a managed container registry using hello Azure CLI</span></span>

<span data-ttu-id="d382c-104">Registro contenitori di Azure è un servizio gestito di registri contenitori Docker usato per l'archiviazione di immagini di un contenitore Docker privato.</span><span class="sxs-lookup"><span data-stu-id="d382c-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span></span> <span data-ttu-id="d382c-105">Questa guida descrive la creazione di un'istanza gestita di Azure del Registro di sistema contenitore utilizzando hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="d382c-105">This guide details creating a managed Azure Container Registry instance using hello Azure CLI.</span></span>

<span data-ttu-id="d382c-106">I registri contenitori di Azure gestiti sono in anteprima e non disponibili in tutte le aree di Azure.</span><span class="sxs-lookup"><span data-stu-id="d382c-106">Managed Azure container registries are in preview and not available in all regions.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d382c-107">Se si sceglie tooinstall e utilizza hello CLI in locale, questa Guida rapida richiede che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="d382c-107">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="d382c-108">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="d382c-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="d382c-109">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d382c-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="d382c-110">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="d382c-110">Create a resource group</span></span>

<span data-ttu-id="d382c-111">Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="d382c-111">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="d382c-112">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="d382c-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="d382c-113">esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *westcentralus* percorso.</span><span class="sxs-lookup"><span data-stu-id="d382c-113">hello following example creates a resource group named *myResourceGroup* in hello *westcentralus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location westcentralus
```

## <a name="create-a-container-registry"></a><span data-ttu-id="d382c-114">Creare un registro di contenitori</span><span class="sxs-lookup"><span data-stu-id="d382c-114">Create a container registry</span></span>

<span data-ttu-id="d382c-115">Creare un'istanza di record con hello [az acr creare](/cli/azure/acr#create) comando.</span><span class="sxs-lookup"><span data-stu-id="d382c-115">Create an ACR instance using hello [az acr create](/cli/azure/acr#create) command.</span></span>

> [!NOTE]
> <span data-ttu-id="d382c-116">Quando si crea un registro, specificare un nome di dominio univoco globale di primo livello, contenente solo lettere e numeri.</span><span class="sxs-lookup"><span data-stu-id="d382c-116">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span>

 <span data-ttu-id="d382c-117">nome del Registro di sistema Hello nell'esempio hello è *myContainerRegistry1*, sostituire con un nome univoco del proprio.</span><span class="sxs-lookup"><span data-stu-id="d382c-117">hello registry name in hello example is *myContainerRegistry1*, substitute a unique name of your own.</span></span>

```azurecli
az acr create --name myContainerRegistry1 --resource-group myResourceGroup --sku Managed_Standard
```

<span data-ttu-id="d382c-118">Quando viene creato il registro hello, l'output di hello è simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="d382c-118">When hello registry is created, hello output is similar toohello following:</span></span>

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-29T04:50:28.607134+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry1",
  "location": "westcentralus",
  "loginServer": "mycontainerregistry1.azurecr.io",
  "name": "myContainerRegistry1",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "name": "Managed_Standard",
    "tier": "Managed"
  },
  "storageAccount": null,
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

## <a name="log-in-tooacr-instance"></a><span data-ttu-id="d382c-119">Accedi tooACR istanza</span><span class="sxs-lookup"><span data-stu-id="d382c-119">Log in tooACR instance</span></span>

<span data-ttu-id="d382c-120">Prima di push e pull immagini contenitore, è necessario accedere nell'istanza di record toohello.</span><span class="sxs-lookup"><span data-stu-id="d382c-120">Before pushing and pulling container images, you must log in toohello ACR instance.</span></span> <span data-ttu-id="d382c-121">toodo in tal caso, utilizzare hello [accesso acr az](/cli/azure/acr#login) comando.</span><span class="sxs-lookup"><span data-stu-id="d382c-121">toodo so, use hello [az acr login](/cli/azure/acr#login) command.</span></span>

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

<span data-ttu-id="d382c-122">comando Hello restituisce un messaggio 'Accesso riuscito' una volta completato.</span><span class="sxs-lookup"><span data-stu-id="d382c-122">hello command returns a 'Login Succeeded' message once completed.</span></span>

## <a name="use-azure-container-registry"></a><span data-ttu-id="d382c-123">Usare Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="d382c-123">Use Azure Container Registry</span></span>

### <a name="list-container-images"></a><span data-ttu-id="d382c-124">Elencare le immagini del contenitore</span><span class="sxs-lookup"><span data-stu-id="d382c-124">List container images</span></span>

<span data-ttu-id="d382c-125">Hello utilizzare `az acr` contiene i comandi CLI immagini hello tooquery e tag in un repository.</span><span class="sxs-lookup"><span data-stu-id="d382c-125">Use hello `az acr` CLI commands tooquery hello images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="d382c-126">Registro di sistema di contenitore non supporta attualmente hello `docker search` comando tooquery per immagini e i tag.</span><span class="sxs-lookup"><span data-stu-id="d382c-126">Currently, Container Registry does not support hello `docker search` command tooquery for images and tags.</span></span>

### <a name="list-repositories"></a><span data-ttu-id="d382c-127">Elencare repository</span><span class="sxs-lookup"><span data-stu-id="d382c-127">List repositories</span></span>

<span data-ttu-id="d382c-128">Hello esempio seguente vengono elencati i repository hello nel Registro di sistema, in formato JSON (JavaScript Object Notation):</span><span class="sxs-lookup"><span data-stu-id="d382c-128">hello following example lists hello repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="d382c-129">Elencare tag</span><span class="sxs-lookup"><span data-stu-id="d382c-129">List tags</span></span>

<span data-ttu-id="d382c-130">Hello esempio seguente vengono elencati i tag hello in hello **esempi/nginx** repository, in formato JSON:</span><span class="sxs-lookup"><span data-stu-id="d382c-130">hello following example lists hello tags on hello **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="d382c-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d382c-131">Next steps</span></span>

<span data-ttu-id="d382c-132">In questa Guida introduttiva è stata creata un'istanza gestita di Azure del Registro di sistema contenitore utilizzando hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="d382c-132">In this quick start, you've created a managed Azure Container Registry instance using hello Azure CLI.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d382c-133">La prima immagine usando Docker CLI hello push</span><span class="sxs-lookup"><span data-stu-id="d382c-133">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
