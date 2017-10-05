---
title: Funzioni per la creazione di definizioni dell'interfaccia utente di Applicazione gestita di Azure | Microsoft Docs
description: Illustra le funzioni da usare durante la creazione di definizioni dell'interfaccia utente per le applicazioni gestite di Azure
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 62ee10eb8e6f33cc4d828cf01b405c846bef8aa4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="createuidefinition-functions"></a><span data-ttu-id="1862e-103">Funzioni di CreateUiDefinition</span><span class="sxs-lookup"><span data-stu-id="1862e-103">CreateUiDefinition functions</span></span>
<span data-ttu-id="1862e-104">Questa sezione contiene le firme per tutte le funzioni supportate di CreateUiDefinition.</span><span class="sxs-lookup"><span data-stu-id="1862e-104">This section contains the signatures for all supported functions of a CreateUiDefinition.</span></span>

<span data-ttu-id="1862e-105">Per usare una funzione, racchiudere la dichiarazione tra parentesi quadre.</span><span class="sxs-lookup"><span data-stu-id="1862e-105">To use a function, surround the declaration with square brackets.</span></span> <span data-ttu-id="1862e-106">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="1862e-106">For example:</span></span>

```json
"[function()]"
```

<span data-ttu-id="1862e-107">È possibile fare riferimento a stringhe e altre funzioni come parametri per una funzione, ma le stringhe devono essere racchiuse tra virgolette singole.</span><span class="sxs-lookup"><span data-stu-id="1862e-107">Strings and other functions can be referenced as parameters for a function, but strings must be surrounded in single quotes.</span></span> <span data-ttu-id="1862e-108">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="1862e-108">For example:</span></span>

```json
"[fn1(fn2(), 'foobar')]"
```

<span data-ttu-id="1862e-109">Ove applicabile, si può fare riferimento alle proprietà dell'output di una funzione usando l'operatore punto.</span><span class="sxs-lookup"><span data-stu-id="1862e-109">Where applicable, you can reference properties of the output of a function by using the dot operator.</span></span> <span data-ttu-id="1862e-110">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="1862e-110">For example:</span></span>

```json
"[func().prop1]"
```

## <a name="referencing-functions"></a><span data-ttu-id="1862e-111">Funzioni di riferimento</span><span class="sxs-lookup"><span data-stu-id="1862e-111">Referencing functions</span></span>
<span data-ttu-id="1862e-112">Queste funzioni possono essere usate per fare riferimento a output delle proprietà o del contesto di CreateUiDefinition.</span><span class="sxs-lookup"><span data-stu-id="1862e-112">These functions can be used to reference outputs from the properties or context of a CreateUiDefinition.</span></span>

### <a name="basics"></a><span data-ttu-id="1862e-113">basics</span><span class="sxs-lookup"><span data-stu-id="1862e-113">basics</span></span>
<span data-ttu-id="1862e-114">Restituisce i valori di output di un elemento che viene definito nel passaggio basics.</span><span class="sxs-lookup"><span data-stu-id="1862e-114">Returns the output values of an element that is defined in the Basics step.</span></span>

<span data-ttu-id="1862e-115">L'esempio seguente restituisce l'output dell'elemento denominato `foo` nel passaggio basics:</span><span class="sxs-lookup"><span data-stu-id="1862e-115">The following example returns the output of the element named `foo` in the Basics step:</span></span>

```json
"[basics('foo')]"
```

### <a name="steps"></a><span data-ttu-id="1862e-116">steps</span><span class="sxs-lookup"><span data-stu-id="1862e-116">steps</span></span>
<span data-ttu-id="1862e-117">Restituisce i valori di output di un elemento che viene definito nel passaggio specificato.</span><span class="sxs-lookup"><span data-stu-id="1862e-117">Returns the output values of an element that is defined in the specified step.</span></span> <span data-ttu-id="1862e-118">Per ottenere i valori di output degli elementi nel passaggio basic, usare invece `basics()`.</span><span class="sxs-lookup"><span data-stu-id="1862e-118">To get the output values of elements in the Basics step, use `basics()` instead.</span></span>

<span data-ttu-id="1862e-119">L'esempio seguente restituisce l'output dell'elemento denominato `bar` nel passaggio denominato `foo`:</span><span class="sxs-lookup"><span data-stu-id="1862e-119">The following example returns the output of the element named `bar` in the step named `foo`:</span></span>

```json
"[steps('foo').bar]"
```

### <a name="location"></a><span data-ttu-id="1862e-120">location</span><span class="sxs-lookup"><span data-stu-id="1862e-120">location</span></span>
<span data-ttu-id="1862e-121">Restituisce il percorso selezionato nel passaggio basics o nel contesto corrente.</span><span class="sxs-lookup"><span data-stu-id="1862e-121">Returns the location selected in the Basics step or the current context.</span></span>

<span data-ttu-id="1862e-122">L'esempio seguente può restituire `"westus"`:</span><span class="sxs-lookup"><span data-stu-id="1862e-122">The following example could return `"westus"`:</span></span>

```json
"[location()]"
```

## <a name="string-functions"></a><span data-ttu-id="1862e-123">Funzioni stringa</span><span class="sxs-lookup"><span data-stu-id="1862e-123">String functions</span></span>
<span data-ttu-id="1862e-124">Queste funzioni possono essere usate solo con stringhe JSON.</span><span class="sxs-lookup"><span data-stu-id="1862e-124">These functions can only be used with JSON strings.</span></span>

### <a name="concat"></a><span data-ttu-id="1862e-125">concat</span><span class="sxs-lookup"><span data-stu-id="1862e-125">concat</span></span>
<span data-ttu-id="1862e-126">Concatena una o più stringhe.</span><span class="sxs-lookup"><span data-stu-id="1862e-126">Concatenates one or more strings.</span></span>

<span data-ttu-id="1862e-127">Se ad esempio il valore di output di `element1` è `"bar"`, questo esempio restituirà la stringa `"foobar!"`:</span><span class="sxs-lookup"><span data-stu-id="1862e-127">For example, if the output value of `element1` if `"bar"`, then this example returns the string `"foobar!"`:</span></span>

```json
"[concat('foo', steps('step1').element1), '!']"
```

### <a name="substring"></a><span data-ttu-id="1862e-128">substring</span><span class="sxs-lookup"><span data-stu-id="1862e-128">substring</span></span>
<span data-ttu-id="1862e-129">Restituisce la sottostringa della stringa specificata.</span><span class="sxs-lookup"><span data-stu-id="1862e-129">Returns the substring of the specified string.</span></span> <span data-ttu-id="1862e-130">La sottostringa inizia in corrispondenza dell'indice specificato e ha la lunghezza specificata.</span><span class="sxs-lookup"><span data-stu-id="1862e-130">The substring starts at the specified index and has the specified length.</span></span>

<span data-ttu-id="1862e-131">L'esempio seguente restituisce `"ftw"`:</span><span class="sxs-lookup"><span data-stu-id="1862e-131">The following example returns `"ftw"`:</span></span>

