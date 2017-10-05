---
title: Monitorare l'archiviazione in memoria XTP | Documentazione Microsoft
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
ms.openlocfilehash: 5afb2209f18b1ba2aa0a916a439509b01afd80da
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-in-memory-oltp-storage"></a><span data-ttu-id="51bae-103">Monitorare l'archiviazione OLTP in memoria</span><span class="sxs-lookup"><span data-stu-id="51bae-103">Monitor In-Memory OLTP Storage</span></span>
<span data-ttu-id="51bae-104">Quando si usa [OLTP in memoria](sql-database-in-memory.md), i dati nelle tabelle con ottimizzazione per la memoria e le variabili di tabella si trovano nell'archiviazione OLTP in memoria.</span><span class="sxs-lookup"><span data-stu-id="51bae-104">When using [In-Memory OLTP](sql-database-in-memory.md), data in memory-optimized tables and table variables resides in In-Memory OLTP storage.</span></span> <span data-ttu-id="51bae-105">Ogni livello di servizio Premium ha dimensioni di archiviazione OLTP in memoria massime documentate nell'articolo [Livelli di servizio del database SQL](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span><span class="sxs-lookup"><span data-stu-id="51bae-105">Each Premium service tier has a maximum In-Memory OLTP storage size, which is documented in the [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span></span> <span data-ttu-id="51bae-106">Dopo il superamento di questo limite, è possibile che le operazioni di inserimento e aggiornamento abbiano esito negativo con errore 41823.</span><span class="sxs-lookup"><span data-stu-id="51bae-106">Once this limit is exceeded, insert and update operations may start failing (with error 41823).</span></span> <span data-ttu-id="51bae-107">Sarà quindi necessario eliminare dati per recuperare memoria oppure aggiornare il livello di prestazioni del database.</span><span class="sxs-lookup"><span data-stu-id="51bae-107">At that point you will need to either delete data to reclaim memory, or upgrade the performance tier of your database.</span></span>

## <a name="determine-whether-data-will-fit-within-the-in-memory-storage-cap"></a><span data-ttu-id="51bae-108">Determinare se i dati rientreranno nel limite di archiviazione in memoria</span><span class="sxs-lookup"><span data-stu-id="51bae-108">Determine whether data will fit within the in-memory storage cap</span></span>
<span data-ttu-id="51bae-109">Determinare il limite di archiviazione: consultare l'articolo [Livelli di servizio del database SQL](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) per informazioni sui limiti di archiviazione dei diversi livelli di servizio Premium.</span><span class="sxs-lookup"><span data-stu-id="51bae-109">Determine the storage cap: consult the [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) for the storage caps of the different Premium service tiers.</span></span>

<span data-ttu-id="51bae-110">La stima dei requisiti di memoria per una tabella con ottimizzazione per la memoria in SQL Server è analoga alla stima eseguita nel database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="51bae-110">Estimating memory requirements for a memory-optimized table works the same way for SQL Server as it does in Azure SQL Database.</span></span> <span data-ttu-id="51bae-111">È consigliabile rivedere l'argomento corrispondente su [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span><span class="sxs-lookup"><span data-stu-id="51bae-111">Take a few minutes to review that topic on [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span></span>

<span data-ttu-id="51bae-112">Si noti che la tabella e le righe di variabili tabella, oltre agli indici, vengono incluse nel calcolo delle dimensioni massime dei dati utente.</span><span class="sxs-lookup"><span data-stu-id="51bae-112">Note that the table and table variable rows, as well as indexes, count toward the max user data size.</span></span> <span data-ttu-id="51bae-113">ALTER TABLE, inoltre, necessita di spazio sufficiente per creare una nuova versione dell'intera tabella e dei relativi indici.</span><span class="sxs-lookup"><span data-stu-id="51bae-113">In addition, ALTER TABLE needs enough room to create a new version of the entire table and its indexes.</span></span>

## <a name="monitoring-and-alerting"></a><span data-ttu-id="51bae-114">Monitoraggio e avviso</span><span class="sxs-lookup"><span data-stu-id="51bae-114">Monitoring and alerting</span></span>
<span data-ttu-id="51bae-115">È possibile monitorare l'uso dell'archiviazione in memoria come percentuale del [limite di archiviazione per il livello di prestazioni](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) nel [portale](https://portal.azure.com/) di Azure:</span><span class="sxs-lookup"><span data-stu-id="51bae-115">You can monitor in-memory storage use as a percentage of the [storage cap for your performance tier](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) in the Azure [portal](https://portal.azure.com/):</span></span> 

* <span data-ttu-id="51bae-116">Nel pannello Database individuare la casella Utilizzo risorse e fare clic su Modifica.</span><span class="sxs-lookup"><span data-stu-id="51bae-116">On the Database blade, locate the Resource utilization box and click on Edit.</span></span>
* <span data-ttu-id="51bae-117">Quindi selezionare la metrica `In-Memory OLTP Storage percentage`.</span><span class="sxs-lookup"><span data-stu-id="51bae-117">Then select the metric `In-Memory OLTP Storage percentage`.</span></span>
* <span data-ttu-id="51bae-118">Per aggiungere un avviso, selezionare la casella Utilizzo risorse per aprire il pannello Metrica, quindi fare clic su Aggiungi avviso.</span><span class="sxs-lookup"><span data-stu-id="51bae-118">To add an alert, click on the Resource Utilization box to open the Metric blade, then click on Add alert.</span></span>

<span data-ttu-id="51bae-119">In alternativa, usare la query seguente per visualizzare l'utilizzo delle risorse di archiviazione in memoria:</span><span class="sxs-lookup"><span data-stu-id="51bae-119">Or use the following query to show the in-memory storage utilization:</span></span>

    SELECT xtp_storage_percent FROM sys.dm_db_resource_stats


## <a name="correct-out-of-memory-situations---error-41823"></a><span data-ttu-id="51bae-120">Correggere le situazioni di memoria insufficiente - Errore 41823</span><span class="sxs-lookup"><span data-stu-id="51bae-120">Correct out-of-memory situations - Error 41823</span></span>
<span data-ttu-id="51bae-121">Se la memoria è insufficiente, le operazioni INSERISCI, AGGIORNA e CREA avranno esito negativo con messaggio di errore 41823.</span><span class="sxs-lookup"><span data-stu-id="51bae-121">Running out-of-memory results in INSERT, UPDATE, and CREATE operations failing with error message 41823.</span></span>

<span data-ttu-id="51bae-122">Il messaggio di errore 41823 indica che le tabelle con ottimizzazione per la memoria e le variabili tabella hanno superato le dimensioni massime.</span><span class="sxs-lookup"><span data-stu-id="51bae-122">Error message 41823 indicates that the memory-optimized tables and table variables have exceeded the maximum size.</span></span>

<span data-ttu-id="51bae-123">Per risolvere l'errore:</span><span class="sxs-lookup"><span data-stu-id="51bae-123">To resolve this error, either:</span></span>

* <span data-ttu-id="51bae-124">Eliminare i dati dalle tabelle con ottimizzazione per la memoria, eseguendo potenzialmente l'offload dei dati in tabelle tradizionali basate su disco oppure</span><span class="sxs-lookup"><span data-stu-id="51bae-124">Delete data from the memory-optimized tables, potentially offloading the data to traditional, disk-based tables; or,</span></span>
* <span data-ttu-id="51bae-125">Aggiornare il livello di servizio selezionandone uno con risorse di archiviazione in memoria sufficienti per i dati da mantenere nelle tabelle con ottimizzazione con memoria.</span><span class="sxs-lookup"><span data-stu-id="51bae-125">Upgrade the service tier to one with enough in-memory storage for the data you need to keep in memory-optimized tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="51bae-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="51bae-126">Next steps</span></span>
<span data-ttu-id="51bae-127">Per le linee guida sul monitoraggio, vedere [Monitoraggio del database SQL di Azure tramite le visualizzazioni di gestione dinamica](sql-database-monitoring-with-dmvs.md).</span><span class="sxs-lookup"><span data-stu-id="51bae-127">For monitoring guidance, see [Monitoring Azure SQL Database using dynamic management views](sql-database-monitoring-with-dmvs.md).</span></span>
