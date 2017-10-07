---
title: "aaaDeploy un'app web che è collegato il repository di GitHub tooa | Documenti Microsoft"
description: Utilizzare un toodeploy modello di gestione risorse di Azure un'app web che contiene un progetto da un repository di GitHub.
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 32739607-85fe-43c8-a4dc-1feb46d93a4d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2016
ms.author: cephalin
ms.openlocfilehash: 8b23416c4c06a60991517e6ee4cd82bebc5a9d73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-web-app-linked-tooa-github-repository"></a>Distribuire un repository di GitHub tooa collegato app web
In questo argomento si apprenderà come toocreate un modello di gestione risorse di Azure che consente di distribuire un'app web che è collegato tooa progetto in un repository di GitHub. Si apprenderà come toodefine quali risorse vengono distribuite come toodefine parametri e che vengono specificati quando è eseguita la distribuzione di hello. È possibile utilizzare questo modello per la propria distribuzioni o personalizzarlo toomeet esigenze.

Per altre informazioni sulla creazione dei modelli, vedere [Creazione di modelli di Gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md).

Per il modello di hello completo, vedere [Web App collegato tooGitHub modello](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a>Elementi distribuiti
Con questo modello verrà distribuito un'app web che contiene il codice hello da un progetto in GitHub.

toorun hello automaticamente la distribuzione, fare clic su hello seguente pulsante:

[![Distribuire tooAzure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)

## <a name="parameters"></a>parameters
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="repourl"></a>repoURL
Hello URL per il repository di GitHub che contiene toodeploy progetto hello. Questo parametro contiene un valore predefinito, ma questo valore è solo tooshow previsto è come tooprovide hello URL per il repository. È possibile utilizzare questo valore quando test modello hello ma si desidererà tooprovide hello URL proprio repository quando si utilizza il modello di hello.

    "repoURL": {
        "type": "string",
        "defaultValue": "https://github.com/davidebbo-test/Mvc52Application.git"
    }

### <a name="branch"></a>ramo
ramo Hello di hello repository toouse quando si distribuisce un'applicazione hello. valore predefinito di Hello è il database master, ma è possibile specificare il nome di hello di qualsiasi ramo nel repository di hello che si desidera toodeploy.

    "branch": {
        "type": "string",
        "defaultValue": "master"
    }

## <a name="resources-toodeploy"></a>Risorse toodeploy
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a>App Web
Crea app web hello del progetto toohello collegato in GitHub. 

Specificare il nome di hello dell'app web hello tramite hello **siteName** parametro e la posizione di hello dell'app web hello tramite hello **siteLocation** parametro. In hello **dependsOn** elemento modello hello definisce hello web app come dipende dal servizio hello piano di hosting. Poiché è dipende dal piano di hosting hello, hello web app non viene creato fino a quando non hello piano di hosting è stata completata la creazione. Hello **dependsOn** elemento è utilizzato toospecify solo ordine di distribuzione. Se non si contrassegna hello web app come dipende dal piano di hosting hello, Azure Resource Manager tenterà toocreate entrambe le risorse in hello stesso tempo e potrebbe essere visualizzato un errore se l'app web hello venga creato prima di hello piano di hosting.

app web Hello dispone anche di una risorsa figlio che è definita in **risorse** sezione riportata di seguito. Risorsa figlio che definisce il codice sorgente per il progetto hello distribuito con hello web app. In questo modello di controllo del codice sorgente hello è collegato tooa particolare repository di GitHub. repository di GitHub Hello è definito con codice hello **"URL repository": "https://github.com/davidebbo-test/Mvc52Application.git"** è possibile codificare hello URL del repository quando si desidera toocreate un modello che consente di distribuire più volte un singolo progetto richiedere numero minimo di hello di parametri.
Anziché a livello di codice hello URL del repository, è possibile aggiungere un parametro per l'URL del repository hello e utilizzare tale valore per hello **URL repository** proprietà.

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/sites",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
      ],
      "properties": {
        "serverFarmId": "[parameters('hostingPlanName')]"
      },
      "resources": [
        {
          "apiVersion": "2015-08-01",
          "name": "web",
          "type": "sourcecontrols",
          "dependsOn": [
            "[resourceId('Microsoft.Web/Sites', parameters('siteName'))]"
          ],
          "properties": {
            "RepoUrl": "[parameters('repoURL')]",
            "branch": "[parameters('branch')]",
            "IsManualIntegration": true
          }
        }
      ]
    }

## <a name="commands-toorun-deployment"></a>Comandi toorun distribuzione
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json -siteName ExampleSite -hostingPlanName ExamplePlan -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a>Interfaccia della riga di comando di Azure

    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json

### <a name="azure-cli-20"></a>Interfaccia della riga di comando di Azure 2.0

    az group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE] 
> Per il contenuto del file JSON di hello parametri, vedere [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).
>
>

