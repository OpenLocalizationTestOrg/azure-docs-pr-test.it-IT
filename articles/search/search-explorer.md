---
title: aaa "Query di un indice (portale - ricerca di Azure) | Documenti di Microsoft"
description: Eseguire una query di ricerca in soluzioni di ricerca del portale di Azure hello.
services: search
manager: jhubbard
documentationcenter: 
author: ashmaka
ms.assetid: 8e524188-73a7-44db-9e64-ae8bf66b05d3
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 07/10/2017
ms.author: ashmaka
ms.openlocfilehash: 56bab3ef8a66eeb053fbbeb6d322acb6824fb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="query-an-azure-search-index-using-search-explorer-in-hello-azure-portal"></a><span data-ttu-id="28764-103">Query di un indice di ricerca di Azure utilizzando Esplora ricerche in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="28764-103">Query an Azure Search index using Search Explorer in hello Azure Portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="28764-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="28764-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="28764-105">Portale</span><span class="sxs-lookup"><span data-stu-id="28764-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="28764-106">.NET</span><span class="sxs-lookup"><span data-stu-id="28764-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="28764-107">REST</span><span class="sxs-lookup"><span data-stu-id="28764-107">REST</span></span>](search-query-rest-api.md)
> 
> 

<span data-ttu-id="28764-108">Questo articolo viene illustrato come un indice utilizzando una ricerca di Azure tooquery **Esplora ricerche** in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="28764-108">This article shows you how tooquery an Azure Search index using **Search Explorer** in hello Azure portal.</span></span> <span data-ttu-id="28764-109">È possibile usare Esplora ricerche toosubmit semplice o completo Lucene query stringhe tooany indice esistente nel servizio.</span><span class="sxs-lookup"><span data-stu-id="28764-109">You can use Search Explorer toosubmit simple or full Lucene query strings tooany existing index in your service.</span></span>

## <a name="open-hello-service-dashboard"></a><span data-ttu-id="28764-110">Dashboard del servizio aprire hello</span><span class="sxs-lookup"><span data-stu-id="28764-110">Open hello service dashboard</span></span>
1. <span data-ttu-id="28764-111">Fare clic su **tutte le risorse** sulla barra di spostamento hello hello il lato sinistro di hello [portale di Azure](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).</span><span class="sxs-lookup"><span data-stu-id="28764-111">Click **All resources** in hello jump bar on hello left side of hello [Azure portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).</span></span>
2. <span data-ttu-id="28764-112">Selezionare il servizio Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="28764-112">Select your Azure Search service.</span></span>

## <a name="select-an-index"></a><span data-ttu-id="28764-113">Selezionare un indice</span><span class="sxs-lookup"><span data-stu-id="28764-113">Select an index</span></span>

<span data-ttu-id="28764-114">Indice di hello selezionare desideri toosearch da hello **indici** riquadro.</span><span class="sxs-lookup"><span data-stu-id="28764-114">Select hello index you would like toosearch from hello **Indexes** tile.</span></span>

   ![](./media/search-explorer/pick-index.png)

## <a name="open-search-explorer"></a><span data-ttu-id="28764-115">Aprire Esplora ricerche</span><span class="sxs-lookup"><span data-stu-id="28764-115">Open Search Explorer</span></span>

<span data-ttu-id="28764-116">Fare clic sulla barra di ricerca di Esplora ricerche riquadro tooslide hello aprire hello e riquadro risultati.</span><span class="sxs-lookup"><span data-stu-id="28764-116">Click on hello Search Explorer tile tooslide open hello search bar and results pane.</span></span>

   ![](./media/search-explorer/search-explorer-tile.png)

## <a name="start-searching"></a><span data-ttu-id="28764-117">Avviare la ricerca</span><span class="sxs-lookup"><span data-stu-id="28764-117">Start searching</span></span>

<span data-ttu-id="28764-118">Quando si utilizza Esplora ricerche hello, è possibile specificare [parametri di query](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) query hello tooformulate.</span><span class="sxs-lookup"><span data-stu-id="28764-118">When using hello Search Explorer, you can specify [query parameters](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) tooformulate hello query.</span></span>

1. <span data-ttu-id="28764-119">In **Stringa di query** digitare una query e quindi fare clic su **Cerca**.</span><span class="sxs-lookup"><span data-stu-id="28764-119">In **Query string**, type a query and then press **Search**.</span></span> 

   <span data-ttu-id="28764-120">stringa di query Hello viene analizzata automaticamente in richiesta corretto hello URL toosubmit hello Azure API REST di ricerca di una richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="28764-120">hello query string is automatically parsed into hello proper request URL toosubmit a HTTP request against hello Azure Search REST API.</span></span>   
   
   <span data-ttu-id="28764-121">È possibile utilizzare qualsiasi valido semplice o completo Lucene sintassi toocreate hello richiesta di query.</span><span class="sxs-lookup"><span data-stu-id="28764-121">You can use any valid simple or full Lucene query syntax toocreate hello request.</span></span> <span data-ttu-id="28764-122">Hello `*` carattere è ricerca vuoto o non specificato tooan equivalente che restituisce tutti i documenti in nessun ordine particolare.</span><span class="sxs-lookup"><span data-stu-id="28764-122">hello `*` character is equivalent tooan empty or unspecified search that returns all documents in no particular order.</span></span>

2. <span data-ttu-id="28764-123">In **risultati**, risultati della query sono presentati in JSON non elaborati, payload toohello identici restituiti in un corpo della risposta HTTP quando si inviano richieste a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="28764-123">In  **Results**, query results are presented in raw JSON, identical toohello payload returned in an HTTP Response Body when issuing requests programmatically.</span></span>

   ![](./media/search-explorer/search-bar.png)

## <a name="next-steps"></a><span data-ttu-id="28764-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="28764-124">Next steps</span></span>

<span data-ttu-id="28764-125">Hello seguenti risorse fornisce esempi e informazioni sulla sintassi di query aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="28764-125">hello following resources provide additional query syntax information and examples.</span></span>

 + [<span data-ttu-id="28764-126">Sintassi di query semplice</span><span class="sxs-lookup"><span data-stu-id="28764-126">Simple query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) 
 + [<span data-ttu-id="28764-127">Sintassi di query Lucene</span><span class="sxs-lookup"><span data-stu-id="28764-127">Lucene query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) 
 + [<span data-ttu-id="28764-128">Esempi di sintassi di query Lucene</span><span class="sxs-lookup"><span data-stu-id="28764-128">Lucene query syntax examples</span></span>](https://docs.microsoft.com/azure/search/search-query-lucene-examples) 
 + [<span data-ttu-id="28764-129">Sintassi delle espressioni filtro OData</span><span class="sxs-lookup"><span data-stu-id="28764-129">OData Filter expression syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) 