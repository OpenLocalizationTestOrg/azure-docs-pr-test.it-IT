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
# <a name="stored-procedures-in-sql-data-warehouse"></a><span data-ttu-id="5f265-103">Stored procedure in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="5f265-103">Stored procedures in SQL Data Warehouse</span></span>
<span data-ttu-id="5f265-104">SQL Data Warehouse supporta molte delle funzionalità di Transact-SQL hello disponibili in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5f265-104">SQL Data Warehouse supports many of hello Transact-SQL features found in SQL Server.</span></span> <span data-ttu-id="5f265-105">Non esistono ancora più importante funzionalità specifiche che vogliamo delle prestazioni di hello toomaximize tooleverage della soluzione di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="5f265-105">More importantly there are scale out specific features that we will want tooleverage toomaximize hello performance of your solution.</span></span>

<span data-ttu-id="5f265-106">Scala hello toomaintain e le prestazioni di SQL Data Warehouse sono sono tuttavia anche alcune caratteristiche e funzionalità con differenze di comportamento e ad altri utenti che non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="5f265-106">However, toomaintain hello scale and performance of SQL Data Warehouse there are also some features and functionality that have behavioral differences and others that are not supported.</span></span>

<span data-ttu-id="5f265-107">Questo articolo spiega come tooimplement stored procedure all'interno di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="5f265-107">This article explains how tooimplement stored procedures within SQL Data Warehouse.</span></span>

## <a name="introducing-stored-procedures"></a><span data-ttu-id="5f265-108">Introduzione alle stored procedure</span><span class="sxs-lookup"><span data-stu-id="5f265-108">Introducing stored procedures</span></span>
<span data-ttu-id="5f265-109">Stored procedure sono un ottimo modo per incapsulare il codice SQL; archiviazione dati tooyour Chiudi nel data warehouse di hello.</span><span class="sxs-lookup"><span data-stu-id="5f265-109">Stored procedures are a great way for encapsulating your SQL code; storing it close tooyour data in hello data warehouse.</span></span> <span data-ttu-id="5f265-110">Incapsulando codice hello in unità gestibili stored procedure consentono agli sviluppatori di modularizzare le relative soluzioni; semplificazione di maggiore riutilizzo del codice.</span><span class="sxs-lookup"><span data-stu-id="5f265-110">By encapsulating hello code into manageable units stored procedures help developers modularize their solutions; facilitating greater re-usability of code.</span></span> <span data-ttu-id="5f265-111">Ogni stored procedure può anche accettare parametri toomake li ancora più flessibile.</span><span class="sxs-lookup"><span data-stu-id="5f265-111">Each stored procedure can also accept parameters toomake them even more flexible.</span></span>

<span data-ttu-id="5f265-112">SQL Data Warehouse fornisce un'implementazione semplificata e ottimizzata delle stored procedure.</span><span class="sxs-lookup"><span data-stu-id="5f265-112">SQL Data Warehouse provides a simplified and streamlined stored procedure implementation.</span></span> <span data-ttu-id="5f265-113">Hello più grande differenza rispetto tooSQL Server è che hello stored procedure non è codice precompilato.</span><span class="sxs-lookup"><span data-stu-id="5f265-113">hello biggest difference compared tooSQL Server is that hello stored procedure is not pre-compiled code.</span></span> <span data-ttu-id="5f265-114">In data warehouse di Microsoft è in genere meno interessati alla fase di compilazione hello.</span><span class="sxs-lookup"><span data-stu-id="5f265-114">In data warehouses we are generally less concerned with hello compilation time.</span></span> <span data-ttu-id="5f265-115">È più importante che hello stored procedure codice è ottimizzato in modo corretto quando si lavora con grandi volumi di dati.</span><span class="sxs-lookup"><span data-stu-id="5f265-115">It is more important that hello stored procedure code is correctly optimised when operating against large data volumes.</span></span> <span data-ttu-id="5f265-116">obiettivo di Hello è toosave ore, minuti e secondi non millisecondi.</span><span class="sxs-lookup"><span data-stu-id="5f265-116">hello goal is toosave hours, minutes and seconds not milliseconds.</span></span> <span data-ttu-id="5f265-117">È pertanto toothink più utili di stored procedure come contenitori per la logica di SQL.</span><span class="sxs-lookup"><span data-stu-id="5f265-117">It is therefore more helpful toothink of stored procedures as containers for SQL logic.</span></span>     

