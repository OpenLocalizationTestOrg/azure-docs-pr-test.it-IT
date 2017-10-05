---
title: Provider e tipi di risorse di Azure | Microsoft Docs
description: "Descrive i provider di risorse che supportano Gestione risorse, i relativi schemi e le versioni API disponibili, nonché le aree che possono ospitare le risorse."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 3c7a6fe4-371a-40da-9ebe-b574f583305b
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: tomfitz
ms.openlocfilehash: 6a9128f45d4199404019cee594842d59c7f1aaf3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="resource-providers-and-types"></a><span data-ttu-id="238d6-103">Provider e tipi di risorse</span><span class="sxs-lookup"><span data-stu-id="238d6-103">Resource providers and types</span></span>

<span data-ttu-id="238d6-104">Quando si distribuiscono risorse, è spesso necessario recuperare informazioni sui provider e i tipi di risorse.</span><span class="sxs-lookup"><span data-stu-id="238d6-104">When deploying resources, you frequently need to retrieve information about the resource providers and types.</span></span> <span data-ttu-id="238d6-105">Questo articolo illustra come:</span><span class="sxs-lookup"><span data-stu-id="238d6-105">In this article, you learn to:</span></span>

* <span data-ttu-id="238d6-106">Visualizzare tutti i provider di risorse in Azure</span><span class="sxs-lookup"><span data-stu-id="238d6-106">View all resource providers in Azure</span></span>
* <span data-ttu-id="238d6-107">Controllare lo stato di registrazione di un provider di risorse</span><span class="sxs-lookup"><span data-stu-id="238d6-107">Check registration status of a resource provider</span></span>
* <span data-ttu-id="238d6-108">Registrare un provider di risorse</span><span class="sxs-lookup"><span data-stu-id="238d6-108">Register a resource provider</span></span>
* <span data-ttu-id="238d6-109">Visualizzare i tipi di risorse per un provider di risorse</span><span class="sxs-lookup"><span data-stu-id="238d6-109">View resource types for a resource provider</span></span>
* <span data-ttu-id="238d6-110">Visualizzare le località valide per un tipo di risorsa</span><span class="sxs-lookup"><span data-stu-id="238d6-110">View valid locations for a resource type</span></span>
* <span data-ttu-id="238d6-111">Visualizzare le versioni API valide per un tipo di risorsa</span><span class="sxs-lookup"><span data-stu-id="238d6-111">View valid API versions for a resource type</span></span>

<span data-ttu-id="238d6-112">È possibile eseguire questi passaggi tramite il portale, PowerShell o l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="238d6-112">You can perform these steps through the portal, PowerShell, or Azure CLI.</span></span>

## <a name="powershell"></a><span data-ttu-id="238d6-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="238d6-113">PowerShell</span></span>

<span data-ttu-id="238d6-114">Per visualizzare tutti i provider di risorse in Azure e lo stato di registrazione di una sottoscrizione, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="238d6-114">To see all resource providers in Azure, and the registration status for your subscription, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable | Select-Object ProviderNamespace, RegistrationState
```

<span data-ttu-id="238d6-115">Che restituisce risultati simili a:</span><span class="sxs-lookup"><span data-stu-id="238d6-115">Which returns results similar to:</span></span>

```powershell
ProviderNamespace                RegistrationState
-------------------------------- ------------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="238d6-116">La registrazione di un provider di risorse configura la sottoscrizione per l'utilizzo del provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="238d6-116">Registering a resource provider configures your subscription to work with the resource provider.</span></span> <span data-ttu-id="238d6-117">L'ambito per la registrazione è sempre la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="238d6-117">The scope for registration is always the subscription.</span></span> <span data-ttu-id="238d6-118">Per impostazione predefinita, molti provider di risorse vengono registrati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="238d6-118">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="238d6-119">Potrebbe essere tuttavia necessario registrare manualmente alcuni provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="238d6-119">However, you may need to manually register some resource providers.</span></span> <span data-ttu-id="238d6-120">Per registrare un provider di risorse, è necessaria l'autorizzazione per eseguire l'operazione `/register/action` per il provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="238d6-120">To register a resource provider, you must have permission to perform the `/register/action` operation for the resource provider.</span></span> <span data-ttu-id="238d6-121">Questa operazione è inclusa nei ruoli Collaboratore e Proprietario.</span><span class="sxs-lookup"><span data-stu-id="238d6-121">This operation is included in the Contributor and Owner roles.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="238d6-122">Che restituisce risultati simili a:</span><span class="sxs-lookup"><span data-stu-id="238d6-122">Which returns results similar to:</span></span>

