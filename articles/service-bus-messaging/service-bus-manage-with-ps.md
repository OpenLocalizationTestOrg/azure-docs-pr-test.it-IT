---
title: Gestire le risorse del bus di servizio di Azure con PowerShell | Microsoft Docs
description: Usare il modulo di PowerShell per creare e gestire le risorse del bus di servizio
services: service-bus-messaging
documentationcenter: .NET
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/06/2017
ms.author: sethm
ms.openlocfilehash: 1205f9fcabf5788c970fbce257aa5ad04f32cddc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-manage-service-bus-resources"></a><span data-ttu-id="14f9a-103">Gestire le risorse del bus di servizio di Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="14f9a-103">Use PowerShell to manage Service Bus resources</span></span>

<span data-ttu-id="14f9a-104">Microsoft Azure PowerShell è un ambiente di scripting che può essere usato per controllare e automatizzare la distribuzione e la gestione dei servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="14f9a-104">Microsoft Azure PowerShell is a scripting environment that you can use to control and automate the deployment and management of Azure services.</span></span> <span data-ttu-id="14f9a-105">L'articolo descrive come usare il [modulo PowerShell di Resource Manager del bus di servizio](/powershell/module/azurerm.servicebus) per effettuare il provisioning e gestire le entità del bus di servizio (spazi dei nomi, code, argomenti e sottoscrizioni) tramite una console o uno script locale di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="14f9a-105">This article describes how to use the [Service Bus Resource Manager PowerShell module](/powershell/module/azurerm.servicebus) to provision and manage Service Bus entities (namespaces, queues, topics, and subscriptions) using a local Azure PowerShell console or script.</span></span>

<span data-ttu-id="14f9a-106">È possibile gestire le risorse del bus di servizio anche usando i modelli di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="14f9a-106">You can also manage Service Bus entities using Azure Resource Manager templates.</span></span> <span data-ttu-id="14f9a-107">Per altre informazioni, vedere l'articolo [Creare risorse del bus di servizio usando i modelli di Azure Resource Manager](service-bus-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="14f9a-107">For more information, see the article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14f9a-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="14f9a-108">Prerequisites</span></span>

<span data-ttu-id="14f9a-109">Prima di iniziare, è necessario disporre di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="14f9a-109">Before you begin, you'll need the following:</span></span>

* <span data-ttu-id="14f9a-110">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="14f9a-110">An Azure subscription.</span></span> <span data-ttu-id="14f9a-111">Per altre informazioni su come ottenere una sottoscrizione, vedere le [opzioni di acquisto][purchase options], le [offerte per i membri][member offers] oppure l'[account gratuito][free account].</span><span class="sxs-lookup"><span data-stu-id="14f9a-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span></span>
* <span data-ttu-id="14f9a-112">Un computer con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="14f9a-112">A computer with Azure PowerShell.</span></span> <span data-ttu-id="14f9a-113">Per le istruzioni vedere [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) (Introduzione ai cmdlet di Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="14f9a-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span></span>
* <span data-ttu-id="14f9a-114">Conoscenza generale degli script di PowerShell, dei pacchetti NuGet e di .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="14f9a-114">A general understanding of PowerShell scripts, NuGet packages, and the .NET Framework.</span></span>

## <a name="get-started"></a><span data-ttu-id="14f9a-115">Introduzione</span><span class="sxs-lookup"><span data-stu-id="14f9a-115">Get started</span></span>

<span data-ttu-id="14f9a-116">Il primo passaggio consiste nell'usare PowerShell per accedere all'account Azure e alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="14f9a-116">The first step is to use PowerShell to log in to your Azure account and Azure subscription.</span></span> <span data-ttu-id="14f9a-117">Seguire le istruzioni in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) (Introduzione ai cmdlet di Azure PowerShell) per accedere al proprio account Azure e recuperare e accedere alle risorse nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="14f9a-117">Follow the instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) to log in to your Azure account, and retrieve and access the resources in your Azure subscription.</span></span>

## <a name="provision-a-service-bus-namespace"></a><span data-ttu-id="14f9a-118">Provisioning di uno spazio dei nomi del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="14f9a-118">Provision a Service Bus namespace</span></span>

