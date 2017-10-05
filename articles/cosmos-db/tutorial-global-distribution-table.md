---
title: Esercitazione sulla distribuzione globale in Azure Cosmos DB per l'API Table | Documentazione Microsoft
description: Informazioni su come configurare la distribuzione globale in Azure Cosmos DB usando l'API Table.
services: cosmos-db
keywords: Distribuzione globale, Table
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 63c9e530a4982e2e6e478fea56e015fc77851e1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-table-api"></a><span data-ttu-id="4c6a0-104">Procedura di configurazione della distribuzione globale in Azure Cosmos DB usando l'API Table</span><span class="sxs-lookup"><span data-stu-id="4c6a0-104">How to setup Azure Cosmos DB global distribution using the Table API</span></span>

<span data-ttu-id="4c6a0-105">Questo articolo illustra come usare il portale di Azure per configurare la distribuzione globale in Azure Cosmos DB e quindi connettersi tramite l'API Table (anteprima).</span><span class="sxs-lookup"><span data-stu-id="4c6a0-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the Table API (preview).</span></span>

<span data-ttu-id="4c6a0-106">Questo articolo illustra le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="4c6a0-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="4c6a0-107">Configurare la distribuzione globale tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="4c6a0-107">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="4c6a0-108">Configurare la distribuzione globale tramite l'[API Table](table-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="4c6a0-108">Configure global distribution using the [Table API](table-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-to-a-preferred-region-using-the-table-api"></a><span data-ttu-id="4c6a0-109">Connessione a un'area preferita tramite l'API Table</span><span class="sxs-lookup"><span data-stu-id="4c6a0-109">Connecting to a preferred region using the Table API</span></span>

<span data-ttu-id="4c6a0-110">Per sfruttare la [distribuzione globale](distribute-data-globally.md), le applicazioni client possono specificare un elenco di aree, nell'ordine preferito, da usare per eseguire operazioni sui documenti.</span><span class="sxs-lookup"><span data-stu-id="4c6a0-110">In order to take advantage of [global distribution](distribute-data-globally.md), client applications can specify the ordered preference list of regions to be used to perform document operations.</span></span> <span data-ttu-id="4c6a0-111">Questa operazione può essere eseguita impostando il valore di configurazione `TablePreferredLocations` nella configurazione dell'applicazione per l'anteprima di Azure Storage SDK.</span><span class="sxs-lookup"><span data-stu-id="4c6a0-111">This can be done by setting the `TablePreferredLocations` configuration value in the app config for the preview Azure Storage SDK.</span></span> <span data-ttu-id="4c6a0-112">A seconda della configurazione dell'account Azure Cosmos DB, della disponibilità corrente delle aree e dell'elenco delle preferenze specificato, l'SDK sceglierà l'endpoint ottimale per eseguire le operazioni di scrittura e lettura.</span><span class="sxs-lookup"><span data-stu-id="4c6a0-112">Based on the Azure Cosmos DB account configuration, current regional availability and the preference list specified, the most optimal endpoint will be chosen by the Azure Storage SDK to perform write and read operations.</span></span>

<span data-ttu-id="4c6a0-113">`TablePreferredLocations` deve contenere un elenco delimitato da virgole di percorsi preferiti (multihoming) per le letture.</span><span class="sxs-lookup"><span data-stu-id="4c6a0-113">The `TablePreferredLocations` should contain a comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="4c6a0-114">Ogni istanza del client può specificare un sottoinsieme di queste aree nell'ordine preferito per le letture a bassa latenza.</span><span class="sxs-lookup"><span data-stu-id="4c6a0-114">Each client instance can specify a subset of these regions in the preferred order for low latency reads.</span></span> <span data-ttu-id="4c6a0-115">Le aree devono essere denominate usando i [nomi visualizzati](https://msdn.microsoft.com/library/azure/gg441293.aspx), ad esempio, `West US`.</span><span class="sxs-lookup"><span data-stu-id="4c6a0-115">The regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span>

<span data-ttu-id="4c6a0-116">Tutte le letture verranno inviate alla prima area disponibile nell'elenco `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="4c6a0-116">All reads will be sent to the first available region in the `TablePreferredLocations` list.</span></span> <span data-ttu-id="4c6a0-117">Se la richiesta ha esito negativo, il client trasferisce l'elenco all'area successiva e così via.</span><span class="sxs-lookup"><span data-stu-id="4c6a0-117">If the request fails, the client will fail down the list to the next region, and so on.</span></span>

<span data-ttu-id="4c6a0-118">Gli SDK tenteranno solo di leggere dalle aree specificate nell'elenco `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="4c6a0-118">The SDK will only attempt to read from the regions specified in `TablePreferredLocations`.</span></span> <span data-ttu-id="4c6a0-119">Quindi se l'account di database è disponibile ad esempio in tre aree, ma il client specifica solo due delle aree di non scrittura per `TablePreferredLocations`, le letture non verranno distribuite fuori dall'area di scrittura, anche in caso di failover.</span><span class="sxs-lookup"><span data-stu-id="4c6a0-119">So, for example, if the Database Account is available in three regions, but the client only specifies two of the non-write regions for `TablePreferredLocations`, then no reads will be served out of the write region, even in the case of failover.</span></span>

<span data-ttu-id="4c6a0-120">L'SDK invia automaticamente tutte le scritture all'area di scrittura corrente.</span><span class="sxs-lookup"><span data-stu-id="4c6a0-120">The SDK will automatically send all writes to the current write region.</span></span>

<span data-ttu-id="4c6a0-121">Se la proprietà `TablePreferredLocations` non è impostata, tutte le richieste verranno distribuite dall'area di scrittura corrente.</span><span class="sxs-lookup"><span data-stu-id="4c6a0-121">If the `TablePreferredLocations` property is not set, all requests will be served from the current write region.</span></span>

```xml
    <appSettings>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>           
    </appSettings>
```

<span data-ttu-id="4c6a0-122">L'esercitazione è terminata.</span><span class="sxs-lookup"><span data-stu-id="4c6a0-122">That's it, that completes this tutorial.</span></span> <span data-ttu-id="4c6a0-123">Per informazioni su come gestire la coerenza dell'account con replica globale, vedere [Livelli di coerenza in Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="4c6a0-123">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="4c6a0-124">Per informazioni sul funzionamento della replica di database globale in Azure Cosmos DB, vedere [Distribuire i dati a livello globale con Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="4c6a0-124">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c6a0-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4c6a0-125">Next steps</span></span>

<span data-ttu-id="4c6a0-126">In questa esercitazione sono state eseguite le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="4c6a0-126">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4c6a0-127">Configurare la distribuzione globale tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="4c6a0-127">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="4c6a0-128">Configurare la distribuzione globale tramite le API di DocumentDB</span><span class="sxs-lookup"><span data-stu-id="4c6a0-128">Configure global distribution using the DocumentDB APIs</span></span>

<span data-ttu-id="4c6a0-129">È ora possibile passare all'esercitazione successiva per imparare a sviluppare in locale usando l'emulatore locale di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="4c6a0-129">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4c6a0-130">Sviluppare in locale con l'emulatore</span><span class="sxs-lookup"><span data-stu-id="4c6a0-130">Develop locally with the emulator</span></span>](local-emulator.md)