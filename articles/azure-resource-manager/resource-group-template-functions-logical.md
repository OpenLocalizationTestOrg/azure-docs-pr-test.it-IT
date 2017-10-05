---
title: 'Funzioni del modello di Azure Resource Manager: logiche | Microsoft Docs'
description: "Informazioni sulle funzioni che è possibile usare in un modello di Azure Resource Manager per determinare i valori logici."
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
ms.date: 08/01/2017
ms.author: tomfitz
ms.openlocfilehash: 313601ad99cdc12c4b50f5469959d37a9fa70d35
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="logical-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="eee56-103">Funzioni logiche nei modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="eee56-103">Logical functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="eee56-104">Resource Manager include numerose funzioni per l'esecuzione di confronti nei modelli.</span><span class="sxs-lookup"><span data-stu-id="eee56-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="eee56-105">and</span><span class="sxs-lookup"><span data-stu-id="eee56-105">and</span></span>](#and)
* [<span data-ttu-id="eee56-106">bool</span><span class="sxs-lookup"><span data-stu-id="eee56-106">bool</span></span>](#bool)
* [<span data-ttu-id="eee56-107">if</span><span class="sxs-lookup"><span data-stu-id="eee56-107">if</span></span>](#if)
* [<span data-ttu-id="eee56-108">not</span><span class="sxs-lookup"><span data-stu-id="eee56-108">not</span></span>](#not)
* [<span data-ttu-id="eee56-109">or</span><span class="sxs-lookup"><span data-stu-id="eee56-109">or</span></span>](#or)

## <a name="and"></a><span data-ttu-id="eee56-110">e</span><span class="sxs-lookup"><span data-stu-id="eee56-110">and</span></span>
`and(arg1, arg2)`

<span data-ttu-id="eee56-111">Controlla se i valori di entrambi i parametri sono true.</span><span class="sxs-lookup"><span data-stu-id="eee56-111">Checks whether both parameter values are true.</span></span>

### <a name="parameters"></a><span data-ttu-id="eee56-112">parameters</span><span class="sxs-lookup"><span data-stu-id="eee56-112">Parameters</span></span>

| <span data-ttu-id="eee56-113">Parametro</span><span class="sxs-lookup"><span data-stu-id="eee56-113">Parameter</span></span> | <span data-ttu-id="eee56-114">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="eee56-114">Required</span></span> | <span data-ttu-id="eee56-115">Tipo</span><span class="sxs-lookup"><span data-stu-id="eee56-115">Type</span></span> | <span data-ttu-id="eee56-116">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eee56-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="eee56-117">arg1</span><span class="sxs-lookup"><span data-stu-id="eee56-117">arg1</span></span> |<span data-ttu-id="eee56-118">Sì</span><span class="sxs-lookup"><span data-stu-id="eee56-118">Yes</span></span> |<span data-ttu-id="eee56-119">boolean</span><span class="sxs-lookup"><span data-stu-id="eee56-119">boolean</span></span> |<span data-ttu-id="eee56-120">Primo valore da controllare per verificare se è true.</span><span class="sxs-lookup"><span data-stu-id="eee56-120">The first value to check whether is true.</span></span> |
| <span data-ttu-id="eee56-121">arg2</span><span class="sxs-lookup"><span data-stu-id="eee56-121">arg2</span></span> |<span data-ttu-id="eee56-122">Sì</span><span class="sxs-lookup"><span data-stu-id="eee56-122">Yes</span></span> |<span data-ttu-id="eee56-123">boolean</span><span class="sxs-lookup"><span data-stu-id="eee56-123">boolean</span></span> |<span data-ttu-id="eee56-124">Secondo valore da controllare per verificare se è true.</span><span class="sxs-lookup"><span data-stu-id="eee56-124">The second value to check whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="eee56-125">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="eee56-125">Return value</span></span>

<span data-ttu-id="eee56-126">Restituisce **True** se entrambi i valori sono true. In caso contrario, restituisce **False**.</span><span class="sxs-lookup"><span data-stu-id="eee56-126">Returns **True** if both values are true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="eee56-127">Esempi</span><span class="sxs-lookup"><span data-stu-id="eee56-127">Examples</span></span>

<span data-ttu-id="eee56-128">L'esempio seguente mostra come usare le funzioni logiche.</span><span class="sxs-lookup"><span data-stu-id="eee56-128">The following example shows how to use logical functions.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

<span data-ttu-id="eee56-129">L'output dell'esempio precedente è:</span><span class="sxs-lookup"><span data-stu-id="eee56-129">The output from the preceding example is:</span></span>

| <span data-ttu-id="eee56-130">Nome</span><span class="sxs-lookup"><span data-stu-id="eee56-130">Name</span></span> | <span data-ttu-id="eee56-131">Tipo</span><span class="sxs-lookup"><span data-stu-id="eee56-131">Type</span></span> | <span data-ttu-id="eee56-132">Valore</span><span class="sxs-lookup"><span data-stu-id="eee56-132">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="eee56-133">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="eee56-133">andExampleOutput</span></span> | <span data-ttu-id="eee56-134">Booleano</span><span class="sxs-lookup"><span data-stu-id="eee56-134">Bool</span></span> | <span data-ttu-id="eee56-135">False</span><span class="sxs-lookup"><span data-stu-id="eee56-135">False</span></span> |
| <span data-ttu-id="eee56-136">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="eee56-136">orExampleOutput</span></span> | <span data-ttu-id="eee56-137">Booleano</span><span class="sxs-lookup"><span data-stu-id="eee56-137">Bool</span></span> | <span data-ttu-id="eee56-138">True </span><span class="sxs-lookup"><span data-stu-id="eee56-138">True</span></span> |
| <span data-ttu-id="eee56-139">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="eee56-139">notExampleOutput</span></span> | <span data-ttu-id="eee56-140">Booleano</span><span class="sxs-lookup"><span data-stu-id="eee56-140">Bool</span></span> | <span data-ttu-id="eee56-141">False</span><span class="sxs-lookup"><span data-stu-id="eee56-141">False</span></span> |


## <a name="bool"></a><span data-ttu-id="eee56-142">bool</span><span class="sxs-lookup"><span data-stu-id="eee56-142">bool</span></span>
`bool(arg1)`

<span data-ttu-id="eee56-143">Converte il parametro in un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="eee56-143">Converts the parameter to a boolean.</span></span>

### <a name="parameters"></a><span data-ttu-id="eee56-144">Parametri</span><span class="sxs-lookup"><span data-stu-id="eee56-144">Parameters</span></span>

| <span data-ttu-id="eee56-145">Parametro</span><span class="sxs-lookup"><span data-stu-id="eee56-145">Parameter</span></span> | <span data-ttu-id="eee56-146">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="eee56-146">Required</span></span> | <span data-ttu-id="eee56-147">Tipo</span><span class="sxs-lookup"><span data-stu-id="eee56-147">Type</span></span> | <span data-ttu-id="eee56-148">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eee56-148">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="eee56-149">arg1</span><span class="sxs-lookup"><span data-stu-id="eee56-149">arg1</span></span> |<span data-ttu-id="eee56-150">Sì</span><span class="sxs-lookup"><span data-stu-id="eee56-150">Yes</span></span> |<span data-ttu-id="eee56-151">Stringa o numero intero</span><span class="sxs-lookup"><span data-stu-id="eee56-151">string or int</span></span> |<span data-ttu-id="eee56-152">Valore da convertire in un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="eee56-152">The value to convert to a boolean.</span></span> |

### <a name="return-value"></a><span data-ttu-id="eee56-153">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="eee56-153">Return value</span></span>
<span data-ttu-id="eee56-154">Valore booleano del valore convertito.</span><span class="sxs-lookup"><span data-stu-id="eee56-154">A boolean of the converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="eee56-155">esempi</span><span class="sxs-lookup"><span data-stu-id="eee56-155">Examples</span></span>

<span data-ttu-id="eee56-156">L'esempio seguente illustra come usare il parametro bool con un numero intero o una stringa.</span><span class="sxs-lookup"><span data-stu-id="eee56-156">The following example shows how to use bool with a string or integer.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "trueString": {
            "value": "[bool('true')]",
            "type" : "bool"
        },
        "falseString": {
            "value": "[bool('false')]",
            "type" : "bool"
        },
        "trueInt": {
            "value": "[bool(1)]",
            "type" : "bool"
        },
        "falseInt": {
            "value": "[bool(0)]",
            "type" : "bool"
        }
    }
}
```

<span data-ttu-id="eee56-157">L'output dell'esempio precedente con i valori predefiniti è:</span><span class="sxs-lookup"><span data-stu-id="eee56-157">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="eee56-158">Nome</span><span class="sxs-lookup"><span data-stu-id="eee56-158">Name</span></span> | <span data-ttu-id="eee56-159">Tipo</span><span class="sxs-lookup"><span data-stu-id="eee56-159">Type</span></span> | <span data-ttu-id="eee56-160">Valore</span><span class="sxs-lookup"><span data-stu-id="eee56-160">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="eee56-161">trueString</span><span class="sxs-lookup"><span data-stu-id="eee56-161">trueString</span></span> | <span data-ttu-id="eee56-162">Booleano</span><span class="sxs-lookup"><span data-stu-id="eee56-162">Bool</span></span> | <span data-ttu-id="eee56-163">True </span><span class="sxs-lookup"><span data-stu-id="eee56-163">True</span></span> |
| <span data-ttu-id="eee56-164">falseString</span><span class="sxs-lookup"><span data-stu-id="eee56-164">falseString</span></span> | <span data-ttu-id="eee56-165">Booleano</span><span class="sxs-lookup"><span data-stu-id="eee56-165">Bool</span></span> | <span data-ttu-id="eee56-166">False</span><span class="sxs-lookup"><span data-stu-id="eee56-166">False</span></span> |
| <span data-ttu-id="eee56-167">trueInt</span><span class="sxs-lookup"><span data-stu-id="eee56-167">trueInt</span></span> | <span data-ttu-id="eee56-168">Booleano</span><span class="sxs-lookup"><span data-stu-id="eee56-168">Bool</span></span> | <span data-ttu-id="eee56-169">True </span><span class="sxs-lookup"><span data-stu-id="eee56-169">True</span></span> |
| <span data-ttu-id="eee56-170">falseInt</span><span class="sxs-lookup"><span data-stu-id="eee56-170">falseInt</span></span> | <span data-ttu-id="eee56-171">Booleano</span><span class="sxs-lookup"><span data-stu-id="eee56-171">Bool</span></span> | <span data-ttu-id="eee56-172">False</span><span class="sxs-lookup"><span data-stu-id="eee56-172">False</span></span> |

## <a name="if"></a><span data-ttu-id="eee56-173">if</span><span class="sxs-lookup"><span data-stu-id="eee56-173">if</span></span>
`if(condition, trueValue, falseValue)`

<span data-ttu-id="eee56-174">Restituisce un valore in base a un condizione true o false.</span><span class="sxs-lookup"><span data-stu-id="eee56-174">Returns a value based on whether a condition is true or false.</span></span>

### <a name="parameters"></a><span data-ttu-id="eee56-175">Parametri</span><span class="sxs-lookup"><span data-stu-id="eee56-175">Parameters</span></span>

| <span data-ttu-id="eee56-176">Parametro</span><span class="sxs-lookup"><span data-stu-id="eee56-176">Parameter</span></span> | <span data-ttu-id="eee56-177">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="eee56-177">Required</span></span> | <span data-ttu-id="eee56-178">Tipo</span><span class="sxs-lookup"><span data-stu-id="eee56-178">Type</span></span> | <span data-ttu-id="eee56-179">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eee56-179">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="eee56-180">condition</span><span class="sxs-lookup"><span data-stu-id="eee56-180">condition</span></span> |<span data-ttu-id="eee56-181">Sì</span><span class="sxs-lookup"><span data-stu-id="eee56-181">Yes</span></span> |<span data-ttu-id="eee56-182">boolean</span><span class="sxs-lookup"><span data-stu-id="eee56-182">boolean</span></span> |<span data-ttu-id="eee56-183">Valore da controllare per verificare se è true.</span><span class="sxs-lookup"><span data-stu-id="eee56-183">The value to check whether it is true.</span></span> |
| <span data-ttu-id="eee56-184">trueValue</span><span class="sxs-lookup"><span data-stu-id="eee56-184">trueValue</span></span> |<span data-ttu-id="eee56-185">Sì</span><span class="sxs-lookup"><span data-stu-id="eee56-185">Yes</span></span> | <span data-ttu-id="eee56-186">string, int, object o array</span><span class="sxs-lookup"><span data-stu-id="eee56-186">string, int, object, or array</span></span> |<span data-ttu-id="eee56-187">Valore da restituire quando la condizione è true.</span><span class="sxs-lookup"><span data-stu-id="eee56-187">The value to return when the condition is true.</span></span> |
| <span data-ttu-id="eee56-188">falseValue</span><span class="sxs-lookup"><span data-stu-id="eee56-188">falseValue</span></span> |<span data-ttu-id="eee56-189">Sì</span><span class="sxs-lookup"><span data-stu-id="eee56-189">Yes</span></span> | <span data-ttu-id="eee56-190">string, int, object o array</span><span class="sxs-lookup"><span data-stu-id="eee56-190">string, int, object, or array</span></span> |<span data-ttu-id="eee56-191">Valore da restituire quando la condizione è false.</span><span class="sxs-lookup"><span data-stu-id="eee56-191">The value to return when the condition is false.</span></span> |

### <a name="return-value"></a><span data-ttu-id="eee56-192">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="eee56-192">Return value</span></span>

<span data-ttu-id="eee56-193">Restituisce il secondo parametro, quando il primo parametro è **True**. In caso contrario, restituisce il terzo parametro.</span><span class="sxs-lookup"><span data-stu-id="eee56-193">Returns second parameter when first parameter is **True**; otherwise, returns third parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="eee56-194">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="eee56-194">Remarks</span></span>

<span data-ttu-id="eee56-195">È possibile usare questa funzione per impostare in modo condizionale una proprietà di una risorsa.</span><span class="sxs-lookup"><span data-stu-id="eee56-195">You can use this function to conditionally set a resource property.</span></span> <span data-ttu-id="eee56-196">L'esempio seguente non è un modello completo, ma mostra le sezioni rilevanti per l'impostazione condizionale del set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="eee56-196">The following example is not a full template, but it shows the relevant portions for conditionally setting the availability set.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "availabilitySet": {
            "type": "string",
            "allowedValues": [
                "yes",
                "no"
            ]
        }
    },
    "variables": {
        ...
        "availabilitySetName": "availabilitySet1",
        "availabilitySet": {
            "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
        }
    },
    "resources": [
        {
            "condition": "[equals(parameters('availabilitySet'),'yes')]",
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            ...
        },
        {
            "apiVersion": "2016-03-30",
            "type": "Microsoft.Compute/virtualMachines",
            "properties": {
                "availabilitySet": "[if(equals(parameters('availabilitySet'),'yes'), variables('availabilitySet'), json('null'))]",
                ...
            }
        },
        ...
    ],
    ...
}
```

### <a name="examples"></a><span data-ttu-id="eee56-197">Esempi</span><span class="sxs-lookup"><span data-stu-id="eee56-197">Examples</span></span>

<span data-ttu-id="eee56-198">L'esempio seguente illustra come usare la funzione `if`.</span><span class="sxs-lookup"><span data-stu-id="eee56-198">The following example shows how to use the `if` function.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "yesOutput": {
            "type": "string",
            "value": "[if(equals('a', 'a'), 'yes', 'no')]"
        },
        "noOutput": {
            "type": "string",
            "value": "[if(equals('a', 'b'), 'yes', 'no')]"
        }
    }
}
```

<span data-ttu-id="eee56-199">L'output dell'esempio precedente è:</span><span class="sxs-lookup"><span data-stu-id="eee56-199">The output from the preceding example is:</span></span>

| <span data-ttu-id="eee56-200">Nome</span><span class="sxs-lookup"><span data-stu-id="eee56-200">Name</span></span> | <span data-ttu-id="eee56-201">Tipo</span><span class="sxs-lookup"><span data-stu-id="eee56-201">Type</span></span> | <span data-ttu-id="eee56-202">Valore</span><span class="sxs-lookup"><span data-stu-id="eee56-202">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="eee56-203">yesOutput</span><span class="sxs-lookup"><span data-stu-id="eee56-203">yesOutput</span></span> | <span data-ttu-id="eee56-204">String</span><span class="sxs-lookup"><span data-stu-id="eee56-204">String</span></span> | <span data-ttu-id="eee56-205">sì</span><span class="sxs-lookup"><span data-stu-id="eee56-205">yes</span></span> |
| <span data-ttu-id="eee56-206">noOutput</span><span class="sxs-lookup"><span data-stu-id="eee56-206">noOutput</span></span> | <span data-ttu-id="eee56-207">String</span><span class="sxs-lookup"><span data-stu-id="eee56-207">String</span></span> | <span data-ttu-id="eee56-208">no</span><span class="sxs-lookup"><span data-stu-id="eee56-208">no</span></span> |


## <a name="not"></a><span data-ttu-id="eee56-209">not</span><span class="sxs-lookup"><span data-stu-id="eee56-209">not</span></span>
`not(arg1)`

<span data-ttu-id="eee56-210">Converte il valore booleano nel valore opposto.</span><span class="sxs-lookup"><span data-stu-id="eee56-210">Converts boolean value to its opposite value.</span></span>

### <a name="parameters"></a><span data-ttu-id="eee56-211">parameters</span><span class="sxs-lookup"><span data-stu-id="eee56-211">Parameters</span></span>

| <span data-ttu-id="eee56-212">Parametro</span><span class="sxs-lookup"><span data-stu-id="eee56-212">Parameter</span></span> | <span data-ttu-id="eee56-213">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="eee56-213">Required</span></span> | <span data-ttu-id="eee56-214">Tipo</span><span class="sxs-lookup"><span data-stu-id="eee56-214">Type</span></span> | <span data-ttu-id="eee56-215">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eee56-215">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="eee56-216">arg1</span><span class="sxs-lookup"><span data-stu-id="eee56-216">arg1</span></span> |<span data-ttu-id="eee56-217">Sì</span><span class="sxs-lookup"><span data-stu-id="eee56-217">Yes</span></span> |<span data-ttu-id="eee56-218">boolean</span><span class="sxs-lookup"><span data-stu-id="eee56-218">boolean</span></span> |<span data-ttu-id="eee56-219">Valore da convertire.</span><span class="sxs-lookup"><span data-stu-id="eee56-219">The value to convert.</span></span> |


### <a name="return-value"></a><span data-ttu-id="eee56-220">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="eee56-220">Return value</span></span>

<span data-ttu-id="eee56-221">Restituisce **True** quando il parametro è **False**.</span><span class="sxs-lookup"><span data-stu-id="eee56-221">Returns **True** when parameter is **False**.</span></span> <span data-ttu-id="eee56-222">Restituisce **False** quando il parametro è **True**.</span><span class="sxs-lookup"><span data-stu-id="eee56-222">Returns **False** when parameter is **True**.</span></span>

### <a name="examples"></a><span data-ttu-id="eee56-223">Esempi</span><span class="sxs-lookup"><span data-stu-id="eee56-223">Examples</span></span>

<span data-ttu-id="eee56-224">L'esempio seguente mostra come usare le funzioni logiche.</span><span class="sxs-lookup"><span data-stu-id="eee56-224">The following example shows how to use logical functions.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

<span data-ttu-id="eee56-225">L'output dell'esempio precedente è:</span><span class="sxs-lookup"><span data-stu-id="eee56-225">The output from the preceding example is:</span></span>

| <span data-ttu-id="eee56-226">Nome</span><span class="sxs-lookup"><span data-stu-id="eee56-226">Name</span></span> | <span data-ttu-id="eee56-227">Tipo</span><span class="sxs-lookup"><span data-stu-id="eee56-227">Type</span></span> | <span data-ttu-id="eee56-228">Valore</span><span class="sxs-lookup"><span data-stu-id="eee56-228">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="eee56-229">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="eee56-229">andExampleOutput</span></span> | <span data-ttu-id="eee56-230">Booleano</span><span class="sxs-lookup"><span data-stu-id="eee56-230">Bool</span></span> | <span data-ttu-id="eee56-231">False</span><span class="sxs-lookup"><span data-stu-id="eee56-231">False</span></span> |
| <span data-ttu-id="eee56-232">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="eee56-232">orExampleOutput</span></span> | <span data-ttu-id="eee56-233">Booleano</span><span class="sxs-lookup"><span data-stu-id="eee56-233">Bool</span></span> | <span data-ttu-id="eee56-234">True </span><span class="sxs-lookup"><span data-stu-id="eee56-234">True</span></span> |
| <span data-ttu-id="eee56-235">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="eee56-235">notExampleOutput</span></span> | <span data-ttu-id="eee56-236">Booleano</span><span class="sxs-lookup"><span data-stu-id="eee56-236">Bool</span></span> | <span data-ttu-id="eee56-237">False</span><span class="sxs-lookup"><span data-stu-id="eee56-237">False</span></span> |

<span data-ttu-id="eee56-238">L'esempio seguente usa **not** con [equals](resource-group-template-functions-comparison.md#equals).</span><span class="sxs-lookup"><span data-stu-id="eee56-238">The following example uses **not** with [equals](resource-group-template-functions-comparison.md#equals).</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "checkNotEquals": {
            "type": "bool",
            "value": "[not(equals(1, 2))]"
        }
    }
```

