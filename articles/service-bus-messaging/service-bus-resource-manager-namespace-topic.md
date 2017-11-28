---
title: aaaCreate sottoscrizione dell'argomento dello spazio dei nomi Service Bus di Azure utilizzando il modello di gestione risorse di Azure | Documenti Microsoft
description: Creare uno spazio dei nomi del bus di servizio con argomento e sottoscrizione usando un modello di Azure Resource Manager
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: d3d55200-5c60-4b5f-822d-59974cafff0e
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: 9b5f7d8710e598b73c0a7ea3daf8c300f7fa9ecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-with-topic-and-subscription-using-an-azure-resource-manager-template"></a><span data-ttu-id="bd5ab-103">Creare uno spazio dei nomi del bus di servizio con argomento e sottoscrizione usando un modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bd5ab-103">Create a Service Bus namespace with topic and subscription using an Azure Resource Manager template</span></span>

<span data-ttu-id="bd5ab-104">In questo articolo viene illustrato come toouse un modello di gestione risorse di Azure che crea uno spazio dei nomi del Bus di servizio e un argomento e una sottoscrizione all'interno di tale spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="bd5ab-104">This article shows how toouse an Azure Resource Manager template that creates a Service Bus namespace and a topic and subscription within that namespace.</span></span> <span data-ttu-id="bd5ab-105">Si apprenderà come toodefine quali risorse vengono distribuite come toodefine parametri e che vengono specificati quando è eseguita la distribuzione di hello.</span><span class="sxs-lookup"><span data-stu-id="bd5ab-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="bd5ab-106">È possibile utilizzare questo modello per la propria distribuzioni o personalizzarlo toomeet i requisiti</span><span class="sxs-lookup"><span data-stu-id="bd5ab-106">You can use this template for your own deployments, or customize it toomeet your requirements</span></span>

