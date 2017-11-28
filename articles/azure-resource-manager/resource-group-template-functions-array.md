---
title: 'modello di gestione risorse aaaAzure funzioni: le matrici e oggetti | Documenti Microsoft'
description: Viene descritto toouse funzioni hello in un modello di gestione risorse di Azure per l'utilizzo di matrici e oggetti.
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
ms.date: 06/12/2017
ms.author: tomfitz
ms.openlocfilehash: e5f1a9b2a71039562eae7e48c2474a1fa59a7bea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="array-and-object-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="20d87-103">Funzioni di matrice e oggetto per i modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="20d87-103">Array and object functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="20d87-104">Resource Manager offre diverse funzioni per l'uso di matrici e oggetti.</span><span class="sxs-lookup"><span data-stu-id="20d87-104">Resource Manager provides several functions for working with arrays and objects.</span></span>

* [<span data-ttu-id="20d87-105">array</span><span class="sxs-lookup"><span data-stu-id="20d87-105">array</span></span>](#array)
* [<span data-ttu-id="20d87-106">coalesce</span><span class="sxs-lookup"><span data-stu-id="20d87-106">coalesce</span></span>](#coalesce)
* [<span data-ttu-id="20d87-107">concat</span><span class="sxs-lookup"><span data-stu-id="20d87-107">concat</span></span>](#concat)
* [<span data-ttu-id="20d87-108">contains</span><span class="sxs-lookup"><span data-stu-id="20d87-108">contains</span></span>](#contains)
* [<span data-ttu-id="20d87-109">createArray</span><span class="sxs-lookup"><span data-stu-id="20d87-109">createArray</span></span>](#createarray)
* [<span data-ttu-id="20d87-110">empty</span><span class="sxs-lookup"><span data-stu-id="20d87-110">empty</span></span>](#empty)
* [<span data-ttu-id="20d87-111">first</span><span class="sxs-lookup"><span data-stu-id="20d87-111">first</span></span>](#first)
* [<span data-ttu-id="20d87-112">intersection</span><span class="sxs-lookup"><span data-stu-id="20d87-112">intersection</span></span>](#intersection)
* [<span data-ttu-id="20d87-113">json</span><span class="sxs-lookup"><span data-stu-id="20d87-113">json</span></span>](#json)
* [<span data-ttu-id="20d87-114">last</span><span class="sxs-lookup"><span data-stu-id="20d87-114">last</span></span>](#last)
* [<span data-ttu-id="20d87-115">length</span><span class="sxs-lookup"><span data-stu-id="20d87-115">length</span></span>](#length)
* [<span data-ttu-id="20d87-116">min</span><span class="sxs-lookup"><span data-stu-id="20d87-116">min</span></span>](#min)
* [<span data-ttu-id="20d87-117">max</span><span class="sxs-lookup"><span data-stu-id="20d87-117">max</span></span>](#max)
* [<span data-ttu-id="20d87-118">range</span><span class="sxs-lookup"><span data-stu-id="20d87-118">range</span></span>](#range)
* [<span data-ttu-id="20d87-119">skip</span><span class="sxs-lookup"><span data-stu-id="20d87-119">skip</span></span>](#skip)
* [<span data-ttu-id="20d87-120">take</span><span class="sxs-lookup"><span data-stu-id="20d87-120">take</span></span>](#take)
* [<span data-ttu-id="20d87-121">union</span><span class="sxs-lookup"><span data-stu-id="20d87-121">union</span></span>](#union)

<span data-ttu-id="20d87-122">tooget una matrice di valori di stringa delimitata da un valore, vedere [dividere](resource-group-template-functions-string.md#split).</span><span class="sxs-lookup"><span data-stu-id="20d87-122">tooget an array of string values delimited by a value, see [split](resource-group-template-functions-string.md#split).</span></span>

<a id="array" />

## <a name="array"></a><span data-ttu-id="20d87-123">array</span><span class="sxs-lookup"><span data-stu-id="20d87-123">array</span></span>
`array(convertToArray)`

<span data-ttu-id="20d87-124">Converte una matrice di tooan valori hello.</span><span class="sxs-lookup"><span data-stu-id="20d87-124">Converts hello value tooan array.</span></span>

### <a name="parameters"></a><span data-ttu-id="20d87-125">parameters</span><span class="sxs-lookup"><span data-stu-id="20d87-125">Parameters</span></span>

| <span data-ttu-id="20d87-126">Parametro</span><span class="sxs-lookup"><span data-stu-id="20d87-126">Parameter</span></span> | <span data-ttu-id="20d87-127">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="20d87-127">Required</span></span> | <span data-ttu-id="20d87-128">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-128">Type</span></span> | <span data-ttu-id="20d87-129">Descrizione</span><span class="sxs-lookup"><span data-stu-id="20d87-129">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="20d87-130">convertToArray</span><span class="sxs-lookup"><span data-stu-id="20d87-130">convertToArray</span></span> |<span data-ttu-id="20d87-131">Sì</span><span class="sxs-lookup"><span data-stu-id="20d87-131">Yes</span></span> |<span data-ttu-id="20d87-132">int, stringa, matrice o oggetto</span><span class="sxs-lookup"><span data-stu-id="20d87-132">int, string, array, or object</span></span> |<span data-ttu-id="20d87-133">Matrice di tooan tooconvert valori Hello.</span><span class="sxs-lookup"><span data-stu-id="20d87-133">hello value tooconvert tooan array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="20d87-134">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="20d87-134">Return value</span></span>

<span data-ttu-id="20d87-135">Una matrice.</span><span class="sxs-lookup"><span data-stu-id="20d87-135">An array.</span></span>

### <a name="example"></a><span data-ttu-id="20d87-136">Esempio</span><span class="sxs-lookup"><span data-stu-id="20d87-136">Example</span></span>

<span data-ttu-id="20d87-137">Hello esempio seguente viene illustrato come toouse hello funzione matrice con tipi diversi.</span><span class="sxs-lookup"><span data-stu-id="20d87-137">hello following example shows how toouse hello array function with different types.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "intToConvert": {
            "type": "int",
            "defaultValue": 1
        },
        "stringToConvert": {
            "type": "string",
            "defaultValue": "a"
        },
        "objectToConvert": {
            "type": "object",
            "defaultValue": {"a": "b", "c": "d"}
        }
    },
    "resources": [
    ],
    "outputs": {
        "intOutput": {
            "type": "array",
            "value": "[array(parameters('intToConvert'))]"
        },
        "stringOutput": {
            "type": "array",
            "value": "[array(parameters('stringToConvert'))]"
        },
        "objectOutput": {
            "type": "array",
            "value": "[array(parameters('objectToConvert'))]"
        }
    }
}
```

<span data-ttu-id="20d87-138">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="20d87-138">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="20d87-139">Nome</span><span class="sxs-lookup"><span data-stu-id="20d87-139">Name</span></span> | <span data-ttu-id="20d87-140">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-140">Type</span></span> | <span data-ttu-id="20d87-141">Valore</span><span class="sxs-lookup"><span data-stu-id="20d87-141">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="20d87-142">intOutput</span><span class="sxs-lookup"><span data-stu-id="20d87-142">intOutput</span></span> | <span data-ttu-id="20d87-143">Array</span><span class="sxs-lookup"><span data-stu-id="20d87-143">Array</span></span> | <span data-ttu-id="20d87-144">[1]</span><span class="sxs-lookup"><span data-stu-id="20d87-144">[1]</span></span> |
| <span data-ttu-id="20d87-145">stringOutput</span><span class="sxs-lookup"><span data-stu-id="20d87-145">stringOutput</span></span> | <span data-ttu-id="20d87-146">Array</span><span class="sxs-lookup"><span data-stu-id="20d87-146">Array</span></span> | <span data-ttu-id="20d87-147">["a"]</span><span class="sxs-lookup"><span data-stu-id="20d87-147">["a"]</span></span> |
| <span data-ttu-id="20d87-148">objectOutput</span><span class="sxs-lookup"><span data-stu-id="20d87-148">objectOutput</span></span> | <span data-ttu-id="20d87-149">Array</span><span class="sxs-lookup"><span data-stu-id="20d87-149">Array</span></span> | <span data-ttu-id="20d87-150">[{"a": "b", "c": "d"}]</span><span class="sxs-lookup"><span data-stu-id="20d87-150">[{"a": "b", "c": "d"}]</span></span> |

<a id="coalesce" />

## <a name="coalesce"></a><span data-ttu-id="20d87-151">coalesce</span><span class="sxs-lookup"><span data-stu-id="20d87-151">coalesce</span></span>
`coalesce(arg1, arg2, arg3, ...)`

<span data-ttu-id="20d87-152">Restituisce i valori non null prima dai parametri hello.</span><span class="sxs-lookup"><span data-stu-id="20d87-152">Returns first non-null value from hello parameters.</span></span> <span data-ttu-id="20d87-153">Stringhe vuote, matrici vuote e oggetti vuoti sono non null.</span><span class="sxs-lookup"><span data-stu-id="20d87-153">Empty strings, empty arrays, and empty objects are not null.</span></span>

### <a name="parameters"></a><span data-ttu-id="20d87-154">Parametri</span><span class="sxs-lookup"><span data-stu-id="20d87-154">Parameters</span></span>

| <span data-ttu-id="20d87-155">Parametro</span><span class="sxs-lookup"><span data-stu-id="20d87-155">Parameter</span></span> | <span data-ttu-id="20d87-156">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="20d87-156">Required</span></span> | <span data-ttu-id="20d87-157">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-157">Type</span></span> | <span data-ttu-id="20d87-158">Descrizione</span><span class="sxs-lookup"><span data-stu-id="20d87-158">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="20d87-159">arg1</span><span class="sxs-lookup"><span data-stu-id="20d87-159">arg1</span></span> |<span data-ttu-id="20d87-160">Sì</span><span class="sxs-lookup"><span data-stu-id="20d87-160">Yes</span></span> |<span data-ttu-id="20d87-161">int, stringa, matrice o oggetto</span><span class="sxs-lookup"><span data-stu-id="20d87-161">int, string, array, or object</span></span> |<span data-ttu-id="20d87-162">Hello tootest prima di valore per i valori null.</span><span class="sxs-lookup"><span data-stu-id="20d87-162">hello first value tootest for null.</span></span> |
| <span data-ttu-id="20d87-163">argomenti aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="20d87-163">additional args</span></span> |<span data-ttu-id="20d87-164">No</span><span class="sxs-lookup"><span data-stu-id="20d87-164">No</span></span> |<span data-ttu-id="20d87-165">int, stringa, matrice o oggetto</span><span class="sxs-lookup"><span data-stu-id="20d87-165">int, string, array, or object</span></span> |<span data-ttu-id="20d87-166">Tootest valori aggiuntivi per i valori null.</span><span class="sxs-lookup"><span data-stu-id="20d87-166">Additional values tootest for null.</span></span> |

### <a name="return-value"></a><span data-ttu-id="20d87-167">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="20d87-167">Return value</span></span>

<span data-ttu-id="20d87-168">valore di Hello dei parametri non null prima hello, che può essere una stringa, int, una matrice o un oggetto.</span><span class="sxs-lookup"><span data-stu-id="20d87-168">hello value of hello first non-null parameters, which can be a string, int, array, or object.</span></span> <span data-ttu-id="20d87-169">Null se tutti i parametri sono null.</span><span class="sxs-lookup"><span data-stu-id="20d87-169">Null if all parameters are null.</span></span> 

### <a name="example"></a><span data-ttu-id="20d87-170">Esempio</span><span class="sxs-lookup"><span data-stu-id="20d87-170">Example</span></span>

<span data-ttu-id="20d87-171">Hello seguente esempio Mostra output di hello da diversi utilizzi di coalesce.</span><span class="sxs-lookup"><span data-stu-id="20d87-171">hello following example shows hello output from different uses of coalesce.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "objectToTest": {
            "type": "object",
            "defaultValue": {
                "null1": null, 
                "null2": null,
                "string": "default",
                "int": 1,
                "object": {"first": "default"},
                "array": [1]
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringOutput": {
            "type": "string",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').string)]"
        },
        "intOutput": {
            "type": "int",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').int)]"
        },
        "objectOutput": {
            "type": "object",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').object)]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').array)]"
        },
        "emptyOutput": {
            "type": "bool",
            "value": "[empty(coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2))]"
        }
    }
}
```

<span data-ttu-id="20d87-172">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="20d87-172">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="20d87-173">Nome</span><span class="sxs-lookup"><span data-stu-id="20d87-173">Name</span></span> | <span data-ttu-id="20d87-174">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-174">Type</span></span> | <span data-ttu-id="20d87-175">Valore</span><span class="sxs-lookup"><span data-stu-id="20d87-175">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="20d87-176">stringOutput</span><span class="sxs-lookup"><span data-stu-id="20d87-176">stringOutput</span></span> | <span data-ttu-id="20d87-177">String</span><span class="sxs-lookup"><span data-stu-id="20d87-177">String</span></span> | <span data-ttu-id="20d87-178">default</span><span class="sxs-lookup"><span data-stu-id="20d87-178">default</span></span> |
| <span data-ttu-id="20d87-179">intOutput</span><span class="sxs-lookup"><span data-stu-id="20d87-179">intOutput</span></span> | <span data-ttu-id="20d87-180">int</span><span class="sxs-lookup"><span data-stu-id="20d87-180">Int</span></span> | <span data-ttu-id="20d87-181">1</span><span class="sxs-lookup"><span data-stu-id="20d87-181">1</span></span> |
| <span data-ttu-id="20d87-182">objectOutput</span><span class="sxs-lookup"><span data-stu-id="20d87-182">objectOutput</span></span> | <span data-ttu-id="20d87-183">Oggetto</span><span class="sxs-lookup"><span data-stu-id="20d87-183">Object</span></span> | <span data-ttu-id="20d87-184">{"first": "default"}</span><span class="sxs-lookup"><span data-stu-id="20d87-184">{"first": "default"}</span></span> |
| <span data-ttu-id="20d87-185">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="20d87-185">arrayOutput</span></span> | <span data-ttu-id="20d87-186">Array</span><span class="sxs-lookup"><span data-stu-id="20d87-186">Array</span></span> | <span data-ttu-id="20d87-187">[1]</span><span class="sxs-lookup"><span data-stu-id="20d87-187">[1]</span></span> |
| <span data-ttu-id="20d87-188">emptyOutput</span><span class="sxs-lookup"><span data-stu-id="20d87-188">emptyOutput</span></span> | <span data-ttu-id="20d87-189">Booleano</span><span class="sxs-lookup"><span data-stu-id="20d87-189">Bool</span></span> | <span data-ttu-id="20d87-190">True </span><span class="sxs-lookup"><span data-stu-id="20d87-190">True</span></span> |

<a id="concat" />

## <a name="concat"></a><span data-ttu-id="20d87-191">concat</span><span class="sxs-lookup"><span data-stu-id="20d87-191">concat</span></span>
`concat(arg1, arg2, arg3, ...)`

<span data-ttu-id="20d87-192">Combina più matrici e restituisce una matrice, hello concatenato o combina più valori di stringa e restituisce la stringa hello concatenato.</span><span class="sxs-lookup"><span data-stu-id="20d87-192">Combines multiple arrays and returns hello concatenated array, or combines multiple string values and returns hello concatenated string.</span></span> 

### <a name="parameters"></a><span data-ttu-id="20d87-193">parameters</span><span class="sxs-lookup"><span data-stu-id="20d87-193">Parameters</span></span>

| <span data-ttu-id="20d87-194">Parametro</span><span class="sxs-lookup"><span data-stu-id="20d87-194">Parameter</span></span> | <span data-ttu-id="20d87-195">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="20d87-195">Required</span></span> | <span data-ttu-id="20d87-196">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-196">Type</span></span> | <span data-ttu-id="20d87-197">Descrizione</span><span class="sxs-lookup"><span data-stu-id="20d87-197">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="20d87-198">arg1</span><span class="sxs-lookup"><span data-stu-id="20d87-198">arg1</span></span> |<span data-ttu-id="20d87-199">Sì</span><span class="sxs-lookup"><span data-stu-id="20d87-199">Yes</span></span> |<span data-ttu-id="20d87-200">stringa o matrice</span><span class="sxs-lookup"><span data-stu-id="20d87-200">array or string</span></span> |<span data-ttu-id="20d87-201">Hello prima matrice o stringa per la concatenazione.</span><span class="sxs-lookup"><span data-stu-id="20d87-201">hello first array or string for concatenation.</span></span> |
| <span data-ttu-id="20d87-202">argomenti aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="20d87-202">additional arguments</span></span> |<span data-ttu-id="20d87-203">No</span><span class="sxs-lookup"><span data-stu-id="20d87-203">No</span></span> |<span data-ttu-id="20d87-204">stringa o matrice</span><span class="sxs-lookup"><span data-stu-id="20d87-204">array or string</span></span> |<span data-ttu-id="20d87-205">Matrici o stringhe aggiuntive in ordine sequenziale per la concatenazione.</span><span class="sxs-lookup"><span data-stu-id="20d87-205">Additional arrays or strings in sequential order for concatenation.</span></span> |

<span data-ttu-id="20d87-206">Questa funzione può accettare un numero qualsiasi di argomenti e può accettare stringhe o matrici per i parametri di hello.</span><span class="sxs-lookup"><span data-stu-id="20d87-206">This function can take any number of arguments, and can accept either strings or arrays for hello parameters.</span></span>

### <a name="return-value"></a><span data-ttu-id="20d87-207">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="20d87-207">Return value</span></span>
<span data-ttu-id="20d87-208">Stringa o matrice di valori concatenati.</span><span class="sxs-lookup"><span data-stu-id="20d87-208">A string or array of concatenated values.</span></span>

### <a name="example"></a><span data-ttu-id="20d87-209">Esempio</span><span class="sxs-lookup"><span data-stu-id="20d87-209">Example</span></span>

<span data-ttu-id="20d87-210">Hello di esempio seguente viene illustrato come toocombine due matrici.</span><span class="sxs-lookup"><span data-stu-id="20d87-210">hello following example shows how toocombine two arrays.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "firstArray": { 
            "type": "array", 
            "defaultValue": [ 
                "1-1", 
                "1-2", 
                "1-3" 
            ] 
        },
        "secondArray": {
            "type": "array", 
            "defaultValue": [ 
                "2-1", 
                "2-2",
                "2-3" 
            ] 
        }
    },
    "resources": [
    ],
    "outputs": {
        "return": {
            "type": "array",
            "value": "[concat(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

<span data-ttu-id="20d87-211">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="20d87-211">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="20d87-212">Nome</span><span class="sxs-lookup"><span data-stu-id="20d87-212">Name</span></span> | <span data-ttu-id="20d87-213">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-213">Type</span></span> | <span data-ttu-id="20d87-214">Valore</span><span class="sxs-lookup"><span data-stu-id="20d87-214">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="20d87-215">return</span><span class="sxs-lookup"><span data-stu-id="20d87-215">return</span></span> | <span data-ttu-id="20d87-216">Array</span><span class="sxs-lookup"><span data-stu-id="20d87-216">Array</span></span> | <span data-ttu-id="20d87-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="20d87-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<span data-ttu-id="20d87-218">Hello di esempio seguente viene illustrato come toocombine due valori stringa e restituire una stringa concatenata.</span><span class="sxs-lookup"><span data-stu-id="20d87-218">hello following example shows how toocombine two string values and return a concatenated string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "prefix": {
            "type": "string",
            "defaultValue": "prefix"
        }
    },
    "resources": [],
    "outputs": {
        "concatOutput": {
            "value": "[concat(parameters('prefix'), '-', uniqueString(resourceGroup().id))]",
            "type" : "string"
        }
    }
}
```

<span data-ttu-id="20d87-219">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="20d87-219">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="20d87-220">Nome</span><span class="sxs-lookup"><span data-stu-id="20d87-220">Name</span></span> | <span data-ttu-id="20d87-221">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-221">Type</span></span> | <span data-ttu-id="20d87-222">Valore</span><span class="sxs-lookup"><span data-stu-id="20d87-222">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="20d87-223">concatOutput</span><span class="sxs-lookup"><span data-stu-id="20d87-223">concatOutput</span></span> | <span data-ttu-id="20d87-224">String</span><span class="sxs-lookup"><span data-stu-id="20d87-224">String</span></span> | <span data-ttu-id="20d87-225">prefix-5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="20d87-225">prefix-5yj4yjf5mbg72</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="20d87-226">contains</span><span class="sxs-lookup"><span data-stu-id="20d87-226">contains</span></span>
`contains(container, itemToFind)`

<span data-ttu-id="20d87-227">Verifica se una matrice contiene un valore, se un oggetto contiene una chiave o se una stringa contiene una sottostringa.</span><span class="sxs-lookup"><span data-stu-id="20d87-227">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="20d87-228">Parametri</span><span class="sxs-lookup"><span data-stu-id="20d87-228">Parameters</span></span>

| <span data-ttu-id="20d87-229">Parametro</span><span class="sxs-lookup"><span data-stu-id="20d87-229">Parameter</span></span> | <span data-ttu-id="20d87-230">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="20d87-230">Required</span></span> | <span data-ttu-id="20d87-231">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-231">Type</span></span> | <span data-ttu-id="20d87-232">Descrizione</span><span class="sxs-lookup"><span data-stu-id="20d87-232">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="20d87-233">Contenitore</span><span class="sxs-lookup"><span data-stu-id="20d87-233">container</span></span> |<span data-ttu-id="20d87-234">Sì</span><span class="sxs-lookup"><span data-stu-id="20d87-234">Yes</span></span> |<span data-ttu-id="20d87-235">matrice, oggetto o stringa</span><span class="sxs-lookup"><span data-stu-id="20d87-235">array, object, or string</span></span> |<span data-ttu-id="20d87-236">valore di Hello contenente toofind valore hello.</span><span class="sxs-lookup"><span data-stu-id="20d87-236">hello value that contains hello value toofind.</span></span> |
| <span data-ttu-id="20d87-237">itemToFind</span><span class="sxs-lookup"><span data-stu-id="20d87-237">itemToFind</span></span> |<span data-ttu-id="20d87-238">Sì</span><span class="sxs-lookup"><span data-stu-id="20d87-238">Yes</span></span> |<span data-ttu-id="20d87-239">stringa o numero intero</span><span class="sxs-lookup"><span data-stu-id="20d87-239">string or int</span></span> |<span data-ttu-id="20d87-240">toofind valore Hello.</span><span class="sxs-lookup"><span data-stu-id="20d87-240">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="20d87-241">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="20d87-241">Return value</span></span>

<span data-ttu-id="20d87-242">**True** se l'elemento hello è stato trovato; in caso contrario, **False**.</span><span class="sxs-lookup"><span data-stu-id="20d87-242">**True** if hello item is found; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="20d87-243">Esempio</span><span class="sxs-lookup"><span data-stu-id="20d87-243">Example</span></span>

<span data-ttu-id="20d87-244">Hello esempio seguente viene illustrato come toouse contiene con tipi diversi:</span><span class="sxs-lookup"><span data-stu-id="20d87-244">hello following example shows how toouse contains with different types:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "OneTwoThree"
        },
        "objectToTest": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringTrue": {
            "type": "bool",
            "value": "[contains(parameters('stringToTest'), 'e')]"
        },
        "stringFalse": {
            "type": "bool",
            "value": "[contains(parameters('stringToTest'), 'z')]"
        },
        "objectTrue": {
            "type": "bool",
            "value": "[contains(parameters('objectToTest'), 'one')]"
        },
        "objectFalse": {
            "type": "bool",
            "value": "[contains(parameters('objectToTest'), 'a')]"
        },
        "arrayTrue": {
            "type": "bool",
            "value": "[contains(parameters('arrayToTest'), 'three')]"
        },
        "arrayFalse": {
            "type": "bool",
            "value": "[contains(parameters('arrayToTest'), 'four')]"
        }
    }
}
```

<span data-ttu-id="20d87-245">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="20d87-245">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="20d87-246">Nome</span><span class="sxs-lookup"><span data-stu-id="20d87-246">Name</span></span> | <span data-ttu-id="20d87-247">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-247">Type</span></span> | <span data-ttu-id="20d87-248">Valore</span><span class="sxs-lookup"><span data-stu-id="20d87-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="20d87-249">stringTrue</span><span class="sxs-lookup"><span data-stu-id="20d87-249">stringTrue</span></span> | <span data-ttu-id="20d87-250">Booleano</span><span class="sxs-lookup"><span data-stu-id="20d87-250">Bool</span></span> | <span data-ttu-id="20d87-251">True </span><span class="sxs-lookup"><span data-stu-id="20d87-251">True</span></span> |
| <span data-ttu-id="20d87-252">stringFalse</span><span class="sxs-lookup"><span data-stu-id="20d87-252">stringFalse</span></span> | <span data-ttu-id="20d87-253">Booleano</span><span class="sxs-lookup"><span data-stu-id="20d87-253">Bool</span></span> | <span data-ttu-id="20d87-254">False</span><span class="sxs-lookup"><span data-stu-id="20d87-254">False</span></span> |
| <span data-ttu-id="20d87-255">objectTrue</span><span class="sxs-lookup"><span data-stu-id="20d87-255">objectTrue</span></span> | <span data-ttu-id="20d87-256">Booleano</span><span class="sxs-lookup"><span data-stu-id="20d87-256">Bool</span></span> | <span data-ttu-id="20d87-257">True </span><span class="sxs-lookup"><span data-stu-id="20d87-257">True</span></span> |
| <span data-ttu-id="20d87-258">objectFalse</span><span class="sxs-lookup"><span data-stu-id="20d87-258">objectFalse</span></span> | <span data-ttu-id="20d87-259">Booleano</span><span class="sxs-lookup"><span data-stu-id="20d87-259">Bool</span></span> | <span data-ttu-id="20d87-260">False</span><span class="sxs-lookup"><span data-stu-id="20d87-260">False</span></span> |
| <span data-ttu-id="20d87-261">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="20d87-261">arrayTrue</span></span> | <span data-ttu-id="20d87-262">Booleano</span><span class="sxs-lookup"><span data-stu-id="20d87-262">Bool</span></span> | <span data-ttu-id="20d87-263">True </span><span class="sxs-lookup"><span data-stu-id="20d87-263">True</span></span> |
| <span data-ttu-id="20d87-264">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="20d87-264">arrayFalse</span></span> | <span data-ttu-id="20d87-265">Booleano</span><span class="sxs-lookup"><span data-stu-id="20d87-265">Bool</span></span> | <span data-ttu-id="20d87-266">False</span><span class="sxs-lookup"><span data-stu-id="20d87-266">False</span></span> |

<a id="createarray" />

## <a name="createarray"></a><span data-ttu-id="20d87-267">createarray</span><span class="sxs-lookup"><span data-stu-id="20d87-267">createarray</span></span>
`createArray (arg1, arg2, arg3, ...)`

<span data-ttu-id="20d87-268">Crea una matrice di parametri di hello.</span><span class="sxs-lookup"><span data-stu-id="20d87-268">Creates an array from hello parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="20d87-269">parameters</span><span class="sxs-lookup"><span data-stu-id="20d87-269">Parameters</span></span>

| <span data-ttu-id="20d87-270">Parametro</span><span class="sxs-lookup"><span data-stu-id="20d87-270">Parameter</span></span> | <span data-ttu-id="20d87-271">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="20d87-271">Required</span></span> | <span data-ttu-id="20d87-272">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-272">Type</span></span> | <span data-ttu-id="20d87-273">Descrizione</span><span class="sxs-lookup"><span data-stu-id="20d87-273">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="20d87-274">arg1</span><span class="sxs-lookup"><span data-stu-id="20d87-274">arg1</span></span> |<span data-ttu-id="20d87-275">Sì</span><span class="sxs-lookup"><span data-stu-id="20d87-275">Yes</span></span> |<span data-ttu-id="20d87-276">Stringa, numero intero, matrice o oggetto</span><span class="sxs-lookup"><span data-stu-id="20d87-276">String, Integer, Array, or Object</span></span> |<span data-ttu-id="20d87-277">primo valore Hello nella matrice hello.</span><span class="sxs-lookup"><span data-stu-id="20d87-277">hello first value in hello array.</span></span> |
| <span data-ttu-id="20d87-278">argomenti aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="20d87-278">additional arguments</span></span> |<span data-ttu-id="20d87-279">No</span><span class="sxs-lookup"><span data-stu-id="20d87-279">No</span></span> |<span data-ttu-id="20d87-280">Stringa, numero intero, matrice o oggetto</span><span class="sxs-lookup"><span data-stu-id="20d87-280">String, Integer, Array, or Object</span></span> |<span data-ttu-id="20d87-281">Valori aggiuntivi nella matrice hello.</span><span class="sxs-lookup"><span data-stu-id="20d87-281">Additional values in hello array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="20d87-282">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="20d87-282">Return value</span></span>

<span data-ttu-id="20d87-283">Una matrice.</span><span class="sxs-lookup"><span data-stu-id="20d87-283">An array.</span></span>

### <a name="example"></a><span data-ttu-id="20d87-284">Esempio</span><span class="sxs-lookup"><span data-stu-id="20d87-284">Example</span></span>

<span data-ttu-id="20d87-285">Hello seguente esempio viene illustrato come createArray toouse con tipi diversi:</span><span class="sxs-lookup"><span data-stu-id="20d87-285">hello following example shows how toouse createArray with different types:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "objectToTest": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringArray": {
            "type": "array",
            "value": "[createArray('a', 'b', 'c')]"
        },
        "intArray": {
            "type": "array",
            "value": "[createArray(1, 2, 3)]"
        },
        "objectArray": {
            "type": "array",
            "value": "[createArray(parameters('objectToTest'))]"
        },
        "arrayArray": {
            "type": "array",
            "value": "[createArray(parameters('arrayToTest'))]"
        }
    }
}
```

<span data-ttu-id="20d87-286">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="20d87-286">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="20d87-287">Nome</span><span class="sxs-lookup"><span data-stu-id="20d87-287">Name</span></span> | <span data-ttu-id="20d87-288">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-288">Type</span></span> | <span data-ttu-id="20d87-289">Valore</span><span class="sxs-lookup"><span data-stu-id="20d87-289">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="20d87-290">stringArray</span><span class="sxs-lookup"><span data-stu-id="20d87-290">stringArray</span></span> | <span data-ttu-id="20d87-291">Array</span><span class="sxs-lookup"><span data-stu-id="20d87-291">Array</span></span> | <span data-ttu-id="20d87-292">["a", "b", "c"]</span><span class="sxs-lookup"><span data-stu-id="20d87-292">["a", "b", "c"]</span></span> |
| <span data-ttu-id="20d87-293">intArray</span><span class="sxs-lookup"><span data-stu-id="20d87-293">intArray</span></span> | <span data-ttu-id="20d87-294">Array</span><span class="sxs-lookup"><span data-stu-id="20d87-294">Array</span></span> | <span data-ttu-id="20d87-295">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="20d87-295">[1, 2, 3]</span></span> |
| <span data-ttu-id="20d87-296">objectArray</span><span class="sxs-lookup"><span data-stu-id="20d87-296">objectArray</span></span> | <span data-ttu-id="20d87-297">Array</span><span class="sxs-lookup"><span data-stu-id="20d87-297">Array</span></span> | <span data-ttu-id="20d87-298">[{"one": "a", "two": "b", "three": "c"}]</span><span class="sxs-lookup"><span data-stu-id="20d87-298">[{"one": "a", "two": "b", "three": "c"}]</span></span> |
| <span data-ttu-id="20d87-299">arrayArray</span><span class="sxs-lookup"><span data-stu-id="20d87-299">arrayArray</span></span> | <span data-ttu-id="20d87-300">Array</span><span class="sxs-lookup"><span data-stu-id="20d87-300">Array</span></span> | <span data-ttu-id="20d87-301">[["one", "two", "three"]]</span><span class="sxs-lookup"><span data-stu-id="20d87-301">[["one", "two", "three"]]</span></span> |

<a id="empty" />

## <a name="empty"></a><span data-ttu-id="20d87-302">empty</span><span class="sxs-lookup"><span data-stu-id="20d87-302">empty</span></span>

`empty(itemToTest)`

<span data-ttu-id="20d87-303">Determina se una matrice, un oggetto o una stringa sono vuoti.</span><span class="sxs-lookup"><span data-stu-id="20d87-303">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="20d87-304">Parametri</span><span class="sxs-lookup"><span data-stu-id="20d87-304">Parameters</span></span>

| <span data-ttu-id="20d87-305">Parametro</span><span class="sxs-lookup"><span data-stu-id="20d87-305">Parameter</span></span> | <span data-ttu-id="20d87-306">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="20d87-306">Required</span></span> | <span data-ttu-id="20d87-307">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-307">Type</span></span> | <span data-ttu-id="20d87-308">Descrizione</span><span class="sxs-lookup"><span data-stu-id="20d87-308">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="20d87-309">itemToTest</span><span class="sxs-lookup"><span data-stu-id="20d87-309">itemToTest</span></span> |<span data-ttu-id="20d87-310">Sì</span><span class="sxs-lookup"><span data-stu-id="20d87-310">Yes</span></span> |<span data-ttu-id="20d87-311">matrice, oggetto o stringa</span><span class="sxs-lookup"><span data-stu-id="20d87-311">array, object, or string</span></span> |<span data-ttu-id="20d87-312">Hello toocheck valore se è vuota.</span><span class="sxs-lookup"><span data-stu-id="20d87-312">hello value toocheck if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="20d87-313">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="20d87-313">Return value</span></span>

<span data-ttu-id="20d87-314">Restituisce **True** se il valore di hello è vuota; in caso contrario, **False**.</span><span class="sxs-lookup"><span data-stu-id="20d87-314">Returns **True** if hello value is empty; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="20d87-315">Esempio</span><span class="sxs-lookup"><span data-stu-id="20d87-315">Example</span></span>

<span data-ttu-id="20d87-316">Hello di esempio seguente controlla se una matrice, un oggetto e una stringa sono vuote.</span><span class="sxs-lookup"><span data-stu-id="20d87-316">hello following example checks whether an array, object, and string are empty.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": []
        },
        "testObject": {
            "type": "object",
            "defaultValue": {}
        },
        "testString": {
            "type": "string",
            "defaultValue": ""
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testArray'))]"
        },
        "objectEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testObject'))]"
        },
        "stringEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testString'))]"
        }
    }
}
```

<span data-ttu-id="20d87-317">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="20d87-317">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="20d87-318">Nome</span><span class="sxs-lookup"><span data-stu-id="20d87-318">Name</span></span> | <span data-ttu-id="20d87-319">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-319">Type</span></span> | <span data-ttu-id="20d87-320">Valore</span><span class="sxs-lookup"><span data-stu-id="20d87-320">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="20d87-321">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="20d87-321">arrayEmpty</span></span> | <span data-ttu-id="20d87-322">Booleano</span><span class="sxs-lookup"><span data-stu-id="20d87-322">Bool</span></span> | <span data-ttu-id="20d87-323">True </span><span class="sxs-lookup"><span data-stu-id="20d87-323">True</span></span> |
| <span data-ttu-id="20d87-324">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="20d87-324">objectEmpty</span></span> | <span data-ttu-id="20d87-325">Booleano</span><span class="sxs-lookup"><span data-stu-id="20d87-325">Bool</span></span> | <span data-ttu-id="20d87-326">True </span><span class="sxs-lookup"><span data-stu-id="20d87-326">True</span></span> |
| <span data-ttu-id="20d87-327">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="20d87-327">stringEmpty</span></span> | <span data-ttu-id="20d87-328">Booleano</span><span class="sxs-lookup"><span data-stu-id="20d87-328">Bool</span></span> | <span data-ttu-id="20d87-329">True </span><span class="sxs-lookup"><span data-stu-id="20d87-329">True</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="20d87-330">first</span><span class="sxs-lookup"><span data-stu-id="20d87-330">first</span></span>
`first(arg1)`

<span data-ttu-id="20d87-331">Restituisce hello primo elemento della matrice hello o primo carattere della stringa hello.</span><span class="sxs-lookup"><span data-stu-id="20d87-331">Returns hello first element of hello array, or first character of hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="20d87-332">parameters</span><span class="sxs-lookup"><span data-stu-id="20d87-332">Parameters</span></span>

| <span data-ttu-id="20d87-333">Parametro</span><span class="sxs-lookup"><span data-stu-id="20d87-333">Parameter</span></span> | <span data-ttu-id="20d87-334">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="20d87-334">Required</span></span> | <span data-ttu-id="20d87-335">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-335">Type</span></span> | <span data-ttu-id="20d87-336">Descrizione</span><span class="sxs-lookup"><span data-stu-id="20d87-336">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="20d87-337">arg1</span><span class="sxs-lookup"><span data-stu-id="20d87-337">arg1</span></span> |<span data-ttu-id="20d87-338">Sì</span><span class="sxs-lookup"><span data-stu-id="20d87-338">Yes</span></span> |<span data-ttu-id="20d87-339">stringa o matrice</span><span class="sxs-lookup"><span data-stu-id="20d87-339">array or string</span></span> |<span data-ttu-id="20d87-340">carattere o Hello valore tooretrieve hello primo elemento.</span><span class="sxs-lookup"><span data-stu-id="20d87-340">hello value tooretrieve hello first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="20d87-341">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="20d87-341">Return value</span></span>

<span data-ttu-id="20d87-342">tipo (string, int, matrice o oggetto) del primo elemento di hello in una matrice di Hello o hello primo carattere della stringa.</span><span class="sxs-lookup"><span data-stu-id="20d87-342">hello type (string, int, array, or object) of hello first element in an array, or hello first character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="20d87-343">Esempio</span><span class="sxs-lookup"><span data-stu-id="20d87-343">Example</span></span>

<span data-ttu-id="20d87-344">Hello esempio seguente viene illustrato come toouse hello prima funzione con una matrice e una stringa.</span><span class="sxs-lookup"><span data-stu-id="20d87-344">hello following example shows how toouse hello first function with an array and string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayOutput": {
            "type": "string",
            "value": "[first(parameters('arrayToTest'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[first('One Two Three')]"
        }
    }
}
```

<span data-ttu-id="20d87-345">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="20d87-345">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="20d87-346">Nome</span><span class="sxs-lookup"><span data-stu-id="20d87-346">Name</span></span> | <span data-ttu-id="20d87-347">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-347">Type</span></span> | <span data-ttu-id="20d87-348">Valore</span><span class="sxs-lookup"><span data-stu-id="20d87-348">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="20d87-349">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="20d87-349">arrayOutput</span></span> | <span data-ttu-id="20d87-350">String</span><span class="sxs-lookup"><span data-stu-id="20d87-350">String</span></span> | <span data-ttu-id="20d87-351">one</span><span class="sxs-lookup"><span data-stu-id="20d87-351">one</span></span> |
| <span data-ttu-id="20d87-352">stringOutput</span><span class="sxs-lookup"><span data-stu-id="20d87-352">stringOutput</span></span> | <span data-ttu-id="20d87-353">String</span><span class="sxs-lookup"><span data-stu-id="20d87-353">String</span></span> | <span data-ttu-id="20d87-354">O</span><span class="sxs-lookup"><span data-stu-id="20d87-354">O</span></span> |

<a id="intersection" />

## <a name="intersection"></a><span data-ttu-id="20d87-355">intersezione</span><span class="sxs-lookup"><span data-stu-id="20d87-355">intersection</span></span>
`intersection(arg1, arg2, arg3, ...)`

<span data-ttu-id="20d87-356">Restituisce una matrice o un oggetto con elementi comuni hello dai parametri hello.</span><span class="sxs-lookup"><span data-stu-id="20d87-356">Returns a single array or object with hello common elements from hello parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="20d87-357">parameters</span><span class="sxs-lookup"><span data-stu-id="20d87-357">Parameters</span></span>

| <span data-ttu-id="20d87-358">Parametro</span><span class="sxs-lookup"><span data-stu-id="20d87-358">Parameter</span></span> | <span data-ttu-id="20d87-359">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="20d87-359">Required</span></span> | <span data-ttu-id="20d87-360">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-360">Type</span></span> | <span data-ttu-id="20d87-361">Descrizione</span><span class="sxs-lookup"><span data-stu-id="20d87-361">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="20d87-362">arg1</span><span class="sxs-lookup"><span data-stu-id="20d87-362">arg1</span></span> |<span data-ttu-id="20d87-363">Sì</span><span class="sxs-lookup"><span data-stu-id="20d87-363">Yes</span></span> |<span data-ttu-id="20d87-364">matrice o oggetto</span><span class="sxs-lookup"><span data-stu-id="20d87-364">array or object</span></span> |<span data-ttu-id="20d87-365">Hello toouse prima di valore per la ricerca di elementi comuni.</span><span class="sxs-lookup"><span data-stu-id="20d87-365">hello first value toouse for finding common elements.</span></span> |
| <span data-ttu-id="20d87-366">arg2</span><span class="sxs-lookup"><span data-stu-id="20d87-366">arg2</span></span> |<span data-ttu-id="20d87-367">Sì</span><span class="sxs-lookup"><span data-stu-id="20d87-367">Yes</span></span> |<span data-ttu-id="20d87-368">matrice o oggetto</span><span class="sxs-lookup"><span data-stu-id="20d87-368">array or object</span></span> |<span data-ttu-id="20d87-369">Hello secondo valore toouse per la ricerca di elementi comuni.</span><span class="sxs-lookup"><span data-stu-id="20d87-369">hello second value toouse for finding common elements.</span></span> |
| <span data-ttu-id="20d87-370">argomenti aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="20d87-370">additional arguments</span></span> |<span data-ttu-id="20d87-371">No</span><span class="sxs-lookup"><span data-stu-id="20d87-371">No</span></span> |<span data-ttu-id="20d87-372">matrice o oggetto</span><span class="sxs-lookup"><span data-stu-id="20d87-372">array or object</span></span> |<span data-ttu-id="20d87-373">Toouse valori aggiuntivi per la ricerca di elementi comuni.</span><span class="sxs-lookup"><span data-stu-id="20d87-373">Additional values toouse for finding common elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="20d87-374">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="20d87-374">Return value</span></span>

<span data-ttu-id="20d87-375">Una matrice o un oggetto con elementi comuni hello.</span><span class="sxs-lookup"><span data-stu-id="20d87-375">An array or object with hello common elements.</span></span>

### <a name="example"></a><span data-ttu-id="20d87-376">Esempio</span><span class="sxs-lookup"><span data-stu-id="20d87-376">Example</span></span>

<span data-ttu-id="20d87-377">Hello esempio viene illustrato come toouse intersezione con matrici e gli oggetti seguenti:</span><span class="sxs-lookup"><span data-stu-id="20d87-377">hello following example shows how toouse intersection with arrays and objects:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "z", "three": "c"}
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "objectOutput": {
            "type": "object",
            "value": "[intersection(parameters('firstObject'), parameters('secondObject'))]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[intersection(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

<span data-ttu-id="20d87-378">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="20d87-378">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="20d87-379">Nome</span><span class="sxs-lookup"><span data-stu-id="20d87-379">Name</span></span> | <span data-ttu-id="20d87-380">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-380">Type</span></span> | <span data-ttu-id="20d87-381">Valore</span><span class="sxs-lookup"><span data-stu-id="20d87-381">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="20d87-382">objectOutput</span><span class="sxs-lookup"><span data-stu-id="20d87-382">objectOutput</span></span> | <span data-ttu-id="20d87-383">Oggetto</span><span class="sxs-lookup"><span data-stu-id="20d87-383">Object</span></span> | <span data-ttu-id="20d87-384">{"one": "a", "three": "c"}</span><span class="sxs-lookup"><span data-stu-id="20d87-384">{"one": "a", "three": "c"}</span></span> |
| <span data-ttu-id="20d87-385">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="20d87-385">arrayOutput</span></span> | <span data-ttu-id="20d87-386">Array</span><span class="sxs-lookup"><span data-stu-id="20d87-386">Array</span></span> | <span data-ttu-id="20d87-387">["two", "three"]</span><span class="sxs-lookup"><span data-stu-id="20d87-387">["two", "three"]</span></span> |


## <a name="json"></a><span data-ttu-id="20d87-388">json</span><span class="sxs-lookup"><span data-stu-id="20d87-388">json</span></span>
`json(arg1)`

<span data-ttu-id="20d87-389">Restituisce un oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="20d87-389">Returns a JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="20d87-390">parameters</span><span class="sxs-lookup"><span data-stu-id="20d87-390">Parameters</span></span>

| <span data-ttu-id="20d87-391">Parametro</span><span class="sxs-lookup"><span data-stu-id="20d87-391">Parameter</span></span> | <span data-ttu-id="20d87-392">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="20d87-392">Required</span></span> | <span data-ttu-id="20d87-393">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-393">Type</span></span> | <span data-ttu-id="20d87-394">Descrizione</span><span class="sxs-lookup"><span data-stu-id="20d87-394">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="20d87-395">arg1</span><span class="sxs-lookup"><span data-stu-id="20d87-395">arg1</span></span> |<span data-ttu-id="20d87-396">Sì</span><span class="sxs-lookup"><span data-stu-id="20d87-396">Yes</span></span> |<span data-ttu-id="20d87-397">string</span><span class="sxs-lookup"><span data-stu-id="20d87-397">string</span></span> |<span data-ttu-id="20d87-398">Hello valore tooconvert tooJSON.</span><span class="sxs-lookup"><span data-stu-id="20d87-398">hello value tooconvert tooJSON.</span></span> |


### <a name="return-value"></a><span data-ttu-id="20d87-399">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="20d87-399">Return value</span></span>

<span data-ttu-id="20d87-400">oggetto JSON Hello hello specificato stringa o un oggetto vuoto quando **null** specificato.</span><span class="sxs-lookup"><span data-stu-id="20d87-400">hello JSON object from hello specified string, or an empty object when **null** is specified.</span></span>

### <a name="example"></a><span data-ttu-id="20d87-401">Esempio</span><span class="sxs-lookup"><span data-stu-id="20d87-401">Example</span></span>

<span data-ttu-id="20d87-402">Hello esempio viene illustrato come toouse intersezione con matrici e gli oggetti seguenti:</span><span class="sxs-lookup"><span data-stu-id="20d87-402">hello following example shows how toouse intersection with arrays and objects:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "jsonOutput": {
            "type": "object",
            "value": "[json('{\"a\": \"b\"}')]"
        },
        "nullOutput": {
            "type": "bool",
            "value": "[empty(json('null'))]"
        }
    }
}
```

<span data-ttu-id="20d87-403">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="20d87-403">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="20d87-404">Nome</span><span class="sxs-lookup"><span data-stu-id="20d87-404">Name</span></span> | <span data-ttu-id="20d87-405">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-405">Type</span></span> | <span data-ttu-id="20d87-406">Valore</span><span class="sxs-lookup"><span data-stu-id="20d87-406">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="20d87-407">jsonOutput</span><span class="sxs-lookup"><span data-stu-id="20d87-407">jsonOutput</span></span> | <span data-ttu-id="20d87-408">Oggetto</span><span class="sxs-lookup"><span data-stu-id="20d87-408">Object</span></span> | <span data-ttu-id="20d87-409">{"a": "b"}</span><span class="sxs-lookup"><span data-stu-id="20d87-409">{"a": "b"}</span></span> |
| <span data-ttu-id="20d87-410">nullOutput</span><span class="sxs-lookup"><span data-stu-id="20d87-410">nullOutput</span></span> | <span data-ttu-id="20d87-411">Boolean</span><span class="sxs-lookup"><span data-stu-id="20d87-411">Boolean</span></span> | <span data-ttu-id="20d87-412">True </span><span class="sxs-lookup"><span data-stu-id="20d87-412">True</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="20d87-413">last</span><span class="sxs-lookup"><span data-stu-id="20d87-413">last</span></span>
`last (arg1)`

<span data-ttu-id="20d87-414">Restituisce hello l'ultimo elemento della matrice hello o ultimo carattere della stringa hello.</span><span class="sxs-lookup"><span data-stu-id="20d87-414">Returns hello last element of hello array, or last character of hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="20d87-415">parameters</span><span class="sxs-lookup"><span data-stu-id="20d87-415">Parameters</span></span>

| <span data-ttu-id="20d87-416">Parametro</span><span class="sxs-lookup"><span data-stu-id="20d87-416">Parameter</span></span> | <span data-ttu-id="20d87-417">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="20d87-417">Required</span></span> | <span data-ttu-id="20d87-418">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-418">Type</span></span> | <span data-ttu-id="20d87-419">Descrizione</span><span class="sxs-lookup"><span data-stu-id="20d87-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="20d87-420">arg1</span><span class="sxs-lookup"><span data-stu-id="20d87-420">arg1</span></span> |<span data-ttu-id="20d87-421">Sì</span><span class="sxs-lookup"><span data-stu-id="20d87-421">Yes</span></span> |<span data-ttu-id="20d87-422">stringa o matrice</span><span class="sxs-lookup"><span data-stu-id="20d87-422">array or string</span></span> |<span data-ttu-id="20d87-423">carattere o Hello valore tooretrieve hello ultimo elemento.</span><span class="sxs-lookup"><span data-stu-id="20d87-423">hello value tooretrieve hello last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="20d87-424">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="20d87-424">Return value</span></span>

<span data-ttu-id="20d87-425">tipo di Hello (string, int, matrice o oggetto) dell'ultimo elemento di hello in una matrice o ultimo carattere di hello di una stringa.</span><span class="sxs-lookup"><span data-stu-id="20d87-425">hello type (string, int, array, or object) of hello last element in an array, or hello last character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="20d87-426">Esempio</span><span class="sxs-lookup"><span data-stu-id="20d87-426">Example</span></span>

<span data-ttu-id="20d87-427">Hello esempio seguente viene illustrato come toouse hello ultima funzione con una matrice e una stringa.</span><span class="sxs-lookup"><span data-stu-id="20d87-427">hello following example shows how toouse hello last function with an array and string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayOutput": {
            "type": "string",
            "value": "[last(parameters('arrayToTest'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[last('One Two Three')]"
        }
    }
}
```

<span data-ttu-id="20d87-428">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="20d87-428">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="20d87-429">Nome</span><span class="sxs-lookup"><span data-stu-id="20d87-429">Name</span></span> | <span data-ttu-id="20d87-430">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-430">Type</span></span> | <span data-ttu-id="20d87-431">Valore</span><span class="sxs-lookup"><span data-stu-id="20d87-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="20d87-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="20d87-432">arrayOutput</span></span> | <span data-ttu-id="20d87-433">String</span><span class="sxs-lookup"><span data-stu-id="20d87-433">String</span></span> | <span data-ttu-id="20d87-434">three</span><span class="sxs-lookup"><span data-stu-id="20d87-434">three</span></span> |
| <span data-ttu-id="20d87-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="20d87-435">stringOutput</span></span> | <span data-ttu-id="20d87-436">String</span><span class="sxs-lookup"><span data-stu-id="20d87-436">String</span></span> | <span data-ttu-id="20d87-437">e</span><span class="sxs-lookup"><span data-stu-id="20d87-437">e</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="20d87-438">length</span><span class="sxs-lookup"><span data-stu-id="20d87-438">length</span></span>
`length(arg1)`

<span data-ttu-id="20d87-439">Restituisce il numero di hello di elementi in una matrice o in una stringa di caratteri.</span><span class="sxs-lookup"><span data-stu-id="20d87-439">Returns hello number of elements in an array, or characters in a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="20d87-440">parameters</span><span class="sxs-lookup"><span data-stu-id="20d87-440">Parameters</span></span>

| <span data-ttu-id="20d87-441">Parametro</span><span class="sxs-lookup"><span data-stu-id="20d87-441">Parameter</span></span> | <span data-ttu-id="20d87-442">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="20d87-442">Required</span></span> | <span data-ttu-id="20d87-443">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-443">Type</span></span> | <span data-ttu-id="20d87-444">Descrizione</span><span class="sxs-lookup"><span data-stu-id="20d87-444">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="20d87-445">arg1</span><span class="sxs-lookup"><span data-stu-id="20d87-445">arg1</span></span> |<span data-ttu-id="20d87-446">Sì</span><span class="sxs-lookup"><span data-stu-id="20d87-446">Yes</span></span> |<span data-ttu-id="20d87-447">stringa o matrice</span><span class="sxs-lookup"><span data-stu-id="20d87-447">array or string</span></span> |<span data-ttu-id="20d87-448">Hello toouse matrice per ottenere il numero di hello di elementi o hello toouse stringa per ottenere il numero di hello di caratteri.</span><span class="sxs-lookup"><span data-stu-id="20d87-448">hello array toouse for getting hello number of elements, or hello string toouse for getting hello number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="20d87-449">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="20d87-449">Return value</span></span>

<span data-ttu-id="20d87-450">Numero intero</span><span class="sxs-lookup"><span data-stu-id="20d87-450">An int.</span></span> 

### <a name="example"></a><span data-ttu-id="20d87-451">Esempio</span><span class="sxs-lookup"><span data-stu-id="20d87-451">Example</span></span>

<span data-ttu-id="20d87-452">Hello seguente esempio viene illustrato come lunghezza toouse con una matrice e la stringa:</span><span class="sxs-lookup"><span data-stu-id="20d87-452">hello following example shows how toouse length with an array and string:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "stringToTest": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "arrayLength": {
            "type": "int",
            "value": "[length(parameters('arrayToTest'))]"
        },
        "stringLength": {
            "type": "int",
            "value": "[length(parameters('stringToTest'))]"
        }
    }
}
```

<span data-ttu-id="20d87-453">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="20d87-453">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="20d87-454">Nome</span><span class="sxs-lookup"><span data-stu-id="20d87-454">Name</span></span> | <span data-ttu-id="20d87-455">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-455">Type</span></span> | <span data-ttu-id="20d87-456">Valore</span><span class="sxs-lookup"><span data-stu-id="20d87-456">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="20d87-457">arrayLength</span><span class="sxs-lookup"><span data-stu-id="20d87-457">arrayLength</span></span> | <span data-ttu-id="20d87-458">int</span><span class="sxs-lookup"><span data-stu-id="20d87-458">Int</span></span> | <span data-ttu-id="20d87-459">3</span><span class="sxs-lookup"><span data-stu-id="20d87-459">3</span></span> |
| <span data-ttu-id="20d87-460">stringLength</span><span class="sxs-lookup"><span data-stu-id="20d87-460">stringLength</span></span> | <span data-ttu-id="20d87-461">int</span><span class="sxs-lookup"><span data-stu-id="20d87-461">Int</span></span> | <span data-ttu-id="20d87-462">13</span><span class="sxs-lookup"><span data-stu-id="20d87-462">13</span></span> |

<span data-ttu-id="20d87-463">È possibile utilizzare questa funzione con un numero di hello matrice toospecify di iterazioni quando si creano risorse.</span><span class="sxs-lookup"><span data-stu-id="20d87-463">You can use this function with an array toospecify hello number of iterations when creating resources.</span></span> <span data-ttu-id="20d87-464">Nell'esempio seguente di hello, hello parametro **siteNames** tooan matrice di nomi toouse riferimento durante la creazione di siti web hello.</span><span class="sxs-lookup"><span data-stu-id="20d87-464">In hello following example, hello parameter **siteNames** would refer tooan array of names toouse when creating hello web sites.</span></span>

```json
"copy": {
    "name": "websitescopy",
    "count": "[length(parameters('siteNames'))]"
}
```

<span data-ttu-id="20d87-465">Per altre informazioni sull'uso di questa funzione con una matrice, vedere [Creare più istanze di risorse in Gestione risorse di Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="20d87-465">For more information about using this function with an array, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<a id="min" />

## <a name="min"></a><span data-ttu-id="20d87-466">Min</span><span class="sxs-lookup"><span data-stu-id="20d87-466">min</span></span>
`min(arg1)`

<span data-ttu-id="20d87-467">Restituisce hello valore minimo da una matrice di interi o un elenco delimitato da virgole di numeri interi.</span><span class="sxs-lookup"><span data-stu-id="20d87-467">Returns hello minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="20d87-468">parameters</span><span class="sxs-lookup"><span data-stu-id="20d87-468">Parameters</span></span>

| <span data-ttu-id="20d87-469">Parametro</span><span class="sxs-lookup"><span data-stu-id="20d87-469">Parameter</span></span> | <span data-ttu-id="20d87-470">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="20d87-470">Required</span></span> | <span data-ttu-id="20d87-471">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-471">Type</span></span> | <span data-ttu-id="20d87-472">Descrizione</span><span class="sxs-lookup"><span data-stu-id="20d87-472">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="20d87-473">arg1</span><span class="sxs-lookup"><span data-stu-id="20d87-473">arg1</span></span> |<span data-ttu-id="20d87-474">Sì</span><span class="sxs-lookup"><span data-stu-id="20d87-474">Yes</span></span> |<span data-ttu-id="20d87-475">matrice di numeri interi o elenco di numeri interi delimitato da virgole</span><span class="sxs-lookup"><span data-stu-id="20d87-475">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="20d87-476">Hello raccolta tooget hello valore minimo.</span><span class="sxs-lookup"><span data-stu-id="20d87-476">hello collection tooget hello minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="20d87-477">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="20d87-477">Return value</span></span>

<span data-ttu-id="20d87-478">Un integer che rappresenta il valore minimo di hello.</span><span class="sxs-lookup"><span data-stu-id="20d87-478">An int representing hello minimum value.</span></span>

### <a name="example"></a><span data-ttu-id="20d87-479">Esempio</span><span class="sxs-lookup"><span data-stu-id="20d87-479">Example</span></span>

<span data-ttu-id="20d87-480">Hello seguente esempio viene illustrato come toouse min con una matrice e un elenco di numeri interi:</span><span class="sxs-lookup"><span data-stu-id="20d87-480">hello following example shows how toouse min with an array and a list of integers:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [0,3,2,5,4]
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "int",
            "value": "[min(parameters('arrayToTest'))]"
        },
        "intOutput": {
            "type": "int",
            "value": "[min(0,3,2,5,4)]"
        }
    }
}
```

<span data-ttu-id="20d87-481">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="20d87-481">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="20d87-482">Nome</span><span class="sxs-lookup"><span data-stu-id="20d87-482">Name</span></span> | <span data-ttu-id="20d87-483">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-483">Type</span></span> | <span data-ttu-id="20d87-484">Valore</span><span class="sxs-lookup"><span data-stu-id="20d87-484">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="20d87-485">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="20d87-485">arrayOutput</span></span> | <span data-ttu-id="20d87-486">int</span><span class="sxs-lookup"><span data-stu-id="20d87-486">Int</span></span> | <span data-ttu-id="20d87-487">0</span><span class="sxs-lookup"><span data-stu-id="20d87-487">0</span></span> |
| <span data-ttu-id="20d87-488">intOutput</span><span class="sxs-lookup"><span data-stu-id="20d87-488">intOutput</span></span> | <span data-ttu-id="20d87-489">int</span><span class="sxs-lookup"><span data-stu-id="20d87-489">Int</span></span> | <span data-ttu-id="20d87-490">0</span><span class="sxs-lookup"><span data-stu-id="20d87-490">0</span></span> |

<a id="max" />

## <a name="max"></a><span data-ttu-id="20d87-491">max</span><span class="sxs-lookup"><span data-stu-id="20d87-491">max</span></span>
`max(arg1)`

<span data-ttu-id="20d87-492">Restituisce hello valore massimo da una matrice di interi o un elenco delimitato da virgole di numeri interi.</span><span class="sxs-lookup"><span data-stu-id="20d87-492">Returns hello maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="20d87-493">parameters</span><span class="sxs-lookup"><span data-stu-id="20d87-493">Parameters</span></span>

| <span data-ttu-id="20d87-494">Parametro</span><span class="sxs-lookup"><span data-stu-id="20d87-494">Parameter</span></span> | <span data-ttu-id="20d87-495">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="20d87-495">Required</span></span> | <span data-ttu-id="20d87-496">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-496">Type</span></span> | <span data-ttu-id="20d87-497">Descrizione</span><span class="sxs-lookup"><span data-stu-id="20d87-497">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="20d87-498">arg1</span><span class="sxs-lookup"><span data-stu-id="20d87-498">arg1</span></span> |<span data-ttu-id="20d87-499">Sì</span><span class="sxs-lookup"><span data-stu-id="20d87-499">Yes</span></span> |<span data-ttu-id="20d87-500">matrice di numeri interi o elenco di numeri interi delimitato da virgole</span><span class="sxs-lookup"><span data-stu-id="20d87-500">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="20d87-501">Hello raccolta tooget hello valore massimo.</span><span class="sxs-lookup"><span data-stu-id="20d87-501">hello collection tooget hello maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="20d87-502">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="20d87-502">Return value</span></span>

<span data-ttu-id="20d87-503">Un integer che rappresenta il valore massimo di hello.</span><span class="sxs-lookup"><span data-stu-id="20d87-503">An int representing hello maximum value.</span></span>

### <a name="example"></a><span data-ttu-id="20d87-504">Esempio</span><span class="sxs-lookup"><span data-stu-id="20d87-504">Example</span></span>

<span data-ttu-id="20d87-505">Hello seguente esempio viene illustrato come toouse max a una matrice e un elenco di numeri interi:</span><span class="sxs-lookup"><span data-stu-id="20d87-505">hello following example shows how toouse max with an array and a list of integers:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [0,3,2,5,4]
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "int",
            "value": "[max(parameters('arrayToTest'))]"
        },
        "intOutput": {
            "type": "int",
            "value": "[max(0,3,2,5,4)]"
        }
    }
}
```

<span data-ttu-id="20d87-506">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="20d87-506">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="20d87-507">Nome</span><span class="sxs-lookup"><span data-stu-id="20d87-507">Name</span></span> | <span data-ttu-id="20d87-508">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-508">Type</span></span> | <span data-ttu-id="20d87-509">Valore</span><span class="sxs-lookup"><span data-stu-id="20d87-509">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="20d87-510">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="20d87-510">arrayOutput</span></span> | <span data-ttu-id="20d87-511">int</span><span class="sxs-lookup"><span data-stu-id="20d87-511">Int</span></span> | <span data-ttu-id="20d87-512">5</span><span class="sxs-lookup"><span data-stu-id="20d87-512">5</span></span> |
| <span data-ttu-id="20d87-513">intOutput</span><span class="sxs-lookup"><span data-stu-id="20d87-513">intOutput</span></span> | <span data-ttu-id="20d87-514">int</span><span class="sxs-lookup"><span data-stu-id="20d87-514">Int</span></span> | <span data-ttu-id="20d87-515">5</span><span class="sxs-lookup"><span data-stu-id="20d87-515">5</span></span> |

<a id="range" />

## <a name="range"></a><span data-ttu-id="20d87-516">range</span><span class="sxs-lookup"><span data-stu-id="20d87-516">range</span></span>
`range(startingInteger, numberOfElements)`

<span data-ttu-id="20d87-517">Crea una matrice di numeri interi da un numero intero iniziale, contenente un dato numero di elementi.</span><span class="sxs-lookup"><span data-stu-id="20d87-517">Creates an array of integers from a starting integer and containing a number of items.</span></span>

### <a name="parameters"></a><span data-ttu-id="20d87-518">Parametri</span><span class="sxs-lookup"><span data-stu-id="20d87-518">Parameters</span></span>

| <span data-ttu-id="20d87-519">Parametro</span><span class="sxs-lookup"><span data-stu-id="20d87-519">Parameter</span></span> | <span data-ttu-id="20d87-520">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="20d87-520">Required</span></span> | <span data-ttu-id="20d87-521">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-521">Type</span></span> | <span data-ttu-id="20d87-522">Descrizione</span><span class="sxs-lookup"><span data-stu-id="20d87-522">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="20d87-523">startingInteger</span><span class="sxs-lookup"><span data-stu-id="20d87-523">startingInteger</span></span> |<span data-ttu-id="20d87-524">Sì</span><span class="sxs-lookup"><span data-stu-id="20d87-524">Yes</span></span> |<span data-ttu-id="20d87-525">int</span><span class="sxs-lookup"><span data-stu-id="20d87-525">int</span></span> |<span data-ttu-id="20d87-526">Hello primo intero hello matrice.</span><span class="sxs-lookup"><span data-stu-id="20d87-526">hello first integer in hello array.</span></span> |
| <span data-ttu-id="20d87-527">numberofElements</span><span class="sxs-lookup"><span data-stu-id="20d87-527">numberofElements</span></span> |<span data-ttu-id="20d87-528">Sì</span><span class="sxs-lookup"><span data-stu-id="20d87-528">Yes</span></span> |<span data-ttu-id="20d87-529">int</span><span class="sxs-lookup"><span data-stu-id="20d87-529">int</span></span> |<span data-ttu-id="20d87-530">numero di Hello dei numeri interi nella matrice hello.</span><span class="sxs-lookup"><span data-stu-id="20d87-530">hello number of integers in hello array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="20d87-531">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="20d87-531">Return value</span></span>

<span data-ttu-id="20d87-532">Matrice di numeri interi.</span><span class="sxs-lookup"><span data-stu-id="20d87-532">An array of integers.</span></span>

### <a name="example"></a><span data-ttu-id="20d87-533">Esempio</span><span class="sxs-lookup"><span data-stu-id="20d87-533">Example</span></span>

<span data-ttu-id="20d87-534">Hello di esempio seguente viene illustrato come toouse hello funzione intervallo:</span><span class="sxs-lookup"><span data-stu-id="20d87-534">hello following example shows how toouse hello range function:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "startingInt": {
            "type": "int",
            "defaultValue": 5
        },
        "numberOfElements": {
            "type": "int",
            "defaultValue": 3
        }
    },
    "resources": [],
    "outputs": {
        "rangeOutput": {
            "type": "array",
            "value": "[range(parameters('startingInt'),parameters('numberOfElements'))]"
        }
    }
}
```

<span data-ttu-id="20d87-535">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="20d87-535">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="20d87-536">Nome</span><span class="sxs-lookup"><span data-stu-id="20d87-536">Name</span></span> | <span data-ttu-id="20d87-537">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-537">Type</span></span> | <span data-ttu-id="20d87-538">Valore</span><span class="sxs-lookup"><span data-stu-id="20d87-538">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="20d87-539">rangeOutput</span><span class="sxs-lookup"><span data-stu-id="20d87-539">rangeOutput</span></span> | <span data-ttu-id="20d87-540">Array</span><span class="sxs-lookup"><span data-stu-id="20d87-540">Array</span></span> | <span data-ttu-id="20d87-541">[5, 6, 7]</span><span class="sxs-lookup"><span data-stu-id="20d87-541">[5, 6, 7]</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="20d87-542">skip</span><span class="sxs-lookup"><span data-stu-id="20d87-542">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="20d87-543">Restituisce una matrice con tutti gli elementi di hello dopo il numero specificato nella matrice hello hello o restituisce una stringa con tutti i caratteri di hello dopo hello numero specificato nella stringa hello.</span><span class="sxs-lookup"><span data-stu-id="20d87-543">Returns an array with all hello elements after hello specified number in hello array, or returns a string with all hello characters after hello specified number in hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="20d87-544">parameters</span><span class="sxs-lookup"><span data-stu-id="20d87-544">Parameters</span></span>

| <span data-ttu-id="20d87-545">Parametro</span><span class="sxs-lookup"><span data-stu-id="20d87-545">Parameter</span></span> | <span data-ttu-id="20d87-546">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="20d87-546">Required</span></span> | <span data-ttu-id="20d87-547">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-547">Type</span></span> | <span data-ttu-id="20d87-548">Descrizione</span><span class="sxs-lookup"><span data-stu-id="20d87-548">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="20d87-549">originalValue</span><span class="sxs-lookup"><span data-stu-id="20d87-549">originalValue</span></span> |<span data-ttu-id="20d87-550">Sì</span><span class="sxs-lookup"><span data-stu-id="20d87-550">Yes</span></span> |<span data-ttu-id="20d87-551">stringa o matrice</span><span class="sxs-lookup"><span data-stu-id="20d87-551">array or string</span></span> |<span data-ttu-id="20d87-552">Hello toouse matrice o stringa per l'omissione.</span><span class="sxs-lookup"><span data-stu-id="20d87-552">hello array or string toouse for skipping.</span></span> |
| <span data-ttu-id="20d87-553">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="20d87-553">numberToSkip</span></span> |<span data-ttu-id="20d87-554">Sì</span><span class="sxs-lookup"><span data-stu-id="20d87-554">Yes</span></span> |<span data-ttu-id="20d87-555">int</span><span class="sxs-lookup"><span data-stu-id="20d87-555">int</span></span> |<span data-ttu-id="20d87-556">numero di Hello di tooskip elementi o i caratteri.</span><span class="sxs-lookup"><span data-stu-id="20d87-556">hello number of elements or characters tooskip.</span></span> <span data-ttu-id="20d87-557">Se questo valore è 0 o meno, tutti gli elementi di hello o vengono restituiti i caratteri nel valore hello.</span><span class="sxs-lookup"><span data-stu-id="20d87-557">If this value is 0 or less, all hello elements or characters in hello value are returned.</span></span> <span data-ttu-id="20d87-558">Se è maggiore della lunghezza della stringa o matrice hello hello, viene restituita una matrice vuota o una stringa.</span><span class="sxs-lookup"><span data-stu-id="20d87-558">If it is larger than hello length of hello array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="20d87-559">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="20d87-559">Return value</span></span>

<span data-ttu-id="20d87-560">Stringa o matrice.</span><span class="sxs-lookup"><span data-stu-id="20d87-560">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="20d87-561">Esempio</span><span class="sxs-lookup"><span data-stu-id="20d87-561">Example</span></span>

<span data-ttu-id="20d87-562">Hello seguente esempio Ignora hello numero specificato di elementi nella matrice hello e hello numero specificato di caratteri in una stringa.</span><span class="sxs-lookup"><span data-stu-id="20d87-562">hello following example skips hello specified number of elements in hello array, and hello specified number of characters in a string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "elementsToSkip": {
            "type": "int",
            "defaultValue": 2
        },
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        },
        "charactersToSkip": {
            "type": "int",
            "defaultValue": 4
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "array",
            "value": "[skip(parameters('testArray'),parameters('elementsToSkip'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[skip(parameters('testString'),parameters('charactersToSkip'))]"
        }
    }
}
```

