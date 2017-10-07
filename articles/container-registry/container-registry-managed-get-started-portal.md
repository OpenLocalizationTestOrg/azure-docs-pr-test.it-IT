---
title: aaaCreate privata Docker Registro di sistema - portale di Azure | Documenti Microsoft
description: Iniziare a creare e gestire i registri contenitore Docker privati con hello portale di Azure
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
ms.openlocfilehash: cf3ce0dcf3036d0e9cd1eaf01721deccb00248d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-portal"></a><span data-ttu-id="a82a7-103">Creare un registro di sistema di contenitore gestito mediante hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a82a7-103">Create a managed container registry using hello Azure portal</span></span>

<span data-ttu-id="a82a7-104">Registro contenitori di Azure è un servizio gestito di registri contenitori Docker usato per l'archiviazione di immagini di un contenitore Docker privato.</span><span class="sxs-lookup"><span data-stu-id="a82a7-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span></span> <span data-ttu-id="a82a7-105">Questa guida descrive la creazione di un'istanza gestita di Azure del Registro di sistema contenitore utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a82a7-105">This guide details creating a managed Azure Container Registry instance using hello Azure portal.</span></span>

<span data-ttu-id="a82a7-106">I registri contenitori di Azure gestiti sono in anteprima e non disponibili in tutte le aree di Azure.</span><span class="sxs-lookup"><span data-stu-id="a82a7-106">Managed Azure container registries are in preview and not available in all regions.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="a82a7-107">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="a82a7-107">Log in tooAzure</span></span>

<span data-ttu-id="a82a7-108">Accedi toohello portale di Azure all'indirizzo http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="a82a7-108">Log in toohello Azure portal at http://portal.azure.com.</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="a82a7-109">Creare un registro di contenitori</span><span class="sxs-lookup"><span data-stu-id="a82a7-109">Create a container registry</span></span>

1. <span data-ttu-id="a82a7-110">Fare clic su hello **New** pulsante disponibile nella hello angolo superiore sinistro del portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a82a7-110">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="a82a7-111">Marketplace hello ricerca per **Registro di sistema di contenitore di Azure** e selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="a82a7-111">Search hello marketplace for **Azure container registry** and select it.</span></span>

3. <span data-ttu-id="a82a7-112">Fare clic su **crea** aprire Pannello di creazione ACR hello.</span><span class="sxs-lookup"><span data-stu-id="a82a7-112">Click **Create** which will open hello ACR creation blade.</span></span>

    ![Impostazioni di Registro contenitori](./media/container-registry-get-started-portal/managed-container-registry-settings.png)

