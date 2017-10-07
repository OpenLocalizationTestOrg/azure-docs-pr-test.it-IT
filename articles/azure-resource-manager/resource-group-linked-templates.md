---
title: aaaLink modelli per la distribuzione di Azure | Documenti Microsoft
description: Viene descritto come toouse collegato modelli in un toocreate modello di gestione risorse di Azure una soluzione di modello modulare. Illustra come specificare un file di parametri, valori dei parametri toopass e creati in modo dinamico gli URL.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 27d8c4b2-1e24-45fe-88fd-8cf98a6bb2d2
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: tomfitz
ms.openlocfilehash: b935b1810db5ce894d009403cd4bb945cab34ba7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-linked-templates-when-deploying-azure-resources"></a>Uso di modelli collegati nella distribuzione di risorse di Azure
All'interno di un modello di gestione risorse di Azure, è possibile collegare tooanother modello, che consentono di toodecompose la distribuzione in un set di modelli di destinazione, scopo specifico. In modo analogo alla scomposizione di un'applicazione in diverse classi di codice, la scomposizione offre vantaggi in termini di testing, riuso e leggibilità.  

È possibile passare parametri da un modello di collegato tooa principale dei modelli, e tali parametri è possono mappare direttamente tooparameters o variabili esposte dal modello di chiamata hello. modello collegato Hello è inoltre possibile passare un modello di origine toohello nascosto variabile output, l'abilitazione di uno scambio di dati bidirezionale tra modelli.

## <a name="linking-tooa-template"></a>Collegamento tooa modello
Si crea un collegamento tra due modelli mediante l'aggiunta di una risorsa di distribuzione nel modello principale hello punti toohello modello collegato. Impostare hello **templateLink** toohello proprietà URI del modello collegato hello. È possibile fornire i valori dei parametri per il modello collegato hello direttamente nel modello o in un file di parametro. esempio Hello utilizza hello **parametri** toospecify proprietà direttamente un valore di parametro.

```json
"resources": [ 
  { 
      "apiVersion": "2017-05-10", 
      "name": "linkedTemplate", 
      "type": "Microsoft.Resources/deployments", 
      "properties": { 
        "mode": "incremental", 
        "templateLink": {
          "uri": "https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion": "1.0.0.0"
        }, 
        "parameters": { 
          "StorageAccountName":{"value": "[parameters('StorageAccountName')]"} 
        } 
      } 
  } 
] 
```

Come altri tipi di risorse, è possibile impostare le dipendenze tra modello collegato hello e altre risorse. Di conseguenza, quando le altre risorse richiedono un valore di output dal modello collegato hello, è possibile verificare che sia distribuito modello collegato hello prima li. In alternativa, quando il modello di hello collegato si basa su altre risorse, per verificare se che altre risorse distribuite prima modello collegato hello. È possibile recuperare un valore da un modello collegato con hello la seguente sintassi:

```json
"[reference('linkedTemplate').outputs.exampleProperty.value]"
```

Hello del servizio Gestione risorse deve essere in grado di tooaccess modello collegato di hello. È possibile specificare un file locale o un file che è disponibile solo in una rete locale per il modello collegato hello. È possibile fornire solo un valore URI che includa **http** o **https**. È il modello collegato in un account di archiviazione e utilizzo hello URI per l'elemento, come illustrato nell'esempio seguente hello tooplace:

```json
"templateLink": {
    "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
    "contentVersion": "1.0.0.0",
}
```

