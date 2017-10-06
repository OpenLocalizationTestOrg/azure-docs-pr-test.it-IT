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
# <a name="createuidefinition-functions"></a>Funzioni di CreateUiDefinition
In questa sezione contiene firme hello per tutte le funzioni supportate di un CreateUiDefinition.

toouse una funzione, dichiarazione di hello racchiudere tra parentesi quadre. ad esempio:

```json
"[function()]"
```

È possibile fare riferimento a stringhe e altre funzioni come parametri per una funzione, ma le stringhe devono essere racchiuse tra virgolette singole. ad esempio:

```json
"[fn1(fn2(), 'foobar')]"
```

Ove applicabile, è possibile fare riferimento le proprietà di output di hello di una funzione tramite l'operatore punto hello. ad esempio:

```json
"[func().prop1]"
```

## <a name="referencing-functions"></a>Funzioni di riferimento
Queste funzioni possono essere utilizzati tooreference output dal contesto di un CreateUiDefinition o proprietà hello.

### <a name="basics"></a>basics
Restituisce i valori di output di hello di un elemento che viene definito nel passaggio di hello nozioni di base.

esempio Hello restituisce output di hello dell'elemento hello denominato `foo` nel passaggio di hello nozioni fondamentali:

```json
"[basics('foo')]"
```

### <a name="steps"></a>steps
Restituisce i valori di output di hello di un elemento che viene definito nel passaggio specificato hello. i valori di output di hello tooget di elementi hello nozioni di base, utilizzare `basics()` invece.

esempio Hello restituisce output di hello dell'elemento hello denominato `bar` nel passaggio hello denominato `foo`:

```json
"[steps('foo').bar]"
```

### <a name="location"></a>location
Restituisce la posizione di hello selezionata nel passaggio di nozioni di base hello o contesto corrente hello.

Hello riportato potrebbe restituire `"westus"`:

```json
"[location()]"
```

## <a name="string-functions"></a>Funzioni stringa
Queste funzioni possono essere usate solo con stringhe JSON.

### <a name="concat"></a>concat
Concatena una o più stringhe.

Ad esempio, se il valore di output di hello `element1` se `"bar"`, quindi questo esempio viene restituita la stringa hello `"foobar!"`:

```json
"[concat('foo', steps('step1').element1), '!']"
```

### <a name="substring"></a>substring
Restituisce hello sottostringa di hello stringa specificata. sottostringa Hello inizia in corrispondenza dell'indice specificato hello e hello lunghezza specificata.

Hello esempio seguente viene restituito `"ftw"`:

```json
"[substring('azure-ftw!!!1one', 6, 3)]"
```

### <a name="replace"></a>replace
Restituisce una stringa in cui tutte le occorrenze di hello stringa specificata nella stringa di hello corrente vengono sostituite con un'altra stringa.

Hello esempio seguente viene restituito `"Everything is awesome!"`:

```json
"[replace('Everything is terrible!', 'terrible', 'awesome')]"
```

### <a name="guid"></a>guid
Genera una stringa univoca globale (GUID).

