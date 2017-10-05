---
title: Transazioni in SQL Data Warehouse | Documentazione Microsoft
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
ms.openlocfilehash: 29d53e18539f2c24dd64090b2ac6f9dd4c783961
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="transactions-in-sql-data-warehouse"></a><span data-ttu-id="4e6ee-103">Transazioni in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="4e6ee-103">Transactions in SQL Data Warehouse</span></span>
<span data-ttu-id="4e6ee-104">Come si può immaginare, SQL Data Warehouse supporta le transazioni come parte del carico di lavoro del data warehouse.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-104">As you would expect, SQL Data Warehouse supports transactions as part of the data warehouse workload.</span></span> <span data-ttu-id="4e6ee-105">Tuttavia, per garantire che le prestazioni di SQL Data Warehouse siano mantenute al massimo livello, alcune funzionalità sono limitate rispetto a SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-105">However, to ensure the performance of SQL Data Warehouse is maintained at scale some features are limited when compared to SQL Server.</span></span> <span data-ttu-id="4e6ee-106">Questo articolo evidenzia le differenze ed elenca le altre.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-106">This article highlights the differences and lists the others.</span></span> 

## <a name="transaction-isolation-levels"></a><span data-ttu-id="4e6ee-107">Livelli di isolamento delle transazioni</span><span class="sxs-lookup"><span data-stu-id="4e6ee-107">Transaction isolation levels</span></span>
<span data-ttu-id="4e6ee-108">SQL Data Warehouse implementa le transazioni ACID.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-108">SQL Data Warehouse implements ACID transactions.</span></span> <span data-ttu-id="4e6ee-109">Tuttavia, l'isolamento del supporto delle transazioni è limitato a `READ UNCOMMITTED` e non può essere modificato.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-109">However, the Isolation of the transactional support is limited to `READ UNCOMMITTED` and this cannot be changed.</span></span> <span data-ttu-id="4e6ee-110">È possibile implementare numerosi metodi di codifica per evitare letture dirty dei dati se ciò costituisce un problema.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-110">You can implement a number of coding methods to prevent dirty reads of data if this is a concern for you.</span></span> <span data-ttu-id="4e6ee-111">I metodi più diffusi usano CTAS e il cambio della partizione di tabella (spesso noto come modello di finestra temporale scorrevole) per impedire agli utenti di eseguire query sui dati ancora in fase di preparazione.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-111">The most popular methods leverage both CTAS and table partition switching (often known as the sliding window pattern) to prevent users from querying data that is still being prepared.</span></span> <span data-ttu-id="4e6ee-112">Anche le visualizzazioni che filtrano preventivamente i dati costituiscono un approccio comune.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-112">Views that pre-filter the data is also a popular approach.</span></span>  

## <a name="transaction-size"></a><span data-ttu-id="4e6ee-113">Dimensioni delle transazioni</span><span class="sxs-lookup"><span data-stu-id="4e6ee-113">Transaction size</span></span>
<span data-ttu-id="4e6ee-114">Le dimensioni di una singola transazione di modifica dati sono limitate.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-114">A single data modification transaction is limited in size.</span></span> <span data-ttu-id="4e6ee-115">Il limite è attualmente applicato "per ogni distribuzione".</span><span class="sxs-lookup"><span data-stu-id="4e6ee-115">The limit today is applied "per distribution".</span></span> <span data-ttu-id="4e6ee-116">Per calcolare l'allocazione totale, quindi, è possibile moltiplicare il limite per il conteggio di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-116">Therefore, the total allocation can be calculated by multiplying the limit by the distribution count.</span></span> <span data-ttu-id="4e6ee-117">Per calcolare approssimativamente il numero massimo di righe nella transazione, dividere il limite di distribuzione per le dimensioni totali di ogni riga.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-117">To approximate the maximum number of rows in the transaction divide the distribution cap by the total size of each row.</span></span> <span data-ttu-id="4e6ee-118">Per le colonne di lunghezza variabile valutare la possibilità di usare una lunghezza di colonna media invece delle dimensioni massime.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-118">For variable length columns consider taking an average column length rather than using the maximum size.</span></span>

