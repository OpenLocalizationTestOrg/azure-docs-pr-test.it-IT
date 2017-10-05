---
title: 'Automazione di Azure Cosmos DB: gestione con Powershell | Microsoft Docs'
description: Usare Azure Powershell per gestire gli account di Azure Cosmos DB.
services: cosmos-db
author: dmakwana
manager: jhubbard
editor: 
tags: azure-resource-manager
documentationcenter: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: dimakwan
ms.openlocfilehash: 25c543528119410dff0684845a713dcb0d6151d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-cosmos-db-account-using-powershell"></a><span data-ttu-id="d0288-103">Creare un account di Azure Cosmos DB mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="d0288-103">Create an Azure Cosmos DB account using PowerShell</span></span>

<span data-ttu-id="d0288-104">La guida seguente illustra i comandi per automatizzare la gestione degli account del database Azure Cosmos DB usando Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="d0288-104">The following guide describes commands to automate management of your Azure Cosmos DB database accounts using Azure Powershell.</span></span> <span data-ttu-id="d0288-105">Include anche i comandi per gestire le chiavi dell'account e le priorità di failover in [account di database tra più aree][scaling-globally].</span><span class="sxs-lookup"><span data-stu-id="d0288-105">It also includes commands to manage account keys and failover priorities in [multi-region database accounts][scaling-globally].</span></span> <span data-ttu-id="d0288-106">L'aggiornamento dell'account del database consente di modificare i criteri di coerenza e di aggiungere/rimuovere le aree.</span><span class="sxs-lookup"><span data-stu-id="d0288-106">Updating your database account allows you to modify consistency policies and add/remove regions.</span></span> <span data-ttu-id="d0288-107">Per la gestione multipiattaforma dell'account di Azure Cosmos DB, è possibile usare l'[interfaccia della riga di comando di Azure](cli-samples.md), l'[API REST del provider di risorse][rp-rest-api] o il [portale di Azure](create-documentdb-dotnet.md#create-account).</span><span class="sxs-lookup"><span data-stu-id="d0288-107">For cross-platform management of your Azure Cosmos DB account, you can use either [Azure CLI](cli-samples.md), the [Resource Provider REST API][rp-rest-api], or the [Azure portal](create-documentdb-dotnet.md#create-account).</span></span>

## <a name="getting-started"></a><span data-ttu-id="d0288-108">Introduzione</span><span class="sxs-lookup"><span data-stu-id="d0288-108">Getting Started</span></span>

<span data-ttu-id="d0288-109">Seguire le istruzioni in [Come installare e configurare Azure PowerShell][powershell-install-configure] per installare e accedere all'account di Azure Resource Manager in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d0288-109">Follow the instructions in [How to install and configure Azure PowerShell][powershell-install-configure] to install and log in to your Azure Resource Manager account in Powershell.</span></span>

### <a name="notes"></a><span data-ttu-id="d0288-110">Note</span><span class="sxs-lookup"><span data-stu-id="d0288-110">Notes</span></span>

* <span data-ttu-id="d0288-111">Per eseguire i comandi seguenti senza richiedere la conferma dell'utente, aggiungere il flag `-Force` al comando.</span><span class="sxs-lookup"><span data-stu-id="d0288-111">If you would like to execute the following commands without requiring user confirmation, append the `-Force` flag to the command.</span></span>
* <span data-ttu-id="d0288-112">Tutti i comandi seguenti sono sincroni.</span><span class="sxs-lookup"><span data-stu-id="d0288-112">All the following commands are synchronous.</span></span>

## <span data-ttu-id="d0288-113"><a id="create-documentdb-account-powershell"></a> Creare un account di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d0288-113"><a id="create-documentdb-account-powershell"></a> Create an Azure Cosmos DB Account</span></span>

<span data-ttu-id="d0288-114">Questo comando consente di creare un account del database di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d0288-114">This command allows you to create an Azure Cosmos DB database account.</span></span> <span data-ttu-id="d0288-115">Configurare il nuovo account del database come ad area singola o [a più aree][scaling-globally] con un determinato [criterio di coerenza](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="d0288-115">Configure your new database account as either single-region or [multi-region][scaling-globally] with a certain [consistency policy](consistency-levels.md).</span></span>

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name>  -Location "<resource-group-location>" -Name <database-account-name> -Properties $CosmosDBProperties
    
* <span data-ttu-id="d0288-116">`<write-region-location>` Nome della località dell'area di scrittura dell'account del database.</span><span class="sxs-lookup"><span data-stu-id="d0288-116">`<write-region-location>` The location name of the write region of the database account.</span></span> <span data-ttu-id="d0288-117">La località è necessaria per impostare il valore della priorità di failover su 0.</span><span class="sxs-lookup"><span data-stu-id="d0288-117">This location is required to have a failover priority value of 0.</span></span> <span data-ttu-id="d0288-118">Deve essere presente esattamente un'area di scrittura per ogni account di database.</span><span class="sxs-lookup"><span data-stu-id="d0288-118">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="d0288-119">`<read-region-location>` Nome della località dell'area di lettura dell'account del database.</span><span class="sxs-lookup"><span data-stu-id="d0288-119">`<read-region-location>` The location name of the read region of the database account.</span></span> <span data-ttu-id="d0288-120">La località è necessaria per impostare il valore della priorità di failover come maggiore di 0.</span><span class="sxs-lookup"><span data-stu-id="d0288-120">This location is required to have a failover priority value of greater than 0.</span></span> <span data-ttu-id="d0288-121">Possono essere presenti più aree di lettura per ogni account di database.</span><span class="sxs-lookup"><span data-stu-id="d0288-121">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="d0288-122">`<ip-range-filter>` Specifica il set di indirizzi IP e di intervalli di indirizzi IP nel formato CIDR da includere come elenco consentito di IP client per un determinato account di database.</span><span class="sxs-lookup"><span data-stu-id="d0288-122">`<ip-range-filter>` Specifies the set of IP addresses or IP address ranges in CIDR form to be included as the allowed list of client IPs for a given database account.</span></span> <span data-ttu-id="d0288-123">Gli intervalli di indirizzi IP o i singoli indirizzi IP devono essere delimitati da virgole e non devono contenere spazi.</span><span class="sxs-lookup"><span data-stu-id="d0288-123">IP addresses/ranges must be comma separated and must not contain any spaces.</span></span> <span data-ttu-id="d0288-124">Per altre informazioni, vedere [Azure Cosmos DB Firewall Support](firewall-support.md) (Supporto al firewall di Azure Cosmos DB)</span><span class="sxs-lookup"><span data-stu-id="d0288-124">For more information, see [Azure Cosmos DB Firewall Support](firewall-support.md)</span></span>
* <span data-ttu-id="d0288-125">`<default-consistency-level>` Livello di coerenza predefinito dell'account di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d0288-125">`<default-consistency-level>` The default consistency level of the Azure Cosmos DB account.</span></span> <span data-ttu-id="d0288-126">Per altre informazioni, vedere [Livelli di coerenza in Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="d0288-126">For more information, see [Consistency Levels in Azure Cosmos DB](consistency-levels.md).</span></span>
* <span data-ttu-id="d0288-127">`<max-interval>` Quando è usato con il livello di coerenza Decadimento ristretto, questo valore rappresenta l'intervallo di tempo di decadimento (in secondi) tollerato.</span><span class="sxs-lookup"><span data-stu-id="d0288-127">`<max-interval>` When used with Bounded Staleness consistency, this value represents the time amount of staleness (in seconds) tolerated.</span></span> <span data-ttu-id="d0288-128">L'intervallo consentito per questo valore è compreso tra 1 e 100.</span><span class="sxs-lookup"><span data-stu-id="d0288-128">Accepted range for this value is 1 - 100.</span></span>
* <span data-ttu-id="d0288-129">`<max-staleness-prefix>` Quando è usato con il livello di coerenza Decadimento ristretto, questo valore rappresenta il numero di richieste non aggiornate tollerate.</span><span class="sxs-lookup"><span data-stu-id="d0288-129">`<max-staleness-prefix>` When used with Bounded Staleness consistency, this value represents the number of stale requests tolerated.</span></span> <span data-ttu-id="d0288-130">L'intervallo consentito per questo valore è compreso tra 1 e 2.147.483.647.</span><span class="sxs-lookup"><span data-stu-id="d0288-130">Accepted range for this value is 1 – 2,147,483,647.</span></span>
* <span data-ttu-id="d0288-131">`<resource-group-name>` Nome del [gruppo di risorse di Azure][azure-resource-groups] a cui appartiene il nuovo account del database Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d0288-131">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="d0288-132">`<resource-group-location>` Posizione del gruppo di risorse di Azure a cui appartiene il nuovo account del database Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d0288-132">`<resource-group-location>` The location of the Azure Resource Group to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="d0288-133">`<database-account-name>` Nome dell'account del database Azure Cosmos DB da creare.</span><span class="sxs-lookup"><span data-stu-id="d0288-133">`<database-account-name>` The name of the Azure Cosmos DB database account to be created.</span></span> <span data-ttu-id="d0288-134">Può contenere solo lettere minuscole, numeri, il carattere "-" e deve essere compreso fra 3 e 50 caratteri.</span><span class="sxs-lookup"><span data-stu-id="d0288-134">It can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters.</span></span>

<span data-ttu-id="d0288-135">Esempio:</span><span class="sxs-lookup"><span data-stu-id="d0288-135">Example:</span></span> 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Location "West US" -Name "docdb-test" -Properties $CosmosDBProperties

### <a name="notes"></a><span data-ttu-id="d0288-136">Note</span><span class="sxs-lookup"><span data-stu-id="d0288-136">Notes</span></span>
* <span data-ttu-id="d0288-137">L'esempio precedente crea un account di database con due aree.</span><span class="sxs-lookup"><span data-stu-id="d0288-137">The preceding example creates a database account with two regions.</span></span> <span data-ttu-id="d0288-138">È anche possibile creare un account di database con un'area (designata come area di scrittura con un valore di priorità di failover pari a 0) o con più di due aree.</span><span class="sxs-lookup"><span data-stu-id="d0288-138">It is also possible to create a database account with either one region (which is designated as the write region and have a failover priority value of 0) or more than two regions.</span></span> <span data-ttu-id="d0288-139">Per altre informazioni, vedere gli [account di database tra più aree][scaling-globally].</span><span class="sxs-lookup"><span data-stu-id="d0288-139">For more information, see [multi-region database accounts][scaling-globally].</span></span>
* <span data-ttu-id="d0288-140">Le località devono essere aree in cui Azure Cosmos DB è disponibile a livello generale.</span><span class="sxs-lookup"><span data-stu-id="d0288-140">The locations must be regions in which Azure Cosmos DB is generally available.</span></span> <span data-ttu-id="d0288-141">L'elenco corrente delle aree geografiche è disponibile nella [pagina Aree di Azure](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="d0288-141">The current list of regions is provided on the [Azure Regions page](https://azure.microsoft.com/regions/#services).</span></span>

## <span data-ttu-id="d0288-142"><a id="update-documentdb-account-powershell"> </a> Aggiornare un account di database DocumentDB</span><span class="sxs-lookup"><span data-stu-id="d0288-142"><a id="update-documentdb-account-powershell"></a> Update a DocumentDB Database Account</span></span>

<span data-ttu-id="d0288-143">Questo comando consente di aggiornare le proprietà di un account del database Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d0288-143">This command allows you to update your Azure Cosmos DB database account properties.</span></span> <span data-ttu-id="d0288-144">e include il criterio di coerenza e le località in cui esiste l'account di database.</span><span class="sxs-lookup"><span data-stu-id="d0288-144">This includes the consistency policy and the locations which the database account exists in.</span></span>

> [!NOTE]
> <span data-ttu-id="d0288-145">Il comando consente di aggiungere e rimuovere aree, ma non di modificare le priorità di failover.</span><span class="sxs-lookup"><span data-stu-id="d0288-145">This command allows you to add and remove regions but does not allow you to modify failover priorities.</span></span> <span data-ttu-id="d0288-146">Per modificare le priorità di failover, vedere [sotto](#modify-failover-priority-powershell).</span><span class="sxs-lookup"><span data-stu-id="d0288-146">To modify failover priorities, see [below](#modify-failover-priority-powershell).</span></span>

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name> -Name <database-account-name> -Properties $CosmosDBProperties
    
* <span data-ttu-id="d0288-147">`<write-region-location>` Nome della località dell'area di scrittura dell'account del database.</span><span class="sxs-lookup"><span data-stu-id="d0288-147">`<write-region-location>` The location name of the write region of the database account.</span></span> <span data-ttu-id="d0288-148">La località è necessaria per impostare il valore della priorità di failover su 0.</span><span class="sxs-lookup"><span data-stu-id="d0288-148">This location is required to have a failover priority value of 0.</span></span> <span data-ttu-id="d0288-149">Deve essere presente esattamente un'area di scrittura per ogni account di database.</span><span class="sxs-lookup"><span data-stu-id="d0288-149">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="d0288-150">`<read-region-location>` Nome della località dell'area di lettura dell'account del database.</span><span class="sxs-lookup"><span data-stu-id="d0288-150">`<read-region-location>` The location name of the read region of the database account.</span></span> <span data-ttu-id="d0288-151">La località è necessaria per impostare il valore della priorità di failover come maggiore di 0.</span><span class="sxs-lookup"><span data-stu-id="d0288-151">This location is required to have a failover priority value of greater than 0.</span></span> <span data-ttu-id="d0288-152">Possono essere presenti più aree di lettura per ogni account di database.</span><span class="sxs-lookup"><span data-stu-id="d0288-152">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="d0288-153">`<default-consistency-level>` Livello di coerenza predefinito dell'account di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d0288-153">`<default-consistency-level>` The default consistency level of the Azure Cosmos DB account.</span></span> <span data-ttu-id="d0288-154">Per altre informazioni, vedere [Livelli di coerenza in Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="d0288-154">For more information, see [Consistency Levels in Azure Cosmos DB](consistency-levels.md).</span></span>
* <span data-ttu-id="d0288-155">`<ip-range-filter>` Specifica il set di indirizzi IP e di intervalli di indirizzi IP nel formato CIDR da includere come elenco consentito di IP client per un determinato account di database.</span><span class="sxs-lookup"><span data-stu-id="d0288-155">`<ip-range-filter>` Specifies the set of IP addresses or IP address ranges in CIDR form to be included as the allowed list of client IPs for a given database account.</span></span> <span data-ttu-id="d0288-156">Gli intervalli di indirizzi IP o i singoli indirizzi IP devono essere delimitati da virgole e non devono contenere spazi.</span><span class="sxs-lookup"><span data-stu-id="d0288-156">IP addresses/ranges must be comma separated and must not contain any spaces.</span></span> <span data-ttu-id="d0288-157">Per altre informazioni, vedere [Azure Cosmos DB Firewall Support](firewall-support.md) (Supporto al firewall di Azure Cosmos DB)</span><span class="sxs-lookup"><span data-stu-id="d0288-157">For more information, see [Azure Cosmos DB Firewall Support](firewall-support.md)</span></span>
* <span data-ttu-id="d0288-158">`<max-interval>` Quando è usato con il livello di coerenza Decadimento ristretto, questo valore rappresenta l'intervallo di tempo di decadimento (in secondi) tollerato.</span><span class="sxs-lookup"><span data-stu-id="d0288-158">`<max-interval>` When used with Bounded Staleness consistency, this value represents the time amount of staleness (in seconds) tolerated.</span></span> <span data-ttu-id="d0288-159">L'intervallo consentito per questo valore è compreso tra 1 e 100.</span><span class="sxs-lookup"><span data-stu-id="d0288-159">Accepted range for this value is 1 - 100.</span></span>
* <span data-ttu-id="d0288-160">`<max-staleness-prefix>` Quando è usato con il livello di coerenza Decadimento ristretto, questo valore rappresenta il numero di richieste non aggiornate tollerate.</span><span class="sxs-lookup"><span data-stu-id="d0288-160">`<max-staleness-prefix>` When used with Bounded Staleness consistency, this value represents the number of stale requests tolerated.</span></span> <span data-ttu-id="d0288-161">L'intervallo consentito per questo valore è compreso tra 1 e 2.147.483.647.</span><span class="sxs-lookup"><span data-stu-id="d0288-161">Accepted range for this value is 1 – 2,147,483,647.</span></span>
* <span data-ttu-id="d0288-162">`<resource-group-name>` Nome del [gruppo di risorse di Azure][azure-resource-groups] a cui appartiene il nuovo account del database Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d0288-162">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="d0288-163">`<resource-group-location>` Posizione del gruppo di risorse di Azure a cui appartiene il nuovo account del database Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d0288-163">`<resource-group-location>` The location of the Azure Resource Group to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="d0288-164">`<database-account-name>` Nome dell'account del database Azure Cosmos DB da aggiornare.</span><span class="sxs-lookup"><span data-stu-id="d0288-164">`<database-account-name>` The name of the Azure Cosmos DB database account to be updated.</span></span>

<span data-ttu-id="d0288-165">Esempio:</span><span class="sxs-lookup"><span data-stu-id="d0288-165">Example:</span></span> 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Properties $CosmosDBProperties

## <span data-ttu-id="d0288-166"><a id="delete-documentdb-account-powershell"></a> Eliminare un account di database DocumentDB</span><span class="sxs-lookup"><span data-stu-id="d0288-166"><a id="delete-documentdb-account-powershell"></a> Delete a DocumentDB Database Account</span></span>

<span data-ttu-id="d0288-167">Questo comando consente di eliminare un account del database Azure Cosmos DB esistente.</span><span class="sxs-lookup"><span data-stu-id="d0288-167">This command allows you to delete an existing Azure Cosmos DB database account.</span></span>

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"
    
* <span data-ttu-id="d0288-168">`<resource-group-name>` Nome del [gruppo di risorse di Azure][azure-resource-groups] a cui appartiene il nuovo account del database Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d0288-168">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="d0288-169">`<database-account-name>` Nome dell'account del database Azure Cosmos DB da eliminare.</span><span class="sxs-lookup"><span data-stu-id="d0288-169">`<database-account-name>` The name of the Azure Cosmos DB database account to be deleted.</span></span>

<span data-ttu-id="d0288-170">Esempio:</span><span class="sxs-lookup"><span data-stu-id="d0288-170">Example:</span></span>

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="d0288-171"><a id="get-documentdb-properties-powershell"></a> Ottenere le proprietà di un account di database DocumentDB</span><span class="sxs-lookup"><span data-stu-id="d0288-171"><a id="get-documentdb-properties-powershell"></a> Get Properties of a DocumentDB Database Account</span></span>

<span data-ttu-id="d0288-172">Questo comando consente di ottenere le proprietà di un account del database Azure Cosmos DB esistente.</span><span class="sxs-lookup"><span data-stu-id="d0288-172">This command allows you to get the properties of an existing Azure Cosmos DB database account.</span></span>

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="d0288-173">`<resource-group-name>` Nome del [gruppo di risorse di Azure][azure-resource-groups] a cui appartiene il nuovo account del database Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d0288-173">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="d0288-174">`<database-account-name>` Nome dell'account del database Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d0288-174">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>

<span data-ttu-id="d0288-175">Esempio:</span><span class="sxs-lookup"><span data-stu-id="d0288-175">Example:</span></span>

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="d0288-176"><a id="update-tags-powershell"></a> Tag di aggiornamento dell'account del database Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d0288-176"><a id="update-tags-powershell"></a> Update Tags of an Azure Cosmos DB Database Account</span></span>

<span data-ttu-id="d0288-177">L'esempio seguente illustra come impostare i [tag delle risorse di Azure][azure-resource-tags] per l'account del database Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d0288-177">The following example describes how to set [Azure resource tags][azure-resource-tags] for your Azure Cosmos DB database account.</span></span>

> [!NOTE]
> <span data-ttu-id="d0288-178">Questo comando può essere combinato con i comandi di creazione o aggiornamento aggiungendo il flag `-Tags` con il parametro corrispondente.</span><span class="sxs-lookup"><span data-stu-id="d0288-178">This command can be combined with the create or update commands by appending the `-Tags` flag with the corresponding parameter.</span></span>

<span data-ttu-id="d0288-179">Esempio:</span><span class="sxs-lookup"><span data-stu-id="d0288-179">Example:</span></span>

    $tags = @{"dept" = "Finance”; environment = “Production”}
    Set-AzureRmResource -ResourceType “Microsoft.DocumentDB/databaseAccounts”  -ResourceGroupName "rg-test" -Name "docdb-test" -Tags $tags

## <span data-ttu-id="d0288-180"><a id="list-account-keys-powershell"></a> Elencare le chiavi dell'account</span><span class="sxs-lookup"><span data-stu-id="d0288-180"><a id="list-account-keys-powershell"></a> List Account Keys</span></span>

<span data-ttu-id="d0288-181">Quando si crea un account Azure Cosmos DB, il servizio genera due chiavi di accesso principali che possono essere usate per l'autenticazione quando si accede all'account di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d0288-181">When you create an Azure Cosmos DB account, the service generates two master access keys that can be used for authentication when the Azure Cosmos DB account is accessed.</span></span> <span data-ttu-id="d0288-182">Generando due chiavi di accesso, Azure Cosmos DB consente di rigenerare le chiavi senza interruzioni dell'account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d0288-182">By providing two access keys, Azure Cosmos DB enables you to regenerate the keys with no interruption to your Azure Cosmos DB account.</span></span> <span data-ttu-id="d0288-183">Sono disponibili anche chiavi di sola lettura per l'autenticazione delle operazioni di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="d0288-183">Read-only keys for authenticating read-only operations are also available.</span></span> <span data-ttu-id="d0288-184">Esistono due chiavi di lettura/scrittura (primaria e secondaria) e due chiavi di sola lettura (primaria e secondaria).</span><span class="sxs-lookup"><span data-stu-id="d0288-184">There are two read-write keys (primary and secondary) and two read-only keys (primary and secondary).</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="d0288-185">`<resource-group-name>` Nome del [gruppo di risorse di Azure][azure-resource-groups] a cui appartiene il nuovo account del database Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d0288-185">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="d0288-186">`<database-account-name>` Nome dell'account del database Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d0288-186">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>

<span data-ttu-id="d0288-187">Esempio:</span><span class="sxs-lookup"><span data-stu-id="d0288-187">Example:</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="d0288-188"><a id="list-connection-strings-powershell"></a> Elencare le stringhe di connessione</span><span class="sxs-lookup"><span data-stu-id="d0288-188"><a id="list-connection-strings-powershell"></a> List Connection Strings</span></span>

<span data-ttu-id="d0288-189">Per gli account di MongoDB, è possibile recuperare la stringa di connessione per connettere l'app MongoDB all'account del database usando il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="d0288-189">For MongoDB accounts, the connection string to connect your MongoDB app to the database account can be retrieved using the following command.</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="d0288-190">`<resource-group-name>` Nome del [gruppo di risorse di Azure][azure-resource-groups] a cui appartiene il nuovo account del database Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d0288-190">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="d0288-191">`<database-account-name>` Nome dell'account del database Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d0288-191">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>

<span data-ttu-id="d0288-192">Esempio:</span><span class="sxs-lookup"><span data-stu-id="d0288-192">Example:</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="d0288-193"><a id="regenerate-account-key-powershell"></a> Rigenerare una chiave dell'account</span><span class="sxs-lookup"><span data-stu-id="d0288-193"><a id="regenerate-account-key-powershell"></a> Regenerate Account Key</span></span>

<span data-ttu-id="d0288-194">È consigliabile modificare periodicamente le chiavi di accesso all'account Azure Cosmos DB per mantenere più sicure le connessioni.</span><span class="sxs-lookup"><span data-stu-id="d0288-194">You should change the access keys to your Azure Cosmos DB account periodically to help keep your connections more secure.</span></span> <span data-ttu-id="d0288-195">Vengono assegnate due chiavi di accesso per consentire di mantenere le connessioni all'account Azure Cosmos DB con una delle due chiavi mentre si rigenera l'altra.</span><span class="sxs-lookup"><span data-stu-id="d0288-195">Two access keys are assigned to enable you to maintain connections to the Azure Cosmos DB account using one access key while you regenerate the other access key.</span></span>

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"keyKind"="<key-kind>"}

* <span data-ttu-id="d0288-196">`<resource-group-name>` Nome del [gruppo di risorse di Azure][azure-resource-groups] a cui appartiene il nuovo account del database Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d0288-196">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="d0288-197">`<database-account-name>` Nome dell'account del database Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d0288-197">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>
* <span data-ttu-id="d0288-198">`<key-kind>` Uno dei quattro tipi di chiavi: ["Primary"|"Secondary"|"PrimaryReadonly"|"SecondaryReadonly"] che si vuole rigenerare.</span><span class="sxs-lookup"><span data-stu-id="d0288-198">`<key-kind>` One of the four types of keys: ["Primary"|"Secondary"|"PrimaryReadonly"|"SecondaryReadonly"] that you would like to regenerate.</span></span>

<span data-ttu-id="d0288-199">Esempio:</span><span class="sxs-lookup"><span data-stu-id="d0288-199">Example:</span></span>

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"keyKind"="Primary"}

## <span data-ttu-id="d0288-200"><a id="modify-failover-priority-powershell"></a> Modificare la priorità di failover di un account del database Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d0288-200"><a id="modify-failover-priority-powershell"></a> Modify Failover Priority of an Azure Cosmos DB Database Account</span></span>

<span data-ttu-id="d0288-201">Per gli account del database tra più aree, è possibile modificare la priorità di failover delle diverse aree in cui esiste l'account del database Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d0288-201">For multi-region database accounts, you can change the failover priority of the various regions which the Azure Cosmos DB database account exists in.</span></span> <span data-ttu-id="d0288-202">Per altre informazioni sul failover nell'account del database Azure Cosmos DB, vedere [Distribuire i dati a livello globale con Azure Cosmos DB][distribute-data-globally].</span><span class="sxs-lookup"><span data-stu-id="d0288-202">For more information on failover in your Azure Cosmos DB database account, see [Distribute data globally with Azure Cosmos DB][distribute-data-globally].</span></span>

    $failoverPolicies = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0},@{"locationName"="<read-region-location>"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"failoverPolicies"=$failoverPolicies}

