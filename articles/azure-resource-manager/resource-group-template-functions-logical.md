---
title: aaaAzure Gestione risorse funzioni di modello - logiche | Documenti Microsoft
description: Viene descritto toouse funzioni hello in un valori logici di modello toodetermine Gestione risorse di Azure.
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
ms.openlocfilehash: aec6341fbde00b4eba3b4539ff9a9aec774333fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="logical-functions-for-azure-resource-manager-templates"></a>Funzioni logiche nei modelli di Azure Resource Manager

Resource Manager include numerose funzioni per l'esecuzione di confronti nei modelli.

* [and](#and)
* [bool](#bool)
* [if](#if)
* [not](#not)
* [or](#or)

## <a name="and"></a>e
`and(arg1, arg2)`

Controlla se i valori di entrambi i parametri sono true.

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| arg1 |Sì |boolean |Hello toocheck valore primo se è true. |
| arg2 |Sì |boolean |Hello toocheck valore secondo se è true. |

### <a name="return-value"></a>Valore restituito

Restituisce **True** se entrambi i valori sono true. In caso contrario, restituisce **False**.

### <a name="examples"></a>esempi

Hello seguente esempio viene illustrato come le funzioni logiche toouse.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

output di Hello hello sopra riportato è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| andExampleOutput | Booleano | False |
| orExampleOutput | Booleano | True  |
| notExampleOutput | Booleano | False |


## <a name="bool"></a>bool
`bool(arg1)`

Converte hello tooa parametro booleano.

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| arg1 |Sì |stringa o numero intero |Hello tooa tooconvert valore booleano. |

### <a name="return-value"></a>Valore restituito
Un valore booleano di hello valore convertito.

### <a name="examples"></a>esempi

Hello seguente esempio viene illustrato come toouse bool con un numero intero o stringa.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "trueString": {
            "value": "[bool('true')]",
            "type" : "bool"
        },
        "falseString": {
            "value": "[bool('false')]",
            "type" : "bool"
        },
        "trueInt": {
            "value": "[bool(1)]",
            "type" : "bool"
        },
        "falseInt": {
            "value": "[bool(0)]",
            "type" : "bool"
        }
    }
}
```

Hello output di hello precedente esempio con i valori predefiniti di hello è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| trueString | Booleano | True  |
| falseString | Booleano | False |
| trueInt | Booleano | True  |
| falseInt | Booleano | False |

## <a name="if"></a>if
`if(condition, trueValue, falseValue)`

Restituisce un valore in base a un condizione true o false.

### <a name="parameters"></a>Parametri

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| condition |Sì |boolean |Hello toocheck valore se è true. |
| trueValue |Sì | string, int, object o array |valore di Hello tooreturn quando hello condizione è true. |
| falseValue |Sì | string, int, object o array |valore di Hello tooreturn quando hello condizione è false. |

### <a name="return-value"></a>Valore restituito

Restituisce il secondo parametro, quando il primo parametro è **True**. In caso contrario, restituisce il terzo parametro.

### <a name="remarks"></a>Osservazioni

È possibile utilizzare questo set di funzioni tooconditionally una proprietà della risorsa. Hello seguente non è un modello completo, ma visualizza parti pertinenti di hello per l'impostazione di set di disponibilità hello in modo condizionale.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "availabilitySet": {
            "type": "string",
            "allowedValues": [
                "yes",
                "no"
            ]
        }
    },
    "variables": {
        ...
        "availabilitySetName": "availabilitySet1",
        "availabilitySet": {
            "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
        }
    },
    "resources": [
        {
            "condition": "[equals(parameters('availabilitySet'),'yes')]",
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            ...
        },
        {
            "apiVersion": "2016-03-30",
            "type": "Microsoft.Compute/virtualMachines",
            "properties": {
                "availabilitySet": "[if(equals(parameters('availabilitySet'),'yes'), variables('availabilitySet'), json('null'))]",
                ...
            }
        },
        ...
    ],
    ...
}
```

### <a name="examples"></a>esempi

Hello seguente esempio viene illustrato come hello toouse `if` (funzione).

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "yesOutput": {
            "type": "string",
            "value": "[if(equals('a', 'a'), 'yes', 'no')]"
        },
        "noOutput": {
            "type": "string",
            "value": "[if(equals('a', 'b'), 'yes', 'no')]"
        }
    }
}
```

output di Hello hello sopra riportato è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| yesOutput | String | sì |
| noOutput | String | no |


## <a name="not"></a>not
`not(arg1)`

Converte un valore booleano tooits opposto valore.

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| arg1 |Sì |boolean |tooconvert valore Hello. |


### <a name="return-value"></a>Valore restituito

Restituisce **True** quando il parametro è **False**. Restituisce **False** quando il parametro è **True**.

### <a name="examples"></a>esempi

Hello seguente esempio viene illustrato come le funzioni logiche toouse.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

output di Hello hello sopra riportato è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| andExampleOutput | Booleano | False |
| orExampleOutput | Booleano | True  |
| notExampleOutput | Booleano | False |

Hello seguente utilizza **non** con [è uguale a](resource-group-template-functions-comparison.md#equals).

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


## <a name="or"></a>oppure
`or(arg1, arg2)`

Controlla se il valore di uno dei due parametri è true.

### <a name="parameters"></a>Parametri

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| arg1 |Sì |boolean |Hello toocheck valore primo se è true. |
| arg2 |Sì |boolean |Hello toocheck valore secondo se è true. |

### <a name="return-value"></a>Valore restituito

Restituisce **True** se uno dei due valori è true. In caso contrario, restituisce **False**.

### <a name="examples"></a>esempi

Hello seguente esempio viene illustrato come le funzioni logiche toouse.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

output di Hello hello sopra riportato è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| andExampleOutput | Booleano | False |
| orExampleOutput | Booleano | True  |
| notExampleOutput | Booleano | False |


## <a name="next-steps"></a>Passaggi successivi
* Per una descrizione delle sezioni hello in un modello di gestione risorse di Azure, vedere [modelli Authoring Azure Resource Manager](resource-group-authoring-templates.md).
* toomerge più modelli, vedere [con modelli collegati con Azure Resource Manager](resource-group-linked-templates.md).
* tooiterate un numero specificato di volte durante la creazione di un tipo di risorsa, vedere [creare più istanze delle risorse in Azure Resource Manager](resource-group-create-multiple.md).
* toosee come modello hello toodeploy è stato creato, vedere [distribuire un'applicazione con il modello di gestione risorse di Azure](resource-group-template-deploy.md).

