---
title: aaaAzure funzioni di definizione dell'interfaccia utente di creare applicazioni gestite | Documenti Microsoft
description: Viene descritto toouse funzioni hello durante la costruzione di definizioni dell'interfaccia utente per le applicazioni gestite di Azure
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
ms.openlocfilehash: 7a311a25404ccaec8c19c3ed8cd7038f6887c013
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="createuidefinition-functions"></a><span data-ttu-id="8ffe2-103">Funzioni di CreateUiDefinition</span><span class="sxs-lookup"><span data-stu-id="8ffe2-103">CreateUiDefinition functions</span></span>
<span data-ttu-id="8ffe2-104">In questa sezione contiene firme hello per tutte le funzioni supportate di un CreateUiDefinition.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-104">This section contains hello signatures for all supported functions of a CreateUiDefinition.</span></span>

<span data-ttu-id="8ffe2-105">toouse una funzione, dichiarazione di hello racchiudere tra parentesi quadre.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-105">toouse a function, surround hello declaration with square brackets.</span></span> <span data-ttu-id="8ffe2-106">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-106">For example:</span></span>

```json
"[function()]"
```

<span data-ttu-id="8ffe2-107">È possibile fare riferimento a stringhe e altre funzioni come parametri per una funzione, ma le stringhe devono essere racchiuse tra virgolette singole.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-107">Strings and other functions can be referenced as parameters for a function, but strings must be surrounded in single quotes.</span></span> <span data-ttu-id="8ffe2-108">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-108">For example:</span></span>

```json
"[fn1(fn2(), 'foobar')]"
```

<span data-ttu-id="8ffe2-109">Ove applicabile, è possibile fare riferimento le proprietà di output di hello di una funzione tramite l'operatore punto hello.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-109">Where applicable, you can reference properties of hello output of a function by using hello dot operator.</span></span> <span data-ttu-id="8ffe2-110">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-110">For example:</span></span>

```json
"[func().prop1]"
```

## <a name="referencing-functions"></a><span data-ttu-id="8ffe2-111">Funzioni di riferimento</span><span class="sxs-lookup"><span data-stu-id="8ffe2-111">Referencing functions</span></span>
<span data-ttu-id="8ffe2-112">Queste funzioni possono essere utilizzati tooreference output dal contesto di un CreateUiDefinition o proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-112">These functions can be used tooreference outputs from hello properties or context of a CreateUiDefinition.</span></span>

### <a name="basics"></a><span data-ttu-id="8ffe2-113">basics</span><span class="sxs-lookup"><span data-stu-id="8ffe2-113">basics</span></span>
<span data-ttu-id="8ffe2-114">Restituisce i valori di output di hello di un elemento che viene definito nel passaggio di hello nozioni di base.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-114">Returns hello output values of an element that is defined in hello Basics step.</span></span>

<span data-ttu-id="8ffe2-115">esempio Hello restituisce output di hello dell'elemento hello denominato `foo` nel passaggio di hello nozioni fondamentali:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-115">hello following example returns hello output of hello element named `foo` in hello Basics step:</span></span>

```json
"[basics('foo')]"
```

### <a name="steps"></a><span data-ttu-id="8ffe2-116">steps</span><span class="sxs-lookup"><span data-stu-id="8ffe2-116">steps</span></span>
<span data-ttu-id="8ffe2-117">Restituisce i valori di output di hello di un elemento che viene definito nel passaggio specificato hello.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-117">Returns hello output values of an element that is defined in hello specified step.</span></span> <span data-ttu-id="8ffe2-118">i valori di output di hello tooget di elementi hello nozioni di base, utilizzare `basics()` invece.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-118">tooget hello output values of elements in hello Basics step, use `basics()` instead.</span></span>

<span data-ttu-id="8ffe2-119">esempio Hello restituisce output di hello dell'elemento hello denominato `bar` nel passaggio hello denominato `foo`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-119">hello following example returns hello output of hello element named `bar` in hello step named `foo`:</span></span>

```json
"[steps('foo').bar]"
```

### <a name="location"></a><span data-ttu-id="8ffe2-120">location</span><span class="sxs-lookup"><span data-stu-id="8ffe2-120">location</span></span>
<span data-ttu-id="8ffe2-121">Restituisce la posizione di hello selezionata nel passaggio di nozioni di base hello o contesto corrente hello.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-121">Returns hello location selected in hello Basics step or hello current context.</span></span>

<span data-ttu-id="8ffe2-122">Hello riportato potrebbe restituire `"westus"`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-122">hello following example could return `"westus"`:</span></span>

```json
"[location()]"
```

## <a name="string-functions"></a><span data-ttu-id="8ffe2-123">Funzioni stringa</span><span class="sxs-lookup"><span data-stu-id="8ffe2-123">String functions</span></span>
<span data-ttu-id="8ffe2-124">Queste funzioni possono essere usate solo con stringhe JSON.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-124">These functions can only be used with JSON strings.</span></span>

### <a name="concat"></a><span data-ttu-id="8ffe2-125">concat</span><span class="sxs-lookup"><span data-stu-id="8ffe2-125">concat</span></span>
<span data-ttu-id="8ffe2-126">Concatena una o più stringhe.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-126">Concatenates one or more strings.</span></span>

<span data-ttu-id="8ffe2-127">Ad esempio, se il valore di output di hello `element1` se `"bar"`, quindi questo esempio viene restituita la stringa hello `"foobar!"`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-127">For example, if hello output value of `element1` if `"bar"`, then this example returns hello string `"foobar!"`:</span></span>

```json
"[concat('foo', steps('step1').element1), '!']"
```

### <a name="substring"></a><span data-ttu-id="8ffe2-128">substring</span><span class="sxs-lookup"><span data-stu-id="8ffe2-128">substring</span></span>
<span data-ttu-id="8ffe2-129">Restituisce hello sottostringa di hello stringa specificata.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-129">Returns hello substring of hello specified string.</span></span> <span data-ttu-id="8ffe2-130">sottostringa Hello inizia in corrispondenza dell'indice specificato hello e hello lunghezza specificata.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-130">hello substring starts at hello specified index and has hello specified length.</span></span>

