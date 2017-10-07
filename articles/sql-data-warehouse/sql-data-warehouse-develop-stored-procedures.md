---
title: aaaStored procedure in SQL Data Warehouse | Documenti Microsoft
description: Suggerimenti per l'implementazione delle stored procedure in Azure SQL Data Warehouse per lo sviluppo di soluzioni.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 9b238789-6efe-4820-bf77-5a5da2afa0e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 416252dd3dea95c66aa5e886860b933b22578002
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="stored-procedures-in-sql-data-warehouse"></a>Stored procedure in SQL Data Warehouse
SQL Data Warehouse supporta molte delle funzionalità di Transact-SQL hello disponibili in SQL Server. Non esistono ancora più importante funzionalità specifiche che vogliamo delle prestazioni di hello toomaximize tooleverage della soluzione di scalabilità.

Scala hello toomaintain e le prestazioni di SQL Data Warehouse sono sono tuttavia anche alcune caratteristiche e funzionalità con differenze di comportamento e ad altri utenti che non sono supportati.

Questo articolo spiega come tooimplement stored procedure all'interno di SQL Data Warehouse.

## <a name="introducing-stored-procedures"></a>Introduzione alle stored procedure
Stored procedure sono un ottimo modo per incapsulare il codice SQL; archiviazione dati tooyour Chiudi nel data warehouse di hello. Incapsulando codice hello in unità gestibili stored procedure consentono agli sviluppatori di modularizzare le relative soluzioni; semplificazione di maggiore riutilizzo del codice. Ogni stored procedure può anche accettare parametri toomake li ancora più flessibile.

SQL Data Warehouse fornisce un'implementazione semplificata e ottimizzata delle stored procedure. Hello più grande differenza rispetto tooSQL Server è che hello stored procedure non è codice precompilato. In data warehouse di Microsoft è in genere meno interessati alla fase di compilazione hello. È più importante che hello stored procedure codice è ottimizzato in modo corretto quando si lavora con grandi volumi di dati. obiettivo di Hello è toosave ore, minuti e secondi non millisecondi. È pertanto toothink più utili di stored procedure come contenitori per la logica di SQL.     

Quando viene eseguito SQL Data Warehouse istruzioni SQL hello stored procedure vengono analizzate, convertire e ottimizzate in fase di esecuzione. Durante questo processo, ogni istruzione viene convertita in query distribuite. il codice SQL che viene effettivamente eseguito su dati hello Hello è toohello diverse query inviata.

## <a name="nesting-stored-procedures"></a>Annidamento di stored procedure
Quando le stored procedure chiamano altre stored procedure o eseguono istruzioni sql dinamiche, quindi interna hello o la stored procedure chiamata di codice viene definita toobe annidati.

SQL Data Warehouse supporta un massimo di 8 livelli di annidamento. Si tratta di tooSQL leggermente diversi Server. livello di nidificazione Hello in SQL Server è 32.

chiamata di livello superiore da stored procedure Hello equivale toonest livello 1

```sql
EXEC prc_nesting
```
Se hello stored procedure effettua inoltre EXEC un'altra chiamata, ciò comporta un aumento too2 livello di nidificazione hello

```sql
CREATE PROCEDURE prc_nesting
AS
EXEC prc_nesting_2  -- This call is nest level 2
GO
EXEC prc_nesting
```
Se seconda procedura hello viene quindi eseguito alcune istruzioni sql dinamiche quindi aumenterà too3 livello di nidificazione hello

```sql
CREATE PROCEDURE prc_nesting_2
AS
EXEC sp_executesql 'SELECT 'another nest level'  -- This call is nest level 2
GO
EXEC prc_nesting
```

Tenere presente che SQL Data Warehouse attualmente non supporta @@NESTLEVEL. È necessario tookeep una traccia del livello di nidificazione manualmente. È improbabile che verrà raggiunto limite del livello di nidificazione hello 8, ma se non si sarà anche necessario toore lavoro il codice e "convertirla" in modo da adattarlo entro tale limite.

## <a name="insertexecute"></a>INSERT..EXECUTE
SQL Data Warehouse non consentono di set di risultati hello tooconsume di una stored procedure con un'istruzione INSERT. Si può tuttavia un approccio alternativo.

Vedere l'articolo seguente toohello [tabelle temporanee] per un esempio su come toodo questo.

## <a name="limitations"></a>Limitazioni
Esistono alcuni aspetti delle stored procedure Transact-SQL che non sono implementate in SQL Data Warehouse.

Sono:

* Stored procedure temporanee
* Stored procedure numerate
* Stored procedure estese
* Stored procedure CLR
* Opzione di crittografia
* Opzione di replica
* Parametri con valori di tabella
* Parametri di sola lettura
* Parametri predefiniti
* Contesti di esecuzione
* Istruzione return

## <a name="next-steps"></a>Passaggi successivi
Per altri suggerimenti sullo sviluppo, vedere la [panoramica dello sviluppo][development overview].

<!--Image references-->

<!--Article references-->
[tabelle temporanee]: ./sql-data-warehouse-tables-temporary.md#modularizing-code
[development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[nest level]: https://msdn.microsoft.com/library/ms187371.aspx

<!--Other Web references-->