<span data-ttu-id="4e6ee-119">Ecco alcuni presupposti riportati nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="4e6ee-119">In the table below the following assumptions have been made:</span></span>

* <span data-ttu-id="4e6ee-120">Si è verificata una distribuzione uniforme dei dati</span><span class="sxs-lookup"><span data-stu-id="4e6ee-120">An even distribution of data has occurred</span></span> 
* <span data-ttu-id="4e6ee-121">La lunghezza media delle righe è 250 byte</span><span class="sxs-lookup"><span data-stu-id="4e6ee-121">The average row length is 250 bytes</span></span>

| <span data-ttu-id="4e6ee-122">[DWU][DWU]</span><span class="sxs-lookup"><span data-stu-id="4e6ee-122">[DWU][DWU]</span></span> | <span data-ttu-id="4e6ee-123">Limite per ogni distribuzione (GiB)</span><span class="sxs-lookup"><span data-stu-id="4e6ee-123">Cap per distribution (GiB)</span></span> | <span data-ttu-id="4e6ee-124">Numero di distribuzioni</span><span class="sxs-lookup"><span data-stu-id="4e6ee-124">Number of Distributions</span></span> | <span data-ttu-id="4e6ee-125">Dimensioni MAX delle transazioni (GiB)</span><span class="sxs-lookup"><span data-stu-id="4e6ee-125">MAX transaction size (GiB)</span></span> | <span data-ttu-id="4e6ee-126"># Righe per la distribuzione</span><span class="sxs-lookup"><span data-stu-id="4e6ee-126"># Rows per distribution</span></span> | <span data-ttu-id="4e6ee-127">Righe max per transazione</span><span class="sxs-lookup"><span data-stu-id="4e6ee-127">Max Rows per transaction</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="4e6ee-128">DW100</span><span class="sxs-lookup"><span data-stu-id="4e6ee-128">DW100</span></span> |<span data-ttu-id="4e6ee-129">1</span><span class="sxs-lookup"><span data-stu-id="4e6ee-129">1</span></span> |<span data-ttu-id="4e6ee-130">60</span><span class="sxs-lookup"><span data-stu-id="4e6ee-130">60</span></span> |<span data-ttu-id="4e6ee-131">60</span><span class="sxs-lookup"><span data-stu-id="4e6ee-131">60</span></span> |<span data-ttu-id="4e6ee-132">4.000.000</span><span class="sxs-lookup"><span data-stu-id="4e6ee-132">4,000,000</span></span> |<span data-ttu-id="4e6ee-133">240.000.000</span><span class="sxs-lookup"><span data-stu-id="4e6ee-133">240,000,000</span></span> |
| <span data-ttu-id="4e6ee-134">DW200</span><span class="sxs-lookup"><span data-stu-id="4e6ee-134">DW200</span></span> |<span data-ttu-id="4e6ee-135">1,5</span><span class="sxs-lookup"><span data-stu-id="4e6ee-135">1.5</span></span> |<span data-ttu-id="4e6ee-136">60</span><span class="sxs-lookup"><span data-stu-id="4e6ee-136">60</span></span> |<span data-ttu-id="4e6ee-137">90</span><span class="sxs-lookup"><span data-stu-id="4e6ee-137">90</span></span> |<span data-ttu-id="4e6ee-138">6.000.000</span><span class="sxs-lookup"><span data-stu-id="4e6ee-138">6,000,000</span></span> |<span data-ttu-id="4e6ee-139">360.000.000</span><span class="sxs-lookup"><span data-stu-id="4e6ee-139">360,000,000</span></span> |
| <span data-ttu-id="4e6ee-140">DW300</span><span class="sxs-lookup"><span data-stu-id="4e6ee-140">DW300</span></span> |<span data-ttu-id="4e6ee-141">2.25</span><span class="sxs-lookup"><span data-stu-id="4e6ee-141">2.25</span></span> |<span data-ttu-id="4e6ee-142">60</span><span class="sxs-lookup"><span data-stu-id="4e6ee-142">60</span></span> |<span data-ttu-id="4e6ee-143">135</span><span class="sxs-lookup"><span data-stu-id="4e6ee-143">135</span></span> |<span data-ttu-id="4e6ee-144">9.000.000</span><span class="sxs-lookup"><span data-stu-id="4e6ee-144">9,000,000</span></span> |<span data-ttu-id="4e6ee-145">540.000.000</span><span class="sxs-lookup"><span data-stu-id="4e6ee-145">540,000,000</span></span> |
| <span data-ttu-id="4e6ee-146">DW400</span><span class="sxs-lookup"><span data-stu-id="4e6ee-146">DW400</span></span> |<span data-ttu-id="4e6ee-147">3</span><span class="sxs-lookup"><span data-stu-id="4e6ee-147">3</span></span> |<span data-ttu-id="4e6ee-148">60</span><span class="sxs-lookup"><span data-stu-id="4e6ee-148">60</span></span> |<span data-ttu-id="4e6ee-149">180</span><span class="sxs-lookup"><span data-stu-id="4e6ee-149">180</span></span> |<span data-ttu-id="4e6ee-150">12.000.000</span><span class="sxs-lookup"><span data-stu-id="4e6ee-150">12,000,000</span></span> |<span data-ttu-id="4e6ee-151">720.000.000</span><span class="sxs-lookup"><span data-stu-id="4e6ee-151">720,000,000</span></span> |
| <span data-ttu-id="4e6ee-152">DW500</span><span class="sxs-lookup"><span data-stu-id="4e6ee-152">DW500</span></span> |<span data-ttu-id="4e6ee-153">3,75</span><span class="sxs-lookup"><span data-stu-id="4e6ee-153">3.75</span></span> |<span data-ttu-id="4e6ee-154">60</span><span class="sxs-lookup"><span data-stu-id="4e6ee-154">60</span></span> |<span data-ttu-id="4e6ee-155">225</span><span class="sxs-lookup"><span data-stu-id="4e6ee-155">225</span></span> |<span data-ttu-id="4e6ee-156">15.000.000</span><span class="sxs-lookup"><span data-stu-id="4e6ee-156">15,000,000</span></span> |<span data-ttu-id="4e6ee-157">900.000.000</span><span class="sxs-lookup"><span data-stu-id="4e6ee-157">900,000,000</span></span> |
| <span data-ttu-id="4e6ee-158">DW600</span><span class="sxs-lookup"><span data-stu-id="4e6ee-158">DW600</span></span> |<span data-ttu-id="4e6ee-159">4.5</span><span class="sxs-lookup"><span data-stu-id="4e6ee-159">4.5</span></span> |<span data-ttu-id="4e6ee-160">60</span><span class="sxs-lookup"><span data-stu-id="4e6ee-160">60</span></span> |<span data-ttu-id="4e6ee-161">270</span><span class="sxs-lookup"><span data-stu-id="4e6ee-161">270</span></span> |<span data-ttu-id="4e6ee-162">18.000.000</span><span class="sxs-lookup"><span data-stu-id="4e6ee-162">18,000,000</span></span> |<span data-ttu-id="4e6ee-163">1.080.000.000</span><span class="sxs-lookup"><span data-stu-id="4e6ee-163">1,080,000,000</span></span> |
| <span data-ttu-id="4e6ee-164">DW1000</span><span class="sxs-lookup"><span data-stu-id="4e6ee-164">DW1000</span></span> |<span data-ttu-id="4e6ee-165">7.5</span><span class="sxs-lookup"><span data-stu-id="4e6ee-165">7.5</span></span> |<span data-ttu-id="4e6ee-166">60</span><span class="sxs-lookup"><span data-stu-id="4e6ee-166">60</span></span> |<span data-ttu-id="4e6ee-167">450</span><span class="sxs-lookup"><span data-stu-id="4e6ee-167">450</span></span> |<span data-ttu-id="4e6ee-168">30.000.000</span><span class="sxs-lookup"><span data-stu-id="4e6ee-168">30,000,000</span></span> |<span data-ttu-id="4e6ee-169">1.800.000.000</span><span class="sxs-lookup"><span data-stu-id="4e6ee-169">1,800,000,000</span></span> |
| <span data-ttu-id="4e6ee-170">DW1200</span><span class="sxs-lookup"><span data-stu-id="4e6ee-170">DW1200</span></span> |<span data-ttu-id="4e6ee-171">9</span><span class="sxs-lookup"><span data-stu-id="4e6ee-171">9</span></span> |<span data-ttu-id="4e6ee-172">60</span><span class="sxs-lookup"><span data-stu-id="4e6ee-172">60</span></span> |<span data-ttu-id="4e6ee-173">540</span><span class="sxs-lookup"><span data-stu-id="4e6ee-173">540</span></span> |<span data-ttu-id="4e6ee-174">36.000.000</span><span class="sxs-lookup"><span data-stu-id="4e6ee-174">36,000,000</span></span> |<span data-ttu-id="4e6ee-175">2.160.000.000</span><span class="sxs-lookup"><span data-stu-id="4e6ee-175">2,160,000,000</span></span> |
| <span data-ttu-id="4e6ee-176">DW1500</span><span class="sxs-lookup"><span data-stu-id="4e6ee-176">DW1500</span></span> |<span data-ttu-id="4e6ee-177">11,25</span><span class="sxs-lookup"><span data-stu-id="4e6ee-177">11.25</span></span> |<span data-ttu-id="4e6ee-178">60</span><span class="sxs-lookup"><span data-stu-id="4e6ee-178">60</span></span> |<span data-ttu-id="4e6ee-179">675</span><span class="sxs-lookup"><span data-stu-id="4e6ee-179">675</span></span> |<span data-ttu-id="4e6ee-180">45.000.000</span><span class="sxs-lookup"><span data-stu-id="4e6ee-180">45,000,000</span></span> |<span data-ttu-id="4e6ee-181">2.700.000.000</span><span class="sxs-lookup"><span data-stu-id="4e6ee-181">2,700,000,000</span></span> |
| <span data-ttu-id="4e6ee-182">DW2000</span><span class="sxs-lookup"><span data-stu-id="4e6ee-182">DW2000</span></span> |<span data-ttu-id="4e6ee-183">15</span><span class="sxs-lookup"><span data-stu-id="4e6ee-183">15</span></span> |<span data-ttu-id="4e6ee-184">60</span><span class="sxs-lookup"><span data-stu-id="4e6ee-184">60</span></span> |<span data-ttu-id="4e6ee-185">900</span><span class="sxs-lookup"><span data-stu-id="4e6ee-185">900</span></span> |<span data-ttu-id="4e6ee-186">60.000.000</span><span class="sxs-lookup"><span data-stu-id="4e6ee-186">60,000,000</span></span> |<span data-ttu-id="4e6ee-187">3.600.000.000</span><span class="sxs-lookup"><span data-stu-id="4e6ee-187">3,600,000,000</span></span> |
| <span data-ttu-id="4e6ee-188">DW3000</span><span class="sxs-lookup"><span data-stu-id="4e6ee-188">DW3000</span></span> |<span data-ttu-id="4e6ee-189">22,5</span><span class="sxs-lookup"><span data-stu-id="4e6ee-189">22.5</span></span> |<span data-ttu-id="4e6ee-190">60</span><span class="sxs-lookup"><span data-stu-id="4e6ee-190">60</span></span> |<span data-ttu-id="4e6ee-191">1.350</span><span class="sxs-lookup"><span data-stu-id="4e6ee-191">1,350</span></span> |<span data-ttu-id="4e6ee-192">90.000.000</span><span class="sxs-lookup"><span data-stu-id="4e6ee-192">90,000,000</span></span> |<span data-ttu-id="4e6ee-193">5.400.000.000</span><span class="sxs-lookup"><span data-stu-id="4e6ee-193">5,400,000,000</span></span> |
| <span data-ttu-id="4e6ee-194">DW6000</span><span class="sxs-lookup"><span data-stu-id="4e6ee-194">DW6000</span></span> |<span data-ttu-id="4e6ee-195">45</span><span class="sxs-lookup"><span data-stu-id="4e6ee-195">45</span></span> |<span data-ttu-id="4e6ee-196">60</span><span class="sxs-lookup"><span data-stu-id="4e6ee-196">60</span></span> |<span data-ttu-id="4e6ee-197">2.700</span><span class="sxs-lookup"><span data-stu-id="4e6ee-197">2,700</span></span> |<span data-ttu-id="4e6ee-198">180.000.000</span><span class="sxs-lookup"><span data-stu-id="4e6ee-198">180,000,000</span></span> |<span data-ttu-id="4e6ee-199">10.800.000.000</span><span class="sxs-lookup"><span data-stu-id="4e6ee-199">10,800,000,000</span></span> |