<span data-ttu-id="14f9a-119">Quando si usano gli spazi dei nomi del bus di servizio, è possibile usare i cmdlet [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [New-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace) e [Set-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace).</span><span class="sxs-lookup"><span data-stu-id="14f9a-119">When working with Service Bus namespaces, you can use the [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [New-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), and [Set-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlets.</span></span>

<span data-ttu-id="14f9a-120">Questo esempio crea alcune variabili locali nello script: `$Namespace` e `$Location`.</span><span class="sxs-lookup"><span data-stu-id="14f9a-120">This example creates a few local variables in the script; `$Namespace` and `$Location`.</span></span>

* <span data-ttu-id="14f9a-121">`$Namespace` è il nome dello spazio dei nomi del bus di servizio che si vuole usare.</span><span class="sxs-lookup"><span data-stu-id="14f9a-121">`$Namespace` is the name of the Service Bus namespace with which we want to work.</span></span>
* <span data-ttu-id="14f9a-122">`$Location` identifica il data center in cui si eseguirà il provisioning dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="14f9a-122">`$Location` identifies the data center in which will we provision the namespace.</span></span>
* <span data-ttu-id="14f9a-123">`$CurrentNamespace` archivia lo spazio dei nomi di riferimento che viene recuperato (o creato).</span><span class="sxs-lookup"><span data-stu-id="14f9a-123">`$CurrentNamespace` stores the reference namespace that we retrieve (or create).</span></span>

<span data-ttu-id="14f9a-124">In uno script effettivo, `$Namespace` e `$Location` possono essere passati come parametri.</span><span class="sxs-lookup"><span data-stu-id="14f9a-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span></span>

<span data-ttu-id="14f9a-125">Questa parte dello script esegue le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="14f9a-125">This part of the script does the following:</span></span>

1. <span data-ttu-id="14f9a-126">Tenta di recuperare uno spazio dei nomi del bus di servizio con il nome specificato.</span><span class="sxs-lookup"><span data-stu-id="14f9a-126">Attempts to retrieve a Service Bus namespace with the specified name.</span></span>
2. <span data-ttu-id="14f9a-127">Se lo spazio dei nomi viene trovato, viene segnalato ciò che viene trovato.</span><span class="sxs-lookup"><span data-stu-id="14f9a-127">If the namespace is found, it reports what was found.</span></span>
3. <span data-ttu-id="14f9a-128">Se lo spazio dei nomi non viene trovato, viene creato lo spazio dei nomi e quindi viene recuperato lo spazio dei nomi appena creato.</span><span class="sxs-lookup"><span data-stu-id="14f9a-128">If the namespace is not found, it creates the namespace and then retrieves the newly created namespace.</span></span>
   
    ``` powershell
    # Query to see if the namespace currently exists
    $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
   
    # Check if the namespace already exists or needs to be created
    if ($CurrentNamespace)
    {
        Write-Host "The namespace $Namespace already exists in the $Location region:"
        # Report what was found
        Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "The $Namespace namespace does not exist."
        Write-Host "Creating the $Namespace namespace in the $Location region..."
        New-AzureRmServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
        Write-Host "The $Namespace namespace in Resource Group $ResGrpName in the $Location region has been successfully created."
                
    }
    ```

### <a name="create-a-namespace-authorization-rule"></a><span data-ttu-id="14f9a-129">Crea una regola di autorizzazione dello spazio dei nomi</span><span class="sxs-lookup"><span data-stu-id="14f9a-129">Create a namespace authorization rule</span></span>

<span data-ttu-id="14f9a-130">L'esempio seguente illustra come gestire le regole di autorizzazione dello spazio dei nomi usando i cmdlet [New-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Set-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule) e [Remove-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).</span><span class="sxs-lookup"><span data-stu-id="14f9a-130">The following example shows how to manage namespace authorization rules using the [New-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Set-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), and [Remove-AzureRmServiceBusNamespaceAuthorizationRule cmdlets](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).</span></span>

```powershell
# Query to see if rule exists
$CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

# Check if the rule already exists or needs to be created
if ($CurrentRule)
{
    Write-Host "The $AuthRule rule already exists for the namespace $Namespace."
}
else
{
    Write-Host "The $AuthRule rule does not exist."
    Write-Host "Creating the $AuthRule rule for the $Namespace namespace..."
    New-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule -Rights @("Listen","Send")
    $CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
    Write-Host "The $AuthRule rule for the $Namespace namespace has been successfully created."

    Write-Host "Setting rights on the namespace"
    $authRuleObj = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

    Write-Host "Remove Send rights"
    $authRuleObj.Rights.Remove("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Add Send and Manage rights to the namespace"
    $authRuleObj.Rights.Add("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj
    $authRuleObj.Rights.Add("Manage")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Show value of primary key"
    $CurrentKey = Get-AzureRmServiceBusNamespaceKey -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
        
    Write-Host "Remove this authorization rule"
    Remove-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
}
```

## <a name="create-a-queue"></a><span data-ttu-id="14f9a-131">Creare una coda</span><span class="sxs-lookup"><span data-stu-id="14f9a-131">Create a queue</span></span>

<span data-ttu-id="14f9a-132">Per creare una coda o un argomento, eseguire una verifica dello spazio dei nomi usando lo script indicato nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="14f9a-132">To create a queue or topic, perform a namespace check using the script in the previous section.</span></span> <span data-ttu-id="14f9a-133">Creare quindi la coda:</span><span class="sxs-lookup"><span data-stu-id="14f9a-133">Then, create the queue:</span></span>

```powershell
# Check if queue already exists
$CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName

if($CurrentQ)
{
    Write-Host "The queue $QueueName already exists in the $Location region:"
}
else
{
    Write-Host "The $QueueName queue does not exist."
    Write-Host "Creating the $QueueName queue in the $Location region..."
    New-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -EnablePartitioning $True
    $CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName
    Write-Host "The $QueueName queue in Resource Group $ResGrpName in the $Location region has been successfully created."
}
```

### <a name="modify-queue-properties"></a><span data-ttu-id="14f9a-134">Modificare le proprietà della coda</span><span class="sxs-lookup"><span data-stu-id="14f9a-134">Modify queue properties</span></span>

<span data-ttu-id="14f9a-135">Dopo avere eseguito lo script della sezione precedente, è possibile usare il cmdlet [Set-AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) per aggiornare le proprietà di una coda, come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="14f9a-135">After executing the script in the preceding section, you can use the [Set-AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) cmdlet to update the properties of a queue, as in the following example:</span></span>

```powershell
$CurrentQ.DeadLetteringOnMessageExpiration = $True
$CurrentQ.MaxDeliveryCount = 7
$CurrentQ.MaxSizeInMegabytes = 2048
$CurrentQ.EnableExpress = $True

Set-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -QueueObj $CurrentQ
```

## <a name="provisioning-other-service-bus-entities"></a><span data-ttu-id="14f9a-136">Provisioning di altre entità del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="14f9a-136">Provisioning other Service Bus entities</span></span>

<span data-ttu-id="14f9a-137">È possibile usare il [modulo PowerShell del bus di servizio](/powershell/module/azurerm.servicebus) per effettuare il provisioning di altre entità, ad esempio argomenti e sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="14f9a-137">You can use the [Service Bus PowerShell module](/powershell/module/azurerm.servicebus) to provision other entities, such as topics and subscriptions.</span></span> <span data-ttu-id="14f9a-138">Questi cmdlet sono sintatticamente simili a quelli per la creazione della coda illustrati nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="14f9a-138">These cmdlets are syntactically similar to the queue creation cmdlets demonstrated in the previous section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="14f9a-139">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="14f9a-139">Next steps</span></span>

- <span data-ttu-id="14f9a-140">Vedere la documentazione completa del modulo PowerShell di Resource Manager del bus di servizio [qui](/powershell/module/azurerm.servicebus).</span><span class="sxs-lookup"><span data-stu-id="14f9a-140">See the complete Service Bus Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.servicebus).</span></span> <span data-ttu-id="14f9a-141">Questa pagina elenca tutti i cmdlet disponibili.</span><span class="sxs-lookup"><span data-stu-id="14f9a-141">This page lists all available cmdlets.</span></span>
- <span data-ttu-id="14f9a-142">Per informazioni sull'uso dei modelli di Azure Resource Manager, vedere l'articolo [Creare risorse del bus di servizio usando i modelli di Azure Resource Manager](service-bus-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="14f9a-142">For information about using Azure Resource Manager templates, see the article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>
- <span data-ttu-id="14f9a-143">Informazioni sulle [librerie di gestione .NET del bus di servizio](service-bus-management-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="14f9a-143">Information about [Service Bus .NET management libraries](service-bus-management-libraries.md).</span></span>

<span data-ttu-id="14f9a-144">Esistono alcune soluzioni alternative per la gestione delle entità del bus di servizio, come descritto in questi post di blog:</span><span class="sxs-lookup"><span data-stu-id="14f9a-144">There are some alternate ways to manage Service Bus entities, as described in these blog posts:</span></span>

* [<span data-ttu-id="14f9a-145">Come creare code, argomenti e sottoscrizioni del bus di servizio tramite uno script di PowerShell</span><span class="sxs-lookup"><span data-stu-id="14f9a-145">How to create Service Bus queues, topics and subscriptions using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [<span data-ttu-id="14f9a-146">Come creare uno spazio dei nomi del bus di servizio e un hub eventi tramite uno script PowerShell</span><span class="sxs-lookup"><span data-stu-id="14f9a-146">How to create a Service Bus Namespace and an Event Hub using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)
* [<span data-ttu-id="14f9a-147">Script PowerShell del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="14f9a-147">Service Bus PowerShell Scripts</span></span>](https://code.msdn.microsoft.com/Service-Bus-PowerShell-a46b7059)

<!--Anchors-->

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
