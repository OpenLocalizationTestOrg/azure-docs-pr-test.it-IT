---
title: Creare una regola di autorizzazione del bus di servizio usando un modello di Azure Resource Manager | Documentazione Microsoft
description: Creare una regola di autorizzazione del bus di servizio per spazio dei nomi e coda usando un modello di Azure Resource Manager
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 7f1443a0-5fa8-4d90-8637-1a977ef0b1f0
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: fbd2372829a1aefa2c080c0a8a72b9ff4375b16f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-bus-authorization-rule-for-namespace-and-queue-using-an-azure-resource-manager-template"></a><span data-ttu-id="1025f-103">Creare una regola di autorizzazione del bus di servizio per spazio dei nomi e coda usando un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1025f-103">Create a Service Bus authorization rule for namespace and queue using an Azure Resource Manager template</span></span>

<span data-ttu-id="1025f-104">Questo articolo illustra come usare un modello di Azure Resource Manager per creare una [regola di autorizzazione](service-bus-authentication-and-authorization.md#shared-access-signature-authentication) per uno spazio dei nomi e una coda del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="1025f-104">This article shows how to use an Azure Resource Manager template that creates an [authorization rule](service-bus-authentication-and-authorization.md#shared-access-signature-authentication) for a Service Bus namespace and queue.</span></span> <span data-ttu-id="1025f-105">Verrà illustrato come definire le risorse da distribuire e i parametri specificati quando viene eseguita la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="1025f-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="1025f-106">È possibile usare questo modello per le proprie distribuzioni o personalizzarlo in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="1025f-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="1025f-107">Per altre informazioni sulla creazione di modelli, vedere [Creazione di modelli di Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="1025f-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="1025f-108">Per il modello completo, vedere il [modello della regola di autorizzazione del bus di servizio][Service Bus auth rule template] su GitHub.</span><span class="sxs-lookup"><span data-stu-id="1025f-108">For the complete template, see the [Service Bus authorization rule template][Service Bus auth rule template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="1025f-109">Questi modelli di Azure Resource Manager sono disponibili per il download e la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="1025f-109">The following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="1025f-110">Creare uno spazio dei nomi del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="1025f-110">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="1025f-111">Creare uno spazio dei nomi del bus di servizio con coda</span><span class="sxs-lookup"><span data-stu-id="1025f-111">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="1025f-112">Creare uno spazio dei nomi del bus di servizio con argomento e sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="1025f-112">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="1025f-113">Creare uno spazio dei nomi del bus di servizio con argomento, sottoscrizione e regola</span><span class="sxs-lookup"><span data-stu-id="1025f-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="1025f-114">Per verificare gli ultimi modelli, visitare la raccolta [Modelli di avvio rapido di Azure][Azure Quickstart Templates] e cercare "service bus".</span><span class="sxs-lookup"><span data-stu-id="1025f-114">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="1025f-115">Distribuzione</span><span class="sxs-lookup"><span data-stu-id="1025f-115">What will you deploy?</span></span>
<span data-ttu-id="1025f-116">Questo modello consente di distribuire una regola di autorizzazione del bus di servizio per uno spazio dei nomi e un'identità di messaggistica (in questo caso, una coda).</span><span class="sxs-lookup"><span data-stu-id="1025f-116">With this template, you will deploy a Service Bus authorization rule for a namespace and messaging entity (in this case, a queue).</span></span>

<span data-ttu-id="1025f-117">Questo modello usa la [firma di accesso condiviso (SAS, Shared Access Signature)](service-bus-sas.md) per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="1025f-117">This template uses [Shared Access Signature (SAS)](service-bus-sas.md) for authentication.</span></span> <span data-ttu-id="1025f-118">La firma di accesso condiviso consente alle applicazione di eseguire l'autenticazione al bus di servizio usando una chiave di accesso configurata nello spazio dei nomi o nell'entità di messaggistica, ad esempio coda o argomento, a cui sono associati diritti specifici.</span><span class="sxs-lookup"><span data-stu-id="1025f-118">SAS enables applications to authenticate to Service Bus using an access key configured on the namespace, or on the messaging entity (queue or topic) with which specific rights are associated.</span></span> <span data-ttu-id="1025f-119">È quindi possibile usare questa chiave per generare un token di firma di accesso condiviso di cui possono avvalersi i client per eseguire l'autenticazione al bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="1025f-119">You can then use this key to generate a SAS token that clients can in turn use to authenticate to Service Bus.</span></span>

<span data-ttu-id="1025f-120">Per eseguire automaticamente la distribuzione, fare clic sul pulsante seguente:</span><span class="sxs-lookup"><span data-stu-id="1025f-120">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="1025f-121">[![Distribuzione in Azure](./media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="1025f-121">[![Deploy to Azure](./media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="1025f-122">Parametri</span><span class="sxs-lookup"><span data-stu-id="1025f-122">Parameters</span></span>

<span data-ttu-id="1025f-123">Gestione risorse di Azure permette di definire i parametri per i valori da specificare durante la distribuzione del modello.</span><span class="sxs-lookup"><span data-stu-id="1025f-123">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="1025f-124">Il modello include una sezione denominata `Parameters` che contiene tutti i valori dei parametri.</span><span class="sxs-lookup"><span data-stu-id="1025f-124">The template includes a section called `Parameters` that contains all of the parameter values.</span></span> <span data-ttu-id="1025f-125">È necessario definire un parametro per i valori che variano in base al progetto distribuito o all'ambiente in cui viene distribuito il progetto.</span><span class="sxs-lookup"><span data-stu-id="1025f-125">You should define a parameter for those values that will vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="1025f-126">Non definire i parametri per i valori che rimangono invariati.</span><span class="sxs-lookup"><span data-stu-id="1025f-126">Do not define parameters for values that will always stay the same.</span></span> <span data-ttu-id="1025f-127">Ogni valore di parametro nel modello viene usato per definire le risorse distribuite.</span><span class="sxs-lookup"><span data-stu-id="1025f-127">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="1025f-128">Il modello definisce i parametri seguenti.</span><span class="sxs-lookup"><span data-stu-id="1025f-128">The template defines the following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="1025f-129">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="1025f-129">serviceBusNamespaceName</span></span>
<span data-ttu-id="1025f-130">Nome dello spazio dei nomi del bus di servizio da creare.</span><span class="sxs-lookup"><span data-stu-id="1025f-130">The name of the Service Bus namespace to create.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="namespaceauthorizationrulename"></a><span data-ttu-id="1025f-131">namespaceAuthorizationRuleName</span><span class="sxs-lookup"><span data-stu-id="1025f-131">namespaceAuthorizationRuleName</span></span>
<span data-ttu-id="1025f-132">Nome della regola di autorizzazione per lo spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="1025f-132">The name of the authorization rule for the namespace.</span></span>

```json
"namespaceAuthorizationRuleName ": {
"type": "string"
}
```

### <a name="servicebusqueuename"></a><span data-ttu-id="1025f-133">serviceBusQueueName</span><span class="sxs-lookup"><span data-stu-id="1025f-133">serviceBusQueueName</span></span>
<span data-ttu-id="1025f-134">Nome della coda nello spazio dei nomi del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="1025f-134">The name of the queue in the Service Bus namespace.</span></span>

```json
"serviceBusQueueName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="1025f-135">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="1025f-135">serviceBusApiVersion</span></span>
<span data-ttu-id="1025f-136">Versione API del bus di servizio del modello.</span><span class="sxs-lookup"><span data-stu-id="1025f-136">The Service Bus API version of the template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```

## <a name="resources-to-deploy"></a><span data-ttu-id="1025f-137">Risorse da distribuire</span><span class="sxs-lookup"><span data-stu-id="1025f-137">Resources to deploy</span></span>
<span data-ttu-id="1025f-138">Crea uno spazio dei nomi del bus di servizio standard di tipo **Messaggistica**e una regola di autorizzazione del bus di servizio per spazio dei nomi ed entità.</span><span class="sxs-lookup"><span data-stu-id="1025f-138">Creates a standard Service Bus namespace of type **Messaging**, and a Service Bus authorization rule for namespace and entity.</span></span>

```json
"resources": [
        {
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusNamespaceName')]",
            "type": "Microsoft.ServiceBus/namespaces",
            "location": "[variables('location')]",
            "kind": "Messaging",
            "sku": {
                "name": "StandardSku",
                "tier": "Standard"
            },
            "resources": [
                {
                    "apiVersion": "[variables('sbVersion')]",
                    "name": "[parameters('serviceBusQueueName')]",
                    "type": "Queues",
                    "dependsOn": [
                        "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
                    ],
                    "properties": {
                        "path": "[parameters('serviceBusQueueName')]"
                    },
                    "resources": [
                        {
                            "apiVersion": "[variables('sbVersion')]",
                            "name": "[parameters('queueAuthorizationRuleName')]",
                            "type": "authorizationRules",
                            "dependsOn": [
                                "[parameters('serviceBusQueueName')]"
                            ],
                            "properties": {
                                "Rights": ["Listen"]
                            }
                        }
                    ]
                }
            ]
        }, {
            "apiVersion": "[variables('sbVersion')]",
            "name": "[variables('namespaceAuthRuleName')]",
            "type": "Microsoft.ServiceBus/namespaces/authorizationRules",
            "dependsOn": ["[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"],
            "location": "[resourceGroup().location]",
            "properties": {
                "Rights": ["Send"]
            }
        }
    ]
```

## <a name="commands-to-run-deployment"></a><span data-ttu-id="1025f-139">Comandi per eseguire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="1025f-139">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="1025f-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1025f-140">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="1025f-141">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="1025f-141">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="1025f-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1025f-142">Next steps</span></span>
<span data-ttu-id="1025f-143">Dopo aver creato e distribuito le risorse con Azure Resource Manager, è possibile imparare a gestire queste risorse. Leggere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="1025f-143">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="1025f-144">Gestire Bus di servizio con PowerShell</span><span class="sxs-lookup"><span data-stu-id="1025f-144">Manage Service Bus with PowerShell</span></span>](service-bus-powershell-how-to-provision.md)
* [<span data-ttu-id="1025f-145">Gestire le risorse del bus di servizio con Service Bus Explorer</span><span class="sxs-lookup"><span data-stu-id="1025f-145">Manage Service Bus resources with the Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)
* [<span data-ttu-id="1025f-146">Autenticazione e autorizzazione del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="1025f-146">Service Bus authentication and authorization</span></span>](service-bus-authentication-and-authorization.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus auth rule template]: https://github.com/Azure/azure-quickstart-templates/blob/master/301-servicebus-create-authrule-namespace-and-queue/
