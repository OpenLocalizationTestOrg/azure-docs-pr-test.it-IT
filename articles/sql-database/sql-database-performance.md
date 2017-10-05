---
title: Monitorare e migliorare le prestazioni - Database SQL di Azure | Microsoft Docs
description: "Il database SQL di Azure offre strumenti per le prestazioni che consentono di identificare le aree in cui è possibile migliorare le prestazioni delle query correnti."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: a60b75ac-cf27-4d73-8322-ee4d4c448aa2
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/19/2016
ms.author: sstein
ms.openlocfilehash: 522b932ab055978c52f085dbaa36095bb6b77962
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-improve-performance"></a><span data-ttu-id="be4e0-103">Monitorare e migliorare le prestazioni</span><span class="sxs-lookup"><span data-stu-id="be4e0-103">Monitor and improve performance</span></span>
<span data-ttu-id="be4e0-104">Il database SQL di Azure identifica potenziali problemi in un database e propone azioni che consentono di migliorare le prestazioni del carico di lavoro tramite azioni e raccomandazioni per l'ottimizzazione intelligente.</span><span class="sxs-lookup"><span data-stu-id="be4e0-104">Azure SQL Database identifies potential problems in your database and recommends actions that can improve performance of your workload by providing intelligent tuning actions and recommendations.</span></span>

<span data-ttu-id="be4e0-105">Per esaminare le prestazioni dei database, usare il riquadro **Prestazioni** nella pagina Informazioni generali oppure passare alla sezione "Supporto e risoluzione dei problemi":</span><span class="sxs-lookup"><span data-stu-id="be4e0-105">To review your database performance, use the **Performance** tile on the Overview page, or navigate down to "Support + troubleshooting" section:</span></span>

   ![Visualizzare le prestazioni](./media/sql-database-performance/entries.png)

<span data-ttu-id="be4e0-107">Nella sezione "Supporto e risoluzione dei problemi" è possibile usare le pagine seguenti:</span><span class="sxs-lookup"><span data-stu-id="be4e0-107">In the "Support + troubleshooting" section, you can use the following pages:</span></span>


