---
title: aaaAzure i provider di risorse e i tipi di risorsa | Documenti Microsoft
description: Descrive i provider di risorse hello che supportano Gestione risorse, i relativi schemi e le versioni disponibili di API e le aree di hello in grado di ospitare le risorse di hello.
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
ms.openlocfilehash: 23db1d3808a20166f3b44ec801e1bcc46fbb9bd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="resource-providers-and-types"></a><span data-ttu-id="8307e-103">Provider e tipi di risorse</span><span class="sxs-lookup"><span data-stu-id="8307e-103">Resource providers and types</span></span>

<span data-ttu-id="8307e-104">Durante la distribuzione di risorse, spesso necessario tooretrieve informazioni sui tipi e i provider di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="8307e-104">When deploying resources, you frequently need tooretrieve information about hello resource providers and types.</span></span> <span data-ttu-id="8307e-105">Questo articolo illustra come:</span><span class="sxs-lookup"><span data-stu-id="8307e-105">In this article, you learn to:</span></span>

* <span data-ttu-id="8307e-106">Visualizzare tutti i provider di risorse in Azure</span><span class="sxs-lookup"><span data-stu-id="8307e-106">View all resource providers in Azure</span></span>
* <span data-ttu-id="8307e-107">Controllare lo stato di registrazione di un provider di risorse</span><span class="sxs-lookup"><span data-stu-id="8307e-107">Check registration status of a resource provider</span></span>
* <span data-ttu-id="8307e-108">Registrare un provider di risorse</span><span class="sxs-lookup"><span data-stu-id="8307e-108">Register a resource provider</span></span>
* <span data-ttu-id="8307e-109">Visualizzare i tipi di risorse per un provider di risorse</span><span class="sxs-lookup"><span data-stu-id="8307e-109">View resource types for a resource provider</span></span>
* <span data-ttu-id="8307e-110">Visualizzare le località valide per un tipo di risorsa</span><span class="sxs-lookup"><span data-stu-id="8307e-110">View valid locations for a resource type</span></span>
* <span data-ttu-id="8307e-111">Visualizzare le versioni API valide per un tipo di risorsa</span><span class="sxs-lookup"><span data-stu-id="8307e-111">View valid API versions for a resource type</span></span>

<span data-ttu-id="8307e-112">È possibile eseguire questi passaggi tramite il portale di hello, PowerShell o CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="8307e-112">You can perform these steps through hello portal, PowerShell, or Azure CLI.</span></span>

## <a name="powershell"></a><span data-ttu-id="8307e-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8307e-113">PowerShell</span></span>

<span data-ttu-id="8307e-114">toosee tutti i provider di risorse in Azure e lo stato della registrazione hello per la sottoscrizione, utilizzano:</span><span class="sxs-lookup"><span data-stu-id="8307e-114">toosee all resource providers in Azure, and hello registration status for your subscription, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable | Select-Object ProviderNamespace, RegistrationState
```

<span data-ttu-id="8307e-115">Che restituisce risultati simili a:</span><span class="sxs-lookup"><span data-stu-id="8307e-115">Which returns results similar to:</span></span>

```powershell
ProviderNamespace                RegistrationState
-------------------------------- ------------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="8307e-116">Registrazione di un provider di risorse Configura toowork l'abbonamento con provider di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="8307e-116">Registering a resource provider configures your subscription toowork with hello resource provider.</span></span> <span data-ttu-id="8307e-117">ambito Hello per la registrazione è sempre sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="8307e-117">hello scope for registration is always hello subscription.</span></span> <span data-ttu-id="8307e-118">Per impostazione predefinita, molti provider di risorse vengono registrati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8307e-118">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="8307e-119">Tuttavia, potrebbe essere necessario toomanually registrare alcuni provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="8307e-119">However, you may need toomanually register some resource providers.</span></span> <span data-ttu-id="8307e-120">tooregister un provider di risorse, è necessario disporre di hello tooperform autorizzazione `/register/action` operazione hello provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="8307e-120">tooregister a resource provider, you must have permission tooperform hello `/register/action` operation for hello resource provider.</span></span> <span data-ttu-id="8307e-121">Questa operazione è incluso nei ruoli di proprietario e collaboratore hello.</span><span class="sxs-lookup"><span data-stu-id="8307e-121">This operation is included in hello Contributor and Owner roles.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="8307e-122">Che restituisce risultati simili a:</span><span class="sxs-lookup"><span data-stu-id="8307e-122">Which returns results similar to:</span></span>