Hello riportato potrebbe restituire `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:

```json
"[guid()]"
```

### <a name="tolower"></a>toLower
Restituisce un toolowercase stringa convertita.

Hello esempio seguente viene restituito `"foobar"`:

```json
"[toLower('FOOBAR')]"
```

### <a name="toupper"></a>toUpper
Restituisce un toouppercase stringa convertita.

Hello esempio seguente viene restituito `"FOOBAR"`:

```json
"[toUpper('foobar')]"
```

## <a name="collection-functions"></a>Funzioni di raccolta
Queste funzioni possono essere usate con le raccolte, ad esempio stringhe, matrici e oggetti JSON.

### <a name="contains"></a>contains
Restituisce `true` se contiene una stringa hello sottostringa specificata, una matrice contiene hello valore specificato o un oggetto contiene la chiave specificata hello.

#### <a name="example-1-string"></a>Esempio 1: stringa
Hello esempio seguente viene restituito `true`:

```json
"[contains('foobar', 'foo')]"
```

#### <a name="example-2-array"></a>Esempio 2: matrice
Si supponga che `element1` restituisca `[1, 2, 3]`. Hello esempio seguente viene restituito `false`:

```json
"[contains(steps('foo').element1, 4)]"
```

#### <a name="example-3-object"></a>Esempio 3: oggetto
Si supponga che `element1` restituisca:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Hello esempio seguente viene restituito `true`:

```json
"[contains(steps('foo').element1, 'key1')]"
```

### <a name="length"></a>length
Restituisce il numero di hello di caratteri in una stringa, un numero hello di valori in una matrice o un numero di hello delle chiavi in un oggetto.

#### <a name="example-1-string"></a>Esempio 1: stringa
Hello esempio seguente viene restituito `6`:

```json
"[length('foobar')]"
```

#### <a name="example-2-array"></a>Esempio 2: matrice
Si supponga che `element1` restituisca `[1, 2, 3]`. Hello esempio seguente viene restituito `3`:

```json
"[length(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>Esempio 3: oggetto
Si supponga che `element1` restituisca:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Hello esempio seguente viene restituito `2`:

```json
"[length(steps('foo').element1)]"
```

### <a name="empty"></a>empty
Restituisce `true` se l'oggetto, matrice o stringa hello è null o vuoto.

#### <a name="example-1-string"></a>Esempio 1: stringa
Hello esempio seguente viene restituito `true`:

```json
"[empty('')]"
```

#### <a name="example-2-array"></a>Esempio 2: matrice
Si supponga che `element1` restituisca `[1, 2, 3]`. Hello esempio seguente viene restituito `false`:

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>Esempio 3: oggetto
Si supponga che `element1` restituisca:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Hello esempio seguente viene restituito `false`:

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-4-null-and-undefined"></a>Esempio 4: Null e non definito
Si supponga che `element1` sia `null` o non definito. Hello esempio seguente viene restituito `true`:

```json
"[empty(steps('foo').element1)]"
```

### <a name="first"></a>first
Stringa; specificata restituisce hello primo carattere di hello primo valore della matrice specificata di hello; o hello prima chiave e il valore dell'oggetto specificato hello.

#### <a name="example-1-string"></a>Esempio 1: stringa
Hello esempio seguente viene restituito `"f"`:

```json
"[first('foobar')]"
```

#### <a name="example-2-array"></a>Esempio 2: matrice
Si supponga che `element1` restituisca `[1, 2, 3]`. Hello esempio seguente viene restituito `1`:

```json
"[first(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>Esempio 3: oggetto
Si supponga che `element1` restituisca:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
Hello esempio seguente viene restituito `{"key1": "foobar"}`:

```json
"[first(steps('foo').element1)]"
```

### <a name="last"></a>last
Restituisce hello ultimo carattere di hello specificato valore di stringa, hello ultimo della matrice specificata di hello, o hello l'ultima chiave e il valore dell'oggetto specificato hello.

#### <a name="example-1-string"></a>Esempio 1: stringa
Hello esempio seguente viene restituito `"r"`:

```json
"[last('foobar')]"
```

#### <a name="example-2-array"></a>Esempio 2: matrice
Si supponga che `element1` restituisca `[1, 2, 3]`. Hello esempio seguente viene restituito `2`:

```json
"[last(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>Esempio 3: oggetto
Si supponga che `element1` restituisca:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Hello esempio seguente viene restituito `{"key2": "raboof"}`:

```json
"[last(steps('foo').element1)]"
```

### <a name="take"></a>take
Restituisce un numero specificato di caratteri contigui dall'inizio di hello della stringa hello, un numero specificato di valori contigui dall'inizio di hello della matrice hello o un numero specificato di valori dall'inizio di hello dell'oggetto hello e chiavi contigue.

#### <a name="example-1-string"></a>Esempio 1: stringa
Hello esempio seguente viene restituito `"foo"`:

```json
"[take('foobar', 3)]"
```

#### <a name="example-2-array"></a>Esempio 2: matrice
Si supponga che `element1` restituisca `[1, 2, 3]`. Hello esempio seguente viene restituito `[1, 2]`:

