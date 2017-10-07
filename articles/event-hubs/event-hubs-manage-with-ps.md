---
title: risorse di hub eventi di Azure aaaUse PowerShell toomanage | Documenti Microsoft
description: Utilizzare PowerShell modulo toocreate e gestire hub eventi
services: event-hubs
documentationcenter: .NET
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: d79cb307c2b4a031d059ce6ca67117ffc0b4600b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomanage-event-hubs-resources"></a><span data-ttu-id="857fa-103">Utilizzare le risorse di PowerShell toomanage hub eventi</span><span class="sxs-lookup"><span data-stu-id="857fa-103">Use PowerShell toomanage Event Hubs resources</span></span>

<span data-ttu-id="857fa-104">Microsoft Azure PowerShell è un ambiente di scripting che è possibile utilizzare toocontrol e automatizzare la distribuzione di hello e gestione dei servizi Azure.</span><span class="sxs-lookup"><span data-stu-id="857fa-104">Microsoft Azure PowerShell is a scripting environment that you can use toocontrol and automate hello deployment and management of Azure services.</span></span> <span data-ttu-id="857fa-105">Questo articolo viene descritto come hello toouse [modulo PowerShell di gestione risorse hub eventi](/powershell/module/azurerm.eventhub) tooprovision e gestire le entità di hub di eventi (spazi dei nomi, gli hub di eventi singoli e gruppi di consumer) utilizzando una console locale di Azure PowerShell o script.</span><span class="sxs-lookup"><span data-stu-id="857fa-105">This article describes how toouse hello [Event Hubs Resource Manager PowerShell module](/powershell/module/azurerm.eventhub) tooprovision and manage Event Hubs entities (namespaces, individual event hubs, and consumer groups) using a local Azure PowerShell console or script.</span></span>

