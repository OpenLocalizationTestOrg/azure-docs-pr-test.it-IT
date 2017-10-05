---
title: Usare etichette per instrumentare query in SQL Data Warehouse | Microsoft Docs
description: Suggerimenti per l'uso di etichette per instrumentare query in Azure SQL Data Warehouse per lo sviluppo di soluzioni.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 44988de8-04c1-4fed-92be-e1935661a4e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 9e75bbe528a427724a623305fbd45e2277e9d0af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-labels-to-instrument-queries-in-sql-data-warehouse"></a><span data-ttu-id="98ef3-103">Usare etichette per instrumentare query in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="98ef3-103">Use labels to instrument queries in SQL Data Warehouse</span></span>
<span data-ttu-id="98ef3-104">SQL Data Warehouse supporta un concetto detto etichette di query.</span><span class="sxs-lookup"><span data-stu-id="98ef3-104">SQL Data Warehouse supports a concept called query labels.</span></span> <span data-ttu-id="98ef3-105">Prima di approfondire il concetto, eccone un esempio:</span><span class="sxs-lookup"><span data-stu-id="98ef3-105">Before going into any depth let's look at an example of one:</span></span>

```sql
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query Label')
;
```

<span data-ttu-id="98ef3-106">L'ultima riga contrassegna la stringa 'My Query Label' per la query.</span><span class="sxs-lookup"><span data-stu-id="98ef3-106">This last line tags the string 'My Query Label' to the query.</span></span> <span data-ttu-id="98ef3-107">Ciò è particolarmente utile in quanto l'etichetta supporta la query tramite le DMV.</span><span class="sxs-lookup"><span data-stu-id="98ef3-107">This is particularly helpful as the label is query-able through the DMVs.</span></span> <span data-ttu-id="98ef3-108">In questo modo si dispone di un meccanismo per tenere traccia di query problematiche e per identificare lo stato di avanzamento tramite un'esecuzione ETL.</span><span class="sxs-lookup"><span data-stu-id="98ef3-108">This provides us with a mechanism to track down problem queries and also to help identify progress through an ETL run.</span></span>

<span data-ttu-id="98ef3-109">Una buona convenzione di denominazione è estremamente utile in questo caso.</span><span class="sxs-lookup"><span data-stu-id="98ef3-109">A good naming convention really helps here.</span></span> <span data-ttu-id="98ef3-110">Ad esempio, una stringa simile a ' PROJECT : PROCEDURE : STATEMENT : COMMENT' può facilitare l'identificazione della query in tutto il codice nel controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="98ef3-110">For example something like ' PROJECT : PROCEDURE : STATEMENT : COMMENT' would help to uniquely identify the query in amongst all the code in source control.</span></span>

<span data-ttu-id="98ef3-111">Per la ricerca in base all'etichetta, è possibile usare la query seguente che usa le viste a gestione dinamica:</span><span class="sxs-lookup"><span data-stu-id="98ef3-111">To search by label you can use the following query that uses the dynamic management views:</span></span>

```sql
SELECT  *
FROM    sys.dm_pdw_exec_requests r
WHERE   r.[label] = 'My Query Label'
;
```

> [!NOTE]
> <span data-ttu-id="98ef3-112">È essenziale racchiudere tra parentesi quadre o virgolette doppie la parola label durante l'esecuzione della query.</span><span class="sxs-lookup"><span data-stu-id="98ef3-112">It is essential that you wrap square brackets or double quotes around the word label when querying.</span></span> <span data-ttu-id="98ef3-113">Label è una parola riservata e causa un errore se non viene delimitata.</span><span class="sxs-lookup"><span data-stu-id="98ef3-113">Label is a reserved word and will caused an error if it has not been delimited.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="98ef3-114">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="98ef3-114">Next steps</span></span>
<span data-ttu-id="98ef3-115">Per altri suggerimenti sullo sviluppo, vedere la [panoramica dello sviluppo][development overview].</span><span class="sxs-lookup"><span data-stu-id="98ef3-115">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
