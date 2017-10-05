---
title: Stored procedure in SQL Data Warehouse | Documentazione Microsoft
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
ms.openlocfilehash: e42d80f0ca35f3fbb67389c66d072bc40d8a8d2c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="stored-procedures-in-sql-data-warehouse"></a><span data-ttu-id="77a49-103">Stored procedure in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="77a49-103">Stored procedures in SQL Data Warehouse</span></span>
<span data-ttu-id="77a49-104">SQL Data Warehouse supporta molte delle funzionalità Transact-SQL disponibili in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="77a49-104">SQL Data Warehouse supports many of the Transact-SQL features found in SQL Server.</span></span> <span data-ttu-id="77a49-105">Ancora più importanti sono le funzionalità di scalabilità orizzontale specifiche, che si useranno per massimizzare le prestazioni della soluzione.</span><span class="sxs-lookup"><span data-stu-id="77a49-105">More importantly there are scale out specific features that we will want to leverage to maximize the performance of your solution.</span></span>

<span data-ttu-id="77a49-106">Tuttavia, per mantenere la scalabilità e le prestazioni di SQL Data Warehouse sono disponibili anche funzionalità e caratteristiche con differenze di comportamento e altra che non sono supportate.</span><span class="sxs-lookup"><span data-stu-id="77a49-106">However, to maintain the scale and performance of SQL Data Warehouse there are also some features and functionality that have behavioral differences and others that are not supported.</span></span>

<span data-ttu-id="77a49-107">Questo articolo illustra come implementare stored procedure in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="77a49-107">This article explains how to implement stored procedures within SQL Data Warehouse.</span></span>

## <a name="introducing-stored-procedures"></a><span data-ttu-id="77a49-108">Introduzione alle stored procedure</span><span class="sxs-lookup"><span data-stu-id="77a49-108">Introducing stored procedures</span></span>
<span data-ttu-id="77a49-109">Le stored procedure sono un ottimo modo per incapsulare il codice SQL, archiviandolo vicino i dati nel data warehouse.</span><span class="sxs-lookup"><span data-stu-id="77a49-109">Stored procedures are a great way for encapsulating your SQL code; storing it close to your data in the data warehouse.</span></span> <span data-ttu-id="77a49-110">Incapsulando il codice in unità gestibili, stored procedure consentono agli sviluppatori di modularizzare le soluzioni, rendendo possibile un maggiore riutilizzo del codice.</span><span class="sxs-lookup"><span data-stu-id="77a49-110">By encapsulating the code into manageable units stored procedures help developers modularize their solutions; facilitating greater re-usability of code.</span></span> <span data-ttu-id="77a49-111">Ogni stored procedure può anche accettare parametri per essere ancora più flessibile.</span><span class="sxs-lookup"><span data-stu-id="77a49-111">Each stored procedure can also accept parameters to make them even more flexible.</span></span>

<span data-ttu-id="77a49-112">SQL Data Warehouse fornisce un'implementazione semplificata e ottimizzata delle stored procedure.</span><span class="sxs-lookup"><span data-stu-id="77a49-112">SQL Data Warehouse provides a simplified and streamlined stored procedure implementation.</span></span> <span data-ttu-id="77a49-113">La differenza principale rispetto a SQL Server è che la stored procedure non è codice precompilato.</span><span class="sxs-lookup"><span data-stu-id="77a49-113">The biggest difference compared to SQL Server is that the stored procedure is not pre-compiled code.</span></span> <span data-ttu-id="77a49-114">Nei data warehouse si è in genere meno preoccupati del tempo di compilazione.</span><span class="sxs-lookup"><span data-stu-id="77a49-114">In data warehouses we are generally less concerned with the compilation time.</span></span> <span data-ttu-id="77a49-115">È più importante che il codice della stored procedure sia ottimizzato nel modo corretto quando si lavora con grandi volumi di dati.</span><span class="sxs-lookup"><span data-stu-id="77a49-115">It is more important that the stored procedure code is correctly optimised when operating against large data volumes.</span></span> <span data-ttu-id="77a49-116">L'obiettivo consiste nel risparmiare ore, minuti e secondi, non millisecondi.</span><span class="sxs-lookup"><span data-stu-id="77a49-116">The goal is to save hours, minutes and seconds not milliseconds.</span></span> <span data-ttu-id="77a49-117">È quindi più utile pensare alle stored procedure come contenitori per la logica di SQL.</span><span class="sxs-lookup"><span data-stu-id="77a49-117">It is therefore more helpful to think of stored procedures as containers for SQL logic.</span></span>     

