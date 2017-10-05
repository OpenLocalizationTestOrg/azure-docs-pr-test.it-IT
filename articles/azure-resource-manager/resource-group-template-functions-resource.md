---
title: Funzioni del modello di Azure Resource Manager | Documentazione Microsoft
description: Informazioni sulle funzioni da usare in un modello di Azure Resource Manager per recuperare i valori relativi alle risorse.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/09/2017
ms.author: tomfitz
ms.openlocfilehash: 494ade55f21c19d9c68d5cc52756528401d9bb77
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="resource-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="e9a18-103">Funzioni delle risorse per i modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e9a18-103">Resource functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="e9a18-104">Gestione risorse fornisce le funzioni seguenti per ottenere i valori delle risorse:</span><span class="sxs-lookup"><span data-stu-id="e9a18-104">Resource Manager provides the following functions for getting resource values:</span></span>

* [<span data-ttu-id="e9a18-105">listKeys e list{Value}</span><span class="sxs-lookup"><span data-stu-id="e9a18-105">listKeys and list{Value}</span></span>](#listkeys)
* [<span data-ttu-id="e9a18-106">provider</span><span class="sxs-lookup"><span data-stu-id="e9a18-106">providers</span></span>](#providers)
* [<span data-ttu-id="e9a18-107">reference</span><span class="sxs-lookup"><span data-stu-id="e9a18-107">reference</span></span>](#reference)
* [<span data-ttu-id="e9a18-108">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="e9a18-108">resourceGroup</span></span>](#resourcegroup)
* [<span data-ttu-id="e9a18-109">resourceId</span><span class="sxs-lookup"><span data-stu-id="e9a18-109">resourceId</span></span>](#resourceid)
* [<span data-ttu-id="e9a18-110">sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="e9a18-110">subscription</span></span>](#subscription)

<span data-ttu-id="e9a18-111">Per ottenere valori dai parametri, dalle variabili o dalla distribuzione corrente, vedere [Funzioni dei valori della distribuzione](resource-group-template-functions-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="e9a18-111">To get values from parameters, variables, or the current deployment, see [Deployment value functions](resource-group-template-functions-deployment.md).</span></span>

<a id="listkeys" />
<a id="list" />

## <a name="listkeys-and-listvalue"></a><span data-ttu-id="e9a18-112">listKeys e list{Value}</span><span class="sxs-lookup"><span data-stu-id="e9a18-112">listKeys and list{Value}</span></span>
`listKeys(resourceName or resourceIdentifier, apiVersion)`

`list{Value}(resourceName or resourceIdentifier, apiVersion)`

<span data-ttu-id="e9a18-113">Restituisce i valori per qualsiasi tipo di risorsa che supporta l'operazione di tipo elenco.</span><span class="sxs-lookup"><span data-stu-id="e9a18-113">Returns the values for any resource type that supports the list operation.</span></span> <span data-ttu-id="e9a18-114">L'uso più comune è rappresentato da `listKeys`.</span><span class="sxs-lookup"><span data-stu-id="e9a18-114">The most common usage is `listKeys`.</span></span> 

### <a name="parameters"></a><span data-ttu-id="e9a18-115">Parametri</span><span class="sxs-lookup"><span data-stu-id="e9a18-115">Parameters</span></span>

| <span data-ttu-id="e9a18-116">Parametro</span><span class="sxs-lookup"><span data-stu-id="e9a18-116">Parameter</span></span> | <span data-ttu-id="e9a18-117">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="e9a18-117">Required</span></span> | <span data-ttu-id="e9a18-118">Tipo</span><span class="sxs-lookup"><span data-stu-id="e9a18-118">Type</span></span> | <span data-ttu-id="e9a18-119">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e9a18-119">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e9a18-120">resourceName o resourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="e9a18-120">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="e9a18-121">Sì</span><span class="sxs-lookup"><span data-stu-id="e9a18-121">Yes</span></span> |<span data-ttu-id="e9a18-122">string</span><span class="sxs-lookup"><span data-stu-id="e9a18-122">string</span></span> |<span data-ttu-id="e9a18-123">Identificatore univoco della risorsa.</span><span class="sxs-lookup"><span data-stu-id="e9a18-123">Unique identifier for the resource.</span></span> |
| <span data-ttu-id="e9a18-124">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9a18-124">apiVersion</span></span> |<span data-ttu-id="e9a18-125">Sì</span><span class="sxs-lookup"><span data-stu-id="e9a18-125">Yes</span></span> |<span data-ttu-id="e9a18-126">string</span><span class="sxs-lookup"><span data-stu-id="e9a18-126">string</span></span> |<span data-ttu-id="e9a18-127">Versione dell'API dello stato di runtime della risorsa.</span><span class="sxs-lookup"><span data-stu-id="e9a18-127">API version of resource runtime state.</span></span> <span data-ttu-id="e9a18-128">In genere il formato è **aaaa-mm-gg**.</span><span class="sxs-lookup"><span data-stu-id="e9a18-128">Typically, in the format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="e9a18-129">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="e9a18-129">Return value</span></span>

<span data-ttu-id="e9a18-130">L'oggetto restituito da listKeys è nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="e9a18-130">The returned object from listKeys has the following format:</span></span>

```json
{
  "keys": [
    {
      "keyName": "key1",
      "permissions": "Full",
      "value": "{value}"
    },
    {
      "keyName": "key2",
      "permissions": "Full",
      "value": "{value}"
    }
  ]
}
```

<span data-ttu-id="e9a18-131">Altre funzioni list possono avere formati di restituzione diversi.</span><span class="sxs-lookup"><span data-stu-id="e9a18-131">Other list functions have different return formats.</span></span> <span data-ttu-id="e9a18-132">Per visualizzare il formato di una funzione, includerlo nella sezione outputs, come mostrato nel modello di esempio.</span><span class="sxs-lookup"><span data-stu-id="e9a18-132">To see the format of a function, include it in the outputs section as shown in the example template.</span></span> 

### <a name="remarks"></a><span data-ttu-id="e9a18-133">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="e9a18-133">Remarks</span></span>

<span data-ttu-id="e9a18-134">Qualsiasi operazione che inizia con **list** può essere usata come funzione nel modello.</span><span class="sxs-lookup"><span data-stu-id="e9a18-134">Any operation that starts with **list** can be used as a function in your template.</span></span> <span data-ttu-id="e9a18-135">Le operazioni disponibili non includono solo listKeys, ma anche operazioni come `list`, `listAdminKeys` e `listStatus`.</span><span class="sxs-lookup"><span data-stu-id="e9a18-135">The available operations include not only listKeys, but also operations like `list`, `listAdminKeys`, and `listStatus`.</span></span> <span data-ttu-id="e9a18-136">Non è tuttavia possibile usare operazioni **list** che richiedono valori nel corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="e9a18-136">However, you cannot use **list** operations that require values in the request body.</span></span> <span data-ttu-id="e9a18-137">L'operazione [List Account SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS), ad esempio, richiede parametri del corpo della richiesta come *signedExpiry*, quindi non è possibile usarla in un modello.</span><span class="sxs-lookup"><span data-stu-id="e9a18-137">For example, the [List Account SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operation requires request body parameters like *signedExpiry*, so you cannot use it within a template.</span></span>

<span data-ttu-id="e9a18-138">Per determinare quali tipi di risorse dispongono di un'operazione list, usare le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="e9a18-138">To determine which resource types have a list operation, you have the following options:</span></span>

* <span data-ttu-id="e9a18-139">Visualizzare le [operazioni dell'API REST](/rest/api/) di un provider di risorse e individuare le operazioni list.</span><span class="sxs-lookup"><span data-stu-id="e9a18-139">View the [REST API operations](/rest/api/) for a resource provider, and look for list operations.</span></span> <span data-ttu-id="e9a18-140">Gli account di archiviazione, ad esempio, dispongono dell'[operazione listKeys](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span><span class="sxs-lookup"><span data-stu-id="e9a18-140">For example, storage accounts have the [listKeys operation](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span></span>
* <span data-ttu-id="e9a18-141">Usare il cmdlet di PowerShell [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation).</span><span class="sxs-lookup"><span data-stu-id="e9a18-141">Use the [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) PowerShell cmdlet.</span></span> <span data-ttu-id="e9a18-142">L'esempio seguente ottiene tutte le operazioni list degli account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="e9a18-142">The following example gets all list operations for storage accounts:</span></span>

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* <span data-ttu-id="e9a18-143">Usare il comando seguente dell'interfaccia della riga di comando di Azure per filtrare solo le operazioni list:</span><span class="sxs-lookup"><span data-stu-id="e9a18-143">Use the following Azure CLI command to filter only the list operations:</span></span>

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

<span data-ttu-id="e9a18-144">Specificare la risorsa usando la [funzione resourceId](#resourceid) o il formato `{providerNamespace}/{resourceType}/{resourceName}`.</span><span class="sxs-lookup"><span data-stu-id="e9a18-144">Specify the resource by using either the [resourceId function](#resourceid), or the format `{providerNamespace}/{resourceType}/{resourceName}`.</span></span>


### <a name="example"></a><span data-ttu-id="e9a18-145">Esempio</span><span class="sxs-lookup"><span data-stu-id="e9a18-145">Example</span></span>

<span data-ttu-id="e9a18-146">L'esempio seguente mostra come restituire le chiavi primaria e secondaria da un account di archiviazione nella sezione outputs.</span><span class="sxs-lookup"><span data-stu-id="e9a18-146">The following example shows how to return the primary and secondary keys from a storage account in the outputs section.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountId": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "storageKeysOutput": {
            "value": "[listKeys(parameters('storageAccountId'), '2016-01-01')]",
            "type" : "object"
        }
    }
}
``` 

<a id="providers" />

## <a name="providers"></a><span data-ttu-id="e9a18-147">provider</span><span class="sxs-lookup"><span data-stu-id="e9a18-147">providers</span></span>
`providers(providerNamespace, [resourceType])`

<span data-ttu-id="e9a18-148">Restituisce informazioni su un provider di risorse e i relativi tipi di risorse supportati.</span><span class="sxs-lookup"><span data-stu-id="e9a18-148">Returns information about a resource provider and its supported resource types.</span></span> <span data-ttu-id="e9a18-149">Se non si specifica un tipo di risorsa, la funzione restituisce tutti i tipi supportati per il provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="e9a18-149">If you do not provide a resource type, the function returns all the supported types for the resource provider.</span></span>

### <a name="parameters"></a><span data-ttu-id="e9a18-150">Parametri</span><span class="sxs-lookup"><span data-stu-id="e9a18-150">Parameters</span></span>

| <span data-ttu-id="e9a18-151">Parametro</span><span class="sxs-lookup"><span data-stu-id="e9a18-151">Parameter</span></span> | <span data-ttu-id="e9a18-152">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="e9a18-152">Required</span></span> | <span data-ttu-id="e9a18-153">Tipo</span><span class="sxs-lookup"><span data-stu-id="e9a18-153">Type</span></span> | <span data-ttu-id="e9a18-154">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e9a18-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e9a18-155">providerNamespace</span><span class="sxs-lookup"><span data-stu-id="e9a18-155">providerNamespace</span></span> |<span data-ttu-id="e9a18-156">Sì</span><span class="sxs-lookup"><span data-stu-id="e9a18-156">Yes</span></span> |<span data-ttu-id="e9a18-157">string</span><span class="sxs-lookup"><span data-stu-id="e9a18-157">string</span></span> |<span data-ttu-id="e9a18-158">Spazio dei nomi del provider</span><span class="sxs-lookup"><span data-stu-id="e9a18-158">Namespace of the provider</span></span> |
| <span data-ttu-id="e9a18-159">resourceType</span><span class="sxs-lookup"><span data-stu-id="e9a18-159">resourceType</span></span> |<span data-ttu-id="e9a18-160">No</span><span class="sxs-lookup"><span data-stu-id="e9a18-160">No</span></span> |<span data-ttu-id="e9a18-161">string</span><span class="sxs-lookup"><span data-stu-id="e9a18-161">string</span></span> |<span data-ttu-id="e9a18-162">Il tipo di risorsa all'interno dello spazio dei nomi specificato.</span><span class="sxs-lookup"><span data-stu-id="e9a18-162">The type of resource within the specified namespace.</span></span> |

### <a name="return-value"></a><span data-ttu-id="e9a18-163">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="e9a18-163">Return value</span></span>

<span data-ttu-id="e9a18-164">Ogni tipo supportato viene restituito nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="e9a18-164">Each supported type is returned in the following format:</span></span> 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

<span data-ttu-id="e9a18-165">L'ordine della matrice dei valori restituiti non è garantito.</span><span class="sxs-lookup"><span data-stu-id="e9a18-165">Array ordering of the returned values is not guaranteed.</span></span>

### <a name="example"></a><span data-ttu-id="e9a18-166">Esempio</span><span class="sxs-lookup"><span data-stu-id="e9a18-166">Example</span></span>

<span data-ttu-id="e9a18-167">L'esempio seguente mostra come usare la funzione provider:</span><span class="sxs-lookup"><span data-stu-id="e9a18-167">The following example shows how to use the provider function:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "providerOutput": {
            "value": "[providers('Microsoft.Web', 'sites')]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="e9a18-168">L'esempio precedente restituisce un oggetto nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="e9a18-168">The preceding example returns an object in the following format:</span></span>

```json
{
  "resourceType": "sites",
  "locations": [
    "South Central US",
    "North Europe",
    "West Europe",
    "Southeast Asia",
    ...
  ],
  "apiVersions": [
    "2016-08-01",
    "2016-03-01",
    "2015-08-01-preview",
    "2015-08-01",
    ...
  ]
}
```

<a id="reference" />

## <a name="reference"></a><span data-ttu-id="e9a18-169">reference</span><span class="sxs-lookup"><span data-stu-id="e9a18-169">reference</span></span>
`reference(resourceName or resourceIdentifier, [apiVersion])`

<span data-ttu-id="e9a18-170">Restituisce un oggetto che rappresenta lo stato di runtime di una risorsa.</span><span class="sxs-lookup"><span data-stu-id="e9a18-170">Returns an object representing a resource's runtime state.</span></span>

### <a name="parameters"></a><span data-ttu-id="e9a18-171">Parametri</span><span class="sxs-lookup"><span data-stu-id="e9a18-171">Parameters</span></span>

| <span data-ttu-id="e9a18-172">Parametro</span><span class="sxs-lookup"><span data-stu-id="e9a18-172">Parameter</span></span> | <span data-ttu-id="e9a18-173">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="e9a18-173">Required</span></span> | <span data-ttu-id="e9a18-174">Tipo</span><span class="sxs-lookup"><span data-stu-id="e9a18-174">Type</span></span> | <span data-ttu-id="e9a18-175">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e9a18-175">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e9a18-176">resourceName o resourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="e9a18-176">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="e9a18-177">Sì</span><span class="sxs-lookup"><span data-stu-id="e9a18-177">Yes</span></span> |<span data-ttu-id="e9a18-178">string</span><span class="sxs-lookup"><span data-stu-id="e9a18-178">string</span></span> |<span data-ttu-id="e9a18-179">Nome o identificatore univoco di una risorsa.</span><span class="sxs-lookup"><span data-stu-id="e9a18-179">Name or unique identifier of a resource.</span></span> |
| <span data-ttu-id="e9a18-180">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9a18-180">apiVersion</span></span> |<span data-ttu-id="e9a18-181">No</span><span class="sxs-lookup"><span data-stu-id="e9a18-181">No</span></span> |<span data-ttu-id="e9a18-182">string</span><span class="sxs-lookup"><span data-stu-id="e9a18-182">string</span></span> |<span data-ttu-id="e9a18-183">Versione dell'API della risorsa specificata.</span><span class="sxs-lookup"><span data-stu-id="e9a18-183">API version of the specified resource.</span></span> <span data-ttu-id="e9a18-184">Includere questo parametro quando non viene effettuato il provisioning della risorsa nello stesso modello.</span><span class="sxs-lookup"><span data-stu-id="e9a18-184">Include this parameter when the resource is not provisioned within same template.</span></span> <span data-ttu-id="e9a18-185">In genere il formato è **aaaa-mm-gg**.</span><span class="sxs-lookup"><span data-stu-id="e9a18-185">Typically, in the format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="e9a18-186">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="e9a18-186">Return value</span></span>

<span data-ttu-id="e9a18-187">Ogni tipo di risorsa restituisce proprietà diverse per la funzione di riferimento.</span><span class="sxs-lookup"><span data-stu-id="e9a18-187">Every resource type returns different properties for the reference function.</span></span> <span data-ttu-id="e9a18-188">La funzione non restituisce un singolo formato predefinito.</span><span class="sxs-lookup"><span data-stu-id="e9a18-188">The function does not return a single, predefined format.</span></span> <span data-ttu-id="e9a18-189">Per visualizzare le proprietà per un tipo di risorsa, restituire l'oggetto nella sezione output, come illustrato nell'esempio.</span><span class="sxs-lookup"><span data-stu-id="e9a18-189">To see the properties for a resource type, return the object in the outputs section as shown in the example.</span></span>

### <a name="remarks"></a><span data-ttu-id="e9a18-190">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="e9a18-190">Remarks</span></span>

<span data-ttu-id="e9a18-191">La funzione reference deriva il proprio valore da uno stato di runtime, quindi non può essere usata nella sezione variables.</span><span class="sxs-lookup"><span data-stu-id="e9a18-191">The reference function derives its value from a runtime state, and therefore cannot be used in the variables section.</span></span> <span data-ttu-id="e9a18-192">Può essere usata, invece, nella sezione outputs di un modello.</span><span class="sxs-lookup"><span data-stu-id="e9a18-192">It can be used in outputs section of a template.</span></span> 

<span data-ttu-id="e9a18-193">Usando la funzione di riferimento, si dichiara implicitamente che una risorsa dipende da un'altra se il provisioning della risorsa cui si fa riferimento viene effettuato nello stesso modello.</span><span class="sxs-lookup"><span data-stu-id="e9a18-193">By using the reference function, you implicitly declare that one resource depends on another resource if the referenced resource is provisioned within same template.</span></span> <span data-ttu-id="e9a18-194">Non è necessario usare anche la proprietà dependsOn.</span><span class="sxs-lookup"><span data-stu-id="e9a18-194">You do not need to also use the dependsOn property.</span></span> <span data-ttu-id="e9a18-195">La funzione non viene valutata fino a quando la risorsa cui si fa riferimento ha completato la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e9a18-195">The function is not evaluated until the referenced resource has completed deployment.</span></span>

<span data-ttu-id="e9a18-196">Per visualizzare i nomi e i valori delle proprietà per un tipo di risorsa, creare un modello che restituisca l'oggetto nella sezione outputs.</span><span class="sxs-lookup"><span data-stu-id="e9a18-196">To see the property names and values for a resource type, create a template that returns the object in the outputs section.</span></span> <span data-ttu-id="e9a18-197">Se si dispone di una risorsa esistente di quel tipo, il modello restituisce l'oggetto senza distribuire nuove risorse.</span><span class="sxs-lookup"><span data-stu-id="e9a18-197">If you have an existing resource of that type, your template returns the object without deploying any new resources.</span></span> 

<span data-ttu-id="e9a18-198">In genere, la funzione **reference** viene usata per restituire un valore specifico da un oggetto, ad esempio l'URI dell'endpoint BLOB o il nome di dominio completo.</span><span class="sxs-lookup"><span data-stu-id="e9a18-198">Typically, you use the **reference** function to return a particular value from an object, such as the blob endpoint URI or fully qualified domain name.</span></span>

```json
"outputs": {
    "BlobUri": {
        "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01').primaryEndpoints.blob]",
        "type" : "string"
    },
    "FQDN": {
        "value": "[reference(concat('Microsoft.Network/publicIPAddresses/', parameters('ipAddressName')), '2016-03-30').dnsSettings.fqdn]",
        "type" : "string"
    }
}
```

### <a name="example"></a><span data-ttu-id="e9a18-199">Esempio</span><span class="sxs-lookup"><span data-stu-id="e9a18-199">Example</span></span>

<span data-ttu-id="e9a18-200">Per distribuire e far riferimento alla risorsa nello stesso modello, usare:</span><span class="sxs-lookup"><span data-stu-id="e9a18-200">To deploy and reference the resource in the same template, use:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "storageAccountName": { 
          "type": "string"
      }
  },
  "resources": [
    {
      "name": "[parameters('storageAccountName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-12-01",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {
      "referenceOutput": {
          "type": "object",
          "value": "[reference(parameters('storageAccountName'))]"
      }
    }
}
``` 

<span data-ttu-id="e9a18-201">L'esempio precedente restituisce un oggetto nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="e9a18-201">The preceding example returns an object in the following format:</span></span>

```json
{
   "creationTime": "2017-06-13T21:24:46.618364Z",
   "primaryEndpoints": {
     "blob": "https://examplestorage.blob.core.windows.net/",
     "file": "https://examplestorage.file.core.windows.net/",
     "queue": "https://examplestorage.queue.core.windows.net/",
     "table": "https://examplestorage.table.core.windows.net/"
   },
   "primaryLocation": "southcentralus",
   "provisioningState": "Succeeded",
   "statusOfPrimary": "available",
   "supportsHttpsTrafficOnly": false
}
```

<span data-ttu-id="e9a18-202">L'esempio seguente fa riferimento a un account di archiviazione non distribuito in questo modello.</span><span class="sxs-lookup"><span data-stu-id="e9a18-202">The following example references a storage account that is not deployed in this template.</span></span> <span data-ttu-id="e9a18-203">L'account di archiviazione esiste già nello stesso gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="e9a18-203">The storage account already exists within the same resource group.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountName": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "ExistingStorage": {
            "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01')]",
            "type" : "object"
        }
    }
}
```

<a id="resourcegroup" />

## <a name="resourcegroup"></a><span data-ttu-id="e9a18-204">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="e9a18-204">resourceGroup</span></span>
`resourceGroup()`

<span data-ttu-id="e9a18-205">Restituisce un oggetto che rappresenta il gruppo di risorse corrente.</span><span class="sxs-lookup"><span data-stu-id="e9a18-205">Returns an object that represents the current resource group.</span></span> 

### <a name="return-value"></a><span data-ttu-id="e9a18-206">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="e9a18-206">Return value</span></span>

<span data-ttu-id="e9a18-207">L'oggetto restituito è nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="e9a18-207">The returned object is in the following format:</span></span>

```json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}",
  "name": "{resourceGroupName}",
  "location": "{resourceGroupLocation}",
  "tags": {
  },
  "properties": {
    "provisioningState": "{status}"
  }
}
```

### <a name="remarks"></a><span data-ttu-id="e9a18-208">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="e9a18-208">Remarks</span></span>

<span data-ttu-id="e9a18-209">Un utilizzo comune della funzione resourceGroup consiste nel creare risorse nello stesso percorso del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="e9a18-209">A common use of the resourceGroup function is to create resources in the same location as the resource group.</span></span> <span data-ttu-id="e9a18-210">L'esempio seguente usa il percorso del gruppo di risorse per assegnare il percorso per un sito Web.</span><span class="sxs-lookup"><span data-stu-id="e9a18-210">The following example uses the resource group location to assign the location for a web site.</span></span>

```json
"resources": [
   {
      "apiVersion": "2016-08-01",
      "type": "Microsoft.Web/sites",
      "name": "[parameters('siteName')]",
      "location": "[resourceGroup().location]",
      ...
   }
]
```

### <a name="example"></a><span data-ttu-id="e9a18-211">Esempio</span><span class="sxs-lookup"><span data-stu-id="e9a18-211">Example</span></span>

<span data-ttu-id="e9a18-212">Il modello seguente restituisce le proprietà del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="e9a18-212">The following template returns the properties of the resource group.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[resourceGroup()]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="e9a18-213">L'esempio precedente restituisce un oggetto nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="e9a18-213">The preceding example returns an object in the following format:</span></span>

```json
{
  "id": "/subscriptions/{subscription-id}/resourceGroups/examplegroup",
  "name": "examplegroup",
  "location": "southcentralus",
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

<a id="resourceid" />

## <a name="resourceid"></a><span data-ttu-id="e9a18-214">resourceId</span><span class="sxs-lookup"><span data-stu-id="e9a18-214">resourceId</span></span>
`resourceId([subscriptionId], [resourceGroupName], resourceType, resourceName1, [resourceName2]...)`

<span data-ttu-id="e9a18-215">Restituisce l'identificatore univoco di una risorsa.</span><span class="sxs-lookup"><span data-stu-id="e9a18-215">Returns the unique identifier of a resource.</span></span> <span data-ttu-id="e9a18-216">Questa funzione viene usata quando il nome della risorsa è ambiguo o non è stato sottoposto a provisioning all'interno dello stesso modello.</span><span class="sxs-lookup"><span data-stu-id="e9a18-216">You use this function when the resource name is ambiguous or not provisioned within the same template.</span></span> 

### <a name="parameters"></a><span data-ttu-id="e9a18-217">Parametri</span><span class="sxs-lookup"><span data-stu-id="e9a18-217">Parameters</span></span>

| <span data-ttu-id="e9a18-218">Parametro</span><span class="sxs-lookup"><span data-stu-id="e9a18-218">Parameter</span></span> | <span data-ttu-id="e9a18-219">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="e9a18-219">Required</span></span> | <span data-ttu-id="e9a18-220">Tipo</span><span class="sxs-lookup"><span data-stu-id="e9a18-220">Type</span></span> | <span data-ttu-id="e9a18-221">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e9a18-221">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e9a18-222">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="e9a18-222">subscriptionId</span></span> |<span data-ttu-id="e9a18-223">No</span><span class="sxs-lookup"><span data-stu-id="e9a18-223">No</span></span> |<span data-ttu-id="e9a18-224">Stringa (in formato GUID)</span><span class="sxs-lookup"><span data-stu-id="e9a18-224">string (In GUID format)</span></span> |<span data-ttu-id="e9a18-225">Il valore predefinito è la sottoscrizione corrente.</span><span class="sxs-lookup"><span data-stu-id="e9a18-225">Default value is the current subscription.</span></span> <span data-ttu-id="e9a18-226">Specificare questo valore quando si vuole recuperare una risorsa in un'altra sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="e9a18-226">Specify this value when you need to retrieve a resource in another subscription.</span></span> |
| <span data-ttu-id="e9a18-227">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="e9a18-227">resourceGroupName</span></span> |<span data-ttu-id="e9a18-228">No</span><span class="sxs-lookup"><span data-stu-id="e9a18-228">No</span></span> |<span data-ttu-id="e9a18-229">string</span><span class="sxs-lookup"><span data-stu-id="e9a18-229">string</span></span> |<span data-ttu-id="e9a18-230">Il valore predefinito è il gruppo di risorse corrente.</span><span class="sxs-lookup"><span data-stu-id="e9a18-230">Default value is current resource group.</span></span> <span data-ttu-id="e9a18-231">Specificare questo valore quando si vuole recuperare una risorsa in un altro gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="e9a18-231">Specify this value when you need to retrieve a resource in another resource group.</span></span> |
| <span data-ttu-id="e9a18-232">resourceType</span><span class="sxs-lookup"><span data-stu-id="e9a18-232">resourceType</span></span> |<span data-ttu-id="e9a18-233">Sì</span><span class="sxs-lookup"><span data-stu-id="e9a18-233">Yes</span></span> |<span data-ttu-id="e9a18-234">string</span><span class="sxs-lookup"><span data-stu-id="e9a18-234">string</span></span> |<span data-ttu-id="e9a18-235">Tipo di risorsa, incluso lo spazio dei nomi del provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="e9a18-235">Type of resource including resource provider namespace.</span></span> |
| <span data-ttu-id="e9a18-236">resourceName1</span><span class="sxs-lookup"><span data-stu-id="e9a18-236">resourceName1</span></span> |<span data-ttu-id="e9a18-237">Sì</span><span class="sxs-lookup"><span data-stu-id="e9a18-237">Yes</span></span> |<span data-ttu-id="e9a18-238">string</span><span class="sxs-lookup"><span data-stu-id="e9a18-238">string</span></span> |<span data-ttu-id="e9a18-239">Nome della risorsa.</span><span class="sxs-lookup"><span data-stu-id="e9a18-239">Name of resource.</span></span> |
| <span data-ttu-id="e9a18-240">resourceName2</span><span class="sxs-lookup"><span data-stu-id="e9a18-240">resourceName2</span></span> |<span data-ttu-id="e9a18-241">No</span><span class="sxs-lookup"><span data-stu-id="e9a18-241">No</span></span> |<span data-ttu-id="e9a18-242">string</span><span class="sxs-lookup"><span data-stu-id="e9a18-242">string</span></span> |<span data-ttu-id="e9a18-243">Segmento successivo del nome della risorsa se la risorsa è annidata.</span><span class="sxs-lookup"><span data-stu-id="e9a18-243">Next resource name segment if resource is nested.</span></span> |

### <a name="return-value"></a><span data-ttu-id="e9a18-244">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="e9a18-244">Return value</span></span>

<span data-ttu-id="e9a18-245">L'identificatore viene restituito nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="e9a18-245">The identifier is returned in the following format:</span></span>

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### <a name="remarks"></a><span data-ttu-id="e9a18-246">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="e9a18-246">Remarks</span></span>

<span data-ttu-id="e9a18-247">I valori da specificare per i parametri dipendono dall'appartenenza o meno della risorsa alla stessa sottoscrizione e allo stesso gruppo di risorse della distribuzione corrente.</span><span class="sxs-lookup"><span data-stu-id="e9a18-247">The parameter values you specify depend on whether the resource is in the same subscription and resource group as the current deployment.</span></span>

<span data-ttu-id="e9a18-248">Per ottenere l'ID risorsa per un account di archiviazione nella stessa sottoscrizione e nello stesso gruppo di risorse, usare:</span><span class="sxs-lookup"><span data-stu-id="e9a18-248">To get the resource ID for a storage account in the same subscription and resource group, use:</span></span>

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="e9a18-249">Per ottenere l'ID risorsa per un account di archiviazione nella stessa sottoscrizione, ma in un gruppo di risorse differente, usare:</span><span class="sxs-lookup"><span data-stu-id="e9a18-249">To get the resource ID for a storage account in the same subscription but a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="e9a18-250">Per ottenere l'ID risorsa per un account di archiviazione in una sottoscrizione differente, ma nello stesso gruppo di risorse, usare:</span><span class="sxs-lookup"><span data-stu-id="e9a18-250">To get the resource ID for a storage account in a different subscription and resource group, use:</span></span>

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="e9a18-251">Per ottenere l'ID risorsa per un database in un gruppo di risorse differente, usare:</span><span class="sxs-lookup"><span data-stu-id="e9a18-251">To get the resource ID for a database in a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

<span data-ttu-id="e9a18-252">Spesso è necessario usare questa funzione quando si usa un account di archiviazione o una rete virtuale in un gruppo di risorse alternative.</span><span class="sxs-lookup"><span data-stu-id="e9a18-252">Often, you need to use this function when using a storage account or virtual network in an alternate resource group.</span></span> <span data-ttu-id="e9a18-253">L'esempio seguente mostra come usare facilmente una risorsa di un gruppo di risorse esterno:</span><span class="sxs-lookup"><span data-stu-id="e9a18-253">The following example shows how a resource from an external resource group can easily be used:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "virtualNetworkName": {
          "type": "string"
      },
      "virtualNetworkResourceGroup": {
          "type": "string"
      },
      "subnet1Name": {
          "type": "string"
      },
      "nicName": {
          "type": "string"
      }
  },
  "variables": {
      "vnetID": "[resourceId(parameters('virtualNetworkResourceGroup'), 'Microsoft.Network/virtualNetworks', parameters('virtualNetworkName'))]",
      "subnet1Ref": "[concat(variables('vnetID'),'/subnets/', parameters('subnet1Name'))]"
  },
  "resources": [
  {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[parameters('nicName')]",
      "location": "[parameters('location')]",
      "properties": {
          "ipConfigurations": [{
              "name": "ipconfig1",
              "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "subnet": {
                      "id": "[variables('subnet1Ref')]"
                  }
              }
          }]
       }
  }]
}
```

### <a name="example"></a><span data-ttu-id="e9a18-254">Esempio</span><span class="sxs-lookup"><span data-stu-id="e9a18-254">Example</span></span>

<span data-ttu-id="e9a18-255">L'esempio seguente restituisce l'ID della risorsa per un account di archiviazione nel gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="e9a18-255">The following example returns the resource ID for a storage account in the resource group:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "sameRGOutput": {
            "value": "[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentRGOutput": {
            "value": "[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentSubOutput": {
            "value": "[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "nestedResourceOutput": {
            "value": "[resourceId('Microsoft.SQL/servers/databases', 'serverName', 'databaseName')]",
            "type" : "string"
        }
    }
}
```