4. <span data-ttu-id="a82a7-114">In hello **Registro di sistema di Azure contenitore** pannello, immettere le seguenti informazioni hello.</span><span class="sxs-lookup"><span data-stu-id="a82a7-114">In hello **Azure Container Registry** blade, enter hello following information.</span></span> <span data-ttu-id="a82a7-115">Al termine dell'operazione fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a82a7-115">Click **Create** when you are done.</span></span>

    <span data-ttu-id="a82a7-116">a.</span><span class="sxs-lookup"><span data-stu-id="a82a7-116">a.</span></span> <span data-ttu-id="a82a7-117">**Registry name** (Nome registro): nome di dominio di primo livello univoco globale per il registro.</span><span class="sxs-lookup"><span data-stu-id="a82a7-117">**Registry name**: A globally unique top-level domain name for your specific registry.</span></span> <span data-ttu-id="a82a7-118">In questo esempio, nome del Registro di sistema hello è *myAzureContainerRegistry1*, ma sostituire un nome univoco del proprio.</span><span class="sxs-lookup"><span data-stu-id="a82a7-118">In this example, hello registry name is *myAzureContainerRegistry1*, but substitute a unique name of your own.</span></span> <span data-ttu-id="a82a7-119">Hello nome può contenere solo lettere e numeri.</span><span class="sxs-lookup"><span data-stu-id="a82a7-119">hello name can contain only letters and numbers.</span></span>

    <span data-ttu-id="a82a7-120">b.</span><span class="sxs-lookup"><span data-stu-id="a82a7-120">b.</span></span> <span data-ttu-id="a82a7-121">**Gruppo di risorse**: selezionare un oggetto esistente [gruppo di risorse](../azure-resource-manager/resource-group-overview.md#resource-groups) o nome di tipo hello uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="a82a7-121">**Resource group**: Select an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span>

    <span data-ttu-id="a82a7-122">c.</span><span class="sxs-lookup"><span data-stu-id="a82a7-122">c.</span></span> <span data-ttu-id="a82a7-123">**Percorso**: selezionare un Data Center di Azure posizione servizio hello [disponibile](https://azure.microsoft.com/regions/services/), ad esempio **centro-meridionali**.</span><span class="sxs-lookup"><span data-stu-id="a82a7-123">**Location**: Select an Azure datacenter location where hello service is [available](https://azure.microsoft.com/regions/services/), such as **South Central US**.</span></span>

    <span data-ttu-id="a82a7-124">d.</span><span class="sxs-lookup"><span data-stu-id="a82a7-124">d.</span></span> <span data-ttu-id="a82a7-125">**L'utente amministratore**: se si desidera, attivare del Registro di sistema hello tooaccess utente amministratore.</span><span class="sxs-lookup"><span data-stu-id="a82a7-125">**Admin user**: If you want, enable an admin user tooaccess hello registry.</span></span> <span data-ttu-id="a82a7-126">È possibile modificare questa impostazione dopo la creazione del Registro di sistema di hello.</span><span class="sxs-lookup"><span data-stu-id="a82a7-126">You can change this setting after creating hello registry.</span></span>

    <span data-ttu-id="a82a7-127">e.</span><span class="sxs-lookup"><span data-stu-id="a82a7-127">e.</span></span> <span data-ttu-id="a82a7-128">**Registro di sistema gestito utilizzare**: selezionare Sì toohave ACR automaticamente gestire l'archiviazione del Registro di sistema hello, utilizzare webhook e utilizzare l'autenticazione AAD.</span><span class="sxs-lookup"><span data-stu-id="a82a7-128">**Use managed registry**: Select yes toohave ACR automatically manage hello registry storage, use webhooks, and use AAD authentication.</span></span>

    <span data-ttu-id="a82a7-129">f.</span><span class="sxs-lookup"><span data-stu-id="a82a7-129">f.</span></span> <span data-ttu-id="a82a7-130">**Piano tariffario**: selezionare un piano tariffario. Vedere le informazioni sui prezzi di Registro contenitori di Azure per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="a82a7-130">**Pricing Tier**: Select a pricing tier, see here ACR pricing for more information.</span></span>

## <a name="log-in-tooacr-instance"></a><span data-ttu-id="a82a7-131">Accedi tooACR istanza</span><span class="sxs-lookup"><span data-stu-id="a82a7-131">Log in tooACR instance</span></span>

<span data-ttu-id="a82a7-132">Prima di push e pull immagini contenitore, è necessario accedere nell'istanza di record toohello.</span><span class="sxs-lookup"><span data-stu-id="a82a7-132">Before pushing and pulling container images, you must log in toohello ACR instance.</span></span> 

<span data-ttu-id="a82a7-133">toodo, utilizzare hello CLI di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="a82a7-133">toodo so, use hello Azure CLI 2.0.</span></span> <span data-ttu-id="a82a7-134">Innanzitutto, se necessario, accedere utilizzando hello Azure [accesso az](/cli/azure/#login) comando.</span><span class="sxs-lookup"><span data-stu-id="a82a7-134">First, if needed, log into Azure using hello [az login](/cli/azure/#login) command.</span></span> 

```azurecli
az login
```

<span data-ttu-id="a82a7-135">Successivamente, utilizzare hello [accesso acr az](/cli/azure/acr#login) comando toolog in toohello del Registro di sistema contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="a82a7-135">Next, use hello [az acr login](/cli/azure/acr#login) command toolog in toohello Azure Container Registry.</span></span>

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

## <a name="use-azure-container-registry"></a><span data-ttu-id="a82a7-136">Usare Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="a82a7-136">Use Azure Container Registry</span></span>

### <a name="list-container-images"></a><span data-ttu-id="a82a7-137">Elencare le immagini del contenitore</span><span class="sxs-lookup"><span data-stu-id="a82a7-137">List container images</span></span>

<span data-ttu-id="a82a7-138">Hello utilizzare `az acr` contiene i comandi CLI immagini hello tooquery e tag in un repository.</span><span class="sxs-lookup"><span data-stu-id="a82a7-138">Use hello `az acr` CLI commands tooquery hello images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="a82a7-139">Registro di sistema di contenitore non supporta attualmente hello `docker search` comando tooquery per immagini e i tag.</span><span class="sxs-lookup"><span data-stu-id="a82a7-139">Currently, Container Registry does not support hello `docker search` command tooquery for images and tags.</span></span>

### <a name="list-repositories"></a><span data-ttu-id="a82a7-140">Elencare repository</span><span class="sxs-lookup"><span data-stu-id="a82a7-140">List repositories</span></span>

<span data-ttu-id="a82a7-141">Hello esempio seguente vengono elencati i repository hello nel Registro di sistema, in formato JSON (JavaScript Object Notation):</span><span class="sxs-lookup"><span data-stu-id="a82a7-141">hello following example lists hello repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="a82a7-142">Elencare tag</span><span class="sxs-lookup"><span data-stu-id="a82a7-142">List tags</span></span>

<span data-ttu-id="a82a7-143">Hello esempio seguente vengono elencati i tag hello in hello **esempi/nginx** repository, in formato JSON:</span><span class="sxs-lookup"><span data-stu-id="a82a7-143">hello following example lists hello tags on hello **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="a82a7-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a82a7-144">Next steps</span></span>

<span data-ttu-id="a82a7-145">In questa Guida introduttiva è stata creata un'istanza gestita di Azure del Registro di sistema contenitore utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a82a7-145">In this quick start, you've created a managed Azure Container Registry instance using hello Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a82a7-146">La prima immagine usando Docker CLI hello push</span><span class="sxs-lookup"><span data-stu-id="a82a7-146">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
