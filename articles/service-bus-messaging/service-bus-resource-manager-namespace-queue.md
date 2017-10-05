---
title: Creare uno spazio dei nomi del bus di servizio di Azure e una coda tramite il modello di Azure Resource Manager | Documentazione Microsoft
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
ms.openlocfilehash: 4358130a2c8e897a0fdd1f9560f766d6e22db4d2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-bus-namespace-and-a-queue-using-an-azure-resource-manager-template"></a><span data-ttu-id="7bef5-103">Creare uno spazio dei nomi e una coda del bus di servizio tramite il modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7bef5-103">Create a Service Bus namespace and a queue using an Azure Resource Manager template</span></span>

<span data-ttu-id="7bef5-104">Questo articolo illustra come usare un modello di Azure Resource Manager per creare uno spazio dei nomi e una coda del bus di servizio all'interno dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="7bef5-104">This article shows how to use an Azure Resource Manager template that creates a Service Bus namespace and a queue within that namespace.</span></span> <span data-ttu-id="7bef5-105">Verrà illustrato come definire le risorse da distribuire e i parametri specificati quando viene eseguita la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="7bef5-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="7bef5-106">È possibile usare questo modello per le proprie distribuzioni o personalizzarlo in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="7bef5-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="7bef5-107">Per altre informazioni sulla creazione di modelli, vedere [Creazione di modelli di Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="7bef5-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="7bef5-108">Per il modello completo, vedere il [modello dello spazio dei nomi e della coda del bus di servizio][Service Bus namespace and queue template] su GitHub.</span><span class="sxs-lookup"><span data-stu-id="7bef5-108">For the complete template, see the [Service Bus namespace and queue template][Service Bus namespace and queue template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="7bef5-109">Questi modelli di Azure Resource Manager sono disponibili per il download e la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="7bef5-109">The following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="7bef5-110">Creare uno spazio dei nomi del bus di servizio con coda e regola di autorizzazione</span><span class="sxs-lookup"><span data-stu-id="7bef5-110">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="7bef5-111">Creare uno spazio dei nomi del bus di servizio con argomento e sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="7bef5-111">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="7bef5-112">Creare uno spazio dei nomi del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="7bef5-112">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="7bef5-113">Creare uno spazio dei nomi del bus di servizio con argomento, sottoscrizione e regola</span><span class="sxs-lookup"><span data-stu-id="7bef5-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="7bef5-114">Per verificare gli ultimi modelli, visitare la raccolta [Modelli di avvio rapido di Azure][Azure Quickstart Templates] e cercare "service bus".</span><span class="sxs-lookup"><span data-stu-id="7bef5-114">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="7bef5-115">Distribuzione</span><span class="sxs-lookup"><span data-stu-id="7bef5-115">What will you deploy?</span></span>

<span data-ttu-id="7bef5-116">Questo modello consente di distribuire uno spazio dei nomi del bus di servizio con una coda.</span><span class="sxs-lookup"><span data-stu-id="7bef5-116">With this template, you will deploy a Service Bus namespace with a queue.</span></span>

