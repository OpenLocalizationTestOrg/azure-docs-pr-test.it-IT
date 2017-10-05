---
title: Risorse per lo sviluppo di un data warehouse in Azure | Documentazione Microsoft
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
ms.openlocfilehash: b85a4f09e561e429aa5bf46ec680014487fb40c7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="design-decisions-and-coding-techniques-for-sql-data-warehouse"></a><span data-ttu-id="c2f3a-103">Decisioni di progettazione e tecniche di codifica per SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c2f3a-103">Design decisions and coding techniques for SQL Data Warehouse</span></span>
<span data-ttu-id="c2f3a-104">Esaminare questi articoli sullo sviluppo per capire meglio le decisioni chiave nella progettazione, i suggerimenti e le tecniche di codifica per SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c2f3a-104">Take a look through these development articles to better understand key design decisions, recommendations and coding techniques for SQL Data Warehouse.</span></span>

## <a name="key-design-decisions"></a><span data-ttu-id="c2f3a-105">Decisioni chiave nella progettazione</span><span class="sxs-lookup"><span data-stu-id="c2f3a-105">Key design decisions</span></span>
<span data-ttu-id="c2f3a-106">Gli articoli seguenti illustrano alcuni dei concetti chiave e alcune delle decisioni di progettazione che sarà necessario conoscere per lo sviluppo del data warehouse distribuito tramite SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="c2f3a-106">The following articles highlight some of the key concepts and design decisions you will need to understand for the development of your distributed data warehouse using SQL Data Warehouse:</span></span>

* <span data-ttu-id="c2f3a-107">[connessioni][connections]</span><span class="sxs-lookup"><span data-stu-id="c2f3a-107">[connections][connections]</span></span>
* <span data-ttu-id="c2f3a-108">[concorrenza][concurrency]</span><span class="sxs-lookup"><span data-stu-id="c2f3a-108">[concurrency][concurrency]</span></span>
* <span data-ttu-id="c2f3a-109">[transazioni][transactions]</span><span class="sxs-lookup"><span data-stu-id="c2f3a-109">[transactions][transactions]</span></span>
* <span data-ttu-id="c2f3a-110">[schemi definiti dall'utente][user-defined schemas]</span><span class="sxs-lookup"><span data-stu-id="c2f3a-110">[user-defined schemas][user-defined schemas]</span></span>
* <span data-ttu-id="c2f3a-111">[distribuzione di tabelle][table distribution]</span><span class="sxs-lookup"><span data-stu-id="c2f3a-111">[table distribution][table distribution]</span></span>
* <span data-ttu-id="c2f3a-112">[indici di tabella][table indexes]</span><span class="sxs-lookup"><span data-stu-id="c2f3a-112">[table indexes][table indexes]</span></span>
* <span data-ttu-id="c2f3a-113">[partizioni di tabella][table partitions]</span><span class="sxs-lookup"><span data-stu-id="c2f3a-113">[table partitions][table partitions]</span></span>
* <span data-ttu-id="c2f3a-114">[CTAS][CTAS]</span><span class="sxs-lookup"><span data-stu-id="c2f3a-114">[CTAS][CTAS]</span></span>
* <span data-ttu-id="c2f3a-115">[statistiche][statistics]</span><span class="sxs-lookup"><span data-stu-id="c2f3a-115">[statistics][statistics]</span></span>

## <a name="development-recommendations-and-coding-techniques"></a><span data-ttu-id="c2f3a-116">Sviluppo dei suggerimenti e delle tecniche di codifica</span><span class="sxs-lookup"><span data-stu-id="c2f3a-116">Development recommendations and coding techniques</span></span>
<span data-ttu-id="c2f3a-117">Questi articoli illustrano le tecniche di codifica, i consigli e i suggerimenti consigliate specifici per lo sviluppo dell’SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="c2f3a-117">These articles highlight specific coding techniques, tips and recommendations for developing your SQL Data Warehouse:</span></span>

* <span data-ttu-id="c2f3a-118">[stored procedure][stored procedures]</span><span class="sxs-lookup"><span data-stu-id="c2f3a-118">[stored procedures][stored procedures]</span></span>
* <span data-ttu-id="c2f3a-119">[etichette][labels]</span><span class="sxs-lookup"><span data-stu-id="c2f3a-119">[labels][labels]</span></span>
* <span data-ttu-id="c2f3a-120">[viste][views]</span><span class="sxs-lookup"><span data-stu-id="c2f3a-120">[views][views]</span></span>
* <span data-ttu-id="c2f3a-121">[tabelle temporanee][temporary tables]</span><span class="sxs-lookup"><span data-stu-id="c2f3a-121">[temporary tables][temporary tables]</span></span>
* <span data-ttu-id="c2f3a-122">[SQL dinamico][dynamic SQL]</span><span class="sxs-lookup"><span data-stu-id="c2f3a-122">[dynamic SQL][dynamic SQL]</span></span>
* <span data-ttu-id="c2f3a-123">[cicli][looping]</span><span class="sxs-lookup"><span data-stu-id="c2f3a-123">[looping][looping]</span></span>
* <span data-ttu-id="c2f3a-124">[opzioni di raggruppamento][group by options]</span><span class="sxs-lookup"><span data-stu-id="c2f3a-124">[group by options][group by options]</span></span>
* <span data-ttu-id="c2f3a-125">[assegnazione di variabili][variable assignment]</span><span class="sxs-lookup"><span data-stu-id="c2f3a-125">[variable assignment][variable assignment]</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2f3a-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c2f3a-126">Next steps</span></span>
<span data-ttu-id="c2f3a-127">Dopo aver letto gli articoli sullo sviluppo, esaminare la pagina relativa agli [argomenti di riferimento per Transact-SQL][Transact-SQL reference] per altri dettagli sulla sintassi supportata per SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c2f3a-127">Once you have been through the development articles take a look through the [Transact-SQL reference][Transact-SQL reference] page for more details on the supported syntax for SQL Data Warehouse.</span></span>

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
