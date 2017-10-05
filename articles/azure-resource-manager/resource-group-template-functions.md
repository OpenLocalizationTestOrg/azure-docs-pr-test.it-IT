---
title: Funzioni del modello di gestione risorse | Microsoft Docs
description: Vengono descritte le funzioni da utilizzare in un modello di gestione risorse di Azure per recuperare valori, lavorare con stringhe e valori numerici, e recuperare informazioni sulla distribuzione.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 0644abe1-abaa-443d-820d-1966d7d26bfd
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: tomfitz
ms.openlocfilehash: 1324bed07e991e9d84cb6832afe78bdb2d3348fa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-resource-manager-template-functions"></a><span data-ttu-id="fdb72-103">Funzioni del modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fdb72-103">Azure Resource Manager template functions</span></span>
<span data-ttu-id="fdb72-104">Questo argomento descrive tutte le funzioni disponibili in un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fdb72-104">This topic describes all the functions you can use in an Azure Resource Manager template.</span></span>

<span data-ttu-id="fdb72-105">Le funzioni vengono aggiunte ai modelli racchiudendole tra parentesi quadre: `[` e `]`, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="fdb72-105">You add functions in your templates by enclosing them within brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="fdb72-106">L'espressione viene valutata durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="fdb72-106">The expression is evaluated during deployment.</span></span> <span data-ttu-id="fdb72-107">Sebbene sia scritto come valore letterale stringa, il risultato della valutazione dell'espressione può essere di un tipo JSON diverso, ad esempio una matrice, un oggetto o un numero intero.</span><span class="sxs-lookup"><span data-stu-id="fdb72-107">While written as a string literal, the result of evaluating the expression can be of a different JSON type, such as an array, object, or integer.</span></span> <span data-ttu-id="fdb72-108">Proprio come in JavaScript, le chiamate di funzione sono formattate come `functionName(arg1,arg2,arg3)`.</span><span class="sxs-lookup"><span data-stu-id="fdb72-108">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="fdb72-109">Per i riferimenti alle proprietà si usano il punto e gli operatori [index].</span><span class="sxs-lookup"><span data-stu-id="fdb72-109">You reference properties by using the dot and [index] operators.</span></span>

<span data-ttu-id="fdb72-110">L'espressione di un modello non può superare i 24.576 caratteri.</span><span class="sxs-lookup"><span data-stu-id="fdb72-110">A template expression cannot exceed 24,576 characters.</span></span>

<span data-ttu-id="fdb72-111">Le funzioni del modello e i relativi parametri non hanno la distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="fdb72-111">Template functions and their parameters are case-insensitive.</span></span> <span data-ttu-id="fdb72-112">Ad esempio, Gestione risorse consente di risolvere allo stesso modo le **variables('var1')** e le **VARIABLES('VAR1')**.</span><span class="sxs-lookup"><span data-stu-id="fdb72-112">For example, Resource Manager resolves **variables('var1')** and **VARIABLES('VAR1')** as the same.</span></span> <span data-ttu-id="fdb72-113">Durante la valutazione, la funzione mantiene invariato l'uso delle maiuscole/minuscole, a meno che queste non vengano modificate espressamente dalla funzione, ad esempio toUpper o toLower.</span><span class="sxs-lookup"><span data-stu-id="fdb72-113">When evaluated, unless the function expressly modifies case (such as toUpper or toLower), the function preserves the case.</span></span> <span data-ttu-id="fdb72-114">Alcuni tipi di risorse possono avere requisiti per le maiuscole e minuscole indipendentemente dalla modalità di valutazione delle funzioni.</span><span class="sxs-lookup"><span data-stu-id="fdb72-114">Certain resource types may have case requirements irrespective of how functions are evaluated.</span></span>

<a id="array" />
<a id="coalesce" />
<a id="concatarray" />
<a id="contains" />
<a id="createarray" />
<a id="empty" />
<a id="first" />
<a id="intersection" />
<a id="last" />
<a id="length" />
<a id="min" />
<a id="max" />
<a id="range" />
<a id="skip" />
<a id="take" />
<a id="union" />

