---
title: distribuzione di risorse aaaAutomate per un'app di funzione in funzioni di Azure | Documenti Microsoft
description: Informazioni su come toobuild un modello di gestione risorse di Azure che consente di distribuire l'app di funzione.
services: Functions
documtationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: funzioni di azure, funzioni, architettura senza server, infrastruttura come codice, azure resource manager
ms.assetid: d20743e3-aab6-442c-a836-9bcea09bfd32
ms.server: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: b0df0d4ef9fe93213f7b1cb1d1e6b4e14f8b3a30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automate-resource-deployment-for-your-function-app-in-azure-functions"></a>Automatizzare la distribuzione di risorse per l'app per le funzioni in Funzioni di Azure

È possibile utilizzare un toodeploy modello di gestione risorse di Azure un'app di funzione. Questo articolo vengono illustrati hello necessarie risorse e i parametri per questa operazione. Potrebbe essere necessario toodeploy altre risorse, a seconda di hello [trigger e le associazioni](functions-triggers-bindings.md) nell'app di funzione.

Per altre informazioni sulla creazione dei modelli, vedere [Creazione di modelli di Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

Per i modelli di esempio, vedere:
- [App per le funzioni nel piano a consumo]
- [App per le funzioni nel piano di servizio app di Azure]

## <a name="required-resources"></a>Risorse necessarie

Un'app per le funzioni richiede le risorse seguenti:

* Un account di [archiviazione di Azure](../storage/index.md)
* Un piano di hosting (piano a consumo o piano di servizio app)
* Un'app per le funzioni 

### <a name="storage-account"></a>Account di archiviazione

Per un'app per le funzioni è necessario l'account di archiviazione di Azure. È necessario un account per utilizzo generico che supporti BLOB, tabelle, code e i file. Per altre informazioni, vedere i [requisiti dell'account di archiviazione per Funzioni di Azure](functions-create-function-app-portal.md#storage-account-requirements).

```json
{
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2015-06-15",
    "location": "[resourceGroup().location]",
    "properties": {
        "accountType": "[parameters('storageAccountType')]"
    }
}
```

Inoltre, hello proprietà `AzureWebJobsStorage` e `AzureWebJobsDashboard` deve essere specificata come impostazioni dell'app nella configurazione del sito hello. il runtime di Azure funzioni Hello utilizza hello `AzureWebJobsStorage` code interne toocreate stringa di connessione. stringa di connessione Hello `AzureWebJobsDashboard` è usato toolog tooAzure tabella archiviazione e la potenza hello **monitoraggio** scheda nel portale di hello.

Queste proprietà sono specificate in hello `appSettings` insieme in hello `siteConfig` oggetto:

```json
"appSettings": [
    {
        "name": "AzureWebJobsStorage",
        "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
    },
    {
        "name": "AzureWebJobsDashboard",
        "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
    }
```    

### <a name="hosting-plan"></a>Piano di hosting

definizione di Hello del piano di hosting hello varia a seconda se si utilizza un piano di servizio App o di utilizzo. Vedere [distribuire un'app di funzione nel piano di consumo hello](#consumption) e [distribuire un'app di funzione nel piano di servizio App hello](#app-service-plan).

### <a name="function-app"></a>App per le funzioni

risorse app di funzione Hello sono definita tramite una risorsa di tipo **Microsoft.Web/Site** e tipo **functionapp**:

```json
{
    "apiVersion": "2015-08-01",
    "type": "Microsoft.Web/sites",
    "name": "[variables('functionAppName')]",
    "location": "[resourceGroup().location]",
    "kind": "functionapp",            
    "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
    ]
```

<a name="consumption"></a>

## <a name="deploy-a-function-app-on-hello-consumption-plan"></a>Distribuire un'app di funzione nel piano di consumo hello

È possibile eseguire un'app di funzione in due modalità diverse: hello piano il consumo e hello piano di servizio App. piano di consumo Hello alloca automaticamente potenza di calcolo quando il codice è in esecuzione, consente una scalabilità orizzontale come carico toohandle necessarie e quindi il ridimensionamento quando codice non è in esecuzione. In tal caso, non si dispone di toopay per le macchine virtuali inattive e non è la capacità di tooreserve in anticipo. vedere toolearn ulteriori informazioni sui piani di hosting [i piani di consumo di funzioni di Azure e servizio App](functions-scale.md).

Per un modello di Azure Resource Manager di esempio, vedere [App per le funzioni nel piano a consumo].

### <a name="create-a-consumption-plan"></a>Creare un piano a consumo

Un piano a consumo è un tipo particolare di risorsa "serverfarm". Specificare tramite hello `Dynamic` valore per hello `computeMode` e `sku` proprietà:

```json
{
    "type": "Microsoft.Web/serverfarms",
    "apiVersion": "2015-04-01",
    "name": "[variables('hostingPlanName')]",
    "location": "[resourceGroup().location]",
    "properties": {
        "name": "[variables('hostingPlanName')]",
        "computeMode": "Dynamic",
        "sku": "Dynamic"
    }
}
```

### <a name="create-a-function-app"></a>Creare un'app per le funzioni

Inoltre, un piano di consumo richiede due impostazioni aggiuntive nella configurazione del sito hello: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` e `WEBSITE_CONTENTSHARE`. Queste proprietà consentono di configurare hello storage account e il percorso in cui sono archiviati hello funzione app codice e la configurazione.

```json
{
    "apiVersion": "2015-08-01",
    "type": "Microsoft.Web/sites",
    "name": "[variables('functionAppName')]",
    "location": "[resourceGroup().location]",
    "kind": "functionapp",            
    "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
    ],
    "properties": {
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "siteConfig": {
            "appSettings": [
                {
                    "name": "AzureWebJobsDashboard",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "AzureWebJobsStorage",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "WEBSITE_CONTENTAZUREFILECONNECTIONSTRING",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "WEBSITE_CONTENTSHARE",
                    "value": "[toLower(variables('functionAppName'))]"
                },
                {
                    "name": "FUNCTIONS_EXTENSION_VERSION",
                    "value": "~1"
                }
            ]
        }
    }
}
```                    

<a name="app-service-plan"></a> 

## <a name="deploy-a-function-app-on-hello-app-service-plan"></a>Distribuire un'app di funzione nel piano di servizio App hello

Nel piano di servizio App hello, l'app di funzione viene eseguita nelle macchine virtuali dedicate Basic, Standard e Premium SKU, App tooweb simile. Per informazioni dettagliate sul funzionamento di hello piano di servizio App, vedere hello [piani di servizio App di Azure ad approfondimenti su](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

Per un modello di Azure Resource Manager di esempio, vedere [App per le funzioni nel piano di servizio app di Azure].

### <a name="create-an-app-service-plan"></a>Creare un piano di servizio app

```json
{
    "type": "Microsoft.Web/serverfarms",
    "apiVersion": "2015-04-01",
    "name": "[variables('hostingPlanName')]",
    "location": "[resourceGroup().location]",
    "properties": {
        "name": "[variables('hostingPlanName')]",
        "sku": "[parameters('sku')]",
        "workerSize": "[parameters('workerSize')]",
        "hostingEnvironment": "",
        "numberOfWorkers": 1
    }
}
```

### <a name="create-a-function-app"></a>Creare un'app per le funzioni 

Dopo aver selezionato un'opzione di scalabilità, creare un'app per le funzioni. app Hello è hello contenitore contiene tutte le funzioni.

Un'app per le funzioni contiene numerose risorse figlio che possono essere usate nella distribuzione, incluse le impostazioni dell'app e le opzioni di controllo del codice sorgente. È anche possibile scegliere hello tooremove **sourcecontrols** risorse figlio e utilizzare un altro [opzione di distribuzione](functions-continuous-deployment.md) invece.

> [!IMPORTANT]
> toosuccessfully distribuire l'applicazione usando Gestione risorse di Azure, è importante toounderstand la distribuzione di risorse in Azure. Nell'esempio seguente di hello, vengono applicate le configurazioni di livello superiore tramite **della configurazione di sito**. È importante tooset queste configurazioni in un alto livello, non vengono utilizzati solo informazioni toohello funzioni runtime e la distribuzione del motore. Informazioni di primo livello sono necessario prima figlio hello **sourcecontrols/web** è applicata una risorsa. Sebbene sia possibile tooconfigure queste impostazioni in hello livello figlio **config/appSettings** risorse, in alcuni casi l'app di funzione deve essere distribuito *prima* **config/appSettings**  viene applicato. Quando ad esempio si usano le funzioni con [app per la logica](../logic-apps/index.md), le funzioni sono una dipendenza di un'altra risorsa.

```json
{
  "apiVersion": "2015-08-01",
  "name": "[parameters('appName')]",
  "type": "Microsoft.Web/sites",
  "kind": "functionapp",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]",
    "[resourceId('Microsoft.Web/serverfarms', parameters('appName'))]"
  ],
  "properties": {
     "serverFarmId": "[variables('appServicePlanName')]",
     "siteConfig": {
        "alwaysOn": true,
        "appSettings": [
            { "name": "FUNCTIONS_EXTENSION_VERSION", "value": "~1" },
            { "name": "Project", "value": "src" }
        ]
     }
  },
  "resources": [
     {
        "apiVersion": "2015-08-01",
        "name": "appsettings",
        "type": "config",
        "dependsOn": [
          "[resourceId('Microsoft.Web/Sites', parameters('appName'))]",
          "[resourceId('Microsoft.Web/Sites/sourcecontrols', parameters('appName'), 'web')]",
          "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
        ],
        "properties": {
          "AzureWebJobsStorage": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]",
          "AzureWebJobsDashboard": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
        }
     },
     {
          "apiVersion": "2015-08-01",
          "name": "web",
          "type": "sourcecontrols",
          "dependsOn": [
            "[resourceId('Microsoft.Web/sites/', parameters('appName'))]"
          ],
          "properties": {
            "RepoUrl": "[parameters('sourceCodeRepositoryURL')]",
            "branch": "[parameters('sourceCodeBranch')]",
            "IsManualIntegration": "[parameters('sourceCodeManualIntegration')]"
          }
     }
  ]
}
```
> [!TIP]
> Questo modello Usa hello [progetto](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) valore di impostazioni applicazione, che imposta hello directory di base in cui hello il motore di distribuzione di funzioni (Kudu) esegue la ricerca di codice distribuibile. Il repository, nostro funzioni sono in una sottocartella di hello **src** cartella. In tal caso, nell'hello sopra riportato, viene impostato il valore delle impostazioni app hello troppo`src`. Se le funzioni si trovano nella radice di hello del repository, o se non si sta distribuendo dal controllo del codice sorgente, è possibile rimuovere questo valore di impostazioni di app.

## <a name="deploy-your-template"></a>Distribuire il modello

È possibile utilizzare uno qualsiasi dei seguenti modi toodeploy hello del modello:

* [PowerShell](../azure-resource-manager/resource-group-template-deploy.md)
* [Interfaccia della riga di comando di Azure](../azure-resource-manager/resource-group-template-deploy-cli.md)
* [Portale di Azure](../azure-resource-manager/resource-group-template-deploy-portal.md)
* [API REST](../azure-resource-manager/resource-group-template-deploy-rest.md)

### <a name="deploy-tooazure-button"></a>Pulsante tooAzure di distribuzione

Sostituire ```<url-encoded-path-to-azuredeploy-json>``` con un [con codifica URL](https://www.bing.com/search?q=url+encode) versione di hello path non elaborato del `azuredeploy.json` file in GitHub.

Di seguito è riportato un esempio che usa la sintassi markdown:

```markdown
[![Deploy tooAzure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>)
```

Di seguito è riportato un esempio che usa HTML:

```html
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"></a>
```

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su toodevelop e configurare le funzioni di Azure.

* [Guida di riferimento per gli sviluppatori di Funzioni di Azure](functions-reference.md)
* [Funzionamento delle impostazioni dell'app Azure tooconfigure](functions-how-to-use-azure-function-app-settings.md)
* [Create your first Azure function](functions-create-first-azure-function.md) (Creare la prima funzione di Azure)

<!-- LINKS -->

[App per le funzioni nel piano a consumo]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dynamic/azuredeploy.json
[App per le funzioni nel piano di servizio app di Azure]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dedicated/azuredeploy.json
