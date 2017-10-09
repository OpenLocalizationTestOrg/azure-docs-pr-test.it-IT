---
title: aaaMonitor e migliorare le prestazioni - Database SQL di Azure | Documenti Microsoft
description: Database SQL di Azure offre prestazioni Hello strumenti toohelp si identificano le aree che possono migliorare le prestazioni delle query corrente.
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
ms.openlocfilehash: 84b8a1bc62698a29deb49e765f208bd7e14d0870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-improve-performance"></a><span data-ttu-id="12004-103">Monitorare e migliorare le prestazioni</span><span class="sxs-lookup"><span data-stu-id="12004-103">Monitor and improve performance</span></span>
<span data-ttu-id="12004-104">Il database SQL di Azure identifica potenziali problemi in un database e propone azioni che consentono di migliorare le prestazioni del carico di lavoro tramite azioni e raccomandazioni per l'ottimizzazione intelligente.</span><span class="sxs-lookup"><span data-stu-id="12004-104">Azure SQL Database identifies potential problems in your database and recommends actions that can improve performance of your workload by providing intelligent tuning actions and recommendations.</span></span>

<span data-ttu-id="12004-105">tooreview le prestazioni del database, utilizzare hello **prestazioni** riquadro nella pagina di panoramica hello o spostarsi verso il basso troppo "Supporto + risoluzione dei problemi" sezione:</span><span class="sxs-lookup"><span data-stu-id="12004-105">tooreview your database performance, use hello **Performance** tile on hello Overview page, or navigate down too"Support + troubleshooting" section:</span></span>

   ![Visualizzare le prestazioni](./media/sql-database-performance/entries.png)

<span data-ttu-id="12004-107">Nella sezione hello "Supporto + risoluzione dei problemi", è possibile utilizzare hello seguenti pagine:</span><span class="sxs-lookup"><span data-stu-id="12004-107">In hello "Support + troubleshooting" section, you can use hello following pages:</span></span>


