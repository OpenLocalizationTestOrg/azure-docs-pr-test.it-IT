---
title: Risolvere i problemi di prestazioni e ottimizzare il database | Microsoft Docs
description: Applicare le raccomandazioni sulle prestazioni al database SQL e ottenere informazioni dettagliate sulle prestazioni delle query in esecuzione nel database
metakeywords: azure sql database performance monitoring recommendation
services: sql-database
documentationcenter: 
manager: jhubbard
author: jan-eng
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,monitor & tune
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: janeng
ms.openlocfilehash: f9ae96cdc80c347593f229cb2fce3f2d4d8e7caf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-performance-issues-and-optimize-your-database"></a><span data-ttu-id="eb233-103">Risolvere i problemi di prestazioni e ottimizzare il database</span><span class="sxs-lookup"><span data-stu-id="eb233-103">Troubleshoot performance issues and optimize your database</span></span>

<span data-ttu-id="eb233-104">Spesso le prestazioni non ottimali del database sono dovute a indici mancanti e query non ottimizzate correttamente.</span><span class="sxs-lookup"><span data-stu-id="eb233-104">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="eb233-105">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="eb233-105">In this tutorial you learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="eb233-106">Esaminare, applicare e ripristinare le raccomandazioni per migliorare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="eb233-106">Review, apply and revert performance improvement recommendations</span></span>
> * <span data-ttu-id="eb233-107">Trovare query con un utilizzo elevato delle risorse.</span><span class="sxs-lookup"><span data-stu-id="eb233-107">Find queries with high resource utilization</span></span>
> * <span data-ttu-id="eb233-108">Trovare query con esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="eb233-108">Find long running queries</span></span>

> <span data-ttu-id="eb233-109">Per ricevere una raccomandazione, è necessario un carico di lavoro continuo in un database con problemi di prestazioni, ad esempio a causa di un indice mancante.</span><span class="sxs-lookup"><span data-stu-id="eb233-109">You need a continuous workload on a database with performance issues – missing an index for example to receive a recommendation.</span></span>
>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="eb233-110">Accedere al Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="eb233-110">Log in to the Azure portal</span></span>

