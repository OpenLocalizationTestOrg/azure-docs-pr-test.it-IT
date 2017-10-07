---
title: prestazioni aaaTroubleshoot problemi e ottimizzare il database | Documenti Microsoft
description: "Applicare tooyour indicazioni sulle prestazioni del Database SQL, nonché Cancella come toogain informazioni dettagliate sul hello prestazioni delle query hello in esecuzione nel database"
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
ms.openlocfilehash: e948d30ac74eecf45420d5d77ef55e3c0b6f3f47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-performance-issues-and-optimize-your-database"></a><span data-ttu-id="7ffee-103">Risolvere i problemi di prestazioni e ottimizzare il database</span><span class="sxs-lookup"><span data-stu-id="7ffee-103">Troubleshoot performance issues and optimize your database</span></span>

<span data-ttu-id="7ffee-104">Spesso le prestazioni non ottimali del database sono dovute a indici mancanti e query non ottimizzate correttamente.</span><span class="sxs-lookup"><span data-stu-id="7ffee-104">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="7ffee-105">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="7ffee-105">In this tutorial you learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="7ffee-106">Esaminare, applicare e ripristinare le raccomandazioni per migliorare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="7ffee-106">Review, apply and revert performance improvement recommendations</span></span>
> * <span data-ttu-id="7ffee-107">Trovare query con un utilizzo elevato delle risorse.</span><span class="sxs-lookup"><span data-stu-id="7ffee-107">Find queries with high resource utilization</span></span>
> * <span data-ttu-id="7ffee-108">Trovare query con esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="7ffee-108">Find long running queries</span></span>

> <span data-ttu-id="7ffee-109">È necessario un carico di lavoro continua in un database con problemi di prestazioni: manca un indice, ad esempio tooreceive una raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="7ffee-109">You need a continuous workload on a database with performance issues – missing an index for example tooreceive a recommendation.</span></span>
>

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="7ffee-110">Accedi toohello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="7ffee-110">Log in toohello Azure portal</span></span>

<span data-ttu-id="7ffee-111">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7ffee-111">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="review-and-apply-a-recommendation"></a><span data-ttu-id="7ffee-112">Esaminare e applicare una raccomandazione</span><span class="sxs-lookup"><span data-stu-id="7ffee-112">Review and apply a recommendation</span></span>

<span data-ttu-id="7ffee-113">Seguire questi tooapply passaggi raccomandazione dal sistema hello per il database:</span><span class="sxs-lookup"><span data-stu-id="7ffee-113">Follow these steps tooapply a recommendation from hello system for your database:</span></span>

1. <span data-ttu-id="7ffee-114">Fare clic su hello **consigli relativi alle prestazioni** menu nel pannello database hello.</span><span class="sxs-lookup"><span data-stu-id="7ffee-114">Click hello **Performance recommendations** menu in hello database blade.</span></span>

    ![Raccomandazioni per le prestazioni](./media/sql-database-performance-tutorial/perf_recommendations.png)

2. <span data-ttu-id="7ffee-116">Selezionare un'indicazione active hello elenco di indicazioni.</span><span class="sxs-lookup"><span data-stu-id="7ffee-116">From hello list of recommendations, select an active recommendation.</span></span> <span data-ttu-id="7ffee-117">In questo esempio si sceglie Crea indice.</span><span class="sxs-lookup"><span data-stu-id="7ffee-117">In this example, Create Index.</span></span>

    ![Selezionare una raccomandazione](./media/sql-database-performance-tutorial/create_index.png)

3. <span data-ttu-id="7ffee-119">Applicare la raccomandazione hello facendo hello **applica** pulsante.</span><span class="sxs-lookup"><span data-stu-id="7ffee-119">Apply hello recommendation by clicking hello **Apply** button.</span></span> <span data-ttu-id="7ffee-120">Facoltativamente, rivedere i dettagli sulle raccomandazioni hello e vedere script T-SQL hello troppo essere eseguita facendo clic su **Visualizza Script** pulsante.</span><span class="sxs-lookup"><span data-stu-id="7ffee-120">Optionally, review hello recommendation details and see hello T-SQL script too be executed by clicking on **View Script** button.</span></span>

    ![Applicare una raccomandazione](./media/sql-database-performance-tutorial/apply.png)

4. <span data-ttu-id="7ffee-122">[Facoltativo] Abilitare l'ottimizzazione automatica per indicazioni toobe applicati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="7ffee-122">[Optional] Enable automatic tuning for recommendations toobe applied automatically.</span></span>

    ![Ottimizzazione automatica](./media/sql-database-performance-tutorial/auto_tuning.png)

## <a name="revert-a-recommendation"></a><span data-ttu-id="7ffee-124">Ripristinare una raccomandazione</span><span class="sxs-lookup"><span data-stu-id="7ffee-124">Revert a recommendation</span></span>

<span data-ttu-id="7ffee-125">Hello guidata Database consente di monitorare ogni raccomandazione implementato.</span><span class="sxs-lookup"><span data-stu-id="7ffee-125">hello Database Advisor monitors every recommendation implemented.</span></span> <span data-ttu-id="7ffee-126">Se una raccomandazione non migliora il carico di lavoro di hello verrà ripristinato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="7ffee-126">If a recommendation doesn't improve hello workload it will be automatically reverted.</span></span> <span data-ttu-id="7ffee-127">Il ripristino manualmente di una raccomandazione è possibile, ma nella maggior parte dei casi non è necessario.</span><span class="sxs-lookup"><span data-stu-id="7ffee-127">Manually reverting a recommendation is possible, but not necessary in most cases.</span></span> <span data-ttu-id="7ffee-128">toorevert un'indicazione:</span><span class="sxs-lookup"><span data-stu-id="7ffee-128">toorevert a recommendation:</span></span>

