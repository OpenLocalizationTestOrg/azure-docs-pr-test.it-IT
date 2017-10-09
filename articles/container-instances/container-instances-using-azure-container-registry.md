---
title: aaaDeploy tooAzure istanze di contenitori da hello del Registro di sistema di Azure contenitore | Documenti di Azure
description: Distribuire istanze di contenitori tooAzure da hello del Registro di sistema contenitore di Azure
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
ms.openlocfilehash: 2667f91db8ed92a9ccc9ba722a2b1f5c5ea93886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-container-instances-from-hello-azure-container-registry"></a><span data-ttu-id="33636-103">Distribuire istanze di contenitori tooAzure da hello del Registro di sistema contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="33636-103">Deploy tooAzure Container Instances from hello Azure Container Registry</span></span>

<span data-ttu-id="33636-104">Hello del Registro di sistema di Azure contenitore è un registro basato su Azure e privato, per le immagini contenitore Docker.</span><span class="sxs-lookup"><span data-stu-id="33636-104">hello Azure Container Registry is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="33636-105">Questo articolo descrive come le immagini contenitore toodeploy archiviati in hello del Registro di sistema di Azure contenitore tooAzure istanze di contenitori.</span><span class="sxs-lookup"><span data-stu-id="33636-105">This article covers how toodeploy container images stored in hello Azure Container Registry tooAzure Container Instances.</span></span>

## <a name="using-hello-azure-cli"></a><span data-ttu-id="33636-106">Utilizzo di hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="33636-106">Using hello Azure CLI</span></span>

<span data-ttu-id="33636-107">Hello CLI di Azure include i comandi per la creazione e gestione dei contenitori di istanze di contenitori di Azure.</span><span class="sxs-lookup"><span data-stu-id="33636-107">hello Azure CLI includes commands for creating and managing containers in Azure Container Instances.</span></span> <span data-ttu-id="33636-108">Se si specifica un'immagine privata in hello `create` comando, è inoltre possibile specificare hello immagine del Registro di sistema di password tooauthenticate con del Registro di sistema di hello contenitore.</span><span class="sxs-lookup"><span data-stu-id="33636-108">If you specify a private image in hello `create` command, you can also specify hello image registry password required tooauthenticate with hello container registry.</span></span>

```azurecli-interactive
az container create --name myprivatecontainer --image mycontainerregistry.azurecr.io/mycontainerimage:v1 --registry-password myRegistryPassword --resource-group myresourcegroup
```

<span data-ttu-id="33636-109">Hello `create` comando inoltre supporta la definizione di hello `registry-login-server` e `registry-username`.</span><span class="sxs-lookup"><span data-stu-id="33636-109">hello `create` command also supports specifying hello `registry-login-server` and `registry-username`.</span></span> <span data-ttu-id="33636-110">Tuttavia, il server di accesso hello per hello del Registro di sistema di Azure contenitore è sempre *registryname*. nome utente predefinito azurecr.io e hello *registryname*, pertanto questi valori vengono dedotti dal nome dell'immagine hello se non specificato in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="33636-110">However, hello login server for hello Azure Container Registry is always *registryname*.azurecr.io and hello default username is *registryname*, so these values are inferred from hello image name if not explicitly provided.</span></span>

## <a name="using-an-azure-resource-manager-template"></a><span data-ttu-id="33636-111">Uso di un modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="33636-111">Using an Azure Resource Manager template</span></span>

<span data-ttu-id="33636-112">È possibile specificare proprietà hello Azure contenitore del Registro di sistema in un modello di gestione risorse di Azure includendo hello `imageRegistryCredentials` proprietà nella definizione del gruppo contenitore hello:</span><span class="sxs-lookup"><span data-stu-id="33636-112">You can specify hello properties of your Azure Container Registry in an Azure Resource Manager template by including hello `imageRegistryCredentials` property in hello container group definition:</span></span>

```json
"imageRegistryCredentials": [
  {
    "server": "imageRegistryLoginServer",
    "username": "imageRegistryUsername",
    "password": "imageRegistryPassword"
  }
]
```

