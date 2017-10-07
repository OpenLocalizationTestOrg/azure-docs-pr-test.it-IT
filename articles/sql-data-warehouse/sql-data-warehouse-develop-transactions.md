---
title: in SQL Data Warehouse aaaTransactions | Documenti Microsoft
description: Suggerimenti per l'implementazione di transazioni in Azure SQL Data Warehouse per lo sviluppo di soluzioni.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: ae621788-e575-41f5-8bfe-fa04dc4b0b53
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 7c541648553238443b407666612561918096eb61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="transactions-in-sql-data-warehouse"></a><span data-ttu-id="589f0-103">Transazioni in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="589f0-103">Transactions in SQL Data Warehouse</span></span>
<span data-ttu-id="589f0-104">Come prevedibile, SQL Data Warehouse supporta le transazioni come parte del carico di lavoro di hello data warehouse.</span><span class="sxs-lookup"><span data-stu-id="589f0-104">As you would expect, SQL Data Warehouse supports transactions as part of hello data warehouse workload.</span></span> <span data-ttu-id="589f0-105">Prestazioni di hello tooensure di SQL Data Warehouse vengono comunque mantenute su larga scala, che alcune funzionalità sono limitate quando confrontati tooSQL Server.</span><span class="sxs-lookup"><span data-stu-id="589f0-105">However, tooensure hello performance of SQL Data Warehouse is maintained at scale some features are limited when compared tooSQL Server.</span></span> <span data-ttu-id="589f0-106">Questo articolo evidenzia le differenze di hello e gli elenchi di hello ad altri utenti.</span><span class="sxs-lookup"><span data-stu-id="589f0-106">This article highlights hello differences and lists hello others.</span></span> 

## <a name="transaction-isolation-levels"></a><span data-ttu-id="589f0-107">Livelli di isolamento delle transazioni</span><span class="sxs-lookup"><span data-stu-id="589f0-107">Transaction isolation levels</span></span>
<span data-ttu-id="589f0-108">SQL Data Warehouse implementa le transazioni ACID.</span><span class="sxs-lookup"><span data-stu-id="589f0-108">SQL Data Warehouse implements ACID transactions.</span></span> <span data-ttu-id="589f0-109">Tuttavia, l'isolamento del supporto transazionale hello hello è limitato troppo`READ UNCOMMITTED` e non può essere modificato.</span><span class="sxs-lookup"><span data-stu-id="589f0-109">However, hello Isolation of hello transactional support is limited too`READ UNCOMMITTED` and this cannot be changed.</span></span> <span data-ttu-id="589f0-110">È possibile implementare un numero di metodi di codifica tooprevent dirty legge dei dati se si tratta di un problema per l'utente.</span><span class="sxs-lookup"><span data-stu-id="589f0-110">You can implement a number of coding methods tooprevent dirty reads of data if this is a concern for you.</span></span> <span data-ttu-id="589f0-111">Hello metodi più diffusi sfruttano un'istruzione CTAS e cambio della partizione nella tabella (spesso noto come modello di finestra temporale scorrevole hello) tooprevent agli utenti di eseguire query sui dati che è ancora in corso di preparazione.</span><span class="sxs-lookup"><span data-stu-id="589f0-111">hello most popular methods leverage both CTAS and table partition switching (often known as hello sliding window pattern) tooprevent users from querying data that is still being prepared.</span></span> <span data-ttu-id="589f0-112">Visualizzazioni dati pre-filtro hello sono anche un approccio comune.</span><span class="sxs-lookup"><span data-stu-id="589f0-112">Views that pre-filter hello data is also a popular approach.</span></span>  

