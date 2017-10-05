---
title: Gestire Ricerca di Azure con script di PowerShell | Microsoft Docs
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
ms.openlocfilehash: aa51c846efef12461ec382274199bc049c42aaa3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="manage-your-azure-search-service-with-powershell"></a><span data-ttu-id="c0f18-104">Gestire il servizio Ricerca di Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="c0f18-104">Manage your Azure Search service with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c0f18-105">Portale</span><span class="sxs-lookup"><span data-stu-id="c0f18-105">Portal</span></span>](search-manage.md)
> * [<span data-ttu-id="c0f18-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c0f18-106">PowerShell</span></span>](search-manage-powershell.md)
> 
> 

<span data-ttu-id="c0f18-107">Questo argomento descrive i comandi di PowerShell che consentono di eseguire molte delle attività di gestione dei servizi di Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="c0f18-107">This topic describes the PowerShell commands to perform many of the management tasks for Azure Search services.</span></span> <span data-ttu-id="c0f18-108">Illustreremo in dettaglio come creare un servizio di ricerca, come ridimensionarlo e come gestire le relative chiavi API.</span><span class="sxs-lookup"><span data-stu-id="c0f18-108">We will walk through creating a search service, scaling it, and managing its API keys.</span></span>
<span data-ttu-id="c0f18-109">Questi comandi si affiancano alle opzioni di gestione disponibili nella pagina relativa alle [API REST di gestione di Ricerca di Azure](http://msdn.microsoft.com/library/dn832684.aspx).</span><span class="sxs-lookup"><span data-stu-id="c0f18-109">These commands parallel the management options available in the [Azure Search Management REST API](http://msdn.microsoft.com/library/dn832684.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0f18-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c0f18-110">Prerequisites</span></span>
* <span data-ttu-id="c0f18-111">È necessario disporre di Azure PowerShell 1.0 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="c0f18-111">You must have Azure PowerShell 1.0 or greater.</span></span> <span data-ttu-id="c0f18-112">Per istruzioni, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c0f18-112">For instructions, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="c0f18-113">In PowerShell è necessario connettersi alla sottoscrizione di Azure come descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="c0f18-113">You must be logged in to your Azure subscription in PowerShell as described below.</span></span>

<span data-ttu-id="c0f18-114">In primo luogo, è necessario accedere a Microsoft Azure con questo comando:</span><span class="sxs-lookup"><span data-stu-id="c0f18-114">First, you must login to Azure with this command:</span></span>

    Login-AzureRmAccount

<span data-ttu-id="c0f18-115">Specificare l'indirizzo e-mail del proprio account Microsoft Azure e la relativa password nella finestra di dialogo di accesso a Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c0f18-115">Specify the email address of your Azure account and its password in the Microsoft Azure login dialog.</span></span>

<span data-ttu-id="c0f18-116">In alternativa è possibile [accedere in modo non interattivo con un'entità servizio](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="c0f18-116">Alternatively you can [login non-interactively with a service principal](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="c0f18-117">Se sono disponibili più sottoscrizioni di Azure, è necessario impostare la sottoscrizione di Azure in uso.</span><span class="sxs-lookup"><span data-stu-id="c0f18-117">If you have multiple Azure subscriptions, you need to set your Azure subscription.</span></span> <span data-ttu-id="c0f18-118">Per visualizzare un elenco di sottoscrizioni correnti, eseguire questo comando.</span><span class="sxs-lookup"><span data-stu-id="c0f18-118">To see a list of your current subscriptions, run this command.</span></span>

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="c0f18-119">Per specificare la sottoscrizione, eseguire il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="c0f18-119">To specify the subscription, run the following command.</span></span> <span data-ttu-id="c0f18-120">Nell'esempio seguente, il nome della sottoscrizione è `ContosoSubscription`.</span><span class="sxs-lookup"><span data-stu-id="c0f18-120">In the following example, the subscription name is `ContosoSubscription`.</span></span>

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

## <a name="commands-to-help-you-get-started"></a><span data-ttu-id="c0f18-121">Comandi utili per iniziare</span><span class="sxs-lookup"><span data-stu-id="c0f18-121">Commands to help you get started</span></span>
    $serviceName = "your-service-name-lowercase-with-dashes"
    $sku = "free" # or "basic" or "standard" for paid services
    $location = "West US"
    # You can get a list of potential locations with
    # (Get-AzureRmResourceProvider -ListAvailable | Where-Object {$_.ProviderNamespace -eq 'Microsoft.Search'}).Locations
    $resourceGroupName = "YourResourceGroup" 
    # If you don't already have this resource group, you can create it with 
    # New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Register the ARM provider idempotently. This must be done once per subscription
    Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Search"

    # Create a new search service
    # This command will return once the service is fully created
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

    # Get the primary admin API key
    $primaryKey = (Invoke-AzureRmResourceAction `
        -Action listAdminKeys `
        -ResourceId $resource.ResourceId `
        -ApiVersion 2015-08-19).PrimaryKey

    # Regenerate the secondary admin API Key
    $secondaryKey = (Invoke-AzureRmResourceAction `
        -ResourceType "Microsoft.Search/searchServices/regenerateAdminKey" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19 `
        -Action secondary).SecondaryKey

    # Create a query key for read only access to your indexes
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
    # This command will not return until the operation is finished
    # It can take 15 minutes or more to provision the additional resources
    $resource.Properties.ReplicaCount = 2
    $resource | Set-AzureRmResource

    # Delete your service
    # Deleting your service will delete all indexes and data in the service
    $resource | Remove-AzureRmResource

## <a name="next-steps"></a><span data-ttu-id="c0f18-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c0f18-122">Next Steps</span></span>
<span data-ttu-id="c0f18-123">Dopo aver creato il servizio, è possibile procedere a compilare un [indice](search-what-is-an-index.md), eseguire [query su un indice](search-query-overview.md) e infine creare e gestire la propria applicazione di ricerca che usa Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="c0f18-123">Now that your service is created, you can take the next steps: build an [index](search-what-is-an-index.md), [query an index](search-query-overview.md), and finally create and manage your own search application that uses Azure Search.</span></span>

* [<span data-ttu-id="c0f18-124">Creare un indice di Ricerca di Azure nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c0f18-124">Create an Azure Search index in the Azure portal</span></span>](search-create-index-portal.md)
* [<span data-ttu-id="c0f18-125">Eseguire query in un indice di Ricerca di Azure con Esplora ricerche nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c0f18-125">Query an Azure Search index using Search Explorer in the Azure portal</span></span>](search-explorer.md)
* [<span data-ttu-id="c0f18-126">Installare un indicizzatore per caricare dati da altri servizi</span><span class="sxs-lookup"><span data-stu-id="c0f18-126">Setup an indexer to load data from other services</span></span>](search-indexer-overview.md)
* [<span data-ttu-id="c0f18-127">Come utilizzare Ricerca di Azure in .NET</span><span class="sxs-lookup"><span data-stu-id="c0f18-127">How to use Azure Search in .NET</span></span>](search-howto-dotnet-sdk.md)
* [<span data-ttu-id="c0f18-128">Analizzare il traffico di Ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="c0f18-128">Analyze your Azure Search traffic</span></span>](search-traffic-analytics.md)