<span data-ttu-id="8ffe2-131">Hello esempio seguente viene restituito `"ftw"`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-131">hello following example returns `"ftw"`:</span></span>

```json
"[substring('azure-ftw!!!1one', 6, 3)]"
```

### <a name="replace"></a><span data-ttu-id="8ffe2-132">replace</span><span class="sxs-lookup"><span data-stu-id="8ffe2-132">replace</span></span>
<span data-ttu-id="8ffe2-133">Restituisce una stringa in cui tutte le occorrenze di hello stringa specificata nella stringa di hello corrente vengono sostituite con un'altra stringa.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-133">Returns a string in which all occurrences of hello specified string in hello current string are replaced with another string.</span></span>

<span data-ttu-id="8ffe2-134">Hello esempio seguente viene restituito `"Everything is awesome!"`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-134">hello following example returns `"Everything is awesome!"`:</span></span>

```json
"[replace('Everything is terrible!', 'terrible', 'awesome')]"
```

### <a name="guid"></a><span data-ttu-id="8ffe2-135">guid</span><span class="sxs-lookup"><span data-stu-id="8ffe2-135">guid</span></span>
<span data-ttu-id="8ffe2-136">Genera una stringa univoca globale (GUID).</span><span class="sxs-lookup"><span data-stu-id="8ffe2-136">Generates a globally unique string (GUID).</span></span>

<span data-ttu-id="8ffe2-137">Hello riportato potrebbe restituire `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-137">hello following example could return `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:</span></span>

```json
"[guid()]"
```

### <a name="tolower"></a><span data-ttu-id="8ffe2-138">toLower</span><span class="sxs-lookup"><span data-stu-id="8ffe2-138">toLower</span></span>
<span data-ttu-id="8ffe2-139">Restituisce un toolowercase stringa convertita.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-139">Returns a string converted toolowercase.</span></span>

<span data-ttu-id="8ffe2-140">Hello esempio seguente viene restituito `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-140">hello following example returns `"foobar"`:</span></span>

```json
"[toLower('FOOBAR')]"
```

### <a name="toupper"></a><span data-ttu-id="8ffe2-141">toUpper</span><span class="sxs-lookup"><span data-stu-id="8ffe2-141">toUpper</span></span>
<span data-ttu-id="8ffe2-142">Restituisce un toouppercase stringa convertita.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-142">Returns a string converted toouppercase.</span></span>

<span data-ttu-id="8ffe2-143">Hello esempio seguente viene restituito `"FOOBAR"`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-143">hello following example returns `"FOOBAR"`:</span></span>

```json
"[toUpper('foobar')]"
```

## <a name="collection-functions"></a><span data-ttu-id="8ffe2-144">Funzioni di raccolta</span><span class="sxs-lookup"><span data-stu-id="8ffe2-144">Collection functions</span></span>
<span data-ttu-id="8ffe2-145">Queste funzioni possono essere usate con le raccolte, ad esempio stringhe, matrici e oggetti JSON.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-145">These functions can be used with collections, like JSON strings, arrays and objects.</span></span>

### <a name="contains"></a><span data-ttu-id="8ffe2-146">contains</span><span class="sxs-lookup"><span data-stu-id="8ffe2-146">contains</span></span>
<span data-ttu-id="8ffe2-147">Restituisce `true` se contiene una stringa hello sottostringa specificata, una matrice contiene hello valore specificato o un oggetto contiene la chiave specificata hello.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-147">Returns `true` if a string contains hello specified substring, an array contains hello specified value, or an object contains hello specified key.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="8ffe2-148">Esempio 1: stringa</span><span class="sxs-lookup"><span data-stu-id="8ffe2-148">Example 1: string</span></span>
<span data-ttu-id="8ffe2-149">Hello esempio seguente viene restituito `true`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-149">hello following example returns `true`:</span></span>

```json
"[contains('foobar', 'foo')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="8ffe2-150">Esempio 2: matrice</span><span class="sxs-lookup"><span data-stu-id="8ffe2-150">Example 2: array</span></span>
<span data-ttu-id="8ffe2-151">Si supponga che `element1` restituisca `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-151">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="8ffe2-152">Hello esempio seguente viene restituito `false`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-152">hello following example returns `false`:</span></span>

```json
"[contains(steps('foo').element1, 4)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="8ffe2-153">Esempio 3: oggetto</span><span class="sxs-lookup"><span data-stu-id="8ffe2-153">Example 3: object</span></span>
<span data-ttu-id="8ffe2-154">Si supponga che `element1` restituisca:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-154">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="8ffe2-155">Hello esempio seguente viene restituito `true`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-155">hello following example returns `true`:</span></span>

```json
"[contains(steps('foo').element1, 'key1')]"
```

### <a name="length"></a><span data-ttu-id="8ffe2-156">length</span><span class="sxs-lookup"><span data-stu-id="8ffe2-156">length</span></span>
<span data-ttu-id="8ffe2-157">Restituisce il numero di hello di caratteri in una stringa, un numero hello di valori in una matrice o un numero di hello delle chiavi in un oggetto.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-157">Returns hello number of characters in a string, hello number of values in an array, or hello number of keys in an object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="8ffe2-158">Esempio 1: stringa</span><span class="sxs-lookup"><span data-stu-id="8ffe2-158">Example 1: string</span></span>
<span data-ttu-id="8ffe2-159">Hello esempio seguente viene restituito `6`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-159">hello following example returns `6`:</span></span>

```json
"[length('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="8ffe2-160">Esempio 2: matrice</span><span class="sxs-lookup"><span data-stu-id="8ffe2-160">Example 2: array</span></span>
<span data-ttu-id="8ffe2-161">Si supponga che `element1` restituisca `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-161">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="8ffe2-162">Hello esempio seguente viene restituito `3`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-162">hello following example returns `3`:</span></span>