## <a name="transaction-size"></a><span data-ttu-id="589f0-113">Dimensioni delle transazioni</span><span class="sxs-lookup"><span data-stu-id="589f0-113">Transaction size</span></span>
<span data-ttu-id="589f0-114">Le dimensioni di una singola transazione di modifica dati sono limitate.</span><span class="sxs-lookup"><span data-stu-id="589f0-114">A single data modification transaction is limited in size.</span></span> <span data-ttu-id="589f0-115">oggi viene applicato il limite di Hello "per ogni distribuzione".</span><span class="sxs-lookup"><span data-stu-id="589f0-115">hello limit today is applied "per distribution".</span></span> <span data-ttu-id="589f0-116">Pertanto, l'allocazione totale hello può essere calcolato moltiplicando il limite di hello per il conteggio di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="589f0-116">Therefore, hello total allocation can be calculated by multiplying hello limit by hello distribution count.</span></span> <span data-ttu-id="589f0-117">numero massimo di hello tooapproximate di righe nella transazione hello divide perno distribuzione hello per dimensioni totali di hello di ogni riga.</span><span class="sxs-lookup"><span data-stu-id="589f0-117">tooapproximate hello maximum number of rows in hello transaction divide hello distribution cap by hello total size of each row.</span></span> <span data-ttu-id="589f0-118">Per prendere in considerazione le colonne a lunghezza variabile richiede una lunghezza di colonna medio anziché la dimensione massima di hello.</span><span class="sxs-lookup"><span data-stu-id="589f0-118">For variable length columns consider taking an average column length rather than using hello maximum size.</span></span>

<span data-ttu-id="589f0-119">Nella tabella hello seguito hello seguenti presupposti:</span><span class="sxs-lookup"><span data-stu-id="589f0-119">In hello table below hello following assumptions have been made:</span></span>

* <span data-ttu-id="589f0-120">Si è verificata una distribuzione uniforme dei dati</span><span class="sxs-lookup"><span data-stu-id="589f0-120">An even distribution of data has occurred</span></span> 
* <span data-ttu-id="589f0-121">lunghezza media della riga Hello è 250 byte</span><span class="sxs-lookup"><span data-stu-id="589f0-121">hello average row length is 250 bytes</span></span>