1. <span data-ttu-id="be4e0-108">[Informazioni generali sulle prestazioni](#performance-overview) per monitorare le prestazioni del database.</span><span class="sxs-lookup"><span data-stu-id="be4e0-108">[Performance overview](#performance-overview) to monitor performance of your database.</span></span> 
2. <span data-ttu-id="be4e0-109">[Raccomandazioni per le prestazioni](#performance-recommendations) per trovare suggerimenti relativi alle prestazioni che possono migliorare le prestazioni del carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="be4e0-109">[Performance recommendations](#performance-recommendations) to find performance recommendations that can improve performance of your workload.</span></span>
3. <span data-ttu-id="be4e0-110">[Informazioni dettagliate prestazioni query](#query-performance-insight) per trovare le query con il maggior consumo di risorse.</span><span class="sxs-lookup"><span data-stu-id="be4e0-110">[Query Performance Insight](#query-performance-insight) to find top resource consuming queries.</span></span>
4. <span data-ttu-id="be4e0-111">[Ottimizzazione automatica](#automatic-tuning) per consentire al database SQL di Azure di ottimizzare automaticamente il database.</span><span class="sxs-lookup"><span data-stu-id="be4e0-111">[Automatic tuning](#automatic-tuning) to let Azure SQL Database automatically optimize your database.</span></span>

## <a name="performance-overview"></a><span data-ttu-id="be4e0-112">Panoramica sulle prestazioni</span><span class="sxs-lookup"><span data-stu-id="be4e0-112">Performance Overview</span></span>
<span data-ttu-id="be4e0-113">Questa vista offre una panoramica delle prestazioni del database e facilita le operazioni di ottimizzazione delle prestazioni e risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="be4e0-113">This view provides a summary of your database performance, and helps you with performance tuning and troubleshooting.</span></span> 

![Prestazioni](./media/sql-database-performance/performance.png)

* <span data-ttu-id="be4e0-115">Il riquadro **Raccomandazioni** offre un elenco di raccomandazioni di ottimizzazione per il database (vengono visualizzate le tre raccomandazioni principali se ne sono presenti di più).</span><span class="sxs-lookup"><span data-stu-id="be4e0-115">The **Recommendations** tile provides a breakdown of tuning recommendations for your database (top three recommendations are shown if there are more).</span></span> <span data-ttu-id="be4e0-116">Se si fa clic su questo riquadro vengono visualizzate le **[Raccomandazioni per le prestazioni](#performance-recommendations)**.</span><span class="sxs-lookup"><span data-stu-id="be4e0-116">Clicking this tile takes you to **[Performance recommendations](#performance-recommendations)**.</span></span> 
* <span data-ttu-id="be4e0-117">Il riquadro **Attività di ottimizzazione** fornisce un riepilogo delle operazioni di ottimizzazione in corso e completate per il database e offre una vista rapida della cronologia delle attività di ottimizzazione.</span><span class="sxs-lookup"><span data-stu-id="be4e0-117">The **Tuning activity** tile provides a summary of the ongoing and completed tuning actions for your database, giving you a quick view into the history of tuning activity.</span></span> <span data-ttu-id="be4e0-118">Se si fa clic su questo riquadro viene visualizzata la cronologia di ottimizzazione completa per il database.</span><span class="sxs-lookup"><span data-stu-id="be4e0-118">Clicking this tile takes you to the full tuning history view for your database.</span></span>
* <span data-ttu-id="be4e0-119">Il riquadro **Ottimizzazione automatica** visualizza la [configurazione di ottimizzazione automatica](sql-database-automatic-tuning-enable.md) per il database, ovvero le opzioni di ottimizzazione applicate automaticamente al database.</span><span class="sxs-lookup"><span data-stu-id="be4e0-119">The **Auto-tuning** tile shows the [auto-tuning configuration](sql-database-automatic-tuning-enable.md) for your database (tuning options that are automatically applied to your database).</span></span> <span data-ttu-id="be4e0-120">Se si fa clic su questo riquadro viene visualizzata la finestra di dialogo di configurazione dell'automazione.</span><span class="sxs-lookup"><span data-stu-id="be4e0-120">Clicking this tile opens the automation configuration dialog.</span></span>
* <span data-ttu-id="be4e0-121">Il riquadro **Query su database** visualizza un riepilogo delle prestazioni delle query per il database (uso complessivo di DTU e query con il maggior consumo di risorse).</span><span class="sxs-lookup"><span data-stu-id="be4e0-121">The **Database queries** tile shows the summary of the query performance for your database (overall DTU usage and top resource consuming queries).</span></span> <span data-ttu-id="be4e0-122">Se si fa clic su questo riquadro viene visualizzata la pagina **[Informazioni dettagliate prestazioni query](#query-performance-insight)**.</span><span class="sxs-lookup"><span data-stu-id="be4e0-122">Clicking this tile takes you to **[Query Performance Insight](#query-performance-insight)**.</span></span>

## <a name="performance-recommendations"></a><span data-ttu-id="be4e0-123">Raccomandazioni per le prestazioni</span><span class="sxs-lookup"><span data-stu-id="be4e0-123">Performance recommendations</span></span>
<span data-ttu-id="be4e0-124">Questa pagina offre [raccomandazioni per l'ottimizzazione](sql-database-advisor.md) intelligenti che consentono di migliorare le prestazioni del database.</span><span class="sxs-lookup"><span data-stu-id="be4e0-124">This page provides intelligent [tuning recommendations](sql-database-advisor.md) that can improve your database's performance.</span></span> <span data-ttu-id="be4e0-125">In questa pagina vengono illustrati i tipi seguenti di raccomandazioni:</span><span class="sxs-lookup"><span data-stu-id="be4e0-125">The following types of recommendations are shown on this page:</span></span>

* <span data-ttu-id="be4e0-126">Consigli per gli indici da creare o eliminare.</span><span class="sxs-lookup"><span data-stu-id="be4e0-126">Recommendations on which indexes to create or drop.</span></span>
* <span data-ttu-id="be4e0-127">Consigli su come procedere quando vengono identificati problemi di schema nel database.</span><span class="sxs-lookup"><span data-stu-id="be4e0-127">Recommendations when schema issues are identified in the database.</span></span>
* <span data-ttu-id="be4e0-128">Consigli sui casi in cui trarre vantaggio dalle query con parametri.</span><span class="sxs-lookup"><span data-stu-id="be4e0-128">Recommendations when queries can benefit from parameterized queries.</span></span>

![Prestazioni](./media/sql-database-performance/recommendations.png)

<span data-ttu-id="be4e0-130">È anche possibile trovare la cronologia completa delle azioni di ottimizzazione applicate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="be4e0-130">You can also find complete history of tuning actions that were applied in the past.</span></span>

<span data-ttu-id="be4e0-131">Per informazioni su come trovare e applicare le raccomandazioni per le prestazioni, vedere l'articolo [Trovare e applicare raccomandazioni per le prestazioni](sql-database-advisor-portal.md).</span><span class="sxs-lookup"><span data-stu-id="be4e0-131">Learn how to find an apply performance recommendations in [Find and apply performance recommendations](sql-database-advisor-portal.md) article.</span></span>

## <a name="automatic-tuning"></a><span data-ttu-id="be4e0-132">Ottimizzazione automatica</span><span class="sxs-lookup"><span data-stu-id="be4e0-132">Automatic tuning</span></span>
<span data-ttu-id="be4e0-133">Il database SQL di Azure può ottimizzare automaticamente le prestazioni del database tramite l'applicazione di [raccomandazioni per le prestazioni](sql-database-advisor.md).</span><span class="sxs-lookup"><span data-stu-id="be4e0-133">Azure SQL Databases can automatically tune database performance by applying [performance recommendations](sql-database-advisor.md).</span></span> <span data-ttu-id="be4e0-134">Per altre informazioni, leggere l'[articolo sull'ottimizzazione automatica](sql-database-automatic-tuning.md) .</span><span class="sxs-lookup"><span data-stu-id="be4e0-134">To learn more, read [Automatic tuning article](sql-database-automatic-tuning.md).</span></span> <span data-ttu-id="be4e0-135">Per abilitare questa funzionalità, leggere l'[articolo su come abilitare l'ottimizzazione automatica](sql-database-automatic-tuning-enable.md).</span><span class="sxs-lookup"><span data-stu-id="be4e0-135">To enable it, read [how to enable automatic tuning](sql-database-automatic-tuning-enable.md).</span></span>

## <a name="query-performance-insight"></a><span data-ttu-id="be4e0-136">Informazioni dettagliate prestazioni query</span><span class="sxs-lookup"><span data-stu-id="be4e0-136">Query Performance Insight</span></span>
<span data-ttu-id="be4e0-137">[Informazioni dettagliate prestazioni query](sql-database-query-performance.md) consente di dedicare meno tempo alla risoluzione dei problemi di prestazioni del database, offrendo i vantaggi seguenti:​</span><span class="sxs-lookup"><span data-stu-id="be4e0-137">[Query Performance Insight](sql-database-query-performance.md) allows you to spend less time troubleshooting database performance by providing:</span></span>

* <span data-ttu-id="be4e0-138">Informazioni più approfondite sull'utilizzo delle risorse del database (DTU).</span><span class="sxs-lookup"><span data-stu-id="be4e0-138">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="be4e0-139">Query principali a livello di utilizzo di CPU, che possono essere ottimizzate per migliorare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="be4e0-139">The top CPU consuming queries, which can potentially be tuned for improved performance.</span></span> 
* <span data-ttu-id="be4e0-140">Capacità di eseguire il drill-down nei dettagli di una query. ​</span><span class="sxs-lookup"><span data-stu-id="be4e0-140">The ability to drill down into the details of a query.</span></span> 

  ![dashboard prestazioni](./media/sql-database-query-performance/performance.png)

<span data-ttu-id="be4e0-142">Altre informazioni su questa pagina sono disponibili nell'articolo **[Usare Informazioni dettagliate prestazioni query](sql-database-query-performance.md)**.</span><span class="sxs-lookup"><span data-stu-id="be4e0-142">Find more information about this page in the article **[How to use Query Performance Insight](sql-database-query-performance.md)**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="be4e0-143">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="be4e0-143">Additional resources</span></span>
* [<span data-ttu-id="be4e0-144">Indicazioni sulle prestazioni del database SQL di Azure per i singoli database</span><span class="sxs-lookup"><span data-stu-id="be4e0-144">Azure SQL Database performance guidance for single databases</span></span>](sql-database-performance-guidance.md)
* [<span data-ttu-id="be4e0-145">Quando usare un pool elastico</span><span class="sxs-lookup"><span data-stu-id="be4e0-145">When should an elastic pool be used?</span></span>](sql-database-elastic-pool-guidance.md)