```json
"[length(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="8ffe2-163">Esempio 3: oggetto</span><span class="sxs-lookup"><span data-stu-id="8ffe2-163">Example 3: object</span></span>
<span data-ttu-id="8ffe2-164">Si supponga che `element1` restituisca:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-164">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="8ffe2-165">Hello esempio seguente viene restituito `2`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-165">hello following example returns `2`:</span></span>

```json
"[length(steps('foo').element1)]"
```

### <a name="empty"></a><span data-ttu-id="8ffe2-166">empty</span><span class="sxs-lookup"><span data-stu-id="8ffe2-166">empty</span></span>
<span data-ttu-id="8ffe2-167">Restituisce `true` se l'oggetto, matrice o stringa hello è null o vuoto.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-167">Returns `true` if hello string, array, or object is null or empty.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="8ffe2-168">Esempio 1: stringa</span><span class="sxs-lookup"><span data-stu-id="8ffe2-168">Example 1: string</span></span>
<span data-ttu-id="8ffe2-169">Hello esempio seguente viene restituito `true`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-169">hello following example returns `true`:</span></span>

```json
"[empty('')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="8ffe2-170">Esempio 2: matrice</span><span class="sxs-lookup"><span data-stu-id="8ffe2-170">Example 2: array</span></span>
<span data-ttu-id="8ffe2-171">Si supponga che `element1` restituisca `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-171">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="8ffe2-172">Hello esempio seguente viene restituito `false`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-172">hello following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="8ffe2-173">Esempio 3: oggetto</span><span class="sxs-lookup"><span data-stu-id="8ffe2-173">Example 3: object</span></span>
<span data-ttu-id="8ffe2-174">Si supponga che `element1` restituisca:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-174">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="8ffe2-175">Hello esempio seguente viene restituito `false`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-175">hello following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-4-null-and-undefined"></a><span data-ttu-id="8ffe2-176">Esempio 4: Null e non definito</span><span class="sxs-lookup"><span data-stu-id="8ffe2-176">Example 4: null and undefined</span></span>
<span data-ttu-id="8ffe2-177">Si supponga che `element1` sia `null` o non definito.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-177">Assume `element1` is `null` or undefined.</span></span> <span data-ttu-id="8ffe2-178">Hello esempio seguente viene restituito `true`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-178">hello following example returns `true`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

### <a name="first"></a><span data-ttu-id="8ffe2-179">first</span><span class="sxs-lookup"><span data-stu-id="8ffe2-179">first</span></span>
<span data-ttu-id="8ffe2-180">Stringa; specificata restituisce hello primo carattere di hello primo valore della matrice specificata di hello; o hello prima chiave e il valore dell'oggetto specificato hello.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-180">Returns hello first character of hello specified string; first value of hello specified array; or hello first key and value of hello specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="8ffe2-181">Esempio 1: stringa</span><span class="sxs-lookup"><span data-stu-id="8ffe2-181">Example 1: string</span></span>
<span data-ttu-id="8ffe2-182">Hello esempio seguente viene restituito `"f"`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-182">hello following example returns `"f"`:</span></span>

```json
"[first('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="8ffe2-183">Esempio 2: matrice</span><span class="sxs-lookup"><span data-stu-id="8ffe2-183">Example 2: array</span></span>
<span data-ttu-id="8ffe2-184">Si supponga che `element1` restituisca `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-184">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="8ffe2-185">Hello esempio seguente viene restituito `1`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-185">hello following example returns `1`:</span></span>

```json
"[first(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="8ffe2-186">Esempio 3: oggetto</span><span class="sxs-lookup"><span data-stu-id="8ffe2-186">Example 3: object</span></span>
<span data-ttu-id="8ffe2-187">Si supponga che `element1` restituisca:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-187">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="8ffe2-188">Hello esempio seguente viene restituito `{"key1": "foobar"}`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-188">hello following example returns `{"key1": "foobar"}`:</span></span>

```json
"[first(steps('foo').element1)]"
```

### <a name="last"></a><span data-ttu-id="8ffe2-189">last</span><span class="sxs-lookup"><span data-stu-id="8ffe2-189">last</span></span>
<span data-ttu-id="8ffe2-190">Restituisce hello ultimo carattere di hello specificato valore di stringa, hello ultimo della matrice specificata di hello, o hello l'ultima chiave e il valore dell'oggetto specificato hello.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-190">Returns hello last character of hello specified string, hello last value of hello specified array, or hello last key and value of hello specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="8ffe2-191">Esempio 1: stringa</span><span class="sxs-lookup"><span data-stu-id="8ffe2-191">Example 1: string</span></span>
<span data-ttu-id="8ffe2-192">Hello esempio seguente viene restituito `"r"`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-192">hello following example returns `"r"`:</span></span>

```json
"[last('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="8ffe2-193">Esempio 2: matrice</span><span class="sxs-lookup"><span data-stu-id="8ffe2-193">Example 2: array</span></span>
<span data-ttu-id="8ffe2-194">Si supponga che `element1` restituisca `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-194">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="8ffe2-195">Hello esempio seguente viene restituito `2`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-195">hello following example returns `2`:</span></span>

