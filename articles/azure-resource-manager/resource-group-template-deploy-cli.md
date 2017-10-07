---
title: risorse aaaDeploy con Azure CLI e modello | Documenti Microsoft
description: Utilizzare Gestione risorse di Azure e Azure CLI toodeploy un tooAzure di risorse. risorse di Hello vengono definite in un modello di gestione risorse.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 493b7932-8d1e-4499-912c-26098282ec95
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: tomfitz
ms.openlocfilehash: 9f8bb9a8720399390a407030d2d32bcd97d32f13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-cli"></a>Distribuire le risorse con i modelli di Azure Resource Manager e l'interfaccia della riga di comando di Azure

Questo argomento viene illustrato come toouse 2.0 CLI di Azure con Gestione risorse modelli toodeploy tooAzure le risorse. Se non si ha familiarità con concetti hello della distribuzione e gestione di soluzioni di Azure, vedere [Panoramica di gestione risorse di Azure](resource-group-overview.md).  

il modello di gestione risorse di Hello è distribuire può essere un file nel computer locale o un file esterno che si trova in un archivio come GitHub. modello Hello si distribuisce in questo articolo è disponibile in hello [modello di esempio](#sample-template) sezione, oppure come un [modello di account di archiviazione in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).

[!INCLUDE [sample-cli-install](../../includes/sample-cli-install.md)]

Se non si dispone di Azure CLI installato, è possibile utilizzare hello [Shell Cloud](#deploy-template-from-cloud-shell).

## <a name="deploy-local-template"></a>Distribuire un modello locale

Quando si distribuisce tooAzure risorse, è:

1. Accedi tooyour account Azure
2. Creare un gruppo di risorse che funge da contenitore hello per le risorse di hello distribuito. nome Hello hello del gruppo di risorse possa includere solo caratteri alfanumerici, punti, caratteri di sottolineatura, trattini e parentesi. Può trattarsi di too90 caratteri. Non può terminare con un punto.
3. Distribuire toohello risorse gruppo hello modello che definisce hello risorse toocreate

Un modello può includere parametri che consentono la distribuzione di hello toocustomize. Può includere ad esempio valori specifici per un determinato ambiente (di sviluppo, test e produzione). modello di esempio Hello definisce un parametro per l'account di archiviazione hello SKU. 

Hello di esempio seguente crea un gruppo di risorse e distribuisce un modello dal computer locale:

```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

distribuzione di Hello può richiedere alcuni minuti toocomplete. Al termine, viene visualizzato un messaggio che include i risultati di hello:

```azurecli
"provisioningState": "Succeeded",
```

## <a name="deploy-external-template"></a>Distribuire un modello esterno

Invece di archiviare i modelli di gestione risorse nel computer locale, è preferibile toostore multipla in una posizione esterna. ad esempio in un repository di controllo del codice sorgente come GitHub. È possibile, in alternativa, archiviarli in un account di archiviazione di Azure per consentire l'accesso condiviso nell'organizzazione.

toodeploy un modello esterno, usare hello **modello uri** parametro. Utilizzare Ciao URI hello esempio toodeploy hello modello di esempio da GitHub.
   
```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
    --parameters storageAccountType=Standard_GRS
```

Hello esempio precedente richiede un URI accessibile pubblicamente per il modello di hello, che può essere usato per la maggior parte degli scenari perché il modello non deve includere dati riservati. Se è necessario toospecify dati riservati (ad esempio una password di amministratore), passare il valore come parametro sicura. Tuttavia, se si desidera toobe il modello accessibile pubblicamente, è possibile proteggerli da archiviare in un contenitore di archiviazione privato. Per informazioni sulla distribuzione di un modello che richiede un token di firma di accesso condiviso (SAS), vedere [Distribuire un modello privato con un token di firma di accesso condiviso](resource-manager-cli-sas-token.md).

## <a name="deploy-template-from-cloud-shell"></a>Distribuire il modello da Cloud Shell

È possibile utilizzare [Shell Cloud](../cloud-shell/overview.md) toorun hello CLI di Azure i comandi per la distribuzione del modello. Tuttavia, è necessario caricare prima il modello in una condivisione di file hello per la Shell di Cloud. Per informazioni sulla configurazione di Cloud Shell per il primo utilizzo, vedere [Panoramica di Azure Cloud Shell](../cloud-shell/overview.md).

1. Accedi toohello [portale di Azure](https://portal.azure.com).   

2. Selezionare il gruppo di risorse di Cloud Shell. modello di nome Hello è `cloud-shell-storage-<region>`.

   ![Selezionare il gruppo di risorse](./media/resource-group-template-deploy-cli/select-cs-resource-group.png)

3. Selezionare un account di archiviazione hello per la Shell di Cloud.

   ![Selezionare l'account di archiviazione](./media/resource-group-template-deploy-cli/select-storage.png)

4. Selezionare **File**.

   ![Selezione dei file](./media/resource-group-template-deploy-cli/select-files.png)

5. Selezionare condivisione file hello per Cloud Shell. modello di nome Hello è `cs-<user>-<domain>-com-<uniqueGuid>`.

   ![Selezionare la condivisione file](./media/resource-group-template-deploy-cli/select-file-share.png)

6. Selezionare **Aggiungi directory**.

   ![Aggiungi directory](./media/resource-group-template-deploy-cli/select-add-directory.png)

7. Assegnare il nome **templates** e scegliere **OK**.

   ![Assegnare il nome alla directory](./media/resource-group-template-deploy-cli/name-templates.png)

8. Selezionare la nuova directory.

   ![Selezionare la directory](./media/resource-group-template-deploy-cli/select-templates.png)

9. Selezionare **Carica**.

   ![Selezionare Carica](./media/resource-group-template-deploy-cli/select-upload.png)

10. Trovare e caricare il modello.

   ![Caricare il file](./media/resource-group-template-deploy-cli/upload-files.png)

11. Prompt dei comandi aprire hello.

   ![Aprire Cloud Shell](./media/resource-group-template-deploy-cli/start-cloud-shell.png)

12. Immettere i seguenti comandi nella Shell di Cloud hello hello:

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageAccountType=Standard_GRS
   ```

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

Utilizzare un file di parametro locale, toopass `@` toospecify un file locale denominato storage.parameters.json.

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

## <a name="test-a-template-deployment"></a>Testare una distribuzione del modello

Utilizzare i valori di parametro e modello senza distribuire effettivamente le risorse, tootest [distribuzione gruppo az convalidare](/cli/azure/group/deployment#validate). 

```azurecli
az group deployment validate \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

Se non vengono rilevati errori, il comando hello restituisce informazioni sulla distribuzione dei test hello. In particolare, si noti che hello **errore** valore è null.

```azurecli
{
  "error": null,
  "properties": {
      ...
```

Se viene rilevato un errore, il comando hello restituisce un messaggio di errore. Ad esempio, il tentativo di un valore non corretto per l'account di archiviazione hello SKU, toopass restituisce hello errore seguente:

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template validation failed: 'hello provided value 'badSKU' for hello template parameter 
      'storageAccountType' at line '13' and column '20' is not valid. hello parameter value is not part of hello allowed 
      value(s): 'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.",
    "target": null
  },
  "properties": null
}
```

Se il modello dispone di un errore di sintassi, il comando hello restituisce un errore che indica che non è stato possibile analizzare il modello di hello. messaggio Hello indica il numero di riga hello e la posizione di hello errore di analisi.

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template parse failed: 'After parsing a value an unexpected character was encountered:
      \". Path 'variables', line 31, position 3.'.",
    "target": null
  },
  "properties": null
}
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

modalità completa toouse, utilizzare hello `mode` parametro:

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --mode Complete \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
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
* esempi di Hello in questo articolo distribuire un gruppo di risorse tooa risorse nella sottoscrizione predefinita. toouse una sottoscrizione diversa, vedere [gestiscono più sottoscrizioni Azure](/cli/azure/manage-azure-subscriptions-azure-cli).
* Per uno script di esempio completo che consente di distribuire un modello, vedere lo [script di distribuzione di modelli di Resource Manager](resource-manager-samples-cli-deploy.md).
* toounderstand toodefine parametri nel modello, vedere [comprendere hello struttura e la sintassi dei modelli di Azure Resource Manager](resource-group-authoring-templates.md).
* Per suggerimenti su come risolvere i comuni errori di distribuzione, vedere [Risolvere errori comuni durante la distribuzione di risorse in Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).
* Per informazioni sulla distribuzione di un modello che richiede un token di firma di accesso condiviso, vedere [Distribuire un modello privato con un token di firma di accesso condiviso](resource-manager-cli-sas-token.md).
* Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).