```json
"[take(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a>Esempio 3: oggetto
Si supponga che `element1` restituisca:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Hello esempio seguente viene restituito `{"key1": "foobar"}`:

```json
"[take(steps('foo').element1, 1)]"
```

### <a name="skip"></a>skip
Ignora un numero specificato di elementi in una raccolta e restituisce quindi hello elementi rimanenti.

#### <a name="example-1-string"></a>Esempio 1: stringa
Hello esempio seguente viene restituito `"bar"`:

```json
"[skip('foobar', 3)]"
```

#### <a name="example-2-array"></a>Esempio 2: matrice
Si supponga che `element1` restituisca `[1, 2, 3]`. Hello esempio seguente viene restituito `[3]`:

```json
"[skip(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a>Esempio 3: oggetto
Si supponga che `element1` restituisca:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
Hello esempio seguente viene restituito `{"key2": "raboof"}`:

```json
"[skip(steps('foo').element1, 1)]"
```

## <a name="logical-functions"></a>Funzioni logiche
Queste funzioni possono essere usate nelle istruzioni condizionali. Alcune funzioni potrebbero non supportare tutti i tipi di dati JSON.

### <a name="equals"></a>equals
Restituisce `true` se entrambi i parametri hanno hello stesso tipo e valore. Questa funzione supporta tutti i tipi di dati JSON.

Hello esempio seguente viene restituito `true`:

```json
"[equals(0, 0)]"
```

Hello esempio seguente viene restituito `true`:

```json
"[equals('foo', 'foo')]"
```

Hello esempio seguente viene restituito `false`:

```json
"[equals('abc', ['a', 'b', 'c'])]"
```

### <a name="less"></a>less
Restituisce `true` se hello primo parametro è minore di secondo parametro hello. Questa funzione supporta solo parametri di tipo numero e stringa.

Hello esempio seguente viene restituito `true`:

```json
"[less(1, 2)]"
```

Hello esempio seguente viene restituito `false`:

```json
"[less('9', '10')]"
```

### <a name="lessorequals"></a>lessOrEquals
Restituisce `true` se hello primo parametro è minore o uguale toohello secondo parametro. Questa funzione supporta solo parametri di tipo numero e stringa.

Hello esempio seguente viene restituito `true`:

```json
"[lessOrEquals(2, 2)]"
```

### <a name="greater"></a>greater
Restituisce `true` se hello primo parametro è maggiore di secondo parametro hello. Questa funzione supporta solo parametri di tipo numero e stringa.

Hello esempio seguente viene restituito `false`:

```json
"[greater(1, 2)]"
```

Hello esempio seguente viene restituito `true`:

```json
"[greater('9', '10')]"
```

### <a name="greaterorequals"></a>greaterOrEquals
Restituisce `true` se hello primo parametro è maggiore o uguale toohello secondo parametro. Questa funzione supporta solo parametri di tipo numero e stringa.

Hello esempio seguente viene restituito `true`:

```json
"[greaterOrEquals(2, 2)]"
```

### <a name="and"></a>e
Restituisce `true` se tutti i parametri di hello restituiscono troppo`true`. Questa funzione supporta solo due o più parametri di tipo booleano.

Hello esempio seguente viene restituito `true`:

```json
"[and(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

Hello esempio seguente viene restituito `false`:

```json
"[and(equals(0, 0), greater(1, 2))]"
```

### <a name="or"></a>oppure
Restituisce `true` se almeno uno dei parametri di hello restituisce troppo`true`. Questa funzione supporta solo due o più parametri di tipo booleano.

Hello esempio seguente viene restituito `true`:

```json
"[or(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

Hello esempio seguente viene restituito `true`:

```json
"[or(equals(0, 0), greater(1, 2))]"
```

### <a name="not"></a>not
Restituisce `true` se il parametro hello restituisce troppo`false`. Questa funzione supporta solo parametri di tipo booleano.

Hello esempio seguente viene restituito `true`:

```json
"[not(false)]"
```

Hello esempio seguente viene restituito `false`:

```json
"[not(equals(0, 0))]"
```

### <a name="coalesce"></a>coalesce
Restituisce hello valore del primo parametro non null di hello. Questa funzione supporta tutti i tipi di dati JSON.

Si supponga che `element1` e `element2` non siano definiti. Hello esempio seguente viene restituito `"foobar"`:

```json
"[coalesce(steps('foo').element1, steps('foo').element2, 'foobar')]"
```

## <a name="conversion-functions"></a>Funzioni di conversione
Queste funzioni possono essere valori di tooconvert utilizzati tra i tipi di dati JSON e le codifiche.

### <a name="int"></a>int
Converte hello parametro tooan intero. Questa funzione supporta parametri di tipo numero e stringa.

Hello esempio seguente viene restituito `1`:

```json
"[int('1')]"
```

Hello esempio seguente viene restituito `2`:

```json
"[int(2.9)]"
```

### <a name="float"></a>float
Converte tooa parametro hello a virgola mobile. Questa funzione supporta parametri di tipo numero e stringa.

Hello esempio seguente viene restituito `1.0`:

```json
"[float('1.0')]"
```

Hello esempio seguente viene restituito `2.9`:

```json
"[float(2.9)]"
```

### <a name="string"></a>string
Converte una stringa di tooa parametro hello. Questa funzione supporta parametri di tutti i tipi di dati JSON.

Hello esempio seguente viene restituito `"1"`:

```json
"[string(1)]"
```

Hello esempio seguente viene restituito `"2.9"`:

```json
"[string(2.9)]"
```

Hello esempio seguente viene restituito `"[1,2,3]"`:

```json
"[string([1,2,3])]"
```

Hello esempio seguente viene restituito `"{"foo":"bar"}"`:

```json
"[string({\"foo\":\"bar\"})]"
```

### <a name="bool"></a>bool
Converte tooa parametro hello Boolean. Questa funzione supporta parametri di tipo numero, stringa e booleano. TooBooleans simili in JavaScript, qualsiasi valore eccetto `0` o `'false'` restituisce `true`.

Hello esempio seguente viene restituito `true`:

```json
"[bool(1)]"
```

Hello esempio seguente viene restituito `false`:

```json
"[bool(0)]"
```

Hello esempio seguente viene restituito `true`:

```json
"[bool(true)]"
```

Hello esempio seguente viene restituito `true`:

```json
"[bool('true')]"
```

### <a name="parse"></a>parse
Converte il tipo nativo hello parametro tooa. In altre parole, questa funzione è inverso hello di `string()`. Questa funzione supporta solo parametri di tipo stringa.

Hello esempio seguente viene restituito `1`:

```json
"[parse('1')]"
```

Hello esempio seguente viene restituito `true`:

```json
"[parse('true')]"
```

Hello esempio seguente viene restituito `[1,2,3]`:

```json
"[parse('[1,2,3]')]"
```

Hello esempio seguente viene restituito `{"foo":"bar"}`:

```json
"[parse('{\"foo\":\"bar\"}')]"
```

### <a name="encodebase64"></a>encodeBase64
Codifica una stringa con codifica base 64 tooa parametro hello. Questa funzione supporta solo parametri di tipo stringa.

Hello esempio seguente viene restituito `"Zm9vYmFy"`:

```json
"[encodeBase64('foobar')]"
```

### <a name="decodebase64"></a>decodeBase64
Decodifica il parametro hello da una stringa con codifica base 64. Questa funzione supporta solo parametri di tipo stringa.

Hello esempio seguente viene restituito `"foobar"`:

```json
"[decodeBase64('Zm9vYmFy')]"
```

### <a name="encodeuricomponent"></a>encodeUriComponent
Codifica hello parametro tooa codificato in URL stringa. Questa funzione supporta solo parametri di tipo stringa.

Hello esempio seguente viene restituito `"https%3A%2F%2Fportal.azure.com%2F"`:

```json
"[encodeUriComponent('https://portal.azure.com/')]"
```

### <a name="decodeuricomponent"></a>decodeUriComponent
Decodifica il parametro hello da una stringa con codificata URL. Questa funzione supporta solo parametri di tipo stringa.

