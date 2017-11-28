---
title: Eseguire la distribuzione in Istanze di contenitore di Azure da Registro contenitori di Azure | Azure Docs
description: Eseguire la distribuzione in Istanze di contenitore di Azure da Registro contenitori di Azure
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
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: aa1c4ea379c10dff246e2f924a345f9fa444aa64
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-to-azure-container-instances-from-the-azure-container-registry"></a><span data-ttu-id="7df20-103">Eseguire la distribuzione in Istanze di contenitore di Azure da Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="7df20-103">Deploy to Azure Container Instances from the Azure Container Registry</span></span>

<span data-ttu-id="7df20-104">Registro contenitori di Azure è un registro privato basato su Azure per le immagini del contenitore Docker.</span><span class="sxs-lookup"><span data-stu-id="7df20-104">The Azure Container Registry is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="7df20-105">Questo articolo illustra come distribuire in Istanze di contenitore di Azure immagini del contenitore archiviate in Registro contenitori di Azure.</span><span class="sxs-lookup"><span data-stu-id="7df20-105">This article covers how to deploy container images stored in the Azure Container Registry to Azure Container Instances.</span></span>

## <a name="using-the-azure-cli"></a><span data-ttu-id="7df20-106">Uso dell'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="7df20-106">Using the Azure CLI</span></span>

<span data-ttu-id="7df20-107">L'interfaccia della riga di comando di Azure include i comandi per la creazione e la gestione dei contenitori in Istanze di contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="7df20-107">The Azure CLI includes commands for creating and managing containers in Azure Container Instances.</span></span> <span data-ttu-id="7df20-108">Se si specifica un'immagine privata nel comando `create`, è anche possibile specificare la password del registro dell'immagine necessaria per l'autenticazione con il registro contenitori.</span><span class="sxs-lookup"><span data-stu-id="7df20-108">If you specify a private image in the `create` command, you can also specify the image registry password required to authenticate with the container registry.</span></span>

```azurecli-interactive
az container create --name myprivatecontainer --image mycontainerregistry.azurecr.io/mycontainerimage:v1 --registry-password myRegistryPassword --resource-group myresourcegroup
```

<span data-ttu-id="7df20-109">Il comando `create` consente anche di specificare `registry-login-server` e `registry-username`.</span><span class="sxs-lookup"><span data-stu-id="7df20-109">The `create` command also supports specifying the `registry-login-server` and `registry-username`.</span></span> <span data-ttu-id="7df20-110">Il server di accesso di Registro contenitori di Azure è tuttavia sempre *nomeregistro*.azurecr.io e il nome utente predefinito è *nomeregistro*, quindi questi valori vengono dedotti dal nome dell'immagine, se non specificati in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="7df20-110">However, the login server for the Azure Container Registry is always *registryname*.azurecr.io and the default username is *registryname*, so these values are inferred from the image name if not explicitly provided.</span></span>

## <a name="using-an-azure-resource-manager-template"></a><span data-ttu-id="7df20-111">Uso di un modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7df20-111">Using an Azure Resource Manager template</span></span>

<span data-ttu-id="7df20-112">È possibile specificare le proprietà di Registro contenitori di Azure in un modello di Azure Resource Manager includendo la proprietà `imageRegistryCredentials` nella definizione del gruppo di contenitori:</span><span class="sxs-lookup"><span data-stu-id="7df20-112">You can specify the properties of your Azure Container Registry in an Azure Resource Manager template by including the `imageRegistryCredentials` property in the container group definition:</span></span>

```json
"imageRegistryCredentials": [
  {
    "server": "imageRegistryLoginServer",
    "username": "imageRegistryUsername",
    "password": "imageRegistryPassword"
  }
]
```

