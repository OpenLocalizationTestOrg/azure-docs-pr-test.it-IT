---
title: Consigli di Azure Advisor sulle prestazioni | Microsoft Docs
description: Usare Advisor per ottimizzare le prestazioni delle distribuzioni di Azure.
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
ms.openlocfilehash: 5fb86c60b2d1f258dde5636ff8854b6f30f7f1c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="advisor-performance-recommendations"></a><span data-ttu-id="65525-103">Consigli di Advisor sulle prestazioni</span><span class="sxs-lookup"><span data-stu-id="65525-103">Advisor Performance recommendations</span></span>

<span data-ttu-id="65525-104">Grazie ai consigli di Azure Advisor sulle prestazioni, è possibile migliorare e aumentare la velocità e la reattività delle applicazioni aziendali critiche.</span><span class="sxs-lookup"><span data-stu-id="65525-104">Azure Advisor performance recommendations help improve the speed and responsiveness of your business-critical applications.</span></span> <span data-ttu-id="65525-105">È possibile ottenere da Advisor consigli sulle prestazioni nella scheda **Prestazioni** scheda del dashboard di Advisor.</span><span class="sxs-lookup"><span data-stu-id="65525-105">You can get performance recommendations from Advisor on the **Performance** tab of the Advisor dashboard.</span></span>

![Scheda Prestazioni di Advisor](./media/advisor-performance-recommendations/advisor-performance-tab.png)

## <a name="improve-database-performance-with-sql-db-advisor"></a><span data-ttu-id="65525-107">Migliorare le prestazioni del database con Advisor per database SQL</span><span class="sxs-lookup"><span data-stu-id="65525-107">Improve database performance with SQL DB Advisor</span></span>

<span data-ttu-id="65525-108">Advisor fornisce una visualizzazione coerente e consolidata dei consigli per tutte le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="65525-108">Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span></span> <span data-ttu-id="65525-109">Si integra con Advisor per database SQL per offrire consigli su come migliorare le prestazioni del database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="65525-109">It integrates with SQL Database Advisor to bring you recommendations for improving the performance of your SQL Azure database.</span></span> <span data-ttu-id="65525-110">Advisor per database SQL consente di valutare le prestazioni dei database SQL di Azure analizzando la cronologia relativa all'uso.</span><span class="sxs-lookup"><span data-stu-id="65525-110">SQL Database Advisor assesses the performance of your SQL Azure databases by analyzing your usage history.</span></span> <span data-ttu-id="65525-111">Offre quindi consigli ideali per l'esecuzione del carico di lavoro tipico del database.</span><span class="sxs-lookup"><span data-stu-id="65525-111">It then offers recommendations that are best suited for running the database’s typical workload.</span></span> 

> [!NOTE]
> <span data-ttu-id="65525-112">Per ottenere consigli, è necessario che un database sia stato in uso per circa una settimana, nel corso della quale deve essersi verificata attività coerente.</span><span class="sxs-lookup"><span data-stu-id="65525-112">To get recommendations, a database must have about a week of usage, and within that week there must be some consistent activity.</span></span> <span data-ttu-id="65525-113">Advisor per database SQL può essere più facilmente ottimizzato per modelli di query coerenti anziché picchi irregolari casuali di attività.</span><span class="sxs-lookup"><span data-stu-id="65525-113">SQL Database Advisor can optimize more easily for consistent query patterns than for random bursts of activity.</span></span>

<span data-ttu-id="65525-114">Per altre informazioni su Advisor per database SQL, vedere [Advisor per database SQL](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).</span><span class="sxs-lookup"><span data-stu-id="65525-114">For more information about SQL Database Advisor, see [SQL Database Advisor](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).</span></span>

![Consigli sul database SQL](./media/advisor-performance-recommendations/advisor-performance-sql.png)

## <a name="improve-redis-cache-performance-and-reliability"></a><span data-ttu-id="65525-116">Migliorare affidabilità e prestazioni di Cache Redis</span><span class="sxs-lookup"><span data-stu-id="65525-116">Improve Redis Cache performance and reliability</span></span>

<span data-ttu-id="65525-117">Advisor identifica le istanze di Cache Redis in cui le prestazioni potrebbero aver subito effetti negativi a causa di uso di memoria, carico del server, larghezza di banda di rete e numero di connessioni client elevati.</span><span class="sxs-lookup"><span data-stu-id="65525-117">Advisor identifies Redis Cache instances where performance may be adversely affected by high memory usage, server load, network bandwidth, or a large number of client connections.</span></span> <span data-ttu-id="65525-118">Advisor fornisce inoltre consigli sulle procedure consigliate che consentono di evitare potenziali problemi.</span><span class="sxs-lookup"><span data-stu-id="65525-118">Advisor also provides best practices recommendations to help you avoid potential issues.</span></span> <span data-ttu-id="65525-119">Per altre informazioni relative ai consigli su Cache Redis, vedere [Redis Cache Advisor](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).</span><span class="sxs-lookup"><span data-stu-id="65525-119">For more information about Redis Cache recommendations, see [Redis Cache Advisor](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).</span></span>


## <a name="improve-app-service-performance-and-reliability"></a><span data-ttu-id="65525-120">Migliorare affidabilità e prestazioni di Servizi app</span><span class="sxs-lookup"><span data-stu-id="65525-120">Improve App Service performance and reliability</span></span>

