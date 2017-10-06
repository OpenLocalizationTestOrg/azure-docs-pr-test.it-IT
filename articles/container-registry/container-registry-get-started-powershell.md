---
title: repository del Registro di sistema di contenitore aaaAzure | Documenti Microsoft
description: Il repository del Registro di sistema di Azure contenitore toouse per le immagini Docker
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: cristyg
ms.openlocfilehash: 448fb812f537c9502041ce5fb372b0681a9dac4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-powershell"></a><span data-ttu-id="b765a-103">Creare un registro di sistema contenitore Docker privata mediante hello Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b765a-103">Create a private Docker container registry using hello Azure PowerShell</span></span>
<span data-ttu-id="b765a-104">Usare i comandi in [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) toocreate del Registro di sistema un contenitore e gestire le impostazioni dal computer Windows.</span><span class="sxs-lookup"><span data-stu-id="b765a-104">Use commands in [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) toocreate a container registry and manage its settings from your Windows computer.</span></span> <span data-ttu-id="b765a-105">È anche possibile creare e gestire i registri di contenitore usando hello [portale di Azure](container-registry-get-started-portal.md), hello [CLI di Azure](container-registry-get-started-azure-cli.md), o a livello di codice con hello contenitore del Registro di sistema [API REST](https://go.microsoft.com/fwlink/p/?linkid=834376).</span><span class="sxs-lookup"><span data-stu-id="b765a-105">You can also create and manage container registries using hello [Azure portal](container-registry-get-started-portal.md), hello [Azure CLI](container-registry-get-started-azure-cli.md), or programmatically with hello Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>


* <span data-ttu-id="b765a-106">Per lo sfondo e i concetti, vedere [hello Panoramica](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="b765a-106">For background and concepts, see [hello overview](container-registry-intro.md)</span></span>
* <span data-ttu-id="b765a-107">Per un elenco completo dei cmdlet supportati, vedere [AzureRM.ContainerRegistry](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).</span><span class="sxs-lookup"><span data-stu-id="b765a-107">For a full list of supported cmdlets, see [Azure Container Registry Management Cmdlets](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="b765a-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b765a-108">Prerequisites</span></span>
* <span data-ttu-id="b765a-109">**Azure PowerShell**: tooinstall e acquisire familiarità con Azure PowerShell, vedere hello [le istruzioni di installazione](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="b765a-109">**Azure PowerShell**: tooinstall and get started with Azure PowerShell, see hello [installation instructions](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="b765a-110">Accedi tooyour sottoscrizione di Azure eseguendo `Login-AzureRMAccount`.</span><span class="sxs-lookup"><span data-stu-id="b765a-110">Log in tooyour Azure subscription by running `Login-AzureRMAccount`.</span></span> <span data-ttu-id="b765a-111">Per altre informazioni, vedere [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep) (Introduzione ad Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="b765a-111">For more information, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).</span></span>
* <span data-ttu-id="b765a-112">**Gruppo di risorse**: creare un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md#resource-groups) prima di creare un registro di contenitori o usare un gruppo di risorse esistente.</span><span class="sxs-lookup"><span data-stu-id="b765a-112">**Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group.</span></span> <span data-ttu-id="b765a-113">Verificare che il gruppo di risorse hello è in una posizione in cui è hello servizio Registro di sistema contenitore [disponibile](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="b765a-113">Make sure hello resource group is in a location where hello Container Registry service is [available](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="b765a-114">toocreate un gruppo di risorse con Azure PowerShell, vedere [hello PowerShell riferimento](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).</span><span class="sxs-lookup"><span data-stu-id="b765a-114">toocreate a resource group using Azure PowerShell, see [hello PowerShell reference](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).</span></span>
* <span data-ttu-id="b765a-115">**Account di archiviazione** (facoltativo): creare un Azure standard [account di archiviazione](../storage/common/storage-introduction.md) tooback hello contenitore nel Registro di sistema hello nello stesso percorso.</span><span class="sxs-lookup"><span data-stu-id="b765a-115">**Storage account** (optional): Create a standard Azure [storage account](../storage/common/storage-introduction.md) tooback hello container registry in hello same location.</span></span> <span data-ttu-id="b765a-116">Se non si specifica un account di archiviazione durante la creazione di un registro di sistema `New-AzureRMContainerRegistry`, comando hello viene creata una automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b765a-116">If you don't specify a storage account when creating a registry with `New-AzureRMContainerRegistry`, hello command creates one for you.</span></span> <span data-ttu-id="b765a-117">uno spazio di archiviazione toocreate account usando PowerShell, vedere [hello PowerShell riferimento](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount).</span><span class="sxs-lookup"><span data-stu-id="b765a-117">toocreate a storage account using PowerShell, see [hello PowerShell reference](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount).</span></span> <span data-ttu-id="b765a-118">Archiviazione Premium non è attualmente supportata.</span><span class="sxs-lookup"><span data-stu-id="b765a-118">Currently Premium Storage is not supported.</span></span>
* <span data-ttu-id="b765a-119">**Entità servizio** (facoltativo): quando si crea un registro con PowerShell, per impostazione predefinita il registro non è configurato per l'accesso.</span><span class="sxs-lookup"><span data-stu-id="b765a-119">**Service principal** (optional): When you create a registry with PowerShell, by default it is not set up for access.</span></span> <span data-ttu-id="b765a-120">A seconda delle esigenze, è possibile assegnare un registro tooa principale di servizio Azure Active Directory esistente, creare e assegnare una nuova.</span><span class="sxs-lookup"><span data-stu-id="b765a-120">Depending on your needs, you can assign an existing Azure Active Directory service principal tooa registry or create and assign a new one.</span></span> <span data-ttu-id="b765a-121">In alternativa, è possibile abilitare l'account amministratore del Registro di sistema di hello.</span><span class="sxs-lookup"><span data-stu-id="b765a-121">Alternatively, you can enable hello registry's admin user account.</span></span> <span data-ttu-id="b765a-122">Vedere hello sezioni più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="b765a-122">See hello sections later in this article.</span></span> <span data-ttu-id="b765a-123">Per ulteriori informazioni sull'accesso del Registro di sistema, vedere [autentica con del Registro di sistema di hello contenitore](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b765a-123">For more information about registry access, see [Authenticate with hello container registry](container-registry-authentication.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="b765a-124">Creare un registro di contenitori</span><span class="sxs-lookup"><span data-stu-id="b765a-124">Create a container registry</span></span>
<span data-ttu-id="b765a-125">Eseguire hello `New-AzureRMContainerRegistry` toocreate comando del Registro di sistema un contenitore.</span><span class="sxs-lookup"><span data-stu-id="b765a-125">Run hello `New-AzureRMContainerRegistry` command toocreate a container registry.</span></span>

> [!TIP]
> <span data-ttu-id="b765a-126">Quando si crea un registro, specificare un nome di dominio univoco globale di primo livello, contenente solo lettere e numeri.</span><span class="sxs-lookup"><span data-stu-id="b765a-126">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span> <span data-ttu-id="b765a-127">nome del Registro di sistema Hello negli esempi di hello è `MyRegistry`, ma sostituire un nome univoco del proprio.</span><span class="sxs-lookup"><span data-stu-id="b765a-127">hello registry name in hello examples is `MyRegistry`, but substitute a unique name of your own.</span></span>
>
>

<span data-ttu-id="b765a-128">Hello comando utilizza hello del Registro di sistema di numero minimo di parametri toocreate contenitore seguente `MyRegistry` nel gruppo di risorse hello `MyResourceGroup` in hello centro-meridionali percorso:</span><span class="sxs-lookup"><span data-stu-id="b765a-128">hello following command uses hello minimal parameters toocreate container registry `MyRegistry` in hello resource group `MyResourceGroup` in hello South Central US location:</span></span>

```PowerShell
$Registry = New-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

* <span data-ttu-id="b765a-129">`-StorageAccountName` è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="b765a-129">`-StorageAccountName` is optional.</span></span> <span data-ttu-id="b765a-130">Se non viene specificato, viene creato un account di archiviazione con un nome composto dal nome del Registro di sistema hello e un timestamp in hello specificato gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="b765a-130">If not specified, a storage account is created with a name consisting of hello registry name and a timestamp in hello specified resource group.</span></span>

## <a name="assign-a-service-principal"></a><span data-ttu-id="b765a-131">Assegnare un'entità servizio</span><span class="sxs-lookup"><span data-stu-id="b765a-131">Assign a service principal</span></span>
<span data-ttu-id="b765a-132">Utilizzare i comandi di PowerShell tooassign di Azure Active Directory [dell'entità servizio](../azure-resource-manager/resource-group-authenticate-service-principal.md) tooa Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="b765a-132">Use PowerShell commands tooassign an Azure Active Directory [service principal](../azure-resource-manager/resource-group-authenticate-service-principal.md) tooa registry.</span></span> <span data-ttu-id="b765a-133">Hello dell'entità servizio in questi esempi viene assegnato il ruolo di proprietario hello, ma è possibile assegnare [altri ruoli](../active-directory/role-based-access-control-configure.md) se si desidera.</span><span class="sxs-lookup"><span data-stu-id="b765a-133">hello service principal in these examples is assigned hello Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.</span></span>

### <a name="create-a-service-principal"></a><span data-ttu-id="b765a-134">Creare un’entità servizio</span><span class="sxs-lookup"><span data-stu-id="b765a-134">Create a service principal</span></span>
<span data-ttu-id="b765a-135">Nel comando seguente di hello, viene creata una nuova entità servizio.</span><span class="sxs-lookup"><span data-stu-id="b765a-135">In hello following command, a new service principal is created.</span></span> <span data-ttu-id="b765a-136">Specificare una password complessa con hello `-Password` parametro.</span><span class="sxs-lookup"><span data-stu-id="b765a-136">Specify a strong password with hello `-Password` parameter.</span></span>

```PowerShell
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName ApplicationDisplayName -Password "MyPassword"
```

### <a name="assign-a-new-or-existing-service-principal"></a><span data-ttu-id="b765a-137">Assegnare un'entità servizio nuova o esistente</span><span class="sxs-lookup"><span data-stu-id="b765a-137">Assign a new or existing service principal</span></span>
<span data-ttu-id="b765a-138">È possibile assegnare un nuovo oggetto o un registro di sistema di tooa dell'entità servizio esistente.</span><span class="sxs-lookup"><span data-stu-id="b765a-138">You can assign a new or an existing service principal tooa registry.</span></span> <span data-ttu-id="b765a-139">tooassign è proprietario ruolo accesso toohello Registro di sistema, eseguire una toohello simile comando riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="b765a-139">tooassign it Owner role access toohello registry, run a command similar toohello following example:</span></span>

```PowerShell
New-AzureRMRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Registry.Id
```

##<a name="sign-in-toohello-registry-with-hello-service-principal"></a><span data-ttu-id="b765a-140">Accedi al Registro di sistema toohello entità servizio hello</span><span class="sxs-lookup"><span data-stu-id="b765a-140">Sign in toohello registry with hello service principal</span></span>
<span data-ttu-id="b765a-141">Dopo l'assegnazione del Registro di sistema di hello servizio toohello principale, è possibile accedere tramite hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b765a-141">After assigning hello service principal toohello registry, you can sign in using hello following command:</span></span>

```PowerShell
docker login -u $ServicePrincipal.ApplicationId -p myPassword
```

## <a name="manage-admin-credentials"></a><span data-ttu-id="b765a-142">Gestire le credenziali di amministratore</span><span class="sxs-lookup"><span data-stu-id="b765a-142">Manage admin credentials</span></span>
<span data-ttu-id="b765a-143">Per ogni registro di contenitori viene creato automaticamente un account amministratore che è disabilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="b765a-143">An admin account is automatically created for each container registry and is disabled by default.</span></span> <span data-ttu-id="b765a-144">Hello esempi seguenti mostrano i comandi di PowerShell le credenziali di amministratore hello toomanage per il Registro di sistema del contenitore.</span><span class="sxs-lookup"><span data-stu-id="b765a-144">hello following examples show PowerShell commands toomanage hello admin credentials for your container registry.</span></span>

### <a name="obtain-admin-user-credentials"></a><span data-ttu-id="b765a-145">Ottenere le credenziali di utente amministratore</span><span class="sxs-lookup"><span data-stu-id="b765a-145">Obtain admin user credentials</span></span>
```PowerShell
Get-AzureRMContainerRegistryCredential -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

### <a name="enable-admin-user-for-an-existing-registry"></a><span data-ttu-id="b765a-146">Abilitare l'utente amministratore per un registro esistente</span><span class="sxs-lookup"><span data-stu-id="b765a-146">Enable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -EnableAdminUser
```

### <a name="disable-admin-user-for-an-existing-registry"></a><span data-ttu-id="b765a-147">Disabilitare l'utente amministratore per un registro esistente</span><span class="sxs-lookup"><span data-stu-id="b765a-147">Disable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -DisableAdminUser
```

## <a name="next-steps"></a><span data-ttu-id="b765a-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b765a-148">Next steps</span></span>
* [<span data-ttu-id="b765a-149">La prima immagine usando Docker CLI hello push</span><span class="sxs-lookup"><span data-stu-id="b765a-149">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
