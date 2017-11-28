---
title: archiviazione in memoria XTP aaaMonitor | Documenti Microsoft
description: "Stimare e monitorare l'uso e la capacità delle risorse di archiviazione in memoria XTP e risolvere l'errore di capacità 41823"
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: b617308e-692c-4938-8fa2-070034a3ecef
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: jodebrui
ms.openlocfilehash: fcb17bd8e9ebef4862d4b55bf5a79b45b9419fca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-in-memory-oltp-storage"></a><span data-ttu-id="919a2-103">Monitorare l'archiviazione OLTP in memoria</span><span class="sxs-lookup"><span data-stu-id="919a2-103">Monitor In-Memory OLTP Storage</span></span>
<span data-ttu-id="919a2-104">Quando si usa [OLTP in memoria](sql-database-in-memory.md), i dati nelle tabelle con ottimizzazione per la memoria e le variabili di tabella si trovano nell'archiviazione OLTP in memoria.</span><span class="sxs-lookup"><span data-stu-id="919a2-104">When using [In-Memory OLTP](sql-database-in-memory.md), data in memory-optimized tables and table variables resides in In-Memory OLTP storage.</span></span> <span data-ttu-id="919a2-105">Ogni livello di servizio Premium ha un formato di archiviazione OLTP In memoria massimo, che è documentato in hello [articolo livelli di servizio di Database SQL](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span><span class="sxs-lookup"><span data-stu-id="919a2-105">Each Premium service tier has a maximum In-Memory OLTP storage size, which is documented in hello [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span></span> <span data-ttu-id="919a2-106">Dopo il superamento di questo limite, è possibile che le operazioni di inserimento e aggiornamento abbiano esito negativo con errore 41823.</span><span class="sxs-lookup"><span data-stu-id="919a2-106">Once this limit is exceeded, insert and update operations may start failing (with error 41823).</span></span> <span data-ttu-id="919a2-107">A questo punto sarà necessario tooeither Elimina dati tooreclaim memoria o aggiornare hello livello di prestazioni del database.</span><span class="sxs-lookup"><span data-stu-id="919a2-107">At that point you will need tooeither delete data tooreclaim memory, or upgrade hello performance tier of your database.</span></span>

## <a name="determine-whether-data-will-fit-within-hello-in-memory-storage-cap"></a><span data-ttu-id="919a2-108">Determinare se i dati si adattino all'interno di criteri di archiviazione in memoria hello</span><span class="sxs-lookup"><span data-stu-id="919a2-108">Determine whether data will fit within hello in-memory storage cap</span></span>
<span data-ttu-id="919a2-109">Determinare il limite di archiviazione hello: hello, consultare [articolo livelli di servizio di Database SQL](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) per caps archiviazione hello di diversi livelli di servizio Premium hello.</span><span class="sxs-lookup"><span data-stu-id="919a2-109">Determine hello storage cap: consult hello [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) for hello storage caps of hello different Premium service tiers.</span></span>

