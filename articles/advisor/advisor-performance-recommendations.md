---
title: consigli relativi alle prestazioni di preparazione di aaaAzure | Documenti Microsoft
description: Utilizzare Advisor toooptimize hello prestazioni delle distribuzioni di Azure.
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: eb3d928664717f6f322132ac740f42015f56b76e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-performance-recommendations"></a><span data-ttu-id="89ec3-103">Consigli di Advisor sulle prestazioni</span><span class="sxs-lookup"><span data-stu-id="89ec3-103">Advisor Performance recommendations</span></span>

<span data-ttu-id="89ec3-104">Consigli relativi alle prestazioni di Azure Advisor consentono al miglioramento di hello velocità e la velocità di risposta delle applicazioni business-critical.</span><span class="sxs-lookup"><span data-stu-id="89ec3-104">Azure Advisor performance recommendations help improve hello speed and responsiveness of your business-critical applications.</span></span> <span data-ttu-id="89ec3-105">È possibile ottenere indicazioni relative alle prestazioni da Advisor in hello **prestazioni** scheda dashboard Advisor hello.</span><span class="sxs-lookup"><span data-stu-id="89ec3-105">You can get performance recommendations from Advisor on hello **Performance** tab of hello Advisor dashboard.</span></span>

![Scheda Prestazioni di Advisor](./media/advisor-performance-recommendations/advisor-performance-tab.png)

## <a name="improve-database-performance-with-sql-db-advisor"></a><span data-ttu-id="89ec3-107">Migliorare le prestazioni del database con Advisor per database SQL</span><span class="sxs-lookup"><span data-stu-id="89ec3-107">Improve database performance with SQL DB Advisor</span></span>

<span data-ttu-id="89ec3-108">Advisor fornisce una visualizzazione coerente e consolidata dei consigli per tutte le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="89ec3-108">Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span></span> <span data-ttu-id="89ec3-109">Si integra con toobring guidata Database SQL di indicazioni per migliorare le prestazioni di hello del database di SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="89ec3-109">It integrates with SQL Database Advisor toobring you recommendations for improving hello performance of your SQL Azure database.</span></span> <span data-ttu-id="89ec3-110">Preparazione del Database SQL valuta le prestazioni di hello dei database di SQL Azure analizzando alla cronologia di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="89ec3-110">SQL Database Advisor assesses hello performance of your SQL Azure databases by analyzing your usage history.</span></span> <span data-ttu-id="89ec3-111">Quindi offre indicazioni più adatti per l'esecuzione del carico di lavoro tipico del database hello.</span><span class="sxs-lookup"><span data-stu-id="89ec3-111">It then offers recommendations that are best suited for running hello database’s typical workload.</span></span> 

> [!NOTE]
> <span data-ttu-id="89ec3-112">indicazioni tooget, un database deve avere circa una settimana di utilizzo e all'interno di tale settimana deve essere un'attività coerenza.</span><span class="sxs-lookup"><span data-stu-id="89ec3-112">tooget recommendations, a database must have about a week of usage, and within that week there must be some consistent activity.</span></span> <span data-ttu-id="89ec3-113">Advisor per database SQL può essere più facilmente ottimizzato per modelli di query coerenti anziché picchi irregolari casuali di attività.</span><span class="sxs-lookup"><span data-stu-id="89ec3-113">SQL Database Advisor can optimize more easily for consistent query patterns than for random bursts of activity.</span></span>

<span data-ttu-id="89ec3-114">Per altre informazioni su Advisor per database SQL, vedere [Advisor per database SQL](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).</span><span class="sxs-lookup"><span data-stu-id="89ec3-114">For more information about SQL Database Advisor, see [SQL Database Advisor](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).</span></span>

![Consigli sul database SQL](./media/advisor-performance-recommendations/advisor-performance-sql.png)