<span data-ttu-id="eb233-111">Accedere al [Portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="eb233-111">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="review-and-apply-a-recommendation"></a><span data-ttu-id="eb233-112">Esaminare e applicare una raccomandazione</span><span class="sxs-lookup"><span data-stu-id="eb233-112">Review and apply a recommendation</span></span>

<span data-ttu-id="eb233-113">Per applicare una raccomandazione del sistema per il database, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="eb233-113">Follow these steps to apply a recommendation from the system for your database:</span></span>

1. <span data-ttu-id="eb233-114">Fare clic sul menu **Raccomandazioni per le prestazioni** nel pannello del database.</span><span class="sxs-lookup"><span data-stu-id="eb233-114">Click the **Performance recommendations** menu in the database blade.</span></span>

    ![Raccomandazioni per le prestazioni](./media/sql-database-performance-tutorial/perf_recommendations.png)

2. <span data-ttu-id="eb233-116">Selezionare una raccomandazione attiva dall'elenco delle raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="eb233-116">From the list of recommendations, select an active recommendation.</span></span> <span data-ttu-id="eb233-117">In questo esempio si sceglie Crea indice.</span><span class="sxs-lookup"><span data-stu-id="eb233-117">In this example, Create Index.</span></span>

    ![Selezionare una raccomandazione](./media/sql-database-performance-tutorial/create_index.png)

3. <span data-ttu-id="eb233-119">Applicare la raccomandazione facendo clic sul pulsante **Applica**.</span><span class="sxs-lookup"><span data-stu-id="eb233-119">Apply the recommendation by clicking the **Apply** button.</span></span> <span data-ttu-id="eb233-120">Facoltativamente, è possibile esaminare i dettagli della raccomandazione e visualizzare lo script T-SQL da eseguire facendo clic sul pulsante **Visualizza script**.</span><span class="sxs-lookup"><span data-stu-id="eb233-120">Optionally, review the recommendation details and see the T-SQL script to  be executed by clicking on **View Script** button.</span></span>

    ![Applicare una raccomandazione](./media/sql-database-performance-tutorial/apply.png)

4. <span data-ttu-id="eb233-122">[Facoltativo] Abilitare l'ottimizzazione automatica per applicare automaticamente le raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="eb233-122">[Optional] Enable automatic tuning for recommendations to be applied automatically.</span></span>

    ![Ottimizzazione automatica](./media/sql-database-performance-tutorial/auto_tuning.png)

## <a name="revert-a-recommendation"></a><span data-ttu-id="eb233-124">Ripristinare una raccomandazione</span><span class="sxs-lookup"><span data-stu-id="eb233-124">Revert a recommendation</span></span>

<span data-ttu-id="eb233-125">Advisor per database monitora tutte le raccomandazioni implementate.</span><span class="sxs-lookup"><span data-stu-id="eb233-125">The Database Advisor monitors every recommendation implemented.</span></span> <span data-ttu-id="eb233-126">Se una raccomandazione non migliora il carico di lavoro, viene ripristinata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="eb233-126">If a recommendation doesn't improve the workload it will be automatically reverted.</span></span> <span data-ttu-id="eb233-127">Il ripristino manualmente di una raccomandazione è possibile, ma nella maggior parte dei casi non è necessario.</span><span class="sxs-lookup"><span data-stu-id="eb233-127">Manually reverting a recommendation is possible, but not necessary in most cases.</span></span> <span data-ttu-id="eb233-128">Per ripristinare una raccomandazione:</span><span class="sxs-lookup"><span data-stu-id="eb233-128">To revert a recommendation:</span></span>

1. <span data-ttu-id="eb233-129">Passare al menu Raccomandazioni per le prestazioni e selezionare una delle raccomandazioni applicate.</span><span class="sxs-lookup"><span data-stu-id="eb233-129">Go to the performance recommendations menu and select one of the applied recommendations.</span></span>

    ![Selezionare una raccomandazione](./media/sql-database-performance-tutorial/select.png)

2. <span data-ttu-id="eb233-131">Nella visualizzazione dettagli, fare clic su **Ripristina**.</span><span class="sxs-lookup"><span data-stu-id="eb233-131">In the details view, click **Revert**.</span></span>

    ![Ripristinare una raccomandazione](./media/sql-database-performance-tutorial/revert.png)

## <a name="find-the-query-that-consumes-the-most-resources"></a><span data-ttu-id="eb233-133">Trovare la query con l'utilizzo di risorse più elevato</span><span class="sxs-lookup"><span data-stu-id="eb233-133">Find the query that consumes the most resources</span></span>

<span data-ttu-id="eb233-134">Per trovare la query con l'utilizzo di risorse più elevato, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="eb233-134">Follow these steps to find the query consuming the most resources:</span></span>

1. <span data-ttu-id="eb233-135">Fare clic sul menu **Informazioni dettagliate prestazioni query** nel pannello del database.</span><span class="sxs-lookup"><span data-stu-id="eb233-135">Click on the **Query Performance Insight** menu in the database blade.</span></span>

    ![Informazioni dettagliate query](./media/sql-database-performance-tutorial/query_perf_insights.png)

2. <span data-ttu-id="eb233-137">Selezionare un tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="eb233-137">Select a resource type.</span></span>

    ![Informazioni dettagliate query](./media/sql-database-performance-tutorial/select_resource_type.png)

3. <span data-ttu-id="eb233-139">Selezionare la prima query nella tabella.</span><span class="sxs-lookup"><span data-stu-id="eb233-139">Select the first query in the table.</span></span>

    ![Informazioni dettagliate query](./media/sql-database-performance-tutorial/select_query.png)

4. <span data-ttu-id="eb233-141">Esaminare i dettagli della query.</span><span class="sxs-lookup"><span data-stu-id="eb233-141">Review the query details.</span></span>

    ![Informazioni dettagliate query](./media/sql-database-performance-tutorial/query_details.png)

## <a name="find-the-longest-running-query"></a><span data-ttu-id="eb233-143">Trovare la query in esecuzione da più tempo</span><span class="sxs-lookup"><span data-stu-id="eb233-143">Find the longest running query</span></span>

1. <span data-ttu-id="eb233-144">Passare a Informazioni dettagliate prestazioni query e selezionare la scheda **Query a esecuzione prolungata**.</span><span class="sxs-lookup"><span data-stu-id="eb233-144">Go to Query Performance Insight and select the **Long running queries** tab.</span></span>

    ![Informazioni dettagliate query](./media/sql-database-performance-tutorial/long_running.png)

3. <span data-ttu-id="eb233-146">Selezionare la prima query nella tabella.</span><span class="sxs-lookup"><span data-stu-id="eb233-146">Select the first query in the table.</span></span>

    ![Informazioni dettagliate query](./media/sql-database-performance-tutorial/select_first_query.png)

4. <span data-ttu-id="eb233-148">Esaminare i dettagli della query.</span><span class="sxs-lookup"><span data-stu-id="eb233-148">Review the query details.</span></span>

    ![Informazioni dettagliate query](./media/sql-database-performance-tutorial/review_query_details.png)



## <a name="next-steps"></a><span data-ttu-id="eb233-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="eb233-150">Next steps</span></span> 
<span data-ttu-id="eb233-151">Spesso le prestazioni non ottimali del database sono dovute a indici mancanti e query non ottimizzate correttamente.</span><span class="sxs-lookup"><span data-stu-id="eb233-151">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="eb233-152">Questa esercitazione illustra come:</span><span class="sxs-lookup"><span data-stu-id="eb233-152">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="eb233-153">Esaminare, applicare e ripristinare le raccomandazioni per migliorare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="eb233-153">Review, apply and revert performance improvement recommendations</span></span>
> * <span data-ttu-id="eb233-154">Trovare query con un utilizzo elevato delle risorse.</span><span class="sxs-lookup"><span data-stu-id="eb233-154">Find queries with high resource utilization</span></span>
> * <span data-ttu-id="eb233-155">Trovare query con esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="eb233-155">Find long running queries</span></span>

[<span data-ttu-id="eb233-156">Suggerimenti sull'ottimizzazione delle prestazioni del database SQL</span><span class="sxs-lookup"><span data-stu-id="eb233-156">SQL Database performance tuning tips</span></span>](https://docs.microsoft.com/azure/sql-database/sql-database-troubleshoot-performance)
