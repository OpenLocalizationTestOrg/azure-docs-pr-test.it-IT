---
title: aaaCreate sottoscrizione argomento del Bus di servizio di Azure e di regole utilizzando il modello di gestione risorse di Azure | Documenti Microsoft
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
ms.openlocfilehash: dbc46da8491aee4d0c73bd4db90c696008920df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-with-topic-subscription-and-rule-using-an-azure-resource-manager-template"></a><span data-ttu-id="91a3d-103">Creare uno spazio dei nomi del bus di servizio con argomento, sottoscrizione e regola usando un modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="91a3d-103">Create a Service Bus namespace with topic, subscription, and rule using an Azure Resource Manager template</span></span>

<span data-ttu-id="91a3d-104">In questo articolo viene illustrato come toouse un modello di gestione risorse di Azure che crea uno spazio dei nomi del Bus di servizio con un argomento, sottoscrizione e regola (filtro).</span><span class="sxs-lookup"><span data-stu-id="91a3d-104">This article shows how toouse an Azure Resource Manager template that creates a Service Bus namespace with a topic, subscription, and rule (filter).</span></span> <span data-ttu-id="91a3d-105">Si apprenderà come toodefine quali risorse vengono distribuite come toodefine parametri e che vengono specificati quando è eseguita la distribuzione di hello.</span><span class="sxs-lookup"><span data-stu-id="91a3d-105">You learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="91a3d-106">È possibile utilizzare questo modello per la propria distribuzioni o personalizzarlo toomeet i requisiti</span><span class="sxs-lookup"><span data-stu-id="91a3d-106">You can use this template for your own deployments, or customize it toomeet your requirements</span></span>

