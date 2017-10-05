---
title: Creare risorse del bus di servizio di Azure usando i modelli di Azure Resource Manager | Documentazione Microsoft
description: Usare i modelli di Azure Resource Manager per automatizzare la creazione di risorse del bus di servizio
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 24f6a207-0fa4-49cf-8a58-963f9e2fd655
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: c8142d8edfd3a527b13d655bac21acf5332f2d14
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-service-bus-resources-using-azure-resource-manager-templates"></a><span data-ttu-id="3b4ab-103">Creare risorse del bus di servizio usando i modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3b4ab-103">Create Service Bus resources using Azure Resource Manager templates</span></span>

<span data-ttu-id="3b4ab-104">Questo articolo descrive come creare e distribuire risorse del bus di servizio usando i modelli di Azure Resource Manager, PowerShell e il provider di risorse del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="3b4ab-104">This article describes how to create and deploy Service Bus resources using Azure Resource Manager templates, PowerShell, and the Service Bus resource provider.</span></span>

<span data-ttu-id="3b4ab-105">I modelli di Azure Resource Manager aiutano a definire le risorse da distribuire per una soluzione e a specificare i parametri e le variabili che consentono di immettere i valori per diversi ambienti.</span><span class="sxs-lookup"><span data-stu-id="3b4ab-105">Azure Resource Manager templates help you define the resources to deploy for a solution, and to specify parameters and variables that enable you to input values for different environments.</span></span> <span data-ttu-id="3b4ab-106">Il modello è composto da JSON ed espressioni che è possibile usare per creare valori per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="3b4ab-106">The template consists of JSON and expressions that you can use to construct values for your deployment.</span></span> <span data-ttu-id="3b4ab-107">Per informazioni dettagliate sulla creazione di modelli di Azure Resource Manager e per una descrizione del formato dei modelli, vedere [Comprendere la struttura e la sintassi dei modelli di Azure Resource Manger](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="3b4ab-107">For detailed information about writing Azure Resource Manager templates, and a discussion of the template format, see [structure and syntax of Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3b4ab-108">Gli esempi inclusi in questo articolo spiegano come usare Azure Resource Manager per creare uno spazio dei nomi del bus di servizio e una entità di messaggistica, ovvero una coda.</span><span class="sxs-lookup"><span data-stu-id="3b4ab-108">The examples in this article show how to use Azure Resource Manager to create a Service Bus namespace and messaging entity (queue).</span></span> <span data-ttu-id="3b4ab-109">Per altri esempi di modelli, vedere la [raccolta dei modelli di avvio rapido di Azure][Azure Quickstart Templates gallery] e cercare "service bus".</span><span class="sxs-lookup"><span data-stu-id="3b4ab-109">For other template examples, visit the [Azure Quickstart Templates gallery][Azure Quickstart Templates gallery] and search for "Service Bus."</span></span>
>
>

## <a name="service-bus-resource-manager-templates"></a><span data-ttu-id="3b4ab-110">Modelli di Resource Manager per il bus di servizio</span><span class="sxs-lookup"><span data-stu-id="3b4ab-110">Service Bus Resource Manager templates</span></span>

<span data-ttu-id="3b4ab-111">I modelli di Azure Resource Manager del bus di servizio sono disponibili per il download e la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="3b4ab-111">These Service Bus Azure Resource Manager templates are available for download and deployment.</span></span> <span data-ttu-id="3b4ab-112">Fare clic sui collegamenti seguenti per informazioni dettagliate su ognuno di essi, con collegamenti ai modelli su GitHub:</span><span class="sxs-lookup"><span data-stu-id="3b4ab-112">Click the following links for details about each one, with links to the templates on GitHub:</span></span>

* [<span data-ttu-id="3b4ab-113">Creare uno spazio dei nomi del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="3b4ab-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
* [<span data-ttu-id="3b4ab-114">Creare uno spazio dei nomi del bus di servizio con coda</span><span class="sxs-lookup"><span data-stu-id="3b4ab-114">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
* [<span data-ttu-id="3b4ab-115">Creare uno spazio dei nomi del bus di servizio con argomento e sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="3b4ab-115">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
* [<span data-ttu-id="3b4ab-116">Creare uno spazio dei nomi del bus di servizio con coda e regola di autorizzazione</span><span class="sxs-lookup"><span data-stu-id="3b4ab-116">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
* [<span data-ttu-id="3b4ab-117">Creare uno spazio dei nomi del bus di servizio con argomento, sottoscrizione e regola</span><span class="sxs-lookup"><span data-stu-id="3b4ab-117">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)

## <a name="deploy-with-powershell"></a><span data-ttu-id="3b4ab-118">Distribuire con PowerShell</span><span class="sxs-lookup"><span data-stu-id="3b4ab-118">Deploy with PowerShell</span></span>

<span data-ttu-id="3b4ab-119">La procedura seguente illustra come usare PowerShell per distribuire un modello di Azure Resource Manager che crea uno spazio dei nomi del bus di servizio di livello **Standard** e una coda all'interno di tale spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="3b4ab-119">The following procedure describes how to use PowerShell to deploy an Azure Resource Manager template that creates a **Standard** tier Service Bus namespace, and a queue within that namespace.</span></span> <span data-ttu-id="3b4ab-120">Questo esempio è basato sul modello di [Creare uno spazio dei nomi del bus di servizio con coda](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue).</span><span class="sxs-lookup"><span data-stu-id="3b4ab-120">This example is based on the [Create a Service Bus namespace with queue](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) template.</span></span> <span data-ttu-id="3b4ab-121">Il flusso di lavoro è all'incirca il seguente:</span><span class="sxs-lookup"><span data-stu-id="3b4ab-121">The approximate workflow is as follows:</span></span>

1. <span data-ttu-id="3b4ab-122">Installare PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3b4ab-122">Install PowerShell.</span></span>
2. <span data-ttu-id="3b4ab-123">Creare il modello e, facoltativamente, un file di parametri.</span><span class="sxs-lookup"><span data-stu-id="3b4ab-123">Create the template and (optionally) a parameter file.</span></span>
3. <span data-ttu-id="3b4ab-124">In PowerShell accedere all'account Azure.</span><span class="sxs-lookup"><span data-stu-id="3b4ab-124">In PowerShell, log in to your Azure account.</span></span>
4. <span data-ttu-id="3b4ab-125">Se non esiste, creare un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="3b4ab-125">Create a new resource group if one does not exist.</span></span>
5. <span data-ttu-id="3b4ab-126">Testare la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="3b4ab-126">Test the deployment.</span></span>
6. <span data-ttu-id="3b4ab-127">Facoltativamente, è possibile impostare la modalità di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="3b4ab-127">If desired, set the deployment mode.</span></span>
7. <span data-ttu-id="3b4ab-128">Distribuire il modello.</span><span class="sxs-lookup"><span data-stu-id="3b4ab-128">Deploy the template.</span></span>

<span data-ttu-id="3b4ab-129">Per informazioni più complete sulla distribuzione dei modelli di Azure Resource Manager, vedere [Distribuire le risorse con i modelli di Azure Resource Manager][Deploy resources with Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="3b4ab-129">For complete information about deploying Azure Resource Manager templates, see [Deploy resources with Azure Resource Manager templates][Deploy resources with Azure Resource Manager templates].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="3b4ab-130">Installare PowerShell</span><span class="sxs-lookup"><span data-stu-id="3b4ab-130">Install PowerShell</span></span>

<span data-ttu-id="3b4ab-131">Installare Azure PowerShell seguendo le istruzioni riportate in [Introduzione ai cmdlet di Azure PowerShell](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="3b4ab-131">Install Azure PowerShell by following the instructions in [Getting started with Azure PowerShell](/powershell/azure/get-started-azureps).</span></span>

### <a name="create-a-template"></a><span data-ttu-id="3b4ab-132">Creare un modello</span><span class="sxs-lookup"><span data-stu-id="3b4ab-132">Create a template</span></span>

<span data-ttu-id="3b4ab-133">Clonare o copiare il modello [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) da GitHub:</span><span class="sxs-lookup"><span data-stu-id="3b4ab-133">Clone or copy the [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) template from GitHub:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "type": "string",
            "metadata": {
                "description": "Name of the Service Bus namespace"
            }
        },
        "serviceBusQueueName": {
            "type": "string",
            "metadata": {
                "description": "Name of the Queue"
            }
        },
        "serviceBusApiVersion": {
            "type": "string",
            "defaultValue": "2015-08-01",
            "metadata": {
                "description": "Service Bus ApiVersion used by the template"
            }
        }
    },
    "variables": {
        "location": "[resourceGroup().location]",
        "sbVersion": "[parameters('serviceBusApiVersion')]",
        "defaultSASKeyName": "RootManageSharedAccessKey",
        "authRuleResourceId": "[resourceId('Microsoft.ServiceBus/namespaces/authorizationRules', parameters('serviceBusNamespaceName'), variables('defaultSASKeyName'))]"
    },
    "resources": [{
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
                "path": "[parameters('serviceBusQueueName')]"
            }
        }]
    }],
    "outputs": {
        "NamespaceConnectionString": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryConnectionString]"
        },
        "SharedAccessPolicyPrimaryKey": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryKey]"
        }
    }
}
```

### <a name="create-a-parameters-file-optional"></a><span data-ttu-id="3b4ab-134">Creare un file di parametri (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="3b4ab-134">Create a parameters file (optional)</span></span>

<span data-ttu-id="3b4ab-135">Per usare un file di parametri facoltativo, copiare il file [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json).</span><span class="sxs-lookup"><span data-stu-id="3b4ab-135">To use an optional parameters file, copy the [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) file.</span></span> <span data-ttu-id="3b4ab-136">Sostituire il valore di `serviceBusNamespaceName` con il nome dello spazio dei nomi del bus di servizio che si vuole creare in questa distribuzione e sostituire il valore di `serviceBusQueueName` con il nome della coda che si vuole creare.</span><span class="sxs-lookup"><span data-stu-id="3b4ab-136">Replace the value of `serviceBusNamespaceName` with the name of the Service Bus namespace you want to create in this deployment, and replace the value of `serviceBusQueueName` with the name of the queue you want to create.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "value": "<myNamespaceName>"
        },
        "serviceBusQueueName": {
            "value": "<myQueueName>"
        },
        "serviceBusApiVersion": {
            "value": "2015-08-01"
        }
    }
}
```