```json
"[last(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="8ffe2-196">Esempio 3: oggetto</span><span class="sxs-lookup"><span data-stu-id="8ffe2-196">Example 3: object</span></span>
<span data-ttu-id="8ffe2-197">Si supponga che `element1` restituisca:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-197">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="8ffe2-198">Hello esempio seguente viene restituito `{"key2": "raboof"}`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-198">hello following example returns `{"key2": "raboof"}`:</span></span>

```json
"[last(steps('foo').element1)]"
```

### <a name="take"></a><span data-ttu-id="8ffe2-199">take</span><span class="sxs-lookup"><span data-stu-id="8ffe2-199">take</span></span>
<span data-ttu-id="8ffe2-200">Restituisce un numero specificato di caratteri contigui dall'inizio di hello della stringa hello, un numero specificato di valori contigui dall'inizio di hello della matrice hello o un numero specificato di valori dall'inizio di hello dell'oggetto hello e chiavi contigue.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-200">Returns a specified number of contiguous characters from hello start of hello string, a specified number of contiguous values from hello start of hello array, or a specified number of contiguous keys and values from hello start of hello object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="8ffe2-201">Esempio 1: stringa</span><span class="sxs-lookup"><span data-stu-id="8ffe2-201">Example 1: string</span></span>
<span data-ttu-id="8ffe2-202">Hello esempio seguente viene restituito `"foo"`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-202">hello following example returns `"foo"`:</span></span>

```json
"[take('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="8ffe2-203">Esempio 2: matrice</span><span class="sxs-lookup"><span data-stu-id="8ffe2-203">Example 2: array</span></span>
<span data-ttu-id="8ffe2-204">Si supponga che `element1` restituisca `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-204">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="8ffe2-205">Hello esempio seguente viene restituito `[1, 2]`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-205">hello following example returns `[1, 2]`:</span></span>

```json
"[take(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="8ffe2-206">Esempio 3: oggetto</span><span class="sxs-lookup"><span data-stu-id="8ffe2-206">Example 3: object</span></span>
<span data-ttu-id="8ffe2-207">Si supponga che `element1` restituisca:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-207">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="8ffe2-208">Hello esempio seguente viene restituito `{"key1": "foobar"}`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-208">hello following example returns `{"key1": "foobar"}`:</span></span>

```json
"[take(steps('foo').element1, 1)]"
```

### <a name="skip"></a><span data-ttu-id="8ffe2-209">skip</span><span class="sxs-lookup"><span data-stu-id="8ffe2-209">skip</span></span>
<span data-ttu-id="8ffe2-210">Ignora un numero specificato di elementi in una raccolta e restituisce quindi hello elementi rimanenti.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-210">Bypasses a specified number of elements in a collection, and then returns hello remaining elements.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="8ffe2-211">Esempio 1: stringa</span><span class="sxs-lookup"><span data-stu-id="8ffe2-211">Example 1: string</span></span>
<span data-ttu-id="8ffe2-212">Hello esempio seguente viene restituito `"bar"`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-212">hello following example returns `"bar"`:</span></span>

```json
"[skip('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="8ffe2-213">Esempio 2: matrice</span><span class="sxs-lookup"><span data-stu-id="8ffe2-213">Example 2: array</span></span>
<span data-ttu-id="8ffe2-214">Si supponga che `element1` restituisca `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-214">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="8ffe2-215">Hello esempio seguente viene restituito `[3]`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-215">hello following example returns `[3]`:</span></span>

```json
"[skip(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="8ffe2-216">Esempio 3: oggetto</span><span class="sxs-lookup"><span data-stu-id="8ffe2-216">Example 3: object</span></span>
<span data-ttu-id="8ffe2-217">Si supponga che `element1` restituisca:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-217">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="8ffe2-218">Hello esempio seguente viene restituito `{"key2": "raboof"}`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-218">hello following example returns `{"key2": "raboof"}`:</span></span>

```json
"[skip(steps('foo').element1, 1)]"
```

## <a name="logical-functions"></a><span data-ttu-id="8ffe2-219">Funzioni logiche</span><span class="sxs-lookup"><span data-stu-id="8ffe2-219">Logical functions</span></span>
<span data-ttu-id="8ffe2-220">Queste funzioni possono essere usate nelle istruzioni condizionali.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-220">These functions can be used in conditionals.</span></span> <span data-ttu-id="8ffe2-221">Alcune funzioni potrebbero non supportare tutti i tipi di dati JSON.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-221">Some functions may not support all JSON data types.</span></span>

### <a name="equals"></a><span data-ttu-id="8ffe2-222">equals</span><span class="sxs-lookup"><span data-stu-id="8ffe2-222">equals</span></span>
<span data-ttu-id="8ffe2-223">Restituisce `true` se entrambi i parametri hanno hello stesso tipo e valore.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-223">Returns `true` if both parameters have hello same type and value.</span></span> <span data-ttu-id="8ffe2-224">Questa funzione supporta tutti i tipi di dati JSON.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-224">This function supports all JSON data types.</span></span>

<span data-ttu-id="8ffe2-225">Hello esempio seguente viene restituito `true`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-225">hello following example returns `true`:</span></span>

```json
"[equals(0, 0)]"
```

<span data-ttu-id="8ffe2-226">Hello esempio seguente viene restituito `true`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-226">hello following example returns `true`:</span></span>

```json
"[equals('foo', 'foo')]"
```

<span data-ttu-id="8ffe2-227">Hello esempio seguente viene restituito `false`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-227">hello following example returns `false`:</span></span>

```json
"[equals('abc', ['a', 'b', 'c'])]"
```

### <a name="less"></a><span data-ttu-id="8ffe2-228">less</span><span class="sxs-lookup"><span data-stu-id="8ffe2-228">less</span></span>
<span data-ttu-id="8ffe2-229">Restituisce `true` se hello primo parametro è minore di secondo parametro hello.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-229">Returns `true` if hello first parameter is strictly less than hello second parameter.</span></span> <span data-ttu-id="8ffe2-230">Questa funzione supporta solo parametri di tipo numero e stringa.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-230">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="8ffe2-231">Hello esempio seguente viene restituito `true`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-231">hello following example returns `true`:</span></span>

```json
"[less(1, 2)]"
```

<span data-ttu-id="8ffe2-232">Hello esempio seguente viene restituito `false`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-232">hello following example returns `false`:</span></span>

```json
"[less('9', '10')]"
```

### <a name="lessorequals"></a><span data-ttu-id="8ffe2-233">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="8ffe2-233">lessOrEquals</span></span>
<span data-ttu-id="8ffe2-234">Restituisce `true` se hello primo parametro è minore o uguale toohello secondo parametro.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-234">Returns `true` if hello first parameter is less than or equal toohello second parameter.</span></span> <span data-ttu-id="8ffe2-235">Questa funzione supporta solo parametri di tipo numero e stringa.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-235">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="8ffe2-236">Hello esempio seguente viene restituito `true`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-236">hello following example returns `true`:</span></span>

```json
"[lessOrEquals(2, 2)]"
```

### <a name="greater"></a><span data-ttu-id="8ffe2-237">greater</span><span class="sxs-lookup"><span data-stu-id="8ffe2-237">greater</span></span>
<span data-ttu-id="8ffe2-238">Restituisce `true` se hello primo parametro è maggiore di secondo parametro hello.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-238">Returns `true` if hello first parameter is strictly greater than hello second parameter.</span></span> <span data-ttu-id="8ffe2-239">Questa funzione supporta solo parametri di tipo numero e stringa.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-239">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="8ffe2-240">Hello esempio seguente viene restituito `false`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-240">hello following example returns `false`:</span></span>

```json
"[greater(1, 2)]"
```

<span data-ttu-id="8ffe2-241">Hello esempio seguente viene restituito `true`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-241">hello following example returns `true`:</span></span>

```json
"[greater('9', '10')]"
```

### <a name="greaterorequals"></a><span data-ttu-id="8ffe2-242">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="8ffe2-242">greaterOrEquals</span></span>
<span data-ttu-id="8ffe2-243">Restituisce `true` se hello primo parametro è maggiore o uguale toohello secondo parametro.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-243">Returns `true` if hello first parameter is greater than or equal toohello second parameter.</span></span> <span data-ttu-id="8ffe2-244">Questa funzione supporta solo parametri di tipo numero e stringa.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-244">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="8ffe2-245">Hello esempio seguente viene restituito `true`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-245">hello following example returns `true`:</span></span>

```json
"[greaterOrEquals(2, 2)]"
```

### <a name="and"></a><span data-ttu-id="8ffe2-246">e</span><span class="sxs-lookup"><span data-stu-id="8ffe2-246">and</span></span>
<span data-ttu-id="8ffe2-247">Restituisce `true` se tutti i parametri di hello restituiscono troppo`true`.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-247">Returns `true` if all hello parameters evaluate too`true`.</span></span> <span data-ttu-id="8ffe2-248">Questa funzione supporta solo due o più parametri di tipo booleano.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-248">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="8ffe2-249">Hello esempio seguente viene restituito `true`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-249">hello following example returns `true`:</span></span>

```json
"[and(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="8ffe2-250">Hello esempio seguente viene restituito `false`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-250">hello following example returns `false`:</span></span>

