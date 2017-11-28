---
title: funzioni di modello di gestione risorse aaaAzure - confronto | Documenti Microsoft
description: Viene descritto toouse funzioni hello un valori toocompare modello di gestione risorse di Azure.
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
ms.openlocfilehash: ebcfc9ed6c93f8b540ec4c066e9457c621800b7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="comparison-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="d17ba-103">Funzioni di confronto per i modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d17ba-103">Comparison functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="d17ba-104">Resource Manager include numerose funzioni per l'esecuzione di confronti nei modelli.</span><span class="sxs-lookup"><span data-stu-id="d17ba-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="d17ba-105">equals</span><span class="sxs-lookup"><span data-stu-id="d17ba-105">equals</span></span>](#equals)
* [<span data-ttu-id="d17ba-106">greater</span><span class="sxs-lookup"><span data-stu-id="d17ba-106">greater</span></span>](#greater)
* [<span data-ttu-id="d17ba-107">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="d17ba-107">greaterOrEquals</span></span>](#greaterorequals)
* [<span data-ttu-id="d17ba-108">less</span><span class="sxs-lookup"><span data-stu-id="d17ba-108">less</span></span>](#less)
* [<span data-ttu-id="d17ba-109">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="d17ba-109">lessOrEquals</span></span>](#lessorequals)

## <a name="equals"></a><span data-ttu-id="d17ba-110">equals</span><span class="sxs-lookup"><span data-stu-id="d17ba-110">equals</span></span>
`equals(arg1, arg2)`

<span data-ttu-id="d17ba-111">Controlla se due valori sono uguali tra loro.</span><span class="sxs-lookup"><span data-stu-id="d17ba-111">Checks whether two values equal each other.</span></span>

### <a name="parameters"></a><span data-ttu-id="d17ba-112">Parametri</span><span class="sxs-lookup"><span data-stu-id="d17ba-112">Parameters</span></span>

| <span data-ttu-id="d17ba-113">Parametro</span><span class="sxs-lookup"><span data-stu-id="d17ba-113">Parameter</span></span> | <span data-ttu-id="d17ba-114">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d17ba-114">Required</span></span> | <span data-ttu-id="d17ba-115">Tipo</span><span class="sxs-lookup"><span data-stu-id="d17ba-115">Type</span></span> | <span data-ttu-id="d17ba-116">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d17ba-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d17ba-117">arg1</span><span class="sxs-lookup"><span data-stu-id="d17ba-117">arg1</span></span> |<span data-ttu-id="d17ba-118">Sì</span><span class="sxs-lookup"><span data-stu-id="d17ba-118">Yes</span></span> |<span data-ttu-id="d17ba-119">int, stringa, matrice o oggetto</span><span class="sxs-lookup"><span data-stu-id="d17ba-119">int, string, array, or object</span></span> |<span data-ttu-id="d17ba-120">Hello primo valore toocheck per verificarne l'uguaglianza.</span><span class="sxs-lookup"><span data-stu-id="d17ba-120">hello first value toocheck for equality.</span></span> |
| <span data-ttu-id="d17ba-121">arg2</span><span class="sxs-lookup"><span data-stu-id="d17ba-121">arg2</span></span> |<span data-ttu-id="d17ba-122">Sì</span><span class="sxs-lookup"><span data-stu-id="d17ba-122">Yes</span></span> |<span data-ttu-id="d17ba-123">int, stringa, matrice o oggetto</span><span class="sxs-lookup"><span data-stu-id="d17ba-123">int, string, array, or object</span></span> |<span data-ttu-id="d17ba-124">Hello secondo valore toocheck per verificarne l'uguaglianza.</span><span class="sxs-lookup"><span data-stu-id="d17ba-124">hello second value toocheck for equality.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d17ba-125">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="d17ba-125">Return value</span></span>

<span data-ttu-id="d17ba-126">Restituisce **True** se hello valori sono uguali; in caso contrario, **False**.</span><span class="sxs-lookup"><span data-stu-id="d17ba-126">Returns **True** if hello values are equal; otherwise, **False**.</span></span>

### <a name="remarks"></a><span data-ttu-id="d17ba-127">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="d17ba-127">Remarks</span></span>

<span data-ttu-id="d17ba-128">Hello funzione equals viene spesso usato con hello `condition` tootest elemento che viene implementata una risorsa.</span><span class="sxs-lookup"><span data-stu-id="d17ba-128">hello equals function is often used with hello `condition` element tootest whether a resource is deployed.</span></span>

```json
{
    "condition": "[equals(parameters('newOrExisting'),'new')]",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2017-06-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "[variables('storageAccountType')]"
    },
    "kind": "Storage",
    "properties": {}
}
```

### <a name="example"></a><span data-ttu-id="d17ba-129">Esempio</span><span class="sxs-lookup"><span data-stu-id="d17ba-129">Example</span></span>

<span data-ttu-id="d17ba-130">modello di esempio Hello controlla i tipi diversi di valori per verificarne l'uguaglianza.</span><span class="sxs-lookup"><span data-stu-id="d17ba-130">hello example template checks different types of values for equality.</span></span> <span data-ttu-id="d17ba-131">Tutti i valori predefiniti di hello restituiscono True.</span><span class="sxs-lookup"><span data-stu-id="d17ba-131">All hello default values return True.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 1
        },
        "firstString": {
            "type": "string",
            "defaultValue": "a"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["a", "b"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["a", "b"]
        },
        "firstObject": {
            "type": "object",
            "defaultValue": {"a": "b"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"a": "b"}
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[equals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[equals(parameters('firstString'), parameters('secondString'))]"
        },
        "checkArrays": {
            "type": "bool",
            "value": "[equals(parameters('firstArray'), parameters('secondArray'))]"
        },
        "checkObjects": {
            "type": "bool",
            "value": "[equals(parameters('firstObject'), parameters('secondObject'))]"
        }
    }
}
```

<span data-ttu-id="d17ba-132">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="d17ba-132">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d17ba-133">Nome</span><span class="sxs-lookup"><span data-stu-id="d17ba-133">Name</span></span> | <span data-ttu-id="d17ba-134">Tipo</span><span class="sxs-lookup"><span data-stu-id="d17ba-134">Type</span></span> | <span data-ttu-id="d17ba-135">Valore</span><span class="sxs-lookup"><span data-stu-id="d17ba-135">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d17ba-136">checkInts</span><span class="sxs-lookup"><span data-stu-id="d17ba-136">checkInts</span></span> | <span data-ttu-id="d17ba-137">Booleano</span><span class="sxs-lookup"><span data-stu-id="d17ba-137">Bool</span></span> | <span data-ttu-id="d17ba-138">True </span><span class="sxs-lookup"><span data-stu-id="d17ba-138">True</span></span> |
| <span data-ttu-id="d17ba-139">checkStrings</span><span class="sxs-lookup"><span data-stu-id="d17ba-139">checkStrings</span></span> | <span data-ttu-id="d17ba-140">Booleano</span><span class="sxs-lookup"><span data-stu-id="d17ba-140">Bool</span></span> | <span data-ttu-id="d17ba-141">True </span><span class="sxs-lookup"><span data-stu-id="d17ba-141">True</span></span> |
| <span data-ttu-id="d17ba-142">checkArrays</span><span class="sxs-lookup"><span data-stu-id="d17ba-142">checkArrays</span></span> | <span data-ttu-id="d17ba-143">Booleano</span><span class="sxs-lookup"><span data-stu-id="d17ba-143">Bool</span></span> | <span data-ttu-id="d17ba-144">True </span><span class="sxs-lookup"><span data-stu-id="d17ba-144">True</span></span> |
| <span data-ttu-id="d17ba-145">checkObjects</span><span class="sxs-lookup"><span data-stu-id="d17ba-145">checkObjects</span></span> | <span data-ttu-id="d17ba-146">Booleano</span><span class="sxs-lookup"><span data-stu-id="d17ba-146">Bool</span></span> | <span data-ttu-id="d17ba-147">True </span><span class="sxs-lookup"><span data-stu-id="d17ba-147">True</span></span> |


<span data-ttu-id="d17ba-148">Hello seguente utilizza [non](resource-group-template-functions-logical.md#not) con **è uguale a**.</span><span class="sxs-lookup"><span data-stu-id="d17ba-148">hello following example uses [not](resource-group-template-functions-logical.md#not) with **equals**.</span></span>

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

<span data-ttu-id="d17ba-149">output di Hello hello sopra riportato è:</span><span class="sxs-lookup"><span data-stu-id="d17ba-149">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="d17ba-150">Nome</span><span class="sxs-lookup"><span data-stu-id="d17ba-150">Name</span></span> | <span data-ttu-id="d17ba-151">Tipo</span><span class="sxs-lookup"><span data-stu-id="d17ba-151">Type</span></span> | <span data-ttu-id="d17ba-152">Valore</span><span class="sxs-lookup"><span data-stu-id="d17ba-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d17ba-153">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="d17ba-153">checkNotEquals</span></span> | <span data-ttu-id="d17ba-154">Booleano</span><span class="sxs-lookup"><span data-stu-id="d17ba-154">Bool</span></span> | <span data-ttu-id="d17ba-155">True </span><span class="sxs-lookup"><span data-stu-id="d17ba-155">True</span></span> |


## <a name="greater"></a><span data-ttu-id="d17ba-156">greater</span><span class="sxs-lookup"><span data-stu-id="d17ba-156">greater</span></span>
`greater(arg1, arg2)`

<span data-ttu-id="d17ba-157">Controlla se il primo valore di hello è maggiore del secondo valore hello.</span><span class="sxs-lookup"><span data-stu-id="d17ba-157">Checks whether hello first value is greater than hello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="d17ba-158">parameters</span><span class="sxs-lookup"><span data-stu-id="d17ba-158">Parameters</span></span>

| <span data-ttu-id="d17ba-159">Parametro</span><span class="sxs-lookup"><span data-stu-id="d17ba-159">Parameter</span></span> | <span data-ttu-id="d17ba-160">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d17ba-160">Required</span></span> | <span data-ttu-id="d17ba-161">Tipo</span><span class="sxs-lookup"><span data-stu-id="d17ba-161">Type</span></span> | <span data-ttu-id="d17ba-162">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d17ba-162">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d17ba-163">arg1</span><span class="sxs-lookup"><span data-stu-id="d17ba-163">arg1</span></span> |<span data-ttu-id="d17ba-164">Sì</span><span class="sxs-lookup"><span data-stu-id="d17ba-164">Yes</span></span> |<span data-ttu-id="d17ba-165">int o stringa</span><span class="sxs-lookup"><span data-stu-id="d17ba-165">int or string</span></span> |<span data-ttu-id="d17ba-166">primo valore Hello per confronto maggiore di hello.</span><span class="sxs-lookup"><span data-stu-id="d17ba-166">hello first value for hello greater comparison.</span></span> |
| <span data-ttu-id="d17ba-167">arg2</span><span class="sxs-lookup"><span data-stu-id="d17ba-167">arg2</span></span> |<span data-ttu-id="d17ba-168">Sì</span><span class="sxs-lookup"><span data-stu-id="d17ba-168">Yes</span></span> |<span data-ttu-id="d17ba-169">int o stringa</span><span class="sxs-lookup"><span data-stu-id="d17ba-169">int or string</span></span> |<span data-ttu-id="d17ba-170">secondo valore Hello per confronto maggiore di hello.</span><span class="sxs-lookup"><span data-stu-id="d17ba-170">hello second value for hello greater comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d17ba-171">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="d17ba-171">Return value</span></span>

<span data-ttu-id="d17ba-172">Restituisce **True** se hello primo valore è maggiore del secondo valore hello; in caso contrario, **False**.</span><span class="sxs-lookup"><span data-stu-id="d17ba-172">Returns **True** if hello first value is greater than hello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="d17ba-173">Esempio</span><span class="sxs-lookup"><span data-stu-id="d17ba-173">Example</span></span>

<span data-ttu-id="d17ba-174">modello di esempio Hello controlla se un valore di hello è maggiore di hello altri.</span><span class="sxs-lookup"><span data-stu-id="d17ba-174">hello example template checks whether hello one value is greater than hello other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[greater(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[greater(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="d17ba-175">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="d17ba-175">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d17ba-176">Nome</span><span class="sxs-lookup"><span data-stu-id="d17ba-176">Name</span></span> | <span data-ttu-id="d17ba-177">Tipo</span><span class="sxs-lookup"><span data-stu-id="d17ba-177">Type</span></span> | <span data-ttu-id="d17ba-178">Valore</span><span class="sxs-lookup"><span data-stu-id="d17ba-178">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d17ba-179">checkInts</span><span class="sxs-lookup"><span data-stu-id="d17ba-179">checkInts</span></span> | <span data-ttu-id="d17ba-180">Booleano</span><span class="sxs-lookup"><span data-stu-id="d17ba-180">Bool</span></span> | <span data-ttu-id="d17ba-181">False</span><span class="sxs-lookup"><span data-stu-id="d17ba-181">False</span></span> |
| <span data-ttu-id="d17ba-182">checkStrings</span><span class="sxs-lookup"><span data-stu-id="d17ba-182">checkStrings</span></span> | <span data-ttu-id="d17ba-183">Booleano</span><span class="sxs-lookup"><span data-stu-id="d17ba-183">Bool</span></span> | <span data-ttu-id="d17ba-184">True </span><span class="sxs-lookup"><span data-stu-id="d17ba-184">True</span></span> |


## <a name="greaterorequals"></a><span data-ttu-id="d17ba-185">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="d17ba-185">greaterOrEquals</span></span>
`greaterOrEquals(arg1, arg2)`

<span data-ttu-id="d17ba-186">Controlla se hello primo valore è maggiore o uguale toohello secondo valore.</span><span class="sxs-lookup"><span data-stu-id="d17ba-186">Checks whether hello first value is greater than or equal toohello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="d17ba-187">parameters</span><span class="sxs-lookup"><span data-stu-id="d17ba-187">Parameters</span></span>

| <span data-ttu-id="d17ba-188">Parametro</span><span class="sxs-lookup"><span data-stu-id="d17ba-188">Parameter</span></span> | <span data-ttu-id="d17ba-189">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d17ba-189">Required</span></span> | <span data-ttu-id="d17ba-190">Tipo</span><span class="sxs-lookup"><span data-stu-id="d17ba-190">Type</span></span> | <span data-ttu-id="d17ba-191">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d17ba-191">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d17ba-192">arg1</span><span class="sxs-lookup"><span data-stu-id="d17ba-192">arg1</span></span> |<span data-ttu-id="d17ba-193">Sì</span><span class="sxs-lookup"><span data-stu-id="d17ba-193">Yes</span></span> |<span data-ttu-id="d17ba-194">int o stringa</span><span class="sxs-lookup"><span data-stu-id="d17ba-194">int or string</span></span> |<span data-ttu-id="d17ba-195">primo valore Hello per il confronto maggiore o uguale di hello.</span><span class="sxs-lookup"><span data-stu-id="d17ba-195">hello first value for hello greater or equal comparison.</span></span> |
| <span data-ttu-id="d17ba-196">arg2</span><span class="sxs-lookup"><span data-stu-id="d17ba-196">arg2</span></span> |<span data-ttu-id="d17ba-197">Sì</span><span class="sxs-lookup"><span data-stu-id="d17ba-197">Yes</span></span> |<span data-ttu-id="d17ba-198">int o stringa</span><span class="sxs-lookup"><span data-stu-id="d17ba-198">int or string</span></span> |<span data-ttu-id="d17ba-199">secondo valore Hello per il confronto maggiore o uguale di hello.</span><span class="sxs-lookup"><span data-stu-id="d17ba-199">hello second value for hello greater or equal comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d17ba-200">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="d17ba-200">Return value</span></span>

<span data-ttu-id="d17ba-201">Restituisce **True** se hello primo valore è maggiore o uguale toohello secondo; in caso contrario, **False**.</span><span class="sxs-lookup"><span data-stu-id="d17ba-201">Returns **True** if hello first value is greater than or equal toohello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="d17ba-202">Esempio</span><span class="sxs-lookup"><span data-stu-id="d17ba-202">Example</span></span>

<span data-ttu-id="d17ba-203">modello di esempio Hello controlla se un valore di hello è maggiore o uguale toohello altri.</span><span class="sxs-lookup"><span data-stu-id="d17ba-203">hello example template checks whether hello one value is greater than or equal toohello other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[greaterOrEquals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[greaterOrEquals(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="d17ba-204">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="d17ba-204">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d17ba-205">Nome</span><span class="sxs-lookup"><span data-stu-id="d17ba-205">Name</span></span> | <span data-ttu-id="d17ba-206">Tipo</span><span class="sxs-lookup"><span data-stu-id="d17ba-206">Type</span></span> | <span data-ttu-id="d17ba-207">Valore</span><span class="sxs-lookup"><span data-stu-id="d17ba-207">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d17ba-208">checkInts</span><span class="sxs-lookup"><span data-stu-id="d17ba-208">checkInts</span></span> | <span data-ttu-id="d17ba-209">Booleano</span><span class="sxs-lookup"><span data-stu-id="d17ba-209">Bool</span></span> | <span data-ttu-id="d17ba-210">False</span><span class="sxs-lookup"><span data-stu-id="d17ba-210">False</span></span> |
| <span data-ttu-id="d17ba-211">checkStrings</span><span class="sxs-lookup"><span data-stu-id="d17ba-211">checkStrings</span></span> | <span data-ttu-id="d17ba-212">Booleano</span><span class="sxs-lookup"><span data-stu-id="d17ba-212">Bool</span></span> | <span data-ttu-id="d17ba-213">True </span><span class="sxs-lookup"><span data-stu-id="d17ba-213">True</span></span> |



## <a name="less"></a><span data-ttu-id="d17ba-214">less</span><span class="sxs-lookup"><span data-stu-id="d17ba-214">less</span></span>
`less(arg1, arg2)`

<span data-ttu-id="d17ba-215">Controlla se hello primo valore è minore di hello secondo valore.</span><span class="sxs-lookup"><span data-stu-id="d17ba-215">Checks whether hello first value is less than hello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="d17ba-216">parameters</span><span class="sxs-lookup"><span data-stu-id="d17ba-216">Parameters</span></span>

| <span data-ttu-id="d17ba-217">Parametro</span><span class="sxs-lookup"><span data-stu-id="d17ba-217">Parameter</span></span> | <span data-ttu-id="d17ba-218">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d17ba-218">Required</span></span> | <span data-ttu-id="d17ba-219">Tipo</span><span class="sxs-lookup"><span data-stu-id="d17ba-219">Type</span></span> | <span data-ttu-id="d17ba-220">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d17ba-220">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d17ba-221">arg1</span><span class="sxs-lookup"><span data-stu-id="d17ba-221">arg1</span></span> |<span data-ttu-id="d17ba-222">Sì</span><span class="sxs-lookup"><span data-stu-id="d17ba-222">Yes</span></span> |<span data-ttu-id="d17ba-223">int o stringa</span><span class="sxs-lookup"><span data-stu-id="d17ba-223">int or string</span></span> |<span data-ttu-id="d17ba-224">primo valore Hello per hello meno confronto.</span><span class="sxs-lookup"><span data-stu-id="d17ba-224">hello first value for hello less comparison.</span></span> |
| <span data-ttu-id="d17ba-225">arg2</span><span class="sxs-lookup"><span data-stu-id="d17ba-225">arg2</span></span> |<span data-ttu-id="d17ba-226">Sì</span><span class="sxs-lookup"><span data-stu-id="d17ba-226">Yes</span></span> |<span data-ttu-id="d17ba-227">int o stringa</span><span class="sxs-lookup"><span data-stu-id="d17ba-227">int or string</span></span> |<span data-ttu-id="d17ba-228">secondo valore Hello per hello meno confronto.</span><span class="sxs-lookup"><span data-stu-id="d17ba-228">hello second value for hello less comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d17ba-229">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="d17ba-229">Return value</span></span>

<span data-ttu-id="d17ba-230">Restituisce **True** se hello primo valore è minore di hello secondo valore; in caso contrario, **False**.</span><span class="sxs-lookup"><span data-stu-id="d17ba-230">Returns **True** if hello first value is less than hello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="d17ba-231">Esempio</span><span class="sxs-lookup"><span data-stu-id="d17ba-231">Example</span></span>

<span data-ttu-id="d17ba-232">modello di esempio Hello controlla se un valore di hello è minore di hello altri.</span><span class="sxs-lookup"><span data-stu-id="d17ba-232">hello example template checks whether hello one value is less than hello other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[less(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[less(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="d17ba-233">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="d17ba-233">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d17ba-234">Nome</span><span class="sxs-lookup"><span data-stu-id="d17ba-234">Name</span></span> | <span data-ttu-id="d17ba-235">Tipo</span><span class="sxs-lookup"><span data-stu-id="d17ba-235">Type</span></span> | <span data-ttu-id="d17ba-236">Valore</span><span class="sxs-lookup"><span data-stu-id="d17ba-236">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d17ba-237">checkInts</span><span class="sxs-lookup"><span data-stu-id="d17ba-237">checkInts</span></span> | <span data-ttu-id="d17ba-238">Booleano</span><span class="sxs-lookup"><span data-stu-id="d17ba-238">Bool</span></span> | <span data-ttu-id="d17ba-239">True </span><span class="sxs-lookup"><span data-stu-id="d17ba-239">True</span></span> |
| <span data-ttu-id="d17ba-240">checkStrings</span><span class="sxs-lookup"><span data-stu-id="d17ba-240">checkStrings</span></span> | <span data-ttu-id="d17ba-241">Booleano</span><span class="sxs-lookup"><span data-stu-id="d17ba-241">Bool</span></span> | <span data-ttu-id="d17ba-242">False</span><span class="sxs-lookup"><span data-stu-id="d17ba-242">False</span></span> |


## <a name="lessorequals"></a><span data-ttu-id="d17ba-243">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="d17ba-243">lessOrEquals</span></span>
`lessOrEquals(arg1, arg2)`

<span data-ttu-id="d17ba-244">Controlla se il primo valore di hello è minore o uguale toohello secondo valore.</span><span class="sxs-lookup"><span data-stu-id="d17ba-244">Checks whether hello first value is less than or equal toohello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="d17ba-245">parameters</span><span class="sxs-lookup"><span data-stu-id="d17ba-245">Parameters</span></span>

| <span data-ttu-id="d17ba-246">Parametro</span><span class="sxs-lookup"><span data-stu-id="d17ba-246">Parameter</span></span> | <span data-ttu-id="d17ba-247">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d17ba-247">Required</span></span> | <span data-ttu-id="d17ba-248">Tipo</span><span class="sxs-lookup"><span data-stu-id="d17ba-248">Type</span></span> | <span data-ttu-id="d17ba-249">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d17ba-249">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d17ba-250">arg1</span><span class="sxs-lookup"><span data-stu-id="d17ba-250">arg1</span></span> |<span data-ttu-id="d17ba-251">Sì</span><span class="sxs-lookup"><span data-stu-id="d17ba-251">Yes</span></span> |<span data-ttu-id="d17ba-252">int o stringa</span><span class="sxs-lookup"><span data-stu-id="d17ba-252">int or string</span></span> |<span data-ttu-id="d17ba-253">Hello primo valore per hello minore o uguale a confronto.</span><span class="sxs-lookup"><span data-stu-id="d17ba-253">hello first value for hello less or equals comparison.</span></span> |
| <span data-ttu-id="d17ba-254">arg2</span><span class="sxs-lookup"><span data-stu-id="d17ba-254">arg2</span></span> |<span data-ttu-id="d17ba-255">Sì</span><span class="sxs-lookup"><span data-stu-id="d17ba-255">Yes</span></span> |<span data-ttu-id="d17ba-256">int o stringa</span><span class="sxs-lookup"><span data-stu-id="d17ba-256">int or string</span></span> |<span data-ttu-id="d17ba-257">secondo valore di Hello per hello minore o uguale a confronto.</span><span class="sxs-lookup"><span data-stu-id="d17ba-257">hello second value for hello less or equals comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d17ba-258">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="d17ba-258">Return value</span></span>

<span data-ttu-id="d17ba-259">Restituisce **True** se hello primo valore è minore o uguale toohello secondo valore; in caso contrario, **False**.</span><span class="sxs-lookup"><span data-stu-id="d17ba-259">Returns **True** if hello first value is less than or equal toohello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="d17ba-260">Esempio</span><span class="sxs-lookup"><span data-stu-id="d17ba-260">Example</span></span>

<span data-ttu-id="d17ba-261">Hello modello di esempio controlla se un valore di hello è minore o uguale toohello altri.</span><span class="sxs-lookup"><span data-stu-id="d17ba-261">hello example template checks whether hello one value is less than or equal toohello other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[lessOrEquals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[lessOrEquals(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="d17ba-262">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="d17ba-262">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d17ba-263">Nome</span><span class="sxs-lookup"><span data-stu-id="d17ba-263">Name</span></span> | <span data-ttu-id="d17ba-264">Tipo</span><span class="sxs-lookup"><span data-stu-id="d17ba-264">Type</span></span> | <span data-ttu-id="d17ba-265">Valore</span><span class="sxs-lookup"><span data-stu-id="d17ba-265">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d17ba-266">checkInts</span><span class="sxs-lookup"><span data-stu-id="d17ba-266">checkInts</span></span> | <span data-ttu-id="d17ba-267">Booleano</span><span class="sxs-lookup"><span data-stu-id="d17ba-267">Bool</span></span> | <span data-ttu-id="d17ba-268">True </span><span class="sxs-lookup"><span data-stu-id="d17ba-268">True</span></span> |
| <span data-ttu-id="d17ba-269">checkStrings</span><span class="sxs-lookup"><span data-stu-id="d17ba-269">checkStrings</span></span> | <span data-ttu-id="d17ba-270">Booleano</span><span class="sxs-lookup"><span data-stu-id="d17ba-270">Bool</span></span> | <span data-ttu-id="d17ba-271">False</span><span class="sxs-lookup"><span data-stu-id="d17ba-271">False</span></span> |



## <a name="next-steps"></a><span data-ttu-id="d17ba-272">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d17ba-272">Next steps</span></span>
* <span data-ttu-id="d17ba-273">Per una descrizione delle sezioni hello in un modello di gestione risorse di Azure, vedere [modelli Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d17ba-273">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="d17ba-274">toomerge più modelli, vedere [con modelli collegati con Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d17ba-274">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="d17ba-275">tooiterate un numero specificato di volte durante la creazione di un tipo di risorsa, vedere [creare più istanze delle risorse in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="d17ba-275">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="d17ba-276">toosee come modello hello toodeploy è stato creato, vedere [distribuire un'applicazione con il modello di gestione risorse di Azure](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="d17ba-276">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

