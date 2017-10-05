---
title: Creare un registro per contenitori Docker privati - Portale di Azure | Microsoft Docs
description: Introduzione alla creazione e gestione dei registri per contenitori Docker privati con il portale di Azure
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: 560aee42b0c5a61c37c594d7937f833ab7183d49
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="create-a-managed-container-registry-using-the-azure-portal"></a><span data-ttu-id="36a4c-103">Creare un registro contenitori gestito con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="36a4c-103">Create a managed container registry using the Azure portal</span></span>

<span data-ttu-id="36a4c-104">Registro contenitori di Azure è un servizio gestito di registri contenitori Docker usato per l'archiviazione di immagini di un contenitore Docker privato.</span><span class="sxs-lookup"><span data-stu-id="36a4c-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span></span> <span data-ttu-id="36a4c-105">Questa guida descrive la creazione di un'istanza gestita di Registro contenitori di Azure con il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="36a4c-105">This guide details creating a managed Azure Container Registry instance using the Azure portal.</span></span>

<span data-ttu-id="36a4c-106">I registri contenitori di Azure gestiti sono in anteprima e non disponibili in tutte le aree di Azure.</span><span class="sxs-lookup"><span data-stu-id="36a4c-106">Managed Azure container registries are in preview and not available in all regions.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="36a4c-107">Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="36a4c-107">Log in to Azure</span></span>

<span data-ttu-id="36a4c-108">Accedere al portale di Azure all'indirizzo http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="36a4c-108">Log in to the Azure portal at http://portal.azure.com.</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="36a4c-109">Creare un registro di contenitori</span><span class="sxs-lookup"><span data-stu-id="36a4c-109">Create a container registry</span></span>

1. <span data-ttu-id="36a4c-110">Fare clic sul pulsante **Nuovo** nell'angolo superiore sinistro del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="36a4c-110">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="36a4c-111">Cercare **Registro contenitori di Azure** nel Marketplace e selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="36a4c-111">Search the marketplace for **Azure container registry** and select it.</span></span>

3. <span data-ttu-id="36a4c-112">Fare clic su **Crea** per visualizzare il pannello di creazione dell'istanza di Registro contenitori di Azure.</span><span class="sxs-lookup"><span data-stu-id="36a4c-112">Click **Create** which will open the ACR creation blade.</span></span>

    ![Impostazioni di Registro contenitori](./media/container-registry-get-started-portal/managed-container-registry-settings.png)