<span data-ttu-id="5f265-118">Quando viene eseguito SQL Data Warehouse istruzioni SQL hello stored procedure vengono analizzate, convertire e ottimizzate in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="5f265-118">When SQL Data Warehouse executes your stored procedure hello SQL statements are parsed, translated and optimized at run time.</span></span> <span data-ttu-id="5f265-119">Durante questo processo, ogni istruzione viene convertita in query distribuite.</span><span class="sxs-lookup"><span data-stu-id="5f265-119">During this process each statement is converted into distributed queries.</span></span> <span data-ttu-id="5f265-120">il codice SQL che viene effettivamente eseguito su dati hello Hello è toohello diverse query inviata.</span><span class="sxs-lookup"><span data-stu-id="5f265-120">hello SQL code that is actually executed against hello data is different toohello query submitted.</span></span>

## <a name="nesting-stored-procedures"></a><span data-ttu-id="5f265-121">Annidamento di stored procedure</span><span class="sxs-lookup"><span data-stu-id="5f265-121">Nesting stored procedures</span></span>
<span data-ttu-id="5f265-122">Quando le stored procedure chiamano altre stored procedure o eseguono istruzioni sql dinamiche, quindi interna hello o la stored procedure chiamata di codice viene definita toobe annidati.</span><span class="sxs-lookup"><span data-stu-id="5f265-122">When stored procedures call other stored procedures or execute dynamic sql then hello inner stored procedure or code invocation is said toobe nested.</span></span>

<span data-ttu-id="5f265-123">SQL Data Warehouse supporta un massimo di 8 livelli di annidamento.</span><span class="sxs-lookup"><span data-stu-id="5f265-123">SQL Data Warehouse support a maximum of 8 nesting levels.</span></span> <span data-ttu-id="5f265-124">Si tratta di tooSQL leggermente diversi Server.</span><span class="sxs-lookup"><span data-stu-id="5f265-124">This is slightly different tooSQL Server.</span></span> <span data-ttu-id="5f265-125">livello di nidificazione Hello in SQL Server è 32.</span><span class="sxs-lookup"><span data-stu-id="5f265-125">hello nest level in SQL Server is 32.</span></span>

<span data-ttu-id="5f265-126">chiamata di livello superiore da stored procedure Hello equivale toonest livello 1</span><span class="sxs-lookup"><span data-stu-id="5f265-126">hello top level stored procedure call equates toonest level 1</span></span>

```sql
EXEC prc_nesting
```
<span data-ttu-id="5f265-127">Se hello stored procedure effettua inoltre EXEC un'altra chiamata, ciò comporta un aumento too2 livello di nidificazione hello</span><span class="sxs-lookup"><span data-stu-id="5f265-127">If hello stored procedure also makes another EXEC call then this will increase hello nest level too2</span></span>

```sql
CREATE PROCEDURE prc_nesting
AS
EXEC prc_nesting_2  -- This call is nest level 2
GO
EXEC prc_nesting
```
<span data-ttu-id="5f265-128">Se seconda procedura hello viene quindi eseguito alcune istruzioni sql dinamiche quindi aumenterà too3 livello di nidificazione hello</span><span class="sxs-lookup"><span data-stu-id="5f265-128">If hello second procedure then executes some dynamic sql then this will increase hello nest level too3</span></span>

```sql
CREATE PROCEDURE prc_nesting_2
AS
EXEC sp_executesql 'SELECT 'another nest level'  -- This call is nest level 2
GO
EXEC prc_nesting
```

<span data-ttu-id="5f265-129">Tenere presente che SQL Data Warehouse attualmente non supporta @@NESTLEVEL.</span><span class="sxs-lookup"><span data-stu-id="5f265-129">Note SQL Data Warehouse does not currently support @@NESTLEVEL.</span></span> <span data-ttu-id="5f265-130">È necessario tookeep una traccia del livello di nidificazione manualmente.</span><span class="sxs-lookup"><span data-stu-id="5f265-130">You will need tookeep a track of your nest level yourself.</span></span> <span data-ttu-id="5f265-131">È improbabile che verrà raggiunto limite del livello di nidificazione hello 8, ma se non si sarà anche necessario toore lavoro il codice e "convertirla" in modo da adattarlo entro tale limite.</span><span class="sxs-lookup"><span data-stu-id="5f265-131">It is unlikely you will hit hello 8 nest level limit but if you do you will need toore-work your code and "flatten" it so that it fits within this limit.</span></span>