<span data-ttu-id="3b4ab-137">Per altre informazioni, vedere l'argomento [Parametri](../azure-resource-manager/resource-group-template-deploy.md#parameter-files).</span><span class="sxs-lookup"><span data-stu-id="3b4ab-137">For more information, see the [Parameters](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) topic.</span></span>

### <a name="log-in-to-azure-and-set-the-azure-subscription"></a><span data-ttu-id="3b4ab-138">Accedere ad Azure e impostare la sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="3b4ab-138">Log in to Azure and set the Azure subscription</span></span>

<span data-ttu-id="3b4ab-139">Al prompt di PowerShell, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="3b4ab-139">From a PowerShell prompt, run the following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="3b4ab-140">Il sistema chiede di accedere all'account Azure.</span><span class="sxs-lookup"><span data-stu-id="3b4ab-140">You are prompted to log on to your Azure account.</span></span> <span data-ttu-id="3b4ab-141">Dopo l'accesso, eseguire il comando seguente per visualizzare le sottoscrizioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="3b4ab-141">After logging on, run the following command to view your available subscriptions.</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="3b4ab-142">Questo comando restituisce un elenco delle sottoscrizioni di Azure disponibili.</span><span class="sxs-lookup"><span data-stu-id="3b4ab-142">This command returns a list of available Azure subscriptions.</span></span> <span data-ttu-id="3b4ab-143">Scegliere una sottoscrizione per la sessione corrente eseguendo il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="3b4ab-143">Choose a subscription for the current session by running the following command.</span></span> <span data-ttu-id="3b4ab-144">Sostituire `<YourSubscriptionId>` con il GUID della sottoscrizione di Azure che si vuole usare.</span><span class="sxs-lookup"><span data-stu-id="3b4ab-144">Replace `<YourSubscriptionId>` with the GUID for the Azure subscription you want to use.</span></span>