| <span data-ttu-id="589f0-122">[DWU][DWU]</span><span class="sxs-lookup"><span data-stu-id="589f0-122">[DWU][DWU]</span></span> | <span data-ttu-id="589f0-123">Limite per ogni distribuzione (GiB)</span><span class="sxs-lookup"><span data-stu-id="589f0-123">Cap per distribution (GiB)</span></span> | <span data-ttu-id="589f0-124">Numero di distribuzioni</span><span class="sxs-lookup"><span data-stu-id="589f0-124">Number of Distributions</span></span> | <span data-ttu-id="589f0-125">Dimensioni MAX delle transazioni (GiB)</span><span class="sxs-lookup"><span data-stu-id="589f0-125">MAX transaction size (GiB)</span></span> | <span data-ttu-id="589f0-126"># Righe per la distribuzione</span><span class="sxs-lookup"><span data-stu-id="589f0-126"># Rows per distribution</span></span> | <span data-ttu-id="589f0-127">Righe max per transazione</span><span class="sxs-lookup"><span data-stu-id="589f0-127">Max Rows per transaction</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="589f0-128">DW100</span><span class="sxs-lookup"><span data-stu-id="589f0-128">DW100</span></span> |<span data-ttu-id="589f0-129">1</span><span class="sxs-lookup"><span data-stu-id="589f0-129">1</span></span> |<span data-ttu-id="589f0-130">60</span><span class="sxs-lookup"><span data-stu-id="589f0-130">60</span></span> |<span data-ttu-id="589f0-131">60</span><span class="sxs-lookup"><span data-stu-id="589f0-131">60</span></span> |<span data-ttu-id="589f0-132">4.000.000</span><span class="sxs-lookup"><span data-stu-id="589f0-132">4,000,000</span></span> |<span data-ttu-id="589f0-133">240.000.000</span><span class="sxs-lookup"><span data-stu-id="589f0-133">240,000,000</span></span> |
| <span data-ttu-id="589f0-134">DW200</span><span class="sxs-lookup"><span data-stu-id="589f0-134">DW200</span></span> |<span data-ttu-id="589f0-135">1,5</span><span class="sxs-lookup"><span data-stu-id="589f0-135">1.5</span></span> |<span data-ttu-id="589f0-136">60</span><span class="sxs-lookup"><span data-stu-id="589f0-136">60</span></span> |<span data-ttu-id="589f0-137">90</span><span class="sxs-lookup"><span data-stu-id="589f0-137">90</span></span> |<span data-ttu-id="589f0-138">6.000.000</span><span class="sxs-lookup"><span data-stu-id="589f0-138">6,000,000</span></span> |<span data-ttu-id="589f0-139">360.000.000</span><span class="sxs-lookup"><span data-stu-id="589f0-139">360,000,000</span></span> |
| <span data-ttu-id="589f0-140">DW300</span><span class="sxs-lookup"><span data-stu-id="589f0-140">DW300</span></span> |<span data-ttu-id="589f0-141">2.25</span><span class="sxs-lookup"><span data-stu-id="589f0-141">2.25</span></span> |<span data-ttu-id="589f0-142">60</span><span class="sxs-lookup"><span data-stu-id="589f0-142">60</span></span> |<span data-ttu-id="589f0-143">135</span><span class="sxs-lookup"><span data-stu-id="589f0-143">135</span></span> |<span data-ttu-id="589f0-144">9.000.000</span><span class="sxs-lookup"><span data-stu-id="589f0-144">9,000,000</span></span> |<span data-ttu-id="589f0-145">540.000.000</span><span class="sxs-lookup"><span data-stu-id="589f0-145">540,000,000</span></span> |
| <span data-ttu-id="589f0-146">DW400</span><span class="sxs-lookup"><span data-stu-id="589f0-146">DW400</span></span> |<span data-ttu-id="589f0-147">3</span><span class="sxs-lookup"><span data-stu-id="589f0-147">3</span></span> |<span data-ttu-id="589f0-148">60</span><span class="sxs-lookup"><span data-stu-id="589f0-148">60</span></span> |<span data-ttu-id="589f0-149">180</span><span class="sxs-lookup"><span data-stu-id="589f0-149">180</span></span> |<span data-ttu-id="589f0-150">12.000.000</span><span class="sxs-lookup"><span data-stu-id="589f0-150">12,000,000</span></span> |<span data-ttu-id="589f0-151">720.000.000</span><span class="sxs-lookup"><span data-stu-id="589f0-151">720,000,000</span></span> |
| <span data-ttu-id="589f0-152">DW500</span><span class="sxs-lookup"><span data-stu-id="589f0-152">DW500</span></span> |<span data-ttu-id="589f0-153">3,75</span><span class="sxs-lookup"><span data-stu-id="589f0-153">3.75</span></span> |<span data-ttu-id="589f0-154">60</span><span class="sxs-lookup"><span data-stu-id="589f0-154">60</span></span> |<span data-ttu-id="589f0-155">225</span><span class="sxs-lookup"><span data-stu-id="589f0-155">225</span></span> |<span data-ttu-id="589f0-156">15.000.000</span><span class="sxs-lookup"><span data-stu-id="589f0-156">15,000,000</span></span> |<span data-ttu-id="589f0-157">900.000.000</span><span class="sxs-lookup"><span data-stu-id="589f0-157">900,000,000</span></span> |
| <span data-ttu-id="589f0-158">DW600</span><span class="sxs-lookup"><span data-stu-id="589f0-158">DW600</span></span> |<span data-ttu-id="589f0-159">4.5</span><span class="sxs-lookup"><span data-stu-id="589f0-159">4.5</span></span> |<span data-ttu-id="589f0-160">60</span><span class="sxs-lookup"><span data-stu-id="589f0-160">60</span></span> |<span data-ttu-id="589f0-161">270</span><span class="sxs-lookup"><span data-stu-id="589f0-161">270</span></span> |<span data-ttu-id="589f0-162">18.000.000</span><span class="sxs-lookup"><span data-stu-id="589f0-162">18,000,000</span></span> |<span data-ttu-id="589f0-163">1.080.000.000</span><span class="sxs-lookup"><span data-stu-id="589f0-163">1,080,000,000</span></span> |
| <span data-ttu-id="589f0-164">DW1000</span><span class="sxs-lookup"><span data-stu-id="589f0-164">DW1000</span></span> |<span data-ttu-id="589f0-165">7.5</span><span class="sxs-lookup"><span data-stu-id="589f0-165">7.5</span></span> |<span data-ttu-id="589f0-166">60</span><span class="sxs-lookup"><span data-stu-id="589f0-166">60</span></span> |<span data-ttu-id="589f0-167">450</span><span class="sxs-lookup"><span data-stu-id="589f0-167">450</span></span> |<span data-ttu-id="589f0-168">30.000.000</span><span class="sxs-lookup"><span data-stu-id="589f0-168">30,000,000</span></span> |<span data-ttu-id="589f0-169">1.800.000.000</span><span class="sxs-lookup"><span data-stu-id="589f0-169">1,800,000,000</span></span> |
| <span data-ttu-id="589f0-170">DW1200</span><span class="sxs-lookup"><span data-stu-id="589f0-170">DW1200</span></span> |<span data-ttu-id="589f0-171">9</span><span class="sxs-lookup"><span data-stu-id="589f0-171">9</span></span> |<span data-ttu-id="589f0-172">60</span><span class="sxs-lookup"><span data-stu-id="589f0-172">60</span></span> |<span data-ttu-id="589f0-173">540</span><span class="sxs-lookup"><span data-stu-id="589f0-173">540</span></span> |<span data-ttu-id="589f0-174">36.000.000</span><span class="sxs-lookup"><span data-stu-id="589f0-174">36,000,000</span></span> |<span data-ttu-id="589f0-175">2.160.000.000</span><span class="sxs-lookup"><span data-stu-id="589f0-175">2,160,000,000</span></span> |
| <span data-ttu-id="589f0-176">DW1500</span><span class="sxs-lookup"><span data-stu-id="589f0-176">DW1500</span></span> |<span data-ttu-id="589f0-177">11,25</span><span class="sxs-lookup"><span data-stu-id="589f0-177">11.25</span></span> |<span data-ttu-id="589f0-178">60</span><span class="sxs-lookup"><span data-stu-id="589f0-178">60</span></span> |<span data-ttu-id="589f0-179">675</span><span class="sxs-lookup"><span data-stu-id="589f0-179">675</span></span> |<span data-ttu-id="589f0-180">45.000.000</span><span class="sxs-lookup"><span data-stu-id="589f0-180">45,000,000</span></span> |<span data-ttu-id="589f0-181">2.700.000.000</span><span class="sxs-lookup"><span data-stu-id="589f0-181">2,700,000,000</span></span> |
| <span data-ttu-id="589f0-182">DW2000</span><span class="sxs-lookup"><span data-stu-id="589f0-182">DW2000</span></span> |<span data-ttu-id="589f0-183">15</span><span class="sxs-lookup"><span data-stu-id="589f0-183">15</span></span> |<span data-ttu-id="589f0-184">60</span><span class="sxs-lookup"><span data-stu-id="589f0-184">60</span></span> |<span data-ttu-id="589f0-185">900</span><span class="sxs-lookup"><span data-stu-id="589f0-185">900</span></span> |<span data-ttu-id="589f0-186">60.000.000</span><span class="sxs-lookup"><span data-stu-id="589f0-186">60,000,000</span></span> |<span data-ttu-id="589f0-187">3.600.000.000</span><span class="sxs-lookup"><span data-stu-id="589f0-187">3,600,000,000</span></span> |
| <span data-ttu-id="589f0-188">DW3000</span><span class="sxs-lookup"><span data-stu-id="589f0-188">DW3000</span></span> |<span data-ttu-id="589f0-189">22,5</span><span class="sxs-lookup"><span data-stu-id="589f0-189">22.5</span></span> |<span data-ttu-id="589f0-190">60</span><span class="sxs-lookup"><span data-stu-id="589f0-190">60</span></span> |<span data-ttu-id="589f0-191">1.350</span><span class="sxs-lookup"><span data-stu-id="589f0-191">1,350</span></span> |<span data-ttu-id="589f0-192">90.000.000</span><span class="sxs-lookup"><span data-stu-id="589f0-192">90,000,000</span></span> |<span data-ttu-id="589f0-193">5.400.000.000</span><span class="sxs-lookup"><span data-stu-id="589f0-193">5,400,000,000</span></span> |
| <span data-ttu-id="589f0-194">DW6000</span><span class="sxs-lookup"><span data-stu-id="589f0-194">DW6000</span></span> |<span data-ttu-id="589f0-195">45</span><span class="sxs-lookup"><span data-stu-id="589f0-195">45</span></span> |<span data-ttu-id="589f0-196">60</span><span class="sxs-lookup"><span data-stu-id="589f0-196">60</span></span> |<span data-ttu-id="589f0-197">2.700</span><span class="sxs-lookup"><span data-stu-id="589f0-197">2,700</span></span> |<span data-ttu-id="589f0-198">180.000.000</span><span class="sxs-lookup"><span data-stu-id="589f0-198">180,000,000</span></span> |<span data-ttu-id="589f0-199">10.800.000.000</span><span class="sxs-lookup"><span data-stu-id="589f0-199">10,800,000,000</span></span> |