<span data-ttu-id="20d87-563">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="20d87-563">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="20d87-564">Nome</span><span class="sxs-lookup"><span data-stu-id="20d87-564">Name</span></span> | <span data-ttu-id="20d87-565">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-565">Type</span></span> | <span data-ttu-id="20d87-566">Valore</span><span class="sxs-lookup"><span data-stu-id="20d87-566">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="20d87-567">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="20d87-567">arrayOutput</span></span> | <span data-ttu-id="20d87-568">Array</span><span class="sxs-lookup"><span data-stu-id="20d87-568">Array</span></span> | <span data-ttu-id="20d87-569">["three"]</span><span class="sxs-lookup"><span data-stu-id="20d87-569">["three"]</span></span> |
| <span data-ttu-id="20d87-570">stringOutput</span><span class="sxs-lookup"><span data-stu-id="20d87-570">stringOutput</span></span> | <span data-ttu-id="20d87-571">String</span><span class="sxs-lookup"><span data-stu-id="20d87-571">String</span></span> | <span data-ttu-id="20d87-572">two three</span><span class="sxs-lookup"><span data-stu-id="20d87-572">two three</span></span> |

<a id="take" />

## <a name="take"></a><span data-ttu-id="20d87-573">take</span><span class="sxs-lookup"><span data-stu-id="20d87-573">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="20d87-574">Restituisce una matrice con hello specificato numero di elementi dall'inizio della matrice hello di hello o una stringa con hello numero specificato di caratteri dall'inizio di hello della stringa hello.</span><span class="sxs-lookup"><span data-stu-id="20d87-574">Returns an array with hello specified number of elements from hello start of hello array, or a string with hello specified number of characters from hello start of hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="20d87-575">parameters</span><span class="sxs-lookup"><span data-stu-id="20d87-575">Parameters</span></span>