```powershell
Set-AzureRmContext -SubscriptionID <YourSubscriptionId>
```

### <a name="set-the-resource-group"></a><span data-ttu-id="3b4ab-145">Impostare il gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="3b4ab-145">Set the resource group</span></span>

<span data-ttu-id="3b4ab-146">Se non è disponibile un gruppo di risorse, creare un nuovo gruppo di risorse con il comando **New-AzureRmResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="3b4ab-146">If you do not have an existing resource group, create a new resource group with the **New-AzureRmResourceGroup ** command.</span></span> <span data-ttu-id="3b4ab-147">Specificare il nome del gruppo di risorse e la posizione che si vuole usare,</span><span class="sxs-lookup"><span data-stu-id="3b4ab-147">Provide the name of the resource group and location you want to use.</span></span> <span data-ttu-id="3b4ab-148">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="3b4ab-148">For example:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyDemoRG -Location "West US"
```

<span data-ttu-id="3b4ab-149">Se il nuovo gruppo di risorse è stato creato correttamente, viene visualizzato il relativo riepilogo.</span><span class="sxs-lookup"><span data-stu-id="3b4ab-149">If successful, a summary of the new resource group is displayed.</span></span>

```powershell
ResourceGroupName : MyDemoRG
Location          : westus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/<GUID>/resourceGroups/MyDemoRG
```

### <a name="test-the-deployment"></a><span data-ttu-id="3b4ab-150">Test della distribuzione</span><span class="sxs-lookup"><span data-stu-id="3b4ab-150">Test the deployment</span></span>

<span data-ttu-id="3b4ab-151">Convalidare la distribuzione eseguendo il cmdlet `Test-AzureRmResourceGroupDeployment`.</span><span class="sxs-lookup"><span data-stu-id="3b4ab-151">Validate your deployment by running the `Test-AzureRmResourceGroupDeployment` cmdlet.</span></span> <span data-ttu-id="3b4ab-152">Durante il test della distribuzione, specificare esattamente gli stessi parametri di quando si esegue la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="3b4ab-152">When testing the deployment, provide parameters exactly as you would when executing the deployment.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

### <a name="create-the-deployment"></a><span data-ttu-id="3b4ab-153">Creare la distribuzione</span><span class="sxs-lookup"><span data-stu-id="3b4ab-153">Create the deployment</span></span>

<span data-ttu-id="3b4ab-154">Per creare la nuova distribuzione, eseguire il cmdlet `New-AzureRmResourceGroupDeployment` e specificare i parametri necessari quando viene richiesto.</span><span class="sxs-lookup"><span data-stu-id="3b4ab-154">To create the new deployment, run the `New-AzureRmResourceGroupDeployment` cmdlet, and provide the necessary parameters when prompted.</span></span> <span data-ttu-id="3b4ab-155">I parametri includono il nome della distribuzione, il nome del gruppo di risorse e il percorso o l'URL del file di modello.</span><span class="sxs-lookup"><span data-stu-id="3b4ab-155">The parameters include a name for your deployment, the name of your resource group, and the path or URL to the template file.</span></span> <span data-ttu-id="3b4ab-156">Se il parametro **Mode** non è specificato, viene usato il valore predefinito **Incremental**.</span><span class="sxs-lookup"><span data-stu-id="3b4ab-156">If the **Mode** parameter is not specified, the default value of **Incremental** is used.</span></span> <span data-ttu-id="3b4ab-157">Per altre informazioni, vedere [Distribuzioni incrementali e complete](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span><span class="sxs-lookup"><span data-stu-id="3b4ab-157">For more information, see [Incremental and complete deployments](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span></span>

<span data-ttu-id="3b4ab-158">Il comando seguente richiede tre parametri nella finestra di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3b4ab-158">The following command prompts you for the three parameters in the PowerShell window:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

<span data-ttu-id="3b4ab-159">Per specificare invece un file di parametri, usare il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="3b4ab-159">To specify a parameters file instead, use the following command.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json -TemplateParameterFile <path to parameters file>\azuredeploy.parameters.json
```