```powershell
ProviderNamespace : Microsoft.Batch
RegistrationState : Registering
ResourceTypes     : {batchAccounts, operations, locations, locations/quotas}
Locations         : {West Europe, East US, East US 2, West US...}
```

<span data-ttu-id="8307e-123">Non è possibile annullare la registrazione di un provider di risorse quando nella sottoscrizione sono ancora presenti tipi di risorsa di tale provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="8307e-123">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="8307e-124">toosee informazioni per un provider di risorse specifico, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="8307e-124">toosee information for a particular resource provider, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="8307e-125">Che restituisce risultati simili a:</span><span class="sxs-lookup"><span data-stu-id="8307e-125">Which returns results similar to:</span></span>

```powershell
{ProviderNamespace : Microsoft.Batch
RegistrationState : Registered
ResourceTypes     : {batchAccounts}
Locations         : {West Europe, East US, East US 2, West US...}

...
```

<span data-ttu-id="8307e-126">tipi di risorsa hello toosee per un provider di risorse, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="8307e-126">toosee hello resource types for a resource provider, use:</span></span>

```powershell
(Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes.ResourceTypeName
```

<span data-ttu-id="8307e-127">Che restituisce:</span><span class="sxs-lookup"><span data-stu-id="8307e-127">Which returns:</span></span>

```powershell
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="8307e-128">versione dell'API Hello corrisponde versione tooa di operazioni dell'API REST che vengono rilasciati dal provider di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="8307e-128">hello API version corresponds tooa version of REST API operations that are released by hello resource provider.</span></span> <span data-ttu-id="8307e-129">Un provider di risorse consente una nuova funzionalità, viene rilasciata una nuova versione di hello API REST.</span><span class="sxs-lookup"><span data-stu-id="8307e-129">As a resource provider enables new features, it releases a new version of hello REST API.</span></span> 

<span data-ttu-id="8307e-130">tooget hello API le versioni disponibili per un tipo di risorsa, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="8307e-130">tooget hello available API versions for a resource type, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).ApiVersions
```

<span data-ttu-id="8307e-131">Che restituisce:</span><span class="sxs-lookup"><span data-stu-id="8307e-131">Which returns:</span></span>

```powershell
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="8307e-132">Gestione risorse è supportata in tutte le aree, ma le risorse di hello che distribuire potrebbero non essere supportate in tutte le aree.</span><span class="sxs-lookup"><span data-stu-id="8307e-132">Resource Manager is supported in all regions, but hello resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="8307e-133">Inoltre, potrebbe essere limitazioni per la sottoscrizione di impediscano l'utilizzo di alcune aree che supportano la risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="8307e-133">In addition, there may be limitations on your subscription that prevent you from using some regions that support hello resource.</span></span> 

<span data-ttu-id="8307e-134">percorsi di tooget hello è supportato per un tipo di risorsa, utilizzare.</span><span class="sxs-lookup"><span data-stu-id="8307e-134">tooget hello supported locations for a resource type, use.</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).Locations
```

<span data-ttu-id="8307e-135">Che restituisce:</span><span class="sxs-lookup"><span data-stu-id="8307e-135">Which returns:</span></span>

```powershell
West Europe
East US
East US 2
West US
...
```