```json
"[substring('azure-ftw!!!1one', 6, 3)]"
```

### <a name="replace"></a><span data-ttu-id="1862e-132">replace</span><span class="sxs-lookup"><span data-stu-id="1862e-132">replace</span></span>
<span data-ttu-id="1862e-133">Restituisce una stringa in cui tutte le occorrenze della stringa specificata nella stringa corrente vengono sostituite con un'altra stringa.</span><span class="sxs-lookup"><span data-stu-id="1862e-133">Returns a string in which all occurrences of the specified string in the current string are replaced with another string.</span></span>

<span data-ttu-id="1862e-134">L'esempio seguente restituisce `"Everything is awesome!"`:</span><span class="sxs-lookup"><span data-stu-id="1862e-134">The following example returns `"Everything is awesome!"`:</span></span>

```json
"[replace('Everything is terrible!', 'terrible', 'awesome')]"
```

### <a name="guid"></a><span data-ttu-id="1862e-135">guid</span><span class="sxs-lookup"><span data-stu-id="1862e-135">guid</span></span>
<span data-ttu-id="1862e-136">Genera una stringa univoca globale (GUID).</span><span class="sxs-lookup"><span data-stu-id="1862e-136">Generates a globally unique string (GUID).</span></span>

<span data-ttu-id="1862e-137">L'esempio seguente può restituire `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:</span><span class="sxs-lookup"><span data-stu-id="1862e-137">The following example could return `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:</span></span>

```json
"[guid()]"
```

### <a name="tolower"></a><span data-ttu-id="1862e-138">toLower</span><span class="sxs-lookup"><span data-stu-id="1862e-138">toLower</span></span>
<span data-ttu-id="1862e-139">Restituisce una stringa convertita in lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="1862e-139">Returns a string converted to lowercase.</span></span>

<span data-ttu-id="1862e-140">L'esempio seguente restituisce `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="1862e-140">The following example returns `"foobar"`:</span></span>

```json
"[toLower('FOOBAR')]"
```

### <a name="toupper"></a><span data-ttu-id="1862e-141">toUpper</span><span class="sxs-lookup"><span data-stu-id="1862e-141">toUpper</span></span>
<span data-ttu-id="1862e-142">Restituisce una stringa convertita in lettere maiuscole.</span><span class="sxs-lookup"><span data-stu-id="1862e-142">Returns a string converted to uppercase.</span></span>

<span data-ttu-id="1862e-143">L'esempio seguente restituisce `"FOOBAR"`:</span><span class="sxs-lookup"><span data-stu-id="1862e-143">The following example returns `"FOOBAR"`:</span></span>

```json
"[toUpper('foobar')]"
```

## <a name="collection-functions"></a><span data-ttu-id="1862e-144">Funzioni di raccolta</span><span class="sxs-lookup"><span data-stu-id="1862e-144">Collection functions</span></span>
<span data-ttu-id="1862e-145">Queste funzioni possono essere usate con le raccolte, ad esempio stringhe, matrici e oggetti JSON.</span><span class="sxs-lookup"><span data-stu-id="1862e-145">These functions can be used with collections, like JSON strings, arrays and objects.</span></span>

### <a name="contains"></a><span data-ttu-id="1862e-146">contains</span><span class="sxs-lookup"><span data-stu-id="1862e-146">contains</span></span>
<span data-ttu-id="1862e-147">Restituisce `true` se una stringa contiene la sottostringa specificata, una matrice contiene il valore specificato o un oggetto contiene la chiave specificata.</span><span class="sxs-lookup"><span data-stu-id="1862e-147">Returns `true` if a string contains the specified substring, an array contains the specified value, or an object contains the specified key.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="1862e-148">Esempio 1: stringa</span><span class="sxs-lookup"><span data-stu-id="1862e-148">Example 1: string</span></span>
<span data-ttu-id="1862e-149">L'esempio seguente restituisce `true`:</span><span class="sxs-lookup"><span data-stu-id="1862e-149">The following example returns `true`:</span></span>

```json
"[contains('foobar', 'foo')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="1862e-150">Esempio 2: matrice</span><span class="sxs-lookup"><span data-stu-id="1862e-150">Example 2: array</span></span>
<span data-ttu-id="1862e-151">Si supponga che `element1` restituisca `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="1862e-151">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="1862e-152">L'esempio seguente restituisce `false`:</span><span class="sxs-lookup"><span data-stu-id="1862e-152">The following example returns `false`:</span></span>

```json
"[contains(steps('foo').element1, 4)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="1862e-153">Esempio 3: oggetto</span><span class="sxs-lookup"><span data-stu-id="1862e-153">Example 3: object</span></span>
<span data-ttu-id="1862e-154">Si supponga che `element1` restituisca:</span><span class="sxs-lookup"><span data-stu-id="1862e-154">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="1862e-155">L'esempio seguente restituisce `true`:</span><span class="sxs-lookup"><span data-stu-id="1862e-155">The following example returns `true`:</span></span>

```json
"[contains(steps('foo').element1, 'key1')]"
```

### <a name="length"></a><span data-ttu-id="1862e-156">length</span><span class="sxs-lookup"><span data-stu-id="1862e-156">length</span></span>
<span data-ttu-id="1862e-157">Restituisce il numero di caratteri in una stringa, il numero di valori in una matrice o il numero di chiavi in un oggetto.</span><span class="sxs-lookup"><span data-stu-id="1862e-157">Returns the number of characters in a string, the number of values in an array, or the number of keys in an object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="1862e-158">Esempio 1: stringa</span><span class="sxs-lookup"><span data-stu-id="1862e-158">Example 1: string</span></span>
<span data-ttu-id="1862e-159">L'esempio seguente restituisce `6`:</span><span class="sxs-lookup"><span data-stu-id="1862e-159">The following example returns `6`:</span></span>

```json
"[length('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="1862e-160">Esempio 2: matrice</span><span class="sxs-lookup"><span data-stu-id="1862e-160">Example 2: array</span></span>
<span data-ttu-id="1862e-161">Si supponga che `element1` restituisca `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="1862e-161">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="1862e-162">L'esempio seguente restituisce `3`:</span><span class="sxs-lookup"><span data-stu-id="1862e-162">The following example returns `3`:</span></span>

```json
"[length(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="1862e-163">Esempio 3: oggetto</span><span class="sxs-lookup"><span data-stu-id="1862e-163">Example 3: object</span></span>
<span data-ttu-id="1862e-164">Si supponga che `element1` restituisca:</span><span class="sxs-lookup"><span data-stu-id="1862e-164">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="1862e-165">L'esempio seguente restituisce `2`:</span><span class="sxs-lookup"><span data-stu-id="1862e-165">The following example returns `2`:</span></span>

```json
"[length(steps('foo').element1)]"
```

