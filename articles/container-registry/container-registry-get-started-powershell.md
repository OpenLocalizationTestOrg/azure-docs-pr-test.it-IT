---
title: Archivi di registri contenitori di Azure | Documentazione Microsoft
description: Come usare gli archivi di registri contenitori di Azure per le immagini Docker
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
ms.openlocfilehash: 1e5d5ea5b1ec121fe008abc48178b1d58f540ce1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-private-docker-container-registry-using-the-azure-powershell"></a><span data-ttu-id="742ac-103">Creare un registro contenitori Docker privati con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="742ac-103">Create a private Docker container registry using the Azure PowerShell</span></span>
<span data-ttu-id="742ac-104">Usare i comandi in [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) per creare un registro contenitori e gestirne le impostazioni dal computer Windows.</span><span class="sxs-lookup"><span data-stu-id="742ac-104">Use commands in [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) to create a container registry and manage its settings from your Windows computer.</span></span> <span data-ttu-id="742ac-105">È anche possibile creare e gestire registri di contenitori usando il [portale di Azure](container-registry-get-started-portal.md), l'[interfaccia della riga di comando di Azure](https://go.microsoft.com/fwlink/p/?linkid=834376) oppure a livello di codice con l'[API REST](container-registry-get-started-azure-cli.md) del servizio Registro contenitori.</span><span class="sxs-lookup"><span data-stu-id="742ac-105">You can also create and manage container registries using the [Azure portal](container-registry-get-started-portal.md), the [Azure CLI](container-registry-get-started-azure-cli.md), or programmatically with the Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>


