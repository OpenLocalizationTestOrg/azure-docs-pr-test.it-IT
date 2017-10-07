---
title: aaaLeverage cicli di T-SQL in Azure SQL Data Warehouse | Documenti Microsoft
description: Suggerimenti sui di cicli Transact-SQL e sulla sostituzione di cursori in Azure SQL Data Warehouse per lo sviluppo di soluzioni.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: f3384b81-b943-431b-bc73-90e47e4c195f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: c7e8f71b910d00d0dfc30f6e5eba190fd05014b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="loops-in-sql-data-warehouse"></a>Cicli in SQL Data Warehouse
SQL Data Warehouse supporta hello [mentre][mentre] ciclo per eseguire ripetutamente blocchi di istruzioni. Questa operazione continuerà per purché hello specificato le condizioni sono true o fino al codice hello termina in modo specifico il ciclo di hello utilizzando hello `BREAK` (parola chiave). I cicli sono particolarmente utili per la sostituzione di cursori definiti nel codice SQL. Fortunatamente, quasi tutti i cursori vengono scritti nel codice SQL sono di hello veloce in avanti, leggere solo diversi. Pertanto [mentre] cicli sono un'ottima alternativa se è necessario avere tooreplace uno.

## <a name="leveraging-loops-and-replacing-cursors-in-sql-data-warehouse"></a>Uso di cicli e sostituzione di cursori in SQL Data Warehouse
Tuttavia, prima di approfondire ulteriormente head innanzitutto è necessario valutare hello seguenti domande: "il cursore può essere riscritto toouse operazioni basate su set?". In molti casi risposte hello saranno Sì ed sono spesso consigliabile hello. Un'operazione basata su set viene spesso eseguita molto più velocemente rispetto a un approccio iterativo riga per riga.

I cursori ad avanzamento rapido di sola lettura possono essere facilmente sostituiti con un costrutto di ciclo. Un semplice esempio viene riportato di seguito: Questo esempio di codice aggiorna le statistiche di hello per ogni tabella nel database di hello. Scorrendo tabelle hello in ciclo hello è è in grado di tooexecute ogni comando in sequenza.

Creare innanzitutto una tabella temporanea contenente una riga univoca numero usato tooidentify hello singole istruzioni:

```
CREATE TABLE #tbl
WITH
( DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT  ROW_NUMBER() OVER(ORDER BY (SELECT NULL)) AS Sequence
,       [name]
,       'UPDATE STATISTICS '+QUOTENAME([name]) AS sql_code
FROM    sys.tables
;
```

In secondo luogo, inizializzare il ciclo di hello hello variabili tooperform necessarie:

```
DECLARE @nbr_statements INT = (SELECT COUNT(*) FROM #tbl)
,       @i INT = 1
;
```

Ora eseguire un ciclo delle istruzioni, una alla volta:

```
WHILE   @i <= @nbr_statements
BEGIN
    DECLARE @sql_code NVARCHAR(4000) = (SELECT sql_code FROM #tbl WHERE Sequence = @i);
    EXEC    sp_executesql @sql_code;
    SET     @i +=1;
END
```

Infine Elimina tabella temporanea di hello creata nel primo passaggio hello

```
DROP TABLE #tbl;
```


<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a>Passaggi successivi
Per altri suggerimenti sullo sviluppo, vedere la [panoramica dello sviluppo][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[mentre]: https://msdn.microsoft.com/library/ms178642.aspx


<!--Other Web references-->