### <a name="empty"></a><span data-ttu-id="1862e-166">empty</span><span class="sxs-lookup"><span data-stu-id="1862e-166">empty</span></span>
<span data-ttu-id="1862e-167">Restituisce `true` se la stringa, la matrice o l'oggetto sono Null o vuoti.</span><span class="sxs-lookup"><span data-stu-id="1862e-167">Returns `true` if the string, array, or object is null or empty.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="1862e-168">Esempio 1: stringa</span><span class="sxs-lookup"><span data-stu-id="1862e-168">Example 1: string</span></span>
<span data-ttu-id="1862e-169">L'esempio seguente restituisce `true`:</span><span class="sxs-lookup"><span data-stu-id="1862e-169">The following example returns `true`:</span></span>

```json
"[empty('')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="1862e-170">Esempio 2: matrice</span><span class="sxs-lookup"><span data-stu-id="1862e-170">Example 2: array</span></span>
<span data-ttu-id="1862e-171">Si supponga che `element1` restituisca `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="1862e-171">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="1862e-172">L'esempio seguente restituisce `false`:</span><span class="sxs-lookup"><span data-stu-id="1862e-172">The following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="1862e-173">Esempio 3: oggetto</span><span class="sxs-lookup"><span data-stu-id="1862e-173">Example 3: object</span></span>
<span data-ttu-id="1862e-174">Si supponga che `element1` restituisca:</span><span class="sxs-lookup"><span data-stu-id="1862e-174">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="1862e-175">L'esempio seguente restituisce `false`:</span><span class="sxs-lookup"><span data-stu-id="1862e-175">The following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-4-null-and-undefined"></a><span data-ttu-id="1862e-176">Esempio 4: Null e non definito</span><span class="sxs-lookup"><span data-stu-id="1862e-176">Example 4: null and undefined</span></span>
<span data-ttu-id="1862e-177">Si supponga che `element1` sia `null` o non definito.</span><span class="sxs-lookup"><span data-stu-id="1862e-177">Assume `element1` is `null` or undefined.</span></span> <span data-ttu-id="1862e-178">L'esempio seguente restituisce `true`:</span><span class="sxs-lookup"><span data-stu-id="1862e-178">The following example returns `true`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

### <a name="first"></a><span data-ttu-id="1862e-179">first</span><span class="sxs-lookup"><span data-stu-id="1862e-179">first</span></span>
<span data-ttu-id="1862e-180">Restituisce il primo carattere della stringa specificata, il primo valore della matrice specificata o la prima chiave e il primo valore dell'oggetto specificato.</span><span class="sxs-lookup"><span data-stu-id="1862e-180">Returns the first character of the specified string; first value of the specified array; or the first key and value of the specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="1862e-181">Esempio 1: stringa</span><span class="sxs-lookup"><span data-stu-id="1862e-181">Example 1: string</span></span>
<span data-ttu-id="1862e-182">L'esempio seguente restituisce `"f"`:</span><span class="sxs-lookup"><span data-stu-id="1862e-182">The following example returns `"f"`:</span></span>

```json
"[first('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="1862e-183">Esempio 2: matrice</span><span class="sxs-lookup"><span data-stu-id="1862e-183">Example 2: array</span></span>
<span data-ttu-id="1862e-184">Si supponga che `element1` restituisca `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="1862e-184">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="1862e-185">L'esempio seguente restituisce `1`:</span><span class="sxs-lookup"><span data-stu-id="1862e-185">The following example returns `1`:</span></span>

```json
"[first(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="1862e-186">Esempio 3: oggetto</span><span class="sxs-lookup"><span data-stu-id="1862e-186">Example 3: object</span></span>
<span data-ttu-id="1862e-187">Si supponga che `element1` restituisca:</span><span class="sxs-lookup"><span data-stu-id="1862e-187">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="1862e-188">L'esempio seguente restituisce `{"key1": "foobar"}`:</span><span class="sxs-lookup"><span data-stu-id="1862e-188">The following example returns `{"key1": "foobar"}`:</span></span>

```json
"[first(steps('foo').element1)]"
```

### <a name="last"></a><span data-ttu-id="1862e-189">last</span><span class="sxs-lookup"><span data-stu-id="1862e-189">last</span></span>
<span data-ttu-id="1862e-190">Restituisce l'ultimo carattere della stringa specificata, l'ultimo valore della matrice specificata o l'ultima chiave e l'ultimo valore dell'oggetto specificato.</span><span class="sxs-lookup"><span data-stu-id="1862e-190">Returns the last character of the specified string, the last value of the specified array, or the last key and value of the specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="1862e-191">Esempio 1: stringa</span><span class="sxs-lookup"><span data-stu-id="1862e-191">Example 1: string</span></span>
<span data-ttu-id="1862e-192">L'esempio seguente restituisce `"r"`:</span><span class="sxs-lookup"><span data-stu-id="1862e-192">The following example returns `"r"`:</span></span>

```json
"[last('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="1862e-193">Esempio 2: matrice</span><span class="sxs-lookup"><span data-stu-id="1862e-193">Example 2: array</span></span>
<span data-ttu-id="1862e-194">Si supponga che `element1` restituisca `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="1862e-194">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="1862e-195">L'esempio seguente restituisce `2`:</span><span class="sxs-lookup"><span data-stu-id="1862e-195">The following example returns `2`:</span></span>

```json
"[last(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="1862e-196">Esempio 3: oggetto</span><span class="sxs-lookup"><span data-stu-id="1862e-196">Example 3: object</span></span>
<span data-ttu-id="1862e-197">Si supponga che `element1` restituisca:</span><span class="sxs-lookup"><span data-stu-id="1862e-197">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="1862e-198">L'esempio seguente restituisce `{"key2": "raboof"}`:</span><span class="sxs-lookup"><span data-stu-id="1862e-198">The following example returns `{"key2": "raboof"}`:</span></span>

```json
"[last(steps('foo').element1)]"
```

### <a name="take"></a><span data-ttu-id="1862e-199">take</span><span class="sxs-lookup"><span data-stu-id="1862e-199">take</span></span>
<span data-ttu-id="1862e-200">Restituisce un numero specificato di caratteri contigui dall'inizio della stringa, un numero specificato di valori contigui dall'inizio della matrice o un numero di chiavi e valori contigui dall'inizio dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="1862e-200">Returns a specified number of contiguous characters from the start of the string, a specified number of contiguous values from the start of the array, or a specified number of contiguous keys and values from the start of the object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="1862e-201">Esempio 1: stringa</span><span class="sxs-lookup"><span data-stu-id="1862e-201">Example 1: string</span></span>
<span data-ttu-id="1862e-202">L'esempio seguente restituisce `"foo"`:</span><span class="sxs-lookup"><span data-stu-id="1862e-202">The following example returns `"foo"`:</span></span>

```json
"[take('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="1862e-203">Esempio 2: matrice</span><span class="sxs-lookup"><span data-stu-id="1862e-203">Example 2: array</span></span>
<span data-ttu-id="1862e-204">Si supponga che `element1` restituisca `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="1862e-204">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="1862e-205">L'esempio seguente restituisce `[1, 2]`:</span><span class="sxs-lookup"><span data-stu-id="1862e-205">The following example returns `[1, 2]`:</span></span>