<span data-ttu-id="589f0-200">limite delle dimensioni delle transazioni Hello viene applicato per ogni transazione o operazione.</span><span class="sxs-lookup"><span data-stu-id="589f0-200">hello transaction size limit is applied per transaction or operation.</span></span> <span data-ttu-id="589f0-201">Non viene applicato in tutte le transazioni simultanee.</span><span class="sxs-lookup"><span data-stu-id="589f0-201">It is not applied across all concurrent transactions.</span></span> <span data-ttu-id="589f0-202">Pertanto ogni transazione è consentito toowrite questa quantità di dati toohello log.</span><span class="sxs-lookup"><span data-stu-id="589f0-202">Therefore each transaction is permitted toowrite this amount of data toohello log.</span></span> 

<span data-ttu-id="589f0-203">toooptimize e ridurre al minimo la quantità hello dei dati scritti toohello log, vedere toohello [procedure consigliate per le transazioni] [ Transactions best practices] articolo.</span><span class="sxs-lookup"><span data-stu-id="589f0-203">toooptimize and minimize hello amount of data written toohello log please refer toohello [Transactions best practices][Transactions best practices] article.</span></span>

> [!WARNING]
> <span data-ttu-id="589f0-204">massima dimensione delle transazioni può essere ottenuta solo HASH o tabelle ROUND_ROBIN distribuiti in cui di diffondersi hello hello dati Hello è pari.</span><span class="sxs-lookup"><span data-stu-id="589f0-204">hello maximum transaction size can only be achieved for HASH or ROUND_ROBIN distributed tables where hello spread of hello data is even.</span></span> <span data-ttu-id="589f0-205">Se la transazione hello scrive i dati in modo asimmetrici toohello distribuzioni quindi hello limite è probabilmente toobe raggiunto dimensioni di transazione massimo toohello precedente.</span><span class="sxs-lookup"><span data-stu-id="589f0-205">If hello transaction is writing data in a skewed fashion toohello distributions then hello limit is likely toobe reached prior toohello maximum transaction size.</span></span>
> <!--REPLICATED_TABLE-->
> 
> 

