---
title: funzioni di modello di gestione risorse aaaAzure - distribuzione | Documenti Microsoft
description: Viene descritto toouse funzioni hello in un'informazioni sulla distribuzione di Azure Resource Manager modello tooretrieve.
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
ms.openlocfilehash: 458c3f740504fdd6799ed24cc386219726737636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-functions-for-azure-resource-manager-templates"></a>Funzioni di distribuzione per i modelli di Azure Resource Manager 

Gestione risorse offre seguente hello funzioni per ottenere valori dalle sezioni del modello di hello e valori correlati toohello distribuzione:

* [deployment](#deployment)
* [parameters](#parameters)
* [variables](#variables)

i valori di tooget di risorse, gruppi di risorse o le sottoscrizioni, vedere [le funzioni della risorsa](resource-group-template-functions-resource.md).

<a id="deployment" />

## <a name="deployment"></a>distribuzione
`deployment()`

Restituisce informazioni sull'operazione di distribuzione corrente di hello.

### <a name="return-value"></a>Valore restituito

Questa funzione restituisce l'oggetto hello passato durante la distribuzione. proprietà Hello in hello restituito oggetto variano in base al fatto hello distribuzione oggetto viene passato come un collegamento o come un oggetto in linea. Oggetto di distribuzione hello viene passato quando in linea, ad esempio quando si utilizza hello **- TemplateFile** parametro nel file locale tooa toopoint Azure PowerShell, hello restituito l'oggetto ha hello seguente formato:

```json
{
    "name": "",
    "properties": {
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [
            ],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

Quando oggetto hello viene passato come un collegamento, ad esempio quando utilizzando hello **- TemplateUri** dell'oggetto parametro toopoint tooa remoto hello viene restituito in hello seguente formato: 

```json
{
    "name": "",
    "properties": {
        "templateLink": {
            "uri": ""
        },
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

### <a name="remarks"></a>Osservazioni

È possibile utilizzare una distribuzione () toolink tooanother modello basato su URI del modello padre hello hello.

```json
"variables": {  
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"  
}
```  

### <a name="example"></a>Esempio

Hello esempio seguente viene restituito oggetto distribuzione hello:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[deployment()]",
            "type" : "object"
        }
    }
}
```

Hello esempio precedente restituisce hello seguente oggetto:

```json
{
  "name": "deployment",
  "properties": {
    "template": {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "resources": [],
      "outputs": {
        "subscriptionOutput": {
          "type": "Object",
          "value": "[deployment()]"
        }
      }
    },
    "parameters": {},
    "mode": "Incremental",
    "provisioningState": "Accepted"
  }
}
```

<a id="parameters" />

## <a name="parameters"></a>parameters
`parameters(parameterName)`

Restituisce un valore di parametro. nome del parametro specificato Hello deve essere definito nella sezione parametri hello del modello di hello.

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| parameterName |Sì |string |nome Hello del tooreturn parametro hello. |

### <a name="return-value"></a>Valore restituito

parametro specificato il valore Hello hello.

### <a name="remarks"></a>Osservazioni

In genere, si utilizzano valori dei parametri tooset risorse. Hello esempio seguente imposta il nome di hello del sito web toohello valore del parametro passato durante la distribuzione.

```json
"parameters": { 
  "siteName": {
      "type": "string"
  }
},
"resources": [
   {
      "apiVersion": "2016-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/Sites",
      ...
   }
]
```

### <a name="example"></a>Esempio

Hello seguente viene illustrato un utilizzo della funzione parametri hello semplificato.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringParameter": {
            "type" : "string",
            "defaultValue": "option 1"
        },
        "intParameter": {
            "type": "int",
            "defaultValue": 1
        },
        "objectParameter": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b"}
        },
        "arrayParameter": {
            "type": "array",
            "defaultValue": [1, 2, 3]
        },
        "crossParameter": {
            "type": "string",
            "defaultValue": "[parameters('stringParameter')]"
        }
    },
    "variables": {},
    "resources": [],
    "outputs": {
        "stringOutput": {
            "value": "[parameters('stringParameter')]",
            "type" : "string"
        },
        "intOutput": {
            "value": "[parameters('intParameter')]",
            "type" : "int"
        },
        "objectOutput": {
            "value": "[parameters('objectParameter')]",
            "type" : "object"
        },
        "arrayOutput": {
            "value": "[parameters('arrayParameter')]",
            "type" : "array"
        },
        "crossOutput": {
            "value": "[parameters('crossParameter')]",
            "type" : "string"
        }
    }
}
```

Hello output di hello precedente esempio con i valori predefiniti di hello è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| stringOutput | String | option 1 |
| intOutput | int | 1 |
| objectOutput | Oggetto | {"one": "a", "two": "b"} |
| arrayOutput | Array | [1, 2, 3] |
| crossOutput | String | option 1 |

<a id="variables" />

## <a name="variables"></a>variables
`variables(variableName)`

Restituisce hello valore della variabile. nome di variabile specificato Hello deve essere definito nella sezione variabili hello del modello di hello.

### <a name="parameters"></a>parameters

| Parametro | Obbligatorio | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| variableName |Sì |String |nome Hello del tooreturn variabile hello. |

### <a name="return-value"></a>Valore restituito

valore di Hello della variabile specificata hello.

### <a name="remarks"></a>Osservazioni

In genere utilizzata toosimplify variabili del modello creando una sola volta valori complessi. Hello seguente esempio crea un nome univoco per un account di archiviazione.

```json
"variables": {
    "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
},
"resources": [
    {
        "type": "Microsoft.Storage/storageAccounts",
        "name": "[variables('storageName')]",
        ...
    },
    {
        "type": "Microsoft.Compute/virtualMachines",
        "dependsOn": [
            "[variables('storageName')]"
        ],
        ...
    }
],
```

### <a name="example"></a>Esempio

modello di esempio Hello restituisce valori di variabili diversi.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "variables": {
        "var1": "myVariable",
        "var2": [ 1,2,3,4 ],
        "var3": "[ variables('var1') ]",
        "var4": {
            "property1": "value1",
            "property2": "value2"
        }
    },
    "resources": [],
    "outputs": {
        "exampleOutput1": {
            "value": "[variables('var1')]",
            "type" : "string"
        },
        "exampleOutput2": {
            "value": "[variables('var2')]",
            "type" : "array"
        },
        "exampleOutput3": {
            "value": "[variables('var3')]",
            "type" : "string"
        },
        "exampleOutput4": {
            "value": "[variables('var4')]",
            "type" : "object"
        }
    }
}
```

Hello output di hello precedente esempio con i valori predefiniti di hello è:

| Nome | Tipo | Valore |
| ---- | ---- | ----- |
| exampleOutput1 | String | myVariable |
| exampleOutput2 | Array | [1, 2, 3, 4] |
| exampleOutput3 | String | myVariable |
| exampleOutput4 |  Oggetto | {"property1": "value1", "property2": "value2"} |

## <a name="next-steps"></a>Passaggi successivi
* Per una descrizione delle sezioni hello in un modello di gestione risorse di Azure, vedere [modelli Authoring Azure Resource Manager](resource-group-authoring-templates.md).
* toomerge più modelli, vedere [con modelli collegati con Azure Resource Manager](resource-group-linked-templates.md).
* tooiterate un numero specificato di volte durante la creazione di un tipo di risorsa, vedere [creare più istanze delle risorse in Azure Resource Manager](resource-group-create-multiple.md).
* toosee come modello hello toodeploy è stato creato, vedere [distribuire un'applicazione con il modello di gestione risorse di Azure](resource-group-template-deploy.md).