```json
"[take(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="1862e-206">Esempio 3: oggetto</span><span class="sxs-lookup"><span data-stu-id="1862e-206">Example 3: object</span></span>
<span data-ttu-id="1862e-207">Si supponga che `element1` restituisca:</span><span class="sxs-lookup"><span data-stu-id="1862e-207">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="1862e-208">L'esempio seguente restituisce `{"key1": "foobar"}`:</span><span class="sxs-lookup"><span data-stu-id="1862e-208">The following example returns `{"key1": "foobar"}`:</span></span>

```json
"[take(steps('foo').element1, 1)]"
```

### <a name="skip"></a><span data-ttu-id="1862e-209">skip</span><span class="sxs-lookup"><span data-stu-id="1862e-209">skip</span></span>
<span data-ttu-id="1862e-210">Ignora un numero specificato di elementi in una raccolta e quindi restituisce gli elementi rimanenti.</span><span class="sxs-lookup"><span data-stu-id="1862e-210">Bypasses a specified number of elements in a collection, and then returns the remaining elements.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="1862e-211">Esempio 1: stringa</span><span class="sxs-lookup"><span data-stu-id="1862e-211">Example 1: string</span></span>
<span data-ttu-id="1862e-212">L'esempio seguente restituisce `"bar"`:</span><span class="sxs-lookup"><span data-stu-id="1862e-212">The following example returns `"bar"`:</span></span>

```json
"[skip('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="1862e-213">Esempio 2: matrice</span><span class="sxs-lookup"><span data-stu-id="1862e-213">Example 2: array</span></span>
<span data-ttu-id="1862e-214">Si supponga che `element1` restituisca `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="1862e-214">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="1862e-215">L'esempio seguente restituisce `[3]`:</span><span class="sxs-lookup"><span data-stu-id="1862e-215">The following example returns `[3]`:</span></span>

```json
"[skip(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="1862e-216">Esempio 3: oggetto</span><span class="sxs-lookup"><span data-stu-id="1862e-216">Example 3: object</span></span>
<span data-ttu-id="1862e-217">Si supponga che `element1` restituisca:</span><span class="sxs-lookup"><span data-stu-id="1862e-217">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="1862e-218">L'esempio seguente restituisce `{"key2": "raboof"}`:</span><span class="sxs-lookup"><span data-stu-id="1862e-218">The following example returns `{"key2": "raboof"}`:</span></span>

```json
"[skip(steps('foo').element1, 1)]"
```

## <a name="logical-functions"></a><span data-ttu-id="1862e-219">Funzioni logiche</span><span class="sxs-lookup"><span data-stu-id="1862e-219">Logical functions</span></span>
<span data-ttu-id="1862e-220">Queste funzioni possono essere usate nelle istruzioni condizionali.</span><span class="sxs-lookup"><span data-stu-id="1862e-220">These functions can be used in conditionals.</span></span> <span data-ttu-id="1862e-221">Alcune funzioni potrebbero non supportare tutti i tipi di dati JSON.</span><span class="sxs-lookup"><span data-stu-id="1862e-221">Some functions may not support all JSON data types.</span></span>

### <a name="equals"></a><span data-ttu-id="1862e-222">equals</span><span class="sxs-lookup"><span data-stu-id="1862e-222">equals</span></span>
<span data-ttu-id="1862e-223">Restituisce `true` se entrambi i parametri hanno lo stesso tipo e valore.</span><span class="sxs-lookup"><span data-stu-id="1862e-223">Returns `true` if both parameters have the same type and value.</span></span> <span data-ttu-id="1862e-224">Questa funzione supporta tutti i tipi di dati JSON.</span><span class="sxs-lookup"><span data-stu-id="1862e-224">This function supports all JSON data types.</span></span>

<span data-ttu-id="1862e-225">L'esempio seguente restituisce `true`:</span><span class="sxs-lookup"><span data-stu-id="1862e-225">The following example returns `true`:</span></span>

```json
"[equals(0, 0)]"
```

<span data-ttu-id="1862e-226">L'esempio seguente restituisce `true`:</span><span class="sxs-lookup"><span data-stu-id="1862e-226">The following example returns `true`:</span></span>

```json
"[equals('foo', 'foo')]"
```

<span data-ttu-id="1862e-227">L'esempio seguente restituisce `false`:</span><span class="sxs-lookup"><span data-stu-id="1862e-227">The following example returns `false`:</span></span>

```json
"[equals('abc', ['a', 'b', 'c'])]"
```

### <a name="less"></a><span data-ttu-id="1862e-228">less</span><span class="sxs-lookup"><span data-stu-id="1862e-228">less</span></span>
<span data-ttu-id="1862e-229">Restituisce `true` se il primo parametro è necessariamente minore del secondo parametro.</span><span class="sxs-lookup"><span data-stu-id="1862e-229">Returns `true` if the first parameter is strictly less than the second parameter.</span></span> <span data-ttu-id="1862e-230">Questa funzione supporta solo parametri di tipo numero e stringa.</span><span class="sxs-lookup"><span data-stu-id="1862e-230">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="1862e-231">L'esempio seguente restituisce `true`:</span><span class="sxs-lookup"><span data-stu-id="1862e-231">The following example returns `true`:</span></span>

```json
"[less(1, 2)]"
```

<span data-ttu-id="1862e-232">L'esempio seguente restituisce `false`:</span><span class="sxs-lookup"><span data-stu-id="1862e-232">The following example returns `false`:</span></span>

```json
"[less('9', '10')]"
```

### <a name="lessorequals"></a><span data-ttu-id="1862e-233">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="1862e-233">lessOrEquals</span></span>
<span data-ttu-id="1862e-234">Restituisce `true` se il primo parametro è minore o uguale al secondo parametro.</span><span class="sxs-lookup"><span data-stu-id="1862e-234">Returns `true` if the first parameter is less than or equal to the second parameter.</span></span> <span data-ttu-id="1862e-235">Questa funzione supporta solo parametri di tipo numero e stringa.</span><span class="sxs-lookup"><span data-stu-id="1862e-235">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="1862e-236">L'esempio seguente restituisce `true`:</span><span class="sxs-lookup"><span data-stu-id="1862e-236">The following example returns `true`:</span></span>

```json
"[lessOrEquals(2, 2)]"
```

### <a name="greater"></a><span data-ttu-id="1862e-237">greater</span><span class="sxs-lookup"><span data-stu-id="1862e-237">greater</span></span>
<span data-ttu-id="1862e-238">Restituisce `true` se il primo parametro è necessariamente maggiore del secondo parametro.</span><span class="sxs-lookup"><span data-stu-id="1862e-238">Returns `true` if the first parameter is strictly greater than the second parameter.</span></span> <span data-ttu-id="1862e-239">Questa funzione supporta solo parametri di tipo numero e stringa.</span><span class="sxs-lookup"><span data-stu-id="1862e-239">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="1862e-240">L'esempio seguente restituisce `false`:</span><span class="sxs-lookup"><span data-stu-id="1862e-240">The following example returns `false`:</span></span>

