---
title: aaaDeploy risorse con PowerShell e modello | Documenti Microsoft
description: Utilizzare Gestione risorse di Azure e Azure PowerShell toodeploy un tooAzure di risorse. risorse di Hello vengono definite in un modello di gestione risorse.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 55903f35-6c16-4c6d-bf52-dbf365605c3f
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 41506811ba3c2ea5df6313db70978ade50f71161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-powershell"></a>Distribuire le risorse con i modelli di Azure Resource Manager e Azure PowerShell

Questo argomento viene illustrato come toouse Azure PowerShell con Gestione risorse modelli toodeploy tooAzure le risorse. Se non si ha familiarità con concetti hello della distribuzione e gestione di soluzioni di Azure, vedere [Panoramica di gestione risorse di Azure](resource-group-overview.md).

il modello di gestione risorse di Hello è distribuire può essere un file nel computer locale o un file esterno che si trova in un archivio come GitHub. modello Hello si distribuisce in questo articolo è disponibile in hello [modello di esempio](#sample-template) sezione, oppure come [modello di account di archiviazione in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

<a id="deploy-local-template" />

## <a name="deploy-a-template-from-your-local-machine"></a>Distribuire un modello dal computer locale

Quando si distribuisce tooAzure risorse, è:

1. Accedi tooyour account Azure
2. Creare un gruppo di risorse che funge da contenitore hello per le risorse di hello distribuito. nome Hello hello del gruppo di risorse possa includere solo caratteri alfanumerici, punti, caratteri di sottolineatura, trattini e parentesi. Può trattarsi di too90 caratteri. Non può terminare con un punto.
3. Distribuire toohello risorse gruppo hello modello che definisce hello risorse toocreate

Un modello può includere parametri che consentono la distribuzione di hello toocustomize. Può includere ad esempio valori specifici per un determinato ambiente (di sviluppo, test e produzione). modello di esempio Hello definisce un parametro per l'account di archiviazione hello SKU.

Hello di esempio seguente crea un gruppo di risorse e distribuisce un modello dal computer locale:

```powershell
Login-AzureRmAccount
 
New-AzureRmResourceGroup -Name ExampleResourceGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

distribuzione di Hello può richiedere alcuni minuti toocomplete. Al termine, viene visualizzato un messaggio che include i risultati di hello:

```powershell
ProvisioningState       : Succeeded
```

## <a name="deploy-a-template-from-an-external-source"></a>Distribuire un modello da un'origine esterna

Invece di archiviare i modelli di gestione risorse nel computer locale, è preferibile toostore multipla in una posizione esterna. ad esempio in un repository di controllo del codice sorgente come GitHub. È possibile, in alternativa, archiviarli in un account di archiviazione di Azure per consentire l'accesso condiviso nell'organizzazione.

toodeploy un modello esterno, usare hello **TemplateUri** parametro. Utilizzare Ciao URI hello esempio toodeploy hello modello di esempio da GitHub.

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -storageAccountType Standard_GRS
```

Hello esempio precedente richiede un URI accessibile pubblicamente per il modello di hello, che può essere usato per la maggior parte degli scenari perché il modello non deve includere dati riservati. Se è necessario toospecify dati riservati (ad esempio una password di amministratore), passare il valore come parametro sicura. Tuttavia, se si desidera toobe il modello accessibile pubblicamente, è possibile proteggerli da archiviare in un contenitore di archiviazione privato. Per informazioni sulla distribuzione di un modello che richiede un token di firma di accesso condiviso (SAS), vedere [Distribuire un modello privato con un token di firma di accesso condiviso](resource-manager-powershell-sas-token.md).

## <a name="parameter-files"></a>File dei parametri

Anziché il passaggio di parametri come valori inline nello script, può risultare più semplice toouse un file JSON che contiene i valori dei parametri hello. file di parametro Hello deve essere nel seguente formato hello:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
     "storageAccountType": {
         "value": "Standard_GRS"
     }
  }
}
```

Si noti che la sezione parametri di hello include un nome di parametro corrispondente parametro hello definito nel modello (storageAccountType). file di parametro Hello contiene un valore per il parametro hello. Questo valore viene passato automaticamente toohello modello durante la distribuzione. È possibile creare più file di parametro per diversi scenari di distribuzione e quindi passare nel file di parametro appropriato hello. 

Copiare l'esempio sopra riportato hello e salvarlo come un file denominato `storage.parameters.json`.

toopass un file di parametro locale, utilizzare hello **TemplateParameterFile** parametro:

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json `
  -TemplateParameterFile c:\MyTemplates\storage.parameters.json