<span data-ttu-id="7bef5-117">Le [code del bus di servizio](service-bus-queues-topics-subscriptions.md#queues) consentono un recapito dei messaggi di tipo FIFO (First In, First Out) a uno o più consumer concorrenti.</span><span class="sxs-lookup"><span data-stu-id="7bef5-117">[Service Bus queues](service-bus-queues-topics-subscriptions.md#queues) offer First In, First Out (FIFO) message delivery to one or more competing consumers.</span></span>

<span data-ttu-id="7bef5-118">Per eseguire automaticamente la distribuzione, fare clic sul pulsante seguente:</span><span class="sxs-lookup"><span data-stu-id="7bef5-118">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="7bef5-119">[![Distribuzione in Azure](./media/service-bus-resource-manager-namespace-queue/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-queue%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="7bef5-119">[![Deploy to Azure](./media/service-bus-resource-manager-namespace-queue/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-queue%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="7bef5-120">Parametri</span><span class="sxs-lookup"><span data-stu-id="7bef5-120">Parameters</span></span>

<span data-ttu-id="7bef5-121">Gestione risorse di Azure permette di definire i parametri per i valori da specificare durante la distribuzione del modello.</span><span class="sxs-lookup"><span data-stu-id="7bef5-121">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="7bef5-122">Il modello include una sezione denominata `Parameters` che contiene tutti i valori dei parametri.</span><span class="sxs-lookup"><span data-stu-id="7bef5-122">The template includes a section called `Parameters` that contains all of the parameter values.</span></span> <span data-ttu-id="7bef5-123">È necessario definire un parametro per i valori che variano in base al progetto distribuito o all'ambiente in cui viene distribuito il progetto.</span><span class="sxs-lookup"><span data-stu-id="7bef5-123">You should define a parameter for those values that will vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="7bef5-124">Non definire i parametri per i valori che rimangono invariati.</span><span class="sxs-lookup"><span data-stu-id="7bef5-124">Do not define parameters for values that will always stay the same.</span></span> <span data-ttu-id="7bef5-125">Ogni valore di parametro nel modello viene usato per definire le risorse distribuite.</span><span class="sxs-lookup"><span data-stu-id="7bef5-125">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="7bef5-126">Il modello definisce i parametri seguenti.</span><span class="sxs-lookup"><span data-stu-id="7bef5-126">The template defines the following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="7bef5-127">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="7bef5-127">serviceBusNamespaceName</span></span>
<span data-ttu-id="7bef5-128">Nome dello spazio dei nomi del bus di servizio da creare.</span><span class="sxs-lookup"><span data-stu-id="7bef5-128">The name of the Service Bus namespace to create.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of the Service Bus namespace" 
    }
}
```

### <a name="servicebusqueuename"></a><span data-ttu-id="7bef5-129">serviceBusQueueName</span><span class="sxs-lookup"><span data-stu-id="7bef5-129">serviceBusQueueName</span></span>
<span data-ttu-id="7bef5-130">Nome della coda creata nello spazio dei nomi del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="7bef5-130">The name of the queue created in the Service Bus namespace.</span></span>

```json
"serviceBusQueueName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="7bef5-131">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="7bef5-131">serviceBusApiVersion</span></span>
<span data-ttu-id="7bef5-132">Versione API del bus di servizio del modello.</span><span class="sxs-lookup"><span data-stu-id="7bef5-132">The Service Bus API version of the template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```

## <a name="resources-to-deploy"></a><span data-ttu-id="7bef5-133">Risorse da distribuire</span><span class="sxs-lookup"><span data-stu-id="7bef5-133">Resources to deploy</span></span>
<span data-ttu-id="7bef5-134">Crea uno spazio dei nomi del bus di servizio standard di tipo **Messaggistica**con una coda.</span><span class="sxs-lookup"><span data-stu-id="7bef5-134">Creates a standard Service Bus namespace of type **Messaging**, with a queue.</span></span>

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

## <a name="commands-to-run-deployment"></a><span data-ttu-id="7bef5-135">Comandi per eseguire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="7bef5-135">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="7bef5-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7bef5-136">PowerShell</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-queue/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="7bef5-137">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="7bef5-137">Azure CLI</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-queue/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="7bef5-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7bef5-138">Next steps</span></span>
<span data-ttu-id="7bef5-139">Dopo aver creato e distribuito le risorse con Azure Resource Manager, è possibile imparare a gestire queste risorse. Leggere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="7bef5-139">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="7bef5-140">Gestire Bus di servizio con PowerShell</span><span class="sxs-lookup"><span data-stu-id="7bef5-140">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="7bef5-141">Gestire le risorse del bus di servizio con Service Bus Explorer</span><span class="sxs-lookup"><span data-stu-id="7bef5-141">Manage Service Bus resources with the Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace and queue template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus queues]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