```json
"[greater(1, 2)]"
```

<span data-ttu-id="1862e-241">L'esempio seguente restituisce `true`:</span><span class="sxs-lookup"><span data-stu-id="1862e-241">The following example returns `true`:</span></span>

```json
"[greater('9', '10')]"
```

### <a name="greaterorequals"></a><span data-ttu-id="1862e-242">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="1862e-242">greaterOrEquals</span></span>
<span data-ttu-id="1862e-243">Restituisce `true` se il primo parametro è maggiore o uguale al secondo parametro.</span><span class="sxs-lookup"><span data-stu-id="1862e-243">Returns `true` if the first parameter is greater than or equal to the second parameter.</span></span> <span data-ttu-id="1862e-244">Questa funzione supporta solo parametri di tipo numero e stringa.</span><span class="sxs-lookup"><span data-stu-id="1862e-244">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="1862e-245">L'esempio seguente restituisce `true`:</span><span class="sxs-lookup"><span data-stu-id="1862e-245">The following example returns `true`:</span></span>

```json
"[greaterOrEquals(2, 2)]"
```

### <a name="and"></a><span data-ttu-id="1862e-246">e</span><span class="sxs-lookup"><span data-stu-id="1862e-246">and</span></span>
<span data-ttu-id="1862e-247">Restituisce `true` se tutti i parametri restituiscono `true`.</span><span class="sxs-lookup"><span data-stu-id="1862e-247">Returns `true` if all the parameters evaluate to `true`.</span></span> <span data-ttu-id="1862e-248">Questa funzione supporta solo due o più parametri di tipo booleano.</span><span class="sxs-lookup"><span data-stu-id="1862e-248">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="1862e-249">L'esempio seguente restituisce `true`:</span><span class="sxs-lookup"><span data-stu-id="1862e-249">The following example returns `true`:</span></span>

```json
"[and(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="1862e-250">L'esempio seguente restituisce `false`:</span><span class="sxs-lookup"><span data-stu-id="1862e-250">The following example returns `false`:</span></span>

```json
"[and(equals(0, 0), greater(1, 2))]"
```

### <a name="or"></a><span data-ttu-id="1862e-251">oppure</span><span class="sxs-lookup"><span data-stu-id="1862e-251">or</span></span>
<span data-ttu-id="1862e-252">Restituisce `true` se almeno uno dei parametri restituisce `true`.</span><span class="sxs-lookup"><span data-stu-id="1862e-252">Returns `true` if at least one of the parameters evaluates to `true`.</span></span> <span data-ttu-id="1862e-253">Questa funzione supporta solo due o più parametri di tipo booleano.</span><span class="sxs-lookup"><span data-stu-id="1862e-253">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="1862e-254">L'esempio seguente restituisce `true`:</span><span class="sxs-lookup"><span data-stu-id="1862e-254">The following example returns `true`:</span></span>

```json
"[or(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="1862e-255">L'esempio seguente restituisce `true`:</span><span class="sxs-lookup"><span data-stu-id="1862e-255">The following example returns `true`:</span></span>

```json
"[or(equals(0, 0), greater(1, 2))]"
```

### <a name="not"></a><span data-ttu-id="1862e-256">not</span><span class="sxs-lookup"><span data-stu-id="1862e-256">not</span></span>
<span data-ttu-id="1862e-257">Restituisce `true` se il parametro restituisce `false`.</span><span class="sxs-lookup"><span data-stu-id="1862e-257">Returns `true` if the parameter evaluates to `false`.</span></span> <span data-ttu-id="1862e-258">Questa funzione supporta solo parametri di tipo booleano.</span><span class="sxs-lookup"><span data-stu-id="1862e-258">This function supports parameters only of type Boolean.</span></span>

<span data-ttu-id="1862e-259">L'esempio seguente restituisce `true`:</span><span class="sxs-lookup"><span data-stu-id="1862e-259">The following example returns `true`:</span></span>

```json
"[not(false)]"
```

<span data-ttu-id="1862e-260">L'esempio seguente restituisce `false`:</span><span class="sxs-lookup"><span data-stu-id="1862e-260">The following example returns `false`:</span></span>

```json
"[not(equals(0, 0))]"
```

### <a name="coalesce"></a><span data-ttu-id="1862e-261">coalesce</span><span class="sxs-lookup"><span data-stu-id="1862e-261">coalesce</span></span>
<span data-ttu-id="1862e-262">Restituisce il valore del primo parametro non Null.</span><span class="sxs-lookup"><span data-stu-id="1862e-262">Returns the value of the first non-null parameter.</span></span> <span data-ttu-id="1862e-263">Questa funzione supporta tutti i tipi di dati JSON.</span><span class="sxs-lookup"><span data-stu-id="1862e-263">This function supports all JSON data types.</span></span>

<span data-ttu-id="1862e-264">Si supponga che `element1` e `element2` non siano definiti.</span><span class="sxs-lookup"><span data-stu-id="1862e-264">Assume `element1` and `element2` are undefined.</span></span> <span data-ttu-id="1862e-265">L'esempio seguente restituisce `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="1862e-265">The following example returns `"foobar"`:</span></span>

```json
"[coalesce(steps('foo').element1, steps('foo').element2, 'foobar')]"
```

## <a name="conversion-functions"></a><span data-ttu-id="1862e-266">Funzioni di conversione</span><span class="sxs-lookup"><span data-stu-id="1862e-266">Conversion functions</span></span>
<span data-ttu-id="1862e-267">Queste funzioni possono essere usate per convertire i valori tra codifiche e tipi di dati JSON.</span><span class="sxs-lookup"><span data-stu-id="1862e-267">These functions can be used to convert values between JSON data types and encodings.</span></span>

### <a name="int"></a><span data-ttu-id="1862e-268">int</span><span class="sxs-lookup"><span data-stu-id="1862e-268">int</span></span>
<span data-ttu-id="1862e-269">Converte il parametro in un valore intero.</span><span class="sxs-lookup"><span data-stu-id="1862e-269">Converts the parameter to an integer.</span></span> <span data-ttu-id="1862e-270">Questa funzione supporta parametri di tipo numero e stringa.</span><span class="sxs-lookup"><span data-stu-id="1862e-270">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="1862e-271">L'esempio seguente restituisce `1`:</span><span class="sxs-lookup"><span data-stu-id="1862e-271">The following example returns `1`:</span></span>

```json
"[int('1')]"
```

<span data-ttu-id="1862e-272">L'esempio seguente restituisce `2`:</span><span class="sxs-lookup"><span data-stu-id="1862e-272">The following example returns `2`:</span></span>

```json
"[int(2.9)]"
```

