---
title: modello di gestione risorse aaaExport con CLI di Azure | Documenti Microsoft
description: Utilizzare Gestione risorse di Azure e Azure CLI tooexport un modello da un gruppo di risorse.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/01/2017
ms.author: tomfitz
ms.openlocfilehash: 2d44a0a6e9717504d4c2a01254d826679b381f22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="export-azure-resource-manager-templates-with-azure-cli"></a>Esportare il modello di Azure Resource Manager con l'interfaccia della riga di comando di Azure

Gestione risorse consente tooexport un modello di gestione risorse da risorse esistenti nella sottoscrizione. È possibile utilizzare tale toolearn modello generato su hello modello tooautomate o la sintassi di hello ridistribuzione della soluzione in base alle esigenze.

È importante toonote che non esistono due modi diversi tooexport un modello:

* È possibile esportare modello hello effettivo utilizzato per una distribuzione. modello esportato Hello include tutti i parametri di hello e variabili, esattamente come appaiono nel modello originale hello. Questo approccio è utile quando è necessario tooretrieve un modello.
* È possibile esportare un modello che rappresenta lo stato corrente di hello hello del gruppo di risorse. modello esportato Hello non è basato su qualsiasi modello utilizzato per la distribuzione. Al contrario, viene creato un modello che è uno snapshot hello del gruppo di risorse. modello esportato Hello molti valori hardcoded e probabilmente non tutti i parametri in genere è possibile definire. Questo approccio è utile quando è stato modificato il gruppo di risorse hello. A questo punto, è necessario gruppo di risorse hello toocapture come modello.

Questo argomento illustra entrambi gli approcci.

## <a name="deploy-a-solution"></a>Distribuire una soluzione

Per iniziare la distribuzione di una sottoscrizione di tooyour soluzione tooillustrate entrambi approcci per l'esportazione di un modello. Se si dispone già di un gruppo di risorse nella sottoscrizione che si desidera tooexport, non si dispone toodeploy questa soluzione. Tuttavia, il resto di hello di questo articolo si riferisce toohello modello per questa soluzione. lo script di esempio Hello distribuisce un account di archiviazione.

```azurecli
az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name NewStorage \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
```  

## <a name="save-template-from-deployment-history"></a>Salvare un modello dalla cronologia di distribuzione

È possibile recuperare un modello dalla cronologia distribuzione tramite hello [esportazione distribuzione gruppo di az](/cli/azure/group/deployment#export) comando. Hello dopo esempio Salva hello template che si distribuisce in precedenza:

```azurecli
az group deployment export --name NewStorage --resource-group ExampleGroup
```

Restituisce il modello di hello. Copiare hello JSON e salvare come file. Si noti che modello di esatta hello che è utilizzato per la distribuzione. variabili e parametri hello corrispondano il modello di hello da GitHub. È possibile ridistribuire il modello.


## <a name="export-resource-group-as-template"></a>Esportare un gruppo di risorse come modello

Invece di recuperare un modello dalla cronologia della distribuzione di hello, è possibile recuperare un modello che rappresenta lo stato corrente di hello di un gruppo di risorse utilizzando hello [esportazione gruppo az](/cli/azure/group#export) comando. Utilizzare questo comando quando sono state apportate molte gruppo di risorse tooyour modifiche e nessun modello esistente rappresenta tutte le modifiche di hello.

```azurecli
az group export --name ExampleGroup
```

Restituisce il modello di hello. Copiare hello JSON e salvare come file. Si noti che è diverso dal modello hello in GitHub. Contiene parametri diversi e non include variabili. archiviazione Hello SKU e la posizione sono hardcoded toovalues. Hello esempio seguente viene illustrato il modello esportato di hello, ma per il modello è un nome di parametro leggermente diverso:

```json
{
  "parameters": {
    "storageAccounts_mcyzaljiv7qncstandardsa_name": {
      "type": "String",
      "defaultValue": null
    }
  },
  "variables": {},
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "resources": [
    {
      "tags": {},
      "dependsOn": [],
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "Standard_LRS",
        "tier": "Standard"
      },
      "kind": "Storage",
      "type": "Microsoft.Storage/storageAccounts",
      "location": "centralus",
      "name": "[parameters('storageAccounts_mcyzaljiv7qncstandardsa_name')]",
      "properties": {}
    }
  ],
  "contentVersion": "1.0.0.0"
}
```

È possibile ridistribuire il modello, ma richiede l'individuazione di un nome univoco per l'account di archiviazione hello. nome Hello del parametro è leggermente diversa.

```azurecli
az group deployment create --name NewStorage --resource-group ExampleGroup \
  --template-file examplegroup.json \
  --parameters "{\"storageAccounts_mcyzaljiv7qncstandardsa_name\":{\"value\":\"tfstore0501\"}}"
```

## <a name="customize-exported-template"></a>Personalizzare il modello esportato

È possibile modificare questo modello toomake è toouse più semplice e più flessibile. tooallow per più percorsi, modifica hello percorso proprietà toouse hello stesso percorso del gruppo di risorse hello:

```json
"location": "[resourceGroup().location]",
```

tooavoid con tooguess nome univoche per l'account di archiviazione, il parametro hello remove per il nome di account di archiviazione hello. Aggiungere un parametro per il suffisso del nome di archiviazione e uno SKU di archiviazione:

```json
"parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
},
```

Aggiungere una variabile che costruisce nome account di archiviazione hello con funzione uniqueString hello:

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

Impostare il nome di hello della variabile toohello account di archiviazione hello:

```json
"name": "[variables('storageAccountName')]",
```

Impostare hello SKU toohello parametro:

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

Il modello si presenta ora come segue:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), parameters('storageSuffix'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "sku": {
        "name": "[parameters('storageAccountType')]",
        "tier": "Standard"
      },
      "kind": "Storage",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {},
      "dependsOn": []
    }
  ]
}
```

Ridistribuire modello modificato hello.

## <a name="next-steps"></a>Passaggi successivi
* Per informazioni sull'utilizzo di hello portale tooexport un modello, vedere [esportare un modello di gestione risorse di Azure da risorse esistenti](resource-manager-export-template.md).
* toodefine i parametri di modello, vedere [creazione di modelli](resource-group-authoring-templates.md#parameters).
* Per suggerimenti su come risolvere i comuni errori di distribuzione, vedere [Risolvere errori comuni durante la distribuzione di risorse in Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).