| <span data-ttu-id="20d87-576">Parametro</span><span class="sxs-lookup"><span data-stu-id="20d87-576">Parameter</span></span> | <span data-ttu-id="20d87-577">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="20d87-577">Required</span></span> | <span data-ttu-id="20d87-578">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-578">Type</span></span> | <span data-ttu-id="20d87-579">Descrizione</span><span class="sxs-lookup"><span data-stu-id="20d87-579">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="20d87-580">originalValue</span><span class="sxs-lookup"><span data-stu-id="20d87-580">originalValue</span></span> |<span data-ttu-id="20d87-581">Sì</span><span class="sxs-lookup"><span data-stu-id="20d87-581">Yes</span></span> |<span data-ttu-id="20d87-582">stringa o matrice</span><span class="sxs-lookup"><span data-stu-id="20d87-582">array or string</span></span> |<span data-ttu-id="20d87-583">Hello stringa o matrice di elementi di hello tootake da.</span><span class="sxs-lookup"><span data-stu-id="20d87-583">hello array or string tootake hello elements from.</span></span> |
| <span data-ttu-id="20d87-584">numberToTake</span><span class="sxs-lookup"><span data-stu-id="20d87-584">numberToTake</span></span> |<span data-ttu-id="20d87-585">Sì</span><span class="sxs-lookup"><span data-stu-id="20d87-585">Yes</span></span> |<span data-ttu-id="20d87-586">int</span><span class="sxs-lookup"><span data-stu-id="20d87-586">int</span></span> |<span data-ttu-id="20d87-587">numero di Hello di tootake elementi o i caratteri.</span><span class="sxs-lookup"><span data-stu-id="20d87-587">hello number of elements or characters tootake.</span></span> <span data-ttu-id="20d87-588">Se il valore è minore o uguale a 0, viene restituita una stringa o un matrice vuota.</span><span class="sxs-lookup"><span data-stu-id="20d87-588">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="20d87-589">Se è maggiore della lunghezza di hello di hello matrice o stringa specificato, vengono restituiti tutti gli elementi hello hello matrice o stringa.</span><span class="sxs-lookup"><span data-stu-id="20d87-589">If it is larger than hello length of hello given array or string, all hello elements in hello array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="20d87-590">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="20d87-590">Return value</span></span>