<span data-ttu-id="77a49-118">Quando SQL Data Warehouse esegue la stored procedure, le istruzioni SQL vengono analizzate, convertite e ottimizzate in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="77a49-118">When SQL Data Warehouse executes your stored procedure the SQL statements are parsed, translated and optimized at run time.</span></span> <span data-ttu-id="77a49-119">Durante questo processo, ogni istruzione viene convertita in query distribuite.</span><span class="sxs-lookup"><span data-stu-id="77a49-119">During this process each statement is converted into distributed queries.</span></span> <span data-ttu-id="77a49-120">Il codice SQL effettivamente eseguito sui dati è diverso dalla query inviata.</span><span class="sxs-lookup"><span data-stu-id="77a49-120">The SQL code that is actually executed against the data is different to the query submitted.</span></span>

## <a name="nesting-stored-procedures"></a><span data-ttu-id="77a49-121">Annidamento di stored procedure</span><span class="sxs-lookup"><span data-stu-id="77a49-121">Nesting stored procedures</span></span>
<span data-ttu-id="77a49-122">Quando la stored procedure chiamano altre stored procedure o eseguono istruzioni SQL dinamiche, la stored procedure interna o la chiamata al codice è detta annidata.</span><span class="sxs-lookup"><span data-stu-id="77a49-122">When stored procedures call other stored procedures or execute dynamic sql then the inner stored procedure or code invocation is said to be nested.</span></span>

<span data-ttu-id="77a49-123">SQL Data Warehouse supporta un massimo di 8 livelli di annidamento.</span><span class="sxs-lookup"><span data-stu-id="77a49-123">SQL Data Warehouse support a maximum of 8 nesting levels.</span></span> <span data-ttu-id="77a49-124">Questo comportamento è leggermente diverso rispetto a SQL Server.</span><span class="sxs-lookup"><span data-stu-id="77a49-124">This is slightly different to SQL Server.</span></span> <span data-ttu-id="77a49-125">In SQL Server i livelli di annidamento sono 32.</span><span class="sxs-lookup"><span data-stu-id="77a49-125">The nest level in SQL Server is 32.</span></span>

<span data-ttu-id="77a49-126">La chiamata alla stored procedure di livello superiore equivale al livello di annidamento 1.</span><span class="sxs-lookup"><span data-stu-id="77a49-126">The top level stored procedure call equates to nest level 1</span></span>

```sql
EXEC prc_nesting
```
<span data-ttu-id="77a49-127">Se la stored procedure effettua anche un'altra chiamata a EXEC, il livello di annidamento passerà a 2.</span><span class="sxs-lookup"><span data-stu-id="77a49-127">If the stored procedure also makes another EXEC call then this will increase the nest level to 2</span></span>

```sql
CREATE PROCEDURE prc_nesting
AS
EXEC prc_nesting_2  -- This call is nest level 2
GO
EXEC prc_nesting
```
<span data-ttu-id="77a49-128">Se la seconda procedura esegue quindi alcune istruzioni SQL dinamiche, il livello di annidamento passerà a 3.</span><span class="sxs-lookup"><span data-stu-id="77a49-128">If the second procedure then executes some dynamic sql then this will increase the nest level to 3</span></span>

```sql
CREATE PROCEDURE prc_nesting_2
AS
EXEC sp_executesql 'SELECT 'another nest level'  -- This call is nest level 2
GO
EXEC prc_nesting
```

<span data-ttu-id="77a49-129">Tenere presente che SQL Data Warehouse attualmente non supporta @@NESTLEVEL.</span><span class="sxs-lookup"><span data-stu-id="77a49-129">Note SQL Data Warehouse does not currently support @@NESTLEVEL.</span></span> <span data-ttu-id="77a49-130">Sarà necessario tenere traccia manualmente del livello di annidamento.</span><span class="sxs-lookup"><span data-stu-id="77a49-130">You will need to keep a track of your nest level yourself.</span></span> <span data-ttu-id="77a49-131">È improbabile che venga raggiunto il limite del livello di annidamento 8, ma in questo caso sarà necessario usare di nuovo il codice e renderlo "flat" in modo che rientri in tale limite.</span><span class="sxs-lookup"><span data-stu-id="77a49-131">It is unlikely you will hit the 8 nest level limit but if you do you will need to re-work your code and "flatten" it so that it fits within this limit.</span></span>