```json
"[and(equals(0, 0), greater(1, 2))]"
```

### <a name="or"></a><span data-ttu-id="8ffe2-251">oppure</span><span class="sxs-lookup"><span data-stu-id="8ffe2-251">or</span></span>
<span data-ttu-id="8ffe2-252">Restituisce `true` se almeno uno dei parametri di hello restituisce troppo`true`.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-252">Returns `true` if at least one of hello parameters evaluates too`true`.</span></span> <span data-ttu-id="8ffe2-253">Questa funzione supporta solo due o più parametri di tipo booleano.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-253">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="8ffe2-254">Hello esempio seguente viene restituito `true`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-254">hello following example returns `true`:</span></span>

```json
"[or(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="8ffe2-255">Hello esempio seguente viene restituito `true`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-255">hello following example returns `true`:</span></span>

```json
"[or(equals(0, 0), greater(1, 2))]"
```

### <a name="not"></a><span data-ttu-id="8ffe2-256">not</span><span class="sxs-lookup"><span data-stu-id="8ffe2-256">not</span></span>
<span data-ttu-id="8ffe2-257">Restituisce `true` se il parametro hello restituisce troppo`false`.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-257">Returns `true` if hello parameter evaluates too`false`.</span></span> <span data-ttu-id="8ffe2-258">Questa funzione supporta solo parametri di tipo booleano.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-258">This function supports parameters only of type Boolean.</span></span>

<span data-ttu-id="8ffe2-259">Hello esempio seguente viene restituito `true`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-259">hello following example returns `true`:</span></span>

```json
"[not(false)]"
```

<span data-ttu-id="8ffe2-260">Hello esempio seguente viene restituito `false`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-260">hello following example returns `false`:</span></span>

```json
"[not(equals(0, 0))]"
```

### <a name="coalesce"></a><span data-ttu-id="8ffe2-261">coalesce</span><span class="sxs-lookup"><span data-stu-id="8ffe2-261">coalesce</span></span>
<span data-ttu-id="8ffe2-262">Restituisce hello valore del primo parametro non null di hello.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-262">Returns hello value of hello first non-null parameter.</span></span> <span data-ttu-id="8ffe2-263">Questa funzione supporta tutti i tipi di dati JSON.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-263">This function supports all JSON data types.</span></span>

<span data-ttu-id="8ffe2-264">Si supponga che `element1` e `element2` non siano definiti.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-264">Assume `element1` and `element2` are undefined.</span></span> <span data-ttu-id="8ffe2-265">Hello esempio seguente viene restituito `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-265">hello following example returns `"foobar"`:</span></span>

```json
"[coalesce(steps('foo').element1, steps('foo').element2, 'foobar')]"
```

## <a name="conversion-functions"></a><span data-ttu-id="8ffe2-266">Funzioni di conversione</span><span class="sxs-lookup"><span data-stu-id="8ffe2-266">Conversion functions</span></span>
<span data-ttu-id="8ffe2-267">Queste funzioni possono essere valori di tooconvert utilizzati tra i tipi di dati JSON e le codifiche.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-267">These functions can be used tooconvert values between JSON data types and encodings.</span></span>

### <a name="int"></a><span data-ttu-id="8ffe2-268">int</span><span class="sxs-lookup"><span data-stu-id="8ffe2-268">int</span></span>
<span data-ttu-id="8ffe2-269">Converte hello parametro tooan intero.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-269">Converts hello parameter tooan integer.</span></span> <span data-ttu-id="8ffe2-270">Questa funzione supporta parametri di tipo numero e stringa.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-270">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="8ffe2-271">Hello esempio seguente viene restituito `1`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-271">hello following example returns `1`:</span></span>

```json
"[int('1')]"
```

<span data-ttu-id="8ffe2-272">Hello esempio seguente viene restituito `2`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-272">hello following example returns `2`:</span></span>

```json
"[int(2.9)]"
```