### <a name="float"></a><span data-ttu-id="1862e-273">float</span><span class="sxs-lookup"><span data-stu-id="1862e-273">float</span></span>
<span data-ttu-id="1862e-274">Converte il parametro in un valore a virgola mobile.</span><span class="sxs-lookup"><span data-stu-id="1862e-274">Converts the parameter to a floating-point.</span></span> <span data-ttu-id="1862e-275">Questa funzione supporta parametri di tipo numero e stringa.</span><span class="sxs-lookup"><span data-stu-id="1862e-275">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="1862e-276">L'esempio seguente restituisce `1.0`:</span><span class="sxs-lookup"><span data-stu-id="1862e-276">The following example returns `1.0`:</span></span>

```json
"[float('1.0')]"
```

<span data-ttu-id="1862e-277">L'esempio seguente restituisce `2.9`:</span><span class="sxs-lookup"><span data-stu-id="1862e-277">The following example returns `2.9`:</span></span>

```json
"[float(2.9)]"
```

### <a name="string"></a><span data-ttu-id="1862e-278">string</span><span class="sxs-lookup"><span data-stu-id="1862e-278">string</span></span>
<span data-ttu-id="1862e-279">Converte il parametro in una stringa.</span><span class="sxs-lookup"><span data-stu-id="1862e-279">Converts the parameter to a string.</span></span> <span data-ttu-id="1862e-280">Questa funzione supporta parametri di tutti i tipi di dati JSON.</span><span class="sxs-lookup"><span data-stu-id="1862e-280">This function supports parameters of all JSON data types.</span></span>

<span data-ttu-id="1862e-281">L'esempio seguente restituisce `"1"`:</span><span class="sxs-lookup"><span data-stu-id="1862e-281">The following example returns `"1"`:</span></span>

```json
"[string(1)]"
```

<span data-ttu-id="1862e-282">L'esempio seguente restituisce `"2.9"`:</span><span class="sxs-lookup"><span data-stu-id="1862e-282">The following example returns `"2.9"`:</span></span>

```json
"[string(2.9)]"
```

<span data-ttu-id="1862e-283">L'esempio seguente restituisce `"[1,2,3]"`:</span><span class="sxs-lookup"><span data-stu-id="1862e-283">The following example returns `"[1,2,3]"`:</span></span>

```json
"[string([1,2,3])]"
```

<span data-ttu-id="1862e-284">L'esempio seguente restituisce `"{"foo":"bar"}"`:</span><span class="sxs-lookup"><span data-stu-id="1862e-284">The following example returns `"{"foo":"bar"}"`:</span></span>

```json
"[string({\"foo\":\"bar\"})]"
```

### <a name="bool"></a><span data-ttu-id="1862e-285">bool</span><span class="sxs-lookup"><span data-stu-id="1862e-285">bool</span></span>
<span data-ttu-id="1862e-286">Converte il parametro in un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="1862e-286">Converts the parameter to a Boolean.</span></span> <span data-ttu-id="1862e-287">Questa funzione supporta parametri di tipo numero, stringa e booleano.</span><span class="sxs-lookup"><span data-stu-id="1862e-287">This function supports parameters of type number, string, and Boolean.</span></span> <span data-ttu-id="1862e-288">Analogamente ai valori booleani in JavaScript, qualsiasi valore eccetto `0` o `'false'` restituisce `true`.</span><span class="sxs-lookup"><span data-stu-id="1862e-288">Similar to Booleans in JavaScript, any value except `0` or `'false'` returns `true`.</span></span>

<span data-ttu-id="1862e-289">L'esempio seguente restituisce `true`:</span><span class="sxs-lookup"><span data-stu-id="1862e-289">The following example returns `true`:</span></span>

```json
"[bool(1)]"
```

<span data-ttu-id="1862e-290">L'esempio seguente restituisce `false`:</span><span class="sxs-lookup"><span data-stu-id="1862e-290">The following example returns `false`:</span></span>

```json
"[bool(0)]"
```

<span data-ttu-id="1862e-291">L'esempio seguente restituisce `true`:</span><span class="sxs-lookup"><span data-stu-id="1862e-291">The following example returns `true`:</span></span>

```json
"[bool(true)]"
```

<span data-ttu-id="1862e-292">L'esempio seguente restituisce `true`:</span><span class="sxs-lookup"><span data-stu-id="1862e-292">The following example returns `true`:</span></span>

```json
"[bool('true')]"
```

### <a name="parse"></a><span data-ttu-id="1862e-293">parse</span><span class="sxs-lookup"><span data-stu-id="1862e-293">parse</span></span>
<span data-ttu-id="1862e-294">Converte il parametro in un tipo nativo.</span><span class="sxs-lookup"><span data-stu-id="1862e-294">Converts the parameter to a native type.</span></span> <span data-ttu-id="1862e-295">In altre parole, questa funzione è l'inverso di `string()`.</span><span class="sxs-lookup"><span data-stu-id="1862e-295">In other words, this function is the inverse of `string()`.</span></span> <span data-ttu-id="1862e-296">Questa funzione supporta solo parametri di tipo stringa.</span><span class="sxs-lookup"><span data-stu-id="1862e-296">This function supports parameters only of type string.</span></span>

<span data-ttu-id="1862e-297">L'esempio seguente restituisce `1`:</span><span class="sxs-lookup"><span data-stu-id="1862e-297">The following example returns `1`:</span></span>

```json
"[parse('1')]"
```

<span data-ttu-id="1862e-298">L'esempio seguente restituisce `true`:</span><span class="sxs-lookup"><span data-stu-id="1862e-298">The following example returns `true`:</span></span>

```json
"[parse('true')]"
```

<span data-ttu-id="1862e-299">L'esempio seguente restituisce `[1,2,3]`:</span><span class="sxs-lookup"><span data-stu-id="1862e-299">The following example returns `[1,2,3]`:</span></span>

```json
"[parse('[1,2,3]')]"
```

<span data-ttu-id="1862e-300">L'esempio seguente restituisce `{"foo":"bar"}`:</span><span class="sxs-lookup"><span data-stu-id="1862e-300">The following example returns `{"foo":"bar"}`:</span></span>

```json
"[parse('{\"foo\":\"bar\"}')]"
```

### <a name="encodebase64"></a><span data-ttu-id="1862e-301">encodeBase64</span><span class="sxs-lookup"><span data-stu-id="1862e-301">encodeBase64</span></span>
<span data-ttu-id="1862e-302">Codifica il parametro in una stringa Base 64.</span><span class="sxs-lookup"><span data-stu-id="1862e-302">Encodes the parameter to a base-64 encoded string.</span></span> <span data-ttu-id="1862e-303">Questa funzione supporta solo parametri di tipo stringa.</span><span class="sxs-lookup"><span data-stu-id="1862e-303">This function supports parameters only of type string.</span></span>

<span data-ttu-id="1862e-304">L'esempio seguente restituisce `"Zm9vYmFy"`:</span><span class="sxs-lookup"><span data-stu-id="1862e-304">The following example returns `"Zm9vYmFy"`:</span></span>

