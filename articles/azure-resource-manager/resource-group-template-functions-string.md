---
title: funzioni di modello di gestione risorse aaaAzure - stringa | Documenti Microsoft
description: Viene descritto toouse funzioni hello in un toowork del modello di gestione risorse di Azure con le stringhe.
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
ms.openlocfilehash: 27f7f6a52cbe4e9915718184433e92ca92999346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="string-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="a7f47-103">Funzioni di stringa nei modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a7f47-103">String functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="a7f47-104">Gestione risorse offre hello funzioni per l'utilizzo con le stringhe seguenti:</span><span class="sxs-lookup"><span data-stu-id="a7f47-104">Resource Manager provides hello following functions for working with strings:</span></span>

* [<span data-ttu-id="a7f47-105">base64</span><span class="sxs-lookup"><span data-stu-id="a7f47-105">base64</span></span>](#base64)
* [<span data-ttu-id="a7f47-106">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="a7f47-106">base64ToJson</span></span>](#base64tojson)
* [<span data-ttu-id="a7f47-107">base64ToString</span><span class="sxs-lookup"><span data-stu-id="a7f47-107">base64ToString</span></span>](#base64tostring)
* [<span data-ttu-id="a7f47-108">concat</span><span class="sxs-lookup"><span data-stu-id="a7f47-108">concat</span></span>](#concat)
* [<span data-ttu-id="a7f47-109">contains</span><span class="sxs-lookup"><span data-stu-id="a7f47-109">contains</span></span>](#contains)
* [<span data-ttu-id="a7f47-110">dataUri</span><span class="sxs-lookup"><span data-stu-id="a7f47-110">dataUri</span></span>](#datauri)
* [<span data-ttu-id="a7f47-111">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="a7f47-111">dataUriToString</span></span>](#datauritostring)
* [<span data-ttu-id="a7f47-112">empty</span><span class="sxs-lookup"><span data-stu-id="a7f47-112">empty</span></span>](#empty)
* [<span data-ttu-id="a7f47-113">endsWith</span><span class="sxs-lookup"><span data-stu-id="a7f47-113">endsWith</span></span>](#endswith)
* [<span data-ttu-id="a7f47-114">first</span><span class="sxs-lookup"><span data-stu-id="a7f47-114">first</span></span>](#first)
* [<span data-ttu-id="a7f47-115">indexOf</span><span class="sxs-lookup"><span data-stu-id="a7f47-115">indexOf</span></span>](#indexof)
* [<span data-ttu-id="a7f47-116">last</span><span class="sxs-lookup"><span data-stu-id="a7f47-116">last</span></span>](#last)
* [<span data-ttu-id="a7f47-117">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="a7f47-117">lastIndexOf</span></span>](#lastindexof)
* [<span data-ttu-id="a7f47-118">length</span><span class="sxs-lookup"><span data-stu-id="a7f47-118">length</span></span>](#length)
* [<span data-ttu-id="a7f47-119">padLeft</span><span class="sxs-lookup"><span data-stu-id="a7f47-119">padLeft</span></span>](#padleft)
* [<span data-ttu-id="a7f47-120">replace</span><span class="sxs-lookup"><span data-stu-id="a7f47-120">replace</span></span>](#replace)
* [<span data-ttu-id="a7f47-121">skip</span><span class="sxs-lookup"><span data-stu-id="a7f47-121">skip</span></span>](#skip)
* [<span data-ttu-id="a7f47-122">split</span><span class="sxs-lookup"><span data-stu-id="a7f47-122">split</span></span>](#split)
* [<span data-ttu-id="a7f47-123">startsWith</span><span class="sxs-lookup"><span data-stu-id="a7f47-123">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="a7f47-124">string</span><span class="sxs-lookup"><span data-stu-id="a7f47-124">string</span></span>](#string)
* [<span data-ttu-id="a7f47-125">substring</span><span class="sxs-lookup"><span data-stu-id="a7f47-125">substring</span></span>](#substring)
* [<span data-ttu-id="a7f47-126">take</span><span class="sxs-lookup"><span data-stu-id="a7f47-126">take</span></span>](#take)
* [<span data-ttu-id="a7f47-127">toLower</span><span class="sxs-lookup"><span data-stu-id="a7f47-127">toLower</span></span>](#tolower)
* [<span data-ttu-id="a7f47-128">toUpper</span><span class="sxs-lookup"><span data-stu-id="a7f47-128">toUpper</span></span>](#toupper)
* [<span data-ttu-id="a7f47-129">Trim</span><span class="sxs-lookup"><span data-stu-id="a7f47-129">trim</span></span>](#trim)
* [<span data-ttu-id="a7f47-130">uniqueString</span><span class="sxs-lookup"><span data-stu-id="a7f47-130">uniqueString</span></span>](#uniquestring)
* [<span data-ttu-id="a7f47-131">Uri</span><span class="sxs-lookup"><span data-stu-id="a7f47-131">uri</span></span>](#uri)
* [<span data-ttu-id="a7f47-132">uriComponent</span><span class="sxs-lookup"><span data-stu-id="a7f47-132">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="a7f47-133">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="a7f47-133">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)

<a id="base64" />

## <a name="base64"></a><span data-ttu-id="a7f47-134">base64</span><span class="sxs-lookup"><span data-stu-id="a7f47-134">base64</span></span>
`base64(inputString)`

<span data-ttu-id="a7f47-135">Restituisce hello rappresentazione base64 della stringa di input hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-135">Returns hello base64 representation of hello input string.</span></span>

### <a name="parameters"></a><span data-ttu-id="a7f47-136">parameters</span><span class="sxs-lookup"><span data-stu-id="a7f47-136">Parameters</span></span>

| <span data-ttu-id="a7f47-137">Parametro</span><span class="sxs-lookup"><span data-stu-id="a7f47-137">Parameter</span></span> | <span data-ttu-id="a7f47-138">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a7f47-138">Required</span></span> | <span data-ttu-id="a7f47-139">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-139">Type</span></span> | <span data-ttu-id="a7f47-140">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7f47-140">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a7f47-141">inputString</span><span class="sxs-lookup"><span data-stu-id="a7f47-141">inputString</span></span> |<span data-ttu-id="a7f47-142">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-142">Yes</span></span> |<span data-ttu-id="a7f47-143">string</span><span class="sxs-lookup"><span data-stu-id="a7f47-143">string</span></span> |<span data-ttu-id="a7f47-144">Hello valore tooreturn come rappresentazione base64.</span><span class="sxs-lookup"><span data-stu-id="a7f47-144">hello value tooreturn as a base64 representation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a7f47-145">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="a7f47-145">Return value</span></span>

<span data-ttu-id="a7f47-146">Stringa contenente una rappresentazione base64 hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-146">A string containing hello base64 representation.</span></span>

### <a name="examples"></a><span data-ttu-id="a7f47-147">esempi</span><span class="sxs-lookup"><span data-stu-id="a7f47-147">Examples</span></span>

<span data-ttu-id="a7f47-148">Hello di esempio seguente viene illustrato come toouse hello funzione base64.</span><span class="sxs-lookup"><span data-stu-id="a7f47-148">hello following example shows how toouse hello base64 function.</span></span>

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

<span data-ttu-id="a7f47-149">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="a7f47-149">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a7f47-150">Nome</span><span class="sxs-lookup"><span data-stu-id="a7f47-150">Name</span></span> | <span data-ttu-id="a7f47-151">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-151">Type</span></span> | <span data-ttu-id="a7f47-152">Valore</span><span class="sxs-lookup"><span data-stu-id="a7f47-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a7f47-153">base64Output</span><span class="sxs-lookup"><span data-stu-id="a7f47-153">base64Output</span></span> | <span data-ttu-id="a7f47-154">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-154">String</span></span> | <span data-ttu-id="a7f47-155">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="a7f47-155">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="a7f47-156">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-156">toStringOutput</span></span> | <span data-ttu-id="a7f47-157">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-157">String</span></span> | <span data-ttu-id="a7f47-158">one, two, three</span><span class="sxs-lookup"><span data-stu-id="a7f47-158">one, two, three</span></span> |
| <span data-ttu-id="a7f47-159">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-159">toJsonOutput</span></span> | <span data-ttu-id="a7f47-160">Oggetto</span><span class="sxs-lookup"><span data-stu-id="a7f47-160">Object</span></span> | <span data-ttu-id="a7f47-161">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="a7f47-161">{"one": "a", "two": "b"}</span></span> |

<a id="base64tojson" />

## <a name="base64tojson"></a><span data-ttu-id="a7f47-162">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="a7f47-162">base64ToJson</span></span>
`base64tojson`

<span data-ttu-id="a7f47-163">Converte un oggetto JSON tooa rappresentazione base64.</span><span class="sxs-lookup"><span data-stu-id="a7f47-163">Converts a base64 representation tooa JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="a7f47-164">parameters</span><span class="sxs-lookup"><span data-stu-id="a7f47-164">Parameters</span></span>

| <span data-ttu-id="a7f47-165">Parametro</span><span class="sxs-lookup"><span data-stu-id="a7f47-165">Parameter</span></span> | <span data-ttu-id="a7f47-166">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a7f47-166">Required</span></span> | <span data-ttu-id="a7f47-167">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-167">Type</span></span> | <span data-ttu-id="a7f47-168">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7f47-168">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a7f47-169">base64Value</span><span class="sxs-lookup"><span data-stu-id="a7f47-169">base64Value</span></span> |<span data-ttu-id="a7f47-170">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-170">Yes</span></span> |<span data-ttu-id="a7f47-171">string</span><span class="sxs-lookup"><span data-stu-id="a7f47-171">string</span></span> |<span data-ttu-id="a7f47-172">Hello base64 rappresentazione tooconvert tooa oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="a7f47-172">hello base64 representation tooconvert tooa JSON object.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a7f47-173">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="a7f47-173">Return value</span></span>

<span data-ttu-id="a7f47-174">Oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="a7f47-174">A JSON object.</span></span>

### <a name="examples"></a><span data-ttu-id="a7f47-175">esempi</span><span class="sxs-lookup"><span data-stu-id="a7f47-175">Examples</span></span>

<span data-ttu-id="a7f47-176">Hello seguente utilizza hello base64ToJson funzione tooconvert un valore base64:</span><span class="sxs-lookup"><span data-stu-id="a7f47-176">hello following example uses hello base64ToJson function tooconvert a base64 value:</span></span>

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

<span data-ttu-id="a7f47-177">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="a7f47-177">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a7f47-178">Nome</span><span class="sxs-lookup"><span data-stu-id="a7f47-178">Name</span></span> | <span data-ttu-id="a7f47-179">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-179">Type</span></span> | <span data-ttu-id="a7f47-180">Valore</span><span class="sxs-lookup"><span data-stu-id="a7f47-180">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a7f47-181">base64Output</span><span class="sxs-lookup"><span data-stu-id="a7f47-181">base64Output</span></span> | <span data-ttu-id="a7f47-182">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-182">String</span></span> | <span data-ttu-id="a7f47-183">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="a7f47-183">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="a7f47-184">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-184">toStringOutput</span></span> | <span data-ttu-id="a7f47-185">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-185">String</span></span> | <span data-ttu-id="a7f47-186">one, two, three</span><span class="sxs-lookup"><span data-stu-id="a7f47-186">one, two, three</span></span> |
| <span data-ttu-id="a7f47-187">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-187">toJsonOutput</span></span> | <span data-ttu-id="a7f47-188">Oggetto</span><span class="sxs-lookup"><span data-stu-id="a7f47-188">Object</span></span> | <span data-ttu-id="a7f47-189">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="a7f47-189">{"one": "a", "two": "b"}</span></span> |

<a id="base64tostring" />

## <a name="base64tostring"></a><span data-ttu-id="a7f47-190">base64ToString</span><span class="sxs-lookup"><span data-stu-id="a7f47-190">base64ToString</span></span>
`base64ToString(base64Value)`

<span data-ttu-id="a7f47-191">Converte una stringa di tooa rappresentazione base 64.</span><span class="sxs-lookup"><span data-stu-id="a7f47-191">Converts a base64 representation tooa string.</span></span>

### <a name="parameters"></a><span data-ttu-id="a7f47-192">parameters</span><span class="sxs-lookup"><span data-stu-id="a7f47-192">Parameters</span></span>

| <span data-ttu-id="a7f47-193">Parametro</span><span class="sxs-lookup"><span data-stu-id="a7f47-193">Parameter</span></span> | <span data-ttu-id="a7f47-194">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a7f47-194">Required</span></span> | <span data-ttu-id="a7f47-195">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-195">Type</span></span> | <span data-ttu-id="a7f47-196">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7f47-196">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a7f47-197">base64Value</span><span class="sxs-lookup"><span data-stu-id="a7f47-197">base64Value</span></span> |<span data-ttu-id="a7f47-198">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-198">Yes</span></span> |<span data-ttu-id="a7f47-199">string</span><span class="sxs-lookup"><span data-stu-id="a7f47-199">string</span></span> |<span data-ttu-id="a7f47-200">stringa di tooa tooconvert rappresentazione base64 Hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-200">hello base64 representation tooconvert tooa string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a7f47-201">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="a7f47-201">Return value</span></span>

<span data-ttu-id="a7f47-202">Valore base64 di convertire una stringa di hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-202">A string of hello converted base64 value.</span></span>

### <a name="examples"></a><span data-ttu-id="a7f47-203">esempi</span><span class="sxs-lookup"><span data-stu-id="a7f47-203">Examples</span></span>

<span data-ttu-id="a7f47-204">Hello seguente utilizza hello base64ToString funzione tooconvert un valore base64:</span><span class="sxs-lookup"><span data-stu-id="a7f47-204">hello following example uses hello base64ToString function tooconvert a base64 value:</span></span>

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

<span data-ttu-id="a7f47-205">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="a7f47-205">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a7f47-206">Nome</span><span class="sxs-lookup"><span data-stu-id="a7f47-206">Name</span></span> | <span data-ttu-id="a7f47-207">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-207">Type</span></span> | <span data-ttu-id="a7f47-208">Valore</span><span class="sxs-lookup"><span data-stu-id="a7f47-208">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a7f47-209">base64Output</span><span class="sxs-lookup"><span data-stu-id="a7f47-209">base64Output</span></span> | <span data-ttu-id="a7f47-210">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-210">String</span></span> | <span data-ttu-id="a7f47-211">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="a7f47-211">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="a7f47-212">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-212">toStringOutput</span></span> | <span data-ttu-id="a7f47-213">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-213">String</span></span> | <span data-ttu-id="a7f47-214">one, two, three</span><span class="sxs-lookup"><span data-stu-id="a7f47-214">one, two, three</span></span> |
| <span data-ttu-id="a7f47-215">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-215">toJsonOutput</span></span> | <span data-ttu-id="a7f47-216">Oggetto</span><span class="sxs-lookup"><span data-stu-id="a7f47-216">Object</span></span> | <span data-ttu-id="a7f47-217">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="a7f47-217">{"one": "a", "two": "b"}</span></span> |



<a id="concat" />

## <a name="concat"></a><span data-ttu-id="a7f47-218">concat</span><span class="sxs-lookup"><span data-stu-id="a7f47-218">concat</span></span>
`concat (arg1, arg2, arg3, ...)`

<span data-ttu-id="a7f47-219">Consente di combinare più valori di stringa e restituisce la stringa concatenata hello, o combina più array di e matrice hello concatenato.</span><span class="sxs-lookup"><span data-stu-id="a7f47-219">Combines multiple string values and returns hello concatenated string, or combines multiple arrays and returns hello concatenated array.</span></span>

### <a name="parameters"></a><span data-ttu-id="a7f47-220">parameters</span><span class="sxs-lookup"><span data-stu-id="a7f47-220">Parameters</span></span>

| <span data-ttu-id="a7f47-221">Parametro</span><span class="sxs-lookup"><span data-stu-id="a7f47-221">Parameter</span></span> | <span data-ttu-id="a7f47-222">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a7f47-222">Required</span></span> | <span data-ttu-id="a7f47-223">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-223">Type</span></span> | <span data-ttu-id="a7f47-224">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7f47-224">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a7f47-225">arg1</span><span class="sxs-lookup"><span data-stu-id="a7f47-225">arg1</span></span> |<span data-ttu-id="a7f47-226">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-226">Yes</span></span> |<span data-ttu-id="a7f47-227">Stringa o matrice</span><span class="sxs-lookup"><span data-stu-id="a7f47-227">string or array</span></span> |<span data-ttu-id="a7f47-228">primo valore Hello per la concatenazione.</span><span class="sxs-lookup"><span data-stu-id="a7f47-228">hello first value for concatenation.</span></span> |
| <span data-ttu-id="a7f47-229">argomenti aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="a7f47-229">additional arguments</span></span> |<span data-ttu-id="a7f47-230">No</span><span class="sxs-lookup"><span data-stu-id="a7f47-230">No</span></span> |<span data-ttu-id="a7f47-231">string</span><span class="sxs-lookup"><span data-stu-id="a7f47-231">string</span></span> |<span data-ttu-id="a7f47-232">Altri valori in ordine sequenziale per la concatenazione.</span><span class="sxs-lookup"><span data-stu-id="a7f47-232">Additional values in sequential order for concatenation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a7f47-233">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="a7f47-233">Return value</span></span>
<span data-ttu-id="a7f47-234">Stringa o matrice di valori concatenati.</span><span class="sxs-lookup"><span data-stu-id="a7f47-234">A string or array of concatenated values.</span></span>

### <a name="examples"></a><span data-ttu-id="a7f47-235">esempi</span><span class="sxs-lookup"><span data-stu-id="a7f47-235">Examples</span></span>

<span data-ttu-id="a7f47-236">Hello di esempio seguente viene illustrato come toocombine due valori stringa e restituire una stringa concatenata.</span><span class="sxs-lookup"><span data-stu-id="a7f47-236">hello following example shows how toocombine two string values and return a concatenated string.</span></span>

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

<span data-ttu-id="a7f47-237">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="a7f47-237">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a7f47-238">Nome</span><span class="sxs-lookup"><span data-stu-id="a7f47-238">Name</span></span> | <span data-ttu-id="a7f47-239">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-239">Type</span></span> | <span data-ttu-id="a7f47-240">Valore</span><span class="sxs-lookup"><span data-stu-id="a7f47-240">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a7f47-241">concatOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-241">concatOutput</span></span> | <span data-ttu-id="a7f47-242">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-242">String</span></span> | <span data-ttu-id="a7f47-243">prefix-5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="a7f47-243">prefix-5yj4yjf5mbg72</span></span> |

<span data-ttu-id="a7f47-244">Hello di esempio seguente viene illustrato come toocombine due matrici.</span><span class="sxs-lookup"><span data-stu-id="a7f47-244">hello following example shows how toocombine two arrays.</span></span>

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

<span data-ttu-id="a7f47-245">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="a7f47-245">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a7f47-246">Nome</span><span class="sxs-lookup"><span data-stu-id="a7f47-246">Name</span></span> | <span data-ttu-id="a7f47-247">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-247">Type</span></span> | <span data-ttu-id="a7f47-248">Valore</span><span class="sxs-lookup"><span data-stu-id="a7f47-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a7f47-249">return</span><span class="sxs-lookup"><span data-stu-id="a7f47-249">return</span></span> | <span data-ttu-id="a7f47-250">Array</span><span class="sxs-lookup"><span data-stu-id="a7f47-250">Array</span></span> | <span data-ttu-id="a7f47-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="a7f47-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="a7f47-252">contains</span><span class="sxs-lookup"><span data-stu-id="a7f47-252">contains</span></span>
`contains (container, itemToFind)`

<span data-ttu-id="a7f47-253">Verifica se una matrice contiene un valore, se un oggetto contiene una chiave o se una stringa contiene una sottostringa.</span><span class="sxs-lookup"><span data-stu-id="a7f47-253">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="a7f47-254">Parametri</span><span class="sxs-lookup"><span data-stu-id="a7f47-254">Parameters</span></span>

| <span data-ttu-id="a7f47-255">Parametro</span><span class="sxs-lookup"><span data-stu-id="a7f47-255">Parameter</span></span> | <span data-ttu-id="a7f47-256">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a7f47-256">Required</span></span> | <span data-ttu-id="a7f47-257">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-257">Type</span></span> | <span data-ttu-id="a7f47-258">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7f47-258">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a7f47-259">Contenitore</span><span class="sxs-lookup"><span data-stu-id="a7f47-259">container</span></span> |<span data-ttu-id="a7f47-260">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-260">Yes</span></span> |<span data-ttu-id="a7f47-261">matrice, oggetto o stringa</span><span class="sxs-lookup"><span data-stu-id="a7f47-261">array, object, or string</span></span> |<span data-ttu-id="a7f47-262">valore di Hello contenente toofind valore hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-262">hello value that contains hello value toofind.</span></span> |
| <span data-ttu-id="a7f47-263">itemToFind</span><span class="sxs-lookup"><span data-stu-id="a7f47-263">itemToFind</span></span> |<span data-ttu-id="a7f47-264">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-264">Yes</span></span> |<span data-ttu-id="a7f47-265">stringa o numero intero</span><span class="sxs-lookup"><span data-stu-id="a7f47-265">string or int</span></span> |<span data-ttu-id="a7f47-266">toofind valore Hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-266">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a7f47-267">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="a7f47-267">Return value</span></span>

<span data-ttu-id="a7f47-268">**True** se l'elemento hello è stato trovato; in caso contrario, **False**.</span><span class="sxs-lookup"><span data-stu-id="a7f47-268">**True** if hello item is found; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="a7f47-269">esempi</span><span class="sxs-lookup"><span data-stu-id="a7f47-269">Examples</span></span>

<span data-ttu-id="a7f47-270">Hello esempio seguente viene illustrato come toouse contiene con tipi diversi:</span><span class="sxs-lookup"><span data-stu-id="a7f47-270">hello following example shows how toouse contains with different types:</span></span>

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

<span data-ttu-id="a7f47-271">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="a7f47-271">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a7f47-272">Nome</span><span class="sxs-lookup"><span data-stu-id="a7f47-272">Name</span></span> | <span data-ttu-id="a7f47-273">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-273">Type</span></span> | <span data-ttu-id="a7f47-274">Valore</span><span class="sxs-lookup"><span data-stu-id="a7f47-274">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a7f47-275">stringTrue</span><span class="sxs-lookup"><span data-stu-id="a7f47-275">stringTrue</span></span> | <span data-ttu-id="a7f47-276">Booleano</span><span class="sxs-lookup"><span data-stu-id="a7f47-276">Bool</span></span> | <span data-ttu-id="a7f47-277">True </span><span class="sxs-lookup"><span data-stu-id="a7f47-277">True</span></span> |
| <span data-ttu-id="a7f47-278">stringFalse</span><span class="sxs-lookup"><span data-stu-id="a7f47-278">stringFalse</span></span> | <span data-ttu-id="a7f47-279">Booleano</span><span class="sxs-lookup"><span data-stu-id="a7f47-279">Bool</span></span> | <span data-ttu-id="a7f47-280">False</span><span class="sxs-lookup"><span data-stu-id="a7f47-280">False</span></span> |
| <span data-ttu-id="a7f47-281">objectTrue</span><span class="sxs-lookup"><span data-stu-id="a7f47-281">objectTrue</span></span> | <span data-ttu-id="a7f47-282">Booleano</span><span class="sxs-lookup"><span data-stu-id="a7f47-282">Bool</span></span> | <span data-ttu-id="a7f47-283">True </span><span class="sxs-lookup"><span data-stu-id="a7f47-283">True</span></span> |
| <span data-ttu-id="a7f47-284">objectFalse</span><span class="sxs-lookup"><span data-stu-id="a7f47-284">objectFalse</span></span> | <span data-ttu-id="a7f47-285">Booleano</span><span class="sxs-lookup"><span data-stu-id="a7f47-285">Bool</span></span> | <span data-ttu-id="a7f47-286">False</span><span class="sxs-lookup"><span data-stu-id="a7f47-286">False</span></span> |
| <span data-ttu-id="a7f47-287">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="a7f47-287">arrayTrue</span></span> | <span data-ttu-id="a7f47-288">Booleano</span><span class="sxs-lookup"><span data-stu-id="a7f47-288">Bool</span></span> | <span data-ttu-id="a7f47-289">True </span><span class="sxs-lookup"><span data-stu-id="a7f47-289">True</span></span> |
| <span data-ttu-id="a7f47-290">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="a7f47-290">arrayFalse</span></span> | <span data-ttu-id="a7f47-291">Booleano</span><span class="sxs-lookup"><span data-stu-id="a7f47-291">Bool</span></span> | <span data-ttu-id="a7f47-292">False</span><span class="sxs-lookup"><span data-stu-id="a7f47-292">False</span></span> |

<a id="datauri" />

## <a name="datauri"></a><span data-ttu-id="a7f47-293">dataUri</span><span class="sxs-lookup"><span data-stu-id="a7f47-293">dataUri</span></span>
`dataUri(stringToConvert)`

<span data-ttu-id="a7f47-294">Converte i dati tooa valore URI.</span><span class="sxs-lookup"><span data-stu-id="a7f47-294">Converts a value tooa data URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="a7f47-295">parameters</span><span class="sxs-lookup"><span data-stu-id="a7f47-295">Parameters</span></span>

| <span data-ttu-id="a7f47-296">Parametro</span><span class="sxs-lookup"><span data-stu-id="a7f47-296">Parameter</span></span> | <span data-ttu-id="a7f47-297">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a7f47-297">Required</span></span> | <span data-ttu-id="a7f47-298">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-298">Type</span></span> | <span data-ttu-id="a7f47-299">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7f47-299">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a7f47-300">stringToConvert</span><span class="sxs-lookup"><span data-stu-id="a7f47-300">stringToConvert</span></span> |<span data-ttu-id="a7f47-301">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-301">Yes</span></span> |<span data-ttu-id="a7f47-302">string</span><span class="sxs-lookup"><span data-stu-id="a7f47-302">string</span></span> |<span data-ttu-id="a7f47-303">Hello tooconvert tooa dati valore URI.</span><span class="sxs-lookup"><span data-stu-id="a7f47-303">hello value tooconvert tooa data URI.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a7f47-304">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="a7f47-304">Return value</span></span>

<span data-ttu-id="a7f47-305">Stringa formattata come URI di dati.</span><span class="sxs-lookup"><span data-stu-id="a7f47-305">A string formatted as a data URI.</span></span>

### <a name="examples"></a><span data-ttu-id="a7f47-306">esempi</span><span class="sxs-lookup"><span data-stu-id="a7f47-306">Examples</span></span>

<span data-ttu-id="a7f47-307">Hello di esempio seguente converte i dati tooa valore URI e converte i dati stringa tooa URI:</span><span class="sxs-lookup"><span data-stu-id="a7f47-307">hello following example converts a value tooa data URI, and converts a data URI tooa string:</span></span>

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

<span data-ttu-id="a7f47-308">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="a7f47-308">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a7f47-309">Nome</span><span class="sxs-lookup"><span data-stu-id="a7f47-309">Name</span></span> | <span data-ttu-id="a7f47-310">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-310">Type</span></span> | <span data-ttu-id="a7f47-311">Valore</span><span class="sxs-lookup"><span data-stu-id="a7f47-311">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a7f47-312">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-312">dataUriOutput</span></span> | <span data-ttu-id="a7f47-313">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-313">String</span></span> | <span data-ttu-id="a7f47-314">data:text/plain;charset=utf8;base64,SGVsbG8=</span><span class="sxs-lookup"><span data-stu-id="a7f47-314">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="a7f47-315">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-315">toStringOutput</span></span> | <span data-ttu-id="a7f47-316">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-316">String</span></span> | <span data-ttu-id="a7f47-317">Hello, World!</span><span class="sxs-lookup"><span data-stu-id="a7f47-317">Hello, World!</span></span> |

<a id="datauritostring" />

## <a name="datauritostring"></a><span data-ttu-id="a7f47-318">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="a7f47-318">dataUriToString</span></span>
`dataUriToString(dataUriToConvert)`

<span data-ttu-id="a7f47-319">Converte un URI di dati in un formato stringa del valore tooa.</span><span class="sxs-lookup"><span data-stu-id="a7f47-319">Converts a data URI formatted value tooa string.</span></span>

### <a name="parameters"></a><span data-ttu-id="a7f47-320">parameters</span><span class="sxs-lookup"><span data-stu-id="a7f47-320">Parameters</span></span>

| <span data-ttu-id="a7f47-321">Parametro</span><span class="sxs-lookup"><span data-stu-id="a7f47-321">Parameter</span></span> | <span data-ttu-id="a7f47-322">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a7f47-322">Required</span></span> | <span data-ttu-id="a7f47-323">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-323">Type</span></span> | <span data-ttu-id="a7f47-324">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7f47-324">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a7f47-325">dataUriToConvert</span><span class="sxs-lookup"><span data-stu-id="a7f47-325">dataUriToConvert</span></span> |<span data-ttu-id="a7f47-326">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-326">Yes</span></span> |<span data-ttu-id="a7f47-327">string</span><span class="sxs-lookup"><span data-stu-id="a7f47-327">string</span></span> |<span data-ttu-id="a7f47-328">dati Hello tooconvert valore URI.</span><span class="sxs-lookup"><span data-stu-id="a7f47-328">hello data URI value tooconvert.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a7f47-329">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="a7f47-329">Return value</span></span>

<span data-ttu-id="a7f47-330">Stringa contenente hello valore convertito.</span><span class="sxs-lookup"><span data-stu-id="a7f47-330">A string containing hello converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="a7f47-331">esempi</span><span class="sxs-lookup"><span data-stu-id="a7f47-331">Examples</span></span>

<span data-ttu-id="a7f47-332">Hello di esempio seguente converte i dati tooa valore URI e converte i dati stringa tooa URI:</span><span class="sxs-lookup"><span data-stu-id="a7f47-332">hello following example converts a value tooa data URI, and converts a data URI tooa string:</span></span>

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

<span data-ttu-id="a7f47-333">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="a7f47-333">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a7f47-334">Nome</span><span class="sxs-lookup"><span data-stu-id="a7f47-334">Name</span></span> | <span data-ttu-id="a7f47-335">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-335">Type</span></span> | <span data-ttu-id="a7f47-336">Valore</span><span class="sxs-lookup"><span data-stu-id="a7f47-336">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a7f47-337">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-337">dataUriOutput</span></span> | <span data-ttu-id="a7f47-338">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-338">String</span></span> | <span data-ttu-id="a7f47-339">data:text/plain;charset=utf8;base64,SGVsbG8=</span><span class="sxs-lookup"><span data-stu-id="a7f47-339">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="a7f47-340">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-340">toStringOutput</span></span> | <span data-ttu-id="a7f47-341">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-341">String</span></span> | <span data-ttu-id="a7f47-342">Hello, World!</span><span class="sxs-lookup"><span data-stu-id="a7f47-342">Hello, World!</span></span> |

<a id="empty" /> 

## <a name="empty"></a><span data-ttu-id="a7f47-343">empty</span><span class="sxs-lookup"><span data-stu-id="a7f47-343">empty</span></span>
`empty(itemToTest)`

<span data-ttu-id="a7f47-344">Determina se una matrice, un oggetto o una stringa sono vuoti.</span><span class="sxs-lookup"><span data-stu-id="a7f47-344">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="a7f47-345">Parametri</span><span class="sxs-lookup"><span data-stu-id="a7f47-345">Parameters</span></span>

| <span data-ttu-id="a7f47-346">Parametro</span><span class="sxs-lookup"><span data-stu-id="a7f47-346">Parameter</span></span> | <span data-ttu-id="a7f47-347">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a7f47-347">Required</span></span> | <span data-ttu-id="a7f47-348">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-348">Type</span></span> | <span data-ttu-id="a7f47-349">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7f47-349">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a7f47-350">itemToTest</span><span class="sxs-lookup"><span data-stu-id="a7f47-350">itemToTest</span></span> |<span data-ttu-id="a7f47-351">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-351">Yes</span></span> |<span data-ttu-id="a7f47-352">matrice, oggetto o stringa</span><span class="sxs-lookup"><span data-stu-id="a7f47-352">array, object, or string</span></span> |<span data-ttu-id="a7f47-353">Hello toocheck valore se è vuota.</span><span class="sxs-lookup"><span data-stu-id="a7f47-353">hello value toocheck if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a7f47-354">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="a7f47-354">Return value</span></span>

<span data-ttu-id="a7f47-355">Restituisce **True** se il valore di hello è vuota; in caso contrario, **False**.</span><span class="sxs-lookup"><span data-stu-id="a7f47-355">Returns **True** if hello value is empty; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="a7f47-356">esempi</span><span class="sxs-lookup"><span data-stu-id="a7f47-356">Examples</span></span>

<span data-ttu-id="a7f47-357">Hello di esempio seguente controlla se una matrice, un oggetto e una stringa sono vuote.</span><span class="sxs-lookup"><span data-stu-id="a7f47-357">hello following example checks whether an array, object, and string are empty.</span></span>

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

<span data-ttu-id="a7f47-358">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="a7f47-358">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a7f47-359">Nome</span><span class="sxs-lookup"><span data-stu-id="a7f47-359">Name</span></span> | <span data-ttu-id="a7f47-360">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-360">Type</span></span> | <span data-ttu-id="a7f47-361">Valore</span><span class="sxs-lookup"><span data-stu-id="a7f47-361">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a7f47-362">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="a7f47-362">arrayEmpty</span></span> | <span data-ttu-id="a7f47-363">Booleano</span><span class="sxs-lookup"><span data-stu-id="a7f47-363">Bool</span></span> | <span data-ttu-id="a7f47-364">True </span><span class="sxs-lookup"><span data-stu-id="a7f47-364">True</span></span> |
| <span data-ttu-id="a7f47-365">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="a7f47-365">objectEmpty</span></span> | <span data-ttu-id="a7f47-366">Booleano</span><span class="sxs-lookup"><span data-stu-id="a7f47-366">Bool</span></span> | <span data-ttu-id="a7f47-367">True </span><span class="sxs-lookup"><span data-stu-id="a7f47-367">True</span></span> |
| <span data-ttu-id="a7f47-368">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="a7f47-368">stringEmpty</span></span> | <span data-ttu-id="a7f47-369">Booleano</span><span class="sxs-lookup"><span data-stu-id="a7f47-369">Bool</span></span> | <span data-ttu-id="a7f47-370">True </span><span class="sxs-lookup"><span data-stu-id="a7f47-370">True</span></span> |

<a id="endswith" />

## <a name="endswith"></a><span data-ttu-id="a7f47-371">endsWith</span><span class="sxs-lookup"><span data-stu-id="a7f47-371">endsWith</span></span>
`endsWith(stringToSearch, stringToFind)`

<span data-ttu-id="a7f47-372">Determina se una stringa termina con un valore.</span><span class="sxs-lookup"><span data-stu-id="a7f47-372">Determines whether a string ends with a value.</span></span> <span data-ttu-id="a7f47-373">confronto di Hello è tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="a7f47-373">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="a7f47-374">parameters</span><span class="sxs-lookup"><span data-stu-id="a7f47-374">Parameters</span></span>

| <span data-ttu-id="a7f47-375">Parametro</span><span class="sxs-lookup"><span data-stu-id="a7f47-375">Parameter</span></span> | <span data-ttu-id="a7f47-376">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a7f47-376">Required</span></span> | <span data-ttu-id="a7f47-377">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-377">Type</span></span> | <span data-ttu-id="a7f47-378">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7f47-378">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a7f47-379">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="a7f47-379">stringToSearch</span></span> |<span data-ttu-id="a7f47-380">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-380">Yes</span></span> |<span data-ttu-id="a7f47-381">string</span><span class="sxs-lookup"><span data-stu-id="a7f47-381">string</span></span> |<span data-ttu-id="a7f47-382">valore di Hello contenente toofind elemento hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-382">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="a7f47-383">stringToFind</span><span class="sxs-lookup"><span data-stu-id="a7f47-383">stringToFind</span></span> |<span data-ttu-id="a7f47-384">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-384">Yes</span></span> |<span data-ttu-id="a7f47-385">string</span><span class="sxs-lookup"><span data-stu-id="a7f47-385">string</span></span> |<span data-ttu-id="a7f47-386">toofind valore Hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-386">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a7f47-387">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="a7f47-387">Return value</span></span>

<span data-ttu-id="a7f47-388">**True** se hello ultimo o più caratteri della stringa hello corrisponde a quello hello; in caso contrario, **False**.</span><span class="sxs-lookup"><span data-stu-id="a7f47-388">**True** if hello last character or characters of hello string match hello value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="a7f47-389">esempi</span><span class="sxs-lookup"><span data-stu-id="a7f47-389">Examples</span></span>

<span data-ttu-id="a7f47-390">Hello di esempio seguente viene illustrato come toouse hello startsWith ed endsWith funzioni:</span><span class="sxs-lookup"><span data-stu-id="a7f47-390">hello following example shows how toouse hello startsWith and endsWith functions:</span></span>

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

<span data-ttu-id="a7f47-391">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="a7f47-391">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a7f47-392">Nome</span><span class="sxs-lookup"><span data-stu-id="a7f47-392">Name</span></span> | <span data-ttu-id="a7f47-393">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-393">Type</span></span> | <span data-ttu-id="a7f47-394">Valore</span><span class="sxs-lookup"><span data-stu-id="a7f47-394">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a7f47-395">startsTrue</span><span class="sxs-lookup"><span data-stu-id="a7f47-395">startsTrue</span></span> | <span data-ttu-id="a7f47-396">Booleano</span><span class="sxs-lookup"><span data-stu-id="a7f47-396">Bool</span></span> | <span data-ttu-id="a7f47-397">True </span><span class="sxs-lookup"><span data-stu-id="a7f47-397">True</span></span> |
| <span data-ttu-id="a7f47-398">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="a7f47-398">startsCapTrue</span></span> | <span data-ttu-id="a7f47-399">Booleano</span><span class="sxs-lookup"><span data-stu-id="a7f47-399">Bool</span></span> | <span data-ttu-id="a7f47-400">True </span><span class="sxs-lookup"><span data-stu-id="a7f47-400">True</span></span> |
| <span data-ttu-id="a7f47-401">startsFalse</span><span class="sxs-lookup"><span data-stu-id="a7f47-401">startsFalse</span></span> | <span data-ttu-id="a7f47-402">Booleano</span><span class="sxs-lookup"><span data-stu-id="a7f47-402">Bool</span></span> | <span data-ttu-id="a7f47-403">False</span><span class="sxs-lookup"><span data-stu-id="a7f47-403">False</span></span> |
| <span data-ttu-id="a7f47-404">endsTrue</span><span class="sxs-lookup"><span data-stu-id="a7f47-404">endsTrue</span></span> | <span data-ttu-id="a7f47-405">Booleano</span><span class="sxs-lookup"><span data-stu-id="a7f47-405">Bool</span></span> | <span data-ttu-id="a7f47-406">True </span><span class="sxs-lookup"><span data-stu-id="a7f47-406">True</span></span> |
| <span data-ttu-id="a7f47-407">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="a7f47-407">endsCapTrue</span></span> | <span data-ttu-id="a7f47-408">Booleano</span><span class="sxs-lookup"><span data-stu-id="a7f47-408">Bool</span></span> | <span data-ttu-id="a7f47-409">True </span><span class="sxs-lookup"><span data-stu-id="a7f47-409">True</span></span> |
| <span data-ttu-id="a7f47-410">endsFalse</span><span class="sxs-lookup"><span data-stu-id="a7f47-410">endsFalse</span></span> | <span data-ttu-id="a7f47-411">Booleano</span><span class="sxs-lookup"><span data-stu-id="a7f47-411">Bool</span></span> | <span data-ttu-id="a7f47-412">False</span><span class="sxs-lookup"><span data-stu-id="a7f47-412">False</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="a7f47-413">first</span><span class="sxs-lookup"><span data-stu-id="a7f47-413">first</span></span>
`first(arg1)`

<span data-ttu-id="a7f47-414">Restituisce hello primo carattere della stringa hello o primo elemento della matrice hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-414">Returns hello first character of hello string, or first element of hello array.</span></span>

### <a name="parameters"></a><span data-ttu-id="a7f47-415">parameters</span><span class="sxs-lookup"><span data-stu-id="a7f47-415">Parameters</span></span>

| <span data-ttu-id="a7f47-416">Parametro</span><span class="sxs-lookup"><span data-stu-id="a7f47-416">Parameter</span></span> | <span data-ttu-id="a7f47-417">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a7f47-417">Required</span></span> | <span data-ttu-id="a7f47-418">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-418">Type</span></span> | <span data-ttu-id="a7f47-419">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7f47-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a7f47-420">arg1</span><span class="sxs-lookup"><span data-stu-id="a7f47-420">arg1</span></span> |<span data-ttu-id="a7f47-421">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-421">Yes</span></span> |<span data-ttu-id="a7f47-422">stringa o matrice</span><span class="sxs-lookup"><span data-stu-id="a7f47-422">array or string</span></span> |<span data-ttu-id="a7f47-423">carattere o Hello valore tooretrieve hello primo elemento.</span><span class="sxs-lookup"><span data-stu-id="a7f47-423">hello value tooretrieve hello first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a7f47-424">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="a7f47-424">Return value</span></span>

<span data-ttu-id="a7f47-425">Una stringa di caratteri hello o il tipo di hello (string, int, matrice o oggetto) del primo elemento di hello in una matrice.</span><span class="sxs-lookup"><span data-stu-id="a7f47-425">A string of hello first character, or hello type (string, int, array, or object) of hello first element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="a7f47-426">esempi</span><span class="sxs-lookup"><span data-stu-id="a7f47-426">Examples</span></span>

<span data-ttu-id="a7f47-427">Hello esempio seguente viene illustrato come toouse hello prima funzione con una matrice e una stringa.</span><span class="sxs-lookup"><span data-stu-id="a7f47-427">hello following example shows how toouse hello first function with an array and string.</span></span>

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

<span data-ttu-id="a7f47-428">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="a7f47-428">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a7f47-429">Nome</span><span class="sxs-lookup"><span data-stu-id="a7f47-429">Name</span></span> | <span data-ttu-id="a7f47-430">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-430">Type</span></span> | <span data-ttu-id="a7f47-431">Valore</span><span class="sxs-lookup"><span data-stu-id="a7f47-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a7f47-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-432">arrayOutput</span></span> | <span data-ttu-id="a7f47-433">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-433">String</span></span> | <span data-ttu-id="a7f47-434">one</span><span class="sxs-lookup"><span data-stu-id="a7f47-434">one</span></span> |
| <span data-ttu-id="a7f47-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-435">stringOutput</span></span> | <span data-ttu-id="a7f47-436">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-436">String</span></span> | <span data-ttu-id="a7f47-437">O</span><span class="sxs-lookup"><span data-stu-id="a7f47-437">O</span></span> |

<a id="indexof" />

## <a name="indexof"></a><span data-ttu-id="a7f47-438">indexOf</span><span class="sxs-lookup"><span data-stu-id="a7f47-438">indexOf</span></span>
`indexOf(stringToSearch, stringToFind)`

<span data-ttu-id="a7f47-439">Restituisce hello prima posizione di un valore all'interno di una stringa.</span><span class="sxs-lookup"><span data-stu-id="a7f47-439">Returns hello first position of a value within a string.</span></span> <span data-ttu-id="a7f47-440">confronto di Hello è tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="a7f47-440">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="a7f47-441">parameters</span><span class="sxs-lookup"><span data-stu-id="a7f47-441">Parameters</span></span>

| <span data-ttu-id="a7f47-442">Parametro</span><span class="sxs-lookup"><span data-stu-id="a7f47-442">Parameter</span></span> | <span data-ttu-id="a7f47-443">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a7f47-443">Required</span></span> | <span data-ttu-id="a7f47-444">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-444">Type</span></span> | <span data-ttu-id="a7f47-445">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7f47-445">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a7f47-446">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="a7f47-446">stringToSearch</span></span> |<span data-ttu-id="a7f47-447">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-447">Yes</span></span> |<span data-ttu-id="a7f47-448">string</span><span class="sxs-lookup"><span data-stu-id="a7f47-448">string</span></span> |<span data-ttu-id="a7f47-449">valore di Hello contenente toofind elemento hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-449">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="a7f47-450">stringToFind</span><span class="sxs-lookup"><span data-stu-id="a7f47-450">stringToFind</span></span> |<span data-ttu-id="a7f47-451">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-451">Yes</span></span> |<span data-ttu-id="a7f47-452">string</span><span class="sxs-lookup"><span data-stu-id="a7f47-452">string</span></span> |<span data-ttu-id="a7f47-453">toofind valore Hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-453">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a7f47-454">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="a7f47-454">Return value</span></span>

<span data-ttu-id="a7f47-455">Valore intero che rappresenta la posizione hello di hello elemento toofind.</span><span class="sxs-lookup"><span data-stu-id="a7f47-455">An integer that represents hello position of hello item toofind.</span></span> <span data-ttu-id="a7f47-456">il valore di Hello è in base zero.</span><span class="sxs-lookup"><span data-stu-id="a7f47-456">hello value is zero-based.</span></span> <span data-ttu-id="a7f47-457">Se l'elemento hello non viene trovato, viene restituito -1.</span><span class="sxs-lookup"><span data-stu-id="a7f47-457">If hello item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="a7f47-458">esempi</span><span class="sxs-lookup"><span data-stu-id="a7f47-458">Examples</span></span>

<span data-ttu-id="a7f47-459">Hello di esempio seguente viene illustrato come toouse hello indexOf e lastIndexOf funzioni:</span><span class="sxs-lookup"><span data-stu-id="a7f47-459">hello following example shows how toouse hello indexOf and lastIndexOf functions:</span></span>

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

<span data-ttu-id="a7f47-460">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="a7f47-460">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a7f47-461">Nome</span><span class="sxs-lookup"><span data-stu-id="a7f47-461">Name</span></span> | <span data-ttu-id="a7f47-462">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-462">Type</span></span> | <span data-ttu-id="a7f47-463">Valore</span><span class="sxs-lookup"><span data-stu-id="a7f47-463">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a7f47-464">firstT</span><span class="sxs-lookup"><span data-stu-id="a7f47-464">firstT</span></span> | <span data-ttu-id="a7f47-465">int</span><span class="sxs-lookup"><span data-stu-id="a7f47-465">Int</span></span> | <span data-ttu-id="a7f47-466">0</span><span class="sxs-lookup"><span data-stu-id="a7f47-466">0</span></span> |
| <span data-ttu-id="a7f47-467">lastT</span><span class="sxs-lookup"><span data-stu-id="a7f47-467">lastT</span></span> | <span data-ttu-id="a7f47-468">int</span><span class="sxs-lookup"><span data-stu-id="a7f47-468">Int</span></span> | <span data-ttu-id="a7f47-469">3</span><span class="sxs-lookup"><span data-stu-id="a7f47-469">3</span></span> |
| <span data-ttu-id="a7f47-470">firstString</span><span class="sxs-lookup"><span data-stu-id="a7f47-470">firstString</span></span> | <span data-ttu-id="a7f47-471">int</span><span class="sxs-lookup"><span data-stu-id="a7f47-471">Int</span></span> | <span data-ttu-id="a7f47-472">2</span><span class="sxs-lookup"><span data-stu-id="a7f47-472">2</span></span> |
| <span data-ttu-id="a7f47-473">lastString</span><span class="sxs-lookup"><span data-stu-id="a7f47-473">lastString</span></span> | <span data-ttu-id="a7f47-474">int</span><span class="sxs-lookup"><span data-stu-id="a7f47-474">Int</span></span> | <span data-ttu-id="a7f47-475">0</span><span class="sxs-lookup"><span data-stu-id="a7f47-475">0</span></span> |
| <span data-ttu-id="a7f47-476">notFound</span><span class="sxs-lookup"><span data-stu-id="a7f47-476">notFound</span></span> | <span data-ttu-id="a7f47-477">int</span><span class="sxs-lookup"><span data-stu-id="a7f47-477">Int</span></span> | <span data-ttu-id="a7f47-478">-1</span><span class="sxs-lookup"><span data-stu-id="a7f47-478">-1</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="a7f47-479">last</span><span class="sxs-lookup"><span data-stu-id="a7f47-479">last</span></span>
`last (arg1)`

<span data-ttu-id="a7f47-480">Restituisce l'ultimo carattere della stringa hello, o hello l'ultimo elemento della matrice hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-480">Returns last character of hello string, or hello last element of hello array.</span></span>

### <a name="parameters"></a><span data-ttu-id="a7f47-481">parameters</span><span class="sxs-lookup"><span data-stu-id="a7f47-481">Parameters</span></span>

| <span data-ttu-id="a7f47-482">Parametro</span><span class="sxs-lookup"><span data-stu-id="a7f47-482">Parameter</span></span> | <span data-ttu-id="a7f47-483">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a7f47-483">Required</span></span> | <span data-ttu-id="a7f47-484">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-484">Type</span></span> | <span data-ttu-id="a7f47-485">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7f47-485">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a7f47-486">arg1</span><span class="sxs-lookup"><span data-stu-id="a7f47-486">arg1</span></span> |<span data-ttu-id="a7f47-487">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-487">Yes</span></span> |<span data-ttu-id="a7f47-488">stringa o matrice</span><span class="sxs-lookup"><span data-stu-id="a7f47-488">array or string</span></span> |<span data-ttu-id="a7f47-489">carattere o Hello valore tooretrieve hello ultimo elemento.</span><span class="sxs-lookup"><span data-stu-id="a7f47-489">hello value tooretrieve hello last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a7f47-490">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="a7f47-490">Return value</span></span>

<span data-ttu-id="a7f47-491">Stringa di caratteri ultimo hello o il tipo di hello (string, int, matrice o oggetto) di hello ultimo elemento matrice.</span><span class="sxs-lookup"><span data-stu-id="a7f47-491">A string of hello last character, or hello type (string, int, array, or object) of hello last element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="a7f47-492">esempi</span><span class="sxs-lookup"><span data-stu-id="a7f47-492">Examples</span></span>

<span data-ttu-id="a7f47-493">Hello esempio seguente viene illustrato come toouse hello ultima funzione con una matrice e una stringa.</span><span class="sxs-lookup"><span data-stu-id="a7f47-493">hello following example shows how toouse hello last function with an array and string.</span></span>

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

<span data-ttu-id="a7f47-494">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="a7f47-494">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a7f47-495">Nome</span><span class="sxs-lookup"><span data-stu-id="a7f47-495">Name</span></span> | <span data-ttu-id="a7f47-496">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-496">Type</span></span> | <span data-ttu-id="a7f47-497">Valore</span><span class="sxs-lookup"><span data-stu-id="a7f47-497">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a7f47-498">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-498">arrayOutput</span></span> | <span data-ttu-id="a7f47-499">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-499">String</span></span> | <span data-ttu-id="a7f47-500">three</span><span class="sxs-lookup"><span data-stu-id="a7f47-500">three</span></span> |
| <span data-ttu-id="a7f47-501">stringOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-501">stringOutput</span></span> | <span data-ttu-id="a7f47-502">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-502">String</span></span> | <span data-ttu-id="a7f47-503">e</span><span class="sxs-lookup"><span data-stu-id="a7f47-503">e</span></span> |

<a id="lastindexof" />

## <a name="lastindexof"></a><span data-ttu-id="a7f47-504">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="a7f47-504">lastIndexOf</span></span>
`lastIndexOf(stringToSearch, stringToFind)`

<span data-ttu-id="a7f47-505">Restituisce hello ultima posizione di un valore all'interno di una stringa.</span><span class="sxs-lookup"><span data-stu-id="a7f47-505">Returns hello last position of a value within a string.</span></span> <span data-ttu-id="a7f47-506">confronto di Hello è tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="a7f47-506">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="a7f47-507">parameters</span><span class="sxs-lookup"><span data-stu-id="a7f47-507">Parameters</span></span>

| <span data-ttu-id="a7f47-508">Parametro</span><span class="sxs-lookup"><span data-stu-id="a7f47-508">Parameter</span></span> | <span data-ttu-id="a7f47-509">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a7f47-509">Required</span></span> | <span data-ttu-id="a7f47-510">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-510">Type</span></span> | <span data-ttu-id="a7f47-511">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7f47-511">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a7f47-512">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="a7f47-512">stringToSearch</span></span> |<span data-ttu-id="a7f47-513">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-513">Yes</span></span> |<span data-ttu-id="a7f47-514">string</span><span class="sxs-lookup"><span data-stu-id="a7f47-514">string</span></span> |<span data-ttu-id="a7f47-515">valore di Hello contenente toofind elemento hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-515">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="a7f47-516">stringToFind</span><span class="sxs-lookup"><span data-stu-id="a7f47-516">stringToFind</span></span> |<span data-ttu-id="a7f47-517">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-517">Yes</span></span> |<span data-ttu-id="a7f47-518">string</span><span class="sxs-lookup"><span data-stu-id="a7f47-518">string</span></span> |<span data-ttu-id="a7f47-519">toofind valore Hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-519">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a7f47-520">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="a7f47-520">Return value</span></span>

<span data-ttu-id="a7f47-521">Valore intero che rappresenta l'ultima posizione di hello di hello elemento toofind.</span><span class="sxs-lookup"><span data-stu-id="a7f47-521">An integer that represents hello last position of hello item toofind.</span></span> <span data-ttu-id="a7f47-522">il valore di Hello è in base zero.</span><span class="sxs-lookup"><span data-stu-id="a7f47-522">hello value is zero-based.</span></span> <span data-ttu-id="a7f47-523">Se l'elemento hello non viene trovato, viene restituito -1.</span><span class="sxs-lookup"><span data-stu-id="a7f47-523">If hello item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="a7f47-524">esempi</span><span class="sxs-lookup"><span data-stu-id="a7f47-524">Examples</span></span>

<span data-ttu-id="a7f47-525">Hello di esempio seguente viene illustrato come toouse hello indexOf e lastIndexOf funzioni:</span><span class="sxs-lookup"><span data-stu-id="a7f47-525">hello following example shows how toouse hello indexOf and lastIndexOf functions:</span></span>

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

<span data-ttu-id="a7f47-526">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="a7f47-526">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a7f47-527">Nome</span><span class="sxs-lookup"><span data-stu-id="a7f47-527">Name</span></span> | <span data-ttu-id="a7f47-528">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-528">Type</span></span> | <span data-ttu-id="a7f47-529">Valore</span><span class="sxs-lookup"><span data-stu-id="a7f47-529">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a7f47-530">firstT</span><span class="sxs-lookup"><span data-stu-id="a7f47-530">firstT</span></span> | <span data-ttu-id="a7f47-531">int</span><span class="sxs-lookup"><span data-stu-id="a7f47-531">Int</span></span> | <span data-ttu-id="a7f47-532">0</span><span class="sxs-lookup"><span data-stu-id="a7f47-532">0</span></span> |
| <span data-ttu-id="a7f47-533">lastT</span><span class="sxs-lookup"><span data-stu-id="a7f47-533">lastT</span></span> | <span data-ttu-id="a7f47-534">int</span><span class="sxs-lookup"><span data-stu-id="a7f47-534">Int</span></span> | <span data-ttu-id="a7f47-535">3</span><span class="sxs-lookup"><span data-stu-id="a7f47-535">3</span></span> |
| <span data-ttu-id="a7f47-536">firstString</span><span class="sxs-lookup"><span data-stu-id="a7f47-536">firstString</span></span> | <span data-ttu-id="a7f47-537">int</span><span class="sxs-lookup"><span data-stu-id="a7f47-537">Int</span></span> | <span data-ttu-id="a7f47-538">2</span><span class="sxs-lookup"><span data-stu-id="a7f47-538">2</span></span> |
| <span data-ttu-id="a7f47-539">lastString</span><span class="sxs-lookup"><span data-stu-id="a7f47-539">lastString</span></span> | <span data-ttu-id="a7f47-540">int</span><span class="sxs-lookup"><span data-stu-id="a7f47-540">Int</span></span> | <span data-ttu-id="a7f47-541">0</span><span class="sxs-lookup"><span data-stu-id="a7f47-541">0</span></span> |
| <span data-ttu-id="a7f47-542">notFound</span><span class="sxs-lookup"><span data-stu-id="a7f47-542">notFound</span></span> | <span data-ttu-id="a7f47-543">int</span><span class="sxs-lookup"><span data-stu-id="a7f47-543">Int</span></span> | <span data-ttu-id="a7f47-544">-1</span><span class="sxs-lookup"><span data-stu-id="a7f47-544">-1</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="a7f47-545">length</span><span class="sxs-lookup"><span data-stu-id="a7f47-545">length</span></span>
`length(string)`

<span data-ttu-id="a7f47-546">Restituisce il numero di hello di caratteri in una stringa o elementi in una matrice.</span><span class="sxs-lookup"><span data-stu-id="a7f47-546">Returns hello number of characters in a string, or elements in an array.</span></span>

### <a name="parameters"></a><span data-ttu-id="a7f47-547">parameters</span><span class="sxs-lookup"><span data-stu-id="a7f47-547">Parameters</span></span>

| <span data-ttu-id="a7f47-548">Parametro</span><span class="sxs-lookup"><span data-stu-id="a7f47-548">Parameter</span></span> | <span data-ttu-id="a7f47-549">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a7f47-549">Required</span></span> | <span data-ttu-id="a7f47-550">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-550">Type</span></span> | <span data-ttu-id="a7f47-551">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7f47-551">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a7f47-552">arg1</span><span class="sxs-lookup"><span data-stu-id="a7f47-552">arg1</span></span> |<span data-ttu-id="a7f47-553">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-553">Yes</span></span> |<span data-ttu-id="a7f47-554">stringa o matrice</span><span class="sxs-lookup"><span data-stu-id="a7f47-554">array or string</span></span> |<span data-ttu-id="a7f47-555">Hello toouse matrice per ottenere il numero di hello di elementi o hello toouse stringa per ottenere il numero di hello di caratteri.</span><span class="sxs-lookup"><span data-stu-id="a7f47-555">hello array toouse for getting hello number of elements, or hello string toouse for getting hello number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a7f47-556">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="a7f47-556">Return value</span></span>

<span data-ttu-id="a7f47-557">Numero intero</span><span class="sxs-lookup"><span data-stu-id="a7f47-557">An int.</span></span> 

### <a name="examples"></a><span data-ttu-id="a7f47-558">esempi</span><span class="sxs-lookup"><span data-stu-id="a7f47-558">Examples</span></span>

<span data-ttu-id="a7f47-559">Hello seguente esempio viene illustrato come lunghezza toouse con una matrice e la stringa:</span><span class="sxs-lookup"><span data-stu-id="a7f47-559">hello following example shows how toouse length with an array and string:</span></span>

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

<span data-ttu-id="a7f47-560">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="a7f47-560">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a7f47-561">Nome</span><span class="sxs-lookup"><span data-stu-id="a7f47-561">Name</span></span> | <span data-ttu-id="a7f47-562">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-562">Type</span></span> | <span data-ttu-id="a7f47-563">Valore</span><span class="sxs-lookup"><span data-stu-id="a7f47-563">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a7f47-564">arrayLength</span><span class="sxs-lookup"><span data-stu-id="a7f47-564">arrayLength</span></span> | <span data-ttu-id="a7f47-565">int</span><span class="sxs-lookup"><span data-stu-id="a7f47-565">Int</span></span> | <span data-ttu-id="a7f47-566">3</span><span class="sxs-lookup"><span data-stu-id="a7f47-566">3</span></span> |
| <span data-ttu-id="a7f47-567">stringLength</span><span class="sxs-lookup"><span data-stu-id="a7f47-567">stringLength</span></span> | <span data-ttu-id="a7f47-568">int</span><span class="sxs-lookup"><span data-stu-id="a7f47-568">Int</span></span> | <span data-ttu-id="a7f47-569">13</span><span class="sxs-lookup"><span data-stu-id="a7f47-569">13</span></span> |

<a id="padleft" />

## <a name="padleft"></a><span data-ttu-id="a7f47-570">padLeft</span><span class="sxs-lookup"><span data-stu-id="a7f47-570">padLeft</span></span>
`padLeft(valueToPad, totalLength, paddingCharacter)`

<span data-ttu-id="a7f47-571">Restituisce una stringa allineata a destra mediante l'aggiunta di caratteri toohello sinistra fino a raggiungere la lunghezza totale specificata hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-571">Returns a right-aligned string by adding characters toohello left until reaching hello total specified length.</span></span>

### <a name="parameters"></a><span data-ttu-id="a7f47-572">parameters</span><span class="sxs-lookup"><span data-stu-id="a7f47-572">Parameters</span></span>

| <span data-ttu-id="a7f47-573">Parametro</span><span class="sxs-lookup"><span data-stu-id="a7f47-573">Parameter</span></span> | <span data-ttu-id="a7f47-574">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a7f47-574">Required</span></span> | <span data-ttu-id="a7f47-575">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-575">Type</span></span> | <span data-ttu-id="a7f47-576">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7f47-576">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a7f47-577">valueToPad</span><span class="sxs-lookup"><span data-stu-id="a7f47-577">valueToPad</span></span> |<span data-ttu-id="a7f47-578">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-578">Yes</span></span> |<span data-ttu-id="a7f47-579">stringa o numero intero</span><span class="sxs-lookup"><span data-stu-id="a7f47-579">string or int</span></span> |<span data-ttu-id="a7f47-580">valore tooright Hello-align.</span><span class="sxs-lookup"><span data-stu-id="a7f47-580">hello value tooright-align.</span></span> |
| <span data-ttu-id="a7f47-581">totalLength</span><span class="sxs-lookup"><span data-stu-id="a7f47-581">totalLength</span></span> |<span data-ttu-id="a7f47-582">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-582">Yes</span></span> |<span data-ttu-id="a7f47-583">int</span><span class="sxs-lookup"><span data-stu-id="a7f47-583">int</span></span> |<span data-ttu-id="a7f47-584">numero totale di Hello di caratteri in hello stringa restituita.</span><span class="sxs-lookup"><span data-stu-id="a7f47-584">hello total number of characters in hello returned string.</span></span> |
| <span data-ttu-id="a7f47-585">paddingCharacter</span><span class="sxs-lookup"><span data-stu-id="a7f47-585">paddingCharacter</span></span> |<span data-ttu-id="a7f47-586">No</span><span class="sxs-lookup"><span data-stu-id="a7f47-586">No</span></span> |<span data-ttu-id="a7f47-587">Carattere singolo</span><span class="sxs-lookup"><span data-stu-id="a7f47-587">single character</span></span> |<span data-ttu-id="a7f47-588">Hello toouse carattere di riempimento a sinistra fino a raggiunta la lunghezza totale hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-588">hello character toouse for left-padding until hello total length is reached.</span></span> <span data-ttu-id="a7f47-589">valore predefinito di Hello è uno spazio.</span><span class="sxs-lookup"><span data-stu-id="a7f47-589">hello default value is a space.</span></span> |

<span data-ttu-id="a7f47-590">Se la stringa originale hello è più lungo hello numero di caratteri toopad, non vengono aggiunti caratteri.</span><span class="sxs-lookup"><span data-stu-id="a7f47-590">If hello original string is longer than hello number of characters toopad, no characters are added.</span></span>

### <a name="return-value"></a><span data-ttu-id="a7f47-591">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="a7f47-591">Return value</span></span>

<span data-ttu-id="a7f47-592">Una stringa con almeno hello numero di caratteri specificati.</span><span class="sxs-lookup"><span data-stu-id="a7f47-592">A string with at least hello number of specified characters.</span></span>

### <a name="examples"></a><span data-ttu-id="a7f47-593">esempi</span><span class="sxs-lookup"><span data-stu-id="a7f47-593">Examples</span></span>

<span data-ttu-id="a7f47-594">Hello di esempio seguente viene illustrato come toopad hello valore del parametro fornito dall'utente tramite l'aggiunta di hello carattere zero finché raggiunge il numero totale di hello di caratteri.</span><span class="sxs-lookup"><span data-stu-id="a7f47-594">hello following example shows how toopad hello user-provided parameter value by adding hello zero character until it reaches hello total number of characters.</span></span> 

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

<span data-ttu-id="a7f47-595">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="a7f47-595">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a7f47-596">Nome</span><span class="sxs-lookup"><span data-stu-id="a7f47-596">Name</span></span> | <span data-ttu-id="a7f47-597">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-597">Type</span></span> | <span data-ttu-id="a7f47-598">Valore</span><span class="sxs-lookup"><span data-stu-id="a7f47-598">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a7f47-599">stringOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-599">stringOutput</span></span> | <span data-ttu-id="a7f47-600">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-600">String</span></span> | <span data-ttu-id="a7f47-601">0000000123</span><span class="sxs-lookup"><span data-stu-id="a7f47-601">0000000123</span></span> |

<a id="replace" />

## <a name="replace"></a><span data-ttu-id="a7f47-602">replace</span><span class="sxs-lookup"><span data-stu-id="a7f47-602">replace</span></span>
`replace(originalString, oldString, newString)`

<span data-ttu-id="a7f47-603">Restituisce una nuova stringa con tutte le istanze di una stringa sostituita con un'altra stringa.</span><span class="sxs-lookup"><span data-stu-id="a7f47-603">Returns a new string with all instances of one string replaced by another string.</span></span>

### <a name="parameters"></a><span data-ttu-id="a7f47-604">Parametri</span><span class="sxs-lookup"><span data-stu-id="a7f47-604">Parameters</span></span>

| <span data-ttu-id="a7f47-605">Parametro</span><span class="sxs-lookup"><span data-stu-id="a7f47-605">Parameter</span></span> | <span data-ttu-id="a7f47-606">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a7f47-606">Required</span></span> | <span data-ttu-id="a7f47-607">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-607">Type</span></span> | <span data-ttu-id="a7f47-608">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7f47-608">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a7f47-609">originalString</span><span class="sxs-lookup"><span data-stu-id="a7f47-609">originalString</span></span> |<span data-ttu-id="a7f47-610">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-610">Yes</span></span> |<span data-ttu-id="a7f47-611">string</span><span class="sxs-lookup"><span data-stu-id="a7f47-611">string</span></span> |<span data-ttu-id="a7f47-612">valore Hello con tutte le istanze di una stringa sostituita da un'altra stringa.</span><span class="sxs-lookup"><span data-stu-id="a7f47-612">hello value that has all instances of one string replaced by another string.</span></span> |
| <span data-ttu-id="a7f47-613">oldString</span><span class="sxs-lookup"><span data-stu-id="a7f47-613">oldString</span></span> |<span data-ttu-id="a7f47-614">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-614">Yes</span></span> |<span data-ttu-id="a7f47-615">string</span><span class="sxs-lookup"><span data-stu-id="a7f47-615">string</span></span> |<span data-ttu-id="a7f47-616">toobe stringa Hello rimossa dalla stringa originale hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-616">hello string toobe removed from hello original string.</span></span> |
| <span data-ttu-id="a7f47-617">newString</span><span class="sxs-lookup"><span data-stu-id="a7f47-617">newString</span></span> |<span data-ttu-id="a7f47-618">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-618">Yes</span></span> |<span data-ttu-id="a7f47-619">string</span><span class="sxs-lookup"><span data-stu-id="a7f47-619">string</span></span> |<span data-ttu-id="a7f47-620">tooadd stringa Hello al posto di hello rimosso stringa.</span><span class="sxs-lookup"><span data-stu-id="a7f47-620">hello string tooadd in place of hello removed string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a7f47-621">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="a7f47-621">Return value</span></span>

<span data-ttu-id="a7f47-622">Una stringa con hello sostituito caratteri.</span><span class="sxs-lookup"><span data-stu-id="a7f47-622">A string with hello replaced characters.</span></span>

### <a name="examples"></a><span data-ttu-id="a7f47-623">esempi</span><span class="sxs-lookup"><span data-stu-id="a7f47-623">Examples</span></span>

<span data-ttu-id="a7f47-624">Hello di esempio seguente viene illustrato come tooremove tutti i trattini dalla stringa di hello fornito dall'utente e come parte di tooreplace di hello stringa con un'altra stringa.</span><span class="sxs-lookup"><span data-stu-id="a7f47-624">hello following example shows how tooremove all dashes from hello user-provided string, and how tooreplace part of hello string with another string.</span></span>

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

<span data-ttu-id="a7f47-625">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="a7f47-625">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a7f47-626">Nome</span><span class="sxs-lookup"><span data-stu-id="a7f47-626">Name</span></span> | <span data-ttu-id="a7f47-627">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-627">Type</span></span> | <span data-ttu-id="a7f47-628">Valore</span><span class="sxs-lookup"><span data-stu-id="a7f47-628">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a7f47-629">firstOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-629">firstOutput</span></span> | <span data-ttu-id="a7f47-630">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-630">String</span></span> | <span data-ttu-id="a7f47-631">1231231234</span><span class="sxs-lookup"><span data-stu-id="a7f47-631">1231231234</span></span> |
| <span data-ttu-id="a7f47-632">secodeOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-632">secodeOutput</span></span> | <span data-ttu-id="a7f47-633">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-633">String</span></span> | <span data-ttu-id="a7f47-634">123-123-xxxx</span><span class="sxs-lookup"><span data-stu-id="a7f47-634">123-123-xxxx</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="a7f47-635">skip</span><span class="sxs-lookup"><span data-stu-id="a7f47-635">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="a7f47-636">Restituisce una stringa con tutti i caratteri di hello dopo hello specificato numero di caratteri o una matrice con tutti gli elementi di hello dopo hello numero specificato di elementi.</span><span class="sxs-lookup"><span data-stu-id="a7f47-636">Returns a string with all hello characters after hello specified number of characters, or an array with all hello elements after hello specified number of elements.</span></span>

### <a name="parameters"></a><span data-ttu-id="a7f47-637">parameters</span><span class="sxs-lookup"><span data-stu-id="a7f47-637">Parameters</span></span>

| <span data-ttu-id="a7f47-638">Parametro</span><span class="sxs-lookup"><span data-stu-id="a7f47-638">Parameter</span></span> | <span data-ttu-id="a7f47-639">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a7f47-639">Required</span></span> | <span data-ttu-id="a7f47-640">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-640">Type</span></span> | <span data-ttu-id="a7f47-641">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7f47-641">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a7f47-642">originalValue</span><span class="sxs-lookup"><span data-stu-id="a7f47-642">originalValue</span></span> |<span data-ttu-id="a7f47-643">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-643">Yes</span></span> |<span data-ttu-id="a7f47-644">stringa o matrice</span><span class="sxs-lookup"><span data-stu-id="a7f47-644">array or string</span></span> |<span data-ttu-id="a7f47-645">Hello toouse matrice o stringa per l'omissione.</span><span class="sxs-lookup"><span data-stu-id="a7f47-645">hello array or string toouse for skipping.</span></span> |
| <span data-ttu-id="a7f47-646">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="a7f47-646">numberToSkip</span></span> |<span data-ttu-id="a7f47-647">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-647">Yes</span></span> |<span data-ttu-id="a7f47-648">int</span><span class="sxs-lookup"><span data-stu-id="a7f47-648">int</span></span> |<span data-ttu-id="a7f47-649">numero di Hello di tooskip elementi o i caratteri.</span><span class="sxs-lookup"><span data-stu-id="a7f47-649">hello number of elements or characters tooskip.</span></span> <span data-ttu-id="a7f47-650">Se questo valore è 0 o meno, tutti gli elementi di hello o vengono restituiti i caratteri nel valore hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-650">If this value is 0 or less, all hello elements or characters in hello value are returned.</span></span> <span data-ttu-id="a7f47-651">Se è maggiore della lunghezza della stringa o matrice hello hello, viene restituita una matrice vuota o una stringa.</span><span class="sxs-lookup"><span data-stu-id="a7f47-651">If it is larger than hello length of hello array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a7f47-652">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="a7f47-652">Return value</span></span>

<span data-ttu-id="a7f47-653">Stringa o matrice.</span><span class="sxs-lookup"><span data-stu-id="a7f47-653">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="a7f47-654">esempi</span><span class="sxs-lookup"><span data-stu-id="a7f47-654">Examples</span></span>

<span data-ttu-id="a7f47-655">Hello seguente esempio Ignora hello numero specificato di elementi nella matrice hello e hello numero specificato di caratteri in una stringa.</span><span class="sxs-lookup"><span data-stu-id="a7f47-655">hello following example skips hello specified number of elements in hello array, and hello specified number of characters in a string.</span></span>

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

<span data-ttu-id="a7f47-656">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="a7f47-656">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a7f47-657">Nome</span><span class="sxs-lookup"><span data-stu-id="a7f47-657">Name</span></span> | <span data-ttu-id="a7f47-658">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-658">Type</span></span> | <span data-ttu-id="a7f47-659">Valore</span><span class="sxs-lookup"><span data-stu-id="a7f47-659">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a7f47-660">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-660">arrayOutput</span></span> | <span data-ttu-id="a7f47-661">Array</span><span class="sxs-lookup"><span data-stu-id="a7f47-661">Array</span></span> | <span data-ttu-id="a7f47-662">["three"]</span><span class="sxs-lookup"><span data-stu-id="a7f47-662">["three"]</span></span> |
| <span data-ttu-id="a7f47-663">stringOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-663">stringOutput</span></span> | <span data-ttu-id="a7f47-664">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-664">String</span></span> | <span data-ttu-id="a7f47-665">two three</span><span class="sxs-lookup"><span data-stu-id="a7f47-665">two three</span></span> |

<a id="split" />

## <a name="split"></a><span data-ttu-id="a7f47-666">split</span><span class="sxs-lookup"><span data-stu-id="a7f47-666">split</span></span>
`split(inputString, delimiter)`

<span data-ttu-id="a7f47-667">Restituisce una matrice di stringhe contenente le sottostringhe di hello di hello stringa di input che sono delimitate da hello specificato delimitatori.</span><span class="sxs-lookup"><span data-stu-id="a7f47-667">Returns an array of strings that contains hello substrings of hello input string that are delimited by hello specified delimiters.</span></span>

### <a name="parameters"></a><span data-ttu-id="a7f47-668">parameters</span><span class="sxs-lookup"><span data-stu-id="a7f47-668">Parameters</span></span>

| <span data-ttu-id="a7f47-669">Parametro</span><span class="sxs-lookup"><span data-stu-id="a7f47-669">Parameter</span></span> | <span data-ttu-id="a7f47-670">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a7f47-670">Required</span></span> | <span data-ttu-id="a7f47-671">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-671">Type</span></span> | <span data-ttu-id="a7f47-672">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7f47-672">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a7f47-673">inputString</span><span class="sxs-lookup"><span data-stu-id="a7f47-673">inputString</span></span> |<span data-ttu-id="a7f47-674">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-674">Yes</span></span> |<span data-ttu-id="a7f47-675">string</span><span class="sxs-lookup"><span data-stu-id="a7f47-675">string</span></span> |<span data-ttu-id="a7f47-676">toosplit stringa Hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-676">hello string toosplit.</span></span> |
| <span data-ttu-id="a7f47-677">delimiter</span><span class="sxs-lookup"><span data-stu-id="a7f47-677">delimiter</span></span> |<span data-ttu-id="a7f47-678">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-678">Yes</span></span> |<span data-ttu-id="a7f47-679">Stringa o matrice di stringhe</span><span class="sxs-lookup"><span data-stu-id="a7f47-679">string or array of strings</span></span> |<span data-ttu-id="a7f47-680">Hello toouse delimitatore per suddividere la stringa hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-680">hello delimiter toouse for splitting hello string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a7f47-681">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="a7f47-681">Return value</span></span>

<span data-ttu-id="a7f47-682">Matrice di stringhe.</span><span class="sxs-lookup"><span data-stu-id="a7f47-682">An array of strings.</span></span>

### <a name="examples"></a><span data-ttu-id="a7f47-683">esempi</span><span class="sxs-lookup"><span data-stu-id="a7f47-683">Examples</span></span>

<span data-ttu-id="a7f47-684">Hello esempio suddivide hello stringa di input con una virgola e con una virgola o un punto e virgola.</span><span class="sxs-lookup"><span data-stu-id="a7f47-684">hello following example splits hello input string with a comma, and with either a comma or a semi-colon.</span></span>

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

<span data-ttu-id="a7f47-685">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="a7f47-685">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a7f47-686">Nome</span><span class="sxs-lookup"><span data-stu-id="a7f47-686">Name</span></span> | <span data-ttu-id="a7f47-687">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-687">Type</span></span> | <span data-ttu-id="a7f47-688">Valore</span><span class="sxs-lookup"><span data-stu-id="a7f47-688">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a7f47-689">firstOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-689">firstOutput</span></span> | <span data-ttu-id="a7f47-690">Array</span><span class="sxs-lookup"><span data-stu-id="a7f47-690">Array</span></span> | <span data-ttu-id="a7f47-691">["one", "two", "three"]</span><span class="sxs-lookup"><span data-stu-id="a7f47-691">["one", "two", "three"]</span></span> |
| <span data-ttu-id="a7f47-692">secondOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-692">secondOutput</span></span> | <span data-ttu-id="a7f47-693">Array</span><span class="sxs-lookup"><span data-stu-id="a7f47-693">Array</span></span> | <span data-ttu-id="a7f47-694">["one", "two", "three"]</span><span class="sxs-lookup"><span data-stu-id="a7f47-694">["one", "two", "three"]</span></span> |

<a id="startswith" />

## <a name="startswith"></a><span data-ttu-id="a7f47-695">startsWith</span><span class="sxs-lookup"><span data-stu-id="a7f47-695">startsWith</span></span>
`startsWith(stringToSearch, stringToFind)`

<span data-ttu-id="a7f47-696">Determina se una stringa inizia con un valore.</span><span class="sxs-lookup"><span data-stu-id="a7f47-696">Determines whether a string starts with a value.</span></span> <span data-ttu-id="a7f47-697">confronto di Hello è tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="a7f47-697">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="a7f47-698">parameters</span><span class="sxs-lookup"><span data-stu-id="a7f47-698">Parameters</span></span>

| <span data-ttu-id="a7f47-699">Parametro</span><span class="sxs-lookup"><span data-stu-id="a7f47-699">Parameter</span></span> | <span data-ttu-id="a7f47-700">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a7f47-700">Required</span></span> | <span data-ttu-id="a7f47-701">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-701">Type</span></span> | <span data-ttu-id="a7f47-702">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7f47-702">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a7f47-703">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="a7f47-703">stringToSearch</span></span> |<span data-ttu-id="a7f47-704">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-704">Yes</span></span> |<span data-ttu-id="a7f47-705">string</span><span class="sxs-lookup"><span data-stu-id="a7f47-705">string</span></span> |<span data-ttu-id="a7f47-706">valore di Hello contenente toofind elemento hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-706">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="a7f47-707">stringToFind</span><span class="sxs-lookup"><span data-stu-id="a7f47-707">stringToFind</span></span> |<span data-ttu-id="a7f47-708">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-708">Yes</span></span> |<span data-ttu-id="a7f47-709">string</span><span class="sxs-lookup"><span data-stu-id="a7f47-709">string</span></span> |<span data-ttu-id="a7f47-710">toofind valore Hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-710">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a7f47-711">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="a7f47-711">Return value</span></span>

<span data-ttu-id="a7f47-712">**True** se hello primo carattere o caratteri di stringa hello corrisponde a quello hello; in caso contrario, **False**.</span><span class="sxs-lookup"><span data-stu-id="a7f47-712">**True** if hello first character or characters of hello string match hello value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="a7f47-713">esempi</span><span class="sxs-lookup"><span data-stu-id="a7f47-713">Examples</span></span>

<span data-ttu-id="a7f47-714">Hello di esempio seguente viene illustrato come toouse hello startsWith ed endsWith funzioni:</span><span class="sxs-lookup"><span data-stu-id="a7f47-714">hello following example shows how toouse hello startsWith and endsWith functions:</span></span>

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

<span data-ttu-id="a7f47-715">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="a7f47-715">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a7f47-716">Nome</span><span class="sxs-lookup"><span data-stu-id="a7f47-716">Name</span></span> | <span data-ttu-id="a7f47-717">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-717">Type</span></span> | <span data-ttu-id="a7f47-718">Valore</span><span class="sxs-lookup"><span data-stu-id="a7f47-718">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a7f47-719">startsTrue</span><span class="sxs-lookup"><span data-stu-id="a7f47-719">startsTrue</span></span> | <span data-ttu-id="a7f47-720">Booleano</span><span class="sxs-lookup"><span data-stu-id="a7f47-720">Bool</span></span> | <span data-ttu-id="a7f47-721">True </span><span class="sxs-lookup"><span data-stu-id="a7f47-721">True</span></span> |
| <span data-ttu-id="a7f47-722">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="a7f47-722">startsCapTrue</span></span> | <span data-ttu-id="a7f47-723">Booleano</span><span class="sxs-lookup"><span data-stu-id="a7f47-723">Bool</span></span> | <span data-ttu-id="a7f47-724">True </span><span class="sxs-lookup"><span data-stu-id="a7f47-724">True</span></span> |
| <span data-ttu-id="a7f47-725">startsFalse</span><span class="sxs-lookup"><span data-stu-id="a7f47-725">startsFalse</span></span> | <span data-ttu-id="a7f47-726">Booleano</span><span class="sxs-lookup"><span data-stu-id="a7f47-726">Bool</span></span> | <span data-ttu-id="a7f47-727">False</span><span class="sxs-lookup"><span data-stu-id="a7f47-727">False</span></span> |
| <span data-ttu-id="a7f47-728">endsTrue</span><span class="sxs-lookup"><span data-stu-id="a7f47-728">endsTrue</span></span> | <span data-ttu-id="a7f47-729">Booleano</span><span class="sxs-lookup"><span data-stu-id="a7f47-729">Bool</span></span> | <span data-ttu-id="a7f47-730">True </span><span class="sxs-lookup"><span data-stu-id="a7f47-730">True</span></span> |
| <span data-ttu-id="a7f47-731">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="a7f47-731">endsCapTrue</span></span> | <span data-ttu-id="a7f47-732">Booleano</span><span class="sxs-lookup"><span data-stu-id="a7f47-732">Bool</span></span> | <span data-ttu-id="a7f47-733">True </span><span class="sxs-lookup"><span data-stu-id="a7f47-733">True</span></span> |
| <span data-ttu-id="a7f47-734">endsFalse</span><span class="sxs-lookup"><span data-stu-id="a7f47-734">endsFalse</span></span> | <span data-ttu-id="a7f47-735">Booleano</span><span class="sxs-lookup"><span data-stu-id="a7f47-735">Bool</span></span> | <span data-ttu-id="a7f47-736">False</span><span class="sxs-lookup"><span data-stu-id="a7f47-736">False</span></span> |

<a id="string" />

## <a name="string"></a><span data-ttu-id="a7f47-737">string</span><span class="sxs-lookup"><span data-stu-id="a7f47-737">string</span></span>
`string(valueToConvert)`

<span data-ttu-id="a7f47-738">Converte hello specificato tooa stringa del valore.</span><span class="sxs-lookup"><span data-stu-id="a7f47-738">Converts hello specified value tooa string.</span></span>

### <a name="parameters"></a><span data-ttu-id="a7f47-739">parameters</span><span class="sxs-lookup"><span data-stu-id="a7f47-739">Parameters</span></span>

| <span data-ttu-id="a7f47-740">Parametro</span><span class="sxs-lookup"><span data-stu-id="a7f47-740">Parameter</span></span> | <span data-ttu-id="a7f47-741">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a7f47-741">Required</span></span> | <span data-ttu-id="a7f47-742">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-742">Type</span></span> | <span data-ttu-id="a7f47-743">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7f47-743">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a7f47-744">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="a7f47-744">valueToConvert</span></span> |<span data-ttu-id="a7f47-745">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-745">Yes</span></span> | <span data-ttu-id="a7f47-746">Qualsiasi</span><span class="sxs-lookup"><span data-stu-id="a7f47-746">Any</span></span> |<span data-ttu-id="a7f47-747">Hello valore tooconvert toostring.</span><span class="sxs-lookup"><span data-stu-id="a7f47-747">hello value tooconvert toostring.</span></span> <span data-ttu-id="a7f47-748">È possibile convertire qualsiasi tipo di valore, inclusi gli oggetti e le matrici.</span><span class="sxs-lookup"><span data-stu-id="a7f47-748">Any type of value can be converted, including objects and arrays.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a7f47-749">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="a7f47-749">Return value</span></span>

<span data-ttu-id="a7f47-750">Stringa del valore di hello convertito.</span><span class="sxs-lookup"><span data-stu-id="a7f47-750">A string of hello converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="a7f47-751">esempi</span><span class="sxs-lookup"><span data-stu-id="a7f47-751">Examples</span></span>

<span data-ttu-id="a7f47-752">Hello di esempio seguente viene illustrato come tooconvert diversi tipi di valori toostrings:</span><span class="sxs-lookup"><span data-stu-id="a7f47-752">hello following example shows how tooconvert different types of values toostrings:</span></span>

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

<span data-ttu-id="a7f47-753">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="a7f47-753">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a7f47-754">Nome</span><span class="sxs-lookup"><span data-stu-id="a7f47-754">Name</span></span> | <span data-ttu-id="a7f47-755">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-755">Type</span></span> | <span data-ttu-id="a7f47-756">Valore</span><span class="sxs-lookup"><span data-stu-id="a7f47-756">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a7f47-757">objectOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-757">objectOutput</span></span> | <span data-ttu-id="a7f47-758">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-758">String</span></span> | <span data-ttu-id="a7f47-759">{"valueA":10,"valueB":"Example Text"}</span><span class="sxs-lookup"><span data-stu-id="a7f47-759">{"valueA":10,"valueB":"Example Text"}</span></span> |
| <span data-ttu-id="a7f47-760">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-760">arrayOutput</span></span> | <span data-ttu-id="a7f47-761">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-761">String</span></span> | <span data-ttu-id="a7f47-762">["a","b","c"]</span><span class="sxs-lookup"><span data-stu-id="a7f47-762">["a","b","c"]</span></span> |
| <span data-ttu-id="a7f47-763">intOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-763">intOutput</span></span> | <span data-ttu-id="a7f47-764">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-764">String</span></span> | <span data-ttu-id="a7f47-765">5</span><span class="sxs-lookup"><span data-stu-id="a7f47-765">5</span></span> |

<a id="substring" />

## <a name="substring"></a><span data-ttu-id="a7f47-766">substring</span><span class="sxs-lookup"><span data-stu-id="a7f47-766">substring</span></span>
`substring(stringToParse, startIndex, length)`

<span data-ttu-id="a7f47-767">Restituisce una sottostringa che inizia in hello specificato la posizione del carattere e hello contiene un numero specificato di caratteri.</span><span class="sxs-lookup"><span data-stu-id="a7f47-767">Returns a substring that starts at hello specified character position and contains hello specified number of characters.</span></span>

### <a name="parameters"></a><span data-ttu-id="a7f47-768">parameters</span><span class="sxs-lookup"><span data-stu-id="a7f47-768">Parameters</span></span>

| <span data-ttu-id="a7f47-769">Parametro</span><span class="sxs-lookup"><span data-stu-id="a7f47-769">Parameter</span></span> | <span data-ttu-id="a7f47-770">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a7f47-770">Required</span></span> | <span data-ttu-id="a7f47-771">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-771">Type</span></span> | <span data-ttu-id="a7f47-772">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7f47-772">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a7f47-773">stringToParse</span><span class="sxs-lookup"><span data-stu-id="a7f47-773">stringToParse</span></span> |<span data-ttu-id="a7f47-774">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-774">Yes</span></span> |<span data-ttu-id="a7f47-775">string</span><span class="sxs-lookup"><span data-stu-id="a7f47-775">string</span></span> |<span data-ttu-id="a7f47-776">stringa di Hello originale da cui hello estrarre la sottostringa.</span><span class="sxs-lookup"><span data-stu-id="a7f47-776">hello original string from which hello substring is extracted.</span></span> |
| <span data-ttu-id="a7f47-777">startIndex</span><span class="sxs-lookup"><span data-stu-id="a7f47-777">startIndex</span></span> |<span data-ttu-id="a7f47-778">No</span><span class="sxs-lookup"><span data-stu-id="a7f47-778">No</span></span> |<span data-ttu-id="a7f47-779">int</span><span class="sxs-lookup"><span data-stu-id="a7f47-779">int</span></span> |<span data-ttu-id="a7f47-780">Hello in base zero posizione iniziale del carattere per sottostringa hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-780">hello zero-based starting character position for hello substring.</span></span> |
| <span data-ttu-id="a7f47-781">length</span><span class="sxs-lookup"><span data-stu-id="a7f47-781">length</span></span> |<span data-ttu-id="a7f47-782">No</span><span class="sxs-lookup"><span data-stu-id="a7f47-782">No</span></span> |<span data-ttu-id="a7f47-783">int</span><span class="sxs-lookup"><span data-stu-id="a7f47-783">int</span></span> |<span data-ttu-id="a7f47-784">numero di Hello di caratteri per la sottostringa hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-784">hello number of characters for hello substring.</span></span> <span data-ttu-id="a7f47-785">Deve fare riferimento posizione tooa stringa hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-785">Must refer tooa location within hello string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a7f47-786">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="a7f47-786">Return value</span></span>

<span data-ttu-id="a7f47-787">sottostringa Hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-787">hello substring.</span></span>

### <a name="remarks"></a><span data-ttu-id="a7f47-788">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="a7f47-788">Remarks</span></span>

<span data-ttu-id="a7f47-789">funzione Hello non riesce quando sottostringa hello si estende oltre la fine hello della stringa hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-789">hello function fails when hello substring extends beyond hello end of hello string.</span></span> <span data-ttu-id="a7f47-790">Hello di esempio seguente ha esito negativo con hello errore "parametri index e lenght hello devono fare riferimento posizione tooa stringa hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-790">hello following example fails with hello error "hello index and length parameters must refer tooa location within hello string.</span></span> <span data-ttu-id="a7f47-791">Hello parametro index: '0', parametro della lunghezza di hello: lunghezza del parametro della stringa hello di hello '11': '10'. ".</span><span class="sxs-lookup"><span data-stu-id="a7f47-791">hello index parameter: '0', hello length parameter: '11', hello length of hello string parameter: '10'.".</span></span>

```json
"parameters": {
    "inputString": { "type": "string", "value": "1234567890" }
},
"variables": { 
    "prefix": "[substring(parameters('inputString'), 0, 11)]"
}
```

### <a name="examples"></a><span data-ttu-id="a7f47-792">esempi</span><span class="sxs-lookup"><span data-stu-id="a7f47-792">Examples</span></span>

<span data-ttu-id="a7f47-793">Hello di esempio seguente estrae una sottostringa da un parametro.</span><span class="sxs-lookup"><span data-stu-id="a7f47-793">hello following example extracts a substring from a parameter.</span></span>

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

<span data-ttu-id="a7f47-794">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="a7f47-794">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a7f47-795">Nome</span><span class="sxs-lookup"><span data-stu-id="a7f47-795">Name</span></span> | <span data-ttu-id="a7f47-796">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-796">Type</span></span> | <span data-ttu-id="a7f47-797">Valore</span><span class="sxs-lookup"><span data-stu-id="a7f47-797">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a7f47-798">substringOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-798">substringOutput</span></span> | <span data-ttu-id="a7f47-799">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-799">String</span></span> | <span data-ttu-id="a7f47-800">two</span><span class="sxs-lookup"><span data-stu-id="a7f47-800">two</span></span> |


<a id="take" />

## <a name="take"></a><span data-ttu-id="a7f47-801">take</span><span class="sxs-lookup"><span data-stu-id="a7f47-801">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="a7f47-802">Restituisce una stringa con hello numero specificato di caratteri dall'inizio di hello di hello stringa o una matrice con hello numero specificato di elementi dall'inizio di hello della matrice hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-802">Returns a string with hello specified number of characters from hello start of hello string, or an array with hello specified number of elements from hello start of hello array.</span></span>

### <a name="parameters"></a><span data-ttu-id="a7f47-803">parameters</span><span class="sxs-lookup"><span data-stu-id="a7f47-803">Parameters</span></span>

| <span data-ttu-id="a7f47-804">Parametro</span><span class="sxs-lookup"><span data-stu-id="a7f47-804">Parameter</span></span> | <span data-ttu-id="a7f47-805">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a7f47-805">Required</span></span> | <span data-ttu-id="a7f47-806">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-806">Type</span></span> | <span data-ttu-id="a7f47-807">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7f47-807">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a7f47-808">originalValue</span><span class="sxs-lookup"><span data-stu-id="a7f47-808">originalValue</span></span> |<span data-ttu-id="a7f47-809">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-809">Yes</span></span> |<span data-ttu-id="a7f47-810">stringa o matrice</span><span class="sxs-lookup"><span data-stu-id="a7f47-810">array or string</span></span> |<span data-ttu-id="a7f47-811">Hello stringa o matrice di elementi di hello tootake da.</span><span class="sxs-lookup"><span data-stu-id="a7f47-811">hello array or string tootake hello elements from.</span></span> |
| <span data-ttu-id="a7f47-812">numberToTake</span><span class="sxs-lookup"><span data-stu-id="a7f47-812">numberToTake</span></span> |<span data-ttu-id="a7f47-813">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-813">Yes</span></span> |<span data-ttu-id="a7f47-814">int</span><span class="sxs-lookup"><span data-stu-id="a7f47-814">int</span></span> |<span data-ttu-id="a7f47-815">numero di Hello di tootake elementi o i caratteri.</span><span class="sxs-lookup"><span data-stu-id="a7f47-815">hello number of elements or characters tootake.</span></span> <span data-ttu-id="a7f47-816">Se il valore è minore o uguale a 0, viene restituita una stringa o un matrice vuota.</span><span class="sxs-lookup"><span data-stu-id="a7f47-816">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="a7f47-817">Se è maggiore della lunghezza di hello di hello matrice o stringa specificato, vengono restituiti tutti gli elementi hello hello matrice o stringa.</span><span class="sxs-lookup"><span data-stu-id="a7f47-817">If it is larger than hello length of hello given array or string, all hello elements in hello array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a7f47-818">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="a7f47-818">Return value</span></span>

<span data-ttu-id="a7f47-819">Stringa o matrice.</span><span class="sxs-lookup"><span data-stu-id="a7f47-819">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="a7f47-820">esempi</span><span class="sxs-lookup"><span data-stu-id="a7f47-820">Examples</span></span>

<span data-ttu-id="a7f47-821">Hello seguente esempio accetta hello numero specificato di elementi dalla matrice hello e i caratteri di una stringa.</span><span class="sxs-lookup"><span data-stu-id="a7f47-821">hello following example takes hello specified number of elements from hello array, and characters from a string.</span></span>

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

<span data-ttu-id="a7f47-822">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="a7f47-822">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a7f47-823">Nome</span><span class="sxs-lookup"><span data-stu-id="a7f47-823">Name</span></span> | <span data-ttu-id="a7f47-824">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-824">Type</span></span> | <span data-ttu-id="a7f47-825">Valore</span><span class="sxs-lookup"><span data-stu-id="a7f47-825">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a7f47-826">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-826">arrayOutput</span></span> | <span data-ttu-id="a7f47-827">Array</span><span class="sxs-lookup"><span data-stu-id="a7f47-827">Array</span></span> | <span data-ttu-id="a7f47-828">["one", "two"]</span><span class="sxs-lookup"><span data-stu-id="a7f47-828">["one", "two"]</span></span> |
| <span data-ttu-id="a7f47-829">stringOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-829">stringOutput</span></span> | <span data-ttu-id="a7f47-830">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-830">String</span></span> | <span data-ttu-id="a7f47-831">in</span><span class="sxs-lookup"><span data-stu-id="a7f47-831">on</span></span> |

<a id="tolower" />

## <a name="tolower"></a><span data-ttu-id="a7f47-832">toLower</span><span class="sxs-lookup"><span data-stu-id="a7f47-832">toLower</span></span>
`toLower(stringToChange)`

<span data-ttu-id="a7f47-833">Converte hello specificato toolower case della stringa.</span><span class="sxs-lookup"><span data-stu-id="a7f47-833">Converts hello specified string toolower case.</span></span>

### <a name="parameters"></a><span data-ttu-id="a7f47-834">parameters</span><span class="sxs-lookup"><span data-stu-id="a7f47-834">Parameters</span></span>

| <span data-ttu-id="a7f47-835">Parametro</span><span class="sxs-lookup"><span data-stu-id="a7f47-835">Parameter</span></span> | <span data-ttu-id="a7f47-836">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a7f47-836">Required</span></span> | <span data-ttu-id="a7f47-837">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-837">Type</span></span> | <span data-ttu-id="a7f47-838">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7f47-838">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a7f47-839">stringToChange</span><span class="sxs-lookup"><span data-stu-id="a7f47-839">stringToChange</span></span> |<span data-ttu-id="a7f47-840">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-840">Yes</span></span> |<span data-ttu-id="a7f47-841">string</span><span class="sxs-lookup"><span data-stu-id="a7f47-841">string</span></span> |<span data-ttu-id="a7f47-842">Hello valore tooconvert toolower i casi.</span><span class="sxs-lookup"><span data-stu-id="a7f47-842">hello value tooconvert toolower case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a7f47-843">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="a7f47-843">Return value</span></span>

<span data-ttu-id="a7f47-844">la stringa Hello convertito toolower case.</span><span class="sxs-lookup"><span data-stu-id="a7f47-844">hello string converted toolower case.</span></span>

### <a name="examples"></a><span data-ttu-id="a7f47-845">esempi</span><span class="sxs-lookup"><span data-stu-id="a7f47-845">Examples</span></span>

<span data-ttu-id="a7f47-846">Hello di esempio seguente converte un parametro valore toolower case e a tooupper case.</span><span class="sxs-lookup"><span data-stu-id="a7f47-846">hello following example converts a parameter value toolower case and tooupper case.</span></span>

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

<span data-ttu-id="a7f47-847">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="a7f47-847">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a7f47-848">Nome</span><span class="sxs-lookup"><span data-stu-id="a7f47-848">Name</span></span> | <span data-ttu-id="a7f47-849">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-849">Type</span></span> | <span data-ttu-id="a7f47-850">Valore</span><span class="sxs-lookup"><span data-stu-id="a7f47-850">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a7f47-851">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-851">toLowerOutput</span></span> | <span data-ttu-id="a7f47-852">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-852">String</span></span> | <span data-ttu-id="a7f47-853">one two three</span><span class="sxs-lookup"><span data-stu-id="a7f47-853">one two three</span></span> |
| <span data-ttu-id="a7f47-854">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-854">toUpperOutput</span></span> | <span data-ttu-id="a7f47-855">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-855">String</span></span> | <span data-ttu-id="a7f47-856">ONE TWO THREE</span><span class="sxs-lookup"><span data-stu-id="a7f47-856">ONE TWO THREE</span></span> |

<a id="toupper" />

## <a name="toupper"></a><span data-ttu-id="a7f47-857">toUpper</span><span class="sxs-lookup"><span data-stu-id="a7f47-857">toUpper</span></span>
`toUpper(stringToChange)`

<span data-ttu-id="a7f47-858">Converte hello specificato tooupper case della stringa.</span><span class="sxs-lookup"><span data-stu-id="a7f47-858">Converts hello specified string tooupper case.</span></span>

### <a name="parameters"></a><span data-ttu-id="a7f47-859">parameters</span><span class="sxs-lookup"><span data-stu-id="a7f47-859">Parameters</span></span>

| <span data-ttu-id="a7f47-860">Parametro</span><span class="sxs-lookup"><span data-stu-id="a7f47-860">Parameter</span></span> | <span data-ttu-id="a7f47-861">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a7f47-861">Required</span></span> | <span data-ttu-id="a7f47-862">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-862">Type</span></span> | <span data-ttu-id="a7f47-863">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7f47-863">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a7f47-864">stringToChange</span><span class="sxs-lookup"><span data-stu-id="a7f47-864">stringToChange</span></span> |<span data-ttu-id="a7f47-865">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-865">Yes</span></span> |<span data-ttu-id="a7f47-866">string</span><span class="sxs-lookup"><span data-stu-id="a7f47-866">string</span></span> |<span data-ttu-id="a7f47-867">Hello valore tooconvert tooupper i casi.</span><span class="sxs-lookup"><span data-stu-id="a7f47-867">hello value tooconvert tooupper case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a7f47-868">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="a7f47-868">Return value</span></span>

<span data-ttu-id="a7f47-869">la stringa Hello convertito tooupper case.</span><span class="sxs-lookup"><span data-stu-id="a7f47-869">hello string converted tooupper case.</span></span>

### <a name="examples"></a><span data-ttu-id="a7f47-870">esempi</span><span class="sxs-lookup"><span data-stu-id="a7f47-870">Examples</span></span>

<span data-ttu-id="a7f47-871">Hello di esempio seguente converte un parametro valore toolower case e a tooupper case.</span><span class="sxs-lookup"><span data-stu-id="a7f47-871">hello following example converts a parameter value toolower case and tooupper case.</span></span>

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

<span data-ttu-id="a7f47-872">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="a7f47-872">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a7f47-873">Nome</span><span class="sxs-lookup"><span data-stu-id="a7f47-873">Name</span></span> | <span data-ttu-id="a7f47-874">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-874">Type</span></span> | <span data-ttu-id="a7f47-875">Valore</span><span class="sxs-lookup"><span data-stu-id="a7f47-875">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a7f47-876">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-876">toLowerOutput</span></span> | <span data-ttu-id="a7f47-877">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-877">String</span></span> | <span data-ttu-id="a7f47-878">one two three</span><span class="sxs-lookup"><span data-stu-id="a7f47-878">one two three</span></span> |
| <span data-ttu-id="a7f47-879">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-879">toUpperOutput</span></span> | <span data-ttu-id="a7f47-880">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-880">String</span></span> | <span data-ttu-id="a7f47-881">ONE TWO THREE</span><span class="sxs-lookup"><span data-stu-id="a7f47-881">ONE TWO THREE</span></span> |

<a id="trim" />

## <a name="trim"></a><span data-ttu-id="a7f47-882">Trim</span><span class="sxs-lookup"><span data-stu-id="a7f47-882">trim</span></span>
`trim (stringToTrim)`

<span data-ttu-id="a7f47-883">Rimuove tutte iniziali e finali dei caratteri di spazio da hello stringa specificata.</span><span class="sxs-lookup"><span data-stu-id="a7f47-883">Removes all leading and trailing white-space characters from hello specified string.</span></span>

### <a name="parameters"></a><span data-ttu-id="a7f47-884">parameters</span><span class="sxs-lookup"><span data-stu-id="a7f47-884">Parameters</span></span>

| <span data-ttu-id="a7f47-885">Parametro</span><span class="sxs-lookup"><span data-stu-id="a7f47-885">Parameter</span></span> | <span data-ttu-id="a7f47-886">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a7f47-886">Required</span></span> | <span data-ttu-id="a7f47-887">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-887">Type</span></span> | <span data-ttu-id="a7f47-888">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7f47-888">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a7f47-889">stringToTrim</span><span class="sxs-lookup"><span data-stu-id="a7f47-889">stringToTrim</span></span> |<span data-ttu-id="a7f47-890">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-890">Yes</span></span> |<span data-ttu-id="a7f47-891">string</span><span class="sxs-lookup"><span data-stu-id="a7f47-891">string</span></span> |<span data-ttu-id="a7f47-892">tootrim valore Hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-892">hello value tootrim.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a7f47-893">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="a7f47-893">Return value</span></span>

<span data-ttu-id="a7f47-894">stringa Hello senza caratteri spazi vuoti iniziali e finali.</span><span class="sxs-lookup"><span data-stu-id="a7f47-894">hello string without leading and trailing white-space characters.</span></span>

### <a name="examples"></a><span data-ttu-id="a7f47-895">esempi</span><span class="sxs-lookup"><span data-stu-id="a7f47-895">Examples</span></span>

<span data-ttu-id="a7f47-896">Hello esempio seguente vengono eliminate hello spazi vuoti dal parametro hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-896">hello following example trims hello white-space characters from hello parameter.</span></span>

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

<span data-ttu-id="a7f47-897">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="a7f47-897">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a7f47-898">Nome</span><span class="sxs-lookup"><span data-stu-id="a7f47-898">Name</span></span> | <span data-ttu-id="a7f47-899">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-899">Type</span></span> | <span data-ttu-id="a7f47-900">Valore</span><span class="sxs-lookup"><span data-stu-id="a7f47-900">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a7f47-901">return</span><span class="sxs-lookup"><span data-stu-id="a7f47-901">return</span></span> | <span data-ttu-id="a7f47-902">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-902">String</span></span> | <span data-ttu-id="a7f47-903">one two three</span><span class="sxs-lookup"><span data-stu-id="a7f47-903">one two three</span></span> |

<a id="uniquestring" />

## <a name="uniquestring"></a><span data-ttu-id="a7f47-904">uniqueString</span><span class="sxs-lookup"><span data-stu-id="a7f47-904">uniqueString</span></span>
`uniqueString (baseString, ...)`

<span data-ttu-id="a7f47-905">Crea una stringa hash deterministica in base ai valori hello forniti come parametri.</span><span class="sxs-lookup"><span data-stu-id="a7f47-905">Creates a deterministic hash string based on hello values provided as parameters.</span></span> 

### <a name="parameters"></a><span data-ttu-id="a7f47-906">parameters</span><span class="sxs-lookup"><span data-stu-id="a7f47-906">Parameters</span></span>

| <span data-ttu-id="a7f47-907">Parametro</span><span class="sxs-lookup"><span data-stu-id="a7f47-907">Parameter</span></span> | <span data-ttu-id="a7f47-908">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a7f47-908">Required</span></span> | <span data-ttu-id="a7f47-909">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-909">Type</span></span> | <span data-ttu-id="a7f47-910">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7f47-910">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a7f47-911">baseString</span><span class="sxs-lookup"><span data-stu-id="a7f47-911">baseString</span></span> |<span data-ttu-id="a7f47-912">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-912">Yes</span></span> |<span data-ttu-id="a7f47-913">string</span><span class="sxs-lookup"><span data-stu-id="a7f47-913">string</span></span> |<span data-ttu-id="a7f47-914">il valore di Hello utilizzato hello hash funzione toocreate una stringa univoca.</span><span class="sxs-lookup"><span data-stu-id="a7f47-914">hello value used in hello hash function toocreate a unique string.</span></span> |
| <span data-ttu-id="a7f47-915">parametri aggiuntivi in base alle esigenze</span><span class="sxs-lookup"><span data-stu-id="a7f47-915">additional parameters as needed</span></span> |<span data-ttu-id="a7f47-916">No</span><span class="sxs-lookup"><span data-stu-id="a7f47-916">No</span></span> |<span data-ttu-id="a7f47-917">string</span><span class="sxs-lookup"><span data-stu-id="a7f47-917">string</span></span> |<span data-ttu-id="a7f47-918">È possibile aggiungere il numero di stringhe come valore di hello toocreate necessari che specifica il livello di hello di univocità.</span><span class="sxs-lookup"><span data-stu-id="a7f47-918">You can add as many strings as needed toocreate hello value that specifies hello level of uniqueness.</span></span> |

### <a name="remarks"></a><span data-ttu-id="a7f47-919">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="a7f47-919">Remarks</span></span>

<span data-ttu-id="a7f47-920">Questa funzione è utile quando è necessario un nome univoco per una risorsa toocreate.</span><span class="sxs-lookup"><span data-stu-id="a7f47-920">This function is helpful when you need toocreate a unique name for a resource.</span></span> <span data-ttu-id="a7f47-921">Fornire i valori dei parametri che consentono di limitare l'ambito di hello di univocità per i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-921">You provide parameter values that limit hello scope of uniqueness for hello result.</span></span> <span data-ttu-id="a7f47-922">È possibile specificare se il nome di hello è univoco verso il basso toosubscription, gruppo di risorse o distribuzione.</span><span class="sxs-lookup"><span data-stu-id="a7f47-922">You can specify whether hello name is unique down toosubscription, resource group, or deployment.</span></span> 

<span data-ttu-id="a7f47-923">Hello restituito non è una stringa casuale di valore, ma piuttosto hello risultato di una funzione hash.</span><span class="sxs-lookup"><span data-stu-id="a7f47-923">hello returned value is not a random string, but rather hello result of a hash function.</span></span> <span data-ttu-id="a7f47-924">Hello ha restituito il valore è 13 caratteri.</span><span class="sxs-lookup"><span data-stu-id="a7f47-924">hello returned value is 13 characters long.</span></span> <span data-ttu-id="a7f47-925">Non è globalmente univoco.</span><span class="sxs-lookup"><span data-stu-id="a7f47-925">It is not globally unique.</span></span> <span data-ttu-id="a7f47-926">È il valore hello toocombine con un prefisso dal toocreate convenzione di denominazione un nome significativo.</span><span class="sxs-lookup"><span data-stu-id="a7f47-926">You may want toocombine hello value with a prefix from your naming convention toocreate a name that is meaningful.</span></span> <span data-ttu-id="a7f47-927">Hello esempio seguente viene illustrato il formato di hello di hello ha restituito il valore.</span><span class="sxs-lookup"><span data-stu-id="a7f47-927">hello following example shows hello format of hello returned value.</span></span> <span data-ttu-id="a7f47-928">valore effettivo Hello varia in base hello parametri fornito.</span><span class="sxs-lookup"><span data-stu-id="a7f47-928">hello actual value varies by hello provided parameters.</span></span>

    tcvhiyu5h2o5o

<span data-ttu-id="a7f47-929">Hello seguono esempi Mostra come valore toouse uniqueString toocreate univoco per comunemente utilizzati livelli.</span><span class="sxs-lookup"><span data-stu-id="a7f47-929">hello following examples show how toouse uniqueString toocreate a unique value for commonly used levels.</span></span>

<span data-ttu-id="a7f47-930">Toosubscription con ambito univoco</span><span class="sxs-lookup"><span data-stu-id="a7f47-930">Unique scoped toosubscription</span></span>

```json
"[uniqueString(subscription().subscriptionId)]"
```

<span data-ttu-id="a7f47-931">Univoco tooresource con ambito gruppo</span><span class="sxs-lookup"><span data-stu-id="a7f47-931">Unique scoped tooresource group</span></span>

```json
"[uniqueString(resourceGroup().id)]"
```

<span data-ttu-id="a7f47-932">Toodeployment con ambito univoco per un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="a7f47-932">Unique scoped toodeployment for a resource group</span></span>

```json
"[uniqueString(resourceGroup().id, deployment().name)]"
```

<span data-ttu-id="a7f47-933">Hello di esempio seguente mostra come toocreate un nome univoco per un account di archiviazione in base al gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="a7f47-933">hello following example shows how toocreate a unique name for a storage account based on your resource group.</span></span> <span data-ttu-id="a7f47-934">All'interno di hello gruppo di risorse, non è univoco se costruito hello Nome hello allo stesso modo.</span><span class="sxs-lookup"><span data-stu-id="a7f47-934">Inside hello resource group, hello name is not unique if constructed hello same way.</span></span>

```json
"resources": [{ 
    "name": "[concat('storage', uniqueString(resourceGroup().id))]", 
    "type": "Microsoft.Storage/storageAccounts", 
    ...
```

### <a name="return-value"></a><span data-ttu-id="a7f47-935">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="a7f47-935">Return value</span></span>

<span data-ttu-id="a7f47-936">Stringa contenente 13 caratteri.</span><span class="sxs-lookup"><span data-stu-id="a7f47-936">A string containing 13 characters.</span></span>

### <a name="examples"></a><span data-ttu-id="a7f47-937">esempi</span><span class="sxs-lookup"><span data-stu-id="a7f47-937">Examples</span></span>

<span data-ttu-id="a7f47-938">Hello di esempio seguente restituisce risultati dalla uniquestring:</span><span class="sxs-lookup"><span data-stu-id="a7f47-938">hello following example returns results from uniquestring:</span></span>

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

## <a name="uri"></a><span data-ttu-id="a7f47-939">Uri</span><span class="sxs-lookup"><span data-stu-id="a7f47-939">uri</span></span>
`uri (baseUri, relativeUri)`

<span data-ttu-id="a7f47-940">Crea un URI assoluto combinando baseUri hello e stringa relativeUri hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-940">Creates an absolute URI by combining hello baseUri and hello relativeUri string.</span></span>

### <a name="parameters"></a><span data-ttu-id="a7f47-941">parameters</span><span class="sxs-lookup"><span data-stu-id="a7f47-941">Parameters</span></span>

| <span data-ttu-id="a7f47-942">Parametro</span><span class="sxs-lookup"><span data-stu-id="a7f47-942">Parameter</span></span> | <span data-ttu-id="a7f47-943">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a7f47-943">Required</span></span> | <span data-ttu-id="a7f47-944">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-944">Type</span></span> | <span data-ttu-id="a7f47-945">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7f47-945">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a7f47-946">baseUri</span><span class="sxs-lookup"><span data-stu-id="a7f47-946">baseUri</span></span> |<span data-ttu-id="a7f47-947">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-947">Yes</span></span> |<span data-ttu-id="a7f47-948">string</span><span class="sxs-lookup"><span data-stu-id="a7f47-948">string</span></span> |<span data-ttu-id="a7f47-949">stringa uri di base Hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-949">hello base uri string.</span></span> |
| <span data-ttu-id="a7f47-950">relativeUri</span><span class="sxs-lookup"><span data-stu-id="a7f47-950">relativeUri</span></span> |<span data-ttu-id="a7f47-951">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-951">Yes</span></span> |<span data-ttu-id="a7f47-952">string</span><span class="sxs-lookup"><span data-stu-id="a7f47-952">string</span></span> |<span data-ttu-id="a7f47-953">Hello uri relativo tooadd toohello uri di base stringa.</span><span class="sxs-lookup"><span data-stu-id="a7f47-953">hello relative uri string tooadd toohello base uri string.</span></span> |

<span data-ttu-id="a7f47-954">valore per hello Hello **baseUri** parametro può includere un file specifico, ma solo hello percorso verrà utilizzato durante la costruzione di hello URI.</span><span class="sxs-lookup"><span data-stu-id="a7f47-954">hello value for hello **baseUri** parameter can include a specific file, but only hello base path is used when constructing hello URI.</span></span> <span data-ttu-id="a7f47-955">Ad esempio, passare `http://contoso.com/resources/azuredeploy.json` come hello baseUri parametro, verrà generato un URI di base `http://contoso.com/resources/`.</span><span class="sxs-lookup"><span data-stu-id="a7f47-955">For example, passing `http://contoso.com/resources/azuredeploy.json` as hello baseUri parameter results in a base URI of `http://contoso.com/resources/`.</span></span>

### <a name="return-value"></a><span data-ttu-id="a7f47-956">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="a7f47-956">Return value</span></span>

<span data-ttu-id="a7f47-957">Stringa che rappresenta hello URI assoluto per i valori di base e relativi hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-957">A string representing hello absolute URI for hello base and relative values.</span></span>

### <a name="examples"></a><span data-ttu-id="a7f47-958">esempi</span><span class="sxs-lookup"><span data-stu-id="a7f47-958">Examples</span></span>

<span data-ttu-id="a7f47-959">Hello di esempio seguente viene illustrato come tooconstruct un modello annidato tooa di collegamento in base a valore hello del modello padre hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-959">hello following example shows how tooconstruct a link tooa nested template based on hello value of hello parent template.</span></span>

```json
"templateLink": "[uri(deployment().properties.templateLink.uri, 'nested/azuredeploy.json')]"
```

<span data-ttu-id="a7f47-960">Hello seguente come esempio viene illustrato un componente URI, toouse uri e uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="a7f47-960">hello following example shows how toouse uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="a7f47-961">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="a7f47-961">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a7f47-962">Nome</span><span class="sxs-lookup"><span data-stu-id="a7f47-962">Name</span></span> | <span data-ttu-id="a7f47-963">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-963">Type</span></span> | <span data-ttu-id="a7f47-964">Valore</span><span class="sxs-lookup"><span data-stu-id="a7f47-964">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a7f47-965">uriOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-965">uriOutput</span></span> | <span data-ttu-id="a7f47-966">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-966">String</span></span> | <span data-ttu-id="a7f47-967">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="a7f47-967">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="a7f47-968">componentOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-968">componentOutput</span></span> | <span data-ttu-id="a7f47-969">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-969">String</span></span> | <span data-ttu-id="a7f47-970">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="a7f47-970">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="a7f47-971">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-971">toStringOutput</span></span> | <span data-ttu-id="a7f47-972">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-972">String</span></span> | <span data-ttu-id="a7f47-973">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="a7f47-973">http://contoso.com/resources/nested/azuredeploy.json</span></span> |

<a id="uricomponent" />

## <a name="uricomponent"></a><span data-ttu-id="a7f47-974">uriComponent</span><span class="sxs-lookup"><span data-stu-id="a7f47-974">uriComponent</span></span>
`uricomponent(stringToEncode)`

<span data-ttu-id="a7f47-975">Codifica un URI.</span><span class="sxs-lookup"><span data-stu-id="a7f47-975">Encodes a URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="a7f47-976">Parametri</span><span class="sxs-lookup"><span data-stu-id="a7f47-976">Parameters</span></span>

| <span data-ttu-id="a7f47-977">Parametro</span><span class="sxs-lookup"><span data-stu-id="a7f47-977">Parameter</span></span> | <span data-ttu-id="a7f47-978">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a7f47-978">Required</span></span> | <span data-ttu-id="a7f47-979">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-979">Type</span></span> | <span data-ttu-id="a7f47-980">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7f47-980">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a7f47-981">stringToEncode</span><span class="sxs-lookup"><span data-stu-id="a7f47-981">stringToEncode</span></span> |<span data-ttu-id="a7f47-982">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-982">Yes</span></span> |<span data-ttu-id="a7f47-983">string</span><span class="sxs-lookup"><span data-stu-id="a7f47-983">string</span></span> |<span data-ttu-id="a7f47-984">tooencode valore Hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-984">hello value tooencode.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a7f47-985">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="a7f47-985">Return value</span></span>

<span data-ttu-id="a7f47-986">Valore codificato in una stringa di hello URI.</span><span class="sxs-lookup"><span data-stu-id="a7f47-986">A string of hello URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="a7f47-987">esempi</span><span class="sxs-lookup"><span data-stu-id="a7f47-987">Examples</span></span>

<span data-ttu-id="a7f47-988">Hello seguente come esempio viene illustrato un componente URI, toouse uri e uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="a7f47-988">hello following example shows how toouse uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="a7f47-989">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="a7f47-989">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a7f47-990">Nome</span><span class="sxs-lookup"><span data-stu-id="a7f47-990">Name</span></span> | <span data-ttu-id="a7f47-991">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-991">Type</span></span> | <span data-ttu-id="a7f47-992">Valore</span><span class="sxs-lookup"><span data-stu-id="a7f47-992">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a7f47-993">uriOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-993">uriOutput</span></span> | <span data-ttu-id="a7f47-994">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-994">String</span></span> | <span data-ttu-id="a7f47-995">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="a7f47-995">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="a7f47-996">componentOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-996">componentOutput</span></span> | <span data-ttu-id="a7f47-997">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-997">String</span></span> | <span data-ttu-id="a7f47-998">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="a7f47-998">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="a7f47-999">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-999">toStringOutput</span></span> | <span data-ttu-id="a7f47-1000">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-1000">String</span></span> | <span data-ttu-id="a7f47-1001">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="a7f47-1001">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


<a id="uricomponenttostring" />

## <a name="uricomponenttostring"></a><span data-ttu-id="a7f47-1002">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="a7f47-1002">uriComponentToString</span></span>
`uriComponentToString(uriEncodedString)`

<span data-ttu-id="a7f47-1003">Restituisce una stringa di un valore URI codificato.</span><span class="sxs-lookup"><span data-stu-id="a7f47-1003">Returns a string of a URI encoded value.</span></span>

### <a name="parameters"></a><span data-ttu-id="a7f47-1004">Parametri</span><span class="sxs-lookup"><span data-stu-id="a7f47-1004">Parameters</span></span>

| <span data-ttu-id="a7f47-1005">Parametro</span><span class="sxs-lookup"><span data-stu-id="a7f47-1005">Parameter</span></span> | <span data-ttu-id="a7f47-1006">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a7f47-1006">Required</span></span> | <span data-ttu-id="a7f47-1007">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-1007">Type</span></span> | <span data-ttu-id="a7f47-1008">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7f47-1008">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a7f47-1009">uriEncodedString</span><span class="sxs-lookup"><span data-stu-id="a7f47-1009">uriEncodedString</span></span> |<span data-ttu-id="a7f47-1010">Sì</span><span class="sxs-lookup"><span data-stu-id="a7f47-1010">Yes</span></span> |<span data-ttu-id="a7f47-1011">string</span><span class="sxs-lookup"><span data-stu-id="a7f47-1011">string</span></span> |<span data-ttu-id="a7f47-1012">stringa di tooa tooconvert di valore con codifica URI Hello.</span><span class="sxs-lookup"><span data-stu-id="a7f47-1012">hello URI encoded value tooconvert tooa string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a7f47-1013">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="a7f47-1013">Return value</span></span>

<span data-ttu-id="a7f47-1014">Stringa decodificata del valore URI codificato.</span><span class="sxs-lookup"><span data-stu-id="a7f47-1014">A decoded string of URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="a7f47-1015">esempi</span><span class="sxs-lookup"><span data-stu-id="a7f47-1015">Examples</span></span>

<span data-ttu-id="a7f47-1016">Hello seguente come esempio viene illustrato un componente URI, toouse uri e uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="a7f47-1016">hello following example shows how toouse uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="a7f47-1017">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="a7f47-1017">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a7f47-1018">Nome</span><span class="sxs-lookup"><span data-stu-id="a7f47-1018">Name</span></span> | <span data-ttu-id="a7f47-1019">Tipo</span><span class="sxs-lookup"><span data-stu-id="a7f47-1019">Type</span></span> | <span data-ttu-id="a7f47-1020">Valore</span><span class="sxs-lookup"><span data-stu-id="a7f47-1020">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a7f47-1021">uriOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-1021">uriOutput</span></span> | <span data-ttu-id="a7f47-1022">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-1022">String</span></span> | <span data-ttu-id="a7f47-1023">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="a7f47-1023">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="a7f47-1024">componentOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-1024">componentOutput</span></span> | <span data-ttu-id="a7f47-1025">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-1025">String</span></span> | <span data-ttu-id="a7f47-1026">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="a7f47-1026">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="a7f47-1027">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="a7f47-1027">toStringOutput</span></span> | <span data-ttu-id="a7f47-1028">String</span><span class="sxs-lookup"><span data-stu-id="a7f47-1028">String</span></span> | <span data-ttu-id="a7f47-1029">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="a7f47-1029">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


## <a name="next-steps"></a><span data-ttu-id="a7f47-1030">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a7f47-1030">Next steps</span></span>
* <span data-ttu-id="a7f47-1031">Per una descrizione delle sezioni hello in un modello di gestione risorse di Azure, vedere [modelli Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a7f47-1031">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="a7f47-1032">toomerge più modelli, vedere [con modelli collegati con Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a7f47-1032">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="a7f47-1033">tooiterate un numero specificato di volte durante la creazione di un tipo di risorsa, vedere [creare più istanze delle risorse in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="a7f47-1033">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="a7f47-1034">toosee come modello hello toodeploy è stato creato, vedere [distribuire un'applicazione con il modello di gestione risorse di Azure](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="a7f47-1034">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