<span data-ttu-id="919a2-110">Stimare la memoria, i requisiti per una tabella con ottimizzazione per la memoria funziona hello stesso modo per SQL Server come avviene in Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="919a2-110">Estimating memory requirements for a memory-optimized table works hello same way for SQL Server as it does in Azure SQL Database.</span></span> <span data-ttu-id="919a2-111">Richiedere alcuni minuti tooreview tale argomento [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span><span class="sxs-lookup"><span data-stu-id="919a2-111">Take a few minutes tooreview that topic on [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span></span>

<span data-ttu-id="919a2-112">Si noti che nella tabella hello e righe variabile di tabella, nonché gli indici, conteggiati per dimensioni dei dati utente max hello.</span><span class="sxs-lookup"><span data-stu-id="919a2-112">Note that hello table and table variable rows, as well as indexes, count toward hello max user data size.</span></span> <span data-ttu-id="919a2-113">Inoltre, ALTER TABLE è necessario sufficiente toocreate chat una nuova versione dell'intera tabella hello e i relativi indici.</span><span class="sxs-lookup"><span data-stu-id="919a2-113">In addition, ALTER TABLE needs enough room toocreate a new version of hello entire table and its indexes.</span></span>

## <a name="monitoring-and-alerting"></a><span data-ttu-id="919a2-114">Monitoraggio e avviso</span><span class="sxs-lookup"><span data-stu-id="919a2-114">Monitoring and alerting</span></span>
<span data-ttu-id="919a2-115">È possibile monitorare l'utilizzo di archiviazione in memoria come una percentuale di hello [il limite di archiviazione per il livello di prestazioni](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) in hello Azure [portale](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="919a2-115">You can monitor in-memory storage use as a percentage of hello [storage cap for your performance tier](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) in hello Azure [portal](https://portal.azure.com/):</span></span> 

* <span data-ttu-id="919a2-116">Nel pannello Database hello, individuare hello risorse utilizzo casella e fare clic su Modifica.</span><span class="sxs-lookup"><span data-stu-id="919a2-116">On hello Database blade, locate hello Resource utilization box and click on Edit.</span></span>
* <span data-ttu-id="919a2-117">Quindi selezionare la metrica hello `In-Memory OLTP Storage percentage`.</span><span class="sxs-lookup"><span data-stu-id="919a2-117">Then select hello metric `In-Memory OLTP Storage percentage`.</span></span>
* <span data-ttu-id="919a2-118">tooadd un avviso, fare clic su Pannello metriche di hello utilizzo delle risorse casella tooopen hello, quindi fare clic su Aggiungi avviso.</span><span class="sxs-lookup"><span data-stu-id="919a2-118">tooadd an alert, click on hello Resource Utilization box tooopen hello Metric blade, then click on Add alert.</span></span>

<span data-ttu-id="919a2-119">In alternativa utilizzare hello dopo l'utilizzo di archiviazione in memoria hello tooshow query:</span><span class="sxs-lookup"><span data-stu-id="919a2-119">Or use hello following query tooshow hello in-memory storage utilization:</span></span>

    SELECT xtp_storage_percent FROM sys.dm_db_resource_stats


## <a name="correct-out-of-memory-situations---error-41823"></a><span data-ttu-id="919a2-120">Correggere le situazioni di memoria insufficiente - Errore 41823</span><span class="sxs-lookup"><span data-stu-id="919a2-120">Correct out-of-memory situations - Error 41823</span></span>
<span data-ttu-id="919a2-121">Se la memoria è insufficiente, le operazioni INSERISCI, AGGIORNA e CREA avranno esito negativo con messaggio di errore 41823.</span><span class="sxs-lookup"><span data-stu-id="919a2-121">Running out-of-memory results in INSERT, UPDATE, and CREATE operations failing with error message 41823.</span></span>

<span data-ttu-id="919a2-122">Messaggio di errore 41823 indica che le tabelle con ottimizzazione per la memoria hello e variabili di tabella hanno superato la dimensione massima di hello.</span><span class="sxs-lookup"><span data-stu-id="919a2-122">Error message 41823 indicates that hello memory-optimized tables and table variables have exceeded hello maximum size.</span></span>

<span data-ttu-id="919a2-123">tooresolve questo errore, entrambi:</span><span class="sxs-lookup"><span data-stu-id="919a2-123">tooresolve this error, either:</span></span>

* <span data-ttu-id="919a2-124">Eliminare i dati da tabelle con ottimizzazione per la memoria hello, potenzialmente offload hello dati tootraditional, tabelle basate su disco. In alternativa,</span><span class="sxs-lookup"><span data-stu-id="919a2-124">Delete data from hello memory-optimized tables, potentially offloading hello data tootraditional, disk-based tables; or,</span></span>
* <span data-ttu-id="919a2-125">Aggiornare hello servizio livello tooone con sufficiente spazio di archiviazione in memoria per i dati di hello è necessario tookeep nelle tabelle con ottimizzazione per la memoria.</span><span class="sxs-lookup"><span data-stu-id="919a2-125">Upgrade hello service tier tooone with enough in-memory storage for hello data you need tookeep in memory-optimized tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="919a2-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="919a2-126">Next steps</span></span>
<span data-ttu-id="919a2-127">Per le linee guida sul monitoraggio, vedere [Monitoraggio del database SQL di Azure tramite le visualizzazioni di gestione dinamica](sql-database-monitoring-with-dmvs.md).</span><span class="sxs-lookup"><span data-stu-id="919a2-127">For monitoring guidance, see [Monitoring Azure SQL Database using dynamic management views](sql-database-monitoring-with-dmvs.md).</span></span>
