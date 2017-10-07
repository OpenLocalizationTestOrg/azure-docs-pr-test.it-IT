---
title: aaaDeploy risorse tooAzure | Documenti Microsoft
description: Usare Azure PowerShell o l'interfaccia CLI di Azure tooAzure risorse toodeploy. risorse di Hello vengono definite in un modello di gestione risorse.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/16/2017
ms.author: tomfitz
ms.openlocfilehash: 0cd3f8ad45af1fb85c78899b56f6807d00b859f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-tooazure"></a>Distribuire le risorse tooAzure

Questo argomento viene illustrato come toodeploy risorse tooyour sottoscrizione di Azure. È possibile usare Azure PowerShell o Azure CLI toodeploy un modello di gestione risorse che definisce l'infrastruttura di hello per la soluzione.

Per un'introduzione tooconcepts di gestione risorse, vedere [Panoramica di gestione risorse di Azure](resource-group-overview.md).

## <a name="steps-for-deployment"></a>Procedura per la distribuzione

In questo argomento si presuppone che si sta distribuendo hello [modello di archiviazione di esempio](#example-storage-template) in questo argomento. È possibile utilizzare un modello diverso, ma i parametri di hello che passare sono diversi rispetto a quanto mostrato in questo argomento.

Dopo aver creato un modello, hello generale per la distribuzione del modello di passaggi:

1. Accedi tooyour account
2. Selezionare toouse sottoscrizione hello (necessario solo se si dispone di più sottoscrizioni e si desidera toouse uno che non sia sottoscrizione predefinita hello)
3. Creare un gruppo di risorse
4. Distribuire il modello di hello
5. Controllare lo stato della distribuzione

Hello nelle sezioni seguenti mostrano come tooperform tali passaggi con [PowerShell](#powershell) o [CLI di Azure](#azure-cli).

## <a name="powershell"></a>PowerShell

1. tooinstall Azure PowerShell, vedere [Introduzione ai cmdlet di Azure PowerShell](/powershell/azure/overview).

2. tooquickly Introduzione alla distribuzione, utilizzare hello seguente cmdlet:

  ```powershell
  Login-AzureRmAccount
  Set-AzureRmContext -SubscriptionID {subscription-id}

  New-AzureRmResourceGroup -Name ExampleGroup -Location "Central US"
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json 
  ```

  Hello `Set-AzureRmContext` cmdlet è necessario solo se si desidera toouse una sottoscrizione diversa da abbonamento predefinito. toosee tutte le sottoscrizioni e i relativi ID, utilizzare:

  ```powershell
  Get-AzureRmSubscription
  ```

3. distribuzione di Hello può richiedere alcuni minuti toocomplete. Al termine, viene visualizzato un messaggio simile a:

  ```powershell
  DeploymentName          : ExampleDeployment
  CorrelationId           : 07b3b233-8367-4a0b-b9bc-7aa189065665
  ResourceGroupName       : ExampleGroup
  ProvisioningState       : Succeeded
  ...
  ```

4. toosee che l'account di archiviazione e di gruppo di risorse sono stati distribuiti tooyour sottoscrizione, utilizzare:

  ```powershell
  Get-AzureRmResourceGroup -Name ExampleGroup
  Find-AzureRmResource -ResourceGroupNameEquals ExampleGroup
  ```

5. Quando si distribuisce un modello, è possibile specificare i parametri del modello come parametri di PowerShell. Hello l'esempio precedente non include alcun parametro di modello, pertanto sono stati utilizzati i valori predefiniti di hello nel modello di hello. toodeploy archiviazione un altro account e specificare i valori dei parametri per prefisso del nome di archiviazione hello e account di archiviazione hello SKU, utilizzare:

  ```powershell
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment2 -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json -storageNamePrefix "contoso" -storageSKU "Standard_GRS"
  ```

  Si dispone ora di due account di archiviazione nel gruppo di risorse. 

## <a name="azure-cli"></a>Interfaccia della riga di comando di Azure

1. tooinstall CLI di Azure, vedere [installare Azure CLI 2.0](/cli/azure/install-az-cli2).

2. tooquickly Introduzione alla distribuzione, utilizzare hello seguenti comandi:

  ```azurecli
  az login
  az account set --subscription {subscription-id}

  az group create --name ExampleGroup --location "Central US"
  az group deployment create --name ExampleDeployment --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json
  ```

  Hello `az account set` comando è necessario solo se si desidera toouse una sottoscrizione diversa da abbonamento predefinito. toosee tutte le sottoscrizioni e i relativi ID, utilizzare:

  ```azurecli
  az account list
  ```

3. distribuzione di Hello può richiedere alcuni minuti toocomplete. Al termine, viene visualizzato un messaggio simile a:

  ```azurecli
  "provisioningState": "Succeeded",
  ```

4. toosee che l'account di archiviazione e di gruppo di risorse sono stati distribuiti tooyour sottoscrizione, utilizzare:

  ```azurecli
  az group show --name ExampleGroup
  az resource list --resource-group ExampleGroup
  ```

5. Quando si distribuisce un modello, è possibile specificare i parametri del modello come parametri di PowerShell. Hello l'esempio precedente non include alcun parametro di modello, pertanto sono stati utilizzati i valori predefiniti di hello nel modello di hello. toodeploy archiviazione un altro account e specificare i valori dei parametri per prefisso del nome di archiviazione hello e account di archiviazione hello SKU, utilizzare:

  ```azurecli
  az group deployment create --name ExampleDeployment2 --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json --parameters '{"storageNamePrefix":{"value":"contoso"},"storageSKU":{"value":"Standard_GRS"}}'
  ```

  Si dispone ora di due account di archiviazione nel gruppo di risorse. 

## <a name="example-storage-template"></a>Modello di archiviazione di esempio

Utilizzare hello seguente modello di esempio toodeploy sottoscrizione tooyour un account di archiviazione:

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "hello value toouse for starting hello storage account name."
      }
    },
    "storageSKU": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_ZRS",
        "Standard_GRS",
        "Standard_RAGRS",
        "Premium_LRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "hello type of replication toouse for hello storage account."
      }
    }
  },
  "variables": {
    "storageName": "[concat(parameters('storageNamePrefix'), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-05-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {  }
}
```

## <a name="next-steps"></a>Passaggi successivi

* Per informazioni dettagliate sull'utilizzo di PowerShell toodeploy modelli, vedere [distribuire le risorse e modelli di gestione risorse di Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy).
* Per informazioni dettagliate sull'utilizzo dei modelli toodeploy CLI di Azure, vedere [distribuire le risorse con i modelli di gestione risorse e CLI di Azure](/azure/azure-resource-manager/resource-group-template-deploy-cli).