<span data-ttu-id="e9a18-256">L'output dell'esempio precedente con i valori predefiniti è:</span><span class="sxs-lookup"><span data-stu-id="e9a18-256">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="e9a18-257">Nome</span><span class="sxs-lookup"><span data-stu-id="e9a18-257">Name</span></span> | <span data-ttu-id="e9a18-258">Tipo</span><span class="sxs-lookup"><span data-stu-id="e9a18-258">Type</span></span> | <span data-ttu-id="e9a18-259">Valore</span><span class="sxs-lookup"><span data-stu-id="e9a18-259">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="e9a18-260">sameRGOutput</span><span class="sxs-lookup"><span data-stu-id="e9a18-260">sameRGOutput</span></span> | <span data-ttu-id="e9a18-261">String</span><span class="sxs-lookup"><span data-stu-id="e9a18-261">String</span></span> | <span data-ttu-id="e9a18-262">/subscriptions/{id-sott-corrente}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="e9a18-262">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="e9a18-263">differentRGOutput</span><span class="sxs-lookup"><span data-stu-id="e9a18-263">differentRGOutput</span></span> | <span data-ttu-id="e9a18-264">String</span><span class="sxs-lookup"><span data-stu-id="e9a18-264">String</span></span> | <span data-ttu-id="e9a18-265">/subscriptions/{id-sott-corrente}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="e9a18-265">/subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="e9a18-266">differentSubOutput</span><span class="sxs-lookup"><span data-stu-id="e9a18-266">differentSubOutput</span></span> | <span data-ttu-id="e9a18-267">String</span><span class="sxs-lookup"><span data-stu-id="e9a18-267">String</span></span> | <span data-ttu-id="e9a18-268">/subscriptions/{id-sott-differente}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="e9a18-268">/subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="e9a18-269">nestedResourceOutput</span><span class="sxs-lookup"><span data-stu-id="e9a18-269">nestedResourceOutput</span></span> | <span data-ttu-id="e9a18-270">String</span><span class="sxs-lookup"><span data-stu-id="e9a18-270">String</span></span> | <span data-ttu-id="e9a18-271">/subscriptions/{id-sott-corrente}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span><span class="sxs-lookup"><span data-stu-id="e9a18-271">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span></span> |

