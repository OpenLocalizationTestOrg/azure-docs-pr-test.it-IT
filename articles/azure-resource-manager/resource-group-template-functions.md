---
title: Funzioni di modello di gestione aaaResource | Documenti Microsoft
description: Viene descritto hello funzioni toouse i valori tooretrieve un modello Gestione risorse di Azure, utilizzare le stringhe e valori numerici e recuperare le informazioni di distribuzione.
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
ms.openlocfilehash: d1b2e68a33d75058f83d6972dadb33a6390d49b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-template-functions"></a><span data-ttu-id="06823-103">Funzioni del modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="06823-103">Azure Resource Manager template functions</span></span>
<span data-ttu-id="06823-104">In questo argomento vengono descritte tutte le funzioni hello che è possibile utilizzare un modello di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="06823-104">This topic describes all hello functions you can use in an Azure Resource Manager template.</span></span>

<span data-ttu-id="06823-105">Le funzioni vengono aggiunte ai modelli racchiudendole tra parentesi quadre: `[` e `]`, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="06823-105">You add functions in your templates by enclosing them within brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="06823-106">Hello espressione viene valutata durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="06823-106">hello expression is evaluated during deployment.</span></span> <span data-ttu-id="06823-107">Durante la scrittura sotto forma di stringa letterale, il risultato di hello della valutazione di hello espressione può essere di tipo JSON diverso, ad esempio una matrice, un oggetto o un numero intero.</span><span class="sxs-lookup"><span data-stu-id="06823-107">While written as a string literal, hello result of evaluating hello expression can be of a different JSON type, such as an array, object, or integer.</span></span> <span data-ttu-id="06823-108">Proprio come in JavaScript, le chiamate di funzione sono formattate come `functionName(arg1,arg2,arg3)`.</span><span class="sxs-lookup"><span data-stu-id="06823-108">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="06823-109">Fare riferimento alle proprietà utilizzando gli operatori di hello punto e [index].</span><span class="sxs-lookup"><span data-stu-id="06823-109">You reference properties by using hello dot and [index] operators.</span></span>

<span data-ttu-id="06823-110">L'espressione di un modello non può superare i 24.576 caratteri.</span><span class="sxs-lookup"><span data-stu-id="06823-110">A template expression cannot exceed 24,576 characters.</span></span>

<span data-ttu-id="06823-111">Le funzioni del modello e i relativi parametri non hanno la distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="06823-111">Template functions and their parameters are case-insensitive.</span></span> <span data-ttu-id="06823-112">Ad esempio, Gestione risorse risolve **variables('var1')** e **VARIABLES('VAR1')** come hello stesso.</span><span class="sxs-lookup"><span data-stu-id="06823-112">For example, Resource Manager resolves **variables('var1')** and **VARIABLES('VAR1')** as hello same.</span></span> <span data-ttu-id="06823-113">Quando viene valutata, a meno che la funzione hello modifica espressamente case (ad esempio toUpper o toLower), la funzione hello mantiene case hello.</span><span class="sxs-lookup"><span data-stu-id="06823-113">When evaluated, unless hello function expressly modifies case (such as toUpper or toLower), hello function preserves hello case.</span></span> <span data-ttu-id="06823-114">Alcuni tipi di risorse possono avere requisiti per le maiuscole e minuscole indipendentemente dalla modalità di valutazione delle funzioni.</span><span class="sxs-lookup"><span data-stu-id="06823-114">Certain resource types may have case requirements irrespective of how functions are evaluated.</span></span>

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

## <a name="array-and-object-functions"></a><span data-ttu-id="06823-115">Funzioni di array e di oggetto</span><span class="sxs-lookup"><span data-stu-id="06823-115">Array and object functions</span></span>
<span data-ttu-id="06823-116">Resource Manager include numerose funzioni per gestire gli array e gli oggetti.</span><span class="sxs-lookup"><span data-stu-id="06823-116">Resource Manager provides several functions for working with arrays and objects.</span></span>