## <a name="insertexecute"></a><span data-ttu-id="5f265-132">INSERT..EXECUTE</span><span class="sxs-lookup"><span data-stu-id="5f265-132">INSERT..EXECUTE</span></span>
<span data-ttu-id="5f265-133">SQL Data Warehouse non consentono di set di risultati hello tooconsume di una stored procedure con un'istruzione INSERT.</span><span class="sxs-lookup"><span data-stu-id="5f265-133">SQL Data Warehouse does not permit you tooconsume hello result set of a stored procedure with an INSERT statement.</span></span> <span data-ttu-id="5f265-134">Si può tuttavia un approccio alternativo.</span><span class="sxs-lookup"><span data-stu-id="5f265-134">However, there is an alternative approach you can use.</span></span>

<span data-ttu-id="5f265-135">Vedere l'articolo seguente toohello [tabelle temporanee] per un esempio su come toodo questo.</span><span class="sxs-lookup"><span data-stu-id="5f265-135">Please refer toohello following article on [temporary tables] for an example on how toodo this.</span></span>

## <a name="limitations"></a><span data-ttu-id="5f265-136">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="5f265-136">Limitations</span></span>
<span data-ttu-id="5f265-137">Esistono alcuni aspetti delle stored procedure Transact-SQL che non sono implementate in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="5f265-137">There are some aspects of Transact-SQL stored procedures that are not implemented in SQL Data Warehouse.</span></span>

<span data-ttu-id="5f265-138">Sono:</span><span class="sxs-lookup"><span data-stu-id="5f265-138">They are:</span></span>

* <span data-ttu-id="5f265-139">Stored procedure temporanee</span><span class="sxs-lookup"><span data-stu-id="5f265-139">temporary stored procedures</span></span>
* <span data-ttu-id="5f265-140">Stored procedure numerate</span><span class="sxs-lookup"><span data-stu-id="5f265-140">numbered stored procedures</span></span>
* <span data-ttu-id="5f265-141">Stored procedure estese</span><span class="sxs-lookup"><span data-stu-id="5f265-141">extended stored procedures</span></span>
* <span data-ttu-id="5f265-142">Stored procedure CLR</span><span class="sxs-lookup"><span data-stu-id="5f265-142">CLR stored procedures</span></span>
* <span data-ttu-id="5f265-143">Opzione di crittografia</span><span class="sxs-lookup"><span data-stu-id="5f265-143">encryption option</span></span>
* <span data-ttu-id="5f265-144">Opzione di replica</span><span class="sxs-lookup"><span data-stu-id="5f265-144">replication option</span></span>
* <span data-ttu-id="5f265-145">Parametri con valori di tabella</span><span class="sxs-lookup"><span data-stu-id="5f265-145">table-valued parameters</span></span>
* <span data-ttu-id="5f265-146">Parametri di sola lettura</span><span class="sxs-lookup"><span data-stu-id="5f265-146">read-only parameters</span></span>
* <span data-ttu-id="5f265-147">Parametri predefiniti</span><span class="sxs-lookup"><span data-stu-id="5f265-147">default parameters</span></span>
* <span data-ttu-id="5f265-148">Contesti di esecuzione</span><span class="sxs-lookup"><span data-stu-id="5f265-148">execution contexts</span></span>
* <span data-ttu-id="5f265-149">Istruzione return</span><span class="sxs-lookup"><span data-stu-id="5f265-149">return statement</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f265-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5f265-150">Next steps</span></span>
<span data-ttu-id="5f265-151">Per altri suggerimenti sullo sviluppo, vedere la [panoramica dello sviluppo][development overview].</span><span class="sxs-lookup"><span data-stu-id="5f265-151">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[tabelle temporanee]: ./sql-data-warehouse-tables-temporary.md#modularizing-code
[development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[nest level]: https://msdn.microsoft.com/library/ms187371.aspx

<!--Other Web references-->
