---
title: gruppi di risorse toomultiple aaaDeploy risorse di Azure | Documenti Microsoft
description: "Viene illustrato come raggruppare i tootarget più di una risorsa di Azure durante la distribuzione."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: tomfitz
ms.openlocfilehash: 93a39a26e0ca18dfcb5c6e8de95c38a64186d6de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-resources-toomore-than-one-resource-group"></a>Distribuire le risorse di Azure toomore rispetto a un gruppo di risorse

In genere, si distribuisce tutte le risorse di hello del modello tooa singolo gruppo di risorse. Tuttavia, esistono scenari in cui si desidera un set di risorse toodeploy insieme ma posizionarli in diversi gruppi di risorse. Ad esempio, è consigliabile toodeploy hello backup virtual machine per percorso e il gruppo di risorse distinto tooa Azure Site Recovery. Gestione risorse consente toouse annidati modelli tootarget diversi gruppi di risorse di gruppo di risorse hello usato per il modello padre hello.

gruppo di risorse Hello è il contenitore del ciclo di vita hello per un'applicazione hello e la relativa raccolta di risorse. Si crea il gruppo di risorse hello di fuori di modello hello e specificare hello risorsa gruppo tootarget durante la distribuzione. Per i gruppi di tooresource un'introduzione, vedere [Panoramica di gestione risorse di Azure](resource-group-overview.md).

## <a name="example-template"></a>Modello di esempio

tootarget una risorsa diversa, è necessario utilizzare un modello annidato o collegato durante la distribuzione. Hello `Microsoft.Resources/deployments` fornisce un `resourceGroup` parametro che consente di toospecify un gruppo di risorse diversi per hello annidati di distribuzione. Tutti i gruppi di risorse hello devono esistere prima di eseguire la distribuzione di hello. esempio Hello distribuisce due account di archiviazione - in gruppo di risorse hello specificato durante la distribuzione e uno in un gruppo di risorse denominato `crossResourceGroupDeployment`:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "StorageAccountName1": {
            "type": "string"
        },
        "StorageAccountName2": {
            "type": "string"
        }
    },
    "variables": {},
    "resources": [
        {
            "apiVersion": "2017-05-10",
            "name": "nestedTemplate",
            "type": "Microsoft.Resources/deployments",
            "resourceGroup": "crossResourceGroupDeployment",
            "properties": {
                "mode": "Incremental",
                "template": {
                    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
                    "contentVersion": "1.0.0.0",
                    "parameters": {},
                    "variables": {},
                    "resources": [
                        {
                            "type": "Microsoft.Storage/storageAccounts",
                            "name": "[parameters('StorageAccountName2')]",
                            "apiVersion": "2015-06-15",
                            "location": "West US",
                            "properties": {
                                "accountType": "Standard_LRS"
                            }
                        }
                    ]
                },
                "parameters": {}
            }
        },
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('StorageAccountName1')]",
            "apiVersion": "2015-06-15",
            "location": "West US",
            "properties": {
                "accountType": "Standard_LRS"
            }
        }
    ]
}
```

Se si imposta `resourceGroup` toohello nome di un gruppo di risorse che non esiste, hello distribuzione non riesce. Se non si specifica un valore per `resourceGroup`, Gestione risorse Usa gruppo di risorse padre hello.  

## <a name="deploy-hello-template"></a>Distribuire il modello di hello

modello di esempio hello toodeploy, è possibile utilizzare il portale di hello, Azure PowerShell o CLI di Azure. Per Azure PowerShell o l'interfaccia della riga di comando di Azure è necessario usare una versione di maggio 2017 o successiva. Negli esempi di Hello si presuppone di aver salvato il modello di hello in locale come un file denominato **crossrgdeployment.json**.

Per PowerShell:

```powershell
Login-AzureRmAccount

New-AzureRmResourceGroup -Name mainResourceGroup -Location "South Central US"
New-AzureRmResourceGroup -Name crossResourceGroupDeployment -Location "Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName mainResourceGroup `
  -TemplateFile c:\MyTemplates\crossrgdeployment.json
```

Per l'interfaccia della riga di comando di Azure:

```azurecli
az login

az group create --name mainResourceGroup --location "South Central US"
az group create --name crossResourceGroupDeployment --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group mainResourceGroup \
    --template-file crossrgdeployment.json
```

Al termine della distribuzione, vengono visualizzati due gruppi di risorse. Ogni gruppo di risorse contiene un account di archiviazione.

## <a name="use-resourcegroup-function"></a>Usare la funzione resourceGroup()

Per attraversare distribuzioni del gruppo di risorse hello [resouceGroup() funzione](resource-group-template-functions-resource.md#resourcegroup) viene risolta in base alle modalità modello nidificato hello utilizzata per specificare. 

Se si incorpora un modello all'interno di un altro modello, resouceGroup() nel modello annidato hello risolve toohello gruppo di risorse padre. Un modello incorporato utilizza hello seguente formato:

```json
"apiVersion": "2017-05-10",
"name": "embeddedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "template": {
        ...
        resourceGroup() refers tooparent resource group
    }
}
```

Se si collega modello separato tooa, resouceGroup() nel modello collegato hello risolve il gruppo di risorse annidati di toohello. Un modello collegato utilizza hello seguente formato:

```json
"apiVersion": "2017-05-10",
"name": "linkedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "templateLink": {
        ...
        resourceGroup() in linked template refers toolinked resource group
    }
}
```

## <a name="next-steps"></a>Passaggi successivi

* toounderstand toodefine parametri nel modello, vedere [comprendere hello struttura e la sintassi dei modelli di Azure Resource Manager](resource-group-authoring-templates.md).
* Per suggerimenti su come risolvere i comuni errori di distribuzione, vedere [Risolvere errori comuni durante la distribuzione di risorse in Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).
* Per informazioni sulla distribuzione di un modello che richiede un token di firma di accesso condiviso, vedere [Distribuire un modello privato con un token di firma di accesso condiviso](resource-manager-powershell-sas-token.md).
