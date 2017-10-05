---
title: Assegnazione di variabili in SQL Data Warehouse | Documentazione Microsoft
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
ms.openlocfilehash: 045d5148cd3f12dac63c961ccf7c953d355ed725
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="assign-variables-in-sql-data-warehouse"></a><span data-ttu-id="7e18c-103">Assegnare variabili in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="7e18c-103">Assign variables in SQL Data Warehouse</span></span>
<span data-ttu-id="7e18c-104">Le variabili in SQL Data Warehouse vengono impostate usando l'istruzione `DECLARE` o `SET`.</span><span class="sxs-lookup"><span data-stu-id="7e18c-104">Variables in SQL Data Warehouse are set using the `DECLARE` statement or the `SET` statement.</span></span>

<span data-ttu-id="7e18c-105">Tutti modi seguenti sono perfettamente validi per impostare il valore di una variabile:</span><span class="sxs-lookup"><span data-stu-id="7e18c-105">All of the following are perfectly valid ways to set a variable value:</span></span>

## <a name="setting-variables-with-declare"></a><span data-ttu-id="7e18c-106">Impostazione delle variabili con DECLARE</span><span class="sxs-lookup"><span data-stu-id="7e18c-106">Setting variables with DECLARE</span></span>
<span data-ttu-id="7e18c-107">L'inizializzazione di variabili con DECLARE è uno dei modi più flessibili per impostare un valore della variabile in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="7e18c-107">Initializing variables with DECLARE is one of the most flexible ways to set a variable value in SQL Data Warehouse.</span></span>

```sql
DECLARE @v  int = 0
;
```

<span data-ttu-id="7e18c-108">È anche possibile usare DECLARE per impostare più di una variabile contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="7e18c-108">You can also use DECLARE to set more than one variable at a time.</span></span> <span data-ttu-id="7e18c-109">Non è possibile usare `SELECT` o `UPDATE` per eseguire questa operazione:</span><span class="sxs-lookup"><span data-stu-id="7e18c-109">You cannot use `SELECT` or `UPDATE` to do this:</span></span>

```sql
DECLARE @v  INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Smith')
,       @v1 INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Jones')
;
```

<span data-ttu-id="7e18c-110">Non è possibile inizializzare e usare una variabile nella stessa istruzione DECLARE.</span><span class="sxs-lookup"><span data-stu-id="7e18c-110">You cannot initialise and use a variable in the same DECLARE statement.</span></span> <span data-ttu-id="7e18c-111">Per illustrare il concetto, l'esempio seguente **non** è consentito, perché @p1 viene inizializzato e usato nella stessa istruzione DECLARE.</span><span class="sxs-lookup"><span data-stu-id="7e18c-111">To illustrate the point the example below is **not** allowed as @p1 is both initialized and used in the same DECLARE statement.</span></span> <span data-ttu-id="7e18c-112">Ciò comporterà un errore.</span><span class="sxs-lookup"><span data-stu-id="7e18c-112">This will result in an error.</span></span>

```sql
DECLARE @p1 int = 0
,       @p2 int = (SELECT COUNT (*) FROM sys.types where is_user_defined = @p1 )
;
```

## <a name="setting-values-with-set"></a><span data-ttu-id="7e18c-113">Impostazione di valori con SET</span><span class="sxs-lookup"><span data-stu-id="7e18c-113">Setting values with SET</span></span>
<span data-ttu-id="7e18c-114">Set è un metodo molto comune per l'impostazione di una singola variabile.</span><span class="sxs-lookup"><span data-stu-id="7e18c-114">Set is a very common method for setting a single variable.</span></span>

<span data-ttu-id="7e18c-115">Tutti gli esempi seguenti sono modi validi per impostare una variabile con SET:</span><span class="sxs-lookup"><span data-stu-id="7e18c-115">All of the examples below are valid ways of setting a variable with SET:</span></span>

```sql
SET     @v = (Select max(database_id) from sys.databases);
SET     @v = 1;
SET     @v = @v+1;
SET     @v +=1;
```

<span data-ttu-id="7e18c-116">È possibile impostare una sola variabile alla volta con SET.</span><span class="sxs-lookup"><span data-stu-id="7e18c-116">You can only set one variable at a time with SET.</span></span> <span data-ttu-id="7e18c-117">Tuttavia, come illustrato sopra, gli operatori composti sono consentiti.</span><span class="sxs-lookup"><span data-stu-id="7e18c-117">However, as can be seen above compound operators are permissable.</span></span>

## <a name="limitations"></a><span data-ttu-id="7e18c-118">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="7e18c-118">Limitations</span></span>
<span data-ttu-id="7e18c-119">Non è possibile usare SELECT o UPDATE per l'assegnazione di variabili.</span><span class="sxs-lookup"><span data-stu-id="7e18c-119">You cannot use SELECT or UPDATE for variable assignment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e18c-120">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7e18c-120">Next steps</span></span>
<span data-ttu-id="7e18c-121">Per altri suggerimenti sullo sviluppo, vedere la [panoramica dello sviluppo][development overview].</span><span class="sxs-lookup"><span data-stu-id="7e18c-121">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