1. <span data-ttu-id="12004-108">[Cenni preliminari sulle prestazioni](#performance-overview) toomonitor delle prestazioni del database.</span><span class="sxs-lookup"><span data-stu-id="12004-108">[Performance overview](#performance-overview) toomonitor performance of your database.</span></span> 
2. <span data-ttu-id="12004-109">[Consigli relativi alle prestazioni](#performance-recommendations) toofind suggerimenti relativi alle prestazioni che può migliorare le prestazioni del carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="12004-109">[Performance recommendations](#performance-recommendations) toofind performance recommendations that can improve performance of your workload.</span></span>
3. <span data-ttu-id="12004-110">[Informazioni dettagliate prestazioni query](#query-performance-insight) toofind query per consumo di risorse superiore.</span><span class="sxs-lookup"><span data-stu-id="12004-110">[Query Performance Insight](#query-performance-insight) toofind top resource consuming queries.</span></span>
4. <span data-ttu-id="12004-111">[L'ottimizzazione automatica](#automatic-tuning) toolet Database SQL di Azure ottimizzare automaticamente il database.</span><span class="sxs-lookup"><span data-stu-id="12004-111">[Automatic tuning](#automatic-tuning) toolet Azure SQL Database automatically optimize your database.</span></span>

## <a name="performance-overview"></a><span data-ttu-id="12004-112">Panoramica sulle prestazioni</span><span class="sxs-lookup"><span data-stu-id="12004-112">Performance Overview</span></span>
<span data-ttu-id="12004-113">Questa vista offre una panoramica delle prestazioni del database e facilita le operazioni di ottimizzazione delle prestazioni e risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="12004-113">This view provides a summary of your database performance, and helps you with performance tuning and troubleshooting.</span></span> 

![Prestazioni](./media/sql-database-performance/performance.png)

* <span data-ttu-id="12004-115">Hello **indicazioni** riquadro fornisce un riepilogo di indicazioni per il database di ottimizzazione (prime tre raccomandazioni vengono visualizzati se sono presenti più).</span><span class="sxs-lookup"><span data-stu-id="12004-115">hello **Recommendations** tile provides a breakdown of tuning recommendations for your database (top three recommendations are shown if there are more).</span></span> <span data-ttu-id="12004-116">Fare clic su questo riquadro consente di passare troppo**[consigli relativi alle prestazioni](#performance-recommendations)**.</span><span class="sxs-lookup"><span data-stu-id="12004-116">Clicking this tile takes you too**[Performance recommendations](#performance-recommendations)**.</span></span> 
* <span data-ttu-id="12004-117">Hello **ottimizzazione attività** riquadro fornisce un riepilogo di hello in corso e completata ottimizzazione azioni per il database, consentendo di visualizzare rapidamente cronologia hello delle attività di ottimizzazione.</span><span class="sxs-lookup"><span data-stu-id="12004-117">hello **Tuning activity** tile provides a summary of hello ongoing and completed tuning actions for your database, giving you a quick view into hello history of tuning activity.</span></span> <span data-ttu-id="12004-118">Fare clic su questo riquadro consente di passare toohello completo ottimizzazione visualizzazione della cronologia per il database.</span><span class="sxs-lookup"><span data-stu-id="12004-118">Clicking this tile takes you toohello full tuning history view for your database.</span></span>
* <span data-ttu-id="12004-119">Hello **ottimizzazione automatica** riquadro Mostra hello [ottimizzazione automatica della configurazione](sql-database-automatic-tuning-enable.md) per il database (ottimizzazione opzioni che vengono automaticamente applicati tooyour database).</span><span class="sxs-lookup"><span data-stu-id="12004-119">hello **Auto-tuning** tile shows hello [auto-tuning configuration](sql-database-automatic-tuning-enable.md) for your database (tuning options that are automatically applied tooyour database).</span></span> <span data-ttu-id="12004-120">Fare clic su questo riquadro, verrà visualizzata la finestra di dialogo Configurazione automazione hello.</span><span class="sxs-lookup"><span data-stu-id="12004-120">Clicking this tile opens hello automation configuration dialog.</span></span>
* <span data-ttu-id="12004-121">Hello **le query su Database** riquadro riepiloga hello hello le prestazioni delle query per il database (generale DTU utilizzo e top resource query per consumo).</span><span class="sxs-lookup"><span data-stu-id="12004-121">hello **Database queries** tile shows hello summary of hello query performance for your database (overall DTU usage and top resource consuming queries).</span></span> <span data-ttu-id="12004-122">Fare clic su questo riquadro consente di passare troppo**[informazioni dettagliate prestazioni Query](#query-performance-insight)**.</span><span class="sxs-lookup"><span data-stu-id="12004-122">Clicking this tile takes you too**[Query Performance Insight](#query-performance-insight)**.</span></span>

## <a name="performance-recommendations"></a><span data-ttu-id="12004-123">Raccomandazioni per le prestazioni</span><span class="sxs-lookup"><span data-stu-id="12004-123">Performance recommendations</span></span>
<span data-ttu-id="12004-124">Questa pagina offre [raccomandazioni per l'ottimizzazione](sql-database-advisor.md) intelligenti che consentono di migliorare le prestazioni del database.</span><span class="sxs-lookup"><span data-stu-id="12004-124">This page provides intelligent [tuning recommendations](sql-database-advisor.md) that can improve your database's performance.</span></span> <span data-ttu-id="12004-125">in questa pagina viene visualizzato i seguenti tipi di suggerimenti Hello:</span><span class="sxs-lookup"><span data-stu-id="12004-125">hello following types of recommendations are shown on this page:</span></span>

* <span data-ttu-id="12004-126">Suggerimenti su quale toocreate indici o drop.</span><span class="sxs-lookup"><span data-stu-id="12004-126">Recommendations on which indexes toocreate or drop.</span></span>
* <span data-ttu-id="12004-127">Suggerimenti quando vengono identificati i problemi dello schema nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="12004-127">Recommendations when schema issues are identified in hello database.</span></span>
* <span data-ttu-id="12004-128">Consigli sui casi in cui trarre vantaggio dalle query con parametri.</span><span class="sxs-lookup"><span data-stu-id="12004-128">Recommendations when queries can benefit from parameterized queries.</span></span>

![Prestazioni](./media/sql-database-performance/recommendations.png)

<span data-ttu-id="12004-130">È inoltre possibile trovare cronologia completa di ottimizzazione di azioni che sono state applicate in hello precedente.</span><span class="sxs-lookup"><span data-stu-id="12004-130">You can also find complete history of tuning actions that were applied in hello past.</span></span>

<span data-ttu-id="12004-131">Informazioni su come toofind apply consigli relativi alle prestazioni in [cercare e applicare i consigli relativi alle prestazioni](sql-database-advisor-portal.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="12004-131">Learn how toofind an apply performance recommendations in [Find and apply performance recommendations](sql-database-advisor-portal.md) article.</span></span>

## <a name="automatic-tuning"></a><span data-ttu-id="12004-132">Ottimizzazione automatica</span><span class="sxs-lookup"><span data-stu-id="12004-132">Automatic tuning</span></span>
<span data-ttu-id="12004-133">Il database SQL di Azure può ottimizzare automaticamente le prestazioni del database tramite l'applicazione di [raccomandazioni per le prestazioni](sql-database-advisor.md).</span><span class="sxs-lookup"><span data-stu-id="12004-133">Azure SQL Databases can automatically tune database performance by applying [performance recommendations](sql-database-advisor.md).</span></span> <span data-ttu-id="12004-134">leggere più, toolearn [articolo ottimizzazione automatica](sql-database-automatic-tuning.md).</span><span class="sxs-lookup"><span data-stu-id="12004-134">toolearn more, read [Automatic tuning article](sql-database-automatic-tuning.md).</span></span> <span data-ttu-id="12004-135">tooenable, leggere [come l'ottimizzazione automatica tooenable](sql-database-automatic-tuning-enable.md).</span><span class="sxs-lookup"><span data-stu-id="12004-135">tooenable it, read [how tooenable automatic tuning](sql-database-automatic-tuning-enable.md).</span></span>

## <a name="query-performance-insight"></a><span data-ttu-id="12004-136">Informazioni dettagliate prestazioni query</span><span class="sxs-lookup"><span data-stu-id="12004-136">Query Performance Insight</span></span>
<span data-ttu-id="12004-137">[Informazioni dettagliate prestazioni query](sql-database-query-performance.md) toospend consente tempi di risoluzione dei problemi di prestazioni del database fornendo:</span><span class="sxs-lookup"><span data-stu-id="12004-137">[Query Performance Insight](sql-database-query-performance.md) allows you toospend less time troubleshooting database performance by providing:</span></span>

* <span data-ttu-id="12004-138">Informazioni più approfondite sull'utilizzo delle risorse del database (DTU).</span><span class="sxs-lookup"><span data-stu-id="12004-138">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="12004-139">Hello superiore che utilizzano la CPU query, è potenzialmente possibile ottimizzare per migliorare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="12004-139">hello top CPU consuming queries, which can potentially be tuned for improved performance.</span></span> 
* <span data-ttu-id="12004-140">Hello possibilità toodrill verso il basso in dettagli hello di una query.</span><span class="sxs-lookup"><span data-stu-id="12004-140">hello ability toodrill down into hello details of a query.</span></span> 

  ![dashboard prestazioni](./media/sql-database-query-performance/performance.png)

<span data-ttu-id="12004-142">Ulteriori informazioni su questa pagina dell'articolo hello  **[come toouse informazioni dettagliate prestazioni Query](sql-database-query-performance.md)**.</span><span class="sxs-lookup"><span data-stu-id="12004-142">Find more information about this page in hello article **[How toouse Query Performance Insight](sql-database-query-performance.md)**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="12004-143">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="12004-143">Additional resources</span></span>
* [<span data-ttu-id="12004-144">Indicazioni sulle prestazioni del database SQL di Azure per i singoli database</span><span class="sxs-lookup"><span data-stu-id="12004-144">Azure SQL Database performance guidance for single databases</span></span>](sql-database-performance-guidance.md)
* [<span data-ttu-id="12004-145">Quando usare un pool elastico</span><span class="sxs-lookup"><span data-stu-id="12004-145">When should an elastic pool be used?</span></span>](sql-database-elastic-pool-guidance.md)

