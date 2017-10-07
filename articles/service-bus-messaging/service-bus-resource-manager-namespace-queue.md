---
title: spazio dei nomi Service Bus di Azure aaaCreate e mettere in coda utilizzando il modello di gestione risorse di Azure | Documenti Microsoft
description: Creare uno spazio dei nomi e una coda del bus di servizio tramite il modello di Azure Resource Manager
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a6bfb5fd-7b98-4588-8aa1-9d5f91b599b6
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: f230878b7c557bdd80d74da0de5a85ba4ee99ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-and-a-queue-using-an-azure-resource-manager-template"></a>Creare uno spazio dei nomi e una coda del bus di servizio tramite il modello di Azure Resource Manager

In questo articolo viene illustrato come toouse un modello di gestione risorse di Azure che crea uno spazio dei nomi del Bus di servizio e una coda nello spazio dei nomi. Si apprenderà come toodefine quali risorse vengono distribuite come toodefine parametri e che vengono specificati quando è eseguita la distribuzione di hello. È possibile utilizzare questo modello per la propria distribuzioni o personalizzarlo toomeet esigenze.

Per altre informazioni sulla creazione di modelli, vedere [Creazione di modelli di Azure Resource Manager][Authoring Azure Resource Manager templates].

Per il modello di hello completo, vedere hello [modello dello spazio dei nomi e coda di Service Bus] [ Service Bus namespace and queue template] su GitHub.

> [!NOTE]
> Hello seguenti modelli di gestione risorse di Azure sono disponibile per il download e distribuzione.
> 
> * [Creare uno spazio dei nomi del bus di servizio con coda e regola di autorizzazione](service-bus-resource-manager-namespace-auth-rule.md)
> * [Creare uno spazio dei nomi del bus di servizio con argomento e sottoscrizione](service-bus-resource-manager-namespace-topic.md)
> * [Creare uno spazio dei nomi del bus di servizio](service-bus-resource-manager-namespace.md)
> * [Creare uno spazio dei nomi del bus di servizio con argomento, sottoscrizione e regola](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> toocheck per i modelli più recenti di hello, visitare hello [modelli di avvio rapido di Azure] [ Azure Quickstart Templates] raccolta e cercare "Bus di servizio".
> 
> 

## <a name="what-will-you-deploy"></a>Distribuzione

Questo modello consente di distribuire uno spazio dei nomi del bus di servizio con una coda.

[Le code del Bus di servizio](service-bus-queues-topics-subscriptions.md#queues) offrono First In, tooone di recapito di messaggi FIFO (First Out) o più consumer concorrenti.

toorun hello automaticamente la distribuzione, fare clic su hello seguente pulsante:

[![Distribuire tooAzure](./media/service-bus-resource-manager-namespace-queue/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-queue%2Fazuredeploy.json)

## <a name="parameters"></a>parameters

Con Gestione risorse di Azure, si definiscono i parametri per i valori si desidera toospecify quando viene distribuito il modello di hello. modello Hello include una sezione denominata `Parameters` che contiene tutti i valori di parametro hello. È necessario definire un parametro per i valori che variano in base progetto hello che si distribuisce o Hello che si distribuisce ambiente di hello. Non definire parametri per i valori che saranno sempre hello stesso. Ogni valore del parametro viene utilizzato in hello modello toodefine hello le risorse distribuite.

modello di Hello definisce hello seguenti parametri.

### <a name="servicebusnamespacename"></a>serviceBusNamespaceName
nome Hello del toocreate di spazio dei nomi Service Bus hello.

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of hello Service Bus namespace" 
    }
}
```

### <a name="servicebusqueuename"></a>serviceBusQueueName
nome Hello della coda di hello creata nello spazio dei nomi Service Bus hello.

```json
"serviceBusQueueName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a>serviceBusApiVersion
versione di API di Service Bus Hello del modello di hello.

```json
"serviceBusApiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a>Risorse toodeploy
Crea uno spazio dei nomi del bus di servizio standard di tipo **Messaggistica**con una coda.

```json
"resources ": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "resources": [{
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusQueueName')]",
            "type": "Queues",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusQueueName')]",
            }
        }]
    }]
```

## <a name="commands-toorun-deployment"></a>Comandi toorun distribuzione
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a>PowerShell

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-queue/azuredeploy.json>
```

## <a name="azure-cli"></a>Interfaccia della riga di comando di Azure

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-queue/azuredeploy.json>
```

## <a name="next-steps"></a>Passaggi successivi
Dopo aver creato e distribuito risorse usando Gestione risorse di Azure, consultare come toomanage queste risorse visualizzando questi articoli:

* [Gestire Bus di servizio con PowerShell](service-bus-manage-with-ps.md)
* [Gestire le risorse di Service Bus con hello Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace and queue template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus queues]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
