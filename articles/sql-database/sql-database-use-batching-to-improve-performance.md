---
title: toouse aaaHow tooimprove le prestazioni dell'applicazione di Database SQL di Azure batch
description: "Hello argomento fornisce una prova che l'invio in batch le operazioni del database notevolmente imroves hello velocità e la scalabilità delle applicazioni di Database SQL di Azure. Sebbene queste tecniche di invio in batch di lavoro per qualsiasi database di SQL Server, è incentrata hello articolo hello in Azure."
services: sql-database
documentationcenter: na
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 563862ca-c65a-46f6-975d-10df7ff6aa9c
ms.service: sql-database
ms.custom: develop apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/12/2016
ms.author: sstein
ms.openlocfilehash: 124b203ee69c595f0813852ff09ef9ec6841233a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-batching-tooimprove-sql-database-application-performance"></a><span data-ttu-id="2b8a9-104">Come l'invio in batch le prestazioni dell'applicazione di Database SQL tooimprove toouse</span><span class="sxs-lookup"><span data-stu-id="2b8a9-104">How toouse batching tooimprove SQL Database application performance</span></span>
<span data-ttu-id="2b8a9-105">Invio in batch di operazioni tooAzure Database SQL in modo significativo migliora hello prestazioni e scalabilità delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-105">Batching operations tooAzure SQL Database significantly improves hello performance and scalability of your applications.</span></span> <span data-ttu-id="2b8a9-106">Vantaggi di hello toounderstand ordine, prima parte di hello di questo articolo descrive alcuni risultati del test di esempio che consentono di confrontare le richieste in batch e sequenziale tooa Database SQL.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-106">In order toounderstand hello benefits, hello first part of this article covers some sample test results that compare sequential and batched requests tooa SQL Database.</span></span> <span data-ttu-id="2b8a9-107">Hello resto dell'articolo hello Mostra le tecniche di hello, scenari e considerazioni toohelp toouse batch correttamente nelle applicazioni Azure.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-107">hello remainder of hello article shows hello techniques, scenarios, and considerations toohelp you toouse batching successfully in your Azure applications.</span></span>

## <a name="why-is-batching-important-for-sql-database"></a><span data-ttu-id="2b8a9-108">Perché l'invio in batch è importante per il database SQL?</span><span class="sxs-lookup"><span data-stu-id="2b8a9-108">Why is batching important for SQL Database?</span></span>
<span data-ttu-id="2b8a9-109">Servizio remoto di chiamate tooa il batch è una ben nota strategia per migliorare le prestazioni e scalabilità.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-109">Batching calls tooa remote service is a well-known strategy for increasing performance and scalability.</span></span> <span data-ttu-id="2b8a9-110">Fissi di elaborazione delle interazioni tooany costi con un servizio remoto, ad esempio la serializzazione, trasferimento tramite rete e la deserializzazione.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-110">There are fixed processing costs tooany interactions with a remote service, such as serialization, network transfer, and deserialization.</span></span> <span data-ttu-id="2b8a9-111">Il raggruppamento di più transazioni distinte in un singolo batch consente di ridurre al minimo questi costi.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-111">Packaging many separate transactions into a single batch minimizes these costs.</span></span>

<span data-ttu-id="2b8a9-112">In questo documento, è necessario tooexamine diversi scenari e strategie di invio in batch di Database SQL.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-112">In this paper, we want tooexamine various SQL Database batching strategies and scenarios.</span></span> <span data-ttu-id="2b8a9-113">Sebbene tali strategie siano importanti anche per applicazioni locali che utilizzano SQL Server, esistono diversi motivi per evidenziare l'uso di hello del raggruppamento per il Database SQL:</span><span class="sxs-lookup"><span data-stu-id="2b8a9-113">Although these strategies are also important for on-premises applications that use SQL Server, there are several reasons for highlighting hello use of batching for SQL Database:</span></span>

* <span data-ttu-id="2b8a9-114">È potenzialmente maggiore latenza di rete durante l'accesso al Database SQL, in particolare se si accede a Database SQL da hello esterno stesso Data Center di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-114">There is potentially greater network latency in accessing SQL Database, especially if you are accessing SQL Database from outside hello same Microsoft Azure datacenter.</span></span>
* <span data-ttu-id="2b8a9-115">caratteristiche di multi-tenant Hello indica che il Database SQL che hello l'efficienza dei dati hello accedere livello correlata toohello scalabilità generale del database hello.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-115">hello multitenant characteristics of SQL Database means that hello efficiency of hello data access layer correlates toohello overall scalability of hello database.</span></span> <span data-ttu-id="2b8a9-116">Database SQL devono evitare qualsiasi singolo tenant/utente monopolizzi dannosa toohello risorse di database di altri tenant.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-116">SQL Database must prevent any single tenant/user from monopolizing database resources toohello detriment of other tenants.</span></span> <span data-ttu-id="2b8a9-117">Nella risposta toousage eccesso di quote predefinite, Database SQL può compromettono la velocità effettiva oppure rispondere con eccezioni di limitazione.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-117">In response toousage in excess of predefined quotas, SQL Database can reduce throughput or respond with throttling exceptions.</span></span> <span data-ttu-id="2b8a9-118">Maggiore efficienza, ad esempio l'invio in batch, Abilita si toodo più lavoro nel Database SQL prima di raggiungere questi limiti.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-118">Efficiencies, such as batching, enable you toodo more work on SQL Database before reaching these limits.</span></span> 
* <span data-ttu-id="2b8a9-119">L'invio in batch è efficace anche per le architetture che usano più database (partizionamento orizzontale).</span><span class="sxs-lookup"><span data-stu-id="2b8a9-119">Batching is also effective for architectures that use multiple databases (sharding).</span></span> <span data-ttu-id="2b8a9-120">Hello l'efficienza dell'interazione con ogni unità di database è ancora un fattore chiave per la scalabilità complessiva.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-120">hello efficiency of your interaction with each database unit is still a key factor in your overall scalability.</span></span> 

<span data-ttu-id="2b8a9-121">Uno dei vantaggi di hello dell'utilizzo del Database SQL è che non sono toomanage hello server database hello host.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-121">One of hello benefits of using SQL Database is that you don’t have toomanage hello servers that host hello database.</span></span> <span data-ttu-id="2b8a9-122">Tuttavia, questa infrastruttura gestita implica anche la presenza di toothink in modo diverso sull'ottimizzazione di database.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-122">However, this managed infrastructure also means that you have toothink differently about database optimizations.</span></span> <span data-ttu-id="2b8a9-123">Non è possibile esaminare tooimprove hello hardware o rete dell'infrastruttura di database.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-123">You can no longer look tooimprove hello database hardware or network infrastructure.</span></span> <span data-ttu-id="2b8a9-124">Gli ambienti sono controllati da Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-124">Microsoft Azure controls those environments.</span></span> <span data-ttu-id="2b8a9-125">Hello principale che è possibile controllare è rappresentata come l'applicazione interagisce con il Database SQL.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-125">hello main area that you can control is how your application interacts with SQL Database.</span></span> <span data-ttu-id="2b8a9-126">L'invio in batch è una di queste ottimizzazioni.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-126">Batching is one of these optimizations.</span></span> 

<span data-ttu-id="2b8a9-127">prima parte di Hello del documento hello esamina varie tecniche di invio in batch per le applicazioni .NET che utilizzano il Database SQL.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-127">hello first part of hello paper examines various batching techniques for .NET applications that use SQL Database.</span></span> <span data-ttu-id="2b8a9-128">Hello ultime due sezioni illustrano batch linee guida e scenari.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-128">hello last two sections cover batching guidelines and scenarios.</span></span>

## <a name="batching-strategies"></a><span data-ttu-id="2b8a9-129">Strategie di invio in batch</span><span class="sxs-lookup"><span data-stu-id="2b8a9-129">Batching strategies</span></span>
### <a name="note-about-timing-results-in-this-topic"></a><span data-ttu-id="2b8a9-130">Nota sui risultati della tempistica in questo argomento</span><span class="sxs-lookup"><span data-stu-id="2b8a9-130">Note about timing results in this topic</span></span>
> [!NOTE]
> <span data-ttu-id="2b8a9-131">Risultati non sono benchmark ma intendono tooshow **prestazioni relative**.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-131">Results are not benchmarks but are meant tooshow **relative performance**.</span></span> <span data-ttu-id="2b8a9-132">Le tempistiche si basano su una media di almeno 10 esecuzioni del test.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-132">Timings are based on an average of at least 10 test runs.</span></span> <span data-ttu-id="2b8a9-133">Le operazioni sono inserimenti in una tabella vuota.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-133">Operations are inserts into an empty table.</span></span> <span data-ttu-id="2b8a9-134">Questi test sono stati misurati pre-V12 e non corrispondono necessariamente toothroughput che potrebbero verificarsi in un database V12 usando hello [livelli di servizio](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="2b8a9-134">These tests were measured pre-V12, and they do not necessarily correspond toothroughput that you might experience in a V12 database using hello new [service tiers](sql-database-service-tiers.md).</span></span> <span data-ttu-id="2b8a9-135">vantaggio relativo di Hello di hello tecnica di invio in batch dovrebbe essere simile.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-135">hello relative benefit of hello batching technique should be similar.</span></span>
> 
> 

### <a name="transactions"></a><span data-ttu-id="2b8a9-136">Transazioni</span><span class="sxs-lookup"><span data-stu-id="2b8a9-136">Transactions</span></span>
<span data-ttu-id="2b8a9-137">Sembra strano toobegin una revisione dell'invio in batch parlando di transazioni.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-137">It seems strange toobegin a review of batching by discussing transactions.</span></span> <span data-ttu-id="2b8a9-138">Ma utilizzare hello delle transazioni lato client dispone di un leggero effetto di invio in batch sul lato server che consente di migliorare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-138">But hello use of client-side transactions has a subtle server-side batching effect that improves performance.</span></span> <span data-ttu-id="2b8a9-139">E le transazioni possono essere aggiunti con poche righe di codice, in modo che un modo rapido tooimprove di offrire prestazioni operazioni sequenziali.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-139">And transactions can be added with only a few lines of code, so they provide a fast way tooimprove performance of sequential operations.</span></span>

<span data-ttu-id="2b8a9-140">Si consideri hello dopo il codice c# che contiene una sequenza di inserimento e operazioni update in una tabella semplice.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-140">Consider hello following C# code that contains a sequence of insert and update operations on a simple table.</span></span>

    List<string> dbOperations = new List<string>();
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 1");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 2");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 3");
    dbOperations.Add("insert MyTable values ('new value',1)");
    dbOperations.Add("insert MyTable values ('new value',2)");
    dbOperations.Add("insert MyTable values ('new value',3)");

<span data-ttu-id="2b8a9-141">Queste operazioni vengono eseguite Hello seguente di codice ADO.NET in sequenza.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-141">hello following ADO.NET code sequentially performs these operations.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();

        foreach(string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn);
            cmd.ExecuteNonQuery();                   
        }
    }

<span data-ttu-id="2b8a9-142">Hello toooptimize modo migliore questo codice è tooimplement qualche forma di invio in batch sul lato client di queste chiamate.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-142">hello best way toooptimize this code is tooimplement some form of client-side batching of these calls.</span></span> <span data-ttu-id="2b8a9-143">Tuttavia, vi sia un modo semplice tooincrease hello delle prestazioni del codice semplicemente eseguendo il wrapping sequenza hello di chiamate in una transazione.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-143">But there is a simple way tooincrease hello performance of this code by simply wrapping hello sequence of calls in a transaction.</span></span> <span data-ttu-id="2b8a9-144">Ecco hello stesso codice che utilizza una transazione.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-144">Here is hello same code that uses a transaction.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();
        SqlTransaction transaction = conn.BeginTransaction();

        foreach (string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn, transaction);
            cmd.ExecuteNonQuery();
        }

        transaction.Commit();
    }

