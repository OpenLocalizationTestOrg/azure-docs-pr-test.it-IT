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
# <a name="design-decisions-and-coding-techniques-for-sql-data-warehouse"></a>Decisioni di progettazione e tecniche di codifica per SQL Data Warehouse
Esaminare gli articoli di sviluppo toobetter comprendere principali decisioni di progettazione, suggerimenti e tecniche per SQL Data Warehouse.

## <a name="key-design-decisions"></a>Decisioni chiave nella progettazione
Hello articoli seguenti evidenziano alcuni dei concetti chiave hello e sulle decisioni di progettazione, che sarà necessario toounderstand per lo sviluppo di hello della warehouse dati distribuiti tramite SQL Data Warehouse:

* [connessioni][connections]
* [concorrenza][concurrency]
* [transazioni][transactions]
* [schemi definiti dall'utente][user-defined schemas]
* [distribuzione di tabelle][table distribution]
* [indici di tabella][table indexes]
* [partizioni di tabella][table partitions]
* [CTAS][CTAS]
* [statistiche][statistics]

## <a name="development-recommendations-and-coding-techniques"></a>Sviluppo dei suggerimenti e delle tecniche di codifica
Questi articoli illustrano le tecniche di codifica, i consigli e i suggerimenti consigliate specifici per lo sviluppo dell’SQL Data Warehouse:

* [stored procedure][stored procedures]
* [etichette][labels]
* [viste][views]
* [tabelle temporanee][temporary tables]
* [SQL dinamico][dynamic SQL]
* [cicli][looping]
* [opzioni di raggruppamento][group by options]
* [assegnazione di variabili][variable assignment]

## <a name="next-steps"></a>Passaggi successivi
Dopo aver attraverso gli articoli di sviluppo hello esaminare hello [riferimento a Transact-SQL] [ Transact-SQL reference] per ulteriori informazioni sulla sintassi di hello è supportato per SQL Data Warehouse.

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
