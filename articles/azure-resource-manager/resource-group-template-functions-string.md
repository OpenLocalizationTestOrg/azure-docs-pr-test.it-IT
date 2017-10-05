---
title: Funzioni del modello di Azure Resource Manager - Stringa | Documentazione Microsoft
description: Informazioni sulle funzioni da usare in un modello di Azure Resource Manager per operare con le stringhe.
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
ms.openlocfilehash: 3e5c9ca546629f782a3d722b49f5fbaf5147e823
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="string-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="266ea-103">Funzioni di stringa nei modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="266ea-103">String functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="266ea-104">Gestione risorse fornisce le funzioni seguenti per usare le stringhe:</span><span class="sxs-lookup"><span data-stu-id="266ea-104">Resource Manager provides the following functions for working with strings:</span></span>

* [<span data-ttu-id="266ea-105">base64</span><span class="sxs-lookup"><span data-stu-id="266ea-105">base64</span></span>](#base64)
* [<span data-ttu-id="266ea-106">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="266ea-106">base64ToJson</span></span>](#base64tojson)
* [<span data-ttu-id="266ea-107">base64ToString</span><span class="sxs-lookup"><span data-stu-id="266ea-107">base64ToString</span></span>](#base64tostring)
* [<span data-ttu-id="266ea-108">concat</span><span class="sxs-lookup"><span data-stu-id="266ea-108">concat</span></span>](#concat)
* [<span data-ttu-id="266ea-109">contains</span><span class="sxs-lookup"><span data-stu-id="266ea-109">contains</span></span>](#contains)
* [<span data-ttu-id="266ea-110">dataUri</span><span class="sxs-lookup"><span data-stu-id="266ea-110">dataUri</span></span>](#datauri)
* [<span data-ttu-id="266ea-111">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="266ea-111">dataUriToString</span></span>](#datauritostring)
* [<span data-ttu-id="266ea-112">empty</span><span class="sxs-lookup"><span data-stu-id="266ea-112">empty</span></span>](#empty)
* [<span data-ttu-id="266ea-113">endsWith</span><span class="sxs-lookup"><span data-stu-id="266ea-113">endsWith</span></span>](#endswith)
* [<span data-ttu-id="266ea-114">first</span><span class="sxs-lookup"><span data-stu-id="266ea-114">first</span></span>](#first)
* [<span data-ttu-id="266ea-115">indexOf</span><span class="sxs-lookup"><span data-stu-id="266ea-115">indexOf</span></span>](#indexof)
* [<span data-ttu-id="266ea-116">last</span><span class="sxs-lookup"><span data-stu-id="266ea-116">last</span></span>](#last)
* [<span data-ttu-id="266ea-117">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="266ea-117">lastIndexOf</span></span>](#lastindexof)
* [<span data-ttu-id="266ea-118">length</span><span class="sxs-lookup"><span data-stu-id="266ea-118">length</span></span>](#length)
* [<span data-ttu-id="266ea-119">padLeft</span><span class="sxs-lookup"><span data-stu-id="266ea-119">padLeft</span></span>](#padleft)
* [<span data-ttu-id="266ea-120">replace</span><span class="sxs-lookup"><span data-stu-id="266ea-120">replace</span></span>](#replace)
* [<span data-ttu-id="266ea-121">skip</span><span class="sxs-lookup"><span data-stu-id="266ea-121">skip</span></span>](#skip)
* [<span data-ttu-id="266ea-122">split</span><span class="sxs-lookup"><span data-stu-id="266ea-122">split</span></span>](#split)
* [<span data-ttu-id="266ea-123">startsWith</span><span class="sxs-lookup"><span data-stu-id="266ea-123">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="266ea-124">string</span><span class="sxs-lookup"><span data-stu-id="266ea-124">string</span></span>](#string)
* [<span data-ttu-id="266ea-125">substring</span><span class="sxs-lookup"><span data-stu-id="266ea-125">substring</span></span>](#substring)
* [<span data-ttu-id="266ea-126">take</span><span class="sxs-lookup"><span data-stu-id="266ea-126">take</span></span>](#take)
* [<span data-ttu-id="266ea-127">toLower</span><span class="sxs-lookup"><span data-stu-id="266ea-127">toLower</span></span>](#tolower)
* [<span data-ttu-id="266ea-128">toUpper</span><span class="sxs-lookup"><span data-stu-id="266ea-128">toUpper</span></span>](#toupper)
* [<span data-ttu-id="266ea-129">Trim</span><span class="sxs-lookup"><span data-stu-id="266ea-129">trim</span></span>](#trim)
* [<span data-ttu-id="266ea-130">uniqueString</span><span class="sxs-lookup"><span data-stu-id="266ea-130">uniqueString</span></span>](#uniquestring)
* [<span data-ttu-id="266ea-131">Uri</span><span class="sxs-lookup"><span data-stu-id="266ea-131">uri</span></span>](#uri)
* [<span data-ttu-id="266ea-132">uriComponent</span><span class="sxs-lookup"><span data-stu-id="266ea-132">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="266ea-133">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="266ea-133">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)

<a id="base64" />

## <a name="base64"></a><span data-ttu-id="266ea-134">base64</span><span class="sxs-lookup"><span data-stu-id="266ea-134">base64</span></span>
`base64(inputString)`

<span data-ttu-id="266ea-135">Restituisce la rappresentazione base64 della stringa di input.</span><span class="sxs-lookup"><span data-stu-id="266ea-135">Returns the base64 representation of the input string.</span></span>

### <a name="parameters"></a><span data-ttu-id="266ea-136">Parametri</span><span class="sxs-lookup"><span data-stu-id="266ea-136">Parameters</span></span>

| <span data-ttu-id="266ea-137">Parametro</span><span class="sxs-lookup"><span data-stu-id="266ea-137">Parameter</span></span> | <span data-ttu-id="266ea-138">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="266ea-138">Required</span></span> | <span data-ttu-id="266ea-139">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-139">Type</span></span> | <span data-ttu-id="266ea-140">Descrizione</span><span class="sxs-lookup"><span data-stu-id="266ea-140">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="266ea-141">inputString</span><span class="sxs-lookup"><span data-stu-id="266ea-141">inputString</span></span> |<span data-ttu-id="266ea-142">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-142">Yes</span></span> |<span data-ttu-id="266ea-143">string</span><span class="sxs-lookup"><span data-stu-id="266ea-143">string</span></span> |<span data-ttu-id="266ea-144">Il valore da restituire come rappresentazione base64.</span><span class="sxs-lookup"><span data-stu-id="266ea-144">The value to return as a base64 representation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="266ea-145">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="266ea-145">Return value</span></span>

<span data-ttu-id="266ea-146">Stringa contenente la rappresentazione base64.</span><span class="sxs-lookup"><span data-stu-id="266ea-146">A string containing the base64 representation.</span></span>

### <a name="examples"></a><span data-ttu-id="266ea-147">esempi</span><span class="sxs-lookup"><span data-stu-id="266ea-147">Examples</span></span>

<span data-ttu-id="266ea-148">L'esempio seguente mostra come usare la funzione base64.</span><span class="sxs-lookup"><span data-stu-id="266ea-148">The following example shows how to use the base64 function.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

<span data-ttu-id="266ea-149">L'output dell'esempio precedente con i valori predefiniti è:</span><span class="sxs-lookup"><span data-stu-id="266ea-149">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="266ea-150">Nome</span><span class="sxs-lookup"><span data-stu-id="266ea-150">Name</span></span> | <span data-ttu-id="266ea-151">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-151">Type</span></span> | <span data-ttu-id="266ea-152">Valore</span><span class="sxs-lookup"><span data-stu-id="266ea-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="266ea-153">base64Output</span><span class="sxs-lookup"><span data-stu-id="266ea-153">base64Output</span></span> | <span data-ttu-id="266ea-154">String</span><span class="sxs-lookup"><span data-stu-id="266ea-154">String</span></span> | <span data-ttu-id="266ea-155">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="266ea-155">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="266ea-156">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-156">toStringOutput</span></span> | <span data-ttu-id="266ea-157">String</span><span class="sxs-lookup"><span data-stu-id="266ea-157">String</span></span> | <span data-ttu-id="266ea-158">one, two, three</span><span class="sxs-lookup"><span data-stu-id="266ea-158">one, two, three</span></span> |
| <span data-ttu-id="266ea-159">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-159">toJsonOutput</span></span> | <span data-ttu-id="266ea-160">Oggetto</span><span class="sxs-lookup"><span data-stu-id="266ea-160">Object</span></span> | <span data-ttu-id="266ea-161">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="266ea-161">{"one": "a", "two": "b"}</span></span> |

<a id="base64tojson" />

## <a name="base64tojson"></a><span data-ttu-id="266ea-162">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="266ea-162">base64ToJson</span></span>
`base64tojson`

<span data-ttu-id="266ea-163">Converte una rappresentazione base64 in un oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="266ea-163">Converts a base64 representation to a JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="266ea-164">Parametri</span><span class="sxs-lookup"><span data-stu-id="266ea-164">Parameters</span></span>

| <span data-ttu-id="266ea-165">Parametro</span><span class="sxs-lookup"><span data-stu-id="266ea-165">Parameter</span></span> | <span data-ttu-id="266ea-166">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="266ea-166">Required</span></span> | <span data-ttu-id="266ea-167">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-167">Type</span></span> | <span data-ttu-id="266ea-168">Descrizione</span><span class="sxs-lookup"><span data-stu-id="266ea-168">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="266ea-169">base64Value</span><span class="sxs-lookup"><span data-stu-id="266ea-169">base64Value</span></span> |<span data-ttu-id="266ea-170">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-170">Yes</span></span> |<span data-ttu-id="266ea-171">string</span><span class="sxs-lookup"><span data-stu-id="266ea-171">string</span></span> |<span data-ttu-id="266ea-172">Rappresentazione base64 da convertire in un oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="266ea-172">The base64 representation to convert to a JSON object.</span></span> |

### <a name="return-value"></a><span data-ttu-id="266ea-173">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="266ea-173">Return value</span></span>

<span data-ttu-id="266ea-174">Oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="266ea-174">A JSON object.</span></span>

### <a name="examples"></a><span data-ttu-id="266ea-175">esempi</span><span class="sxs-lookup"><span data-stu-id="266ea-175">Examples</span></span>

<span data-ttu-id="266ea-176">L'esempio seguente usa la funzione base64ToJson per convertire un valore base64:</span><span class="sxs-lookup"><span data-stu-id="266ea-176">The following example uses the base64ToJson function to convert a base64 value:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

<span data-ttu-id="266ea-177">L'output dell'esempio precedente con i valori predefiniti è:</span><span class="sxs-lookup"><span data-stu-id="266ea-177">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="266ea-178">Nome</span><span class="sxs-lookup"><span data-stu-id="266ea-178">Name</span></span> | <span data-ttu-id="266ea-179">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-179">Type</span></span> | <span data-ttu-id="266ea-180">Valore</span><span class="sxs-lookup"><span data-stu-id="266ea-180">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="266ea-181">base64Output</span><span class="sxs-lookup"><span data-stu-id="266ea-181">base64Output</span></span> | <span data-ttu-id="266ea-182">String</span><span class="sxs-lookup"><span data-stu-id="266ea-182">String</span></span> | <span data-ttu-id="266ea-183">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="266ea-183">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="266ea-184">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-184">toStringOutput</span></span> | <span data-ttu-id="266ea-185">String</span><span class="sxs-lookup"><span data-stu-id="266ea-185">String</span></span> | <span data-ttu-id="266ea-186">one, two, three</span><span class="sxs-lookup"><span data-stu-id="266ea-186">one, two, three</span></span> |
| <span data-ttu-id="266ea-187">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-187">toJsonOutput</span></span> | <span data-ttu-id="266ea-188">Oggetto</span><span class="sxs-lookup"><span data-stu-id="266ea-188">Object</span></span> | <span data-ttu-id="266ea-189">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="266ea-189">{"one": "a", "two": "b"}</span></span> |

<a id="base64tostring" />

## <a name="base64tostring"></a><span data-ttu-id="266ea-190">base64ToString</span><span class="sxs-lookup"><span data-stu-id="266ea-190">base64ToString</span></span>
`base64ToString(base64Value)`

<span data-ttu-id="266ea-191">Converte una rappresentazione base64 in una stringa.</span><span class="sxs-lookup"><span data-stu-id="266ea-191">Converts a base64 representation to a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="266ea-192">Parametri</span><span class="sxs-lookup"><span data-stu-id="266ea-192">Parameters</span></span>

| <span data-ttu-id="266ea-193">Parametro</span><span class="sxs-lookup"><span data-stu-id="266ea-193">Parameter</span></span> | <span data-ttu-id="266ea-194">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="266ea-194">Required</span></span> | <span data-ttu-id="266ea-195">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-195">Type</span></span> | <span data-ttu-id="266ea-196">Descrizione</span><span class="sxs-lookup"><span data-stu-id="266ea-196">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="266ea-197">base64Value</span><span class="sxs-lookup"><span data-stu-id="266ea-197">base64Value</span></span> |<span data-ttu-id="266ea-198">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-198">Yes</span></span> |<span data-ttu-id="266ea-199">string</span><span class="sxs-lookup"><span data-stu-id="266ea-199">string</span></span> |<span data-ttu-id="266ea-200">Rappresentazione base64 da convertire in stringa.</span><span class="sxs-lookup"><span data-stu-id="266ea-200">The base64 representation to convert to a string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="266ea-201">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="266ea-201">Return value</span></span>

<span data-ttu-id="266ea-202">Stringa del valore base64 convertito.</span><span class="sxs-lookup"><span data-stu-id="266ea-202">A string of the converted base64 value.</span></span>

### <a name="examples"></a><span data-ttu-id="266ea-203">esempi</span><span class="sxs-lookup"><span data-stu-id="266ea-203">Examples</span></span>

<span data-ttu-id="266ea-204">L'esempio seguente usa la funzione base64ToString per convertire un valore base64:</span><span class="sxs-lookup"><span data-stu-id="266ea-204">The following example uses the base64ToString function to convert a base64 value:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

<span data-ttu-id="266ea-205">L'output dell'esempio precedente con i valori predefiniti è:</span><span class="sxs-lookup"><span data-stu-id="266ea-205">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="266ea-206">Nome</span><span class="sxs-lookup"><span data-stu-id="266ea-206">Name</span></span> | <span data-ttu-id="266ea-207">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-207">Type</span></span> | <span data-ttu-id="266ea-208">Valore</span><span class="sxs-lookup"><span data-stu-id="266ea-208">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="266ea-209">base64Output</span><span class="sxs-lookup"><span data-stu-id="266ea-209">base64Output</span></span> | <span data-ttu-id="266ea-210">String</span><span class="sxs-lookup"><span data-stu-id="266ea-210">String</span></span> | <span data-ttu-id="266ea-211">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="266ea-211">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="266ea-212">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-212">toStringOutput</span></span> | <span data-ttu-id="266ea-213">String</span><span class="sxs-lookup"><span data-stu-id="266ea-213">String</span></span> | <span data-ttu-id="266ea-214">one, two, three</span><span class="sxs-lookup"><span data-stu-id="266ea-214">one, two, three</span></span> |
| <span data-ttu-id="266ea-215">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-215">toJsonOutput</span></span> | <span data-ttu-id="266ea-216">Oggetto</span><span class="sxs-lookup"><span data-stu-id="266ea-216">Object</span></span> | <span data-ttu-id="266ea-217">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="266ea-217">{"one": "a", "two": "b"}</span></span> |



<a id="concat" />

## <a name="concat"></a><span data-ttu-id="266ea-218">concat</span><span class="sxs-lookup"><span data-stu-id="266ea-218">concat</span></span>
`concat (arg1, arg2, arg3, ...)`

<span data-ttu-id="266ea-219">Combina più valori stringa e restituisce la stringa concatenata oppure combina più matrici e restituisce la matrice concatenata.</span><span class="sxs-lookup"><span data-stu-id="266ea-219">Combines multiple string values and returns the concatenated string, or combines multiple arrays and returns the concatenated array.</span></span>

### <a name="parameters"></a><span data-ttu-id="266ea-220">Parametri</span><span class="sxs-lookup"><span data-stu-id="266ea-220">Parameters</span></span>

| <span data-ttu-id="266ea-221">Parametro</span><span class="sxs-lookup"><span data-stu-id="266ea-221">Parameter</span></span> | <span data-ttu-id="266ea-222">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="266ea-222">Required</span></span> | <span data-ttu-id="266ea-223">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-223">Type</span></span> | <span data-ttu-id="266ea-224">Descrizione</span><span class="sxs-lookup"><span data-stu-id="266ea-224">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="266ea-225">arg1</span><span class="sxs-lookup"><span data-stu-id="266ea-225">arg1</span></span> |<span data-ttu-id="266ea-226">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-226">Yes</span></span> |<span data-ttu-id="266ea-227">Stringa o matrice</span><span class="sxs-lookup"><span data-stu-id="266ea-227">string or array</span></span> |<span data-ttu-id="266ea-228">Il primo valore per la concatenazione.</span><span class="sxs-lookup"><span data-stu-id="266ea-228">The first value for concatenation.</span></span> |
| <span data-ttu-id="266ea-229">Argomenti aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="266ea-229">additional arguments</span></span> |<span data-ttu-id="266ea-230">No</span><span class="sxs-lookup"><span data-stu-id="266ea-230">No</span></span> |<span data-ttu-id="266ea-231">string</span><span class="sxs-lookup"><span data-stu-id="266ea-231">string</span></span> |<span data-ttu-id="266ea-232">Altri valori in ordine sequenziale per la concatenazione.</span><span class="sxs-lookup"><span data-stu-id="266ea-232">Additional values in sequential order for concatenation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="266ea-233">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="266ea-233">Return value</span></span>
<span data-ttu-id="266ea-234">Stringa o matrice di valori concatenati.</span><span class="sxs-lookup"><span data-stu-id="266ea-234">A string or array of concatenated values.</span></span>

### <a name="examples"></a><span data-ttu-id="266ea-235">esempi</span><span class="sxs-lookup"><span data-stu-id="266ea-235">Examples</span></span>

<span data-ttu-id="266ea-236">L'esempio seguente illustra come combinare due valori stringa e restituisce una stringa concatenata.</span><span class="sxs-lookup"><span data-stu-id="266ea-236">The following example shows how to combine two string values and return a concatenated string.</span></span>

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

<span data-ttu-id="266ea-237">L'output dell'esempio precedente con i valori predefiniti è il seguente:</span><span class="sxs-lookup"><span data-stu-id="266ea-237">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="266ea-238">Nome</span><span class="sxs-lookup"><span data-stu-id="266ea-238">Name</span></span> | <span data-ttu-id="266ea-239">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-239">Type</span></span> | <span data-ttu-id="266ea-240">Valore</span><span class="sxs-lookup"><span data-stu-id="266ea-240">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="266ea-241">concatOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-241">concatOutput</span></span> | <span data-ttu-id="266ea-242">String</span><span class="sxs-lookup"><span data-stu-id="266ea-242">String</span></span> | <span data-ttu-id="266ea-243">prefix-5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="266ea-243">prefix-5yj4yjf5mbg72</span></span> |

<span data-ttu-id="266ea-244">L'esempio seguente illustra come combinare due matrici.</span><span class="sxs-lookup"><span data-stu-id="266ea-244">The following example shows how to combine two arrays.</span></span>

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

<span data-ttu-id="266ea-245">L'output dell'esempio precedente con i valori predefiniti è il seguente:</span><span class="sxs-lookup"><span data-stu-id="266ea-245">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="266ea-246">Nome</span><span class="sxs-lookup"><span data-stu-id="266ea-246">Name</span></span> | <span data-ttu-id="266ea-247">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-247">Type</span></span> | <span data-ttu-id="266ea-248">Valore</span><span class="sxs-lookup"><span data-stu-id="266ea-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="266ea-249">return</span><span class="sxs-lookup"><span data-stu-id="266ea-249">return</span></span> | <span data-ttu-id="266ea-250">Array</span><span class="sxs-lookup"><span data-stu-id="266ea-250">Array</span></span> | <span data-ttu-id="266ea-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="266ea-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="266ea-252">contains</span><span class="sxs-lookup"><span data-stu-id="266ea-252">contains</span></span>
`contains (container, itemToFind)`

<span data-ttu-id="266ea-253">Verifica se una matrice contiene un valore, se un oggetto contiene una chiave o se una stringa contiene una sottostringa.</span><span class="sxs-lookup"><span data-stu-id="266ea-253">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="266ea-254">Parametri</span><span class="sxs-lookup"><span data-stu-id="266ea-254">Parameters</span></span>

| <span data-ttu-id="266ea-255">Parametro</span><span class="sxs-lookup"><span data-stu-id="266ea-255">Parameter</span></span> | <span data-ttu-id="266ea-256">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="266ea-256">Required</span></span> | <span data-ttu-id="266ea-257">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-257">Type</span></span> | <span data-ttu-id="266ea-258">Descrizione</span><span class="sxs-lookup"><span data-stu-id="266ea-258">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="266ea-259">Contenitore</span><span class="sxs-lookup"><span data-stu-id="266ea-259">container</span></span> |<span data-ttu-id="266ea-260">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-260">Yes</span></span> |<span data-ttu-id="266ea-261">matrice, oggetto o stringa</span><span class="sxs-lookup"><span data-stu-id="266ea-261">array, object, or string</span></span> |<span data-ttu-id="266ea-262">Valore che contiene il valore da trovare.</span><span class="sxs-lookup"><span data-stu-id="266ea-262">The value that contains the value to find.</span></span> |
| <span data-ttu-id="266ea-263">itemToFind</span><span class="sxs-lookup"><span data-stu-id="266ea-263">itemToFind</span></span> |<span data-ttu-id="266ea-264">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-264">Yes</span></span> |<span data-ttu-id="266ea-265">stringa o numero intero</span><span class="sxs-lookup"><span data-stu-id="266ea-265">string or int</span></span> |<span data-ttu-id="266ea-266">Valore da trovare.</span><span class="sxs-lookup"><span data-stu-id="266ea-266">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="266ea-267">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="266ea-267">Return value</span></span>

<span data-ttu-id="266ea-268">**True** se l'elemento viene individuato; in caso contrario, restituisce **False**.</span><span class="sxs-lookup"><span data-stu-id="266ea-268">**True** if the item is found; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="266ea-269">esempi</span><span class="sxs-lookup"><span data-stu-id="266ea-269">Examples</span></span>

<span data-ttu-id="266ea-270">L'esempio seguente mostra come usare la funzione contains con tipi diversi:</span><span class="sxs-lookup"><span data-stu-id="266ea-270">The following example shows how to use contains with different types:</span></span>

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

<span data-ttu-id="266ea-271">L'output dell'esempio precedente con i valori predefiniti è il seguente:</span><span class="sxs-lookup"><span data-stu-id="266ea-271">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="266ea-272">Nome</span><span class="sxs-lookup"><span data-stu-id="266ea-272">Name</span></span> | <span data-ttu-id="266ea-273">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-273">Type</span></span> | <span data-ttu-id="266ea-274">Valore</span><span class="sxs-lookup"><span data-stu-id="266ea-274">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="266ea-275">stringTrue</span><span class="sxs-lookup"><span data-stu-id="266ea-275">stringTrue</span></span> | <span data-ttu-id="266ea-276">Booleano</span><span class="sxs-lookup"><span data-stu-id="266ea-276">Bool</span></span> | <span data-ttu-id="266ea-277">True </span><span class="sxs-lookup"><span data-stu-id="266ea-277">True</span></span> |
| <span data-ttu-id="266ea-278">stringFalse</span><span class="sxs-lookup"><span data-stu-id="266ea-278">stringFalse</span></span> | <span data-ttu-id="266ea-279">Booleano</span><span class="sxs-lookup"><span data-stu-id="266ea-279">Bool</span></span> | <span data-ttu-id="266ea-280">False</span><span class="sxs-lookup"><span data-stu-id="266ea-280">False</span></span> |
| <span data-ttu-id="266ea-281">objectTrue</span><span class="sxs-lookup"><span data-stu-id="266ea-281">objectTrue</span></span> | <span data-ttu-id="266ea-282">Booleano</span><span class="sxs-lookup"><span data-stu-id="266ea-282">Bool</span></span> | <span data-ttu-id="266ea-283">True </span><span class="sxs-lookup"><span data-stu-id="266ea-283">True</span></span> |
| <span data-ttu-id="266ea-284">objectFalse</span><span class="sxs-lookup"><span data-stu-id="266ea-284">objectFalse</span></span> | <span data-ttu-id="266ea-285">Booleano</span><span class="sxs-lookup"><span data-stu-id="266ea-285">Bool</span></span> | <span data-ttu-id="266ea-286">False</span><span class="sxs-lookup"><span data-stu-id="266ea-286">False</span></span> |
| <span data-ttu-id="266ea-287">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="266ea-287">arrayTrue</span></span> | <span data-ttu-id="266ea-288">Booleano</span><span class="sxs-lookup"><span data-stu-id="266ea-288">Bool</span></span> | <span data-ttu-id="266ea-289">True </span><span class="sxs-lookup"><span data-stu-id="266ea-289">True</span></span> |
| <span data-ttu-id="266ea-290">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="266ea-290">arrayFalse</span></span> | <span data-ttu-id="266ea-291">Booleano</span><span class="sxs-lookup"><span data-stu-id="266ea-291">Bool</span></span> | <span data-ttu-id="266ea-292">False</span><span class="sxs-lookup"><span data-stu-id="266ea-292">False</span></span> |

<a id="datauri" />

## <a name="datauri"></a><span data-ttu-id="266ea-293">dataUri</span><span class="sxs-lookup"><span data-stu-id="266ea-293">dataUri</span></span>
`dataUri(stringToConvert)`

<span data-ttu-id="266ea-294">Converte un valore in un URI di dati.</span><span class="sxs-lookup"><span data-stu-id="266ea-294">Converts a value to a data URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="266ea-295">Parametri</span><span class="sxs-lookup"><span data-stu-id="266ea-295">Parameters</span></span>

| <span data-ttu-id="266ea-296">Parametro</span><span class="sxs-lookup"><span data-stu-id="266ea-296">Parameter</span></span> | <span data-ttu-id="266ea-297">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="266ea-297">Required</span></span> | <span data-ttu-id="266ea-298">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-298">Type</span></span> | <span data-ttu-id="266ea-299">Descrizione</span><span class="sxs-lookup"><span data-stu-id="266ea-299">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="266ea-300">stringToConvert</span><span class="sxs-lookup"><span data-stu-id="266ea-300">stringToConvert</span></span> |<span data-ttu-id="266ea-301">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-301">Yes</span></span> |<span data-ttu-id="266ea-302">string</span><span class="sxs-lookup"><span data-stu-id="266ea-302">string</span></span> |<span data-ttu-id="266ea-303">Valore da convertire in un URI di dati.</span><span class="sxs-lookup"><span data-stu-id="266ea-303">The value to convert to a data URI.</span></span> |

### <a name="return-value"></a><span data-ttu-id="266ea-304">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="266ea-304">Return value</span></span>

<span data-ttu-id="266ea-305">Stringa formattata come URI di dati.</span><span class="sxs-lookup"><span data-stu-id="266ea-305">A string formatted as a data URI.</span></span>

### <a name="examples"></a><span data-ttu-id="266ea-306">esempi</span><span class="sxs-lookup"><span data-stu-id="266ea-306">Examples</span></span>

<span data-ttu-id="266ea-307">L'esempio seguente converte un valore in un URI di dati e converte un URI di dati in una stringa:</span><span class="sxs-lookup"><span data-stu-id="266ea-307">The following example converts a value to a data URI, and converts a data URI to a string:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "Hello"
        },
        "dataFormattedString": {
            "type": "string",
            "defaultValue": "data:;base64,SGVsbG8sIFdvcmxkIQ=="
        }
    },
    "resources": [],
    "outputs": {
        "dataUriOutput": {
            "value": "[dataUri(parameters('stringToTest'))]",
            "type" : "string"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[dataUriToString(parameters('dataFormattedString'))]"
        }
    }
}
```

<span data-ttu-id="266ea-308">L'output dell'esempio precedente con i valori predefiniti è:</span><span class="sxs-lookup"><span data-stu-id="266ea-308">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="266ea-309">Nome</span><span class="sxs-lookup"><span data-stu-id="266ea-309">Name</span></span> | <span data-ttu-id="266ea-310">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-310">Type</span></span> | <span data-ttu-id="266ea-311">Valore</span><span class="sxs-lookup"><span data-stu-id="266ea-311">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="266ea-312">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-312">dataUriOutput</span></span> | <span data-ttu-id="266ea-313">String</span><span class="sxs-lookup"><span data-stu-id="266ea-313">String</span></span> | <span data-ttu-id="266ea-314">data:text/plain;charset=utf8;base64,SGVsbG8=</span><span class="sxs-lookup"><span data-stu-id="266ea-314">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="266ea-315">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-315">toStringOutput</span></span> | <span data-ttu-id="266ea-316">String</span><span class="sxs-lookup"><span data-stu-id="266ea-316">String</span></span> | <span data-ttu-id="266ea-317">Hello, World!</span><span class="sxs-lookup"><span data-stu-id="266ea-317">Hello, World!</span></span> |

<a id="datauritostring" />

## <a name="datauritostring"></a><span data-ttu-id="266ea-318">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="266ea-318">dataUriToString</span></span>
`dataUriToString(dataUriToConvert)`

<span data-ttu-id="266ea-319">Converte un valore formattato come URI di dati in una stringa.</span><span class="sxs-lookup"><span data-stu-id="266ea-319">Converts a data URI formatted value to a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="266ea-320">Parametri</span><span class="sxs-lookup"><span data-stu-id="266ea-320">Parameters</span></span>

| <span data-ttu-id="266ea-321">Parametro</span><span class="sxs-lookup"><span data-stu-id="266ea-321">Parameter</span></span> | <span data-ttu-id="266ea-322">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="266ea-322">Required</span></span> | <span data-ttu-id="266ea-323">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-323">Type</span></span> | <span data-ttu-id="266ea-324">Descrizione</span><span class="sxs-lookup"><span data-stu-id="266ea-324">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="266ea-325">dataUriToConvert</span><span class="sxs-lookup"><span data-stu-id="266ea-325">dataUriToConvert</span></span> |<span data-ttu-id="266ea-326">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-326">Yes</span></span> |<span data-ttu-id="266ea-327">string</span><span class="sxs-lookup"><span data-stu-id="266ea-327">string</span></span> |<span data-ttu-id="266ea-328">Valore dell'URI di dati da convertire.</span><span class="sxs-lookup"><span data-stu-id="266ea-328">The data URI value to convert.</span></span> |

### <a name="return-value"></a><span data-ttu-id="266ea-329">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="266ea-329">Return value</span></span>

<span data-ttu-id="266ea-330">Stringa contenente il valore convertito.</span><span class="sxs-lookup"><span data-stu-id="266ea-330">A string containing the converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="266ea-331">esempi</span><span class="sxs-lookup"><span data-stu-id="266ea-331">Examples</span></span>

<span data-ttu-id="266ea-332">L'esempio seguente converte un valore in un URI di dati e converte un URI di dati in una stringa:</span><span class="sxs-lookup"><span data-stu-id="266ea-332">The following example converts a value to a data URI, and converts a data URI to a string:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "Hello"
        },
        "dataFormattedString": {
            "type": "string",
            "defaultValue": "data:;base64,SGVsbG8sIFdvcmxkIQ=="
        }
    },
    "resources": [],
    "outputs": {
        "dataUriOutput": {
            "value": "[dataUri(parameters('stringToTest'))]",
            "type" : "string"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[dataUriToString(parameters('dataFormattedString'))]"
        }
    }
}
```

<span data-ttu-id="266ea-333">L'output dell'esempio precedente con i valori predefiniti è:</span><span class="sxs-lookup"><span data-stu-id="266ea-333">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="266ea-334">Nome</span><span class="sxs-lookup"><span data-stu-id="266ea-334">Name</span></span> | <span data-ttu-id="266ea-335">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-335">Type</span></span> | <span data-ttu-id="266ea-336">Valore</span><span class="sxs-lookup"><span data-stu-id="266ea-336">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="266ea-337">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-337">dataUriOutput</span></span> | <span data-ttu-id="266ea-338">String</span><span class="sxs-lookup"><span data-stu-id="266ea-338">String</span></span> | <span data-ttu-id="266ea-339">data:text/plain;charset=utf8;base64,SGVsbG8=</span><span class="sxs-lookup"><span data-stu-id="266ea-339">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="266ea-340">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-340">toStringOutput</span></span> | <span data-ttu-id="266ea-341">String</span><span class="sxs-lookup"><span data-stu-id="266ea-341">String</span></span> | <span data-ttu-id="266ea-342">Hello, World!</span><span class="sxs-lookup"><span data-stu-id="266ea-342">Hello, World!</span></span> |

<a id="empty" /> 

## <a name="empty"></a><span data-ttu-id="266ea-343">empty</span><span class="sxs-lookup"><span data-stu-id="266ea-343">empty</span></span>
`empty(itemToTest)`

<span data-ttu-id="266ea-344">Determina se una matrice, un oggetto o una stringa sono vuoti.</span><span class="sxs-lookup"><span data-stu-id="266ea-344">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="266ea-345">Parametri</span><span class="sxs-lookup"><span data-stu-id="266ea-345">Parameters</span></span>

| <span data-ttu-id="266ea-346">Parametro</span><span class="sxs-lookup"><span data-stu-id="266ea-346">Parameter</span></span> | <span data-ttu-id="266ea-347">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="266ea-347">Required</span></span> | <span data-ttu-id="266ea-348">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-348">Type</span></span> | <span data-ttu-id="266ea-349">Descrizione</span><span class="sxs-lookup"><span data-stu-id="266ea-349">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="266ea-350">itemToTest</span><span class="sxs-lookup"><span data-stu-id="266ea-350">itemToTest</span></span> |<span data-ttu-id="266ea-351">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-351">Yes</span></span> |<span data-ttu-id="266ea-352">matrice, oggetto o stringa</span><span class="sxs-lookup"><span data-stu-id="266ea-352">array, object, or string</span></span> |<span data-ttu-id="266ea-353">Valore da controllare per verificare se è vuoto.</span><span class="sxs-lookup"><span data-stu-id="266ea-353">The value to check if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="266ea-354">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="266ea-354">Return value</span></span>

<span data-ttu-id="266ea-355">**True** se il valore è vuoto; in caso contrario, restituisce **False**.</span><span class="sxs-lookup"><span data-stu-id="266ea-355">Returns **True** if the value is empty; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="266ea-356">esempi</span><span class="sxs-lookup"><span data-stu-id="266ea-356">Examples</span></span>

<span data-ttu-id="266ea-357">L'esempio seguente controlla se una matrice, un oggetto e una stringa sono vuoti.</span><span class="sxs-lookup"><span data-stu-id="266ea-357">The following example checks whether an array, object, and string are empty.</span></span>

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

<span data-ttu-id="266ea-358">L'output dell'esempio precedente con i valori predefiniti è il seguente:</span><span class="sxs-lookup"><span data-stu-id="266ea-358">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="266ea-359">Nome</span><span class="sxs-lookup"><span data-stu-id="266ea-359">Name</span></span> | <span data-ttu-id="266ea-360">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-360">Type</span></span> | <span data-ttu-id="266ea-361">Valore</span><span class="sxs-lookup"><span data-stu-id="266ea-361">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="266ea-362">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="266ea-362">arrayEmpty</span></span> | <span data-ttu-id="266ea-363">Booleano</span><span class="sxs-lookup"><span data-stu-id="266ea-363">Bool</span></span> | <span data-ttu-id="266ea-364">True </span><span class="sxs-lookup"><span data-stu-id="266ea-364">True</span></span> |
| <span data-ttu-id="266ea-365">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="266ea-365">objectEmpty</span></span> | <span data-ttu-id="266ea-366">Booleano</span><span class="sxs-lookup"><span data-stu-id="266ea-366">Bool</span></span> | <span data-ttu-id="266ea-367">True </span><span class="sxs-lookup"><span data-stu-id="266ea-367">True</span></span> |
| <span data-ttu-id="266ea-368">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="266ea-368">stringEmpty</span></span> | <span data-ttu-id="266ea-369">Booleano</span><span class="sxs-lookup"><span data-stu-id="266ea-369">Bool</span></span> | <span data-ttu-id="266ea-370">True </span><span class="sxs-lookup"><span data-stu-id="266ea-370">True</span></span> |

<a id="endswith" />

## <a name="endswith"></a><span data-ttu-id="266ea-371">endsWith</span><span class="sxs-lookup"><span data-stu-id="266ea-371">endsWith</span></span>
`endsWith(stringToSearch, stringToFind)`

<span data-ttu-id="266ea-372">Determina se una stringa termina con un valore.</span><span class="sxs-lookup"><span data-stu-id="266ea-372">Determines whether a string ends with a value.</span></span> <span data-ttu-id="266ea-373">Il confronto non fa distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="266ea-373">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="266ea-374">Parametri</span><span class="sxs-lookup"><span data-stu-id="266ea-374">Parameters</span></span>

| <span data-ttu-id="266ea-375">Parametro</span><span class="sxs-lookup"><span data-stu-id="266ea-375">Parameter</span></span> | <span data-ttu-id="266ea-376">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="266ea-376">Required</span></span> | <span data-ttu-id="266ea-377">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-377">Type</span></span> | <span data-ttu-id="266ea-378">Descrizione</span><span class="sxs-lookup"><span data-stu-id="266ea-378">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="266ea-379">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="266ea-379">stringToSearch</span></span> |<span data-ttu-id="266ea-380">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-380">Yes</span></span> |<span data-ttu-id="266ea-381">string</span><span class="sxs-lookup"><span data-stu-id="266ea-381">string</span></span> |<span data-ttu-id="266ea-382">Valore che contiene l'elemento da cercare.</span><span class="sxs-lookup"><span data-stu-id="266ea-382">The value that contains the item to find.</span></span> |
| <span data-ttu-id="266ea-383">stringToFind</span><span class="sxs-lookup"><span data-stu-id="266ea-383">stringToFind</span></span> |<span data-ttu-id="266ea-384">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-384">Yes</span></span> |<span data-ttu-id="266ea-385">string</span><span class="sxs-lookup"><span data-stu-id="266ea-385">string</span></span> |<span data-ttu-id="266ea-386">Valore da trovare.</span><span class="sxs-lookup"><span data-stu-id="266ea-386">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="266ea-387">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="266ea-387">Return value</span></span>

<span data-ttu-id="266ea-388">**True** se l'ultimo carattere o i caratteri della stringa corrispondono al valore; in caso contrario, restituisce **False**.</span><span class="sxs-lookup"><span data-stu-id="266ea-388">**True** if the last character or characters of the string match the value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="266ea-389">esempi</span><span class="sxs-lookup"><span data-stu-id="266ea-389">Examples</span></span>

<span data-ttu-id="266ea-390">L'esempio seguente mostra come usare le funzioni startsWith ed endsWith:</span><span class="sxs-lookup"><span data-stu-id="266ea-390">The following example shows how to use the startsWith and endsWith functions:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "startsTrue": {
            "value": "[startsWith('abcdef', 'ab')]",
            "type" : "bool"
        },
        "startsCapTrue": {
            "value": "[startsWith('abcdef', 'A')]",
            "type" : "bool"
        },
        "startsFalse": {
            "value": "[startsWith('abcdef', 'e')]",
            "type" : "bool"
        },
        "endsTrue": {
            "value": "[endsWith('abcdef', 'ef')]",
            "type" : "bool"
        },
        "endsCapTrue": {
            "value": "[endsWith('abcdef', 'F')]",
            "type" : "bool"
        },
        "endsFalse": {
            "value": "[endsWith('abcdef', 'e')]",
            "type" : "bool"
        }
    }
}
```

<span data-ttu-id="266ea-391">L'output dell'esempio precedente con i valori predefiniti è:</span><span class="sxs-lookup"><span data-stu-id="266ea-391">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="266ea-392">Nome</span><span class="sxs-lookup"><span data-stu-id="266ea-392">Name</span></span> | <span data-ttu-id="266ea-393">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-393">Type</span></span> | <span data-ttu-id="266ea-394">Valore</span><span class="sxs-lookup"><span data-stu-id="266ea-394">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="266ea-395">startsTrue</span><span class="sxs-lookup"><span data-stu-id="266ea-395">startsTrue</span></span> | <span data-ttu-id="266ea-396">Booleano</span><span class="sxs-lookup"><span data-stu-id="266ea-396">Bool</span></span> | <span data-ttu-id="266ea-397">True </span><span class="sxs-lookup"><span data-stu-id="266ea-397">True</span></span> |
| <span data-ttu-id="266ea-398">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="266ea-398">startsCapTrue</span></span> | <span data-ttu-id="266ea-399">Booleano</span><span class="sxs-lookup"><span data-stu-id="266ea-399">Bool</span></span> | <span data-ttu-id="266ea-400">True </span><span class="sxs-lookup"><span data-stu-id="266ea-400">True</span></span> |
| <span data-ttu-id="266ea-401">startsFalse</span><span class="sxs-lookup"><span data-stu-id="266ea-401">startsFalse</span></span> | <span data-ttu-id="266ea-402">Booleano</span><span class="sxs-lookup"><span data-stu-id="266ea-402">Bool</span></span> | <span data-ttu-id="266ea-403">False</span><span class="sxs-lookup"><span data-stu-id="266ea-403">False</span></span> |
| <span data-ttu-id="266ea-404">endsTrue</span><span class="sxs-lookup"><span data-stu-id="266ea-404">endsTrue</span></span> | <span data-ttu-id="266ea-405">Booleano</span><span class="sxs-lookup"><span data-stu-id="266ea-405">Bool</span></span> | <span data-ttu-id="266ea-406">True </span><span class="sxs-lookup"><span data-stu-id="266ea-406">True</span></span> |
| <span data-ttu-id="266ea-407">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="266ea-407">endsCapTrue</span></span> | <span data-ttu-id="266ea-408">Booleano</span><span class="sxs-lookup"><span data-stu-id="266ea-408">Bool</span></span> | <span data-ttu-id="266ea-409">True </span><span class="sxs-lookup"><span data-stu-id="266ea-409">True</span></span> |
| <span data-ttu-id="266ea-410">endsFalse</span><span class="sxs-lookup"><span data-stu-id="266ea-410">endsFalse</span></span> | <span data-ttu-id="266ea-411">Booleano</span><span class="sxs-lookup"><span data-stu-id="266ea-411">Bool</span></span> | <span data-ttu-id="266ea-412">False</span><span class="sxs-lookup"><span data-stu-id="266ea-412">False</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="266ea-413">first</span><span class="sxs-lookup"><span data-stu-id="266ea-413">first</span></span>
`first(arg1)`

<span data-ttu-id="266ea-414">Restituisce il primo carattere della stringa o il primo elemento della matrice.</span><span class="sxs-lookup"><span data-stu-id="266ea-414">Returns the first character of the string, or first element of the array.</span></span>

### <a name="parameters"></a><span data-ttu-id="266ea-415">Parametri</span><span class="sxs-lookup"><span data-stu-id="266ea-415">Parameters</span></span>

| <span data-ttu-id="266ea-416">Parametro</span><span class="sxs-lookup"><span data-stu-id="266ea-416">Parameter</span></span> | <span data-ttu-id="266ea-417">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="266ea-417">Required</span></span> | <span data-ttu-id="266ea-418">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-418">Type</span></span> | <span data-ttu-id="266ea-419">Descrizione</span><span class="sxs-lookup"><span data-stu-id="266ea-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="266ea-420">arg1</span><span class="sxs-lookup"><span data-stu-id="266ea-420">arg1</span></span> |<span data-ttu-id="266ea-421">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-421">Yes</span></span> |<span data-ttu-id="266ea-422">stringa o matrice</span><span class="sxs-lookup"><span data-stu-id="266ea-422">array or string</span></span> |<span data-ttu-id="266ea-423">Valore per recuperare il primo elemento o carattere.</span><span class="sxs-lookup"><span data-stu-id="266ea-423">The value to retrieve the first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="266ea-424">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="266ea-424">Return value</span></span>

<span data-ttu-id="266ea-425">Stringa del primo carattere o il tipo del primo elemento in una matrice (stringa, numero intero, matrice o oggetto).</span><span class="sxs-lookup"><span data-stu-id="266ea-425">A string of the first character, or the type (string, int, array, or object) of the first element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="266ea-426">esempi</span><span class="sxs-lookup"><span data-stu-id="266ea-426">Examples</span></span>

<span data-ttu-id="266ea-427">L'esempio seguente mostra come usare la prima funzione con una matrice e una stringa.</span><span class="sxs-lookup"><span data-stu-id="266ea-427">The following example shows how to use the first function with an array and string.</span></span>

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

<span data-ttu-id="266ea-428">L'output dell'esempio precedente con i valori predefiniti è il seguente:</span><span class="sxs-lookup"><span data-stu-id="266ea-428">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="266ea-429">Nome</span><span class="sxs-lookup"><span data-stu-id="266ea-429">Name</span></span> | <span data-ttu-id="266ea-430">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-430">Type</span></span> | <span data-ttu-id="266ea-431">Valore</span><span class="sxs-lookup"><span data-stu-id="266ea-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="266ea-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-432">arrayOutput</span></span> | <span data-ttu-id="266ea-433">String</span><span class="sxs-lookup"><span data-stu-id="266ea-433">String</span></span> | <span data-ttu-id="266ea-434">one</span><span class="sxs-lookup"><span data-stu-id="266ea-434">one</span></span> |
| <span data-ttu-id="266ea-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-435">stringOutput</span></span> | <span data-ttu-id="266ea-436">String</span><span class="sxs-lookup"><span data-stu-id="266ea-436">String</span></span> | <span data-ttu-id="266ea-437">O</span><span class="sxs-lookup"><span data-stu-id="266ea-437">O</span></span> |

<a id="indexof" />

## <a name="indexof"></a><span data-ttu-id="266ea-438">indexOf</span><span class="sxs-lookup"><span data-stu-id="266ea-438">indexOf</span></span>
`indexOf(stringToSearch, stringToFind)`

<span data-ttu-id="266ea-439">Restituisce la prima posizione di un valore all'interno di una stringa.</span><span class="sxs-lookup"><span data-stu-id="266ea-439">Returns the first position of a value within a string.</span></span> <span data-ttu-id="266ea-440">Il confronto non fa distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="266ea-440">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="266ea-441">Parametri</span><span class="sxs-lookup"><span data-stu-id="266ea-441">Parameters</span></span>

| <span data-ttu-id="266ea-442">Parametro</span><span class="sxs-lookup"><span data-stu-id="266ea-442">Parameter</span></span> | <span data-ttu-id="266ea-443">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="266ea-443">Required</span></span> | <span data-ttu-id="266ea-444">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-444">Type</span></span> | <span data-ttu-id="266ea-445">Descrizione</span><span class="sxs-lookup"><span data-stu-id="266ea-445">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="266ea-446">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="266ea-446">stringToSearch</span></span> |<span data-ttu-id="266ea-447">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-447">Yes</span></span> |<span data-ttu-id="266ea-448">string</span><span class="sxs-lookup"><span data-stu-id="266ea-448">string</span></span> |<span data-ttu-id="266ea-449">Valore che contiene l'elemento da cercare.</span><span class="sxs-lookup"><span data-stu-id="266ea-449">The value that contains the item to find.</span></span> |
| <span data-ttu-id="266ea-450">stringToFind</span><span class="sxs-lookup"><span data-stu-id="266ea-450">stringToFind</span></span> |<span data-ttu-id="266ea-451">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-451">Yes</span></span> |<span data-ttu-id="266ea-452">string</span><span class="sxs-lookup"><span data-stu-id="266ea-452">string</span></span> |<span data-ttu-id="266ea-453">Valore da trovare.</span><span class="sxs-lookup"><span data-stu-id="266ea-453">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="266ea-454">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="266ea-454">Return value</span></span>

<span data-ttu-id="266ea-455">Numero intero che rappresenta la posizione dell'elemento da trovare.</span><span class="sxs-lookup"><span data-stu-id="266ea-455">An integer that represents the position of the item to find.</span></span> <span data-ttu-id="266ea-456">Il valore è in base zero.</span><span class="sxs-lookup"><span data-stu-id="266ea-456">The value is zero-based.</span></span> <span data-ttu-id="266ea-457">Se l'elemento non viene trovato, viene restituito -1.</span><span class="sxs-lookup"><span data-stu-id="266ea-457">If the item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="266ea-458">esempi</span><span class="sxs-lookup"><span data-stu-id="266ea-458">Examples</span></span>

<span data-ttu-id="266ea-459">L'esempio seguente mostra come usare le funzioni indexOf e lastIndexOf:</span><span class="sxs-lookup"><span data-stu-id="266ea-459">The following example shows how to use the indexOf and lastIndexOf functions:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "firstT": {
            "value": "[indexOf('test', 't')]",
            "type" : "int"
        },
        "lastT": {
            "value": "[lastIndexOf('test', 't')]",
            "type" : "int"
        },
        "firstString": {
            "value": "[indexOf('abcdef', 'CD')]",
            "type" : "int"
        },
        "lastString": {
            "value": "[lastIndexOf('abcdef', 'AB')]",
            "type" : "int"
        },
        "notFound": {
            "value": "[indexOf('abcdef', 'z')]",
            "type" : "int"
        }
    }
}
```

<span data-ttu-id="266ea-460">L'output dell'esempio precedente con i valori predefiniti è:</span><span class="sxs-lookup"><span data-stu-id="266ea-460">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="266ea-461">Nome</span><span class="sxs-lookup"><span data-stu-id="266ea-461">Name</span></span> | <span data-ttu-id="266ea-462">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-462">Type</span></span> | <span data-ttu-id="266ea-463">Valore</span><span class="sxs-lookup"><span data-stu-id="266ea-463">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="266ea-464">firstT</span><span class="sxs-lookup"><span data-stu-id="266ea-464">firstT</span></span> | <span data-ttu-id="266ea-465">int</span><span class="sxs-lookup"><span data-stu-id="266ea-465">Int</span></span> | <span data-ttu-id="266ea-466">0</span><span class="sxs-lookup"><span data-stu-id="266ea-466">0</span></span> |
| <span data-ttu-id="266ea-467">lastT</span><span class="sxs-lookup"><span data-stu-id="266ea-467">lastT</span></span> | <span data-ttu-id="266ea-468">int</span><span class="sxs-lookup"><span data-stu-id="266ea-468">Int</span></span> | <span data-ttu-id="266ea-469">3</span><span class="sxs-lookup"><span data-stu-id="266ea-469">3</span></span> |
| <span data-ttu-id="266ea-470">firstString</span><span class="sxs-lookup"><span data-stu-id="266ea-470">firstString</span></span> | <span data-ttu-id="266ea-471">int</span><span class="sxs-lookup"><span data-stu-id="266ea-471">Int</span></span> | <span data-ttu-id="266ea-472">2</span><span class="sxs-lookup"><span data-stu-id="266ea-472">2</span></span> |
| <span data-ttu-id="266ea-473">lastString</span><span class="sxs-lookup"><span data-stu-id="266ea-473">lastString</span></span> | <span data-ttu-id="266ea-474">int</span><span class="sxs-lookup"><span data-stu-id="266ea-474">Int</span></span> | <span data-ttu-id="266ea-475">0</span><span class="sxs-lookup"><span data-stu-id="266ea-475">0</span></span> |
| <span data-ttu-id="266ea-476">notFound</span><span class="sxs-lookup"><span data-stu-id="266ea-476">notFound</span></span> | <span data-ttu-id="266ea-477">int</span><span class="sxs-lookup"><span data-stu-id="266ea-477">Int</span></span> | <span data-ttu-id="266ea-478">-1</span><span class="sxs-lookup"><span data-stu-id="266ea-478">-1</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="266ea-479">last</span><span class="sxs-lookup"><span data-stu-id="266ea-479">last</span></span>
`last (arg1)`

<span data-ttu-id="266ea-480">Restituisce il primo carattere della stringa o l'ultimo elemento della matrice.</span><span class="sxs-lookup"><span data-stu-id="266ea-480">Returns last character of the string, or the last element of the array.</span></span>

### <a name="parameters"></a><span data-ttu-id="266ea-481">Parametri</span><span class="sxs-lookup"><span data-stu-id="266ea-481">Parameters</span></span>

| <span data-ttu-id="266ea-482">Parametro</span><span class="sxs-lookup"><span data-stu-id="266ea-482">Parameter</span></span> | <span data-ttu-id="266ea-483">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="266ea-483">Required</span></span> | <span data-ttu-id="266ea-484">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-484">Type</span></span> | <span data-ttu-id="266ea-485">Descrizione</span><span class="sxs-lookup"><span data-stu-id="266ea-485">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="266ea-486">arg1</span><span class="sxs-lookup"><span data-stu-id="266ea-486">arg1</span></span> |<span data-ttu-id="266ea-487">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-487">Yes</span></span> |<span data-ttu-id="266ea-488">stringa o matrice</span><span class="sxs-lookup"><span data-stu-id="266ea-488">array or string</span></span> |<span data-ttu-id="266ea-489">Valore per recuperare l'ultimo elemento o carattere.</span><span class="sxs-lookup"><span data-stu-id="266ea-489">The value to retrieve the last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="266ea-490">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="266ea-490">Return value</span></span>

<span data-ttu-id="266ea-491">Stringa dell'ultimo carattere o il tipo dell'ultimo elemento in una matrice (stringa, numero intero, matrice o oggetto).</span><span class="sxs-lookup"><span data-stu-id="266ea-491">A string of the last character, or the type (string, int, array, or object) of the last element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="266ea-492">esempi</span><span class="sxs-lookup"><span data-stu-id="266ea-492">Examples</span></span>

<span data-ttu-id="266ea-493">L'esempio seguente mostra come usare l'ultima funzione con una matrice e una stringa.</span><span class="sxs-lookup"><span data-stu-id="266ea-493">The following example shows how to use the last function with an array and string.</span></span>

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

<span data-ttu-id="266ea-494">L'output dell'esempio precedente con i valori predefiniti è il seguente:</span><span class="sxs-lookup"><span data-stu-id="266ea-494">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="266ea-495">Nome</span><span class="sxs-lookup"><span data-stu-id="266ea-495">Name</span></span> | <span data-ttu-id="266ea-496">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-496">Type</span></span> | <span data-ttu-id="266ea-497">Valore</span><span class="sxs-lookup"><span data-stu-id="266ea-497">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="266ea-498">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-498">arrayOutput</span></span> | <span data-ttu-id="266ea-499">String</span><span class="sxs-lookup"><span data-stu-id="266ea-499">String</span></span> | <span data-ttu-id="266ea-500">three</span><span class="sxs-lookup"><span data-stu-id="266ea-500">three</span></span> |
| <span data-ttu-id="266ea-501">stringOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-501">stringOutput</span></span> | <span data-ttu-id="266ea-502">String</span><span class="sxs-lookup"><span data-stu-id="266ea-502">String</span></span> | <span data-ttu-id="266ea-503">e</span><span class="sxs-lookup"><span data-stu-id="266ea-503">e</span></span> |

<a id="lastindexof" />

## <a name="lastindexof"></a><span data-ttu-id="266ea-504">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="266ea-504">lastIndexOf</span></span>
`lastIndexOf(stringToSearch, stringToFind)`

<span data-ttu-id="266ea-505">Restituisce l'ultima posizione di un valore all'interno di una stringa.</span><span class="sxs-lookup"><span data-stu-id="266ea-505">Returns the last position of a value within a string.</span></span> <span data-ttu-id="266ea-506">Il confronto non fa distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="266ea-506">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="266ea-507">Parametri</span><span class="sxs-lookup"><span data-stu-id="266ea-507">Parameters</span></span>

| <span data-ttu-id="266ea-508">Parametro</span><span class="sxs-lookup"><span data-stu-id="266ea-508">Parameter</span></span> | <span data-ttu-id="266ea-509">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="266ea-509">Required</span></span> | <span data-ttu-id="266ea-510">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-510">Type</span></span> | <span data-ttu-id="266ea-511">Descrizione</span><span class="sxs-lookup"><span data-stu-id="266ea-511">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="266ea-512">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="266ea-512">stringToSearch</span></span> |<span data-ttu-id="266ea-513">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-513">Yes</span></span> |<span data-ttu-id="266ea-514">string</span><span class="sxs-lookup"><span data-stu-id="266ea-514">string</span></span> |<span data-ttu-id="266ea-515">Valore che contiene l'elemento da cercare.</span><span class="sxs-lookup"><span data-stu-id="266ea-515">The value that contains the item to find.</span></span> |
| <span data-ttu-id="266ea-516">stringToFind</span><span class="sxs-lookup"><span data-stu-id="266ea-516">stringToFind</span></span> |<span data-ttu-id="266ea-517">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-517">Yes</span></span> |<span data-ttu-id="266ea-518">string</span><span class="sxs-lookup"><span data-stu-id="266ea-518">string</span></span> |<span data-ttu-id="266ea-519">Valore da trovare.</span><span class="sxs-lookup"><span data-stu-id="266ea-519">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="266ea-520">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="266ea-520">Return value</span></span>

<span data-ttu-id="266ea-521">Numero intero che rappresenta l'ultima posizione dell'elemento da trovare.</span><span class="sxs-lookup"><span data-stu-id="266ea-521">An integer that represents the last position of the item to find.</span></span> <span data-ttu-id="266ea-522">Il valore è in base zero.</span><span class="sxs-lookup"><span data-stu-id="266ea-522">The value is zero-based.</span></span> <span data-ttu-id="266ea-523">Se l'elemento non viene trovato, viene restituito -1.</span><span class="sxs-lookup"><span data-stu-id="266ea-523">If the item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="266ea-524">esempi</span><span class="sxs-lookup"><span data-stu-id="266ea-524">Examples</span></span>

<span data-ttu-id="266ea-525">L'esempio seguente mostra come usare le funzioni indexOf e lastIndexOf:</span><span class="sxs-lookup"><span data-stu-id="266ea-525">The following example shows how to use the indexOf and lastIndexOf functions:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "firstT": {
            "value": "[indexOf('test', 't')]",
            "type" : "int"
        },
        "lastT": {
            "value": "[lastIndexOf('test', 't')]",
            "type" : "int"
        },
        "firstString": {
            "value": "[indexOf('abcdef', 'CD')]",
            "type" : "int"
        },
        "lastString": {
            "value": "[lastIndexOf('abcdef', 'AB')]",
            "type" : "int"
        },
        "notFound": {
            "value": "[indexOf('abcdef', 'z')]",
            "type" : "int"
        }
    }
}
```

<span data-ttu-id="266ea-526">L'output dell'esempio precedente con i valori predefiniti è:</span><span class="sxs-lookup"><span data-stu-id="266ea-526">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="266ea-527">Nome</span><span class="sxs-lookup"><span data-stu-id="266ea-527">Name</span></span> | <span data-ttu-id="266ea-528">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-528">Type</span></span> | <span data-ttu-id="266ea-529">Valore</span><span class="sxs-lookup"><span data-stu-id="266ea-529">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="266ea-530">firstT</span><span class="sxs-lookup"><span data-stu-id="266ea-530">firstT</span></span> | <span data-ttu-id="266ea-531">int</span><span class="sxs-lookup"><span data-stu-id="266ea-531">Int</span></span> | <span data-ttu-id="266ea-532">0</span><span class="sxs-lookup"><span data-stu-id="266ea-532">0</span></span> |
| <span data-ttu-id="266ea-533">lastT</span><span class="sxs-lookup"><span data-stu-id="266ea-533">lastT</span></span> | <span data-ttu-id="266ea-534">int</span><span class="sxs-lookup"><span data-stu-id="266ea-534">Int</span></span> | <span data-ttu-id="266ea-535">3</span><span class="sxs-lookup"><span data-stu-id="266ea-535">3</span></span> |
| <span data-ttu-id="266ea-536">firstString</span><span class="sxs-lookup"><span data-stu-id="266ea-536">firstString</span></span> | <span data-ttu-id="266ea-537">int</span><span class="sxs-lookup"><span data-stu-id="266ea-537">Int</span></span> | <span data-ttu-id="266ea-538">2</span><span class="sxs-lookup"><span data-stu-id="266ea-538">2</span></span> |
| <span data-ttu-id="266ea-539">lastString</span><span class="sxs-lookup"><span data-stu-id="266ea-539">lastString</span></span> | <span data-ttu-id="266ea-540">int</span><span class="sxs-lookup"><span data-stu-id="266ea-540">Int</span></span> | <span data-ttu-id="266ea-541">0</span><span class="sxs-lookup"><span data-stu-id="266ea-541">0</span></span> |
| <span data-ttu-id="266ea-542">notFound</span><span class="sxs-lookup"><span data-stu-id="266ea-542">notFound</span></span> | <span data-ttu-id="266ea-543">int</span><span class="sxs-lookup"><span data-stu-id="266ea-543">Int</span></span> | <span data-ttu-id="266ea-544">-1</span><span class="sxs-lookup"><span data-stu-id="266ea-544">-1</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="266ea-545">length</span><span class="sxs-lookup"><span data-stu-id="266ea-545">length</span></span>
`length(string)`

<span data-ttu-id="266ea-546">Restituisce il numero di caratteri in una stringa o di elementi in una matrice.</span><span class="sxs-lookup"><span data-stu-id="266ea-546">Returns the number of characters in a string, or elements in an array.</span></span>

### <a name="parameters"></a><span data-ttu-id="266ea-547">Parametri</span><span class="sxs-lookup"><span data-stu-id="266ea-547">Parameters</span></span>

| <span data-ttu-id="266ea-548">Parametro</span><span class="sxs-lookup"><span data-stu-id="266ea-548">Parameter</span></span> | <span data-ttu-id="266ea-549">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="266ea-549">Required</span></span> | <span data-ttu-id="266ea-550">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-550">Type</span></span> | <span data-ttu-id="266ea-551">Descrizione</span><span class="sxs-lookup"><span data-stu-id="266ea-551">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="266ea-552">arg1</span><span class="sxs-lookup"><span data-stu-id="266ea-552">arg1</span></span> |<span data-ttu-id="266ea-553">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-553">Yes</span></span> |<span data-ttu-id="266ea-554">stringa o matrice</span><span class="sxs-lookup"><span data-stu-id="266ea-554">array or string</span></span> |<span data-ttu-id="266ea-555">Matrice da usare per ottenere il numero di elementi oppure stringa da usare per ottenere il numero di caratteri.</span><span class="sxs-lookup"><span data-stu-id="266ea-555">The array to use for getting the number of elements, or the string to use for getting the number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="266ea-556">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="266ea-556">Return value</span></span>

<span data-ttu-id="266ea-557">Numero intero</span><span class="sxs-lookup"><span data-stu-id="266ea-557">An int.</span></span> 

### <a name="examples"></a><span data-ttu-id="266ea-558">esempi</span><span class="sxs-lookup"><span data-stu-id="266ea-558">Examples</span></span>

<span data-ttu-id="266ea-559">L'esempio seguente mostra come usare la funzione length con una matrice e una stringa:</span><span class="sxs-lookup"><span data-stu-id="266ea-559">The following example shows how to use length with an array and string:</span></span>

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

<span data-ttu-id="266ea-560">L'output dell'esempio precedente con i valori predefiniti è il seguente:</span><span class="sxs-lookup"><span data-stu-id="266ea-560">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="266ea-561">Nome</span><span class="sxs-lookup"><span data-stu-id="266ea-561">Name</span></span> | <span data-ttu-id="266ea-562">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-562">Type</span></span> | <span data-ttu-id="266ea-563">Valore</span><span class="sxs-lookup"><span data-stu-id="266ea-563">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="266ea-564">arrayLength</span><span class="sxs-lookup"><span data-stu-id="266ea-564">arrayLength</span></span> | <span data-ttu-id="266ea-565">int</span><span class="sxs-lookup"><span data-stu-id="266ea-565">Int</span></span> | <span data-ttu-id="266ea-566">3</span><span class="sxs-lookup"><span data-stu-id="266ea-566">3</span></span> |
| <span data-ttu-id="266ea-567">stringLength</span><span class="sxs-lookup"><span data-stu-id="266ea-567">stringLength</span></span> | <span data-ttu-id="266ea-568">int</span><span class="sxs-lookup"><span data-stu-id="266ea-568">Int</span></span> | <span data-ttu-id="266ea-569">13</span><span class="sxs-lookup"><span data-stu-id="266ea-569">13</span></span> |

<a id="padleft" />

## <a name="padleft"></a><span data-ttu-id="266ea-570">padLeft</span><span class="sxs-lookup"><span data-stu-id="266ea-570">padLeft</span></span>
`padLeft(valueToPad, totalLength, paddingCharacter)`

<span data-ttu-id="266ea-571">Restituisce una stringa allineata a destra mediante l'aggiunta di caratteri a sinistra, fino a raggiungere la lunghezza totale specificata.</span><span class="sxs-lookup"><span data-stu-id="266ea-571">Returns a right-aligned string by adding characters to the left until reaching the total specified length.</span></span>

### <a name="parameters"></a><span data-ttu-id="266ea-572">Parametri</span><span class="sxs-lookup"><span data-stu-id="266ea-572">Parameters</span></span>

| <span data-ttu-id="266ea-573">Parametro</span><span class="sxs-lookup"><span data-stu-id="266ea-573">Parameter</span></span> | <span data-ttu-id="266ea-574">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="266ea-574">Required</span></span> | <span data-ttu-id="266ea-575">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-575">Type</span></span> | <span data-ttu-id="266ea-576">Descrizione</span><span class="sxs-lookup"><span data-stu-id="266ea-576">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="266ea-577">valueToPad</span><span class="sxs-lookup"><span data-stu-id="266ea-577">valueToPad</span></span> |<span data-ttu-id="266ea-578">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-578">Yes</span></span> |<span data-ttu-id="266ea-579">Stringa o numero intero</span><span class="sxs-lookup"><span data-stu-id="266ea-579">string or int</span></span> |<span data-ttu-id="266ea-580">Il valore per eseguire l'allineamento a destra.</span><span class="sxs-lookup"><span data-stu-id="266ea-580">The value to right-align.</span></span> |
| <span data-ttu-id="266ea-581">totalLength</span><span class="sxs-lookup"><span data-stu-id="266ea-581">totalLength</span></span> |<span data-ttu-id="266ea-582">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-582">Yes</span></span> |<span data-ttu-id="266ea-583">int</span><span class="sxs-lookup"><span data-stu-id="266ea-583">int</span></span> |<span data-ttu-id="266ea-584">Numero totale di caratteri della stringa restituita.</span><span class="sxs-lookup"><span data-stu-id="266ea-584">The total number of characters in the returned string.</span></span> |
| <span data-ttu-id="266ea-585">paddingCharacter</span><span class="sxs-lookup"><span data-stu-id="266ea-585">paddingCharacter</span></span> |<span data-ttu-id="266ea-586">No</span><span class="sxs-lookup"><span data-stu-id="266ea-586">No</span></span> |<span data-ttu-id="266ea-587">Carattere singolo</span><span class="sxs-lookup"><span data-stu-id="266ea-587">single character</span></span> |<span data-ttu-id="266ea-588">Il carattere da utilizzare per la spaziatura interna a sinistra, fino a raggiungere la lunghezza totale.</span><span class="sxs-lookup"><span data-stu-id="266ea-588">The character to use for left-padding until the total length is reached.</span></span> <span data-ttu-id="266ea-589">Il valore predefinito è uno spazio.</span><span class="sxs-lookup"><span data-stu-id="266ea-589">The default value is a space.</span></span> |

<span data-ttu-id="266ea-590">Se la stringa originale è più lunga rispetto al numero di caratteri di riempimento, non vengono aggiunti caratteri.</span><span class="sxs-lookup"><span data-stu-id="266ea-590">If the original string is longer than the number of characters to pad, no characters are added.</span></span>

### <a name="return-value"></a><span data-ttu-id="266ea-591">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="266ea-591">Return value</span></span>

<span data-ttu-id="266ea-592">Stringa contenente come minimo il numero di caratteri specificati.</span><span class="sxs-lookup"><span data-stu-id="266ea-592">A string with at least the number of specified characters.</span></span>

### <a name="examples"></a><span data-ttu-id="266ea-593">esempi</span><span class="sxs-lookup"><span data-stu-id="266ea-593">Examples</span></span>

<span data-ttu-id="266ea-594">L'esempio seguente mostra come il valore del parametro fornito dall'utente viene completato aggiungendo il carattere zero finché la stringa non raggiunge il numero totale di caratteri.</span><span class="sxs-lookup"><span data-stu-id="266ea-594">The following example shows how to pad the user-provided parameter value by adding the zero character until it reaches the total number of characters.</span></span> 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "123"
        }
    },
    "resources": [],
    "outputs": {
        "stringOutput": {
            "type": "string",
            "value": "[padLeft(parameters('testString'),10,'0')]"
        }
    }
}
```

<span data-ttu-id="266ea-595">L'output dell'esempio precedente con i valori predefiniti è:</span><span class="sxs-lookup"><span data-stu-id="266ea-595">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="266ea-596">Nome</span><span class="sxs-lookup"><span data-stu-id="266ea-596">Name</span></span> | <span data-ttu-id="266ea-597">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-597">Type</span></span> | <span data-ttu-id="266ea-598">Valore</span><span class="sxs-lookup"><span data-stu-id="266ea-598">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="266ea-599">stringOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-599">stringOutput</span></span> | <span data-ttu-id="266ea-600">String</span><span class="sxs-lookup"><span data-stu-id="266ea-600">String</span></span> | <span data-ttu-id="266ea-601">0000000123</span><span class="sxs-lookup"><span data-stu-id="266ea-601">0000000123</span></span> |

<a id="replace" />

## <a name="replace"></a><span data-ttu-id="266ea-602">replace</span><span class="sxs-lookup"><span data-stu-id="266ea-602">replace</span></span>
`replace(originalString, oldString, newString)`

<span data-ttu-id="266ea-603">Restituisce una nuova stringa con tutte le istanze di una stringa sostituita con un'altra stringa.</span><span class="sxs-lookup"><span data-stu-id="266ea-603">Returns a new string with all instances of one string replaced by another string.</span></span>

### <a name="parameters"></a><span data-ttu-id="266ea-604">Parametri</span><span class="sxs-lookup"><span data-stu-id="266ea-604">Parameters</span></span>

| <span data-ttu-id="266ea-605">Parametro</span><span class="sxs-lookup"><span data-stu-id="266ea-605">Parameter</span></span> | <span data-ttu-id="266ea-606">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="266ea-606">Required</span></span> | <span data-ttu-id="266ea-607">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-607">Type</span></span> | <span data-ttu-id="266ea-608">Descrizione</span><span class="sxs-lookup"><span data-stu-id="266ea-608">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="266ea-609">originalString</span><span class="sxs-lookup"><span data-stu-id="266ea-609">originalString</span></span> |<span data-ttu-id="266ea-610">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-610">Yes</span></span> |<span data-ttu-id="266ea-611">string</span><span class="sxs-lookup"><span data-stu-id="266ea-611">string</span></span> |<span data-ttu-id="266ea-612">Valore che contiene tutte le istanze di una stringa sostituita con un'altra stringa.</span><span class="sxs-lookup"><span data-stu-id="266ea-612">The value that has all instances of one string replaced by another string.</span></span> |
| <span data-ttu-id="266ea-613">oldString</span><span class="sxs-lookup"><span data-stu-id="266ea-613">oldString</span></span> |<span data-ttu-id="266ea-614">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-614">Yes</span></span> |<span data-ttu-id="266ea-615">string</span><span class="sxs-lookup"><span data-stu-id="266ea-615">string</span></span> |<span data-ttu-id="266ea-616">Stringa da rimuovere dalla stringa originale.</span><span class="sxs-lookup"><span data-stu-id="266ea-616">The string to be removed from the original string.</span></span> |
| <span data-ttu-id="266ea-617">newString</span><span class="sxs-lookup"><span data-stu-id="266ea-617">newString</span></span> |<span data-ttu-id="266ea-618">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-618">Yes</span></span> |<span data-ttu-id="266ea-619">string</span><span class="sxs-lookup"><span data-stu-id="266ea-619">string</span></span> |<span data-ttu-id="266ea-620">Stringa da aggiungere al posto della stringa rimossa.</span><span class="sxs-lookup"><span data-stu-id="266ea-620">The string to add in place of the removed string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="266ea-621">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="266ea-621">Return value</span></span>

<span data-ttu-id="266ea-622">Stringa con i caratteri sostituiti.</span><span class="sxs-lookup"><span data-stu-id="266ea-622">A string with the replaced characters.</span></span>

### <a name="examples"></a><span data-ttu-id="266ea-623">esempi</span><span class="sxs-lookup"><span data-stu-id="266ea-623">Examples</span></span>

<span data-ttu-id="266ea-624">L'esempio seguente illustra come rimuovere tutti i trattini dalla stringa fornita dall'utente e come sostituire parte della stringa con un'altra stringa.</span><span class="sxs-lookup"><span data-stu-id="266ea-624">The following example shows how to remove all dashes from the user-provided string, and how to replace part of the string with another string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "123-123-1234"
        }
    },
    "resources": [],
    "outputs": {
        "firstOutput": {
            "type": "string",
            "value": "[replace(parameters('testString'),'-', '')]"
        },
        "secodeOutput": {
            "type": "string",
            "value": "[replace(parameters('testString'),'1234', 'xxxx')]"
        }
    }
}
```

<span data-ttu-id="266ea-625">L'output dell'esempio precedente con i valori predefiniti è:</span><span class="sxs-lookup"><span data-stu-id="266ea-625">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="266ea-626">Nome</span><span class="sxs-lookup"><span data-stu-id="266ea-626">Name</span></span> | <span data-ttu-id="266ea-627">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-627">Type</span></span> | <span data-ttu-id="266ea-628">Valore</span><span class="sxs-lookup"><span data-stu-id="266ea-628">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="266ea-629">firstOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-629">firstOutput</span></span> | <span data-ttu-id="266ea-630">String</span><span class="sxs-lookup"><span data-stu-id="266ea-630">String</span></span> | <span data-ttu-id="266ea-631">1231231234</span><span class="sxs-lookup"><span data-stu-id="266ea-631">1231231234</span></span> |
| <span data-ttu-id="266ea-632">secodeOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-632">secodeOutput</span></span> | <span data-ttu-id="266ea-633">String</span><span class="sxs-lookup"><span data-stu-id="266ea-633">String</span></span> | <span data-ttu-id="266ea-634">123-123-xxxx</span><span class="sxs-lookup"><span data-stu-id="266ea-634">123-123-xxxx</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="266ea-635">skip</span><span class="sxs-lookup"><span data-stu-id="266ea-635">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="266ea-636">Restituisce una stringa con tutti i caratteri dopo il numero specificato di caratteri o una matrice con tutti gli elementi dopo il numero specificato di elementi.</span><span class="sxs-lookup"><span data-stu-id="266ea-636">Returns a string with all the characters after the specified number of characters, or an array with all the elements after the specified number of elements.</span></span>

### <a name="parameters"></a><span data-ttu-id="266ea-637">Parametri</span><span class="sxs-lookup"><span data-stu-id="266ea-637">Parameters</span></span>

| <span data-ttu-id="266ea-638">Parametro</span><span class="sxs-lookup"><span data-stu-id="266ea-638">Parameter</span></span> | <span data-ttu-id="266ea-639">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="266ea-639">Required</span></span> | <span data-ttu-id="266ea-640">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-640">Type</span></span> | <span data-ttu-id="266ea-641">Descrizione</span><span class="sxs-lookup"><span data-stu-id="266ea-641">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="266ea-642">originalValue</span><span class="sxs-lookup"><span data-stu-id="266ea-642">originalValue</span></span> |<span data-ttu-id="266ea-643">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-643">Yes</span></span> |<span data-ttu-id="266ea-644">stringa o matrice</span><span class="sxs-lookup"><span data-stu-id="266ea-644">array or string</span></span> |<span data-ttu-id="266ea-645">Stringa o matrice da usare per i valori da ignorare.</span><span class="sxs-lookup"><span data-stu-id="266ea-645">The array or string to use for skipping.</span></span> |
| <span data-ttu-id="266ea-646">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="266ea-646">numberToSkip</span></span> |<span data-ttu-id="266ea-647">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-647">Yes</span></span> |<span data-ttu-id="266ea-648">int</span><span class="sxs-lookup"><span data-stu-id="266ea-648">int</span></span> |<span data-ttu-id="266ea-649">Numero di elementi o caratteri da ignorare.</span><span class="sxs-lookup"><span data-stu-id="266ea-649">The number of elements or characters to skip.</span></span> <span data-ttu-id="266ea-650">Se il valore è minore o uguale a 0, vengono restituiti tutti gli elementi o i caratteri nel valore.</span><span class="sxs-lookup"><span data-stu-id="266ea-650">If this value is 0 or less, all the elements or characters in the value are returned.</span></span> <span data-ttu-id="266ea-651">Se il valore è maggiore della lunghezza della stringa o della matrice, viene restituita una stringa o una matrice vuota.</span><span class="sxs-lookup"><span data-stu-id="266ea-651">If it is larger than the length of the array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="266ea-652">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="266ea-652">Return value</span></span>

<span data-ttu-id="266ea-653">Stringa o matrice.</span><span class="sxs-lookup"><span data-stu-id="266ea-653">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="266ea-654">esempi</span><span class="sxs-lookup"><span data-stu-id="266ea-654">Examples</span></span>

<span data-ttu-id="266ea-655">L'esempio seguente ignora il numero di elementi specificato nella matrice e il numero di caratteri specificato in una stringa.</span><span class="sxs-lookup"><span data-stu-id="266ea-655">The following example skips the specified number of elements in the array, and the specified number of characters in a string.</span></span>

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

<span data-ttu-id="266ea-656">L'output dell'esempio precedente con i valori predefiniti è il seguente:</span><span class="sxs-lookup"><span data-stu-id="266ea-656">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="266ea-657">Nome</span><span class="sxs-lookup"><span data-stu-id="266ea-657">Name</span></span> | <span data-ttu-id="266ea-658">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-658">Type</span></span> | <span data-ttu-id="266ea-659">Valore</span><span class="sxs-lookup"><span data-stu-id="266ea-659">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="266ea-660">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-660">arrayOutput</span></span> | <span data-ttu-id="266ea-661">Array</span><span class="sxs-lookup"><span data-stu-id="266ea-661">Array</span></span> | <span data-ttu-id="266ea-662">["three"]</span><span class="sxs-lookup"><span data-stu-id="266ea-662">["three"]</span></span> |
| <span data-ttu-id="266ea-663">stringOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-663">stringOutput</span></span> | <span data-ttu-id="266ea-664">String</span><span class="sxs-lookup"><span data-stu-id="266ea-664">String</span></span> | <span data-ttu-id="266ea-665">two three</span><span class="sxs-lookup"><span data-stu-id="266ea-665">two three</span></span> |

<a id="split" />

## <a name="split"></a><span data-ttu-id="266ea-666">split</span><span class="sxs-lookup"><span data-stu-id="266ea-666">split</span></span>
`split(inputString, delimiter)`

<span data-ttu-id="266ea-667">Restituisce una matrice di stringhe che contiene le sottostringhe della stringa di input delimitate dai delimitatori specificati.</span><span class="sxs-lookup"><span data-stu-id="266ea-667">Returns an array of strings that contains the substrings of the input string that are delimited by the specified delimiters.</span></span>

### <a name="parameters"></a><span data-ttu-id="266ea-668">Parametri</span><span class="sxs-lookup"><span data-stu-id="266ea-668">Parameters</span></span>

| <span data-ttu-id="266ea-669">Parametro</span><span class="sxs-lookup"><span data-stu-id="266ea-669">Parameter</span></span> | <span data-ttu-id="266ea-670">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="266ea-670">Required</span></span> | <span data-ttu-id="266ea-671">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-671">Type</span></span> | <span data-ttu-id="266ea-672">Descrizione</span><span class="sxs-lookup"><span data-stu-id="266ea-672">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="266ea-673">inputString</span><span class="sxs-lookup"><span data-stu-id="266ea-673">inputString</span></span> |<span data-ttu-id="266ea-674">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-674">Yes</span></span> |<span data-ttu-id="266ea-675">string</span><span class="sxs-lookup"><span data-stu-id="266ea-675">string</span></span> |<span data-ttu-id="266ea-676">Stringa da dividere.</span><span class="sxs-lookup"><span data-stu-id="266ea-676">The string to split.</span></span> |
| <span data-ttu-id="266ea-677">delimiter</span><span class="sxs-lookup"><span data-stu-id="266ea-677">delimiter</span></span> |<span data-ttu-id="266ea-678">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-678">Yes</span></span> |<span data-ttu-id="266ea-679">Stringa o matrice di stringhe</span><span class="sxs-lookup"><span data-stu-id="266ea-679">string or array of strings</span></span> |<span data-ttu-id="266ea-680">Il delimitatore da usare per dividere la stringa.</span><span class="sxs-lookup"><span data-stu-id="266ea-680">The delimiter to use for splitting the string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="266ea-681">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="266ea-681">Return value</span></span>

<span data-ttu-id="266ea-682">Matrice di stringhe.</span><span class="sxs-lookup"><span data-stu-id="266ea-682">An array of strings.</span></span>

### <a name="examples"></a><span data-ttu-id="266ea-683">esempi</span><span class="sxs-lookup"><span data-stu-id="266ea-683">Examples</span></span>

<span data-ttu-id="266ea-684">L'esempio seguente mostra come suddividere la stringa di input usando una virgola, oppure una virgola o un punto e virgola.</span><span class="sxs-lookup"><span data-stu-id="266ea-684">The following example splits the input string with a comma, and with either a comma or a semi-colon.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstString": {
            "type": "string",
            "defaultValue": "one,two,three"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "one;two,three"
        }
    },
    "variables": {
        "delimiters": [ ",", ";" ]
    },
    "resources": [],
    "outputs": {
        "firstOutput": {
            "type": "array",
            "value": "[split(parameters('firstString'),',')]"
        },
        "secondOutput": {
            "type": "array",
            "value": "[split(parameters('secondString'),variables('delimiters'))]"
        }
    }
}
```

<span data-ttu-id="266ea-685">L'output dell'esempio precedente con i valori predefiniti è:</span><span class="sxs-lookup"><span data-stu-id="266ea-685">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="266ea-686">Nome</span><span class="sxs-lookup"><span data-stu-id="266ea-686">Name</span></span> | <span data-ttu-id="266ea-687">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-687">Type</span></span> | <span data-ttu-id="266ea-688">Valore</span><span class="sxs-lookup"><span data-stu-id="266ea-688">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="266ea-689">firstOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-689">firstOutput</span></span> | <span data-ttu-id="266ea-690">Array</span><span class="sxs-lookup"><span data-stu-id="266ea-690">Array</span></span> | <span data-ttu-id="266ea-691">["one", "two", "three"]</span><span class="sxs-lookup"><span data-stu-id="266ea-691">["one", "two", "three"]</span></span> |
| <span data-ttu-id="266ea-692">secondOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-692">secondOutput</span></span> | <span data-ttu-id="266ea-693">Array</span><span class="sxs-lookup"><span data-stu-id="266ea-693">Array</span></span> | <span data-ttu-id="266ea-694">["one", "two", "three"]</span><span class="sxs-lookup"><span data-stu-id="266ea-694">["one", "two", "three"]</span></span> |

<a id="startswith" />

## <a name="startswith"></a><span data-ttu-id="266ea-695">startsWith</span><span class="sxs-lookup"><span data-stu-id="266ea-695">startsWith</span></span>
`startsWith(stringToSearch, stringToFind)`

<span data-ttu-id="266ea-696">Determina se una stringa inizia con un valore.</span><span class="sxs-lookup"><span data-stu-id="266ea-696">Determines whether a string starts with a value.</span></span> <span data-ttu-id="266ea-697">Il confronto non fa distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="266ea-697">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="266ea-698">Parametri</span><span class="sxs-lookup"><span data-stu-id="266ea-698">Parameters</span></span>

| <span data-ttu-id="266ea-699">Parametro</span><span class="sxs-lookup"><span data-stu-id="266ea-699">Parameter</span></span> | <span data-ttu-id="266ea-700">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="266ea-700">Required</span></span> | <span data-ttu-id="266ea-701">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-701">Type</span></span> | <span data-ttu-id="266ea-702">Descrizione</span><span class="sxs-lookup"><span data-stu-id="266ea-702">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="266ea-703">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="266ea-703">stringToSearch</span></span> |<span data-ttu-id="266ea-704">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-704">Yes</span></span> |<span data-ttu-id="266ea-705">string</span><span class="sxs-lookup"><span data-stu-id="266ea-705">string</span></span> |<span data-ttu-id="266ea-706">Valore che contiene l'elemento da cercare.</span><span class="sxs-lookup"><span data-stu-id="266ea-706">The value that contains the item to find.</span></span> |
| <span data-ttu-id="266ea-707">stringToFind</span><span class="sxs-lookup"><span data-stu-id="266ea-707">stringToFind</span></span> |<span data-ttu-id="266ea-708">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-708">Yes</span></span> |<span data-ttu-id="266ea-709">string</span><span class="sxs-lookup"><span data-stu-id="266ea-709">string</span></span> |<span data-ttu-id="266ea-710">Valore da trovare.</span><span class="sxs-lookup"><span data-stu-id="266ea-710">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="266ea-711">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="266ea-711">Return value</span></span>

<span data-ttu-id="266ea-712">**True** se il primo carattere o i caratteri della stringa corrispondono al valore; in caso contrario, restituisce **False**.</span><span class="sxs-lookup"><span data-stu-id="266ea-712">**True** if the first character or characters of the string match the value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="266ea-713">esempi</span><span class="sxs-lookup"><span data-stu-id="266ea-713">Examples</span></span>

<span data-ttu-id="266ea-714">L'esempio seguente mostra come usare le funzioni startsWith ed endsWith:</span><span class="sxs-lookup"><span data-stu-id="266ea-714">The following example shows how to use the startsWith and endsWith functions:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "startsTrue": {
            "value": "[startsWith('abcdef', 'ab')]",
            "type" : "bool"
        },
        "startsCapTrue": {
            "value": "[startsWith('abcdef', 'A')]",
            "type" : "bool"
        },
        "startsFalse": {
            "value": "[startsWith('abcdef', 'e')]",
            "type" : "bool"
        },
        "endsTrue": {
            "value": "[endsWith('abcdef', 'ef')]",
            "type" : "bool"
        },
        "endsCapTrue": {
            "value": "[endsWith('abcdef', 'F')]",
            "type" : "bool"
        },
        "endsFalse": {
            "value": "[endsWith('abcdef', 'e')]",
            "type" : "bool"
        }
    }
}
```

<span data-ttu-id="266ea-715">L'output dell'esempio precedente con i valori predefiniti è:</span><span class="sxs-lookup"><span data-stu-id="266ea-715">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="266ea-716">Nome</span><span class="sxs-lookup"><span data-stu-id="266ea-716">Name</span></span> | <span data-ttu-id="266ea-717">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-717">Type</span></span> | <span data-ttu-id="266ea-718">Valore</span><span class="sxs-lookup"><span data-stu-id="266ea-718">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="266ea-719">startsTrue</span><span class="sxs-lookup"><span data-stu-id="266ea-719">startsTrue</span></span> | <span data-ttu-id="266ea-720">Booleano</span><span class="sxs-lookup"><span data-stu-id="266ea-720">Bool</span></span> | <span data-ttu-id="266ea-721">True </span><span class="sxs-lookup"><span data-stu-id="266ea-721">True</span></span> |
| <span data-ttu-id="266ea-722">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="266ea-722">startsCapTrue</span></span> | <span data-ttu-id="266ea-723">Booleano</span><span class="sxs-lookup"><span data-stu-id="266ea-723">Bool</span></span> | <span data-ttu-id="266ea-724">True </span><span class="sxs-lookup"><span data-stu-id="266ea-724">True</span></span> |
| <span data-ttu-id="266ea-725">startsFalse</span><span class="sxs-lookup"><span data-stu-id="266ea-725">startsFalse</span></span> | <span data-ttu-id="266ea-726">Booleano</span><span class="sxs-lookup"><span data-stu-id="266ea-726">Bool</span></span> | <span data-ttu-id="266ea-727">False</span><span class="sxs-lookup"><span data-stu-id="266ea-727">False</span></span> |
| <span data-ttu-id="266ea-728">endsTrue</span><span class="sxs-lookup"><span data-stu-id="266ea-728">endsTrue</span></span> | <span data-ttu-id="266ea-729">Booleano</span><span class="sxs-lookup"><span data-stu-id="266ea-729">Bool</span></span> | <span data-ttu-id="266ea-730">True </span><span class="sxs-lookup"><span data-stu-id="266ea-730">True</span></span> |
| <span data-ttu-id="266ea-731">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="266ea-731">endsCapTrue</span></span> | <span data-ttu-id="266ea-732">Booleano</span><span class="sxs-lookup"><span data-stu-id="266ea-732">Bool</span></span> | <span data-ttu-id="266ea-733">True </span><span class="sxs-lookup"><span data-stu-id="266ea-733">True</span></span> |
| <span data-ttu-id="266ea-734">endsFalse</span><span class="sxs-lookup"><span data-stu-id="266ea-734">endsFalse</span></span> | <span data-ttu-id="266ea-735">Booleano</span><span class="sxs-lookup"><span data-stu-id="266ea-735">Bool</span></span> | <span data-ttu-id="266ea-736">False</span><span class="sxs-lookup"><span data-stu-id="266ea-736">False</span></span> |

<a id="string" />

## <a name="string"></a><span data-ttu-id="266ea-737">string</span><span class="sxs-lookup"><span data-stu-id="266ea-737">string</span></span>
`string(valueToConvert)`

<span data-ttu-id="266ea-738">Converte il valore specificato in una stringa.</span><span class="sxs-lookup"><span data-stu-id="266ea-738">Converts the specified value to a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="266ea-739">Parametri</span><span class="sxs-lookup"><span data-stu-id="266ea-739">Parameters</span></span>

| <span data-ttu-id="266ea-740">Parametro</span><span class="sxs-lookup"><span data-stu-id="266ea-740">Parameter</span></span> | <span data-ttu-id="266ea-741">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="266ea-741">Required</span></span> | <span data-ttu-id="266ea-742">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-742">Type</span></span> | <span data-ttu-id="266ea-743">Descrizione</span><span class="sxs-lookup"><span data-stu-id="266ea-743">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="266ea-744">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="266ea-744">valueToConvert</span></span> |<span data-ttu-id="266ea-745">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-745">Yes</span></span> | <span data-ttu-id="266ea-746">Qualsiasi</span><span class="sxs-lookup"><span data-stu-id="266ea-746">Any</span></span> |<span data-ttu-id="266ea-747">Valore da convertire in stringa.</span><span class="sxs-lookup"><span data-stu-id="266ea-747">The value to convert to string.</span></span> <span data-ttu-id="266ea-748">È possibile convertire qualsiasi tipo di valore, inclusi gli oggetti e le matrici.</span><span class="sxs-lookup"><span data-stu-id="266ea-748">Any type of value can be converted, including objects and arrays.</span></span> |

### <a name="return-value"></a><span data-ttu-id="266ea-749">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="266ea-749">Return value</span></span>

<span data-ttu-id="266ea-750">Stringa del valore convertito.</span><span class="sxs-lookup"><span data-stu-id="266ea-750">A string of the converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="266ea-751">esempi</span><span class="sxs-lookup"><span data-stu-id="266ea-751">Examples</span></span>

<span data-ttu-id="266ea-752">L'esempio seguente mostra come convertire diversi tipi di valori di stringa:</span><span class="sxs-lookup"><span data-stu-id="266ea-752">The following example shows how to convert different types of values to strings:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testObject": {
            "type": "object",
            "defaultValue": {
                "valueA": 10,
                "valueB": "Example Text"
            }
        },
        "testArray": {
            "type": "array",
            "defaultValue": [
                "a",
                "b",
                "c"
            ]
        },
        "testInt": {
            "type": "int",
            "defaultValue": 5
        }
    },
    "resources": [],
    "outputs": {
        "objectOutput": {
            "type": "string",
            "value": "[string(parameters('testObject'))]"
        },
        "arrayOutput": {
            "type": "string",
            "value": "[string(parameters('testArray'))]"
        },
        "intOutput": {
            "type": "string",
            "value": "[string(parameters('testInt'))]"
        }
    }
}
```

<span data-ttu-id="266ea-753">L'output dell'esempio precedente con i valori predefiniti è:</span><span class="sxs-lookup"><span data-stu-id="266ea-753">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="266ea-754">Nome</span><span class="sxs-lookup"><span data-stu-id="266ea-754">Name</span></span> | <span data-ttu-id="266ea-755">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-755">Type</span></span> | <span data-ttu-id="266ea-756">Valore</span><span class="sxs-lookup"><span data-stu-id="266ea-756">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="266ea-757">objectOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-757">objectOutput</span></span> | <span data-ttu-id="266ea-758">String</span><span class="sxs-lookup"><span data-stu-id="266ea-758">String</span></span> | <span data-ttu-id="266ea-759">{"valueA":10,"valueB":"Example Text"}</span><span class="sxs-lookup"><span data-stu-id="266ea-759">{"valueA":10,"valueB":"Example Text"}</span></span> |
| <span data-ttu-id="266ea-760">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-760">arrayOutput</span></span> | <span data-ttu-id="266ea-761">String</span><span class="sxs-lookup"><span data-stu-id="266ea-761">String</span></span> | <span data-ttu-id="266ea-762">["a","b","c"]</span><span class="sxs-lookup"><span data-stu-id="266ea-762">["a","b","c"]</span></span> |
| <span data-ttu-id="266ea-763">intOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-763">intOutput</span></span> | <span data-ttu-id="266ea-764">String</span><span class="sxs-lookup"><span data-stu-id="266ea-764">String</span></span> | <span data-ttu-id="266ea-765">5</span><span class="sxs-lookup"><span data-stu-id="266ea-765">5</span></span> |

<a id="substring" />

## <a name="substring"></a><span data-ttu-id="266ea-766">substring</span><span class="sxs-lookup"><span data-stu-id="266ea-766">substring</span></span>
`substring(stringToParse, startIndex, length)`

<span data-ttu-id="266ea-767">Restituisce una sottostringa che inizia nella posizione del carattere specificato e contiene il numero di caratteri specificato.</span><span class="sxs-lookup"><span data-stu-id="266ea-767">Returns a substring that starts at the specified character position and contains the specified number of characters.</span></span>

### <a name="parameters"></a><span data-ttu-id="266ea-768">Parametri</span><span class="sxs-lookup"><span data-stu-id="266ea-768">Parameters</span></span>

| <span data-ttu-id="266ea-769">Parametro</span><span class="sxs-lookup"><span data-stu-id="266ea-769">Parameter</span></span> | <span data-ttu-id="266ea-770">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="266ea-770">Required</span></span> | <span data-ttu-id="266ea-771">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-771">Type</span></span> | <span data-ttu-id="266ea-772">Descrizione</span><span class="sxs-lookup"><span data-stu-id="266ea-772">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="266ea-773">stringToParse</span><span class="sxs-lookup"><span data-stu-id="266ea-773">stringToParse</span></span> |<span data-ttu-id="266ea-774">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-774">Yes</span></span> |<span data-ttu-id="266ea-775">string</span><span class="sxs-lookup"><span data-stu-id="266ea-775">string</span></span> |<span data-ttu-id="266ea-776">La stringa originale da cui estrarre la sottostringa.</span><span class="sxs-lookup"><span data-stu-id="266ea-776">The original string from which the substring is extracted.</span></span> |
| <span data-ttu-id="266ea-777">startIndex</span><span class="sxs-lookup"><span data-stu-id="266ea-777">startIndex</span></span> |<span data-ttu-id="266ea-778">No</span><span class="sxs-lookup"><span data-stu-id="266ea-778">No</span></span> |<span data-ttu-id="266ea-779">int</span><span class="sxs-lookup"><span data-stu-id="266ea-779">int</span></span> |<span data-ttu-id="266ea-780">La posizione del carattere iniziale in base zero della sottostringa.</span><span class="sxs-lookup"><span data-stu-id="266ea-780">The zero-based starting character position for the substring.</span></span> |
| <span data-ttu-id="266ea-781">length</span><span class="sxs-lookup"><span data-stu-id="266ea-781">length</span></span> |<span data-ttu-id="266ea-782">No</span><span class="sxs-lookup"><span data-stu-id="266ea-782">No</span></span> |<span data-ttu-id="266ea-783">int</span><span class="sxs-lookup"><span data-stu-id="266ea-783">int</span></span> |<span data-ttu-id="266ea-784">Il numero di caratteri della sottostringa.</span><span class="sxs-lookup"><span data-stu-id="266ea-784">The number of characters for the substring.</span></span> <span data-ttu-id="266ea-785">Deve fare riferimento a una posizione nella stringa.</span><span class="sxs-lookup"><span data-stu-id="266ea-785">Must refer to a location within the string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="266ea-786">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="266ea-786">Return value</span></span>

<span data-ttu-id="266ea-787">La sottostringa.</span><span class="sxs-lookup"><span data-stu-id="266ea-787">The substring.</span></span>

### <a name="remarks"></a><span data-ttu-id="266ea-788">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="266ea-788">Remarks</span></span>

<span data-ttu-id="266ea-789">La funzione ha esito negativo se la sottostringa si estende oltre la fine della stringa.</span><span class="sxs-lookup"><span data-stu-id="266ea-789">The function fails when the substring extends beyond the end of the string.</span></span> <span data-ttu-id="266ea-790">L'esempio seguente ha esito negativo e visualizza l'errore "I parametri index e length devono fare riferimento a una posizione all'interno della stringa.</span><span class="sxs-lookup"><span data-stu-id="266ea-790">The following example fails with the error "The index and length parameters must refer to a location within the string.</span></span> <span data-ttu-id="266ea-791">Parametro index: '0', parametro length: '11', lunghezza del parametro string: '10'.".</span><span class="sxs-lookup"><span data-stu-id="266ea-791">The index parameter: '0', the length parameter: '11', the length of the string parameter: '10'.".</span></span>

```json
"parameters": {
    "inputString": { "type": "string", "value": "1234567890" }
},
"variables": { 
    "prefix": "[substring(parameters('inputString'), 0, 11)]"
}
```

### <a name="examples"></a><span data-ttu-id="266ea-792">esempi</span><span class="sxs-lookup"><span data-stu-id="266ea-792">Examples</span></span>

<span data-ttu-id="266ea-793">L'esempio seguente estrae una sottostringa da un parametro.</span><span class="sxs-lookup"><span data-stu-id="266ea-793">The following example extracts a substring from a parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        }
    },
    "resources": [],
    "outputs": {
        "substringOutput": {
            "value": "[substring(parameters('testString'), 4, 3)]",
            "type": "string"
        }
    }
}
```

<span data-ttu-id="266ea-794">L'output dell'esempio precedente con i valori predefiniti è:</span><span class="sxs-lookup"><span data-stu-id="266ea-794">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="266ea-795">Nome</span><span class="sxs-lookup"><span data-stu-id="266ea-795">Name</span></span> | <span data-ttu-id="266ea-796">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-796">Type</span></span> | <span data-ttu-id="266ea-797">Valore</span><span class="sxs-lookup"><span data-stu-id="266ea-797">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="266ea-798">substringOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-798">substringOutput</span></span> | <span data-ttu-id="266ea-799">String</span><span class="sxs-lookup"><span data-stu-id="266ea-799">String</span></span> | <span data-ttu-id="266ea-800">two</span><span class="sxs-lookup"><span data-stu-id="266ea-800">two</span></span> |


<a id="take" />

## <a name="take"></a><span data-ttu-id="266ea-801">take</span><span class="sxs-lookup"><span data-stu-id="266ea-801">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="266ea-802">Restituisce una stringa con il numero specificato di caratteri dall'inizio della stringa o una matrice con il numero specificato di elementi dall'inizio della matrice.</span><span class="sxs-lookup"><span data-stu-id="266ea-802">Returns a string with the specified number of characters from the start of the string, or an array with the specified number of elements from the start of the array.</span></span>

### <a name="parameters"></a><span data-ttu-id="266ea-803">Parametri</span><span class="sxs-lookup"><span data-stu-id="266ea-803">Parameters</span></span>

| <span data-ttu-id="266ea-804">Parametro</span><span class="sxs-lookup"><span data-stu-id="266ea-804">Parameter</span></span> | <span data-ttu-id="266ea-805">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="266ea-805">Required</span></span> | <span data-ttu-id="266ea-806">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-806">Type</span></span> | <span data-ttu-id="266ea-807">Descrizione</span><span class="sxs-lookup"><span data-stu-id="266ea-807">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="266ea-808">originalValue</span><span class="sxs-lookup"><span data-stu-id="266ea-808">originalValue</span></span> |<span data-ttu-id="266ea-809">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-809">Yes</span></span> |<span data-ttu-id="266ea-810">stringa o matrice</span><span class="sxs-lookup"><span data-stu-id="266ea-810">array or string</span></span> |<span data-ttu-id="266ea-811">Stringa o matrice da cui prendere gli elementi.</span><span class="sxs-lookup"><span data-stu-id="266ea-811">The array or string to take the elements from.</span></span> |
| <span data-ttu-id="266ea-812">numberToTake</span><span class="sxs-lookup"><span data-stu-id="266ea-812">numberToTake</span></span> |<span data-ttu-id="266ea-813">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-813">Yes</span></span> |<span data-ttu-id="266ea-814">int</span><span class="sxs-lookup"><span data-stu-id="266ea-814">int</span></span> |<span data-ttu-id="266ea-815">Numero di elementi o caratteri da prendere.</span><span class="sxs-lookup"><span data-stu-id="266ea-815">The number of elements or characters to take.</span></span> <span data-ttu-id="266ea-816">Se il valore è minore o uguale a 0, viene restituita una stringa o un matrice vuota.</span><span class="sxs-lookup"><span data-stu-id="266ea-816">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="266ea-817">Se il valore è maggiore della lunghezza della stringa o matrice specificata, vengono restituiti tutti gli elementi nella stringa o nella matrice.</span><span class="sxs-lookup"><span data-stu-id="266ea-817">If it is larger than the length of the given array or string, all the elements in the array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="266ea-818">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="266ea-818">Return value</span></span>

<span data-ttu-id="266ea-819">Stringa o matrice.</span><span class="sxs-lookup"><span data-stu-id="266ea-819">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="266ea-820">esempi</span><span class="sxs-lookup"><span data-stu-id="266ea-820">Examples</span></span>

<span data-ttu-id="266ea-821">L'esempio seguente prende il numero specificato di elementi dalla matrice e di caratteri dalla stringa.</span><span class="sxs-lookup"><span data-stu-id="266ea-821">The following example takes the specified number of elements from the array, and characters from a string.</span></span>

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

<span data-ttu-id="266ea-822">L'output dell'esempio precedente con i valori predefiniti è il seguente:</span><span class="sxs-lookup"><span data-stu-id="266ea-822">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="266ea-823">Nome</span><span class="sxs-lookup"><span data-stu-id="266ea-823">Name</span></span> | <span data-ttu-id="266ea-824">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-824">Type</span></span> | <span data-ttu-id="266ea-825">Valore</span><span class="sxs-lookup"><span data-stu-id="266ea-825">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="266ea-826">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-826">arrayOutput</span></span> | <span data-ttu-id="266ea-827">Array</span><span class="sxs-lookup"><span data-stu-id="266ea-827">Array</span></span> | <span data-ttu-id="266ea-828">["one", "two"]</span><span class="sxs-lookup"><span data-stu-id="266ea-828">["one", "two"]</span></span> |
| <span data-ttu-id="266ea-829">stringOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-829">stringOutput</span></span> | <span data-ttu-id="266ea-830">String</span><span class="sxs-lookup"><span data-stu-id="266ea-830">String</span></span> | <span data-ttu-id="266ea-831">in</span><span class="sxs-lookup"><span data-stu-id="266ea-831">on</span></span> |

<a id="tolower" />

## <a name="tolower"></a><span data-ttu-id="266ea-832">toLower</span><span class="sxs-lookup"><span data-stu-id="266ea-832">toLower</span></span>
`toLower(stringToChange)`

<span data-ttu-id="266ea-833">Converte la stringa specificata in caratteri minuscoli.</span><span class="sxs-lookup"><span data-stu-id="266ea-833">Converts the specified string to lower case.</span></span>

### <a name="parameters"></a><span data-ttu-id="266ea-834">Parametri</span><span class="sxs-lookup"><span data-stu-id="266ea-834">Parameters</span></span>

| <span data-ttu-id="266ea-835">Parametro</span><span class="sxs-lookup"><span data-stu-id="266ea-835">Parameter</span></span> | <span data-ttu-id="266ea-836">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="266ea-836">Required</span></span> | <span data-ttu-id="266ea-837">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-837">Type</span></span> | <span data-ttu-id="266ea-838">Descrizione</span><span class="sxs-lookup"><span data-stu-id="266ea-838">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="266ea-839">stringToChange</span><span class="sxs-lookup"><span data-stu-id="266ea-839">stringToChange</span></span> |<span data-ttu-id="266ea-840">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-840">Yes</span></span> |<span data-ttu-id="266ea-841">string</span><span class="sxs-lookup"><span data-stu-id="266ea-841">string</span></span> |<span data-ttu-id="266ea-842">Il valore da convertire in lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="266ea-842">The value to convert to lower case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="266ea-843">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="266ea-843">Return value</span></span>

<span data-ttu-id="266ea-844">La stringa convertita in lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="266ea-844">The string converted to lower case.</span></span>

### <a name="examples"></a><span data-ttu-id="266ea-845">esempi</span><span class="sxs-lookup"><span data-stu-id="266ea-845">Examples</span></span>

<span data-ttu-id="266ea-846">L'esempio seguente converte il valore del parametro in lettere maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="266ea-846">The following example converts a parameter value to lower case and to upper case.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "toLowerOutput": {
            "value": "[toLower(parameters('testString'))]",
            "type": "string"
        },
        "toUpperOutput": {
            "type": "string",
            "value": "[toUpper(parameters('testString'))]"
        }
    }
}
```

<span data-ttu-id="266ea-847">L'output dell'esempio precedente con i valori predefiniti è:</span><span class="sxs-lookup"><span data-stu-id="266ea-847">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="266ea-848">Nome</span><span class="sxs-lookup"><span data-stu-id="266ea-848">Name</span></span> | <span data-ttu-id="266ea-849">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-849">Type</span></span> | <span data-ttu-id="266ea-850">Valore</span><span class="sxs-lookup"><span data-stu-id="266ea-850">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="266ea-851">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-851">toLowerOutput</span></span> | <span data-ttu-id="266ea-852">String</span><span class="sxs-lookup"><span data-stu-id="266ea-852">String</span></span> | <span data-ttu-id="266ea-853">one two three</span><span class="sxs-lookup"><span data-stu-id="266ea-853">one two three</span></span> |
| <span data-ttu-id="266ea-854">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-854">toUpperOutput</span></span> | <span data-ttu-id="266ea-855">String</span><span class="sxs-lookup"><span data-stu-id="266ea-855">String</span></span> | <span data-ttu-id="266ea-856">ONE TWO THREE</span><span class="sxs-lookup"><span data-stu-id="266ea-856">ONE TWO THREE</span></span> |

<a id="toupper" />

## <a name="toupper"></a><span data-ttu-id="266ea-857">toUpper</span><span class="sxs-lookup"><span data-stu-id="266ea-857">toUpper</span></span>
`toUpper(stringToChange)`

<span data-ttu-id="266ea-858">Converte la stringa specificata in lettere maiuscole.</span><span class="sxs-lookup"><span data-stu-id="266ea-858">Converts the specified string to upper case.</span></span>

### <a name="parameters"></a><span data-ttu-id="266ea-859">Parametri</span><span class="sxs-lookup"><span data-stu-id="266ea-859">Parameters</span></span>

| <span data-ttu-id="266ea-860">Parametro</span><span class="sxs-lookup"><span data-stu-id="266ea-860">Parameter</span></span> | <span data-ttu-id="266ea-861">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="266ea-861">Required</span></span> | <span data-ttu-id="266ea-862">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-862">Type</span></span> | <span data-ttu-id="266ea-863">Descrizione</span><span class="sxs-lookup"><span data-stu-id="266ea-863">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="266ea-864">stringToChange</span><span class="sxs-lookup"><span data-stu-id="266ea-864">stringToChange</span></span> |<span data-ttu-id="266ea-865">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-865">Yes</span></span> |<span data-ttu-id="266ea-866">string</span><span class="sxs-lookup"><span data-stu-id="266ea-866">string</span></span> |<span data-ttu-id="266ea-867">Il valore da convertire in lettere maiuscole.</span><span class="sxs-lookup"><span data-stu-id="266ea-867">The value to convert to upper case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="266ea-868">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="266ea-868">Return value</span></span>

<span data-ttu-id="266ea-869">La stringa convertita in lettere maiuscole.</span><span class="sxs-lookup"><span data-stu-id="266ea-869">The string converted to upper case.</span></span>

### <a name="examples"></a><span data-ttu-id="266ea-870">esempi</span><span class="sxs-lookup"><span data-stu-id="266ea-870">Examples</span></span>

<span data-ttu-id="266ea-871">L'esempio seguente converte il valore del parametro in lettere maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="266ea-871">The following example converts a parameter value to lower case and to upper case.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "toLowerOutput": {
            "value": "[toLower(parameters('testString'))]",
            "type": "string"
        },
        "toUpperOutput": {
            "type": "string",
            "value": "[toUpper(parameters('testString'))]"
        }
    }
}
```

<span data-ttu-id="266ea-872">L'output dell'esempio precedente con i valori predefiniti è:</span><span class="sxs-lookup"><span data-stu-id="266ea-872">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="266ea-873">Nome</span><span class="sxs-lookup"><span data-stu-id="266ea-873">Name</span></span> | <span data-ttu-id="266ea-874">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-874">Type</span></span> | <span data-ttu-id="266ea-875">Valore</span><span class="sxs-lookup"><span data-stu-id="266ea-875">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="266ea-876">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-876">toLowerOutput</span></span> | <span data-ttu-id="266ea-877">String</span><span class="sxs-lookup"><span data-stu-id="266ea-877">String</span></span> | <span data-ttu-id="266ea-878">one two three</span><span class="sxs-lookup"><span data-stu-id="266ea-878">one two three</span></span> |
| <span data-ttu-id="266ea-879">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-879">toUpperOutput</span></span> | <span data-ttu-id="266ea-880">String</span><span class="sxs-lookup"><span data-stu-id="266ea-880">String</span></span> | <span data-ttu-id="266ea-881">ONE TWO THREE</span><span class="sxs-lookup"><span data-stu-id="266ea-881">ONE TWO THREE</span></span> |

<a id="trim" />

## <a name="trim"></a><span data-ttu-id="266ea-882">Trim</span><span class="sxs-lookup"><span data-stu-id="266ea-882">trim</span></span>
`trim (stringToTrim)`

<span data-ttu-id="266ea-883">Rimuove tutti i caratteri di spazi vuoti iniziali e finali dalla stringa specificata.</span><span class="sxs-lookup"><span data-stu-id="266ea-883">Removes all leading and trailing white-space characters from the specified string.</span></span>

### <a name="parameters"></a><span data-ttu-id="266ea-884">Parametri</span><span class="sxs-lookup"><span data-stu-id="266ea-884">Parameters</span></span>

| <span data-ttu-id="266ea-885">Parametro</span><span class="sxs-lookup"><span data-stu-id="266ea-885">Parameter</span></span> | <span data-ttu-id="266ea-886">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="266ea-886">Required</span></span> | <span data-ttu-id="266ea-887">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-887">Type</span></span> | <span data-ttu-id="266ea-888">Descrizione</span><span class="sxs-lookup"><span data-stu-id="266ea-888">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="266ea-889">stringToTrim</span><span class="sxs-lookup"><span data-stu-id="266ea-889">stringToTrim</span></span> |<span data-ttu-id="266ea-890">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-890">Yes</span></span> |<span data-ttu-id="266ea-891">string</span><span class="sxs-lookup"><span data-stu-id="266ea-891">string</span></span> |<span data-ttu-id="266ea-892">Il valore da tagliare.</span><span class="sxs-lookup"><span data-stu-id="266ea-892">The value to trim.</span></span> |

### <a name="return-value"></a><span data-ttu-id="266ea-893">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="266ea-893">Return value</span></span>

<span data-ttu-id="266ea-894">La stringa senza spazi vuoti iniziali e finali.</span><span class="sxs-lookup"><span data-stu-id="266ea-894">The string without leading and trailing white-space characters.</span></span>

### <a name="examples"></a><span data-ttu-id="266ea-895">esempi</span><span class="sxs-lookup"><span data-stu-id="266ea-895">Examples</span></span>

<span data-ttu-id="266ea-896">L'esempio seguente elimina i caratteri spazi vuoti dal parametro.</span><span class="sxs-lookup"><span data-stu-id="266ea-896">The following example trims the white-space characters from the parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "    one two three   "
        }
    },
    "resources": [],
    "outputs": {
        "return": {
            "type": "string",
            "value": "[trim(parameters('testString'))]"
        }
    }
}
```

<span data-ttu-id="266ea-897">L'output dell'esempio precedente con i valori predefiniti è:</span><span class="sxs-lookup"><span data-stu-id="266ea-897">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="266ea-898">Nome</span><span class="sxs-lookup"><span data-stu-id="266ea-898">Name</span></span> | <span data-ttu-id="266ea-899">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-899">Type</span></span> | <span data-ttu-id="266ea-900">Valore</span><span class="sxs-lookup"><span data-stu-id="266ea-900">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="266ea-901">return</span><span class="sxs-lookup"><span data-stu-id="266ea-901">return</span></span> | <span data-ttu-id="266ea-902">String</span><span class="sxs-lookup"><span data-stu-id="266ea-902">String</span></span> | <span data-ttu-id="266ea-903">one two three</span><span class="sxs-lookup"><span data-stu-id="266ea-903">one two three</span></span> |

<a id="uniquestring" />

## <a name="uniquestring"></a><span data-ttu-id="266ea-904">uniqueString</span><span class="sxs-lookup"><span data-stu-id="266ea-904">uniqueString</span></span>
`uniqueString (baseString, ...)`

<span data-ttu-id="266ea-905">Crea una stringa hash deterministica in base ai valori forniti come parametri.</span><span class="sxs-lookup"><span data-stu-id="266ea-905">Creates a deterministic hash string based on the values provided as parameters.</span></span> 

### <a name="parameters"></a><span data-ttu-id="266ea-906">Parametri</span><span class="sxs-lookup"><span data-stu-id="266ea-906">Parameters</span></span>

| <span data-ttu-id="266ea-907">Parametro</span><span class="sxs-lookup"><span data-stu-id="266ea-907">Parameter</span></span> | <span data-ttu-id="266ea-908">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="266ea-908">Required</span></span> | <span data-ttu-id="266ea-909">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-909">Type</span></span> | <span data-ttu-id="266ea-910">Descrizione</span><span class="sxs-lookup"><span data-stu-id="266ea-910">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="266ea-911">baseString</span><span class="sxs-lookup"><span data-stu-id="266ea-911">baseString</span></span> |<span data-ttu-id="266ea-912">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-912">Yes</span></span> |<span data-ttu-id="266ea-913">string</span><span class="sxs-lookup"><span data-stu-id="266ea-913">string</span></span> |<span data-ttu-id="266ea-914">Il valore usato nella funzione hash per creare una stringa univoca.</span><span class="sxs-lookup"><span data-stu-id="266ea-914">The value used in the hash function to create a unique string.</span></span> |
| <span data-ttu-id="266ea-915">parametri aggiuntivi in base alle esigenze</span><span class="sxs-lookup"><span data-stu-id="266ea-915">additional parameters as needed</span></span> |<span data-ttu-id="266ea-916">No</span><span class="sxs-lookup"><span data-stu-id="266ea-916">No</span></span> |<span data-ttu-id="266ea-917">string</span><span class="sxs-lookup"><span data-stu-id="266ea-917">string</span></span> |<span data-ttu-id="266ea-918">È possibile aggiungere tutte le stringhe necessarie per creare il valore che specifica il livello di univocità.</span><span class="sxs-lookup"><span data-stu-id="266ea-918">You can add as many strings as needed to create the value that specifies the level of uniqueness.</span></span> |

### <a name="remarks"></a><span data-ttu-id="266ea-919">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="266ea-919">Remarks</span></span>

<span data-ttu-id="266ea-920">Questa funzione è utile quando è necessario creare un nome univoco per una risorsa.</span><span class="sxs-lookup"><span data-stu-id="266ea-920">This function is helpful when you need to create a unique name for a resource.</span></span> <span data-ttu-id="266ea-921">È possibile specificare i valori dei parametri che limitano l'ambito di univocità per il risultato.</span><span class="sxs-lookup"><span data-stu-id="266ea-921">You provide parameter values that limit the scope of uniqueness for the result.</span></span> <span data-ttu-id="266ea-922">È possibile specificare se il nome è univoco nella sottoscrizione, nel gruppo di risorse o nella distribuzione.</span><span class="sxs-lookup"><span data-stu-id="266ea-922">You can specify whether the name is unique down to subscription, resource group, or deployment.</span></span> 

<span data-ttu-id="266ea-923">Il valore restituito non è una stringa casuale, ma il risultato di una funzione hash.</span><span class="sxs-lookup"><span data-stu-id="266ea-923">The returned value is not a random string, but rather the result of a hash function.</span></span> <span data-ttu-id="266ea-924">Il valore restituito ha una lunghezza di 13 caratteri.</span><span class="sxs-lookup"><span data-stu-id="266ea-924">The returned value is 13 characters long.</span></span> <span data-ttu-id="266ea-925">Non è globalmente univoco.</span><span class="sxs-lookup"><span data-stu-id="266ea-925">It is not globally unique.</span></span> <span data-ttu-id="266ea-926">È possibile combinare il valore con un prefisso dalla convenzione di denominazione scelta per creare un nome significativo.</span><span class="sxs-lookup"><span data-stu-id="266ea-926">You may want to combine the value with a prefix from your naming convention to create a name that is meaningful.</span></span> <span data-ttu-id="266ea-927">L'esempio seguente illustra il formato del valore restituito.</span><span class="sxs-lookup"><span data-stu-id="266ea-927">The following example shows the format of the returned value.</span></span> <span data-ttu-id="266ea-928">Il valore effettivo varia in base ai parametri forniti.</span><span class="sxs-lookup"><span data-stu-id="266ea-928">The actual value varies by the provided parameters.</span></span>

    tcvhiyu5h2o5o

<span data-ttu-id="266ea-929">Gli esempi seguenti mostrano come usare uniqueString per creare un valore univoco per livelli di uso comune.</span><span class="sxs-lookup"><span data-stu-id="266ea-929">The following examples show how to use uniqueString to create a unique value for commonly used levels.</span></span>

<span data-ttu-id="266ea-930">Con ambito univoco nella sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="266ea-930">Unique scoped to subscription</span></span>

```json
"[uniqueString(subscription().subscriptionId)]"
```

<span data-ttu-id="266ea-931">Con ambito univoco nel gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="266ea-931">Unique scoped to resource group</span></span>

```json
"[uniqueString(resourceGroup().id)]"
```

<span data-ttu-id="266ea-932">Con ambito univoco nella distribuzione per un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="266ea-932">Unique scoped to deployment for a resource group</span></span>

```json
"[uniqueString(resourceGroup().id, deployment().name)]"
```

<span data-ttu-id="266ea-933">Nell'esempio seguente viene illustrato come creare un nome univoco per un account di archiviazione in base al gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="266ea-933">The following example shows how to create a unique name for a storage account based on your resource group.</span></span> <span data-ttu-id="266ea-934">All'interno del gruppo di risorse, il nome non è univoco se costruito allo stesso modo.</span><span class="sxs-lookup"><span data-stu-id="266ea-934">Inside the resource group, the name is not unique if constructed the same way.</span></span>

```json
"resources": [{ 
    "name": "[concat('storage', uniqueString(resourceGroup().id))]", 
    "type": "Microsoft.Storage/storageAccounts", 
    ...
```

### <a name="return-value"></a><span data-ttu-id="266ea-935">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="266ea-935">Return value</span></span>

<span data-ttu-id="266ea-936">Stringa contenente 13 caratteri.</span><span class="sxs-lookup"><span data-stu-id="266ea-936">A string containing 13 characters.</span></span>

### <a name="examples"></a><span data-ttu-id="266ea-937">esempi</span><span class="sxs-lookup"><span data-stu-id="266ea-937">Examples</span></span>

<span data-ttu-id="266ea-938">Nell'esempio seguente restituisce risultati da uniqueString:</span><span class="sxs-lookup"><span data-stu-id="266ea-938">The following example returns results from uniquestring:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "uniqueRG": {
            "value": "[uniqueString(resourceGroup().id)]",
            "type" : "string"
        },
        "uniqueDeploy": {
            "value": "[uniqueString(resourceGroup().id, deployment().name)]",
            "type" : "string"
        }
    }
}
```

<a id="uri" />

## <a name="uri"></a><span data-ttu-id="266ea-939">Uri</span><span class="sxs-lookup"><span data-stu-id="266ea-939">uri</span></span>
`uri (baseUri, relativeUri)`

<span data-ttu-id="266ea-940">Crea un URI assoluto combinando la baseUri e la stringa relativeUri.</span><span class="sxs-lookup"><span data-stu-id="266ea-940">Creates an absolute URI by combining the baseUri and the relativeUri string.</span></span>

### <a name="parameters"></a><span data-ttu-id="266ea-941">Parametri</span><span class="sxs-lookup"><span data-stu-id="266ea-941">Parameters</span></span>

| <span data-ttu-id="266ea-942">Parametro</span><span class="sxs-lookup"><span data-stu-id="266ea-942">Parameter</span></span> | <span data-ttu-id="266ea-943">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="266ea-943">Required</span></span> | <span data-ttu-id="266ea-944">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-944">Type</span></span> | <span data-ttu-id="266ea-945">Descrizione</span><span class="sxs-lookup"><span data-stu-id="266ea-945">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="266ea-946">baseUri</span><span class="sxs-lookup"><span data-stu-id="266ea-946">baseUri</span></span> |<span data-ttu-id="266ea-947">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-947">Yes</span></span> |<span data-ttu-id="266ea-948">string</span><span class="sxs-lookup"><span data-stu-id="266ea-948">string</span></span> |<span data-ttu-id="266ea-949">La stringa URI di base.</span><span class="sxs-lookup"><span data-stu-id="266ea-949">The base uri string.</span></span> |
| <span data-ttu-id="266ea-950">relativeUri</span><span class="sxs-lookup"><span data-stu-id="266ea-950">relativeUri</span></span> |<span data-ttu-id="266ea-951">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-951">Yes</span></span> |<span data-ttu-id="266ea-952">string</span><span class="sxs-lookup"><span data-stu-id="266ea-952">string</span></span> |<span data-ttu-id="266ea-953">La stringa URI relativa da aggiungere alla stringa di URI di base.</span><span class="sxs-lookup"><span data-stu-id="266ea-953">The relative uri string to add to the base uri string.</span></span> |

<span data-ttu-id="266ea-954">Il valore per il parametro **baseUri** può includere un file specifico, ma solo il percorso di base viene usato per costruire l'URI.</span><span class="sxs-lookup"><span data-stu-id="266ea-954">The value for the **baseUri** parameter can include a specific file, but only the base path is used when constructing the URI.</span></span> <span data-ttu-id="266ea-955">Ad esempio, se si trasmette `http://contoso.com/resources/azuredeploy.json` come parametro baseUri, viene restituito l'URI di base `http://contoso.com/resources/`.</span><span class="sxs-lookup"><span data-stu-id="266ea-955">For example, passing `http://contoso.com/resources/azuredeploy.json` as the baseUri parameter results in a base URI of `http://contoso.com/resources/`.</span></span>

### <a name="return-value"></a><span data-ttu-id="266ea-956">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="266ea-956">Return value</span></span>

<span data-ttu-id="266ea-957">Stringa che rappresenta l'URI assoluto dei valori di base e relativi.</span><span class="sxs-lookup"><span data-stu-id="266ea-957">A string representing the absolute URI for the base and relative values.</span></span>

### <a name="examples"></a><span data-ttu-id="266ea-958">esempi</span><span class="sxs-lookup"><span data-stu-id="266ea-958">Examples</span></span>

<span data-ttu-id="266ea-959">Nell'esempio seguente viene illustrato come costruire un collegamento a un modello annidato in base al valore del modello padre.</span><span class="sxs-lookup"><span data-stu-id="266ea-959">The following example shows how to construct a link to a nested template based on the value of the parent template.</span></span>

```json
"templateLink": "[uri(deployment().properties.templateLink.uri, 'nested/azuredeploy.json')]"
```

<span data-ttu-id="266ea-960">L'esempio seguente mostra come usare uri, uriComponent e uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="266ea-960">The following example shows how to use uri, uriComponent, and uriComponentToString:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

<span data-ttu-id="266ea-961">L'output dell'esempio precedente con i valori predefiniti è:</span><span class="sxs-lookup"><span data-stu-id="266ea-961">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="266ea-962">Nome</span><span class="sxs-lookup"><span data-stu-id="266ea-962">Name</span></span> | <span data-ttu-id="266ea-963">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-963">Type</span></span> | <span data-ttu-id="266ea-964">Valore</span><span class="sxs-lookup"><span data-stu-id="266ea-964">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="266ea-965">uriOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-965">uriOutput</span></span> | <span data-ttu-id="266ea-966">String</span><span class="sxs-lookup"><span data-stu-id="266ea-966">String</span></span> | <span data-ttu-id="266ea-967">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="266ea-967">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="266ea-968">componentOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-968">componentOutput</span></span> | <span data-ttu-id="266ea-969">String</span><span class="sxs-lookup"><span data-stu-id="266ea-969">String</span></span> | <span data-ttu-id="266ea-970">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="266ea-970">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="266ea-971">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-971">toStringOutput</span></span> | <span data-ttu-id="266ea-972">String</span><span class="sxs-lookup"><span data-stu-id="266ea-972">String</span></span> | <span data-ttu-id="266ea-973">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="266ea-973">http://contoso.com/resources/nested/azuredeploy.json</span></span> |

<a id="uricomponent" />

## <a name="uricomponent"></a><span data-ttu-id="266ea-974">uriComponent</span><span class="sxs-lookup"><span data-stu-id="266ea-974">uriComponent</span></span>
`uricomponent(stringToEncode)`

<span data-ttu-id="266ea-975">Codifica un URI.</span><span class="sxs-lookup"><span data-stu-id="266ea-975">Encodes a URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="266ea-976">Parametri</span><span class="sxs-lookup"><span data-stu-id="266ea-976">Parameters</span></span>

| <span data-ttu-id="266ea-977">Parametro</span><span class="sxs-lookup"><span data-stu-id="266ea-977">Parameter</span></span> | <span data-ttu-id="266ea-978">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="266ea-978">Required</span></span> | <span data-ttu-id="266ea-979">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-979">Type</span></span> | <span data-ttu-id="266ea-980">Descrizione</span><span class="sxs-lookup"><span data-stu-id="266ea-980">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="266ea-981">stringToEncode</span><span class="sxs-lookup"><span data-stu-id="266ea-981">stringToEncode</span></span> |<span data-ttu-id="266ea-982">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-982">Yes</span></span> |<span data-ttu-id="266ea-983">string</span><span class="sxs-lookup"><span data-stu-id="266ea-983">string</span></span> |<span data-ttu-id="266ea-984">Valore da codificare.</span><span class="sxs-lookup"><span data-stu-id="266ea-984">The value to encode.</span></span> |

### <a name="return-value"></a><span data-ttu-id="266ea-985">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="266ea-985">Return value</span></span>

<span data-ttu-id="266ea-986">Stringa del valore URI codificato.</span><span class="sxs-lookup"><span data-stu-id="266ea-986">A string of the URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="266ea-987">esempi</span><span class="sxs-lookup"><span data-stu-id="266ea-987">Examples</span></span>

<span data-ttu-id="266ea-988">L'esempio seguente mostra come usare uri, uriComponent e uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="266ea-988">The following example shows how to use uri, uriComponent, and uriComponentToString:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

<span data-ttu-id="266ea-989">L'output dell'esempio precedente con i valori predefiniti è:</span><span class="sxs-lookup"><span data-stu-id="266ea-989">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="266ea-990">Nome</span><span class="sxs-lookup"><span data-stu-id="266ea-990">Name</span></span> | <span data-ttu-id="266ea-991">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-991">Type</span></span> | <span data-ttu-id="266ea-992">Valore</span><span class="sxs-lookup"><span data-stu-id="266ea-992">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="266ea-993">uriOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-993">uriOutput</span></span> | <span data-ttu-id="266ea-994">String</span><span class="sxs-lookup"><span data-stu-id="266ea-994">String</span></span> | <span data-ttu-id="266ea-995">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="266ea-995">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="266ea-996">componentOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-996">componentOutput</span></span> | <span data-ttu-id="266ea-997">String</span><span class="sxs-lookup"><span data-stu-id="266ea-997">String</span></span> | <span data-ttu-id="266ea-998">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="266ea-998">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="266ea-999">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-999">toStringOutput</span></span> | <span data-ttu-id="266ea-1000">String</span><span class="sxs-lookup"><span data-stu-id="266ea-1000">String</span></span> | <span data-ttu-id="266ea-1001">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="266ea-1001">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


<a id="uricomponenttostring" />

## <a name="uricomponenttostring"></a><span data-ttu-id="266ea-1002">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="266ea-1002">uriComponentToString</span></span>
`uriComponentToString(uriEncodedString)`

<span data-ttu-id="266ea-1003">Restituisce una stringa di un valore URI codificato.</span><span class="sxs-lookup"><span data-stu-id="266ea-1003">Returns a string of a URI encoded value.</span></span>

### <a name="parameters"></a><span data-ttu-id="266ea-1004">Parametri</span><span class="sxs-lookup"><span data-stu-id="266ea-1004">Parameters</span></span>

| <span data-ttu-id="266ea-1005">Parametro</span><span class="sxs-lookup"><span data-stu-id="266ea-1005">Parameter</span></span> | <span data-ttu-id="266ea-1006">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="266ea-1006">Required</span></span> | <span data-ttu-id="266ea-1007">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-1007">Type</span></span> | <span data-ttu-id="266ea-1008">Descrizione</span><span class="sxs-lookup"><span data-stu-id="266ea-1008">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="266ea-1009">uriEncodedString</span><span class="sxs-lookup"><span data-stu-id="266ea-1009">uriEncodedString</span></span> |<span data-ttu-id="266ea-1010">Sì</span><span class="sxs-lookup"><span data-stu-id="266ea-1010">Yes</span></span> |<span data-ttu-id="266ea-1011">string</span><span class="sxs-lookup"><span data-stu-id="266ea-1011">string</span></span> |<span data-ttu-id="266ea-1012">Valore URI codificato da convertire in stringa.</span><span class="sxs-lookup"><span data-stu-id="266ea-1012">The URI encoded value to convert to a string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="266ea-1013">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="266ea-1013">Return value</span></span>

<span data-ttu-id="266ea-1014">Stringa decodificata del valore URI codificato.</span><span class="sxs-lookup"><span data-stu-id="266ea-1014">A decoded string of URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="266ea-1015">esempi</span><span class="sxs-lookup"><span data-stu-id="266ea-1015">Examples</span></span>

<span data-ttu-id="266ea-1016">L'esempio seguente mostra come usare uri, uriComponent e uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="266ea-1016">The following example shows how to use uri, uriComponent, and uriComponentToString:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

<span data-ttu-id="266ea-1017">L'output dell'esempio precedente con i valori predefiniti è:</span><span class="sxs-lookup"><span data-stu-id="266ea-1017">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="266ea-1018">Nome</span><span class="sxs-lookup"><span data-stu-id="266ea-1018">Name</span></span> | <span data-ttu-id="266ea-1019">Tipo</span><span class="sxs-lookup"><span data-stu-id="266ea-1019">Type</span></span> | <span data-ttu-id="266ea-1020">Valore</span><span class="sxs-lookup"><span data-stu-id="266ea-1020">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="266ea-1021">uriOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-1021">uriOutput</span></span> | <span data-ttu-id="266ea-1022">String</span><span class="sxs-lookup"><span data-stu-id="266ea-1022">String</span></span> | <span data-ttu-id="266ea-1023">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="266ea-1023">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="266ea-1024">componentOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-1024">componentOutput</span></span> | <span data-ttu-id="266ea-1025">String</span><span class="sxs-lookup"><span data-stu-id="266ea-1025">String</span></span> | <span data-ttu-id="266ea-1026">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="266ea-1026">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="266ea-1027">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="266ea-1027">toStringOutput</span></span> | <span data-ttu-id="266ea-1028">String</span><span class="sxs-lookup"><span data-stu-id="266ea-1028">String</span></span> | <span data-ttu-id="266ea-1029">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="266ea-1029">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


## <a name="next-steps"></a><span data-ttu-id="266ea-1030">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="266ea-1030">Next steps</span></span>
* <span data-ttu-id="266ea-1031">Per una descrizione delle sezioni in un modello di Azure Resource Manager, vedere [Creazione di modelli di Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="266ea-1031">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="266ea-1032">Per unire più modelli, vedere [Uso di modelli collegati con Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="266ea-1032">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="266ea-1033">Per eseguire un'iterazione di un numero di volte specificato durante la creazione di un tipo di risorsa, vedere [Creare più istanze di risorse in Gestione risorse di Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="266ea-1033">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="266ea-1034">Per informazioni su come distribuire il modello che è stato creato, vedere [Distribuire un'applicazione con un modello di Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="266ea-1034">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

