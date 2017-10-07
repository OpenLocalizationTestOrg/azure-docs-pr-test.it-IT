---
title: il primo modello di gestione risorse di Azure aaaCreate | Documenti Microsoft
description: Toocreating una Guida dettagliata del primo modello di gestione risorse di Azure. Viene visualizzato come toouse hello riferimento di modello per un modello di archiviazione account toocreate hello.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 07/27/2017
ms.topic: get-started-article
ms.author: tomfitz
ms.openlocfilehash: 92e6d6bb7094fe0e4537ee080704967862804bdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-your-first-azure-resource-manager-template"></a>Creare e distribuire il primo modello di Azure Resource Manager
In questo argomento illustra procedure hello di creazione del primo modello di gestione risorse di Azure. Modelli di gestione risorse sono file JSON che definiscono le risorse di hello toodeploy è necessario per la soluzione. concetti di hello toounderstand associati a una distribuzione e gestione di soluzioni di Azure, vedere [Panoramica di gestione risorse di Azure](resource-group-overview.md). Se si dispone di risorse esistenti e si desidera tooget un modello per le risorse, vedere [esportare un modello di gestione risorse di Azure da risorse esistenti](resource-manager-export-template.md).

modelli toocreate e rivedere, è necessario un editor di JSON. [Visual Studio Code](https://code.visualstudio.com/) è un editor di codice, leggero, open source e multipiattaforma. È consigliabile usare Visual Studio Code per la creazione di modelli di Resource Manager. In questo argomento si presuppone che venga usato Visual Studio Code. Se tuttavia si ha un altro editor JSON (ad esempio, Visual Studio), è possibile usare tale editor.

## <a name="prerequisites"></a>Prerequisiti

* Visual Studio Code. Se necessario, installarlo da [https://code.visualstudio.com/](https://code.visualstudio.com/).
* Una sottoscrizione di Azure. Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.

## <a name="create-template"></a>Creare il modello

Iniziamo con un modello semplice che consente di distribuire una sottoscrizione tooyour account di archiviazione.

1. Selezionare **File** > **Nuovo file**. 

   ![Nuovo file](./media/resource-manager-create-first-template/new-file.png)

2. Copiare e incollare la seguente sintassi JSON nel file hello:

   ```json
   {
     "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
     "contentVersion": "1.0.0.0",
     "parameters": {
     },
     "variables": {
     },
     "resources": [
       {
         "name": "[concat('storage', uniqueString(resourceGroup().id))]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "sku": {
           "name": "Standard_LRS"
         },
         "kind": "Storage",
         "location": "South Central US",
         "tags": {},
         "properties": {}
       }
     ],
     "outputs": {  }
   }
   ```

   I nomi degli account di archiviazione dispone di numerose restrizioni che li rendono difficile tooset. nome Hello deve essere compresa tra 3 e 24 caratteri, utilizzare solo numeri e lettere minuscole e univoco. il modello precedente Hello utilizza hello [uniqueString](resource-group-template-functions-string.md#uniquestring) funzione toogenerate un valore hash. valore questo hash toogive più vale a dire, viene aggiunto il prefisso hello *archiviazione*. 

3. Salvare questo file come **azuredeploy.json** tooa di cartella locale.

   ![Salvare il modello](./media/resource-manager-create-first-template/save-template.png)

## <a name="deploy-template"></a>Distribuire il modello

Si sono pronti toodeploy questo modello. Utilizzare PowerShell o Azure CLI toocreate un gruppo di risorse. Sarà quindi possibile distribuire un gruppo di risorse toothat di account di archiviazione.

* Per PowerShell, usare hello seguendo i comandi dalla cartella hello contenente hello modello:

   ```powershell
   Login-AzureRmAccount
   
   New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
   New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json
   ```

* Per un'installazione locale di CLI di Azure, utilizzare hello seguendo i comandi dalla cartella hello contenente il modello di hello:

   ```azurecli
   az login

   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file azuredeploy.json
   ```

Al termine del processo di distribuzione, nel gruppo di risorse hello l'account di archiviazione.

## <a name="deploy-template-from-cloud-shell"></a>Distribuire il modello da Cloud Shell

È possibile utilizzare [Shell Cloud](../cloud-shell/overview.md) toorun hello CLI di Azure i comandi per la distribuzione del modello. Tuttavia, è necessario caricare prima il modello in una condivisione di file hello per la Shell di Cloud. Per informazioni sulla configurazione di Cloud Shell per il primo utilizzo, vedere [Panoramica di Azure Cloud Shell](../cloud-shell/overview.md).

1. Accedi toohello [portale di Azure](https://portal.azure.com).   

2. Selezionare il gruppo di risorse di Cloud Shell. modello di nome Hello è `cloud-shell-storage-<region>`.

   ![Selezionare il gruppo di risorse](./media/resource-manager-create-first-template/select-cs-resource-group.png)

3. Selezionare un account di archiviazione hello per la Shell di Cloud.

   ![Selezionare l'account di archiviazione](./media/resource-manager-create-first-template/select-storage.png)

4. Selezionare **File**.

   ![Selezione dei file](./media/resource-manager-create-first-template/select-files.png)

5. Selezionare condivisione file hello per Cloud Shell. modello di nome Hello è `cs-<user>-<domain>-com-<uniqueGuid>`.

   ![Selezionare la condivisione file](./media/resource-manager-create-first-template/select-file-share.png)

6. Selezionare **Aggiungi directory**.

   ![Aggiungi directory](./media/resource-manager-create-first-template/select-add-directory.png)

7. Assegnare il nome **templates** e scegliere **OK**.

   ![Assegnare il nome alla directory](./media/resource-manager-create-first-template/name-templates.png)

8. Selezionare la nuova directory.

   ![Selezionare la directory](./media/resource-manager-create-first-template/select-templates.png)

9. Selezionare **Carica**.

   ![Selezionare Carica](./media/resource-manager-create-first-template/select-upload.png)

10. Trovare e caricare il modello.

   ![Caricare il file](./media/resource-manager-create-first-template/upload-files.png)

11. Prompt dei comandi aprire hello.

   ![Aprire Cloud Shell](./media/resource-manager-create-first-template/start-cloud-shell.png)

12. Immettere i seguenti comandi nella Shell di Cloud hello hello:

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json
   ```

Al termine del processo di distribuzione, nel gruppo di risorse hello l'account di archiviazione.

## <a name="customize-hello-template"></a>Personalizzare il modello di hello

modello Hello funziona correttamente, ma non è flessibile. Distribuisce sempre un tooSouth di archiviazione con ridondanza locale, Stati Uniti centrali. nome Hello è sempre *archiviazione* seguita da un valore hash. tooenable utilizzando il modello di hello per diversi scenari, aggiungere parametri toohello modello.

Hello riportato di seguito sezione parametri hello con due parametri. primo parametro Hello `storageSKU` consente tipo hello toospecify di ridondanza. Limita i valori hello che è possibile passare toovalues validi per un account di archiviazione. Specifica anche un valore predefinito. secondo parametro Hello `storageNamePrefix` è set tooallow un massimo di 11 caratteri. Specifica un valore predefinito.

```json
"parameters": {
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
  },
  "storageNamePrefix": {
    "type": "string",
    "maxLength": 11,
    "defaultValue": "storage",
    "metadata": {
      "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
    }
  }
},
```

Nella sezione variabili hello, aggiungere una variabile denominata `storageName`. Combina il valore di prefisso hello dai parametri hello e un valore hash hello [uniqueString](resource-group-template-functions-string.md#uniquestring) (funzione). Usa hello [toLower](resource-group-template-functions-string.md#tolower) funzione tooconvert toolowercase di tutti i caratteri.

```json
"variables": {
  "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
},
```

toouse questi nuovi valori per l'account di archiviazione, modificare la definizione di risorsa hello:

```json
"resources": [
  {
    "name": "[variables('storageName')]",
    "type": "Microsoft.Storage/storageAccounts",
    "apiVersion": "2016-01-01",
    "sku": {
      "name": "[parameters('storageSKU')]"
    },
    "kind": "Storage",
    "location": "[resourceGroup().location]",
    "tags": {},
    "properties": {}
  }
],
```

Si noti che hello nome dell'account di archiviazione hello è ora impostato variabile toohello che è stato aggiunto. nome SKU Hello è impostato un valore toohello del parametro hello. ubicazione Hello hello stesso percorso del gruppo di risorse hello.

Salvare il file. 

Dopo aver completato i passaggi di hello in questo articolo, il modello è ora simile a:

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
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
    },   
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
      }
    }
  },
  "variables": {
    "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {}
    }
  ],
  "outputs": {  }
}
```

## <a name="redeploy-template"></a>Ridistribuire il modello

Ridistribuire il modello di hello con valori diversi.

Per PowerShell, usare:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json -storageNamePrefix newstore -storageSKU Standard_RAGRS
```

Per l'interfaccia della riga di comando di Azure usare:

```azurecli
az group deployment create --resource-group examplegroup --template-file azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

Per hello Shell Cloud, è possibile caricare la condivisione di file toohello modello modificato. Sovrascrivi file esistente hello. Usare quindi hello comando seguente:

```azurecli
az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

## <a name="clean-up-resources"></a>Pulire le risorse

Quando non è più necessario, è possibile pulire le risorse di hello che eliminando il gruppo di risorse hello è stato distribuito.

Per PowerShell, usare:

```powershell
Remove-AzureRmResourceGroup -Name examplegroup
```

Per l'interfaccia della riga di comando di Azure usare:

```azurecli
az group delete --name examplegroup
```

## <a name="next-steps"></a>Passaggi successivi
* toolearn ulteriori informazioni su struttura hello di un modello, vedere [modelli Authoring Azure Resource Manager](resource-group-authoring-templates.md).
* toolearn sulle proprietà hello per un account di archiviazione, vedere [riferimento del modello gli account di archiviazione](/azure/templates/microsoft.storage/storageaccounts).
* modelli completo di tooview per molti tipi diversi di soluzioni, vedere hello [modelli di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates/).