<span data-ttu-id="3b4ab-160">È anche possibile usare i parametri inline quando si esegue il cmdlet di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="3b4ab-160">You can also use inline parameters when you run the deployment cmdlet.</span></span> <span data-ttu-id="3b4ab-161">Il comando è il seguente:</span><span class="sxs-lookup"><span data-stu-id="3b4ab-161">The command is as follows:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json -parameterName "parameterValue"
```

<span data-ttu-id="3b4ab-162">Per eseguire una distribuzione [completa](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments), impostare il parametro **Mode** su **Complete**:</span><span class="sxs-lookup"><span data-stu-id="3b4ab-162">To run a [complete](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) deployment, set the **Mode** parameter to **Complete**:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -Mode Complete -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

### <a name="verify-the-deployment"></a><span data-ttu-id="3b4ab-163">Verificare la distribuzione</span><span class="sxs-lookup"><span data-stu-id="3b4ab-163">Verify the deployment</span></span>
<span data-ttu-id="3b4ab-164">Se le risorse vengono distribuite correttamente, nella finestra di PowerShell viene visualizzato il riepilogo della distribuzione:</span><span class="sxs-lookup"><span data-stu-id="3b4ab-164">If the resources are deployed successfully, a summary of the deployment is displayed in the PowerShell window:</span></span>

```powershell
DeploymentName    : MyDemoDeployment
ResourceGroupName : MyDemoRG
ProvisioningState : Succeeded
Timestamp         : 4/19/2016 10:38:30 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
                    Name             Type                       Value
                    ===============  =========================  ==========
                    serviceBusNamespaceName  String             <namespaceName>
                    serviceBusQueueName  String                 <queueName>
                    serviceBusApiVersion  String                2015-08-01