### <a name="float"></a><span data-ttu-id="8ffe2-273">float</span><span class="sxs-lookup"><span data-stu-id="8ffe2-273">float</span></span>
<span data-ttu-id="8ffe2-274">Converte tooa parametro hello a virgola mobile.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-274">Converts hello parameter tooa floating-point.</span></span> <span data-ttu-id="8ffe2-275">Questa funzione supporta parametri di tipo numero e stringa.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-275">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="8ffe2-276">Hello esempio seguente viene restituito `1.0`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-276">hello following example returns `1.0`:</span></span>

```json
"[float('1.0')]"
```

<span data-ttu-id="8ffe2-277">Hello esempio seguente viene restituito `2.9`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-277">hello following example returns `2.9`:</span></span>

```json
"[float(2.9)]"
```

### <a name="string"></a><span data-ttu-id="8ffe2-278">string</span><span class="sxs-lookup"><span data-stu-id="8ffe2-278">string</span></span>
<span data-ttu-id="8ffe2-279">Converte una stringa di tooa parametro hello.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-279">Converts hello parameter tooa string.</span></span> <span data-ttu-id="8ffe2-280">Questa funzione supporta parametri di tutti i tipi di dati JSON.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-280">This function supports parameters of all JSON data types.</span></span>

<span data-ttu-id="8ffe2-281">Hello esempio seguente viene restituito `"1"`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-281">hello following example returns `"1"`:</span></span>

```json
"[string(1)]"
```

<span data-ttu-id="8ffe2-282">Hello esempio seguente viene restituito `"2.9"`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-282">hello following example returns `"2.9"`:</span></span>

```json
"[string(2.9)]"
```

<span data-ttu-id="8ffe2-283">Hello esempio seguente viene restituito `"[1,2,3]"`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-283">hello following example returns `"[1,2,3]"`:</span></span>

```json
"[string([1,2,3])]"
```

<span data-ttu-id="8ffe2-284">Hello esempio seguente viene restituito `"{"foo":"bar"}"`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-284">hello following example returns `"{"foo":"bar"}"`:</span></span>

```json
"[string({\"foo\":\"bar\"})]"
```

### <a name="bool"></a><span data-ttu-id="8ffe2-285">bool</span><span class="sxs-lookup"><span data-stu-id="8ffe2-285">bool</span></span>
<span data-ttu-id="8ffe2-286">Converte tooa parametro hello Boolean.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-286">Converts hello parameter tooa Boolean.</span></span> <span data-ttu-id="8ffe2-287">Questa funzione supporta parametri di tipo numero, stringa e booleano.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-287">This function supports parameters of type number, string, and Boolean.</span></span> <span data-ttu-id="8ffe2-288">TooBooleans simili in JavaScript, qualsiasi valore eccetto `0` o `'false'` restituisce `true`.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-288">Similar tooBooleans in JavaScript, any value except `0` or `'false'` returns `true`.</span></span>

<span data-ttu-id="8ffe2-289">Hello esempio seguente viene restituito `true`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-289">hello following example returns `true`:</span></span>

```json
"[bool(1)]"
```

<span data-ttu-id="8ffe2-290">Hello esempio seguente viene restituito `false`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-290">hello following example returns `false`:</span></span>

```json
"[bool(0)]"
```

<span data-ttu-id="8ffe2-291">Hello esempio seguente viene restituito `true`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-291">hello following example returns `true`:</span></span>

```json
"[bool(true)]"
```

<span data-ttu-id="8ffe2-292">Hello esempio seguente viene restituito `true`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-292">hello following example returns `true`:</span></span>

```json
"[bool('true')]"
```

### <a name="parse"></a><span data-ttu-id="8ffe2-293">parse</span><span class="sxs-lookup"><span data-stu-id="8ffe2-293">parse</span></span>
<span data-ttu-id="8ffe2-294">Converte il tipo nativo hello parametro tooa.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-294">Converts hello parameter tooa native type.</span></span> <span data-ttu-id="8ffe2-295">In altre parole, questa funzione è inverso hello di `string()`.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-295">In other words, this function is hello inverse of `string()`.</span></span> <span data-ttu-id="8ffe2-296">Questa funzione supporta solo parametri di tipo stringa.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-296">This function supports parameters only of type string.</span></span>

<span data-ttu-id="8ffe2-297">Hello esempio seguente viene restituito `1`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-297">hello following example returns `1`:</span></span>

```json
"[parse('1')]"
```

<span data-ttu-id="8ffe2-298">Hello esempio seguente viene restituito `true`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-298">hello following example returns `true`:</span></span>

```json
"[parse('true')]"
```

<span data-ttu-id="8ffe2-299">Hello esempio seguente viene restituito `[1,2,3]`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-299">hello following example returns `[1,2,3]`:</span></span>

```json
"[parse('[1,2,3]')]"
```

<span data-ttu-id="8ffe2-300">Hello esempio seguente viene restituito `{"foo":"bar"}`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-300">hello following example returns `{"foo":"bar"}`:</span></span>

```json
"[parse('{\"foo\":\"bar\"}')]"
```

### <a name="encodebase64"></a><span data-ttu-id="8ffe2-301">encodeBase64</span><span class="sxs-lookup"><span data-stu-id="8ffe2-301">encodeBase64</span></span>
<span data-ttu-id="8ffe2-302">Codifica una stringa con codifica base 64 tooa parametro hello.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-302">Encodes hello parameter tooa base-64 encoded string.</span></span> <span data-ttu-id="8ffe2-303">Questa funzione supporta solo parametri di tipo stringa.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-303">This function supports parameters only of type string.</span></span>

<span data-ttu-id="8ffe2-304">Hello esempio seguente viene restituito `"Zm9vYmFy"`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-304">hello following example returns `"Zm9vYmFy"`:</span></span>

```json
"[encodeBase64('foobar')]"
```