<span data-ttu-id="4e6ee-200">Il limite delle dimensioni delle transazioni viene applicato per transazione o per operazione.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-200">The transaction size limit is applied per transaction or operation.</span></span> <span data-ttu-id="4e6ee-201">Non viene applicato in tutte le transazioni simultanee.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-201">It is not applied across all concurrent transactions.</span></span> <span data-ttu-id="4e6ee-202">A ogni transazione è quindi consentito scrivere questa quantità di dati nel log.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-202">Therefore each transaction is permitted to write this amount of data to the log.</span></span> 

<span data-ttu-id="4e6ee-203">Per ottimizzare e ridurre al minimo la quantità di dati scritti nel log, vedere [Ottimizzazione delle transazioni per SQL Data Warehouse][Transactions best practices].</span><span class="sxs-lookup"><span data-stu-id="4e6ee-203">To optimize and minimize the amount of data written to the log please refer to the [Transactions best practices][Transactions best practices] article.</span></span>

> [!WARNING]
> <span data-ttu-id="4e6ee-204">Le dimensioni massime delle transazioni possono essere ottenute solo per le tabelle distribuite HASH o ROUND_ROBIN in cui i dati sono distribuiti in modo uniforme.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-204">The maximum transaction size can only be achieved for HASH or ROUND_ROBIN distributed tables where the spread of the data is even.</span></span> <span data-ttu-id="4e6ee-205">Se la transazione scrive dati in modo asimmetrico nelle distribuzioni, è probabile che il limite venga raggiunto prima di raggiungere le dimensioni massime delle transazioni.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-205">If the transaction is writing data in a skewed fashion to the distributions then the limit is likely to be reached prior to the maximum transaction size.</span></span>
> <!--REPLICATED_TABLE-->
> 
> 

