---
title: funzioni di modello di gestione risorse aaaAzure - risorse | Documenti Microsoft
description: Vengono descritti le risorse toouse funzioni hello un valori tooretrieve modello di gestione risorse di Azure.
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
ms.openlocfilehash: c9d524b338b8b7ea6d8c9e0135d48e4fb8f167c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="resource-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="271fd-103">Funzioni delle risorse per i modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="271fd-103">Resource functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="271fd-104">Gestione risorse offre hello funzioni per ottenere i valori delle risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="271fd-104">Resource Manager provides hello following functions for getting resource values:</span></span>

* [<span data-ttu-id="271fd-105">listKeys e list{Value}</span><span class="sxs-lookup"><span data-stu-id="271fd-105">listKeys and list{Value}</span></span>](#listkeys)
* [<span data-ttu-id="271fd-106">provider</span><span class="sxs-lookup"><span data-stu-id="271fd-106">providers</span></span>](#providers)
* [<span data-ttu-id="271fd-107">reference</span><span class="sxs-lookup"><span data-stu-id="271fd-107">reference</span></span>](#reference)
* [<span data-ttu-id="271fd-108">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="271fd-108">resourceGroup</span></span>](#resourcegroup)
* [<span data-ttu-id="271fd-109">resourceId</span><span class="sxs-lookup"><span data-stu-id="271fd-109">resourceId</span></span>](#resourceid)
* [<span data-ttu-id="271fd-110">sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="271fd-110">subscription</span></span>](#subscription)

<span data-ttu-id="271fd-111">i valori tooget parametri, variabili o la distribuzione corrente di hello, vedere [funzioni con valori di distribuzione](resource-group-template-functions-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="271fd-111">tooget values from parameters, variables, or hello current deployment, see [Deployment value functions](resource-group-template-functions-deployment.md).</span></span>

<a id="listkeys" />
<a id="list" />

## <a name="listkeys-and-listvalue"></a><span data-ttu-id="271fd-112">listKeys e list{Value}</span><span class="sxs-lookup"><span data-stu-id="271fd-112">listKeys and list{Value}</span></span>
`listKeys(resourceName or resourceIdentifier, apiVersion)`

`list{Value}(resourceName or resourceIdentifier, apiVersion)`

<span data-ttu-id="271fd-113">Restituisce hello valori per qualsiasi tipo di risorsa che supporta l'operazione di elenco hello.</span><span class="sxs-lookup"><span data-stu-id="271fd-113">Returns hello values for any resource type that supports hello list operation.</span></span> <span data-ttu-id="271fd-114">utilizzo più comune di Hello è `listKeys`.</span><span class="sxs-lookup"><span data-stu-id="271fd-114">hello most common usage is `listKeys`.</span></span> 

### <a name="parameters"></a><span data-ttu-id="271fd-115">parameters</span><span class="sxs-lookup"><span data-stu-id="271fd-115">Parameters</span></span>

| <span data-ttu-id="271fd-116">Parametro</span><span class="sxs-lookup"><span data-stu-id="271fd-116">Parameter</span></span> | <span data-ttu-id="271fd-117">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="271fd-117">Required</span></span> | <span data-ttu-id="271fd-118">Tipo</span><span class="sxs-lookup"><span data-stu-id="271fd-118">Type</span></span> | <span data-ttu-id="271fd-119">Descrizione</span><span class="sxs-lookup"><span data-stu-id="271fd-119">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="271fd-120">resourceName o resourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="271fd-120">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="271fd-121">Sì</span><span class="sxs-lookup"><span data-stu-id="271fd-121">Yes</span></span> |<span data-ttu-id="271fd-122">string</span><span class="sxs-lookup"><span data-stu-id="271fd-122">string</span></span> |<span data-ttu-id="271fd-123">Identificatore univoco per la risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="271fd-123">Unique identifier for hello resource.</span></span> |
| <span data-ttu-id="271fd-124">apiVersion</span><span class="sxs-lookup"><span data-stu-id="271fd-124">apiVersion</span></span> |<span data-ttu-id="271fd-125">Sì</span><span class="sxs-lookup"><span data-stu-id="271fd-125">Yes</span></span> |<span data-ttu-id="271fd-126">string</span><span class="sxs-lookup"><span data-stu-id="271fd-126">string</span></span> |<span data-ttu-id="271fd-127">Versione dell'API dello stato di runtime della risorsa.</span><span class="sxs-lookup"><span data-stu-id="271fd-127">API version of resource runtime state.</span></span> <span data-ttu-id="271fd-128">In genere, nel formato di hello, **aaaa-mm-gg**.</span><span class="sxs-lookup"><span data-stu-id="271fd-128">Typically, in hello format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="271fd-129">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="271fd-129">Return value</span></span>

<span data-ttu-id="271fd-130">Hello ha restituito l'elenco chiavi dell'oggetto è hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="271fd-130">hello returned object from listKeys has hello following format:</span></span>

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

<span data-ttu-id="271fd-131">Altre funzioni list possono avere formati di restituzione diversi.</span><span class="sxs-lookup"><span data-stu-id="271fd-131">Other list functions have different return formats.</span></span> <span data-ttu-id="271fd-132">formato di hello toosee di una funzione, includerla nella sezione di output di hello come mostrato nel modello di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="271fd-132">toosee hello format of a function, include it in hello outputs section as shown in hello example template.</span></span> 

### <a name="remarks"></a><span data-ttu-id="271fd-133">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="271fd-133">Remarks</span></span>

<span data-ttu-id="271fd-134">Qualsiasi operazione che inizia con **list** può essere usata come funzione nel modello.</span><span class="sxs-lookup"><span data-stu-id="271fd-134">Any operation that starts with **list** can be used as a function in your template.</span></span> <span data-ttu-id="271fd-135">le operazioni disponibili Hello includono non solo elenco chiavi del, ma anche di operazioni quali `list`, `listAdminKeys`, e `listStatus`.</span><span class="sxs-lookup"><span data-stu-id="271fd-135">hello available operations include not only listKeys, but also operations like `list`, `listAdminKeys`, and `listStatus`.</span></span> <span data-ttu-id="271fd-136">Tuttavia, è possibile utilizzare **elenco** le operazioni che richiedono valori hello corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="271fd-136">However, you cannot use **list** operations that require values in hello request body.</span></span> <span data-ttu-id="271fd-137">Ad esempio, hello [elenco Account SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operazione richiede i parametri del corpo della richiesta come *signedExpiry*, pertanto non può essere utilizzato all'interno di un modello.</span><span class="sxs-lookup"><span data-stu-id="271fd-137">For example, hello [List Account SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operation requires request body parameters like *signedExpiry*, so you cannot use it within a template.</span></span>

<span data-ttu-id="271fd-138">toodetermine quali tipi di risorse dispone di un'operazione di elenco, è necessario hello le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="271fd-138">toodetermine which resource types have a list operation, you have hello following options:</span></span>

* <span data-ttu-id="271fd-139">Hello vista [operazioni dell'API REST](/rest/api/) per un provider di risorse e cercare l'elenco delle operazioni.</span><span class="sxs-lookup"><span data-stu-id="271fd-139">View hello [REST API operations](/rest/api/) for a resource provider, and look for list operations.</span></span> <span data-ttu-id="271fd-140">Ad esempio, gli account di archiviazione sono hello [elenco chiavi dell'operazione](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span><span class="sxs-lookup"><span data-stu-id="271fd-140">For example, storage accounts have hello [listKeys operation](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span></span>
* <span data-ttu-id="271fd-141">Hello utilizzare [Get AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="271fd-141">Use hello [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) PowerShell cmdlet.</span></span> <span data-ttu-id="271fd-142">Hello seguente esempio mostra come ottenere tutte le operazioni di elenco per gli account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="271fd-142">hello following example gets all list operations for storage accounts:</span></span>

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* <span data-ttu-id="271fd-143">Utilizzare hello comando CLI di Azure toofilter hello solo l'elenco delle operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="271fd-143">Use hello following Azure CLI command toofilter only hello list operations:</span></span>

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

<span data-ttu-id="271fd-144">Specificare la risorsa hello utilizzando entrambi hello [funzione resourceId](#resourceid), o formato hello `{providerNamespace}/{resourceType}/{resourceName}`.</span><span class="sxs-lookup"><span data-stu-id="271fd-144">Specify hello resource by using either hello [resourceId function](#resourceid), or hello format `{providerNamespace}/{resourceType}/{resourceName}`.</span></span>


### <a name="example"></a><span data-ttu-id="271fd-145">Esempio</span><span class="sxs-lookup"><span data-stu-id="271fd-145">Example</span></span>

<span data-ttu-id="271fd-146">Hello esempio seguente viene illustrato come chiavi tooreturn hello primaria e secondaria da un account di archiviazione in hello restituisce sezione.</span><span class="sxs-lookup"><span data-stu-id="271fd-146">hello following example shows how tooreturn hello primary and secondary keys from a storage account in hello outputs section.</span></span>

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

## <a name="providers"></a><span data-ttu-id="271fd-147">provider</span><span class="sxs-lookup"><span data-stu-id="271fd-147">providers</span></span>
`providers(providerNamespace, [resourceType])`

<span data-ttu-id="271fd-148">Restituisce informazioni su un provider di risorse e i relativi tipi di risorse supportati.</span><span class="sxs-lookup"><span data-stu-id="271fd-148">Returns information about a resource provider and its supported resource types.</span></span> <span data-ttu-id="271fd-149">Se non si specifica un tipo di risorsa, la funzione hello restituisce tutti i tipi di hello è supportato per i provider di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="271fd-149">If you do not provide a resource type, hello function returns all hello supported types for hello resource provider.</span></span>

### <a name="parameters"></a><span data-ttu-id="271fd-150">parameters</span><span class="sxs-lookup"><span data-stu-id="271fd-150">Parameters</span></span>

| <span data-ttu-id="271fd-151">Parametro</span><span class="sxs-lookup"><span data-stu-id="271fd-151">Parameter</span></span> | <span data-ttu-id="271fd-152">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="271fd-152">Required</span></span> | <span data-ttu-id="271fd-153">Tipo</span><span class="sxs-lookup"><span data-stu-id="271fd-153">Type</span></span> | <span data-ttu-id="271fd-154">Descrizione</span><span class="sxs-lookup"><span data-stu-id="271fd-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="271fd-155">providerNamespace</span><span class="sxs-lookup"><span data-stu-id="271fd-155">providerNamespace</span></span> |<span data-ttu-id="271fd-156">Sì</span><span class="sxs-lookup"><span data-stu-id="271fd-156">Yes</span></span> |<span data-ttu-id="271fd-157">string</span><span class="sxs-lookup"><span data-stu-id="271fd-157">string</span></span> |<span data-ttu-id="271fd-158">Namespace del provider di hello</span><span class="sxs-lookup"><span data-stu-id="271fd-158">Namespace of hello provider</span></span> |
| <span data-ttu-id="271fd-159">resourceType</span><span class="sxs-lookup"><span data-stu-id="271fd-159">resourceType</span></span> |<span data-ttu-id="271fd-160">No</span><span class="sxs-lookup"><span data-stu-id="271fd-160">No</span></span> |<span data-ttu-id="271fd-161">string</span><span class="sxs-lookup"><span data-stu-id="271fd-161">string</span></span> |<span data-ttu-id="271fd-162">tipo di Hello della risorsa all'interno di hello specificato dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="271fd-162">hello type of resource within hello specified namespace.</span></span> |

### <a name="return-value"></a><span data-ttu-id="271fd-163">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="271fd-163">Return value</span></span>

<span data-ttu-id="271fd-164">Ogni tipo supportato viene restituito in hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="271fd-164">Each supported type is returned in hello following format:</span></span> 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

<span data-ttu-id="271fd-165">Matrice di ordinamento di hello restituito non è garantito che i valori.</span><span class="sxs-lookup"><span data-stu-id="271fd-165">Array ordering of hello returned values is not guaranteed.</span></span>

### <a name="example"></a><span data-ttu-id="271fd-166">Esempio</span><span class="sxs-lookup"><span data-stu-id="271fd-166">Example</span></span>

<span data-ttu-id="271fd-167">Hello di esempio seguente viene illustrato come toouse hello funzione del provider:</span><span class="sxs-lookup"><span data-stu-id="271fd-167">hello following example shows how toouse hello provider function:</span></span>

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

<span data-ttu-id="271fd-168">Hello esempio precedente restituisce un oggetto hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="271fd-168">hello preceding example returns an object in hello following format:</span></span>

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

## <a name="reference"></a><span data-ttu-id="271fd-169">reference</span><span class="sxs-lookup"><span data-stu-id="271fd-169">reference</span></span>
`reference(resourceName or resourceIdentifier, [apiVersion])`

<span data-ttu-id="271fd-170">Restituisce un oggetto che rappresenta lo stato di runtime di una risorsa.</span><span class="sxs-lookup"><span data-stu-id="271fd-170">Returns an object representing a resource's runtime state.</span></span>

### <a name="parameters"></a><span data-ttu-id="271fd-171">Parametri</span><span class="sxs-lookup"><span data-stu-id="271fd-171">Parameters</span></span>

| <span data-ttu-id="271fd-172">Parametro</span><span class="sxs-lookup"><span data-stu-id="271fd-172">Parameter</span></span> | <span data-ttu-id="271fd-173">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="271fd-173">Required</span></span> | <span data-ttu-id="271fd-174">Tipo</span><span class="sxs-lookup"><span data-stu-id="271fd-174">Type</span></span> | <span data-ttu-id="271fd-175">Descrizione</span><span class="sxs-lookup"><span data-stu-id="271fd-175">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="271fd-176">resourceName o resourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="271fd-176">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="271fd-177">Sì</span><span class="sxs-lookup"><span data-stu-id="271fd-177">Yes</span></span> |<span data-ttu-id="271fd-178">string</span><span class="sxs-lookup"><span data-stu-id="271fd-178">string</span></span> |<span data-ttu-id="271fd-179">Nome o identificatore univoco di una risorsa.</span><span class="sxs-lookup"><span data-stu-id="271fd-179">Name or unique identifier of a resource.</span></span> |
| <span data-ttu-id="271fd-180">apiVersion</span><span class="sxs-lookup"><span data-stu-id="271fd-180">apiVersion</span></span> |<span data-ttu-id="271fd-181">No</span><span class="sxs-lookup"><span data-stu-id="271fd-181">No</span></span> |<span data-ttu-id="271fd-182">string</span><span class="sxs-lookup"><span data-stu-id="271fd-182">string</span></span> |<span data-ttu-id="271fd-183">Versione dell'API di hello risorsa specificata.</span><span class="sxs-lookup"><span data-stu-id="271fd-183">API version of hello specified resource.</span></span> <span data-ttu-id="271fd-184">Includere questo parametro quando la risorsa hello non è disponibile nel modello stesso.</span><span class="sxs-lookup"><span data-stu-id="271fd-184">Include this parameter when hello resource is not provisioned within same template.</span></span> <span data-ttu-id="271fd-185">In genere, nel formato di hello, **aaaa-mm-gg**.</span><span class="sxs-lookup"><span data-stu-id="271fd-185">Typically, in hello format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="271fd-186">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="271fd-186">Return value</span></span>

<span data-ttu-id="271fd-187">Ogni tipo di risorsa restituisce proprietà diverse per la funzione di riferimento hello.</span><span class="sxs-lookup"><span data-stu-id="271fd-187">Every resource type returns different properties for hello reference function.</span></span> <span data-ttu-id="271fd-188">funzione Hello non restituisce un singolo formato predefinito.</span><span class="sxs-lookup"><span data-stu-id="271fd-188">hello function does not return a single, predefined format.</span></span> <span data-ttu-id="271fd-189">toosee hello per un tipo di risorsa, restituiscono oggetto hello in hello restituisce sezione come illustrato nell'esempio hello.</span><span class="sxs-lookup"><span data-stu-id="271fd-189">toosee hello properties for a resource type, return hello object in hello outputs section as shown in hello example.</span></span>

### <a name="remarks"></a><span data-ttu-id="271fd-190">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="271fd-190">Remarks</span></span>

<span data-ttu-id="271fd-191">funzione riferimento Hello deriva il relativo valore da uno stato di runtime e non può essere utilizzato nella sezione variabili hello.</span><span class="sxs-lookup"><span data-stu-id="271fd-191">hello reference function derives its value from a runtime state, and therefore cannot be used in hello variables section.</span></span> <span data-ttu-id="271fd-192">Può essere usata, invece, nella sezione outputs di un modello.</span><span class="sxs-lookup"><span data-stu-id="271fd-192">It can be used in outputs section of a template.</span></span> 

<span data-ttu-id="271fd-193">Utilizzando hello reference (funzione), in modo implicito dichiarare che una risorsa dipende un'altra risorsa se viene eseguito il provisioning di risorse a cui fa riferimento hello nel modello stesso.</span><span class="sxs-lookup"><span data-stu-id="271fd-193">By using hello reference function, you implicitly declare that one resource depends on another resource if hello referenced resource is provisioned within same template.</span></span> <span data-ttu-id="271fd-194">Proprietà dependsOn hello di tooalso use non è necessario.</span><span class="sxs-lookup"><span data-stu-id="271fd-194">You do not need tooalso use hello dependsOn property.</span></span> <span data-ttu-id="271fd-195">Hello funzione non viene valutata fino a quando non hello risorsa di riferimento è stata completata la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="271fd-195">hello function is not evaluated until hello referenced resource has completed deployment.</span></span>

<span data-ttu-id="271fd-196">i nomi delle proprietà di toosee hello e i valori per un tipo di risorsa, creare un modello che restituisce l'oggetto hello nella sezione di output di hello.</span><span class="sxs-lookup"><span data-stu-id="271fd-196">toosee hello property names and values for a resource type, create a template that returns hello object in hello outputs section.</span></span> <span data-ttu-id="271fd-197">Se si dispone di una risorsa esistente di quel tipo, il modello restituisce l'oggetto di hello senza distribuire le risorse di nuovo.</span><span class="sxs-lookup"><span data-stu-id="271fd-197">If you have an existing resource of that type, your template returns hello object without deploying any new resources.</span></span> 

<span data-ttu-id="271fd-198">In genere, si utilizza hello **riferimento** funzione tooreturn un valore specifico da un oggetto, ad esempio URI dell'endpoint blob hello o un nome di dominio completo.</span><span class="sxs-lookup"><span data-stu-id="271fd-198">Typically, you use hello **reference** function tooreturn a particular value from an object, such as hello blob endpoint URI or fully qualified domain name.</span></span>

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

### <a name="example"></a><span data-ttu-id="271fd-199">Esempio</span><span class="sxs-lookup"><span data-stu-id="271fd-199">Example</span></span>

<span data-ttu-id="271fd-200">riferimenti e toodeploy risorse hello in hello modello stesso, usare:</span><span class="sxs-lookup"><span data-stu-id="271fd-200">toodeploy and reference hello resource in hello same template, use:</span></span>

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

<span data-ttu-id="271fd-201">Hello esempio precedente restituisce un oggetto hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="271fd-201">hello preceding example returns an object in hello following format:</span></span>

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

<span data-ttu-id="271fd-202">Hello seguente fa riferimento a un account di archiviazione che non è distribuito in questo modello.</span><span class="sxs-lookup"><span data-stu-id="271fd-202">hello following example references a storage account that is not deployed in this template.</span></span> <span data-ttu-id="271fd-203">Hello account di archiviazione esiste già all'interno di hello stesso gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="271fd-203">hello storage account already exists within hello same resource group.</span></span>

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

## <a name="resourcegroup"></a><span data-ttu-id="271fd-204">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="271fd-204">resourceGroup</span></span>
`resourceGroup()`

<span data-ttu-id="271fd-205">Restituisce un oggetto che rappresenta il gruppo di risorse corrente hello.</span><span class="sxs-lookup"><span data-stu-id="271fd-205">Returns an object that represents hello current resource group.</span></span> 

### <a name="return-value"></a><span data-ttu-id="271fd-206">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="271fd-206">Return value</span></span>

<span data-ttu-id="271fd-207">Hello ha restituito l'oggetto si trova in hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="271fd-207">hello returned object is in hello following format:</span></span>

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

### <a name="remarks"></a><span data-ttu-id="271fd-208">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="271fd-208">Remarks</span></span>

<span data-ttu-id="271fd-209">Un utilizzo comune della funzione resourceGroup hello è risorse toocreate hello stesso percorso del gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="271fd-209">A common use of hello resourceGroup function is toocreate resources in hello same location as hello resource group.</span></span> <span data-ttu-id="271fd-210">Hello esempio seguente usa hello risorsa gruppo tooassign hello posizione per un sito web.</span><span class="sxs-lookup"><span data-stu-id="271fd-210">hello following example uses hello resource group location tooassign hello location for a web site.</span></span>

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

### <a name="example"></a><span data-ttu-id="271fd-211">Esempio</span><span class="sxs-lookup"><span data-stu-id="271fd-211">Example</span></span>

<span data-ttu-id="271fd-212">Hello modello seguente restituisce le proprietà di hello hello del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="271fd-212">hello following template returns hello properties of hello resource group.</span></span>

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

<span data-ttu-id="271fd-213">Hello esempio precedente restituisce un oggetto hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="271fd-213">hello preceding example returns an object in hello following format:</span></span>

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

## <a name="resourceid"></a><span data-ttu-id="271fd-214">resourceId</span><span class="sxs-lookup"><span data-stu-id="271fd-214">resourceId</span></span>
`resourceId([subscriptionId], [resourceGroupName], resourceType, resourceName1, [resourceName2]...)`

<span data-ttu-id="271fd-215">Restituisce hello identificatore univoco di una risorsa.</span><span class="sxs-lookup"><span data-stu-id="271fd-215">Returns hello unique identifier of a resource.</span></span> <span data-ttu-id="271fd-216">Utilizzare questa funzione quando il nome di risorsa hello è ambiguo o non è disponibile all'interno di hello stesso modello.</span><span class="sxs-lookup"><span data-stu-id="271fd-216">You use this function when hello resource name is ambiguous or not provisioned within hello same template.</span></span> 

### <a name="parameters"></a><span data-ttu-id="271fd-217">parameters</span><span class="sxs-lookup"><span data-stu-id="271fd-217">Parameters</span></span>

| <span data-ttu-id="271fd-218">Parametro</span><span class="sxs-lookup"><span data-stu-id="271fd-218">Parameter</span></span> | <span data-ttu-id="271fd-219">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="271fd-219">Required</span></span> | <span data-ttu-id="271fd-220">Tipo</span><span class="sxs-lookup"><span data-stu-id="271fd-220">Type</span></span> | <span data-ttu-id="271fd-221">Descrizione</span><span class="sxs-lookup"><span data-stu-id="271fd-221">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="271fd-222">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="271fd-222">subscriptionId</span></span> |<span data-ttu-id="271fd-223">No</span><span class="sxs-lookup"><span data-stu-id="271fd-223">No</span></span> |<span data-ttu-id="271fd-224">Stringa (in formato GUID)</span><span class="sxs-lookup"><span data-stu-id="271fd-224">string (In GUID format)</span></span> |<span data-ttu-id="271fd-225">Valore predefinito è la sottoscrizione corrente hello.</span><span class="sxs-lookup"><span data-stu-id="271fd-225">Default value is hello current subscription.</span></span> <span data-ttu-id="271fd-226">Specificare questo valore quando è necessario tooretrieve una risorsa in un'altra sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="271fd-226">Specify this value when you need tooretrieve a resource in another subscription.</span></span> |
| <span data-ttu-id="271fd-227">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="271fd-227">resourceGroupName</span></span> |<span data-ttu-id="271fd-228">No</span><span class="sxs-lookup"><span data-stu-id="271fd-228">No</span></span> |<span data-ttu-id="271fd-229">string</span><span class="sxs-lookup"><span data-stu-id="271fd-229">string</span></span> |<span data-ttu-id="271fd-230">Il valore predefinito è il gruppo di risorse corrente.</span><span class="sxs-lookup"><span data-stu-id="271fd-230">Default value is current resource group.</span></span> <span data-ttu-id="271fd-231">Specificare questo valore quando è necessario tooretrieve una risorsa in un altro gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="271fd-231">Specify this value when you need tooretrieve a resource in another resource group.</span></span> |
| <span data-ttu-id="271fd-232">resourceType</span><span class="sxs-lookup"><span data-stu-id="271fd-232">resourceType</span></span> |<span data-ttu-id="271fd-233">Sì</span><span class="sxs-lookup"><span data-stu-id="271fd-233">Yes</span></span> |<span data-ttu-id="271fd-234">string</span><span class="sxs-lookup"><span data-stu-id="271fd-234">string</span></span> |<span data-ttu-id="271fd-235">Tipo di risorsa, incluso lo spazio dei nomi del provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="271fd-235">Type of resource including resource provider namespace.</span></span> |
| <span data-ttu-id="271fd-236">resourceName1</span><span class="sxs-lookup"><span data-stu-id="271fd-236">resourceName1</span></span> |<span data-ttu-id="271fd-237">Sì</span><span class="sxs-lookup"><span data-stu-id="271fd-237">Yes</span></span> |<span data-ttu-id="271fd-238">string</span><span class="sxs-lookup"><span data-stu-id="271fd-238">string</span></span> |<span data-ttu-id="271fd-239">Nome della risorsa.</span><span class="sxs-lookup"><span data-stu-id="271fd-239">Name of resource.</span></span> |
| <span data-ttu-id="271fd-240">resourceName2</span><span class="sxs-lookup"><span data-stu-id="271fd-240">resourceName2</span></span> |<span data-ttu-id="271fd-241">No</span><span class="sxs-lookup"><span data-stu-id="271fd-241">No</span></span> |<span data-ttu-id="271fd-242">string</span><span class="sxs-lookup"><span data-stu-id="271fd-242">string</span></span> |<span data-ttu-id="271fd-243">Segmento successivo del nome della risorsa se la risorsa è annidata.</span><span class="sxs-lookup"><span data-stu-id="271fd-243">Next resource name segment if resource is nested.</span></span> |

### <a name="return-value"></a><span data-ttu-id="271fd-244">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="271fd-244">Return value</span></span>

<span data-ttu-id="271fd-245">Identificatore Hello viene restituito in hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="271fd-245">hello identifier is returned in hello following format:</span></span>

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### <a name="remarks"></a><span data-ttu-id="271fd-246">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="271fd-246">Remarks</span></span>

<span data-ttu-id="271fd-247">Hello è specificare i valori dei parametri dipendono dalla risorsa hello: in hello stesso gruppo di risorse e di sottoscrizione di distribuzione corrente di hello.</span><span class="sxs-lookup"><span data-stu-id="271fd-247">hello parameter values you specify depend on whether hello resource is in hello same subscription and resource group as hello current deployment.</span></span>

<span data-ttu-id="271fd-248">ID di risorsa hello tooget per un account di archiviazione in hello stessa sottoscrizione e il gruppo di risorse, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="271fd-248">tooget hello resource ID for a storage account in hello same subscription and resource group, use:</span></span>

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="271fd-249">ID della risorsa hello tooget per un account di archiviazione in hello stessa sottoscrizione, ma un gruppo di risorse diverso, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="271fd-249">tooget hello resource ID for a storage account in hello same subscription but a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="271fd-250">ID della risorsa hello tooget per un account di archiviazione in una sottoscrizione diversa e il gruppo di risorse, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="271fd-250">tooget hello resource ID for a storage account in a different subscription and resource group, use:</span></span>

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="271fd-251">ID di risorsa hello tooget per un database in un gruppo di risorse diverso, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="271fd-251">tooget hello resource ID for a database in a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

<span data-ttu-id="271fd-252">Spesso, è necessario toouse questa funzione quando si utilizza un account di archiviazione o di una rete virtuale in un gruppo di risorse alternativo.</span><span class="sxs-lookup"><span data-stu-id="271fd-252">Often, you need toouse this function when using a storage account or virtual network in an alternate resource group.</span></span> <span data-ttu-id="271fd-253">Hello esempio seguente viene illustrato come una risorsa da un gruppo di risorse esterne può essere facilmente usata:</span><span class="sxs-lookup"><span data-stu-id="271fd-253">hello following example shows how a resource from an external resource group can easily be used:</span></span>

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

### <a name="example"></a><span data-ttu-id="271fd-254">Esempio</span><span class="sxs-lookup"><span data-stu-id="271fd-254">Example</span></span>

<span data-ttu-id="271fd-255">Hello esempio seguente restituisce hello ID di risorsa per un account di archiviazione nel gruppo di risorse hello:</span><span class="sxs-lookup"><span data-stu-id="271fd-255">hello following example returns hello resource ID for a storage account in hello resource group:</span></span>

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

<span data-ttu-id="271fd-256">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="271fd-256">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="271fd-257">Nome</span><span class="sxs-lookup"><span data-stu-id="271fd-257">Name</span></span> | <span data-ttu-id="271fd-258">Tipo</span><span class="sxs-lookup"><span data-stu-id="271fd-258">Type</span></span> | <span data-ttu-id="271fd-259">Valore</span><span class="sxs-lookup"><span data-stu-id="271fd-259">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="271fd-260">sameRGOutput</span><span class="sxs-lookup"><span data-stu-id="271fd-260">sameRGOutput</span></span> | <span data-ttu-id="271fd-261">String</span><span class="sxs-lookup"><span data-stu-id="271fd-261">String</span></span> | <span data-ttu-id="271fd-262">/subscriptions/{id-sott-corrente}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="271fd-262">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="271fd-263">differentRGOutput</span><span class="sxs-lookup"><span data-stu-id="271fd-263">differentRGOutput</span></span> | <span data-ttu-id="271fd-264">String</span><span class="sxs-lookup"><span data-stu-id="271fd-264">String</span></span> | <span data-ttu-id="271fd-265">/subscriptions/{id-sott-corrente}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="271fd-265">/subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="271fd-266">differentSubOutput</span><span class="sxs-lookup"><span data-stu-id="271fd-266">differentSubOutput</span></span> | <span data-ttu-id="271fd-267">String</span><span class="sxs-lookup"><span data-stu-id="271fd-267">String</span></span> | <span data-ttu-id="271fd-268">/subscriptions/{id-sott-differente}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="271fd-268">/subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="271fd-269">nestedResourceOutput</span><span class="sxs-lookup"><span data-stu-id="271fd-269">nestedResourceOutput</span></span> | <span data-ttu-id="271fd-270">String</span><span class="sxs-lookup"><span data-stu-id="271fd-270">String</span></span> | <span data-ttu-id="271fd-271">/subscriptions/{id-sott-corrente}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span><span class="sxs-lookup"><span data-stu-id="271fd-271">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span></span> |

<a id="subscription" />

## <a name="subscription"></a><span data-ttu-id="271fd-272">sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="271fd-272">subscription</span></span>
`subscription()`

<span data-ttu-id="271fd-273">Restituisce informazioni dettagliate sulla sottoscrizione hello per la distribuzione corrente di hello.</span><span class="sxs-lookup"><span data-stu-id="271fd-273">Returns details about hello subscription for hello current deployment.</span></span> 

### <a name="return-value"></a><span data-ttu-id="271fd-274">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="271fd-274">Return value</span></span>

<span data-ttu-id="271fd-275">funzione Hello restituisce hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="271fd-275">hello function returns hello following format:</span></span>

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### <a name="example"></a><span data-ttu-id="271fd-276">Esempio</span><span class="sxs-lookup"><span data-stu-id="271fd-276">Example</span></span>

<span data-ttu-id="271fd-277">Hello esempio seguente viene illustrata hello sottoscrizione funzione chiamato nella sezione di output di hello.</span><span class="sxs-lookup"><span data-stu-id="271fd-277">hello following example shows hello subscription function called in hello outputs section.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="271fd-278">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="271fd-278">Next steps</span></span>
* <span data-ttu-id="271fd-279">Per una descrizione delle sezioni hello in un modello di gestione risorse di Azure, vedere [modelli Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="271fd-279">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="271fd-280">toomerge più modelli, vedere [con modelli collegati con Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="271fd-280">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="271fd-281">tooiterate un numero specificato di volte durante la creazione di un tipo di risorsa, vedere [creare più istanze delle risorse in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="271fd-281">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="271fd-282">toosee come modello hello toodeploy è stato creato, vedere [distribuire un'applicazione con il modello di gestione risorse di Azure](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="271fd-282">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

