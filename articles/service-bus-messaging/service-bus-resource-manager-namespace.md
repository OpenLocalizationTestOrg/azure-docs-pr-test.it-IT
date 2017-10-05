---
title: Creare uno spazio dei nomi del bus di servizio di Azure tramite un modello di Resource Manager | Documentazione Microsoft
description: Usare il modello di Azure Resource Manager per creare uno spazio dei nomi del bus di servizio
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
ms.openlocfilehash: 8fff390919a1807995646dab322b4cbe56dd0268
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-bus-namespace-using-an-azure-resource-manager-template"></a><span data-ttu-id="e7404-103">Creare uno spazio dei nomi del bus di servizio tramite il modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e7404-103">Create a Service Bus namespace using an Azure Resource Manager template</span></span>

<span data-ttu-id="e7404-104">Questo articolo illustra come usare un modello di Azure Resource Manager per creare uno spazio dei nomi del bus di servizio di tipo **Messaging** con SKU Standard/Basic.</span><span class="sxs-lookup"><span data-stu-id="e7404-104">This article describes how to use an Azure Resource Manager template that creates a Service Bus namespace of type **Messaging** with a Standard/Basic SKU.</span></span> <span data-ttu-id="e7404-105">L'articolo definisce anche i parametri specificati per eseguire la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e7404-105">The article also defines the parameters that are specified for the execution of the deployment.</span></span> <span data-ttu-id="e7404-106">È possibile usare questo modello per le proprie distribuzioni o personalizzarlo in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="e7404-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="e7404-107">Per altre informazioni sulla creazione di modelli, vedere [Creazione di modelli di Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="e7404-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="e7404-108">Per il modello completo, vedere il [modello dello spazio dei nomi del bus di servizio][Service Bus namespace template] su GitHub.</span><span class="sxs-lookup"><span data-stu-id="e7404-108">For the complete template, see the [Service Bus namespace template][Service Bus namespace template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="e7404-109">Questi modelli di Azure Resource Manager sono disponibili per il download e la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e7404-109">The following Azure Resource Manager templates are available for download and deployment.</span></span> 
> 
> * [<span data-ttu-id="e7404-110">Creare uno spazio dei nomi del bus di servizio con coda</span><span class="sxs-lookup"><span data-stu-id="e7404-110">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="e7404-111">Creare uno spazio dei nomi del bus di servizio con argomento e sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="e7404-111">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="e7404-112">Creare uno spazio dei nomi del bus di servizio con coda e regola di autorizzazione</span><span class="sxs-lookup"><span data-stu-id="e7404-112">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="e7404-113">Creare uno spazio dei nomi del bus di servizio con argomento, sottoscrizione e regola</span><span class="sxs-lookup"><span data-stu-id="e7404-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="e7404-114">Per verificare la disponibilità di nuovi modelli, visitare la raccolta [Modelli di avvio rapido di Azure][Azure Quickstart Templates] e cercare "service bus".</span><span class="sxs-lookup"><span data-stu-id="e7404-114">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="e7404-115">Distribuzione</span><span class="sxs-lookup"><span data-stu-id="e7404-115">What will you deploy?</span></span>
<span data-ttu-id="e7404-116">Questo modello consente di distribuire uno spazio dei nomi del bus di servizio con uno SKU [Basic, Standard o Premium](https://azure.microsoft.com/pricing/details/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="e7404-116">With this template, you will deploy a Service Bus namespace with a [Basic, Standard, or Premium](https://azure.microsoft.com/pricing/details/service-bus/) SKU.</span></span>

<span data-ttu-id="e7404-117">Per eseguire automaticamente la distribuzione, fare clic sul pulsante seguente:</span><span class="sxs-lookup"><span data-stu-id="e7404-117">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="e7404-118">[![Distribuzione in Azure](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="e7404-118">[![Deploy to Azure](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="e7404-119">Parametri</span><span class="sxs-lookup"><span data-stu-id="e7404-119">Parameters</span></span>
<span data-ttu-id="e7404-120">Gestione risorse di Azure permette di definire i parametri per i valori da specificare durante la distribuzione del modello.</span><span class="sxs-lookup"><span data-stu-id="e7404-120">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="e7404-121">Il modello include una sezione denominata `Parameters` che contiene tutti i valori dei parametri.</span><span class="sxs-lookup"><span data-stu-id="e7404-121">The template includes a section called `Parameters` that contains all of the parameter values.</span></span> <span data-ttu-id="e7404-122">È necessario definire un parametro per i valori che variano in base al progetto distribuito o all'ambiente in cui viene distribuito il progetto.</span><span class="sxs-lookup"><span data-stu-id="e7404-122">You should define a parameter for those values that will vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="e7404-123">Non definire i parametri per i valori che rimangono invariati.</span><span class="sxs-lookup"><span data-stu-id="e7404-123">Do not define parameters for values that will always stay the same.</span></span> <span data-ttu-id="e7404-124">Ogni valore di parametro nel modello viene usato per definire le risorse distribuite.</span><span class="sxs-lookup"><span data-stu-id="e7404-124">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="e7404-125">Questo modello definisce i parametri seguenti.</span><span class="sxs-lookup"><span data-stu-id="e7404-125">This template defines the following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="e7404-126">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="e7404-126">serviceBusNamespaceName</span></span>
<span data-ttu-id="e7404-127">Nome dello spazio dei nomi del bus di servizio da creare.</span><span class="sxs-lookup"><span data-stu-id="e7404-127">The name of the Service Bus namespace to create.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of the Service Bus namespace" 
    }
}
```

### <a name="servicebussku"></a><span data-ttu-id="e7404-128">serviceBusSKU</span><span class="sxs-lookup"><span data-stu-id="e7404-128">serviceBusSKU</span></span>
<span data-ttu-id="e7404-129">Nome dello [SKU](https://azure.microsoft.com/pricing/details/service-bus/) del bus di servizio da creare.</span><span class="sxs-lookup"><span data-stu-id="e7404-129">The name of the Service Bus [SKU](https://azure.microsoft.com/pricing/details/service-bus/) to create.</span></span>

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
        "description": "The messaging tier for service Bus namespace" 
    } 

```

<span data-ttu-id="e7404-130">Il modello definisce i valori consentiti per il parametro (Basic, Standard o Premium) e assegna un valore predefinito (Standard) nel caso in cui non venga specificato alcun valore.</span><span class="sxs-lookup"><span data-stu-id="e7404-130">The template defines the values that are permitted for this parameter (Basic, Standard, or Premium) and assigns a default value (Standard) if no value is specified.</span></span>

<span data-ttu-id="e7404-131">Per altre informazioni sui prezzi del bus di servizio, vedere [Service Bus pricing and billing][Service Bus pricing and billing] (Prezzi e fatturazione del bus di servizio).</span><span class="sxs-lookup"><span data-stu-id="e7404-131">For more information about Service Bus pricing, see [Service Bus pricing and billing][Service Bus pricing and billing].</span></span>

### <a name="servicebusapiversion"></a><span data-ttu-id="e7404-132">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="e7404-132">serviceBusApiVersion</span></span>
<span data-ttu-id="e7404-133">Versione API del bus di servizio del modello.</span><span class="sxs-lookup"><span data-stu-id="e7404-133">The Service Bus API version of the template.</span></span>

```json
"serviceBusApiVersion": { 
       "type": "string", 
       "defaultValue": "2015-08-01", 
       "metadata": { 
           "description": "Service Bus ApiVersion used by the template" 
       } 
```

## <a name="resources-to-deploy"></a><span data-ttu-id="e7404-134">Risorse da distribuire</span><span class="sxs-lookup"><span data-stu-id="e7404-134">Resources to deploy</span></span>
### <a name="service-bus-namespace"></a><span data-ttu-id="e7404-135">Spazio dei nomi del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="e7404-135">Service Bus namespace</span></span>
<span data-ttu-id="e7404-136">Crea uno spazio dei nomi del bus di servizio standard di tipo **Messaggistica**.</span><span class="sxs-lookup"><span data-stu-id="e7404-136">Creates a standard Service Bus namespace of type **Messaging**.</span></span>

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

## <a name="commands-to-run-deployment"></a><span data-ttu-id="e7404-137">Comandi per eseguire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="e7404-137">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="e7404-138">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7404-138">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName <resource-group-name> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

### <a name="azure-cli"></a><span data-ttu-id="e7404-139">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="e7404-139">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create <my-resource-group> <my-deployment-name> --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

## <a name="next-steps"></a><span data-ttu-id="e7404-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e7404-140">Next steps</span></span>
<span data-ttu-id="e7404-141">Dopo aver creato e distribuito le risorse con Azure Resource Manager, imparare a gestire le risorse leggendo gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="e7404-141">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by reading these articles:</span></span>

* [<span data-ttu-id="e7404-142">Gestire Bus di servizio con PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7404-142">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="e7404-143">Gestire le risorse del bus di servizio con Service Bus Explorer</span><span class="sxs-lookup"><span data-stu-id="e7404-143">Manage Service Bus resources with the Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace template]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-servicebus-create-namespace/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Service Bus pricing and billing]: service-bus-pricing-billing.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