* <span data-ttu-id="d0288-203">`<write-region-location>` Nome della località dell'area di scrittura dell'account del database.</span><span class="sxs-lookup"><span data-stu-id="d0288-203">`<write-region-location>` The location name of the write region of the database account.</span></span> <span data-ttu-id="d0288-204">La località è necessaria per impostare il valore della priorità di failover su 0.</span><span class="sxs-lookup"><span data-stu-id="d0288-204">This location is required to have a failover priority value of 0.</span></span> <span data-ttu-id="d0288-205">Deve essere presente esattamente un'area di scrittura per ogni account di database.</span><span class="sxs-lookup"><span data-stu-id="d0288-205">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="d0288-206">`<read-region-location>` Nome della località dell'area di lettura dell'account del database.</span><span class="sxs-lookup"><span data-stu-id="d0288-206">`<read-region-location>` The location name of the read region of the database account.</span></span> <span data-ttu-id="d0288-207">La località è necessaria per impostare il valore della priorità di failover come maggiore di 0.</span><span class="sxs-lookup"><span data-stu-id="d0288-207">This location is required to have a failover priority value of greater than 0.</span></span> <span data-ttu-id="d0288-208">Possono essere presenti più aree di lettura per ogni account di database.</span><span class="sxs-lookup"><span data-stu-id="d0288-208">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="d0288-209">`<resource-group-name>` Nome del [gruppo di risorse di Azure][azure-resource-groups] a cui appartiene il nuovo account del database Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d0288-209">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="d0288-210">`<database-account-name>` Nome dell'account del database Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d0288-210">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>

