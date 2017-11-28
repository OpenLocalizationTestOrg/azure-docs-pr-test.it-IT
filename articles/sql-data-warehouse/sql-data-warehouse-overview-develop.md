---
title: aaaResources per lo sviluppo di un data warehouse di Azure | Documenti Microsoft
description: Concetti di sviluppo, decisioni di progettazione, suggerimenti e tecniche di codifica per SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: barbkess
editor: 
ms.assetid: 996e3afc-c21c-4e21-b9df-997f953f6dfd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: develop
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 67e3a6a3e2664919c3445ea5d5eba251054de020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="design-decisions-and-coding-techniques-for-sql-data-warehouse"></a><span data-ttu-id="03d63-103">Decisioni di progettazione e tecniche di codifica per SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="03d63-103">Design decisions and coding techniques for SQL Data Warehouse</span></span>
<span data-ttu-id="03d63-104">Esaminare gli articoli di sviluppo toobetter comprendere principali decisioni di progettazione, suggerimenti e tecniche per SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="03d63-104">Take a look through these development articles toobetter understand key design decisions, recommendations and coding techniques for SQL Data Warehouse.</span></span>

## <a name="key-design-decisions"></a><span data-ttu-id="03d63-105">Decisioni chiave nella progettazione</span><span class="sxs-lookup"><span data-stu-id="03d63-105">Key design decisions</span></span>
<span data-ttu-id="03d63-106">Hello articoli seguenti evidenziano alcuni dei concetti chiave hello e sulle decisioni di progettazione, che sarà necessario toounderstand per lo sviluppo di hello della warehouse dati distribuiti tramite SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="03d63-106">hello following articles highlight some of hello key concepts and design decisions you will need toounderstand for hello development of your distributed data warehouse using SQL Data Warehouse:</span></span>

* <span data-ttu-id="03d63-107">[connessioni][connections]</span><span class="sxs-lookup"><span data-stu-id="03d63-107">[connections][connections]</span></span>
* <span data-ttu-id="03d63-108">[concorrenza][concurrency]</span><span class="sxs-lookup"><span data-stu-id="03d63-108">[concurrency][concurrency]</span></span>
* <span data-ttu-id="03d63-109">[transazioni][transactions]</span><span class="sxs-lookup"><span data-stu-id="03d63-109">[transactions][transactions]</span></span>
* <span data-ttu-id="03d63-110">[schemi definiti dall'utente][user-defined schemas]</span><span class="sxs-lookup"><span data-stu-id="03d63-110">[user-defined schemas][user-defined schemas]</span></span>
* <span data-ttu-id="03d63-111">[distribuzione di tabelle][table distribution]</span><span class="sxs-lookup"><span data-stu-id="03d63-111">[table distribution][table distribution]</span></span>
* <span data-ttu-id="03d63-112">[indici di tabella][table indexes]</span><span class="sxs-lookup"><span data-stu-id="03d63-112">[table indexes][table indexes]</span></span>
* <span data-ttu-id="03d63-113">[partizioni di tabella][table partitions]</span><span class="sxs-lookup"><span data-stu-id="03d63-113">[table partitions][table partitions]</span></span>
* <span data-ttu-id="03d63-114">[CTAS][CTAS]</span><span class="sxs-lookup"><span data-stu-id="03d63-114">[CTAS][CTAS]</span></span>
* <span data-ttu-id="03d63-115">[statistiche][statistics]</span><span class="sxs-lookup"><span data-stu-id="03d63-115">[statistics][statistics]</span></span>

## <a name="development-recommendations-and-coding-techniques"></a><span data-ttu-id="03d63-116">Sviluppo dei suggerimenti e delle tecniche di codifica</span><span class="sxs-lookup"><span data-stu-id="03d63-116">Development recommendations and coding techniques</span></span>
<span data-ttu-id="03d63-117">Questi articoli illustrano le tecniche di codifica, i consigli e i suggerimenti consigliate specifici per lo sviluppo dell’SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="03d63-117">These articles highlight specific coding techniques, tips and recommendations for developing your SQL Data Warehouse:</span></span>

* <span data-ttu-id="03d63-118">[stored procedure][stored procedures]</span><span class="sxs-lookup"><span data-stu-id="03d63-118">[stored procedures][stored procedures]</span></span>
* <span data-ttu-id="03d63-119">[etichette][labels]</span><span class="sxs-lookup"><span data-stu-id="03d63-119">[labels][labels]</span></span>
* <span data-ttu-id="03d63-120">[viste][views]</span><span class="sxs-lookup"><span data-stu-id="03d63-120">[views][views]</span></span>
* <span data-ttu-id="03d63-121">[tabelle temporanee][temporary tables]</span><span class="sxs-lookup"><span data-stu-id="03d63-121">[temporary tables][temporary tables]</span></span>
* <span data-ttu-id="03d63-122">[SQL dinamico][dynamic SQL]</span><span class="sxs-lookup"><span data-stu-id="03d63-122">[dynamic SQL][dynamic SQL]</span></span>
* <span data-ttu-id="03d63-123">[cicli][looping]</span><span class="sxs-lookup"><span data-stu-id="03d63-123">[looping][looping]</span></span>
* <span data-ttu-id="03d63-124">[opzioni di raggruppamento][group by options]</span><span class="sxs-lookup"><span data-stu-id="03d63-124">[group by options][group by options]</span></span>
* <span data-ttu-id="03d63-125">[assegnazione di variabili][variable assignment]</span><span class="sxs-lookup"><span data-stu-id="03d63-125">[variable assignment][variable assignment]</span></span>

## <a name="next-steps"></a><span data-ttu-id="03d63-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="03d63-126">Next steps</span></span>
<span data-ttu-id="03d63-127">Dopo aver attraverso gli articoli di sviluppo hello esaminare hello [riferimento a Transact-SQL] [ Transact-SQL reference] per ulteriori informazioni sulla sintassi di hello è supportato per SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="03d63-127">Once you have been through hello development articles take a look through hello [Transact-SQL reference][Transact-SQL reference] page for more details on hello supported syntax for SQL Data Warehouse.</span></span>

<!--Image references-->

<!--Article references-->
[concurrency]: ./sql-data-warehouse-develop-concurrency.md
[connections]: ./sql-data-warehouse-connect-overview.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[dynamic SQL]: ./sql-data-warehouse-develop-dynamic-sql.md
[group by options]: ./sql-data-warehouse-develop-group-by-options.md
[labels]: ./sql-data-warehouse-develop-label.md
[looping]: ./sql-data-warehouse-develop-loops.md
[statistics]: ./sql-data-warehouse-tables-statistics.md
[stored procedures]: ./sql-data-warehouse-develop-stored-procedures.md
[table distribution]: ./sql-data-warehouse-tables-distribute.md
[table indexes]: ./sql-data-warehouse-tables-index.md
[table partitions]: ./sql-data-warehouse-tables-partition.md
[temporary tables]: ./sql-data-warehouse-tables-temporary.md
[transactions]: ./sql-data-warehouse-develop-transactions.md
[user-defined schemas]: ./sql-data-warehouse-develop-user-defined-schemas.md
[variable assignment]: ./sql-data-warehouse-develop-variable-assignment.md
[views]: ./sql-data-warehouse-develop-views.md
[Transact-SQL reference]: ./sql-data-warehouse-overview-reference.md

<!--MSDN references-->
[renaming objects]: https://msdn.microsoft.com/library/mt631611.aspx

<!--Other Web references-->
