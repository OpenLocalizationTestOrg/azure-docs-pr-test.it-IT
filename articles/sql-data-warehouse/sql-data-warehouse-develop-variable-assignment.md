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
# <a name="assign-variables-in-sql-data-warehouse"></a><span data-ttu-id="3e19e-103">Assegnare variabili in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="3e19e-103">Assign variables in SQL Data Warehouse</span></span>
<span data-ttu-id="3e19e-104">Le variabili in SQL Data Warehouse vengono impostate utilizzando hello `DECLARE` istruzione o hello `SET` istruzione.</span><span class="sxs-lookup"><span data-stu-id="3e19e-104">Variables in SQL Data Warehouse are set using hello `DECLARE` statement or hello `SET` statement.</span></span>

<span data-ttu-id="3e19e-105">Tutti hello seguenti sono validi perfettamente tooset un valore della variabile:</span><span class="sxs-lookup"><span data-stu-id="3e19e-105">All of hello following are perfectly valid ways tooset a variable value:</span></span>

## <a name="setting-variables-with-declare"></a><span data-ttu-id="3e19e-106">Impostazione delle variabili con DECLARE</span><span class="sxs-lookup"><span data-stu-id="3e19e-106">Setting variables with DECLARE</span></span>
<span data-ttu-id="3e19e-107">Inizializzazione di variabili con DECLARE è uno dei hello più flessibile modi tooset un valore della variabile in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3e19e-107">Initializing variables with DECLARE is one of hello most flexible ways tooset a variable value in SQL Data Warehouse.</span></span>

```sql
DECLARE @v  int = 0
;
```

<span data-ttu-id="3e19e-108">È inoltre possibile utilizzare DECLARE tooset più di una variabile alla volta.</span><span class="sxs-lookup"><span data-stu-id="3e19e-108">You can also use DECLARE tooset more than one variable at a time.</span></span> <span data-ttu-id="3e19e-109">Non è possibile utilizzare `SELECT` o `UPDATE` toodo questo:</span><span class="sxs-lookup"><span data-stu-id="3e19e-109">You cannot use `SELECT` or `UPDATE` toodo this:</span></span>

```sql
DECLARE @v  INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Smith')
,       @v1 INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Jones')
;
```

<span data-ttu-id="3e19e-110">Non è possibile inizializzare e utilizzare una variabile in hello stessa istruzione DECLARE.</span><span class="sxs-lookup"><span data-stu-id="3e19e-110">You cannot initialise and use a variable in hello same DECLARE statement.</span></span> <span data-ttu-id="3e19e-111">tooillustrate hello punto hello esempio riportato di seguito è **non** consentito come @p1 sia inizializzata e utilizzato in hello stessa istruzione DECLARE.</span><span class="sxs-lookup"><span data-stu-id="3e19e-111">tooillustrate hello point hello example below is **not** allowed as @p1 is both initialized and used in hello same DECLARE statement.</span></span> <span data-ttu-id="3e19e-112">Ciò comporterà un errore.</span><span class="sxs-lookup"><span data-stu-id="3e19e-112">This will result in an error.</span></span>

```sql
DECLARE @p1 int = 0
,       @p2 int = (SELECT COUNT (*) FROM sys.types where is_user_defined = @p1 )
;
```

## <a name="setting-values-with-set"></a><span data-ttu-id="3e19e-113">Impostazione di valori con SET</span><span class="sxs-lookup"><span data-stu-id="3e19e-113">Setting values with SET</span></span>
<span data-ttu-id="3e19e-114">Set è un metodo molto comune per l'impostazione di una singola variabile.</span><span class="sxs-lookup"><span data-stu-id="3e19e-114">Set is a very common method for setting a single variable.</span></span>

<span data-ttu-id="3e19e-115">Tutti gli esempi di hello riportato di seguito sono validi dell'impostazione di una variabile con SET:</span><span class="sxs-lookup"><span data-stu-id="3e19e-115">All of hello examples below are valid ways of setting a variable with SET:</span></span>

```sql
SET     @v = (Select max(database_id) from sys.databases);
SET     @v = 1;
SET     @v = @v+1;
SET     @v +=1;
```

<span data-ttu-id="3e19e-116">È possibile impostare una sola variabile alla volta con SET.</span><span class="sxs-lookup"><span data-stu-id="3e19e-116">You can only set one variable at a time with SET.</span></span> <span data-ttu-id="3e19e-117">Tuttavia, come illustrato sopra, gli operatori composti sono consentiti.</span><span class="sxs-lookup"><span data-stu-id="3e19e-117">However, as can be seen above compound operators are permissable.</span></span>

## <a name="limitations"></a><span data-ttu-id="3e19e-118">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="3e19e-118">Limitations</span></span>
<span data-ttu-id="3e19e-119">Non è possibile usare SELECT o UPDATE per l'assegnazione di variabili.</span><span class="sxs-lookup"><span data-stu-id="3e19e-119">You cannot use SELECT or UPDATE for variable assignment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e19e-120">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3e19e-120">Next steps</span></span>
<span data-ttu-id="3e19e-121">Per altri suggerimenti sullo sviluppo, vedere la [panoramica dello sviluppo][development overview].</span><span class="sxs-lookup"><span data-stu-id="3e19e-121">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