<span data-ttu-id="857fa-106">È anche possibile gestire risorse Hub eventi usando i modelli di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="857fa-106">You can also manage Event Hubs resources using Azure Resource Manager templates.</span></span> <span data-ttu-id="857fa-107">Per ulteriori informazioni, vedere l'articolo hello [creare uno spazio dei nomi dell'hub eventi con gruppo di hub e consumer di eventi utilizzando un modello di gestione risorse di Azure](event-hubs-resource-manager-namespace-event-hub.md).</span><span class="sxs-lookup"><span data-stu-id="857fa-107">For more information, see hello article [Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="857fa-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="857fa-108">Prerequisites</span></span>

<span data-ttu-id="857fa-109">Prima di iniziare, è necessario seguente hello:</span><span class="sxs-lookup"><span data-stu-id="857fa-109">Before you begin, you'll need hello following:</span></span>

* <span data-ttu-id="857fa-110">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="857fa-110">An Azure subscription.</span></span> <span data-ttu-id="857fa-111">Per altre informazioni su come ottenere una sottoscrizione, vedere le [opzioni di acquisto][purchase options], le [offerte per i membri][member offers] oppure l'[account gratuito][free account].</span><span class="sxs-lookup"><span data-stu-id="857fa-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span></span>
* <span data-ttu-id="857fa-112">Un computer con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="857fa-112">A computer with Azure PowerShell.</span></span> <span data-ttu-id="857fa-113">Per le istruzioni vedere [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) (Introduzione ai cmdlet di Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="857fa-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span></span>
* <span data-ttu-id="857fa-114">Una conoscenza generale di script di PowerShell, i pacchetti NuGet e hello .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="857fa-114">A general understanding of PowerShell scripts, NuGet packages, and hello .NET Framework.</span></span>

## <a name="get-started"></a><span data-ttu-id="857fa-115">Attività iniziali</span><span class="sxs-lookup"><span data-stu-id="857fa-115">Get started</span></span>

<span data-ttu-id="857fa-116">primo passaggio Hello è toouse PowerShell toolog in tooyour account Azure e sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="857fa-116">hello first step is toouse PowerShell toolog in tooyour Azure account and Azure subscription.</span></span> <span data-ttu-id="857fa-117">Seguire le istruzioni hello [Introduzione ai cmdlet di Azure PowerShell](/powershell/azure/get-started-azureps) toolog in tooyour account Azure, quindi recuperare e accedere alle risorse di hello nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="857fa-117">Follow hello instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) toolog in tooyour Azure account, then retrieve and access hello resources in your Azure subscription.</span></span>

## <a name="provision-an-event-hubs-namespace"></a><span data-ttu-id="857fa-118">Eseguire il provisioning di uno spazio dei nomi di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="857fa-118">Provision an Event Hubs namespace</span></span>

<span data-ttu-id="857fa-119">Quando si utilizzano gli spazi dei nomi di hub eventi, è possibile utilizzare hello [Get AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [New AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [Remove AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace) , e [Set AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="857fa-119">When working with Event Hubs namespaces, you can use hello [Get-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [New-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [Remove-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace), and [Set-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) cmdlets.</span></span>

<span data-ttu-id="857fa-120">Questo esempio viene creato alcune variabili locali nello script hello; `$Namespace` e `$Location`.</span><span class="sxs-lookup"><span data-stu-id="857fa-120">This example creates a few local variables in hello script; `$Namespace` and `$Location`.</span></span>

* <span data-ttu-id="857fa-121">`$Namespace`è il nome di hello dello spazio dei nomi di hub eventi hello con cui si desidera toowork.</span><span class="sxs-lookup"><span data-stu-id="857fa-121">`$Namespace` is hello name of hello Event Hubs namespace with which we want toowork.</span></span>
* <span data-ttu-id="857fa-122">`$Location`Identifica il centro dati hello in cui verrà è eseguito il provisioning dello spazio dei nomi hello.</span><span class="sxs-lookup"><span data-stu-id="857fa-122">`$Location` identifies hello data center in which will we provision hello namespace.</span></span>
* <span data-ttu-id="857fa-123">`$CurrentNamespace`Archivia hello riferimento dello spazio dei nomi che è recuperare (o creare).</span><span class="sxs-lookup"><span data-stu-id="857fa-123">`$CurrentNamespace` stores hello reference namespace that we retrieve (or create).</span></span>

<span data-ttu-id="857fa-124">In uno script effettivo, `$Namespace` e `$Location` possono essere passati come parametri.</span><span class="sxs-lookup"><span data-stu-id="857fa-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span></span>

<span data-ttu-id="857fa-125">Questa parte dello script hello hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="857fa-125">This part of hello script does hello following:</span></span>

1. <span data-ttu-id="857fa-126">Tentativi tooretrieve uno spazio dei nomi di hub eventi con hello nome specificato.</span><span class="sxs-lookup"><span data-stu-id="857fa-126">Attempts tooretrieve an Event Hubs namespace with hello specified name.</span></span>
2. <span data-ttu-id="857fa-127">Se lo spazio dei nomi hello viene trovato, viene segnalato ciò che è stato trovato.</span><span class="sxs-lookup"><span data-stu-id="857fa-127">If hello namespace is found, it reports what was found.</span></span>
3. <span data-ttu-id="857fa-128">Se non viene trovato lo spazio dei nomi hello, Crea spazio dei nomi hello e recupera quindi hello appena creato spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="857fa-128">If hello namespace is not found, it creates hello namespace and then retrieves hello newly created namespace.</span></span>

    ```powershell
    # Query toosee if hello namespace currently exists
    $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
   
    # Check if hello namespace already exists or needs toobe created
    if ($CurrentNamespace)
    {
        Write-Host "hello namespace $Namespace already exists in hello $Location region:"
        # Report what was found
        Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "hello $Namespace namespace does not exist."
        Write-Host "Creating hello $Namespace namespace in hello $Location region..."
        New-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
        Write-Host "hello $Namespace namespace in Resource Group $ResGrpName in hello $Location region has been successfully created."
    }
    ```

## <a name="create-an-event-hub"></a><span data-ttu-id="857fa-129">Creare un hub eventi</span><span class="sxs-lookup"><span data-stu-id="857fa-129">Create an event hub</span></span>

<span data-ttu-id="857fa-130">toocreate un hub di eventi, eseguire una verifica di spazio dei nomi utilizzando script hello nella sezione precedente di hello.</span><span class="sxs-lookup"><span data-stu-id="857fa-130">toocreate an event hub, perform a namespace check using hello script in hello previous section.</span></span> <span data-ttu-id="857fa-131">Utilizzare quindi hello [New AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) hub di eventi hello toocreate cmdlet:</span><span class="sxs-lookup"><span data-stu-id="857fa-131">Then, use hello [New-AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) cmdlet toocreate hello event hub:</span></span>

```powershell
# Check if event hub already exists
$CurrentEH = Get-AzureRMEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName

if($CurrentEH)
{
    Write-Host "hello event hub $EventHubName already exists in hello $Location region:"
    # Report what was found
    Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "hello $EventHubName event hub does not exist."
    Write-Host "Creating hello $EventHubName event hub in hello $Location region..."
    New-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -Location $Location -MessageRetentionInDays 3
    $CurrentEH = Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "hello $EventHubName event hub in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

### <a name="create-a-consumer-group"></a><span data-ttu-id="857fa-132">Creare un gruppo di consumer</span><span class="sxs-lookup"><span data-stu-id="857fa-132">Create a consumer group</span></span>

<span data-ttu-id="857fa-133">toocreate un gruppo di consumer all'interno di un hub di eventi, eseguire hello dello spazio dei nomi ed evento hub controlli utilizzando gli script di hello nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="857fa-133">toocreate a consumer group within an event hub, perform hello namespace and event hub checks using hello scripts in hello previous section.</span></span> <span data-ttu-id="857fa-134">Utilizzare quindi hello [New AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) gruppo di consumer hello toocreate cmdlet all'interno di hub eventi hello.</span><span class="sxs-lookup"><span data-stu-id="857fa-134">Then, use hello [New-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) cmdlet toocreate hello consumer group within hello event hub.</span></span> <span data-ttu-id="857fa-135">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="857fa-135">For example:</span></span>

```powershell
# Check if consumer group already exists
$CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -ErrorAction Ignore

if($CurrentCG)
{
    Write-Host "hello consumer group $ConsumerGroupName in event hub $EventHubName already exists in hello $Location region:"
    # Report what was found
    Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "hello $ConsumerGroupName consumer group does not exist."
    Write-Host "Creating hello $ConsumerGroupName consumer group in hello $Location region..."
    New-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
    $CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "hello $ConsumerGroupName consumer group in event hub $EventHubName in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

#### <a name="set-user-metadata"></a><span data-ttu-id="857fa-136">Impostare i metadati dell'utente</span><span class="sxs-lookup"><span data-stu-id="857fa-136">Set user metadata</span></span>

<span data-ttu-id="857fa-137">Dopo l'esecuzione di script hello in hello sezioni precedenti, è possibile utilizzare hello [Set AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) proprietà hello tooupdate di cmdlet di un gruppo di consumer, come in hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="857fa-137">After executing hello scripts in hello preceding sections, you can use hello [Set-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) cmdlet tooupdate hello properties of a consumer group, as in hello following example:</span></span>

```powershell
# Set some user metadata on hello CG
Write-Host "Setting hello UserMetadata field too'Testing'"
Set-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -UserMetadata "Testing"
# Show result
Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
```

## <a name="remove-event-hub"></a><span data-ttu-id="857fa-138">Rimuovere un hub eventi</span><span class="sxs-lookup"><span data-stu-id="857fa-138">Remove event hub</span></span>

<span data-ttu-id="857fa-139">tooremove hello gli hub eventi è stato creato, è possibile utilizzare hello `Remove-*` cmdlet, come in hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="857fa-139">tooremove hello event hubs you created, you can use hello `Remove-*` cmdlets, as in hello following example:</span></span>

```powershell
# Clean up
Remove-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
Remove-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
Remove-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
```

## <a name="next-steps"></a><span data-ttu-id="857fa-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="857fa-140">Next steps</span></span>

- <span data-ttu-id="857fa-141">Vedere la documentazione modulo PowerShell di gestione risorse hub eventi completa hello [qui](/powershell/module/azurerm.eventhub).</span><span class="sxs-lookup"><span data-stu-id="857fa-141">See hello complete Event Hubs Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.eventhub).</span></span> <span data-ttu-id="857fa-142">Questa pagina elenca tutti i cmdlet disponibili.</span><span class="sxs-lookup"><span data-stu-id="857fa-142">This page lists all available cmdlets.</span></span>
- <span data-ttu-id="857fa-143">Per informazioni sull'utilizzo dei modelli di gestione risorse di Azure, vedere l'articolo hello [creare uno spazio dei nomi dell'hub eventi con gruppo di hub e consumer di eventi utilizzando un modello di gestione risorse di Azure](event-hubs-resource-manager-namespace-event-hub.md).</span><span class="sxs-lookup"><span data-stu-id="857fa-143">For information about using Azure Resource Manager templates, see hello article [Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub.md).</span></span>
- <span data-ttu-id="857fa-144">Informazioni sulle [librerie di gestione .NET di hub eventi](event-hubs-management-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="857fa-144">Information about [Event Hubs .NET management libraries](event-hubs-management-libraries.md).</span></span>

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