## <a name="azure-cli"></a><span data-ttu-id="8307e-136">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="8307e-136">Azure CLI</span></span>
<span data-ttu-id="8307e-137">toosee tutti i provider di risorse in Azure e lo stato della registrazione hello per la sottoscrizione, utilizzano:</span><span class="sxs-lookup"><span data-stu-id="8307e-137">toosee all resource providers in Azure, and hello registration status for your subscription, use:</span></span>

```azurecli
az provider list --query "[].{Provider:namespace, Status:registrationState}" --out table
```

<span data-ttu-id="8307e-138">Che restituisce risultati simili a:</span><span class="sxs-lookup"><span data-stu-id="8307e-138">Which returns results similar to:</span></span>

```azurecli
Provider                         Status
-------------------------------- ----------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="8307e-139">Registrazione di un provider di risorse Configura toowork l'abbonamento con provider di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="8307e-139">Registering a resource provider configures your subscription toowork with hello resource provider.</span></span> <span data-ttu-id="8307e-140">ambito Hello per la registrazione è sempre sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="8307e-140">hello scope for registration is always hello subscription.</span></span> <span data-ttu-id="8307e-141">Per impostazione predefinita, molti provider di risorse vengono registrati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8307e-141">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="8307e-142">Tuttavia, potrebbe essere necessario toomanually registrare alcuni provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="8307e-142">However, you may need toomanually register some resource providers.</span></span> <span data-ttu-id="8307e-143">tooregister un provider di risorse, è necessario disporre di hello tooperform autorizzazione `/register/action` operazione hello provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="8307e-143">tooregister a resource provider, you must have permission tooperform hello `/register/action` operation for hello resource provider.</span></span> <span data-ttu-id="8307e-144">Questa operazione è incluso nei ruoli di proprietario e collaboratore hello.</span><span class="sxs-lookup"><span data-stu-id="8307e-144">This operation is included in hello Contributor and Owner roles.</span></span>

```azurecli
az provider register --namespace Microsoft.Batch
```

<span data-ttu-id="8307e-145">Che restituisce un messaggio di registrazione in corso.</span><span class="sxs-lookup"><span data-stu-id="8307e-145">Which returns a message that registration is on-going.</span></span>

<span data-ttu-id="8307e-146">Non è possibile annullare la registrazione di un provider di risorse quando nella sottoscrizione sono ancora presenti tipi di risorsa di tale provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="8307e-146">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="8307e-147">toosee informazioni per un provider di risorse specifico, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="8307e-147">toosee information for a particular resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch
```

<span data-ttu-id="8307e-148">Che restituisce risultati simili a:</span><span class="sxs-lookup"><span data-stu-id="8307e-148">Which returns results similar to:</span></span>

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

<span data-ttu-id="8307e-149">tipi di risorsa hello toosee per un provider di risorse, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="8307e-149">toosee hello resource types for a resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[*].resourceType" --out table
```

<span data-ttu-id="8307e-150">Che restituisce:</span><span class="sxs-lookup"><span data-stu-id="8307e-150">Which returns:</span></span>

```azurecli
Result
---------------
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="8307e-151">versione dell'API Hello corrisponde versione tooa di operazioni dell'API REST che vengono rilasciati dal provider di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="8307e-151">hello API version corresponds tooa version of REST API operations that are released by hello resource provider.</span></span> <span data-ttu-id="8307e-152">Un provider di risorse consente una nuova funzionalità, viene rilasciata una nuova versione di hello API REST.</span><span class="sxs-lookup"><span data-stu-id="8307e-152">As a resource provider enables new features, it releases a new version of hello REST API.</span></span> 