<span data-ttu-id="7df20-113">Per evitare di archiviare la password del registro contenitori direttamente nel modello, è consigliabile archiviarla come segreto in [Azure Key Vault](../key-vault/key-vault-manage-with-cli2.md) e farvi riferimento nel modello usando l'[integrazione nativa tra Azure Resource Manager e Key Vault](../azure-resource-manager/resource-manager-keyvault-parameter.md).</span><span class="sxs-lookup"><span data-stu-id="7df20-113">To avoid storing your container registry password directly in the template, we recommend that you store it as a secret in [Azure Key Vault](../key-vault/key-vault-manage-with-cli2.md) and reference it in the template using the [native integration between the Azure Resource Manager and Key Vault](../azure-resource-manager/resource-manager-keyvault-parameter.md).</span></span>

## <a name="using-the-azure-portal"></a><span data-ttu-id="7df20-114">Uso del portale di Azure</span><span class="sxs-lookup"><span data-stu-id="7df20-114">Using the Azure portal</span></span>

<span data-ttu-id="7df20-115">Se si conservano le immagini del contenitore in Registro contenitori di Azure, è possibile creare facilmente un contenitore in Istanze di contenitore di Azure usando il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7df20-115">If you maintain container images in the Azure Container Registry, you can easily create a container in Azure Container Instances using the Azure portal.</span></span>

1. <span data-ttu-id="7df20-116">Nel portale di Azure passare al registro contenitori.</span><span class="sxs-lookup"><span data-stu-id="7df20-116">In the Azure portal, navigate to your container registry.</span></span>

2. <span data-ttu-id="7df20-117">Scegliere Repository.</span><span class="sxs-lookup"><span data-stu-id="7df20-117">Choose Repositories.</span></span>

    ![Menu di Registro contenitori di Azure nel portale di Azure][acr-menu]

3. <span data-ttu-id="7df20-119">Scegliere il repository da cui si vuole eseguire la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="7df20-119">Choose the repository that you want to deploy from.</span></span>

4. <span data-ttu-id="7df20-120">Fare clic con il pulsante destro del mouse sul tag dell'immagine del contenitore che si vuole distribuire.</span><span class="sxs-lookup"><span data-stu-id="7df20-120">Right-click the tag for the container image you want to deploy.</span></span>

    ![Menu di scelta rapida per avviare il contenitore con Istanze di contenitore di Azure][acr-runinstance-contextmenu]

5. <span data-ttu-id="7df20-122">Immettere un nome per il contenitore e un nome per il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="7df20-122">Enter a name for the container and a name for the resource group.</span></span> <span data-ttu-id="7df20-123">Se si vuole, è anche possibile cambiare i valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="7df20-123">You can also change the default values if you wish.</span></span>

    ![Menu di creazione per Istanze di contenitore di Azure][acr-create-deeplink]

6. <span data-ttu-id="7df20-125">Al termine della distribuzione, è possibile passare al gruppo di contenitori dal riquadro delle notifiche per trovare l'indirizzo IP e le altre proprietà.</span><span class="sxs-lookup"><span data-stu-id="7df20-125">Once the deployment completes, you can navigate to the container group from the notifications pane to find its IP address and other properties.</span></span>

    ![Visualizzazione dei dettagli del gruppo di contenitori in Istanze di contenitore di Azure][aci-detailsview]

## <a name="next-steps"></a><span data-ttu-id="7df20-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7df20-127">Next steps</span></span>

<span data-ttu-id="7df20-128">Informazioni su come creare contenitori, effettuarne il push in un registro contenitori privato e distribuirli in Istanze di contenitore di Azure [completando l'esercitazione](container-instances-tutorial-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="7df20-128">Learn how to build containers, push them to a private container registry, and deploy them to Azure Container Instances by [completing the tutorial](container-instances-tutorial-prepare-app.md).</span></span>

<!-- IMAGES -->
[acr-menu]: ./media/container-instances-using-azure-container-registry/acr-menu.png

[acr-runinstance-contextmenu]: ./media/container-instances-using-azure-container-registry/acr-runinstance-contextmenu.png

[acr-create-deeplink]: ./media/container-instances-using-azure-container-registry/acr-create-deeplink.png

[aci-detailsview]: ./media/container-instances-using-azure-container-registry/aci-detailsview.png
