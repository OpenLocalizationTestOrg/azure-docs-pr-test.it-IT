---
title: Funzioni di confronto del modello di Azure Resource Manager | Microsoft Docs
description: "Informazioni sulle funzioni che è possibile usare in un modello di Azure Resource Manager per confrontare valori."
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
ms.openlocfilehash: 521e5ed06c138bcd374913588f06a2e6c1e99963
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="comparison-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="fba93-103">Funzioni di confronto per i modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fba93-103">Comparison functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="fba93-104">Resource Manager include numerose funzioni per l'esecuzione di confronti nei modelli.</span><span class="sxs-lookup"><span data-stu-id="fba93-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="fba93-105">equals</span><span class="sxs-lookup"><span data-stu-id="fba93-105">equals</span></span>](#equals)
* [<span data-ttu-id="fba93-106">greater</span><span class="sxs-lookup"><span data-stu-id="fba93-106">greater</span></span>](#greater)
* [<span data-ttu-id="fba93-107">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="fba93-107">greaterOrEquals</span></span>](#greaterorequals)
* [<span data-ttu-id="fba93-108">less</span><span class="sxs-lookup"><span data-stu-id="fba93-108">less</span></span>](#less)
* [<span data-ttu-id="fba93-109">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="fba93-109">lessOrEquals</span></span>](#lessorequals)

## <a name="equals"></a><span data-ttu-id="fba93-110">equals</span><span class="sxs-lookup"><span data-stu-id="fba93-110">equals</span></span>
`equals(arg1, arg2)`

<span data-ttu-id="fba93-111">Controlla se due valori sono uguali tra loro.</span><span class="sxs-lookup"><span data-stu-id="fba93-111">Checks whether two values equal each other.</span></span>

### <a name="parameters"></a><span data-ttu-id="fba93-112">Parametri</span><span class="sxs-lookup"><span data-stu-id="fba93-112">Parameters</span></span>

| <span data-ttu-id="fba93-113">Parametro</span><span class="sxs-lookup"><span data-stu-id="fba93-113">Parameter</span></span> | <span data-ttu-id="fba93-114">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="fba93-114">Required</span></span> | <span data-ttu-id="fba93-115">Tipo</span><span class="sxs-lookup"><span data-stu-id="fba93-115">Type</span></span> | <span data-ttu-id="fba93-116">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fba93-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="fba93-117">arg1</span><span class="sxs-lookup"><span data-stu-id="fba93-117">arg1</span></span> |<span data-ttu-id="fba93-118">Sì</span><span class="sxs-lookup"><span data-stu-id="fba93-118">Yes</span></span> |<span data-ttu-id="fba93-119">int, stringa, matrice o oggetto</span><span class="sxs-lookup"><span data-stu-id="fba93-119">int, string, array, or object</span></span> |<span data-ttu-id="fba93-120">Il primo valore per verificare l'uguaglianza.</span><span class="sxs-lookup"><span data-stu-id="fba93-120">The first value to check for equality.</span></span> |
| <span data-ttu-id="fba93-121">arg2</span><span class="sxs-lookup"><span data-stu-id="fba93-121">arg2</span></span> |<span data-ttu-id="fba93-122">Sì</span><span class="sxs-lookup"><span data-stu-id="fba93-122">Yes</span></span> |<span data-ttu-id="fba93-123">int, stringa, matrice o oggetto</span><span class="sxs-lookup"><span data-stu-id="fba93-123">int, string, array, or object</span></span> |<span data-ttu-id="fba93-124">Il secondo valore per verificare l'uguaglianza.</span><span class="sxs-lookup"><span data-stu-id="fba93-124">The second value to check for equality.</span></span> |

### <a name="return-value"></a><span data-ttu-id="fba93-125">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="fba93-125">Return value</span></span>

<span data-ttu-id="fba93-126">Restituisce **True** se i valori sono uguali; in caso contrario, restituisce **False**.</span><span class="sxs-lookup"><span data-stu-id="fba93-126">Returns **True** if the values are equal; otherwise, **False**.</span></span>

### <a name="remarks"></a><span data-ttu-id="fba93-127">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="fba93-127">Remarks</span></span>

<span data-ttu-id="fba93-128">La funzione uguale a viene spesso usata con l'elemento `condition` per verificare se la risorsa viene distribuita.</span><span class="sxs-lookup"><span data-stu-id="fba93-128">The equals function is often used with the `condition` element to test whether a resource is deployed.</span></span>

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

### <a name="example"></a><span data-ttu-id="fba93-129">Esempio</span><span class="sxs-lookup"><span data-stu-id="fba93-129">Example</span></span>

<span data-ttu-id="fba93-130">Il modello di esempio controlla tipi diversi di valori per verificarne l'uguaglianza.</span><span class="sxs-lookup"><span data-stu-id="fba93-130">The example template checks different types of values for equality.</span></span> <span data-ttu-id="fba93-131">Tutti i valori predefiniti restituiscono True.</span><span class="sxs-lookup"><span data-stu-id="fba93-131">All the default values return True.</span></span>

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

<span data-ttu-id="fba93-132">L'output dell'esempio precedente con i valori predefiniti è il seguente:</span><span class="sxs-lookup"><span data-stu-id="fba93-132">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="fba93-133">Nome</span><span class="sxs-lookup"><span data-stu-id="fba93-133">Name</span></span> | <span data-ttu-id="fba93-134">Tipo</span><span class="sxs-lookup"><span data-stu-id="fba93-134">Type</span></span> | <span data-ttu-id="fba93-135">Valore</span><span class="sxs-lookup"><span data-stu-id="fba93-135">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="fba93-136">checkInts</span><span class="sxs-lookup"><span data-stu-id="fba93-136">checkInts</span></span> | <span data-ttu-id="fba93-137">Booleano</span><span class="sxs-lookup"><span data-stu-id="fba93-137">Bool</span></span> | <span data-ttu-id="fba93-138">True </span><span class="sxs-lookup"><span data-stu-id="fba93-138">True</span></span> |
| <span data-ttu-id="fba93-139">checkStrings</span><span class="sxs-lookup"><span data-stu-id="fba93-139">checkStrings</span></span> | <span data-ttu-id="fba93-140">Booleano</span><span class="sxs-lookup"><span data-stu-id="fba93-140">Bool</span></span> | <span data-ttu-id="fba93-141">True </span><span class="sxs-lookup"><span data-stu-id="fba93-141">True</span></span> |
| <span data-ttu-id="fba93-142">checkArrays</span><span class="sxs-lookup"><span data-stu-id="fba93-142">checkArrays</span></span> | <span data-ttu-id="fba93-143">Booleano</span><span class="sxs-lookup"><span data-stu-id="fba93-143">Bool</span></span> | <span data-ttu-id="fba93-144">True </span><span class="sxs-lookup"><span data-stu-id="fba93-144">True</span></span> |
| <span data-ttu-id="fba93-145">checkObjects</span><span class="sxs-lookup"><span data-stu-id="fba93-145">checkObjects</span></span> | <span data-ttu-id="fba93-146">Booleano</span><span class="sxs-lookup"><span data-stu-id="fba93-146">Bool</span></span> | <span data-ttu-id="fba93-147">True </span><span class="sxs-lookup"><span data-stu-id="fba93-147">True</span></span> |


<span data-ttu-id="fba93-148">L'esempio seguente usa [not](resource-group-template-functions-logical.md#not) con **equals**.</span><span class="sxs-lookup"><span data-stu-id="fba93-148">The following example uses [not](resource-group-template-functions-logical.md#not) with **equals**.</span></span>

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

<span data-ttu-id="fba93-149">L'output dell'esempio precedente è:</span><span class="sxs-lookup"><span data-stu-id="fba93-149">The output from the preceding example is:</span></span>

| <span data-ttu-id="fba93-150">Nome</span><span class="sxs-lookup"><span data-stu-id="fba93-150">Name</span></span> | <span data-ttu-id="fba93-151">Tipo</span><span class="sxs-lookup"><span data-stu-id="fba93-151">Type</span></span> | <span data-ttu-id="fba93-152">Valore</span><span class="sxs-lookup"><span data-stu-id="fba93-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="fba93-153">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="fba93-153">checkNotEquals</span></span> | <span data-ttu-id="fba93-154">Booleano</span><span class="sxs-lookup"><span data-stu-id="fba93-154">Bool</span></span> | <span data-ttu-id="fba93-155">True </span><span class="sxs-lookup"><span data-stu-id="fba93-155">True</span></span> |


## <a name="greater"></a><span data-ttu-id="fba93-156">greater</span><span class="sxs-lookup"><span data-stu-id="fba93-156">greater</span></span>
`greater(arg1, arg2)`

<span data-ttu-id="fba93-157">Controlla se il primo valore è maggiore del secondo.</span><span class="sxs-lookup"><span data-stu-id="fba93-157">Checks whether the first value is greater than the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="fba93-158">Parametri</span><span class="sxs-lookup"><span data-stu-id="fba93-158">Parameters</span></span>

| <span data-ttu-id="fba93-159">Parametro</span><span class="sxs-lookup"><span data-stu-id="fba93-159">Parameter</span></span> | <span data-ttu-id="fba93-160">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="fba93-160">Required</span></span> | <span data-ttu-id="fba93-161">Tipo</span><span class="sxs-lookup"><span data-stu-id="fba93-161">Type</span></span> | <span data-ttu-id="fba93-162">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fba93-162">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="fba93-163">arg1</span><span class="sxs-lookup"><span data-stu-id="fba93-163">arg1</span></span> |<span data-ttu-id="fba93-164">Sì</span><span class="sxs-lookup"><span data-stu-id="fba93-164">Yes</span></span> |<span data-ttu-id="fba93-165">int o stringa</span><span class="sxs-lookup"><span data-stu-id="fba93-165">int or string</span></span> |<span data-ttu-id="fba93-166">Il primo valore per il confronto del maggiore.</span><span class="sxs-lookup"><span data-stu-id="fba93-166">The first value for the greater comparison.</span></span> |
| <span data-ttu-id="fba93-167">arg2</span><span class="sxs-lookup"><span data-stu-id="fba93-167">arg2</span></span> |<span data-ttu-id="fba93-168">Sì</span><span class="sxs-lookup"><span data-stu-id="fba93-168">Yes</span></span> |<span data-ttu-id="fba93-169">int o stringa</span><span class="sxs-lookup"><span data-stu-id="fba93-169">int or string</span></span> |<span data-ttu-id="fba93-170">Il secondo valore per il confronto del maggiore.</span><span class="sxs-lookup"><span data-stu-id="fba93-170">The second value for the greater comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="fba93-171">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="fba93-171">Return value</span></span>

<span data-ttu-id="fba93-172">Restituisce **True** se il primo valore è maggiore del secondo; in caso contrario, restituisce **False**.</span><span class="sxs-lookup"><span data-stu-id="fba93-172">Returns **True** if the first value is greater than the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="fba93-173">Esempio</span><span class="sxs-lookup"><span data-stu-id="fba93-173">Example</span></span>

<span data-ttu-id="fba93-174">Il modello di esempio controlla se un valore è maggiore dell'altro.</span><span class="sxs-lookup"><span data-stu-id="fba93-174">The example template checks whether the one value is greater than the other.</span></span>

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

<span data-ttu-id="fba93-175">L'output dell'esempio precedente con i valori predefiniti è il seguente:</span><span class="sxs-lookup"><span data-stu-id="fba93-175">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="fba93-176">Nome</span><span class="sxs-lookup"><span data-stu-id="fba93-176">Name</span></span> | <span data-ttu-id="fba93-177">Tipo</span><span class="sxs-lookup"><span data-stu-id="fba93-177">Type</span></span> | <span data-ttu-id="fba93-178">Valore</span><span class="sxs-lookup"><span data-stu-id="fba93-178">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="fba93-179">checkInts</span><span class="sxs-lookup"><span data-stu-id="fba93-179">checkInts</span></span> | <span data-ttu-id="fba93-180">Booleano</span><span class="sxs-lookup"><span data-stu-id="fba93-180">Bool</span></span> | <span data-ttu-id="fba93-181">False</span><span class="sxs-lookup"><span data-stu-id="fba93-181">False</span></span> |
| <span data-ttu-id="fba93-182">checkStrings</span><span class="sxs-lookup"><span data-stu-id="fba93-182">checkStrings</span></span> | <span data-ttu-id="fba93-183">Booleano</span><span class="sxs-lookup"><span data-stu-id="fba93-183">Bool</span></span> | <span data-ttu-id="fba93-184">True </span><span class="sxs-lookup"><span data-stu-id="fba93-184">True</span></span> |


## <a name="greaterorequals"></a><span data-ttu-id="fba93-185">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="fba93-185">greaterOrEquals</span></span>
`greaterOrEquals(arg1, arg2)`

<span data-ttu-id="fba93-186">Controlla se il primo valore è maggiore o uguale al secondo valore.</span><span class="sxs-lookup"><span data-stu-id="fba93-186">Checks whether the first value is greater than or equal to the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="fba93-187">Parametri</span><span class="sxs-lookup"><span data-stu-id="fba93-187">Parameters</span></span>

| <span data-ttu-id="fba93-188">Parametro</span><span class="sxs-lookup"><span data-stu-id="fba93-188">Parameter</span></span> | <span data-ttu-id="fba93-189">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="fba93-189">Required</span></span> | <span data-ttu-id="fba93-190">Tipo</span><span class="sxs-lookup"><span data-stu-id="fba93-190">Type</span></span> | <span data-ttu-id="fba93-191">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fba93-191">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="fba93-192">arg1</span><span class="sxs-lookup"><span data-stu-id="fba93-192">arg1</span></span> |<span data-ttu-id="fba93-193">Sì</span><span class="sxs-lookup"><span data-stu-id="fba93-193">Yes</span></span> |<span data-ttu-id="fba93-194">int o stringa</span><span class="sxs-lookup"><span data-stu-id="fba93-194">int or string</span></span> |<span data-ttu-id="fba93-195">Il primo valore per il confronto del maggiore e dell'uguaglianza.</span><span class="sxs-lookup"><span data-stu-id="fba93-195">The first value for the greater or equal comparison.</span></span> |
| <span data-ttu-id="fba93-196">arg2</span><span class="sxs-lookup"><span data-stu-id="fba93-196">arg2</span></span> |<span data-ttu-id="fba93-197">Sì</span><span class="sxs-lookup"><span data-stu-id="fba93-197">Yes</span></span> |<span data-ttu-id="fba93-198">int o stringa</span><span class="sxs-lookup"><span data-stu-id="fba93-198">int or string</span></span> |<span data-ttu-id="fba93-199">Il secondo valore per il confronto del maggiore e dell'uguaglianza.</span><span class="sxs-lookup"><span data-stu-id="fba93-199">The second value for the greater or equal comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="fba93-200">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="fba93-200">Return value</span></span>

<span data-ttu-id="fba93-201">Restituisce **True** se il primo valore è maggiore o uguale al secondo; in caso contrario, restituisce **False**.</span><span class="sxs-lookup"><span data-stu-id="fba93-201">Returns **True** if the first value is greater than or equal to the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="fba93-202">Esempio</span><span class="sxs-lookup"><span data-stu-id="fba93-202">Example</span></span>

<span data-ttu-id="fba93-203">Il modello di esempio controlla se un valore è maggiore o uguale all'altro.</span><span class="sxs-lookup"><span data-stu-id="fba93-203">The example template checks whether the one value is greater than or equal to the other.</span></span>

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

<span data-ttu-id="fba93-204">L'output dell'esempio precedente con i valori predefiniti è il seguente:</span><span class="sxs-lookup"><span data-stu-id="fba93-204">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="fba93-205">Nome</span><span class="sxs-lookup"><span data-stu-id="fba93-205">Name</span></span> | <span data-ttu-id="fba93-206">Tipo</span><span class="sxs-lookup"><span data-stu-id="fba93-206">Type</span></span> | <span data-ttu-id="fba93-207">Valore</span><span class="sxs-lookup"><span data-stu-id="fba93-207">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="fba93-208">checkInts</span><span class="sxs-lookup"><span data-stu-id="fba93-208">checkInts</span></span> | <span data-ttu-id="fba93-209">Booleano</span><span class="sxs-lookup"><span data-stu-id="fba93-209">Bool</span></span> | <span data-ttu-id="fba93-210">False</span><span class="sxs-lookup"><span data-stu-id="fba93-210">False</span></span> |
| <span data-ttu-id="fba93-211">checkStrings</span><span class="sxs-lookup"><span data-stu-id="fba93-211">checkStrings</span></span> | <span data-ttu-id="fba93-212">Booleano</span><span class="sxs-lookup"><span data-stu-id="fba93-212">Bool</span></span> | <span data-ttu-id="fba93-213">True </span><span class="sxs-lookup"><span data-stu-id="fba93-213">True</span></span> |



## <a name="less"></a><span data-ttu-id="fba93-214">less</span><span class="sxs-lookup"><span data-stu-id="fba93-214">less</span></span>
`less(arg1, arg2)`

<span data-ttu-id="fba93-215">Controlla se il primo valore è minore del secondo.</span><span class="sxs-lookup"><span data-stu-id="fba93-215">Checks whether the first value is less than the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="fba93-216">Parametri</span><span class="sxs-lookup"><span data-stu-id="fba93-216">Parameters</span></span>

| <span data-ttu-id="fba93-217">Parametro</span><span class="sxs-lookup"><span data-stu-id="fba93-217">Parameter</span></span> | <span data-ttu-id="fba93-218">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="fba93-218">Required</span></span> | <span data-ttu-id="fba93-219">Tipo</span><span class="sxs-lookup"><span data-stu-id="fba93-219">Type</span></span> | <span data-ttu-id="fba93-220">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fba93-220">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="fba93-221">arg1</span><span class="sxs-lookup"><span data-stu-id="fba93-221">arg1</span></span> |<span data-ttu-id="fba93-222">Sì</span><span class="sxs-lookup"><span data-stu-id="fba93-222">Yes</span></span> |<span data-ttu-id="fba93-223">int o stringa</span><span class="sxs-lookup"><span data-stu-id="fba93-223">int or string</span></span> |<span data-ttu-id="fba93-224">Il primo valore per il confronto del minore.</span><span class="sxs-lookup"><span data-stu-id="fba93-224">The first value for the less comparison.</span></span> |
| <span data-ttu-id="fba93-225">arg2</span><span class="sxs-lookup"><span data-stu-id="fba93-225">arg2</span></span> |<span data-ttu-id="fba93-226">Sì</span><span class="sxs-lookup"><span data-stu-id="fba93-226">Yes</span></span> |<span data-ttu-id="fba93-227">int o stringa</span><span class="sxs-lookup"><span data-stu-id="fba93-227">int or string</span></span> |<span data-ttu-id="fba93-228">Il secondo valore per il confronto del minore.</span><span class="sxs-lookup"><span data-stu-id="fba93-228">The second value for the less comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="fba93-229">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="fba93-229">Return value</span></span>

<span data-ttu-id="fba93-230">Restituisce **True** se il primo valore è inferiore al secondo; in caso contrario, restituisce **False**.</span><span class="sxs-lookup"><span data-stu-id="fba93-230">Returns **True** if the first value is less than the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="fba93-231">Esempio</span><span class="sxs-lookup"><span data-stu-id="fba93-231">Example</span></span>

<span data-ttu-id="fba93-232">Il modello di esempio controlla se un valore è minore dell'altro.</span><span class="sxs-lookup"><span data-stu-id="fba93-232">The example template checks whether the one value is less than the other.</span></span>

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

<span data-ttu-id="fba93-233">L'output dell'esempio precedente con i valori predefiniti è il seguente:</span><span class="sxs-lookup"><span data-stu-id="fba93-233">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="fba93-234">Nome</span><span class="sxs-lookup"><span data-stu-id="fba93-234">Name</span></span> | <span data-ttu-id="fba93-235">Tipo</span><span class="sxs-lookup"><span data-stu-id="fba93-235">Type</span></span> | <span data-ttu-id="fba93-236">Valore</span><span class="sxs-lookup"><span data-stu-id="fba93-236">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="fba93-237">checkInts</span><span class="sxs-lookup"><span data-stu-id="fba93-237">checkInts</span></span> | <span data-ttu-id="fba93-238">Booleano</span><span class="sxs-lookup"><span data-stu-id="fba93-238">Bool</span></span> | <span data-ttu-id="fba93-239">True </span><span class="sxs-lookup"><span data-stu-id="fba93-239">True</span></span> |
| <span data-ttu-id="fba93-240">checkStrings</span><span class="sxs-lookup"><span data-stu-id="fba93-240">checkStrings</span></span> | <span data-ttu-id="fba93-241">Booleano</span><span class="sxs-lookup"><span data-stu-id="fba93-241">Bool</span></span> | <span data-ttu-id="fba93-242">False</span><span class="sxs-lookup"><span data-stu-id="fba93-242">False</span></span> |


## <a name="lessorequals"></a><span data-ttu-id="fba93-243">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="fba93-243">lessOrEquals</span></span>
`lessOrEquals(arg1, arg2)`

<span data-ttu-id="fba93-244">Controlla se il primo valore è minore o uguale al secondo valore.</span><span class="sxs-lookup"><span data-stu-id="fba93-244">Checks whether the first value is less than or equal to the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="fba93-245">Parametri</span><span class="sxs-lookup"><span data-stu-id="fba93-245">Parameters</span></span>

| <span data-ttu-id="fba93-246">Parametro</span><span class="sxs-lookup"><span data-stu-id="fba93-246">Parameter</span></span> | <span data-ttu-id="fba93-247">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="fba93-247">Required</span></span> | <span data-ttu-id="fba93-248">Tipo</span><span class="sxs-lookup"><span data-stu-id="fba93-248">Type</span></span> | <span data-ttu-id="fba93-249">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fba93-249">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="fba93-250">arg1</span><span class="sxs-lookup"><span data-stu-id="fba93-250">arg1</span></span> |<span data-ttu-id="fba93-251">Sì</span><span class="sxs-lookup"><span data-stu-id="fba93-251">Yes</span></span> |<span data-ttu-id="fba93-252">int o stringa</span><span class="sxs-lookup"><span data-stu-id="fba93-252">int or string</span></span> |<span data-ttu-id="fba93-253">Il primo valore per il confronto del minore o dell'uguaglianza.</span><span class="sxs-lookup"><span data-stu-id="fba93-253">The first value for the less or equals comparison.</span></span> |
| <span data-ttu-id="fba93-254">arg2</span><span class="sxs-lookup"><span data-stu-id="fba93-254">arg2</span></span> |<span data-ttu-id="fba93-255">Sì</span><span class="sxs-lookup"><span data-stu-id="fba93-255">Yes</span></span> |<span data-ttu-id="fba93-256">int o stringa</span><span class="sxs-lookup"><span data-stu-id="fba93-256">int or string</span></span> |<span data-ttu-id="fba93-257">Il secondo valore per il confronto del minore o dell'uguaglianza.</span><span class="sxs-lookup"><span data-stu-id="fba93-257">The second value for the less or equals comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="fba93-258">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="fba93-258">Return value</span></span>

<span data-ttu-id="fba93-259">Restituisce **True** se il primo valore è minore o uguale al secondo; in caso contrario, restituisce **False**.</span><span class="sxs-lookup"><span data-stu-id="fba93-259">Returns **True** if the first value is less than or equal to the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="fba93-260">Esempio</span><span class="sxs-lookup"><span data-stu-id="fba93-260">Example</span></span>

<span data-ttu-id="fba93-261">Il modello di esempio controlla se un valore è minore o uguale all'altro.</span><span class="sxs-lookup"><span data-stu-id="fba93-261">The example template checks whether the one value is less than or equal to the other.</span></span>

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

<span data-ttu-id="fba93-262">L'output dell'esempio precedente con i valori predefiniti è il seguente:</span><span class="sxs-lookup"><span data-stu-id="fba93-262">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="fba93-263">Nome</span><span class="sxs-lookup"><span data-stu-id="fba93-263">Name</span></span> | <span data-ttu-id="fba93-264">Tipo</span><span class="sxs-lookup"><span data-stu-id="fba93-264">Type</span></span> | <span data-ttu-id="fba93-265">Valore</span><span class="sxs-lookup"><span data-stu-id="fba93-265">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="fba93-266">checkInts</span><span class="sxs-lookup"><span data-stu-id="fba93-266">checkInts</span></span> | <span data-ttu-id="fba93-267">Booleano</span><span class="sxs-lookup"><span data-stu-id="fba93-267">Bool</span></span> | <span data-ttu-id="fba93-268">True </span><span class="sxs-lookup"><span data-stu-id="fba93-268">True</span></span> |
| <span data-ttu-id="fba93-269">checkStrings</span><span class="sxs-lookup"><span data-stu-id="fba93-269">checkStrings</span></span> | <span data-ttu-id="fba93-270">Booleano</span><span class="sxs-lookup"><span data-stu-id="fba93-270">Bool</span></span> | <span data-ttu-id="fba93-271">False</span><span class="sxs-lookup"><span data-stu-id="fba93-271">False</span></span> |



## <a name="next-steps"></a><span data-ttu-id="fba93-272">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fba93-272">Next steps</span></span>
* <span data-ttu-id="fba93-273">Per una descrizione delle sezioni in un modello di Azure Resource Manager, vedere [Creazione di modelli di Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="fba93-273">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="fba93-274">Per unire più modelli, vedere [Uso di modelli collegati con Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="fba93-274">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="fba93-275">Per eseguire un'iterazione di un numero di volte specificato durante la creazione di un tipo di risorsa, vedere [Creare più istanze di risorse in Gestione risorse di Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="fba93-275">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="fba93-276">Per informazioni su come distribuire il modello che è stato creato, vedere [Distribuire un'applicazione con un modello di Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="fba93-276">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

