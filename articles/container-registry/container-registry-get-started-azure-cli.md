---
title: aaaCreate registro contenitore privato Docker - CLI di Azure | Documenti Microsoft
description: Iniziare a creare e gestire i registri contenitore Docker privati con hello Azure CLI 2.0
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0d876a70b71a5e1bd564fbc9198f693dfe8a347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-cli-20"></a><span data-ttu-id="8a655-103">Creare un registro di sistema contenitore Docker privata mediante hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8a655-103">Create a private Docker container registry using hello Azure CLI 2.0</span></span>
<span data-ttu-id="8a655-104">Utilizzare i comandi in hello [CLI di Azure 2.0](https://github.com/Azure/azure-cli) toocreate del Registro di sistema un contenitore e gestire le impostazioni dal computer Linux, Mac e Windows.</span><span class="sxs-lookup"><span data-stu-id="8a655-104">Use commands in hello [Azure CLI 2.0](https://github.com/Azure/azure-cli) toocreate a container registry and manage its settings from your Linux, Mac, or Windows computer.</span></span> <span data-ttu-id="8a655-105">È anche possibile creare e gestire i registri di contenitore usando hello [portale di Azure](container-registry-get-started-portal.md) o a livello di codice con hello contenitore del Registro di sistema [API REST](https://go.microsoft.com/fwlink/p/?linkid=834376).</span><span class="sxs-lookup"><span data-stu-id="8a655-105">You can also create and manage container registries using hello [Azure portal](container-registry-get-started-portal.md) or programmatically with hello Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>


* <span data-ttu-id="8a655-106">Per lo sfondo e i concetti, vedere [hello Panoramica](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="8a655-106">For background and concepts, see [hello overview](container-registry-intro.md)</span></span>
* <span data-ttu-id="8a655-107">Per informazioni sui comandi CLI di contenitore del Registro di sistema (`az acr` comandi), passare hello `-h` comando tooany di parametro.</span><span class="sxs-lookup"><span data-stu-id="8a655-107">For help on Container Registry CLI commands (`az acr` commands), pass hello `-h` parameter tooany command.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="8a655-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8a655-108">Prerequisites</span></span>
* <span data-ttu-id="8a655-109">**Azure CLI 2.0**: tooinstall e iniziare a utilizzare hello CLI 2.0, vedere hello [le istruzioni di installazione](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8a655-109">**Azure CLI 2.0**: tooinstall and get started with hello CLI 2.0, see hello [installation instructions](/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="8a655-110">Accedi tooyour sottoscrizione di Azure eseguendo `az login`.</span><span class="sxs-lookup"><span data-stu-id="8a655-110">Log in tooyour Azure subscription by running `az login`.</span></span> <span data-ttu-id="8a655-111">Per ulteriori informazioni, vedere [introduzione hello CLI 2.0](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8a655-111">For more information, see [Get started with hello CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>
* <span data-ttu-id="8a655-112">**Gruppo di risorse**: creare un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md#resource-groups) prima di creare un registro di contenitori o usare un gruppo di risorse esistente.</span><span class="sxs-lookup"><span data-stu-id="8a655-112">**Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group.</span></span> <span data-ttu-id="8a655-113">Verificare che il gruppo di risorse hello è in una posizione in cui è hello servizio Registro di sistema contenitore [disponibile](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="8a655-113">Make sure hello resource group is in a location where hello Container Registry service is [available](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="8a655-114">un gruppo di risorse utilizzando toocreate hello 2.0 CLI, vedere [hello riferimento CLI 2.0](/cli/azure/group).</span><span class="sxs-lookup"><span data-stu-id="8a655-114">toocreate a resource group using hello CLI 2.0, see [hello CLI 2.0 reference](/cli/azure/group).</span></span>
* <span data-ttu-id="8a655-115">**Account di archiviazione** (facoltativo): creare un Azure standard [account di archiviazione](../storage/common/storage-introduction.md) tooback hello contenitore nel Registro di sistema hello nello stesso percorso.</span><span class="sxs-lookup"><span data-stu-id="8a655-115">**Storage account** (optional): Create a standard Azure [storage account](../storage/common/storage-introduction.md) tooback hello container registry in hello same location.</span></span> <span data-ttu-id="8a655-116">Se non si specifica un account di archiviazione durante la creazione di un registro di sistema `az acr create`, comando hello viene creata una automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8a655-116">If you don't specify a storage account when creating a registry with `az acr create`, hello command creates one for you.</span></span> <span data-ttu-id="8a655-117">un archivio account tramite toocreate hello CLI 2.0, vedere [hello riferimento CLI 2.0](/cli/azure/storage/account).</span><span class="sxs-lookup"><span data-stu-id="8a655-117">toocreate a storage account using hello CLI 2.0, see [hello CLI 2.0 reference](/cli/azure/storage/account).</span></span> <span data-ttu-id="8a655-118">Archiviazione Premium non è attualmente supportata.</span><span class="sxs-lookup"><span data-stu-id="8a655-118">Currently Premium Storage is not supported.</span></span>
* <span data-ttu-id="8a655-119">**Entità servizio** (facoltativo): quando si crea un registro di sistema con hello CLI, per impostazione predefinita non è configurato per l'accesso.</span><span class="sxs-lookup"><span data-stu-id="8a655-119">**Service principal** (optional): When you create a registry with hello CLI, by default it is not set up for access.</span></span> <span data-ttu-id="8a655-120">A seconda delle esigenze, è possibile assegnare un registro tooa principale di servizio Azure Active Directory esistente o creare e assegnare uno nuovo, o abilitare l'account amministratore del Registro di sistema di hello.</span><span class="sxs-lookup"><span data-stu-id="8a655-120">Depending on your needs, you can assign an existing Azure Active Directory service principal tooa registry (or create and assign a new one), or enable hello registry's admin user account.</span></span> <span data-ttu-id="8a655-121">Vedere hello sezioni più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="8a655-121">See hello sections later in this article.</span></span> <span data-ttu-id="8a655-122">Per ulteriori informazioni sull'accesso del Registro di sistema, vedere [autentica con del Registro di sistema di hello contenitore](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="8a655-122">For more information about registry access, see [Authenticate with hello container registry](container-registry-authentication.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="8a655-123">Creare un registro di contenitori</span><span class="sxs-lookup"><span data-stu-id="8a655-123">Create a container registry</span></span>
<span data-ttu-id="8a655-124">Eseguire hello `az acr create` toocreate comando del Registro di sistema un contenitore.</span><span class="sxs-lookup"><span data-stu-id="8a655-124">Run hello `az acr create` command toocreate a container registry.</span></span>

> [!TIP]
> <span data-ttu-id="8a655-125">Quando si crea un registro, specificare un nome di dominio univoco globale di primo livello, contenente solo lettere e numeri.</span><span class="sxs-lookup"><span data-stu-id="8a655-125">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span> <span data-ttu-id="8a655-126">nome del Registro di sistema Hello negli esempi di hello è `myRegistry1`, ma sostituire un nome univoco del proprio.</span><span class="sxs-lookup"><span data-stu-id="8a655-126">hello registry name in hello examples is `myRegistry1`, but substitute a unique name of your own.</span></span>
>
>

<span data-ttu-id="8a655-127">Hello comando utilizza hello del Registro di sistema di numero minimo di parametri toocreate contenitore seguente `myRegistry1` nel gruppo di risorse hello `myResourceGroup`e l'utilizzo di hello *base* sku:</span><span class="sxs-lookup"><span data-stu-id="8a655-127">hello following command uses hello minimal parameters toocreate container registry `myRegistry1` in hello resource group `myResourceGroup`, and using hello *Basic* sku:</span></span>

```azurecli
az acr create --name myRegistry1 --resource-group myResourceGroup --sku Basic
```

* <span data-ttu-id="8a655-128">`--storage-account-name` è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="8a655-128">`--storage-account-name` is optional.</span></span> <span data-ttu-id="8a655-129">Se non viene specificato, viene creato un account di archiviazione con un nome composto dal nome del Registro di sistema hello e un timestamp in hello specificato gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="8a655-129">If not specified, a storage account is created with a name consisting of hello registry name and a timestamp in hello specified resource group.</span></span>

<span data-ttu-id="8a655-130">Quando viene creato il registro hello, l'output di hello è simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="8a655-130">When hello registry is created, hello output is similar toohello following:</span></span>

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T18:36:29.124842+00:00",
  "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry
/registries/myRegistry1",
  "location": "southcentralus",
  "loginServer": "myregistry1.azurecr.io",
  "name": "myRegistry1",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "myregistry123456789"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}

```


<span data-ttu-id="8a655-131">Considerare con attenzione le seguenti voci:</span><span class="sxs-lookup"><span data-stu-id="8a655-131">Take special note:</span></span>

* <span data-ttu-id="8a655-132">`id`-Identificatore del Registro di sistema hello nella sottoscrizione, è necessario se si desidera tooassign un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="8a655-132">`id` - Identifier for hello registry in your subscription, which you need if you want tooassign a service principal.</span></span>
* <span data-ttu-id="8a655-133">`loginServer`-nome completo di hello specificato troppo[log nel Registro di sistema toohello](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="8a655-133">`loginServer` - hello fully qualified name you specify too[log in toohello registry](container-registry-authentication.md).</span></span> <span data-ttu-id="8a655-134">In questo esempio, è il nome di hello `myregistry1.exp.azurecr.io` (tutti in lettere minuscole).</span><span class="sxs-lookup"><span data-stu-id="8a655-134">In this example, hello name is `myregistry1.exp.azurecr.io` (all lowercase).</span></span>

## <a name="assign-a-service-principal"></a><span data-ttu-id="8a655-135">Assegnare un'entità servizio</span><span class="sxs-lookup"><span data-stu-id="8a655-135">Assign a service principal</span></span>
<span data-ttu-id="8a655-136">Utilizzare i comandi di CLI 2.0 tooassign un registro tooa dell'entità servizio di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8a655-136">Use CLI 2.0 commands tooassign an Azure Active Directory service principal tooa registry.</span></span> <span data-ttu-id="8a655-137">Hello dell'entità servizio in questi esempi viene assegnato il ruolo di proprietario hello, ma è possibile assegnare [altri ruoli](../active-directory/role-based-access-control-configure.md) se si desidera.</span><span class="sxs-lookup"><span data-stu-id="8a655-137">hello service principal in these examples is assigned hello Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.</span></span>

### <a name="create-a-service-principal-and-assign-access-toohello-registry"></a><span data-ttu-id="8a655-138">Creare un'entità servizio e assegnare del Registro di sistema di accesso toohello</span><span class="sxs-lookup"><span data-stu-id="8a655-138">Create a service principal and assign access toohello registry</span></span>
<span data-ttu-id="8a655-139">In hello comando seguente, una nuova entità servizio viene assegnata l'ID proprietario ruolo accesso toohello del Registro di sistema superato con hello `--scopes` parametro.</span><span class="sxs-lookup"><span data-stu-id="8a655-139">In hello following command, a new service principal is assigned Owner role access toohello registry identifier passed with hello `--scopes` parameter.</span></span> <span data-ttu-id="8a655-140">Specificare una password complessa con hello `--password` parametro.</span><span class="sxs-lookup"><span data-stu-id="8a655-140">Specify a strong password with hello `--password` parameter.</span></span>

```azurecli
az ad sp create-for-rbac --scopes /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --password myPassword
```



### <a name="assign-an-existing-service-principal"></a><span data-ttu-id="8a655-141">Assegnare un'entità servizio esistente</span><span class="sxs-lookup"><span data-stu-id="8a655-141">Assign an existing service principal</span></span>
<span data-ttu-id="8a655-142">Se si dispone di un'entità servizio già e desidera tooassign è proprietario ruolo accesso toohello Registro di sistema, eseguire una toohello simile comando riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="8a655-142">If you already have a service principal and want tooassign it Owner role access toohello registry, run a command similar toohello following example.</span></span> <span data-ttu-id="8a655-143">Si passa hello ID app dell'entità del servizio utilizzando hello `--assignee` parametro:</span><span class="sxs-lookup"><span data-stu-id="8a655-143">You pass hello service principal app ID using hello `--assignee` parameter:</span></span>

```azurecli
az role assignment create --scope /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --assignee myAppId
```



## <a name="manage-admin-credentials"></a><span data-ttu-id="8a655-144">Gestire le credenziali di amministratore</span><span class="sxs-lookup"><span data-stu-id="8a655-144">Manage admin credentials</span></span>
<span data-ttu-id="8a655-145">Per ogni registro di contenitori viene creato automaticamente un account amministratore che è disabilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="8a655-145">An admin account is automatically created for each container registry and is disabled by default.</span></span> <span data-ttu-id="8a655-146">Hello seguente mostra esempi `az acr` CLI comandi credenziali di amministratore hello toomanage per il Registro di sistema del contenitore.</span><span class="sxs-lookup"><span data-stu-id="8a655-146">hello following examples show `az acr` CLI commands toomanage hello admin credentials for your container registry.</span></span>

### <a name="obtain-admin-user-credentials"></a><span data-ttu-id="8a655-147">Ottenere le credenziali di utente amministratore</span><span class="sxs-lookup"><span data-stu-id="8a655-147">Obtain admin user credentials</span></span>
```azurecli
az acr credential show -n myRegistry1
```

### <a name="enable-admin-user-for-an-existing-registry"></a><span data-ttu-id="8a655-148">Abilitare l'utente amministratore per un registro esistente</span><span class="sxs-lookup"><span data-stu-id="8a655-148">Enable admin user for an existing registry</span></span>
```azurecli
az acr update -n myRegistry1 --admin-enabled true
```

### <a name="disable-admin-user-for-an-existing-registry"></a><span data-ttu-id="8a655-149">Disabilitare l'utente amministratore per un registro esistente</span><span class="sxs-lookup"><span data-stu-id="8a655-149">Disable admin user for an existing registry</span></span>
```azurecli
az acr update -n myRegistry1 --admin-enabled false
```

## <a name="list-images-and-tags"></a><span data-ttu-id="8a655-150">Elencare immagini e tag</span><span class="sxs-lookup"><span data-stu-id="8a655-150">List images and tags</span></span>
<span data-ttu-id="8a655-151">Hello utilizzare `az acr` contiene i comandi CLI immagini hello tooquery e tag in un repository.</span><span class="sxs-lookup"><span data-stu-id="8a655-151">Use hello `az acr` CLI commands tooquery hello images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="8a655-152">Registro di sistema di contenitore non supporta attualmente hello `docker search` comando tooquery per immagini e i tag.</span><span class="sxs-lookup"><span data-stu-id="8a655-152">Currently, Container Registry does not support hello `docker search` command tooquery for images and tags.</span></span>


### <a name="list-repositories"></a><span data-ttu-id="8a655-153">Elencare repository</span><span class="sxs-lookup"><span data-stu-id="8a655-153">List repositories</span></span>
<span data-ttu-id="8a655-154">Hello esempio seguente vengono elencati i repository hello nel Registro di sistema, in formato JSON (JavaScript Object Notation):</span><span class="sxs-lookup"><span data-stu-id="8a655-154">hello following example lists hello repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="8a655-155">Elencare tag</span><span class="sxs-lookup"><span data-stu-id="8a655-155">List tags</span></span>
<span data-ttu-id="8a655-156">Hello esempio seguente vengono elencati i tag hello in hello **esempi/nginx** repository, in formato JSON:</span><span class="sxs-lookup"><span data-stu-id="8a655-156">hello following example lists hello tags on hello **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="8a655-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8a655-157">Next steps</span></span>
* [<span data-ttu-id="8a655-158">La prima immagine usando Docker CLI hello push</span><span class="sxs-lookup"><span data-stu-id="8a655-158">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