## <a name="insertexecute"></a><span data-ttu-id="77a49-132">INSERT..EXECUTE</span><span class="sxs-lookup"><span data-stu-id="77a49-132">INSERT..EXECUTE</span></span>
<span data-ttu-id="77a49-133">SQL Data Warehouse non consente di usare il set di risultati di una stored procedure con un'istruzione INSERT.</span><span class="sxs-lookup"><span data-stu-id="77a49-133">SQL Data Warehouse does not permit you to consume the result set of a stored procedure with an INSERT statement.</span></span> <span data-ttu-id="77a49-134">Si può tuttavia un approccio alternativo.</span><span class="sxs-lookup"><span data-stu-id="77a49-134">However, there is an alternative approach you can use.</span></span>

<span data-ttu-id="77a49-135">Per un esempio di come eseguire questa operazione, fare riferimento all'articolo seguente sulle [tabelle temporanee] .</span><span class="sxs-lookup"><span data-stu-id="77a49-135">Please refer to the following article on [temporary tables] for an example on how to do this.</span></span>

## <a name="limitations"></a><span data-ttu-id="77a49-136">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="77a49-136">Limitations</span></span>
<span data-ttu-id="77a49-137">Esistono alcuni aspetti delle stored procedure Transact-SQL che non sono implementate in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="77a49-137">There are some aspects of Transact-SQL stored procedures that are not implemented in SQL Data Warehouse.</span></span>

<span data-ttu-id="77a49-138">Sono:</span><span class="sxs-lookup"><span data-stu-id="77a49-138">They are:</span></span>

* <span data-ttu-id="77a49-139">Stored procedure temporanee</span><span class="sxs-lookup"><span data-stu-id="77a49-139">temporary stored procedures</span></span>
* <span data-ttu-id="77a49-140">Stored procedure numerate</span><span class="sxs-lookup"><span data-stu-id="77a49-140">numbered stored procedures</span></span>
* <span data-ttu-id="77a49-141">Stored procedure estese</span><span class="sxs-lookup"><span data-stu-id="77a49-141">extended stored procedures</span></span>
* <span data-ttu-id="77a49-142">Stored procedure CLR</span><span class="sxs-lookup"><span data-stu-id="77a49-142">CLR stored procedures</span></span>
* <span data-ttu-id="77a49-143">Opzione di crittografia</span><span class="sxs-lookup"><span data-stu-id="77a49-143">encryption option</span></span>
* <span data-ttu-id="77a49-144">Opzione di replica</span><span class="sxs-lookup"><span data-stu-id="77a49-144">replication option</span></span>
* <span data-ttu-id="77a49-145">Parametri con valori di tabella</span><span class="sxs-lookup"><span data-stu-id="77a49-145">table-valued parameters</span></span>
* <span data-ttu-id="77a49-146">Parametri di sola lettura</span><span class="sxs-lookup"><span data-stu-id="77a49-146">read-only parameters</span></span>
* <span data-ttu-id="77a49-147">Parametri predefiniti</span><span class="sxs-lookup"><span data-stu-id="77a49-147">default parameters</span></span>
* <span data-ttu-id="77a49-148">Contesti di esecuzione</span><span class="sxs-lookup"><span data-stu-id="77a49-148">execution contexts</span></span>
* <span data-ttu-id="77a49-149">Istruzione return</span><span class="sxs-lookup"><span data-stu-id="77a49-149">return statement</span></span>

## <a name="next-steps"></a><span data-ttu-id="77a49-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="77a49-150">Next steps</span></span>
<span data-ttu-id="77a49-151">Per altri suggerimenti sullo sviluppo, vedere la [panoramica dello sviluppo][development overview].</span><span class="sxs-lookup"><span data-stu-id="77a49-151">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
<span data-ttu-id="77a49-152">[tabelle temporanee]: ./sql-data-warehouse-tables-temporary.md#modularizing-code</span><span class="sxs-lookup"><span data-stu-id="77a49-152">[temporary tables]: ./sql-data-warehouse-tables-temporary.md#modularizing-code</span></span>
[development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[nest level]: https://msdn.microsoft.com/library/ms187371.aspx

<!--Other Web references-->