1. <span data-ttu-id="7ffee-129">Menu indicazioni sulle prestazioni di toohello scegliere uno dei consigli hello applicato.</span><span class="sxs-lookup"><span data-stu-id="7ffee-129">Go toohello performance recommendations menu and select one of hello applied recommendations.</span></span>

    ![Selezionare una raccomandazione](./media/sql-database-performance-tutorial/select.png)

2. <span data-ttu-id="7ffee-131">Nella visualizzazione dei dettagli hello, fare clic su **Revert**.</span><span class="sxs-lookup"><span data-stu-id="7ffee-131">In hello details view, click **Revert**.</span></span>

    ![Ripristinare una raccomandazione](./media/sql-database-performance-tutorial/revert.png)

## <a name="find-hello-query-that-consumes-hello-most-resources"></a><span data-ttu-id="7ffee-133">La maggior parte delle risorse di query hello che utilizza hello</span><span class="sxs-lookup"><span data-stu-id="7ffee-133">Find hello query that consumes hello most resources</span></span>

<span data-ttu-id="7ffee-134">Eseguire la query di hello toofind questi passaggi utilizzo hello la maggior parte delle risorse:</span><span class="sxs-lookup"><span data-stu-id="7ffee-134">Follow these steps toofind hello query consuming hello most resources:</span></span>

1. <span data-ttu-id="7ffee-135">Fare clic su hello **informazioni dettagliate prestazioni Query** menu nel pannello database hello.</span><span class="sxs-lookup"><span data-stu-id="7ffee-135">Click on hello **Query Performance Insight** menu in hello database blade.</span></span>

    ![Informazioni dettagliate query](./media/sql-database-performance-tutorial/query_perf_insights.png)

2. <span data-ttu-id="7ffee-137">Selezionare un tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="7ffee-137">Select a resource type.</span></span>

    ![Informazioni dettagliate query](./media/sql-database-performance-tutorial/select_resource_type.png)

3. <span data-ttu-id="7ffee-139">Selezionare prima query hello nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="7ffee-139">Select hello first query in hello table.</span></span>

    ![Informazioni dettagliate query](./media/sql-database-performance-tutorial/select_query.png)

4. <span data-ttu-id="7ffee-141">Esaminare i dettagli di query hello.</span><span class="sxs-lookup"><span data-stu-id="7ffee-141">Review hello query details.</span></span>

    ![Informazioni dettagliate query](./media/sql-database-performance-tutorial/query_details.png)

## <a name="find-hello-longest-running-query"></a><span data-ttu-id="7ffee-143">Trovare la query in esecuzione più lunga di hello</span><span class="sxs-lookup"><span data-stu-id="7ffee-143">Find hello longest running query</span></span>

1. <span data-ttu-id="7ffee-144">Informazioni dettagliate prestazioni tooQuery scegliere hello **query a esecuzione prolungata** scheda.</span><span class="sxs-lookup"><span data-stu-id="7ffee-144">Go tooQuery Performance Insight and select hello **Long running queries** tab.</span></span>

    ![Informazioni dettagliate query](./media/sql-database-performance-tutorial/long_running.png)

3. <span data-ttu-id="7ffee-146">Selezionare prima query hello nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="7ffee-146">Select hello first query in hello table.</span></span>

    ![Informazioni dettagliate query](./media/sql-database-performance-tutorial/select_first_query.png)

4. <span data-ttu-id="7ffee-148">Esaminare i dettagli di query hello.</span><span class="sxs-lookup"><span data-stu-id="7ffee-148">Review hello query details.</span></span>

    ![Informazioni dettagliate query](./media/sql-database-performance-tutorial/review_query_details.png)



## <a name="next-steps"></a><span data-ttu-id="7ffee-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7ffee-150">Next steps</span></span> 
<span data-ttu-id="7ffee-151">Spesso le prestazioni non ottimali del database sono dovute a indici mancanti e query non ottimizzate correttamente.</span><span class="sxs-lookup"><span data-stu-id="7ffee-151">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="7ffee-152">Questa esercitazione illustra come:</span><span class="sxs-lookup"><span data-stu-id="7ffee-152">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="7ffee-153">Esaminare, applicare e ripristinare le raccomandazioni per migliorare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="7ffee-153">Review, apply and revert performance improvement recommendations</span></span>
> * <span data-ttu-id="7ffee-154">Trovare query con un utilizzo elevato delle risorse.</span><span class="sxs-lookup"><span data-stu-id="7ffee-154">Find queries with high resource utilization</span></span>
> * <span data-ttu-id="7ffee-155">Trovare query con esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="7ffee-155">Find long running queries</span></span>

[<span data-ttu-id="7ffee-156">Suggerimenti sull'ottimizzazione delle prestazioni del database SQL</span><span class="sxs-lookup"><span data-stu-id="7ffee-156">SQL Database performance tuning tips</span></span>](https://docs.microsoft.com/azure/sql-database/sql-database-troubleshoot-performance)
