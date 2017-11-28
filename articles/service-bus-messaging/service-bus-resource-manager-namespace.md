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
# <a name="create-a-service-bus-namespace-using-an-azure-resource-manager-template"></a><span data-ttu-id="e055e-103">Creare uno spazio dei nomi del bus di servizio tramite il modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e055e-103">Create a Service Bus namespace using an Azure Resource Manager template</span></span>

<span data-ttu-id="e055e-104">In questo articolo descrive come toouse un modello di gestione risorse di Azure che crea uno spazio dei nomi Service Bus di tipo **messaggistica** con uno SKU Standard o Basic.</span><span class="sxs-lookup"><span data-stu-id="e055e-104">This article describes how toouse an Azure Resource Manager template that creates a Service Bus namespace of type **Messaging** with a Standard/Basic SKU.</span></span> <span data-ttu-id="e055e-105">articolo Hello definisce anche i parametri specificati per l'esecuzione della distribuzione hello hello hello.</span><span class="sxs-lookup"><span data-stu-id="e055e-105">hello article also defines hello parameters that are specified for hello execution of hello deployment.</span></span> <span data-ttu-id="e055e-106">È possibile utilizzare questo modello per la propria distribuzioni o personalizzarlo toomeet esigenze.</span><span class="sxs-lookup"><span data-stu-id="e055e-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="e055e-107">Per altre informazioni sulla creazione di modelli, vedere [Creazione di modelli di Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="e055e-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="e055e-108">Per il modello di hello completo, vedere hello [modello dello spazio dei nomi Service Bus] [ Service Bus namespace template] su GitHub.</span><span class="sxs-lookup"><span data-stu-id="e055e-108">For hello complete template, see hello [Service Bus namespace template][Service Bus namespace template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="e055e-109">Hello seguenti modelli di gestione risorse di Azure sono disponibile per il download e distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e055e-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span> 
> 
> * [<span data-ttu-id="e055e-110">Creare uno spazio dei nomi del bus di servizio con coda</span><span class="sxs-lookup"><span data-stu-id="e055e-110">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="e055e-111">Creare uno spazio dei nomi del bus di servizio con argomento e sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="e055e-111">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="e055e-112">Creare uno spazio dei nomi del bus di servizio con coda e regola di autorizzazione</span><span class="sxs-lookup"><span data-stu-id="e055e-112">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="e055e-113">Creare uno spazio dei nomi del bus di servizio con argomento, sottoscrizione e regola</span><span class="sxs-lookup"><span data-stu-id="e055e-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="e055e-114">toocheck per i modelli più recenti di hello, visitare hello [modelli di avvio rapido di Azure] [ Azure Quickstart Templates] raccolta e la ricerca per il Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="e055e-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="e055e-115">Distribuzione</span><span class="sxs-lookup"><span data-stu-id="e055e-115">What will you deploy?</span></span>
<span data-ttu-id="e055e-116">Questo modello consente di distribuire uno spazio dei nomi del bus di servizio con uno SKU [Basic, Standard o Premium](https://azure.microsoft.com/pricing/details/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="e055e-116">With this template, you will deploy a Service Bus namespace with a [Basic, Standard, or Premium](https://azure.microsoft.com/pricing/details/service-bus/) SKU.</span></span>

<span data-ttu-id="e055e-117">toorun hello automaticamente la distribuzione, fare clic su hello seguente pulsante:</span><span class="sxs-lookup"><span data-stu-id="e055e-117">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="e055e-118">[![Distribuire tooAzure](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="e055e-118">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="e055e-119">parameters</span><span class="sxs-lookup"><span data-stu-id="e055e-119">Parameters</span></span>
<span data-ttu-id="e055e-120">Con Gestione risorse di Azure, si definiscono i parametri per i valori si desidera toospecify quando viene distribuito il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="e055e-120">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="e055e-121">modello Hello include una sezione denominata `Parameters` che contiene tutti i valori di parametro hello.</span><span class="sxs-lookup"><span data-stu-id="e055e-121">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="e055e-122">È necessario definire un parametro per i valori che variano in base progetto hello che si distribuisce o Hello che si distribuisce ambiente di hello.</span><span class="sxs-lookup"><span data-stu-id="e055e-122">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="e055e-123">Non definire parametri per i valori che saranno sempre hello stesso.</span><span class="sxs-lookup"><span data-stu-id="e055e-123">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="e055e-124">Ogni valore del parametro viene utilizzato in hello modello toodefine hello le risorse distribuite.</span><span class="sxs-lookup"><span data-stu-id="e055e-124">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="e055e-125">Questo modello definisce hello seguenti parametri.</span><span class="sxs-lookup"><span data-stu-id="e055e-125">This template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="e055e-126">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="e055e-126">serviceBusNamespaceName</span></span>
<span data-ttu-id="e055e-127">nome Hello del toocreate di spazio dei nomi Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="e055e-127">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of hello Service Bus namespace" 
    }
}
```

### <a name="servicebussku"></a><span data-ttu-id="e055e-128">serviceBusSKU</span><span class="sxs-lookup"><span data-stu-id="e055e-128">serviceBusSKU</span></span>
<span data-ttu-id="e055e-129">nome Hello del Bus di servizio hello [SKU](https://azure.microsoft.com/pricing/details/service-bus/) toocreate.</span><span class="sxs-lookup"><span data-stu-id="e055e-129">hello name of hello Service Bus [SKU](https://azure.microsoft.com/pricing/details/service-bus/) toocreate.</span></span>

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

<span data-ttu-id="e055e-130">modello di Hello definisce i valori hello consentiti per questo parametro (Basic, Standard o Premium) e assegna un valore predefinito (Standard), se viene specificato alcun valore.</span><span class="sxs-lookup"><span data-stu-id="e055e-130">hello template defines hello values that are permitted for this parameter (Basic, Standard, or Premium) and assigns a default value (Standard) if no value is specified.</span></span>

<span data-ttu-id="e055e-131">Per altre informazioni sui prezzi del bus di servizio, vedere [Service Bus pricing and billing][Service Bus pricing and billing] (Prezzi e fatturazione del bus di servizio).</span><span class="sxs-lookup"><span data-stu-id="e055e-131">For more information about Service Bus pricing, see [Service Bus pricing and billing][Service Bus pricing and billing].</span></span>

### <a name="servicebusapiversion"></a><span data-ttu-id="e055e-132">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="e055e-132">serviceBusApiVersion</span></span>
<span data-ttu-id="e055e-133">versione di API di Service Bus Hello del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="e055e-133">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": { 
       "type": "string", 
       "defaultValue": "2015-08-01", 
       "metadata": { 
           "description": "Service Bus ApiVersion used by hello template" 
       } 
```

## <a name="resources-toodeploy"></a><span data-ttu-id="e055e-134">Risorse toodeploy</span><span class="sxs-lookup"><span data-stu-id="e055e-134">Resources toodeploy</span></span>
### <a name="service-bus-namespace"></a><span data-ttu-id="e055e-135">Spazio dei nomi del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="e055e-135">Service Bus namespace</span></span>
<span data-ttu-id="e055e-136">Crea uno spazio dei nomi del bus di servizio standard di tipo **Messaggistica**.</span><span class="sxs-lookup"><span data-stu-id="e055e-136">Creates a standard Service Bus namespace of type **Messaging**.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="e055e-137">Comandi toorun distribuzione</span><span class="sxs-lookup"><span data-stu-id="e055e-137">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="e055e-138">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e055e-138">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName <resource-group-name> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

### <a name="azure-cli"></a><span data-ttu-id="e055e-139">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="e055e-139">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create <my-resource-group> <my-deployment-name> --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

## <a name="next-steps"></a><span data-ttu-id="e055e-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e055e-140">Next steps</span></span>
<span data-ttu-id="e055e-141">Dopo aver creato e distribuito risorse usando Gestione risorse di Azure, consultare come toomanage queste risorse, consultare questi articoli:</span><span class="sxs-lookup"><span data-stu-id="e055e-141">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by reading these articles:</span></span>

* [<span data-ttu-id="e055e-142">Gestire Bus di servizio con PowerShell</span><span class="sxs-lookup"><span data-stu-id="e055e-142">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="e055e-143">Gestire le risorse di Service Bus con hello Service Bus Explorer</span><span class="sxs-lookup"><span data-stu-id="e055e-143">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace template]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-servicebus-create-namespace/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Service Bus pricing and billing]: service-bus-pricing-billing.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
