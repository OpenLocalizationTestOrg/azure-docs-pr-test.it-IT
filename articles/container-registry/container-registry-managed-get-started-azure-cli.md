---
title: Creare un registro per contenitori Docker privati in Azure - Interfaccia della riga di comando di Azure | Microsoft Docs
description: Introduzione alla creazione e gestione dei registri per contenitori Docker privati con l'interfaccia della riga di comando di Azure 2.0
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
ms.openlocfilehash: c7cdb1b13bf32388d18c2a25af28337a81861c1e
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="create-a-managed-container-registry-using-the-azure-cli"></a><span data-ttu-id="38a7c-103">Creare un registro contenitori gestito con l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="38a7c-103">Create a managed container registry using the Azure CLI</span></span>

<span data-ttu-id="38a7c-104">Registro contenitori di Azure è un servizio gestito di registri contenitori Docker usato per l'archiviazione di immagini di un contenitore Docker privato.</span><span class="sxs-lookup"><span data-stu-id="38a7c-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span></span> <span data-ttu-id="38a7c-105">Questa guida descrive la creazione di un'istanza gestita di Registro contenitori di Azure con l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="38a7c-105">This guide details creating a managed Azure Container Registry instance using the Azure CLI.</span></span>

<span data-ttu-id="38a7c-106">I registri contenitori di Azure gestiti sono in anteprima e non disponibili in tutte le aree di Azure.</span><span class="sxs-lookup"><span data-stu-id="38a7c-106">Managed Azure container registries are in preview and not available in all regions.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="38a7c-107">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questa guida introduttiva è necessario eseguire la versione 2.0.4 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="38a7c-107">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="38a7c-108">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="38a7c-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="38a7c-109">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="38a7c-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="38a7c-110">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="38a7c-110">Create a resource group</span></span>

<span data-ttu-id="38a7c-111">Creare un gruppo di risorse con il comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="38a7c-111">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="38a7c-112">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="38a7c-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="38a7c-113">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroup* nella località *westcentralus*.</span><span class="sxs-lookup"><span data-stu-id="38a7c-113">The following example creates a resource group named *myResourceGroup* in the *westcentralus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location westcentralus
```

## <a name="create-a-container-registry"></a><span data-ttu-id="38a7c-114">Creare un registro di contenitori</span><span class="sxs-lookup"><span data-stu-id="38a7c-114">Create a container registry</span></span>

<span data-ttu-id="38a7c-115">Creare un'istanza di Registro contenitori di Azure usando il comando [azure acr create](/cli/azure/acr#create).</span><span class="sxs-lookup"><span data-stu-id="38a7c-115">Create an ACR instance using the [az acr create](/cli/azure/acr#create) command.</span></span>

> [!NOTE]
> <span data-ttu-id="38a7c-116">Quando si crea un registro, specificare un nome di dominio univoco globale di primo livello, contenente solo lettere e numeri.</span><span class="sxs-lookup"><span data-stu-id="38a7c-116">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span>

 <span data-ttu-id="38a7c-117">Il nome del registro nell'esempio è *myContainerRegistry1*, ma è necessario sostituirlo con un nome univoco personalizzato.</span><span class="sxs-lookup"><span data-stu-id="38a7c-117">The registry name in the example is *myContainerRegistry1*, substitute a unique name of your own.</span></span>

```azurecli
az acr create --name myContainerRegistry1 --resource-group myResourceGroup --sku Managed_Standard
```

<span data-ttu-id="38a7c-118">Quando viene creato il registro, l'output è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="38a7c-118">When the registry is created, the output is similar to the following:</span></span>

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

## <a name="log-in-to-acr-instance"></a><span data-ttu-id="38a7c-119">Accedere all'istanza di Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="38a7c-119">Log in to ACR instance</span></span>

<span data-ttu-id="38a7c-120">Prima di eseguire il push e il pull delle immagini del contenitore, è necessario accedere all'istanza di Registro contenitori di Azure.</span><span class="sxs-lookup"><span data-stu-id="38a7c-120">Before pushing and pulling container images, you must log in to the ACR instance.</span></span> <span data-ttu-id="38a7c-121">A tale scopo usare il comando [az acr login](/cli/azure/acr#login).</span><span class="sxs-lookup"><span data-stu-id="38a7c-121">To do so, use the [az acr login](/cli/azure/acr#login) command.</span></span>

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

<span data-ttu-id="38a7c-122">Al termine, il comando restituisce un messaggio di accesso riuscito.</span><span class="sxs-lookup"><span data-stu-id="38a7c-122">The command returns a 'Login Succeeded' message once completed.</span></span>

## <a name="use-azure-container-registry"></a><span data-ttu-id="38a7c-123">Usare Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="38a7c-123">Use Azure Container Registry</span></span>

### <a name="list-container-images"></a><span data-ttu-id="38a7c-124">Elencare le immagini del contenitore</span><span class="sxs-lookup"><span data-stu-id="38a7c-124">List container images</span></span>

<span data-ttu-id="38a7c-125">Usare i comandi dell'interfaccia della riga di comando `az acr` per eseguire query su immagini e tag in un repository.</span><span class="sxs-lookup"><span data-stu-id="38a7c-125">Use the `az acr` CLI commands to query the images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="38a7c-126">Attualmente, il servizio Container Registry non supporta il comando `docker search` per eseguire query relative a immagini e tag.</span><span class="sxs-lookup"><span data-stu-id="38a7c-126">Currently, Container Registry does not support the `docker search` command to query for images and tags.</span></span>

### <a name="list-repositories"></a><span data-ttu-id="38a7c-127">Elencare repository</span><span class="sxs-lookup"><span data-stu-id="38a7c-127">List repositories</span></span>

<span data-ttu-id="38a7c-128">L'esempio seguente elenca i repository in un registro, in formato JSON (JavaScript Object Notation):</span><span class="sxs-lookup"><span data-stu-id="38a7c-128">The following example lists the repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="38a7c-129">Elencare tag</span><span class="sxs-lookup"><span data-stu-id="38a7c-129">List tags</span></span>

<span data-ttu-id="38a7c-130">L'esempio seguente elenca i tag sul repository **samples/nginx**, in formato JSON:</span><span class="sxs-lookup"><span data-stu-id="38a7c-130">The following example lists the tags on the **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="38a7c-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="38a7c-131">Next steps</span></span>

<span data-ttu-id="38a7c-132">In questa guida introduttiva è stata creata un'istanza gestita di Registro contenitori di Azure con l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="38a7c-132">In this quick start, you've created a managed Azure Container Registry instance using the Azure CLI.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="38a7c-133">Effettuare il push della prima immagine tramite l'interfaccia della riga di comando di Docker</span><span class="sxs-lookup"><span data-stu-id="38a7c-133">Push your first image using the Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