## <a name="transaction-state"></a><span data-ttu-id="4e6ee-206">Stato della transazione</span><span class="sxs-lookup"><span data-stu-id="4e6ee-206">Transaction state</span></span>
<span data-ttu-id="4e6ee-207">SQL Data Warehouse usa la funzione XACT_STATE() per segnalare una transazione non riuscita con il valore -2.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-207">SQL Data Warehouse uses the XACT_STATE() function to report a failed transaction using the value -2.</span></span> <span data-ttu-id="4e6ee-208">Ciò significa che la transazione non è riuscita ed è contrassegnata solo per il rollback.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-208">This means that the transaction has failed and is marked for rollback only</span></span>

> [!NOTE]
> <span data-ttu-id="4e6ee-209">L'uso di -2 da parte della funzione XACT_STATE per indicare una transazione non riuscita rappresenta un comportamento diverso da SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-209">The use of -2 by the XACT_STATE function to denote a failed transaction represents different behavior to SQL Server.</span></span> <span data-ttu-id="4e6ee-210">SQL Server usa il valore -1 per rappresentare una transazione di cui non è possibile eseguire il commit.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-210">SQL Server uses the value -1 to represent an un-committable transaction.</span></span> <span data-ttu-id="4e6ee-211">SQL Server è in grado di tollerare alcuni errori all'interno di una transazione senza doverne indicare l'impossibilità di eseguire il commit.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-211">SQL Server can tolerate some errors inside a transaction without it having to be marked as un-committable.</span></span> <span data-ttu-id="4e6ee-212">Ad esempio, `SELECT 1/0` causa un errore, ma non applica alla transazione lo stato per cui non è possibile eseguire il commit.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-212">For example `SELECT 1/0` would cause an error but not force a transaction into an un-committable state.</span></span> <span data-ttu-id="4e6ee-213">SQL Server consente anche letture nella transazione di cui non è possibile eseguire il commit.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-213">SQL Server also permits reads in the un-committable transaction.</span></span> <span data-ttu-id="4e6ee-214">SQL Data Warehouse, invece, non consente questa operazione.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-214">However, SQL Data Warehouse does not let you do this.</span></span> <span data-ttu-id="4e6ee-215">Se si verifica un errore in una transazione SQL Data Warehouse, verrà inserito automaticamente lo stato-2 e non sarà più possibile eseguire ulteriori istruzioni SELECT finché non verrà eseguito il rollback dell'istruzione.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-215">If an error occurs inside a SQL Data Warehouse transaction it will automatically enter the -2 state and you will not be able to make any further select statements until the statement has been rolled back.</span></span> <span data-ttu-id="4e6ee-216">È quindi importante verificare il codice dell'applicazione per vedere se usa XACT_STATE(), perché può essere necessario modificarlo.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-216">It is therefore important to check that your application code to see if it uses  XACT_STATE() as you may need to make code modifications.</span></span>
> 
> 

