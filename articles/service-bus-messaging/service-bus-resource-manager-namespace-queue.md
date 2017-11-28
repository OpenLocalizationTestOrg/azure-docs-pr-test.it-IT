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
# <a name="create-a-service-bus-namespace-and-a-queue-using-an-azure-resource-manager-template"></a><span data-ttu-id="fdbea-103">Creare uno spazio dei nomi e una coda del bus di servizio tramite il modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fdbea-103">Create a Service Bus namespace and a queue using an Azure Resource Manager template</span></span>

<span data-ttu-id="fdbea-104">In questo articolo viene illustrato come toouse un modello di gestione risorse di Azure che crea uno spazio dei nomi del Bus di servizio e una coda nello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="fdbea-104">This article shows how toouse an Azure Resource Manager template that creates a Service Bus namespace and a queue within that namespace.</span></span> <span data-ttu-id="fdbea-105">Si apprenderà come toodefine quali risorse vengono distribuite come toodefine parametri e che vengono specificati quando è eseguita la distribuzione di hello.</span><span class="sxs-lookup"><span data-stu-id="fdbea-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="fdbea-106">È possibile utilizzare questo modello per la propria distribuzioni o personalizzarlo toomeet esigenze.</span><span class="sxs-lookup"><span data-stu-id="fdbea-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="fdbea-107">Per altre informazioni sulla creazione di modelli, vedere [Creazione di modelli di Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="fdbea-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="fdbea-108">Per il modello di hello completo, vedere hello [modello dello spazio dei nomi e coda di Service Bus] [ Service Bus namespace and queue template] su GitHub.</span><span class="sxs-lookup"><span data-stu-id="fdbea-108">For hello complete template, see hello [Service Bus namespace and queue template][Service Bus namespace and queue template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="fdbea-109">Hello seguenti modelli di gestione risorse di Azure sono disponibile per il download e distribuzione.</span><span class="sxs-lookup"><span data-stu-id="fdbea-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="fdbea-110">Creare uno spazio dei nomi del bus di servizio con coda e regola di autorizzazione</span><span class="sxs-lookup"><span data-stu-id="fdbea-110">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="fdbea-111">Creare uno spazio dei nomi del bus di servizio con argomento e sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="fdbea-111">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="fdbea-112">Creare uno spazio dei nomi del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="fdbea-112">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="fdbea-113">Creare uno spazio dei nomi del bus di servizio con argomento, sottoscrizione e regola</span><span class="sxs-lookup"><span data-stu-id="fdbea-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="fdbea-114">toocheck per i modelli più recenti di hello, visitare hello [modelli di avvio rapido di Azure] [ Azure Quickstart Templates] raccolta e cercare "Bus di servizio".</span><span class="sxs-lookup"><span data-stu-id="fdbea-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="fdbea-115">Distribuzione</span><span class="sxs-lookup"><span data-stu-id="fdbea-115">What will you deploy?</span></span>

<span data-ttu-id="fdbea-116">Questo modello consente di distribuire uno spazio dei nomi del bus di servizio con una coda.</span><span class="sxs-lookup"><span data-stu-id="fdbea-116">With this template, you will deploy a Service Bus namespace with a queue.</span></span>

<span data-ttu-id="fdbea-117">[Le code del Bus di servizio](service-bus-queues-topics-subscriptions.md#queues) offrono First In, tooone di recapito di messaggi FIFO (First Out) o più consumer concorrenti.</span><span class="sxs-lookup"><span data-stu-id="fdbea-117">[Service Bus queues](service-bus-queues-topics-subscriptions.md#queues) offer First In, First Out (FIFO) message delivery tooone or more competing consumers.</span></span>

<span data-ttu-id="fdbea-118">toorun hello automaticamente la distribuzione, fare clic su hello seguente pulsante:</span><span class="sxs-lookup"><span data-stu-id="fdbea-118">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="fdbea-119">[![Distribuire tooAzure](./media/service-bus-resource-manager-namespace-queue/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-queue%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="fdbea-119">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-queue/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-queue%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="fdbea-120">parameters</span><span class="sxs-lookup"><span data-stu-id="fdbea-120">Parameters</span></span>

<span data-ttu-id="fdbea-121">Con Gestione risorse di Azure, si definiscono i parametri per i valori si desidera toospecify quando viene distribuito il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="fdbea-121">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="fdbea-122">modello Hello include una sezione denominata `Parameters` che contiene tutti i valori di parametro hello.</span><span class="sxs-lookup"><span data-stu-id="fdbea-122">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="fdbea-123">È necessario definire un parametro per i valori che variano in base progetto hello che si distribuisce o Hello che si distribuisce ambiente di hello.</span><span class="sxs-lookup"><span data-stu-id="fdbea-123">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="fdbea-124">Non definire parametri per i valori che saranno sempre hello stesso.</span><span class="sxs-lookup"><span data-stu-id="fdbea-124">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="fdbea-125">Ogni valore del parametro viene utilizzato in hello modello toodefine hello le risorse distribuite.</span><span class="sxs-lookup"><span data-stu-id="fdbea-125">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="fdbea-126">modello di Hello definisce hello seguenti parametri.</span><span class="sxs-lookup"><span data-stu-id="fdbea-126">hello template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="fdbea-127">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="fdbea-127">serviceBusNamespaceName</span></span>
<span data-ttu-id="fdbea-128">nome Hello del toocreate di spazio dei nomi Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="fdbea-128">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of hello Service Bus namespace" 
    }
}
```

### <a name="servicebusqueuename"></a><span data-ttu-id="fdbea-129">serviceBusQueueName</span><span class="sxs-lookup"><span data-stu-id="fdbea-129">serviceBusQueueName</span></span>
<span data-ttu-id="fdbea-130">nome Hello della coda di hello creata nello spazio dei nomi Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="fdbea-130">hello name of hello queue created in hello Service Bus namespace.</span></span>

```json
"serviceBusQueueName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="fdbea-131">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="fdbea-131">serviceBusApiVersion</span></span>
<span data-ttu-id="fdbea-132">versione di API di Service Bus Hello del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="fdbea-132">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a><span data-ttu-id="fdbea-133">Risorse toodeploy</span><span class="sxs-lookup"><span data-stu-id="fdbea-133">Resources toodeploy</span></span>
<span data-ttu-id="fdbea-134">Crea uno spazio dei nomi del bus di servizio standard di tipo **Messaggistica**con una coda.</span><span class="sxs-lookup"><span data-stu-id="fdbea-134">Creates a standard Service Bus namespace of type **Messaging**, with a queue.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="fdbea-135">Comandi toorun distribuzione</span><span class="sxs-lookup"><span data-stu-id="fdbea-135">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="fdbea-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fdbea-136">PowerShell</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-queue/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="fdbea-137">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="fdbea-137">Azure CLI</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-queue/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="fdbea-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fdbea-138">Next steps</span></span>
<span data-ttu-id="fdbea-139">Dopo aver creato e distribuito risorse usando Gestione risorse di Azure, consultare come toomanage queste risorse visualizzando questi articoli:</span><span class="sxs-lookup"><span data-stu-id="fdbea-139">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="fdbea-140">Gestire Bus di servizio con PowerShell</span><span class="sxs-lookup"><span data-stu-id="fdbea-140">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="fdbea-141">Gestire le risorse di Service Bus con hello Service Bus Explorer</span><span class="sxs-lookup"><span data-stu-id="fdbea-141">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace and queue template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus queues]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
