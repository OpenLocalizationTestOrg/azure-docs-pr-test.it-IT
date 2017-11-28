---
title: funzioni di modello di gestione risorse aaaAzure - distribuzione | Documenti Microsoft
description: Viene descritto toouse funzioni hello in un'informazioni sulla distribuzione di Azure Resource Manager modello tooretrieve.
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
ms.date: 06/13/2017
ms.author: tomfitz
ms.openlocfilehash: 458c3f740504fdd6799ed24cc386219726737636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="2f9f5-103">Funzioni di distribuzione per i modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2f9f5-103">Deployment functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="2f9f5-104">Gestione risorse offre seguente hello funzioni per ottenere valori dalle sezioni del modello di hello e valori correlati toohello distribuzione:</span><span class="sxs-lookup"><span data-stu-id="2f9f5-104">Resource Manager provides hello following functions for getting values from sections of hello template and values related toohello deployment:</span></span>

* [<span data-ttu-id="2f9f5-105">deployment</span><span class="sxs-lookup"><span data-stu-id="2f9f5-105">deployment</span></span>](#deployment)
* [<span data-ttu-id="2f9f5-106">parameters</span><span class="sxs-lookup"><span data-stu-id="2f9f5-106">parameters</span></span>](#parameters)
* [<span data-ttu-id="2f9f5-107">variables</span><span class="sxs-lookup"><span data-stu-id="2f9f5-107">variables</span></span>](#variables)

<span data-ttu-id="2f9f5-108">i valori di tooget di risorse, gruppi di risorse o le sottoscrizioni, vedere [le funzioni della risorsa](resource-group-template-functions-resource.md).</span><span class="sxs-lookup"><span data-stu-id="2f9f5-108">tooget values from resources, resource groups, or subscriptions, see [Resource functions](resource-group-template-functions-resource.md).</span></span>

<a id="deployment" />

## <a name="deployment"></a><span data-ttu-id="2f9f5-109">distribuzione</span><span class="sxs-lookup"><span data-stu-id="2f9f5-109">deployment</span></span>
`deployment()`

<span data-ttu-id="2f9f5-110">Restituisce informazioni sull'operazione di distribuzione corrente di hello.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-110">Returns information about hello current deployment operation.</span></span>

### <a name="return-value"></a><span data-ttu-id="2f9f5-111">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="2f9f5-111">Return value</span></span>

<span data-ttu-id="2f9f5-112">Questa funzione restituisce l'oggetto hello passato durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-112">This function returns hello object that is passed during deployment.</span></span> <span data-ttu-id="2f9f5-113">proprietà Hello in hello restituito oggetto variano in base al fatto hello distribuzione oggetto viene passato come un collegamento o come un oggetto in linea.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-113">hello properties in hello returned object differ based on whether hello deployment object is passed as a link or as an in-line object.</span></span> <span data-ttu-id="2f9f5-114">Oggetto di distribuzione hello viene passato quando in linea, ad esempio quando si utilizza hello **- TemplateFile** parametro nel file locale tooa toopoint Azure PowerShell, hello restituito l'oggetto ha hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="2f9f5-114">When hello deployment object is passed in-line, such as when using hello **-TemplateFile** parameter in Azure PowerShell toopoint tooa local file, hello returned object has hello following format:</span></span>

```json
{
    "name": "",
    "properties": {
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [
            ],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

<span data-ttu-id="2f9f5-115">Quando oggetto hello viene passato come un collegamento, ad esempio quando utilizzando hello **- TemplateUri** dell'oggetto parametro toopoint tooa remoto hello viene restituito in hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="2f9f5-115">When hello object is passed as a link, such as when using hello **-TemplateUri** parameter toopoint tooa remote object, hello object is returned in hello following format:</span></span> 

```json
{
    "name": "",
    "properties": {
        "templateLink": {
            "uri": ""
        },
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

### <a name="remarks"></a><span data-ttu-id="2f9f5-116">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="2f9f5-116">Remarks</span></span>

<span data-ttu-id="2f9f5-117">È possibile utilizzare una distribuzione () toolink tooanother modello basato su URI del modello padre hello hello.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-117">You can use deployment() toolink tooanother template based on hello URI of hello parent template.</span></span>

```json
"variables": {  
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"  
}
```  

### <a name="example"></a><span data-ttu-id="2f9f5-118">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f9f5-118">Example</span></span>

<span data-ttu-id="2f9f5-119">Hello esempio seguente viene restituito oggetto distribuzione hello:</span><span class="sxs-lookup"><span data-stu-id="2f9f5-119">hello following example returns hello deployment object:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[deployment()]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="2f9f5-120">Hello esempio precedente restituisce hello seguente oggetto:</span><span class="sxs-lookup"><span data-stu-id="2f9f5-120">hello preceding example returns hello following object:</span></span>

```json
{
  "name": "deployment",
  "properties": {
    "template": {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "resources": [],
      "outputs": {
        "subscriptionOutput": {
          "type": "Object",
          "value": "[deployment()]"
        }
      }
    },
    "parameters": {},
    "mode": "Incremental",
    "provisioningState": "Accepted"
  }
}
```

<a id="parameters" />

## <a name="parameters"></a><span data-ttu-id="2f9f5-121">parameters</span><span class="sxs-lookup"><span data-stu-id="2f9f5-121">parameters</span></span>
`parameters(parameterName)`

<span data-ttu-id="2f9f5-122">Restituisce un valore di parametro.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-122">Returns a parameter value.</span></span> <span data-ttu-id="2f9f5-123">nome del parametro specificato Hello deve essere definito nella sezione parametri hello del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-123">hello specified parameter name must be defined in hello parameters section of hello template.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f9f5-124">parameters</span><span class="sxs-lookup"><span data-stu-id="2f9f5-124">Parameters</span></span>

| <span data-ttu-id="2f9f5-125">Parametro</span><span class="sxs-lookup"><span data-stu-id="2f9f5-125">Parameter</span></span> | <span data-ttu-id="2f9f5-126">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2f9f5-126">Required</span></span> | <span data-ttu-id="2f9f5-127">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f9f5-127">Type</span></span> | <span data-ttu-id="2f9f5-128">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f9f5-128">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2f9f5-129">parameterName</span><span class="sxs-lookup"><span data-stu-id="2f9f5-129">parameterName</span></span> |<span data-ttu-id="2f9f5-130">Sì</span><span class="sxs-lookup"><span data-stu-id="2f9f5-130">Yes</span></span> |<span data-ttu-id="2f9f5-131">string</span><span class="sxs-lookup"><span data-stu-id="2f9f5-131">string</span></span> |<span data-ttu-id="2f9f5-132">nome Hello del tooreturn parametro hello.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-132">hello name of hello parameter tooreturn.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2f9f5-133">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="2f9f5-133">Return value</span></span>

<span data-ttu-id="2f9f5-134">parametro specificato il valore Hello hello.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-134">hello value of hello specified parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="2f9f5-135">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="2f9f5-135">Remarks</span></span>

<span data-ttu-id="2f9f5-136">In genere, si utilizzano valori dei parametri tooset risorse.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-136">Typically, you use parameters tooset resource values.</span></span> <span data-ttu-id="2f9f5-137">Hello esempio seguente imposta il nome di hello del sito web toohello valore del parametro passato durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-137">hello following example sets hello name of web site toohello parameter value passed in during deployment.</span></span>

```json
"parameters": { 
  "siteName": {
      "type": "string"
  }
},
"resources": [
   {
      "apiVersion": "2016-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/Sites",
      ...
   }
]
```

### <a name="example"></a><span data-ttu-id="2f9f5-138">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f9f5-138">Example</span></span>

<span data-ttu-id="2f9f5-139">Hello seguente viene illustrato un utilizzo della funzione parametri hello semplificato.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-139">hello following example shows a simplified use of hello parameters function.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringParameter": {
            "type" : "string",
            "defaultValue": "option 1"
        },
        "intParameter": {
            "type": "int",
            "defaultValue": 1
        },
        "objectParameter": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b"}
        },
        "arrayParameter": {
            "type": "array",
            "defaultValue": [1, 2, 3]
        },
        "crossParameter": {
            "type": "string",
            "defaultValue": "[parameters('stringParameter')]"
        }
    },
    "variables": {},
    "resources": [],
    "outputs": {
        "stringOutput": {
            "value": "[parameters('stringParameter')]",
            "type" : "string"
        },
        "intOutput": {
            "value": "[parameters('intParameter')]",
            "type" : "int"
        },
        "objectOutput": {
            "value": "[parameters('objectParameter')]",
            "type" : "object"
        },
        "arrayOutput": {
            "value": "[parameters('arrayParameter')]",
            "type" : "array"
        },
        "crossOutput": {
            "value": "[parameters('crossParameter')]",
            "type" : "string"
        }
    }
}
```

<span data-ttu-id="2f9f5-140">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="2f9f5-140">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="2f9f5-141">Nome</span><span class="sxs-lookup"><span data-stu-id="2f9f5-141">Name</span></span> | <span data-ttu-id="2f9f5-142">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f9f5-142">Type</span></span> | <span data-ttu-id="2f9f5-143">Valore</span><span class="sxs-lookup"><span data-stu-id="2f9f5-143">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2f9f5-144">stringOutput</span><span class="sxs-lookup"><span data-stu-id="2f9f5-144">stringOutput</span></span> | <span data-ttu-id="2f9f5-145">String</span><span class="sxs-lookup"><span data-stu-id="2f9f5-145">String</span></span> | <span data-ttu-id="2f9f5-146">option 1</span><span class="sxs-lookup"><span data-stu-id="2f9f5-146">option 1</span></span> |
| <span data-ttu-id="2f9f5-147">intOutput</span><span class="sxs-lookup"><span data-stu-id="2f9f5-147">intOutput</span></span> | <span data-ttu-id="2f9f5-148">int</span><span class="sxs-lookup"><span data-stu-id="2f9f5-148">Int</span></span> | <span data-ttu-id="2f9f5-149">1</span><span class="sxs-lookup"><span data-stu-id="2f9f5-149">1</span></span> |
| <span data-ttu-id="2f9f5-150">objectOutput</span><span class="sxs-lookup"><span data-stu-id="2f9f5-150">objectOutput</span></span> | <span data-ttu-id="2f9f5-151">Oggetto</span><span class="sxs-lookup"><span data-stu-id="2f9f5-151">Object</span></span> | <span data-ttu-id="2f9f5-152">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="2f9f5-152">{"one": "a", "two": "b"}</span></span> |
| <span data-ttu-id="2f9f5-153">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="2f9f5-153">arrayOutput</span></span> | <span data-ttu-id="2f9f5-154">Array</span><span class="sxs-lookup"><span data-stu-id="2f9f5-154">Array</span></span> | <span data-ttu-id="2f9f5-155">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="2f9f5-155">[1, 2, 3]</span></span> |
| <span data-ttu-id="2f9f5-156">crossOutput</span><span class="sxs-lookup"><span data-stu-id="2f9f5-156">crossOutput</span></span> | <span data-ttu-id="2f9f5-157">String</span><span class="sxs-lookup"><span data-stu-id="2f9f5-157">String</span></span> | <span data-ttu-id="2f9f5-158">option 1</span><span class="sxs-lookup"><span data-stu-id="2f9f5-158">option 1</span></span> |

<a id="variables" />

## <a name="variables"></a><span data-ttu-id="2f9f5-159">variables</span><span class="sxs-lookup"><span data-stu-id="2f9f5-159">variables</span></span>
`variables(variableName)`

<span data-ttu-id="2f9f5-160">Restituisce hello valore della variabile.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-160">Returns hello value of variable.</span></span> <span data-ttu-id="2f9f5-161">nome di variabile specificato Hello deve essere definito nella sezione variabili hello del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-161">hello specified variable name must be defined in hello variables section of hello template.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f9f5-162">parameters</span><span class="sxs-lookup"><span data-stu-id="2f9f5-162">Parameters</span></span>

| <span data-ttu-id="2f9f5-163">Parametro</span><span class="sxs-lookup"><span data-stu-id="2f9f5-163">Parameter</span></span> | <span data-ttu-id="2f9f5-164">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2f9f5-164">Required</span></span> | <span data-ttu-id="2f9f5-165">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f9f5-165">Type</span></span> | <span data-ttu-id="2f9f5-166">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f9f5-166">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2f9f5-167">variableName</span><span class="sxs-lookup"><span data-stu-id="2f9f5-167">variableName</span></span> |<span data-ttu-id="2f9f5-168">Sì</span><span class="sxs-lookup"><span data-stu-id="2f9f5-168">Yes</span></span> |<span data-ttu-id="2f9f5-169">String</span><span class="sxs-lookup"><span data-stu-id="2f9f5-169">String</span></span> |<span data-ttu-id="2f9f5-170">nome Hello del tooreturn variabile hello.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-170">hello name of hello variable tooreturn.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2f9f5-171">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="2f9f5-171">Return value</span></span>

<span data-ttu-id="2f9f5-172">valore di Hello della variabile specificata hello.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-172">hello value of hello specified variable.</span></span>

### <a name="remarks"></a><span data-ttu-id="2f9f5-173">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="2f9f5-173">Remarks</span></span>

<span data-ttu-id="2f9f5-174">In genere utilizzata toosimplify variabili del modello creando una sola volta valori complessi.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-174">Typically, you use variables toosimplify your template by constructing complex values only once.</span></span> <span data-ttu-id="2f9f5-175">Hello seguente esempio crea un nome univoco per un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-175">hello following example constructs a unique name for a storage account.</span></span>

```json
"variables": {
    "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
},
"resources": [
    {
        "type": "Microsoft.Storage/storageAccounts",
        "name": "[variables('storageName')]",
        ...
    },
    {
        "type": "Microsoft.Compute/virtualMachines",
        "dependsOn": [
            "[variables('storageName')]"
        ],
        ...
    }
],
```

### <a name="example"></a><span data-ttu-id="2f9f5-176">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f9f5-176">Example</span></span>

<span data-ttu-id="2f9f5-177">modello di esempio Hello restituisce valori di variabili diversi.</span><span class="sxs-lookup"><span data-stu-id="2f9f5-177">hello example template returns different variable values.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "variables": {
        "var1": "myVariable",
        "var2": [ 1,2,3,4 ],
        "var3": "[ variables('var1') ]",
        "var4": {
            "property1": "value1",
            "property2": "value2"
        }
    },
    "resources": [],
    "outputs": {
        "exampleOutput1": {
            "value": "[variables('var1')]",
            "type" : "string"
        },
        "exampleOutput2": {
            "value": "[variables('var2')]",
            "type" : "array"
        },
        "exampleOutput3": {
            "value": "[variables('var3')]",
            "type" : "string"
        },
        "exampleOutput4": {
            "value": "[variables('var4')]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="2f9f5-178">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="2f9f5-178">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="2f9f5-179">Nome</span><span class="sxs-lookup"><span data-stu-id="2f9f5-179">Name</span></span> | <span data-ttu-id="2f9f5-180">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f9f5-180">Type</span></span> | <span data-ttu-id="2f9f5-181">Valore</span><span class="sxs-lookup"><span data-stu-id="2f9f5-181">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2f9f5-182">exampleOutput1</span><span class="sxs-lookup"><span data-stu-id="2f9f5-182">exampleOutput1</span></span> | <span data-ttu-id="2f9f5-183">String</span><span class="sxs-lookup"><span data-stu-id="2f9f5-183">String</span></span> | <span data-ttu-id="2f9f5-184">myVariable</span><span class="sxs-lookup"><span data-stu-id="2f9f5-184">myVariable</span></span> |
| <span data-ttu-id="2f9f5-185">exampleOutput2</span><span class="sxs-lookup"><span data-stu-id="2f9f5-185">exampleOutput2</span></span> | <span data-ttu-id="2f9f5-186">Array</span><span class="sxs-lookup"><span data-stu-id="2f9f5-186">Array</span></span> | <span data-ttu-id="2f9f5-187">[1, 2, 3, 4]</span><span class="sxs-lookup"><span data-stu-id="2f9f5-187">[1, 2, 3, 4]</span></span> |
| <span data-ttu-id="2f9f5-188">exampleOutput3</span><span class="sxs-lookup"><span data-stu-id="2f9f5-188">exampleOutput3</span></span> | <span data-ttu-id="2f9f5-189">String</span><span class="sxs-lookup"><span data-stu-id="2f9f5-189">String</span></span> | <span data-ttu-id="2f9f5-190">myVariable</span><span class="sxs-lookup"><span data-stu-id="2f9f5-190">myVariable</span></span> |
| <span data-ttu-id="2f9f5-191">exampleOutput4</span><span class="sxs-lookup"><span data-stu-id="2f9f5-191">exampleOutput4</span></span> |  <span data-ttu-id="2f9f5-192">Oggetto</span><span class="sxs-lookup"><span data-stu-id="2f9f5-192">Object</span></span> | <span data-ttu-id="2f9f5-193">{"property1": "value1", "property2": "value2"}</span><span class="sxs-lookup"><span data-stu-id="2f9f5-193">{"property1": "value1", "property2": "value2"}</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2f9f5-194">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2f9f5-194">Next steps</span></span>
* <span data-ttu-id="2f9f5-195">Per una descrizione delle sezioni hello in un modello di gestione risorse di Azure, vedere [modelli Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2f9f5-195">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="2f9f5-196">toomerge più modelli, vedere [con modelli collegati con Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2f9f5-196">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="2f9f5-197">tooiterate un numero specificato di volte durante la creazione di un tipo di risorsa, vedere [creare più istanze delle risorse in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="2f9f5-197">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="2f9f5-198">toosee come modello hello toodeploy è stato creato, vedere [distribuire un'applicazione con il modello di gestione risorse di Azure](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="2f9f5-198">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

