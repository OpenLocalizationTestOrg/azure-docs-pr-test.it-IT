---
title: aaaManage ricerca di Azure con gli script di Powershell | Documenti Microsoft
description: Gestire il servizio Ricerca di Azure con script di PowerShell. Creare o aggiornare un servizio Ricerca di Azure e gestire le relative chiavi amministratore
services: search
documentationcenter: 
author: seansaleh
manager: mblythe
editor: 
tags: azure-resource-manager
ms.assetid: 9b3dc1f2-3619-4235-ba1f-d2d6f5c45dd5
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: powershell
ms.date: 08/15/2016
ms.author: seasa
ms.openlocfilehash: fc7fb4b025340c77717601e0aaee938be3e9230f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-azure-search-service-with-powershell"></a>Gestire il servizio Ricerca di Azure con PowerShell
> [!div class="op_single_selector"]
> * [Portale](search-manage.md)
> * [PowerShell](search-manage-powershell.md)
> 
> 

In questo argomento descrive tooperform i comandi di PowerShell hello molti hello attività di gestione per i servizi di ricerca di Azure. Illustreremo in dettaglio come creare un servizio di ricerca, come ridimensionarlo e come gestire le relative chiavi API.
Questi comandi parallela hello opzioni disponibili in hello [API REST di gestione di Azure ricerca](http://msdn.microsoft.com/library/dn832684.aspx).

## <a name="prerequisites"></a>Prerequisiti
* È necessario disporre di Azure PowerShell 1.0 o versioni successive. Per istruzioni, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).
* È necessario eseguire l'accesso tooyour sottoscrizione di Azure PowerShell come descritto di seguito.

In primo luogo, è necessario tooAzure account di accesso con questo comando:

    Login-AzureRmAccount

Specificare l'indirizzo di posta elettronica hello del proprio account Azure e la relativa password nella finestra di dialogo account di accesso di hello Microsoft Azure.

In alternativa è possibile [accedere in modo non interattivo con un'entità servizio](../azure-resource-manager/resource-group-authenticate-service-principal.md).

Se si dispone di più sottoscrizioni di Azure, è necessario tooset la sottoscrizione di Azure. toosee un elenco delle sottoscrizioni correnti, eseguire questo comando.

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

toospecify hello sottoscrizione eseguire hello comando seguente. Nell'esempio seguente di hello, nome della sottoscrizione hello è `ContosoSubscription`.

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

## <a name="commands-toohelp-you-get-started"></a>Comandi toohelp iniziare
    $serviceName = "your-service-name-lowercase-with-dashes"
    $sku = "free" # or "basic" or "standard" for paid services
    $location = "West US"
    # You can get a list of potential locations with
    # (Get-AzureRmResourceProvider -ListAvailable | Where-Object {$_.ProviderNamespace -eq 'Microsoft.Search'}).Locations
    $resourceGroupName = "YourResourceGroup" 
    # If you don't already have this resource group, you can create it with 
    # New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Register hello ARM provider idempotently. This must be done once per subscription
    Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Search"

    # Create a new search service
    # This command will return once hello service is fully created
    New-AzureRmResourceGroupDeployment `
        -ResourceGroupName $resourceGroupName `
        -TemplateUri "https://gallery.azure.com/artifact/20151001/Microsoft.Search.1.0.9/DeploymentTemplates/searchServiceDefaultTemplate.json" `
        -NameFromTemplate $serviceName `
        -Sku $sku `
        -Location $location `
        -PartitionCount 1 `
        -ReplicaCount 1

    # Get information about your new service and store it in $resource
    $resource = Get-AzureRmResource `
        -ResourceType "Microsoft.Search/searchServices" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19

    # View your resource
    $resource

    # Get hello primary admin API key
    $primaryKey = (Invoke-AzureRmResourceAction `
        -Action listAdminKeys `
        -ResourceId $resource.ResourceId `
        -ApiVersion 2015-08-19).PrimaryKey

    # Regenerate hello secondary admin API Key
    $secondaryKey = (Invoke-AzureRmResourceAction `
        -ResourceType "Microsoft.Search/searchServices/regenerateAdminKey" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19 `
        -Action secondary).SecondaryKey

    # Create a query key for read only access tooyour indexes
    $queryKeyDescription = "query-key-created-from-powershell"
    $queryKey = (Invoke-AzureRmResourceAction `
        -ResourceType "Microsoft.Search/searchServices/createQueryKey" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19 `
        -Action $queryKeyDescription).Key

    # View your query key
    $queryKey

    # Delete query key
    Remove-AzureRmResource `
        -ResourceType "Microsoft.Search/searchServices/deleteQueryKey/$($queryKey)" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19

    # Scale your service up
    # Note that this will only work if you made a non "free" service
    # This command will not return until hello operation is finished
    # It can take 15 minutes or more tooprovision hello additional resources
    $resource.Properties.ReplicaCount = 2
    $resource | Set-AzureRmResource

    # Delete your service
    # Deleting your service will delete all indexes and data in hello service
    $resource | Remove-AzureRmResource

## <a name="next-steps"></a>Passaggi successivi
Dopo aver creato il servizio, è possibile eseguire i passaggi successivi di hello: compilare un [indice](search-what-is-an-index.md), [un indice di query](search-query-overview.md)e infine creare e gestire la propria applicazione di ricerca che utilizza una ricerca di Azure.

* [Creare un indice di ricerca di Azure nel portale di Azure hello](search-create-index-portal.md)
* [Query di un indice di ricerca di Azure utilizzando Esplora ricerche in hello portale di Azure](search-explorer.md)
* [Dati di tooload un indicizzatore da altri servizi del programma di installazione](search-indexer-overview.md)
* [La modalità di ricerca di Azure toouse in .NET](search-howto-dotnet-sdk.md)
* [Analizzare il traffico di Ricerca di Azure](search-traffic-analytics.md)