## <a name="transaction-state"></a><span data-ttu-id="589f0-206">Stato della transazione</span><span class="sxs-lookup"><span data-stu-id="589f0-206">Transaction state</span></span>
<span data-ttu-id="589f0-207">SQL Data Warehouse utilizza hello xact_state funzione tooreport una transazione non riuscita con il valore di hello -2.</span><span class="sxs-lookup"><span data-stu-id="589f0-207">SQL Data Warehouse uses hello XACT_STATE() function tooreport a failed transaction using hello value -2.</span></span> <span data-ttu-id="589f0-208">Ciò significa che la transazione hello non è riuscita ed è contrassegnata per il rollback solo</span><span class="sxs-lookup"><span data-stu-id="589f0-208">This means that hello transaction has failed and is marked for rollback only</span></span>

> [!NOTE]
> <span data-ttu-id="589f0-209">Hello utilizzare-2 hello XACT_STATE funzione toodenote un tooSQL di un comportamento diverso rappresenta Server transazione non riuscita.</span><span class="sxs-lookup"><span data-stu-id="589f0-209">hello use of -2 by hello XACT_STATE function toodenote a failed transaction represents different behavior tooSQL Server.</span></span> <span data-ttu-id="589f0-210">SQL Server utilizza hello valore -1 toorepresent una transazione non eseguire il commit.</span><span class="sxs-lookup"><span data-stu-id="589f0-210">SQL Server uses hello value -1 toorepresent an un-committable transaction.</span></span> <span data-ttu-id="589f0-211">SQL Server è in grado di tollerare errori all'interno di una transazione senza che questo disponga toobe contrassegnato come non eseguire il commit.</span><span class="sxs-lookup"><span data-stu-id="589f0-211">SQL Server can tolerate some errors inside a transaction without it having toobe marked as un-committable.</span></span> <span data-ttu-id="589f0-212">Ad esempio, `SELECT 1/0` causa un errore, ma non applica alla transazione lo stato per cui non è possibile eseguire il commit.</span><span class="sxs-lookup"><span data-stu-id="589f0-212">For example `SELECT 1/0` would cause an error but not force a transaction into an un-committable state.</span></span> <span data-ttu-id="589f0-213">SQL Server consente inoltre di operazioni di lettura nella transazione non eseguire il commit di hello.</span><span class="sxs-lookup"><span data-stu-id="589f0-213">SQL Server also permits reads in hello un-committable transaction.</span></span> <span data-ttu-id="589f0-214">SQL Data Warehouse, invece, non consente questa operazione.</span><span class="sxs-lookup"><span data-stu-id="589f0-214">However, SQL Data Warehouse does not let you do this.</span></span> <span data-ttu-id="589f0-215">Se si verifica un errore in una transazione SQL Data Warehouse passerà automaticamente allo stato hello -2 e non sarà in grado di toomake eventuali altre istruzioni select fino a quando non è stato eseguito il rollback dell'istruzione hello.</span><span class="sxs-lookup"><span data-stu-id="589f0-215">If an error occurs inside a SQL Data Warehouse transaction it will automatically enter hello -2 state and you will not be able toomake any further select statements until hello statement has been rolled back.</span></span> <span data-ttu-id="589f0-216">È pertanto importante toocheck che il codice di applicazione toosee se utilizza xact_state come si potrebbe essere necessario toomake modifiche del codice.</span><span class="sxs-lookup"><span data-stu-id="589f0-216">It is therefore important toocheck that your application code toosee if it uses  XACT_STATE() as you may need toomake code modifications.</span></span>
> 
> 

