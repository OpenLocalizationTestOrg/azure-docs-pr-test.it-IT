---
title: risorse di Azure Service Bus aaaCreate utilizzando i modelli di gestione risorse di Azure | Documenti Microsoft
description: Utilizzare Gestione risorse di Azure creazione hello tooautomate di modelli di risorse Bus di servizio
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
ms.openlocfilehash: e539902cae307b63ae7c332580e2064761331ec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-service-bus-resources-using-azure-resource-manager-templates"></a><span data-ttu-id="6f54b-103">Creare risorse del bus di servizio usando i modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6f54b-103">Create Service Bus resources using Azure Resource Manager templates</span></span>

<span data-ttu-id="6f54b-104">Questo articolo viene descritto come toocreate e distribuire le risorse di Service Bus con modelli di gestione risorse di Azure, PowerShell e provider di risorse Bus di servizio hello.</span><span class="sxs-lookup"><span data-stu-id="6f54b-104">This article describes how toocreate and deploy Service Bus resources using Azure Resource Manager templates, PowerShell, and hello Service Bus resource provider.</span></span>

<span data-ttu-id="6f54b-105">Modelli di gestione risorse di Azure consentono di definire hello toodeploy di risorse per una soluzione e toospecify parametri e variabili che consentono valori tooinput per ambienti diversi.</span><span class="sxs-lookup"><span data-stu-id="6f54b-105">Azure Resource Manager templates help you define hello resources toodeploy for a solution, and toospecify parameters and variables that enable you tooinput values for different environments.</span></span> <span data-ttu-id="6f54b-106">modello Hello è costituito da JSON e le espressioni che è possibile utilizzare valori tooconstruct per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="6f54b-106">hello template consists of JSON and expressions that you can use tooconstruct values for your deployment.</span></span> <span data-ttu-id="6f54b-107">Per informazioni dettagliate sulla scrittura di modelli di gestione risorse di Azure e una descrizione del formato di modello hello, vedere [struttura e la sintassi dei modelli di Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6f54b-107">For detailed information about writing Azure Resource Manager templates, and a discussion of hello template format, see [structure and syntax of Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6f54b-108">Hello come negli esempi contenuti in questa presentazione articolo toouse Azure Resource Manager toocreate uno spazio dei nomi del Bus di servizio e la messaggistica entità (coda).</span><span class="sxs-lookup"><span data-stu-id="6f54b-108">hello examples in this article show how toouse Azure Resource Manager toocreate a Service Bus namespace and messaging entity (queue).</span></span> <span data-ttu-id="6f54b-109">Per altri esempi di modello, visitare hello [raccolta di modelli di avvio rapido di Azure] [ Azure Quickstart Templates gallery] e cercare "Bus di servizio".</span><span class="sxs-lookup"><span data-stu-id="6f54b-109">For other template examples, visit hello [Azure Quickstart Templates gallery][Azure Quickstart Templates gallery] and search for "Service Bus."</span></span>
>
>

## <a name="service-bus-resource-manager-templates"></a><span data-ttu-id="6f54b-110">Modelli di Resource Manager per il bus di servizio</span><span class="sxs-lookup"><span data-stu-id="6f54b-110">Service Bus Resource Manager templates</span></span>

<span data-ttu-id="6f54b-111">I modelli di Azure Resource Manager del bus di servizio sono disponibili per il download e la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="6f54b-111">These Service Bus Azure Resource Manager templates are available for download and deployment.</span></span> <span data-ttu-id="6f54b-112">Fare clic su hello seguenti collegamenti per informazioni dettagliate su ciascuno di essi, con i modelli di toohello collegamenti in GitHub:</span><span class="sxs-lookup"><span data-stu-id="6f54b-112">Click hello following links for details about each one, with links toohello templates on GitHub:</span></span>

* [<span data-ttu-id="6f54b-113">Creare uno spazio dei nomi del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="6f54b-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
* [<span data-ttu-id="6f54b-114">Creare uno spazio dei nomi del bus di servizio con coda</span><span class="sxs-lookup"><span data-stu-id="6f54b-114">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
* [<span data-ttu-id="6f54b-115">Creare uno spazio dei nomi del bus di servizio con argomento e sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="6f54b-115">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
* [<span data-ttu-id="6f54b-116">Creare uno spazio dei nomi del bus di servizio con coda e regola di autorizzazione</span><span class="sxs-lookup"><span data-stu-id="6f54b-116">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
* [<span data-ttu-id="6f54b-117">Creare uno spazio dei nomi del bus di servizio con argomento, sottoscrizione e regola</span><span class="sxs-lookup"><span data-stu-id="6f54b-117">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)

## <a name="deploy-with-powershell"></a><span data-ttu-id="6f54b-118">Distribuire con PowerShell</span><span class="sxs-lookup"><span data-stu-id="6f54b-118">Deploy with PowerShell</span></span>

<span data-ttu-id="6f54b-119">Hello procedura riportata di seguito viene descritto come toouse PowerShell toodeploy un modello di gestione risorse di Azure che crea un **Standard** livello dello spazio dei nomi Service Bus e una coda nello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="6f54b-119">hello following procedure describes how toouse PowerShell toodeploy an Azure Resource Manager template that creates a **Standard** tier Service Bus namespace, and a queue within that namespace.</span></span> <span data-ttu-id="6f54b-120">Questo esempio è basato sul hello [creare uno spazio dei nomi del Bus di servizio con coda](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) modello.</span><span class="sxs-lookup"><span data-stu-id="6f54b-120">This example is based on hello [Create a Service Bus namespace with queue](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) template.</span></span> <span data-ttu-id="6f54b-121">flusso di lavoro approssimativo Hello è indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="6f54b-121">hello approximate workflow is as follows:</span></span>

1. <span data-ttu-id="6f54b-122">Installare PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6f54b-122">Install PowerShell.</span></span>
2. <span data-ttu-id="6f54b-123">Creare un modello di hello e, facoltativamente, un file di parametri.</span><span class="sxs-lookup"><span data-stu-id="6f54b-123">Create hello template and (optionally) a parameter file.</span></span>
3. <span data-ttu-id="6f54b-124">In PowerShell, accedi tooyour account Azure.</span><span class="sxs-lookup"><span data-stu-id="6f54b-124">In PowerShell, log in tooyour Azure account.</span></span>
4. <span data-ttu-id="6f54b-125">Se non esiste, creare un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="6f54b-125">Create a new resource group if one does not exist.</span></span>
5. <span data-ttu-id="6f54b-126">Testare la distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="6f54b-126">Test hello deployment.</span></span>
6. <span data-ttu-id="6f54b-127">Se si desidera, impostare la modalità di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="6f54b-127">If desired, set hello deployment mode.</span></span>
7. <span data-ttu-id="6f54b-128">Distribuire il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="6f54b-128">Deploy hello template.</span></span>

<span data-ttu-id="6f54b-129">Per informazioni più complete sulla distribuzione dei modelli di Azure Resource Manager, vedere [Distribuire le risorse con i modelli di Azure Resource Manager][Deploy resources with Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="6f54b-129">For complete information about deploying Azure Resource Manager templates, see [Deploy resources with Azure Resource Manager templates][Deploy resources with Azure Resource Manager templates].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="6f54b-130">Installare PowerShell</span><span class="sxs-lookup"><span data-stu-id="6f54b-130">Install PowerShell</span></span>

<span data-ttu-id="6f54b-131">Installare Azure PowerShell seguendo le istruzioni hello [Introduzione a Azure PowerShell](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="6f54b-131">Install Azure PowerShell by following hello instructions in [Getting started with Azure PowerShell](/powershell/azure/get-started-azureps).</span></span>

### <a name="create-a-template"></a><span data-ttu-id="6f54b-132">Creare un modello</span><span class="sxs-lookup"><span data-stu-id="6f54b-132">Create a template</span></span>

<span data-ttu-id="6f54b-133">Clone o copia hello [201-bus di servizio-creare-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) modello da GitHub:</span><span class="sxs-lookup"><span data-stu-id="6f54b-133">Clone or copy hello [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) template from GitHub:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Service Bus namespace"
            }
        },
        "serviceBusQueueName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Queue"
            }
        },
        "serviceBusApiVersion": {
            "type": "string",
            "defaultValue": "2015-08-01",
            "metadata": {
                "description": "Service Bus ApiVersion used by hello template"
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

### <a name="create-a-parameters-file-optional"></a><span data-ttu-id="6f54b-134">Creare un file di parametri (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="6f54b-134">Create a parameters file (optional)</span></span>

<span data-ttu-id="6f54b-135">toouse un file di parametri facoltativi, hello copia [201-bus di servizio-creare-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) file.</span><span class="sxs-lookup"><span data-stu-id="6f54b-135">toouse an optional parameters file, copy hello [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) file.</span></span> <span data-ttu-id="6f54b-136">Sostituire il valore di hello di `serviceBusNamespaceName` con nome hello dello spazio dei nomi Service Bus hello desiderato toocreate in questa distribuzione e sostituire il valore di hello di `serviceBusQueueName` con nome hello della coda di hello da toocreate.</span><span class="sxs-lookup"><span data-stu-id="6f54b-136">Replace hello value of `serviceBusNamespaceName` with hello name of hello Service Bus namespace you want toocreate in this deployment, and replace hello value of `serviceBusQueueName` with hello name of hello queue you want toocreate.</span></span>

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

<span data-ttu-id="6f54b-137">Per ulteriori informazioni, vedere hello [parametri](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) argomento.</span><span class="sxs-lookup"><span data-stu-id="6f54b-137">For more information, see hello [Parameters](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) topic.</span></span>

### <a name="log-in-tooazure-and-set-hello-azure-subscription"></a><span data-ttu-id="6f54b-138">Accedi tooAzure e impostare hello sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="6f54b-138">Log in tooAzure and set hello Azure subscription</span></span>

<span data-ttu-id="6f54b-139">Da un prompt di PowerShell, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6f54b-139">From a PowerShell prompt, run hello following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="6f54b-140">Si è richiesta toolog su tooyour account Azure.</span><span class="sxs-lookup"><span data-stu-id="6f54b-140">You are prompted toolog on tooyour Azure account.</span></span> <span data-ttu-id="6f54b-141">Dopo l'accesso, eseguire hello successivo comando tooview le sottoscrizioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="6f54b-141">After logging on, run hello following command tooview your available subscriptions.</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="6f54b-142">Questo comando restituisce un elenco delle sottoscrizioni di Azure disponibili.</span><span class="sxs-lookup"><span data-stu-id="6f54b-142">This command returns a list of available Azure subscriptions.</span></span> <span data-ttu-id="6f54b-143">Scegliere una sottoscrizione per hello sessione corrente eseguendo hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="6f54b-143">Choose a subscription for hello current session by running hello following command.</span></span> <span data-ttu-id="6f54b-144">Sostituire `<YourSubscriptionId>` con hello GUID per la sottoscrizione di Azure hello desiderate toouse.</span><span class="sxs-lookup"><span data-stu-id="6f54b-144">Replace `<YourSubscriptionId>` with hello GUID for hello Azure subscription you want toouse.</span></span>

```powershell
Set-AzureRmContext -SubscriptionID <YourSubscriptionId>
```

### <a name="set-hello-resource-group"></a><span data-ttu-id="6f54b-145">Gruppo di risorse hello set</span><span class="sxs-lookup"><span data-stu-id="6f54b-145">Set hello resource group</span></span>

<span data-ttu-id="6f54b-146">Se non è una risorsa esistente di gruppo, creare un nuovo gruppo di risorse con hello * * New-AzureRmResourceGroup * * comando.</span><span class="sxs-lookup"><span data-stu-id="6f54b-146">If you do not have an existing resource group, create a new resource group with hello **New-AzureRmResourceGroup ** command.</span></span> <span data-ttu-id="6f54b-147">Specificare il nome di hello del gruppo di risorse hello e il percorso toouse.</span><span class="sxs-lookup"><span data-stu-id="6f54b-147">Provide hello name of hello resource group and location you want toouse.</span></span> <span data-ttu-id="6f54b-148">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6f54b-148">For example:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyDemoRG -Location "West US"
```

<span data-ttu-id="6f54b-149">Se ha esito positivo, viene visualizzato un riepilogo del nuovo gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="6f54b-149">If successful, a summary of hello new resource group is displayed.</span></span>

```powershell
ResourceGroupName : MyDemoRG
Location          : westus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/<GUID>/resourceGroups/MyDemoRG
```

### <a name="test-hello-deployment"></a><span data-ttu-id="6f54b-150">Distribuzione di prova hello</span><span class="sxs-lookup"><span data-stu-id="6f54b-150">Test hello deployment</span></span>

<span data-ttu-id="6f54b-151">Convalida della distribuzione eseguendo hello `Test-AzureRmResourceGroupDeployment` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6f54b-151">Validate your deployment by running hello `Test-AzureRmResourceGroupDeployment` cmdlet.</span></span> <span data-ttu-id="6f54b-152">Durante il test di distribuzione di hello, specificare i parametri, esattamente come quando si esegue la distribuzione di hello.</span><span class="sxs-lookup"><span data-stu-id="6f54b-152">When testing hello deployment, provide parameters exactly as you would when executing hello deployment.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="create-hello-deployment"></a><span data-ttu-id="6f54b-153">Crea distribuzione hello</span><span class="sxs-lookup"><span data-stu-id="6f54b-153">Create hello deployment</span></span>

<span data-ttu-id="6f54b-154">toocreate hello nuova distribuzione, eseguire hello `New-AzureRmResourceGroupDeployment` cmdlet e parametri di hello necessari quando viene richiesto di fornire.</span><span class="sxs-lookup"><span data-stu-id="6f54b-154">toocreate hello new deployment, run hello `New-AzureRmResourceGroupDeployment` cmdlet, and provide hello necessary parameters when prompted.</span></span> <span data-ttu-id="6f54b-155">parametri di Hello includono un nome per la distribuzione, nome hello del gruppo di risorse e il percorso di hello o file di modello di URL toohello.</span><span class="sxs-lookup"><span data-stu-id="6f54b-155">hello parameters include a name for your deployment, hello name of your resource group, and hello path or URL toohello template file.</span></span> <span data-ttu-id="6f54b-156">Se hello **modalità** parametro viene omesso, il valore predefinito di hello **incrementale** viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="6f54b-156">If hello **Mode** parameter is not specified, hello default value of **Incremental** is used.</span></span> <span data-ttu-id="6f54b-157">Per altre informazioni, vedere [Distribuzioni incrementali e complete](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span><span class="sxs-lookup"><span data-stu-id="6f54b-157">For more information, see [Incremental and complete deployments](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span></span>

<span data-ttu-id="6f54b-158">Hello seguenti al prompt dei comandi è per i parametri nella finestra di PowerShell hello hello tre:</span><span class="sxs-lookup"><span data-stu-id="6f54b-158">hello following command prompts you for hello three parameters in hello PowerShell window:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

<span data-ttu-id="6f54b-159">toospecify file dei parametri utilizzare hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="6f54b-159">toospecify a parameters file instead, use hello following command.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -TemplateParameterFile <path tooparameters file>\azuredeploy.parameters.json
```

<span data-ttu-id="6f54b-160">È anche possibile utilizzare parametri inline quando si esegue il cmdlet di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="6f54b-160">You can also use inline parameters when you run hello deployment cmdlet.</span></span> <span data-ttu-id="6f54b-161">comando Hello è come segue:</span><span class="sxs-lookup"><span data-stu-id="6f54b-161">hello command is as follows:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -parameterName "parameterValue"
```

<span data-ttu-id="6f54b-162">toorun un [completo](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) distribuzione, hello set **modalità** parametro troppo**completa**:</span><span class="sxs-lookup"><span data-stu-id="6f54b-162">toorun a [complete](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) deployment, set hello **Mode** parameter too**Complete**:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -Mode Complete -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="verify-hello-deployment"></a><span data-ttu-id="6f54b-163">Verificare la distribuzione di hello</span><span class="sxs-lookup"><span data-stu-id="6f54b-163">Verify hello deployment</span></span>
<span data-ttu-id="6f54b-164">Se le risorse di hello vengano distribuite correttamente, viene visualizzato un riepilogo della distribuzione hello nella finestra di PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="6f54b-164">If hello resources are deployed successfully, a summary of hello deployment is displayed in hello PowerShell window:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="6f54b-165">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6f54b-165">Next steps</span></span>
<span data-ttu-id="6f54b-166">Abbiamo visto flusso di lavoro base hello e i comandi per la distribuzione di un modello di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="6f54b-166">You've now seen hello basic workflow and commands for deploying an Azure Resource Manager template.</span></span> <span data-ttu-id="6f54b-167">Per informazioni più dettagliate, visitare hello seguenti collegamenti:</span><span class="sxs-lookup"><span data-stu-id="6f54b-167">For more detailed information, visit hello following links:</span></span>

* <span data-ttu-id="6f54b-168">[Panoramica di Azure Resource Manager][Azure Resource Manager overview]</span><span class="sxs-lookup"><span data-stu-id="6f54b-168">[Azure Resource Manager overview][Azure Resource Manager overview]</span></span>
* <span data-ttu-id="6f54b-169">[Distribuire le risorse con i modelli di Azure Resource Manager e Azure PowerShell][Deploy resources with Azure Resource Manager templates]</span><span class="sxs-lookup"><span data-stu-id="6f54b-169">[Deploy resources with Resource Manager templates and Azure PowerShell][Deploy resources with Azure Resource Manager templates]</span></span>
* [<span data-ttu-id="6f54b-170">Creazione di modelli di Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="6f54b-170">Authoring Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure Resource Manager overview]: ../azure-resource-manager/resource-group-overview.md
[Deploy resources with Azure Resource Manager templates]: ../azure-resource-manager/resource-group-template-deploy.md
[Azure Quickstart Templates gallery]: https://azure.microsoft.com/documentation/templates/?term=service+bus