```powershell
ProviderNamespace : Microsoft.Batch
RegistrationState : Registering
ResourceTypes     : {batchAccounts, operations, locations, locations/quotas}
Locations         : {West Europe, East US, East US 2, West US...}
```

<span data-ttu-id="238d6-123">Non è possibile annullare la registrazione di un provider di risorse quando nella sottoscrizione sono ancora presenti tipi di risorsa di tale provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="238d6-123">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="238d6-124">Per visualizzare informazioni su un provider di risorse specifico, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="238d6-124">To see information for a particular resource provider, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="238d6-125">Che restituisce risultati simili a:</span><span class="sxs-lookup"><span data-stu-id="238d6-125">Which returns results similar to:</span></span>

```powershell
{ProviderNamespace : Microsoft.Batch
RegistrationState : Registered
ResourceTypes     : {batchAccounts}
Locations         : {West Europe, East US, East US 2, West US...}

...
```

<span data-ttu-id="238d6-126">Per visualizzare i tipi di risorse per un provider di risorse, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="238d6-126">To see the resource types for a resource provider, use:</span></span>

```powershell
(Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes.ResourceTypeName
```

<span data-ttu-id="238d6-127">Che restituisce:</span><span class="sxs-lookup"><span data-stu-id="238d6-127">Which returns:</span></span>

```powershell
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="238d6-128">La versione dell'API corrisponde a una versione delle operazioni API REST che vengono rilasciate dal provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="238d6-128">The API version corresponds to a version of REST API operations that are released by the resource provider.</span></span> <span data-ttu-id="238d6-129">Poiché un provider di risorse abilita nuove funzionalità, rilascia una nuova versione dell'API REST.</span><span class="sxs-lookup"><span data-stu-id="238d6-129">As a resource provider enables new features, it releases a new version of the REST API.</span></span> 

<span data-ttu-id="238d6-130">Per ottenere le versioni dell'API disponibili per un tipo di risorsa, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="238d6-130">To get the available API versions for a resource type, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).ApiVersions
```

<span data-ttu-id="238d6-131">Che restituisce:</span><span class="sxs-lookup"><span data-stu-id="238d6-131">Which returns:</span></span>

```powershell
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="238d6-132">Gestione risorse è supportato in tutte le aree, ma le risorse distribuite potrebbero non essere supportate in tutte le aree.</span><span class="sxs-lookup"><span data-stu-id="238d6-132">Resource Manager is supported in all regions, but the resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="238d6-133">Potrebbero essere anche presenti limitazioni sulla sottoscrizione che impediscono l'uso di alcune aree che supportano la risorsa.</span><span class="sxs-lookup"><span data-stu-id="238d6-133">In addition, there may be limitations on your subscription that prevent you from using some regions that support the resource.</span></span> 

<span data-ttu-id="238d6-134">Per ottenere le località supportate per un tipo di risorsa, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="238d6-134">To get the supported locations for a resource type, use.</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).Locations
```

<span data-ttu-id="238d6-135">Che restituisce:</span><span class="sxs-lookup"><span data-stu-id="238d6-135">Which returns:</span></span>

```powershell
West Europe
East US
East US 2
West US
...
```