<span data-ttu-id="589f0-217">Ad esempio, in SQL Server potrebbe essere visualizzata una transazione simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="589f0-217">For example, in SQL Server you might see a transaction that looks like this:</span></span>

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

<span data-ttu-id="589f0-218">Se si lascia il codice perché è di sopra verrà visualizzato hello seguente messaggio di errore:</span><span class="sxs-lookup"><span data-stu-id="589f0-218">If you leave your code as it is above then you will get hello following error message:</span></span>

<span data-ttu-id="589f0-219">Messaggio 111233, livello 16, stato 1, riga 1 111233; hello corrente transazione è stata interrotta e le modifiche in sospeso sottoposta a rollback.</span><span class="sxs-lookup"><span data-stu-id="589f0-219">Msg 111233, Level 16, State 1, Line 1 111233;hello current transaction has aborted, and any pending changes have been rolled back.</span></span> <span data-ttu-id="589f0-220">Causa: non è stato eseguito il rollback in modo esplicito di una transazione in uno stato di solo rollback prima di un'istruzione DDL, DML o SELECT.</span><span class="sxs-lookup"><span data-stu-id="589f0-220">Cause: A transaction in a rollback-only state was not explicitly rolled back before a DDL, DML or SELECT statement.</span></span>

<span data-ttu-id="589f0-221">Potranno inoltre ottenere output di hello di errore. il * funzioni hello non.</span><span class="sxs-lookup"><span data-stu-id="589f0-221">You will also not get hello output of hello ERROR_* functions.</span></span>

