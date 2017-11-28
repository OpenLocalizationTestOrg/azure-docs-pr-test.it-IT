---
title: risorse di Azure Service Bus aaaUse PowerShell toomanage | Documenti Microsoft
description: Utilizzare PowerShell modulo toocreate e gestire le risorse di Service Bus
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
ms.openlocfilehash: 737044def913c5798e7e05fc4f1aeece76c8f4dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomanage-service-bus-resources"></a><span data-ttu-id="b76f5-103">Utilizzare le risorse di Service Bus toomanage di PowerShell</span><span class="sxs-lookup"><span data-stu-id="b76f5-103">Use PowerShell toomanage Service Bus resources</span></span>

<span data-ttu-id="b76f5-104">Microsoft Azure PowerShell è un ambiente di scripting che è possibile utilizzare toocontrol e automatizzare la distribuzione di hello e gestione dei servizi Azure.</span><span class="sxs-lookup"><span data-stu-id="b76f5-104">Microsoft Azure PowerShell is a scripting environment that you can use toocontrol and automate hello deployment and management of Azure services.</span></span> <span data-ttu-id="b76f5-105">Questo articolo viene descritto come hello toouse [modulo PowerShell di gestione di risorse Bus di servizio](/powershell/module/azurerm.servicebus) tooprovision e gestire le entità del Bus di servizio (spazi dei nomi, code, argomenti e sottoscrizioni) utilizzando una console locale di Azure PowerShell o script.</span><span class="sxs-lookup"><span data-stu-id="b76f5-105">This article describes how toouse hello [Service Bus Resource Manager PowerShell module](/powershell/module/azurerm.servicebus) tooprovision and manage Service Bus entities (namespaces, queues, topics, and subscriptions) using a local Azure PowerShell console or script.</span></span>

<span data-ttu-id="b76f5-106">È possibile gestire le risorse del bus di servizio anche usando i modelli di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b76f5-106">You can also manage Service Bus entities using Azure Resource Manager templates.</span></span> <span data-ttu-id="b76f5-107">Per ulteriori informazioni, vedere l'articolo hello [risorse Bus di servizio Create mediante modelli di gestione risorse di Azure](service-bus-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b76f5-107">For more information, see hello article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b76f5-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b76f5-108">Prerequisites</span></span>

<span data-ttu-id="b76f5-109">Prima di iniziare, è necessario seguente hello:</span><span class="sxs-lookup"><span data-stu-id="b76f5-109">Before you begin, you'll need hello following:</span></span>

* <span data-ttu-id="b76f5-110">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b76f5-110">An Azure subscription.</span></span> <span data-ttu-id="b76f5-111">Per altre informazioni su come ottenere una sottoscrizione, vedere le [opzioni di acquisto][purchase options], le [offerte per i membri][member offers] oppure l'[account gratuito][free account].</span><span class="sxs-lookup"><span data-stu-id="b76f5-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span></span>
* <span data-ttu-id="b76f5-112">Un computer con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b76f5-112">A computer with Azure PowerShell.</span></span> <span data-ttu-id="b76f5-113">Per le istruzioni vedere [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) (Introduzione ai cmdlet di Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="b76f5-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span></span>
* <span data-ttu-id="b76f5-114">Una conoscenza generale di script di PowerShell, i pacchetti NuGet e hello .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="b76f5-114">A general understanding of PowerShell scripts, NuGet packages, and hello .NET Framework.</span></span>

## <a name="get-started"></a><span data-ttu-id="b76f5-115">Attività iniziali</span><span class="sxs-lookup"><span data-stu-id="b76f5-115">Get started</span></span>

<span data-ttu-id="b76f5-116">primo passaggio Hello è toouse PowerShell toolog in tooyour account Azure e sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b76f5-116">hello first step is toouse PowerShell toolog in tooyour Azure account and Azure subscription.</span></span> <span data-ttu-id="b76f5-117">Seguire le istruzioni hello [Introduzione ai cmdlet di Azure PowerShell](/powershell/azure/get-started-azureps) toolog tooyour account Azure e recuperare e alle risorse di hello nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b76f5-117">Follow hello instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) toolog in tooyour Azure account, and retrieve and access hello resources in your Azure subscription.</span></span>

## <a name="provision-a-service-bus-namespace"></a><span data-ttu-id="b76f5-118">Provisioning di uno spazio dei nomi del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="b76f5-118">Provision a Service Bus namespace</span></span>