<span data-ttu-id="eee56-239">L'output dell'esempio precedente è:</span><span class="sxs-lookup"><span data-stu-id="eee56-239">The output from the preceding example is:</span></span>

| <span data-ttu-id="eee56-240">Nome</span><span class="sxs-lookup"><span data-stu-id="eee56-240">Name</span></span> | <span data-ttu-id="eee56-241">Tipo</span><span class="sxs-lookup"><span data-stu-id="eee56-241">Type</span></span> | <span data-ttu-id="eee56-242">Valore</span><span class="sxs-lookup"><span data-stu-id="eee56-242">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="eee56-243">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="eee56-243">checkNotEquals</span></span> | <span data-ttu-id="eee56-244">Booleano</span><span class="sxs-lookup"><span data-stu-id="eee56-244">Bool</span></span> | <span data-ttu-id="eee56-245">True </span><span class="sxs-lookup"><span data-stu-id="eee56-245">True</span></span> |


## <a name="or"></a><span data-ttu-id="eee56-246">oppure</span><span class="sxs-lookup"><span data-stu-id="eee56-246">or</span></span>
`or(arg1, arg2)`

<span data-ttu-id="eee56-247">Controlla se il valore di uno dei due parametri è true.</span><span class="sxs-lookup"><span data-stu-id="eee56-247">Checks whether either parameter value is true.</span></span>