<span data-ttu-id="4e6ee-217">Ad esempio, in SQL Server potrebbe essere visualizzata una transazione simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="4e6ee-217">For example, in SQL Server you might see a transaction that looks like this:</span></span>

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

<span data-ttu-id="4e6ee-218">Se si lascia il codice come qui sopra, si otterrà il seguente messaggio di errore:</span><span class="sxs-lookup"><span data-stu-id="4e6ee-218">If you leave your code as it is above then you will get the following error message:</span></span>

<span data-ttu-id="4e6ee-219">Msg 111233, livello 16, stato 1, riga 1 111233;La transazione corrente è stata interrotta ed è stato eseguito il rollback di tutte le modifiche in sospeso.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-219">Msg 111233, Level 16, State 1, Line 1 111233;The current transaction has aborted, and any pending changes have been rolled back.</span></span> <span data-ttu-id="4e6ee-220">Causa: non è stato eseguito il rollback in modo esplicito di una transazione in uno stato di solo rollback prima di un'istruzione DDL, DML o SELECT.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-220">Cause: A transaction in a rollback-only state was not explicitly rolled back before a DDL, DML or SELECT statement.</span></span>

<span data-ttu-id="4e6ee-221">Inoltre non si otterrà l'output delle funzioni di ERROR_*.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-221">You will also not get the output of the ERROR_* functions.</span></span>

