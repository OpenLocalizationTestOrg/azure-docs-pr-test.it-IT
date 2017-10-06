---
title: aaaCreate un'app di logica utilizzando un modello in Azure | Documenti Microsoft
description: Utilizzare un toodeploy modello di gestione risorse di Azure un'app per la logica per la definizione di flussi di lavoro.
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7574cc7c-e5a1-4b7c-97f6-0cffb1a5d536
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2016
ms.author: LADocs; mandia
ms.openlocfilehash: efbacb534fc7f11e9b593aae4383480ce3a1752f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-logic-app-using-a-template"></a>Creare un'app per la logica usando un modello
I modelli offrono toouse un modo rapido connettori diversi all'interno di un'app di logica. Logica App include modelli di gestione risorse di Azure per si toocreate un'app di logica che può essere utilizzati toodefine flussi di lavoro aziendali. È possibile definire le risorse vengono distribuite e come parametri toodefine quando si distribuisce l'app logica. È possibile utilizzare questo modello per i propri scenari di business o personalizzarlo toomeet esigenze.

Per ulteriori informazioni sulle proprietà dell'app hello logica, vedere [API di gestione del flusso di lavoro logica App](https://msdn.microsoft.com/library/azure/mt643788.aspx). 

Per esempi di definizione hello, vedere [definizioni autore logica App](logic-apps-author-definitions.md). 

Per altre informazioni sulla creazione dei modelli, vedere [Creazione di modelli di Gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md).

Per il modello di hello completo, vedere [modello logica App](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).

## <a name="what-you-deploy"></a>Cosa viene distribuito
Con questo modello si distribuisce un'app per la logica.

distribuzione di hello toorun automaticamente, selezionare hello seguente pulsante:  

[![Distribuire tooAzure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)

## <a name="parameters"></a>parameters
[!INCLUDE [app-service-logic-deploy-parameters](../../includes/app-service-logic-deploy-parameters.md)]

### <a name="testuri"></a>testUri
     "testUri": {
        "type": "string",
        "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
      }

## <a name="resources-toodeploy"></a>Risorse toodeploy
### <a name="logic-app"></a>App per la logica
Crea app logica hello.

modelli di Hello utilizza un valore di parametro per nome dell'applicazione hello logica. Imposta percorso hello di hello logica app toohello stesso percorso del gruppo di risorse hello. 

Questa definizione particolare viene eseguito una volta all'ora e ping hello posizione specificata in hello **testUri** parametro. 

    {
      "type": "Microsoft.Logic/workflows",
      "apiVersion": "2016-06-01",
      "name": "[parameters('logicAppName')]",
      "location": "[resourceGroup().location]",
      "tags": {
        "displayName": "LogicApp"
      },
      "properties": {
        "definition": {
          "$schema": "http://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {
            "testURI": {
              "type": "string",
              "defaultValue": "[parameters('testUri')]"
            }
          },
          "triggers": {
            "recurrence": {
              "type": "recurrence",
              "recurrence": {
                "frequency": "Hour",
                "interval": 1
              }
            }
          },
          "actions": {
            "http": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('testUri')"
              },
              "runAfter": {}
            }
          },
          "outputs": {}
        },
        "parameters": {}
      }
    }


## <a name="commands-toorun-deployment"></a>Comandi toorun distribuzione
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a>Interfaccia della riga di comando di Azure
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -g ExampleDeployGroup