4. <span data-ttu-id="36a4c-114">Nel pannello **Registro contenitori di Azure** immettere le informazioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="36a4c-114">In the **Azure Container Registry** blade, enter the following information.</span></span> <span data-ttu-id="36a4c-115">Al termine dell'operazione fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="36a4c-115">Click **Create** when you are done.</span></span>

    <span data-ttu-id="36a4c-116">a.</span><span class="sxs-lookup"><span data-stu-id="36a4c-116">a.</span></span> <span data-ttu-id="36a4c-117">**Registry name** (Nome registro): nome di dominio di primo livello univoco globale per il registro.</span><span class="sxs-lookup"><span data-stu-id="36a4c-117">**Registry name**: A globally unique top-level domain name for your specific registry.</span></span> <span data-ttu-id="36a4c-118">In questo esempio, il nome del registro è *myAzureContainerRegistry1*, ma è necessario sostituirlo con un nome univoco personalizzato.</span><span class="sxs-lookup"><span data-stu-id="36a4c-118">In this example, the registry name is *myAzureContainerRegistry1*, but substitute a unique name of your own.</span></span> <span data-ttu-id="36a4c-119">Il nome può contenere solo lettere e numeri.</span><span class="sxs-lookup"><span data-stu-id="36a4c-119">The name can contain only letters and numbers.</span></span>

    <span data-ttu-id="36a4c-120">b.</span><span class="sxs-lookup"><span data-stu-id="36a4c-120">b.</span></span> <span data-ttu-id="36a4c-121">**Resource group** (Gruppo di risorse): selezionare un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md#resource-groups) esistente o specificare il nome di un nuovo gruppo.</span><span class="sxs-lookup"><span data-stu-id="36a4c-121">**Resource group**: Select an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) or type the name for a new one.</span></span>

    <span data-ttu-id="36a4c-122">c.</span><span class="sxs-lookup"><span data-stu-id="36a4c-122">c.</span></span> <span data-ttu-id="36a4c-123">**Location** (Posizione): selezionare la posizione di un data center di Azure in cui il servizio è [disponibile](https://azure.microsoft.com/regions/services/), ad esempio **Stati Uniti centro-meridionali**.</span><span class="sxs-lookup"><span data-stu-id="36a4c-123">**Location**: Select an Azure datacenter location where the service is [available](https://azure.microsoft.com/regions/services/), such as **South Central US**.</span></span>

    <span data-ttu-id="36a4c-124">d.</span><span class="sxs-lookup"><span data-stu-id="36a4c-124">d.</span></span> <span data-ttu-id="36a4c-125">**Admin user** (Utente amministratore): consentire eventualmente a un utente amministratore di accedere al registro.</span><span class="sxs-lookup"><span data-stu-id="36a4c-125">**Admin user**: If you want, enable an admin user to access the registry.</span></span> <span data-ttu-id="36a4c-126">È possibile modificare questa impostazione dopo aver creato il registro.</span><span class="sxs-lookup"><span data-stu-id="36a4c-126">You can change this setting after creating the registry.</span></span>

    <span data-ttu-id="36a4c-127">e.</span><span class="sxs-lookup"><span data-stu-id="36a4c-127">e.</span></span> <span data-ttu-id="36a4c-128">**Usa registro gestito**: selezionare Sì in modo che Registro contenitori di Azure gestisca automaticamente l'archiviazione del registro e usi webhook e l'autenticazione AAD.</span><span class="sxs-lookup"><span data-stu-id="36a4c-128">**Use managed registry**: Select yes to have ACR automatically manage the registry storage, use webhooks, and use AAD authentication.</span></span>

    <span data-ttu-id="36a4c-129">f.</span><span class="sxs-lookup"><span data-stu-id="36a4c-129">f.</span></span> <span data-ttu-id="36a4c-130">**Piano tariffario**: selezionare un piano tariffario. Vedere le informazioni sui prezzi di Registro contenitori di Azure per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="36a4c-130">**Pricing Tier**: Select a pricing tier, see here ACR pricing for more information.</span></span>

## <a name="log-in-to-acr-instance"></a><span data-ttu-id="36a4c-131">Accedere all'istanza di Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="36a4c-131">Log in to ACR instance</span></span>

<span data-ttu-id="36a4c-132">Prima di eseguire il push e il pull delle immagini del contenitore, è necessario accedere all'istanza di Registro contenitori di Azure.</span><span class="sxs-lookup"><span data-stu-id="36a4c-132">Before pushing and pulling container images, you must log in to the ACR instance.</span></span> 

<span data-ttu-id="36a4c-133">A tale scopo usare l'interfaccia della riga di comando di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="36a4c-133">To do so, use the Azure CLI 2.0.</span></span> <span data-ttu-id="36a4c-134">Se necessario, accedere prima ad Azure con il comando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="36a4c-134">First, if needed, log into Azure using the [az login](/cli/azure/#login) command.</span></span> 

```azurecli
az login
```

<span data-ttu-id="36a4c-135">Usare quindi il comando [az acr login](/cli/azure/acr#login) per accedere a Registro contenitori di Azure.</span><span class="sxs-lookup"><span data-stu-id="36a4c-135">Next, use the [az acr login](/cli/azure/acr#login) command to log in to the Azure Container Registry.</span></span>

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

## <a name="use-azure-container-registry"></a><span data-ttu-id="36a4c-136">Usare Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="36a4c-136">Use Azure Container Registry</span></span>

### <a name="list-container-images"></a><span data-ttu-id="36a4c-137">Elencare le immagini del contenitore</span><span class="sxs-lookup"><span data-stu-id="36a4c-137">List container images</span></span>

<span data-ttu-id="36a4c-138">Usare i comandi dell'interfaccia della riga di comando `az acr` per eseguire query su immagini e tag in un repository.</span><span class="sxs-lookup"><span data-stu-id="36a4c-138">Use the `az acr` CLI commands to query the images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="36a4c-139">Attualmente, il servizio Container Registry non supporta il comando `docker search` per eseguire query relative a immagini e tag.</span><span class="sxs-lookup"><span data-stu-id="36a4c-139">Currently, Container Registry does not support the `docker search` command to query for images and tags.</span></span>

### <a name="list-repositories"></a><span data-ttu-id="36a4c-140">Elencare repository</span><span class="sxs-lookup"><span data-stu-id="36a4c-140">List repositories</span></span>

<span data-ttu-id="36a4c-141">L'esempio seguente elenca i repository in un registro, in formato JSON (JavaScript Object Notation):</span><span class="sxs-lookup"><span data-stu-id="36a4c-141">The following example lists the repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="36a4c-142">Elencare tag</span><span class="sxs-lookup"><span data-stu-id="36a4c-142">List tags</span></span>

<span data-ttu-id="36a4c-143">L'esempio seguente elenca i tag sul repository **samples/nginx**, in formato JSON:</span><span class="sxs-lookup"><span data-stu-id="36a4c-143">The following example lists the tags on the **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="36a4c-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="36a4c-144">Next steps</span></span>

<span data-ttu-id="36a4c-145">In questa guida introduttiva è stata creata un'istanza gestita di Registro contenitori di Azure con il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="36a4c-145">In this quick start, you've created a managed Azure Container Registry instance using the Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="36a4c-146">Effettuare il push della prima immagine tramite l'interfaccia della riga di comando di Docker</span><span class="sxs-lookup"><span data-stu-id="36a4c-146">Push your first image using the Docker CLI</span></span>](container-registry-get-started-docker-cli.md)