Hello esempio seguente viene restituito `"https://portal.azure.com/"`:

```json
"[decodeUriComponent('https%3A%2F%2Fportal.azure.com%2F')]"
```

## <a name="math-functions"></a>Funzioni matematiche
### <a name="add"></a>add
Somma due numeri e restituisce il risultato di hello.

Hello esempio seguente viene restituito `3`:

```json
"[add(1, 2)]"
```

### <a name="sub"></a>sub
Sottrae numero secondo di hello da primo hello e restituisce il risultato di hello.

Hello esempio seguente viene restituito `1`:

```json
"[sub(3, 2)]"
```

### <a name="mul"></a>mul
Moltiplica due numeri e restituisce il risultato di hello.

Hello esempio seguente viene restituito `6`:

```json
"[mul(2, 3)]"
```

### <a name="div"></a>div
Divide hello primo numero per hello secondo numero e restituisce il risultato di hello. il risultato di Hello è sempre un numero intero.

Hello esempio seguente viene restituito `2`:

```json
"[div(6, 3)]"
```

### <a name="mod"></a>mod
Divide hello primo numero per hello secondo numero e restituisce il resto di hello.

Hello esempio seguente viene restituito `0`:

```json
"[mod(6, 3)]"
```

Hello esempio seguente viene restituito `2`:

```json
"[mod(6, 4)]"
```

### <a name="min"></a>Min
Restituisce hello piccola dei numeri di hello due.

Hello esempio seguente viene restituito `1`:

```json
"[min(1, 2)]"
```

### <a name="max"></a>max
Hello restituisce più elevato tra due numeri hello.

Hello esempio seguente viene restituito `2`:

```json
"[max(1, 2)]"
```

### <a name="range"></a>range
Genera una sequenza di integrale numeri all'interno di hello intervallo specificato.

Hello esempio seguente viene restituito `[1,2,3]`:

```json
"[range(1, 3)]"
```

### <a name="rand"></a>rand
Restituisce un casuale un numero integrale all'interno di hello intervallo specificato. Questa funzione non genera numeri casuali protetti con crittografia.

Hello riportato potrebbe restituire `42`:

```json
"[rand(-100, 100)]"
```

### <a name="floor"></a>floor
Restituisce l'intero più grande hello minore o uguale toohello il numero specificato.

Hello esempio seguente viene restituito `3`:

```json
"[floor(3.14)]"
```

### <a name="ceil"></a>ceil
Restituisce hello più grande numero intero maggiore o uguale toohello il numero specificato.

Hello esempio seguente viene restituito `4`:

```json
"[ceil(3.14)]"
```

## <a name="date-functions"></a>Funzioni di data
### <a name="utcnow"></a>utcNow
Restituisce una stringa in formato ISO 8601 di hello data e ora nel computer locale hello correnti.

Hello riportato potrebbe restituire `"1990-12-31T23:59:59.000Z"`:

```json
"[utcNow()]"
```

### <a name="addseconds"></a>addSeconds
Aggiunge un numero intero di secondi toohello specificato timestamp.

Hello esempio seguente viene restituito `"1991-01-01T00:00:00.000Z"`:

```json
"[addSeconds('1990-12-31T23:59:60Z', 1)]"
```

### <a name="addminutes"></a>addMinutes
Aggiunge un numero intero di minuti toohello specificato timestamp.

Hello esempio seguente viene restituito `"1991-01-01T00:00:59.000Z"`:

```json
"[addMinutes('1990-12-31T23:59:59Z', 1)]"
```

### <a name="addhours"></a>addHours
Aggiunge un numero integrale di toohello di ore specificato timestamp.

Hello esempio seguente viene restituito `"1991-01-01T00:59:59.000Z"`:

```json
"[addHours('1990-12-31T23:59:59Z', 1)]"
```

## <a name="next-steps"></a>Passaggi successivi
* Per un'introduzione tooAzure Gestione risorse, vedere [Panoramica di gestione risorse di Azure](resource-group-overview.md).