<span data-ttu-id="8307e-153">tooget hello API le versioni disponibili per un tipo di risorsa, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="8307e-153">tooget hello available API versions for a resource type, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].apiVersions | [0]" --out table
```

<span data-ttu-id="8307e-154">Che restituisce:</span><span class="sxs-lookup"><span data-stu-id="8307e-154">Which returns:</span></span>

```azurecli
Result
---------------
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="8307e-155">Gestione risorse è supportata in tutte le aree, ma le risorse di hello che distribuire potrebbero non essere supportate in tutte le aree.</span><span class="sxs-lookup"><span data-stu-id="8307e-155">Resource Manager is supported in all regions, but hello resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="8307e-156">Inoltre, potrebbe essere limitazioni per la sottoscrizione di impediscano l'utilizzo di alcune aree che supportano la risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="8307e-156">In addition, there may be limitations on your subscription that prevent you from using some regions that support hello resource.</span></span> 

<span data-ttu-id="8307e-157">percorsi di tooget hello è supportato per un tipo di risorsa, utilizzare.</span><span class="sxs-lookup"><span data-stu-id="8307e-157">tooget hello supported locations for a resource type, use.</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].locations | [0]" --out table
```

<span data-ttu-id="8307e-158">Che restituisce:</span><span class="sxs-lookup"><span data-stu-id="8307e-158">Which returns:</span></span>

```azurecli
Result
---------------
West Europe
East US
East US 2
West US
...
```

## <a name="portal"></a><span data-ttu-id="8307e-159">di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="8307e-159">Portal</span></span>

<span data-ttu-id="8307e-160">Selezionare tutti i provider di risorse in Azure e per la sottoscrizione, lo stato della registrazione hello toosee **sottoscrizioni**.</span><span class="sxs-lookup"><span data-stu-id="8307e-160">toosee all resource providers in Azure, and hello registration status for your subscription, select **Subscriptions**.</span></span>

![selezionare sottoscrizioni](./media/resource-manager-supported-services/select-subscriptions.png)

<span data-ttu-id="8307e-162">Scegliere tooview sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="8307e-162">Choose hello subscription tooview.</span></span>

![specificare la sottoscrizione](./media/resource-manager-supported-services/subscription.png)

<span data-ttu-id="8307e-164">Selezionare **i provider di risorse** e visualizzare l'elenco hello dei provider di risorse disponibili.</span><span class="sxs-lookup"><span data-stu-id="8307e-164">Select **Resource providers** and view hello list of available resource providers.</span></span>

![visualizzare i provider di risorse](./media/resource-manager-supported-services/show-resource-providers.png)

<span data-ttu-id="8307e-166">Registrazione di un provider di risorse Configura toowork l'abbonamento con provider di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="8307e-166">Registering a resource provider configures your subscription toowork with hello resource provider.</span></span> <span data-ttu-id="8307e-167">ambito Hello per la registrazione è sempre sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="8307e-167">hello scope for registration is always hello subscription.</span></span> <span data-ttu-id="8307e-168">Per impostazione predefinita, molti provider di risorse vengono registrati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8307e-168">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="8307e-169">Tuttavia, potrebbe essere necessario toomanually registrare alcuni provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="8307e-169">However, you may need toomanually register some resource providers.</span></span> <span data-ttu-id="8307e-170">tooregister un provider di risorse, è necessario disporre di hello tooperform autorizzazione `/register/action` operazione hello provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="8307e-170">tooregister a resource provider, you must have permission tooperform hello `/register/action` operation for hello resource provider.</span></span> <span data-ttu-id="8307e-171">Questa operazione è incluso nei ruoli di proprietario e collaboratore hello.</span><span class="sxs-lookup"><span data-stu-id="8307e-171">This operation is included in hello Contributor and Owner roles.</span></span> <span data-ttu-id="8307e-172">Selezionare un provider di risorse, tooregister **registrare**.</span><span class="sxs-lookup"><span data-stu-id="8307e-172">tooregister a resource provider, select **Register**.</span></span>

![registrare un provider di risorse](./media/resource-manager-supported-services/register-provider.png)

<span data-ttu-id="8307e-174">Non è possibile annullare la registrazione di un provider di risorse quando nella sottoscrizione sono ancora presenti tipi di risorsa di tale provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="8307e-174">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="8307e-175">toosee informazioni per un provider di risorse specifico, selezionare **più servizi**.</span><span class="sxs-lookup"><span data-stu-id="8307e-175">toosee information for a particular resource provider, select **More services**.</span></span>

![selezionare altri servizi](./media/resource-manager-supported-services/more-services.png)

<span data-ttu-id="8307e-177">Cercare **Esplora inventario risorse** e selezionare le opzioni disponibili hello.</span><span class="sxs-lookup"><span data-stu-id="8307e-177">Search for **Resource Explorer** and select it from hello available options.</span></span>

![selezionare resource explorer](./media/resource-manager-supported-services/select-resource-explorer.png)

<span data-ttu-id="8307e-179">Selezionare **Provider**.</span><span class="sxs-lookup"><span data-stu-id="8307e-179">Select **Providers**.</span></span>

![Selezionare i provider](./media/resource-manager-supported-services/select-providers.png)

<span data-ttu-id="8307e-181">Tipo di risorsa e il provider di risorse hello selezionare da tooview.</span><span class="sxs-lookup"><span data-stu-id="8307e-181">Select hello resource provider and resource type that you want tooview.</span></span>

![Selezionare il tipo di risorsa](./media/resource-manager-supported-services/select-resource-type.png)

<span data-ttu-id="8307e-183">Gestione risorse è supportata in tutte le aree, ma le risorse di hello che distribuire potrebbero non essere supportate in tutte le aree.</span><span class="sxs-lookup"><span data-stu-id="8307e-183">Resource Manager is supported in all regions, but hello resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="8307e-184">Inoltre, potrebbe essere limitazioni per la sottoscrizione di impediscano l'utilizzo di alcune aree che supportano la risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="8307e-184">In addition, there may be limitations on your subscription that prevent you from using some regions that support hello resource.</span></span> <span data-ttu-id="8307e-185">Esplora inventario risorse Hello consente di visualizzare le posizioni valide per il tipo di risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="8307e-185">hello resource explorer displays valid locations for hello resource type.</span></span>

![Visualizzare le località](./media/resource-manager-supported-services/show-locations.png)

<span data-ttu-id="8307e-187">versione dell'API Hello corrisponde versione tooa di operazioni dell'API REST che vengono rilasciati dal provider di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="8307e-187">hello API version corresponds tooa version of REST API operations that are released by hello resource provider.</span></span> <span data-ttu-id="8307e-188">Un provider di risorse consente una nuova funzionalità, viene rilasciata una nuova versione di hello API REST.</span><span class="sxs-lookup"><span data-stu-id="8307e-188">As a resource provider enables new features, it releases a new version of hello REST API.</span></span> <span data-ttu-id="8307e-189">Esplora inventario risorse Hello Visualizza versioni API valide per il tipo di risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="8307e-189">hello resource explorer displays valid API versions for hello resource type.</span></span>

![Visualizzare le versioni API](./media/resource-manager-supported-services/show-api-versions.png)

## <a name="next-steps"></a><span data-ttu-id="8307e-191">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8307e-191">Next steps</span></span>
* <span data-ttu-id="8307e-192">toolearn sulla creazione di modelli di gestione delle risorse, vedere [modelli Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="8307e-192">toolearn about creating Resource Manager templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="8307e-193">toolearn sulla distribuzione di risorse, vedere [distribuire un'applicazione con il modello di gestione risorse di Azure](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="8307e-193">toolearn about deploying resources, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="8307e-194">operazioni di hello tooview per un provider di risorse, vedere [API REST di Azure](/rest/api/).</span><span class="sxs-lookup"><span data-stu-id="8307e-194">tooview hello operations for a resource provider, see [Azure REST API](/rest/api/).</span></span>