<span data-ttu-id="65525-121">Azure Advisor integra consigli sulle procedure consigliate per migliorare l'esperienza di Servizi app e scoprire le funzionalità della piattaforma pertinente.</span><span class="sxs-lookup"><span data-stu-id="65525-121">Azure Advisor integrates best practices recommendations for improving your App Services experience and discovering relevant platform capabilities.</span></span> <span data-ttu-id="65525-122">Esempi di consigli per Servizi app sono:</span><span class="sxs-lookup"><span data-stu-id="65525-122">Examples of App Services recommendations are:</span></span>
* <span data-ttu-id="65525-123">Rilevamento delle istanze in cui le risorse di CPU o memoria vengono esaurite dai runtime delle app con opzioni di migrazione.</span><span class="sxs-lookup"><span data-stu-id="65525-123">Detection of instances where memory or CPU resources are exhausted by app runtimes with mitigation options.</span></span>
* <span data-ttu-id="65525-124">Rilevamento delle istanze in cui la collocazione delle risorse come App Web e database può aumentare le prestazioni e ridurre il costo.</span><span class="sxs-lookup"><span data-stu-id="65525-124">Detection of instances where collocating resources like web apps and databases can improve performance and lower cost.</span></span> 

<span data-ttu-id="65525-125">Per altre informazioni sui consigli per Servizi app, vedere [Procedure consigliate per Servizio app di Azure](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).</span><span class="sxs-lookup"><span data-stu-id="65525-125">For more information about App Services recommendations, see [Best Practices for Azure App Service](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).</span></span>
<span data-ttu-id="65525-126">![Consigli per Servizi app](./media/advisor-performance-recommendations/advisor-performance-app-service.png)</span><span class="sxs-lookup"><span data-stu-id="65525-126">![App Services recommendations](./media/advisor-performance-recommendations/advisor-performance-app-service.png)</span></span>

## <a name="how-to-access-performance-recommendations-in-advisor"></a><span data-ttu-id="65525-127">Come accedere ai consigli sulle prestazioni in Advisor</span><span class="sxs-lookup"><span data-stu-id="65525-127">How to access Performance recommendations in Advisor</span></span>

1. <span data-ttu-id="65525-128">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="65525-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="65525-129">Nel riquadro sinistro selezionare **Altri servizi**.</span><span class="sxs-lookup"><span data-stu-id="65525-129">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="65525-130">Nel riquadro del menu del servizio in **Monitoraggio e gestione** fare clic su **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="65525-130">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="65525-131">Verrà visualizzato il dashboard di Advisor.</span><span class="sxs-lookup"><span data-stu-id="65525-131">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="65525-132">Nel dashboard di Advisor fare clic sulla scheda **Prestazioni**.</span><span class="sxs-lookup"><span data-stu-id="65525-132">On the Advisor dashboard, click the **Performance** tab.</span></span>

5. <span data-ttu-id="65525-133">Selezionare la sottoscrizione per cui si desidera ricevere consigli e quindi fare clic su **Ottieni raccomandazioni**.</span><span class="sxs-lookup"><span data-stu-id="65525-133">Select the subscription for which you want to receive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="65525-134">Per accedere ai consigli di Advisor, è innanzitutto necessario *registrare la sottoscrizione* con Advisor.</span><span class="sxs-lookup"><span data-stu-id="65525-134">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="65525-135">Una sottoscrizione viene registrata quando il *proprietario della sottoscrizione* avvia il dashboard di Advisor e fa clic sul pulsante **Ottieni raccomandazioni**.</span><span class="sxs-lookup"><span data-stu-id="65525-135">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="65525-136">Si tratta di un'*operazione una tantum*.</span><span class="sxs-lookup"><span data-stu-id="65525-136">This is a *one-time operation*.</span></span> <span data-ttu-id="65525-137">Dopo aver registrato una sottoscrizione, è possibile accedere ai consigli di Advisor come *Proprietario*, *Collaboratore* o *Lettore* di una sottoscrizione, di un gruppo di risorse o di una risorsa specifica.</span><span class="sxs-lookup"><span data-stu-id="65525-137">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65525-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="65525-138">Next steps</span></span>

<span data-ttu-id="65525-139">Per altre informazioni sui consigli di Advisor, vedere:</span><span class="sxs-lookup"><span data-stu-id="65525-139">To learn more about Advisor recommendations, see:</span></span>

* <span data-ttu-id="65525-140">[Introduction to Advisor](advisor-overview.md) (Presentazione di Azure Advisor)</span><span class="sxs-lookup"><span data-stu-id="65525-140">[Introduction to Advisor](advisor-overview.md)</span></span>
* <span data-ttu-id="65525-141">[Get started with Advisor](advisor-get-started.md) (Introduzione ad Advisor)</span><span class="sxs-lookup"><span data-stu-id="65525-141">[Get started with Advisor](advisor-get-started.md)</span></span>
* <span data-ttu-id="65525-142">[Advisor Cost recommendations](advisor-performance-recommendations.md) (Consigli di Advisor sui costi)</span><span class="sxs-lookup"><span data-stu-id="65525-142">[Advisor Cost recommendations](advisor-performance-recommendations.md)</span></span>
* <span data-ttu-id="65525-143">[Advisor High Availability recommendations](advisor-high-availability-recommendations.md) (Consigli di Advisor sulla disponibilità elevata)</span><span class="sxs-lookup"><span data-stu-id="65525-143">[Advisor High Availability recommendations](advisor-high-availability-recommendations.md)</span></span>
* <span data-ttu-id="65525-144">[Advisor Security recommendations](advisor-security-recommendations.md) (Consigli di Advisor sulla sicurezza)</span><span class="sxs-lookup"><span data-stu-id="65525-144">[Advisor Security recommendations](advisor-security-recommendations.md)</span></span>

