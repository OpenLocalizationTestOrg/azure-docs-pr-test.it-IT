---
title: Funzioni numeriche del modello di Azure Resource Manager | Microsoft Docs
description: "Informazioni sulle funzioni che è possibile usare in un modello di Azure Resource Manager per elaborare i numeri."
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
ms.openlocfilehash: ae0261134b8d4a934048f58d6c679a48a904950b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="numeric-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="741a3-103">Funzioni numeriche per i modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="741a3-103">Numeric functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="741a3-104">Gestione risorse fornisce le funzioni seguenti per usare i numeri interi:</span><span class="sxs-lookup"><span data-stu-id="741a3-104">Resource Manager provides the following functions for working with integers:</span></span>

* [<span data-ttu-id="741a3-105">add</span><span class="sxs-lookup"><span data-stu-id="741a3-105">add</span></span>](#add)
* [<span data-ttu-id="741a3-106">copyIndex</span><span class="sxs-lookup"><span data-stu-id="741a3-106">copyIndex</span></span>](#copyindex)
* [<span data-ttu-id="741a3-107">div</span><span class="sxs-lookup"><span data-stu-id="741a3-107">div</span></span>](#div)
* [<span data-ttu-id="741a3-108">float</span><span class="sxs-lookup"><span data-stu-id="741a3-108">float</span></span>](#float)
* [<span data-ttu-id="741a3-109">int</span><span class="sxs-lookup"><span data-stu-id="741a3-109">int</span></span>](#int)
* [<span data-ttu-id="741a3-110">min</span><span class="sxs-lookup"><span data-stu-id="741a3-110">min</span></span>](#min)
* [<span data-ttu-id="741a3-111">max</span><span class="sxs-lookup"><span data-stu-id="741a3-111">max</span></span>](#max)
* [<span data-ttu-id="741a3-112">mod</span><span class="sxs-lookup"><span data-stu-id="741a3-112">mod</span></span>](#mod)
* [<span data-ttu-id="741a3-113">mul</span><span class="sxs-lookup"><span data-stu-id="741a3-113">mul</span></span>](#mul)
* [<span data-ttu-id="741a3-114">sub</span><span class="sxs-lookup"><span data-stu-id="741a3-114">sub</span></span>](#sub)

<a id="add" />

## <a name="add"></a><span data-ttu-id="741a3-115">add</span><span class="sxs-lookup"><span data-stu-id="741a3-115">add</span></span>
`add(operand1, operand2)`

<span data-ttu-id="741a3-116">Restituisce la somma dei due numeri interi forniti.</span><span class="sxs-lookup"><span data-stu-id="741a3-116">Returns the sum of the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="741a3-117">Parametri</span><span class="sxs-lookup"><span data-stu-id="741a3-117">Parameters</span></span>

| <span data-ttu-id="741a3-118">Parametro</span><span class="sxs-lookup"><span data-stu-id="741a3-118">Parameter</span></span> | <span data-ttu-id="741a3-119">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="741a3-119">Required</span></span> | <span data-ttu-id="741a3-120">Tipo</span><span class="sxs-lookup"><span data-stu-id="741a3-120">Type</span></span> | <span data-ttu-id="741a3-121">Descrizione</span><span class="sxs-lookup"><span data-stu-id="741a3-121">Description</span></span> |
|:--- |:--- |:--- |:--- | 
|<span data-ttu-id="741a3-122">operand1</span><span class="sxs-lookup"><span data-stu-id="741a3-122">operand1</span></span> |<span data-ttu-id="741a3-123">Sì</span><span class="sxs-lookup"><span data-stu-id="741a3-123">Yes</span></span> |<span data-ttu-id="741a3-124">int</span><span class="sxs-lookup"><span data-stu-id="741a3-124">int</span></span> |<span data-ttu-id="741a3-125">Il primo numero da aggiungere.</span><span class="sxs-lookup"><span data-stu-id="741a3-125">First number to add.</span></span> |
|<span data-ttu-id="741a3-126">operand2</span><span class="sxs-lookup"><span data-stu-id="741a3-126">operand2</span></span> |<span data-ttu-id="741a3-127">Sì</span><span class="sxs-lookup"><span data-stu-id="741a3-127">Yes</span></span> |<span data-ttu-id="741a3-128">int</span><span class="sxs-lookup"><span data-stu-id="741a3-128">int</span></span> |<span data-ttu-id="741a3-129">Il secondo numero da aggiungere.</span><span class="sxs-lookup"><span data-stu-id="741a3-129">Second number to add.</span></span> |

### <a name="return-value"></a><span data-ttu-id="741a3-130">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="741a3-130">Return value</span></span>

<span data-ttu-id="741a3-131">Un intero che contiene la somma dei parametri.</span><span class="sxs-lookup"><span data-stu-id="741a3-131">An integer that contains the sum of the parameters.</span></span>

### <a name="example"></a><span data-ttu-id="741a3-132">Esempio</span><span class="sxs-lookup"><span data-stu-id="741a3-132">Example</span></span>

<span data-ttu-id="741a3-133">L'esempio seguente aggiunge due parametri.</span><span class="sxs-lookup"><span data-stu-id="741a3-133">The following example adds two parameters.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer to add"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer to add"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "addResult": {
            "type": "int",
            "value": "[add(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="741a3-134">L'output dell'esempio precedente con i valori predefiniti è:</span><span class="sxs-lookup"><span data-stu-id="741a3-134">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="741a3-135">Nome</span><span class="sxs-lookup"><span data-stu-id="741a3-135">Name</span></span> | <span data-ttu-id="741a3-136">Tipo</span><span class="sxs-lookup"><span data-stu-id="741a3-136">Type</span></span> | <span data-ttu-id="741a3-137">Valore</span><span class="sxs-lookup"><span data-stu-id="741a3-137">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="741a3-138">addResult</span><span class="sxs-lookup"><span data-stu-id="741a3-138">addResult</span></span> | <span data-ttu-id="741a3-139">int</span><span class="sxs-lookup"><span data-stu-id="741a3-139">Int</span></span> | <span data-ttu-id="741a3-140">8</span><span class="sxs-lookup"><span data-stu-id="741a3-140">8</span></span> |

<a id="copyindex" />

## <a name="copyindex"></a><span data-ttu-id="741a3-141">copyIndex</span><span class="sxs-lookup"><span data-stu-id="741a3-141">copyIndex</span></span>
`copyIndex(loopName, offset)`

<span data-ttu-id="741a3-142">Restituisce l'indice di un ciclo di iterazione.</span><span class="sxs-lookup"><span data-stu-id="741a3-142">Returns the index of an iteration loop.</span></span> 

### <a name="parameters"></a><span data-ttu-id="741a3-143">Parametri</span><span class="sxs-lookup"><span data-stu-id="741a3-143">Parameters</span></span>

| <span data-ttu-id="741a3-144">Parametro</span><span class="sxs-lookup"><span data-stu-id="741a3-144">Parameter</span></span> | <span data-ttu-id="741a3-145">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="741a3-145">Required</span></span> | <span data-ttu-id="741a3-146">Tipo</span><span class="sxs-lookup"><span data-stu-id="741a3-146">Type</span></span> | <span data-ttu-id="741a3-147">Descrizione</span><span class="sxs-lookup"><span data-stu-id="741a3-147">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="741a3-148">loopName</span><span class="sxs-lookup"><span data-stu-id="741a3-148">loopName</span></span> | <span data-ttu-id="741a3-149">No</span><span class="sxs-lookup"><span data-stu-id="741a3-149">No</span></span> | <span data-ttu-id="741a3-150">string</span><span class="sxs-lookup"><span data-stu-id="741a3-150">string</span></span> | <span data-ttu-id="741a3-151">Nome del ciclo per ottenere l'iterazione.</span><span class="sxs-lookup"><span data-stu-id="741a3-151">The name of the loop for getting the iteration.</span></span> |
| <span data-ttu-id="741a3-152">offset</span><span class="sxs-lookup"><span data-stu-id="741a3-152">offset</span></span> |<span data-ttu-id="741a3-153">No</span><span class="sxs-lookup"><span data-stu-id="741a3-153">No</span></span> |<span data-ttu-id="741a3-154">int</span><span class="sxs-lookup"><span data-stu-id="741a3-154">int</span></span> |<span data-ttu-id="741a3-155">Il numero da aggiungere al valore di iterazione in base zero.</span><span class="sxs-lookup"><span data-stu-id="741a3-155">The number to add to the zero-based iteration value.</span></span> |

### <a name="remarks"></a><span data-ttu-id="741a3-156">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="741a3-156">Remarks</span></span>

<span data-ttu-id="741a3-157">Questa funzione viene sempre usata con un oggetto **copy** .</span><span class="sxs-lookup"><span data-stu-id="741a3-157">This function is always used with a **copy** object.</span></span> <span data-ttu-id="741a3-158">Se non viene specificato alcun valore per **offset**, viene restituito il valore di iterazione corrente.</span><span class="sxs-lookup"><span data-stu-id="741a3-158">If no value is provided for **offset**, the current iteration value is returned.</span></span> <span data-ttu-id="741a3-159">Il valore di iterazione inizia da zero.</span><span class="sxs-lookup"><span data-stu-id="741a3-159">The iteration value starts at zero.</span></span>

<span data-ttu-id="741a3-160">La proprietà **loopName** consente di specificare se copyIndex fa riferimento all'iterazione di una risorsa o all'iterazione di una proprietà.</span><span class="sxs-lookup"><span data-stu-id="741a3-160">The **loopName** property enables you to specify whether copyIndex is referring to a resource iteration or property iteration.</span></span> <span data-ttu-id="741a3-161">Se non viene specificato alcun valore per **loopName**, viene usata l'iterazione del tipo di risorsa corrente.</span><span class="sxs-lookup"><span data-stu-id="741a3-161">If no value is provided for **loopName**, the current resource type iteration is used.</span></span> <span data-ttu-id="741a3-162">Specificare un valore per **loopName** durante l'iterazione di una proprietà.</span><span class="sxs-lookup"><span data-stu-id="741a3-162">Provide a value for **loopName** when iterating on a property.</span></span> 
 
<span data-ttu-id="741a3-163">Per una descrizione completa dell'uso di **copyIndex**, vedere [Creare più istanze di risorse in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="741a3-163">For a complete description of how you use **copyIndex**, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

### <a name="example"></a><span data-ttu-id="741a3-164">Esempio</span><span class="sxs-lookup"><span data-stu-id="741a3-164">Example</span></span>

<span data-ttu-id="741a3-165">L'esempio seguente illustra un ciclo di copy e il valore di indice incluso nel nome.</span><span class="sxs-lookup"><span data-stu-id="741a3-165">The following example shows a copy loop and the index value included in the name.</span></span> 

```json
"resources": [ 
  { 
    "name": "[concat('examplecopy-', copyIndex())]", 
    "type": "Microsoft.Web/sites", 
    "copy": { 
      "name": "websitescopy", 
      "count": "[parameters('count')]" 
    }, 
    ...
  }
]
```

### <a name="return-value"></a><span data-ttu-id="741a3-166">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="741a3-166">Return value</span></span>

<span data-ttu-id="741a3-167">Un intero che rappresenta l'indice corrente dell'iterazione.</span><span class="sxs-lookup"><span data-stu-id="741a3-167">An integer representing the current index of the iteration.</span></span>

<a id="div" />

## <a name="div"></a><span data-ttu-id="741a3-168">div</span><span class="sxs-lookup"><span data-stu-id="741a3-168">div</span></span>
`div(operand1, operand2)`

<span data-ttu-id="741a3-169">Restituisce la divisione Integer dei due numeri interi forniti.</span><span class="sxs-lookup"><span data-stu-id="741a3-169">Returns the integer division of the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="741a3-170">Parametri</span><span class="sxs-lookup"><span data-stu-id="741a3-170">Parameters</span></span>

| <span data-ttu-id="741a3-171">Parametro</span><span class="sxs-lookup"><span data-stu-id="741a3-171">Parameter</span></span> | <span data-ttu-id="741a3-172">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="741a3-172">Required</span></span> | <span data-ttu-id="741a3-173">Tipo</span><span class="sxs-lookup"><span data-stu-id="741a3-173">Type</span></span> | <span data-ttu-id="741a3-174">Descrizione</span><span class="sxs-lookup"><span data-stu-id="741a3-174">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="741a3-175">operand1</span><span class="sxs-lookup"><span data-stu-id="741a3-175">operand1</span></span> |<span data-ttu-id="741a3-176">Sì</span><span class="sxs-lookup"><span data-stu-id="741a3-176">Yes</span></span> |<span data-ttu-id="741a3-177">int</span><span class="sxs-lookup"><span data-stu-id="741a3-177">int</span></span> |<span data-ttu-id="741a3-178">Il numero da dividere.</span><span class="sxs-lookup"><span data-stu-id="741a3-178">The number being divided.</span></span> |
| <span data-ttu-id="741a3-179">operand2</span><span class="sxs-lookup"><span data-stu-id="741a3-179">operand2</span></span> |<span data-ttu-id="741a3-180">Sì</span><span class="sxs-lookup"><span data-stu-id="741a3-180">Yes</span></span> |<span data-ttu-id="741a3-181">int</span><span class="sxs-lookup"><span data-stu-id="741a3-181">int</span></span> |<span data-ttu-id="741a3-182">Il numero usato per dividere.</span><span class="sxs-lookup"><span data-stu-id="741a3-182">The number that is used to divide.</span></span> <span data-ttu-id="741a3-183">Non può essere 0.</span><span class="sxs-lookup"><span data-stu-id="741a3-183">Cannot be 0.</span></span> |

### <a name="return-value"></a><span data-ttu-id="741a3-184">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="741a3-184">Return value</span></span>

<span data-ttu-id="741a3-185">Un intero che rappresenta la divisione.</span><span class="sxs-lookup"><span data-stu-id="741a3-185">An integer representing the division.</span></span>

### <a name="example"></a><span data-ttu-id="741a3-186">Esempio</span><span class="sxs-lookup"><span data-stu-id="741a3-186">Example</span></span>

<span data-ttu-id="741a3-187">L'esempio seguente mostra come dividere un parametro per un altro parametro.</span><span class="sxs-lookup"><span data-stu-id="741a3-187">The following example divides one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 8,
            "metadata": {
                "description": "Integer being divided"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer used to divide"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "divResult": {
            "type": "int",
            "value": "[div(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="741a3-188">L'output dell'esempio precedente con i valori predefiniti è:</span><span class="sxs-lookup"><span data-stu-id="741a3-188">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="741a3-189">Nome</span><span class="sxs-lookup"><span data-stu-id="741a3-189">Name</span></span> | <span data-ttu-id="741a3-190">Tipo</span><span class="sxs-lookup"><span data-stu-id="741a3-190">Type</span></span> | <span data-ttu-id="741a3-191">Valore</span><span class="sxs-lookup"><span data-stu-id="741a3-191">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="741a3-192">divResult</span><span class="sxs-lookup"><span data-stu-id="741a3-192">divResult</span></span> | <span data-ttu-id="741a3-193">int</span><span class="sxs-lookup"><span data-stu-id="741a3-193">Int</span></span> | <span data-ttu-id="741a3-194">2</span><span class="sxs-lookup"><span data-stu-id="741a3-194">2</span></span> |

<a id="float" />

## <a name="float"></a><span data-ttu-id="741a3-195">float</span><span class="sxs-lookup"><span data-stu-id="741a3-195">float</span></span>
`float(arg1)`

<span data-ttu-id="741a3-196">Converte il valore in un numero a virgola mobile.</span><span class="sxs-lookup"><span data-stu-id="741a3-196">Converts the value to a floating point number.</span></span> <span data-ttu-id="741a3-197">Usare questa funzione solo quando si passano parametri personalizzati a un'applicazione, ad esempio un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="741a3-197">You only use this function when passing custom parameters to an application, such as a Logic App.</span></span>

### <a name="parameters"></a><span data-ttu-id="741a3-198">Parametri</span><span class="sxs-lookup"><span data-stu-id="741a3-198">Parameters</span></span>

| <span data-ttu-id="741a3-199">Parametro</span><span class="sxs-lookup"><span data-stu-id="741a3-199">Parameter</span></span> | <span data-ttu-id="741a3-200">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="741a3-200">Required</span></span> | <span data-ttu-id="741a3-201">Tipo</span><span class="sxs-lookup"><span data-stu-id="741a3-201">Type</span></span> | <span data-ttu-id="741a3-202">Descrizione</span><span class="sxs-lookup"><span data-stu-id="741a3-202">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="741a3-203">arg1</span><span class="sxs-lookup"><span data-stu-id="741a3-203">arg1</span></span> |<span data-ttu-id="741a3-204">Sì</span><span class="sxs-lookup"><span data-stu-id="741a3-204">Yes</span></span> |<span data-ttu-id="741a3-205">stringa o int</span><span class="sxs-lookup"><span data-stu-id="741a3-205">string or int</span></span> |<span data-ttu-id="741a3-206">Il valore da convertire in un numero a virgola mobile.</span><span class="sxs-lookup"><span data-stu-id="741a3-206">The value to convert to a floating point number.</span></span> |

### <a name="return-value"></a><span data-ttu-id="741a3-207">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="741a3-207">Return value</span></span>
<span data-ttu-id="741a3-208">Un numero a virgola mobile.</span><span class="sxs-lookup"><span data-stu-id="741a3-208">A floating point number.</span></span>

### <a name="example"></a><span data-ttu-id="741a3-209">Esempio</span><span class="sxs-lookup"><span data-stu-id="741a3-209">Example</span></span>

<span data-ttu-id="741a3-210">L'esempio seguente illustra come usare float per passare parametri a un'app per la logica:</span><span class="sxs-lookup"><span data-stu-id="741a3-210">The following example shows how to use float to pass parameters to a Logic App:</span></span>

```json
{
    "type": "Microsoft.Logic/workflows",
    "properties": {
        ...
        "parameters": {
        "custom1": {
            "value": "[float('3.0')]"
        },
        "custom2": {
            "value": "[float(3)]"
        },
```

<a id="int" />

## <a name="int"></a><span data-ttu-id="741a3-211">int</span><span class="sxs-lookup"><span data-stu-id="741a3-211">int</span></span>
`int(valueToConvert)`

<span data-ttu-id="741a3-212">Converte il valore specificato in un numero intero.</span><span class="sxs-lookup"><span data-stu-id="741a3-212">Converts the specified value to an integer.</span></span>

### <a name="parameters"></a><span data-ttu-id="741a3-213">Parametri</span><span class="sxs-lookup"><span data-stu-id="741a3-213">Parameters</span></span>

| <span data-ttu-id="741a3-214">Parametro</span><span class="sxs-lookup"><span data-stu-id="741a3-214">Parameter</span></span> | <span data-ttu-id="741a3-215">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="741a3-215">Required</span></span> | <span data-ttu-id="741a3-216">Tipo</span><span class="sxs-lookup"><span data-stu-id="741a3-216">Type</span></span> | <span data-ttu-id="741a3-217">Descrizione</span><span class="sxs-lookup"><span data-stu-id="741a3-217">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="741a3-218">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="741a3-218">valueToConvert</span></span> |<span data-ttu-id="741a3-219">Sì</span><span class="sxs-lookup"><span data-stu-id="741a3-219">Yes</span></span> |<span data-ttu-id="741a3-220">stringa o int</span><span class="sxs-lookup"><span data-stu-id="741a3-220">string or int</span></span> |<span data-ttu-id="741a3-221">Il valore da convertire in numero intero.</span><span class="sxs-lookup"><span data-stu-id="741a3-221">The value to convert to an integer.</span></span> |

### <a name="return-value"></a><span data-ttu-id="741a3-222">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="741a3-222">Return value</span></span>

<span data-ttu-id="741a3-223">Un intero del valore convertito.</span><span class="sxs-lookup"><span data-stu-id="741a3-223">An integer of the converted value.</span></span>

### <a name="example"></a><span data-ttu-id="741a3-224">Esempio</span><span class="sxs-lookup"><span data-stu-id="741a3-224">Example</span></span>

<span data-ttu-id="741a3-225">L'esempio seguente converte il valore del parametro fornito dall'utente in intero.</span><span class="sxs-lookup"><span data-stu-id="741a3-225">The following example converts the user-provided parameter value to integer.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToConvert": { 
            "type": "string",
            "defaultValue": "4"
        }
    },
    "resources": [
    ],
    "outputs": {
        "intResult": {
            "type": "int",
            "value": "[int(parameters('stringToConvert'))]"
        }
    }
}
```

<span data-ttu-id="741a3-226">L'output dell'esempio precedente con i valori predefiniti è:</span><span class="sxs-lookup"><span data-stu-id="741a3-226">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="741a3-227">Nome</span><span class="sxs-lookup"><span data-stu-id="741a3-227">Name</span></span> | <span data-ttu-id="741a3-228">Tipo</span><span class="sxs-lookup"><span data-stu-id="741a3-228">Type</span></span> | <span data-ttu-id="741a3-229">Valore</span><span class="sxs-lookup"><span data-stu-id="741a3-229">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="741a3-230">intResult</span><span class="sxs-lookup"><span data-stu-id="741a3-230">intResult</span></span> | <span data-ttu-id="741a3-231">int</span><span class="sxs-lookup"><span data-stu-id="741a3-231">Int</span></span> | <span data-ttu-id="741a3-232">4</span><span class="sxs-lookup"><span data-stu-id="741a3-232">4</span></span> |


<a id="min" />

## <a name="min"></a><span data-ttu-id="741a3-233">Min</span><span class="sxs-lookup"><span data-stu-id="741a3-233">min</span></span>
`min (arg1)`

<span data-ttu-id="741a3-234">Restituisce il valore minimo di una matrice di numeri interi o di un elenco di numeri interi delimitato da virgole.</span><span class="sxs-lookup"><span data-stu-id="741a3-234">Returns the minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="741a3-235">Parametri</span><span class="sxs-lookup"><span data-stu-id="741a3-235">Parameters</span></span>

| <span data-ttu-id="741a3-236">Parametro</span><span class="sxs-lookup"><span data-stu-id="741a3-236">Parameter</span></span> | <span data-ttu-id="741a3-237">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="741a3-237">Required</span></span> | <span data-ttu-id="741a3-238">Tipo</span><span class="sxs-lookup"><span data-stu-id="741a3-238">Type</span></span> | <span data-ttu-id="741a3-239">Descrizione</span><span class="sxs-lookup"><span data-stu-id="741a3-239">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="741a3-240">arg1</span><span class="sxs-lookup"><span data-stu-id="741a3-240">arg1</span></span> |<span data-ttu-id="741a3-241">Sì</span><span class="sxs-lookup"><span data-stu-id="741a3-241">Yes</span></span> |<span data-ttu-id="741a3-242">matrice di numeri interi o elenco di numeri interi delimitato da virgole</span><span class="sxs-lookup"><span data-stu-id="741a3-242">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="741a3-243">La raccolta per ottenere il valore minimo.</span><span class="sxs-lookup"><span data-stu-id="741a3-243">The collection to get the minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="741a3-244">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="741a3-244">Return value</span></span>

<span data-ttu-id="741a3-245">un intero che rappresenta il valore minimo dalla raccolta.</span><span class="sxs-lookup"><span data-stu-id="741a3-245">An integer representing minimum value from the collection.</span></span>

### <a name="example"></a><span data-ttu-id="741a3-246">Esempio</span><span class="sxs-lookup"><span data-stu-id="741a3-246">Example</span></span>

<span data-ttu-id="741a3-247">L'esempio seguente mostra come usare la funzione min con una matrice e un elenco di numeri interi:</span><span class="sxs-lookup"><span data-stu-id="741a3-247">The following example shows how to use min with an array and a list of integers:</span></span>

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

<span data-ttu-id="741a3-248">L'output dell'esempio precedente con i valori predefiniti è il seguente:</span><span class="sxs-lookup"><span data-stu-id="741a3-248">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="741a3-249">Nome</span><span class="sxs-lookup"><span data-stu-id="741a3-249">Name</span></span> | <span data-ttu-id="741a3-250">Tipo</span><span class="sxs-lookup"><span data-stu-id="741a3-250">Type</span></span> | <span data-ttu-id="741a3-251">Valore</span><span class="sxs-lookup"><span data-stu-id="741a3-251">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="741a3-252">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="741a3-252">arrayOutput</span></span> | <span data-ttu-id="741a3-253">int</span><span class="sxs-lookup"><span data-stu-id="741a3-253">Int</span></span> | <span data-ttu-id="741a3-254">0</span><span class="sxs-lookup"><span data-stu-id="741a3-254">0</span></span> |
| <span data-ttu-id="741a3-255">intOutput</span><span class="sxs-lookup"><span data-stu-id="741a3-255">intOutput</span></span> | <span data-ttu-id="741a3-256">int</span><span class="sxs-lookup"><span data-stu-id="741a3-256">Int</span></span> | <span data-ttu-id="741a3-257">0</span><span class="sxs-lookup"><span data-stu-id="741a3-257">0</span></span> |

<a id="max" />

## <a name="max"></a><span data-ttu-id="741a3-258">max</span><span class="sxs-lookup"><span data-stu-id="741a3-258">max</span></span>
`max (arg1)`

<span data-ttu-id="741a3-259">Restituisce il valore massimo da una matrice di numeri interi o da un elenco di numeri interi delimitato da virgole.</span><span class="sxs-lookup"><span data-stu-id="741a3-259">Returns the maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="741a3-260">Parametri</span><span class="sxs-lookup"><span data-stu-id="741a3-260">Parameters</span></span>

| <span data-ttu-id="741a3-261">Parametro</span><span class="sxs-lookup"><span data-stu-id="741a3-261">Parameter</span></span> | <span data-ttu-id="741a3-262">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="741a3-262">Required</span></span> | <span data-ttu-id="741a3-263">Tipo</span><span class="sxs-lookup"><span data-stu-id="741a3-263">Type</span></span> | <span data-ttu-id="741a3-264">Descrizione</span><span class="sxs-lookup"><span data-stu-id="741a3-264">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="741a3-265">arg1</span><span class="sxs-lookup"><span data-stu-id="741a3-265">arg1</span></span> |<span data-ttu-id="741a3-266">Sì</span><span class="sxs-lookup"><span data-stu-id="741a3-266">Yes</span></span> |<span data-ttu-id="741a3-267">matrice di numeri interi o elenco di numeri interi delimitato da virgole</span><span class="sxs-lookup"><span data-stu-id="741a3-267">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="741a3-268">La raccolta per ottenere il valore massimo.</span><span class="sxs-lookup"><span data-stu-id="741a3-268">The collection to get the maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="741a3-269">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="741a3-269">Return value</span></span>

<span data-ttu-id="741a3-270">Un intero che rappresenta il valore massimo dalla raccolta.</span><span class="sxs-lookup"><span data-stu-id="741a3-270">An integer representing the maximum value from the collection.</span></span>

### <a name="example"></a><span data-ttu-id="741a3-271">Esempio</span><span class="sxs-lookup"><span data-stu-id="741a3-271">Example</span></span>

<span data-ttu-id="741a3-272">L'esempio seguente mostra come usare la funzione max con una matrice e un elenco di numeri interi:</span><span class="sxs-lookup"><span data-stu-id="741a3-272">The following example shows how to use max with an array and a list of integers:</span></span>

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

<span data-ttu-id="741a3-273">L'output dell'esempio precedente con i valori predefiniti è il seguente:</span><span class="sxs-lookup"><span data-stu-id="741a3-273">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="741a3-274">Nome</span><span class="sxs-lookup"><span data-stu-id="741a3-274">Name</span></span> | <span data-ttu-id="741a3-275">Tipo</span><span class="sxs-lookup"><span data-stu-id="741a3-275">Type</span></span> | <span data-ttu-id="741a3-276">Valore</span><span class="sxs-lookup"><span data-stu-id="741a3-276">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="741a3-277">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="741a3-277">arrayOutput</span></span> | <span data-ttu-id="741a3-278">int</span><span class="sxs-lookup"><span data-stu-id="741a3-278">Int</span></span> | <span data-ttu-id="741a3-279">5</span><span class="sxs-lookup"><span data-stu-id="741a3-279">5</span></span> |
| <span data-ttu-id="741a3-280">intOutput</span><span class="sxs-lookup"><span data-stu-id="741a3-280">intOutput</span></span> | <span data-ttu-id="741a3-281">int</span><span class="sxs-lookup"><span data-stu-id="741a3-281">Int</span></span> | <span data-ttu-id="741a3-282">5</span><span class="sxs-lookup"><span data-stu-id="741a3-282">5</span></span> |

<a id="mod" />

## <a name="mod"></a><span data-ttu-id="741a3-283">mod</span><span class="sxs-lookup"><span data-stu-id="741a3-283">mod</span></span>
`mod(operand1, operand2)`

<span data-ttu-id="741a3-284">Restituisce la parte rimanente della divisione Integer usando i due numeri interi forniti.</span><span class="sxs-lookup"><span data-stu-id="741a3-284">Returns the remainder of the integer division using the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="741a3-285">Parametri</span><span class="sxs-lookup"><span data-stu-id="741a3-285">Parameters</span></span>

| <span data-ttu-id="741a3-286">Parametro</span><span class="sxs-lookup"><span data-stu-id="741a3-286">Parameter</span></span> | <span data-ttu-id="741a3-287">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="741a3-287">Required</span></span> | <span data-ttu-id="741a3-288">Tipo</span><span class="sxs-lookup"><span data-stu-id="741a3-288">Type</span></span> | <span data-ttu-id="741a3-289">Descrizione</span><span class="sxs-lookup"><span data-stu-id="741a3-289">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="741a3-290">operand1</span><span class="sxs-lookup"><span data-stu-id="741a3-290">operand1</span></span> |<span data-ttu-id="741a3-291">Sì</span><span class="sxs-lookup"><span data-stu-id="741a3-291">Yes</span></span> |<span data-ttu-id="741a3-292">int</span><span class="sxs-lookup"><span data-stu-id="741a3-292">int</span></span> |<span data-ttu-id="741a3-293">Il numero da dividere.</span><span class="sxs-lookup"><span data-stu-id="741a3-293">The number being divided.</span></span> |
| <span data-ttu-id="741a3-294">operand2</span><span class="sxs-lookup"><span data-stu-id="741a3-294">operand2</span></span> |<span data-ttu-id="741a3-295">Sì</span><span class="sxs-lookup"><span data-stu-id="741a3-295">Yes</span></span> |<span data-ttu-id="741a3-296">int</span><span class="sxs-lookup"><span data-stu-id="741a3-296">int</span></span> |<span data-ttu-id="741a3-297">Il numero usato per dividere; non può corrispondere a 0.</span><span class="sxs-lookup"><span data-stu-id="741a3-297">The number that is used to divide, Cannot be 0.</span></span> |

### <a name="return-value"></a><span data-ttu-id="741a3-298">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="741a3-298">Return value</span></span>
<span data-ttu-id="741a3-299">Un intero che rappresenta il resto.</span><span class="sxs-lookup"><span data-stu-id="741a3-299">An integer representing the remainder.</span></span>

### <a name="example"></a><span data-ttu-id="741a3-300">Esempio</span><span class="sxs-lookup"><span data-stu-id="741a3-300">Example</span></span>

<span data-ttu-id="741a3-301">L'esempio seguente restituisce il resto della divisione di un parametro per un altro parametro.</span><span class="sxs-lookup"><span data-stu-id="741a3-301">The following example returns the remainder of dividing one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 7,
            "metadata": {
                "description": "Integer being divided"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer used to divide"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "modResult": {
            "type": "int",
            "value": "[mod(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="741a3-302">L'output dell'esempio precedente con i valori predefiniti è:</span><span class="sxs-lookup"><span data-stu-id="741a3-302">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="741a3-303">Nome</span><span class="sxs-lookup"><span data-stu-id="741a3-303">Name</span></span> | <span data-ttu-id="741a3-304">Tipo</span><span class="sxs-lookup"><span data-stu-id="741a3-304">Type</span></span> | <span data-ttu-id="741a3-305">Valore</span><span class="sxs-lookup"><span data-stu-id="741a3-305">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="741a3-306">modResult</span><span class="sxs-lookup"><span data-stu-id="741a3-306">modResult</span></span> | <span data-ttu-id="741a3-307">int</span><span class="sxs-lookup"><span data-stu-id="741a3-307">Int</span></span> | <span data-ttu-id="741a3-308">1</span><span class="sxs-lookup"><span data-stu-id="741a3-308">1</span></span> |

<a id="mul" />

## <a name="mul"></a><span data-ttu-id="741a3-309">mul</span><span class="sxs-lookup"><span data-stu-id="741a3-309">mul</span></span>
`mul(operand1, operand2)`

<span data-ttu-id="741a3-310">Restituisce la moltiplicazione dei due numeri interi forniti.</span><span class="sxs-lookup"><span data-stu-id="741a3-310">Returns the multiplication of the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="741a3-311">Parametri</span><span class="sxs-lookup"><span data-stu-id="741a3-311">Parameters</span></span>

| <span data-ttu-id="741a3-312">Parametro</span><span class="sxs-lookup"><span data-stu-id="741a3-312">Parameter</span></span> | <span data-ttu-id="741a3-313">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="741a3-313">Required</span></span> | <span data-ttu-id="741a3-314">Tipo</span><span class="sxs-lookup"><span data-stu-id="741a3-314">Type</span></span> | <span data-ttu-id="741a3-315">Descrizione</span><span class="sxs-lookup"><span data-stu-id="741a3-315">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="741a3-316">operand1</span><span class="sxs-lookup"><span data-stu-id="741a3-316">operand1</span></span> |<span data-ttu-id="741a3-317">Sì</span><span class="sxs-lookup"><span data-stu-id="741a3-317">Yes</span></span> |<span data-ttu-id="741a3-318">int</span><span class="sxs-lookup"><span data-stu-id="741a3-318">int</span></span> |<span data-ttu-id="741a3-319">Il primo numero da moltiplicare.</span><span class="sxs-lookup"><span data-stu-id="741a3-319">First number to multiply.</span></span> |
| <span data-ttu-id="741a3-320">operand2</span><span class="sxs-lookup"><span data-stu-id="741a3-320">operand2</span></span> |<span data-ttu-id="741a3-321">Sì</span><span class="sxs-lookup"><span data-stu-id="741a3-321">Yes</span></span> |<span data-ttu-id="741a3-322">int</span><span class="sxs-lookup"><span data-stu-id="741a3-322">int</span></span> |<span data-ttu-id="741a3-323">Il secondo numero da moltiplicare.</span><span class="sxs-lookup"><span data-stu-id="741a3-323">Second number to multiply.</span></span> |

### <a name="return-value"></a><span data-ttu-id="741a3-324">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="741a3-324">Return value</span></span>

<span data-ttu-id="741a3-325">Un intero che rappresenta la moltiplicazione.</span><span class="sxs-lookup"><span data-stu-id="741a3-325">An integer representing the multiplication.</span></span>

### <a name="example"></a><span data-ttu-id="741a3-326">Esempio</span><span class="sxs-lookup"><span data-stu-id="741a3-326">Example</span></span>

<span data-ttu-id="741a3-327">L'esempio seguente mostra come moltiplicare un parametro per un altro parametro.</span><span class="sxs-lookup"><span data-stu-id="741a3-327">The following example multiplies one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer to multiply"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer to multiply"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "mulResult": {
            "type": "int",
            "value": "[mul(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="741a3-328">L'output dell'esempio precedente con i valori predefiniti è:</span><span class="sxs-lookup"><span data-stu-id="741a3-328">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="741a3-329">Nome</span><span class="sxs-lookup"><span data-stu-id="741a3-329">Name</span></span> | <span data-ttu-id="741a3-330">Tipo</span><span class="sxs-lookup"><span data-stu-id="741a3-330">Type</span></span> | <span data-ttu-id="741a3-331">Valore</span><span class="sxs-lookup"><span data-stu-id="741a3-331">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="741a3-332">mulResult</span><span class="sxs-lookup"><span data-stu-id="741a3-332">mulResult</span></span> | <span data-ttu-id="741a3-333">int</span><span class="sxs-lookup"><span data-stu-id="741a3-333">Int</span></span> | <span data-ttu-id="741a3-334">15</span><span class="sxs-lookup"><span data-stu-id="741a3-334">15</span></span> |

<a id="sub" />

## <a name="sub"></a><span data-ttu-id="741a3-335">sub</span><span class="sxs-lookup"><span data-stu-id="741a3-335">sub</span></span>
`sub(operand1, operand2)`

<span data-ttu-id="741a3-336">Restituisce la sottrazione dei due numeri interi forniti.</span><span class="sxs-lookup"><span data-stu-id="741a3-336">Returns the subtraction of the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="741a3-337">Parametri</span><span class="sxs-lookup"><span data-stu-id="741a3-337">Parameters</span></span>

| <span data-ttu-id="741a3-338">Parametro</span><span class="sxs-lookup"><span data-stu-id="741a3-338">Parameter</span></span> | <span data-ttu-id="741a3-339">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="741a3-339">Required</span></span> | <span data-ttu-id="741a3-340">Tipo</span><span class="sxs-lookup"><span data-stu-id="741a3-340">Type</span></span> | <span data-ttu-id="741a3-341">Descrizione</span><span class="sxs-lookup"><span data-stu-id="741a3-341">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="741a3-342">operand1</span><span class="sxs-lookup"><span data-stu-id="741a3-342">operand1</span></span> |<span data-ttu-id="741a3-343">Sì</span><span class="sxs-lookup"><span data-stu-id="741a3-343">Yes</span></span> |<span data-ttu-id="741a3-344">int</span><span class="sxs-lookup"><span data-stu-id="741a3-344">int</span></span> |<span data-ttu-id="741a3-345">Il numero da cui sottrarre.</span><span class="sxs-lookup"><span data-stu-id="741a3-345">The number that is subtracted from.</span></span> |
| <span data-ttu-id="741a3-346">operand2</span><span class="sxs-lookup"><span data-stu-id="741a3-346">operand2</span></span> |<span data-ttu-id="741a3-347">Sì</span><span class="sxs-lookup"><span data-stu-id="741a3-347">Yes</span></span> |<span data-ttu-id="741a3-348">int</span><span class="sxs-lookup"><span data-stu-id="741a3-348">int</span></span> |<span data-ttu-id="741a3-349">Il numero sottratto.</span><span class="sxs-lookup"><span data-stu-id="741a3-349">The number that is subtracted.</span></span> |

### <a name="return-value"></a><span data-ttu-id="741a3-350">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="741a3-350">Return value</span></span>
<span data-ttu-id="741a3-351">Un intero che rappresenta la sottrazione.</span><span class="sxs-lookup"><span data-stu-id="741a3-351">An integer representing the subtraction.</span></span>

### <a name="example"></a><span data-ttu-id="741a3-352">Esempio</span><span class="sxs-lookup"><span data-stu-id="741a3-352">Example</span></span>

<span data-ttu-id="741a3-353">L'esempio seguente mostra come sottrarre un parametro da un altro parametro.</span><span class="sxs-lookup"><span data-stu-id="741a3-353">The following example subtracts one parameter from another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 7,
            "metadata": {
                "description": "Integer subtracted from"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer to subtract"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "subResult": {
            "type": "int",
            "value": "[sub(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="741a3-354">L'output dell'esempio precedente con i valori predefiniti è:</span><span class="sxs-lookup"><span data-stu-id="741a3-354">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="741a3-355">Nome</span><span class="sxs-lookup"><span data-stu-id="741a3-355">Name</span></span> | <span data-ttu-id="741a3-356">Tipo</span><span class="sxs-lookup"><span data-stu-id="741a3-356">Type</span></span> | <span data-ttu-id="741a3-357">Valore</span><span class="sxs-lookup"><span data-stu-id="741a3-357">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="741a3-358">subResult</span><span class="sxs-lookup"><span data-stu-id="741a3-358">subResult</span></span> | <span data-ttu-id="741a3-359">int</span><span class="sxs-lookup"><span data-stu-id="741a3-359">Int</span></span> | <span data-ttu-id="741a3-360">4</span><span class="sxs-lookup"><span data-stu-id="741a3-360">4</span></span> |

## <a name="next-steps"></a><span data-ttu-id="741a3-361">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="741a3-361">Next steps</span></span>
* <span data-ttu-id="741a3-362">Per una descrizione delle sezioni in un modello di Azure Resource Manager, vedere [Creazione di modelli di Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="741a3-362">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="741a3-363">Per unire più modelli, vedere [Uso di modelli collegati con Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="741a3-363">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="741a3-364">Per eseguire un'iterazione di un numero di volte specificato durante la creazione di un tipo di risorsa, vedere [Creare più istanze di risorse in Gestione risorse di Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="741a3-364">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="741a3-365">Per informazioni su come distribuire il modello che è stato creato, vedere [Distribuire un'applicazione con un modello di Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="741a3-365">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