## <a name="improve-redis-cache-performance-and-reliability"></a><span data-ttu-id="89ec3-116">Migliorare affidabilità e prestazioni di Cache Redis</span><span class="sxs-lookup"><span data-stu-id="89ec3-116">Improve Redis Cache performance and reliability</span></span>

<span data-ttu-id="89ec3-117">Advisor identifica le istanze di Cache Redis in cui le prestazioni potrebbero aver subito effetti negativi a causa di uso di memoria, carico del server, larghezza di banda di rete e numero di connessioni client elevati.</span><span class="sxs-lookup"><span data-stu-id="89ec3-117">Advisor identifies Redis Cache instances where performance may be adversely affected by high memory usage, server load, network bandwidth, or a large number of client connections.</span></span> <span data-ttu-id="89ec3-118">Advisor fornisce inoltre procedure consigliate toohelp suggerimenti evitare potenziali problemi.</span><span class="sxs-lookup"><span data-stu-id="89ec3-118">Advisor also provides best practices recommendations toohelp you avoid potential issues.</span></span> <span data-ttu-id="89ec3-119">Per altre informazioni relative ai consigli su Cache Redis, vedere [Redis Cache Advisor](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).</span><span class="sxs-lookup"><span data-stu-id="89ec3-119">For more information about Redis Cache recommendations, see [Redis Cache Advisor](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).</span></span>


## <a name="improve-app-service-performance-and-reliability"></a><span data-ttu-id="89ec3-120">Migliorare affidabilità e prestazioni di Servizi app</span><span class="sxs-lookup"><span data-stu-id="89ec3-120">Improve App Service performance and reliability</span></span>

<span data-ttu-id="89ec3-121">Azure Advisor integra consigli sulle procedure consigliate per migliorare l'esperienza di Servizi app e scoprire le funzionalità della piattaforma pertinente.</span><span class="sxs-lookup"><span data-stu-id="89ec3-121">Azure Advisor integrates best practices recommendations for improving your App Services experience and discovering relevant platform capabilities.</span></span> <span data-ttu-id="89ec3-122">Esempi di consigli per Servizi app sono:</span><span class="sxs-lookup"><span data-stu-id="89ec3-122">Examples of App Services recommendations are:</span></span>
* <span data-ttu-id="89ec3-123">Rilevamento delle istanze in cui le risorse di CPU o memoria vengono esaurite dai runtime delle app con opzioni di migrazione.</span><span class="sxs-lookup"><span data-stu-id="89ec3-123">Detection of instances where memory or CPU resources are exhausted by app runtimes with mitigation options.</span></span>
* <span data-ttu-id="89ec3-124">Rilevamento delle istanze in cui la collocazione delle risorse come App Web e database può aumentare le prestazioni e ridurre il costo.</span><span class="sxs-lookup"><span data-stu-id="89ec3-124">Detection of instances where collocating resources like web apps and databases can improve performance and lower cost.</span></span> 

<span data-ttu-id="89ec3-125">Per altre informazioni sui consigli per Servizi app, vedere [Procedure consigliate per Servizio app di Azure](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).</span><span class="sxs-lookup"><span data-stu-id="89ec3-125">For more information about App Services recommendations, see [Best Practices for Azure App Service](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).</span></span>
<span data-ttu-id="89ec3-126">![Consigli per Servizi app](./media/advisor-performance-recommendations/advisor-performance-app-service.png)</span><span class="sxs-lookup"><span data-stu-id="89ec3-126">![App Services recommendations](./media/advisor-performance-recommendations/advisor-performance-app-service.png)</span></span>

## <a name="how-tooaccess-performance-recommendations-in-advisor"></a><span data-ttu-id="89ec3-127">Come tooaccess consigli relativi alle prestazioni Advisor</span><span class="sxs-lookup"><span data-stu-id="89ec3-127">How tooaccess Performance recommendations in Advisor</span></span>

