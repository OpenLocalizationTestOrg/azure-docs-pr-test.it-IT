---
title: spazio dei nomi Service Bus aaaCreate utilizzando un modello di gestione risorse di Azure | Documenti Microsoft
description: Utilizzare Gestione risorse di Azure modello toocreate uno spazio dei nomi del Bus di servizio
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: dc0d6482-6344-4cef-8644-d4573639f5e4
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: fddf370affe761a734991ae9b60c1e5825e54ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-using-an-azure-resource-manager-template"></a>Creare uno spazio dei nomi del bus di servizio tramite il modello di Azure Resource Manager

In questo articolo descrive come toouse un modello di gestione risorse di Azure che crea uno spazio dei nomi Service Bus di tipo **messaggistica** con uno SKU Standard o Basic. articolo Hello definisce anche i parametri specificati per l'esecuzione della distribuzione hello hello hello. È possibile utilizzare questo modello per la propria distribuzioni o personalizzarlo toomeet esigenze.

Per altre informazioni sulla creazione di modelli, vedere [Creazione di modelli di Azure Resource Manager][Authoring Azure Resource Manager templates].

Per il modello di hello completo, vedere hello [modello dello spazio dei nomi Service Bus] [ Service Bus namespace template] su GitHub.

> [!NOTE]
> Hello seguenti modelli di gestione risorse di Azure sono disponibile per il download e distribuzione. 
> 
> * [Creare uno spazio dei nomi del bus di servizio con coda](service-bus-resource-manager-namespace-queue.md)
> * [Creare uno spazio dei nomi del bus di servizio con argomento e sottoscrizione](service-bus-resource-manager-namespace-topic.md)
> * [Creare uno spazio dei nomi del bus di servizio con coda e regola di autorizzazione](service-bus-resource-manager-namespace-auth-rule.md)
> * [Creare uno spazio dei nomi del bus di servizio con argomento, sottoscrizione e regola](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> toocheck per i modelli più recenti di hello, visitare hello [modelli di avvio rapido di Azure] [ Azure Quickstart Templates] raccolta e la ricerca per il Bus di servizio.
> 
> 

## <a name="what-will-you-deploy"></a>Distribuzione
Questo modello consente di distribuire uno spazio dei nomi del bus di servizio con uno SKU [Basic, Standard o Premium](https://azure.microsoft.com/pricing/details/service-bus/).

toorun hello automaticamente la distribuzione, fare clic su hello seguente pulsante:

[![Distribuire tooAzure](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)

## <a name="parameters"></a>parameters
Con Gestione risorse di Azure, si definiscono i parametri per i valori si desidera toospecify quando viene distribuito il modello di hello. modello Hello include una sezione denominata `Parameters` che contiene tutti i valori di parametro hello. È necessario definire un parametro per i valori che variano in base progetto hello che si distribuisce o Hello che si distribuisce ambiente di hello. Non definire parametri per i valori che saranno sempre hello stesso. Ogni valore del parametro viene utilizzato in hello modello toodefine hello le risorse distribuite.

Questo modello definisce hello seguenti parametri.

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

### <a name="servicebussku"></a>serviceBusSKU
nome Hello del Bus di servizio hello [SKU](https://azure.microsoft.com/pricing/details/service-bus/) toocreate.

```json
"serviceBusSku": { 
    "type": "string", 
    "allowedValues": [ 
        "Basic", 
        "Standard",
        "Premium" 
    ], 
    "defaultValue": "Standard", 
    "metadata": { 
        "description": "hello messaging tier for service Bus namespace" 
    } 

```

modello di Hello definisce i valori hello consentiti per questo parametro (Basic, Standard o Premium) e assegna un valore predefinito (Standard), se viene specificato alcun valore.

Per altre informazioni sui prezzi del bus di servizio, vedere [Service Bus pricing and billing][Service Bus pricing and billing] (Prezzi e fatturazione del bus di servizio).

### <a name="servicebusapiversion"></a>serviceBusApiVersion
versione di API di Service Bus Hello del modello di hello.

```json
"serviceBusApiVersion": { 
       "type": "string", 
       "defaultValue": "2015-08-01", 
       "metadata": { 
           "description": "Service Bus ApiVersion used by hello template" 
       } 
```

## <a name="resources-toodeploy"></a>Risorse toodeploy
### <a name="service-bus-namespace"></a>Spazio dei nomi del bus di servizio
Crea uno spazio dei nomi del bus di servizio standard di tipo **Messaggistica**.

```json
"resources": [
    {
        "apiVersion": "[parameters('serviceBusApiVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "properties": {
        }
    }
]
```

## <a name="commands-toorun-deployment"></a>Comandi toorun distribuzione
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName <resource-group-name> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

### <a name="azure-cli"></a>Interfaccia della riga di comando di Azure
```azurecli
azure config mode arm

azure group deployment create <my-resource-group> <my-deployment-name> --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

## <a name="next-steps"></a>Passaggi successivi
Dopo aver creato e distribuito risorse usando Gestione risorse di Azure, consultare come toomanage queste risorse, consultare questi articoli:

* [Gestire Bus di servizio con PowerShell](service-bus-manage-with-ps.md)
* [Gestire le risorse di Service Bus con hello Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace template]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-servicebus-create-namespace/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Service Bus pricing and billing]: service-bus-pricing-billing.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