## <a name="azure-cli"></a><span data-ttu-id="238d6-136">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="238d6-136">Azure CLI</span></span>
<span data-ttu-id="238d6-137">Per visualizzare tutti i provider di risorse in Azure e lo stato di registrazione di una sottoscrizione, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="238d6-137">To see all resource providers in Azure, and the registration status for your subscription, use:</span></span>

```azurecli
az provider list --query "[].{Provider:namespace, Status:registrationState}" --out table
```

<span data-ttu-id="238d6-138">Che restituisce risultati simili a:</span><span class="sxs-lookup"><span data-stu-id="238d6-138">Which returns results similar to:</span></span>

```azurecli
Provider                         Status
-------------------------------- ----------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="238d6-139">La registrazione di un provider di risorse configura la sottoscrizione per l'utilizzo del provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="238d6-139">Registering a resource provider configures your subscription to work with the resource provider.</span></span> <span data-ttu-id="238d6-140">L'ambito per la registrazione è sempre la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="238d6-140">The scope for registration is always the subscription.</span></span> <span data-ttu-id="238d6-141">Per impostazione predefinita, molti provider di risorse vengono registrati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="238d6-141">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="238d6-142">Potrebbe essere tuttavia necessario registrare manualmente alcuni provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="238d6-142">However, you may need to manually register some resource providers.</span></span> <span data-ttu-id="238d6-143">Per registrare un provider di risorse, è necessaria l'autorizzazione per eseguire l'operazione `/register/action` per il provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="238d6-143">To register a resource provider, you must have permission to perform the `/register/action` operation for the resource provider.</span></span> <span data-ttu-id="238d6-144">Questa operazione è inclusa nei ruoli Collaboratore e Proprietario.</span><span class="sxs-lookup"><span data-stu-id="238d6-144">This operation is included in the Contributor and Owner roles.</span></span>

```azurecli
az provider register --namespace Microsoft.Batch
```

<span data-ttu-id="238d6-145">Che restituisce un messaggio di registrazione in corso.</span><span class="sxs-lookup"><span data-stu-id="238d6-145">Which returns a message that registration is on-going.</span></span>

<span data-ttu-id="238d6-146">Non è possibile annullare la registrazione di un provider di risorse quando nella sottoscrizione sono ancora presenti tipi di risorsa di tale provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="238d6-146">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="238d6-147">Per visualizzare informazioni su un provider di risorse specifico, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="238d6-147">To see information for a particular resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch
```

<span data-ttu-id="238d6-148">Che restituisce risultati simili a:</span><span class="sxs-lookup"><span data-stu-id="238d6-148">Which returns results similar to:</span></span>

```azurecli
{
    "id": "/subscriptions/####-####/providers/Microsoft.Batch",
    "namespace": "Microsoft.Batch",
    "registrationsState": "Registering",
    "resourceTypes:" [
        ...
    ]
}
```

<span data-ttu-id="238d6-149">Per visualizzare i tipi di risorse per un provider di risorse, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="238d6-149">To see the resource types for a resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[*].resourceType" --out table
```

<span data-ttu-id="238d6-150">Che restituisce:</span><span class="sxs-lookup"><span data-stu-id="238d6-150">Which returns:</span></span>

```azurecli
Result
---------------
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="238d6-151">La versione dell'API corrisponde a una versione delle operazioni API REST che vengono rilasciate dal provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="238d6-151">The API version corresponds to a version of REST API operations that are released by the resource provider.</span></span> <span data-ttu-id="238d6-152">Poiché un provider di risorse abilita nuove funzionalità, rilascia una nuova versione dell'API REST.</span><span class="sxs-lookup"><span data-stu-id="238d6-152">As a resource provider enables new features, it releases a new version of the REST API.</span></span> 

