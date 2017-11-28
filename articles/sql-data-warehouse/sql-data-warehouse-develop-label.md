---
title: aaaUse tooinstrument query in SQL Data Warehouse di etichette | Documenti Microsoft
description: Suggerimenti per l'utilizzo di query tooinstrument etichette in Azure SQL Data Warehouse per lo sviluppo di soluzioni.
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
ms.openlocfilehash: 82e7ea98e1417134227f1d7c529fdaf2f1df3853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-labels-tooinstrument-queries-in-sql-data-warehouse"></a><span data-ttu-id="196c3-103">Utilizzare le query tooinstrument di etichette in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="196c3-103">Use labels tooinstrument queries in SQL Data Warehouse</span></span>
<span data-ttu-id="196c3-104">SQL Data Warehouse supporta un concetto detto etichette di query.</span><span class="sxs-lookup"><span data-stu-id="196c3-104">SQL Data Warehouse supports a concept called query labels.</span></span> <span data-ttu-id="196c3-105">Prima di approfondire il concetto, eccone un esempio:</span><span class="sxs-lookup"><span data-stu-id="196c3-105">Before going into any depth let's look at an example of one:</span></span>

```sql
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query Label')
;
```

<span data-ttu-id="196c3-106">L'ultima riga tag query toohello di hello stringa 'My Query Label'.</span><span class="sxs-lookup"><span data-stu-id="196c3-106">This last line tags hello string 'My Query Label' toohello query.</span></span> <span data-ttu-id="196c3-107">Ciò è particolarmente utile come etichetta di hello è in grado query tramite hello DMV.</span><span class="sxs-lookup"><span data-stu-id="196c3-107">This is particularly helpful as hello label is query-able through hello DMVs.</span></span> <span data-ttu-id="196c3-108">Ciò offre a un meccanismo tootrack verso il basso di query problematiche e anche toohelp identificare lo stato di avanzamento tramite un'esecuzione ETL.</span><span class="sxs-lookup"><span data-stu-id="196c3-108">This provides us with a mechanism tootrack down problem queries and also toohelp identify progress through an ETL run.</span></span>

<span data-ttu-id="196c3-109">Una buona convenzione di denominazione è estremamente utile in questo caso.</span><span class="sxs-lookup"><span data-stu-id="196c3-109">A good naming convention really helps here.</span></span> <span data-ttu-id="196c3-110">Ad esempio qualcosa di simile a ' progetto: procedura: istruzione: commento ' Guida toouniquely identificare query hello in tra tutto il codice hello nel controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="196c3-110">For example something like ' PROJECT : PROCEDURE : STATEMENT : COMMENT' would help toouniquely identify hello query in amongst all hello code in source control.</span></span>

<span data-ttu-id="196c3-111">viste a gestione dinamica di hello toosearch dall'etichetta, è possibile utilizzare hello seguente query che utilizza:</span><span class="sxs-lookup"><span data-stu-id="196c3-111">toosearch by label you can use hello following query that uses hello dynamic management views:</span></span>

```sql
SELECT  *
FROM    sys.dm_pdw_exec_requests r
WHERE   r.[label] = 'My Query Label'
;
```

> [!NOTE]
> <span data-ttu-id="196c3-112">È essenziale che eseguire il wrapping delle parentesi quadre o virgolette doppie etichetta parola hello quando si eseguono query.</span><span class="sxs-lookup"><span data-stu-id="196c3-112">It is essential that you wrap square brackets or double quotes around hello word label when querying.</span></span> <span data-ttu-id="196c3-113">Label è una parola riservata e causa un errore se non viene delimitata.</span><span class="sxs-lookup"><span data-stu-id="196c3-113">Label is a reserved word and will caused an error if it has not been delimited.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="196c3-114">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="196c3-114">Next steps</span></span>
<span data-ttu-id="196c3-115">Per altri suggerimenti sullo sviluppo, vedere la [panoramica dello sviluppo][development overview].</span><span class="sxs-lookup"><span data-stu-id="196c3-115">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