<span data-ttu-id="589f0-222">In SQL Data Warehouse codice hello deve toobe leggermente modificato:</span><span class="sxs-lookup"><span data-stu-id="589f0-222">In SQL Data Warehouse hello code needs toobe slightly altered:</span></span>

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;
    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

<span data-ttu-id="589f0-223">Hello previsto ora venga rispettato il comportamento.</span><span class="sxs-lookup"><span data-stu-id="589f0-223">hello expected behavior is now observed.</span></span> <span data-ttu-id="589f0-224">Errore Hello in transazione hello è gestito ed errore. il * funzioni hello forniscono i valori come previsto.</span><span class="sxs-lookup"><span data-stu-id="589f0-224">hello error in hello transaction is managed and hello ERROR_* functions provide values as expected.</span></span>

<span data-ttu-id="589f0-225">Tutto ciò che è stata modificata è che hello `ROLLBACK` di hello transazione era toohappen prima hello lettura delle informazioni di errore hello in hello `CATCH` blocco.</span><span class="sxs-lookup"><span data-stu-id="589f0-225">All that has changed is that hello `ROLLBACK` of hello transaction had toohappen before hello read of hello error information in hello `CATCH` block.</span></span>

## <a name="errorline-function"></a><span data-ttu-id="589f0-226">Funzione Error_Line()</span><span class="sxs-lookup"><span data-stu-id="589f0-226">Error_Line() function</span></span>
<span data-ttu-id="589f0-227">È inoltre importante notare che SQL Data Warehouse non è in implementare o funzione di hello error_line ().</span><span class="sxs-lookup"><span data-stu-id="589f0-227">It is also worth noting that SQL Data Warehouse does not implement or support hello ERROR_LINE() function.</span></span> <span data-ttu-id="589f0-228">Se hai nel codice, è necessario tooremove è toobe conforme a SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="589f0-228">If you have this in your code you will need tooremove it toobe compliant with SQL Data Warehouse.</span></span> <span data-ttu-id="589f0-229">Utilizzare le etichette di query nel codice tooimplement una funzionalità equivalente.</span><span class="sxs-lookup"><span data-stu-id="589f0-229">Use query labels in your code instead tooimplement equivalent functionality.</span></span> <span data-ttu-id="589f0-230">Consultare toohello [etichetta] [ LABEL] articolo per ulteriori informazioni su questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="589f0-230">Please refer toohello [LABEL][LABEL] article for more details on this feature.</span></span>