* <span data-ttu-id="742ac-106">Per informazioni di base e concetti, vedere la [panoramica](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="742ac-106">For background and concepts, see [the overview](container-registry-intro.md)</span></span>
* <span data-ttu-id="742ac-107">Per un elenco completo dei cmdlet supportati, vedere [AzureRM.ContainerRegistry](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).</span><span class="sxs-lookup"><span data-stu-id="742ac-107">For a full list of supported cmdlets, see [Azure Container Registry Management Cmdlets](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="742ac-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="742ac-108">Prerequisites</span></span>
* <span data-ttu-id="742ac-109">**Azure PowerShell**: per installare e iniziare a usare Azure PowerShell, vedere le [istruzioni di installazione](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="742ac-109">**Azure PowerShell**: To install and get started with Azure PowerShell, see the [installation instructions](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="742ac-110">Accedere alla sottoscrizione di Azure usando `Login-AzureRMAccount`.</span><span class="sxs-lookup"><span data-stu-id="742ac-110">Log in to your Azure subscription by running `Login-AzureRMAccount`.</span></span> <span data-ttu-id="742ac-111">Per altre informazioni, vedere [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep) (Introduzione ad Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="742ac-111">For more information, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).</span></span>
* <span data-ttu-id="742ac-112">**Gruppo di risorse**: creare un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md#resource-groups) prima di creare un registro di contenitori o usare un gruppo di risorse esistente.</span><span class="sxs-lookup"><span data-stu-id="742ac-112">**Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group.</span></span> <span data-ttu-id="742ac-113">Verificare che il gruppo di risorse si trovi in una posizione in cui il servizio Container Registry è [disponibile](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="742ac-113">Make sure the resource group is in a location where the Container Registry service is [available](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="742ac-114">Per creare un gruppo di risorse con Azure PowerShell, vedere la [documentazione di riferimento su PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).</span><span class="sxs-lookup"><span data-stu-id="742ac-114">To create a resource group using Azure PowerShell, see [the PowerShell reference](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).</span></span>
* <span data-ttu-id="742ac-115">**Account di archiviazione** (facoltativo): creare un [account di archiviazione](../storage/common/storage-introduction.md) di Azure standard per eseguire il backup del registro di contenitori nella stessa posizione.</span><span class="sxs-lookup"><span data-stu-id="742ac-115">**Storage account** (optional): Create a standard Azure [storage account](../storage/common/storage-introduction.md) to back the container registry in the same location.</span></span> <span data-ttu-id="742ac-116">Se non si specifica un account di archiviazione durante la creazione di un registro con `New-AzureRMContainerRegistry`, l'account viene creato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="742ac-116">If you don't specify a storage account when creating a registry with `New-AzureRMContainerRegistry`, the command creates one for you.</span></span> <span data-ttu-id="742ac-117">Per creare un account di archiviazione con PowerShell, vedere la [documentazione di riferimento su PowerShell](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount).</span><span class="sxs-lookup"><span data-stu-id="742ac-117">To create a storage account using PowerShell, see [the PowerShell reference](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount).</span></span> <span data-ttu-id="742ac-118">Archiviazione Premium non è attualmente supportata.</span><span class="sxs-lookup"><span data-stu-id="742ac-118">Currently Premium Storage is not supported.</span></span>
* <span data-ttu-id="742ac-119">**Entità servizio** (facoltativo): quando si crea un registro con PowerShell, per impostazione predefinita il registro non è configurato per l'accesso.</span><span class="sxs-lookup"><span data-stu-id="742ac-119">**Service principal** (optional): When you create a registry with PowerShell, by default it is not set up for access.</span></span> <span data-ttu-id="742ac-120">A seconda delle esigenze, è possibile assegnare a un registro un'entità servizio Azure Active Directory esistente oppure crearne e assegnarne una nuova.</span><span class="sxs-lookup"><span data-stu-id="742ac-120">Depending on your needs, you can assign an existing Azure Active Directory service principal to a registry or create and assign a new one.</span></span> <span data-ttu-id="742ac-121">In alternativa è possibile abilitare l'account di utente amministratore del registro.</span><span class="sxs-lookup"><span data-stu-id="742ac-121">Alternatively, you can enable the registry's admin user account.</span></span> <span data-ttu-id="742ac-122">Vedere le sezioni più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="742ac-122">See the sections later in this article.</span></span> <span data-ttu-id="742ac-123">Per altre informazioni sull'accesso al registro, vedere [Authenticate with the container registry](container-registry-authentication.md) (Eseguire l'autenticazione al registro di contenitori).</span><span class="sxs-lookup"><span data-stu-id="742ac-123">For more information about registry access, see [Authenticate with the container registry](container-registry-authentication.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="742ac-124">Creare un registro di contenitori</span><span class="sxs-lookup"><span data-stu-id="742ac-124">Create a container registry</span></span>
<span data-ttu-id="742ac-125">Eseguire il comando `New-AzureRMContainerRegistry` per creare un registro di contenitori.</span><span class="sxs-lookup"><span data-stu-id="742ac-125">Run the `New-AzureRMContainerRegistry` command to create a container registry.</span></span>

> [!TIP]
> <span data-ttu-id="742ac-126">Quando si crea un registro, specificare un nome di dominio univoco globale di primo livello, contenente solo lettere e numeri.</span><span class="sxs-lookup"><span data-stu-id="742ac-126">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span> <span data-ttu-id="742ac-127">Il nome del registro negli esempi è `MyRegistry`, ma è necessario sostituirlo con un nome univoco personalizzato.</span><span class="sxs-lookup"><span data-stu-id="742ac-127">The registry name in the examples is `MyRegistry`, but substitute a unique name of your own.</span></span>
>
>

<span data-ttu-id="742ac-128">Il comando seguente usa i parametri minimi per creare il registro di contenitori `MyRegistry` nel gruppo di risorse `MyResourceGroup` nell'area South Central US:</span><span class="sxs-lookup"><span data-stu-id="742ac-128">The following command uses the minimal parameters to create container registry `MyRegistry` in the resource group `MyResourceGroup` in the South Central US location:</span></span>

```PowerShell
$Registry = New-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

* <span data-ttu-id="742ac-129">`-StorageAccountName` è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="742ac-129">`-StorageAccountName` is optional.</span></span> <span data-ttu-id="742ac-130">Se non è specificato, verrà creato un account di archiviazione con un nome costituito dal nome registro e un timestamp nel gruppo di risorse specificato.</span><span class="sxs-lookup"><span data-stu-id="742ac-130">If not specified, a storage account is created with a name consisting of the registry name and a timestamp in the specified resource group.</span></span>

## <a name="assign-a-service-principal"></a><span data-ttu-id="742ac-131">Assegnare un'entità servizio</span><span class="sxs-lookup"><span data-stu-id="742ac-131">Assign a service principal</span></span>
<span data-ttu-id="742ac-132">Usare i comandi di PowerShell per assegnare a un registro un'[entità servizio](../azure-resource-manager/resource-group-authenticate-service-principal.md) Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="742ac-132">Use PowerShell commands to assign an Azure Active Directory [service principal](../azure-resource-manager/resource-group-authenticate-service-principal.md) to a registry.</span></span> <span data-ttu-id="742ac-133">All'entità servizio in questi esempi è assegnato il ruolo di proprietario, ma è possibile assegnare [altri ruoli](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="742ac-133">The service principal in these examples is assigned the Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.</span></span>

### <a name="create-a-service-principal"></a><span data-ttu-id="742ac-134">Creare un'entità servizio</span><span class="sxs-lookup"><span data-stu-id="742ac-134">Create a service principal</span></span>
<span data-ttu-id="742ac-135">Con il comando seguente viene creata una nuova entità servizio.</span><span class="sxs-lookup"><span data-stu-id="742ac-135">In the following command, a new service principal is created.</span></span> <span data-ttu-id="742ac-136">Specificare una password complessa con il parametro `-Password`.</span><span class="sxs-lookup"><span data-stu-id="742ac-136">Specify a strong password with the `-Password` parameter.</span></span>

```PowerShell
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName ApplicationDisplayName -Password "MyPassword"
```

### <a name="assign-a-new-or-existing-service-principal"></a><span data-ttu-id="742ac-137">Assegnare un'entità servizio nuova o esistente</span><span class="sxs-lookup"><span data-stu-id="742ac-137">Assign a new or existing service principal</span></span>
<span data-ttu-id="742ac-138">È possibile assegnare un'entità servizio nuova o esistente a un registro.</span><span class="sxs-lookup"><span data-stu-id="742ac-138">You can assign a new or an existing service principal to a registry.</span></span> <span data-ttu-id="742ac-139">Per assegnare a tale entità il ruolo di proprietario per l'accesso al registro, eseguire un comando simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="742ac-139">To assign it Owner role access to the registry, run a command similar to the following example:</span></span>

```PowerShell
New-AzureRMRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Registry.Id
```

##<a name="sign-in-to-the-registry-with-the-service-principal"></a><span data-ttu-id="742ac-140">Accedere al registro con l'entità servizio</span><span class="sxs-lookup"><span data-stu-id="742ac-140">Sign in to the registry with the service principal</span></span>
<span data-ttu-id="742ac-141">Dopo l'assegnazione dell'entità servizio al registro, è possibile accedere con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="742ac-141">After assigning the service principal to the registry, you can sign in using the following command:</span></span>

```PowerShell
docker login -u $ServicePrincipal.ApplicationId -p myPassword
```

## <a name="manage-admin-credentials"></a><span data-ttu-id="742ac-142">Gestire le credenziali di amministratore</span><span class="sxs-lookup"><span data-stu-id="742ac-142">Manage admin credentials</span></span>
<span data-ttu-id="742ac-143">Per ogni registro di contenitori viene creato automaticamente un account amministratore che è disabilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="742ac-143">An admin account is automatically created for each container registry and is disabled by default.</span></span> <span data-ttu-id="742ac-144">Gli esempi seguenti mostrano i comandi di PowerShell che consentono di gestire le credenziali di amministratore per il registro contenitori.</span><span class="sxs-lookup"><span data-stu-id="742ac-144">The following examples show PowerShell commands to manage the admin credentials for your container registry.</span></span>

### <a name="obtain-admin-user-credentials"></a><span data-ttu-id="742ac-145">Ottenere le credenziali di utente amministratore</span><span class="sxs-lookup"><span data-stu-id="742ac-145">Obtain admin user credentials</span></span>
```PowerShell
Get-AzureRMContainerRegistryCredential -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

### <a name="enable-admin-user-for-an-existing-registry"></a><span data-ttu-id="742ac-146">Abilitare l'utente amministratore per un registro esistente</span><span class="sxs-lookup"><span data-stu-id="742ac-146">Enable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -EnableAdminUser
```

### <a name="disable-admin-user-for-an-existing-registry"></a><span data-ttu-id="742ac-147">Disabilitare l'utente amministratore per un registro esistente</span><span class="sxs-lookup"><span data-stu-id="742ac-147">Disable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -DisableAdminUser
```

## <a name="next-steps"></a><span data-ttu-id="742ac-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="742ac-148">Next steps</span></span>
* [<span data-ttu-id="742ac-149">Effettuare il push della prima immagine tramite l'interfaccia della riga di comando di Docker</span><span class="sxs-lookup"><span data-stu-id="742ac-149">Push your first image using the Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
