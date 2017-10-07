---
title: funzioni di modello di gestione risorse aaaAzure - confronto | Documenti Microsoft
description: Viene descritto toouse funzioni hello un valori toocompare modello di gestione risorse di Azure.
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
ms.openlocfilehash: ebcfc9ed6c93f8b540ec4c066e9457c621800b7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="comparison-functions-for-azure-resource-manager-templates"></a>Funzioni di confronto per i modelli di Azure Resource Manager

Resource Manager include numerose funzioni per l'esecuzione di confronti nei modelli.

* [equals](#equals)
* [greater](#greater)
* [greaterOrEquals](#greaterorequals)
* [less](#less)
* [lessOrEquals](#lessorequals)

## <a name="equals"></a>equals
`equals(arg1, arg2)`

Controlla se due valori sono uguali tra loro.

### <a name="parameters"></a>Parametri

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| arg1 |Sì |int, stringa, matrice o oggetto |Hello primo valore toocheck per verificarne l'uguaglianza. |
| arg2 |Sì |int, stringa, matrice o oggetto |Hello secondo valore toocheck per verificarne l'uguaglianza. |

### <a name="return-value"></a>Valore restituito

Restituisce **True** se hello valori sono uguali; in caso contrario, **False**.

### <a name="remarks"></a>Osservazioni

Hello funzione equals viene spesso usato con hello `condition` tootest elemento che viene implementata una risorsa.

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

### <a name="example"></a>Esempio

modello di esempio Hello controlla i tipi diversi di valori per verificarne l'uguaglianza. Tutti i valori predefiniti di hello restituiscono True.

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

Hello output di hello precedente esempio con i valori predefiniti di hello è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| checkInts | Booleano | True  |
| checkStrings | Booleano | True  |
| checkArrays | Booleano | True  |
| checkObjects | Booleano | True  |


Hello seguente utilizza [non](resource-group-template-functions-logical.md#not) con **è uguale a**.

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

output di Hello hello sopra riportato è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| checkNotEquals | Booleano | True  |


## <a name="greater"></a>greater
`greater(arg1, arg2)`

Controlla se il primo valore di hello è maggiore del secondo valore hello.

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| arg1 |Sì |int o stringa |primo valore Hello per confronto maggiore di hello. |
| arg2 |Sì |int o stringa |secondo valore Hello per confronto maggiore di hello. |

### <a name="return-value"></a>Valore restituito

Restituisce **True** se hello primo valore è maggiore del secondo valore hello; in caso contrario, **False**.

### <a name="example"></a>Esempio

modello di esempio Hello controlla se un valore di hello è maggiore di hello altri.

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

Hello output di hello precedente esempio con i valori predefiniti di hello è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| checkInts | Booleano | False |
| checkStrings | Booleano | True  |


## <a name="greaterorequals"></a>greaterOrEquals
`greaterOrEquals(arg1, arg2)`

Controlla se hello primo valore è maggiore o uguale toohello secondo valore.

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| arg1 |Sì |int o stringa |primo valore Hello per il confronto maggiore o uguale di hello. |
| arg2 |Sì |int o stringa |secondo valore Hello per il confronto maggiore o uguale di hello. |

### <a name="return-value"></a>Valore restituito

Restituisce **True** se hello primo valore è maggiore o uguale toohello secondo; in caso contrario, **False**.

### <a name="example"></a>Esempio

modello di esempio Hello controlla se un valore di hello è maggiore o uguale toohello altri.

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

Hello output di hello precedente esempio con i valori predefiniti di hello è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| checkInts | Booleano | False |
| checkStrings | Booleano | True  |



## <a name="less"></a>less
`less(arg1, arg2)`

Controlla se hello primo valore è minore di hello secondo valore.

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| arg1 |Sì |int o stringa |primo valore Hello per hello meno confronto. |
| arg2 |Sì |int o stringa |secondo valore Hello per hello meno confronto. |

### <a name="return-value"></a>Valore restituito

Restituisce **True** se hello primo valore è minore di hello secondo valore; in caso contrario, **False**.

### <a name="example"></a>Esempio

modello di esempio Hello controlla se un valore di hello è minore di hello altri.

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

Hello output di hello precedente esempio con i valori predefiniti di hello è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| checkInts | Booleano | True  |
| checkStrings | Booleano | False |


## <a name="lessorequals"></a>lessOrEquals
`lessOrEquals(arg1, arg2)`

Controlla se il primo valore di hello è minore o uguale toohello secondo valore.

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| arg1 |Sì |int o stringa |Hello primo valore per hello minore o uguale a confronto. |
| arg2 |Sì |int o stringa |secondo valore di Hello per hello minore o uguale a confronto. |

### <a name="return-value"></a>Valore restituito

Restituisce **True** se hello primo valore è minore o uguale toohello secondo valore; in caso contrario, **False**.

### <a name="example"></a>Esempio

Hello modello di esempio controlla se un valore di hello è minore o uguale toohello altri.

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

Hello output di hello precedente esempio con i valori predefiniti di hello è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| checkInts | Booleano | True  |
| checkStrings | Booleano | False |



## <a name="next-steps"></a>Passaggi successivi
* Per una descrizione delle sezioni hello in un modello di gestione risorse di Azure, vedere [modelli Authoring Azure Resource Manager](resource-group-authoring-templates.md).
* toomerge più modelli, vedere [con modelli collegati con Azure Resource Manager](resource-group-linked-templates.md).
* tooiterate un numero specificato di volte durante la creazione di un tipo di risorsa, vedere [creare più istanze delle risorse in Azure Resource Manager](resource-group-create-multiple.md).
* toosee come modello hello toodeploy è stato creato, vedere [distribuire un'applicazione con il modello di gestione risorse di Azure](resource-group-template-deploy.md).