Sebbene il modello collegato hello devono essere disponibile esternamente, non è necessario toobe toohello generalmente disponibili pubblico. È possibile aggiungere l'account di archiviazione privato tooa modello che è proprietario dell'account di archiviazione accessibile tooonly hello. È quindi possibile creare un accesso tooenable token di accesso condiviso (firma) durante la distribuzione. Aggiungere tale toohello token SAS URI per il modello collegato hello. Per conoscere la procedura per la configurazione di un modello in un account di archiviazione e per la generazione di un token con firma di accesso condiviso, consultare [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md) (Distribuire le risorse con i modelli di Resource Manager e Azure PowerShell) o [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md) (Distribuire le risorse con i modelli di Azure Resource Manager e l'interfaccia della riga di comando di Azure). 

Hello di esempio seguente viene illustrato un modello padre tale modello tooanother collegamenti. è possibile accedere con un token di firma di accesso condiviso che viene passato come un parametro di modello collegato Hello.

```json
"parameters": {
    "sasToken": { "type": "securestring" }
},
"resources": [
    {
        "apiVersion": "2017-05-10",
        "name": "linkedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
          "mode": "incremental",
          "templateLink": {
            "uri": "[concat('https://storagecontosotemplates.blob.core.windows.net/templates/helloworld.json', parameters('sasToken'))]",
            "contentVersion": "1.0.0.0"
          }
        }
    }
],
```

Anche se il token hello viene passato come stringa sicura, hello URI del modello collegato hello, incluso il token di firma di accesso condiviso hello, viene registrato nelle operazioni di distribuzione hello. esposizione di toolimit, impostare una scadenza per il token hello.

Resource Manager gestisce ogni modello collegato come una distribuzione distinta. Nella cronologia di distribuzione hello per il gruppo di risorse hello, vedrai distribuzioni separate per padre hello e i modelli annidati.

![cronologia della distribuzione](./media/resource-group-linked-templates/linked-deployment-history.png)

## <a name="linking-tooa-parameter-file"></a>Il collegamento di file di parametro tooa
esempio Hello utilizza hello **parametersLink** file dei parametri di proprietà toolink tooa.

```json
"resources": [ 
  { 
     "apiVersion": "2017-05-10", 
     "name": "linkedTemplate", 
     "type": "Microsoft.Resources/deployments", 
     "properties": { 
       "mode": "incremental", 
       "templateLink": {
          "uri":"https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion":"1.0.0.0"
       }, 
       "parametersLink": { 
          "uri":"https://www.contoso.com/AzureTemplates/parameters.json",
          "contentVersion":"1.0.0.0"
       } 
     } 
  } 
] 
```

valore dell'URI Hello per file collegato parametro hello non può essere un file locale e deve includere una **http** o **https**. file di parametro Hello può essere limitato tooaccess tramite un token di firma di accesso condiviso.

## <a name="using-variables-toolink-templates"></a>Utilizzo di variabili toolink modelli
Negli esempi precedenti Hello mostrano i valori di URL hardcoded per i collegamenti di modello hello. Questo approccio potrebbe funzionare per un modello semplice ma non funziona correttamente in caso di uso di un ampio set di modelli modulari. In alternativa, è possibile creare una variabile statica che archivia un URL di base per il modello principale hello e quindi creare in modo dinamico gli URL per i modelli di hello collegato da tale URL di base. Il vantaggio di Hello di questo approccio è che è possibile spostare o divisione modello hello poiché è sufficiente variabile statica di hello toochange nel modello principale hello. modello principale Hello passa hello URI di hello scomposto modello corretto.

Hello esempio seguente viene illustrato come una base toocreate URL toouse due URL per collegato modelli (**sharedTemplateUrl** e **vmTemplate**). 

```json
"variables": {
    "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
    "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
    "vmTemplateUrl": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]"
}
```

È inoltre possibile utilizzare [distribuzione ()](resource-group-template-functions-deployment.md#deployment) tooget hello URL di base per il modello corrente hello e utilizzare l'URL hello tooget per gli altri modelli hello nello stesso percorso. Questo approccio è utile se viene modificato il percorso del modello (probabilmente dovuto tooversioning) o si desidera tooavoid rigido codifica URL nel file di modello hello. 

```json
"variables": {
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"
}
```

## <a name="complete-example"></a>Esempio completo
Hello modelli di esempio seguente mostra una disposizione semplificata dei modelli collegati tooillustrate alcuni dei concetti hello in questo articolo. Si presuppone che i modelli di hello sono stati aggiunti toohello stesso contenitore in un account di archiviazione con accesso pubblico disattivato. modello collegato Hello passa un valore toohello indietro principale dei modelli in hello **restituisce** sezione.

Hello **parent.json** file costituito da:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "containerSasToken": { "type": "string" }
  },
  "resources": [
    {
      "apiVersion": "2017-05-10",
      "name": "linkedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
        "mode": "incremental",
        "templateLink": {
          "uri": "[concat(uri(deployment().properties.templateLink.uri, 'helloworld.json'), parameters('containerSasToken'))]",
          "contentVersion": "1.0.0.0"
        }
      }
    }
  ],
  "outputs": {
    "result": {
      "type": "string",
      "value": "[reference('linkedTemplate').outputs.result.value]"
    }
  }
}
```

Hello **helloworld.json** file costituito da:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "variables": {},
  "resources": [],
  "outputs": {
    "result": {
        "value": "Hello World",
        "type" : "string"
    }
  }
}
```

In PowerShell, ottenere un token per il contenitore di hello e distribuire modelli hello con:

```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name storagecontosotemplates
$token = New-AzureStorageContainerSASToken -Name templates -Permission r -ExpiryTime (Get-Date).AddMinutes(30.0)
$url = (Get-AzureStorageBlob -Container templates -Blob parent.json).ICloudBlob.uri.AbsoluteUri
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri ($url + $token) -containerSasToken $token
```

2.0 CLI di Azure, ottenere un token per il contenitore di hello e distribuire modelli hello con hello seguente codice:

```azurecli
expiretime=$(date -u -d '30 minutes' +%Y-%m-%dT%H:%MZ)
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name storagecontosotemplates \
    --query connectionString)
token=$(az storage container generate-sas \
    --name templates \
    --expiry $expiretime \
    --permissions r \
    --output tsv \
    --connection-string $connection)
url=$(az storage blob url \
    --container-name templates \
    --name parent.json \
    --output tsv \
    --connection-string $connection)
parameter='{"containerSasToken":{"value":"?'$token'"}}'
az group deployment create --resource-group ExampleGroup --template-uri $url?$token --parameters $parameter
```

## <a name="next-steps"></a>Passaggi successivi
* vedere toolearn sulla definizione di ordine di distribuzione hello per le risorse, hello [definizione delle dipendenze nei modelli di gestione risorse di Azure](resource-group-define-dependencies.md)
* toolearn come una risorsa toodefine ma creare molte istanze di, vedere [creare più istanze delle risorse di gestione risorse di Azure](resource-group-create-multiple.md)