<span data-ttu-id="bd5ab-107">Per altre informazioni sulla creazione di modelli, vedere [Creazione di modelli di Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="bd5ab-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="bd5ab-108">Per il modello di hello completo, vedere hello [spazio dei nomi Service Bus con argomento e sottoscrizione] [ Service Bus namespace with topic and subscription] modello.</span><span class="sxs-lookup"><span data-stu-id="bd5ab-108">For hello complete template, see hello [Service Bus namespace with topic and subscription][Service Bus namespace with topic and subscription] template.</span></span>

> [!NOTE]
> <span data-ttu-id="bd5ab-109">Hello seguenti modelli di gestione risorse di Azure sono disponibile per il download e distribuzione.</span><span class="sxs-lookup"><span data-stu-id="bd5ab-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="bd5ab-110">Creare uno spazio dei nomi del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="bd5ab-110">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="bd5ab-111">Creare uno spazio dei nomi del bus di servizio con coda</span><span class="sxs-lookup"><span data-stu-id="bd5ab-111">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="bd5ab-112">Creare uno spazio dei nomi del bus di servizio con coda e regola di autorizzazione</span><span class="sxs-lookup"><span data-stu-id="bd5ab-112">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="bd5ab-113">Creare uno spazio dei nomi del bus di servizio con argomento, sottoscrizione e regola</span><span class="sxs-lookup"><span data-stu-id="bd5ab-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="bd5ab-114">toocheck per i modelli più recenti di hello, visitare hello [modelli di avvio rapido di Azure] [ Azure Quickstart Templates] raccolta e cercare "Bus di servizio".</span><span class="sxs-lookup"><span data-stu-id="bd5ab-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="bd5ab-115">Distribuzione</span><span class="sxs-lookup"><span data-stu-id="bd5ab-115">What will you deploy?</span></span>

<span data-ttu-id="bd5ab-116">Questo modello consente di distribuire uno spazio dei nomi del bus di servizio con un argomento e una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="bd5ab-116">With this template, you will deploy a Service Bus namespace with topic and subscription.</span></span>

<span data-ttu-id="bd5ab-117">Gli [argomenti e le sottoscrizioni del bus di servizio](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) offrono una forma di comunicazione uno-a-molti, in un schema di *pubblicazione/sottoscrizione*.</span><span class="sxs-lookup"><span data-stu-id="bd5ab-117">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span>

<span data-ttu-id="bd5ab-118">toorun hello automaticamente la distribuzione, fare clic su hello seguente pulsante:</span><span class="sxs-lookup"><span data-stu-id="bd5ab-118">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="bd5ab-119">[![Distribuire tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="bd5ab-119">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="bd5ab-120">parameters</span><span class="sxs-lookup"><span data-stu-id="bd5ab-120">Parameters</span></span>

<span data-ttu-id="bd5ab-121">Con Gestione risorse di Azure, si definiscono i parametri per i valori si desidera toospecify quando viene distribuito il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="bd5ab-121">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="bd5ab-122">modello Hello include una sezione denominata `Parameters` che contiene tutti i valori di parametro hello.</span><span class="sxs-lookup"><span data-stu-id="bd5ab-122">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="bd5ab-123">È necessario definire un parametro per i valori che variano in base progetto hello che si distribuisce o Hello che si distribuisce ambiente di hello.</span><span class="sxs-lookup"><span data-stu-id="bd5ab-123">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="bd5ab-124">Non definire parametri per i valori che saranno sempre hello stesso.</span><span class="sxs-lookup"><span data-stu-id="bd5ab-124">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="bd5ab-125">Ogni valore del parametro viene utilizzato in hello modello toodefine hello le risorse distribuite.</span><span class="sxs-lookup"><span data-stu-id="bd5ab-125">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="bd5ab-126">modello di Hello definisce hello seguenti parametri.</span><span class="sxs-lookup"><span data-stu-id="bd5ab-126">hello template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="bd5ab-127">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="bd5ab-127">serviceBusNamespaceName</span></span>
<span data-ttu-id="bd5ab-128">nome Hello del toocreate di spazio dei nomi Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="bd5ab-128">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a><span data-ttu-id="bd5ab-129">serviceBusTopicName</span><span class="sxs-lookup"><span data-stu-id="bd5ab-129">serviceBusTopicName</span></span>
<span data-ttu-id="bd5ab-130">nome Hello dell'argomento hello creato nello spazio dei nomi Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="bd5ab-130">hello name of hello topic created in hello Service Bus namespace.</span></span>

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a><span data-ttu-id="bd5ab-131">serviceBusSubscriptionName</span><span class="sxs-lookup"><span data-stu-id="bd5ab-131">serviceBusSubscriptionName</span></span>
<span data-ttu-id="bd5ab-132">nome Hello della sottoscrizione di hello creato nello spazio dei nomi Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="bd5ab-132">hello name of hello subscription created in hello Service Bus namespace.</span></span>

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="bd5ab-133">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="bd5ab-133">serviceBusApiVersion</span></span>
<span data-ttu-id="bd5ab-134">versione di API di Service Bus Hello del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="bd5ab-134">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-toodeploy"></a><span data-ttu-id="bd5ab-135">Risorse toodeploy</span><span class="sxs-lookup"><span data-stu-id="bd5ab-135">Resources toodeploy</span></span>
<span data-ttu-id="bd5ab-136">Crea uno spazio dei nomi del bus di servizio standard di tipo **Messaggistica**con un argomento e una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="bd5ab-136">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription.</span></span>

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
            "name": "[parameters('serviceBusTopicName')]",
            "type": "Topics",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusTopicName')]",
            },
            "resources": [{
                "apiVersion": "[variables('sbVersion')]",
                "name": "[parameters('serviceBusSubscriptionName')]",
                "type": "Subscriptions",
                "dependsOn": [
                    "[parameters('serviceBusTopicName')]"
                ],
                "properties": {}
            }]
        }]
    }]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="bd5ab-137">Comandi toorun distribuzione</span><span class="sxs-lookup"><span data-stu-id="bd5ab-137">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="bd5ab-138">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd5ab-138">PowerShell</span></span>
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="bd5ab-139">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="bd5ab-139">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="bd5ab-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bd5ab-140">Next steps</span></span>
<span data-ttu-id="bd5ab-141">Dopo aver creato e distribuito risorse usando Gestione risorse di Azure, consultare come toomanage queste risorse visualizzando questi articoli:</span><span class="sxs-lookup"><span data-stu-id="bd5ab-141">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="bd5ab-142">Gestire Bus di servizio con PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd5ab-142">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="bd5ab-143">Gestire le risorse di Service Bus con hello Service Bus Explorer</span><span class="sxs-lookup"><span data-stu-id="bd5ab-143">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus namespace with topic and subscription]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-and-subscription/