<span data-ttu-id="33636-113">tooavoid archiviare la password del Registro di sistema contenitore direttamente nel modello di hello, è consigliabile memorizzarlo come segreto in [insieme credenziali chiavi Azure](../key-vault/key-vault-manage-with-cli2.md) e farvi riferimento nel modello di hello utilizzando hello [integrazione nativa tra Hello Azure Resource Manager e l'insieme di credenziali chiave](../azure-resource-manager/resource-manager-keyvault-parameter.md).</span><span class="sxs-lookup"><span data-stu-id="33636-113">tooavoid storing your container registry password directly in hello template, we recommend that you store it as a secret in [Azure Key Vault](../key-vault/key-vault-manage-with-cli2.md) and reference it in hello template using hello [native integration between hello Azure Resource Manager and Key Vault](../azure-resource-manager/resource-manager-keyvault-parameter.md).</span></span>

## <a name="using-hello-azure-portal"></a><span data-ttu-id="33636-114">Utilizzo di hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="33636-114">Using hello Azure portal</span></span>

<span data-ttu-id="33636-115">Se si mantengono le immagini contenitore in hello del Registro di sistema contenitore di Azure, è possibile creare facilmente un contenitore in istanze di contenitori di Azure utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="33636-115">If you maintain container images in hello Azure Container Registry, you can easily create a container in Azure Container Instances using hello Azure portal.</span></span>

1. <span data-ttu-id="33636-116">Nel portale di Azure hello, passare tooyour del Registro di sistema contenitore.</span><span class="sxs-lookup"><span data-stu-id="33636-116">In hello Azure portal, navigate tooyour container registry.</span></span>

2. <span data-ttu-id="33636-117">Scegliere Repository.</span><span class="sxs-lookup"><span data-stu-id="33636-117">Choose Repositories.</span></span>

    ![dal menu del Registro di sistema di Azure contenitore Hello hello portale di Azure][acr-menu]

3. <span data-ttu-id="33636-119">Scegliere il repository hello che si desidera toodeploy da.</span><span class="sxs-lookup"><span data-stu-id="33636-119">Choose hello repository that you want toodeploy from.</span></span>

4. <span data-ttu-id="33636-120">Fare doppio clic su tag hello per immagine contenitore hello desiderato toodeploy.</span><span class="sxs-lookup"><span data-stu-id="33636-120">Right-click hello tag for hello container image you want toodeploy.</span></span>

    ![Menu di scelta rapida per avviare il contenitore con Istanze di contenitore di Azure][acr-runinstance-contextmenu]

5. <span data-ttu-id="33636-122">Immettere un nome per il contenitore di hello e un nome per il gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="33636-122">Enter a name for hello container and a name for hello resource group.</span></span> <span data-ttu-id="33636-123">Se si desidera, è possibile modificare anche i valori predefiniti di hello.</span><span class="sxs-lookup"><span data-stu-id="33636-123">You can also change hello default values if you wish.</span></span>

    ![Menu di creazione per Istanze di contenitore di Azure][acr-create-deeplink]

6. <span data-ttu-id="33636-125">Una volta completata la distribuzione di hello, è possibile passare il gruppo di contenitori toohello da hello notifiche riquadro toofind l'indirizzo IP e altre proprietà.</span><span class="sxs-lookup"><span data-stu-id="33636-125">Once hello deployment completes, you can navigate toohello container group from hello notifications pane toofind its IP address and other properties.</span></span>

    ![Visualizzazione dei dettagli del gruppo di contenitori in Istanze di contenitore di Azure][aci-detailsview]

## <a name="next-steps"></a><span data-ttu-id="33636-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="33636-127">Next steps</span></span>

<span data-ttu-id="33636-128">Informazioni su come effettuare il push del Registro di sistema di tooa contenitore privato, contenitori toobuild e distribuirli istanze di contenitori tooAzure da [completato hello esercitazione](container-instances-tutorial-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="33636-128">Learn how toobuild containers, push them tooa private container registry, and deploy them tooAzure Container Instances by [completing hello tutorial](container-instances-tutorial-prepare-app.md).</span></span>

<!-- IMAGES -->
[acr-menu]: ./media/container-instances-using-azure-container-registry/acr-menu.png

[acr-runinstance-contextmenu]: ./media/container-instances-using-azure-container-registry/acr-runinstance-contextmenu.png

[acr-create-deeplink]: ./media/container-instances-using-azure-container-registry/acr-create-deeplink.png

[aci-detailsview]: ./media/container-instances-using-azure-container-registry/aci-detailsview.png