<span data-ttu-id="d0288-211">Esempio:</span><span class="sxs-lookup"><span data-stu-id="d0288-211">Example:</span></span>

    $failoverPolicies = @(@{"locationName"="East US"; "failoverPriority"=0},@{"locationName"="West US"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"failoverPolicies"=$failoverPolicies}

## <a name="next-steps"></a><span data-ttu-id="d0288-212">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d0288-212">Next steps</span></span>

* <span data-ttu-id="d0288-213">Per connettersi usando .NET, vedere [Connettersi ed eseguire query con .NET](create-documentdb-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="d0288-213">To connect using .NET, see [Connect and query with .NET](create-documentdb-dotnet.md).</span></span>
* <span data-ttu-id="d0288-214">Per connettersi usando .NET Core, vedere [Connettersi ed eseguire query con .NET Core](create-documentdb-dotnet-core.md).</span><span class="sxs-lookup"><span data-stu-id="d0288-214">To connect using .NET Core, see [Connect and query with .NET Core](create-documentdb-dotnet-core.md).</span></span>
* <span data-ttu-id="d0288-215">Per connettersi usando Node.js, vedere [Connettersi ed eseguire query con Node.js e un'app MongoDB](create-mongodb-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="d0288-215">To connect using Node.js, see [Connect and query with Node.js and a MongoDB app](create-mongodb-nodejs.md).</span></span>

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[powershell-install-configure]: https://docs.microsoft.com/azure/powershell-install-configure
[scaling-globally]: distribute-data-globally.md#EnableGlobalDistribution
[distribute-data-globally]: distribute-data-globally.md
[azure-resource-groups]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups
[azure-resource-tags]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags
[rp-rest-api]: https://docs.microsoft.com/rest/api/documentdbresourceprovider/
