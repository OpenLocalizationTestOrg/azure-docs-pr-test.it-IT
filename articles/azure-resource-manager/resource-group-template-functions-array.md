---
title: Funzioni del modello di Azure Resource Manager - matrici e oggetti | Microsoft Docs
description: Descrive le funzioni da usare in un modello di Azure Resource Manager per l'uso di matrici e oggetti.
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
ms.openlocfilehash: 0bd9ec41761c9ce575f3bcf4d1f8e8578b83e01c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="array-and-object-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="fd0b4-103">Funzioni di matrice e oggetto per i modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fd0b4-103">Array and object functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="fd0b4-104">Resource Manager offre diverse funzioni per l'uso di matrici e oggetti.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-104">Resource Manager provides several functions for working with arrays and objects.</span></span>

* [<span data-ttu-id="fd0b4-105">array</span><span class="sxs-lookup"><span data-stu-id="fd0b4-105">array</span></span>](#array)
* [<span data-ttu-id="fd0b4-106">coalesce</span><span class="sxs-lookup"><span data-stu-id="fd0b4-106">coalesce</span></span>](#coalesce)
* [<span data-ttu-id="fd0b4-107">concat</span><span class="sxs-lookup"><span data-stu-id="fd0b4-107">concat</span></span>](#concat)
* [<span data-ttu-id="fd0b4-108">contains</span><span class="sxs-lookup"><span data-stu-id="fd0b4-108">contains</span></span>](#contains)
* [<span data-ttu-id="fd0b4-109">createArray</span><span class="sxs-lookup"><span data-stu-id="fd0b4-109">createArray</span></span>](#createarray)
* [<span data-ttu-id="fd0b4-110">empty</span><span class="sxs-lookup"><span data-stu-id="fd0b4-110">empty</span></span>](#empty)
* [<span data-ttu-id="fd0b4-111">first</span><span class="sxs-lookup"><span data-stu-id="fd0b4-111">first</span></span>](#first)
* [<span data-ttu-id="fd0b4-112">intersection</span><span class="sxs-lookup"><span data-stu-id="fd0b4-112">intersection</span></span>](#intersection)
* [<span data-ttu-id="fd0b4-113">json</span><span class="sxs-lookup"><span data-stu-id="fd0b4-113">json</span></span>](#json)
* [<span data-ttu-id="fd0b4-114">last</span><span class="sxs-lookup"><span data-stu-id="fd0b4-114">last</span></span>](#last)
* [<span data-ttu-id="fd0b4-115">length</span><span class="sxs-lookup"><span data-stu-id="fd0b4-115">length</span></span>](#length)
* [<span data-ttu-id="fd0b4-116">min</span><span class="sxs-lookup"><span data-stu-id="fd0b4-116">min</span></span>](#min)
* [<span data-ttu-id="fd0b4-117">max</span><span class="sxs-lookup"><span data-stu-id="fd0b4-117">max</span></span>](#max)
* [<span data-ttu-id="fd0b4-118">range</span><span class="sxs-lookup"><span data-stu-id="fd0b4-118">range</span></span>](#range)
* [<span data-ttu-id="fd0b4-119">skip</span><span class="sxs-lookup"><span data-stu-id="fd0b4-119">skip</span></span>](#skip)
* [<span data-ttu-id="fd0b4-120">take</span><span class="sxs-lookup"><span data-stu-id="fd0b4-120">take</span></span>](#take)
* [<span data-ttu-id="fd0b4-121">union</span><span class="sxs-lookup"><span data-stu-id="fd0b4-121">union</span></span>](#union)

<span data-ttu-id="fd0b4-122">Per ottenere una matrice di valori stringa delimitata da un valore, vedere [split](resource-group-template-functions-string.md#split).</span><span class="sxs-lookup"><span data-stu-id="fd0b4-122">To get an array of string values delimited by a value, see [split](resource-group-template-functions-string.md#split).</span></span>

<a id="array" />

## <a name="array"></a><span data-ttu-id="fd0b4-123">array</span><span class="sxs-lookup"><span data-stu-id="fd0b4-123">array</span></span>
`array(convertToArray)`

<span data-ttu-id="fd0b4-124">Converte il valore in matrice.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-124">Converts the value to an array.</span></span>

### <a name="parameters"></a><span data-ttu-id="fd0b4-125">Parametri</span><span class="sxs-lookup"><span data-stu-id="fd0b4-125">Parameters</span></span>

| <span data-ttu-id="fd0b4-126">Parametro</span><span class="sxs-lookup"><span data-stu-id="fd0b4-126">Parameter</span></span> | <span data-ttu-id="fd0b4-127">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="fd0b4-127">Required</span></span> | <span data-ttu-id="fd0b4-128">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-128">Type</span></span> | <span data-ttu-id="fd0b4-129">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fd0b4-129">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="fd0b4-130">convertToArray</span><span class="sxs-lookup"><span data-stu-id="fd0b4-130">convertToArray</span></span> |<span data-ttu-id="fd0b4-131">Sì</span><span class="sxs-lookup"><span data-stu-id="fd0b4-131">Yes</span></span> |<span data-ttu-id="fd0b4-132">numero intero, stringa, matrice o oggetto</span><span class="sxs-lookup"><span data-stu-id="fd0b4-132">int, string, array, or object</span></span> |<span data-ttu-id="fd0b4-133">Valore da convertire in matrice.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-133">The value to convert to an array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="fd0b4-134">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="fd0b4-134">Return value</span></span>

<span data-ttu-id="fd0b4-135">Una matrice.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-135">An array.</span></span>

### <a name="example"></a><span data-ttu-id="fd0b4-136">Esempio</span><span class="sxs-lookup"><span data-stu-id="fd0b4-136">Example</span></span>

<span data-ttu-id="fd0b4-137">L'esempio seguente mostra come usare la funzione matrice con tipi diversi.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-137">The following example shows how to use the array function with different types.</span></span>

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

<span data-ttu-id="fd0b4-138">L'output dell'esempio precedente con i valori predefiniti è il seguente:</span><span class="sxs-lookup"><span data-stu-id="fd0b4-138">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="fd0b4-139">Nome</span><span class="sxs-lookup"><span data-stu-id="fd0b4-139">Name</span></span> | <span data-ttu-id="fd0b4-140">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-140">Type</span></span> | <span data-ttu-id="fd0b4-141">Valore</span><span class="sxs-lookup"><span data-stu-id="fd0b4-141">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="fd0b4-142">intOutput</span><span class="sxs-lookup"><span data-stu-id="fd0b4-142">intOutput</span></span> | <span data-ttu-id="fd0b4-143">Array</span><span class="sxs-lookup"><span data-stu-id="fd0b4-143">Array</span></span> | <span data-ttu-id="fd0b4-144">[1]</span><span class="sxs-lookup"><span data-stu-id="fd0b4-144">[1]</span></span> |
| <span data-ttu-id="fd0b4-145">stringOutput</span><span class="sxs-lookup"><span data-stu-id="fd0b4-145">stringOutput</span></span> | <span data-ttu-id="fd0b4-146">Array</span><span class="sxs-lookup"><span data-stu-id="fd0b4-146">Array</span></span> | <span data-ttu-id="fd0b4-147">["a"]</span><span class="sxs-lookup"><span data-stu-id="fd0b4-147">["a"]</span></span> |
| <span data-ttu-id="fd0b4-148">objectOutput</span><span class="sxs-lookup"><span data-stu-id="fd0b4-148">objectOutput</span></span> | <span data-ttu-id="fd0b4-149">Array</span><span class="sxs-lookup"><span data-stu-id="fd0b4-149">Array</span></span> | <span data-ttu-id="fd0b4-150">[{"a": "b", "c": "d"}]</span><span class="sxs-lookup"><span data-stu-id="fd0b4-150">[{"a": "b", "c": "d"}]</span></span> |

<a id="coalesce" />

## <a name="coalesce"></a><span data-ttu-id="fd0b4-151">coalesce</span><span class="sxs-lookup"><span data-stu-id="fd0b4-151">coalesce</span></span>
`coalesce(arg1, arg2, arg3, ...)`

<span data-ttu-id="fd0b4-152">Restituisce il primo valore non null dai parametri.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-152">Returns first non-null value from the parameters.</span></span> <span data-ttu-id="fd0b4-153">Stringhe vuote, matrici vuote e oggetti vuoti sono non null.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-153">Empty strings, empty arrays, and empty objects are not null.</span></span>

### <a name="parameters"></a><span data-ttu-id="fd0b4-154">Parametri</span><span class="sxs-lookup"><span data-stu-id="fd0b4-154">Parameters</span></span>

| <span data-ttu-id="fd0b4-155">Parametro</span><span class="sxs-lookup"><span data-stu-id="fd0b4-155">Parameter</span></span> | <span data-ttu-id="fd0b4-156">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="fd0b4-156">Required</span></span> | <span data-ttu-id="fd0b4-157">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-157">Type</span></span> | <span data-ttu-id="fd0b4-158">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fd0b4-158">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="fd0b4-159">arg1</span><span class="sxs-lookup"><span data-stu-id="fd0b4-159">arg1</span></span> |<span data-ttu-id="fd0b4-160">Sì</span><span class="sxs-lookup"><span data-stu-id="fd0b4-160">Yes</span></span> |<span data-ttu-id="fd0b4-161">numero intero, stringa, matrice o oggetto</span><span class="sxs-lookup"><span data-stu-id="fd0b4-161">int, string, array, or object</span></span> |<span data-ttu-id="fd0b4-162">Il primo valore da controllare per verificare se è null.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-162">The first value to test for null.</span></span> |
| <span data-ttu-id="fd0b4-163">argomenti aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="fd0b4-163">additional args</span></span> |<span data-ttu-id="fd0b4-164">No</span><span class="sxs-lookup"><span data-stu-id="fd0b4-164">No</span></span> |<span data-ttu-id="fd0b4-165">numero intero, stringa, matrice o oggetto</span><span class="sxs-lookup"><span data-stu-id="fd0b4-165">int, string, array, or object</span></span> |<span data-ttu-id="fd0b4-166">Valori aggiuntivi da controllare per verificare se sono null.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-166">Additional values to test for null.</span></span> |

### <a name="return-value"></a><span data-ttu-id="fd0b4-167">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="fd0b4-167">Return value</span></span>

<span data-ttu-id="fd0b4-168">Valore dei primi parametri non null, che può essere una stringa, un numero intero, una matrice o un oggetto.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-168">The value of the first non-null parameters, which can be a string, int, array, or object.</span></span> <span data-ttu-id="fd0b4-169">Null se tutti i parametri sono null.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-169">Null if all parameters are null.</span></span> 

### <a name="example"></a><span data-ttu-id="fd0b4-170">Esempio</span><span class="sxs-lookup"><span data-stu-id="fd0b4-170">Example</span></span>

<span data-ttu-id="fd0b4-171">L'esempio seguente illustra l'output per diversi usi di coalesce.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-171">The following example shows the output from different uses of coalesce.</span></span>

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

<span data-ttu-id="fd0b4-172">L'output dell'esempio precedente con i valori predefiniti è il seguente:</span><span class="sxs-lookup"><span data-stu-id="fd0b4-172">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="fd0b4-173">Nome</span><span class="sxs-lookup"><span data-stu-id="fd0b4-173">Name</span></span> | <span data-ttu-id="fd0b4-174">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-174">Type</span></span> | <span data-ttu-id="fd0b4-175">Valore</span><span class="sxs-lookup"><span data-stu-id="fd0b4-175">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="fd0b4-176">stringOutput</span><span class="sxs-lookup"><span data-stu-id="fd0b4-176">stringOutput</span></span> | <span data-ttu-id="fd0b4-177">String</span><span class="sxs-lookup"><span data-stu-id="fd0b4-177">String</span></span> | <span data-ttu-id="fd0b4-178">default</span><span class="sxs-lookup"><span data-stu-id="fd0b4-178">default</span></span> |
| <span data-ttu-id="fd0b4-179">intOutput</span><span class="sxs-lookup"><span data-stu-id="fd0b4-179">intOutput</span></span> | <span data-ttu-id="fd0b4-180">int</span><span class="sxs-lookup"><span data-stu-id="fd0b4-180">Int</span></span> | <span data-ttu-id="fd0b4-181">1</span><span class="sxs-lookup"><span data-stu-id="fd0b4-181">1</span></span> |
| <span data-ttu-id="fd0b4-182">objectOutput</span><span class="sxs-lookup"><span data-stu-id="fd0b4-182">objectOutput</span></span> | <span data-ttu-id="fd0b4-183">Oggetto</span><span class="sxs-lookup"><span data-stu-id="fd0b4-183">Object</span></span> | <span data-ttu-id="fd0b4-184">{"first": "default"}</span><span class="sxs-lookup"><span data-stu-id="fd0b4-184">{"first": "default"}</span></span> |
| <span data-ttu-id="fd0b4-185">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="fd0b4-185">arrayOutput</span></span> | <span data-ttu-id="fd0b4-186">Array</span><span class="sxs-lookup"><span data-stu-id="fd0b4-186">Array</span></span> | <span data-ttu-id="fd0b4-187">[1]</span><span class="sxs-lookup"><span data-stu-id="fd0b4-187">[1]</span></span> |
| <span data-ttu-id="fd0b4-188">emptyOutput</span><span class="sxs-lookup"><span data-stu-id="fd0b4-188">emptyOutput</span></span> | <span data-ttu-id="fd0b4-189">Booleano</span><span class="sxs-lookup"><span data-stu-id="fd0b4-189">Bool</span></span> | <span data-ttu-id="fd0b4-190">True </span><span class="sxs-lookup"><span data-stu-id="fd0b4-190">True</span></span> |

<a id="concat" />

## <a name="concat"></a><span data-ttu-id="fd0b4-191">concat</span><span class="sxs-lookup"><span data-stu-id="fd0b4-191">concat</span></span>
`concat(arg1, arg2, arg3, ...)`

<span data-ttu-id="fd0b4-192">Combina più matrici e restituisce la matrice concatenata oppure combina più valori di stringa e restituisce la stringa concatenata.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-192">Combines multiple arrays and returns the concatenated array, or combines multiple string values and returns the concatenated string.</span></span> 

### <a name="parameters"></a><span data-ttu-id="fd0b4-193">Parametri</span><span class="sxs-lookup"><span data-stu-id="fd0b4-193">Parameters</span></span>

| <span data-ttu-id="fd0b4-194">Parametro</span><span class="sxs-lookup"><span data-stu-id="fd0b4-194">Parameter</span></span> | <span data-ttu-id="fd0b4-195">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="fd0b4-195">Required</span></span> | <span data-ttu-id="fd0b4-196">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-196">Type</span></span> | <span data-ttu-id="fd0b4-197">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fd0b4-197">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="fd0b4-198">arg1</span><span class="sxs-lookup"><span data-stu-id="fd0b4-198">arg1</span></span> |<span data-ttu-id="fd0b4-199">Sì</span><span class="sxs-lookup"><span data-stu-id="fd0b4-199">Yes</span></span> |<span data-ttu-id="fd0b4-200">stringa o matrice</span><span class="sxs-lookup"><span data-stu-id="fd0b4-200">array or string</span></span> |<span data-ttu-id="fd0b4-201">La prima matrice o stringa per la concatenazione.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-201">The first array or string for concatenation.</span></span> |
| <span data-ttu-id="fd0b4-202">argomenti aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="fd0b4-202">additional arguments</span></span> |<span data-ttu-id="fd0b4-203">No</span><span class="sxs-lookup"><span data-stu-id="fd0b4-203">No</span></span> |<span data-ttu-id="fd0b4-204">stringa o matrice</span><span class="sxs-lookup"><span data-stu-id="fd0b4-204">array or string</span></span> |<span data-ttu-id="fd0b4-205">Matrici o stringhe aggiuntive in ordine sequenziale per la concatenazione.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-205">Additional arrays or strings in sequential order for concatenation.</span></span> |

<span data-ttu-id="fd0b4-206">Questa funzione può accettare qualsiasi numero di argomenti e può accettare stringhe o matrici per i parametri.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-206">This function can take any number of arguments, and can accept either strings or arrays for the parameters.</span></span>

### <a name="return-value"></a><span data-ttu-id="fd0b4-207">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="fd0b4-207">Return value</span></span>
<span data-ttu-id="fd0b4-208">Stringa o matrice di valori concatenati.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-208">A string or array of concatenated values.</span></span>

### <a name="example"></a><span data-ttu-id="fd0b4-209">Esempio</span><span class="sxs-lookup"><span data-stu-id="fd0b4-209">Example</span></span>

<span data-ttu-id="fd0b4-210">L'esempio seguente illustra come combinare due matrici.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-210">The following example shows how to combine two arrays.</span></span>

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

<span data-ttu-id="fd0b4-211">L'output dell'esempio precedente con i valori predefiniti è il seguente:</span><span class="sxs-lookup"><span data-stu-id="fd0b4-211">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="fd0b4-212">Nome</span><span class="sxs-lookup"><span data-stu-id="fd0b4-212">Name</span></span> | <span data-ttu-id="fd0b4-213">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-213">Type</span></span> | <span data-ttu-id="fd0b4-214">Valore</span><span class="sxs-lookup"><span data-stu-id="fd0b4-214">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="fd0b4-215">return</span><span class="sxs-lookup"><span data-stu-id="fd0b4-215">return</span></span> | <span data-ttu-id="fd0b4-216">Array</span><span class="sxs-lookup"><span data-stu-id="fd0b4-216">Array</span></span> | <span data-ttu-id="fd0b4-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="fd0b4-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<span data-ttu-id="fd0b4-218">L'esempio seguente illustra come combinare due valori stringa e restituisce una stringa concatenata.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-218">The following example shows how to combine two string values and return a concatenated string.</span></span>

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

<span data-ttu-id="fd0b4-219">L'output dell'esempio precedente con i valori predefiniti è il seguente:</span><span class="sxs-lookup"><span data-stu-id="fd0b4-219">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="fd0b4-220">Nome</span><span class="sxs-lookup"><span data-stu-id="fd0b4-220">Name</span></span> | <span data-ttu-id="fd0b4-221">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-221">Type</span></span> | <span data-ttu-id="fd0b4-222">Valore</span><span class="sxs-lookup"><span data-stu-id="fd0b4-222">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="fd0b4-223">concatOutput</span><span class="sxs-lookup"><span data-stu-id="fd0b4-223">concatOutput</span></span> | <span data-ttu-id="fd0b4-224">String</span><span class="sxs-lookup"><span data-stu-id="fd0b4-224">String</span></span> | <span data-ttu-id="fd0b4-225">prefix-5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="fd0b4-225">prefix-5yj4yjf5mbg72</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="fd0b4-226">contains</span><span class="sxs-lookup"><span data-stu-id="fd0b4-226">contains</span></span>
`contains(container, itemToFind)`

<span data-ttu-id="fd0b4-227">Verifica se una matrice contiene un valore, se un oggetto contiene una chiave o se una stringa contiene una sottostringa.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-227">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="fd0b4-228">Parametri</span><span class="sxs-lookup"><span data-stu-id="fd0b4-228">Parameters</span></span>

| <span data-ttu-id="fd0b4-229">Parametro</span><span class="sxs-lookup"><span data-stu-id="fd0b4-229">Parameter</span></span> | <span data-ttu-id="fd0b4-230">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="fd0b4-230">Required</span></span> | <span data-ttu-id="fd0b4-231">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-231">Type</span></span> | <span data-ttu-id="fd0b4-232">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fd0b4-232">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="fd0b4-233">Contenitore</span><span class="sxs-lookup"><span data-stu-id="fd0b4-233">container</span></span> |<span data-ttu-id="fd0b4-234">Sì</span><span class="sxs-lookup"><span data-stu-id="fd0b4-234">Yes</span></span> |<span data-ttu-id="fd0b4-235">matrice, oggetto o stringa</span><span class="sxs-lookup"><span data-stu-id="fd0b4-235">array, object, or string</span></span> |<span data-ttu-id="fd0b4-236">Valore che contiene il valore da trovare.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-236">The value that contains the value to find.</span></span> |
| <span data-ttu-id="fd0b4-237">itemToFind</span><span class="sxs-lookup"><span data-stu-id="fd0b4-237">itemToFind</span></span> |<span data-ttu-id="fd0b4-238">Sì</span><span class="sxs-lookup"><span data-stu-id="fd0b4-238">Yes</span></span> |<span data-ttu-id="fd0b4-239">stringa o numero intero</span><span class="sxs-lookup"><span data-stu-id="fd0b4-239">string or int</span></span> |<span data-ttu-id="fd0b4-240">Valore da trovare.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-240">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="fd0b4-241">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="fd0b4-241">Return value</span></span>

<span data-ttu-id="fd0b4-242">**True** se l'elemento viene individuato; in caso contrario, restituisce **False**.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-242">**True** if the item is found; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="fd0b4-243">Esempio</span><span class="sxs-lookup"><span data-stu-id="fd0b4-243">Example</span></span>

<span data-ttu-id="fd0b4-244">L'esempio seguente mostra come usare la funzione contains con tipi diversi:</span><span class="sxs-lookup"><span data-stu-id="fd0b4-244">The following example shows how to use contains with different types:</span></span>

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

<span data-ttu-id="fd0b4-245">L'output dell'esempio precedente con i valori predefiniti è il seguente:</span><span class="sxs-lookup"><span data-stu-id="fd0b4-245">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="fd0b4-246">Nome</span><span class="sxs-lookup"><span data-stu-id="fd0b4-246">Name</span></span> | <span data-ttu-id="fd0b4-247">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-247">Type</span></span> | <span data-ttu-id="fd0b4-248">Valore</span><span class="sxs-lookup"><span data-stu-id="fd0b4-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="fd0b4-249">stringTrue</span><span class="sxs-lookup"><span data-stu-id="fd0b4-249">stringTrue</span></span> | <span data-ttu-id="fd0b4-250">Booleano</span><span class="sxs-lookup"><span data-stu-id="fd0b4-250">Bool</span></span> | <span data-ttu-id="fd0b4-251">True </span><span class="sxs-lookup"><span data-stu-id="fd0b4-251">True</span></span> |
| <span data-ttu-id="fd0b4-252">stringFalse</span><span class="sxs-lookup"><span data-stu-id="fd0b4-252">stringFalse</span></span> | <span data-ttu-id="fd0b4-253">Booleano</span><span class="sxs-lookup"><span data-stu-id="fd0b4-253">Bool</span></span> | <span data-ttu-id="fd0b4-254">False</span><span class="sxs-lookup"><span data-stu-id="fd0b4-254">False</span></span> |
| <span data-ttu-id="fd0b4-255">objectTrue</span><span class="sxs-lookup"><span data-stu-id="fd0b4-255">objectTrue</span></span> | <span data-ttu-id="fd0b4-256">Booleano</span><span class="sxs-lookup"><span data-stu-id="fd0b4-256">Bool</span></span> | <span data-ttu-id="fd0b4-257">True </span><span class="sxs-lookup"><span data-stu-id="fd0b4-257">True</span></span> |
| <span data-ttu-id="fd0b4-258">objectFalse</span><span class="sxs-lookup"><span data-stu-id="fd0b4-258">objectFalse</span></span> | <span data-ttu-id="fd0b4-259">Booleano</span><span class="sxs-lookup"><span data-stu-id="fd0b4-259">Bool</span></span> | <span data-ttu-id="fd0b4-260">False</span><span class="sxs-lookup"><span data-stu-id="fd0b4-260">False</span></span> |
| <span data-ttu-id="fd0b4-261">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="fd0b4-261">arrayTrue</span></span> | <span data-ttu-id="fd0b4-262">Booleano</span><span class="sxs-lookup"><span data-stu-id="fd0b4-262">Bool</span></span> | <span data-ttu-id="fd0b4-263">True </span><span class="sxs-lookup"><span data-stu-id="fd0b4-263">True</span></span> |
| <span data-ttu-id="fd0b4-264">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="fd0b4-264">arrayFalse</span></span> | <span data-ttu-id="fd0b4-265">Booleano</span><span class="sxs-lookup"><span data-stu-id="fd0b4-265">Bool</span></span> | <span data-ttu-id="fd0b4-266">False</span><span class="sxs-lookup"><span data-stu-id="fd0b4-266">False</span></span> |

<a id="createarray" />

## <a name="createarray"></a><span data-ttu-id="fd0b4-267">createarray</span><span class="sxs-lookup"><span data-stu-id="fd0b4-267">createarray</span></span>
`createArray (arg1, arg2, arg3, ...)`

<span data-ttu-id="fd0b4-268">Crea una matrice dai parametri.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-268">Creates an array from the parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="fd0b4-269">Parametri</span><span class="sxs-lookup"><span data-stu-id="fd0b4-269">Parameters</span></span>

| <span data-ttu-id="fd0b4-270">Parametro</span><span class="sxs-lookup"><span data-stu-id="fd0b4-270">Parameter</span></span> | <span data-ttu-id="fd0b4-271">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="fd0b4-271">Required</span></span> | <span data-ttu-id="fd0b4-272">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-272">Type</span></span> | <span data-ttu-id="fd0b4-273">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fd0b4-273">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="fd0b4-274">arg1</span><span class="sxs-lookup"><span data-stu-id="fd0b4-274">arg1</span></span> |<span data-ttu-id="fd0b4-275">Sì</span><span class="sxs-lookup"><span data-stu-id="fd0b4-275">Yes</span></span> |<span data-ttu-id="fd0b4-276">Stringa, numero intero, matrice o oggetto</span><span class="sxs-lookup"><span data-stu-id="fd0b4-276">String, Integer, Array, or Object</span></span> |<span data-ttu-id="fd0b4-277">Primo valore della matrice.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-277">The first value in the array.</span></span> |
| <span data-ttu-id="fd0b4-278">argomenti aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="fd0b4-278">additional arguments</span></span> |<span data-ttu-id="fd0b4-279">No</span><span class="sxs-lookup"><span data-stu-id="fd0b4-279">No</span></span> |<span data-ttu-id="fd0b4-280">Stringa, numero intero, matrice o oggetto</span><span class="sxs-lookup"><span data-stu-id="fd0b4-280">String, Integer, Array, or Object</span></span> |<span data-ttu-id="fd0b4-281">Altri valori della matrice.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-281">Additional values in the array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="fd0b4-282">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="fd0b4-282">Return value</span></span>

<span data-ttu-id="fd0b4-283">Una matrice.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-283">An array.</span></span>

### <a name="example"></a><span data-ttu-id="fd0b4-284">Esempio</span><span class="sxs-lookup"><span data-stu-id="fd0b4-284">Example</span></span>

<span data-ttu-id="fd0b4-285">L'esempio seguente mostra come usare la funzione createArray con tipi diversi:</span><span class="sxs-lookup"><span data-stu-id="fd0b4-285">The following example shows how to use createArray with different types:</span></span>

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

<span data-ttu-id="fd0b4-286">L'output dell'esempio precedente con i valori predefiniti è il seguente:</span><span class="sxs-lookup"><span data-stu-id="fd0b4-286">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="fd0b4-287">Nome</span><span class="sxs-lookup"><span data-stu-id="fd0b4-287">Name</span></span> | <span data-ttu-id="fd0b4-288">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-288">Type</span></span> | <span data-ttu-id="fd0b4-289">Valore</span><span class="sxs-lookup"><span data-stu-id="fd0b4-289">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="fd0b4-290">stringArray</span><span class="sxs-lookup"><span data-stu-id="fd0b4-290">stringArray</span></span> | <span data-ttu-id="fd0b4-291">Array</span><span class="sxs-lookup"><span data-stu-id="fd0b4-291">Array</span></span> | <span data-ttu-id="fd0b4-292">["a", "b", "c"]</span><span class="sxs-lookup"><span data-stu-id="fd0b4-292">["a", "b", "c"]</span></span> |
| <span data-ttu-id="fd0b4-293">intArray</span><span class="sxs-lookup"><span data-stu-id="fd0b4-293">intArray</span></span> | <span data-ttu-id="fd0b4-294">Array</span><span class="sxs-lookup"><span data-stu-id="fd0b4-294">Array</span></span> | <span data-ttu-id="fd0b4-295">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="fd0b4-295">[1, 2, 3]</span></span> |
| <span data-ttu-id="fd0b4-296">objectArray</span><span class="sxs-lookup"><span data-stu-id="fd0b4-296">objectArray</span></span> | <span data-ttu-id="fd0b4-297">Array</span><span class="sxs-lookup"><span data-stu-id="fd0b4-297">Array</span></span> | <span data-ttu-id="fd0b4-298">[{"one": "a", "two": "b", "three": "c"}]</span><span class="sxs-lookup"><span data-stu-id="fd0b4-298">[{"one": "a", "two": "b", "three": "c"}]</span></span> |
| <span data-ttu-id="fd0b4-299">arrayArray</span><span class="sxs-lookup"><span data-stu-id="fd0b4-299">arrayArray</span></span> | <span data-ttu-id="fd0b4-300">Array</span><span class="sxs-lookup"><span data-stu-id="fd0b4-300">Array</span></span> | <span data-ttu-id="fd0b4-301">[["one", "two", "three"]]</span><span class="sxs-lookup"><span data-stu-id="fd0b4-301">[["one", "two", "three"]]</span></span> |

<a id="empty" />

## <a name="empty"></a><span data-ttu-id="fd0b4-302">empty</span><span class="sxs-lookup"><span data-stu-id="fd0b4-302">empty</span></span>

`empty(itemToTest)`

<span data-ttu-id="fd0b4-303">Determina se una matrice, un oggetto o una stringa sono vuoti.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-303">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="fd0b4-304">Parametri</span><span class="sxs-lookup"><span data-stu-id="fd0b4-304">Parameters</span></span>

| <span data-ttu-id="fd0b4-305">Parametro</span><span class="sxs-lookup"><span data-stu-id="fd0b4-305">Parameter</span></span> | <span data-ttu-id="fd0b4-306">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="fd0b4-306">Required</span></span> | <span data-ttu-id="fd0b4-307">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-307">Type</span></span> | <span data-ttu-id="fd0b4-308">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fd0b4-308">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="fd0b4-309">itemToTest</span><span class="sxs-lookup"><span data-stu-id="fd0b4-309">itemToTest</span></span> |<span data-ttu-id="fd0b4-310">Sì</span><span class="sxs-lookup"><span data-stu-id="fd0b4-310">Yes</span></span> |<span data-ttu-id="fd0b4-311">matrice, oggetto o stringa</span><span class="sxs-lookup"><span data-stu-id="fd0b4-311">array, object, or string</span></span> |<span data-ttu-id="fd0b4-312">Valore da controllare per verificare se è vuoto.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-312">The value to check if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="fd0b4-313">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="fd0b4-313">Return value</span></span>

<span data-ttu-id="fd0b4-314">**True** se il valore è vuoto; in caso contrario, restituisce **False**.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-314">Returns **True** if the value is empty; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="fd0b4-315">Esempio</span><span class="sxs-lookup"><span data-stu-id="fd0b4-315">Example</span></span>

<span data-ttu-id="fd0b4-316">L'esempio seguente controlla se una matrice, un oggetto e una stringa sono vuoti.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-316">The following example checks whether an array, object, and string are empty.</span></span>

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

<span data-ttu-id="fd0b4-317">L'output dell'esempio precedente con i valori predefiniti è il seguente:</span><span class="sxs-lookup"><span data-stu-id="fd0b4-317">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="fd0b4-318">Nome</span><span class="sxs-lookup"><span data-stu-id="fd0b4-318">Name</span></span> | <span data-ttu-id="fd0b4-319">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-319">Type</span></span> | <span data-ttu-id="fd0b4-320">Valore</span><span class="sxs-lookup"><span data-stu-id="fd0b4-320">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="fd0b4-321">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="fd0b4-321">arrayEmpty</span></span> | <span data-ttu-id="fd0b4-322">Booleano</span><span class="sxs-lookup"><span data-stu-id="fd0b4-322">Bool</span></span> | <span data-ttu-id="fd0b4-323">True </span><span class="sxs-lookup"><span data-stu-id="fd0b4-323">True</span></span> |
| <span data-ttu-id="fd0b4-324">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="fd0b4-324">objectEmpty</span></span> | <span data-ttu-id="fd0b4-325">Booleano</span><span class="sxs-lookup"><span data-stu-id="fd0b4-325">Bool</span></span> | <span data-ttu-id="fd0b4-326">True </span><span class="sxs-lookup"><span data-stu-id="fd0b4-326">True</span></span> |
| <span data-ttu-id="fd0b4-327">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="fd0b4-327">stringEmpty</span></span> | <span data-ttu-id="fd0b4-328">Booleano</span><span class="sxs-lookup"><span data-stu-id="fd0b4-328">Bool</span></span> | <span data-ttu-id="fd0b4-329">True </span><span class="sxs-lookup"><span data-stu-id="fd0b4-329">True</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="fd0b4-330">first</span><span class="sxs-lookup"><span data-stu-id="fd0b4-330">first</span></span>
`first(arg1)`

<span data-ttu-id="fd0b4-331">Restituisce il primo elemento della matrice o il primo carattere della stringa.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-331">Returns the first element of the array, or first character of the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="fd0b4-332">Parametri</span><span class="sxs-lookup"><span data-stu-id="fd0b4-332">Parameters</span></span>

| <span data-ttu-id="fd0b4-333">Parametro</span><span class="sxs-lookup"><span data-stu-id="fd0b4-333">Parameter</span></span> | <span data-ttu-id="fd0b4-334">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="fd0b4-334">Required</span></span> | <span data-ttu-id="fd0b4-335">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-335">Type</span></span> | <span data-ttu-id="fd0b4-336">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fd0b4-336">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="fd0b4-337">arg1</span><span class="sxs-lookup"><span data-stu-id="fd0b4-337">arg1</span></span> |<span data-ttu-id="fd0b4-338">Sì</span><span class="sxs-lookup"><span data-stu-id="fd0b4-338">Yes</span></span> |<span data-ttu-id="fd0b4-339">stringa o matrice</span><span class="sxs-lookup"><span data-stu-id="fd0b4-339">array or string</span></span> |<span data-ttu-id="fd0b4-340">Valore per recuperare il primo elemento o carattere.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-340">The value to retrieve the first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="fd0b4-341">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="fd0b4-341">Return value</span></span>

<span data-ttu-id="fd0b4-342">Il tipo (string, int, array o object) del primo elemento di una matrice o il primo carattere di una stringa.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-342">The type (string, int, array, or object) of the first element in an array, or the first character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="fd0b4-343">Esempio</span><span class="sxs-lookup"><span data-stu-id="fd0b4-343">Example</span></span>

<span data-ttu-id="fd0b4-344">L'esempio seguente mostra come usare la prima funzione con una matrice e una stringa.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-344">The following example shows how to use the first function with an array and string.</span></span>

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

<span data-ttu-id="fd0b4-345">L'output dell'esempio precedente con i valori predefiniti è il seguente:</span><span class="sxs-lookup"><span data-stu-id="fd0b4-345">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="fd0b4-346">Nome</span><span class="sxs-lookup"><span data-stu-id="fd0b4-346">Name</span></span> | <span data-ttu-id="fd0b4-347">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-347">Type</span></span> | <span data-ttu-id="fd0b4-348">Valore</span><span class="sxs-lookup"><span data-stu-id="fd0b4-348">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="fd0b4-349">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="fd0b4-349">arrayOutput</span></span> | <span data-ttu-id="fd0b4-350">String</span><span class="sxs-lookup"><span data-stu-id="fd0b4-350">String</span></span> | <span data-ttu-id="fd0b4-351">one</span><span class="sxs-lookup"><span data-stu-id="fd0b4-351">one</span></span> |
| <span data-ttu-id="fd0b4-352">stringOutput</span><span class="sxs-lookup"><span data-stu-id="fd0b4-352">stringOutput</span></span> | <span data-ttu-id="fd0b4-353">String</span><span class="sxs-lookup"><span data-stu-id="fd0b4-353">String</span></span> | <span data-ttu-id="fd0b4-354">O</span><span class="sxs-lookup"><span data-stu-id="fd0b4-354">O</span></span> |

<a id="intersection" />

## <a name="intersection"></a><span data-ttu-id="fd0b4-355">intersezione</span><span class="sxs-lookup"><span data-stu-id="fd0b4-355">intersection</span></span>
`intersection(arg1, arg2, arg3, ...)`

<span data-ttu-id="fd0b4-356">Restituisce una matrice o un oggetto singoli con gli elementi comuni dei parametri.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-356">Returns a single array or object with the common elements from the parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="fd0b4-357">Parametri</span><span class="sxs-lookup"><span data-stu-id="fd0b4-357">Parameters</span></span>

| <span data-ttu-id="fd0b4-358">Parametro</span><span class="sxs-lookup"><span data-stu-id="fd0b4-358">Parameter</span></span> | <span data-ttu-id="fd0b4-359">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="fd0b4-359">Required</span></span> | <span data-ttu-id="fd0b4-360">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-360">Type</span></span> | <span data-ttu-id="fd0b4-361">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fd0b4-361">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="fd0b4-362">arg1</span><span class="sxs-lookup"><span data-stu-id="fd0b4-362">arg1</span></span> |<span data-ttu-id="fd0b4-363">Sì</span><span class="sxs-lookup"><span data-stu-id="fd0b4-363">Yes</span></span> |<span data-ttu-id="fd0b4-364">matrice o oggetto</span><span class="sxs-lookup"><span data-stu-id="fd0b4-364">array or object</span></span> |<span data-ttu-id="fd0b4-365">Primo valore da usare per cercare elementi comuni.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-365">The first value to use for finding common elements.</span></span> |
| <span data-ttu-id="fd0b4-366">arg2</span><span class="sxs-lookup"><span data-stu-id="fd0b4-366">arg2</span></span> |<span data-ttu-id="fd0b4-367">Sì</span><span class="sxs-lookup"><span data-stu-id="fd0b4-367">Yes</span></span> |<span data-ttu-id="fd0b4-368">matrice o oggetto</span><span class="sxs-lookup"><span data-stu-id="fd0b4-368">array or object</span></span> |<span data-ttu-id="fd0b4-369">Secondo valore da usare per cercare elementi comuni.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-369">The second value to use for finding common elements.</span></span> |
| <span data-ttu-id="fd0b4-370">argomenti aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="fd0b4-370">additional arguments</span></span> |<span data-ttu-id="fd0b4-371">No</span><span class="sxs-lookup"><span data-stu-id="fd0b4-371">No</span></span> |<span data-ttu-id="fd0b4-372">matrice o oggetto</span><span class="sxs-lookup"><span data-stu-id="fd0b4-372">array or object</span></span> |<span data-ttu-id="fd0b4-373">Valori aggiuntivi da usare per cercare elementi comuni.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-373">Additional values to use for finding common elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="fd0b4-374">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="fd0b4-374">Return value</span></span>

<span data-ttu-id="fd0b4-375">Una matrice o un oggetto con elementi comuni.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-375">An array or object with the common elements.</span></span>

### <a name="example"></a><span data-ttu-id="fd0b4-376">Esempio</span><span class="sxs-lookup"><span data-stu-id="fd0b4-376">Example</span></span>

<span data-ttu-id="fd0b4-377">L'esempio seguente mostra come usare l'intersezione con matrici e oggetti:</span><span class="sxs-lookup"><span data-stu-id="fd0b4-377">The following example shows how to use intersection with arrays and objects:</span></span>

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

<span data-ttu-id="fd0b4-378">L'output dell'esempio precedente con i valori predefiniti è il seguente:</span><span class="sxs-lookup"><span data-stu-id="fd0b4-378">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="fd0b4-379">Nome</span><span class="sxs-lookup"><span data-stu-id="fd0b4-379">Name</span></span> | <span data-ttu-id="fd0b4-380">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-380">Type</span></span> | <span data-ttu-id="fd0b4-381">Valore</span><span class="sxs-lookup"><span data-stu-id="fd0b4-381">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="fd0b4-382">objectOutput</span><span class="sxs-lookup"><span data-stu-id="fd0b4-382">objectOutput</span></span> | <span data-ttu-id="fd0b4-383">Oggetto</span><span class="sxs-lookup"><span data-stu-id="fd0b4-383">Object</span></span> | <span data-ttu-id="fd0b4-384">{"one": "a", "three": "c"}</span><span class="sxs-lookup"><span data-stu-id="fd0b4-384">{"one": "a", "three": "c"}</span></span> |
| <span data-ttu-id="fd0b4-385">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="fd0b4-385">arrayOutput</span></span> | <span data-ttu-id="fd0b4-386">Array</span><span class="sxs-lookup"><span data-stu-id="fd0b4-386">Array</span></span> | <span data-ttu-id="fd0b4-387">["two", "three"]</span><span class="sxs-lookup"><span data-stu-id="fd0b4-387">["two", "three"]</span></span> |


## <a name="json"></a><span data-ttu-id="fd0b4-388">json</span><span class="sxs-lookup"><span data-stu-id="fd0b4-388">json</span></span>
`json(arg1)`

<span data-ttu-id="fd0b4-389">Restituisce un oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-389">Returns a JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="fd0b4-390">parameters</span><span class="sxs-lookup"><span data-stu-id="fd0b4-390">Parameters</span></span>

| <span data-ttu-id="fd0b4-391">Parametro</span><span class="sxs-lookup"><span data-stu-id="fd0b4-391">Parameter</span></span> | <span data-ttu-id="fd0b4-392">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="fd0b4-392">Required</span></span> | <span data-ttu-id="fd0b4-393">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-393">Type</span></span> | <span data-ttu-id="fd0b4-394">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fd0b4-394">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="fd0b4-395">arg1</span><span class="sxs-lookup"><span data-stu-id="fd0b4-395">arg1</span></span> |<span data-ttu-id="fd0b4-396">Sì</span><span class="sxs-lookup"><span data-stu-id="fd0b4-396">Yes</span></span> |<span data-ttu-id="fd0b4-397">string</span><span class="sxs-lookup"><span data-stu-id="fd0b4-397">string</span></span> |<span data-ttu-id="fd0b4-398">Valore da convertire in JSON.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-398">The value to convert to JSON.</span></span> |


### <a name="return-value"></a><span data-ttu-id="fd0b4-399">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="fd0b4-399">Return value</span></span>

<span data-ttu-id="fd0b4-400">Oggetto JSON dalla stringa specificata o un oggetto vuoto quando viene specificato **null**.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-400">The JSON object from the specified string, or an empty object when **null** is specified.</span></span>

### <a name="example"></a><span data-ttu-id="fd0b4-401">Esempio</span><span class="sxs-lookup"><span data-stu-id="fd0b4-401">Example</span></span>

<span data-ttu-id="fd0b4-402">L'esempio seguente mostra come usare l'intersezione con matrici e oggetti:</span><span class="sxs-lookup"><span data-stu-id="fd0b4-402">The following example shows how to use intersection with arrays and objects:</span></span>

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

<span data-ttu-id="fd0b4-403">L'output dell'esempio precedente con i valori predefiniti è il seguente:</span><span class="sxs-lookup"><span data-stu-id="fd0b4-403">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="fd0b4-404">Nome</span><span class="sxs-lookup"><span data-stu-id="fd0b4-404">Name</span></span> | <span data-ttu-id="fd0b4-405">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-405">Type</span></span> | <span data-ttu-id="fd0b4-406">Valore</span><span class="sxs-lookup"><span data-stu-id="fd0b4-406">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="fd0b4-407">jsonOutput</span><span class="sxs-lookup"><span data-stu-id="fd0b4-407">jsonOutput</span></span> | <span data-ttu-id="fd0b4-408">Oggetto</span><span class="sxs-lookup"><span data-stu-id="fd0b4-408">Object</span></span> | <span data-ttu-id="fd0b4-409">{"a": "b"}</span><span class="sxs-lookup"><span data-stu-id="fd0b4-409">{"a": "b"}</span></span> |
| <span data-ttu-id="fd0b4-410">nullOutput</span><span class="sxs-lookup"><span data-stu-id="fd0b4-410">nullOutput</span></span> | <span data-ttu-id="fd0b4-411">Boolean</span><span class="sxs-lookup"><span data-stu-id="fd0b4-411">Boolean</span></span> | <span data-ttu-id="fd0b4-412">True </span><span class="sxs-lookup"><span data-stu-id="fd0b4-412">True</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="fd0b4-413">last</span><span class="sxs-lookup"><span data-stu-id="fd0b4-413">last</span></span>
`last (arg1)`

<span data-ttu-id="fd0b4-414">Restituisce l'ultimo elemento della matrice o l'ultimo carattere della stringa.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-414">Returns the last element of the array, or last character of the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="fd0b4-415">Parametri</span><span class="sxs-lookup"><span data-stu-id="fd0b4-415">Parameters</span></span>

| <span data-ttu-id="fd0b4-416">Parametro</span><span class="sxs-lookup"><span data-stu-id="fd0b4-416">Parameter</span></span> | <span data-ttu-id="fd0b4-417">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="fd0b4-417">Required</span></span> | <span data-ttu-id="fd0b4-418">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-418">Type</span></span> | <span data-ttu-id="fd0b4-419">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fd0b4-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="fd0b4-420">arg1</span><span class="sxs-lookup"><span data-stu-id="fd0b4-420">arg1</span></span> |<span data-ttu-id="fd0b4-421">Sì</span><span class="sxs-lookup"><span data-stu-id="fd0b4-421">Yes</span></span> |<span data-ttu-id="fd0b4-422">stringa o matrice</span><span class="sxs-lookup"><span data-stu-id="fd0b4-422">array or string</span></span> |<span data-ttu-id="fd0b4-423">Valore per recuperare l'ultimo elemento o carattere.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-423">The value to retrieve the last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="fd0b4-424">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="fd0b4-424">Return value</span></span>

<span data-ttu-id="fd0b4-425">Il tipo (string, int, array o object) dell'ultimo elemento di una matrice o l'ultimo carattere di una stringa.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-425">The type (string, int, array, or object) of the last element in an array, or the last character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="fd0b4-426">Esempio</span><span class="sxs-lookup"><span data-stu-id="fd0b4-426">Example</span></span>

<span data-ttu-id="fd0b4-427">L'esempio seguente mostra come usare l'ultima funzione con una matrice e una stringa.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-427">The following example shows how to use the last function with an array and string.</span></span>

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

<span data-ttu-id="fd0b4-428">L'output dell'esempio precedente con i valori predefiniti è il seguente:</span><span class="sxs-lookup"><span data-stu-id="fd0b4-428">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="fd0b4-429">Nome</span><span class="sxs-lookup"><span data-stu-id="fd0b4-429">Name</span></span> | <span data-ttu-id="fd0b4-430">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-430">Type</span></span> | <span data-ttu-id="fd0b4-431">Valore</span><span class="sxs-lookup"><span data-stu-id="fd0b4-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="fd0b4-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="fd0b4-432">arrayOutput</span></span> | <span data-ttu-id="fd0b4-433">String</span><span class="sxs-lookup"><span data-stu-id="fd0b4-433">String</span></span> | <span data-ttu-id="fd0b4-434">three</span><span class="sxs-lookup"><span data-stu-id="fd0b4-434">three</span></span> |
| <span data-ttu-id="fd0b4-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="fd0b4-435">stringOutput</span></span> | <span data-ttu-id="fd0b4-436">String</span><span class="sxs-lookup"><span data-stu-id="fd0b4-436">String</span></span> | <span data-ttu-id="fd0b4-437">e</span><span class="sxs-lookup"><span data-stu-id="fd0b4-437">e</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="fd0b4-438">length</span><span class="sxs-lookup"><span data-stu-id="fd0b4-438">length</span></span>
`length(arg1)`

<span data-ttu-id="fd0b4-439">Restituisce il numero di elementi in una matrice o di caratteri in una stringa.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-439">Returns the number of elements in an array, or characters in a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="fd0b4-440">Parametri</span><span class="sxs-lookup"><span data-stu-id="fd0b4-440">Parameters</span></span>

| <span data-ttu-id="fd0b4-441">Parametro</span><span class="sxs-lookup"><span data-stu-id="fd0b4-441">Parameter</span></span> | <span data-ttu-id="fd0b4-442">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="fd0b4-442">Required</span></span> | <span data-ttu-id="fd0b4-443">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-443">Type</span></span> | <span data-ttu-id="fd0b4-444">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fd0b4-444">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="fd0b4-445">arg1</span><span class="sxs-lookup"><span data-stu-id="fd0b4-445">arg1</span></span> |<span data-ttu-id="fd0b4-446">Sì</span><span class="sxs-lookup"><span data-stu-id="fd0b4-446">Yes</span></span> |<span data-ttu-id="fd0b4-447">stringa o matrice</span><span class="sxs-lookup"><span data-stu-id="fd0b4-447">array or string</span></span> |<span data-ttu-id="fd0b4-448">Matrice da usare per ottenere il numero di elementi oppure stringa da usare per ottenere il numero di caratteri.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-448">The array to use for getting the number of elements, or the string to use for getting the number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="fd0b4-449">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="fd0b4-449">Return value</span></span>

<span data-ttu-id="fd0b4-450">Numero intero</span><span class="sxs-lookup"><span data-stu-id="fd0b4-450">An int.</span></span> 

### <a name="example"></a><span data-ttu-id="fd0b4-451">Esempio</span><span class="sxs-lookup"><span data-stu-id="fd0b4-451">Example</span></span>

<span data-ttu-id="fd0b4-452">L'esempio seguente mostra come usare la funzione length con una matrice e una stringa:</span><span class="sxs-lookup"><span data-stu-id="fd0b4-452">The following example shows how to use length with an array and string:</span></span>

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

<span data-ttu-id="fd0b4-453">L'output dell'esempio precedente con i valori predefiniti è il seguente:</span><span class="sxs-lookup"><span data-stu-id="fd0b4-453">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="fd0b4-454">Nome</span><span class="sxs-lookup"><span data-stu-id="fd0b4-454">Name</span></span> | <span data-ttu-id="fd0b4-455">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-455">Type</span></span> | <span data-ttu-id="fd0b4-456">Valore</span><span class="sxs-lookup"><span data-stu-id="fd0b4-456">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="fd0b4-457">arrayLength</span><span class="sxs-lookup"><span data-stu-id="fd0b4-457">arrayLength</span></span> | <span data-ttu-id="fd0b4-458">int</span><span class="sxs-lookup"><span data-stu-id="fd0b4-458">Int</span></span> | <span data-ttu-id="fd0b4-459">3</span><span class="sxs-lookup"><span data-stu-id="fd0b4-459">3</span></span> |
| <span data-ttu-id="fd0b4-460">stringLength</span><span class="sxs-lookup"><span data-stu-id="fd0b4-460">stringLength</span></span> | <span data-ttu-id="fd0b4-461">int</span><span class="sxs-lookup"><span data-stu-id="fd0b4-461">Int</span></span> | <span data-ttu-id="fd0b4-462">13</span><span class="sxs-lookup"><span data-stu-id="fd0b4-462">13</span></span> |

<span data-ttu-id="fd0b4-463">È possibile usare questa funzione con una matrice per specificare il numero di iterazioni durante la creazione di risorse.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-463">You can use this function with an array to specify the number of iterations when creating resources.</span></span> <span data-ttu-id="fd0b4-464">Nell'esempio seguente, il parametro **siteNames** fa riferimento a una matrice di nomi da usare durante la creazione di siti Web.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-464">In the following example, the parameter **siteNames** would refer to an array of names to use when creating the web sites.</span></span>

```json
"copy": {
    "name": "websitescopy",
    "count": "[length(parameters('siteNames'))]"
}
```

<span data-ttu-id="fd0b4-465">Per altre informazioni sull'uso di questa funzione con una matrice, vedere [Creare più istanze di risorse in Gestione risorse di Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="fd0b4-465">For more information about using this function with an array, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<a id="min" />

## <a name="min"></a><span data-ttu-id="fd0b4-466">Min</span><span class="sxs-lookup"><span data-stu-id="fd0b4-466">min</span></span>
`min(arg1)`

<span data-ttu-id="fd0b4-467">Restituisce il valore minimo di una matrice di numeri interi o di un elenco di numeri interi delimitato da virgole.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-467">Returns the minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="fd0b4-468">Parametri</span><span class="sxs-lookup"><span data-stu-id="fd0b4-468">Parameters</span></span>

| <span data-ttu-id="fd0b4-469">Parametro</span><span class="sxs-lookup"><span data-stu-id="fd0b4-469">Parameter</span></span> | <span data-ttu-id="fd0b4-470">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="fd0b4-470">Required</span></span> | <span data-ttu-id="fd0b4-471">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-471">Type</span></span> | <span data-ttu-id="fd0b4-472">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fd0b4-472">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="fd0b4-473">arg1</span><span class="sxs-lookup"><span data-stu-id="fd0b4-473">arg1</span></span> |<span data-ttu-id="fd0b4-474">Sì</span><span class="sxs-lookup"><span data-stu-id="fd0b4-474">Yes</span></span> |<span data-ttu-id="fd0b4-475">matrice di numeri interi o elenco di numeri interi delimitato da virgole</span><span class="sxs-lookup"><span data-stu-id="fd0b4-475">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="fd0b4-476">La raccolta per ottenere il valore minimo.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-476">The collection to get the minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="fd0b4-477">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="fd0b4-477">Return value</span></span>

<span data-ttu-id="fd0b4-478">Numero intero che rappresenta il valore minimo.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-478">An int representing the minimum value.</span></span>

### <a name="example"></a><span data-ttu-id="fd0b4-479">Esempio</span><span class="sxs-lookup"><span data-stu-id="fd0b4-479">Example</span></span>

<span data-ttu-id="fd0b4-480">L'esempio seguente mostra come usare la funzione min con una matrice e un elenco di numeri interi:</span><span class="sxs-lookup"><span data-stu-id="fd0b4-480">The following example shows how to use min with an array and a list of integers:</span></span>

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

<span data-ttu-id="fd0b4-481">L'output dell'esempio precedente con i valori predefiniti è il seguente:</span><span class="sxs-lookup"><span data-stu-id="fd0b4-481">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="fd0b4-482">Nome</span><span class="sxs-lookup"><span data-stu-id="fd0b4-482">Name</span></span> | <span data-ttu-id="fd0b4-483">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-483">Type</span></span> | <span data-ttu-id="fd0b4-484">Valore</span><span class="sxs-lookup"><span data-stu-id="fd0b4-484">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="fd0b4-485">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="fd0b4-485">arrayOutput</span></span> | <span data-ttu-id="fd0b4-486">int</span><span class="sxs-lookup"><span data-stu-id="fd0b4-486">Int</span></span> | <span data-ttu-id="fd0b4-487">0</span><span class="sxs-lookup"><span data-stu-id="fd0b4-487">0</span></span> |
| <span data-ttu-id="fd0b4-488">intOutput</span><span class="sxs-lookup"><span data-stu-id="fd0b4-488">intOutput</span></span> | <span data-ttu-id="fd0b4-489">int</span><span class="sxs-lookup"><span data-stu-id="fd0b4-489">Int</span></span> | <span data-ttu-id="fd0b4-490">0</span><span class="sxs-lookup"><span data-stu-id="fd0b4-490">0</span></span> |

<a id="max" />

## <a name="max"></a><span data-ttu-id="fd0b4-491">max</span><span class="sxs-lookup"><span data-stu-id="fd0b4-491">max</span></span>
`max(arg1)`

<span data-ttu-id="fd0b4-492">Restituisce il valore massimo da una matrice di numeri interi o da un elenco di numeri interi delimitato da virgole.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-492">Returns the maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="fd0b4-493">Parametri</span><span class="sxs-lookup"><span data-stu-id="fd0b4-493">Parameters</span></span>

| <span data-ttu-id="fd0b4-494">Parametro</span><span class="sxs-lookup"><span data-stu-id="fd0b4-494">Parameter</span></span> | <span data-ttu-id="fd0b4-495">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="fd0b4-495">Required</span></span> | <span data-ttu-id="fd0b4-496">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-496">Type</span></span> | <span data-ttu-id="fd0b4-497">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fd0b4-497">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="fd0b4-498">arg1</span><span class="sxs-lookup"><span data-stu-id="fd0b4-498">arg1</span></span> |<span data-ttu-id="fd0b4-499">Sì</span><span class="sxs-lookup"><span data-stu-id="fd0b4-499">Yes</span></span> |<span data-ttu-id="fd0b4-500">matrice di numeri interi o elenco di numeri interi delimitato da virgole</span><span class="sxs-lookup"><span data-stu-id="fd0b4-500">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="fd0b4-501">La raccolta per ottenere il valore massimo.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-501">The collection to get the maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="fd0b4-502">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="fd0b4-502">Return value</span></span>

<span data-ttu-id="fd0b4-503">Numero intero che rappresenta il valore massimo.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-503">An int representing the maximum value.</span></span>

### <a name="example"></a><span data-ttu-id="fd0b4-504">Esempio</span><span class="sxs-lookup"><span data-stu-id="fd0b4-504">Example</span></span>

<span data-ttu-id="fd0b4-505">L'esempio seguente mostra come usare la funzione max con una matrice e un elenco di numeri interi:</span><span class="sxs-lookup"><span data-stu-id="fd0b4-505">The following example shows how to use max with an array and a list of integers:</span></span>

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

<span data-ttu-id="fd0b4-506">L'output dell'esempio precedente con i valori predefiniti è il seguente:</span><span class="sxs-lookup"><span data-stu-id="fd0b4-506">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="fd0b4-507">Nome</span><span class="sxs-lookup"><span data-stu-id="fd0b4-507">Name</span></span> | <span data-ttu-id="fd0b4-508">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-508">Type</span></span> | <span data-ttu-id="fd0b4-509">Valore</span><span class="sxs-lookup"><span data-stu-id="fd0b4-509">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="fd0b4-510">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="fd0b4-510">arrayOutput</span></span> | <span data-ttu-id="fd0b4-511">int</span><span class="sxs-lookup"><span data-stu-id="fd0b4-511">Int</span></span> | <span data-ttu-id="fd0b4-512">5</span><span class="sxs-lookup"><span data-stu-id="fd0b4-512">5</span></span> |
| <span data-ttu-id="fd0b4-513">intOutput</span><span class="sxs-lookup"><span data-stu-id="fd0b4-513">intOutput</span></span> | <span data-ttu-id="fd0b4-514">int</span><span class="sxs-lookup"><span data-stu-id="fd0b4-514">Int</span></span> | <span data-ttu-id="fd0b4-515">5</span><span class="sxs-lookup"><span data-stu-id="fd0b4-515">5</span></span> |

<a id="range" />

## <a name="range"></a><span data-ttu-id="fd0b4-516">range</span><span class="sxs-lookup"><span data-stu-id="fd0b4-516">range</span></span>
`range(startingInteger, numberOfElements)`

<span data-ttu-id="fd0b4-517">Crea una matrice di numeri interi da un numero intero iniziale, contenente un dato numero di elementi.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-517">Creates an array of integers from a starting integer and containing a number of items.</span></span>

### <a name="parameters"></a><span data-ttu-id="fd0b4-518">Parametri</span><span class="sxs-lookup"><span data-stu-id="fd0b4-518">Parameters</span></span>

| <span data-ttu-id="fd0b4-519">Parametro</span><span class="sxs-lookup"><span data-stu-id="fd0b4-519">Parameter</span></span> | <span data-ttu-id="fd0b4-520">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="fd0b4-520">Required</span></span> | <span data-ttu-id="fd0b4-521">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-521">Type</span></span> | <span data-ttu-id="fd0b4-522">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fd0b4-522">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="fd0b4-523">startingInteger</span><span class="sxs-lookup"><span data-stu-id="fd0b4-523">startingInteger</span></span> |<span data-ttu-id="fd0b4-524">Sì</span><span class="sxs-lookup"><span data-stu-id="fd0b4-524">Yes</span></span> |<span data-ttu-id="fd0b4-525">int</span><span class="sxs-lookup"><span data-stu-id="fd0b4-525">int</span></span> |<span data-ttu-id="fd0b4-526">Primo numero intero nella matrice.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-526">The first integer in the array.</span></span> |
| <span data-ttu-id="fd0b4-527">numberofElements</span><span class="sxs-lookup"><span data-stu-id="fd0b4-527">numberofElements</span></span> |<span data-ttu-id="fd0b4-528">Sì</span><span class="sxs-lookup"><span data-stu-id="fd0b4-528">Yes</span></span> |<span data-ttu-id="fd0b4-529">int</span><span class="sxs-lookup"><span data-stu-id="fd0b4-529">int</span></span> |<span data-ttu-id="fd0b4-530">Numero di valori interi della matrice.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-530">The number of integers in the array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="fd0b4-531">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="fd0b4-531">Return value</span></span>

<span data-ttu-id="fd0b4-532">Matrice di numeri interi.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-532">An array of integers.</span></span>

### <a name="example"></a><span data-ttu-id="fd0b4-533">Esempio</span><span class="sxs-lookup"><span data-stu-id="fd0b4-533">Example</span></span>

<span data-ttu-id="fd0b4-534">L'esempio seguente mostra come usare la funzione range:</span><span class="sxs-lookup"><span data-stu-id="fd0b4-534">The following example shows how to use the range function:</span></span>

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

<span data-ttu-id="fd0b4-535">L'output dell'esempio precedente con i valori predefiniti è il seguente:</span><span class="sxs-lookup"><span data-stu-id="fd0b4-535">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="fd0b4-536">Nome</span><span class="sxs-lookup"><span data-stu-id="fd0b4-536">Name</span></span> | <span data-ttu-id="fd0b4-537">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-537">Type</span></span> | <span data-ttu-id="fd0b4-538">Valore</span><span class="sxs-lookup"><span data-stu-id="fd0b4-538">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="fd0b4-539">rangeOutput</span><span class="sxs-lookup"><span data-stu-id="fd0b4-539">rangeOutput</span></span> | <span data-ttu-id="fd0b4-540">Array</span><span class="sxs-lookup"><span data-stu-id="fd0b4-540">Array</span></span> | <span data-ttu-id="fd0b4-541">[5, 6, 7]</span><span class="sxs-lookup"><span data-stu-id="fd0b4-541">[5, 6, 7]</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="fd0b4-542">skip</span><span class="sxs-lookup"><span data-stu-id="fd0b4-542">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="fd0b4-543">Restituisce una matrice con tutti gli elementi dopo il numero specificato nella matrice stessa o una stringa con tutti i caratteri dopo il numero specificato nella stringa stessa.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-543">Returns an array with all the elements after the specified number in the array, or returns a string with all the characters after the specified number in the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="fd0b4-544">Parametri</span><span class="sxs-lookup"><span data-stu-id="fd0b4-544">Parameters</span></span>

| <span data-ttu-id="fd0b4-545">Parametro</span><span class="sxs-lookup"><span data-stu-id="fd0b4-545">Parameter</span></span> | <span data-ttu-id="fd0b4-546">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="fd0b4-546">Required</span></span> | <span data-ttu-id="fd0b4-547">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-547">Type</span></span> | <span data-ttu-id="fd0b4-548">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fd0b4-548">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="fd0b4-549">originalValue</span><span class="sxs-lookup"><span data-stu-id="fd0b4-549">originalValue</span></span> |<span data-ttu-id="fd0b4-550">Sì</span><span class="sxs-lookup"><span data-stu-id="fd0b4-550">Yes</span></span> |<span data-ttu-id="fd0b4-551">stringa o matrice</span><span class="sxs-lookup"><span data-stu-id="fd0b4-551">array or string</span></span> |<span data-ttu-id="fd0b4-552">Stringa o matrice da usare per i valori da ignorare.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-552">The array or string to use for skipping.</span></span> |
| <span data-ttu-id="fd0b4-553">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="fd0b4-553">numberToSkip</span></span> |<span data-ttu-id="fd0b4-554">Sì</span><span class="sxs-lookup"><span data-stu-id="fd0b4-554">Yes</span></span> |<span data-ttu-id="fd0b4-555">int</span><span class="sxs-lookup"><span data-stu-id="fd0b4-555">int</span></span> |<span data-ttu-id="fd0b4-556">Numero di elementi o caratteri da ignorare.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-556">The number of elements or characters to skip.</span></span> <span data-ttu-id="fd0b4-557">Se il valore è minore o uguale a 0, vengono restituiti tutti gli elementi o i caratteri nel valore.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-557">If this value is 0 or less, all the elements or characters in the value are returned.</span></span> <span data-ttu-id="fd0b4-558">Se il valore è maggiore della lunghezza della stringa o della matrice, viene restituita una stringa o una matrice vuota.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-558">If it is larger than the length of the array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="fd0b4-559">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="fd0b4-559">Return value</span></span>

<span data-ttu-id="fd0b4-560">Stringa o matrice.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-560">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="fd0b4-561">Esempio</span><span class="sxs-lookup"><span data-stu-id="fd0b4-561">Example</span></span>

<span data-ttu-id="fd0b4-562">L'esempio seguente ignora il numero di elementi specificato nella matrice e il numero di caratteri specificato in una stringa.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-562">The following example skips the specified number of elements in the array, and the specified number of characters in a string.</span></span>

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

<span data-ttu-id="fd0b4-563">L'output dell'esempio precedente con i valori predefiniti è il seguente:</span><span class="sxs-lookup"><span data-stu-id="fd0b4-563">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="fd0b4-564">Nome</span><span class="sxs-lookup"><span data-stu-id="fd0b4-564">Name</span></span> | <span data-ttu-id="fd0b4-565">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-565">Type</span></span> | <span data-ttu-id="fd0b4-566">Valore</span><span class="sxs-lookup"><span data-stu-id="fd0b4-566">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="fd0b4-567">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="fd0b4-567">arrayOutput</span></span> | <span data-ttu-id="fd0b4-568">Array</span><span class="sxs-lookup"><span data-stu-id="fd0b4-568">Array</span></span> | <span data-ttu-id="fd0b4-569">["three"]</span><span class="sxs-lookup"><span data-stu-id="fd0b4-569">["three"]</span></span> |
| <span data-ttu-id="fd0b4-570">stringOutput</span><span class="sxs-lookup"><span data-stu-id="fd0b4-570">stringOutput</span></span> | <span data-ttu-id="fd0b4-571">String</span><span class="sxs-lookup"><span data-stu-id="fd0b4-571">String</span></span> | <span data-ttu-id="fd0b4-572">two three</span><span class="sxs-lookup"><span data-stu-id="fd0b4-572">two three</span></span> |

<a id="take" />

## <a name="take"></a><span data-ttu-id="fd0b4-573">take</span><span class="sxs-lookup"><span data-stu-id="fd0b4-573">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="fd0b4-574">Restituisce una matrice con il numero specificato di elementi dall'inizio della matrice, o una stringa con il numero specificato di caratteri dall'inizio della stringa.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-574">Returns an array with the specified number of elements from the start of the array, or a string with the specified number of characters from the start of the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="fd0b4-575">Parametri</span><span class="sxs-lookup"><span data-stu-id="fd0b4-575">Parameters</span></span>

| <span data-ttu-id="fd0b4-576">Parametro</span><span class="sxs-lookup"><span data-stu-id="fd0b4-576">Parameter</span></span> | <span data-ttu-id="fd0b4-577">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="fd0b4-577">Required</span></span> | <span data-ttu-id="fd0b4-578">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-578">Type</span></span> | <span data-ttu-id="fd0b4-579">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fd0b4-579">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="fd0b4-580">originalValue</span><span class="sxs-lookup"><span data-stu-id="fd0b4-580">originalValue</span></span> |<span data-ttu-id="fd0b4-581">Sì</span><span class="sxs-lookup"><span data-stu-id="fd0b4-581">Yes</span></span> |<span data-ttu-id="fd0b4-582">stringa o matrice</span><span class="sxs-lookup"><span data-stu-id="fd0b4-582">array or string</span></span> |<span data-ttu-id="fd0b4-583">Stringa o matrice da cui prendere gli elementi.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-583">The array or string to take the elements from.</span></span> |
| <span data-ttu-id="fd0b4-584">numberToTake</span><span class="sxs-lookup"><span data-stu-id="fd0b4-584">numberToTake</span></span> |<span data-ttu-id="fd0b4-585">Sì</span><span class="sxs-lookup"><span data-stu-id="fd0b4-585">Yes</span></span> |<span data-ttu-id="fd0b4-586">int</span><span class="sxs-lookup"><span data-stu-id="fd0b4-586">int</span></span> |<span data-ttu-id="fd0b4-587">Numero di elementi o caratteri da prendere.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-587">The number of elements or characters to take.</span></span> <span data-ttu-id="fd0b4-588">Se il valore è minore o uguale a 0, viene restituita una stringa o un matrice vuota.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-588">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="fd0b4-589">Se il valore è maggiore della lunghezza della stringa o matrice specificata, vengono restituiti tutti gli elementi nella stringa o nella matrice.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-589">If it is larger than the length of the given array or string, all the elements in the array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="fd0b4-590">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="fd0b4-590">Return value</span></span>

<span data-ttu-id="fd0b4-591">Stringa o matrice.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-591">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="fd0b4-592">Esempio</span><span class="sxs-lookup"><span data-stu-id="fd0b4-592">Example</span></span>

<span data-ttu-id="fd0b4-593">L'esempio seguente prende il numero specificato di elementi dalla matrice e di caratteri dalla stringa.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-593">The following example takes the specified number of elements from the array, and characters from a string.</span></span>

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

<span data-ttu-id="fd0b4-594">L'output dell'esempio precedente con i valori predefiniti è il seguente:</span><span class="sxs-lookup"><span data-stu-id="fd0b4-594">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="fd0b4-595">Nome</span><span class="sxs-lookup"><span data-stu-id="fd0b4-595">Name</span></span> | <span data-ttu-id="fd0b4-596">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-596">Type</span></span> | <span data-ttu-id="fd0b4-597">Valore</span><span class="sxs-lookup"><span data-stu-id="fd0b4-597">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="fd0b4-598">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="fd0b4-598">arrayOutput</span></span> | <span data-ttu-id="fd0b4-599">Array</span><span class="sxs-lookup"><span data-stu-id="fd0b4-599">Array</span></span> | <span data-ttu-id="fd0b4-600">["one", "two"]</span><span class="sxs-lookup"><span data-stu-id="fd0b4-600">["one", "two"]</span></span> |
| <span data-ttu-id="fd0b4-601">stringOutput</span><span class="sxs-lookup"><span data-stu-id="fd0b4-601">stringOutput</span></span> | <span data-ttu-id="fd0b4-602">String</span><span class="sxs-lookup"><span data-stu-id="fd0b4-602">String</span></span> | <span data-ttu-id="fd0b4-603">in</span><span class="sxs-lookup"><span data-stu-id="fd0b4-603">on</span></span> |

<a id="union" />

## <a name="union"></a><span data-ttu-id="fd0b4-604">union</span><span class="sxs-lookup"><span data-stu-id="fd0b4-604">union</span></span>
`union(arg1, arg2, arg3, ...)`

<span data-ttu-id="fd0b4-605">Restituisce una matrice o un oggetto singoli con tutti gli elementi dei parametri.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-605">Returns a single array or object with all elements from the parameters.</span></span> <span data-ttu-id="fd0b4-606">Valori e chiavi duplicati sono inclusi una sola volta.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-606">Duplicate values or keys are only included once.</span></span>

### <a name="parameters"></a><span data-ttu-id="fd0b4-607">Parametri</span><span class="sxs-lookup"><span data-stu-id="fd0b4-607">Parameters</span></span>

| <span data-ttu-id="fd0b4-608">Parametro</span><span class="sxs-lookup"><span data-stu-id="fd0b4-608">Parameter</span></span> | <span data-ttu-id="fd0b4-609">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="fd0b4-609">Required</span></span> | <span data-ttu-id="fd0b4-610">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-610">Type</span></span> | <span data-ttu-id="fd0b4-611">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fd0b4-611">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="fd0b4-612">arg1</span><span class="sxs-lookup"><span data-stu-id="fd0b4-612">arg1</span></span> |<span data-ttu-id="fd0b4-613">Sì</span><span class="sxs-lookup"><span data-stu-id="fd0b4-613">Yes</span></span> |<span data-ttu-id="fd0b4-614">matrice o oggetto</span><span class="sxs-lookup"><span data-stu-id="fd0b4-614">array or object</span></span> |<span data-ttu-id="fd0b4-615">Primo valore da usare per l'aggiunta di elementi.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-615">The first value to use for joining elements.</span></span> |
| <span data-ttu-id="fd0b4-616">arg2</span><span class="sxs-lookup"><span data-stu-id="fd0b4-616">arg2</span></span> |<span data-ttu-id="fd0b4-617">Sì</span><span class="sxs-lookup"><span data-stu-id="fd0b4-617">Yes</span></span> |<span data-ttu-id="fd0b4-618">matrice o oggetto</span><span class="sxs-lookup"><span data-stu-id="fd0b4-618">array or object</span></span> |<span data-ttu-id="fd0b4-619">Secondo valore da usare per l'aggiunta di elementi.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-619">The second value to use for joining elements.</span></span> |
| <span data-ttu-id="fd0b4-620">argomenti aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="fd0b4-620">additional arguments</span></span> |<span data-ttu-id="fd0b4-621">No</span><span class="sxs-lookup"><span data-stu-id="fd0b4-621">No</span></span> |<span data-ttu-id="fd0b4-622">matrice o oggetto</span><span class="sxs-lookup"><span data-stu-id="fd0b4-622">array or object</span></span> |<span data-ttu-id="fd0b4-623">Valori aggiuntivi da usare per l'aggiunta di elementi.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-623">Additional values to use for joining elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="fd0b4-624">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="fd0b4-624">Return value</span></span>

<span data-ttu-id="fd0b4-625">Una matrice o un oggetto.</span><span class="sxs-lookup"><span data-stu-id="fd0b4-625">An array or object.</span></span>

### <a name="example"></a><span data-ttu-id="fd0b4-626">Esempio</span><span class="sxs-lookup"><span data-stu-id="fd0b4-626">Example</span></span>

<span data-ttu-id="fd0b4-627">L'esempio seguente mostra come usare l'unione con matrici e oggetti:</span><span class="sxs-lookup"><span data-stu-id="fd0b4-627">The following example shows how to use union with arrays and objects:</span></span>

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

<span data-ttu-id="fd0b4-628">L'output dell'esempio precedente con i valori predefiniti è il seguente:</span><span class="sxs-lookup"><span data-stu-id="fd0b4-628">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="fd0b4-629">Nome</span><span class="sxs-lookup"><span data-stu-id="fd0b4-629">Name</span></span> | <span data-ttu-id="fd0b4-630">Tipo</span><span class="sxs-lookup"><span data-stu-id="fd0b4-630">Type</span></span> | <span data-ttu-id="fd0b4-631">Valore</span><span class="sxs-lookup"><span data-stu-id="fd0b4-631">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="fd0b4-632">objectOutput</span><span class="sxs-lookup"><span data-stu-id="fd0b4-632">objectOutput</span></span> | <span data-ttu-id="fd0b4-633">Oggetto</span><span class="sxs-lookup"><span data-stu-id="fd0b4-633">Object</span></span> | <span data-ttu-id="fd0b4-634">{"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"}</span><span class="sxs-lookup"><span data-stu-id="fd0b4-634">{"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"}</span></span> |
| <span data-ttu-id="fd0b4-635">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="fd0b4-635">arrayOutput</span></span> | <span data-ttu-id="fd0b4-636">Array</span><span class="sxs-lookup"><span data-stu-id="fd0b4-636">Array</span></span> | <span data-ttu-id="fd0b4-637">["one", "two", "three", "four"]</span><span class="sxs-lookup"><span data-stu-id="fd0b4-637">["one", "two", "three", "four"]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fd0b4-638">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fd0b4-638">Next steps</span></span>
* <span data-ttu-id="fd0b4-639">Per una descrizione delle sezioni in un modello di Azure Resource Manager, vedere [Creazione di modelli di Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="fd0b4-639">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="fd0b4-640">Per unire più modelli, vedere [Uso di modelli collegati con Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="fd0b4-640">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="fd0b4-641">Per eseguire un'iterazione di un numero di volte specificato durante la creazione di un tipo di risorsa, vedere [Creare più istanze di risorse in Gestione risorse di Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="fd0b4-641">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="fd0b4-642">Per informazioni su come distribuire il modello che è stato creato, vedere [Distribuire un'applicazione con un modello di Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="fd0b4-642">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

