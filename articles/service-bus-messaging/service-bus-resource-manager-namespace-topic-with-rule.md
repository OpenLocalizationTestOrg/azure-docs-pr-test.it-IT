---
title: Creare una sottoscrizione di argomento e una regola del bus di servizio di Azure tramite un modello di Azure Resource Manager | Documentazione Microsoft
description: Creare uno spazio dei nomi del bus di servizio con argomento, sottoscrizione e regola usando un modello di Azure Resource Manager
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 9e0aaf58-0214-4bca-bd00-d29c08f9b1bc
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: 35e67d86b42358c4ce28b41beae1ee8e1896e939
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-bus-namespace-with-topic-subscription-and-rule-using-an-azure-resource-manager-template"></a><span data-ttu-id="37d2c-103">Creare uno spazio dei nomi del bus di servizio con argomento, sottoscrizione e regola usando un modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="37d2c-103">Create a Service Bus namespace with topic, subscription, and rule using an Azure Resource Manager template</span></span>

<span data-ttu-id="37d2c-104">Questo articolo illustra come usare un modello di Azure Resource Manager per creare uno spazio dei nomi del bus di servizio con un argomento, una sottoscrizione e una regola (filtro).</span><span class="sxs-lookup"><span data-stu-id="37d2c-104">This article shows how to use an Azure Resource Manager template that creates a Service Bus namespace with a topic, subscription, and rule (filter).</span></span> <span data-ttu-id="37d2c-105">Illustra inoltre le modalità di definizione delle risorse da distribuire e dei parametri specificati durante l'esecuzione della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="37d2c-105">You learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="37d2c-106">È possibile usare questo modello per la distribuzione o personalizzarlo in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="37d2c-106">You can use this template for your own deployments, or customize it to meet your requirements</span></span>