* [<span data-ttu-id="06823-117">array</span><span class="sxs-lookup"><span data-stu-id="06823-117">array</span></span>](resource-group-template-functions-array.md#array)
* [<span data-ttu-id="06823-118">coalesce</span><span class="sxs-lookup"><span data-stu-id="06823-118">coalesce</span></span>](resource-group-template-functions-array.md#coalesce)
* [<span data-ttu-id="06823-119">concat</span><span class="sxs-lookup"><span data-stu-id="06823-119">concat</span></span>](resource-group-template-functions-array.md#concat)
* [<span data-ttu-id="06823-120">contains</span><span class="sxs-lookup"><span data-stu-id="06823-120">contains</span></span>](resource-group-template-functions-array.md#contains)
* [<span data-ttu-id="06823-121">createArray</span><span class="sxs-lookup"><span data-stu-id="06823-121">createArray</span></span>](resource-group-template-functions-array.md#createarray)
* [<span data-ttu-id="06823-122">empty</span><span class="sxs-lookup"><span data-stu-id="06823-122">empty</span></span>](resource-group-template-functions-array.md#empty)
* [<span data-ttu-id="06823-123">first</span><span class="sxs-lookup"><span data-stu-id="06823-123">first</span></span>](resource-group-template-functions-array.md#first)
* [<span data-ttu-id="06823-124">intersection</span><span class="sxs-lookup"><span data-stu-id="06823-124">intersection</span></span>](resource-group-template-functions-array.md#intersection)
* [<span data-ttu-id="06823-125">json</span><span class="sxs-lookup"><span data-stu-id="06823-125">json</span></span>](resource-group-template-functions-array.md#json)
* [<span data-ttu-id="06823-126">last</span><span class="sxs-lookup"><span data-stu-id="06823-126">last</span></span>](resource-group-template-functions-array.md#last)
* [<span data-ttu-id="06823-127">length</span><span class="sxs-lookup"><span data-stu-id="06823-127">length</span></span>](resource-group-template-functions-array.md#length)
* [<span data-ttu-id="06823-128">min</span><span class="sxs-lookup"><span data-stu-id="06823-128">min</span></span>](resource-group-template-functions-array.md#min)
* [<span data-ttu-id="06823-129">max</span><span class="sxs-lookup"><span data-stu-id="06823-129">max</span></span>](resource-group-template-functions-array.md#max)
* [<span data-ttu-id="06823-130">range</span><span class="sxs-lookup"><span data-stu-id="06823-130">range</span></span>](resource-group-template-functions-array.md#range)
* [<span data-ttu-id="06823-131">skip</span><span class="sxs-lookup"><span data-stu-id="06823-131">skip</span></span>](resource-group-template-functions-array.md#skip)
* [<span data-ttu-id="06823-132">take</span><span class="sxs-lookup"><span data-stu-id="06823-132">take</span></span>](resource-group-template-functions-array.md#take)
* [<span data-ttu-id="06823-133">union</span><span class="sxs-lookup"><span data-stu-id="06823-133">union</span></span>](resource-group-template-functions-array.md#union)

<a id="equals" />
<a id="less" />
<a id="lessorequals" />
<a id="greater" />
<a id="greaterorequals" />

## <a name="comparison-functions"></a><span data-ttu-id="06823-134">Funzioni di confronto</span><span class="sxs-lookup"><span data-stu-id="06823-134">Comparison functions</span></span>
<span data-ttu-id="06823-135">Resource Manager include numerose funzioni per l'esecuzione di confronti nei modelli.</span><span class="sxs-lookup"><span data-stu-id="06823-135">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="06823-136">equals</span><span class="sxs-lookup"><span data-stu-id="06823-136">equals</span></span>](resource-group-template-functions-comparison.md#equals)
* [<span data-ttu-id="06823-137">less</span><span class="sxs-lookup"><span data-stu-id="06823-137">less</span></span>](resource-group-template-functions-comparison.md#less)
* [<span data-ttu-id="06823-138">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="06823-138">lessOrEquals</span></span>](resource-group-template-functions-comparison.md#lessorequals)
* [<span data-ttu-id="06823-139">greater</span><span class="sxs-lookup"><span data-stu-id="06823-139">greater</span></span>](resource-group-template-functions-comparison.md#greater)
* [<span data-ttu-id="06823-140">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="06823-140">greaterOrEquals</span></span>](resource-group-template-functions-comparison.md#greaterorequals)

<a id="deployment" />
<a id="parameters" />
<a id="variables" />

## <a name="deployment-value-functions"></a><span data-ttu-id="06823-141">Funzioni dei valori della distribuzione</span><span class="sxs-lookup"><span data-stu-id="06823-141">Deployment value functions</span></span>
<span data-ttu-id="06823-142">Gestione risorse offre seguente hello funzioni per ottenere valori dalle sezioni del modello di hello e valori correlati toohello distribuzione:</span><span class="sxs-lookup"><span data-stu-id="06823-142">Resource Manager provides hello following functions for getting values from sections of hello template and values related toohello deployment:</span></span>

* [<span data-ttu-id="06823-143">deployment</span><span class="sxs-lookup"><span data-stu-id="06823-143">deployment</span></span>](resource-group-template-functions-deployment.md#deployment)
* [<span data-ttu-id="06823-144">parameters</span><span class="sxs-lookup"><span data-stu-id="06823-144">parameters</span></span>](resource-group-template-functions-deployment.md#parameters)
* [<span data-ttu-id="06823-145">variables</span><span class="sxs-lookup"><span data-stu-id="06823-145">variables</span></span>](resource-group-template-functions-deployment.md#variables)

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

## <a name="logical-functions"></a><span data-ttu-id="06823-146">Funzioni logiche</span><span class="sxs-lookup"><span data-stu-id="06823-146">Logical functions</span></span>
<span data-ttu-id="06823-147">Gestione risorse offre hello seguenti funzioni per l'utilizzo di condizioni logiche:</span><span class="sxs-lookup"><span data-stu-id="06823-147">Resource Manager provides hello following functions for working with logical conditions:</span></span>

* [<span data-ttu-id="06823-148">and</span><span class="sxs-lookup"><span data-stu-id="06823-148">and</span></span>](resource-group-template-functions-logical.md#and)
* [<span data-ttu-id="06823-149">bool</span><span class="sxs-lookup"><span data-stu-id="06823-149">bool</span></span>](resource-group-template-functions-logical.md#bool)
* [<span data-ttu-id="06823-150">if</span><span class="sxs-lookup"><span data-stu-id="06823-150">if</span></span>](resource-group-template-functions-logical.md#if)
* [<span data-ttu-id="06823-151">not</span><span class="sxs-lookup"><span data-stu-id="06823-151">not</span></span>](resource-group-template-functions-logical.md#not)
* [<span data-ttu-id="06823-152">or</span><span class="sxs-lookup"><span data-stu-id="06823-152">or</span></span>](resource-group-template-functions-logical.md#or)

## <a name="numeric-functions"></a><span data-ttu-id="06823-153">Funzioni numeriche</span><span class="sxs-lookup"><span data-stu-id="06823-153">Numeric functions</span></span>
<span data-ttu-id="06823-154">Gestione risorse offre hello seguenti funzioni per l'utilizzo di numeri interi:</span><span class="sxs-lookup"><span data-stu-id="06823-154">Resource Manager provides hello following functions for working with integers:</span></span>

* [<span data-ttu-id="06823-155">add</span><span class="sxs-lookup"><span data-stu-id="06823-155">add</span></span>](resource-group-template-functions-numeric.md#add)
* [<span data-ttu-id="06823-156">copyIndex</span><span class="sxs-lookup"><span data-stu-id="06823-156">copyIndex</span></span>](resource-group-template-functions-numeric.md#copyindex)
* [<span data-ttu-id="06823-157">div</span><span class="sxs-lookup"><span data-stu-id="06823-157">div</span></span>](resource-group-template-functions-numeric.md#div)
* [<span data-ttu-id="06823-158">float</span><span class="sxs-lookup"><span data-stu-id="06823-158">float</span></span>](resource-group-template-functions-numeric.md#float)
* [<span data-ttu-id="06823-159">int</span><span class="sxs-lookup"><span data-stu-id="06823-159">int</span></span>](resource-group-template-functions-numeric.md#int)
* [<span data-ttu-id="06823-160">min</span><span class="sxs-lookup"><span data-stu-id="06823-160">min</span></span>](resource-group-template-functions-numeric.md#min)
* [<span data-ttu-id="06823-161">max</span><span class="sxs-lookup"><span data-stu-id="06823-161">max</span></span>](resource-group-template-functions-numeric.md#max)
* [<span data-ttu-id="06823-162">mod</span><span class="sxs-lookup"><span data-stu-id="06823-162">mod</span></span>](resource-group-template-functions-numeric.md#mod)
* [<span data-ttu-id="06823-163">mul</span><span class="sxs-lookup"><span data-stu-id="06823-163">mul</span></span>](resource-group-template-functions-numeric.md#mul)
* [<span data-ttu-id="06823-164">sub</span><span class="sxs-lookup"><span data-stu-id="06823-164">sub</span></span>](resource-group-template-functions-numeric.md#sub)

<a id="listkeys" />
<a id="list" />
<a id="providers" />
<a id="reference" />
<a id="resourcegroup" />
<a id="resourceid" />
<a id="subscription" />

## <a name="resource-functions"></a><span data-ttu-id="06823-165">Funzioni delle risorse</span><span class="sxs-lookup"><span data-stu-id="06823-165">Resource functions</span></span>
<span data-ttu-id="06823-166">Gestione risorse offre hello funzioni per ottenere i valori delle risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="06823-166">Resource Manager provides hello following functions for getting resource values:</span></span>

* [<span data-ttu-id="06823-167">listKeys e list{Value}</span><span class="sxs-lookup"><span data-stu-id="06823-167">listKeys and list{Value}</span></span>](resource-group-template-functions-resource.md#listkeys)
* [<span data-ttu-id="06823-168">provider</span><span class="sxs-lookup"><span data-stu-id="06823-168">providers</span></span>](resource-group-template-functions-resource.md#providers)
* [<span data-ttu-id="06823-169">reference</span><span class="sxs-lookup"><span data-stu-id="06823-169">reference</span></span>](resource-group-template-functions-resource.md#reference)
* [<span data-ttu-id="06823-170">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="06823-170">resourceGroup</span></span>](resource-group-template-functions-resource.md#resourcegroup)
* [<span data-ttu-id="06823-171">resourceId</span><span class="sxs-lookup"><span data-stu-id="06823-171">resourceId</span></span>](resource-group-template-functions-resource.md#resourceid)
* [<span data-ttu-id="06823-172">sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="06823-172">subscription</span></span>](resource-group-template-functions-resource.md#subscription)

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

## <a name="string-functions"></a><span data-ttu-id="06823-173">Funzioni stringa</span><span class="sxs-lookup"><span data-stu-id="06823-173">String functions</span></span>
<span data-ttu-id="06823-174">Gestione risorse offre hello funzioni per l'utilizzo con le stringhe seguenti:</span><span class="sxs-lookup"><span data-stu-id="06823-174">Resource Manager provides hello following functions for working with strings:</span></span>

* [<span data-ttu-id="06823-175">base64</span><span class="sxs-lookup"><span data-stu-id="06823-175">base64</span></span>](resource-group-template-functions-string.md#base64)
* [<span data-ttu-id="06823-176">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="06823-176">base64ToJson</span></span>](resource-group-template-functions-string.md#base64tojson)
* [<span data-ttu-id="06823-177">base64ToString</span><span class="sxs-lookup"><span data-stu-id="06823-177">base64ToString</span></span>](resource-group-template-functions-string.md#base64tostring)
* [<span data-ttu-id="06823-178">concat</span><span class="sxs-lookup"><span data-stu-id="06823-178">concat</span></span>](resource-group-template-functions-string.md#concat)
* [<span data-ttu-id="06823-179">contains</span><span class="sxs-lookup"><span data-stu-id="06823-179">contains</span></span>](resource-group-template-functions-string.md#contains)
* [<span data-ttu-id="06823-180">dataUri</span><span class="sxs-lookup"><span data-stu-id="06823-180">dataUri</span></span>](resource-group-template-functions-string.md#datauri)
* [<span data-ttu-id="06823-181">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="06823-181">dataUriToString</span></span>](resource-group-template-functions-string.md#datauritostring)
* [<span data-ttu-id="06823-182">empty</span><span class="sxs-lookup"><span data-stu-id="06823-182">empty</span></span>](resource-group-template-functions-string.md#empty)
* [<span data-ttu-id="06823-183">endsWith</span><span class="sxs-lookup"><span data-stu-id="06823-183">endsWith</span></span>](resource-group-template-functions-string.md#endswith)
* [<span data-ttu-id="06823-184">first</span><span class="sxs-lookup"><span data-stu-id="06823-184">first</span></span>](resource-group-template-functions-string.md#first)
* [<span data-ttu-id="06823-185">indexOf</span><span class="sxs-lookup"><span data-stu-id="06823-185">indexOf</span></span>](resource-group-template-functions-string.md#indexof)
* [<span data-ttu-id="06823-186">last</span><span class="sxs-lookup"><span data-stu-id="06823-186">last</span></span>](resource-group-template-functions-string.md#last)
* [<span data-ttu-id="06823-187">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="06823-187">lastIndexOf</span></span>](resource-group-template-functions-string.md#lastindexof)
* [<span data-ttu-id="06823-188">length</span><span class="sxs-lookup"><span data-stu-id="06823-188">length</span></span>](resource-group-template-functions-string.md#length)
* [<span data-ttu-id="06823-189">padLeft</span><span class="sxs-lookup"><span data-stu-id="06823-189">padLeft</span></span>](resource-group-template-functions-string.md#padleft)
* [<span data-ttu-id="06823-190">replace</span><span class="sxs-lookup"><span data-stu-id="06823-190">replace</span></span>](resource-group-template-functions-string.md#replace)
* [<span data-ttu-id="06823-191">skip</span><span class="sxs-lookup"><span data-stu-id="06823-191">skip</span></span>](resource-group-template-functions-string.md#skip)
* [<span data-ttu-id="06823-192">split</span><span class="sxs-lookup"><span data-stu-id="06823-192">split</span></span>](resource-group-template-functions-string.md#split)
* [<span data-ttu-id="06823-193">startsWith</span><span class="sxs-lookup"><span data-stu-id="06823-193">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="06823-194">string</span><span class="sxs-lookup"><span data-stu-id="06823-194">string</span></span>](resource-group-template-functions-string.md#string)
* [<span data-ttu-id="06823-195">substring</span><span class="sxs-lookup"><span data-stu-id="06823-195">substring</span></span>](resource-group-template-functions-string.md#substring)
* [<span data-ttu-id="06823-196">take</span><span class="sxs-lookup"><span data-stu-id="06823-196">take</span></span>](resource-group-template-functions-string.md#take)
* [<span data-ttu-id="06823-197">toLower</span><span class="sxs-lookup"><span data-stu-id="06823-197">toLower</span></span>](resource-group-template-functions-string.md#tolower)
* [<span data-ttu-id="06823-198">toUpper</span><span class="sxs-lookup"><span data-stu-id="06823-198">toUpper</span></span>](resource-group-template-functions-string.md#toupper)
* [<span data-ttu-id="06823-199">Trim</span><span class="sxs-lookup"><span data-stu-id="06823-199">trim</span></span>](resource-group-template-functions-string.md#trim)
* [<span data-ttu-id="06823-200">uniqueString</span><span class="sxs-lookup"><span data-stu-id="06823-200">uniqueString</span></span>](resource-group-template-functions-string.md#uniquestring)
* [<span data-ttu-id="06823-201">Uri</span><span class="sxs-lookup"><span data-stu-id="06823-201">uri</span></span>](resource-group-template-functions-string.md#uri)
* [<span data-ttu-id="06823-202">uriComponent</span><span class="sxs-lookup"><span data-stu-id="06823-202">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="06823-203">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="06823-203">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)


## <a name="next-steps"></a><span data-ttu-id="06823-204">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="06823-204">Next steps</span></span>
* <span data-ttu-id="06823-205">Per una descrizione delle sezioni hello in un modello di gestione risorse di Azure, vedere [modelli di creazione di gestione risorse di Azure](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="06823-205">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="06823-206">toomerge più modelli, vedere [con modelli collegati con Azure Resource Manager](resource-group-linked-templates.md)</span><span class="sxs-lookup"><span data-stu-id="06823-206">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md)</span></span>
* <span data-ttu-id="06823-207">tooiterate un numero specificato di volte durante la creazione di un tipo di risorsa, vedere [creare più istanze delle risorse di gestione risorse di Azure](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="06823-207">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>
* <span data-ttu-id="06823-208">toosee come modello hello toodeploy è stato creato, vedere [distribuire un'applicazione con il modello di gestione risorse di Azure](resource-group-template-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="06823-208">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md)</span></span>