```json
"[encodeBase64('foobar')]"
```

### <a name="decodebase64"></a><span data-ttu-id="1862e-305">decodeBase64</span><span class="sxs-lookup"><span data-stu-id="1862e-305">decodeBase64</span></span>
<span data-ttu-id="1862e-306">Decodifica il parametro da una stringa Base 64.</span><span class="sxs-lookup"><span data-stu-id="1862e-306">Decodes the parameter from a base-64 encoded string.</span></span> <span data-ttu-id="1862e-307">Questa funzione supporta solo parametri di tipo stringa.</span><span class="sxs-lookup"><span data-stu-id="1862e-307">This function supports parameters only of type string.</span></span>

<span data-ttu-id="1862e-308">L'esempio seguente restituisce `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="1862e-308">The following example returns `"foobar"`:</span></span>

```json
"[decodeBase64('Zm9vYmFy')]"
```

### <a name="encodeuricomponent"></a><span data-ttu-id="1862e-309">encodeUriComponent</span><span class="sxs-lookup"><span data-stu-id="1862e-309">encodeUriComponent</span></span>
<span data-ttu-id="1862e-310">Codifica il parametro in una stringa con codifica URL.</span><span class="sxs-lookup"><span data-stu-id="1862e-310">Encodes the parameter to a URL encoded string.</span></span> <span data-ttu-id="1862e-311">Questa funzione supporta solo parametri di tipo stringa.</span><span class="sxs-lookup"><span data-stu-id="1862e-311">This function supports parameters only of type string.</span></span>

<span data-ttu-id="1862e-312">L'esempio seguente restituisce `"https%3A%2F%2Fportal.azure.com%2F"`:</span><span class="sxs-lookup"><span data-stu-id="1862e-312">The following example returns `"https%3A%2F%2Fportal.azure.com%2F"`:</span></span>

```json
"[encodeUriComponent('https://portal.azure.com/')]"
```

### <a name="decodeuricomponent"></a><span data-ttu-id="1862e-313">decodeUriComponent</span><span class="sxs-lookup"><span data-stu-id="1862e-313">decodeUriComponent</span></span>
<span data-ttu-id="1862e-314">Decodifica il parametro da una stringa con codifica URL.</span><span class="sxs-lookup"><span data-stu-id="1862e-314">Decodes the parameter from a URL encoded string.</span></span> <span data-ttu-id="1862e-315">Questa funzione supporta solo parametri di tipo stringa.</span><span class="sxs-lookup"><span data-stu-id="1862e-315">This function supports parameters only of type string.</span></span>

<span data-ttu-id="1862e-316">L'esempio seguente restituisce `"https://portal.azure.com/"`:</span><span class="sxs-lookup"><span data-stu-id="1862e-316">The following example returns `"https://portal.azure.com/"`:</span></span>

```json
"[decodeUriComponent('https%3A%2F%2Fportal.azure.com%2F')]"
```

## <a name="math-functions"></a><span data-ttu-id="1862e-317">Funzioni matematiche</span><span class="sxs-lookup"><span data-stu-id="1862e-317">Math functions</span></span>
### <a name="add"></a><span data-ttu-id="1862e-318">add</span><span class="sxs-lookup"><span data-stu-id="1862e-318">add</span></span>
<span data-ttu-id="1862e-319">Somma due numeri e restituisce il risultato.</span><span class="sxs-lookup"><span data-stu-id="1862e-319">Adds two numbers, and returns the result.</span></span>

<span data-ttu-id="1862e-320">L'esempio seguente restituisce `3`:</span><span class="sxs-lookup"><span data-stu-id="1862e-320">The following example returns `3`:</span></span>

```json
"[add(1, 2)]"
```

### <a name="sub"></a><span data-ttu-id="1862e-321">sub</span><span class="sxs-lookup"><span data-stu-id="1862e-321">sub</span></span>
<span data-ttu-id="1862e-322">Sottrae il secondo numero dal primo e restituisce il risultato.</span><span class="sxs-lookup"><span data-stu-id="1862e-322">Subtracts the second number from the first number, and returns the result.</span></span>

<span data-ttu-id="1862e-323">L'esempio seguente restituisce `1`:</span><span class="sxs-lookup"><span data-stu-id="1862e-323">The following example returns `1`:</span></span>

```json
"[sub(3, 2)]"
```

### <a name="mul"></a><span data-ttu-id="1862e-324">mul</span><span class="sxs-lookup"><span data-stu-id="1862e-324">mul</span></span>
<span data-ttu-id="1862e-325">Moltiplica due numeri e restituisce il risultato.</span><span class="sxs-lookup"><span data-stu-id="1862e-325">Multiplies two numbers, and returns the result.</span></span>

<span data-ttu-id="1862e-326">L'esempio seguente restituisce `6`:</span><span class="sxs-lookup"><span data-stu-id="1862e-326">The following example returns `6`:</span></span>

```json
"[mul(2, 3)]"
```

### <a name="div"></a><span data-ttu-id="1862e-327">div</span><span class="sxs-lookup"><span data-stu-id="1862e-327">div</span></span>
<span data-ttu-id="1862e-328">Divide il primo numero per il secondo e restituisce il risultato.</span><span class="sxs-lookup"><span data-stu-id="1862e-328">Divides the first number by the second number, and returns the result.</span></span> <span data-ttu-id="1862e-329">Il risultato è sempre un numero intero.</span><span class="sxs-lookup"><span data-stu-id="1862e-329">The result is always an integer.</span></span>

<span data-ttu-id="1862e-330">L'esempio seguente restituisce `2`:</span><span class="sxs-lookup"><span data-stu-id="1862e-330">The following example returns `2`:</span></span>

```json
"[div(6, 3)]"
```

### <a name="mod"></a><span data-ttu-id="1862e-331">mod</span><span class="sxs-lookup"><span data-stu-id="1862e-331">mod</span></span>
<span data-ttu-id="1862e-332">Divide il primo numero per il secondo e restituisce il resto.</span><span class="sxs-lookup"><span data-stu-id="1862e-332">Divides the first number by the second number, and returns the remainder.</span></span>

<span data-ttu-id="1862e-333">L'esempio seguente restituisce `0`:</span><span class="sxs-lookup"><span data-stu-id="1862e-333">The following example returns `0`:</span></span>

```json
"[mod(6, 3)]"
```

<span data-ttu-id="1862e-334">L'esempio seguente restituisce `2`:</span><span class="sxs-lookup"><span data-stu-id="1862e-334">The following example returns `2`:</span></span>

```json
"[mod(6, 4)]"
```

### <a name="min"></a><span data-ttu-id="1862e-335">Min</span><span class="sxs-lookup"><span data-stu-id="1862e-335">min</span></span>
<span data-ttu-id="1862e-336">Restituisce il più piccolo di due numeri.</span><span class="sxs-lookup"><span data-stu-id="1862e-336">Returns the small of the two numbers.</span></span>