<span data-ttu-id="37d2c-107">Per altre informazioni sulla creazione dei modelli, vedere [Creazione di modelli di Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="37d2c-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="37d2c-108">Per altre informazioni su procedure e modelli relativi alle convenzioni di denominazione delle risorse di Azure, vedere [Recommended naming conventions for Azure resources][Recommended naming conventions for Azure resources] (Convenzioni di denominazione consigliate per le risorse di Azure).</span><span class="sxs-lookup"><span data-stu-id="37d2c-108">For more information about practice and patterns on Azure resources naming conventions, see [Recommended naming conventions for Azure resources][Recommended naming conventions for Azure resources].</span></span>

<span data-ttu-id="37d2c-109">Per il modello completo, vedere il [modello dello spazio dei nomi del bus di servizio con argomento, sottoscrizione e regola][Service Bus namespace with topic, subscription, and rule] su GitHub.</span><span class="sxs-lookup"><span data-stu-id="37d2c-109">For the complete template, see the [Service Bus namespace with topic, subscription, and rule][Service Bus namespace with topic, subscription, and rule] template.</span></span>

> [!NOTE]
> <span data-ttu-id="37d2c-110">Questi modelli di Azure Resource Manager sono disponibili per il download e la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="37d2c-110">The following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="37d2c-111">Creare uno spazio dei nomi del bus di servizio con coda e regola di autorizzazione</span><span class="sxs-lookup"><span data-stu-id="37d2c-111">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="37d2c-112">Creare uno spazio dei nomi del bus di servizio con coda</span><span class="sxs-lookup"><span data-stu-id="37d2c-112">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="37d2c-113">Creare uno spazio dei nomi del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="37d2c-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="37d2c-114">Creare uno spazio dei nomi del bus di servizio con argomento e sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="37d2c-114">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> 
> <span data-ttu-id="37d2c-115">Per verificare la disponibilità di nuovi modelli, visitare la raccolta [Modelli di avvio rapido di Azure][Azure Quickstart Templates] e cercare "service bus".</span><span class="sxs-lookup"><span data-stu-id="37d2c-115">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="37d2c-116">Distribuzione</span><span class="sxs-lookup"><span data-stu-id="37d2c-116">What will you deploy?</span></span>

<span data-ttu-id="37d2c-117">Questo modello consente di distribuire uno spazio dei nomi del bus di servizio con un argomento, una sottoscrizione e una regola (filtro).</span><span class="sxs-lookup"><span data-stu-id="37d2c-117">With this template, you deploy a Service Bus namespace with topic, subscription, and rule (filter).</span></span>

<span data-ttu-id="37d2c-118">Gli [argomenti e le sottoscrizioni del bus di servizio](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) offrono una forma di comunicazione uno-a-molti, in un schema di *pubblicazione/sottoscrizione*.</span><span class="sxs-lookup"><span data-stu-id="37d2c-118">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span> <span data-ttu-id="37d2c-119">Quando si usano gli argomenti e le sottoscrizioni, i componenti di un'applicazione distribuita non comunicano direttamente tra loro, ma scambiano messaggi tramite un argomento, che agisce da intermediario. La sottoscrizione a un argomento è simile a una coda virtuale che riceve copie dei messaggi che sono stati inviati all'argomento.</span><span class="sxs-lookup"><span data-stu-id="37d2c-119">When using topics and subscriptions, components of a distributed application do not communicate directly with each other, instead they exchange messages via topic that acts as an intermediary.A subscription to a topic resembles a virtual queue that receives copies of messages that were sent to the topic.</span></span> <span data-ttu-id="37d2c-120">L'applicazione di un filtro a una sottoscrizione consente di specificare quali messaggi inviati a un argomento devono essere presenti in una specifica sottoscrizione dell'argomento.</span><span class="sxs-lookup"><span data-stu-id="37d2c-120">A filter on subscription enables you to specify which messages sent to a topic should appear within a specific topic subscription.</span></span>

## <a name="what-are-rules-filters"></a><span data-ttu-id="37d2c-121">Che cosa sono le regole (filtri)?</span><span class="sxs-lookup"><span data-stu-id="37d2c-121">What are rules (filters)?</span></span>

<span data-ttu-id="37d2c-122">In molti scenari, i messaggi con caratteristiche specifiche devono essere elaborati in modi specifici.</span><span class="sxs-lookup"><span data-stu-id="37d2c-122">In many scenarios, messages that have specific characteristics must be processed in different ways.</span></span> <span data-ttu-id="37d2c-123">A questo scopo è possibile configurare le sottoscrizioni in modo che trovino i messaggi che presentano le proprietà specifiche e apportare quindi modifiche a tali proprietà.</span><span class="sxs-lookup"><span data-stu-id="37d2c-123">To enable this, you can configure subscriptions to find messages that have specific properties and then perform modifications to those properties.</span></span> <span data-ttu-id="37d2c-124">Anche se nelle sottoscrizioni del bus di servizio tutti i messaggi vengono inviati all'argomento, l'utente può copiare solo un sottoinsieme di tali messaggi nella coda virtuale delle sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="37d2c-124">Although Service Bus subscriptions see all messages sent to the topic, you can only copy a subset of those messages to the virtual subscription queue.</span></span> <span data-ttu-id="37d2c-125">Questa operazione viene eseguita usando i filtri della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="37d2c-125">This is accomplished using subscription filters.</span></span> <span data-ttu-id="37d2c-126">Per altre informazioni sulle regole (filtri), vedere [Regole e azioni](service-bus-queues-topics-subscriptions.md#rules-and-actions).</span><span class="sxs-lookup"><span data-stu-id="37d2c-126">To learn more about rules (filters), see [Rules and actions](service-bus-queues-topics-subscriptions.md#rules-and-actions).</span></span>

<span data-ttu-id="37d2c-127">Per eseguire automaticamente la distribuzione, fare clic sul pulsante seguente:</span><span class="sxs-lookup"><span data-stu-id="37d2c-127">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="37d2c-128">[![Distribuzione in Azure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="37d2c-128">[![Deploy to Azure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="37d2c-129">Parametri</span><span class="sxs-lookup"><span data-stu-id="37d2c-129">Parameters</span></span>

<span data-ttu-id="37d2c-130">Con Azure Resource Manager è necessario definire i parametri per i valori da specificare durante la distribuzione del modello.</span><span class="sxs-lookup"><span data-stu-id="37d2c-130">With Azure Resource Manager, you should define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="37d2c-131">Il modello include una sezione denominata `Parameters` che contiene tutti i valori dei parametri.</span><span class="sxs-lookup"><span data-stu-id="37d2c-131">The template includes a section called `Parameters` that contains all the parameter values.</span></span> <span data-ttu-id="37d2c-132">È necessario definire un parametro per i valori che variano in base al progetto distribuito o all'ambiente in cui viene distribuito il progetto.</span><span class="sxs-lookup"><span data-stu-id="37d2c-132">You should define a parameter for those values that vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="37d2c-133">Non definire i parametri per i valori che rimangono invariati.</span><span class="sxs-lookup"><span data-stu-id="37d2c-133">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="37d2c-134">Ogni valore di parametro nel modello viene usato per definire le risorse distribuite.</span><span class="sxs-lookup"><span data-stu-id="37d2c-134">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="37d2c-135">Il modello definisce i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="37d2c-135">The template defines the following parameters:</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="37d2c-136">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="37d2c-136">serviceBusNamespaceName</span></span>
<span data-ttu-id="37d2c-137">Nome dello spazio dei nomi del bus di servizio da creare.</span><span class="sxs-lookup"><span data-stu-id="37d2c-137">The name of the Service Bus namespace to create.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a><span data-ttu-id="37d2c-138">serviceBusTopicName</span><span class="sxs-lookup"><span data-stu-id="37d2c-138">serviceBusTopicName</span></span>
<span data-ttu-id="37d2c-139">Nome dell'argomento creato nello spazio dei nomi del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="37d2c-139">The name of the topic created in the Service Bus namespace.</span></span>

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a><span data-ttu-id="37d2c-140">serviceBusSubscriptionName</span><span class="sxs-lookup"><span data-stu-id="37d2c-140">serviceBusSubscriptionName</span></span>
<span data-ttu-id="37d2c-141">Nome della sottoscrizione creata nello spazio dei nomi del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="37d2c-141">The name of the subscription created in the Service Bus namespace.</span></span>

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```
### <a name="servicebusrulename"></a><span data-ttu-id="37d2c-142">serviceBusRuleName</span><span class="sxs-lookup"><span data-stu-id="37d2c-142">serviceBusRuleName</span></span>
<span data-ttu-id="37d2c-143">Nome della regola (filtro) creata nello spazio dei nomi del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="37d2c-143">The name of the rule(filter) created in the Service Bus namespace.</span></span>

```json
   "serviceBusRuleName": {
   "type": "string",
  }
```
### <a name="servicebusapiversion"></a><span data-ttu-id="37d2c-144">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="37d2c-144">serviceBusApiVersion</span></span>
<span data-ttu-id="37d2c-145">Versione API del bus di servizio del modello.</span><span class="sxs-lookup"><span data-stu-id="37d2c-145">The Service Bus API version of the template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-to-deploy"></a><span data-ttu-id="37d2c-146">Risorse da distribuire</span><span class="sxs-lookup"><span data-stu-id="37d2c-146">Resources to deploy</span></span>
<span data-ttu-id="37d2c-147">Crea uno spazio dei nomi del bus di servizio standard di tipo **Messaggistica** con argomento, sottoscrizione e regole.</span><span class="sxs-lookup"><span data-stu-id="37d2c-147">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription and rules.</span></span>

```json
 "resources": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "sku": {
            "name": "Standard",
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
                "path": "[parameters('serviceBusTopicName')]"
            },
            "resources": [{
                "apiVersion": "[variables('sbVersion')]",
                "name": "[parameters('serviceBusSubscriptionName')]",
                "type": "Subscriptions",
                "dependsOn": [
                    "[parameters('serviceBusTopicName')]"
                ],
                "properties": {},
                "resources": [{
                    "apiVersion": "[variables('sbVersion')]",
                    "name": "[parameters('serviceBusRuleName')]",
                    "type": "Rules",
                    "dependsOn": [
                        "[parameters('serviceBusSubscriptionName')]"
                    ],
                    "properties": {
                        "filter": {
                            "sqlExpression": "StoreName = 'Store1'"
                        },
                        "action": {
                            "sqlExpression": "set FilterTag = 'true'"
                        }
                    }
                }]
            }]
        }]
    }]
```

## <a name="commands-to-run-deployment"></a><span data-ttu-id="37d2c-148">Comandi per eseguire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="37d2c-148">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="37d2c-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="37d2c-149">PowerShell</span></span>
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="37d2c-150">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="37d2c-150">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="37d2c-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="37d2c-151">Next steps</span></span>
<span data-ttu-id="37d2c-152">Dopo aver creato e distribuito le risorse con Azure Resource Manager, è possibile imparare a gestire queste risorse. Leggere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="37d2c-152">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="37d2c-153">Gestire i bus di servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="37d2c-153">Manage Azure Service Bus</span></span>](service-bus-management-libraries.md)
* [<span data-ttu-id="37d2c-154">Gestire Bus di servizio con PowerShell</span><span class="sxs-lookup"><span data-stu-id="37d2c-154">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="37d2c-155">Gestire le risorse del bus di servizio con Service Bus Explorer</span><span class="sxs-lookup"><span data-stu-id="37d2c-155">Manage Service Bus resources with the Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Recommended naming conventions for Azure resources]: ../guidance/guidance-naming-conventions.md
[Service Bus namespace with topic, subscription, and rule]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-subscription-rule/
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md

