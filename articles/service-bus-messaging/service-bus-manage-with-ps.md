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
# <a name="use-powershell-toomanage-service-bus-resources"></a>Utilizzare le risorse di Service Bus toomanage di PowerShell

Microsoft Azure PowerShell è un ambiente di scripting che è possibile utilizzare toocontrol e automatizzare la distribuzione di hello e gestione dei servizi Azure. Questo articolo viene descritto come hello toouse [modulo PowerShell di gestione di risorse Bus di servizio](/powershell/module/azurerm.servicebus) tooprovision e gestire le entità del Bus di servizio (spazi dei nomi, code, argomenti e sottoscrizioni) utilizzando una console locale di Azure PowerShell o script.

È possibile gestire le risorse del bus di servizio anche usando i modelli di Azure Resource Manager. Per ulteriori informazioni, vedere l'articolo hello [risorse Bus di servizio Create mediante modelli di gestione risorse di Azure](service-bus-resource-manager-overview.md).

## <a name="prerequisites"></a>Prerequisiti

Prima di iniziare, è necessario seguente hello:

* Una sottoscrizione di Azure. Per altre informazioni su come ottenere una sottoscrizione, vedere le [opzioni di acquisto][purchase options], le [offerte per i membri][member offers] oppure l'[account gratuito][free account].
* Un computer con Azure PowerShell. Per le istruzioni vedere [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) (Introduzione ai cmdlet di Azure PowerShell).
* Una conoscenza generale di script di PowerShell, i pacchetti NuGet e hello .NET Framework.

## <a name="get-started"></a>Attività iniziali

primo passaggio Hello è toouse PowerShell toolog in tooyour account Azure e sottoscrizione di Azure. Seguire le istruzioni hello [Introduzione ai cmdlet di Azure PowerShell](/powershell/azure/get-started-azureps) toolog tooyour account Azure e recuperare e alle risorse di hello nella sottoscrizione di Azure.

## <a name="provision-a-service-bus-namespace"></a>Provisioning di uno spazio dei nomi del bus di servizio

Quando si utilizzano spazi dei nomi Service Bus, è possibile utilizzare hello [Get AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [New AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), e [Set AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlet.

Questo esempio viene creato alcune variabili locali nello script hello; `$Namespace` e `$Location`.

* `$Namespace`è il nome di hello dello spazio dei nomi Service Bus hello con cui si desidera toowork.
* `$Location`Identifica il centro dati hello in cui verrà è eseguito il provisioning dello spazio dei nomi hello.
* `$CurrentNamespace`Archivia hello riferimento dello spazio dei nomi che è recuperare (o creare).

In uno script effettivo, `$Namespace` e `$Location` possono essere passati come parametri.

Questa parte dello script hello hello seguenti:

1. Tentativi tooretrieve uno spazio dei nomi Service Bus con hello nome specificato.
2. Se lo spazio dei nomi hello viene trovato, viene segnalato ciò che è stato trovato.
3. Se non viene trovato lo spazio dei nomi hello, Crea spazio dei nomi hello e recupera quindi hello appena creato spazio dei nomi.
   
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

### <a name="create-a-namespace-authorization-rule"></a>Crea una regola di autorizzazione dello spazio dei nomi

Hello esempio seguente viene illustrato come tramite le regole di autorizzazione dello spazio dei nomi toomanage hello [New AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Set AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), e [cmdlet Remove-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).

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

## <a name="create-a-queue"></a>Creare una coda

toocreate una coda o argomento, eseguire un controllo dello spazio dei nomi utilizzando script hello nella sezione precedente di hello. Quindi, creare la coda hello:

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

### <a name="modify-queue-properties"></a>Modificare le proprietà della coda

Dopo l'esecuzione di script hello nella precedente sezione hello, è possibile utilizzare hello [Set AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) proprietà hello tooupdate di cmdlet di una coda, come in hello di esempio seguente:

```powershell
$CurrentQ.DeadLetteringOnMessageExpiration = $True
$CurrentQ.MaxDeliveryCount = 7
$CurrentQ.MaxSizeInMegabytes = 2048
$CurrentQ.EnableExpress = $True

Set-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -QueueObj $CurrentQ
```

## <a name="provisioning-other-service-bus-entities"></a>Provisioning di altre entità del bus di servizio

È possibile utilizzare hello [modulo PowerShell di Service Bus](/powershell/module/azurerm.servicebus) tooprovision altre entità, ad esempio argomenti e sottoscrizioni. Questi cmdlet sono sintatticamente simile toohello coda creazione cmdlet illustrati nella sezione precedente hello.

## <a name="next-steps"></a>Passaggi successivi

- Vedere documentazione di modulo PowerShell di Service Bus Resource Manager completa hello [qui](/powershell/module/azurerm.servicebus). Questa pagina elenca tutti i cmdlet disponibili.
- Per informazioni sull'utilizzo dei modelli di gestione risorse di Azure, vedere l'articolo hello [risorse Bus di servizio Create mediante modelli di gestione risorse di Azure](service-bus-resource-manager-overview.md).
- Informazioni sulle [librerie di gestione .NET del bus di servizio](service-bus-management-libraries.md).

Esistono alcuni modi alternativi toomanage entità del Bus di servizio, come descritto in questi post di blog:

* [Il Bus di servizio toocreate code, argomenti e sottoscrizioni tramite uno script di PowerShell](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [Come toocreate Namespace Bus di servizio e un Hub di eventi tramite uno script di PowerShell](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)
* [Script PowerShell del bus di servizio](https://code.msdn.microsoft.com/Service-Bus-PowerShell-a46b7059)

<!--Anchors-->

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
