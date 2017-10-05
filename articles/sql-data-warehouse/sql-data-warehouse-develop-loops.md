---
title: Sfruttare cicli T-SQL in Azure SQL Data Warehouse | Documentazione Microsoft
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
ms.openlocfilehash: 40a872ff310f48bfd543ac184fe7301b85b50258
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="loops-in-sql-data-warehouse"></a><span data-ttu-id="3d85a-103">Cicli in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="3d85a-103">Loops in SQL Data Warehouse</span></span>
<span data-ttu-id="3d85a-104">SQL Data Warehouse supporta il ciclo [WHILE][WHILE] per eseguire ripetutamente blocchi di istruzioni.</span><span class="sxs-lookup"><span data-stu-id="3d85a-104">SQL Data Warehouse supports the [WHILE][WHILE] loop for repeatedly executing statement blocks.</span></span> <span data-ttu-id="3d85a-105">L'esecuzione continua fino a quando le condizioni specificate sono vere o fino a quando il codice termina il ciclo in modo specifico usando la parola chiave `BREAK` .</span><span class="sxs-lookup"><span data-stu-id="3d85a-105">This will continue for as long as the specified conditions are true or until the code specifically terminates the loop using the `BREAK` keyword.</span></span> <span data-ttu-id="3d85a-106">I cicli sono particolarmente utili per la sostituzione di cursori definiti nel codice SQL.</span><span class="sxs-lookup"><span data-stu-id="3d85a-106">Loops are particularly useful for replacing cursors defined in SQL code.</span></span> <span data-ttu-id="3d85a-107">Per fortuna, quasi tutti i cursori scritti in codice SQL sono del tipo avanzamento rapido, di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="3d85a-107">Fortunately, almost all cursors that are written in SQL code are of the fast forward, read only variety.</span></span> <span data-ttu-id="3d85a-108">Di conseguenza i cicli [WHILE] rappresentano un'ottima alternativa se è necessario sostituirne uno.</span><span class="sxs-lookup"><span data-stu-id="3d85a-108">Therefore [WHILE] loops are a great alternative if you find yourself having to replace one.</span></span>

## <a name="leveraging-loops-and-replacing-cursors-in-sql-data-warehouse"></a><span data-ttu-id="3d85a-109">Uso di cicli e sostituzione di cursori in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="3d85a-109">Leveraging loops and replacing cursors in SQL Data Warehouse</span></span>
<span data-ttu-id="3d85a-110">Tuttavia, prima di procedere è innanzitutto necessario chiedersi se il cursore può essere riscritto per l'uso di operazioni basate su set.</span><span class="sxs-lookup"><span data-stu-id="3d85a-110">However, before diving in head first you should ask yourself the following question: "Could this cursor be re-written to use set based operations?".</span></span> <span data-ttu-id="3d85a-111">In molti casi la risposta è Sì ed è spesso l'approccio migliore.</span><span class="sxs-lookup"><span data-stu-id="3d85a-111">In many cases the answer will be yes and is often the best approach.</span></span> <span data-ttu-id="3d85a-112">Un'operazione basata su set viene spesso eseguita molto più velocemente rispetto a un approccio iterativo riga per riga.</span><span class="sxs-lookup"><span data-stu-id="3d85a-112">A set based operation often performs significantly faster than an iterative, row by row approach.</span></span>

<span data-ttu-id="3d85a-113">I cursori ad avanzamento rapido di sola lettura possono essere facilmente sostituiti con un costrutto di ciclo.</span><span class="sxs-lookup"><span data-stu-id="3d85a-113">Fast forward read-only cursors can be easily replaced with a looping construct.</span></span> <span data-ttu-id="3d85a-114">Un semplice esempio viene riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="3d85a-114">Below is a simple example.</span></span> <span data-ttu-id="3d85a-115">Questo esempio di codice aggiorna le statistiche per ogni tabella nel database.</span><span class="sxs-lookup"><span data-stu-id="3d85a-115">This code example updates the statistics for every table in the database.</span></span> <span data-ttu-id="3d85a-116">Scorrendo le tabelle nel ciclo è possibile eseguire ogni comando in sequenza.</span><span class="sxs-lookup"><span data-stu-id="3d85a-116">By iterating over the tables in the loop we are able to execute each command in sequence.</span></span>

<span data-ttu-id="3d85a-117">Prima di tutto, creare una tabella temporanea contenente un numero di riga univoco usato per identificare le singole istruzioni:</span><span class="sxs-lookup"><span data-stu-id="3d85a-117">First, create a temporary table containing a unique row number used to identify the individual statements:</span></span>

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

<span data-ttu-id="3d85a-118">Inizializzare quindi le variabili necessarie per eseguire il ciclo:</span><span class="sxs-lookup"><span data-stu-id="3d85a-118">Second, initialize the variables required to perform the loop:</span></span>

```
DECLARE @nbr_statements INT = (SELECT COUNT(*) FROM #tbl)
,       @i INT = 1
;
```

<span data-ttu-id="3d85a-119">Ora eseguire un ciclo delle istruzioni, una alla volta:</span><span class="sxs-lookup"><span data-stu-id="3d85a-119">Now loop over statements executing them one at a time:</span></span>

```
WHILE   @i <= @nbr_statements
BEGIN
    DECLARE @sql_code NVARCHAR(4000) = (SELECT sql_code FROM #tbl WHERE Sequence = @i);
    EXEC    sp_executesql @sql_code;
    SET     @i +=1;
END
```

<span data-ttu-id="3d85a-120">Infine eliminare la tabella temporanea creata nel primo passaggio.</span><span class="sxs-lookup"><span data-stu-id="3d85a-120">Finally drop the temporary table created in the first step</span></span>

```
DROP TABLE #tbl;
```


<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->

## <a name="next-steps"></a><span data-ttu-id="3d85a-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3d85a-121">Next steps</span></span>
<span data-ttu-id="3d85a-122">Per altri suggerimenti sullo sviluppo, vedere la [panoramica dello sviluppo][development overview].</span><span class="sxs-lookup"><span data-stu-id="3d85a-122">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
<span data-ttu-id="3d85a-123">[WHILE]: https://msdn.microsoft.com/library/ms178642.aspx</span><span class="sxs-lookup"><span data-stu-id="3d85a-123">[WHILE]: https://msdn.microsoft.com/library/ms178642.aspx</span></span>


<!--Other Web references-->
