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
# <a name="loops-in-sql-data-warehouse"></a><span data-ttu-id="270cf-103">Cicli in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="270cf-103">Loops in SQL Data Warehouse</span></span>
<span data-ttu-id="270cf-104">SQL Data Warehouse supporta hello [mentre][mentre] ciclo per eseguire ripetutamente blocchi di istruzioni.</span><span class="sxs-lookup"><span data-stu-id="270cf-104">SQL Data Warehouse supports hello [WHILE][WHILE] loop for repeatedly executing statement blocks.</span></span> <span data-ttu-id="270cf-105">Questa operazione continuerà per purché hello specificato le condizioni sono true o fino al codice hello termina in modo specifico il ciclo di hello utilizzando hello `BREAK` (parola chiave).</span><span class="sxs-lookup"><span data-stu-id="270cf-105">This will continue for as long as hello specified conditions are true or until hello code specifically terminates hello loop using hello `BREAK` keyword.</span></span> <span data-ttu-id="270cf-106">I cicli sono particolarmente utili per la sostituzione di cursori definiti nel codice SQL.</span><span class="sxs-lookup"><span data-stu-id="270cf-106">Loops are particularly useful for replacing cursors defined in SQL code.</span></span> <span data-ttu-id="270cf-107">Fortunatamente, quasi tutti i cursori vengono scritti nel codice SQL sono di hello veloce in avanti, leggere solo diversi.</span><span class="sxs-lookup"><span data-stu-id="270cf-107">Fortunately, almost all cursors that are written in SQL code are of hello fast forward, read only variety.</span></span> <span data-ttu-id="270cf-108">Pertanto [mentre] cicli sono un'ottima alternativa se è necessario avere tooreplace uno.</span><span class="sxs-lookup"><span data-stu-id="270cf-108">Therefore [WHILE] loops are a great alternative if you find yourself having tooreplace one.</span></span>

## <a name="leveraging-loops-and-replacing-cursors-in-sql-data-warehouse"></a><span data-ttu-id="270cf-109">Uso di cicli e sostituzione di cursori in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="270cf-109">Leveraging loops and replacing cursors in SQL Data Warehouse</span></span>
<span data-ttu-id="270cf-110">Tuttavia, prima di approfondire ulteriormente head innanzitutto è necessario valutare hello seguenti domande: "il cursore può essere riscritto toouse operazioni basate su set?".</span><span class="sxs-lookup"><span data-stu-id="270cf-110">However, before diving in head first you should ask yourself hello following question: "Could this cursor be re-written toouse set based operations?".</span></span> <span data-ttu-id="270cf-111">In molti casi risposte hello saranno Sì ed sono spesso consigliabile hello.</span><span class="sxs-lookup"><span data-stu-id="270cf-111">In many cases hello answer will be yes and is often hello best approach.</span></span> <span data-ttu-id="270cf-112">Un'operazione basata su set viene spesso eseguita molto più velocemente rispetto a un approccio iterativo riga per riga.</span><span class="sxs-lookup"><span data-stu-id="270cf-112">A set based operation often performs significantly faster than an iterative, row by row approach.</span></span>

<span data-ttu-id="270cf-113">I cursori ad avanzamento rapido di sola lettura possono essere facilmente sostituiti con un costrutto di ciclo.</span><span class="sxs-lookup"><span data-stu-id="270cf-113">Fast forward read-only cursors can be easily replaced with a looping construct.</span></span> <span data-ttu-id="270cf-114">Un semplice esempio viene riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="270cf-114">Below is a simple example.</span></span> <span data-ttu-id="270cf-115">Questo esempio di codice aggiorna le statistiche di hello per ogni tabella nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="270cf-115">This code example updates hello statistics for every table in hello database.</span></span> <span data-ttu-id="270cf-116">Scorrendo tabelle hello in ciclo hello è è in grado di tooexecute ogni comando in sequenza.</span><span class="sxs-lookup"><span data-stu-id="270cf-116">By iterating over hello tables in hello loop we are able tooexecute each command in sequence.</span></span>

<span data-ttu-id="270cf-117">Creare innanzitutto una tabella temporanea contenente una riga univoca numero usato tooidentify hello singole istruzioni:</span><span class="sxs-lookup"><span data-stu-id="270cf-117">First, create a temporary table containing a unique row number used tooidentify hello individual statements:</span></span>

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

<span data-ttu-id="270cf-118">In secondo luogo, inizializzare il ciclo di hello hello variabili tooperform necessarie:</span><span class="sxs-lookup"><span data-stu-id="270cf-118">Second, initialize hello variables required tooperform hello loop:</span></span>

```
DECLARE @nbr_statements INT = (SELECT COUNT(*) FROM #tbl)
,       @i INT = 1
;
```

<span data-ttu-id="270cf-119">Ora eseguire un ciclo delle istruzioni, una alla volta:</span><span class="sxs-lookup"><span data-stu-id="270cf-119">Now loop over statements executing them one at a time:</span></span>

```
WHILE   @i <= @nbr_statements
BEGIN
    DECLARE @sql_code NVARCHAR(4000) = (SELECT sql_code FROM #tbl WHERE Sequence = @i);
    EXEC    sp_executesql @sql_code;
    SET     @i +=1;
END
```

<span data-ttu-id="270cf-120">Infine Elimina tabella temporanea di hello creata nel primo passaggio hello</span><span class="sxs-lookup"><span data-stu-id="270cf-120">Finally drop hello temporary table created in hello first step</span></span>

```
DROP TABLE #tbl;
```


<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a><span data-ttu-id="270cf-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="270cf-121">Next steps</span></span>
<span data-ttu-id="270cf-122">Per altri suggerimenti sullo sviluppo, vedere la [panoramica dello sviluppo][development overview].</span><span class="sxs-lookup"><span data-stu-id="270cf-122">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[mentre]: https://msdn.microsoft.com/library/ms178642.aspx


<!--Other Web references-->