### <a name="parameters"></a><span data-ttu-id="eee56-248">Parametri</span><span class="sxs-lookup"><span data-stu-id="eee56-248">Parameters</span></span>

| <span data-ttu-id="eee56-249">Parametro</span><span class="sxs-lookup"><span data-stu-id="eee56-249">Parameter</span></span> | <span data-ttu-id="eee56-250">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="eee56-250">Required</span></span> | <span data-ttu-id="eee56-251">Tipo</span><span class="sxs-lookup"><span data-stu-id="eee56-251">Type</span></span> | <span data-ttu-id="eee56-252">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eee56-252">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="eee56-253">arg1</span><span class="sxs-lookup"><span data-stu-id="eee56-253">arg1</span></span> |<span data-ttu-id="eee56-254">Sì</span><span class="sxs-lookup"><span data-stu-id="eee56-254">Yes</span></span> |<span data-ttu-id="eee56-255">boolean</span><span class="sxs-lookup"><span data-stu-id="eee56-255">boolean</span></span> |<span data-ttu-id="eee56-256">Primo valore da controllare per verificare se è true.</span><span class="sxs-lookup"><span data-stu-id="eee56-256">The first value to check whether is true.</span></span> |
| <span data-ttu-id="eee56-257">arg2</span><span class="sxs-lookup"><span data-stu-id="eee56-257">arg2</span></span> |<span data-ttu-id="eee56-258">Sì</span><span class="sxs-lookup"><span data-stu-id="eee56-258">Yes</span></span> |<span data-ttu-id="eee56-259">boolean</span><span class="sxs-lookup"><span data-stu-id="eee56-259">boolean</span></span> |<span data-ttu-id="eee56-260">Secondo valore da controllare per verificare se è true.</span><span class="sxs-lookup"><span data-stu-id="eee56-260">The second value to check whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="eee56-261">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="eee56-261">Return value</span></span>