<span data-ttu-id="2b8a9-145">Le transazioni vengono in effetti usate in entrambi questi esempi.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-145">Transactions are actually being used in both of these examples.</span></span> <span data-ttu-id="2b8a9-146">Nel primo esempio hello, ogni singola chiamata è una transazione implicita.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-146">In hello first example, each individual call is an implicit transaction.</span></span> <span data-ttu-id="2b8a9-147">Nel secondo esempio hello, una transazione esplicita esegue il wrapping di tutte le chiamate di hello.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-147">In hello second example, an explicit transaction wraps all of hello calls.</span></span> <span data-ttu-id="2b8a9-148">Per la documentazione di hello per hello [log delle transazioni write-ahead](https://msdn.microsoft.com/library/ms186259.aspx), i record del log sono disco toohello scaricato quando si esegue il commit delle transazioni hello.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-148">Per hello documentation for hello [write-ahead transaction log](https://msdn.microsoft.com/library/ms186259.aspx), log records are flushed toohello disk when hello transaction commits.</span></span> <span data-ttu-id="2b8a9-149">Pertanto, includendo più chiamate in una transazione, hello log delle transazioni di scrittura toohello possibile ritardare fino a quando non viene eseguito il commit delle transazioni hello.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-149">So by including more calls in a transaction, hello write toohello transaction log can delay until hello transaction is committed.</span></span> <span data-ttu-id="2b8a9-150">In effetti, si abilita l'invio in batch per il log delle transazioni del server di hello scritture toohello.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-150">In effect, you are enabling batching for hello writes toohello server’s transaction log.</span></span>

<span data-ttu-id="2b8a9-151">Hello nella tabella seguente mostra alcuni risultati di test ad hoc.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-151">hello following table shows some ad-hoc testing results.</span></span> <span data-ttu-id="2b8a9-152">eseguire i test di Hello hello che stesso sequenziale inserisce con e senza transazioni.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-152">hello tests performed hello same sequential inserts with and without transactions.</span></span> <span data-ttu-id="2b8a9-153">Per maggiore chiarezza, hello primo set di test è stato eseguito in modalità remota da un database toohello portatile in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-153">For more perspective, hello first set of tests ran remotely from a laptop toohello database in Microsoft Azure.</span></span> <span data-ttu-id="2b8a9-154">Hello secondo set di test è stato eseguito da un servizio cloud e un database entrambi residenti nello hello stesso Data Center di Microsoft Azure (Stati Uniti occidentali).</span><span class="sxs-lookup"><span data-stu-id="2b8a9-154">hello second set of tests ran from a cloud service and database that both resided within hello same Microsoft Azure datacenter (West US).</span></span> <span data-ttu-id="2b8a9-155">Hello nella tabella seguente mostra la durata di hello in millisecondi di operazioni sequenziali di inserimento con e senza transazioni.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-155">hello following table shows hello duration in milliseconds of sequential inserts with and without transactions.</span></span>

<span data-ttu-id="2b8a9-156">**On-premise tooAzure**:</span><span class="sxs-lookup"><span data-stu-id="2b8a9-156">**On-Premises tooAzure**:</span></span>

| <span data-ttu-id="2b8a9-157">Operazioni</span><span class="sxs-lookup"><span data-stu-id="2b8a9-157">Operations</span></span> | <span data-ttu-id="2b8a9-158">Senza transazione (ms)</span><span class="sxs-lookup"><span data-stu-id="2b8a9-158">No Transaction (ms)</span></span> | <span data-ttu-id="2b8a9-159">Con transazione (ms)</span><span class="sxs-lookup"><span data-stu-id="2b8a9-159">Transaction (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2b8a9-160">1</span><span class="sxs-lookup"><span data-stu-id="2b8a9-160">1</span></span> |<span data-ttu-id="2b8a9-161">130</span><span class="sxs-lookup"><span data-stu-id="2b8a9-161">130</span></span> |<span data-ttu-id="2b8a9-162">402</span><span class="sxs-lookup"><span data-stu-id="2b8a9-162">402</span></span> |
| <span data-ttu-id="2b8a9-163">10</span><span class="sxs-lookup"><span data-stu-id="2b8a9-163">10</span></span> |<span data-ttu-id="2b8a9-164">1208</span><span class="sxs-lookup"><span data-stu-id="2b8a9-164">1208</span></span> |<span data-ttu-id="2b8a9-165">1226</span><span class="sxs-lookup"><span data-stu-id="2b8a9-165">1226</span></span> |
| <span data-ttu-id="2b8a9-166">100</span><span class="sxs-lookup"><span data-stu-id="2b8a9-166">100</span></span> |<span data-ttu-id="2b8a9-167">12662</span><span class="sxs-lookup"><span data-stu-id="2b8a9-167">12662</span></span> |<span data-ttu-id="2b8a9-168">10395</span><span class="sxs-lookup"><span data-stu-id="2b8a9-168">10395</span></span> |
| <span data-ttu-id="2b8a9-169">1000</span><span class="sxs-lookup"><span data-stu-id="2b8a9-169">1000</span></span> |<span data-ttu-id="2b8a9-170">128852</span><span class="sxs-lookup"><span data-stu-id="2b8a9-170">128852</span></span> |<span data-ttu-id="2b8a9-171">102917</span><span class="sxs-lookup"><span data-stu-id="2b8a9-171">102917</span></span> |

<span data-ttu-id="2b8a9-172">**Azure tooAzure (medesimo datacenter)**:</span><span class="sxs-lookup"><span data-stu-id="2b8a9-172">**Azure tooAzure (same datacenter)**:</span></span>

| <span data-ttu-id="2b8a9-173">Operazioni</span><span class="sxs-lookup"><span data-stu-id="2b8a9-173">Operations</span></span> | <span data-ttu-id="2b8a9-174">Senza transazione (ms)</span><span class="sxs-lookup"><span data-stu-id="2b8a9-174">No Transaction (ms)</span></span> | <span data-ttu-id="2b8a9-175">Con transazione (ms)</span><span class="sxs-lookup"><span data-stu-id="2b8a9-175">Transaction (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2b8a9-176">1</span><span class="sxs-lookup"><span data-stu-id="2b8a9-176">1</span></span> |<span data-ttu-id="2b8a9-177">21</span><span class="sxs-lookup"><span data-stu-id="2b8a9-177">21</span></span> |<span data-ttu-id="2b8a9-178">26</span><span class="sxs-lookup"><span data-stu-id="2b8a9-178">26</span></span> |
| <span data-ttu-id="2b8a9-179">10</span><span class="sxs-lookup"><span data-stu-id="2b8a9-179">10</span></span> |<span data-ttu-id="2b8a9-180">220</span><span class="sxs-lookup"><span data-stu-id="2b8a9-180">220</span></span> |<span data-ttu-id="2b8a9-181">56</span><span class="sxs-lookup"><span data-stu-id="2b8a9-181">56</span></span> |
| <span data-ttu-id="2b8a9-182">100</span><span class="sxs-lookup"><span data-stu-id="2b8a9-182">100</span></span> |<span data-ttu-id="2b8a9-183">2145</span><span class="sxs-lookup"><span data-stu-id="2b8a9-183">2145</span></span> |<span data-ttu-id="2b8a9-184">341</span><span class="sxs-lookup"><span data-stu-id="2b8a9-184">341</span></span> |
| <span data-ttu-id="2b8a9-185">1000</span><span class="sxs-lookup"><span data-stu-id="2b8a9-185">1000</span></span> |<span data-ttu-id="2b8a9-186">21479</span><span class="sxs-lookup"><span data-stu-id="2b8a9-186">21479</span></span> |<span data-ttu-id="2b8a9-187">2756</span><span class="sxs-lookup"><span data-stu-id="2b8a9-187">2756</span></span> |

> [!NOTE]
> <span data-ttu-id="2b8a9-188">I risultati non sono benchmark.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-188">Results are not benchmarks.</span></span> <span data-ttu-id="2b8a9-189">Vedere hello [nota sui risultati di temporizzazione in questo argomento](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="2b8a9-189">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="2b8a9-190">In base ai risultati dei test precedenti hello, il wrapping di una singola operazione in una transazione effettivamente riduce le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-190">Based on hello previous test results, wrapping a single operation in a transaction actually decreases performance.</span></span> <span data-ttu-id="2b8a9-191">Ma quando si aumenta il numero di hello di operazioni in una singola transazione, miglioramento delle prestazioni hello diventa più evidente.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-191">But as you increase hello number of operations within a single transaction, hello performance improvement becomes more marked.</span></span> <span data-ttu-id="2b8a9-192">è inoltre più significativa differenza nelle prestazioni Hello quando tutte le operazioni si verificano nel Data Center di Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-192">hello performance difference is also more noticeable when all operations occur within hello Microsoft Azure datacenter.</span></span> <span data-ttu-id="2b8a9-193">Hello un aumento della latenza di utilizzo dal Data Center di Microsoft Azure hello all'esterno del Database SQL leggibile miglioramento delle prestazioni hello utilizzo delle transazioni.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-193">hello increased latency of using SQL Database from outside hello Microsoft Azure datacenter overshadows hello performance gain of using transactions.</span></span>

<span data-ttu-id="2b8a9-194">Sebbene l'utilizzo di hello delle transazioni può migliorare le prestazioni, continuare troppo[osservare le procedure consigliate per le connessioni e transazioni](https://msdn.microsoft.com/library/ms187484.aspx).</span><span class="sxs-lookup"><span data-stu-id="2b8a9-194">Although hello use of transactions can increase performance, continue too[observe best practices for transactions and connections](https://msdn.microsoft.com/library/ms187484.aspx).</span></span> <span data-ttu-id="2b8a9-195">Mantenere transazioni hello più brevi connessione al database hello possibili e di chiusura dopo hello lavoro viene completato.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-195">Keep hello transaction as short as possible, and close hello database connection after hello work completes.</span></span> <span data-ttu-id="2b8a9-196">istruzione using nell'esempio precedente hello Hello assicura la chiusura connessione hello termine del blocco di codice successivo hello.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-196">hello using statement in hello previous example assures that hello connection is closed when hello subsequent code block completes.</span></span>

<span data-ttu-id="2b8a9-197">Hello precedente esempio viene illustrato che è possibile aggiungere un codice ADO.NET tooany transazione locale con due righe.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-197">hello previous example demonstrates that you can add a local transaction tooany ADO.NET code with two lines.</span></span> <span data-ttu-id="2b8a9-198">Le transazioni rappresentano un modo rapido le prestazioni di hello tooimprove di codice che effettua sequenza di inserimento e aggiornamento e le operazioni di eliminazione.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-198">Transactions offer a quick way tooimprove hello performance of code that makes sequential insert, update, and delete operations.</span></span> <span data-ttu-id="2b8a9-199">Tuttavia, per prestazioni più veloci hello, provare a modificare hello codice tootake vantaggio dell'invio in batch sul lato client, quali i parametri con valori di tabella.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-199">However, for hello fastest performance, consider changing hello code further tootake advantage of client-side batching, such as table-valued parameters.</span></span>

<span data-ttu-id="2b8a9-200">Per altre informazioni sulle transazioni in ADO.NET, vedere [Transazioni locali in ADO.NET](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).</span><span class="sxs-lookup"><span data-stu-id="2b8a9-200">For more information about transactions in ADO.NET, see [Local Transactions in ADO.NET](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).</span></span>

### <a name="table-valued-parameters"></a><span data-ttu-id="2b8a9-201">Parametri con valori di tabella</span><span class="sxs-lookup"><span data-stu-id="2b8a9-201">Table-valued parameters</span></span>
<span data-ttu-id="2b8a9-202">I parametri con valori di tabella supportano tipi di tabella definiti dall'utente come parametri nelle funzioni, nelle stored procedure e nelle istruzioni Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-202">Table-valued parameters support user-defined table types as parameters in Transact-SQL statements, stored procedures, and functions.</span></span> <span data-ttu-id="2b8a9-203">Questa tecnica di invio in batch sul lato client consente toosend più righe di dati all'interno di parametro con valori di tabella hello.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-203">This client-side batching technique allows you toosend multiple rows of data within hello table-valued parameter.</span></span> <span data-ttu-id="2b8a9-204">toouse parametri con valori di tabella, innanzitutto definire un tipo di tabella.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-204">toouse table-valued parameters, first define a table type.</span></span> <span data-ttu-id="2b8a9-205">Hello istruzione Transact-SQL seguente crea un tipo di tabella denominato **MyTableType**.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-205">hello following Transact-SQL statement creates a table type named **MyTableType**.</span></span>

    CREATE TYPE MyTableType AS TABLE 
    ( mytext TEXT,
      num INT );


<span data-ttu-id="2b8a9-206">Nel codice, si crea un **DataTable** con hello esatta stessi nomi e tipi hello del tipo di tabella.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-206">In code, you create a **DataTable** with hello exact same names and types of hello table type.</span></span> <span data-ttu-id="2b8a9-207">Passare l'oggetto **DataTable** in un parametro in una chiamata di stored procedure o query di testo.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-207">Pass this **DataTable** in a parameter in a text query or stored procedure call.</span></span> <span data-ttu-id="2b8a9-208">Hello seguente illustra questa tecnica:</span><span class="sxs-lookup"><span data-stu-id="2b8a9-208">hello following example shows this technique:</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        DataTable table = new DataTable();
        // Add columns and rows. hello following is a simple example.
        table.Columns.Add("mytext", typeof(string));
        table.Columns.Add("num", typeof(int));    
        for (var i = 0; i < 10; i++)
        {
            table.Rows.Add(DateTime.Now.ToString(), DateTime.Now.Millisecond);
        }

        SqlCommand cmd = new SqlCommand(
            "INSERT INTO MyTable(mytext, num) SELECT mytext, num FROM @TestTvp",
            connection);

        cmd.Parameters.Add(
            new SqlParameter()
            {
                ParameterName = "@TestTvp",
                SqlDbType = SqlDbType.Structured,
                TypeName = "MyTableType",
                Value = table,
            });

        cmd.ExecuteNonQuery();
    }

<span data-ttu-id="2b8a9-209">Nell'esempio precedente hello hello **SqlCommand** oggetto inserisce righe da un parametro con valori di tabella,  **@TestTvp** .</span><span class="sxs-lookup"><span data-stu-id="2b8a9-209">In hello previous example, hello **SqlCommand** object inserts rows from a table-valued parameter, **@TestTvp**.</span></span> <span data-ttu-id="2b8a9-210">Hello creato in precedenza **DataTable** oggetto viene assegnato il parametro toothis con hello **SqlCommand.Parameters.Add** metodo.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-210">hello previously created **DataTable** object is assigned toothis parameter with hello **SqlCommand.Parameters.Add** method.</span></span> <span data-ttu-id="2b8a9-211">Batch hello inserimenti in una chiamano in modo significativo aumenta le prestazioni di hello su operazioni sequenziali di inserimento.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-211">Batching hello inserts in one call significantly increases hello performance over sequential inserts.</span></span>

<span data-ttu-id="2b8a9-212">tooimprove hello precedente esempio, inoltre, utilizzare una stored procedure anziché un comando basata su testo.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-212">tooimprove hello previous example further, use a stored procedure instead of a text-based command.</span></span> <span data-ttu-id="2b8a9-213">Hello comando Transact-SQL seguente crea una stored procedure che accetta hello **SimpleTestTableType** parametro con valori di tabella.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-213">hello following Transact-SQL command creates a stored procedure that takes hello **SimpleTestTableType** table-valued parameter.</span></span>

    CREATE PROCEDURE [dbo].[sp_InsertRows] 
    @TestTvp as MyTableType READONLY
    AS
    BEGIN
    INSERT INTO MyTable(mytext, num) 
    SELECT mytext, num FROM @TestTvp
    END
    GO

<span data-ttu-id="2b8a9-214">Modificare quindi hello **SqlCommand** dichiarazione seguente toohello esempio hello precedente codice dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-214">Then change hello **SqlCommand** object declaration in hello previous code example toohello following.</span></span>

    SqlCommand cmd = new SqlCommand("sp_InsertRows", connection);
    cmd.CommandType = CommandType.StoredProcedure;

<span data-ttu-id="2b8a9-215">Nella maggior parte dei casi i parametri con valori di tabella hanno prestazioni equivalenti o superiori rispetto ad altre tecniche di invio in batch.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-215">In most cases, table-valued parameters have equivalent or better performance than other batching techniques.</span></span> <span data-ttu-id="2b8a9-216">I parametri con valori di tabella sono spesso preferibili perché più flessibili di altre opzioni.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-216">Table-valued parameters are often preferable, because they are more flexible than other options.</span></span> <span data-ttu-id="2b8a9-217">Ad esempio, altre tecniche come la copia bulk di SQL, consentono solo inserimento hello di nuove righe.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-217">For example, other techniques, such as SQL bulk copy, only permit hello insertion of new rows.</span></span> <span data-ttu-id="2b8a9-218">Ma con i parametri con valori di tabella, è possibile utilizzare la logica in hello stored procedure toodetermine le righe da aggiornare e quelle da inserire.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-218">But with table-valued parameters, you can use logic in hello stored procedure toodetermine which rows are updates and which are inserts.</span></span> <span data-ttu-id="2b8a9-219">tipo di tabella Hello può essere modificato toocontain una colonna "Operation" che indica se hello specificata riga deve essere inserita, aggiornata o eliminata.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-219">hello table type can also be modified toocontain an “Operation” column that indicates whether hello specified row should be inserted, updated, or deleted.</span></span>

<span data-ttu-id="2b8a9-220">Hello nella tabella seguente mostra i risultati dei test ad hoc per l'utilizzo di hello di parametri con valori di tabella in millisecondi.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-220">hello following table shows ad-hoc test results for hello use of table-valued parameters in milliseconds.</span></span>

| <span data-ttu-id="2b8a9-221">Operazioni</span><span class="sxs-lookup"><span data-stu-id="2b8a9-221">Operations</span></span> | <span data-ttu-id="2b8a9-222">On-premise tooAzure (ms)</span><span class="sxs-lookup"><span data-stu-id="2b8a9-222">On-Premises tooAzure (ms)</span></span> | <span data-ttu-id="2b8a9-223">Azure stesso data center (ms)</span><span class="sxs-lookup"><span data-stu-id="2b8a9-223">Azure same datacenter (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2b8a9-224">1</span><span class="sxs-lookup"><span data-stu-id="2b8a9-224">1</span></span> |<span data-ttu-id="2b8a9-225">124</span><span class="sxs-lookup"><span data-stu-id="2b8a9-225">124</span></span> |<span data-ttu-id="2b8a9-226">32</span><span class="sxs-lookup"><span data-stu-id="2b8a9-226">32</span></span> |
| <span data-ttu-id="2b8a9-227">10</span><span class="sxs-lookup"><span data-stu-id="2b8a9-227">10</span></span> |<span data-ttu-id="2b8a9-228">131</span><span class="sxs-lookup"><span data-stu-id="2b8a9-228">131</span></span> |<span data-ttu-id="2b8a9-229">25</span><span class="sxs-lookup"><span data-stu-id="2b8a9-229">25</span></span> |
| <span data-ttu-id="2b8a9-230">100</span><span class="sxs-lookup"><span data-stu-id="2b8a9-230">100</span></span> |<span data-ttu-id="2b8a9-231">338</span><span class="sxs-lookup"><span data-stu-id="2b8a9-231">338</span></span> |<span data-ttu-id="2b8a9-232">51</span><span class="sxs-lookup"><span data-stu-id="2b8a9-232">51</span></span> |
| <span data-ttu-id="2b8a9-233">1000</span><span class="sxs-lookup"><span data-stu-id="2b8a9-233">1000</span></span> |<span data-ttu-id="2b8a9-234">2615</span><span class="sxs-lookup"><span data-stu-id="2b8a9-234">2615</span></span> |<span data-ttu-id="2b8a9-235">382</span><span class="sxs-lookup"><span data-stu-id="2b8a9-235">382</span></span> |
| <span data-ttu-id="2b8a9-236">10000</span><span class="sxs-lookup"><span data-stu-id="2b8a9-236">10000</span></span> |<span data-ttu-id="2b8a9-237">23830</span><span class="sxs-lookup"><span data-stu-id="2b8a9-237">23830</span></span> |<span data-ttu-id="2b8a9-238">3586</span><span class="sxs-lookup"><span data-stu-id="2b8a9-238">3586</span></span> |

> [!NOTE]
> <span data-ttu-id="2b8a9-239">I risultati non sono benchmark.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-239">Results are not benchmarks.</span></span> <span data-ttu-id="2b8a9-240">Vedere hello [nota sui risultati di temporizzazione in questo argomento](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="2b8a9-240">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="2b8a9-241">miglioramento delle prestazioni Hello dall'invio in batch è immediatamente evidente.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-241">hello performance gain from batching is immediately apparent.</span></span> <span data-ttu-id="2b8a9-242">Nel test sequenziale precedente hello, 1000 operazioni hanno richiesto 129 secondi hello esterno datacenter e 21 secondi all'interno di hello datacenter.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-242">In hello previous sequential test, 1000 operations took 129 seconds outside hello datacenter and 21 seconds from within hello datacenter.</span></span> <span data-ttu-id="2b8a9-243">Ma con i parametri con valori di tabella, 1000 operazioni richiedono invece solo 2,6 secondi all'esterno di hello datacenter e 0,4 secondi all'interno di hello datacenter.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-243">But with table-valued parameters, 1000 operations take only 2.6 seconds outside hello datacenter and 0.4 seconds within hello datacenter.</span></span>

<span data-ttu-id="2b8a9-244">Per altre informazioni sui parametri con valori di tabella, vedere [Usare parametri con valori di tabella (motore di database)](https://msdn.microsoft.com/library/bb510489.aspx).</span><span class="sxs-lookup"><span data-stu-id="2b8a9-244">For more information on table-valued parameters, see [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span></span>

### <a name="sql-bulk-copy"></a><span data-ttu-id="2b8a9-245">Copia bulk di SQL</span><span class="sxs-lookup"><span data-stu-id="2b8a9-245">SQL bulk copy</span></span>
<span data-ttu-id="2b8a9-246">Copia bulk di SQL è un altro modo tooinsert grandi quantità di dati in un database di destinazione.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-246">SQL bulk copy is another way tooinsert large amounts of data into a target database.</span></span> <span data-ttu-id="2b8a9-247">Applicazioni .NET possono usare hello **SqlBulkCopy** operazioni di inserimento bulk tooperform di classe.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-247">.NET applications can use hello **SqlBulkCopy** class tooperform bulk insert operations.</span></span> <span data-ttu-id="2b8a9-248">**SqlBulkCopy** è simile nello strumento da riga di comando di funzione toohello, **Bcp.exe**, o istruzione Transact-SQL, hello **BULK INSERT**.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-248">**SqlBulkCopy** is similar in function toohello command-line tool, **Bcp.exe**, or hello Transact-SQL statement, **BULK INSERT**.</span></span> <span data-ttu-id="2b8a9-249">Hello esempio di codice seguente viene illustrato come hello copia toobulk righe nell'origine hello **DataTable**, table, tabella di destinazione toohello in SQL Server, MyTable.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-249">hello following code example shows how toobulk copy hello rows in hello source **DataTable**, table, toohello destination table in SQL Server, MyTable.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        using (SqlBulkCopy bulkCopy = new SqlBulkCopy(connection))
        {
            bulkCopy.DestinationTableName = "MyTable";
            bulkCopy.ColumnMappings.Add("mytext", "mytext");
            bulkCopy.ColumnMappings.Add("num", "num");
            bulkCopy.WriteToServer(table);
        }
    }

<span data-ttu-id="2b8a9-250">In alcuni casi la copia bulk è preferibile rispetto ai parametri con valori di tabella.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-250">There are some cases where bulk copy is preferred over table-valued parameters.</span></span> <span data-ttu-id="2b8a9-251">Vedere la tabella di confronto hello dei parametri con valori di tabella rispetto alle operazioni BULK INSERT in argomento hello [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span><span class="sxs-lookup"><span data-stu-id="2b8a9-251">See hello comparison table of Table-Valued parameters versus BULK INSERT operations in hello topic [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span></span>

<span data-ttu-id="2b8a9-252">risultati dei test ad hoc seguenti Hello mostrano prestazioni hello dell'invio in batch con **SqlBulkCopy** in millisecondi.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-252">hello following ad-hoc test results show hello performance of batching with **SqlBulkCopy** in milliseconds.</span></span>

| <span data-ttu-id="2b8a9-253">Operazioni</span><span class="sxs-lookup"><span data-stu-id="2b8a9-253">Operations</span></span> | <span data-ttu-id="2b8a9-254">On-premise tooAzure (ms)</span><span class="sxs-lookup"><span data-stu-id="2b8a9-254">On-Premises tooAzure (ms)</span></span> | <span data-ttu-id="2b8a9-255">Azure stesso data center (ms)</span><span class="sxs-lookup"><span data-stu-id="2b8a9-255">Azure same datacenter (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2b8a9-256">1</span><span class="sxs-lookup"><span data-stu-id="2b8a9-256">1</span></span> |<span data-ttu-id="2b8a9-257">433</span><span class="sxs-lookup"><span data-stu-id="2b8a9-257">433</span></span> |<span data-ttu-id="2b8a9-258">57</span><span class="sxs-lookup"><span data-stu-id="2b8a9-258">57</span></span> |
| <span data-ttu-id="2b8a9-259">10</span><span class="sxs-lookup"><span data-stu-id="2b8a9-259">10</span></span> |<span data-ttu-id="2b8a9-260">441</span><span class="sxs-lookup"><span data-stu-id="2b8a9-260">441</span></span> |<span data-ttu-id="2b8a9-261">32</span><span class="sxs-lookup"><span data-stu-id="2b8a9-261">32</span></span> |
| <span data-ttu-id="2b8a9-262">100</span><span class="sxs-lookup"><span data-stu-id="2b8a9-262">100</span></span> |<span data-ttu-id="2b8a9-263">636</span><span class="sxs-lookup"><span data-stu-id="2b8a9-263">636</span></span> |<span data-ttu-id="2b8a9-264">53</span><span class="sxs-lookup"><span data-stu-id="2b8a9-264">53</span></span> |
| <span data-ttu-id="2b8a9-265">1000</span><span class="sxs-lookup"><span data-stu-id="2b8a9-265">1000</span></span> |<span data-ttu-id="2b8a9-266">2535</span><span class="sxs-lookup"><span data-stu-id="2b8a9-266">2535</span></span> |<span data-ttu-id="2b8a9-267">341</span><span class="sxs-lookup"><span data-stu-id="2b8a9-267">341</span></span> |
| <span data-ttu-id="2b8a9-268">10000</span><span class="sxs-lookup"><span data-stu-id="2b8a9-268">10000</span></span> |<span data-ttu-id="2b8a9-269">21605</span><span class="sxs-lookup"><span data-stu-id="2b8a9-269">21605</span></span> |<span data-ttu-id="2b8a9-270">2737</span><span class="sxs-lookup"><span data-stu-id="2b8a9-270">2737</span></span> |

> [!NOTE]
> <span data-ttu-id="2b8a9-271">I risultati non sono benchmark.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-271">Results are not benchmarks.</span></span> <span data-ttu-id="2b8a9-272">Vedere hello [nota sui risultati di temporizzazione in questo argomento](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="2b8a9-272">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="2b8a9-273">Nel batch di dimensioni minori, i parametri con valori di tabella di utilizzo hello buoni hello **SqlBulkCopy** classe.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-273">In smaller batch sizes, hello use table-valued parameters outperformed hello **SqlBulkCopy** class.</span></span> <span data-ttu-id="2b8a9-274">Tuttavia, **SqlBulkCopy** eseguita 12-31% più rapida rispetto ai parametri con valori di tabella per i test hello di 1.000 e 10.000 righe.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-274">However, **SqlBulkCopy** performed 12-31% faster than table-valued parameters for hello tests of 1,000 and 10,000 rows.</span></span> <span data-ttu-id="2b8a9-275">Come i parametri con valori di tabella, **SqlBulkCopy** è un'opzione valida per inserimenti batch, in particolare quando confrontati toohello le prestazioni delle operazioni non in batch.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-275">Like table-valued parameters, **SqlBulkCopy** is a good option for batched inserts, especially when compared toohello performance of non-batched operations.</span></span>

<span data-ttu-id="2b8a9-276">Per altre informazioni sulla copia bulk in ADO.NET, vedere [Operazioni di copia bulk in SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).</span><span class="sxs-lookup"><span data-stu-id="2b8a9-276">For more information on bulk copy in ADO.NET, see [Bulk Copy Operations in SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).</span></span>

### <a name="multiple-row-parameterized-insert-statements"></a><span data-ttu-id="2b8a9-277">Istruzioni INSERT con parametri a più righe</span><span class="sxs-lookup"><span data-stu-id="2b8a9-277">Multiple-row Parameterized INSERT statements</span></span>
<span data-ttu-id="2b8a9-278">Un'alternativa per i batch di piccole dimensioni è un grande tooconstruct istruzione INSERT per inserire più righe con parametri.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-278">One alternative for small batches is tooconstruct a large parameterized INSERT statement that inserts multiple rows.</span></span> <span data-ttu-id="2b8a9-279">Hello esempio di codice seguente viene illustrata questa tecnica.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-279">hello following code example demonstrates this technique.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        string insertCommand = "INSERT INTO [MyTable] ( mytext, num ) " +
            "VALUES (@p1, @p2), (@p3, @p4), (@p5, @p6), (@p7, @p8), (@p9, @p10)";

        SqlCommand cmd = new SqlCommand(insertCommand, connection);

        for (int i = 1; i <= 10; i += 2)
        {
            cmd.Parameters.Add(new SqlParameter("@p" + i.ToString(), "test"));
            cmd.Parameters.Add(new SqlParameter("@p" + (i+1).ToString(), i));
        }

        cmd.ExecuteNonQuery();
    }


<span data-ttu-id="2b8a9-280">Questo esempio è ideato tooshow concetti di base hello.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-280">This example is meant tooshow hello basic concept.</span></span> <span data-ttu-id="2b8a9-281">Uno scenario più realistico sarebbe ciclo stringa di query hello tooconstruct entità hello necessarie e i parametri del comando hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-281">A more realistic scenario would loop through hello required entities tooconstruct hello query string and hello command parameters simultaneously.</span></span> <span data-ttu-id="2b8a9-282">Si è limitati totale tooa 2100 parametri di query, il che limita il numero totale di hello di righe che possono essere elaborati in questo modo.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-282">You are limited tooa total of 2100 query parameters, so this limits hello total number of rows that can be processed in this manner.</span></span>

<span data-ttu-id="2b8a9-283">Hello seguente ad hoc testare risultati Mostra hello le prestazioni di questo tipo di istruzione insert in millisecondi.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-283">hello following ad-hoc test results show hello performance of this type of insert statement in milliseconds.</span></span>

| <span data-ttu-id="2b8a9-284">Operazioni</span><span class="sxs-lookup"><span data-stu-id="2b8a9-284">Operations</span></span> | <span data-ttu-id="2b8a9-285">Parametri con valori di tabella (ms)</span><span class="sxs-lookup"><span data-stu-id="2b8a9-285">Table-valued parameters (ms)</span></span> | <span data-ttu-id="2b8a9-286">Singola istruzione INSERT (ms)</span><span class="sxs-lookup"><span data-stu-id="2b8a9-286">Single-statement INSERT (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2b8a9-287">1</span><span class="sxs-lookup"><span data-stu-id="2b8a9-287">1</span></span> |<span data-ttu-id="2b8a9-288">32</span><span class="sxs-lookup"><span data-stu-id="2b8a9-288">32</span></span> |<span data-ttu-id="2b8a9-289">20</span><span class="sxs-lookup"><span data-stu-id="2b8a9-289">20</span></span> |
| <span data-ttu-id="2b8a9-290">10</span><span class="sxs-lookup"><span data-stu-id="2b8a9-290">10</span></span> |<span data-ttu-id="2b8a9-291">30</span><span class="sxs-lookup"><span data-stu-id="2b8a9-291">30</span></span> |<span data-ttu-id="2b8a9-292">25</span><span class="sxs-lookup"><span data-stu-id="2b8a9-292">25</span></span> |
| <span data-ttu-id="2b8a9-293">100</span><span class="sxs-lookup"><span data-stu-id="2b8a9-293">100</span></span> |<span data-ttu-id="2b8a9-294">33</span><span class="sxs-lookup"><span data-stu-id="2b8a9-294">33</span></span> |<span data-ttu-id="2b8a9-295">51</span><span class="sxs-lookup"><span data-stu-id="2b8a9-295">51</span></span> |

> [!NOTE]
> <span data-ttu-id="2b8a9-296">I risultati non sono benchmark.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-296">Results are not benchmarks.</span></span> <span data-ttu-id="2b8a9-297">Vedere hello [nota sui risultati di temporizzazione in questo argomento](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="2b8a9-297">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="2b8a9-298">Questo approccio può essere leggermente più veloce per i batch minori di 100 righe.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-298">This approach can be slightly faster for batches that are less than 100 rows.</span></span> <span data-ttu-id="2b8a9-299">Benché miglioramento hello è piccolo, questa tecnica è un'altra opzione che potrebbe rivelarsi utile in specifici scenari applicativi.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-299">Although hello improvement is small, this technique is another option that might work well in your specific application scenario.</span></span>

### <a name="dataadapter"></a><span data-ttu-id="2b8a9-300">DataAdapter</span><span class="sxs-lookup"><span data-stu-id="2b8a9-300">DataAdapter</span></span>
<span data-ttu-id="2b8a9-301">Hello **DataAdapter** classe consente toomodify un **DataSet** dell'oggetto e quindi inviare le modifiche di hello come operazioni INSERT, UPDATE e DELETE.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-301">hello **DataAdapter** class allows you toomodify a **DataSet** object and then submit hello changes as INSERT, UPDATE, and DELETE operations.</span></span> <span data-ttu-id="2b8a9-302">Se si utilizza hello **DataAdapter** in questo modo, è importante toonote che separano le chiamate vengono eseguite per ogni distinta operazione.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-302">If you are using hello **DataAdapter** in this manner, it is important toonote that separate calls are made for each distinct operation.</span></span> <span data-ttu-id="2b8a9-303">prestazioni tooimprove, utilizzare hello **UpdateBatchSize** numero di operazioni che devono essere raggruppate in un momento toohello della proprietà.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-303">tooimprove performance, use hello **UpdateBatchSize** property toohello number of operations that should be batched at a time.</span></span> <span data-ttu-id="2b8a9-304">Per altre informazioni, vedere [Esecuzione di operazioni batch usando DataAdapters](https://msdn.microsoft.com/library/aadf8fk2.aspx).</span><span class="sxs-lookup"><span data-stu-id="2b8a9-304">For more information, see [Performing Batch Operations Using DataAdapters](https://msdn.microsoft.com/library/aadf8fk2.aspx).</span></span>

### <a name="entity-framework"></a><span data-ttu-id="2b8a9-305">Entity Framework</span><span class="sxs-lookup"><span data-stu-id="2b8a9-305">Entity framework</span></span>
<span data-ttu-id="2b8a9-306">Entity Framework non supporta attualmente l'invio in batch.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-306">Entity Framework does not currently support batching.</span></span> <span data-ttu-id="2b8a9-307">Diversi sviluppatori della community di hello sono provato a soluzioni alternative toodemonstrate, ad esempio hello override **SaveChanges** metodo.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-307">Different developers in hello community have attempted toodemonstrate workarounds, such as override hello **SaveChanges** method.</span></span> <span data-ttu-id="2b8a9-308">Ma hello soluzioni sono in genere applicazioni complesse e personalizzate toohello e modello di dati.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-308">But hello solutions are typically complex and customized toohello application and data model.</span></span> <span data-ttu-id="2b8a9-309">progetto codeplex di Entity Framework Hello dispone attualmente di una pagina di discussione sulla richiesta di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-309">hello Entity Framework codeplex project currently has a discussion page on this feature request.</span></span> <span data-ttu-id="2b8a9-310">tooview questa discussione, vedere [Design Meeting Notes - 2 agosto 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).</span><span class="sxs-lookup"><span data-stu-id="2b8a9-310">tooview this discussion, see [Design Meeting Notes - August 2, 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).</span></span>

### <a name="xml"></a><span data-ttu-id="2b8a9-311">XML</span><span class="sxs-lookup"><span data-stu-id="2b8a9-311">XML</span></span>
<span data-ttu-id="2b8a9-312">Per motivi di completezza, riteniamo che è importante tootalk informazioni XML come strategia di invio in batch.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-312">For completeness, we feel that it is important tootalk about XML as a batching strategy.</span></span> <span data-ttu-id="2b8a9-313">Tuttavia, utilizzare hello di XML ha non offre vantaggi rispetto ad altri metodi e presenta numerosi svantaggi.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-313">However, hello use of XML has no advantages over other methods and several disadvantages.</span></span> <span data-ttu-id="2b8a9-314">approccio Hello è simile tootable parametri con valori di un file XML o una stringa viene passato tooa stored procedure anziché una tabella definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-314">hello approach is similar tootable-valued parameters, but an XML file or string is passed tooa stored procedure instead of a user-defined table.</span></span> <span data-ttu-id="2b8a9-315">procedura Hello archiviato analizza i comandi di hello nella procedura hello archiviato.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-315">hello stored procedure parses hello commands in hello stored procedure.</span></span>

<span data-ttu-id="2b8a9-316">Esistono diversi svantaggi toothis approccio:</span><span class="sxs-lookup"><span data-stu-id="2b8a9-316">There are several disadvantages toothis approach:</span></span>

* <span data-ttu-id="2b8a9-317">L'uso di XML può risultare complesso e soggetto a errori.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-317">Working with XML can be cumbersome and error prone.</span></span>
* <span data-ttu-id="2b8a9-318">Analisi hello XML nel database di hello può essere elevato della CPU.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-318">Parsing hello XML on hello database can be CPU-intensive.</span></span>
* <span data-ttu-id="2b8a9-319">Nella maggior parte dei casi questo metodo è più lento rispetto ai parametri con valori di tabella.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-319">In most cases, this method is slower than table-valued parameters.</span></span>

<span data-ttu-id="2b8a9-320">Per questi motivi, non è invece consigliabile usare hello XML per query in batch.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-320">For these reasons, hello use of XML for batch queries is not recommended.</span></span>

## <a name="batching-considerations"></a><span data-ttu-id="2b8a9-321">Considerazioni sull'invio in batch</span><span class="sxs-lookup"><span data-stu-id="2b8a9-321">Batching considerations</span></span>
<span data-ttu-id="2b8a9-322">Hello le sezioni seguenti fornisce informazioni aggiuntive per l'utilizzo di hello dell'invio in batch nelle applicazioni di Database SQL.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-322">hello following sections provide more guidance for hello use of batching in SQL Database applications.</span></span>

### <a name="tradeoffs"></a><span data-ttu-id="2b8a9-323">Compromessi</span><span class="sxs-lookup"><span data-stu-id="2b8a9-323">Tradeoffs</span></span>
<span data-ttu-id="2b8a9-324">A seconda dell'architettura, l'invio in batch può comportare un compromesso tra prestazioni e resilienza.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-324">Depending on your architecture, batching can involve a tradeoff between performance and resiliency.</span></span> <span data-ttu-id="2b8a9-325">Ad esempio, si consideri uno scenario di hello in cui il ruolo viene inaspettatamente disattivato.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-325">For example, consider hello scenario where your role unexpectedly goes down.</span></span> <span data-ttu-id="2b8a9-326">Se si perde una riga di dati, l'impatto di hello è minore di impatto hello di perdere un batch di grandi dimensioni di righe non inviate.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-326">If you lose one row of data, hello impact is smaller than hello impact of losing a large batch of unsubmitted rows.</span></span> <span data-ttu-id="2b8a9-327">È un rischio maggiore quando si buffer di riga prima di inviarli toohello database in un intervallo di tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-327">There is a greater risk when you buffer rows before sending them toohello database in a specified time window.</span></span>

<span data-ttu-id="2b8a9-328">Considerando questo compromesso, valutare il tipo di hello di operazioni da eseguire in batch.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-328">Because of this tradeoff, evaluate hello type of operations that you batch.</span></span> <span data-ttu-id="2b8a9-329">Usare più ampiamente i batch, con dimensioni maggiori e finestre temporali più ampie, per i dati meno critici.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-329">Batch more aggressively (larger batches and longer time windows) with data that is less critical.</span></span>

### <a name="batch-size"></a><span data-ttu-id="2b8a9-330">Dimensioni dei batch</span><span class="sxs-lookup"><span data-stu-id="2b8a9-330">Batch size</span></span>
<span data-ttu-id="2b8a9-331">Nei test, si è verificato in genere batch di grandi dimensioni toobreaking alcun vantaggio in blocchi più piccoli.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-331">In our tests, there was typically no advantage toobreaking large batches into smaller chunks.</span></span> <span data-ttu-id="2b8a9-332">In effetti, questa suddivisione ha causato spesso prestazioni inferiori rispetto all'invio di un singolo batch di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-332">In fact, this subdivision often resulted in slower performance than submitting a single large batch.</span></span> <span data-ttu-id="2b8a9-333">Ad esempio, si consideri uno scenario in cui si desidera tooinsert 1000 righe.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-333">For example, consider a scenario where you want tooinsert 1000 rows.</span></span> <span data-ttu-id="2b8a9-334">Hello nella tabella seguente mostra il tempo impiegato parametri con valori di tabella toouse tooinsert 1000 righe divise in batch più piccoli.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-334">hello following table shows how long it takes toouse table-valued parameters tooinsert 1000 rows when divided into smaller batches.</span></span>

| <span data-ttu-id="2b8a9-335">Dimensioni dei batch</span><span class="sxs-lookup"><span data-stu-id="2b8a9-335">Batch size</span></span> | <span data-ttu-id="2b8a9-336">Iterazioni</span><span class="sxs-lookup"><span data-stu-id="2b8a9-336">Iterations</span></span> | <span data-ttu-id="2b8a9-337">Parametri con valori di tabella (ms)</span><span class="sxs-lookup"><span data-stu-id="2b8a9-337">Table-valued parameters (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2b8a9-338">1000</span><span class="sxs-lookup"><span data-stu-id="2b8a9-338">1000</span></span> |<span data-ttu-id="2b8a9-339">1</span><span class="sxs-lookup"><span data-stu-id="2b8a9-339">1</span></span> |<span data-ttu-id="2b8a9-340">347</span><span class="sxs-lookup"><span data-stu-id="2b8a9-340">347</span></span> |
| <span data-ttu-id="2b8a9-341">500</span><span class="sxs-lookup"><span data-stu-id="2b8a9-341">500</span></span> |<span data-ttu-id="2b8a9-342">2</span><span class="sxs-lookup"><span data-stu-id="2b8a9-342">2</span></span> |<span data-ttu-id="2b8a9-343">355</span><span class="sxs-lookup"><span data-stu-id="2b8a9-343">355</span></span> |
| <span data-ttu-id="2b8a9-344">100</span><span class="sxs-lookup"><span data-stu-id="2b8a9-344">100</span></span> |<span data-ttu-id="2b8a9-345">10</span><span class="sxs-lookup"><span data-stu-id="2b8a9-345">10</span></span> |<span data-ttu-id="2b8a9-346">465</span><span class="sxs-lookup"><span data-stu-id="2b8a9-346">465</span></span> |
| <span data-ttu-id="2b8a9-347">50</span><span class="sxs-lookup"><span data-stu-id="2b8a9-347">50</span></span> |<span data-ttu-id="2b8a9-348">20</span><span class="sxs-lookup"><span data-stu-id="2b8a9-348">20</span></span> |<span data-ttu-id="2b8a9-349">630</span><span class="sxs-lookup"><span data-stu-id="2b8a9-349">630</span></span> |

> [!NOTE]
> <span data-ttu-id="2b8a9-350">I risultati non sono benchmark.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-350">Results are not benchmarks.</span></span> <span data-ttu-id="2b8a9-351">Vedere hello [nota sui risultati di temporizzazione in questo argomento](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="2b8a9-351">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="2b8a9-352">È possibile vedere che le prestazioni migliori di hello per 1000 righe sono toosubmit tutti contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-352">You can see that hello best performance for 1000 rows is toosubmit them all at once.</span></span> <span data-ttu-id="2b8a9-353">In altri test (non mostrato qui) si è verificato un toobreak di miglioramento delle prestazioni di piccole dimensioni un batch di 10000 righe in due batch da 5000.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-353">In other tests (not shown here) there was a small performance gain toobreak a 10000 row batch into two batches of 5000.</span></span> <span data-ttu-id="2b8a9-354">Ma schema della tabella hello per questi test è relativamente semplice, pertanto è consigliabile eseguire test sul tooverify le dimensioni di batch e dati specifici questi risultati.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-354">But hello table schema for these tests is relatively simple, so you should perform tests on your specific data and batch sizes tooverify these findings.</span></span>

<span data-ttu-id="2b8a9-355">Un altro fattore tooconsider è che se il batch complessivo hello diventa troppo grande, Database SQL potrebbe applicare limitazioni e rifiutarne di batch hello toocommit.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-355">Another factor tooconsider is that if hello total batch becomes too large, SQL Database might throttle and refuse toocommit hello batch.</span></span> <span data-ttu-id="2b8a9-356">Per ottenere risultati ottimali hello, testare il toodetermine uno scenario specifico nel caso di dimensioni ideali dei batch.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-356">For hello best results, test your specific scenario toodetermine if there is an ideal batch size.</span></span> <span data-ttu-id="2b8a9-357">Rendi hello batch configurabili al runtime tooenable modifiche rapide in base alle prestazioni o gli errori.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-357">Make hello batch size configurable at runtime tooenable quick adjustments based on performance or errors.</span></span>

<span data-ttu-id="2b8a9-358">Infine, bilanciare dimensioni hello di batch di hello con hello rischi con l'invio in batch.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-358">Finally, balance hello size of hello batch with hello risks associated with batching.</span></span> <span data-ttu-id="2b8a9-359">Se si verificano errori temporanei o ruolo hello ha esito negativo, considerare hello conseguenze di ripetere l'operazione di hello o di perdita di dati hello in batch hello.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-359">If there are transient errors or hello role fails, consider hello consequences of retrying hello operation or of losing hello data in hello batch.</span></span>

### <a name="parallel-processing"></a><span data-ttu-id="2b8a9-360">Elaborazione parallela</span><span class="sxs-lookup"><span data-stu-id="2b8a9-360">Parallel processing</span></span>
<span data-ttu-id="2b8a9-361">Cosa accade se si ha impiegato approccio hello di riduzione delle dimensioni di batch hello ma utilizzati più thread tooexecute hello lavoro?</span><span class="sxs-lookup"><span data-stu-id="2b8a9-361">What if you took hello approach of reducing hello batch size but used multiple threads tooexecute hello work?</span></span> <span data-ttu-id="2b8a9-362">Anche in questo caso, i test indicano che diversi batch multithreading di dimensioni ridotte producono prestazioni generalmente inferiori a un singolo batch di dimensioni maggiori.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-362">Again, our tests showed that several smaller multithreaded batches typically performed worse than a single larger batch.</span></span> <span data-ttu-id="2b8a9-363">Hello test seguente tenta tooinsert 1000 righe in una o più batch paralleli.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-363">hello following test attempts tooinsert 1000 rows in one or more parallel batches.</span></span> <span data-ttu-id="2b8a9-364">Questo test indica come più batch simultanei causino in effetti una riduzione delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-364">This test shows how more simultaneous batches actually decreased performance.</span></span>

| <span data-ttu-id="2b8a9-365">Dimensioni dei batch [iterazioni]</span><span class="sxs-lookup"><span data-stu-id="2b8a9-365">Batch size [Iterations]</span></span> | <span data-ttu-id="2b8a9-366">Due thread (ms)</span><span class="sxs-lookup"><span data-stu-id="2b8a9-366">Two threads (ms)</span></span> | <span data-ttu-id="2b8a9-367">Quattro thread (ms)</span><span class="sxs-lookup"><span data-stu-id="2b8a9-367">Four threads (ms)</span></span> | <span data-ttu-id="2b8a9-368">Sei thread (ms)</span><span class="sxs-lookup"><span data-stu-id="2b8a9-368">Six threads (ms)</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2b8a9-369">1000 [1]</span><span class="sxs-lookup"><span data-stu-id="2b8a9-369">1000 [1]</span></span> |<span data-ttu-id="2b8a9-370">277</span><span class="sxs-lookup"><span data-stu-id="2b8a9-370">277</span></span> |<span data-ttu-id="2b8a9-371">315</span><span class="sxs-lookup"><span data-stu-id="2b8a9-371">315</span></span> |<span data-ttu-id="2b8a9-372">266</span><span class="sxs-lookup"><span data-stu-id="2b8a9-372">266</span></span> |
| <span data-ttu-id="2b8a9-373">500 [2]</span><span class="sxs-lookup"><span data-stu-id="2b8a9-373">500 [2]</span></span> |<span data-ttu-id="2b8a9-374">548</span><span class="sxs-lookup"><span data-stu-id="2b8a9-374">548</span></span> |<span data-ttu-id="2b8a9-375">278</span><span class="sxs-lookup"><span data-stu-id="2b8a9-375">278</span></span> |<span data-ttu-id="2b8a9-376">256</span><span class="sxs-lookup"><span data-stu-id="2b8a9-376">256</span></span> |
| <span data-ttu-id="2b8a9-377">250 [4]</span><span class="sxs-lookup"><span data-stu-id="2b8a9-377">250 [4]</span></span> |<span data-ttu-id="2b8a9-378">405</span><span class="sxs-lookup"><span data-stu-id="2b8a9-378">405</span></span> |<span data-ttu-id="2b8a9-379">329</span><span class="sxs-lookup"><span data-stu-id="2b8a9-379">329</span></span> |<span data-ttu-id="2b8a9-380">265</span><span class="sxs-lookup"><span data-stu-id="2b8a9-380">265</span></span> |
| <span data-ttu-id="2b8a9-381">100 [10]</span><span class="sxs-lookup"><span data-stu-id="2b8a9-381">100 [10]</span></span> |<span data-ttu-id="2b8a9-382">488</span><span class="sxs-lookup"><span data-stu-id="2b8a9-382">488</span></span> |<span data-ttu-id="2b8a9-383">439</span><span class="sxs-lookup"><span data-stu-id="2b8a9-383">439</span></span> |<span data-ttu-id="2b8a9-384">391</span><span class="sxs-lookup"><span data-stu-id="2b8a9-384">391</span></span> |

> [!NOTE]
> <span data-ttu-id="2b8a9-385">I risultati non sono benchmark.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-385">Results are not benchmarks.</span></span> <span data-ttu-id="2b8a9-386">Vedere hello [nota sui risultati di temporizzazione in questo argomento](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="2b8a9-386">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="2b8a9-387">Esistono diverse potenziali cause delle prestazioni hello tooparallelism scadenza:</span><span class="sxs-lookup"><span data-stu-id="2b8a9-387">There are several potential reasons for hello degradation in performance due tooparallelism:</span></span>

* <span data-ttu-id="2b8a9-388">Sono presenti più chiamate di rete simultanee invece di una.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-388">There are multiple simultaneous network calls instead of one.</span></span>
* <span data-ttu-id="2b8a9-389">L'esecuzione di più operazioni su una singola tabella può determinare contese e blocchi.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-389">Multiple operations against a single table can result in contention and blocking.</span></span>
* <span data-ttu-id="2b8a9-390">Il multithreading implica overhead.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-390">There are overheads associated with multithreading.</span></span>
* <span data-ttu-id="2b8a9-391">costo di Hello dell'apertura di più connessioni supera il vantaggio di hello dell'elaborazione parallela.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-391">hello expense of opening multiple connections outweighs hello benefit of parallel processing.</span></span>

<span data-ttu-id="2b8a9-392">Se la destinazione è più tabelle o database, è possibile toosee miglioramento alcune delle prestazioni con questa strategia.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-392">If you target different tables or databases, it is possible toosee some performance gain with this strategy.</span></span> <span data-ttu-id="2b8a9-393">Il partizionamento orizzontale o le federazioni di database rappresentano uno scenario possibile per questo approccio.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-393">Database sharding or federations would be a scenario for this approach.</span></span> <span data-ttu-id="2b8a9-394">Partizionamento orizzontale utilizza più database e database tooeach di route dati diversi.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-394">Sharding uses multiple databases and routes different data tooeach database.</span></span> <span data-ttu-id="2b8a9-395">Se ogni piccolo batch verrà tooa diversi database, quindi l'esecuzione di operazioni di hello in parallelo può essere più efficiente.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-395">If each small batch is going tooa different database, then performing hello operations in parallel can be more efficient.</span></span> <span data-ttu-id="2b8a9-396">Tuttavia, miglioramento delle prestazioni di hello non è sufficientemente elevato toouse base hello per il partizionamento orizzontale di database toouse una decisione nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-396">However, hello performance gain is not significant enough toouse as hello basis for a decision toouse database sharding in your solution.</span></span>

<span data-ttu-id="2b8a9-397">In alcune progettazioni, l'esecuzione parallela di batch di piccole dimensioni può produrre un miglioramento della velocità effettiva delle richieste in un sistema sotto carico.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-397">In some designs, parallel execution of smaller batches can result in improved throughput of requests in a system under load.</span></span> <span data-ttu-id="2b8a9-398">In questo caso, anche se è più veloce tooprocess un singolo batch di dimensioni maggiori, l'elaborazione di più batch in parallelo potrebbero risultare più efficiente.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-398">In this case, even though it is quicker tooprocess a single larger batch, processing multiple batches in parallel might be more efficient.</span></span>

<span data-ttu-id="2b8a9-399">Se si usa l'esecuzione parallela, prendere in considerazione controllo hello di numero massimo di thread di lavoro.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-399">If you do use parallel execution, consider controlling hello maximum number of worker threads.</span></span> <span data-ttu-id="2b8a9-400">Un numero più piccolo potrebbe ridurre il rischio di contese e i tempi di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-400">A smaller number might result in less contention and a faster execution time.</span></span> <span data-ttu-id="2b8a9-401">Inoltre, prendere in considerazione hello ulteriori carichi di lavoro che si inserisce nel database di destinazione hello sia le connessioni e transazioni.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-401">Also, consider hello additional load that this places on hello target database both in connections and transactions.</span></span>

### <a name="related-performance-factors"></a><span data-ttu-id="2b8a9-402">Fattori correlati alle prestazioni</span><span class="sxs-lookup"><span data-stu-id="2b8a9-402">Related performance factors</span></span>
<span data-ttu-id="2b8a9-403">Le indicazioni tipiche relative alle prestazioni dei database influiscono anche sull'invio in batch.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-403">Typical guidance on database performance also affects batching.</span></span> <span data-ttu-id="2b8a9-404">Le prestazioni delle operazioni di inserimento, ad esempio, risultano ridotte per le tabelle con chiave primaria di grandi dimensioni o con numerosi indici non cluster.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-404">For example, insert performance is reduced for tables that have a large primary key or many nonclustered indexes.</span></span>

<span data-ttu-id="2b8a9-405">Se i parametri con valori di tabella utilizzano una stored procedure, è possibile utilizzare il comando hello **SET NOCOUNT ON** all'inizio di hello della procedura hello.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-405">If table-valued parameters use a stored procedure, you can use hello command **SET NOCOUNT ON** at hello beginning of hello procedure.</span></span> <span data-ttu-id="2b8a9-406">Questa istruzione rimuove restituito hello del conteggio hello di righe interessata hello nella procedura hello.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-406">This statement suppresses hello return of hello count of hello affected rows in hello procedure.</span></span> <span data-ttu-id="2b8a9-407">Tuttavia, nei test eseguiti, uso di hello **SET NOCOUNT ON** non aveva alcun effetto o una diminuzione delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-407">However, in our tests, hello use of **SET NOCOUNT ON** either had no effect or decreased performance.</span></span> <span data-ttu-id="2b8a9-408">Hello stored procedure di test è semplice con un singolo **inserire** dal parametro con valori di tabella hello.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-408">hello test stored procedure was simple with a single **INSERT** command from hello table-valued parameter.</span></span> <span data-ttu-id="2b8a9-409">È possibile che stored procedure più complesse possano trarre vantaggio da questa istruzione.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-409">It is possible that more complex stored procedures would benefit from this statement.</span></span> <span data-ttu-id="2b8a9-410">Non si presuppone che l'aggiunta tuttavia **SET NOCOUNT ON** tooyour stored procedure migliori automaticamente le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-410">But don’t assume that adding **SET NOCOUNT ON** tooyour stored procedure automatically improves performance.</span></span> <span data-ttu-id="2b8a9-411">toounderstand hello effetto, testare la stored procedure con e senza hello **SET NOCOUNT ON** istruzione.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-411">toounderstand hello effect, test your stored procedure with and without hello **SET NOCOUNT ON** statement.</span></span>

## <a name="batching-scenarios"></a><span data-ttu-id="2b8a9-412">Scenari di invio in batch</span><span class="sxs-lookup"><span data-stu-id="2b8a9-412">Batching scenarios</span></span>
<span data-ttu-id="2b8a9-413">Hello sezioni seguenti descrivono come parametri con valori di tabella toouse in tre scenari di applicazione.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-413">hello following sections describe how toouse table-valued parameters in three application scenarios.</span></span> <span data-ttu-id="2b8a9-414">Hello primo scenario illustra come la memorizzazione nel buffer e l'invio in batch possono essere usati insieme.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-414">hello first scenario shows how buffering and batching can work together.</span></span> <span data-ttu-id="2b8a9-415">il secondo scenario di Hello migliora le prestazioni eseguendo operazioni master / dettaglio in una chiamata a singola stored procedure.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-415">hello second scenario improves performance by performing master-detail operations in a single stored procedure call.</span></span> <span data-ttu-id="2b8a9-416">Hello nello scenario finale illustra come parametri con valori di tabella toouse in un'operazione "UPSERT".</span><span class="sxs-lookup"><span data-stu-id="2b8a9-416">hello final scenario shows how toouse table-valued parameters in an “UPSERT” operation.</span></span>

### <a name="buffering"></a><span data-ttu-id="2b8a9-417">Buffering</span><span class="sxs-lookup"><span data-stu-id="2b8a9-417">Buffering</span></span>
<span data-ttu-id="2b8a9-418">Sebbene alcuni scenari siano particolarmente adatti all'invio in batch, ne esistono numerosi che potrebbero trarre vantaggio da questo tipo di operazione grazie all'elaborazione ritardata.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-418">Although there are some scenarios that are obvious candidate for batching, there are many scenarios that could take advantage of batching by delayed processing.</span></span> <span data-ttu-id="2b8a9-419">Tuttavia, anche l'elaborazione ritardata comporta un rischio maggiore hello dati vengono persi in caso di hello di un errore imprevisto.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-419">However, delayed processing also carries a greater risk that hello data is lost in hello event of an unexpected failure.</span></span> <span data-ttu-id="2b8a9-420">È importante toounderstand questo rischio e hello conseguenze.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-420">It is important toounderstand this risk and consider hello consequences.</span></span>

<span data-ttu-id="2b8a9-421">Ad esempio, si consideri un'applicazione web che tiene traccia della cronologia di navigazione hello di ogni utente.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-421">For example, consider a web application that tracks hello navigation history of each user.</span></span> <span data-ttu-id="2b8a9-422">In ogni richiesta di pagina, un'applicazione hello esegua visualizzazione pagina database chiamata toorecord hello dell'utente.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-422">On each page request, hello application could make a database call toorecord hello user’s page view.</span></span> <span data-ttu-id="2b8a9-423">Ma, è possibile ottenere prestazioni e scalabilità buffering delle attività di navigazione degli utenti hello e quindi invia questo database toohello dati in batch.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-423">But higher performance and scalability can be achieved by buffering hello users’ navigation activities and then sending this data toohello database in batches.</span></span> <span data-ttu-id="2b8a9-424">È possibile attivare l'aggiornamento del database hello dal tempo trascorso e/o dimensione del buffer.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-424">You can trigger hello database update by elapsed time and/or buffer size.</span></span> <span data-ttu-id="2b8a9-425">Ad esempio, una regola è possibile specificare che tale batch hello deve essere elaborato dopo 20 secondi o quando il buffer di hello raggiunge i 1000 elementi.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-425">For example, a rule could specify that hello batch should be processed after 20 seconds or when hello buffer reaches 1000 items.</span></span>

<span data-ttu-id="2b8a9-426">codice Hello seguente viene utilizzato [Reactive Extensions - Rx](https://msdn.microsoft.com/data/gg577609) tooprocess memorizzato nel buffer gli eventi generati da una classe di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-426">hello following code example uses [Reactive Extensions - Rx](https://msdn.microsoft.com/data/gg577609) tooprocess buffered events raised by a monitoring class.</span></span> <span data-ttu-id="2b8a9-427">Quando hello riempimenti buffer o viene raggiunto un timeout, batch hello dei dati utente viene inviato toohello database con un parametro con valori di tabella.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-427">When hello buffer fills or a timeout is reached, hello batch of user data is sent toohello database with a table-valued parameter.</span></span>

<span data-ttu-id="2b8a9-428">Hello seguenti NavHistoryData classe modelli hello utente navigazione dettagli.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-428">hello following NavHistoryData class models hello user navigation details.</span></span> <span data-ttu-id="2b8a9-429">Contiene informazioni di base, ad esempio l'identificatore utente hello, hello URL accessibili e hello tempo di accesso.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-429">It contains basic information such as hello user identifier, hello URL accessed, and hello access time.</span></span>

    public class NavHistoryData
    {
        public NavHistoryData(int userId, string url, DateTime accessTime)
        { UserId = userId; URL = url; AccessTime = accessTime; }
        public int UserId { get; set; }
        public string URL { get; set; }
        public DateTime AccessTime { get; set; }
    }

<span data-ttu-id="2b8a9-430">classe NavHistoryDataMonitor Hello è responsabile del buffering database toohello di hello utente spostamento dati.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-430">hello NavHistoryDataMonitor class is responsible for buffering hello user navigation data toohello database.</span></span> <span data-ttu-id="2b8a9-431">Contiene un metodo RecordUserNavigationEntry che risponde generando un evento **OnAdded** .</span><span class="sxs-lookup"><span data-stu-id="2b8a9-431">It contains a method, RecordUserNavigationEntry, which responds by raising an **OnAdded** event.</span></span> <span data-ttu-id="2b8a9-432">Hello codice seguente illustra la logica del costruttore hello che utilizza Rx toocreate una raccolta osservabile in base all'evento hello.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-432">hello following code shows hello constructor logic that uses Rx toocreate an observable collection based on hello event.</span></span> <span data-ttu-id="2b8a9-433">Viene quindi sottoscritta la raccolta osservabile toothis con metodo hello del Buffer.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-433">It then subscribes toothis observable collection with hello Buffer method.</span></span> <span data-ttu-id="2b8a9-434">overload di Hello specifica che buffer hello deve essere inviato ogni 20 secondi o 1000 voci.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-434">hello overload specifies that hello buffer should be sent every 20 seconds or 1000 entries.</span></span>

    public NavHistoryDataMonitor()
    {
        var observableData =
            Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

        observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
    }

<span data-ttu-id="2b8a9-435">gestore Hello converte tutti gli elementi memorizzati nel buffer hello in un tipo con valori di tabella e quindi passa questa procedura tooa archiviato di tipo batch hello processi.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-435">hello handler converts all of hello buffered items into a table-valued type and then passes this type tooa stored procedure that processes hello batch.</span></span> <span data-ttu-id="2b8a9-436">Hello codice seguente viene illustrato definizione completa di hello per le classi NavHistoryDataMonitor hello e hello NavHistoryDataEventArgs.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-436">hello following code shows hello complete definition for both hello NavHistoryDataEventArgs and hello NavHistoryDataMonitor classes.</span></span>

    public class NavHistoryDataEventArgs : System.EventArgs
    {
        public NavHistoryDataEventArgs(NavHistoryData data) { Data = data; }
        public NavHistoryData Data { get; set; }
    }

    public class NavHistoryDataMonitor
    {
        public event EventHandler<NavHistoryDataEventArgs> OnAdded;

        public NavHistoryDataMonitor()
        {
            var observableData =
                Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

            observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
        }

        public void RecordUserNavigationEntry(NavHistoryData data)
        {    
            if (OnAdded != null)
                OnAdded(this, new NavHistoryDataEventArgs(data));
        }

        protected void Handler(IList<EventPattern<NavHistoryDataEventArgs>> items)
        {
            DataTable navHistoryBatch = new DataTable("NavigationHistoryBatch");
            navHistoryBatch.Columns.Add("UserId", typeof(int));
            navHistoryBatch.Columns.Add("URL", typeof(string));
            navHistoryBatch.Columns.Add("AccessTime", typeof(DateTime));
            foreach (EventPattern<NavHistoryDataEventArgs> item in items)
            {
                NavHistoryData data = item.EventArgs.Data;
                navHistoryBatch.Rows.Add(data.UserId, data.URL, data.AccessTime);
            }

            using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
            {
                connection.Open();

                SqlCommand cmd = new SqlCommand("sp_RecordUserNavigation", connection);
                cmd.CommandType = CommandType.StoredProcedure;

                cmd.Parameters.Add(
                    new SqlParameter()
                    {
                        ParameterName = "@NavHistoryBatch",
                        SqlDbType = SqlDbType.Structured,
                        TypeName = "NavigationHistoryTableType",
                        Value = navHistoryBatch,
                    });

                cmd.ExecuteNonQuery();
            }
        }
    }

<span data-ttu-id="2b8a9-437">toouse questa classe di buffering, un'applicazione hello crea un oggetto NavHistoryDataMonitor statico.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-437">toouse this buffering class, hello application creates a static NavHistoryDataMonitor object.</span></span> <span data-ttu-id="2b8a9-438">Ogni volta che un utente accede a una pagina, un'applicazione hello chiama il metodo NavHistoryDataMonitor.RecordUserNavigationEntry hello.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-438">Each time a user accesses a page, hello application calls hello NavHistoryDataMonitor.RecordUserNavigationEntry method.</span></span> <span data-ttu-id="2b8a9-439">Hello logica di buffering continua tootake cure l'invio di questi database toohello voci in batch.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-439">hello buffering logic proceeds tootake care of sending these entries toohello database in batches.</span></span>

### <a name="master-detail"></a><span data-ttu-id="2b8a9-440">Master/dettaglio</span><span class="sxs-lookup"><span data-stu-id="2b8a9-440">Master detail</span></span>
<span data-ttu-id="2b8a9-441">I parametri con valori di tabella sono utili per gli scenari INSERT semplici.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-441">Table-valued parameters are useful for simple INSERT scenarios.</span></span> <span data-ttu-id="2b8a9-442">Tuttavia, può essere più impegnativo inserimenti toobatch che coinvolgono più di una tabella.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-442">However, it can be more challenging toobatch inserts that involve more than one table.</span></span> <span data-ttu-id="2b8a9-443">scenario "master-details" Hello è un buon esempio.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-443">hello “master/detail” scenario is a good example.</span></span> <span data-ttu-id="2b8a9-444">la tabella master di Hello identifica l'entità primaria hello.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-444">hello master table identifies hello primary entity.</span></span> <span data-ttu-id="2b8a9-445">Uno o più tabelle dettagli archiviano altri dati sull'entità hello.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-445">One or more detail tables store more data about hello entity.</span></span> <span data-ttu-id="2b8a9-446">In questo scenario, relazioni di chiave esterna applicano relazione hello di entità master univoca di dettagli tooa.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-446">In this scenario, foreign key relationships enforce hello relationship of details tooa unique master entity.</span></span> <span data-ttu-id="2b8a9-447">Si consideri una versione semplificata di una tabella PurchaseOrder e la tabella associata OrderDetail.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-447">Consider a simplified version of a PurchaseOrder table and its associated OrderDetail table.</span></span> <span data-ttu-id="2b8a9-448">Hello Transact-SQL seguente crea tabella PurchaseOrder hello con quattro colonne: lo stato, OrderDate, CustomerID e OrderID.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-448">hello following Transact-SQL creates hello PurchaseOrder table with four columns: OrderID, OrderDate, CustomerID, and Status.</span></span>

    CREATE TABLE [dbo].[PurchaseOrder](
    [OrderID] [int] IDENTITY(1,1) NOT NULL,
    [OrderDate] [datetime] NOT NULL,
    [CustomerID] [int] NOT NULL,
    [Status] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrder] 
    PRIMARY KEY CLUSTERED ( [OrderID] ASC ))

<span data-ttu-id="2b8a9-449">Ogni ordine contiene uno o più acquisti di prodotti.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-449">Each order contains one or more product purchases.</span></span> <span data-ttu-id="2b8a9-450">Queste informazioni vengono acquisite nella tabella PurchaseOrderDetail hello.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-450">This information is captured in hello PurchaseOrderDetail table.</span></span> <span data-ttu-id="2b8a9-451">Hello Transact-SQL seguente crea tabella PurchaseOrderDetail hello con cinque colonne: OrderID, OrderDetailID, ProductID, UnitPrice e OrderQty.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-451">hello following Transact-SQL creates hello PurchaseOrderDetail table with five columns: OrderID, OrderDetailID, ProductID, UnitPrice, and OrderQty.</span></span>

    CREATE TABLE [dbo].[PurchaseOrderDetail](
    [OrderID] [int] NOT NULL,
    [OrderDetailID] [int] IDENTITY(1,1) NOT NULL,
    [ProductID] [int] NOT NULL,
    [UnitPrice] [money] NULL,
    [OrderQty] [smallint] NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrderDetail] PRIMARY KEY CLUSTERED 
    ( [OrderID] ASC, [OrderDetailID] ASC ))

<span data-ttu-id="2b8a9-452">colonna OrderID Hello nella tabella PurchaseOrderDetail hello deve fare riferimento a un ordine dalla tabella PurchaseOrder hello.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-452">hello OrderID column in hello PurchaseOrderDetail table must reference an order from hello PurchaseOrder table.</span></span> <span data-ttu-id="2b8a9-453">Hello seguente definizione di una chiave esterna applica il vincolo.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-453">hello following definition of a foreign key enforces this constraint.</span></span>

    ALTER TABLE [dbo].[PurchaseOrderDetail]  WITH CHECK ADD 
    CONSTRAINT [FK_OrderID_PurchaseOrder] FOREIGN KEY([OrderID])
    REFERENCES [dbo].[PurchaseOrder] ([OrderID])

<span data-ttu-id="2b8a9-454">In parametri con valori di tabella toouse di ordine, è necessario disporre di un tipo di tabella definito dall'utente per ogni tabella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-454">In order toouse table-valued parameters, you must have one user-defined table type for each target table.</span></span>

    CREATE TYPE PurchaseOrderTableType AS TABLE 
    ( OrderID INT,
      OrderDate DATETIME,
      CustomerID INT,
      Status NVARCHAR(50) );
    GO

    CREATE TYPE PurchaseOrderDetailTableType AS TABLE 
    ( OrderID INT,
      ProductID INT,
      UnitPrice MONEY,
      OrderQty SMALLINT );
    GO

<span data-ttu-id="2b8a9-455">Definire quindi una stored procedure che accetti tabelle di questi tipi.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-455">Then define a stored procedure that accepts tables of these types.</span></span> <span data-ttu-id="2b8a9-456">Questa procedura consente a un batch di toolocally applicazione un set di ordini e dettagli ordine in una singola chiamata.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-456">This procedure allows an application toolocally batch a set of orders and order details in a single call.</span></span> <span data-ttu-id="2b8a9-457">Hello Transact-SQL seguente fornisce hello dichiarazione di stored procedure completa per questo esempio di ordine di acquisto.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-457">hello following Transact-SQL provides hello complete stored procedure declaration for this purchase order example.</span></span>

    CREATE PROCEDURE sp_InsertOrdersBatch (
    @orders as PurchaseOrderTableType READONLY,
    @details as PurchaseOrderDetailTableType READONLY )
    AS
    SET NOCOUNT ON;

    -- Table that connects hello order identifiers in hello @orders
    -- table with hello actual order identifiers in hello PurchaseOrder table
    DECLARE @IdentityLink AS TABLE ( 
    SubmittedKey int, 
    ActualKey int, 
    RowNumber int identity(1,1)
    );

          -- Add new orders toohello PurchaseOrder table, storing hello actual
    -- order identifiers in hello @IdentityLink table   
    INSERT INTO PurchaseOrder ([OrderDate], [CustomerID], [Status])
    OUTPUT inserted.OrderID INTO @IdentityLink (ActualKey)
    SELECT [OrderDate], [CustomerID], [Status] FROM @orders ORDER BY OrderID;

    -- Match hello passed-in order identifiers with hello actual identifiers
    -- and complete hello @IdentityLink table for use with inserting hello details
    WITH OrderedRows As (
    SELECT OrderID, ROW_NUMBER () OVER (ORDER BY OrderID) As RowNumber 
    FROM @orders
    )
    UPDATE @IdentityLink SET SubmittedKey = M.OrderID
    FROM @IdentityLink L JOIN OrderedRows M ON L.RowNumber = M.RowNumber;

    -- Insert hello order details into hello PurchaseOrderDetail table, 
          -- using hello actual order identifiers of hello master table, PurchaseOrder
    INSERT INTO PurchaseOrderDetail (
    [OrderID],
    [ProductID],
    [UnitPrice],
    [OrderQty] )
    SELECT L.ActualKey, D.ProductID, D.UnitPrice, D.OrderQty
    FROM @details D
    JOIN @IdentityLink L ON L.SubmittedKey = D.OrderID;
    GO

<span data-ttu-id="2b8a9-458">In questo esempio hello definite localmente @IdentityLink tabella archivia hello OrderID i valori effettivi dalle righe appena inserita hello.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-458">In this example, hello locally defined @IdentityLink table stores hello actual OrderID values from hello newly inserted rows.</span></span> <span data-ttu-id="2b8a9-459">Questi identificatori di ordine sono diversi dai valori OrderID temporanei hello in hello @orders e @details parametri con valori di tabella.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-459">These order identifiers are different from hello temporary OrderID values in hello @orders and @details table-valued parameters.</span></span> <span data-ttu-id="2b8a9-460">Per questo motivo, hello @IdentityLink tabella collega quindi i valori OrderID hello in hello @orders toohello reale OrderID valori dei parametri per le nuove righe hello nella tabella PurchaseOrder hello.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-460">For this reason, hello @IdentityLink table then connects hello OrderID values from hello @orders parameter toohello real OrderID values for hello new rows in hello PurchaseOrder table.</span></span> <span data-ttu-id="2b8a9-461">Dopo questo passaggio, hello @IdentityLink tabella può facilitare l'inserimento dei dettagli ordine hello con hello OrderID effettivo che soddisfa il vincolo di chiave esterna di hello.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-461">After this step, hello @IdentityLink table can facilitate inserting hello order details with hello actual OrderID that satisfies hello foreign key constraint.</span></span>

<span data-ttu-id="2b8a9-462">Questa stored procedure può essere utilizzata dal codice o da altre chiamate Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-462">This stored procedure can be used from code or from other Transact-SQL calls.</span></span> <span data-ttu-id="2b8a9-463">Nella sezione hello parametri con valori di tabella di questo articolo per un esempio di codice.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-463">See hello table-valued parameters section of this paper for a code example.</span></span> <span data-ttu-id="2b8a9-464">Hello Transact-SQL seguente viene illustrato come toocall hello sp_InsertOrdersBatch.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-464">hello following Transact-SQL shows how toocall hello sp_InsertOrdersBatch.</span></span>

    declare @orders as PurchaseOrderTableType
    declare @details as PurchaseOrderDetailTableType

    INSERT @orders 
    ([OrderID], [OrderDate], [CustomerID], [Status])
    VALUES(1, '1/1/2013', 1125, 'Complete'),
    (2, '1/13/2013', 348, 'Processing'),
    (3, '1/12/2013', 2504, 'Shipped')

    INSERT @details
    ([OrderID], [ProductID], [UnitPrice], [OrderQty])
    VALUES(1, 10, $11.50, 1),
    (1, 12, $1.58, 1),
    (2, 23, $2.57, 2),
    (3, 4, $10.00, 1)

    exec sp_InsertOrdersBatch @orders, @details

<span data-ttu-id="2b8a9-465">Questa soluzione consente a un set di valori OrderID che iniziano da 1 toouse ogni batch.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-465">This solution allows each batch toouse a set of OrderID values that begin at 1.</span></span> <span data-ttu-id="2b8a9-466">Questi valori OrderID temporanei descrivono le relazioni di hello in batch hello ma hello effettivo OrderID valori vengono determinati in fase di hello dell'operazione di inserimento hello.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-466">These temporary OrderID values describe hello relationships in hello batch, but hello actual OrderID values are determined at hello time of hello insert operation.</span></span> <span data-ttu-id="2b8a9-467">È possibile eseguire hello stesse istruzioni nell'esempio precedente hello ripetutamente e generare gli ordini univoci nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-467">You can run hello same statements in hello previous example repeatedly and generate unique orders in hello database.</span></span> <span data-ttu-id="2b8a9-468">Per questo motivo, considerare l'aggiunta di più logica di database o di codice che impedisca gli ordini duplicati quando si usa questa tecnica di invio in batch.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-468">For this reason, consider adding more code or database logic that prevents duplicate orders when using this batching technique.</span></span>

<span data-ttu-id="2b8a9-469">In questo esempio viene spiegato che è possibile eseguire in batch anche operazioni di database più complesse, ad esempio operazioni master/dettaglio, usando i parametri con valori di tabella.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-469">This example demonstrates that even more complex database operations, such as master-detail operations, can be batched using table-valued parameters.</span></span>

### <a name="upsert"></a><span data-ttu-id="2b8a9-470">UPSERT</span><span class="sxs-lookup"><span data-stu-id="2b8a9-470">UPSERT</span></span>
<span data-ttu-id="2b8a9-471">Un altro scenario di invio in batch prevede l'aggiornamento simultaneo di righe esistenti e l'inserimento di nuove righe.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-471">Another batching scenario involves simultaneously updating existing rows and inserting new rows.</span></span> <span data-ttu-id="2b8a9-472">Questa operazione è talvolta tooas cui un'operazione "UPSERT" (aggiornamento + inserimento).</span><span class="sxs-lookup"><span data-stu-id="2b8a9-472">This operation is sometimes referred tooas an “UPSERT” (update + insert) operation.</span></span> <span data-ttu-id="2b8a9-473">Anziché eseguire chiamate separate tooINSERT e l'aggiornamento, istruzione MERGE hello è più adatta toothis attività.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-473">Rather than making separate calls tooINSERT and UPDATE, hello MERGE statement is best suited toothis task.</span></span> <span data-ttu-id="2b8a9-474">Hello istruzione MERGE può eseguire sia insert e operazioni in una singola chiamata di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-474">hello MERGE statement can perform both insert and update operations in a single call.</span></span>

<span data-ttu-id="2b8a9-475">Parametri con valori di tabella possono essere utilizzati con hello MERGE istruzione tooperform aggiornamenti e inserimenti.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-475">Table-valued parameters can be used with hello MERGE statement tooperform updates and inserts.</span></span> <span data-ttu-id="2b8a9-476">Si consideri ad esempio una tabella Employee semplificata contenente hello seguenti colonne: EmployeeID, FirstName, LastName, SocialSecurityNumber:</span><span class="sxs-lookup"><span data-stu-id="2b8a9-476">For example, consider a simplified Employee table that contains hello following columns: EmployeeID, FirstName, LastName, SocialSecurityNumber:</span></span>

    CREATE TABLE [dbo].[Employee](
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [SocialSecurityNumber] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_Employee] PRIMARY KEY CLUSTERED 
    ([EmployeeID] ASC ))

<span data-ttu-id="2b8a9-477">In questo esempio, è possibile utilizzare hello fatto tale hello SocialSecurityNumber univoco tooperform un'unione di più dipendenti.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-477">In this example, you can use hello fact that hello SocialSecurityNumber is unique tooperform a MERGE of multiple employees.</span></span> <span data-ttu-id="2b8a9-478">Creare innanzitutto il tipo di tabella definito dall'utente hello:</span><span class="sxs-lookup"><span data-stu-id="2b8a9-478">First, create hello user-defined table type:</span></span>

    CREATE TYPE EmployeeTableType AS TABLE 
    ( Employee_ID INT,
      FirstName NVARCHAR(50),
      LastName NVARCHAR(50),
      SocialSecurityNumber NVARCHAR(50) );
    GO

<span data-ttu-id="2b8a9-479">Successivamente, creare una stored procedure oppure scrivere codice che usa hello aggiornamento hello tooperform istruzione di tipo MERGE e insert.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-479">Next, create a stored procedure or write code that uses hello MERGE statement tooperform hello update and insert.</span></span> <span data-ttu-id="2b8a9-480">Hello esempio seguente viene utilizzata hello istruzione MERGE in un parametro con valori di tabella, @employees, di tipo EmployeeTableType.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-480">hello following example uses hello MERGE statement on a table-valued parameter, @employees, of type EmployeeTableType.</span></span> <span data-ttu-id="2b8a9-481">contenuto di hello Hello @employees tabella non vengono visualizzati qui.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-481">hello contents of hello @employees table are not shown here.</span></span>

    MERGE Employee AS target
    USING (SELECT [FirstName], [LastName], [SocialSecurityNumber] FROM @employees) 
    AS source ([FirstName], [LastName], [SocialSecurityNumber])
    ON (target.[SocialSecurityNumber] = source.[SocialSecurityNumber])
    WHEN MATCHED THEN 
    UPDATE SET
    target.FirstName = source.FirstName, 
    target.LastName = source.LastName
    WHEN NOT MATCHED THEN
       INSERT ([FirstName], [LastName], [SocialSecurityNumber])
       VALUES (source.[FirstName], source.[LastName], source.[SocialSecurityNumber]);

<span data-ttu-id="2b8a9-482">Per ulteriori informazioni, vedere la documentazione di hello ed esempi per l'istruzione MERGE hello.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-482">For more information, see hello documentation and examples for hello MERGE statement.</span></span> <span data-ttu-id="2b8a9-483">Sebbene hello stessa operazione possa essere eseguita in più passaggi chiamata alla stored procedure con operazioni INSERT e UPDATE separate, hello istruzione MERGE è più efficiente.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-483">Although hello same work could be performed in a multiple-step stored procedure call with separate INSERT and UPDATE operations, hello MERGE statement is more efficient.</span></span> <span data-ttu-id="2b8a9-484">Codice del database è inoltre possibile creare chiamate Transact-SQL che utilizzano l'istruzione MERGE hello direttamente senza richiedere due chiamate di database per INSERT e UPDATE.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-484">Database code can also construct Transact-SQL calls that use hello MERGE statement directly without requiring two database calls for INSERT and UPDATE.</span></span>

## <a name="recommendation-summary"></a><span data-ttu-id="2b8a9-485">Riepilogo delle indicazioni</span><span class="sxs-lookup"><span data-stu-id="2b8a9-485">Recommendation summary</span></span>
<span data-ttu-id="2b8a9-486">Hello elenco riportato di seguito viene fornito un riepilogo di hello batch raccomandazioni descritte in questo argomento:</span><span class="sxs-lookup"><span data-stu-id="2b8a9-486">hello following list provides a summary of hello batching recommendations discussed in this topic:</span></span>

* <span data-ttu-id="2b8a9-487">Utilizzare la memorizzazione nel buffer e l'invio in batch tooincrease hello prestazioni e scalabilità delle applicazioni di Database SQL.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-487">Use buffering and batching tooincrease hello performance and scalability of SQL Database applications.</span></span>
* <span data-ttu-id="2b8a9-488">Comprendere i compromessi hello tra l'invio in batch/buffering e resilienza.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-488">Understand hello tradeoffs between batching/buffering and resiliency.</span></span> <span data-ttu-id="2b8a9-489">Durante un errore di ruolo, il rischio di hello di perdere un batch non elaborato di dati aziendali critici superiore a quello previsto miglioramento delle prestazioni hello dell'invio in batch.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-489">During a role failure, hello risk of losing an unprocessed batch of business-critical data might outweigh hello performance benefit of batching.</span></span>
* <span data-ttu-id="2b8a9-490">Tentativo tookeep tutti i database toohello chiamate all'interno di una latenza tooreduce singolo Data Center.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-490">Attempt tookeep all calls toohello database within a single datacenter tooreduce latency.</span></span>
* <span data-ttu-id="2b8a9-491">Se si sceglie una tecnica di invio in batch singola, i parametri con valori di tabella offrono flessibilità e prestazioni ottimali hello.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-491">If you choose a single batching technique, table-valued parameters offer hello best performance and flexibility.</span></span>
* <span data-ttu-id="2b8a9-492">Per più veloce hello inserire le prestazioni, seguire queste linee guida generali ma testare lo scenario:</span><span class="sxs-lookup"><span data-stu-id="2b8a9-492">For hello fastest insert performance, follow these general guidelines but test your scenario:</span></span>
  * <span data-ttu-id="2b8a9-493">Per < 100 righe, usare un singolo comando INSERT con parametri.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-493">For < 100 rows, use a single parameterized INSERT command.</span></span>
  * <span data-ttu-id="2b8a9-494">Per < 1000 righe usare parametri con valori di tabella.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-494">For < 1000 rows, use table-valued parameters.</span></span>
  * <span data-ttu-id="2b8a9-495">Per >= 1000 righe usare SqlBulkCopy.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-495">For >= 1000 rows, use SqlBulkCopy.</span></span>
* <span data-ttu-id="2b8a9-496">Per aggiornare e le operazioni di eliminazione, utilizzare i parametri con valori di tabella con logica della stored procedure che determina il corretto funzionamento di hello in ogni riga nel parametro tabella hello.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-496">For update and delete operations, use table-valued parameters with stored procedure logic that determines hello correct operation on each row in hello table parameter.</span></span>
* <span data-ttu-id="2b8a9-497">Linee guida sulle dimensioni dei batch:</span><span class="sxs-lookup"><span data-stu-id="2b8a9-497">Batch size guidelines:</span></span>
  * <span data-ttu-id="2b8a9-498">Utilizzare hello più grande le dimensioni di batch in base allo scopo dell'applicazione e i requisiti aziendali.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-498">Use hello largest batch sizes that make sense for your application and business requirements.</span></span>
  * <span data-ttu-id="2b8a9-499">Il miglioramento delle prestazioni di hello saldo di batch di grandi dimensioni con rischio di hello di errori temporanei o irreversibili.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-499">Balance hello performance gain of large batches with hello risks of temporary or catastrophic failures.</span></span> <span data-ttu-id="2b8a9-500">Qual è la conseguenza hello di tentativi o perdita di dati hello in batch hello?</span><span class="sxs-lookup"><span data-stu-id="2b8a9-500">What is hello consequence of retries or loss of hello data in hello batch?</span></span> 
  * <span data-ttu-id="2b8a9-501">Test hello più grande batch dimensioni tooverify che il Database SQL non li respinga.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-501">Test hello largest batch size tooverify that SQL Database does not reject it.</span></span>
  * <span data-ttu-id="2b8a9-502">Creare le impostazioni di configurazione di tale controllo invio in batch, ad esempio la dimensione del batch hello o finestra temporale di buffering hello.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-502">Create configuration settings that control batching, such as hello batch size or hello buffering time window.</span></span> <span data-ttu-id="2b8a9-503">Queste impostazioni offrono flessibilità.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-503">These settings provide flexibility.</span></span> <span data-ttu-id="2b8a9-504">È possibile modificare l'invio in batch comportamento nell'ambiente di produzione senza ridistribuire il servizio di cloud hello hello.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-504">You can change hello batching behavior in production without redeploying hello cloud service.</span></span>
* <span data-ttu-id="2b8a9-505">Evitare l'esecuzione parallela di batch che operano su una singola tabella in un database.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-505">Avoid parallel execution of batches that operate on a single table in one database.</span></span> <span data-ttu-id="2b8a9-506">Se si sceglie un singolo batch toodivide tra più thread di lavoro, eseguire test toodetermine hello numero ideale di thread.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-506">If you do choose toodivide a single batch across multiple worker threads, run tests toodetermine hello ideal number of threads.</span></span> <span data-ttu-id="2b8a9-507">Dopo una soglia non specificata, più thread determinano una riduzione delle prestazioni invece di un aumento.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-507">After an unspecified threshold, more threads will decrease performance rather than increase it.</span></span>
* <span data-ttu-id="2b8a9-508">Considerare il buffering in base a dimensioni e tempo come modalità di implementazione dell'invio in batch per più scenari.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-508">Consider buffering on size and time as a way of implementing batching for more scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b8a9-509">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2b8a9-509">Next steps</span></span>
<span data-ttu-id="2b8a9-510">In questo articolo attivando la modalità progettazione di database e le tecniche di codifica correlati toobatching può migliorare le prestazioni dell'applicazione e la scalabilità.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-510">This article focused on how database design and coding techniques related toobatching can improve your application performance and scalability.</span></span> <span data-ttu-id="2b8a9-511">Questo è però solo uno dei fattori della strategia complessiva.</span><span class="sxs-lookup"><span data-stu-id="2b8a9-511">But this is just one factor in your overall strategy.</span></span> <span data-ttu-id="2b8a9-512">Per altre prestazioni tooimprove modi e scalabilità, vedere [linee guida sulle prestazioni di Database SQL di Azure per singoli database](sql-database-performance-guidance.md) e [prezzo e considerazioni sulle prestazioni per un pool elastico](sql-database-elastic-pool-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="2b8a9-512">For more ways tooimprove performance and scalability, see [Azure SQL Database performance guidance for single databases](sql-database-performance-guidance.md) and [Price and performance considerations for an elastic pool](sql-database-elastic-pool-guidance.md).</span></span>

