---
title: 'modello di gestione risorse aaaAzure funzioni: le matrici e oggetti | Documenti Microsoft'
description: Viene descritto toouse funzioni hello in un modello di gestione risorse di Azure per l'utilizzo di matrici e oggetti.
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
ms.date: 06/12/2017
ms.author: tomfitz
ms.openlocfilehash: e5f1a9b2a71039562eae7e48c2474a1fa59a7bea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="array-and-object-functions-for-azure-resource-manager-templates"></a>Funzioni di matrice e oggetto per i modelli di Azure Resource Manager 

Resource Manager offre diverse funzioni per l'uso di matrici e oggetti.

* [array](#array)
* [coalesce](#coalesce)
* [concat](#concat)
* [contains](#contains)
* [createArray](#createarray)
* [empty](#empty)
* [first](#first)
* [intersection](#intersection)
* [json](#json)
* [last](#last)
* [length](#length)
* [min](#min)
* [max](#max)
* [range](#range)
* [skip](#skip)
* [take](#take)
* [union](#union)

tooget una matrice di valori di stringa delimitata da un valore, vedere [dividere](resource-group-template-functions-string.md#split).

<a id="array" />

## <a name="array"></a>array
`array(convertToArray)`

Converte una matrice di tooan valori hello.

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| convertToArray |Sì |int, stringa, matrice o oggetto |Matrice di tooan tooconvert valori Hello. |

### <a name="return-value"></a>Valore restituito

Una matrice.

### <a name="example"></a>Esempio

Hello esempio seguente viene illustrato come toouse hello funzione matrice con tipi diversi.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "intToConvert": {
            "type": "int",
            "defaultValue": 1
        },
        "stringToConvert": {
            "type": "string",
            "defaultValue": "a"
        },
        "objectToConvert": {
            "type": "object",
            "defaultValue": {"a": "b", "c": "d"}
        }
    },
    "resources": [
    ],
    "outputs": {
        "intOutput": {
            "type": "array",
            "value": "[array(parameters('intToConvert'))]"
        },
        "stringOutput": {
            "type": "array",
            "value": "[array(parameters('stringToConvert'))]"
        },
        "objectOutput": {
            "type": "array",
            "value": "[array(parameters('objectToConvert'))]"
        }
    }
}
```

Hello output di hello precedente esempio con i valori predefiniti di hello è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| intOutput | Array | [1] |
| stringOutput | Array | ["a"] |
| objectOutput | Array | [{"a": "b", "c": "d"}] |

<a id="coalesce" />

## <a name="coalesce"></a>coalesce
`coalesce(arg1, arg2, arg3, ...)`

Restituisce i valori non null prima dai parametri hello. Stringhe vuote, matrici vuote e oggetti vuoti sono non null.

### <a name="parameters"></a>Parametri

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| arg1 |Sì |int, stringa, matrice o oggetto |Hello tootest prima di valore per i valori null. |
| argomenti aggiuntivi |No |int, stringa, matrice o oggetto |Tootest valori aggiuntivi per i valori null. |

### <a name="return-value"></a>Valore restituito

valore di Hello dei parametri non null prima hello, che può essere una stringa, int, una matrice o un oggetto. Null se tutti i parametri sono null. 

### <a name="example"></a>Esempio

Hello seguente esempio Mostra output di hello da diversi utilizzi di coalesce.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "objectToTest": {
            "type": "object",
            "defaultValue": {
                "null1": null, 
                "null2": null,
                "string": "default",
                "int": 1,
                "object": {"first": "default"},
                "array": [1]
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringOutput": {
            "type": "string",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').string)]"
        },
        "intOutput": {
            "type": "int",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').int)]"
        },
        "objectOutput": {
            "type": "object",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').object)]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').array)]"
        },
        "emptyOutput": {
            "type": "bool",
            "value": "[empty(coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2))]"
        }
    }
}
```

Hello output di hello precedente esempio con i valori predefiniti di hello è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| stringOutput | String | default |
| intOutput | int | 1 |
| objectOutput | Oggetto | {"first": "default"} |
| arrayOutput | Array | [1] |
| emptyOutput | Booleano | True  |

<a id="concat" />

## <a name="concat"></a>concat
`concat(arg1, arg2, arg3, ...)`

Combina più matrici e restituisce una matrice, hello concatenato o combina più valori di stringa e restituisce la stringa hello concatenato. 

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| arg1 |Sì |stringa o matrice |Hello prima matrice o stringa per la concatenazione. |
| argomenti aggiuntivi |No |stringa o matrice |Matrici o stringhe aggiuntive in ordine sequenziale per la concatenazione. |

Questa funzione può accettare un numero qualsiasi di argomenti e può accettare stringhe o matrici per i parametri di hello.

### <a name="return-value"></a>Valore restituito
Stringa o matrice di valori concatenati.

### <a name="example"></a>Esempio

Hello di esempio seguente viene illustrato come toocombine due matrici.

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

Hello output di hello precedente esempio con i valori predefiniti di hello è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| return | Array | ["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"] |

Hello di esempio seguente viene illustrato come toocombine due valori stringa e restituire una stringa concatenata.

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

Hello output di hello precedente esempio con i valori predefiniti di hello è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| concatOutput | String | prefix-5yj4yjf5mbg72 |

<a id="contains" />

## <a name="contains"></a>contains
`contains(container, itemToFind)`

Verifica se una matrice contiene un valore, se un oggetto contiene una chiave o se una stringa contiene una sottostringa.

### <a name="parameters"></a>Parametri

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| Contenitore |Sì |matrice, oggetto o stringa |valore di Hello contenente toofind valore hello. |
| itemToFind |Sì |stringa o numero intero |toofind valore Hello. |

### <a name="return-value"></a>Valore restituito

**True** se l'elemento hello è stato trovato; in caso contrario, **False**.

### <a name="example"></a>Esempio

Hello esempio seguente viene illustrato come toouse contiene con tipi diversi:

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

Hello output di hello precedente esempio con i valori predefiniti di hello è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| stringTrue | Booleano | True  |
| stringFalse | Booleano | False |
| objectTrue | Booleano | True  |
| objectFalse | Booleano | False |
| arrayTrue | Booleano | True  |
| arrayFalse | Booleano | False |

<a id="createarray" />

## <a name="createarray"></a>createarray
`createArray (arg1, arg2, arg3, ...)`

Crea una matrice di parametri di hello.

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| arg1 |Sì |Stringa, numero intero, matrice o oggetto |primo valore Hello nella matrice hello. |
| argomenti aggiuntivi |No |Stringa, numero intero, matrice o oggetto |Valori aggiuntivi nella matrice hello. |

### <a name="return-value"></a>Valore restituito

Una matrice.

### <a name="example"></a>Esempio

Hello seguente esempio viene illustrato come createArray toouse con tipi diversi:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
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
        "stringArray": {
            "type": "array",
            "value": "[createArray('a', 'b', 'c')]"
        },
        "intArray": {
            "type": "array",
            "value": "[createArray(1, 2, 3)]"
        },
        "objectArray": {
            "type": "array",
            "value": "[createArray(parameters('objectToTest'))]"
        },
        "arrayArray": {
            "type": "array",
            "value": "[createArray(parameters('arrayToTest'))]"
        }
    }
}
```

Hello output di hello precedente esempio con i valori predefiniti di hello è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| stringArray | Array | ["a", "b", "c"] |
| intArray | Array | [1, 2, 3] |
| objectArray | Array | [{"one": "a", "two": "b", "three": "c"}] |
| arrayArray | Array | [["one", "two", "three"]] |

<a id="empty" />

## <a name="empty"></a>empty

`empty(itemToTest)`

Determina se una matrice, un oggetto o una stringa sono vuoti.

### <a name="parameters"></a>Parametri

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| itemToTest |Sì |matrice, oggetto o stringa |Hello toocheck valore se è vuota. |

### <a name="return-value"></a>Valore restituito

Restituisce **True** se il valore di hello è vuota; in caso contrario, **False**.

### <a name="example"></a>Esempio

Hello di esempio seguente controlla se una matrice, un oggetto e una stringa sono vuote.

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

Hello output di hello precedente esempio con i valori predefiniti di hello è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| arrayEmpty | Booleano | True  |
| objectEmpty | Booleano | True  |
| stringEmpty | Booleano | True  |

<a id="first" />

## <a name="first"></a>first
`first(arg1)`

Restituisce hello primo elemento della matrice hello o primo carattere della stringa hello.

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| arg1 |Sì |stringa o matrice |carattere o Hello valore tooretrieve hello primo elemento. |

### <a name="return-value"></a>Valore restituito

tipo (string, int, matrice o oggetto) del primo elemento di hello in una matrice di Hello o hello primo carattere della stringa.

### <a name="example"></a>Esempio

Hello esempio seguente viene illustrato come toouse hello prima funzione con una matrice e una stringa.

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

Hello output di hello precedente esempio con i valori predefiniti di hello è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| arrayOutput | String | one |
| stringOutput | String | O |

<a id="intersection" />

## <a name="intersection"></a>intersezione
`intersection(arg1, arg2, arg3, ...)`

Restituisce una matrice o un oggetto con elementi comuni hello dai parametri hello.

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| arg1 |Sì |matrice o oggetto |Hello toouse prima di valore per la ricerca di elementi comuni. |
| arg2 |Sì |matrice o oggetto |Hello secondo valore toouse per la ricerca di elementi comuni. |
| argomenti aggiuntivi |No |matrice o oggetto |Toouse valori aggiuntivi per la ricerca di elementi comuni. |

### <a name="return-value"></a>Valore restituito

Una matrice o un oggetto con elementi comuni hello.

### <a name="example"></a>Esempio

Hello esempio viene illustrato come toouse intersezione con matrici e gli oggetti seguenti:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "z", "three": "c"}
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "objectOutput": {
            "type": "object",
            "value": "[intersection(parameters('firstObject'), parameters('secondObject'))]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[intersection(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

Hello output di hello precedente esempio con i valori predefiniti di hello è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| objectOutput | Oggetto | {"one": "a", "three": "c"} |
| arrayOutput | Array | ["two", "three"] |


## <a name="json"></a>json
`json(arg1)`

Restituisce un oggetto JSON.

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| arg1 |Sì |string |Hello valore tooconvert tooJSON. |


### <a name="return-value"></a>Valore restituito

oggetto JSON Hello hello specificato stringa o un oggetto vuoto quando **null** specificato.

### <a name="example"></a>Esempio

Hello esempio viene illustrato come toouse intersezione con matrici e gli oggetti seguenti:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "jsonOutput": {
            "type": "object",
            "value": "[json('{\"a\": \"b\"}')]"
        },
        "nullOutput": {
            "type": "bool",
            "value": "[empty(json('null'))]"
        }
    }
}
```

Hello output di hello precedente esempio con i valori predefiniti di hello è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| jsonOutput | Oggetto | {"a": "b"} |
| nullOutput | Boolean | True  |

<a id="last" />

## <a name="last"></a>last
`last (arg1)`

Restituisce hello l'ultimo elemento della matrice hello o ultimo carattere della stringa hello.

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| arg1 |Sì |stringa o matrice |carattere o Hello valore tooretrieve hello ultimo elemento. |

### <a name="return-value"></a>Valore restituito

tipo di Hello (string, int, matrice o oggetto) dell'ultimo elemento di hello in una matrice o ultimo carattere di hello di una stringa.

### <a name="example"></a>Esempio

Hello esempio seguente viene illustrato come toouse hello ultima funzione con una matrice e una stringa.

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

Hello output di hello precedente esempio con i valori predefiniti di hello è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| arrayOutput | String | three |
| stringOutput | String | e |

<a id="length" />

## <a name="length"></a>length
`length(arg1)`

Restituisce il numero di hello di elementi in una matrice o in una stringa di caratteri.

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| arg1 |Sì |stringa o matrice |Hello toouse matrice per ottenere il numero di hello di elementi o hello toouse stringa per ottenere il numero di hello di caratteri. |

### <a name="return-value"></a>Valore restituito

Numero intero 

### <a name="example"></a>Esempio

Hello seguente esempio viene illustrato come lunghezza toouse con una matrice e la stringa:

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

Hello output di hello precedente esempio con i valori predefiniti di hello è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| arrayLength | int | 3 |
| stringLength | int | 13 |

È possibile utilizzare questa funzione con un numero di hello matrice toospecify di iterazioni quando si creano risorse. Nell'esempio seguente di hello, hello parametro **siteNames** tooan matrice di nomi toouse riferimento durante la creazione di siti web hello.

```json
"copy": {
    "name": "websitescopy",
    "count": "[length(parameters('siteNames'))]"
}
```

Per altre informazioni sull'uso di questa funzione con una matrice, vedere [Creare più istanze di risorse in Gestione risorse di Azure](resource-group-create-multiple.md).

<a id="min" />

## <a name="min"></a>Min
`min(arg1)`

Restituisce hello valore minimo da una matrice di interi o un elenco delimitato da virgole di numeri interi.

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| arg1 |Sì |matrice di numeri interi o elenco di numeri interi delimitato da virgole |Hello raccolta tooget hello valore minimo. |

### <a name="return-value"></a>Valore restituito

Un integer che rappresenta il valore minimo di hello.

### <a name="example"></a>Esempio

Hello seguente esempio viene illustrato come toouse min con una matrice e un elenco di numeri interi:

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

Hello output di hello precedente esempio con i valori predefiniti di hello è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| arrayOutput | int | 0 |
| intOutput | int | 0 |

<a id="max" />

## <a name="max"></a>max
`max(arg1)`

Restituisce hello valore massimo da una matrice di interi o un elenco delimitato da virgole di numeri interi.

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| arg1 |Sì |matrice di numeri interi o elenco di numeri interi delimitato da virgole |Hello raccolta tooget hello valore massimo. |

### <a name="return-value"></a>Valore restituito

Un integer che rappresenta il valore massimo di hello.

### <a name="example"></a>Esempio

Hello seguente esempio viene illustrato come toouse max a una matrice e un elenco di numeri interi:

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

Hello output di hello precedente esempio con i valori predefiniti di hello è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| arrayOutput | int | 5 |
| intOutput | int | 5 |

<a id="range" />

## <a name="range"></a>range
`range(startingInteger, numberOfElements)`

Crea una matrice di numeri interi da un numero intero iniziale, contenente un dato numero di elementi.

### <a name="parameters"></a>Parametri

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| startingInteger |Sì |int |Hello primo intero hello matrice. |
| numberofElements |Sì |int |numero di Hello dei numeri interi nella matrice hello. |

### <a name="return-value"></a>Valore restituito

Matrice di numeri interi.

### <a name="example"></a>Esempio

Hello di esempio seguente viene illustrato come toouse hello funzione intervallo:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "startingInt": {
            "type": "int",
            "defaultValue": 5
        },
        "numberOfElements": {
            "type": "int",
            "defaultValue": 3
        }
    },
    "resources": [],
    "outputs": {
        "rangeOutput": {
            "type": "array",
            "value": "[range(parameters('startingInt'),parameters('numberOfElements'))]"
        }
    }
}
```

Hello output di hello precedente esempio con i valori predefiniti di hello è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| rangeOutput | Array | [5, 6, 7] |

<a id="skip" />

## <a name="skip"></a>skip
`skip(originalValue, numberToSkip)`

Restituisce una matrice con tutti gli elementi di hello dopo il numero specificato nella matrice hello hello o restituisce una stringa con tutti i caratteri di hello dopo hello numero specificato nella stringa hello.

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| originalValue |Sì |stringa o matrice |Hello toouse matrice o stringa per l'omissione. |
| numberToSkip |Sì |int |numero di Hello di tooskip elementi o i caratteri. Se questo valore è 0 o meno, tutti gli elementi di hello o vengono restituiti i caratteri nel valore hello. Se è maggiore della lunghezza della stringa o matrice hello hello, viene restituita una matrice vuota o una stringa. |

### <a name="return-value"></a>Valore restituito

Stringa o matrice.

### <a name="example"></a>Esempio

Hello seguente esempio Ignora hello numero specificato di elementi nella matrice hello e hello numero specificato di caratteri in una stringa.

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

Hello output di hello precedente esempio con i valori predefiniti di hello è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| arrayOutput | Array | ["three"] |
| stringOutput | String | two three |

<a id="take" />

## <a name="take"></a>take
`take(originalValue, numberToTake)`

Restituisce una matrice con hello specificato numero di elementi dall'inizio della matrice hello di hello o una stringa con hello numero specificato di caratteri dall'inizio di hello della stringa hello.

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| originalValue |Sì |stringa o matrice |Hello stringa o matrice di elementi di hello tootake da. |
| numberToTake |Sì |int |numero di Hello di tootake elementi o i caratteri. Se il valore è minore o uguale a 0, viene restituita una stringa o un matrice vuota. Se è maggiore della lunghezza di hello di hello matrice o stringa specificato, vengono restituiti tutti gli elementi hello hello matrice o stringa. |

### <a name="return-value"></a>Valore restituito

Stringa o matrice.

### <a name="example"></a>Esempio

Hello seguente esempio accetta hello numero specificato di elementi dalla matrice hello e i caratteri di una stringa.

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

Hello output di hello precedente esempio con i valori predefiniti di hello è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| arrayOutput | Array | ["one", "two"] |
| stringOutput | String | in |

<a id="union" />

## <a name="union"></a>union
`union(arg1, arg2, arg3, ...)`

Restituisce una matrice o un oggetto con tutti gli elementi dai parametri hello. Valori e chiavi duplicati sono inclusi una sola volta.

### <a name="parameters"></a>Parametri

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| arg1 |Sì |matrice o oggetto |Hello toouse prima di valore per l'aggiunta di elementi. |
| arg2 |Sì |matrice o oggetto |Hello secondo valore toouse per l'aggiunta di elementi. |
| argomenti aggiuntivi |No |matrice o oggetto |Toouse valori aggiuntivi per l'aggiunta di elementi. |

### <a name="return-value"></a>Valore restituito

Una matrice o un oggetto.

### <a name="example"></a>Esempio

Hello esempio viene illustrato come unione toouse con matrici e gli oggetti seguenti:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"three": "c", "four": "d", "five": "e"}
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["three", "four"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "objectOutput": {
            "type": "object",
            "value": "[union(parameters('firstObject'), parameters('secondObject'))]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[union(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

Hello output di hello precedente esempio con i valori predefiniti di hello è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| objectOutput | Oggetto | {"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"} |
| arrayOutput | Array | ["one", "two", "three", "four"] |

## <a name="next-steps"></a>Passaggi successivi
* Per una descrizione delle sezioni hello in un modello di gestione risorse di Azure, vedere [modelli Authoring Azure Resource Manager](resource-group-authoring-templates.md).
* toomerge più modelli, vedere [con modelli collegati con Azure Resource Manager](resource-group-linked-templates.md).
* tooiterate un numero specificato di volte durante la creazione di un tipo di risorsa, vedere [creare più istanze delle risorse in Azure Resource Manager](resource-group-create-multiple.md).
* toosee come modello hello toodeploy è stato creato, vedere [distribuire un'applicazione con il modello di gestione risorse di Azure](resource-group-template-deploy.md).