<span data-ttu-id="eee56-262">Restituisce **True** se uno dei due valori è true. In caso contrario, restituisce **False**.</span><span class="sxs-lookup"><span data-stu-id="eee56-262">Returns **True** if either value is true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="eee56-263">Esempi</span><span class="sxs-lookup"><span data-stu-id="eee56-263">Examples</span></span>

<span data-ttu-id="eee56-264">L'esempio seguente mostra come usare le funzioni logiche.</span><span class="sxs-lookup"><span data-stu-id="eee56-264">The following example shows how to use logical functions.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

<span data-ttu-id="eee56-265">L'output dell'esempio precedente è:</span><span class="sxs-lookup"><span data-stu-id="eee56-265">The output from the preceding example is:</span></span>

| <span data-ttu-id="eee56-266">Nome</span><span class="sxs-lookup"><span data-stu-id="eee56-266">Name</span></span> | <span data-ttu-id="eee56-267">Tipo</span><span class="sxs-lookup"><span data-stu-id="eee56-267">Type</span></span> | <span data-ttu-id="eee56-268">Valore</span><span class="sxs-lookup"><span data-stu-id="eee56-268">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="eee56-269">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="eee56-269">andExampleOutput</span></span> | <span data-ttu-id="eee56-270">Booleano</span><span class="sxs-lookup"><span data-stu-id="eee56-270">Bool</span></span> | <span data-ttu-id="eee56-271">False</span><span class="sxs-lookup"><span data-stu-id="eee56-271">False</span></span> |
| <span data-ttu-id="eee56-272">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="eee56-272">orExampleOutput</span></span> | <span data-ttu-id="eee56-273">Booleano</span><span class="sxs-lookup"><span data-stu-id="eee56-273">Bool</span></span> | <span data-ttu-id="eee56-274">True </span><span class="sxs-lookup"><span data-stu-id="eee56-274">True</span></span> |
| <span data-ttu-id="eee56-275">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="eee56-275">notExampleOutput</span></span> | <span data-ttu-id="eee56-276">Booleano</span><span class="sxs-lookup"><span data-stu-id="eee56-276">Bool</span></span> | <span data-ttu-id="eee56-277">False</span><span class="sxs-lookup"><span data-stu-id="eee56-277">False</span></span> |


## <a name="next-steps"></a><span data-ttu-id="eee56-278">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="eee56-278">Next steps</span></span>
* <span data-ttu-id="eee56-279">Per una descrizione delle sezioni in un modello di Azure Resource Manager, vedere [Creazione di modelli di Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="eee56-279">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="eee56-280">Per unire più modelli, vedere [Uso di modelli collegati con Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="eee56-280">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="eee56-281">Per eseguire un'iterazione di un numero di volte specificato durante la creazione di un tipo di risorsa, vedere [Creare più istanze di risorse in Gestione risorse di Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="eee56-281">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="eee56-282">Per informazioni su come distribuire il modello che è stato creato, vedere [Distribuire un'applicazione con un modello di Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="eee56-282">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