```

toopass un file di parametro esterna, utilizzare hello **TemplateParameterUri** parametro:

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.parameters.json
```

È possibile utilizzare parametri inline e un parametro locale del file in hello stessa operazione di distribuzione. Ad esempio, è possibile specificare alcuni valori nel file dei parametri locali hello e aggiungere altri valori inline durante la distribuzione. Se si specificano valori per un parametro nel file dei parametri locali hello sia in linea, hello inline valore ha la precedenza.

Tuttavia, quando si usa un file di parametri esterni, non è possibile trasmettere altri valori, né inline né da un file locale. Quando si specifica un file di parametro hello **TemplateParameterUri** parametro, in linea tutti i parametri vengono ignorati. Specificare tutti i valori di parametro nel file esterno hello. Se il modello include un valore importante che non è possibile includere nel file di parametro hello, aggiungere tale valore tooa chiave dell'insieme di credenziali, oppure fornire in modo dinamico tutti i valori di parametro inline.

Se il modello include un parametro con stesso nome come uno dei parametri di hello nel comando di PowerShell hello hello, PowerShell presenta il parametro hello in base al modello con suffisso hello **FromTemplate**. Ad esempio, un parametro denominato **ResourceGroupName** nei conflitti di modelli con hello **ResourceGroupName** parametro hello [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment)cmdlet. Si è tooprovide richiesto un valore per **ResourceGroupNameFromTemplate**. In generale, si dovrebbe evitare questa confusione, non denominazione dei parametri con hello stesso nome come parametri utilizzati per operazioni di distribuzione.

## <a name="test-a-template-deployment"></a>Testare una distribuzione del modello

Utilizzare i valori di parametro e modello senza distribuire effettivamente le risorse, tootest [Test AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment). 

```powershell
Test-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

Se non vengono rilevati errori, il comando hello termina senza una risposta. Se viene rilevato un errore, il comando hello restituisce un messaggio di errore. Ad esempio, il tentativo di un valore non corretto per l'account di archiviazione hello SKU, toopass restituisce hello errore seguente:

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName testgroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType badSku

Code    : InvalidTemplate
Message : Deployment template validation failed: 'hello provided value 'badSku' for hello template parameter 'storageAccountType'
          at line '15' and column '24' is not valid. hello parameter value is not part of hello allowed value(s):
          'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.
Details :
```

Se il modello dispone di un errore di sintassi, il comando hello restituisce un errore che indica che non è stato possibile analizzare il modello di hello. messaggio Hello indica il numero di riga hello e la posizione di hello errore di analisi.

```powershell
Test-AzureRmResourceGroupDeployment : After parsing a value an unexpected character was encountered: 
  ". Path 'variables', line 31, position 3.
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

modalità completa toouse, utilizzare hello `Mode` parametro:

```powershell
New-AzureRmResourceGroupDeployment -Mode Complete -Name ExampleDeployment `
  -ResourceGroupName ExampleResourceGroup -TemplateFile c:\MyTemplates\storage.json 
```

## <a name="sample-template"></a>Modello di esempio

Hello modello seguente viene utilizzato per gli esempi di hello in questo argomento. Copiarlo e salvarlo come file denominato storage.json. toounderstand come toocreate questo modello, vedere [creare il primo modello di gestione risorse di Azure](resource-manager-create-first-template.md).  

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "sku": {
          "name": "[parameters('storageAccountType')]"
      },
      "kind": "Storage", 
      "properties": {
      }
    }
  ],
  "outputs": {
      "storageAccountName": {
          "type": "string",
          "value": "[variables('storageAccountName')]"
      }
  }
}
```

## <a name="next-steps"></a>Passaggi successivi
* esempi di Hello in questo articolo distribuire un gruppo di risorse tooa risorse nella sottoscrizione predefinita. toouse una sottoscrizione diversa, vedere [gestiscono più sottoscrizioni Azure](/powershell/azure/manage-subscriptions-azureps).
* Per uno script di esempio completo che consente di distribuire un modello, vedere lo [script di distribuzione di modelli di Resource Manager](resource-manager-samples-powershell-deploy.md).
* toounderstand toodefine parametri nel modello, vedere [comprendere hello struttura e la sintassi dei modelli di Azure Resource Manager](resource-group-authoring-templates.md).
* Per suggerimenti su come risolvere i comuni errori di distribuzione, vedere [Risolvere errori comuni durante la distribuzione di risorse in Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).
* Per informazioni sulla distribuzione di un modello che richiede un token di firma di accesso condiviso, vedere [Distribuire un modello privato con un token di firma di accesso condiviso](resource-manager-powershell-sas-token.md).
* Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).

