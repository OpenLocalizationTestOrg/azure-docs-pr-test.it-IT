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
# <a name="use-powershell-toomanage-event-hubs-resources"></a>Utilizzare le risorse di PowerShell toomanage hub eventi

Microsoft Azure PowerShell è un ambiente di scripting che è possibile utilizzare toocontrol e automatizzare la distribuzione di hello e gestione dei servizi Azure. Questo articolo viene descritto come hello toouse [modulo PowerShell di gestione risorse hub eventi](/powershell/module/azurerm.eventhub) tooprovision e gestire le entità di hub di eventi (spazi dei nomi, gli hub di eventi singoli e gruppi di consumer) utilizzando una console locale di Azure PowerShell o script.

È anche possibile gestire risorse Hub eventi usando i modelli di Azure Resource Manager. Per ulteriori informazioni, vedere l'articolo hello [creare uno spazio dei nomi dell'hub eventi con gruppo di hub e consumer di eventi utilizzando un modello di gestione risorse di Azure](event-hubs-resource-manager-namespace-event-hub.md).

## <a name="prerequisites"></a>Prerequisiti

Prima di iniziare, è necessario seguente hello:

* Una sottoscrizione di Azure. Per altre informazioni su come ottenere una sottoscrizione, vedere le [opzioni di acquisto][purchase options], le [offerte per i membri][member offers] oppure l'[account gratuito][free account].
* Un computer con Azure PowerShell. Per le istruzioni vedere [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) (Introduzione ai cmdlet di Azure PowerShell).
* Una conoscenza generale di script di PowerShell, i pacchetti NuGet e hello .NET Framework.

## <a name="get-started"></a>Attività iniziali

primo passaggio Hello è toouse PowerShell toolog in tooyour account Azure e sottoscrizione di Azure. Seguire le istruzioni hello [Introduzione ai cmdlet di Azure PowerShell](/powershell/azure/get-started-azureps) toolog in tooyour account Azure, quindi recuperare e accedere alle risorse di hello nella sottoscrizione di Azure.

## <a name="provision-an-event-hubs-namespace"></a>Eseguire il provisioning di uno spazio dei nomi di Hub eventi

Quando si utilizzano gli spazi dei nomi di hub eventi, è possibile utilizzare hello [Get AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [New AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [Remove AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace) , e [Set AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) cmdlet.

Questo esempio viene creato alcune variabili locali nello script hello; `$Namespace` e `$Location`.

* `$Namespace`è il nome di hello dello spazio dei nomi di hub eventi hello con cui si desidera toowork.
* `$Location`Identifica il centro dati hello in cui verrà è eseguito il provisioning dello spazio dei nomi hello.
* `$CurrentNamespace`Archivia hello riferimento dello spazio dei nomi che è recuperare (o creare).

In uno script effettivo, `$Namespace` e `$Location` possono essere passati come parametri.

Questa parte dello script hello hello seguenti:

1. Tentativi tooretrieve uno spazio dei nomi di hub eventi con hello nome specificato.
2. Se lo spazio dei nomi hello viene trovato, viene segnalato ciò che è stato trovato.
3. Se non viene trovato lo spazio dei nomi hello, Crea spazio dei nomi hello e recupera quindi hello appena creato spazio dei nomi.

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

## <a name="create-an-event-hub"></a>Creare un hub eventi

toocreate un hub di eventi, eseguire una verifica di spazio dei nomi utilizzando script hello nella sezione precedente di hello. Utilizzare quindi hello [New AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) hub di eventi hello toocreate cmdlet:

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

### <a name="create-a-consumer-group"></a>Creare un gruppo di consumer

toocreate un gruppo di consumer all'interno di un hub di eventi, eseguire hello dello spazio dei nomi ed evento hub controlli utilizzando gli script di hello nella sezione precedente hello. Utilizzare quindi hello [New AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) gruppo di consumer hello toocreate cmdlet all'interno di hub eventi hello. ad esempio:

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

#### <a name="set-user-metadata"></a>Impostare i metadati dell'utente

Dopo l'esecuzione di script hello in hello sezioni precedenti, è possibile utilizzare hello [Set AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) proprietà hello tooupdate di cmdlet di un gruppo di consumer, come in hello di esempio seguente:

```powershell
# Set some user metadata on hello CG
Write-Host "Setting hello UserMetadata field too'Testing'"
Set-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -UserMetadata "Testing"
# Show result
Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
```

## <a name="remove-event-hub"></a>Rimuovere un hub eventi

tooremove hello gli hub eventi è stato creato, è possibile utilizzare hello `Remove-*` cmdlet, come in hello di esempio seguente:

```powershell
# Clean up
Remove-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
Remove-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
Remove-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
```

## <a name="next-steps"></a>Passaggi successivi

- Vedere la documentazione modulo PowerShell di gestione risorse hub eventi completa hello [qui](/powershell/module/azurerm.eventhub). Questa pagina elenca tutti i cmdlet disponibili.
- Per informazioni sull'utilizzo dei modelli di gestione risorse di Azure, vedere l'articolo hello [creare uno spazio dei nomi dell'hub eventi con gruppo di hub e consumer di eventi utilizzando un modello di gestione risorse di Azure](event-hubs-resource-manager-namespace-event-hub.md).
- Informazioni sulle [librerie di gestione .NET di hub eventi](event-hubs-management-libraries.md).

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