<span data-ttu-id="b76f5-119">Quando si utilizzano spazi dei nomi Service Bus, è possibile utilizzare hello [Get AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [New AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), e [Set AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b76f5-119">When working with Service Bus namespaces, you can use hello [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [New-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), and [Set-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlets.</span></span>

<span data-ttu-id="b76f5-120">Questo esempio viene creato alcune variabili locali nello script hello; `$Namespace` e `$Location`.</span><span class="sxs-lookup"><span data-stu-id="b76f5-120">This example creates a few local variables in hello script; `$Namespace` and `$Location`.</span></span>

* <span data-ttu-id="b76f5-121">`$Namespace`è il nome di hello dello spazio dei nomi Service Bus hello con cui si desidera toowork.</span><span class="sxs-lookup"><span data-stu-id="b76f5-121">`$Namespace` is hello name of hello Service Bus namespace with which we want toowork.</span></span>
* <span data-ttu-id="b76f5-122">`$Location`Identifica il centro dati hello in cui verrà è eseguito il provisioning dello spazio dei nomi hello.</span><span class="sxs-lookup"><span data-stu-id="b76f5-122">`$Location` identifies hello data center in which will we provision hello namespace.</span></span>
* <span data-ttu-id="b76f5-123">`$CurrentNamespace`Archivia hello riferimento dello spazio dei nomi che è recuperare (o creare).</span><span class="sxs-lookup"><span data-stu-id="b76f5-123">`$CurrentNamespace` stores hello reference namespace that we retrieve (or create).</span></span>

<span data-ttu-id="b76f5-124">In uno script effettivo, `$Namespace` e `$Location` possono essere passati come parametri.</span><span class="sxs-lookup"><span data-stu-id="b76f5-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span></span>

<span data-ttu-id="b76f5-125">Questa parte dello script hello hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="b76f5-125">This part of hello script does hello following:</span></span>

1. <span data-ttu-id="b76f5-126">Tentativi tooretrieve uno spazio dei nomi Service Bus con hello nome specificato.</span><span class="sxs-lookup"><span data-stu-id="b76f5-126">Attempts tooretrieve a Service Bus namespace with hello specified name.</span></span>
2. <span data-ttu-id="b76f5-127">Se lo spazio dei nomi hello viene trovato, viene segnalato ciò che è stato trovato.</span><span class="sxs-lookup"><span data-stu-id="b76f5-127">If hello namespace is found, it reports what was found.</span></span>
3. <span data-ttu-id="b76f5-128">Se non viene trovato lo spazio dei nomi hello, Crea spazio dei nomi hello e recupera quindi hello appena creato spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="b76f5-128">If hello namespace is not found, it creates hello namespace and then retrieves hello newly created namespace.</span></span>
   
    ``` powershell
    # Query toosee if hello namespace currently exists
    $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
   
    # Check if hello namespace already exists or needs toobe created
    if ($CurrentNamespace)
    {
        Write-Host "hello namespace $Namespace already exists in hello $Location region:"
        # Report what was found
        Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "hello $Namespace namespace does not exist."
        Write-Host "Creating hello $Namespace namespace in hello $Location region..."
        New-AzureRmServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
        Write-Host "hello $Namespace namespace in Resource Group $ResGrpName in hello $Location region has been successfully created."
                
    }
    ```

### <a name="create-a-namespace-authorization-rule"></a><span data-ttu-id="b76f5-129">Crea una regola di autorizzazione dello spazio dei nomi</span><span class="sxs-lookup"><span data-stu-id="b76f5-129">Create a namespace authorization rule</span></span>

<span data-ttu-id="b76f5-130">Hello esempio seguente viene illustrato come tramite le regole di autorizzazione dello spazio dei nomi toomanage hello [New AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Set AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), e [cmdlet Remove-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).</span><span class="sxs-lookup"><span data-stu-id="b76f5-130">hello following example shows how toomanage namespace authorization rules using hello [New-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Set-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), and [Remove-AzureRmServiceBusNamespaceAuthorizationRule cmdlets](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).</span></span>

```powershell
# Query toosee if rule exists
$CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

# Check if hello rule already exists or needs toobe created
if ($CurrentRule)
{
    Write-Host "hello $AuthRule rule already exists for hello namespace $Namespace."
}
else
{
    Write-Host "hello $AuthRule rule does not exist."
    Write-Host "Creating hello $AuthRule rule for hello $Namespace namespace..."
    New-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule -Rights @("Listen","Send")
    $CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
    Write-Host "hello $AuthRule rule for hello $Namespace namespace has been successfully created."

    Write-Host "Setting rights on hello namespace"
    $authRuleObj = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

    Write-Host "Remove Send rights"
    $authRuleObj.Rights.Remove("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Add Send and Manage rights toohello namespace"
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

## <a name="create-a-queue"></a><span data-ttu-id="b76f5-131">Creare una coda</span><span class="sxs-lookup"><span data-stu-id="b76f5-131">Create a queue</span></span>

<span data-ttu-id="b76f5-132">toocreate una coda o argomento, eseguire un controllo dello spazio dei nomi utilizzando script hello nella sezione precedente di hello.</span><span class="sxs-lookup"><span data-stu-id="b76f5-132">toocreate a queue or topic, perform a namespace check using hello script in hello previous section.</span></span> <span data-ttu-id="b76f5-133">Quindi, creare la coda hello:</span><span class="sxs-lookup"><span data-stu-id="b76f5-133">Then, create hello queue:</span></span>

```powershell
# Check if queue already exists
$CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName

if($CurrentQ)
{
    Write-Host "hello queue $QueueName already exists in hello $Location region:"
}
else
{
    Write-Host "hello $QueueName queue does not exist."
    Write-Host "Creating hello $QueueName queue in hello $Location region..."
    New-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -EnablePartitioning $True
    $CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName
    Write-Host "hello $QueueName queue in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

### <a name="modify-queue-properties"></a><span data-ttu-id="b76f5-134">Modificare le proprietà della coda</span><span class="sxs-lookup"><span data-stu-id="b76f5-134">Modify queue properties</span></span>

<span data-ttu-id="b76f5-135">Dopo l'esecuzione di script hello nella precedente sezione hello, è possibile utilizzare hello [Set AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) proprietà hello tooupdate di cmdlet di una coda, come in hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="b76f5-135">After executing hello script in hello preceding section, you can use hello [Set-AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) cmdlet tooupdate hello properties of a queue, as in hello following example:</span></span>

```powershell
$CurrentQ.DeadLetteringOnMessageExpiration = $True
$CurrentQ.MaxDeliveryCount = 7
$CurrentQ.MaxSizeInMegabytes = 2048
$CurrentQ.EnableExpress = $True

Set-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -QueueObj $CurrentQ
```

## <a name="provisioning-other-service-bus-entities"></a><span data-ttu-id="b76f5-136">Provisioning di altre entità del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="b76f5-136">Provisioning other Service Bus entities</span></span>

<span data-ttu-id="b76f5-137">È possibile utilizzare hello [modulo PowerShell di Service Bus](/powershell/module/azurerm.servicebus) tooprovision altre entità, ad esempio argomenti e sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="b76f5-137">You can use hello [Service Bus PowerShell module](/powershell/module/azurerm.servicebus) tooprovision other entities, such as topics and subscriptions.</span></span> <span data-ttu-id="b76f5-138">Questi cmdlet sono sintatticamente simile toohello coda creazione cmdlet illustrati nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="b76f5-138">These cmdlets are syntactically similar toohello queue creation cmdlets demonstrated in hello previous section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b76f5-139">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b76f5-139">Next steps</span></span>

- <span data-ttu-id="b76f5-140">Vedere documentazione di modulo PowerShell di Service Bus Resource Manager completa hello [qui](/powershell/module/azurerm.servicebus).</span><span class="sxs-lookup"><span data-stu-id="b76f5-140">See hello complete Service Bus Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.servicebus).</span></span> <span data-ttu-id="b76f5-141">Questa pagina elenca tutti i cmdlet disponibili.</span><span class="sxs-lookup"><span data-stu-id="b76f5-141">This page lists all available cmdlets.</span></span>
- <span data-ttu-id="b76f5-142">Per informazioni sull'utilizzo dei modelli di gestione risorse di Azure, vedere l'articolo hello [risorse Bus di servizio Create mediante modelli di gestione risorse di Azure](service-bus-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b76f5-142">For information about using Azure Resource Manager templates, see hello article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>
- <span data-ttu-id="b76f5-143">Informazioni sulle [librerie di gestione .NET del bus di servizio](service-bus-management-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="b76f5-143">Information about [Service Bus .NET management libraries](service-bus-management-libraries.md).</span></span>

<span data-ttu-id="b76f5-144">Esistono alcuni modi alternativi toomanage entità del Bus di servizio, come descritto in questi post di blog:</span><span class="sxs-lookup"><span data-stu-id="b76f5-144">There are some alternate ways toomanage Service Bus entities, as described in these blog posts:</span></span>

* [<span data-ttu-id="b76f5-145">Il Bus di servizio toocreate code, argomenti e sottoscrizioni tramite uno script di PowerShell</span><span class="sxs-lookup"><span data-stu-id="b76f5-145">How toocreate Service Bus queues, topics and subscriptions using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [<span data-ttu-id="b76f5-146">Come toocreate Namespace Bus di servizio e un Hub di eventi tramite uno script di PowerShell</span><span class="sxs-lookup"><span data-stu-id="b76f5-146">How toocreate a Service Bus Namespace and an Event Hub using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)
* [<span data-ttu-id="b76f5-147">Script PowerShell del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="b76f5-147">Service Bus PowerShell Scripts</span></span>](https://code.msdn.microsoft.com/Service-Bus-PowerShell-a46b7059)

<!--Anchors-->

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