<span data-ttu-id="20d87-591">Stringa o matrice.</span><span class="sxs-lookup"><span data-stu-id="20d87-591">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="20d87-592">Esempio</span><span class="sxs-lookup"><span data-stu-id="20d87-592">Example</span></span>

<span data-ttu-id="20d87-593">Hello seguente esempio accetta hello numero specificato di elementi dalla matrice hello e i caratteri di una stringa.</span><span class="sxs-lookup"><span data-stu-id="20d87-593">hello following example takes hello specified number of elements from hello array, and characters from a string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "elementsToTake": {
            "type": "int",
            "defaultValue": 2
        },
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        },
        "charactersToTake": {
            "type": "int",
            "defaultValue": 2
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "array",
            "value": "[take(parameters('testArray'),parameters('elementsToTake'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[take(parameters('testString'),parameters('charactersToTake'))]"
        }
    }
}
```

<span data-ttu-id="20d87-594">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="20d87-594">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="20d87-595">Nome</span><span class="sxs-lookup"><span data-stu-id="20d87-595">Name</span></span> | <span data-ttu-id="20d87-596">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-596">Type</span></span> | <span data-ttu-id="20d87-597">Valore</span><span class="sxs-lookup"><span data-stu-id="20d87-597">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="20d87-598">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="20d87-598">arrayOutput</span></span> | <span data-ttu-id="20d87-599">Array</span><span class="sxs-lookup"><span data-stu-id="20d87-599">Array</span></span> | <span data-ttu-id="20d87-600">["one", "two"]</span><span class="sxs-lookup"><span data-stu-id="20d87-600">["one", "two"]</span></span> |
| <span data-ttu-id="20d87-601">stringOutput</span><span class="sxs-lookup"><span data-stu-id="20d87-601">stringOutput</span></span> | <span data-ttu-id="20d87-602">String</span><span class="sxs-lookup"><span data-stu-id="20d87-602">String</span></span> | <span data-ttu-id="20d87-603">in</span><span class="sxs-lookup"><span data-stu-id="20d87-603">on</span></span> |

<a id="union" />

## <a name="union"></a><span data-ttu-id="20d87-604">union</span><span class="sxs-lookup"><span data-stu-id="20d87-604">union</span></span>
`union(arg1, arg2, arg3, ...)`

<span data-ttu-id="20d87-605">Restituisce una matrice o un oggetto con tutti gli elementi dai parametri hello.</span><span class="sxs-lookup"><span data-stu-id="20d87-605">Returns a single array or object with all elements from hello parameters.</span></span> <span data-ttu-id="20d87-606">Valori e chiavi duplicati sono inclusi una sola volta.</span><span class="sxs-lookup"><span data-stu-id="20d87-606">Duplicate values or keys are only included once.</span></span>

### <a name="parameters"></a><span data-ttu-id="20d87-607">Parametri</span><span class="sxs-lookup"><span data-stu-id="20d87-607">Parameters</span></span>

| <span data-ttu-id="20d87-608">Parametro</span><span class="sxs-lookup"><span data-stu-id="20d87-608">Parameter</span></span> | <span data-ttu-id="20d87-609">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="20d87-609">Required</span></span> | <span data-ttu-id="20d87-610">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-610">Type</span></span> | <span data-ttu-id="20d87-611">Descrizione</span><span class="sxs-lookup"><span data-stu-id="20d87-611">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="20d87-612">arg1</span><span class="sxs-lookup"><span data-stu-id="20d87-612">arg1</span></span> |<span data-ttu-id="20d87-613">Sì</span><span class="sxs-lookup"><span data-stu-id="20d87-613">Yes</span></span> |<span data-ttu-id="20d87-614">matrice o oggetto</span><span class="sxs-lookup"><span data-stu-id="20d87-614">array or object</span></span> |<span data-ttu-id="20d87-615">Hello toouse prima di valore per l'aggiunta di elementi.</span><span class="sxs-lookup"><span data-stu-id="20d87-615">hello first value toouse for joining elements.</span></span> |
| <span data-ttu-id="20d87-616">arg2</span><span class="sxs-lookup"><span data-stu-id="20d87-616">arg2</span></span> |<span data-ttu-id="20d87-617">Sì</span><span class="sxs-lookup"><span data-stu-id="20d87-617">Yes</span></span> |<span data-ttu-id="20d87-618">matrice o oggetto</span><span class="sxs-lookup"><span data-stu-id="20d87-618">array or object</span></span> |<span data-ttu-id="20d87-619">Hello secondo valore toouse per l'aggiunta di elementi.</span><span class="sxs-lookup"><span data-stu-id="20d87-619">hello second value toouse for joining elements.</span></span> |
| <span data-ttu-id="20d87-620">argomenti aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="20d87-620">additional arguments</span></span> |<span data-ttu-id="20d87-621">No</span><span class="sxs-lookup"><span data-stu-id="20d87-621">No</span></span> |<span data-ttu-id="20d87-622">matrice o oggetto</span><span class="sxs-lookup"><span data-stu-id="20d87-622">array or object</span></span> |<span data-ttu-id="20d87-623">Toouse valori aggiuntivi per l'aggiunta di elementi.</span><span class="sxs-lookup"><span data-stu-id="20d87-623">Additional values toouse for joining elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="20d87-624">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="20d87-624">Return value</span></span>

<span data-ttu-id="20d87-625">Una matrice o un oggetto.</span><span class="sxs-lookup"><span data-stu-id="20d87-625">An array or object.</span></span>

### <a name="example"></a><span data-ttu-id="20d87-626">Esempio</span><span class="sxs-lookup"><span data-stu-id="20d87-626">Example</span></span>

<span data-ttu-id="20d87-627">Hello esempio viene illustrato come unione toouse con matrici e gli oggetti seguenti:</span><span class="sxs-lookup"><span data-stu-id="20d87-627">hello following example shows how toouse union with arrays and objects:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"three": "c", "four": "d", "five": "e"}
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["three", "four"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "objectOutput": {
            "type": "object",
            "value": "[union(parameters('firstObject'), parameters('secondObject'))]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[union(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

<span data-ttu-id="20d87-628">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="20d87-628">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="20d87-629">Nome</span><span class="sxs-lookup"><span data-stu-id="20d87-629">Name</span></span> | <span data-ttu-id="20d87-630">Tipo</span><span class="sxs-lookup"><span data-stu-id="20d87-630">Type</span></span> | <span data-ttu-id="20d87-631">Valore</span><span class="sxs-lookup"><span data-stu-id="20d87-631">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="20d87-632">objectOutput</span><span class="sxs-lookup"><span data-stu-id="20d87-632">objectOutput</span></span> | <span data-ttu-id="20d87-633">Oggetto</span><span class="sxs-lookup"><span data-stu-id="20d87-633">Object</span></span> | <span data-ttu-id="20d87-634">{"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"}</span><span class="sxs-lookup"><span data-stu-id="20d87-634">{"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"}</span></span> |
| <span data-ttu-id="20d87-635">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="20d87-635">arrayOutput</span></span> | <span data-ttu-id="20d87-636">Array</span><span class="sxs-lookup"><span data-stu-id="20d87-636">Array</span></span> | <span data-ttu-id="20d87-637">["one", "two", "three", "four"]</span><span class="sxs-lookup"><span data-stu-id="20d87-637">["one", "two", "three", "four"]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="20d87-638">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="20d87-638">Next steps</span></span>
* <span data-ttu-id="20d87-639">Per una descrizione delle sezioni hello in un modello di gestione risorse di Azure, vedere [modelli Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="20d87-639">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="20d87-640">toomerge più modelli, vedere [con modelli collegati con Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="20d87-640">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="20d87-641">tooiterate un numero specificato di volte durante la creazione di un tipo di risorsa, vedere [creare più istanze delle risorse in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="20d87-641">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="20d87-642">toosee come modello hello toodeploy è stato creato, vedere [distribuire un'applicazione con il modello di gestione risorse di Azure](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="20d87-642">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

