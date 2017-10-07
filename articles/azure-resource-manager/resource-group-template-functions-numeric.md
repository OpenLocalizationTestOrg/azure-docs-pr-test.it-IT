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
# <a name="numeric-functions-for-azure-resource-manager-templates"></a>Funzioni numeriche per i modelli di Azure Resource Manager

Gestione risorse offre hello seguenti funzioni per l'utilizzo di numeri interi:

* [add](#add)
* [copyIndex](#copyindex)
* [div](#div)
* [float](#float)
* [int](#int)
* [min](#min)
* [max](#max)
* [mod](#mod)
* [mul](#mul)
* [sub](#sub)

<a id="add" />

## <a name="add"></a>add
`add(operand1, operand2)`

Restituisce hello somma di due interi fornito di hello.

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- | 
|operand1 |Sì |int |Primo numero tooadd. |
|operand2 |Sì |int |Secondo numero tooadd. |

### <a name="return-value"></a>Valore restituito

Valore intero che contiene la somma hello dei parametri di hello.

### <a name="example"></a>Esempio

Hello di esempio seguente vengono aggiunti due parametri.

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

Hello output di hello precedente esempio con i valori predefiniti di hello è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| addResult | int | 8 |

<a id="copyindex" />

## <a name="copyindex"></a>copyIndex
`copyIndex(loopName, offset)`

Restituisce hello indice di un ciclo di iterazione. 

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| loopName | No | string | nome di Hello del ciclo di hello per il recupero di iterazione hello. |
| offset |No |int |Hello tooadd toohello iterazione in base zero in valore numerico. |

### <a name="remarks"></a>Osservazioni

Questa funzione viene sempre usata con un oggetto **copy** . Se non viene fornito alcun valore per **offset**, viene restituito il valore di iterazione corrente hello. il valore di iterazione Hello inizia in corrispondenza di zero.

Hello **loopName** proprietà consente toospecify se copyIndex fa riferimento iterazione risorsa tooa o l'iterazione di proprietà. Se non viene fornito alcun valore per **loopName**, viene utilizzato l'iterazione di tipo risorsa corrente hello. Specificare un valore per **loopName** durante l'iterazione di una proprietà. 
 
Per una descrizione completa dell'uso di **copyIndex**, vedere [Creare più istanze di risorse in Azure Resource Manager](resource-group-create-multiple.md).

### <a name="example"></a>Esempio

Hello esempio seguente viene illustrato un ciclo e hello indice valore copia incluso nel nome hello. 

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

### <a name="return-value"></a>Valore restituito

Numero intero che rappresenta l'indice corrente di hello di iterazione hello.

<a id="div" />

## <a name="div"></a>div
`div(operand1, operand2)`

Restituisce hello divisione di integer di due interi fornito di hello.

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| operand1 |Sì |int |numero di Hello viene diviso. |
| operand2 |Sì |int |Hello numero toodivide utilizzato. Non può essere 0. |

### <a name="return-value"></a>Valore restituito

Una divisione di interi che rappresentano hello.

### <a name="example"></a>Esempio

Hello di esempio seguente consente di dividere un parametro da un altro parametro.

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

Hello output di hello precedente esempio con i valori predefiniti di hello è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| divResult | int | 2 |

<a id="float" />

## <a name="float"></a>float
`float(arg1)`

Converte tooa valore hello numero a virgola mobile. Questa funzione è utilizzare solo quando si passano parametri personalizzati tooan applicazione, ad esempio un'App di logica.

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| arg1 |Sì |stringa o numero intero |Hello valore tooconvert tooa numero a virgola mobile. |

### <a name="return-value"></a>Valore restituito
Un numero a virgola mobile.

### <a name="example"></a>Esempio

Hello di esempio seguente viene illustrato come toouse float toopass parametri tooa logica App:

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

## <a name="int"></a>int
`int(valueToConvert)`

Converte l'intero tooan di hello valore specificato.

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| valueToConvert |Sì |stringa o numero intero |Hello valore tooconvert tooan numero intero. |

### <a name="return-value"></a>Valore restituito

Valore convertito da un numero intero di hello.

### <a name="example"></a>Esempio

Hello seguente converte toointeger valore di parametro fornito dall'utente hello.

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

Hello output di hello precedente esempio con i valori predefiniti di hello è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| intResult | int | 4 |


<a id="min" />

## <a name="min"></a>Min
`min (arg1)`

Restituisce hello valore minimo da una matrice di interi o un elenco delimitato da virgole di numeri interi.

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| arg1 |Sì |matrice di numeri interi o elenco di numeri interi delimitato da virgole |Hello raccolta tooget hello valore minimo. |

### <a name="return-value"></a>Valore restituito

Intero che rappresenta il valore minimo da raccolta hello.

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
`max (arg1)`

Restituisce hello valore massimo da una matrice di interi o un elenco delimitato da virgole di numeri interi.

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| arg1 |Sì |matrice di numeri interi o elenco di numeri interi delimitato da virgole |Hello raccolta tooget hello valore massimo. |

### <a name="return-value"></a>Valore restituito

Intero che rappresenta il valore massimo di hello dalla raccolta hello.

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

<a id="mod" />

## <a name="mod"></a>mod
`mod(operand1, operand2)`

Restituisce il resto di hello della divisione di interi hello usando interi forniti due hello.

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| operand1 |Sì |int |numero di Hello viene diviso. |
| operand2 |Sì |int |numero di Hello toodivide utilizzato, non può essere 0. |

### <a name="return-value"></a>Valore restituito
Un numero intero che rappresenta hello parte restante.

### <a name="example"></a>Esempio

Hello esempio seguente restituisce il resto di hello della divisione di un parametro da un altro parametro.

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

Hello output di hello precedente esempio con i valori predefiniti di hello è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| modResult | int | 1 |

<a id="mul" />

## <a name="mul"></a>mul
`mul(operand1, operand2)`

Restituisce hello moltiplicazione di due interi fornito di hello.

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| operand1 |Sì |int |Primo numero toomultiply. |
| operand2 |Sì |int |Secondo numero toomultiply. |

### <a name="return-value"></a>Valore restituito

Una numero intero che rappresenta hello la moltiplicazione.

### <a name="example"></a>Esempio

Hello di esempio seguente moltiplica un parametro da un altro parametro.

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

Hello output di hello precedente esempio con i valori predefiniti di hello è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| mulResult | int | 15 |

<a id="sub" />

## <a name="sub"></a>sub
`sub(operand1, operand2)`

Restituisce hello sottrazione di due interi fornito di hello.

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| operand1 |Sì |int |numero di Hello che viene sottratto. |
| operand2 |Sì |int |numero di Hello che viene sottratto. |

### <a name="return-value"></a>Valore restituito
Una numero intero che rappresenta hello la sottrazione.

### <a name="example"></a>Esempio

Hello di esempio seguente sottrae un parametro da un altro parametro.

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

Hello output di hello precedente esempio con i valori predefiniti di hello è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| subResult | int | 4 |

## <a name="next-steps"></a>Passaggi successivi
* Per una descrizione delle sezioni hello in un modello di gestione risorse di Azure, vedere [modelli Authoring Azure Resource Manager](resource-group-authoring-templates.md).
* toomerge più modelli, vedere [con modelli collegati con Azure Resource Manager](resource-group-linked-templates.md).
* tooiterate un numero specificato di volte durante la creazione di un tipo di risorsa, vedere [creare più istanze delle risorse in Azure Resource Manager](resource-group-create-multiple.md).
* toosee come modello hello toodeploy è stato creato, vedere [distribuire un'applicazione con il modello di gestione risorse di Azure](resource-group-template-deploy.md).

