---
title: regola di autorizzazione aaaCreate Bus di servizio utilizzando il modello di gestione risorse di Azure | Documenti Microsoft
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
ms.openlocfilehash: 48df97849281d3b47e9d722d4e821c874644be59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-authorization-rule-for-namespace-and-queue-using-an-azure-resource-manager-template"></a><span data-ttu-id="e56a3-103">Creare una regola di autorizzazione del bus di servizio per spazio dei nomi e coda usando un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e56a3-103">Create a Service Bus authorization rule for namespace and queue using an Azure Resource Manager template</span></span>

<span data-ttu-id="e56a3-104">Questo articolo viene illustrato come toouse un modello di gestione risorse di Azure che crea un [regola di autorizzazione](service-bus-authentication-and-authorization.md#shared-access-signature-authentication) per un spazio dei nomi Service Bus e una coda.</span><span class="sxs-lookup"><span data-stu-id="e56a3-104">This article shows how toouse an Azure Resource Manager template that creates an [authorization rule](service-bus-authentication-and-authorization.md#shared-access-signature-authentication) for a Service Bus namespace and queue.</span></span> <span data-ttu-id="e56a3-105">Si apprenderà come toodefine quali risorse vengono distribuite come toodefine parametri e che vengono specificati quando è eseguita la distribuzione di hello.</span><span class="sxs-lookup"><span data-stu-id="e56a3-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="e56a3-106">È possibile utilizzare questo modello per la propria distribuzioni o personalizzarlo toomeet esigenze.</span><span class="sxs-lookup"><span data-stu-id="e56a3-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="e56a3-107">Per altre informazioni sulla creazione di modelli, vedere [Creazione di modelli di Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="e56a3-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="e56a3-108">Per il modello di hello completo, vedere hello [modello di regola di autorizzazione di Service Bus] [ Service Bus auth rule template] su GitHub.</span><span class="sxs-lookup"><span data-stu-id="e56a3-108">For hello complete template, see hello [Service Bus authorization rule template][Service Bus auth rule template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="e56a3-109">Hello seguenti modelli di gestione risorse di Azure sono disponibile per il download e distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e56a3-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="e56a3-110">Creare uno spazio dei nomi del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="e56a3-110">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="e56a3-111">Creare uno spazio dei nomi del bus di servizio con coda</span><span class="sxs-lookup"><span data-stu-id="e56a3-111">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="e56a3-112">Creare uno spazio dei nomi del bus di servizio con argomento e sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="e56a3-112">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="e56a3-113">Creare uno spazio dei nomi del bus di servizio con argomento, sottoscrizione e regola</span><span class="sxs-lookup"><span data-stu-id="e56a3-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="e56a3-114">toocheck per i modelli più recenti di hello, visitare hello [modelli di avvio rapido di Azure] [ Azure Quickstart Templates] raccolta e cercare "Bus di servizio".</span><span class="sxs-lookup"><span data-stu-id="e56a3-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="e56a3-115">Distribuzione</span><span class="sxs-lookup"><span data-stu-id="e56a3-115">What will you deploy?</span></span>
<span data-ttu-id="e56a3-116">Questo modello consente di distribuire una regola di autorizzazione del bus di servizio per uno spazio dei nomi e un'identità di messaggistica (in questo caso, una coda).</span><span class="sxs-lookup"><span data-stu-id="e56a3-116">With this template, you will deploy a Service Bus authorization rule for a namespace and messaging entity (in this case, a queue).</span></span>

<span data-ttu-id="e56a3-117">Questo modello usa la [firma di accesso condiviso (SAS, Shared Access Signature)](service-bus-sas.md) per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="e56a3-117">This template uses [Shared Access Signature (SAS)](service-bus-sas.md) for authentication.</span></span> <span data-ttu-id="e56a3-118">Firma di accesso condiviso consente applicazioni tooauthenticate tooService Bus usando una chiave di accesso configurata nello spazio dei nomi hello o in hello messaggistica entità (coda o argomento) con cui sono associati diritti specifici.</span><span class="sxs-lookup"><span data-stu-id="e56a3-118">SAS enables applications tooauthenticate tooService Bus using an access key configured on hello namespace, or on hello messaging entity (queue or topic) with which specific rights are associated.</span></span> <span data-ttu-id="e56a3-119">È quindi possibile utilizzare questa chiave toogenerate un token di firma di accesso condiviso che i client possono utilizzare tooauthenticate tooService Bus.</span><span class="sxs-lookup"><span data-stu-id="e56a3-119">You can then use this key toogenerate a SAS token that clients can in turn use tooauthenticate tooService Bus.</span></span>

<span data-ttu-id="e56a3-120">toorun hello automaticamente la distribuzione, fare clic su hello seguente pulsante:</span><span class="sxs-lookup"><span data-stu-id="e56a3-120">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="e56a3-121">[![Distribuire tooAzure](./media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="e56a3-121">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="e56a3-122">parameters</span><span class="sxs-lookup"><span data-stu-id="e56a3-122">Parameters</span></span>

<span data-ttu-id="e56a3-123">Con Gestione risorse di Azure, si definiscono i parametri per i valori si desidera toospecify quando viene distribuito il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="e56a3-123">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="e56a3-124">modello Hello include una sezione denominata `Parameters` che contiene tutti i valori di parametro hello.</span><span class="sxs-lookup"><span data-stu-id="e56a3-124">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="e56a3-125">È necessario definire un parametro per i valori che variano in base progetto hello che si distribuisce o Hello che si distribuisce ambiente di hello.</span><span class="sxs-lookup"><span data-stu-id="e56a3-125">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="e56a3-126">Non definire parametri per i valori che saranno sempre hello stesso.</span><span class="sxs-lookup"><span data-stu-id="e56a3-126">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="e56a3-127">Ogni valore del parametro viene utilizzato in hello modello toodefine hello le risorse distribuite.</span><span class="sxs-lookup"><span data-stu-id="e56a3-127">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="e56a3-128">modello di Hello definisce hello seguenti parametri.</span><span class="sxs-lookup"><span data-stu-id="e56a3-128">hello template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="e56a3-129">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="e56a3-129">serviceBusNamespaceName</span></span>
<span data-ttu-id="e56a3-130">nome Hello del toocreate di spazio dei nomi Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="e56a3-130">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="namespaceauthorizationrulename"></a><span data-ttu-id="e56a3-131">namespaceAuthorizationRuleName</span><span class="sxs-lookup"><span data-stu-id="e56a3-131">namespaceAuthorizationRuleName</span></span>
<span data-ttu-id="e56a3-132">nome di Hello della regola di autorizzazione hello per hello dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="e56a3-132">hello name of hello authorization rule for hello namespace.</span></span>

```json
"namespaceAuthorizationRuleName ": {
"type": "string"
}
```

### <a name="servicebusqueuename"></a><span data-ttu-id="e56a3-133">serviceBusQueueName</span><span class="sxs-lookup"><span data-stu-id="e56a3-133">serviceBusQueueName</span></span>
<span data-ttu-id="e56a3-134">nome Hello della coda di hello nello spazio dei nomi Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="e56a3-134">hello name of hello queue in hello Service Bus namespace.</span></span>

```json
"serviceBusQueueName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="e56a3-135">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="e56a3-135">serviceBusApiVersion</span></span>
<span data-ttu-id="e56a3-136">versione di API di Service Bus Hello del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="e56a3-136">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a><span data-ttu-id="e56a3-137">Risorse toodeploy</span><span class="sxs-lookup"><span data-stu-id="e56a3-137">Resources toodeploy</span></span>
<span data-ttu-id="e56a3-138">Crea uno spazio dei nomi del bus di servizio standard di tipo **Messaggistica**e una regola di autorizzazione del bus di servizio per spazio dei nomi ed entità.</span><span class="sxs-lookup"><span data-stu-id="e56a3-138">Creates a standard Service Bus namespace of type **Messaging**, and a Service Bus authorization rule for namespace and entity.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="e56a3-139">Comandi toorun distribuzione</span><span class="sxs-lookup"><span data-stu-id="e56a3-139">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="e56a3-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e56a3-140">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="e56a3-141">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="e56a3-141">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="e56a3-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e56a3-142">Next steps</span></span>
<span data-ttu-id="e56a3-143">Dopo aver creato e distribuito risorse usando Gestione risorse di Azure, consultare come toomanage queste risorse visualizzando questi articoli:</span><span class="sxs-lookup"><span data-stu-id="e56a3-143">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="e56a3-144">Gestire Bus di servizio con PowerShell</span><span class="sxs-lookup"><span data-stu-id="e56a3-144">Manage Service Bus with PowerShell</span></span>](service-bus-powershell-how-to-provision.md)
* [<span data-ttu-id="e56a3-145">Gestire le risorse di Service Bus con hello Service Bus Explorer</span><span class="sxs-lookup"><span data-stu-id="e56a3-145">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)
* [<span data-ttu-id="e56a3-146">Autenticazione e autorizzazione del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="e56a3-146">Service Bus authentication and authorization</span></span>](service-bus-authentication-and-authorization.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus auth rule template]: https://github.com/Azure/azure-quickstart-templates/blob/master/301-servicebus-create-authrule-namespace-and-queue/