## <a name="using-throw-and-raiserror"></a><span data-ttu-id="589f0-231">Uso di THROW e RAISERROR</span><span class="sxs-lookup"><span data-stu-id="589f0-231">Using THROW and RAISERROR</span></span>
<span data-ttu-id="589f0-232">THROW è hello più moderno implementazione per la generazione di eccezioni in SQL Data Warehouse ma è supportato anche RAISERROR.</span><span class="sxs-lookup"><span data-stu-id="589f0-232">THROW is hello more modern implementation for raising exceptions in SQL Data Warehouse but RAISERROR is also supported.</span></span> <span data-ttu-id="589f0-233">Esistono alcune differenze che vale la pena prestando attenzione toohowever.</span><span class="sxs-lookup"><span data-stu-id="589f0-233">There are a few differences that are worth paying attention toohowever.</span></span>

* <span data-ttu-id="589f0-234">I numeri non possono essere hello 100.000 a 150.000 intervallo per la generazione di messaggi di errore definiti dall'utente</span><span class="sxs-lookup"><span data-stu-id="589f0-234">User defined error messages numbers cannot be in hello 100,000 - 150,000 range for THROW</span></span>
* <span data-ttu-id="589f0-235">I messaggi di errore di RAISERROR sono fissati a 50.000.</span><span class="sxs-lookup"><span data-stu-id="589f0-235">RAISERROR error messages are fixed at 50,000</span></span>
* <span data-ttu-id="589f0-236">L'uso di sys.messages non è supportato.</span><span class="sxs-lookup"><span data-stu-id="589f0-236">Use of sys.messages is not supported</span></span>

## <a name="limitiations"></a><span data-ttu-id="589f0-237">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="589f0-237">Limitiations</span></span>
<span data-ttu-id="589f0-238">SQL Data Warehouse sono poche altre restrizioni relativi tootransactions.</span><span class="sxs-lookup"><span data-stu-id="589f0-238">SQL Data Warehouse does have a few other restrictions that relate tootransactions.</span></span>

<span data-ttu-id="589f0-239">Ecco quali sono:</span><span class="sxs-lookup"><span data-stu-id="589f0-239">They are as follows:</span></span>

* <span data-ttu-id="589f0-240">Nessuna transazione distribuita</span><span class="sxs-lookup"><span data-stu-id="589f0-240">No distributed transactions</span></span>
* <span data-ttu-id="589f0-241">Non sono consentite transazioni annidate</span><span class="sxs-lookup"><span data-stu-id="589f0-241">No nested transactions permitted</span></span>
* <span data-ttu-id="589f0-242">Non sono consentiti punti di salvataggio</span><span class="sxs-lookup"><span data-stu-id="589f0-242">No save points allowed</span></span>
* <span data-ttu-id="589f0-243">Nessuna transazione denominata</span><span class="sxs-lookup"><span data-stu-id="589f0-243">No named transactions</span></span>
* <span data-ttu-id="589f0-244">Nessuna transazione contrassegnata</span><span class="sxs-lookup"><span data-stu-id="589f0-244">No marked transactions</span></span>
* <span data-ttu-id="589f0-245">Nessun supporto per DDL come `CREATE TABLE` all'interno di una transazione definita dall'utente</span><span class="sxs-lookup"><span data-stu-id="589f0-245">No support for DDL such as `CREATE TABLE` inside a user defined transaction</span></span>

## <a name="next-steps"></a><span data-ttu-id="589f0-246">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="589f0-246">Next steps</span></span>
<span data-ttu-id="589f0-247">toolearn più sull'ottimizzazione delle transazioni, vedere [procedure consigliate per le transazioni][Transactions best practices].</span><span class="sxs-lookup"><span data-stu-id="589f0-247">toolearn more about optimizing transactions, see [Transactions best practices][Transactions best practices].</span></span>  <span data-ttu-id="589f0-248">toolearn su altre procedure consigliate di SQL Data Warehouse, vedere [le procedure consigliate di SQL Data Warehouse][SQL Data Warehouse best practices].</span><span class="sxs-lookup"><span data-stu-id="589f0-248">toolearn about other SQL Data Warehouse best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse best practices].</span></span>

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Transactions best practices]: ./sql-data-warehouse-develop-best-practices-transactions.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->

<!--Other Web references-->
