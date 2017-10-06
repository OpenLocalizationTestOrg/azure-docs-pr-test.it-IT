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
# <a name="manage-your-azure-search-service-with-powershell"></a><span data-ttu-id="b88fa-104">Gestire il servizio Ricerca di Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="b88fa-104">Manage your Azure Search service with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b88fa-105">Portale</span><span class="sxs-lookup"><span data-stu-id="b88fa-105">Portal</span></span>](search-manage.md)
> * [<span data-ttu-id="b88fa-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b88fa-106">PowerShell</span></span>](search-manage-powershell.md)
> 
> 

<span data-ttu-id="b88fa-107">In questo argomento descrive tooperform i comandi di PowerShell hello molti hello attività di gestione per i servizi di ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="b88fa-107">This topic describes hello PowerShell commands tooperform many of hello management tasks for Azure Search services.</span></span> <span data-ttu-id="b88fa-108">Illustreremo in dettaglio come creare un servizio di ricerca, come ridimensionarlo e come gestire le relative chiavi API.</span><span class="sxs-lookup"><span data-stu-id="b88fa-108">We will walk through creating a search service, scaling it, and managing its API keys.</span></span>
<span data-ttu-id="b88fa-109">Questi comandi parallela hello opzioni disponibili in hello [API REST di gestione di Azure ricerca](http://msdn.microsoft.com/library/dn832684.aspx).</span><span class="sxs-lookup"><span data-stu-id="b88fa-109">These commands parallel hello management options available in hello [Azure Search Management REST API](http://msdn.microsoft.com/library/dn832684.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b88fa-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b88fa-110">Prerequisites</span></span>
* <span data-ttu-id="b88fa-111">È necessario disporre di Azure PowerShell 1.0 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="b88fa-111">You must have Azure PowerShell 1.0 or greater.</span></span> <span data-ttu-id="b88fa-112">Per istruzioni, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b88fa-112">For instructions, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="b88fa-113">È necessario eseguire l'accesso tooyour sottoscrizione di Azure PowerShell come descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="b88fa-113">You must be logged in tooyour Azure subscription in PowerShell as described below.</span></span>

<span data-ttu-id="b88fa-114">In primo luogo, è necessario tooAzure account di accesso con questo comando:</span><span class="sxs-lookup"><span data-stu-id="b88fa-114">First, you must login tooAzure with this command:</span></span>

    Login-AzureRmAccount

<span data-ttu-id="b88fa-115">Specificare l'indirizzo di posta elettronica hello del proprio account Azure e la relativa password nella finestra di dialogo account di accesso di hello Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b88fa-115">Specify hello email address of your Azure account and its password in hello Microsoft Azure login dialog.</span></span>

<span data-ttu-id="b88fa-116">In alternativa è possibile [accedere in modo non interattivo con un'entità servizio](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="b88fa-116">Alternatively you can [login non-interactively with a service principal](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="b88fa-117">Se si dispone di più sottoscrizioni di Azure, è necessario tooset la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b88fa-117">If you have multiple Azure subscriptions, you need tooset your Azure subscription.</span></span> <span data-ttu-id="b88fa-118">toosee un elenco delle sottoscrizioni correnti, eseguire questo comando.</span><span class="sxs-lookup"><span data-stu-id="b88fa-118">toosee a list of your current subscriptions, run this command.</span></span>

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="b88fa-119">toospecify hello sottoscrizione eseguire hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="b88fa-119">toospecify hello subscription, run hello following command.</span></span> <span data-ttu-id="b88fa-120">Nell'esempio seguente di hello, nome della sottoscrizione hello è `ContosoSubscription`.</span><span class="sxs-lookup"><span data-stu-id="b88fa-120">In hello following example, hello subscription name is `ContosoSubscription`.</span></span>

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

## <a name="commands-toohelp-you-get-started"></a><span data-ttu-id="b88fa-121">Comandi toohelp iniziare</span><span class="sxs-lookup"><span data-stu-id="b88fa-121">Commands toohelp you get started</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="b88fa-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b88fa-122">Next Steps</span></span>
<span data-ttu-id="b88fa-123">Dopo aver creato il servizio, è possibile eseguire i passaggi successivi di hello: compilare un [indice](search-what-is-an-index.md), [un indice di query](search-query-overview.md)e infine creare e gestire la propria applicazione di ricerca che utilizza una ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="b88fa-123">Now that your service is created, you can take hello next steps: build an [index](search-what-is-an-index.md), [query an index](search-query-overview.md), and finally create and manage your own search application that uses Azure Search.</span></span>

* [<span data-ttu-id="b88fa-124">Creare un indice di ricerca di Azure nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="b88fa-124">Create an Azure Search index in hello Azure portal</span></span>](search-create-index-portal.md)
* [<span data-ttu-id="b88fa-125">Query di un indice di ricerca di Azure utilizzando Esplora ricerche in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b88fa-125">Query an Azure Search index using Search Explorer in hello Azure portal</span></span>](search-explorer.md)
* [<span data-ttu-id="b88fa-126">Dati di tooload un indicizzatore da altri servizi del programma di installazione</span><span class="sxs-lookup"><span data-stu-id="b88fa-126">Setup an indexer tooload data from other services</span></span>](search-indexer-overview.md)
* [<span data-ttu-id="b88fa-127">La modalità di ricerca di Azure toouse in .NET</span><span class="sxs-lookup"><span data-stu-id="b88fa-127">How toouse Azure Search in .NET</span></span>](search-howto-dotnet-sdk.md)
* [<span data-ttu-id="b88fa-128">Analizzare il traffico di Ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="b88fa-128">Analyze your Azure Search traffic</span></span>](search-traffic-analytics.md)