### <a name="decodebase64"></a><span data-ttu-id="8ffe2-305">decodeBase64</span><span class="sxs-lookup"><span data-stu-id="8ffe2-305">decodeBase64</span></span>
<span data-ttu-id="8ffe2-306">Decodifica il parametro hello da una stringa con codifica base 64.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-306">Decodes hello parameter from a base-64 encoded string.</span></span> <span data-ttu-id="8ffe2-307">Questa funzione supporta solo parametri di tipo stringa.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-307">This function supports parameters only of type string.</span></span>

<span data-ttu-id="8ffe2-308">Hello esempio seguente viene restituito `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-308">hello following example returns `"foobar"`:</span></span>

```json
"[decodeBase64('Zm9vYmFy')]"
```

### <a name="encodeuricomponent"></a><span data-ttu-id="8ffe2-309">encodeUriComponent</span><span class="sxs-lookup"><span data-stu-id="8ffe2-309">encodeUriComponent</span></span>
<span data-ttu-id="8ffe2-310">Codifica hello parametro tooa codificato in URL stringa.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-310">Encodes hello parameter tooa URL encoded string.</span></span> <span data-ttu-id="8ffe2-311">Questa funzione supporta solo parametri di tipo stringa.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-311">This function supports parameters only of type string.</span></span>

<span data-ttu-id="8ffe2-312">Hello esempio seguente viene restituito `"https%3A%2F%2Fportal.azure.com%2F"`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-312">hello following example returns `"https%3A%2F%2Fportal.azure.com%2F"`:</span></span>

```json
"[encodeUriComponent('https://portal.azure.com/')]"
```

### <a name="decodeuricomponent"></a><span data-ttu-id="8ffe2-313">decodeUriComponent</span><span class="sxs-lookup"><span data-stu-id="8ffe2-313">decodeUriComponent</span></span>
<span data-ttu-id="8ffe2-314">Decodifica il parametro hello da una stringa con codificata URL.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-314">Decodes hello parameter from a URL encoded string.</span></span> <span data-ttu-id="8ffe2-315">Questa funzione supporta solo parametri di tipo stringa.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-315">This function supports parameters only of type string.</span></span>

<span data-ttu-id="8ffe2-316">Hello esempio seguente viene restituito `"https://portal.azure.com/"`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-316">hello following example returns `"https://portal.azure.com/"`:</span></span>

```json
"[decodeUriComponent('https%3A%2F%2Fportal.azure.com%2F')]"
```

## <a name="math-functions"></a><span data-ttu-id="8ffe2-317">Funzioni matematiche</span><span class="sxs-lookup"><span data-stu-id="8ffe2-317">Math functions</span></span>
### <a name="add"></a><span data-ttu-id="8ffe2-318">add</span><span class="sxs-lookup"><span data-stu-id="8ffe2-318">add</span></span>
<span data-ttu-id="8ffe2-319">Somma due numeri e restituisce il risultato di hello.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-319">Adds two numbers, and returns hello result.</span></span>

<span data-ttu-id="8ffe2-320">Hello esempio seguente viene restituito `3`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-320">hello following example returns `3`:</span></span>

```json
"[add(1, 2)]"
```

### <a name="sub"></a><span data-ttu-id="8ffe2-321">sub</span><span class="sxs-lookup"><span data-stu-id="8ffe2-321">sub</span></span>
<span data-ttu-id="8ffe2-322">Sottrae numero secondo di hello da primo hello e restituisce il risultato di hello.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-322">Subtracts hello second number from hello first number, and returns hello result.</span></span>

<span data-ttu-id="8ffe2-323">Hello esempio seguente viene restituito `1`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-323">hello following example returns `1`:</span></span>

```json
"[sub(3, 2)]"
```

### <a name="mul"></a><span data-ttu-id="8ffe2-324">mul</span><span class="sxs-lookup"><span data-stu-id="8ffe2-324">mul</span></span>
<span data-ttu-id="8ffe2-325">Moltiplica due numeri e restituisce il risultato di hello.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-325">Multiplies two numbers, and returns hello result.</span></span>

<span data-ttu-id="8ffe2-326">Hello esempio seguente viene restituito `6`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-326">hello following example returns `6`:</span></span>

```json
"[mul(2, 3)]"
```

### <a name="div"></a><span data-ttu-id="8ffe2-327">div</span><span class="sxs-lookup"><span data-stu-id="8ffe2-327">div</span></span>
<span data-ttu-id="8ffe2-328">Divide hello primo numero per hello secondo numero e restituisce il risultato di hello.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-328">Divides hello first number by hello second number, and returns hello result.</span></span> <span data-ttu-id="8ffe2-329">il risultato di Hello è sempre un numero intero.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-329">hello result is always an integer.</span></span>

<span data-ttu-id="8ffe2-330">Hello esempio seguente viene restituito `2`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-330">hello following example returns `2`:</span></span>

```json
"[div(6, 3)]"
```

### <a name="mod"></a><span data-ttu-id="8ffe2-331">mod</span><span class="sxs-lookup"><span data-stu-id="8ffe2-331">mod</span></span>
<span data-ttu-id="8ffe2-332">Divide hello primo numero per hello secondo numero e restituisce il resto di hello.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-332">Divides hello first number by hello second number, and returns hello remainder.</span></span>

<span data-ttu-id="8ffe2-333">Hello esempio seguente viene restituito `0`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-333">hello following example returns `0`:</span></span>

```json
"[mod(6, 3)]"
```

<span data-ttu-id="8ffe2-334">Hello esempio seguente viene restituito `2`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-334">hello following example returns `2`:</span></span>

```json
"[mod(6, 4)]"
```

### <a name="min"></a><span data-ttu-id="8ffe2-335">Min</span><span class="sxs-lookup"><span data-stu-id="8ffe2-335">min</span></span>
<span data-ttu-id="8ffe2-336">Restituisce hello piccola dei numeri di hello due.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-336">Returns hello small of hello two numbers.</span></span>

<span data-ttu-id="8ffe2-337">Hello esempio seguente viene restituito `1`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-337">hello following example returns `1`:</span></span>

```json
"[min(1, 2)]"
```

### <a name="max"></a><span data-ttu-id="8ffe2-338">max</span><span class="sxs-lookup"><span data-stu-id="8ffe2-338">max</span></span>
<span data-ttu-id="8ffe2-339">Hello restituisce più elevato tra due numeri hello.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-339">Returns hello larger of hello two numbers.</span></span>

<span data-ttu-id="8ffe2-340">Hello esempio seguente viene restituito `2`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-340">hello following example returns `2`:</span></span>

```json
"[max(1, 2)]"
```

### <a name="range"></a><span data-ttu-id="8ffe2-341">range</span><span class="sxs-lookup"><span data-stu-id="8ffe2-341">range</span></span>
<span data-ttu-id="8ffe2-342">Genera una sequenza di integrale numeri all'interno di hello intervallo specificato.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-342">Generates a sequence of integral numbers within hello specified range.</span></span>

<span data-ttu-id="8ffe2-343">Hello esempio seguente viene restituito `[1,2,3]`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-343">hello following example returns `[1,2,3]`:</span></span>

```json
"[range(1, 3)]"
```

### <a name="rand"></a><span data-ttu-id="8ffe2-344">rand</span><span class="sxs-lookup"><span data-stu-id="8ffe2-344">rand</span></span>
<span data-ttu-id="8ffe2-345">Restituisce un casuale un numero integrale all'interno di hello intervallo specificato.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-345">Returns a random integral number within hello specified range.</span></span> <span data-ttu-id="8ffe2-346">Questa funzione non genera numeri casuali protetti con crittografia.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-346">This function does not generate cryptographically secure random numbers.</span></span>

<span data-ttu-id="8ffe2-347">Hello riportato potrebbe restituire `42`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-347">hello following example could return `42`:</span></span>

```json
"[rand(-100, 100)]"
```

### <a name="floor"></a><span data-ttu-id="8ffe2-348">floor</span><span class="sxs-lookup"><span data-stu-id="8ffe2-348">floor</span></span>
<span data-ttu-id="8ffe2-349">Restituisce l'intero più grande hello minore o uguale toohello il numero specificato.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-349">Returns hello largest integer less than or equal toohello specified number.</span></span>

<span data-ttu-id="8ffe2-350">Hello esempio seguente viene restituito `3`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-350">hello following example returns `3`:</span></span>

```json
"[floor(3.14)]"
```

### <a name="ceil"></a><span data-ttu-id="8ffe2-351">ceil</span><span class="sxs-lookup"><span data-stu-id="8ffe2-351">ceil</span></span>
<span data-ttu-id="8ffe2-352">Restituisce hello più grande numero intero maggiore o uguale toohello il numero specificato.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-352">Returns hello largest integer greater than or equal toohello specified number.</span></span>

<span data-ttu-id="8ffe2-353">Hello esempio seguente viene restituito `4`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-353">hello following example returns `4`:</span></span>

```json
"[ceil(3.14)]"
```

## <a name="date-functions"></a><span data-ttu-id="8ffe2-354">Funzioni di data</span><span class="sxs-lookup"><span data-stu-id="8ffe2-354">Date functions</span></span>
### <a name="utcnow"></a><span data-ttu-id="8ffe2-355">utcNow</span><span class="sxs-lookup"><span data-stu-id="8ffe2-355">utcNow</span></span>
<span data-ttu-id="8ffe2-356">Restituisce una stringa in formato ISO 8601 di hello data e ora nel computer locale hello correnti.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-356">Returns a string in ISO 8601 format of hello current date and time on hello local computer.</span></span>

<span data-ttu-id="8ffe2-357">Hello riportato potrebbe restituire `"1990-12-31T23:59:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-357">hello following example could return `"1990-12-31T23:59:59.000Z"`:</span></span>

