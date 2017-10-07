---
title: le variabili aaaAssign in SQL Data Warehouse | Documenti Microsoft
description: Suggerimenti per l'assegnazione di variabili Transact-SQL in Azure SQL Data Warehouse per lo sviluppo di soluzioni.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 81ddc7cf-a6ba-4585-91a3-b6ea50f49227
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 9de48739bb0af80ff2a117704b31512c680f78d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="assign-variables-in-sql-data-warehouse"></a>Assegnare variabili in SQL Data Warehouse
Le variabili in SQL Data Warehouse vengono impostate utilizzando hello `DECLARE` istruzione o hello `SET` istruzione.

Tutti hello seguenti sono validi perfettamente tooset un valore della variabile:

## <a name="setting-variables-with-declare"></a>Impostazione delle variabili con DECLARE
Inizializzazione di variabili con DECLARE è uno dei hello più flessibile modi tooset un valore della variabile in SQL Data Warehouse.

```sql
DECLARE @v  int = 0
;
```

È inoltre possibile utilizzare DECLARE tooset più di una variabile alla volta. Non è possibile utilizzare `SELECT` o `UPDATE` toodo questo:

```sql
DECLARE @v  INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Smith')
,       @v1 INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Jones')
;
```

Non è possibile inizializzare e utilizzare una variabile in hello stessa istruzione DECLARE. tooillustrate hello punto hello esempio riportato di seguito è **non** consentito come @p1 sia inizializzata e utilizzato in hello stessa istruzione DECLARE. Ciò comporterà un errore.

```sql
DECLARE @p1 int = 0
,       @p2 int = (SELECT COUNT (*) FROM sys.types where is_user_defined = @p1 )
;
```

## <a name="setting-values-with-set"></a>Impostazione di valori con SET
Set è un metodo molto comune per l'impostazione di una singola variabile.

Tutti gli esempi di hello riportato di seguito sono validi dell'impostazione di una variabile con SET:

```sql
SET     @v = (Select max(database_id) from sys.databases);
SET     @v = 1;
SET     @v = @v+1;
SET     @v +=1;
```

È possibile impostare una sola variabile alla volta con SET. Tuttavia, come illustrato sopra, gli operatori composti sono consentiti.

## <a name="limitations"></a>Limitazioni
Non è possibile usare SELECT o UPDATE per l'assegnazione di variabili.

## <a name="next-steps"></a>Passaggi successivi
Per altri suggerimenti sullo sviluppo, vedere la [panoramica dello sviluppo][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