<span data-ttu-id="91a3d-107">Per altre informazioni sulla creazione dei modelli, vedere [Creazione di modelli di Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="91a3d-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="91a3d-108">Per altre informazioni su procedure e modelli relativi alle convenzioni di denominazione delle risorse di Azure, vedere [Recommended naming conventions for Azure resources][Recommended naming conventions for Azure resources] (Convenzioni di denominazione consigliate per le risorse di Azure).</span><span class="sxs-lookup"><span data-stu-id="91a3d-108">For more information about practice and patterns on Azure resources naming conventions, see [Recommended naming conventions for Azure resources][Recommended naming conventions for Azure resources].</span></span>

<span data-ttu-id="91a3d-109">Per il modello di hello completo, vedere hello [spazio dei nomi Service Bus con argomento, sottoscrizione e regola] [ Service Bus namespace with topic, subscription, and rule] modello.</span><span class="sxs-lookup"><span data-stu-id="91a3d-109">For hello complete template, see hello [Service Bus namespace with topic, subscription, and rule][Service Bus namespace with topic, subscription, and rule] template.</span></span>

> [!NOTE]
> <span data-ttu-id="91a3d-110">Hello seguenti modelli di gestione risorse di Azure sono disponibile per il download e distribuzione.</span><span class="sxs-lookup"><span data-stu-id="91a3d-110">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="91a3d-111">Creare uno spazio dei nomi del bus di servizio con coda e regola di autorizzazione</span><span class="sxs-lookup"><span data-stu-id="91a3d-111">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="91a3d-112">Creare uno spazio dei nomi del bus di servizio con coda</span><span class="sxs-lookup"><span data-stu-id="91a3d-112">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="91a3d-113">Creare uno spazio dei nomi del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="91a3d-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="91a3d-114">Creare uno spazio dei nomi del bus di servizio con argomento e sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="91a3d-114">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> 
> <span data-ttu-id="91a3d-115">toocheck per i modelli più recenti di hello, visitare hello [modelli di avvio rapido di Azure] [ Azure Quickstart Templates] raccolta e la ricerca per il Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="91a3d-115">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="91a3d-116">Distribuzione</span><span class="sxs-lookup"><span data-stu-id="91a3d-116">What will you deploy?</span></span>

<span data-ttu-id="91a3d-117">Questo modello consente di distribuire uno spazio dei nomi del bus di servizio con un argomento, una sottoscrizione e una regola (filtro).</span><span class="sxs-lookup"><span data-stu-id="91a3d-117">With this template, you deploy a Service Bus namespace with topic, subscription, and rule (filter).</span></span>

<span data-ttu-id="91a3d-118">Gli [argomenti e le sottoscrizioni del bus di servizio](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) offrono una forma di comunicazione uno-a-molti, in un schema di *pubblicazione/sottoscrizione*.</span><span class="sxs-lookup"><span data-stu-id="91a3d-118">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span> <span data-ttu-id="91a3d-119">Quando si usano argomenti e sottoscrizioni, i componenti di un'applicazione distribuita non comunicano direttamente tra loro, invece scambiano messaggi tramite l'argomento che funge da intermediario. Un argomento tooa sottoscrizione simile a una coda virtuale che riceve copie dei messaggi inviati toohello argomento.</span><span class="sxs-lookup"><span data-stu-id="91a3d-119">When using topics and subscriptions, components of a distributed application do not communicate directly with each other, instead they exchange messages via topic that acts as an intermediary.A subscription tooa topic resembles a virtual queue that receives copies of messages that were sent toohello topic.</span></span> <span data-ttu-id="91a3d-120">Un filtro di sottoscrizione consente toospecify cui i messaggi inviati tooa argomento deve trovarsi all'interno di una sottoscrizione di argomento specifico.</span><span class="sxs-lookup"><span data-stu-id="91a3d-120">A filter on subscription enables you toospecify which messages sent tooa topic should appear within a specific topic subscription.</span></span>

## <a name="what-are-rules-filters"></a><span data-ttu-id="91a3d-121">Che cosa sono le regole (filtri)?</span><span class="sxs-lookup"><span data-stu-id="91a3d-121">What are rules (filters)?</span></span>

<span data-ttu-id="91a3d-122">In molti scenari, i messaggi con caratteristiche specifiche devono essere elaborati in modi specifici.</span><span class="sxs-lookup"><span data-stu-id="91a3d-122">In many scenarios, messages that have specific characteristics must be processed in different ways.</span></span> <span data-ttu-id="91a3d-123">tooenable, è possibile configurare i messaggi toofind le sottoscrizioni che dispongono di proprietà specifica e quindi eseguono proprietà toothose modifiche.</span><span class="sxs-lookup"><span data-stu-id="91a3d-123">tooenable this, you can configure subscriptions toofind messages that have specific properties and then perform modifications toothose properties.</span></span> <span data-ttu-id="91a3d-124">Sebbene le sottoscrizioni del Bus di servizio vedere tutti i messaggi inviati toohello argomento, è possibile copiare solo un subset della coda di sottoscrizione virtuale toohello tali messaggi.</span><span class="sxs-lookup"><span data-stu-id="91a3d-124">Although Service Bus subscriptions see all messages sent toohello topic, you can only copy a subset of those messages toohello virtual subscription queue.</span></span> <span data-ttu-id="91a3d-125">Questa operazione viene eseguita usando i filtri della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="91a3d-125">This is accomplished using subscription filters.</span></span> <span data-ttu-id="91a3d-126">toolearn più sulle regole (filtri), vedere [regole e le azioni](service-bus-queues-topics-subscriptions.md#rules-and-actions).</span><span class="sxs-lookup"><span data-stu-id="91a3d-126">toolearn more about rules (filters), see [Rules and actions](service-bus-queues-topics-subscriptions.md#rules-and-actions).</span></span>

<span data-ttu-id="91a3d-127">toorun hello automaticamente la distribuzione, fare clic su hello seguente pulsante:</span><span class="sxs-lookup"><span data-stu-id="91a3d-127">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="91a3d-128">[![Distribuire tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="91a3d-128">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="91a3d-129">parameters</span><span class="sxs-lookup"><span data-stu-id="91a3d-129">Parameters</span></span>

<span data-ttu-id="91a3d-130">Con Gestione risorse di Azure, è consigliabile definire parametri per i valori si desidera toospecify quando viene distribuito il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="91a3d-130">With Azure Resource Manager, you should define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="91a3d-131">modello Hello include una sezione denominata `Parameters` che contiene tutti i valori di parametro hello.</span><span class="sxs-lookup"><span data-stu-id="91a3d-131">hello template includes a section called `Parameters` that contains all hello parameter values.</span></span> <span data-ttu-id="91a3d-132">È necessario definire un parametro per i valori che variano in base progetto hello che si distribuisce o Hello che si distribuisce ambiente di hello.</span><span class="sxs-lookup"><span data-stu-id="91a3d-132">You should define a parameter for those values that vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="91a3d-133">Non definire parametri per i valori che restano sempre hello stesso.</span><span class="sxs-lookup"><span data-stu-id="91a3d-133">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="91a3d-134">Ogni valore del parametro viene utilizzato in hello modello toodefine hello le risorse distribuite.</span><span class="sxs-lookup"><span data-stu-id="91a3d-134">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="91a3d-135">modello di Hello definisce hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="91a3d-135">hello template defines hello following parameters:</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="91a3d-136">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="91a3d-136">serviceBusNamespaceName</span></span>
<span data-ttu-id="91a3d-137">nome Hello del toocreate di spazio dei nomi Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="91a3d-137">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a><span data-ttu-id="91a3d-138">serviceBusTopicName</span><span class="sxs-lookup"><span data-stu-id="91a3d-138">serviceBusTopicName</span></span>
<span data-ttu-id="91a3d-139">nome Hello dell'argomento hello creato nello spazio dei nomi Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="91a3d-139">hello name of hello topic created in hello Service Bus namespace.</span></span>

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a><span data-ttu-id="91a3d-140">serviceBusSubscriptionName</span><span class="sxs-lookup"><span data-stu-id="91a3d-140">serviceBusSubscriptionName</span></span>
<span data-ttu-id="91a3d-141">nome Hello della sottoscrizione di hello creato nello spazio dei nomi Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="91a3d-141">hello name of hello subscription created in hello Service Bus namespace.</span></span>

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```
### <a name="servicebusrulename"></a><span data-ttu-id="91a3d-142">serviceBusRuleName</span><span class="sxs-lookup"><span data-stu-id="91a3d-142">serviceBusRuleName</span></span>
<span data-ttu-id="91a3d-143">nome Hello di hello rule(filter) creato nello spazio dei nomi Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="91a3d-143">hello name of hello rule(filter) created in hello Service Bus namespace.</span></span>

```json
   "serviceBusRuleName": {
   "type": "string",
  }
```
### <a name="servicebusapiversion"></a><span data-ttu-id="91a3d-144">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="91a3d-144">serviceBusApiVersion</span></span>
<span data-ttu-id="91a3d-145">versione di API di Service Bus Hello del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="91a3d-145">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-toodeploy"></a><span data-ttu-id="91a3d-146">Risorse toodeploy</span><span class="sxs-lookup"><span data-stu-id="91a3d-146">Resources toodeploy</span></span>
<span data-ttu-id="91a3d-147">Crea uno spazio dei nomi del bus di servizio standard di tipo **Messaggistica** con argomento, sottoscrizione e regole.</span><span class="sxs-lookup"><span data-stu-id="91a3d-147">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription and rules.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="91a3d-148">Comandi toorun distribuzione</span><span class="sxs-lookup"><span data-stu-id="91a3d-148">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="91a3d-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="91a3d-149">PowerShell</span></span>
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="91a3d-150">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="91a3d-150">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="91a3d-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="91a3d-151">Next steps</span></span>
<span data-ttu-id="91a3d-152">Dopo aver creato e distribuito risorse usando Gestione risorse di Azure, consultare come toomanage queste risorse visualizzando questi articoli:</span><span class="sxs-lookup"><span data-stu-id="91a3d-152">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="91a3d-153">Gestire i bus di servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="91a3d-153">Manage Azure Service Bus</span></span>](service-bus-management-libraries.md)
* [<span data-ttu-id="91a3d-154">Gestire Bus di servizio con PowerShell</span><span class="sxs-lookup"><span data-stu-id="91a3d-154">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="91a3d-155">Gestire le risorse di Service Bus con hello Service Bus Explorer</span><span class="sxs-lookup"><span data-stu-id="91a3d-155">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Recommended naming conventions for Azure resources]: ../guidance/guidance-naming-conventions.md
[Service Bus namespace with topic, subscription, and rule]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-subscription-rule/
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md

