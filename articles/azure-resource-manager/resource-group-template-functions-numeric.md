---
title: aaaAzure Gestione risorse funzioni di modello - numeriche | Documenti Microsoft
description: Descrive toouse funzioni hello in un toowork modello di gestione risorse di Azure con i numeri.
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
ms.openlocfilehash: 855d5b354d094b9815edc160e3d72efbfd36ba77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="numeric-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="c642f-103">Funzioni numeriche per i modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c642f-103">Numeric functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="c642f-104">Gestione risorse offre hello seguenti funzioni per l'utilizzo di numeri interi:</span><span class="sxs-lookup"><span data-stu-id="c642f-104">Resource Manager provides hello following functions for working with integers:</span></span>

* [<span data-ttu-id="c642f-105">add</span><span class="sxs-lookup"><span data-stu-id="c642f-105">add</span></span>](#add)
* [<span data-ttu-id="c642f-106">copyIndex</span><span class="sxs-lookup"><span data-stu-id="c642f-106">copyIndex</span></span>](#copyindex)
* [<span data-ttu-id="c642f-107">div</span><span class="sxs-lookup"><span data-stu-id="c642f-107">div</span></span>](#div)
* [<span data-ttu-id="c642f-108">float</span><span class="sxs-lookup"><span data-stu-id="c642f-108">float</span></span>](#float)
* [<span data-ttu-id="c642f-109">int</span><span class="sxs-lookup"><span data-stu-id="c642f-109">int</span></span>](#int)
* [<span data-ttu-id="c642f-110">min</span><span class="sxs-lookup"><span data-stu-id="c642f-110">min</span></span>](#min)
* [<span data-ttu-id="c642f-111">max</span><span class="sxs-lookup"><span data-stu-id="c642f-111">max</span></span>](#max)
* [<span data-ttu-id="c642f-112">mod</span><span class="sxs-lookup"><span data-stu-id="c642f-112">mod</span></span>](#mod)
* [<span data-ttu-id="c642f-113">mul</span><span class="sxs-lookup"><span data-stu-id="c642f-113">mul</span></span>](#mul)
* [<span data-ttu-id="c642f-114">sub</span><span class="sxs-lookup"><span data-stu-id="c642f-114">sub</span></span>](#sub)

<a id="add" />

## <a name="add"></a><span data-ttu-id="c642f-115">add</span><span class="sxs-lookup"><span data-stu-id="c642f-115">add</span></span>
`add(operand1, operand2)`

<span data-ttu-id="c642f-116">Restituisce hello somma di due interi fornito di hello.</span><span class="sxs-lookup"><span data-stu-id="c642f-116">Returns hello sum of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="c642f-117">parameters</span><span class="sxs-lookup"><span data-stu-id="c642f-117">Parameters</span></span>

| <span data-ttu-id="c642f-118">Parametro</span><span class="sxs-lookup"><span data-stu-id="c642f-118">Parameter</span></span> | <span data-ttu-id="c642f-119">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="c642f-119">Required</span></span> | <span data-ttu-id="c642f-120">Tipo</span><span class="sxs-lookup"><span data-stu-id="c642f-120">Type</span></span> | <span data-ttu-id="c642f-121">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c642f-121">Description</span></span> |
|:--- |:--- |:--- |:--- | 
|<span data-ttu-id="c642f-122">operand1</span><span class="sxs-lookup"><span data-stu-id="c642f-122">operand1</span></span> |<span data-ttu-id="c642f-123">Sì</span><span class="sxs-lookup"><span data-stu-id="c642f-123">Yes</span></span> |<span data-ttu-id="c642f-124">int</span><span class="sxs-lookup"><span data-stu-id="c642f-124">int</span></span> |<span data-ttu-id="c642f-125">Primo numero tooadd.</span><span class="sxs-lookup"><span data-stu-id="c642f-125">First number tooadd.</span></span> |
|<span data-ttu-id="c642f-126">operand2</span><span class="sxs-lookup"><span data-stu-id="c642f-126">operand2</span></span> |<span data-ttu-id="c642f-127">Sì</span><span class="sxs-lookup"><span data-stu-id="c642f-127">Yes</span></span> |<span data-ttu-id="c642f-128">int</span><span class="sxs-lookup"><span data-stu-id="c642f-128">int</span></span> |<span data-ttu-id="c642f-129">Secondo numero tooadd.</span><span class="sxs-lookup"><span data-stu-id="c642f-129">Second number tooadd.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c642f-130">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="c642f-130">Return value</span></span>

<span data-ttu-id="c642f-131">Valore intero che contiene la somma hello dei parametri di hello.</span><span class="sxs-lookup"><span data-stu-id="c642f-131">An integer that contains hello sum of hello parameters.</span></span>

### <a name="example"></a><span data-ttu-id="c642f-132">Esempio</span><span class="sxs-lookup"><span data-stu-id="c642f-132">Example</span></span>

<span data-ttu-id="c642f-133">Hello di esempio seguente vengono aggiunti due parametri.</span><span class="sxs-lookup"><span data-stu-id="c642f-133">hello following example adds two parameters.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer tooadd"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer tooadd"
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

<span data-ttu-id="c642f-134">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="c642f-134">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="c642f-135">Nome</span><span class="sxs-lookup"><span data-stu-id="c642f-135">Name</span></span> | <span data-ttu-id="c642f-136">Tipo</span><span class="sxs-lookup"><span data-stu-id="c642f-136">Type</span></span> | <span data-ttu-id="c642f-137">Valore</span><span class="sxs-lookup"><span data-stu-id="c642f-137">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c642f-138">addResult</span><span class="sxs-lookup"><span data-stu-id="c642f-138">addResult</span></span> | <span data-ttu-id="c642f-139">int</span><span class="sxs-lookup"><span data-stu-id="c642f-139">Int</span></span> | <span data-ttu-id="c642f-140">8</span><span class="sxs-lookup"><span data-stu-id="c642f-140">8</span></span> |

<a id="copyindex" />

## <a name="copyindex"></a><span data-ttu-id="c642f-141">copyIndex</span><span class="sxs-lookup"><span data-stu-id="c642f-141">copyIndex</span></span>
`copyIndex(loopName, offset)`

<span data-ttu-id="c642f-142">Restituisce hello indice di un ciclo di iterazione.</span><span class="sxs-lookup"><span data-stu-id="c642f-142">Returns hello index of an iteration loop.</span></span> 

### <a name="parameters"></a><span data-ttu-id="c642f-143">parameters</span><span class="sxs-lookup"><span data-stu-id="c642f-143">Parameters</span></span>

| <span data-ttu-id="c642f-144">Parametro</span><span class="sxs-lookup"><span data-stu-id="c642f-144">Parameter</span></span> | <span data-ttu-id="c642f-145">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="c642f-145">Required</span></span> | <span data-ttu-id="c642f-146">Tipo</span><span class="sxs-lookup"><span data-stu-id="c642f-146">Type</span></span> | <span data-ttu-id="c642f-147">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c642f-147">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c642f-148">loopName</span><span class="sxs-lookup"><span data-stu-id="c642f-148">loopName</span></span> | <span data-ttu-id="c642f-149">No</span><span class="sxs-lookup"><span data-stu-id="c642f-149">No</span></span> | <span data-ttu-id="c642f-150">string</span><span class="sxs-lookup"><span data-stu-id="c642f-150">string</span></span> | <span data-ttu-id="c642f-151">nome di Hello del ciclo di hello per il recupero di iterazione hello.</span><span class="sxs-lookup"><span data-stu-id="c642f-151">hello name of hello loop for getting hello iteration.</span></span> |
| <span data-ttu-id="c642f-152">offset</span><span class="sxs-lookup"><span data-stu-id="c642f-152">offset</span></span> |<span data-ttu-id="c642f-153">No</span><span class="sxs-lookup"><span data-stu-id="c642f-153">No</span></span> |<span data-ttu-id="c642f-154">int</span><span class="sxs-lookup"><span data-stu-id="c642f-154">int</span></span> |<span data-ttu-id="c642f-155">Hello tooadd toohello iterazione in base zero in valore numerico.</span><span class="sxs-lookup"><span data-stu-id="c642f-155">hello number tooadd toohello zero-based iteration value.</span></span> |

### <a name="remarks"></a><span data-ttu-id="c642f-156">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="c642f-156">Remarks</span></span>

<span data-ttu-id="c642f-157">Questa funzione viene sempre usata con un oggetto **copy** .</span><span class="sxs-lookup"><span data-stu-id="c642f-157">This function is always used with a **copy** object.</span></span> <span data-ttu-id="c642f-158">Se non viene fornito alcun valore per **offset**, viene restituito il valore di iterazione corrente hello.</span><span class="sxs-lookup"><span data-stu-id="c642f-158">If no value is provided for **offset**, hello current iteration value is returned.</span></span> <span data-ttu-id="c642f-159">il valore di iterazione Hello inizia in corrispondenza di zero.</span><span class="sxs-lookup"><span data-stu-id="c642f-159">hello iteration value starts at zero.</span></span>

<span data-ttu-id="c642f-160">Hello **loopName** proprietà consente toospecify se copyIndex fa riferimento iterazione risorsa tooa o l'iterazione di proprietà.</span><span class="sxs-lookup"><span data-stu-id="c642f-160">hello **loopName** property enables you toospecify whether copyIndex is referring tooa resource iteration or property iteration.</span></span> <span data-ttu-id="c642f-161">Se non viene fornito alcun valore per **loopName**, viene utilizzato l'iterazione di tipo risorsa corrente hello.</span><span class="sxs-lookup"><span data-stu-id="c642f-161">If no value is provided for **loopName**, hello current resource type iteration is used.</span></span> <span data-ttu-id="c642f-162">Specificare un valore per **loopName** durante l'iterazione di una proprietà.</span><span class="sxs-lookup"><span data-stu-id="c642f-162">Provide a value for **loopName** when iterating on a property.</span></span> 
 
<span data-ttu-id="c642f-163">Per una descrizione completa dell'uso di **copyIndex**, vedere [Creare più istanze di risorse in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="c642f-163">For a complete description of how you use **copyIndex**, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

### <a name="example"></a><span data-ttu-id="c642f-164">Esempio</span><span class="sxs-lookup"><span data-stu-id="c642f-164">Example</span></span>

<span data-ttu-id="c642f-165">Hello esempio seguente viene illustrato un ciclo e hello indice valore copia incluso nel nome hello.</span><span class="sxs-lookup"><span data-stu-id="c642f-165">hello following example shows a copy loop and hello index value included in hello name.</span></span> 

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

### <a name="return-value"></a><span data-ttu-id="c642f-166">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="c642f-166">Return value</span></span>

<span data-ttu-id="c642f-167">Numero intero che rappresenta l'indice corrente di hello di iterazione hello.</span><span class="sxs-lookup"><span data-stu-id="c642f-167">An integer representing hello current index of hello iteration.</span></span>

<a id="div" />

## <a name="div"></a><span data-ttu-id="c642f-168">div</span><span class="sxs-lookup"><span data-stu-id="c642f-168">div</span></span>
`div(operand1, operand2)`

<span data-ttu-id="c642f-169">Restituisce hello divisione di integer di due interi fornito di hello.</span><span class="sxs-lookup"><span data-stu-id="c642f-169">Returns hello integer division of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="c642f-170">parameters</span><span class="sxs-lookup"><span data-stu-id="c642f-170">Parameters</span></span>

| <span data-ttu-id="c642f-171">Parametro</span><span class="sxs-lookup"><span data-stu-id="c642f-171">Parameter</span></span> | <span data-ttu-id="c642f-172">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="c642f-172">Required</span></span> | <span data-ttu-id="c642f-173">Tipo</span><span class="sxs-lookup"><span data-stu-id="c642f-173">Type</span></span> | <span data-ttu-id="c642f-174">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c642f-174">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c642f-175">operand1</span><span class="sxs-lookup"><span data-stu-id="c642f-175">operand1</span></span> |<span data-ttu-id="c642f-176">Sì</span><span class="sxs-lookup"><span data-stu-id="c642f-176">Yes</span></span> |<span data-ttu-id="c642f-177">int</span><span class="sxs-lookup"><span data-stu-id="c642f-177">int</span></span> |<span data-ttu-id="c642f-178">numero di Hello viene diviso.</span><span class="sxs-lookup"><span data-stu-id="c642f-178">hello number being divided.</span></span> |
| <span data-ttu-id="c642f-179">operand2</span><span class="sxs-lookup"><span data-stu-id="c642f-179">operand2</span></span> |<span data-ttu-id="c642f-180">Sì</span><span class="sxs-lookup"><span data-stu-id="c642f-180">Yes</span></span> |<span data-ttu-id="c642f-181">int</span><span class="sxs-lookup"><span data-stu-id="c642f-181">int</span></span> |<span data-ttu-id="c642f-182">Hello numero toodivide utilizzato.</span><span class="sxs-lookup"><span data-stu-id="c642f-182">hello number that is used toodivide.</span></span> <span data-ttu-id="c642f-183">Non può essere 0.</span><span class="sxs-lookup"><span data-stu-id="c642f-183">Cannot be 0.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c642f-184">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="c642f-184">Return value</span></span>

<span data-ttu-id="c642f-185">Una divisione di interi che rappresentano hello.</span><span class="sxs-lookup"><span data-stu-id="c642f-185">An integer representing hello division.</span></span>

### <a name="example"></a><span data-ttu-id="c642f-186">Esempio</span><span class="sxs-lookup"><span data-stu-id="c642f-186">Example</span></span>

<span data-ttu-id="c642f-187">Hello di esempio seguente consente di dividere un parametro da un altro parametro.</span><span class="sxs-lookup"><span data-stu-id="c642f-187">hello following example divides one parameter by another parameter.</span></span>

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
                "description": "Integer used toodivide"
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

<span data-ttu-id="c642f-188">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="c642f-188">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="c642f-189">Nome</span><span class="sxs-lookup"><span data-stu-id="c642f-189">Name</span></span> | <span data-ttu-id="c642f-190">Tipo</span><span class="sxs-lookup"><span data-stu-id="c642f-190">Type</span></span> | <span data-ttu-id="c642f-191">Valore</span><span class="sxs-lookup"><span data-stu-id="c642f-191">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c642f-192">divResult</span><span class="sxs-lookup"><span data-stu-id="c642f-192">divResult</span></span> | <span data-ttu-id="c642f-193">int</span><span class="sxs-lookup"><span data-stu-id="c642f-193">Int</span></span> | <span data-ttu-id="c642f-194">2</span><span class="sxs-lookup"><span data-stu-id="c642f-194">2</span></span> |

<a id="float" />

## <a name="float"></a><span data-ttu-id="c642f-195">float</span><span class="sxs-lookup"><span data-stu-id="c642f-195">float</span></span>
`float(arg1)`

<span data-ttu-id="c642f-196">Converte tooa valore hello numero a virgola mobile.</span><span class="sxs-lookup"><span data-stu-id="c642f-196">Converts hello value tooa floating point number.</span></span> <span data-ttu-id="c642f-197">Questa funzione è utilizzare solo quando si passano parametri personalizzati tooan applicazione, ad esempio un'App di logica.</span><span class="sxs-lookup"><span data-stu-id="c642f-197">You only use this function when passing custom parameters tooan application, such as a Logic App.</span></span>

### <a name="parameters"></a><span data-ttu-id="c642f-198">parameters</span><span class="sxs-lookup"><span data-stu-id="c642f-198">Parameters</span></span>

| <span data-ttu-id="c642f-199">Parametro</span><span class="sxs-lookup"><span data-stu-id="c642f-199">Parameter</span></span> | <span data-ttu-id="c642f-200">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="c642f-200">Required</span></span> | <span data-ttu-id="c642f-201">Tipo</span><span class="sxs-lookup"><span data-stu-id="c642f-201">Type</span></span> | <span data-ttu-id="c642f-202">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c642f-202">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c642f-203">arg1</span><span class="sxs-lookup"><span data-stu-id="c642f-203">arg1</span></span> |<span data-ttu-id="c642f-204">Sì</span><span class="sxs-lookup"><span data-stu-id="c642f-204">Yes</span></span> |<span data-ttu-id="c642f-205">stringa o numero intero</span><span class="sxs-lookup"><span data-stu-id="c642f-205">string or int</span></span> |<span data-ttu-id="c642f-206">Hello valore tooconvert tooa numero a virgola mobile.</span><span class="sxs-lookup"><span data-stu-id="c642f-206">hello value tooconvert tooa floating point number.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c642f-207">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="c642f-207">Return value</span></span>
<span data-ttu-id="c642f-208">Un numero a virgola mobile.</span><span class="sxs-lookup"><span data-stu-id="c642f-208">A floating point number.</span></span>

### <a name="example"></a><span data-ttu-id="c642f-209">Esempio</span><span class="sxs-lookup"><span data-stu-id="c642f-209">Example</span></span>

<span data-ttu-id="c642f-210">Hello di esempio seguente viene illustrato come toouse float toopass parametri tooa logica App:</span><span class="sxs-lookup"><span data-stu-id="c642f-210">hello following example shows how toouse float toopass parameters tooa Logic App:</span></span>

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

## <a name="int"></a><span data-ttu-id="c642f-211">int</span><span class="sxs-lookup"><span data-stu-id="c642f-211">int</span></span>
`int(valueToConvert)`

<span data-ttu-id="c642f-212">Converte l'intero tooan di hello valore specificato.</span><span class="sxs-lookup"><span data-stu-id="c642f-212">Converts hello specified value tooan integer.</span></span>

### <a name="parameters"></a><span data-ttu-id="c642f-213">parameters</span><span class="sxs-lookup"><span data-stu-id="c642f-213">Parameters</span></span>

| <span data-ttu-id="c642f-214">Parametro</span><span class="sxs-lookup"><span data-stu-id="c642f-214">Parameter</span></span> | <span data-ttu-id="c642f-215">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="c642f-215">Required</span></span> | <span data-ttu-id="c642f-216">Tipo</span><span class="sxs-lookup"><span data-stu-id="c642f-216">Type</span></span> | <span data-ttu-id="c642f-217">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c642f-217">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c642f-218">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="c642f-218">valueToConvert</span></span> |<span data-ttu-id="c642f-219">Sì</span><span class="sxs-lookup"><span data-stu-id="c642f-219">Yes</span></span> |<span data-ttu-id="c642f-220">stringa o numero intero</span><span class="sxs-lookup"><span data-stu-id="c642f-220">string or int</span></span> |<span data-ttu-id="c642f-221">Hello valore tooconvert tooan numero intero.</span><span class="sxs-lookup"><span data-stu-id="c642f-221">hello value tooconvert tooan integer.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c642f-222">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="c642f-222">Return value</span></span>

<span data-ttu-id="c642f-223">Valore convertito da un numero intero di hello.</span><span class="sxs-lookup"><span data-stu-id="c642f-223">An integer of hello converted value.</span></span>

### <a name="example"></a><span data-ttu-id="c642f-224">Esempio</span><span class="sxs-lookup"><span data-stu-id="c642f-224">Example</span></span>

<span data-ttu-id="c642f-225">Hello seguente converte toointeger valore di parametro fornito dall'utente hello.</span><span class="sxs-lookup"><span data-stu-id="c642f-225">hello following example converts hello user-provided parameter value toointeger.</span></span>

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

<span data-ttu-id="c642f-226">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="c642f-226">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="c642f-227">Nome</span><span class="sxs-lookup"><span data-stu-id="c642f-227">Name</span></span> | <span data-ttu-id="c642f-228">Tipo</span><span class="sxs-lookup"><span data-stu-id="c642f-228">Type</span></span> | <span data-ttu-id="c642f-229">Valore</span><span class="sxs-lookup"><span data-stu-id="c642f-229">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c642f-230">intResult</span><span class="sxs-lookup"><span data-stu-id="c642f-230">intResult</span></span> | <span data-ttu-id="c642f-231">int</span><span class="sxs-lookup"><span data-stu-id="c642f-231">Int</span></span> | <span data-ttu-id="c642f-232">4</span><span class="sxs-lookup"><span data-stu-id="c642f-232">4</span></span> |


<a id="min" />

## <a name="min"></a><span data-ttu-id="c642f-233">Min</span><span class="sxs-lookup"><span data-stu-id="c642f-233">min</span></span>
`min (arg1)`

<span data-ttu-id="c642f-234">Restituisce hello valore minimo da una matrice di interi o un elenco delimitato da virgole di numeri interi.</span><span class="sxs-lookup"><span data-stu-id="c642f-234">Returns hello minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="c642f-235">parameters</span><span class="sxs-lookup"><span data-stu-id="c642f-235">Parameters</span></span>

| <span data-ttu-id="c642f-236">Parametro</span><span class="sxs-lookup"><span data-stu-id="c642f-236">Parameter</span></span> | <span data-ttu-id="c642f-237">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="c642f-237">Required</span></span> | <span data-ttu-id="c642f-238">Tipo</span><span class="sxs-lookup"><span data-stu-id="c642f-238">Type</span></span> | <span data-ttu-id="c642f-239">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c642f-239">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c642f-240">arg1</span><span class="sxs-lookup"><span data-stu-id="c642f-240">arg1</span></span> |<span data-ttu-id="c642f-241">Sì</span><span class="sxs-lookup"><span data-stu-id="c642f-241">Yes</span></span> |<span data-ttu-id="c642f-242">matrice di numeri interi o elenco di numeri interi delimitato da virgole</span><span class="sxs-lookup"><span data-stu-id="c642f-242">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="c642f-243">Hello raccolta tooget hello valore minimo.</span><span class="sxs-lookup"><span data-stu-id="c642f-243">hello collection tooget hello minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c642f-244">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="c642f-244">Return value</span></span>

<span data-ttu-id="c642f-245">Intero che rappresenta il valore minimo da raccolta hello.</span><span class="sxs-lookup"><span data-stu-id="c642f-245">An integer representing minimum value from hello collection.</span></span>

### <a name="example"></a><span data-ttu-id="c642f-246">Esempio</span><span class="sxs-lookup"><span data-stu-id="c642f-246">Example</span></span>

<span data-ttu-id="c642f-247">Hello seguente esempio viene illustrato come toouse min con una matrice e un elenco di numeri interi:</span><span class="sxs-lookup"><span data-stu-id="c642f-247">hello following example shows how toouse min with an array and a list of integers:</span></span>

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

<span data-ttu-id="c642f-248">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="c642f-248">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="c642f-249">Nome</span><span class="sxs-lookup"><span data-stu-id="c642f-249">Name</span></span> | <span data-ttu-id="c642f-250">Tipo</span><span class="sxs-lookup"><span data-stu-id="c642f-250">Type</span></span> | <span data-ttu-id="c642f-251">Valore</span><span class="sxs-lookup"><span data-stu-id="c642f-251">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c642f-252">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="c642f-252">arrayOutput</span></span> | <span data-ttu-id="c642f-253">int</span><span class="sxs-lookup"><span data-stu-id="c642f-253">Int</span></span> | <span data-ttu-id="c642f-254">0</span><span class="sxs-lookup"><span data-stu-id="c642f-254">0</span></span> |
| <span data-ttu-id="c642f-255">intOutput</span><span class="sxs-lookup"><span data-stu-id="c642f-255">intOutput</span></span> | <span data-ttu-id="c642f-256">int</span><span class="sxs-lookup"><span data-stu-id="c642f-256">Int</span></span> | <span data-ttu-id="c642f-257">0</span><span class="sxs-lookup"><span data-stu-id="c642f-257">0</span></span> |

<a id="max" />

## <a name="max"></a><span data-ttu-id="c642f-258">max</span><span class="sxs-lookup"><span data-stu-id="c642f-258">max</span></span>
`max (arg1)`

<span data-ttu-id="c642f-259">Restituisce hello valore massimo da una matrice di interi o un elenco delimitato da virgole di numeri interi.</span><span class="sxs-lookup"><span data-stu-id="c642f-259">Returns hello maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="c642f-260">parameters</span><span class="sxs-lookup"><span data-stu-id="c642f-260">Parameters</span></span>

| <span data-ttu-id="c642f-261">Parametro</span><span class="sxs-lookup"><span data-stu-id="c642f-261">Parameter</span></span> | <span data-ttu-id="c642f-262">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="c642f-262">Required</span></span> | <span data-ttu-id="c642f-263">Tipo</span><span class="sxs-lookup"><span data-stu-id="c642f-263">Type</span></span> | <span data-ttu-id="c642f-264">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c642f-264">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c642f-265">arg1</span><span class="sxs-lookup"><span data-stu-id="c642f-265">arg1</span></span> |<span data-ttu-id="c642f-266">Sì</span><span class="sxs-lookup"><span data-stu-id="c642f-266">Yes</span></span> |<span data-ttu-id="c642f-267">matrice di numeri interi o elenco di numeri interi delimitato da virgole</span><span class="sxs-lookup"><span data-stu-id="c642f-267">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="c642f-268">Hello raccolta tooget hello valore massimo.</span><span class="sxs-lookup"><span data-stu-id="c642f-268">hello collection tooget hello maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c642f-269">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="c642f-269">Return value</span></span>

<span data-ttu-id="c642f-270">Intero che rappresenta il valore massimo di hello dalla raccolta hello.</span><span class="sxs-lookup"><span data-stu-id="c642f-270">An integer representing hello maximum value from hello collection.</span></span>

### <a name="example"></a><span data-ttu-id="c642f-271">Esempio</span><span class="sxs-lookup"><span data-stu-id="c642f-271">Example</span></span>

<span data-ttu-id="c642f-272">Hello seguente esempio viene illustrato come toouse max a una matrice e un elenco di numeri interi:</span><span class="sxs-lookup"><span data-stu-id="c642f-272">hello following example shows how toouse max with an array and a list of integers:</span></span>

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

<span data-ttu-id="c642f-273">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="c642f-273">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="c642f-274">Nome</span><span class="sxs-lookup"><span data-stu-id="c642f-274">Name</span></span> | <span data-ttu-id="c642f-275">Tipo</span><span class="sxs-lookup"><span data-stu-id="c642f-275">Type</span></span> | <span data-ttu-id="c642f-276">Valore</span><span class="sxs-lookup"><span data-stu-id="c642f-276">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c642f-277">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="c642f-277">arrayOutput</span></span> | <span data-ttu-id="c642f-278">int</span><span class="sxs-lookup"><span data-stu-id="c642f-278">Int</span></span> | <span data-ttu-id="c642f-279">5</span><span class="sxs-lookup"><span data-stu-id="c642f-279">5</span></span> |
| <span data-ttu-id="c642f-280">intOutput</span><span class="sxs-lookup"><span data-stu-id="c642f-280">intOutput</span></span> | <span data-ttu-id="c642f-281">int</span><span class="sxs-lookup"><span data-stu-id="c642f-281">Int</span></span> | <span data-ttu-id="c642f-282">5</span><span class="sxs-lookup"><span data-stu-id="c642f-282">5</span></span> |

<a id="mod" />

## <a name="mod"></a><span data-ttu-id="c642f-283">mod</span><span class="sxs-lookup"><span data-stu-id="c642f-283">mod</span></span>
`mod(operand1, operand2)`

<span data-ttu-id="c642f-284">Restituisce il resto di hello della divisione di interi hello usando interi forniti due hello.</span><span class="sxs-lookup"><span data-stu-id="c642f-284">Returns hello remainder of hello integer division using hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="c642f-285">parameters</span><span class="sxs-lookup"><span data-stu-id="c642f-285">Parameters</span></span>

| <span data-ttu-id="c642f-286">Parametro</span><span class="sxs-lookup"><span data-stu-id="c642f-286">Parameter</span></span> | <span data-ttu-id="c642f-287">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="c642f-287">Required</span></span> | <span data-ttu-id="c642f-288">Tipo</span><span class="sxs-lookup"><span data-stu-id="c642f-288">Type</span></span> | <span data-ttu-id="c642f-289">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c642f-289">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c642f-290">operand1</span><span class="sxs-lookup"><span data-stu-id="c642f-290">operand1</span></span> |<span data-ttu-id="c642f-291">Sì</span><span class="sxs-lookup"><span data-stu-id="c642f-291">Yes</span></span> |<span data-ttu-id="c642f-292">int</span><span class="sxs-lookup"><span data-stu-id="c642f-292">int</span></span> |<span data-ttu-id="c642f-293">numero di Hello viene diviso.</span><span class="sxs-lookup"><span data-stu-id="c642f-293">hello number being divided.</span></span> |
| <span data-ttu-id="c642f-294">operand2</span><span class="sxs-lookup"><span data-stu-id="c642f-294">operand2</span></span> |<span data-ttu-id="c642f-295">Sì</span><span class="sxs-lookup"><span data-stu-id="c642f-295">Yes</span></span> |<span data-ttu-id="c642f-296">int</span><span class="sxs-lookup"><span data-stu-id="c642f-296">int</span></span> |<span data-ttu-id="c642f-297">numero di Hello toodivide utilizzato, non può essere 0.</span><span class="sxs-lookup"><span data-stu-id="c642f-297">hello number that is used toodivide, Cannot be 0.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c642f-298">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="c642f-298">Return value</span></span>
<span data-ttu-id="c642f-299">Un numero intero che rappresenta hello parte restante.</span><span class="sxs-lookup"><span data-stu-id="c642f-299">An integer representing hello remainder.</span></span>

### <a name="example"></a><span data-ttu-id="c642f-300">Esempio</span><span class="sxs-lookup"><span data-stu-id="c642f-300">Example</span></span>

<span data-ttu-id="c642f-301">Hello esempio seguente restituisce il resto di hello della divisione di un parametro da un altro parametro.</span><span class="sxs-lookup"><span data-stu-id="c642f-301">hello following example returns hello remainder of dividing one parameter by another parameter.</span></span>

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
                "description": "Integer used toodivide"
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

<span data-ttu-id="c642f-302">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="c642f-302">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="c642f-303">Nome</span><span class="sxs-lookup"><span data-stu-id="c642f-303">Name</span></span> | <span data-ttu-id="c642f-304">Tipo</span><span class="sxs-lookup"><span data-stu-id="c642f-304">Type</span></span> | <span data-ttu-id="c642f-305">Valore</span><span class="sxs-lookup"><span data-stu-id="c642f-305">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c642f-306">modResult</span><span class="sxs-lookup"><span data-stu-id="c642f-306">modResult</span></span> | <span data-ttu-id="c642f-307">int</span><span class="sxs-lookup"><span data-stu-id="c642f-307">Int</span></span> | <span data-ttu-id="c642f-308">1</span><span class="sxs-lookup"><span data-stu-id="c642f-308">1</span></span> |

<a id="mul" />

## <a name="mul"></a><span data-ttu-id="c642f-309">mul</span><span class="sxs-lookup"><span data-stu-id="c642f-309">mul</span></span>
`mul(operand1, operand2)`

<span data-ttu-id="c642f-310">Restituisce hello moltiplicazione di due interi fornito di hello.</span><span class="sxs-lookup"><span data-stu-id="c642f-310">Returns hello multiplication of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="c642f-311">parameters</span><span class="sxs-lookup"><span data-stu-id="c642f-311">Parameters</span></span>

| <span data-ttu-id="c642f-312">Parametro</span><span class="sxs-lookup"><span data-stu-id="c642f-312">Parameter</span></span> | <span data-ttu-id="c642f-313">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="c642f-313">Required</span></span> | <span data-ttu-id="c642f-314">Tipo</span><span class="sxs-lookup"><span data-stu-id="c642f-314">Type</span></span> | <span data-ttu-id="c642f-315">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c642f-315">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c642f-316">operand1</span><span class="sxs-lookup"><span data-stu-id="c642f-316">operand1</span></span> |<span data-ttu-id="c642f-317">Sì</span><span class="sxs-lookup"><span data-stu-id="c642f-317">Yes</span></span> |<span data-ttu-id="c642f-318">int</span><span class="sxs-lookup"><span data-stu-id="c642f-318">int</span></span> |<span data-ttu-id="c642f-319">Primo numero toomultiply.</span><span class="sxs-lookup"><span data-stu-id="c642f-319">First number toomultiply.</span></span> |
| <span data-ttu-id="c642f-320">operand2</span><span class="sxs-lookup"><span data-stu-id="c642f-320">operand2</span></span> |<span data-ttu-id="c642f-321">Sì</span><span class="sxs-lookup"><span data-stu-id="c642f-321">Yes</span></span> |<span data-ttu-id="c642f-322">int</span><span class="sxs-lookup"><span data-stu-id="c642f-322">int</span></span> |<span data-ttu-id="c642f-323">Secondo numero toomultiply.</span><span class="sxs-lookup"><span data-stu-id="c642f-323">Second number toomultiply.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c642f-324">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="c642f-324">Return value</span></span>

<span data-ttu-id="c642f-325">Una numero intero che rappresenta hello la moltiplicazione.</span><span class="sxs-lookup"><span data-stu-id="c642f-325">An integer representing hello multiplication.</span></span>

### <a name="example"></a><span data-ttu-id="c642f-326">Esempio</span><span class="sxs-lookup"><span data-stu-id="c642f-326">Example</span></span>

<span data-ttu-id="c642f-327">Hello di esempio seguente moltiplica un parametro da un altro parametro.</span><span class="sxs-lookup"><span data-stu-id="c642f-327">hello following example multiplies one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer toomultiply"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer toomultiply"
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

<span data-ttu-id="c642f-328">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="c642f-328">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="c642f-329">Nome</span><span class="sxs-lookup"><span data-stu-id="c642f-329">Name</span></span> | <span data-ttu-id="c642f-330">Tipo</span><span class="sxs-lookup"><span data-stu-id="c642f-330">Type</span></span> | <span data-ttu-id="c642f-331">Valore</span><span class="sxs-lookup"><span data-stu-id="c642f-331">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c642f-332">mulResult</span><span class="sxs-lookup"><span data-stu-id="c642f-332">mulResult</span></span> | <span data-ttu-id="c642f-333">int</span><span class="sxs-lookup"><span data-stu-id="c642f-333">Int</span></span> | <span data-ttu-id="c642f-334">15</span><span class="sxs-lookup"><span data-stu-id="c642f-334">15</span></span> |

<a id="sub" />

## <a name="sub"></a><span data-ttu-id="c642f-335">sub</span><span class="sxs-lookup"><span data-stu-id="c642f-335">sub</span></span>
`sub(operand1, operand2)`

<span data-ttu-id="c642f-336">Restituisce hello sottrazione di due interi fornito di hello.</span><span class="sxs-lookup"><span data-stu-id="c642f-336">Returns hello subtraction of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="c642f-337">parameters</span><span class="sxs-lookup"><span data-stu-id="c642f-337">Parameters</span></span>

| <span data-ttu-id="c642f-338">Parametro</span><span class="sxs-lookup"><span data-stu-id="c642f-338">Parameter</span></span> | <span data-ttu-id="c642f-339">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="c642f-339">Required</span></span> | <span data-ttu-id="c642f-340">Tipo</span><span class="sxs-lookup"><span data-stu-id="c642f-340">Type</span></span> | <span data-ttu-id="c642f-341">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c642f-341">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c642f-342">operand1</span><span class="sxs-lookup"><span data-stu-id="c642f-342">operand1</span></span> |<span data-ttu-id="c642f-343">Sì</span><span class="sxs-lookup"><span data-stu-id="c642f-343">Yes</span></span> |<span data-ttu-id="c642f-344">int</span><span class="sxs-lookup"><span data-stu-id="c642f-344">int</span></span> |<span data-ttu-id="c642f-345">numero di Hello che viene sottratto.</span><span class="sxs-lookup"><span data-stu-id="c642f-345">hello number that is subtracted from.</span></span> |
| <span data-ttu-id="c642f-346">operand2</span><span class="sxs-lookup"><span data-stu-id="c642f-346">operand2</span></span> |<span data-ttu-id="c642f-347">Sì</span><span class="sxs-lookup"><span data-stu-id="c642f-347">Yes</span></span> |<span data-ttu-id="c642f-348">int</span><span class="sxs-lookup"><span data-stu-id="c642f-348">int</span></span> |<span data-ttu-id="c642f-349">numero di Hello che viene sottratto.</span><span class="sxs-lookup"><span data-stu-id="c642f-349">hello number that is subtracted.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c642f-350">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="c642f-350">Return value</span></span>
<span data-ttu-id="c642f-351">Una numero intero che rappresenta hello la sottrazione.</span><span class="sxs-lookup"><span data-stu-id="c642f-351">An integer representing hello subtraction.</span></span>

### <a name="example"></a><span data-ttu-id="c642f-352">Esempio</span><span class="sxs-lookup"><span data-stu-id="c642f-352">Example</span></span>

<span data-ttu-id="c642f-353">Hello di esempio seguente sottrae un parametro da un altro parametro.</span><span class="sxs-lookup"><span data-stu-id="c642f-353">hello following example subtracts one parameter from another parameter.</span></span>

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
                "description": "Integer toosubtract"
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

<span data-ttu-id="c642f-354">Hello output di hello precedente esempio con i valori predefiniti di hello è:</span><span class="sxs-lookup"><span data-stu-id="c642f-354">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="c642f-355">Nome</span><span class="sxs-lookup"><span data-stu-id="c642f-355">Name</span></span> | <span data-ttu-id="c642f-356">Tipo</span><span class="sxs-lookup"><span data-stu-id="c642f-356">Type</span></span> | <span data-ttu-id="c642f-357">Valore</span><span class="sxs-lookup"><span data-stu-id="c642f-357">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c642f-358">subResult</span><span class="sxs-lookup"><span data-stu-id="c642f-358">subResult</span></span> | <span data-ttu-id="c642f-359">int</span><span class="sxs-lookup"><span data-stu-id="c642f-359">Int</span></span> | <span data-ttu-id="c642f-360">4</span><span class="sxs-lookup"><span data-stu-id="c642f-360">4</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c642f-361">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c642f-361">Next steps</span></span>
* <span data-ttu-id="c642f-362">Per una descrizione delle sezioni hello in un modello di gestione risorse di Azure, vedere [modelli Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c642f-362">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="c642f-363">toomerge più modelli, vedere [con modelli collegati con Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c642f-363">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="c642f-364">tooiterate un numero specificato di volte durante la creazione di un tipo di risorsa, vedere [creare più istanze delle risorse in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="c642f-364">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="c642f-365">toosee come modello hello toodeploy è stato creato, vedere [distribuire un'applicazione con il modello di gestione risorse di Azure](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="c642f-365">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