## <a name="array-and-object-functions"></a><span data-ttu-id="fdb72-115">Funzioni di array e di oggetto</span><span class="sxs-lookup"><span data-stu-id="fdb72-115">Array and object functions</span></span>
<span data-ttu-id="fdb72-116">Resource Manager include numerose funzioni per gestire gli array e gli oggetti.</span><span class="sxs-lookup"><span data-stu-id="fdb72-116">Resource Manager provides several functions for working with arrays and objects.</span></span>

* [<span data-ttu-id="fdb72-117">array</span><span class="sxs-lookup"><span data-stu-id="fdb72-117">array</span></span>](resource-group-template-functions-array.md#array)
* [<span data-ttu-id="fdb72-118">coalesce</span><span class="sxs-lookup"><span data-stu-id="fdb72-118">coalesce</span></span>](resource-group-template-functions-array.md#coalesce)
* [<span data-ttu-id="fdb72-119">concat</span><span class="sxs-lookup"><span data-stu-id="fdb72-119">concat</span></span>](resource-group-template-functions-array.md#concat)
* [<span data-ttu-id="fdb72-120">contains</span><span class="sxs-lookup"><span data-stu-id="fdb72-120">contains</span></span>](resource-group-template-functions-array.md#contains)
* [<span data-ttu-id="fdb72-121">createArray</span><span class="sxs-lookup"><span data-stu-id="fdb72-121">createArray</span></span>](resource-group-template-functions-array.md#createarray)
* [<span data-ttu-id="fdb72-122">empty</span><span class="sxs-lookup"><span data-stu-id="fdb72-122">empty</span></span>](resource-group-template-functions-array.md#empty)
* [<span data-ttu-id="fdb72-123">first</span><span class="sxs-lookup"><span data-stu-id="fdb72-123">first</span></span>](resource-group-template-functions-array.md#first)
* [<span data-ttu-id="fdb72-124">intersection</span><span class="sxs-lookup"><span data-stu-id="fdb72-124">intersection</span></span>](resource-group-template-functions-array.md#intersection)
* [<span data-ttu-id="fdb72-125">json</span><span class="sxs-lookup"><span data-stu-id="fdb72-125">json</span></span>](resource-group-template-functions-array.md#json)
* [<span data-ttu-id="fdb72-126">last</span><span class="sxs-lookup"><span data-stu-id="fdb72-126">last</span></span>](resource-group-template-functions-array.md#last)
* [<span data-ttu-id="fdb72-127">length</span><span class="sxs-lookup"><span data-stu-id="fdb72-127">length</span></span>](resource-group-template-functions-array.md#length)
* [<span data-ttu-id="fdb72-128">min</span><span class="sxs-lookup"><span data-stu-id="fdb72-128">min</span></span>](resource-group-template-functions-array.md#min)
* [<span data-ttu-id="fdb72-129">max</span><span class="sxs-lookup"><span data-stu-id="fdb72-129">max</span></span>](resource-group-template-functions-array.md#max)
* [<span data-ttu-id="fdb72-130">range</span><span class="sxs-lookup"><span data-stu-id="fdb72-130">range</span></span>](resource-group-template-functions-array.md#range)
* [<span data-ttu-id="fdb72-131">skip</span><span class="sxs-lookup"><span data-stu-id="fdb72-131">skip</span></span>](resource-group-template-functions-array.md#skip)
* [<span data-ttu-id="fdb72-132">take</span><span class="sxs-lookup"><span data-stu-id="fdb72-132">take</span></span>](resource-group-template-functions-array.md#take)
* [<span data-ttu-id="fdb72-133">union</span><span class="sxs-lookup"><span data-stu-id="fdb72-133">union</span></span>](resource-group-template-functions-array.md#union)

<a id="equals" />
<a id="less" />
<a id="lessorequals" />
<a id="greater" />
<a id="greaterorequals" />

## <a name="comparison-functions"></a><span data-ttu-id="fdb72-134">Funzioni di confronto</span><span class="sxs-lookup"><span data-stu-id="fdb72-134">Comparison functions</span></span>
<span data-ttu-id="fdb72-135">Resource Manager include numerose funzioni per l'esecuzione di confronti nei modelli.</span><span class="sxs-lookup"><span data-stu-id="fdb72-135">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="fdb72-136">equals</span><span class="sxs-lookup"><span data-stu-id="fdb72-136">equals</span></span>](resource-group-template-functions-comparison.md#equals)
* [<span data-ttu-id="fdb72-137">less</span><span class="sxs-lookup"><span data-stu-id="fdb72-137">less</span></span>](resource-group-template-functions-comparison.md#less)
* [<span data-ttu-id="fdb72-138">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="fdb72-138">lessOrEquals</span></span>](resource-group-template-functions-comparison.md#lessorequals)
* [<span data-ttu-id="fdb72-139">greater</span><span class="sxs-lookup"><span data-stu-id="fdb72-139">greater</span></span>](resource-group-template-functions-comparison.md#greater)
* [<span data-ttu-id="fdb72-140">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="fdb72-140">greaterOrEquals</span></span>](resource-group-template-functions-comparison.md#greaterorequals)

<a id="deployment" />
<a id="parameters" />
<a id="variables" />

## <a name="deployment-value-functions"></a><span data-ttu-id="fdb72-141">Funzioni dei valori della distribuzione</span><span class="sxs-lookup"><span data-stu-id="fdb72-141">Deployment value functions</span></span>
<span data-ttu-id="fdb72-142">Gestione risorse fornisce le funzioni seguenti per ottenere i valori dalle sezioni del modello e i valori relativi alla distribuzione:</span><span class="sxs-lookup"><span data-stu-id="fdb72-142">Resource Manager provides the following functions for getting values from sections of the template and values related to the deployment:</span></span>

* [<span data-ttu-id="fdb72-143">deployment</span><span class="sxs-lookup"><span data-stu-id="fdb72-143">deployment</span></span>](resource-group-template-functions-deployment.md#deployment)
* [<span data-ttu-id="fdb72-144">parameters</span><span class="sxs-lookup"><span data-stu-id="fdb72-144">parameters</span></span>](resource-group-template-functions-deployment.md#parameters)
* [<span data-ttu-id="fdb72-145">variables</span><span class="sxs-lookup"><span data-stu-id="fdb72-145">variables</span></span>](resource-group-template-functions-deployment.md#variables)

<a id="add" />
<a id="copyindex" />
<a id="div" />
<a id="float" />
<a id="int" />
<a id="minint" />
<a id="maxint" />
<a id="mod" />
<a id="mul" />
<a id="sub" />

## <a name="logical-functions"></a><span data-ttu-id="fdb72-146">Funzioni logiche</span><span class="sxs-lookup"><span data-stu-id="fdb72-146">Logical functions</span></span>
<span data-ttu-id="fdb72-147">Resource Manager fornisce le funzioni seguenti per utilizzare le condizioni logiche:</span><span class="sxs-lookup"><span data-stu-id="fdb72-147">Resource Manager provides the following functions for working with logical conditions:</span></span>

* [<span data-ttu-id="fdb72-148">and</span><span class="sxs-lookup"><span data-stu-id="fdb72-148">and</span></span>](resource-group-template-functions-logical.md#and)
* [<span data-ttu-id="fdb72-149">bool</span><span class="sxs-lookup"><span data-stu-id="fdb72-149">bool</span></span>](resource-group-template-functions-logical.md#bool)
* [<span data-ttu-id="fdb72-150">if</span><span class="sxs-lookup"><span data-stu-id="fdb72-150">if</span></span>](resource-group-template-functions-logical.md#if)
* [<span data-ttu-id="fdb72-151">not</span><span class="sxs-lookup"><span data-stu-id="fdb72-151">not</span></span>](resource-group-template-functions-logical.md#not)
* [<span data-ttu-id="fdb72-152">or</span><span class="sxs-lookup"><span data-stu-id="fdb72-152">or</span></span>](resource-group-template-functions-logical.md#or)

## <a name="numeric-functions"></a><span data-ttu-id="fdb72-153">Funzioni numeriche</span><span class="sxs-lookup"><span data-stu-id="fdb72-153">Numeric functions</span></span>
<span data-ttu-id="fdb72-154">Gestione risorse fornisce le funzioni seguenti per usare i numeri interi:</span><span class="sxs-lookup"><span data-stu-id="fdb72-154">Resource Manager provides the following functions for working with integers:</span></span>

* [<span data-ttu-id="fdb72-155">add</span><span class="sxs-lookup"><span data-stu-id="fdb72-155">add</span></span>](resource-group-template-functions-numeric.md#add)
* [<span data-ttu-id="fdb72-156">copyIndex</span><span class="sxs-lookup"><span data-stu-id="fdb72-156">copyIndex</span></span>](resource-group-template-functions-numeric.md#copyindex)
* [<span data-ttu-id="fdb72-157">div</span><span class="sxs-lookup"><span data-stu-id="fdb72-157">div</span></span>](resource-group-template-functions-numeric.md#div)
* [<span data-ttu-id="fdb72-158">float</span><span class="sxs-lookup"><span data-stu-id="fdb72-158">float</span></span>](resource-group-template-functions-numeric.md#float)
* [<span data-ttu-id="fdb72-159">int</span><span class="sxs-lookup"><span data-stu-id="fdb72-159">int</span></span>](resource-group-template-functions-numeric.md#int)
* [<span data-ttu-id="fdb72-160">min</span><span class="sxs-lookup"><span data-stu-id="fdb72-160">min</span></span>](resource-group-template-functions-numeric.md#min)
* [<span data-ttu-id="fdb72-161">max</span><span class="sxs-lookup"><span data-stu-id="fdb72-161">max</span></span>](resource-group-template-functions-numeric.md#max)
* [<span data-ttu-id="fdb72-162">mod</span><span class="sxs-lookup"><span data-stu-id="fdb72-162">mod</span></span>](resource-group-template-functions-numeric.md#mod)
* [<span data-ttu-id="fdb72-163">mul</span><span class="sxs-lookup"><span data-stu-id="fdb72-163">mul</span></span>](resource-group-template-functions-numeric.md#mul)
* [<span data-ttu-id="fdb72-164">sub</span><span class="sxs-lookup"><span data-stu-id="fdb72-164">sub</span></span>](resource-group-template-functions-numeric.md#sub)

<a id="listkeys" />
<a id="list" />
<a id="providers" />
<a id="reference" />
<a id="resourcegroup" />
<a id="resourceid" />
<a id="subscription" />

## <a name="resource-functions"></a><span data-ttu-id="fdb72-165">Funzioni delle risorse</span><span class="sxs-lookup"><span data-stu-id="fdb72-165">Resource functions</span></span>
<span data-ttu-id="fdb72-166">Gestione risorse fornisce le funzioni seguenti per ottenere i valori delle risorse:</span><span class="sxs-lookup"><span data-stu-id="fdb72-166">Resource Manager provides the following functions for getting resource values:</span></span>

* [<span data-ttu-id="fdb72-167">listKeys e list{Value}</span><span class="sxs-lookup"><span data-stu-id="fdb72-167">listKeys and list{Value}</span></span>](resource-group-template-functions-resource.md#listkeys)
* [<span data-ttu-id="fdb72-168">provider</span><span class="sxs-lookup"><span data-stu-id="fdb72-168">providers</span></span>](resource-group-template-functions-resource.md#providers)
* [<span data-ttu-id="fdb72-169">reference</span><span class="sxs-lookup"><span data-stu-id="fdb72-169">reference</span></span>](resource-group-template-functions-resource.md#reference)
* [<span data-ttu-id="fdb72-170">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="fdb72-170">resourceGroup</span></span>](resource-group-template-functions-resource.md#resourcegroup)
* [<span data-ttu-id="fdb72-171">resourceId</span><span class="sxs-lookup"><span data-stu-id="fdb72-171">resourceId</span></span>](resource-group-template-functions-resource.md#resourceid)
* [<span data-ttu-id="fdb72-172">sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="fdb72-172">subscription</span></span>](resource-group-template-functions-resource.md#subscription)

<a id="base64" />
<a id="base64tojson" />
<a id="base64tostring" />
<a id="concat" />
<a id="containsstring" />
<a id="datauri" />
<a id="datauritostring" />
<a id="emptystring" />
<a id="endswith" />
<a id="firststring" />
<a id="indexof" />
<a id="laststring" />
<a id="lastindexof" />
<a id="lengthstring" />
<a id="padleft" />
<a id="replace" />
<a id="skipstring" />
<a id="split" />
<a id="startswith" />
<a id="string" />
<a id="substring" />
<a id="takestring" />
<a id="tolower" />
<a id="toupper" />
<a id="trim" />
<a id="uniquestring" />
<a id="uri" />
<a id="uricomponent" />
<a id="uricomponenttostring" />

## <a name="string-functions"></a><span data-ttu-id="fdb72-173">Funzioni stringa</span><span class="sxs-lookup"><span data-stu-id="fdb72-173">String functions</span></span>
<span data-ttu-id="fdb72-174">Gestione risorse fornisce le funzioni seguenti per usare le stringhe:</span><span class="sxs-lookup"><span data-stu-id="fdb72-174">Resource Manager provides the following functions for working with strings:</span></span>

* [<span data-ttu-id="fdb72-175">base64</span><span class="sxs-lookup"><span data-stu-id="fdb72-175">base64</span></span>](resource-group-template-functions-string.md#base64)
* [<span data-ttu-id="fdb72-176">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="fdb72-176">base64ToJson</span></span>](resource-group-template-functions-string.md#base64tojson)
* [<span data-ttu-id="fdb72-177">base64ToString</span><span class="sxs-lookup"><span data-stu-id="fdb72-177">base64ToString</span></span>](resource-group-template-functions-string.md#base64tostring)
* [<span data-ttu-id="fdb72-178">concat</span><span class="sxs-lookup"><span data-stu-id="fdb72-178">concat</span></span>](resource-group-template-functions-string.md#concat)
* [<span data-ttu-id="fdb72-179">contains</span><span class="sxs-lookup"><span data-stu-id="fdb72-179">contains</span></span>](resource-group-template-functions-string.md#contains)
* [<span data-ttu-id="fdb72-180">dataUri</span><span class="sxs-lookup"><span data-stu-id="fdb72-180">dataUri</span></span>](resource-group-template-functions-string.md#datauri)
* [<span data-ttu-id="fdb72-181">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="fdb72-181">dataUriToString</span></span>](resource-group-template-functions-string.md#datauritostring)
* [<span data-ttu-id="fdb72-182">empty</span><span class="sxs-lookup"><span data-stu-id="fdb72-182">empty</span></span>](resource-group-template-functions-string.md#empty)
* [<span data-ttu-id="fdb72-183">endsWith</span><span class="sxs-lookup"><span data-stu-id="fdb72-183">endsWith</span></span>](resource-group-template-functions-string.md#endswith)
* [<span data-ttu-id="fdb72-184">first</span><span class="sxs-lookup"><span data-stu-id="fdb72-184">first</span></span>](resource-group-template-functions-string.md#first)
* [<span data-ttu-id="fdb72-185">indexOf</span><span class="sxs-lookup"><span data-stu-id="fdb72-185">indexOf</span></span>](resource-group-template-functions-string.md#indexof)
* [<span data-ttu-id="fdb72-186">last</span><span class="sxs-lookup"><span data-stu-id="fdb72-186">last</span></span>](resource-group-template-functions-string.md#last)
* [<span data-ttu-id="fdb72-187">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="fdb72-187">lastIndexOf</span></span>](resource-group-template-functions-string.md#lastindexof)
* [<span data-ttu-id="fdb72-188">length</span><span class="sxs-lookup"><span data-stu-id="fdb72-188">length</span></span>](resource-group-template-functions-string.md#length)
* [<span data-ttu-id="fdb72-189">padLeft</span><span class="sxs-lookup"><span data-stu-id="fdb72-189">padLeft</span></span>](resource-group-template-functions-string.md#padleft)
* [<span data-ttu-id="fdb72-190">replace</span><span class="sxs-lookup"><span data-stu-id="fdb72-190">replace</span></span>](resource-group-template-functions-string.md#replace)
* [<span data-ttu-id="fdb72-191">skip</span><span class="sxs-lookup"><span data-stu-id="fdb72-191">skip</span></span>](resource-group-template-functions-string.md#skip)
* [<span data-ttu-id="fdb72-192">split</span><span class="sxs-lookup"><span data-stu-id="fdb72-192">split</span></span>](resource-group-template-functions-string.md#split)
* [<span data-ttu-id="fdb72-193">startsWith</span><span class="sxs-lookup"><span data-stu-id="fdb72-193">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="fdb72-194">string</span><span class="sxs-lookup"><span data-stu-id="fdb72-194">string</span></span>](resource-group-template-functions-string.md#string)
* [<span data-ttu-id="fdb72-195">substring</span><span class="sxs-lookup"><span data-stu-id="fdb72-195">substring</span></span>](resource-group-template-functions-string.md#substring)
* [<span data-ttu-id="fdb72-196">take</span><span class="sxs-lookup"><span data-stu-id="fdb72-196">take</span></span>](resource-group-template-functions-string.md#take)
* [<span data-ttu-id="fdb72-197">toLower</span><span class="sxs-lookup"><span data-stu-id="fdb72-197">toLower</span></span>](resource-group-template-functions-string.md#tolower)
* [<span data-ttu-id="fdb72-198">toUpper</span><span class="sxs-lookup"><span data-stu-id="fdb72-198">toUpper</span></span>](resource-group-template-functions-string.md#toupper)
* [<span data-ttu-id="fdb72-199">Trim</span><span class="sxs-lookup"><span data-stu-id="fdb72-199">trim</span></span>](resource-group-template-functions-string.md#trim)
* [<span data-ttu-id="fdb72-200">uniqueString</span><span class="sxs-lookup"><span data-stu-id="fdb72-200">uniqueString</span></span>](resource-group-template-functions-string.md#uniquestring)
* [<span data-ttu-id="fdb72-201">Uri</span><span class="sxs-lookup"><span data-stu-id="fdb72-201">uri</span></span>](resource-group-template-functions-string.md#uri)
* [<span data-ttu-id="fdb72-202">uriComponent</span><span class="sxs-lookup"><span data-stu-id="fdb72-202">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="fdb72-203">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="fdb72-203">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)


## <a name="next-steps"></a><span data-ttu-id="fdb72-204">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fdb72-204">Next steps</span></span>
* <span data-ttu-id="fdb72-205">Per una descrizione delle sezioni in un modello di Gestione risorse di Azure, vedere [Creazione di modelli di Gestione risorse di Azure](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="fdb72-205">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="fdb72-206">Per unire più modelli, vedere [Uso di modelli collegati con Gestione risorse di Azure](resource-group-linked-templates.md)</span><span class="sxs-lookup"><span data-stu-id="fdb72-206">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md)</span></span>
* <span data-ttu-id="fdb72-207">Per eseguire un'iterazione di un numero di volte specificato durante la creazione di un tipo di risorsa, vedere [Creare più istanze di risorse in Azure Resource Manager](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="fdb72-207">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>
* <span data-ttu-id="fdb72-208">Per informazioni su come distribuire il modello che è stato creato, vedere [Distribuire un'applicazione con un modello di Gestione risorse di Azure](resource-group-template-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="fdb72-208">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md)</span></span>

