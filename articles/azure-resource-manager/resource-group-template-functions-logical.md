---
title: aaaAzure Gestione risorse funzioni di modello - logiche | Documenti Microsoft
description: Viene descritto toouse funzioni hello in un valori logici di modello toodetermine Gestione risorse di Azure.
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
ms.openlocfilehash: aec6341fbde00b4eba3b4539ff9a9aec774333fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="logical-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="3823c-103">Funzioni logiche nei modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3823c-103">Logical functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="3823c-104">Resource Manager include numerose funzioni per l'esecuzione di confronti nei modelli.</span><span class="sxs-lookup"><span data-stu-id="3823c-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="3823c-105">and</span><span class="sxs-lookup"><span data-stu-id="3823c-105">and</span></span>](#and)
* [<span data-ttu-id="3823c-106">bool</span><span class="sxs-lookup"><span data-stu-id="3823c-106">bool</span></span>](#bool)
* [<span data-ttu-id="3823c-107">if</span><span class="sxs-lookup"><span data-stu-id="3823c-107">if</span></span>](#if)
* [<span data-ttu-id="3823c-108">not</span><span class="sxs-lookup"><span data-stu-id="3823c-108">not</span></span>](#not)
* [<span data-ttu-id="3823c-109">or</span><span class="sxs-lookup"><span data-stu-id="3823c-109">or</span></span>](#or)

## <a name="and"></a><span data-ttu-id="3823c-110">e</span><span class="sxs-lookup"><span data-stu-id="3823c-110">and</span></span>
`and(arg1, arg2)`

<span data-ttu-id="3823c-111">Controlla se i valori di entrambi i parametri sono true.</span><span class="sxs-lookup"><span data-stu-id="3823c-111">Checks whether both parameter values are true.</span></span>

### <a name="parameters"></a><span data-ttu-id="3823c-112">parameters</span><span class="sxs-lookup"><span data-stu-id="3823c-112">Parameters</span></span>

| <span data-ttu-id="3823c-113">Parametro</span><span class="sxs-lookup"><span data-stu-id="3823c-113">Parameter</span></span> | <span data-ttu-id="3823c-114">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="3823c-114">Required</span></span> | <span data-ttu-id="3823c-115">Tipo</span><span class="sxs-lookup"><span data-stu-id="3823c-115">Type</span></span> | <span data-ttu-id="3823c-116">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3823c-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3823c-117">arg1</span><span class="sxs-lookup"><span data-stu-id="3823c-117">arg1</span></span> |<span data-ttu-id="3823c-118">Sì</span><span class="sxs-lookup"><span data-stu-id="3823c-118">Yes</span></span> |<span data-ttu-id="3823c-119">boolean</span><span class="sxs-lookup"><span data-stu-id="3823c-119">boolean</span></span> |<span data-ttu-id="3823c-120">Hello toocheck valore primo se è true.</span><span class="sxs-lookup"><span data-stu-id="3823c-120">hello first value toocheck whether is true.</span></span> |
| <span data-ttu-id="3823c-121">arg2</span><span class="sxs-lookup"><span data-stu-id="3823c-121">arg2</span></span> |<span data-ttu-id="3823c-122">Sì</span><span class="sxs-lookup"><span data-stu-id="3823c-122">Yes</span></span> |<span data-ttu-id="3823c-123">boolean</span><span class="sxs-lookup"><span data-stu-id="3823c-123">boolean</span></span> |<span data-ttu-id="3823c-124">Hello toocheck valore secondo se è true.</span><span class="sxs-lookup"><span data-stu-id="3823c-124">hello second value toocheck whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="3823c-125">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="3823c-125">Return value</span></span>

<span data-ttu-id="3823c-126">Restituisce **True** se entrambi i valori sono true. In caso contrario, restituisce **False**.</span><span class="sxs-lookup"><span data-stu-id="3823c-126">Returns **True** if both values are true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="3823c-127">esempi</span><span class="sxs-lookup"><span data-stu-id="3823c-127">Examples</span></span>

<span data-ttu-id="3823c-128">Hello seguente esempio viene illustrato come le funzioni logiche toouse.</span><span class="sxs-lookup"><span data-stu-id="3823c-128">hello following example shows how toouse logical functions.</span></span>

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

<span data-ttu-id="3823c-129">output di Hello hello sopra riportato è:</span><span class="sxs-lookup"><span data-stu-id="3823c-129">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="3823c-130">Nome</span><span class="sxs-lookup"><span data-stu-id="3823c-130">Name</span></span> | <span data-ttu-id="3823c-131">Tipo</span><span class="sxs-lookup"><span data-stu-id="3823c-131">Type</span></span> | <span data-ttu-id="3823c-132">Valore</span><span class="sxs-lookup"><span data-stu-id="3823c-132">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="3823c-133">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="3823c-133">andExampleOutput</span></span> | <span data-ttu-id="3823c-134">Booleano</span><span class="sxs-lookup"><span data-stu-id="3823c-134">Bool</span></span> | <span data-ttu-id="3823c-135">False</span><span class="sxs-lookup"><span data-stu-id="3823c-135">False</span></span> |
| <span data-ttu-id="3823c-136">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="3823c-136">orExampleOutput</span></span> | <span data-ttu-id="3823c-137">Booleano</span><span class="sxs-lookup"><span data-stu-id="3823c-137">Bool</span></span> | <span data-ttu-id="3823c-138">True </span><span class="sxs-lookup"><span data-stu-id="3823c-138">True</span></span> |
| <span data-ttu-id="3823c-139">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="3823c-139">notExampleOutput</span></span> | <span data-ttu-id="3823c-140">Booleano</span><span class="sxs-lookup"><span data-stu-id="3823c-140">Bool</span></span> | <span data-ttu-id="3823c-141">False</span><span class="sxs-lookup"><span data-stu-id="3823c-141">False</span></span> |


## <a name="bool"></a><span data-ttu-id="3823c-142">bool</span><span class="sxs-lookup"><span data-stu-id="3823c-142">bool</span></span>
`bool(arg1)`

<span data-ttu-id="3823c-143">Converte hello tooa parametro booleano.</span><span class="sxs-lookup"><span data-stu-id="3823c-143">Converts hello parameter tooa boolean.</span></span>

### <a name="parameters"></a><span data-ttu-id="3823c-144">parameters</span><span class="sxs-lookup"><span data-stu-id="3823c-144">Parameters</span></span>

| <span data-ttu-id="3823c-145">Parametro</span><span class="sxs-lookup"><span data-stu-id="3823c-145">Parameter</span></span> | <span data-ttu-id="3823c-146">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="3823c-146">Required</span></span> | <span data-ttu-id="3823c-147">Tipo</span><span class="sxs-lookup"><span data-stu-id="3823c-147">Type</span></span> | <span data-ttu-id="3823c-148">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3823c-148">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3823c-149">arg1</span><span class="sxs-lookup"><span data-stu-id="3823c-149">arg1</span></span> |<span data-ttu-id="3823c-150">Sì</span><span class="sxs-lookup"><span data-stu-id="3823c-150">Yes</span></span> |<span data-ttu-id="3823c-151">stringa o numero intero</span><span class="sxs-lookup"><span data-stu-id="3823c-151">string or int</span></span> |<span data-ttu-id="3823c-152">Hello tooa tooconvert valore booleano.</span><span class="sxs-lookup"><span data-stu-id="3823c-152">hello value tooconvert tooa boolean.</span></span> |

### <a name="return-value"></a><span data-ttu-id="3823c-153">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="3823c-153">Return value</span></span>
<span data-ttu-id="3823c-154">Un valore booleano di hello valore convertito.</span><span class="sxs-lookup"><span data-stu-id="3823c-154">A boolean of hello converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="3823c-155">esempi</span><span class="sxs-lookup"><span data-stu-id="3823c-155">Examples</span></span>

<span data-ttu-id="3823c-156">Hello seguente esempio viene illustrato come toouse bool con un numero intero o stringa.</span><span class="sxs-lookup"><span data-stu-id="3823c-156">hello following example shows how toouse bool with a string or integer.</span></span>

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

<span data-ttu-id="3823c-157">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="3823c-157">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="3823c-158">Nome</span><span class="sxs-lookup"><span data-stu-id="3823c-158">Name</span></span> | <span data-ttu-id="3823c-159">Tipo</span><span class="sxs-lookup"><span data-stu-id="3823c-159">Type</span></span> | <span data-ttu-id="3823c-160">Valore</span><span class="sxs-lookup"><span data-stu-id="3823c-160">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="3823c-161">trueString</span><span class="sxs-lookup"><span data-stu-id="3823c-161">trueString</span></span> | <span data-ttu-id="3823c-162">Booleano</span><span class="sxs-lookup"><span data-stu-id="3823c-162">Bool</span></span> | <span data-ttu-id="3823c-163">True </span><span class="sxs-lookup"><span data-stu-id="3823c-163">True</span></span> |
| <span data-ttu-id="3823c-164">falseString</span><span class="sxs-lookup"><span data-stu-id="3823c-164">falseString</span></span> | <span data-ttu-id="3823c-165">Booleano</span><span class="sxs-lookup"><span data-stu-id="3823c-165">Bool</span></span> | <span data-ttu-id="3823c-166">False</span><span class="sxs-lookup"><span data-stu-id="3823c-166">False</span></span> |
| <span data-ttu-id="3823c-167">trueInt</span><span class="sxs-lookup"><span data-stu-id="3823c-167">trueInt</span></span> | <span data-ttu-id="3823c-168">Booleano</span><span class="sxs-lookup"><span data-stu-id="3823c-168">Bool</span></span> | <span data-ttu-id="3823c-169">True </span><span class="sxs-lookup"><span data-stu-id="3823c-169">True</span></span> |
| <span data-ttu-id="3823c-170">falseInt</span><span class="sxs-lookup"><span data-stu-id="3823c-170">falseInt</span></span> | <span data-ttu-id="3823c-171">Booleano</span><span class="sxs-lookup"><span data-stu-id="3823c-171">Bool</span></span> | <span data-ttu-id="3823c-172">False</span><span class="sxs-lookup"><span data-stu-id="3823c-172">False</span></span> |

## <a name="if"></a><span data-ttu-id="3823c-173">if</span><span class="sxs-lookup"><span data-stu-id="3823c-173">if</span></span>
`if(condition, trueValue, falseValue)`

<span data-ttu-id="3823c-174">Restituisce un valore in base a un condizione true o false.</span><span class="sxs-lookup"><span data-stu-id="3823c-174">Returns a value based on whether a condition is true or false.</span></span>

### <a name="parameters"></a><span data-ttu-id="3823c-175">Parametri</span><span class="sxs-lookup"><span data-stu-id="3823c-175">Parameters</span></span>

| <span data-ttu-id="3823c-176">Parametro</span><span class="sxs-lookup"><span data-stu-id="3823c-176">Parameter</span></span> | <span data-ttu-id="3823c-177">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="3823c-177">Required</span></span> | <span data-ttu-id="3823c-178">Tipo</span><span class="sxs-lookup"><span data-stu-id="3823c-178">Type</span></span> | <span data-ttu-id="3823c-179">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3823c-179">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3823c-180">condition</span><span class="sxs-lookup"><span data-stu-id="3823c-180">condition</span></span> |<span data-ttu-id="3823c-181">Sì</span><span class="sxs-lookup"><span data-stu-id="3823c-181">Yes</span></span> |<span data-ttu-id="3823c-182">boolean</span><span class="sxs-lookup"><span data-stu-id="3823c-182">boolean</span></span> |<span data-ttu-id="3823c-183">Hello toocheck valore se è true.</span><span class="sxs-lookup"><span data-stu-id="3823c-183">hello value toocheck whether it is true.</span></span> |
| <span data-ttu-id="3823c-184">trueValue</span><span class="sxs-lookup"><span data-stu-id="3823c-184">trueValue</span></span> |<span data-ttu-id="3823c-185">Sì</span><span class="sxs-lookup"><span data-stu-id="3823c-185">Yes</span></span> | <span data-ttu-id="3823c-186">string, int, object o array</span><span class="sxs-lookup"><span data-stu-id="3823c-186">string, int, object, or array</span></span> |<span data-ttu-id="3823c-187">valore di Hello tooreturn quando hello condizione è true.</span><span class="sxs-lookup"><span data-stu-id="3823c-187">hello value tooreturn when hello condition is true.</span></span> |
| <span data-ttu-id="3823c-188">falseValue</span><span class="sxs-lookup"><span data-stu-id="3823c-188">falseValue</span></span> |<span data-ttu-id="3823c-189">Sì</span><span class="sxs-lookup"><span data-stu-id="3823c-189">Yes</span></span> | <span data-ttu-id="3823c-190">string, int, object o array</span><span class="sxs-lookup"><span data-stu-id="3823c-190">string, int, object, or array</span></span> |<span data-ttu-id="3823c-191">valore di Hello tooreturn quando hello condizione è false.</span><span class="sxs-lookup"><span data-stu-id="3823c-191">hello value tooreturn when hello condition is false.</span></span> |

### <a name="return-value"></a><span data-ttu-id="3823c-192">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="3823c-192">Return value</span></span>

<span data-ttu-id="3823c-193">Restituisce il secondo parametro, quando il primo parametro è **True**. In caso contrario, restituisce il terzo parametro.</span><span class="sxs-lookup"><span data-stu-id="3823c-193">Returns second parameter when first parameter is **True**; otherwise, returns third parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="3823c-194">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="3823c-194">Remarks</span></span>

<span data-ttu-id="3823c-195">È possibile utilizzare questo set di funzioni tooconditionally una proprietà della risorsa.</span><span class="sxs-lookup"><span data-stu-id="3823c-195">You can use this function tooconditionally set a resource property.</span></span> <span data-ttu-id="3823c-196">Hello seguente non è un modello completo, ma visualizza parti pertinenti di hello per l'impostazione di set di disponibilità hello in modo condizionale.</span><span class="sxs-lookup"><span data-stu-id="3823c-196">hello following example is not a full template, but it shows hello relevant portions for conditionally setting hello availability set.</span></span>

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

### <a name="examples"></a><span data-ttu-id="3823c-197">esempi</span><span class="sxs-lookup"><span data-stu-id="3823c-197">Examples</span></span>

<span data-ttu-id="3823c-198">Hello seguente esempio viene illustrato come hello toouse `if` (funzione).</span><span class="sxs-lookup"><span data-stu-id="3823c-198">hello following example shows how toouse hello `if` function.</span></span>

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

<span data-ttu-id="3823c-199">output di Hello hello sopra riportato è:</span><span class="sxs-lookup"><span data-stu-id="3823c-199">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="3823c-200">Nome</span><span class="sxs-lookup"><span data-stu-id="3823c-200">Name</span></span> | <span data-ttu-id="3823c-201">Tipo</span><span class="sxs-lookup"><span data-stu-id="3823c-201">Type</span></span> | <span data-ttu-id="3823c-202">Valore</span><span class="sxs-lookup"><span data-stu-id="3823c-202">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="3823c-203">yesOutput</span><span class="sxs-lookup"><span data-stu-id="3823c-203">yesOutput</span></span> | <span data-ttu-id="3823c-204">String</span><span class="sxs-lookup"><span data-stu-id="3823c-204">String</span></span> | <span data-ttu-id="3823c-205">sì</span><span class="sxs-lookup"><span data-stu-id="3823c-205">yes</span></span> |
| <span data-ttu-id="3823c-206">noOutput</span><span class="sxs-lookup"><span data-stu-id="3823c-206">noOutput</span></span> | <span data-ttu-id="3823c-207">String</span><span class="sxs-lookup"><span data-stu-id="3823c-207">String</span></span> | <span data-ttu-id="3823c-208">no</span><span class="sxs-lookup"><span data-stu-id="3823c-208">no</span></span> |


## <a name="not"></a><span data-ttu-id="3823c-209">not</span><span class="sxs-lookup"><span data-stu-id="3823c-209">not</span></span>
`not(arg1)`

<span data-ttu-id="3823c-210">Converte un valore booleano tooits opposto valore.</span><span class="sxs-lookup"><span data-stu-id="3823c-210">Converts boolean value tooits opposite value.</span></span>

### <a name="parameters"></a><span data-ttu-id="3823c-211">parameters</span><span class="sxs-lookup"><span data-stu-id="3823c-211">Parameters</span></span>

| <span data-ttu-id="3823c-212">Parametro</span><span class="sxs-lookup"><span data-stu-id="3823c-212">Parameter</span></span> | <span data-ttu-id="3823c-213">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="3823c-213">Required</span></span> | <span data-ttu-id="3823c-214">Tipo</span><span class="sxs-lookup"><span data-stu-id="3823c-214">Type</span></span> | <span data-ttu-id="3823c-215">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3823c-215">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3823c-216">arg1</span><span class="sxs-lookup"><span data-stu-id="3823c-216">arg1</span></span> |<span data-ttu-id="3823c-217">Sì</span><span class="sxs-lookup"><span data-stu-id="3823c-217">Yes</span></span> |<span data-ttu-id="3823c-218">boolean</span><span class="sxs-lookup"><span data-stu-id="3823c-218">boolean</span></span> |<span data-ttu-id="3823c-219">tooconvert valore Hello.</span><span class="sxs-lookup"><span data-stu-id="3823c-219">hello value tooconvert.</span></span> |


### <a name="return-value"></a><span data-ttu-id="3823c-220">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="3823c-220">Return value</span></span>

<span data-ttu-id="3823c-221">Restituisce **True** quando il parametro è **False**.</span><span class="sxs-lookup"><span data-stu-id="3823c-221">Returns **True** when parameter is **False**.</span></span> <span data-ttu-id="3823c-222">Restituisce **False** quando il parametro è **True**.</span><span class="sxs-lookup"><span data-stu-id="3823c-222">Returns **False** when parameter is **True**.</span></span>

### <a name="examples"></a><span data-ttu-id="3823c-223">esempi</span><span class="sxs-lookup"><span data-stu-id="3823c-223">Examples</span></span>

<span data-ttu-id="3823c-224">Hello seguente esempio viene illustrato come le funzioni logiche toouse.</span><span class="sxs-lookup"><span data-stu-id="3823c-224">hello following example shows how toouse logical functions.</span></span>

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

<span data-ttu-id="3823c-225">output di Hello hello sopra riportato è:</span><span class="sxs-lookup"><span data-stu-id="3823c-225">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="3823c-226">Nome</span><span class="sxs-lookup"><span data-stu-id="3823c-226">Name</span></span> | <span data-ttu-id="3823c-227">Tipo</span><span class="sxs-lookup"><span data-stu-id="3823c-227">Type</span></span> | <span data-ttu-id="3823c-228">Valore</span><span class="sxs-lookup"><span data-stu-id="3823c-228">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="3823c-229">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="3823c-229">andExampleOutput</span></span> | <span data-ttu-id="3823c-230">Booleano</span><span class="sxs-lookup"><span data-stu-id="3823c-230">Bool</span></span> | <span data-ttu-id="3823c-231">False</span><span class="sxs-lookup"><span data-stu-id="3823c-231">False</span></span> |
| <span data-ttu-id="3823c-232">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="3823c-232">orExampleOutput</span></span> | <span data-ttu-id="3823c-233">Booleano</span><span class="sxs-lookup"><span data-stu-id="3823c-233">Bool</span></span> | <span data-ttu-id="3823c-234">True </span><span class="sxs-lookup"><span data-stu-id="3823c-234">True</span></span> |
| <span data-ttu-id="3823c-235">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="3823c-235">notExampleOutput</span></span> | <span data-ttu-id="3823c-236">Booleano</span><span class="sxs-lookup"><span data-stu-id="3823c-236">Bool</span></span> | <span data-ttu-id="3823c-237">False</span><span class="sxs-lookup"><span data-stu-id="3823c-237">False</span></span> |

<span data-ttu-id="3823c-238">Hello seguente utilizza **non** con [è uguale a](resource-group-template-functions-comparison.md#equals).</span><span class="sxs-lookup"><span data-stu-id="3823c-238">hello following example uses **not** with [equals](resource-group-template-functions-comparison.md#equals).</span></span>

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

<span data-ttu-id="3823c-239">output di Hello hello sopra riportato è:</span><span class="sxs-lookup"><span data-stu-id="3823c-239">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="3823c-240">Nome</span><span class="sxs-lookup"><span data-stu-id="3823c-240">Name</span></span> | <span data-ttu-id="3823c-241">Tipo</span><span class="sxs-lookup"><span data-stu-id="3823c-241">Type</span></span> | <span data-ttu-id="3823c-242">Valore</span><span class="sxs-lookup"><span data-stu-id="3823c-242">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="3823c-243">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="3823c-243">checkNotEquals</span></span> | <span data-ttu-id="3823c-244">Booleano</span><span class="sxs-lookup"><span data-stu-id="3823c-244">Bool</span></span> | <span data-ttu-id="3823c-245">True </span><span class="sxs-lookup"><span data-stu-id="3823c-245">True</span></span> |


## <a name="or"></a><span data-ttu-id="3823c-246">oppure</span><span class="sxs-lookup"><span data-stu-id="3823c-246">or</span></span>
`or(arg1, arg2)`

<span data-ttu-id="3823c-247">Controlla se il valore di uno dei due parametri è true.</span><span class="sxs-lookup"><span data-stu-id="3823c-247">Checks whether either parameter value is true.</span></span>

### <a name="parameters"></a><span data-ttu-id="3823c-248">Parametri</span><span class="sxs-lookup"><span data-stu-id="3823c-248">Parameters</span></span>

| <span data-ttu-id="3823c-249">Parametro</span><span class="sxs-lookup"><span data-stu-id="3823c-249">Parameter</span></span> | <span data-ttu-id="3823c-250">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="3823c-250">Required</span></span> | <span data-ttu-id="3823c-251">Tipo</span><span class="sxs-lookup"><span data-stu-id="3823c-251">Type</span></span> | <span data-ttu-id="3823c-252">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3823c-252">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3823c-253">arg1</span><span class="sxs-lookup"><span data-stu-id="3823c-253">arg1</span></span> |<span data-ttu-id="3823c-254">Sì</span><span class="sxs-lookup"><span data-stu-id="3823c-254">Yes</span></span> |<span data-ttu-id="3823c-255">boolean</span><span class="sxs-lookup"><span data-stu-id="3823c-255">boolean</span></span> |<span data-ttu-id="3823c-256">Hello toocheck valore primo se è true.</span><span class="sxs-lookup"><span data-stu-id="3823c-256">hello first value toocheck whether is true.</span></span> |
| <span data-ttu-id="3823c-257">arg2</span><span class="sxs-lookup"><span data-stu-id="3823c-257">arg2</span></span> |<span data-ttu-id="3823c-258">Sì</span><span class="sxs-lookup"><span data-stu-id="3823c-258">Yes</span></span> |<span data-ttu-id="3823c-259">boolean</span><span class="sxs-lookup"><span data-stu-id="3823c-259">boolean</span></span> |<span data-ttu-id="3823c-260">Hello toocheck valore secondo se è true.</span><span class="sxs-lookup"><span data-stu-id="3823c-260">hello second value toocheck whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="3823c-261">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="3823c-261">Return value</span></span>

<span data-ttu-id="3823c-262">Restituisce **True** se uno dei due valori è true. In caso contrario, restituisce **False**.</span><span class="sxs-lookup"><span data-stu-id="3823c-262">Returns **True** if either value is true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="3823c-263">esempi</span><span class="sxs-lookup"><span data-stu-id="3823c-263">Examples</span></span>

<span data-ttu-id="3823c-264">Hello seguente esempio viene illustrato come le funzioni logiche toouse.</span><span class="sxs-lookup"><span data-stu-id="3823c-264">hello following example shows how toouse logical functions.</span></span>

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

<span data-ttu-id="3823c-265">output di Hello hello sopra riportato è:</span><span class="sxs-lookup"><span data-stu-id="3823c-265">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="3823c-266">Nome</span><span class="sxs-lookup"><span data-stu-id="3823c-266">Name</span></span> | <span data-ttu-id="3823c-267">Tipo</span><span class="sxs-lookup"><span data-stu-id="3823c-267">Type</span></span> | <span data-ttu-id="3823c-268">Valore</span><span class="sxs-lookup"><span data-stu-id="3823c-268">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="3823c-269">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="3823c-269">andExampleOutput</span></span> | <span data-ttu-id="3823c-270">Booleano</span><span class="sxs-lookup"><span data-stu-id="3823c-270">Bool</span></span> | <span data-ttu-id="3823c-271">False</span><span class="sxs-lookup"><span data-stu-id="3823c-271">False</span></span> |
| <span data-ttu-id="3823c-272">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="3823c-272">orExampleOutput</span></span> | <span data-ttu-id="3823c-273">Booleano</span><span class="sxs-lookup"><span data-stu-id="3823c-273">Bool</span></span> | <span data-ttu-id="3823c-274">True </span><span class="sxs-lookup"><span data-stu-id="3823c-274">True</span></span> |
| <span data-ttu-id="3823c-275">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="3823c-275">notExampleOutput</span></span> | <span data-ttu-id="3823c-276">Booleano</span><span class="sxs-lookup"><span data-stu-id="3823c-276">Bool</span></span> | <span data-ttu-id="3823c-277">False</span><span class="sxs-lookup"><span data-stu-id="3823c-277">False</span></span> |


## <a name="next-steps"></a><span data-ttu-id="3823c-278">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3823c-278">Next steps</span></span>
* <span data-ttu-id="3823c-279">Per una descrizione delle sezioni hello in un modello di gestione risorse di Azure, vedere [modelli Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="3823c-279">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="3823c-280">toomerge più modelli, vedere [con modelli collegati con Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="3823c-280">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="3823c-281">tooiterate un numero specificato di volte durante la creazione di un tipo di risorsa, vedere [creare più istanze delle risorse in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="3823c-281">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="3823c-282">toosee come modello hello toodeploy è stato creato, vedere [distribuire un'applicazione con il modello di gestione risorse di Azure](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="3823c-282">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