```

## <a name="next-steps"></a><span data-ttu-id="3b4ab-165">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3b4ab-165">Next steps</span></span>
<span data-ttu-id="3b4ab-166">Finora sono stati illustrati il flusso di lavoro di base e i comandi per la distribuzione di un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3b4ab-166">You've now seen the basic workflow and commands for deploying an Azure Resource Manager template.</span></span> <span data-ttu-id="3b4ab-167">Per informazioni più dettagliate, visitare i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="3b4ab-167">For more detailed information, visit the following links:</span></span>

* <span data-ttu-id="3b4ab-168">[Panoramica di Azure Resource Manager][Azure Resource Manager overview]</span><span class="sxs-lookup"><span data-stu-id="3b4ab-168">[Azure Resource Manager overview][Azure Resource Manager overview]</span></span>
* <span data-ttu-id="3b4ab-169">[Distribuire le risorse con i modelli di Azure Resource Manager e Azure PowerShell][Deploy resources with Azure Resource Manager templates]</span><span class="sxs-lookup"><span data-stu-id="3b4ab-169">[Deploy resources with Resource Manager templates and Azure PowerShell][Deploy resources with Azure Resource Manager templates]</span></span>
* [<span data-ttu-id="3b4ab-170">Creazione di modelli di Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="3b4ab-170">Authoring Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure Resource Manager overview]: ../azure-resource-manager/resource-group-overview.md
[Deploy resources with Azure Resource Manager templates]: ../azure-resource-manager/resource-group-template-deploy.md
[Azure Quickstart Templates gallery]: https://azure.microsoft.com/documentation/templates/?term=service+bus
