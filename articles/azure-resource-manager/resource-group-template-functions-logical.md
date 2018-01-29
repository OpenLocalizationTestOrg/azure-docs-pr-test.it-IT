---
title: 'Funzioni del modello di Azure Resource Manager: logiche | Microsoft Docs'
description: "Informazioni sulle funzioni che è possibile usare in un modello di Azure Resource Manager per determinare i valori logici."
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
ms.date: 09/05/2017
ms.author: tomfitz
ms.openlocfilehash: d16264abf64ef88dfb24948fc04e33de619f4e3f
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
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
| arg1 |Sì |boolean |Primo valore da controllare per verificare se è true. |
| arg2 |Sì |boolean |Secondo valore da controllare per verificare se è true. |

### <a name="return-value"></a>Valore restituito

Restituisce **True** se entrambi i valori sono true. In caso contrario, restituisce **False**.

### <a name="examples"></a>esempi

Il [modello di esempio](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/andornot.json) seguente mostra come usare le funzioni logiche.

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

L'output dell'esempio precedente è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| andExampleOutput | Booleano | False |
| orExampleOutput | Booleano | True  |
| notExampleOutput | Booleano | False |

Per distribuire questo modello di esempio con l'interfaccia della riga di comando di Azure, usare:

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/andornot.json
```

Per distribuire questo modello di esempio con PowerShell, usare:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/andornot.json
```

## <a name="bool"></a>bool
`bool(arg1)`

Converte il parametro in un valore booleano.

### <a name="parameters"></a>Parametri

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| arg1 |Sì |Stringa o numero intero |Valore da convertire in un valore booleano. |

### <a name="return-value"></a>Valore restituito
Valore booleano del valore convertito.

### <a name="examples"></a>esempi

Il [modello di esempio](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/bool.json) seguente illustra come usare il parametro bool con un numero intero o una stringa.

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

L'output dell'esempio precedente con i valori predefiniti è il seguente:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| trueString | Booleano | True  |
| falseString | Booleano | False |
| trueInt | Booleano | True  |
| falseInt | Booleano | False |

Per distribuire questo modello di esempio con l'interfaccia della riga di comando di Azure, usare:

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/bool.json
```

Per distribuire questo modello di esempio con PowerShell, usare:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/bool.json
```

## <a name="if"></a>if
`if(condition, trueValue, falseValue)`

Restituisce un valore in base a un condizione true o false.

### <a name="parameters"></a>Parametri

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| condition |Sì |boolean |Valore da controllare per verificare se è true. |
| trueValue |Sì | string, int, object o array |Valore da restituire quando la condizione è true. |
| falseValue |Sì | string, int, object o array |Valore da restituire quando la condizione è false. |

### <a name="return-value"></a>Valore restituito

Restituisce il secondo parametro, quando il primo parametro è **True**. In caso contrario, restituisce il terzo parametro.

### <a name="remarks"></a>Osservazioni

È possibile usare questa funzione per impostare in modo condizionale una proprietà di una risorsa. L'esempio seguente non è un modello completo, ma mostra le sezioni rilevanti per l'impostazione condizionale del set di disponibilità.

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

Il [modello di esempio](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/if.json) seguente illustra come usare la funzione `if`.

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

L'output dell'esempio precedente è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| yesOutput | String | sì |
| noOutput | String | no |

Per distribuire questo modello di esempio con l'interfaccia della riga di comando di Azure, usare:

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/if.json
```

Per distribuire questo modello di esempio con PowerShell, usare:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/if.json
```

## <a name="not"></a>not
`not(arg1)`

Converte il valore booleano nel valore opposto.

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| arg1 |Sì |boolean |Valore da convertire. |

### <a name="return-value"></a>Valore restituito

Restituisce **True** quando il parametro è **False**. Restituisce **False** quando il parametro è **True**.

### <a name="examples"></a>esempi

Il [modello di esempio](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/andornot.json) seguente mostra come usare le funzioni logiche.

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

L'output dell'esempio precedente è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| andExampleOutput | Booleano | False |
| orExampleOutput | Booleano | True  |
| notExampleOutput | Booleano | False |

Per distribuire questo modello di esempio con l'interfaccia della riga di comando di Azure, usare:

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/andornot.json
```

Per distribuire questo modello di esempio con PowerShell, usare:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/andornot.json
```

Il [modello di esempio](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/not-equals.json) seguente usa **not** con [equals](resource-group-template-functions-comparison.md#equals).

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

L'output dell'esempio precedente è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| checkNotEquals | Booleano | True  |

Per distribuire questo modello di esempio con l'interfaccia della riga di comando di Azure, usare:

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/not-equals.json
```

Per distribuire questo modello di esempio con PowerShell, usare:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/not-equals.json
```

## <a name="or"></a>oppure
`or(arg1, arg2)`

Controlla se il valore di uno dei due parametri è true.

### <a name="parameters"></a>Parametri

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| arg1 |Sì |boolean |Primo valore da controllare per verificare se è true. |
| arg2 |Sì |boolean |Secondo valore da controllare per verificare se è true. |

### <a name="return-value"></a>Valore restituito

Restituisce **True** se uno dei due valori è true. In caso contrario, restituisce **False**.

### <a name="examples"></a>esempi

Il [modello di esempio](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/andornot.json) seguente mostra come usare le funzioni logiche.

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

L'output dell'esempio precedente è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| andExampleOutput | Booleano | False |
| orExampleOutput | Booleano | True  |
| notExampleOutput | Booleano | False |

Per distribuire questo modello di esempio con l'interfaccia della riga di comando di Azure, usare:

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/andornot.json
```

Per distribuire questo modello di esempio con PowerShell, usare:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/andornot.json
```

## <a name="next-steps"></a>Passaggi successivi
* Per una descrizione delle sezioni in un modello di Azure Resource Manager, vedere [Creazione di modelli di Azure Resource Manager](resource-group-authoring-templates.md).
* Per unire più modelli, vedere [Uso di modelli collegati con Azure Resource Manager](resource-group-linked-templates.md).
* Per eseguire un'iterazione di un numero di volte specificato durante la creazione di un tipo di risorsa, vedere [Creare più istanze di risorse in Gestione risorse di Azure](resource-group-create-multiple.md).
* Per informazioni su come distribuire il modello che è stato creato, vedere [Distribuire un'applicazione con un modello di Azure Resource Manager](resource-group-template-deploy.md).