<span data-ttu-id="4e6ee-222">È quindi necessario modificare leggermente il codice in SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="4e6ee-222">In SQL Data Warehouse the code needs to be slightly altered:</span></span>

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

<span data-ttu-id="4e6ee-223">A questo punto si osserva il comportamento previsto.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-223">The expected behavior is now observed.</span></span> <span data-ttu-id="4e6ee-224">L'errore della transazione viene gestito e le funzioni ERROR_* forniscono i valori previsti.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-224">The error in the transaction is managed and the ERROR_* functions provide values as expected.</span></span>

<span data-ttu-id="4e6ee-225">Ciò dimostra che il `ROLLBACK` della transazione doveva essere eseguito prima della lettura delle informazioni sull'errore nel blocco `CATCH`.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-225">All that has changed is that the `ROLLBACK` of the transaction had to happen before the read of the error information in the `CATCH` block.</span></span>

## <a name="errorline-function"></a><span data-ttu-id="4e6ee-226">Funzione Error_Line()</span><span class="sxs-lookup"><span data-stu-id="4e6ee-226">Error_Line() function</span></span>
<span data-ttu-id="4e6ee-227">È importante sottolineare anche che SQL Data Warehouse non implementa né supporta la funzione ERROR_LINE().</span><span class="sxs-lookup"><span data-stu-id="4e6ee-227">It is also worth noting that SQL Data Warehouse does not implement or support the ERROR_LINE() function.</span></span> <span data-ttu-id="4e6ee-228">Se è contenuta nel codice sarà necessario rimuoverla per renderlo compatibile con SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-228">If you have this in your code you will need to remove it to be compliant with SQL Data Warehouse.</span></span> <span data-ttu-id="4e6ee-229">Anziché implementare una funzionalità equivalente, usare etichette di query nel codice.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-229">Use query labels in your code instead to implement equivalent functionality.</span></span> <span data-ttu-id="4e6ee-230">Per altre informazioni su questa funzionalità, vedere l'articolo [Usare etichette per instrumentare query in SQL Data Warehouse][LABEL].</span><span class="sxs-lookup"><span data-stu-id="4e6ee-230">Please refer to the [LABEL][LABEL] article for more details on this feature.</span></span>