```json
"[utcNow()]"
```

### <a name="addseconds"></a><span data-ttu-id="8ffe2-358">addSeconds</span><span class="sxs-lookup"><span data-stu-id="8ffe2-358">addSeconds</span></span>
<span data-ttu-id="8ffe2-359">Aggiunge un numero intero di secondi toohello specificato timestamp.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-359">Adds an integral number of seconds toohello specified timestamp.</span></span>

<span data-ttu-id="8ffe2-360">Hello esempio seguente viene restituito `"1991-01-01T00:00:00.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-360">hello following example returns `"1991-01-01T00:00:00.000Z"`:</span></span>

```json
"[addSeconds('1990-12-31T23:59:60Z', 1)]"
```

### <a name="addminutes"></a><span data-ttu-id="8ffe2-361">addMinutes</span><span class="sxs-lookup"><span data-stu-id="8ffe2-361">addMinutes</span></span>
<span data-ttu-id="8ffe2-362">Aggiunge un numero intero di minuti toohello specificato timestamp.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-362">Adds an integral number of minutes toohello specified timestamp.</span></span>

<span data-ttu-id="8ffe2-363">Hello esempio seguente viene restituito `"1991-01-01T00:00:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-363">hello following example returns `"1991-01-01T00:00:59.000Z"`:</span></span>

```json
"[addMinutes('1990-12-31T23:59:59Z', 1)]"
```

### <a name="addhours"></a><span data-ttu-id="8ffe2-364">addHours</span><span class="sxs-lookup"><span data-stu-id="8ffe2-364">addHours</span></span>
<span data-ttu-id="8ffe2-365">Aggiunge un numero integrale di toohello di ore specificato timestamp.</span><span class="sxs-lookup"><span data-stu-id="8ffe2-365">Adds an integral number of hours toohello specified timestamp.</span></span>

<span data-ttu-id="8ffe2-366">Hello esempio seguente viene restituito `"1991-01-01T00:59:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="8ffe2-366">hello following example returns `"1991-01-01T00:59:59.000Z"`:</span></span>

```json
"[addHours('1990-12-31T23:59:59Z', 1)]"
```

## <a name="next-steps"></a><span data-ttu-id="8ffe2-367">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8ffe2-367">Next steps</span></span>
* <span data-ttu-id="8ffe2-368">Per un'introduzione tooAzure Gestione risorse, vedere [Panoramica di gestione risorse di Azure](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8ffe2-368">For an introduction tooAzure Resource Manager, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