<a id="subscription" />

## <a name="subscription"></a><span data-ttu-id="e9a18-272">sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="e9a18-272">subscription</span></span>
`subscription()`

<span data-ttu-id="e9a18-273">Restituisce i dettagli sulla sottoscrizione per la distribuzione corrente.</span><span class="sxs-lookup"><span data-stu-id="e9a18-273">Returns details about the subscription for the current deployment.</span></span> 

### <a name="return-value"></a><span data-ttu-id="e9a18-274">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="e9a18-274">Return value</span></span>

<span data-ttu-id="e9a18-275">La funzione restituisce il formato seguente:</span><span class="sxs-lookup"><span data-stu-id="e9a18-275">The function returns the following format:</span></span>

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### <a name="example"></a><span data-ttu-id="e9a18-276">Esempio</span><span class="sxs-lookup"><span data-stu-id="e9a18-276">Example</span></span>

<span data-ttu-id="e9a18-277">L'esempio seguente mostra la funzione subscription chiamata nella sezione outputs.</span><span class="sxs-lookup"><span data-stu-id="e9a18-277">The following example shows the subscription function called in the outputs section.</span></span> 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[subscription()]",
            "type" : "object"
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="e9a18-278">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e9a18-278">Next steps</span></span>
* <span data-ttu-id="e9a18-279">Per una descrizione delle sezioni in un modello di Azure Resource Manager, vedere [Creazione di modelli di Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="e9a18-279">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="e9a18-280">Per unire più modelli, vedere [Uso di modelli collegati con Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="e9a18-280">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="e9a18-281">Per eseguire un'iterazione di un numero di volte specificato durante la creazione di un tipo di risorsa, vedere [Creare più istanze di risorse in Gestione risorse di Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="e9a18-281">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="e9a18-282">Per informazioni su come distribuire il modello che è stato creato, vedere [Distribuire un'applicazione con un modello di Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="e9a18-282">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