<span data-ttu-id="1862e-337">L'esempio seguente restituisce `1`:</span><span class="sxs-lookup"><span data-stu-id="1862e-337">The following example returns `1`:</span></span>

```json
"[min(1, 2)]"
```

### <a name="max"></a><span data-ttu-id="1862e-338">max</span><span class="sxs-lookup"><span data-stu-id="1862e-338">max</span></span>
<span data-ttu-id="1862e-339">Restituisce il più grande di due numeri.</span><span class="sxs-lookup"><span data-stu-id="1862e-339">Returns the larger of the two numbers.</span></span>

<span data-ttu-id="1862e-340">L'esempio seguente restituisce `2`:</span><span class="sxs-lookup"><span data-stu-id="1862e-340">The following example returns `2`:</span></span>

```json
"[max(1, 2)]"
```

### <a name="range"></a><span data-ttu-id="1862e-341">range</span><span class="sxs-lookup"><span data-stu-id="1862e-341">range</span></span>
<span data-ttu-id="1862e-342">Genera una sequenza di numeri integrali nell'intervallo specificato.</span><span class="sxs-lookup"><span data-stu-id="1862e-342">Generates a sequence of integral numbers within the specified range.</span></span>

<span data-ttu-id="1862e-343">L'esempio seguente restituisce `[1,2,3]`:</span><span class="sxs-lookup"><span data-stu-id="1862e-343">The following example returns `[1,2,3]`:</span></span>

```json
"[range(1, 3)]"
```

### <a name="rand"></a><span data-ttu-id="1862e-344">rand</span><span class="sxs-lookup"><span data-stu-id="1862e-344">rand</span></span>
<span data-ttu-id="1862e-345">Restituisce un numero integrale casuale nell'intervallo specificato.</span><span class="sxs-lookup"><span data-stu-id="1862e-345">Returns a random integral number within the specified range.</span></span> <span data-ttu-id="1862e-346">Questa funzione non genera numeri casuali protetti con crittografia.</span><span class="sxs-lookup"><span data-stu-id="1862e-346">This function does not generate cryptographically secure random numbers.</span></span>

<span data-ttu-id="1862e-347">L'esempio seguente può restituire `42`:</span><span class="sxs-lookup"><span data-stu-id="1862e-347">The following example could return `42`:</span></span>

```json
"[rand(-100, 100)]"
```

### <a name="floor"></a><span data-ttu-id="1862e-348">floor</span><span class="sxs-lookup"><span data-stu-id="1862e-348">floor</span></span>
<span data-ttu-id="1862e-349">Restituisce il valore intero più alto minore o uguale al numero specificato.</span><span class="sxs-lookup"><span data-stu-id="1862e-349">Returns the largest integer less than or equal to the specified number.</span></span>

<span data-ttu-id="1862e-350">L'esempio seguente restituisce `3`:</span><span class="sxs-lookup"><span data-stu-id="1862e-350">The following example returns `3`:</span></span>

```json
"[floor(3.14)]"
```

### <a name="ceil"></a><span data-ttu-id="1862e-351">ceil</span><span class="sxs-lookup"><span data-stu-id="1862e-351">ceil</span></span>
<span data-ttu-id="1862e-352">Restituisce il valore intero più alto maggiore o uguale al numero specificato.</span><span class="sxs-lookup"><span data-stu-id="1862e-352">Returns the largest integer greater than or equal to the specified number.</span></span>

<span data-ttu-id="1862e-353">L'esempio seguente restituisce `4`:</span><span class="sxs-lookup"><span data-stu-id="1862e-353">The following example returns `4`:</span></span>

```json
"[ceil(3.14)]"
```

## <a name="date-functions"></a><span data-ttu-id="1862e-354">Funzioni di data</span><span class="sxs-lookup"><span data-stu-id="1862e-354">Date functions</span></span>
### <a name="utcnow"></a><span data-ttu-id="1862e-355">utcNow</span><span class="sxs-lookup"><span data-stu-id="1862e-355">utcNow</span></span>
<span data-ttu-id="1862e-356">Restituisce una stringa in formato ISO 8601 della data e ora corrente del computer locale.</span><span class="sxs-lookup"><span data-stu-id="1862e-356">Returns a string in ISO 8601 format of the current date and time on the local computer.</span></span>

<span data-ttu-id="1862e-357">L'esempio seguente può restituire `"1990-12-31T23:59:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="1862e-357">The following example could return `"1990-12-31T23:59:59.000Z"`:</span></span>

```json
"[utcNow()]"
```

### <a name="addseconds"></a><span data-ttu-id="1862e-358">addSeconds</span><span class="sxs-lookup"><span data-stu-id="1862e-358">addSeconds</span></span>
<span data-ttu-id="1862e-359">Aggiunge un numero integrale di secondi a un timestamp specificato.</span><span class="sxs-lookup"><span data-stu-id="1862e-359">Adds an integral number of seconds to the specified timestamp.</span></span>

<span data-ttu-id="1862e-360">L'esempio seguente restituisce `"1991-01-01T00:00:00.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="1862e-360">The following example returns `"1991-01-01T00:00:00.000Z"`:</span></span>

```json
"[addSeconds('1990-12-31T23:59:60Z', 1)]"
```

### <a name="addminutes"></a><span data-ttu-id="1862e-361">addMinutes</span><span class="sxs-lookup"><span data-stu-id="1862e-361">addMinutes</span></span>
<span data-ttu-id="1862e-362">Aggiunge un numero integrale di minuti a un timestamp specificato.</span><span class="sxs-lookup"><span data-stu-id="1862e-362">Adds an integral number of minutes to the specified timestamp.</span></span>

<span data-ttu-id="1862e-363">L'esempio seguente restituisce `"1991-01-01T00:00:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="1862e-363">The following example returns `"1991-01-01T00:00:59.000Z"`:</span></span>

```json
"[addMinutes('1990-12-31T23:59:59Z', 1)]"
```

### <a name="addhours"></a><span data-ttu-id="1862e-364">addHours</span><span class="sxs-lookup"><span data-stu-id="1862e-364">addHours</span></span>
<span data-ttu-id="1862e-365">Aggiunge un numero integrale di ore a un timestamp specificato.</span><span class="sxs-lookup"><span data-stu-id="1862e-365">Adds an integral number of hours to the specified timestamp.</span></span>

<span data-ttu-id="1862e-366">L'esempio seguente restituisce `"1991-01-01T00:59:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="1862e-366">The following example returns `"1991-01-01T00:59:59.000Z"`:</span></span>

```json
"[addHours('1990-12-31T23:59:59Z', 1)]"
```

## <a name="next-steps"></a><span data-ttu-id="1862e-367">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1862e-367">Next steps</span></span>
* <span data-ttu-id="1862e-368">Per un'introduzione ad Azure Resource Manager, vedere [Panoramica di Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1862e-368">For an introduction to Azure Resource Manager, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

