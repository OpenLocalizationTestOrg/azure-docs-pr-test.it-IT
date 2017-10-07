---
title: un gruppo di spazio dei nomi e i consumer di hub eventi di Azure utilizzando un modello aaaCreate | Documenti Microsoft
description: Creare uno spazio dei nomi dell'hub eventi con Hub eventi e un gruppo di consumer usando i modelli di Azure Resource Manager
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 28bb4591-1fd7-444f-a327-4e67e8878798
ms.service: event-hubs
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/12/2017
ms.author: sethm;shvija
ms.openlocfilehash: 74b0d6b3fbe848705e2c20e628aa4e5269b53edb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-with-event-hub-and-consumer-group-using-an-azure-resource-manager-template"></a>Creare uno spazio dei nomi Hub eventi con hub eventi e gruppo di consumer usando il modello di Azure Resource Manager

In questo articolo viene illustrato come toouse un modello di gestione risorse di Azure che crea uno spazio dei nomi di tipo hub eventi, con l'hub di un evento e un gruppo di consumer. Hello articolo viene illustrato come toodefine quali risorse vengono distribuite come toodefine parametri e che vengono specificati quando è eseguita la distribuzione di hello. È possibile utilizzare questo modello per la propria distribuzioni o personalizzarlo toomeet i requisiti

Per altre informazioni sulla creazione dei modelli, vedere [Creazione di modelli di Azure Resource Manager][Authoring Azure Resource Manager templates].

Per il modello di hello completo, vedere hello [modello gruppo di hub e consumer di eventi] [ Event Hub and consumer group template] su GitHub.

> [!NOTE]
> toocheck per i modelli più recenti di hello, visitare hello [modelli di avvio rapido di Azure] [ Azure Quickstart Templates] raccolta e la ricerca per gli hub eventi.
> 
> 

## <a name="what-will-you-deploy"></a>Distribuzione
Questo modello consente di distribuire uno spazio dei nomi di Hub eventi con un hub eventi e un gruppo di consumer.

[Hub eventi](event-hubs-what-is-event-hubs.md) è un evento di elaborazione del servizio utilizzato tooprovide eventi e dati di telemetria in ingresso tooAzure su larga scala, con bassa latenza e affidabilità elevata.

toorun hello automaticamente la distribuzione, fare clic su hello seguente pulsante:

[![Distribuire tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)

## <a name="parameters"></a>parameters
Con Gestione risorse di Azure, si definiscono i parametri per i valori si desidera toospecify quando viene distribuito il modello di hello. modello Hello include una sezione denominata `Parameters` che contiene tutti i valori di parametro hello. È necessario definire un parametro per i valori che possono variare, basato su progetto hello che si distribuisce o su hello ambiente toowhich che si sta distribuendo. Non definire parametri per i valori che restano sempre hello stesso. Ogni valore del parametro nel modello hello definisce le risorse hello distribuite.

modello di Hello definisce hello seguenti parametri:

### <a name="eventhubnamespacename"></a>eventHubNamespaceName
nome Hello del toocreate dello spazio dei nomi di hello hub eventi.

```json
"eventHubNamespaceName": {
"type": "string"
}
```

### <a name="eventhubname"></a>eventHubName
nome Hello dell'hub di eventi hello creato nello spazio dei nomi di hello hub eventi.

```json
"eventHubName": {
"type": "string"
}
```

### <a name="eventhubconsumergroupname"></a>eventHubConsumerGroupName
nome Hello del gruppo di consumer hello creato per l'hub di eventi hello.

```json
"eventHubConsumerGroupName": {
"type": "string"
}
```

### <a name="apiversion"></a>apiVersion
versione di Hello API del modello di hello.

```json
"apiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a>Risorse toodeploy
Crea uno spazio dei nomi di tipo **Hub eventi**con un hub eventi e un gruppo di consumer.

```json
"resources":[  
      {  
         "apiVersion":"[variables('ehVersion')]",
         "name":"[parameters('namespaceName')]",
         "type":"Microsoft.EventHub/namespaces",
         "location":"[variables('location')]",
         "sku":{  
            "name":"Standard",
            "tier":"Standard"
         },
         "resources":[  
            {  
               "apiVersion":"[variables('ehVersion')]",
               "name":"[parameters('eventHubName')]",
               "type":"EventHubs",
               "dependsOn":[  
                  "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
               ],
               "properties":{  
                  "path":"[parameters('eventHubName')]"
               },
               "resources":[  
                  {  
                     "apiVersion":"[variables('ehVersion')]",
                     "name":"[parameters('consumerGroupName')]",
                     "type":"ConsumerGroups",
                     "dependsOn":[  
                        "[parameters('eventHubName')]"
                     ],
                     "properties":{  

                     }
                  }
               ]
            }
         ]
      }
   ],
```

## <a name="commands-toorun-deployment"></a>Comandi toorun distribuzione
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a>PowerShell
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json
```

## <a name="azure-cli"></a>Interfaccia della riga di comando di Azure
```cli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json][]
```

## <a name="next-steps"></a>Passaggi successivi
Sono disponibili ulteriori informazioni sugli hub di eventi visitando hello seguenti collegamenti:

* [Panoramica di Hub eventi](event-hubs-what-is-event-hubs.md)
* [Creare un hub eventi](event-hubs-create.md)
* [Domande frequenti su Hub eventi](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Using Azure PowerShell with Azure Resource Manager]: ../powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../xplat-cli-azure-resource-manager.md
[Event hub and consumer group template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-event-hubs-create-event-hub-and-consumer-group/