1. <span data-ttu-id="89ec3-128">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="89ec3-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="89ec3-129">Nel riquadro di sinistra hello, fare clic su **più servizi**.</span><span class="sxs-lookup"><span data-stu-id="89ec3-129">In hello left pane, click **More services**.</span></span>

3. <span data-ttu-id="89ec3-130">Hello servizio dei menu, in **monitoraggio e gestione**, fare clic su **Advisor Azure**.</span><span class="sxs-lookup"><span data-stu-id="89ec3-130">In hello service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="89ec3-131">Hello Advisor dashboard viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="89ec3-131">hello Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="89ec3-132">Nel dashboard di Advisor hello, fare clic su hello **prestazioni** scheda.</span><span class="sxs-lookup"><span data-stu-id="89ec3-132">On hello Advisor dashboard, click hello **Performance** tab.</span></span>

5. <span data-ttu-id="89ec3-133">Selezionare hello sottoscrizione per il quale desidera tooreceive indicazioni e quindi fare clic su **consigli**.</span><span class="sxs-lookup"><span data-stu-id="89ec3-133">Select hello subscription for which you want tooreceive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="89ec3-134">tooaccess raccomandazioni di Advisor, è innanzitutto necessario *registrare la sottoscrizione* con Advisor.</span><span class="sxs-lookup"><span data-stu-id="89ec3-134">tooaccess Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="89ec3-135">Una sottoscrizione viene registrata quando un *sottoscrizione proprietario* avvia hello hello di dashboard e fa clic su Advisor **consigli** pulsante.</span><span class="sxs-lookup"><span data-stu-id="89ec3-135">A subscription is registered when a *subscription Owner* launches hello Advisor dashboard and clicks hello **Get recommendations** button.</span></span> <span data-ttu-id="89ec3-136">Si tratta di un'*operazione una tantum*.</span><span class="sxs-lookup"><span data-stu-id="89ec3-136">This is a *one-time operation*.</span></span> <span data-ttu-id="89ec3-137">Dopo la sottoscrizione hello è registrata, è possibile accedere raccomandazioni di Advisor come *proprietario*, *collaboratore*, o *lettore* per una sottoscrizione, un gruppo di risorse, o risorsa specifica.</span><span class="sxs-lookup"><span data-stu-id="89ec3-137">After hello subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89ec3-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="89ec3-138">Next steps</span></span>

<span data-ttu-id="89ec3-139">toolearn sulle raccomandazioni di Advisor, vedere:</span><span class="sxs-lookup"><span data-stu-id="89ec3-139">toolearn more about Advisor recommendations, see:</span></span>

* [<span data-ttu-id="89ec3-140">Introduzione tooAdvisor</span><span class="sxs-lookup"><span data-stu-id="89ec3-140">Introduction tooAdvisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="89ec3-141">Introduzione ad Advisor</span><span class="sxs-lookup"><span data-stu-id="89ec3-141">Get started with Advisor</span></span>](advisor-get-started.md)
* <span data-ttu-id="89ec3-142">[Advisor Cost recommendations](advisor-performance-recommendations.md) (Consigli di Advisor sui costi)</span><span class="sxs-lookup"><span data-stu-id="89ec3-142">[Advisor Cost recommendations](advisor-performance-recommendations.md)</span></span>
* <span data-ttu-id="89ec3-143">[Advisor High Availability recommendations](advisor-high-availability-recommendations.md) (Consigli di Advisor sulla disponibilità elevata)</span><span class="sxs-lookup"><span data-stu-id="89ec3-143">[Advisor High Availability recommendations](advisor-high-availability-recommendations.md)</span></span>
* <span data-ttu-id="89ec3-144">[Advisor Security recommendations](advisor-security-recommendations.md) (Consigli di Advisor sulla sicurezza)</span><span class="sxs-lookup"><span data-stu-id="89ec3-144">[Advisor Security recommendations](advisor-security-recommendations.md)</span></span>