<span data-ttu-id="238d6-153">Per ottenere le versioni dell'API disponibili per un tipo di risorsa, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="238d6-153">To get the available API versions for a resource type, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].apiVersions | [0]" --out table
```

<span data-ttu-id="238d6-154">Che restituisce:</span><span class="sxs-lookup"><span data-stu-id="238d6-154">Which returns:</span></span>

```azurecli
Result
---------------
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="238d6-155">Gestione risorse è supportato in tutte le aree, ma le risorse distribuite potrebbero non essere supportate in tutte le aree.</span><span class="sxs-lookup"><span data-stu-id="238d6-155">Resource Manager is supported in all regions, but the resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="238d6-156">Potrebbero essere anche presenti limitazioni sulla sottoscrizione che impediscono l'uso di alcune aree che supportano la risorsa.</span><span class="sxs-lookup"><span data-stu-id="238d6-156">In addition, there may be limitations on your subscription that prevent you from using some regions that support the resource.</span></span> 

<span data-ttu-id="238d6-157">Per ottenere le località supportate per un tipo di risorsa, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="238d6-157">To get the supported locations for a resource type, use.</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].locations | [0]" --out table
```

<span data-ttu-id="238d6-158">Che restituisce:</span><span class="sxs-lookup"><span data-stu-id="238d6-158">Which returns:</span></span>

```azurecli
Result
---------------
West Europe
East US
East US 2
West US
...
```

## <a name="portal"></a><span data-ttu-id="238d6-159">di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="238d6-159">Portal</span></span>

<span data-ttu-id="238d6-160">Per visualizzare tutti i provider di risorse in Azure e lo stato di registrazione di una sottoscrizione, selezionare **Sottoscrizioni**.</span><span class="sxs-lookup"><span data-stu-id="238d6-160">To see all resource providers in Azure, and the registration status for your subscription, select **Subscriptions**.</span></span>

![selezionare sottoscrizioni](./media/resource-manager-supported-services/select-subscriptions.png)

<span data-ttu-id="238d6-162">Scegliere la sottoscrizione da visualizzare.</span><span class="sxs-lookup"><span data-stu-id="238d6-162">Choose the subscription to view.</span></span>

![specificare la sottoscrizione](./media/resource-manager-supported-services/subscription.png)

<span data-ttu-id="238d6-164">Selezionare **Provider di risorse** e visualizzare l'elenco dei provider di risorse disponibili.</span><span class="sxs-lookup"><span data-stu-id="238d6-164">Select **Resource providers** and view the list of available resource providers.</span></span>

![visualizzare i provider di risorse](./media/resource-manager-supported-services/show-resource-providers.png)

<span data-ttu-id="238d6-166">La registrazione di un provider di risorse configura la sottoscrizione per l'utilizzo del provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="238d6-166">Registering a resource provider configures your subscription to work with the resource provider.</span></span> <span data-ttu-id="238d6-167">L'ambito per la registrazione è sempre la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="238d6-167">The scope for registration is always the subscription.</span></span> <span data-ttu-id="238d6-168">Per impostazione predefinita, molti provider di risorse vengono registrati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="238d6-168">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="238d6-169">Potrebbe essere tuttavia necessario registrare manualmente alcuni provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="238d6-169">However, you may need to manually register some resource providers.</span></span> <span data-ttu-id="238d6-170">Per registrare un provider di risorse, è necessaria l'autorizzazione per eseguire l'operazione `/register/action` per il provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="238d6-170">To register a resource provider, you must have permission to perform the `/register/action` operation for the resource provider.</span></span> <span data-ttu-id="238d6-171">Questa operazione è inclusa nei ruoli Collaboratore e Proprietario.</span><span class="sxs-lookup"><span data-stu-id="238d6-171">This operation is included in the Contributor and Owner roles.</span></span> <span data-ttu-id="238d6-172">Per registrare un provider di risorse, selezionare **Registra**.</span><span class="sxs-lookup"><span data-stu-id="238d6-172">To register a resource provider, select **Register**.</span></span>

![registrare un provider di risorse](./media/resource-manager-supported-services/register-provider.png)

<span data-ttu-id="238d6-174">Non è possibile annullare la registrazione di un provider di risorse quando nella sottoscrizione sono ancora presenti tipi di risorsa di tale provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="238d6-174">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="238d6-175">Per visualizzare informazioni su un provider di risorse specifico, selezionare **Altri servizi**.</span><span class="sxs-lookup"><span data-stu-id="238d6-175">To see information for a particular resource provider, select **More services**.</span></span>

![selezionare altri servizi](./media/resource-manager-supported-services/more-services.png)

<span data-ttu-id="238d6-177">Cercare **Resource Explorer** e selezionarlo dalle opzioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="238d6-177">Search for **Resource Explorer** and select it from the available options.</span></span>

![selezionare resource explorer](./media/resource-manager-supported-services/select-resource-explorer.png)

<span data-ttu-id="238d6-179">Selezionare **Provider**.</span><span class="sxs-lookup"><span data-stu-id="238d6-179">Select **Providers**.</span></span>

![Selezionare i provider](./media/resource-manager-supported-services/select-providers.png)

<span data-ttu-id="238d6-181">Selezionare il provider di risorse e il tipo di risorsa da visualizzare.</span><span class="sxs-lookup"><span data-stu-id="238d6-181">Select the resource provider and resource type that you want to view.</span></span>

![Selezionare il tipo di risorsa](./media/resource-manager-supported-services/select-resource-type.png)

<span data-ttu-id="238d6-183">Gestione risorse è supportato in tutte le aree, ma le risorse distribuite potrebbero non essere supportate in tutte le aree.</span><span class="sxs-lookup"><span data-stu-id="238d6-183">Resource Manager is supported in all regions, but the resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="238d6-184">Potrebbero essere anche presenti limitazioni sulla sottoscrizione che impediscono l'uso di alcune aree che supportano la risorsa.</span><span class="sxs-lookup"><span data-stu-id="238d6-184">In addition, there may be limitations on your subscription that prevent you from using some regions that support the resource.</span></span> <span data-ttu-id="238d6-185">Resource Explorer visualizza le località valide per il tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="238d6-185">The resource explorer displays valid locations for the resource type.</span></span>

![Visualizzare le località](./media/resource-manager-supported-services/show-locations.png)

<span data-ttu-id="238d6-187">La versione dell'API corrisponde a una versione delle operazioni API REST che vengono rilasciate dal provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="238d6-187">The API version corresponds to a version of REST API operations that are released by the resource provider.</span></span> <span data-ttu-id="238d6-188">Poiché un provider di risorse abilita nuove funzionalità, rilascia una nuova versione dell'API REST.</span><span class="sxs-lookup"><span data-stu-id="238d6-188">As a resource provider enables new features, it releases a new version of the REST API.</span></span> <span data-ttu-id="238d6-189">Resource Explorer visualizza le versioni API valide per il tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="238d6-189">The resource explorer displays valid API versions for the resource type.</span></span>

![Visualizzare le versioni API](./media/resource-manager-supported-services/show-api-versions.png)

## <a name="next-steps"></a><span data-ttu-id="238d6-191">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="238d6-191">Next steps</span></span>
* <span data-ttu-id="238d6-192">Per altre informazioni sulla creazione dei modelli, vedere [Creazione di modelli di Gestione risorse di Azure](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="238d6-192">To learn about creating Resource Manager templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="238d6-193">Per informazioni sulla distribuzione delle risorse, vedere [Distribuire un'applicazione con un modello di Gestione risorse di Azure](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="238d6-193">To learn about deploying resources, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="238d6-194">Per visualizzare le operazioni di un provider di risorse, vedere [Azure REST API](/rest/api/) (API REST di Azure).</span><span class="sxs-lookup"><span data-stu-id="238d6-194">To view the operations for a resource provider, see [Azure REST API](/rest/api/).</span></span>