## <a name="using-throw-and-raiserror"></a><span data-ttu-id="4e6ee-231">Uso di THROW e RAISERROR</span><span class="sxs-lookup"><span data-stu-id="4e6ee-231">Using THROW and RAISERROR</span></span>
<span data-ttu-id="4e6ee-232">THROW è l'implementazione più moderna per la generazione di eccezioni in SQL Data Warehouse, ma è supportata anche RAISERROR.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-232">THROW is the more modern implementation for raising exceptions in SQL Data Warehouse but RAISERROR is also supported.</span></span> <span data-ttu-id="4e6ee-233">Esistono tuttavia alcune differenze a cui vale la pena prestare attenzione.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-233">There are a few differences that are worth paying attention to however.</span></span>

* <span data-ttu-id="4e6ee-234">I numeri dei messaggi di errore definiti dall'utente non possono essere compresi nell'intervallo da 100.000 a 150.000 per THROW.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-234">User defined error messages numbers cannot be in the 100,000 - 150,000 range for THROW</span></span>
* <span data-ttu-id="4e6ee-235">I messaggi di errore di RAISERROR sono fissati a 50.000.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-235">RAISERROR error messages are fixed at 50,000</span></span>
* <span data-ttu-id="4e6ee-236">L'uso di sys.messages non è supportato.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-236">Use of sys.messages is not supported</span></span>

## <a name="limitiations"></a><span data-ttu-id="4e6ee-237">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="4e6ee-237">Limitiations</span></span>
<span data-ttu-id="4e6ee-238">SQL Data Warehouse presenta qualche altra limitazione relativa alle transazioni.</span><span class="sxs-lookup"><span data-stu-id="4e6ee-238">SQL Data Warehouse does have a few other restrictions that relate to transactions.</span></span>

<span data-ttu-id="4e6ee-239">Ecco quali sono:</span><span class="sxs-lookup"><span data-stu-id="4e6ee-239">They are as follows:</span></span>

* <span data-ttu-id="4e6ee-240">Nessuna transazione distribuita</span><span class="sxs-lookup"><span data-stu-id="4e6ee-240">No distributed transactions</span></span>
* <span data-ttu-id="4e6ee-241">Non sono consentite transazioni annidate</span><span class="sxs-lookup"><span data-stu-id="4e6ee-241">No nested transactions permitted</span></span>
* <span data-ttu-id="4e6ee-242">Non sono consentiti punti di salvataggio</span><span class="sxs-lookup"><span data-stu-id="4e6ee-242">No save points allowed</span></span>
* <span data-ttu-id="4e6ee-243">Nessuna transazione denominata</span><span class="sxs-lookup"><span data-stu-id="4e6ee-243">No named transactions</span></span>
* <span data-ttu-id="4e6ee-244">Nessuna transazione contrassegnata</span><span class="sxs-lookup"><span data-stu-id="4e6ee-244">No marked transactions</span></span>
* <span data-ttu-id="4e6ee-245">Nessun supporto per DDL come `CREATE TABLE` all'interno di una transazione definita dall'utente</span><span class="sxs-lookup"><span data-stu-id="4e6ee-245">No support for DDL such as `CREATE TABLE` inside a user defined transaction</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e6ee-246">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4e6ee-246">Next steps</span></span>
<span data-ttu-id="4e6ee-247">Per altre informazioni sull'ottimizzazione delle transazioni, vedere [Ottimizzazione delle transazioni per SQL Data Warehouse][Transactions best practices].</span><span class="sxs-lookup"><span data-stu-id="4e6ee-247">To learn more about optimizing transactions, see [Transactions best practices][Transactions best practices].</span></span>  <span data-ttu-id="4e6ee-248">Per altre informazioni sulle procedure consigliate per SQL Data Warehouse, vedere [Procedure consigliate per Azure SQL Data Warehouse][SQL Data Warehouse best practices].</span><span class="sxs-lookup"><span data-stu-id="4e6ee-248">To learn about other SQL Data Warehouse best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse best practices].</span></span>

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Transactions best practices]: ./sql-data-warehouse-develop-best-practices-transactions.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->

<!--Other Web references-->
