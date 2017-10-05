---
title: Come usare l'invio in batch per migliorare le prestazioni delle applicazioni di database SQL di Azure
description: "Questo argomento dimostra che le operazioni di database in batch migliorano significativamente la velocità e la scalabilità delle applicazioni di database SQL di Azure. Anche se le tecniche di invio in batch funzionano con qualsiasi database SQL, questo articolo è incentrato su Azure."
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
ms.openlocfilehash: 22cff47444306e599325ba3035d83a0266d69c72
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-batching-to-improve-sql-database-application-performance"></a><span data-ttu-id="13a80-104">Come usare l'invio in batch per migliorare le prestazioni delle applicazioni di database SQL</span><span class="sxs-lookup"><span data-stu-id="13a80-104">How to use batching to improve SQL Database application performance</span></span>
<span data-ttu-id="13a80-105">Le operazioni di invio in batch al database SQL di Azure migliorano in modo significativo le prestazioni e la scalabilità delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="13a80-105">Batching operations to Azure SQL Database significantly improves the performance and scalability of your applications.</span></span> <span data-ttu-id="13a80-106">Per comprendere i vantaggi, la prima parte di questo articolo descrive alcuni risultati dei test di esempio che confrontano le richieste sequenziali e in batch inviate a un database SQL.</span><span class="sxs-lookup"><span data-stu-id="13a80-106">In order to understand the benefits, the first part of this article covers some sample test results that compare sequential and batched requests to a SQL Database.</span></span> <span data-ttu-id="13a80-107">Il resto dell'articolo illustra le tecniche, gli scenari e le considerazioni che facilitano l'uso corretto dell'invio in batch nelle applicazioni Azure.</span><span class="sxs-lookup"><span data-stu-id="13a80-107">The remainder of the article shows the techniques, scenarios, and considerations to help you to use batching successfully in your Azure applications.</span></span>

## <a name="why-is-batching-important-for-sql-database"></a><span data-ttu-id="13a80-108">Perché l'invio in batch è importante per il database SQL?</span><span class="sxs-lookup"><span data-stu-id="13a80-108">Why is batching important for SQL Database?</span></span>
<span data-ttu-id="13a80-109">L'invio in batch di chiamate a un servizio remoto è una strategia nota per migliorare le prestazioni e la scalabilità.</span><span class="sxs-lookup"><span data-stu-id="13a80-109">Batching calls to a remote service is a well-known strategy for increasing performance and scalability.</span></span> <span data-ttu-id="13a80-110">Ogni interazione con un servizio remoto, ad esempio la serializzazione, il trasferimento in rete e la deserializzazione, comporta costi fissi di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="13a80-110">There are fixed processing costs to any interactions with a remote service, such as serialization, network transfer, and deserialization.</span></span> <span data-ttu-id="13a80-111">Il raggruppamento di più transazioni distinte in un singolo batch consente di ridurre al minimo questi costi.</span><span class="sxs-lookup"><span data-stu-id="13a80-111">Packaging many separate transactions into a single batch minimizes these costs.</span></span>

<span data-ttu-id="13a80-112">In questo articolo si esamineranno diversi scenari e strategie di invio in batch al database SQL.</span><span class="sxs-lookup"><span data-stu-id="13a80-112">In this paper, we want to examine various SQL Database batching strategies and scenarios.</span></span> <span data-ttu-id="13a80-113">Queste strategie sono importanti anche per le applicazioni locali che usano SQL Server, tuttavia ci sono diversi motivi per evidenziare l'uso dell'invio in batch per il database SQL:</span><span class="sxs-lookup"><span data-stu-id="13a80-113">Although these strategies are also important for on-premises applications that use SQL Server, there are several reasons for highlighting the use of batching for SQL Database:</span></span>

* <span data-ttu-id="13a80-114">La latenza di rete per l'accesso al database SQL è potenzialmente maggiore, in particolare se si accede dall'esterno dello stesso data center di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="13a80-114">There is potentially greater network latency in accessing SQL Database, especially if you are accessing SQL Database from outside the same Microsoft Azure datacenter.</span></span>
* <span data-ttu-id="13a80-115">Le caratteristiche multi-tenant del database SQL indicano che l'efficienza del livello di accesso ai dati è correlata alla scalabilità generale del database.</span><span class="sxs-lookup"><span data-stu-id="13a80-115">The multitenant characteristics of SQL Database means that the efficiency of the data access layer correlates to the overall scalability of the database.</span></span> <span data-ttu-id="13a80-116">Il database SQL deve impedire che qualsiasi tenant/utente singolo monopolizzi le risorse del database a scapito di altri tenant.</span><span class="sxs-lookup"><span data-stu-id="13a80-116">SQL Database must prevent any single tenant/user from monopolizing database resources to the detriment of other tenants.</span></span> <span data-ttu-id="13a80-117">In risposta all'utilizzo eccessivo di quote predefinite, il database SQL può ridurre la velocità effettiva o rispondere con eccezioni di limitazione delle richieste.</span><span class="sxs-lookup"><span data-stu-id="13a80-117">In response to usage in excess of predefined quotas, SQL Database can reduce throughput or respond with throttling exceptions.</span></span> <span data-ttu-id="13a80-118">Strategie efficienti, come l'invio in batch, consentono di effettuare un maggior numero di operazioni sul database SQL prima di raggiungere questi limiti.</span><span class="sxs-lookup"><span data-stu-id="13a80-118">Efficiencies, such as batching, enable you to do more work on SQL Database before reaching these limits.</span></span> 
* <span data-ttu-id="13a80-119">L'invio in batch è efficace anche per le architetture che usano più database (partizionamento orizzontale).</span><span class="sxs-lookup"><span data-stu-id="13a80-119">Batching is also effective for architectures that use multiple databases (sharding).</span></span> <span data-ttu-id="13a80-120">L'efficienza dell'interazione con ogni unità database rimane comunque un fattore chiave ai fini della scalabilità generale.</span><span class="sxs-lookup"><span data-stu-id="13a80-120">The efficiency of your interaction with each database unit is still a key factor in your overall scalability.</span></span> 

<span data-ttu-id="13a80-121">Uno dei vantaggi che derivano dall'uso del database SQL consiste nel non dover gestire i server che ospitano il database.</span><span class="sxs-lookup"><span data-stu-id="13a80-121">One of the benefits of using SQL Database is that you don’t have to manage the servers that host the database.</span></span> <span data-ttu-id="13a80-122">Tuttavia, questa infrastruttura gestita implica anche una diversa concezione delle ottimizzazioni del database.</span><span class="sxs-lookup"><span data-stu-id="13a80-122">However, this managed infrastructure also means that you have to think differently about database optimizations.</span></span> <span data-ttu-id="13a80-123">Non è più possibile migliorare l'hardware o l'infrastruttura di rete del database.</span><span class="sxs-lookup"><span data-stu-id="13a80-123">You can no longer look to improve the database hardware or network infrastructure.</span></span> <span data-ttu-id="13a80-124">Gli ambienti sono controllati da Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="13a80-124">Microsoft Azure controls those environments.</span></span> <span data-ttu-id="13a80-125">L'area principale su cui è possibile esercitare un controllo è la modalità di interazione dell'applicazione con il database SQL.</span><span class="sxs-lookup"><span data-stu-id="13a80-125">The main area that you can control is how your application interacts with SQL Database.</span></span> <span data-ttu-id="13a80-126">L'invio in batch è una di queste ottimizzazioni.</span><span class="sxs-lookup"><span data-stu-id="13a80-126">Batching is one of these optimizations.</span></span> 

<span data-ttu-id="13a80-127">La prima parte del documento esamina le diverse tecniche di invio in batch per le applicazioni .NET che usano il database SQL.</span><span class="sxs-lookup"><span data-stu-id="13a80-127">The first part of the paper examines various batching techniques for .NET applications that use SQL Database.</span></span> <span data-ttu-id="13a80-128">Le ultime due sezioni illustrano invece le linee guida e gli scenari di invio in batch.</span><span class="sxs-lookup"><span data-stu-id="13a80-128">The last two sections cover batching guidelines and scenarios.</span></span>

## <a name="batching-strategies"></a><span data-ttu-id="13a80-129">Strategie di invio in batch</span><span class="sxs-lookup"><span data-stu-id="13a80-129">Batching strategies</span></span>
### <a name="note-about-timing-results-in-this-topic"></a><span data-ttu-id="13a80-130">Nota sui risultati della tempistica in questo argomento</span><span class="sxs-lookup"><span data-stu-id="13a80-130">Note about timing results in this topic</span></span>
> [!NOTE]
> <span data-ttu-id="13a80-131">I risultati non sono benchmark ma servono per indicare le **prestazioni relative**.</span><span class="sxs-lookup"><span data-stu-id="13a80-131">Results are not benchmarks but are meant to show **relative performance**.</span></span> <span data-ttu-id="13a80-132">Le tempistiche si basano su una media di almeno 10 esecuzioni del test.</span><span class="sxs-lookup"><span data-stu-id="13a80-132">Timings are based on an average of at least 10 test runs.</span></span> <span data-ttu-id="13a80-133">Le operazioni sono inserimenti in una tabella vuota.</span><span class="sxs-lookup"><span data-stu-id="13a80-133">Operations are inserts into an empty table.</span></span> <span data-ttu-id="13a80-134">Questi test sono stati misurati con un database antecedente a V12 e non corrispondono necessariamente alla velocità effettiva che si potrebbe ottenere in un database V12 usando i nuovi [livelli di servizio](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="13a80-134">These tests were measured pre-V12, and they do not necessarily correspond to throughput that you might experience in a V12 database using the new [service tiers](sql-database-service-tiers.md).</span></span> <span data-ttu-id="13a80-135">Il vantaggio relativo della tecnica di invio in batch dovrebbe essere simile.</span><span class="sxs-lookup"><span data-stu-id="13a80-135">The relative benefit of the batching technique should be similar.</span></span>
> 
> 

### <a name="transactions"></a><span data-ttu-id="13a80-136">Transazioni</span><span class="sxs-lookup"><span data-stu-id="13a80-136">Transactions</span></span>
<span data-ttu-id="13a80-137">Può apparire inconsueto che si inizi un'analisi dell'invio in batch parlando di transazioni.</span><span class="sxs-lookup"><span data-stu-id="13a80-137">It seems strange to begin a review of batching by discussing transactions.</span></span> <span data-ttu-id="13a80-138">Tuttavia, l'uso delle transazioni sul lato client ha un sottile effetto sull'invio in batch sul lato server che migliora le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="13a80-138">But the use of client-side transactions has a subtle server-side batching effect that improves performance.</span></span> <span data-ttu-id="13a80-139">Inoltre, le transazioni possono essere aggiunte con poche righe di codice, quindi sono un modo rapido per migliorare le prestazioni delle operazioni sequenziali.</span><span class="sxs-lookup"><span data-stu-id="13a80-139">And transactions can be added with only a few lines of code, so they provide a fast way to improve performance of sequential operations.</span></span>

<span data-ttu-id="13a80-140">Si consideri il codice C# seguente che contiene una sequenza di operazioni di inserimento e aggiornamento in una semplice tabella.</span><span class="sxs-lookup"><span data-stu-id="13a80-140">Consider the following C# code that contains a sequence of insert and update operations on a simple table.</span></span>

    List<string> dbOperations = new List<string>();
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 1");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 2");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 3");
    dbOperations.Add("insert MyTable values ('new value',1)");
    dbOperations.Add("insert MyTable values ('new value',2)");
    dbOperations.Add("insert MyTable values ('new value',3)");

<span data-ttu-id="13a80-141">Il codice ADO.NET seguente esegue queste operazioni in sequenza.</span><span class="sxs-lookup"><span data-stu-id="13a80-141">The following ADO.NET code sequentially performs these operations.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();

        foreach(string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn);
            cmd.ExecuteNonQuery();                   
        }
    }

<span data-ttu-id="13a80-142">Il modo migliore per ottimizzare il codice consiste nell'implementare una qualche forma di invio in batch di queste chiamate sul lato client.</span><span class="sxs-lookup"><span data-stu-id="13a80-142">The best way to optimize this code is to implement some form of client-side batching of these calls.</span></span> <span data-ttu-id="13a80-143">Esiste tuttavia un modo semplice per migliorare le prestazioni del codice, eseguendo semplicemente il wrapping della sequenza di chiamate in una transazione.</span><span class="sxs-lookup"><span data-stu-id="13a80-143">But there is a simple way to increase the performance of this code by simply wrapping the sequence of calls in a transaction.</span></span> <span data-ttu-id="13a80-144">Ecco lo stesso codice che usa una transazione.</span><span class="sxs-lookup"><span data-stu-id="13a80-144">Here is the same code that uses a transaction.</span></span>

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

<span data-ttu-id="13a80-145">Le transazioni vengono in effetti usate in entrambi questi esempi.</span><span class="sxs-lookup"><span data-stu-id="13a80-145">Transactions are actually being used in both of these examples.</span></span> <span data-ttu-id="13a80-146">Nel primo ogni singola chiamata rappresenta una transazione implicita.</span><span class="sxs-lookup"><span data-stu-id="13a80-146">In the first example, each individual call is an implicit transaction.</span></span> <span data-ttu-id="13a80-147">Nel secondo esempio viene eseguito il wrapping di tutte le chiamate in una transazione esplicita.</span><span class="sxs-lookup"><span data-stu-id="13a80-147">In the second example, an explicit transaction wraps all of the calls.</span></span> <span data-ttu-id="13a80-148">Secondo la documentazione relativa al [log delle transazioni write-ahead](https://msdn.microsoft.com/library/ms186259.aspx), i record del log vengono scaricati su disco al momento del commit della transazione.</span><span class="sxs-lookup"><span data-stu-id="13a80-148">Per the documentation for the [write-ahead transaction log](https://msdn.microsoft.com/library/ms186259.aspx), log records are flushed to the disk when the transaction commits.</span></span> <span data-ttu-id="13a80-149">Si conseguenza, se si includono più chiamate in una transazione, la scrittura nel log delle transazioni può essere ritardata finché non viene eseguito il commit della transazione stessa.</span><span class="sxs-lookup"><span data-stu-id="13a80-149">So by including more calls in a transaction, the write to the transaction log can delay until the transaction is committed.</span></span> <span data-ttu-id="13a80-150">In effetti, si abilita l'invio in batch per le operazioni di scrittura nel log delle transazioni del server.</span><span class="sxs-lookup"><span data-stu-id="13a80-150">In effect, you are enabling batching for the writes to the server’s transaction log.</span></span>

<span data-ttu-id="13a80-151">La tabella seguente illustra alcuni risultati di test ad hoc.</span><span class="sxs-lookup"><span data-stu-id="13a80-151">The following table shows some ad-hoc testing results.</span></span> <span data-ttu-id="13a80-152">I test eseguono le medesime operazioni sequenziali di inserimento con e senza transazioni.</span><span class="sxs-lookup"><span data-stu-id="13a80-152">The tests performed the same sequential inserts with and without transactions.</span></span> <span data-ttu-id="13a80-153">Per maggiore chiarezza, il primo set di test è stato eseguito in remoto da un portatile al database in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="13a80-153">For more perspective, the first set of tests ran remotely from a laptop to the database in Microsoft Azure.</span></span> <span data-ttu-id="13a80-154">Il secondo set di test è stato eseguito da un servizio cloud e un database entrambi residenti nello stesso data center di Microsoft Azure (Stati Uniti occidentali).</span><span class="sxs-lookup"><span data-stu-id="13a80-154">The second set of tests ran from a cloud service and database that both resided within the same Microsoft Azure datacenter (West US).</span></span> <span data-ttu-id="13a80-155">La tabella seguente mostra la durata in millisecondi delle operazioni di inserimento sequenziali con e senza transazioni.</span><span class="sxs-lookup"><span data-stu-id="13a80-155">The following table shows the duration in milliseconds of sequential inserts with and without transactions.</span></span>

<span data-ttu-id="13a80-156">**Da ambiente locale ad Azure**</span><span class="sxs-lookup"><span data-stu-id="13a80-156">**On-Premises to Azure**:</span></span>

| <span data-ttu-id="13a80-157">Operazioni</span><span class="sxs-lookup"><span data-stu-id="13a80-157">Operations</span></span> | <span data-ttu-id="13a80-158">Senza transazione (ms)</span><span class="sxs-lookup"><span data-stu-id="13a80-158">No Transaction (ms)</span></span> | <span data-ttu-id="13a80-159">Con transazione (ms)</span><span class="sxs-lookup"><span data-stu-id="13a80-159">Transaction (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="13a80-160">1</span><span class="sxs-lookup"><span data-stu-id="13a80-160">1</span></span> |<span data-ttu-id="13a80-161">130</span><span class="sxs-lookup"><span data-stu-id="13a80-161">130</span></span> |<span data-ttu-id="13a80-162">402</span><span class="sxs-lookup"><span data-stu-id="13a80-162">402</span></span> |
| <span data-ttu-id="13a80-163">10</span><span class="sxs-lookup"><span data-stu-id="13a80-163">10</span></span> |<span data-ttu-id="13a80-164">1208</span><span class="sxs-lookup"><span data-stu-id="13a80-164">1208</span></span> |<span data-ttu-id="13a80-165">1226</span><span class="sxs-lookup"><span data-stu-id="13a80-165">1226</span></span> |
| <span data-ttu-id="13a80-166">100</span><span class="sxs-lookup"><span data-stu-id="13a80-166">100</span></span> |<span data-ttu-id="13a80-167">12662</span><span class="sxs-lookup"><span data-stu-id="13a80-167">12662</span></span> |<span data-ttu-id="13a80-168">10395</span><span class="sxs-lookup"><span data-stu-id="13a80-168">10395</span></span> |
| <span data-ttu-id="13a80-169">1000</span><span class="sxs-lookup"><span data-stu-id="13a80-169">1000</span></span> |<span data-ttu-id="13a80-170">128852</span><span class="sxs-lookup"><span data-stu-id="13a80-170">128852</span></span> |<span data-ttu-id="13a80-171">102917</span><span class="sxs-lookup"><span data-stu-id="13a80-171">102917</span></span> |

<span data-ttu-id="13a80-172">**Da Azure ad Azure (stesso data center)**:</span><span class="sxs-lookup"><span data-stu-id="13a80-172">**Azure to Azure (same datacenter)**:</span></span>

| <span data-ttu-id="13a80-173">Operazioni</span><span class="sxs-lookup"><span data-stu-id="13a80-173">Operations</span></span> | <span data-ttu-id="13a80-174">Senza transazione (ms)</span><span class="sxs-lookup"><span data-stu-id="13a80-174">No Transaction (ms)</span></span> | <span data-ttu-id="13a80-175">Con transazione (ms)</span><span class="sxs-lookup"><span data-stu-id="13a80-175">Transaction (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="13a80-176">1</span><span class="sxs-lookup"><span data-stu-id="13a80-176">1</span></span> |<span data-ttu-id="13a80-177">21</span><span class="sxs-lookup"><span data-stu-id="13a80-177">21</span></span> |<span data-ttu-id="13a80-178">26</span><span class="sxs-lookup"><span data-stu-id="13a80-178">26</span></span> |
| <span data-ttu-id="13a80-179">10</span><span class="sxs-lookup"><span data-stu-id="13a80-179">10</span></span> |<span data-ttu-id="13a80-180">220</span><span class="sxs-lookup"><span data-stu-id="13a80-180">220</span></span> |<span data-ttu-id="13a80-181">56</span><span class="sxs-lookup"><span data-stu-id="13a80-181">56</span></span> |
| <span data-ttu-id="13a80-182">100</span><span class="sxs-lookup"><span data-stu-id="13a80-182">100</span></span> |<span data-ttu-id="13a80-183">2145</span><span class="sxs-lookup"><span data-stu-id="13a80-183">2145</span></span> |<span data-ttu-id="13a80-184">341</span><span class="sxs-lookup"><span data-stu-id="13a80-184">341</span></span> |
| <span data-ttu-id="13a80-185">1000</span><span class="sxs-lookup"><span data-stu-id="13a80-185">1000</span></span> |<span data-ttu-id="13a80-186">21479</span><span class="sxs-lookup"><span data-stu-id="13a80-186">21479</span></span> |<span data-ttu-id="13a80-187">2756</span><span class="sxs-lookup"><span data-stu-id="13a80-187">2756</span></span> |

> [!NOTE]
> <span data-ttu-id="13a80-188">I risultati non sono benchmark.</span><span class="sxs-lookup"><span data-stu-id="13a80-188">Results are not benchmarks.</span></span> <span data-ttu-id="13a80-189">Vedere la [nota sui risultati della tempistica in questo argomento](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="13a80-189">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="13a80-190">In base ai risultati di test precedenti, il wrapping di una singola operazione in una transazione riduce in effetti le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="13a80-190">Based on the previous test results, wrapping a single operation in a transaction actually decreases performance.</span></span> <span data-ttu-id="13a80-191">Tuttavia, maggiore è il numero di operazioni in una singola transazione, più evidente risulta il miglioramento delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="13a80-191">But as you increase the number of operations within a single transaction, the performance improvement becomes more marked.</span></span> <span data-ttu-id="13a80-192">La differenza nelle prestazioni è anche più significativa se tutte le operazioni vengono eseguite nello stesso data center di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="13a80-192">The performance difference is also more noticeable when all operations occur within the Microsoft Azure datacenter.</span></span> <span data-ttu-id="13a80-193">La maggiore latenza dovuta all'uso del database SQL dall'esterno del data center di Microsoft Azure vanifica il vantaggio in termini di prestazioni derivante dall'uso delle transazioni.</span><span class="sxs-lookup"><span data-stu-id="13a80-193">The increased latency of using SQL Database from outside the Microsoft Azure datacenter overshadows the performance gain of using transactions.</span></span>

<span data-ttu-id="13a80-194">Anche se l'uso delle transazioni può migliorare le prestazioni, continuare a [osservare le procedure consigliate per transazioni e connessioni](https://msdn.microsoft.com/library/ms187484.aspx).</span><span class="sxs-lookup"><span data-stu-id="13a80-194">Although the use of transactions can increase performance, continue to [observe best practices for transactions and connections](https://msdn.microsoft.com/library/ms187484.aspx).</span></span> <span data-ttu-id="13a80-195">Usare transazioni più brevi possibile e chiudere la connessione al database al termine delle operazioni.</span><span class="sxs-lookup"><span data-stu-id="13a80-195">Keep the transaction as short as possible, and close the database connection after the work completes.</span></span> <span data-ttu-id="13a80-196">L'istruzione using nell'esempio precedente assicura la chiusura della connessione al termine del blocco di codice successivo.</span><span class="sxs-lookup"><span data-stu-id="13a80-196">The using statement in the previous example assures that the connection is closed when the subsequent code block completes.</span></span>

<span data-ttu-id="13a80-197">L'esempio precedente illustra che è possibile aggiungere una transazione locale al codice ADO.NET con due righe.</span><span class="sxs-lookup"><span data-stu-id="13a80-197">The previous example demonstrates that you can add a local transaction to any ADO.NET code with two lines.</span></span> <span data-ttu-id="13a80-198">Le transazioni rappresentano un modo rapido per migliorare le prestazioni del codice usato per le operazioni sequenziali di inserimento, aggiornamento ed eliminazione.</span><span class="sxs-lookup"><span data-stu-id="13a80-198">Transactions offer a quick way to improve the performance of code that makes sequential insert, update, and delete operations.</span></span> <span data-ttu-id="13a80-199">Per prestazioni ottimali, provare tuttavia a modificare ulteriormente il codice per sfruttare l'invio in batch sul lato client, ad esempio i parametri con valori di tabella.</span><span class="sxs-lookup"><span data-stu-id="13a80-199">However, for the fastest performance, consider changing the code further to take advantage of client-side batching, such as table-valued parameters.</span></span>

<span data-ttu-id="13a80-200">Per altre informazioni sulle transazioni in ADO.NET, vedere [Transazioni locali in ADO.NET](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).</span><span class="sxs-lookup"><span data-stu-id="13a80-200">For more information about transactions in ADO.NET, see [Local Transactions in ADO.NET](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).</span></span>

### <a name="table-valued-parameters"></a><span data-ttu-id="13a80-201">Parametri con valori di tabella</span><span class="sxs-lookup"><span data-stu-id="13a80-201">Table-valued parameters</span></span>
<span data-ttu-id="13a80-202">I parametri con valori di tabella supportano tipi di tabella definiti dall'utente come parametri nelle funzioni, nelle stored procedure e nelle istruzioni Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="13a80-202">Table-valued parameters support user-defined table types as parameters in Transact-SQL statements, stored procedures, and functions.</span></span> <span data-ttu-id="13a80-203">Questa tecnica di invio in batch sul lato client consente di inviare più righe di dati nel parametro con valori di tabella.</span><span class="sxs-lookup"><span data-stu-id="13a80-203">This client-side batching technique allows you to send multiple rows of data within the table-valued parameter.</span></span> <span data-ttu-id="13a80-204">Per usare parametri con valori di tabella, definire prima di tutto un tipo di tabella.</span><span class="sxs-lookup"><span data-stu-id="13a80-204">To use table-valued parameters, first define a table type.</span></span> <span data-ttu-id="13a80-205">L'istruzione Transact-SQL seguente crea un tipo di tabella denominato **MyTableType**.</span><span class="sxs-lookup"><span data-stu-id="13a80-205">The following Transact-SQL statement creates a table type named **MyTableType**.</span></span>

    CREATE TYPE MyTableType AS TABLE 
    ( mytext TEXT,
      num INT );


<span data-ttu-id="13a80-206">Nel codice si crea un oggetto **DataTable** con gli stessi nomi e tipi del tipo di tabella.</span><span class="sxs-lookup"><span data-stu-id="13a80-206">In code, you create a **DataTable** with the exact same names and types of the table type.</span></span> <span data-ttu-id="13a80-207">Passare l'oggetto **DataTable** in un parametro in una chiamata di stored procedure o query di testo.</span><span class="sxs-lookup"><span data-stu-id="13a80-207">Pass this **DataTable** in a parameter in a text query or stored procedure call.</span></span> <span data-ttu-id="13a80-208">Questa tecnica è illustrata nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="13a80-208">The following example shows this technique:</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        DataTable table = new DataTable();
        // Add columns and rows. The following is a simple example.
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

<span data-ttu-id="13a80-209">Nell'esempio precedente l'oggetto **SqlCommand** inserisce righe da un parametro con valori di tabella, **@TestTvp**.</span><span class="sxs-lookup"><span data-stu-id="13a80-209">In the previous example, the **SqlCommand** object inserts rows from a table-valued parameter, **@TestTvp**.</span></span> <span data-ttu-id="13a80-210">L'oggetto **DataTable** creato in precedenza viene assegnato a questo parametro con il metodo **SqlCommand.Parameters.Add**.</span><span class="sxs-lookup"><span data-stu-id="13a80-210">The previously created **DataTable** object is assigned to this parameter with the **SqlCommand.Parameters.Add** method.</span></span> <span data-ttu-id="13a80-211">L'invio in batch delle operazioni di inserimento in una singola chiamata migliora sensibilmente le prestazioni rispetto alle operazioni di inserimento sequenziali.</span><span class="sxs-lookup"><span data-stu-id="13a80-211">Batching the inserts in one call significantly increases the performance over sequential inserts.</span></span>

<span data-ttu-id="13a80-212">Per migliorare ulteriormente l'esempio precedente, usare una stored procedure anziché un comando basato su testo.</span><span class="sxs-lookup"><span data-stu-id="13a80-212">To improve the previous example further, use a stored procedure instead of a text-based command.</span></span> <span data-ttu-id="13a80-213">Il comando Transact-SQL seguente crea una stored procedure che accetta il parametro con valori di tabella **SimpleTestTableType** .</span><span class="sxs-lookup"><span data-stu-id="13a80-213">The following Transact-SQL command creates a stored procedure that takes the **SimpleTestTableType** table-valued parameter.</span></span>

    CREATE PROCEDURE [dbo].[sp_InsertRows] 
    @TestTvp as MyTableType READONLY
    AS
    BEGIN
    INSERT INTO MyTable(mytext, num) 
    SELECT mytext, num FROM @TestTvp
    END
    GO

<span data-ttu-id="13a80-214">Modificare quindi la dichiarazione dell'oggetto **SqlCommand** nell'esempio di codice precedente come segue.</span><span class="sxs-lookup"><span data-stu-id="13a80-214">Then change the **SqlCommand** object declaration in the previous code example to the following.</span></span>

    SqlCommand cmd = new SqlCommand("sp_InsertRows", connection);
    cmd.CommandType = CommandType.StoredProcedure;

<span data-ttu-id="13a80-215">Nella maggior parte dei casi i parametri con valori di tabella hanno prestazioni equivalenti o superiori rispetto ad altre tecniche di invio in batch.</span><span class="sxs-lookup"><span data-stu-id="13a80-215">In most cases, table-valued parameters have equivalent or better performance than other batching techniques.</span></span> <span data-ttu-id="13a80-216">I parametri con valori di tabella sono spesso preferibili perché più flessibili di altre opzioni.</span><span class="sxs-lookup"><span data-stu-id="13a80-216">Table-valued parameters are often preferable, because they are more flexible than other options.</span></span> <span data-ttu-id="13a80-217">Ad esempio, altre tecniche come la copia bulk di SQL consentono solo l'inserimento di nuove righe.</span><span class="sxs-lookup"><span data-stu-id="13a80-217">For example, other techniques, such as SQL bulk copy, only permit the insertion of new rows.</span></span> <span data-ttu-id="13a80-218">Con i parametri con valori di tabella è invece possibile usare la logica della stored procedure per determinare le righe da aggiornare e quelle da inserire.</span><span class="sxs-lookup"><span data-stu-id="13a80-218">But with table-valued parameters, you can use logic in the stored procedure to determine which rows are updates and which are inserts.</span></span> <span data-ttu-id="13a80-219">È anche possibile modificare il tipo di tabella perché contenga la colonna "Operation" che indica se la riga specificata deve essere inserita, aggiornata o eliminata.</span><span class="sxs-lookup"><span data-stu-id="13a80-219">The table type can also be modified to contain an “Operation” column that indicates whether the specified row should be inserted, updated, or deleted.</span></span>

<span data-ttu-id="13a80-220">La tabella seguente illustra i risultati, in millisecondi, dei test ad hoc per l'uso di parametri con valori di tabella.</span><span class="sxs-lookup"><span data-stu-id="13a80-220">The following table shows ad-hoc test results for the use of table-valued parameters in milliseconds.</span></span>

| <span data-ttu-id="13a80-221">Operazioni</span><span class="sxs-lookup"><span data-stu-id="13a80-221">Operations</span></span> | <span data-ttu-id="13a80-222">Da ambiente locale ad Azure (ms)</span><span class="sxs-lookup"><span data-stu-id="13a80-222">On-Premises to Azure (ms)</span></span> | <span data-ttu-id="13a80-223">Azure stesso data center (ms)</span><span class="sxs-lookup"><span data-stu-id="13a80-223">Azure same datacenter (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="13a80-224">1</span><span class="sxs-lookup"><span data-stu-id="13a80-224">1</span></span> |<span data-ttu-id="13a80-225">124</span><span class="sxs-lookup"><span data-stu-id="13a80-225">124</span></span> |<span data-ttu-id="13a80-226">32</span><span class="sxs-lookup"><span data-stu-id="13a80-226">32</span></span> |
| <span data-ttu-id="13a80-227">10</span><span class="sxs-lookup"><span data-stu-id="13a80-227">10</span></span> |<span data-ttu-id="13a80-228">131</span><span class="sxs-lookup"><span data-stu-id="13a80-228">131</span></span> |<span data-ttu-id="13a80-229">25</span><span class="sxs-lookup"><span data-stu-id="13a80-229">25</span></span> |
| <span data-ttu-id="13a80-230">100</span><span class="sxs-lookup"><span data-stu-id="13a80-230">100</span></span> |<span data-ttu-id="13a80-231">338</span><span class="sxs-lookup"><span data-stu-id="13a80-231">338</span></span> |<span data-ttu-id="13a80-232">51</span><span class="sxs-lookup"><span data-stu-id="13a80-232">51</span></span> |
| <span data-ttu-id="13a80-233">1000</span><span class="sxs-lookup"><span data-stu-id="13a80-233">1000</span></span> |<span data-ttu-id="13a80-234">2615</span><span class="sxs-lookup"><span data-stu-id="13a80-234">2615</span></span> |<span data-ttu-id="13a80-235">382</span><span class="sxs-lookup"><span data-stu-id="13a80-235">382</span></span> |
| <span data-ttu-id="13a80-236">10000</span><span class="sxs-lookup"><span data-stu-id="13a80-236">10000</span></span> |<span data-ttu-id="13a80-237">23830</span><span class="sxs-lookup"><span data-stu-id="13a80-237">23830</span></span> |<span data-ttu-id="13a80-238">3586</span><span class="sxs-lookup"><span data-stu-id="13a80-238">3586</span></span> |

> [!NOTE]
> <span data-ttu-id="13a80-239">I risultati non sono benchmark.</span><span class="sxs-lookup"><span data-stu-id="13a80-239">Results are not benchmarks.</span></span> <span data-ttu-id="13a80-240">Vedere la [nota sui risultati della tempistica in questo argomento](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="13a80-240">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="13a80-241">Il miglioramento delle prestazioni che deriva dall'invio in batch è evidente.</span><span class="sxs-lookup"><span data-stu-id="13a80-241">The performance gain from batching is immediately apparent.</span></span> <span data-ttu-id="13a80-242">Nel test sequenziale precedente 1000 operazioni hanno richiesto 129 secondi all'esterno del data center e 21 secondi all'interno del data center.</span><span class="sxs-lookup"><span data-stu-id="13a80-242">In the previous sequential test, 1000 operations took 129 seconds outside the datacenter and 21 seconds from within the datacenter.</span></span> <span data-ttu-id="13a80-243">Con i parametri con valori di tabella 1000 operazioni richiedono invece solo 2,6 secondi all'esterno del data center e 0,4 secondi all'interno.</span><span class="sxs-lookup"><span data-stu-id="13a80-243">But with table-valued parameters, 1000 operations take only 2.6 seconds outside the datacenter and 0.4 seconds within the datacenter.</span></span>

<span data-ttu-id="13a80-244">Per altre informazioni sui parametri con valori di tabella, vedere [Usare parametri con valori di tabella (motore di database)](https://msdn.microsoft.com/library/bb510489.aspx).</span><span class="sxs-lookup"><span data-stu-id="13a80-244">For more information on table-valued parameters, see [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span></span>

### <a name="sql-bulk-copy"></a><span data-ttu-id="13a80-245">Copia bulk di SQL</span><span class="sxs-lookup"><span data-stu-id="13a80-245">SQL bulk copy</span></span>
<span data-ttu-id="13a80-246">La copia bulk di SQL è un altro modo per inserire una grande quantità di dati in un database di destinazione.</span><span class="sxs-lookup"><span data-stu-id="13a80-246">SQL bulk copy is another way to insert large amounts of data into a target database.</span></span> <span data-ttu-id="13a80-247">Le applicazioni .NET possono usare la classe **SqlBulkCopy** per eseguire le operazioni di inserimento bulk.</span><span class="sxs-lookup"><span data-stu-id="13a80-247">.NET applications can use the **SqlBulkCopy** class to perform bulk insert operations.</span></span> <span data-ttu-id="13a80-248">In termini di funzionamento, la classe **SqlBulkCopy** è analoga allo strumento da riga di comando **Bcp.exe** o all'istruzione Transact-SQL **BULK INSERT**.</span><span class="sxs-lookup"><span data-stu-id="13a80-248">**SqlBulkCopy** is similar in function to the command-line tool, **Bcp.exe**, or the Transact-SQL statement, **BULK INSERT**.</span></span> <span data-ttu-id="13a80-249">L'esempio di codice seguente illustra come eseguire la copia bulk delle righe nella tabella di origine **DataTable**alla tabella di destinazione MyTable in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="13a80-249">The following code example shows how to bulk copy the rows in the source **DataTable**, table, to the destination table in SQL Server, MyTable.</span></span>

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

<span data-ttu-id="13a80-250">In alcuni casi la copia bulk è preferibile rispetto ai parametri con valori di tabella.</span><span class="sxs-lookup"><span data-stu-id="13a80-250">There are some cases where bulk copy is preferred over table-valued parameters.</span></span> <span data-ttu-id="13a80-251">Vedere la tabella di confronto dei parametri con valori di tabella rispetto alle operazioni BULK INSERT nell'argomento [Parametri con valori di tabella (motore di database)](https://msdn.microsoft.com/library/bb510489.aspx).</span><span class="sxs-lookup"><span data-stu-id="13a80-251">See the comparison table of Table-Valued parameters versus BULK INSERT operations in the topic [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span></span>

<span data-ttu-id="13a80-252">I risultati dei test ad hoc seguenti mostrano le prestazioni, in millisecondi, dell'invio in batch con **SqlBulkCopy** .</span><span class="sxs-lookup"><span data-stu-id="13a80-252">The following ad-hoc test results show the performance of batching with **SqlBulkCopy** in milliseconds.</span></span>

| <span data-ttu-id="13a80-253">Operazioni</span><span class="sxs-lookup"><span data-stu-id="13a80-253">Operations</span></span> | <span data-ttu-id="13a80-254">Da ambiente locale ad Azure (ms)</span><span class="sxs-lookup"><span data-stu-id="13a80-254">On-Premises to Azure (ms)</span></span> | <span data-ttu-id="13a80-255">Azure stesso data center (ms)</span><span class="sxs-lookup"><span data-stu-id="13a80-255">Azure same datacenter (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="13a80-256">1</span><span class="sxs-lookup"><span data-stu-id="13a80-256">1</span></span> |<span data-ttu-id="13a80-257">433</span><span class="sxs-lookup"><span data-stu-id="13a80-257">433</span></span> |<span data-ttu-id="13a80-258">57</span><span class="sxs-lookup"><span data-stu-id="13a80-258">57</span></span> |
| <span data-ttu-id="13a80-259">10</span><span class="sxs-lookup"><span data-stu-id="13a80-259">10</span></span> |<span data-ttu-id="13a80-260">441</span><span class="sxs-lookup"><span data-stu-id="13a80-260">441</span></span> |<span data-ttu-id="13a80-261">32</span><span class="sxs-lookup"><span data-stu-id="13a80-261">32</span></span> |
| <span data-ttu-id="13a80-262">100</span><span class="sxs-lookup"><span data-stu-id="13a80-262">100</span></span> |<span data-ttu-id="13a80-263">636</span><span class="sxs-lookup"><span data-stu-id="13a80-263">636</span></span> |<span data-ttu-id="13a80-264">53</span><span class="sxs-lookup"><span data-stu-id="13a80-264">53</span></span> |
| <span data-ttu-id="13a80-265">1000</span><span class="sxs-lookup"><span data-stu-id="13a80-265">1000</span></span> |<span data-ttu-id="13a80-266">2535</span><span class="sxs-lookup"><span data-stu-id="13a80-266">2535</span></span> |<span data-ttu-id="13a80-267">341</span><span class="sxs-lookup"><span data-stu-id="13a80-267">341</span></span> |
| <span data-ttu-id="13a80-268">10000</span><span class="sxs-lookup"><span data-stu-id="13a80-268">10000</span></span> |<span data-ttu-id="13a80-269">21605</span><span class="sxs-lookup"><span data-stu-id="13a80-269">21605</span></span> |<span data-ttu-id="13a80-270">2737</span><span class="sxs-lookup"><span data-stu-id="13a80-270">2737</span></span> |

> [!NOTE]
> <span data-ttu-id="13a80-271">I risultati non sono benchmark.</span><span class="sxs-lookup"><span data-stu-id="13a80-271">Results are not benchmarks.</span></span> <span data-ttu-id="13a80-272">Vedere la [nota sui risultati della tempistica in questo argomento](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="13a80-272">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="13a80-273">Nei batch di dimensioni inferiori l'uso dei parametri con valori di tabella ha prodotto prestazioni migliori rispetto alla classe **SqlBulkCopy** .</span><span class="sxs-lookup"><span data-stu-id="13a80-273">In smaller batch sizes, the use table-valued parameters outperformed the **SqlBulkCopy** class.</span></span> <span data-ttu-id="13a80-274">Tuttavia, l'esecuzione della classe **SqlBulkCopy** risulta del 12-31% più rapida rispetto ai parametri con valori di tabella per i test di 1.000 e 10.000 righe.</span><span class="sxs-lookup"><span data-stu-id="13a80-274">However, **SqlBulkCopy** performed 12-31% faster than table-valued parameters for the tests of 1,000 and 10,000 rows.</span></span> <span data-ttu-id="13a80-275">Come i parametri con valori di tabella, la classe **SqlBulkCopy** è un'opzione valida per le operazioni di inserimento in batch, in particolare rispetto alle prestazioni di operazioni non in batch.</span><span class="sxs-lookup"><span data-stu-id="13a80-275">Like table-valued parameters, **SqlBulkCopy** is a good option for batched inserts, especially when compared to the performance of non-batched operations.</span></span>

<span data-ttu-id="13a80-276">Per altre informazioni sulla copia bulk in ADO.NET, vedere [Operazioni di copia bulk in SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).</span><span class="sxs-lookup"><span data-stu-id="13a80-276">For more information on bulk copy in ADO.NET, see [Bulk Copy Operations in SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).</span></span>

### <a name="multiple-row-parameterized-insert-statements"></a><span data-ttu-id="13a80-277">Istruzioni INSERT con parametri a più righe</span><span class="sxs-lookup"><span data-stu-id="13a80-277">Multiple-row Parameterized INSERT statements</span></span>
<span data-ttu-id="13a80-278">Un'alternativa per i batch piccoli consiste nella creazione di un'istruzione INSERT con parametri di grandi dimensioni per l'inserimento di più righe.</span><span class="sxs-lookup"><span data-stu-id="13a80-278">One alternative for small batches is to construct a large parameterized INSERT statement that inserts multiple rows.</span></span> <span data-ttu-id="13a80-279">L'esempio di codice seguente illustra questa tecnica.</span><span class="sxs-lookup"><span data-stu-id="13a80-279">The following code example demonstrates this technique.</span></span>

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


<span data-ttu-id="13a80-280">Questo esempio è ideato per illustrare il concetto di base.</span><span class="sxs-lookup"><span data-stu-id="13a80-280">This example is meant to show the basic concept.</span></span> <span data-ttu-id="13a80-281">Uno scenario più realistico prevedrebbe l'esecuzione di un ciclo sulle entità richieste per costruire contemporaneamente la stringa di query e i parametri del comando.</span><span class="sxs-lookup"><span data-stu-id="13a80-281">A more realistic scenario would loop through the required entities to construct the query string and the command parameters simultaneously.</span></span> <span data-ttu-id="13a80-282">Esiste un limite massimo di 2100 parametri di query, il che limita il numero totale di righe elaborabili in questo modo.</span><span class="sxs-lookup"><span data-stu-id="13a80-282">You are limited to a total of 2100 query parameters, so this limits the total number of rows that can be processed in this manner.</span></span>

<span data-ttu-id="13a80-283">I risultati dei test ad hoc seguenti mostrano le prestazioni di questo tipo di istruzione di inserimento, espresse in millisecondi.</span><span class="sxs-lookup"><span data-stu-id="13a80-283">The following ad-hoc test results show the performance of this type of insert statement in milliseconds.</span></span>

| <span data-ttu-id="13a80-284">Operazioni</span><span class="sxs-lookup"><span data-stu-id="13a80-284">Operations</span></span> | <span data-ttu-id="13a80-285">Parametri con valori di tabella (ms)</span><span class="sxs-lookup"><span data-stu-id="13a80-285">Table-valued parameters (ms)</span></span> | <span data-ttu-id="13a80-286">Singola istruzione INSERT (ms)</span><span class="sxs-lookup"><span data-stu-id="13a80-286">Single-statement INSERT (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="13a80-287">1</span><span class="sxs-lookup"><span data-stu-id="13a80-287">1</span></span> |<span data-ttu-id="13a80-288">32</span><span class="sxs-lookup"><span data-stu-id="13a80-288">32</span></span> |<span data-ttu-id="13a80-289">20</span><span class="sxs-lookup"><span data-stu-id="13a80-289">20</span></span> |
| <span data-ttu-id="13a80-290">10</span><span class="sxs-lookup"><span data-stu-id="13a80-290">10</span></span> |<span data-ttu-id="13a80-291">30</span><span class="sxs-lookup"><span data-stu-id="13a80-291">30</span></span> |<span data-ttu-id="13a80-292">25</span><span class="sxs-lookup"><span data-stu-id="13a80-292">25</span></span> |
| <span data-ttu-id="13a80-293">100</span><span class="sxs-lookup"><span data-stu-id="13a80-293">100</span></span> |<span data-ttu-id="13a80-294">33</span><span class="sxs-lookup"><span data-stu-id="13a80-294">33</span></span> |<span data-ttu-id="13a80-295">51</span><span class="sxs-lookup"><span data-stu-id="13a80-295">51</span></span> |

> [!NOTE]
> <span data-ttu-id="13a80-296">I risultati non sono benchmark.</span><span class="sxs-lookup"><span data-stu-id="13a80-296">Results are not benchmarks.</span></span> <span data-ttu-id="13a80-297">Vedere la [nota sui risultati della tempistica in questo argomento](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="13a80-297">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="13a80-298">Questo approccio può essere leggermente più veloce per i batch minori di 100 righe.</span><span class="sxs-lookup"><span data-stu-id="13a80-298">This approach can be slightly faster for batches that are less than 100 rows.</span></span> <span data-ttu-id="13a80-299">Sebbene l'entità del miglioramento sia lieve, questa tecnica rappresenta un'altra opzione che potrebbe rivelarsi utile in scenari di applicazione specifici.</span><span class="sxs-lookup"><span data-stu-id="13a80-299">Although the improvement is small, this technique is another option that might work well in your specific application scenario.</span></span>

### <a name="dataadapter"></a><span data-ttu-id="13a80-300">DataAdapter</span><span class="sxs-lookup"><span data-stu-id="13a80-300">DataAdapter</span></span>
<span data-ttu-id="13a80-301">La classe **DataAdapter** consente di modificare un oggetto **DataSet** e di inviare quindi le modifiche come operazioni di tipo INSERT, UPDATE e DELETE.</span><span class="sxs-lookup"><span data-stu-id="13a80-301">The **DataAdapter** class allows you to modify a **DataSet** object and then submit the changes as INSERT, UPDATE, and DELETE operations.</span></span> <span data-ttu-id="13a80-302">Se si usa **DataAdapter** in questo modo, è importante notare che vengono eseguite chiamate separate per ogni singola operazione.</span><span class="sxs-lookup"><span data-stu-id="13a80-302">If you are using the **DataAdapter** in this manner, it is important to note that separate calls are made for each distinct operation.</span></span> <span data-ttu-id="13a80-303">Per migliorare le prestazioni, usare la proprietà **UpdateBatchSize** impostata sul numero di operazioni da eseguire in batch contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="13a80-303">To improve performance, use the **UpdateBatchSize** property to the number of operations that should be batched at a time.</span></span> <span data-ttu-id="13a80-304">Per altre informazioni, vedere [Esecuzione di operazioni batch usando DataAdapters](https://msdn.microsoft.com/library/aadf8fk2.aspx).</span><span class="sxs-lookup"><span data-stu-id="13a80-304">For more information, see [Performing Batch Operations Using DataAdapters](https://msdn.microsoft.com/library/aadf8fk2.aspx).</span></span>

### <a name="entity-framework"></a><span data-ttu-id="13a80-305">Entity Framework</span><span class="sxs-lookup"><span data-stu-id="13a80-305">Entity framework</span></span>
<span data-ttu-id="13a80-306">Entity Framework non supporta attualmente l'invio in batch.</span><span class="sxs-lookup"><span data-stu-id="13a80-306">Entity Framework does not currently support batching.</span></span> <span data-ttu-id="13a80-307">Diversi sviluppatori della community hanno provato a elaborare soluzioni alternative, ad esempio l'override del metodo **SaveChanges** .</span><span class="sxs-lookup"><span data-stu-id="13a80-307">Different developers in the community have attempted to demonstrate workarounds, such as override the **SaveChanges** method.</span></span> <span data-ttu-id="13a80-308">Tuttavia, le soluzioni sono in genere complesse e personalizzate a seconda dell'applicazione e del modello di dati.</span><span class="sxs-lookup"><span data-stu-id="13a80-308">But the solutions are typically complex and customized to the application and data model.</span></span> <span data-ttu-id="13a80-309">Il progetto codeplex di Entity Framework include attualmente una pagina di discussione sulla richiesta di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="13a80-309">The Entity Framework codeplex project currently has a discussion page on this feature request.</span></span> <span data-ttu-id="13a80-310">Per accedere alla discussione, vedere la pagina [Design Meeting Notes - 2 agosto 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).</span><span class="sxs-lookup"><span data-stu-id="13a80-310">To view this discussion, see [Design Meeting Notes - August 2, 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).</span></span>

### <a name="xml"></a><span data-ttu-id="13a80-311">XML</span><span class="sxs-lookup"><span data-stu-id="13a80-311">XML</span></span>
<span data-ttu-id="13a80-312">Per completezza, è importante considerare l'XML come strategia di invio in batch.</span><span class="sxs-lookup"><span data-stu-id="13a80-312">For completeness, we feel that it is important to talk about XML as a batching strategy.</span></span> <span data-ttu-id="13a80-313">Tuttavia, l'uso di XML non offre vantaggi rispetto ad altri metodi e presenta numerosi svantaggi.</span><span class="sxs-lookup"><span data-stu-id="13a80-313">However, the use of XML has no advantages over other methods and several disadvantages.</span></span> <span data-ttu-id="13a80-314">L'approccio è simile a quello dei parametri con valori di tabella, con la differenza che alla stored procedure viene passato un file o una stringa XML invece di una tabella definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="13a80-314">The approach is similar to table-valued parameters, but an XML file or string is passed to a stored procedure instead of a user-defined table.</span></span> <span data-ttu-id="13a80-315">La stored procedure analizza i comandi al suo interno.</span><span class="sxs-lookup"><span data-stu-id="13a80-315">The stored procedure parses the commands in the stored procedure.</span></span>

<span data-ttu-id="13a80-316">Questo approccio presenta diversi svantaggi:</span><span class="sxs-lookup"><span data-stu-id="13a80-316">There are several disadvantages to this approach:</span></span>

* <span data-ttu-id="13a80-317">L'uso di XML può risultare complesso e soggetto a errori.</span><span class="sxs-lookup"><span data-stu-id="13a80-317">Working with XML can be cumbersome and error prone.</span></span>
* <span data-ttu-id="13a80-318">L'analisi dell'XML nel database può implicare un uso intensivo della CPU.</span><span class="sxs-lookup"><span data-stu-id="13a80-318">Parsing the XML on the database can be CPU-intensive.</span></span>
* <span data-ttu-id="13a80-319">Nella maggior parte dei casi questo metodo è più lento rispetto ai parametri con valori di tabella.</span><span class="sxs-lookup"><span data-stu-id="13a80-319">In most cases, this method is slower than table-valued parameters.</span></span>

<span data-ttu-id="13a80-320">Per questi motivi, l'uso dell'XML per le query in batch non è consigliabile.</span><span class="sxs-lookup"><span data-stu-id="13a80-320">For these reasons, the use of XML for batch queries is not recommended.</span></span>

## <a name="batching-considerations"></a><span data-ttu-id="13a80-321">Considerazioni sull'invio in batch</span><span class="sxs-lookup"><span data-stu-id="13a80-321">Batching considerations</span></span>
<span data-ttu-id="13a80-322">Le sezioni seguenti includono altre indicazioni per l'uso dell'invio in batch nelle applicazioni di database SQL.</span><span class="sxs-lookup"><span data-stu-id="13a80-322">The following sections provide more guidance for the use of batching in SQL Database applications.</span></span>

### <a name="tradeoffs"></a><span data-ttu-id="13a80-323">Compromessi</span><span class="sxs-lookup"><span data-stu-id="13a80-323">Tradeoffs</span></span>
<span data-ttu-id="13a80-324">A seconda dell'architettura, l'invio in batch può comportare un compromesso tra prestazioni e resilienza.</span><span class="sxs-lookup"><span data-stu-id="13a80-324">Depending on your architecture, batching can involve a tradeoff between performance and resiliency.</span></span> <span data-ttu-id="13a80-325">Si consideri ad esempio uno scenario in cui il proprio ruolo viene inaspettatamente disattivato.</span><span class="sxs-lookup"><span data-stu-id="13a80-325">For example, consider the scenario where your role unexpectedly goes down.</span></span> <span data-ttu-id="13a80-326">La perdita di una riga di dati produce un impatto inferiore alla perdita di un grosso batch di righe non inviate.</span><span class="sxs-lookup"><span data-stu-id="13a80-326">If you lose one row of data, the impact is smaller than the impact of losing a large batch of unsubmitted rows.</span></span> <span data-ttu-id="13a80-327">Esiste un rischio maggiore nei casi in cui le righe vengono memorizzate in un buffer prima dell'invio al database in una finestra temporale specificata.</span><span class="sxs-lookup"><span data-stu-id="13a80-327">There is a greater risk when you buffer rows before sending them to the database in a specified time window.</span></span>

<span data-ttu-id="13a80-328">Considerando questo compromesso, valutare con attenzione i tipi di operazioni da eseguire in batch.</span><span class="sxs-lookup"><span data-stu-id="13a80-328">Because of this tradeoff, evaluate the type of operations that you batch.</span></span> <span data-ttu-id="13a80-329">Usare più ampiamente i batch, con dimensioni maggiori e finestre temporali più ampie, per i dati meno critici.</span><span class="sxs-lookup"><span data-stu-id="13a80-329">Batch more aggressively (larger batches and longer time windows) with data that is less critical.</span></span>

### <a name="batch-size"></a><span data-ttu-id="13a80-330">Dimensioni dei batch</span><span class="sxs-lookup"><span data-stu-id="13a80-330">Batch size</span></span>
<span data-ttu-id="13a80-331">I test non hanno in genere evidenziato vantaggi correlati alla suddivisione di batch di grandi dimensioni in blocchi più piccoli.</span><span class="sxs-lookup"><span data-stu-id="13a80-331">In our tests, there was typically no advantage to breaking large batches into smaller chunks.</span></span> <span data-ttu-id="13a80-332">In effetti, questa suddivisione ha causato spesso prestazioni inferiori rispetto all'invio di un singolo batch di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="13a80-332">In fact, this subdivision often resulted in slower performance than submitting a single large batch.</span></span> <span data-ttu-id="13a80-333">Si consideri ad esempio uno scenario che prevede l'inserimento di 1000 righe.</span><span class="sxs-lookup"><span data-stu-id="13a80-333">For example, consider a scenario where you want to insert 1000 rows.</span></span> <span data-ttu-id="13a80-334">La tabella seguente mostra il tempo necessario per usare parametri con valori di tabella per l'inserimento di 1000 righe divise in batch più piccoli.</span><span class="sxs-lookup"><span data-stu-id="13a80-334">The following table shows how long it takes to use table-valued parameters to insert 1000 rows when divided into smaller batches.</span></span>

| <span data-ttu-id="13a80-335">Dimensioni dei batch</span><span class="sxs-lookup"><span data-stu-id="13a80-335">Batch size</span></span> | <span data-ttu-id="13a80-336">Iterazioni</span><span class="sxs-lookup"><span data-stu-id="13a80-336">Iterations</span></span> | <span data-ttu-id="13a80-337">Parametri con valori di tabella (ms)</span><span class="sxs-lookup"><span data-stu-id="13a80-337">Table-valued parameters (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="13a80-338">1000</span><span class="sxs-lookup"><span data-stu-id="13a80-338">1000</span></span> |<span data-ttu-id="13a80-339">1</span><span class="sxs-lookup"><span data-stu-id="13a80-339">1</span></span> |<span data-ttu-id="13a80-340">347</span><span class="sxs-lookup"><span data-stu-id="13a80-340">347</span></span> |
| <span data-ttu-id="13a80-341">500</span><span class="sxs-lookup"><span data-stu-id="13a80-341">500</span></span> |<span data-ttu-id="13a80-342">2</span><span class="sxs-lookup"><span data-stu-id="13a80-342">2</span></span> |<span data-ttu-id="13a80-343">355</span><span class="sxs-lookup"><span data-stu-id="13a80-343">355</span></span> |
| <span data-ttu-id="13a80-344">100</span><span class="sxs-lookup"><span data-stu-id="13a80-344">100</span></span> |<span data-ttu-id="13a80-345">10</span><span class="sxs-lookup"><span data-stu-id="13a80-345">10</span></span> |<span data-ttu-id="13a80-346">465</span><span class="sxs-lookup"><span data-stu-id="13a80-346">465</span></span> |
| <span data-ttu-id="13a80-347">50</span><span class="sxs-lookup"><span data-stu-id="13a80-347">50</span></span> |<span data-ttu-id="13a80-348">20</span><span class="sxs-lookup"><span data-stu-id="13a80-348">20</span></span> |<span data-ttu-id="13a80-349">630</span><span class="sxs-lookup"><span data-stu-id="13a80-349">630</span></span> |

> [!NOTE]
> <span data-ttu-id="13a80-350">I risultati non sono benchmark.</span><span class="sxs-lookup"><span data-stu-id="13a80-350">Results are not benchmarks.</span></span> <span data-ttu-id="13a80-351">Vedere la [nota sui risultati della tempistica in questo argomento](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="13a80-351">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="13a80-352">È possibile notare che le prestazioni migliori per 1000 righe si ottengono inviandole tutte insieme.</span><span class="sxs-lookup"><span data-stu-id="13a80-352">You can see that the best performance for 1000 rows is to submit them all at once.</span></span> <span data-ttu-id="13a80-353">In altri test, non riportati qui, si è notato un lieve miglioramento delle prestazioni suddividendo un batch di 10000 righe in due batch da 5000.</span><span class="sxs-lookup"><span data-stu-id="13a80-353">In other tests (not shown here) there was a small performance gain to break a 10000 row batch into two batches of 5000.</span></span> <span data-ttu-id="13a80-354">Lo schema della tabella in questi test è tuttavia relativamente semplice, quindi è consigliabile condurre test su dati e dimensioni di batch specifici per verificare questi risultati.</span><span class="sxs-lookup"><span data-stu-id="13a80-354">But the table schema for these tests is relatively simple, so you should perform tests on your specific data and batch sizes to verify these findings.</span></span>

<span data-ttu-id="13a80-355">Un altro fattore da tenere presente è il fatto che se il batch complessivo diventa troppo grande, il database SQL potrebbe applicare limitazioni e rifiutarne il commit.</span><span class="sxs-lookup"><span data-stu-id="13a80-355">Another factor to consider is that if the total batch becomes too large, SQL Database might throttle and refuse to commit the batch.</span></span> <span data-ttu-id="13a80-356">Per ottenere risultati ottimali, testare il proprio scenario specifico per determinare le dimensioni ideali dei batch.</span><span class="sxs-lookup"><span data-stu-id="13a80-356">For the best results, test your specific scenario to determine if there is an ideal batch size.</span></span> <span data-ttu-id="13a80-357">Rendere configurabili le dimensioni del batch in fase di esecuzione per consentire modifiche rapide in base alle prestazioni o agli errori.</span><span class="sxs-lookup"><span data-stu-id="13a80-357">Make the batch size configurable at runtime to enable quick adjustments based on performance or errors.</span></span>

<span data-ttu-id="13a80-358">Infine, individuare un equilibro tra le dimensioni del batch e i rischi associati all'invio in batch.</span><span class="sxs-lookup"><span data-stu-id="13a80-358">Finally, balance the size of the batch with the risks associated with batching.</span></span> <span data-ttu-id="13a80-359">Se si verificano errori temporanei o il ruolo ha esito negativo, valutare le conseguenze di dover ripetere l'operazione o di perdere i dati nel batch.</span><span class="sxs-lookup"><span data-stu-id="13a80-359">If there are transient errors or the role fails, consider the consequences of retrying the operation or of losing the data in the batch.</span></span>

### <a name="parallel-processing"></a><span data-ttu-id="13a80-360">Elaborazione parallela</span><span class="sxs-lookup"><span data-stu-id="13a80-360">Parallel processing</span></span>
<span data-ttu-id="13a80-361">Che cosa accadrebbe se si adottasse l'approccio di ridurre le dimensioni del batch, ma si utilizzassero più thread per eseguire le operazioni?</span><span class="sxs-lookup"><span data-stu-id="13a80-361">What if you took the approach of reducing the batch size but used multiple threads to execute the work?</span></span> <span data-ttu-id="13a80-362">Anche in questo caso, i test indicano che diversi batch multithreading di dimensioni ridotte producono prestazioni generalmente inferiori a un singolo batch di dimensioni maggiori.</span><span class="sxs-lookup"><span data-stu-id="13a80-362">Again, our tests showed that several smaller multithreaded batches typically performed worse than a single larger batch.</span></span> <span data-ttu-id="13a80-363">Il test seguente tenta di inserire 1000 righe in uno o più batch paralleli.</span><span class="sxs-lookup"><span data-stu-id="13a80-363">The following test attempts to insert 1000 rows in one or more parallel batches.</span></span> <span data-ttu-id="13a80-364">Questo test indica come più batch simultanei causino in effetti una riduzione delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="13a80-364">This test shows how more simultaneous batches actually decreased performance.</span></span>

| <span data-ttu-id="13a80-365">Dimensioni dei batch [iterazioni]</span><span class="sxs-lookup"><span data-stu-id="13a80-365">Batch size [Iterations]</span></span> | <span data-ttu-id="13a80-366">Due thread (ms)</span><span class="sxs-lookup"><span data-stu-id="13a80-366">Two threads (ms)</span></span> | <span data-ttu-id="13a80-367">Quattro thread (ms)</span><span class="sxs-lookup"><span data-stu-id="13a80-367">Four threads (ms)</span></span> | <span data-ttu-id="13a80-368">Sei thread (ms)</span><span class="sxs-lookup"><span data-stu-id="13a80-368">Six threads (ms)</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="13a80-369">1000 [1]</span><span class="sxs-lookup"><span data-stu-id="13a80-369">1000 [1]</span></span> |<span data-ttu-id="13a80-370">277</span><span class="sxs-lookup"><span data-stu-id="13a80-370">277</span></span> |<span data-ttu-id="13a80-371">315</span><span class="sxs-lookup"><span data-stu-id="13a80-371">315</span></span> |<span data-ttu-id="13a80-372">266</span><span class="sxs-lookup"><span data-stu-id="13a80-372">266</span></span> |
| <span data-ttu-id="13a80-373">500 [2]</span><span class="sxs-lookup"><span data-stu-id="13a80-373">500 [2]</span></span> |<span data-ttu-id="13a80-374">548</span><span class="sxs-lookup"><span data-stu-id="13a80-374">548</span></span> |<span data-ttu-id="13a80-375">278</span><span class="sxs-lookup"><span data-stu-id="13a80-375">278</span></span> |<span data-ttu-id="13a80-376">256</span><span class="sxs-lookup"><span data-stu-id="13a80-376">256</span></span> |
| <span data-ttu-id="13a80-377">250 [4]</span><span class="sxs-lookup"><span data-stu-id="13a80-377">250 [4]</span></span> |<span data-ttu-id="13a80-378">405</span><span class="sxs-lookup"><span data-stu-id="13a80-378">405</span></span> |<span data-ttu-id="13a80-379">329</span><span class="sxs-lookup"><span data-stu-id="13a80-379">329</span></span> |<span data-ttu-id="13a80-380">265</span><span class="sxs-lookup"><span data-stu-id="13a80-380">265</span></span> |
| <span data-ttu-id="13a80-381">100 [10]</span><span class="sxs-lookup"><span data-stu-id="13a80-381">100 [10]</span></span> |<span data-ttu-id="13a80-382">488</span><span class="sxs-lookup"><span data-stu-id="13a80-382">488</span></span> |<span data-ttu-id="13a80-383">439</span><span class="sxs-lookup"><span data-stu-id="13a80-383">439</span></span> |<span data-ttu-id="13a80-384">391</span><span class="sxs-lookup"><span data-stu-id="13a80-384">391</span></span> |

> [!NOTE]
> <span data-ttu-id="13a80-385">I risultati non sono benchmark.</span><span class="sxs-lookup"><span data-stu-id="13a80-385">Results are not benchmarks.</span></span> <span data-ttu-id="13a80-386">Vedere la [nota sui risultati della tempistica in questo argomento](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="13a80-386">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="13a80-387">Esistono diverse potenziali cause della riduzione delle prestazioni derivante dal parallelismo:</span><span class="sxs-lookup"><span data-stu-id="13a80-387">There are several potential reasons for the degradation in performance due to parallelism:</span></span>

* <span data-ttu-id="13a80-388">Sono presenti più chiamate di rete simultanee invece di una.</span><span class="sxs-lookup"><span data-stu-id="13a80-388">There are multiple simultaneous network calls instead of one.</span></span>
* <span data-ttu-id="13a80-389">L'esecuzione di più operazioni su una singola tabella può determinare contese e blocchi.</span><span class="sxs-lookup"><span data-stu-id="13a80-389">Multiple operations against a single table can result in contention and blocking.</span></span>
* <span data-ttu-id="13a80-390">Il multithreading implica overhead.</span><span class="sxs-lookup"><span data-stu-id="13a80-390">There are overheads associated with multithreading.</span></span>
* <span data-ttu-id="13a80-391">Il costo dell'apertura di più connessioni annulla il vantaggio dell'elaborazione parallela.</span><span class="sxs-lookup"><span data-stu-id="13a80-391">The expense of opening multiple connections outweighs the benefit of parallel processing.</span></span>

<span data-ttu-id="13a80-392">Se si opera su più tabelle o database, questa strategia può produrre un aumento delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="13a80-392">If you target different tables or databases, it is possible to see some performance gain with this strategy.</span></span> <span data-ttu-id="13a80-393">Il partizionamento orizzontale o le federazioni di database rappresentano uno scenario possibile per questo approccio.</span><span class="sxs-lookup"><span data-stu-id="13a80-393">Database sharding or federations would be a scenario for this approach.</span></span> <span data-ttu-id="13a80-394">Il partizionamento orizzontale usa più database e indirizza dati diversi a ognuno di essi.</span><span class="sxs-lookup"><span data-stu-id="13a80-394">Sharding uses multiple databases and routes different data to each database.</span></span> <span data-ttu-id="13a80-395">Se ogni piccolo batch viene indirizzato a un database diverso, l'esecuzione delle operazioni in parallelo può risultare più efficiente.</span><span class="sxs-lookup"><span data-stu-id="13a80-395">If each small batch is going to a different database, then performing the operations in parallel can be more efficient.</span></span> <span data-ttu-id="13a80-396">Tuttavia, il miglioramento delle prestazioni non è sufficientemente elevato da giustificare la decisione di adottare il partizionamento orizzontale del database nella propria soluzione.</span><span class="sxs-lookup"><span data-stu-id="13a80-396">However, the performance gain is not significant enough to use as the basis for a decision to use database sharding in your solution.</span></span>

<span data-ttu-id="13a80-397">In alcune progettazioni, l'esecuzione parallela di batch di piccole dimensioni può produrre un miglioramento della velocità effettiva delle richieste in un sistema sotto carico.</span><span class="sxs-lookup"><span data-stu-id="13a80-397">In some designs, parallel execution of smaller batches can result in improved throughput of requests in a system under load.</span></span> <span data-ttu-id="13a80-398">In questo caso, anche se l'esecuzione di un singolo batch di dimensioni maggiori è più rapida, quella di più batch in parallelo può risultare più efficiente.</span><span class="sxs-lookup"><span data-stu-id="13a80-398">In this case, even though it is quicker to process a single larger batch, processing multiple batches in parallel might be more efficient.</span></span>

<span data-ttu-id="13a80-399">Se si usa l'esecuzione parallela, provare a controllare il numero massimo di thread di lavoro.</span><span class="sxs-lookup"><span data-stu-id="13a80-399">If you do use parallel execution, consider controlling the maximum number of worker threads.</span></span> <span data-ttu-id="13a80-400">Un numero più piccolo potrebbe ridurre il rischio di contese e i tempi di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="13a80-400">A smaller number might result in less contention and a faster execution time.</span></span> <span data-ttu-id="13a80-401">Tenere anche presente il carico aggiuntivo di questa soluzione sul database di destinazione, sia in termini di connessioni sia di transazioni.</span><span class="sxs-lookup"><span data-stu-id="13a80-401">Also, consider the additional load that this places on the target database both in connections and transactions.</span></span>

### <a name="related-performance-factors"></a><span data-ttu-id="13a80-402">Fattori correlati alle prestazioni</span><span class="sxs-lookup"><span data-stu-id="13a80-402">Related performance factors</span></span>
<span data-ttu-id="13a80-403">Le indicazioni tipiche relative alle prestazioni dei database influiscono anche sull'invio in batch.</span><span class="sxs-lookup"><span data-stu-id="13a80-403">Typical guidance on database performance also affects batching.</span></span> <span data-ttu-id="13a80-404">Le prestazioni delle operazioni di inserimento, ad esempio, risultano ridotte per le tabelle con chiave primaria di grandi dimensioni o con numerosi indici non cluster.</span><span class="sxs-lookup"><span data-stu-id="13a80-404">For example, insert performance is reduced for tables that have a large primary key or many nonclustered indexes.</span></span>

<span data-ttu-id="13a80-405">Se i parametri con valori di tabella usano una stored procedure, è possibile eseguire il comando **SET NOCOUNT ON** all'inizio della routine.</span><span class="sxs-lookup"><span data-stu-id="13a80-405">If table-valued parameters use a stored procedure, you can use the command **SET NOCOUNT ON** at the beginning of the procedure.</span></span> <span data-ttu-id="13a80-406">Questa istruzione rimuove la restituzione del conteggio delle righe interessate nella routine.</span><span class="sxs-lookup"><span data-stu-id="13a80-406">This statement suppresses the return of the count of the affected rows in the procedure.</span></span> <span data-ttu-id="13a80-407">Tuttavia, nei test l'uso di **SET NOCOUNT ON** non ha avuto alcun effetto sulle prestazioni o le ha ridotte.</span><span class="sxs-lookup"><span data-stu-id="13a80-407">However, in our tests, the use of **SET NOCOUNT ON** either had no effect or decreased performance.</span></span> <span data-ttu-id="13a80-408">La stored procedure usata per i test era semplice, con un singolo comando **INSERT** del parametro con valori di tabella.</span><span class="sxs-lookup"><span data-stu-id="13a80-408">The test stored procedure was simple with a single **INSERT** command from the table-valued parameter.</span></span> <span data-ttu-id="13a80-409">È possibile che stored procedure più complesse possano trarre vantaggio da questa istruzione.</span><span class="sxs-lookup"><span data-stu-id="13a80-409">It is possible that more complex stored procedures would benefit from this statement.</span></span> <span data-ttu-id="13a80-410">Non si deve tuttavia supporre che l'aggiunta di **SET NOCOUNT ON** alla stored procedure migliori automaticamente le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="13a80-410">But don’t assume that adding **SET NOCOUNT ON** to your stored procedure automatically improves performance.</span></span> <span data-ttu-id="13a80-411">Per comprendere l'effetto, testare la stored procedure con e senza l'istruzione **SET NOCOUNT ON** .</span><span class="sxs-lookup"><span data-stu-id="13a80-411">To understand the effect, test your stored procedure with and without the **SET NOCOUNT ON** statement.</span></span>

## <a name="batching-scenarios"></a><span data-ttu-id="13a80-412">Scenari di invio in batch</span><span class="sxs-lookup"><span data-stu-id="13a80-412">Batching scenarios</span></span>
<span data-ttu-id="13a80-413">Nelle sezioni seguenti viene descritto come usare parametri con valori di tabella in tre scenari di applicazione.</span><span class="sxs-lookup"><span data-stu-id="13a80-413">The following sections describe how to use table-valued parameters in three application scenarios.</span></span> <span data-ttu-id="13a80-414">Il primo scenario illustra in che modo interagiscono il buffering e l'invio in batch.</span><span class="sxs-lookup"><span data-stu-id="13a80-414">The first scenario shows how buffering and batching can work together.</span></span> <span data-ttu-id="13a80-415">Nel secondo scenario le prestazioni vengono migliorate eseguendo operazioni master/dettaglio in una singola chiamata di stored procedure.</span><span class="sxs-lookup"><span data-stu-id="13a80-415">The second scenario improves performance by performing master-detail operations in a single stored procedure call.</span></span> <span data-ttu-id="13a80-416">Lo scenario finale illustra come usare parametri con valori di tabella in un'operazione "UPSERT".</span><span class="sxs-lookup"><span data-stu-id="13a80-416">The final scenario shows how to use table-valued parameters in an “UPSERT” operation.</span></span>

### <a name="buffering"></a><span data-ttu-id="13a80-417">Buffering</span><span class="sxs-lookup"><span data-stu-id="13a80-417">Buffering</span></span>
<span data-ttu-id="13a80-418">Sebbene alcuni scenari siano particolarmente adatti all'invio in batch, ne esistono numerosi che potrebbero trarre vantaggio da questo tipo di operazione grazie all'elaborazione ritardata.</span><span class="sxs-lookup"><span data-stu-id="13a80-418">Although there are some scenarios that are obvious candidate for batching, there are many scenarios that could take advantage of batching by delayed processing.</span></span> <span data-ttu-id="13a80-419">L'elaborazione ritardata implica tuttavia anche un maggiore rischio che i dati vengano persi in caso di errore imprevisto.</span><span class="sxs-lookup"><span data-stu-id="13a80-419">However, delayed processing also carries a greater risk that the data is lost in the event of an unexpected failure.</span></span> <span data-ttu-id="13a80-420">È importante comprendere tale rischio e valutarne le conseguenze.</span><span class="sxs-lookup"><span data-stu-id="13a80-420">It is important to understand this risk and consider the consequences.</span></span>

<span data-ttu-id="13a80-421">Si consideri ad esempio un'applicazione Web che tiene traccia della cronologia di navigazione di ogni utente.</span><span class="sxs-lookup"><span data-stu-id="13a80-421">For example, consider a web application that tracks the navigation history of each user.</span></span> <span data-ttu-id="13a80-422">Per ogni richiesta di pagina, l'applicazione potrebbe eseguire una chiamata al database per registrare la visualizzazione della pagina da parte dell'utente.</span><span class="sxs-lookup"><span data-stu-id="13a80-422">On each page request, the application could make a database call to record the user’s page view.</span></span> <span data-ttu-id="13a80-423">Tuttavia è possibile conseguire livelli maggiori di prestazioni e scalabilità mediante il buffering delle attività di navigazione dell'utente e quindi inviando i dati al database in batch.</span><span class="sxs-lookup"><span data-stu-id="13a80-423">But higher performance and scalability can be achieved by buffering the users’ navigation activities and then sending this data to the database in batches.</span></span> <span data-ttu-id="13a80-424">È possibile attivare l'aggiornamento del database in base al tempo trascorso e/o alle dimensioni del buffer.</span><span class="sxs-lookup"><span data-stu-id="13a80-424">You can trigger the database update by elapsed time and/or buffer size.</span></span> <span data-ttu-id="13a80-425">Ad esempio, una regola potrebbe indicare che il batch deve essere elaborato dopo 20 secondi o quando il buffer raggiunge i 1000 elementi.</span><span class="sxs-lookup"><span data-stu-id="13a80-425">For example, a rule could specify that the batch should be processed after 20 seconds or when the buffer reaches 1000 items.</span></span>

<span data-ttu-id="13a80-426">L'esempio di codice seguente usa [Reactive Extensions - Rx](https://msdn.microsoft.com/data/gg577609) per elaborare eventi memorizzati nel buffer generati da una classe di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="13a80-426">The following code example uses [Reactive Extensions - Rx](https://msdn.microsoft.com/data/gg577609) to process buffered events raised by a monitoring class.</span></span> <span data-ttu-id="13a80-427">Quando il buffer si riempie o si raggiunge un timeout, il batch di dati utente viene inviato al database con un parametro con valori di tabella.</span><span class="sxs-lookup"><span data-stu-id="13a80-427">When the buffer fills or a timeout is reached, the batch of user data is sent to the database with a table-valued parameter.</span></span>

<span data-ttu-id="13a80-428">La classe NavHistoryData seguente modella i dettagli di navigazione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="13a80-428">The following NavHistoryData class models the user navigation details.</span></span> <span data-ttu-id="13a80-429">Contiene informazioni di base quali l'identificatore utente, l'URL a cui si accede e l'ora di accesso.</span><span class="sxs-lookup"><span data-stu-id="13a80-429">It contains basic information such as the user identifier, the URL accessed, and the access time.</span></span>

    public class NavHistoryData
    {
        public NavHistoryData(int userId, string url, DateTime accessTime)
        { UserId = userId; URL = url; AccessTime = accessTime; }
        public int UserId { get; set; }
        public string URL { get; set; }
        public DateTime AccessTime { get; set; }
    }

<span data-ttu-id="13a80-430">La classe NavHistoryDataMonitor è responsabile del buffering dei dati di navigazione dell'utente nel database.</span><span class="sxs-lookup"><span data-stu-id="13a80-430">The NavHistoryDataMonitor class is responsible for buffering the user navigation data to the database.</span></span> <span data-ttu-id="13a80-431">Contiene un metodo RecordUserNavigationEntry che risponde generando un evento **OnAdded** .</span><span class="sxs-lookup"><span data-stu-id="13a80-431">It contains a method, RecordUserNavigationEntry, which responds by raising an **OnAdded** event.</span></span> <span data-ttu-id="13a80-432">Il codice seguente illustra la logica del costruttore che utilizza Rx per creare una raccolta osservabile in base all'evento.</span><span class="sxs-lookup"><span data-stu-id="13a80-432">The following code shows the constructor logic that uses Rx to create an observable collection based on the event.</span></span> <span data-ttu-id="13a80-433">Sottoscrive quindi questa raccolta osservabile con il metodo Buffer.</span><span class="sxs-lookup"><span data-stu-id="13a80-433">It then subscribes to this observable collection with the Buffer method.</span></span> <span data-ttu-id="13a80-434">L'overload specifica che il buffer deve essere inviato ogni 20 secondi o 1000 voci.</span><span class="sxs-lookup"><span data-stu-id="13a80-434">The overload specifies that the buffer should be sent every 20 seconds or 1000 entries.</span></span>

    public NavHistoryDataMonitor()
    {
        var observableData =
            Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

        observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
    }

<span data-ttu-id="13a80-435">Il gestore converte tutti gli elementi memorizzati nel buffer nel tipo con valori di tabella e quindi passa questo tipo a una stored procedure che elabora il batch.</span><span class="sxs-lookup"><span data-stu-id="13a80-435">The handler converts all of the buffered items into a table-valued type and then passes this type to a stored procedure that processes the batch.</span></span> <span data-ttu-id="13a80-436">Il codice seguente illustra la definizione completa per le classi NavHistoryDataEventArgs e NavHistoryDataMonitor.</span><span class="sxs-lookup"><span data-stu-id="13a80-436">The following code shows the complete definition for both the NavHistoryDataEventArgs and the NavHistoryDataMonitor classes.</span></span>

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

<span data-ttu-id="13a80-437">Per usare questa classe di buffering, l'applicazione crea un oggetto statico NavHistoryDataMonitor.</span><span class="sxs-lookup"><span data-stu-id="13a80-437">To use this buffering class, the application creates a static NavHistoryDataMonitor object.</span></span> <span data-ttu-id="13a80-438">Ogni volta che l'utente accede a una pagina, l'applicazione chiama il metodo NavHistoryDataMonitor.RecordUserNavigationEntry.</span><span class="sxs-lookup"><span data-stu-id="13a80-438">Each time a user accesses a page, the application calls the NavHistoryDataMonitor.RecordUserNavigationEntry method.</span></span> <span data-ttu-id="13a80-439">La logica di buffering continua a provvedere all'invio delle voci al database in batch.</span><span class="sxs-lookup"><span data-stu-id="13a80-439">The buffering logic proceeds to take care of sending these entries to the database in batches.</span></span>

### <a name="master-detail"></a><span data-ttu-id="13a80-440">Master/dettaglio</span><span class="sxs-lookup"><span data-stu-id="13a80-440">Master detail</span></span>
<span data-ttu-id="13a80-441">I parametri con valori di tabella sono utili per gli scenari INSERT semplici.</span><span class="sxs-lookup"><span data-stu-id="13a80-441">Table-valued parameters are useful for simple INSERT scenarios.</span></span> <span data-ttu-id="13a80-442">Tuttavia, può risultare più difficile inviare in batch le operazioni di inserimento che includono più tabelle.</span><span class="sxs-lookup"><span data-stu-id="13a80-442">However, it can be more challenging to batch inserts that involve more than one table.</span></span> <span data-ttu-id="13a80-443">Lo scenario "master/dettaglio" è un buon esempio.</span><span class="sxs-lookup"><span data-stu-id="13a80-443">The “master/detail” scenario is a good example.</span></span> <span data-ttu-id="13a80-444">La tabella master identifica l'entità primaria.</span><span class="sxs-lookup"><span data-stu-id="13a80-444">The master table identifies the primary entity.</span></span> <span data-ttu-id="13a80-445">In una o più tabelle dei dettagli sono archiviati altri dati sull'entità.</span><span class="sxs-lookup"><span data-stu-id="13a80-445">One or more detail tables store more data about the entity.</span></span> <span data-ttu-id="13a80-446">In questo scenario, le relazioni di chiave esterna applicano la relazione dei dettagli a un'entità master univoca.</span><span class="sxs-lookup"><span data-stu-id="13a80-446">In this scenario, foreign key relationships enforce the relationship of details to a unique master entity.</span></span> <span data-ttu-id="13a80-447">Si consideri una versione semplificata di una tabella PurchaseOrder e la tabella associata OrderDetail.</span><span class="sxs-lookup"><span data-stu-id="13a80-447">Consider a simplified version of a PurchaseOrder table and its associated OrderDetail table.</span></span> <span data-ttu-id="13a80-448">L'istruzione Transact-SQL seguente crea la tabella PurchaseOrder con quattro colonne: OrderID, OrderDate, CustomerID e Status.</span><span class="sxs-lookup"><span data-stu-id="13a80-448">The following Transact-SQL creates the PurchaseOrder table with four columns: OrderID, OrderDate, CustomerID, and Status.</span></span>

    CREATE TABLE [dbo].[PurchaseOrder](
    [OrderID] [int] IDENTITY(1,1) NOT NULL,
    [OrderDate] [datetime] NOT NULL,
    [CustomerID] [int] NOT NULL,
    [Status] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrder] 
    PRIMARY KEY CLUSTERED ( [OrderID] ASC ))

<span data-ttu-id="13a80-449">Ogni ordine contiene uno o più acquisti di prodotti.</span><span class="sxs-lookup"><span data-stu-id="13a80-449">Each order contains one or more product purchases.</span></span> <span data-ttu-id="13a80-450">Tali informazioni vengono acquisite nella tabella PurchaseOrderDetail.</span><span class="sxs-lookup"><span data-stu-id="13a80-450">This information is captured in the PurchaseOrderDetail table.</span></span> <span data-ttu-id="13a80-451">L'istruzione Transact-SQL seguente crea la tabella PurchaseOrderDetail con cinque colonne: OrderID, OrderDetailID, ProductID, UnitPrice e OrderQty.</span><span class="sxs-lookup"><span data-stu-id="13a80-451">The following Transact-SQL creates the PurchaseOrderDetail table with five columns: OrderID, OrderDetailID, ProductID, UnitPrice, and OrderQty.</span></span>

    CREATE TABLE [dbo].[PurchaseOrderDetail](
    [OrderID] [int] NOT NULL,
    [OrderDetailID] [int] IDENTITY(1,1) NOT NULL,
    [ProductID] [int] NOT NULL,
    [UnitPrice] [money] NULL,
    [OrderQty] [smallint] NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrderDetail] PRIMARY KEY CLUSTERED 
    ( [OrderID] ASC, [OrderDetailID] ASC ))

<span data-ttu-id="13a80-452">La colonna OrderID della tabella PurchaseOrderDetail deve fare riferimento a un ordine dalla tabella PurchaseOrder.</span><span class="sxs-lookup"><span data-stu-id="13a80-452">The OrderID column in the PurchaseOrderDetail table must reference an order from the PurchaseOrder table.</span></span> <span data-ttu-id="13a80-453">La seguente definizione di una chiave esterna applica il vincolo.</span><span class="sxs-lookup"><span data-stu-id="13a80-453">The following definition of a foreign key enforces this constraint.</span></span>

    ALTER TABLE [dbo].[PurchaseOrderDetail]  WITH CHECK ADD 
    CONSTRAINT [FK_OrderID_PurchaseOrder] FOREIGN KEY([OrderID])
    REFERENCES [dbo].[PurchaseOrder] ([OrderID])

<span data-ttu-id="13a80-454">Per usare parametri con valori di tabella, è necessario avere un tipo di tabella definito dall'utente per ogni tabella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="13a80-454">In order to use table-valued parameters, you must have one user-defined table type for each target table.</span></span>

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

<span data-ttu-id="13a80-455">Definire quindi una stored procedure che accetti tabelle di questi tipi.</span><span class="sxs-lookup"><span data-stu-id="13a80-455">Then define a stored procedure that accepts tables of these types.</span></span> <span data-ttu-id="13a80-456">Questa routine consente a un'applicazione di inviare in batch localmente un set di ordini e i dettagli degli ordini in una singola chiamata.</span><span class="sxs-lookup"><span data-stu-id="13a80-456">This procedure allows an application to locally batch a set of orders and order details in a single call.</span></span> <span data-ttu-id="13a80-457">L'istruzione Transact-SQL seguente fornisce la dichiarazione completa della stored procedure per questo esempio di ordine di acquisto.</span><span class="sxs-lookup"><span data-stu-id="13a80-457">The following Transact-SQL provides the complete stored procedure declaration for this purchase order example.</span></span>

    CREATE PROCEDURE sp_InsertOrdersBatch (
    @orders as PurchaseOrderTableType READONLY,
    @details as PurchaseOrderDetailTableType READONLY )
    AS
    SET NOCOUNT ON;

    -- Table that connects the order identifiers in the @orders
    -- table with the actual order identifiers in the PurchaseOrder table
    DECLARE @IdentityLink AS TABLE ( 
    SubmittedKey int, 
    ActualKey int, 
    RowNumber int identity(1,1)
    );

          -- Add new orders to the PurchaseOrder table, storing the actual
    -- order identifiers in the @IdentityLink table   
    INSERT INTO PurchaseOrder ([OrderDate], [CustomerID], [Status])
    OUTPUT inserted.OrderID INTO @IdentityLink (ActualKey)
    SELECT [OrderDate], [CustomerID], [Status] FROM @orders ORDER BY OrderID;

    -- Match the passed-in order identifiers with the actual identifiers
    -- and complete the @IdentityLink table for use with inserting the details
    WITH OrderedRows As (
    SELECT OrderID, ROW_NUMBER () OVER (ORDER BY OrderID) As RowNumber 
    FROM @orders
    )
    UPDATE @IdentityLink SET SubmittedKey = M.OrderID
    FROM @IdentityLink L JOIN OrderedRows M ON L.RowNumber = M.RowNumber;

    -- Insert the order details into the PurchaseOrderDetail table, 
          -- using the actual order identifiers of the master table, PurchaseOrder
    INSERT INTO PurchaseOrderDetail (
    [OrderID],
    [ProductID],
    [UnitPrice],
    [OrderQty] )
    SELECT L.ActualKey, D.ProductID, D.UnitPrice, D.OrderQty
    FROM @details D
    JOIN @IdentityLink L ON L.SubmittedKey = D.OrderID;
    GO

<span data-ttu-id="13a80-458">In questo esempio la tabella @IdentityLink definita a livello locale archivia i valori OrderID effettivi dalle righe appena inserite.</span><span class="sxs-lookup"><span data-stu-id="13a80-458">In this example, the locally defined @IdentityLink table stores the actual OrderID values from the newly inserted rows.</span></span> <span data-ttu-id="13a80-459">Gli identificatori di ordine sono diversi dai valori OrderID temporanei nei parametri con valori di tabella @orders e @details.</span><span class="sxs-lookup"><span data-stu-id="13a80-459">These order identifiers are different from the temporary OrderID values in the @orders and @details table-valued parameters.</span></span> <span data-ttu-id="13a80-460">Per questo motivo, la tabella @IdentityLink connette quindi i valori OrderID del parametro @orders ai valori OrderID reali per le nuove righe della tabella PurchaseOrder.</span><span class="sxs-lookup"><span data-stu-id="13a80-460">For this reason, the @IdentityLink table then connects the OrderID values from the @orders parameter to the real OrderID values for the new rows in the PurchaseOrder table.</span></span> <span data-ttu-id="13a80-461">Dopo questo passaggio, la tabella @IdentityLink può facilitare l'inserimento dei dettagli degli ordini con il valore OrderID effettivo che soddisfa il vincolo di chiave esterna.</span><span class="sxs-lookup"><span data-stu-id="13a80-461">After this step, the @IdentityLink table can facilitate inserting the order details with the actual OrderID that satisfies the foreign key constraint.</span></span>

<span data-ttu-id="13a80-462">Questa stored procedure può essere utilizzata dal codice o da altre chiamate Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="13a80-462">This stored procedure can be used from code or from other Transact-SQL calls.</span></span> <span data-ttu-id="13a80-463">Vedere la sezione sui parametri con valori di tabella di questo articolo per un esempio di codice.</span><span class="sxs-lookup"><span data-stu-id="13a80-463">See the table-valued parameters section of this paper for a code example.</span></span> <span data-ttu-id="13a80-464">Il codice Transact-SQL seguente mostra come chiamare sp_InsertOrdersBatch.</span><span class="sxs-lookup"><span data-stu-id="13a80-464">The following Transact-SQL shows how to call the sp_InsertOrdersBatch.</span></span>

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

<span data-ttu-id="13a80-465">Questa soluzione consente a ogni batch di usare un set di valori OrderID che iniziano da 1.</span><span class="sxs-lookup"><span data-stu-id="13a80-465">This solution allows each batch to use a set of OrderID values that begin at 1.</span></span> <span data-ttu-id="13a80-466">Questi valori OrderID temporanei descrivono le relazioni nel batch, ma i valori OrderID effettivi vengono determinati al momento dell'operazione di inserimento.</span><span class="sxs-lookup"><span data-stu-id="13a80-466">These temporary OrderID values describe the relationships in the batch, but the actual OrderID values are determined at the time of the insert operation.</span></span> <span data-ttu-id="13a80-467">È possibile eseguire ripetutamente le stesse istruzioni dell'esempio precedente e generare ordini univoci nel database.</span><span class="sxs-lookup"><span data-stu-id="13a80-467">You can run the same statements in the previous example repeatedly and generate unique orders in the database.</span></span> <span data-ttu-id="13a80-468">Per questo motivo, considerare l'aggiunta di più logica di database o di codice che impedisca gli ordini duplicati quando si usa questa tecnica di invio in batch.</span><span class="sxs-lookup"><span data-stu-id="13a80-468">For this reason, consider adding more code or database logic that prevents duplicate orders when using this batching technique.</span></span>

<span data-ttu-id="13a80-469">In questo esempio viene spiegato che è possibile eseguire in batch anche operazioni di database più complesse, ad esempio operazioni master/dettaglio, usando i parametri con valori di tabella.</span><span class="sxs-lookup"><span data-stu-id="13a80-469">This example demonstrates that even more complex database operations, such as master-detail operations, can be batched using table-valued parameters.</span></span>

### <a name="upsert"></a><span data-ttu-id="13a80-470">UPSERT</span><span class="sxs-lookup"><span data-stu-id="13a80-470">UPSERT</span></span>
<span data-ttu-id="13a80-471">Un altro scenario di invio in batch prevede l'aggiornamento simultaneo di righe esistenti e l'inserimento di nuove righe.</span><span class="sxs-lookup"><span data-stu-id="13a80-471">Another batching scenario involves simultaneously updating existing rows and inserting new rows.</span></span> <span data-ttu-id="13a80-472">Questa operazione viene talvolta denominata "UPSERT" (aggiornamento + inserimento).</span><span class="sxs-lookup"><span data-stu-id="13a80-472">This operation is sometimes referred to as an “UPSERT” (update + insert) operation.</span></span> <span data-ttu-id="13a80-473">Invece di eseguire chiamate separate a INSERT e UPDATE, l'istruzione MERGE è più adatta a questa attività.</span><span class="sxs-lookup"><span data-stu-id="13a80-473">Rather than making separate calls to INSERT and UPDATE, the MERGE statement is best suited to this task.</span></span> <span data-ttu-id="13a80-474">L'istruzione MERGE può eseguire operazioni di inserimento e aggiornamento in una singola chiamata.</span><span class="sxs-lookup"><span data-stu-id="13a80-474">The MERGE statement can perform both insert and update operations in a single call.</span></span>

<span data-ttu-id="13a80-475">I parametri con valori di tabella possono essere usati con l'istruzione MERGE per eseguire aggiornamenti e inserimenti.</span><span class="sxs-lookup"><span data-stu-id="13a80-475">Table-valued parameters can be used with the MERGE statement to perform updates and inserts.</span></span> <span data-ttu-id="13a80-476">Si consideri ad esempio una tabella Employee semplificata che contiene le colonne seguenti: EmployeeID, FirstName, LastName, SocialSecurityNumber:</span><span class="sxs-lookup"><span data-stu-id="13a80-476">For example, consider a simplified Employee table that contains the following columns: EmployeeID, FirstName, LastName, SocialSecurityNumber:</span></span>

    CREATE TABLE [dbo].[Employee](
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [SocialSecurityNumber] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_Employee] PRIMARY KEY CLUSTERED 
    ([EmployeeID] ASC ))

<span data-ttu-id="13a80-477">In questo esempio, è possibile usare il fatto che la colonna SocialSecurityNumber è unica per eseguire un'operazione MERGE di più dipendenti.</span><span class="sxs-lookup"><span data-stu-id="13a80-477">In this example, you can use the fact that the SocialSecurityNumber is unique to perform a MERGE of multiple employees.</span></span> <span data-ttu-id="13a80-478">Creare innanzitutto il tipo di tabella definito dall'utente:</span><span class="sxs-lookup"><span data-stu-id="13a80-478">First, create the user-defined table type:</span></span>

    CREATE TYPE EmployeeTableType AS TABLE 
    ( Employee_ID INT,
      FirstName NVARCHAR(50),
      LastName NVARCHAR(50),
      SocialSecurityNumber NVARCHAR(50) );
    GO

<span data-ttu-id="13a80-479">Successivamente, creare una stored procedure oppure scrivere codice che usi l'istruzione MERGE per eseguire l'aggiornamento e l'inserimento.</span><span class="sxs-lookup"><span data-stu-id="13a80-479">Next, create a stored procedure or write code that uses the MERGE statement to perform the update and insert.</span></span> <span data-ttu-id="13a80-480">L'esempio seguente usa l'istruzione MERGE in un parametro con valori di tabella, @employees, di tipo EmployeeTableType.</span><span class="sxs-lookup"><span data-stu-id="13a80-480">The following example uses the MERGE statement on a table-valued parameter, @employees, of type EmployeeTableType.</span></span> <span data-ttu-id="13a80-481">Il contenuto della tabella @employees non è illustrato.</span><span class="sxs-lookup"><span data-stu-id="13a80-481">The contents of the @employees table are not shown here.</span></span>

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

<span data-ttu-id="13a80-482">Per altre informazioni, vedere la documentazione e gli esempi relativi all'istruzione MERGE.</span><span class="sxs-lookup"><span data-stu-id="13a80-482">For more information, see the documentation and examples for the MERGE statement.</span></span> <span data-ttu-id="13a80-483">Anche se la stessa operazione può essere eseguita in una chiamata di stored procedure in più passaggi con le operazioni INSERT e UPDATE, l'istruzione MERGE è più efficiente.</span><span class="sxs-lookup"><span data-stu-id="13a80-483">Although the same work could be performed in a multiple-step stored procedure call with separate INSERT and UPDATE operations, the MERGE statement is more efficient.</span></span> <span data-ttu-id="13a80-484">Il codice del database può anche creare chiamate Transact-SQL che usano l'istruzione MERGE direttamente senza richiedere due chiamate di database per INSERT e UPDATE.</span><span class="sxs-lookup"><span data-stu-id="13a80-484">Database code can also construct Transact-SQL calls that use the MERGE statement directly without requiring two database calls for INSERT and UPDATE.</span></span>

## <a name="recommendation-summary"></a><span data-ttu-id="13a80-485">Riepilogo delle indicazioni</span><span class="sxs-lookup"><span data-stu-id="13a80-485">Recommendation summary</span></span>
<span data-ttu-id="13a80-486">L'elenco seguente fornisce un riepilogo delle indicazioni relative all'invio in batch descritte in questo argomento:</span><span class="sxs-lookup"><span data-stu-id="13a80-486">The following list provides a summary of the batching recommendations discussed in this topic:</span></span>

* <span data-ttu-id="13a80-487">Usare il buffering e l'invio in batch per migliorare le prestazioni e la scalabilità delle applicazioni di database SQL.</span><span class="sxs-lookup"><span data-stu-id="13a80-487">Use buffering and batching to increase the performance and scalability of SQL Database applications.</span></span>
* <span data-ttu-id="13a80-488">Esaminare i compromessi tra invio in batch/buffering e resilienza.</span><span class="sxs-lookup"><span data-stu-id="13a80-488">Understand the tradeoffs between batching/buffering and resiliency.</span></span> <span data-ttu-id="13a80-489">In caso di errore in un ruolo, il rischio di perdere un batch non elaborato di dati aziendali critici potrebbe vanificare il vantaggio in termini di prestazioni che deriva dall'invio in batch.</span><span class="sxs-lookup"><span data-stu-id="13a80-489">During a role failure, the risk of losing an unprocessed batch of business-critical data might outweigh the performance benefit of batching.</span></span>
* <span data-ttu-id="13a80-490">Provare a mantenere tutte le chiamate al database entro un singolo data center per ridurre la latenza.</span><span class="sxs-lookup"><span data-stu-id="13a80-490">Attempt to keep all calls to the database within a single datacenter to reduce latency.</span></span>
* <span data-ttu-id="13a80-491">Se si sceglie una singola tecnica di invio in batch, i parametri con valori di tabella offrono il miglior rapporto tra prestazioni e flessibilità.</span><span class="sxs-lookup"><span data-stu-id="13a80-491">If you choose a single batching technique, table-valued parameters offer the best performance and flexibility.</span></span>
* <span data-ttu-id="13a80-492">Per prestazioni di inserimento estremamente veloci, attenersi alle linee guida generali, ma testare lo scenario:</span><span class="sxs-lookup"><span data-stu-id="13a80-492">For the fastest insert performance, follow these general guidelines but test your scenario:</span></span>
  * <span data-ttu-id="13a80-493">Per < 100 righe, usare un singolo comando INSERT con parametri.</span><span class="sxs-lookup"><span data-stu-id="13a80-493">For < 100 rows, use a single parameterized INSERT command.</span></span>
  * <span data-ttu-id="13a80-494">Per < 1000 righe usare parametri con valori di tabella.</span><span class="sxs-lookup"><span data-stu-id="13a80-494">For < 1000 rows, use table-valued parameters.</span></span>
  * <span data-ttu-id="13a80-495">Per >= 1000 righe usare SqlBulkCopy.</span><span class="sxs-lookup"><span data-stu-id="13a80-495">For >= 1000 rows, use SqlBulkCopy.</span></span>
* <span data-ttu-id="13a80-496">Per operazioni di aggiornamento ed eliminazione, usare parametri con valori di tabella con la logica della stored procedure che determini il corretto funzionamento in ogni riga del parametro della tabella.</span><span class="sxs-lookup"><span data-stu-id="13a80-496">For update and delete operations, use table-valued parameters with stored procedure logic that determines the correct operation on each row in the table parameter.</span></span>
* <span data-ttu-id="13a80-497">Linee guida sulle dimensioni dei batch:</span><span class="sxs-lookup"><span data-stu-id="13a80-497">Batch size guidelines:</span></span>
  * <span data-ttu-id="13a80-498">Usare batch di grandi dimensioni considerando i requisiti delle applicazioni e aziendali.</span><span class="sxs-lookup"><span data-stu-id="13a80-498">Use the largest batch sizes that make sense for your application and business requirements.</span></span>
  * <span data-ttu-id="13a80-499">Bilanciare il miglioramento delle prestazioni dei batch di grandi dimensioni e i rischi di errori temporanei o irreversibili.</span><span class="sxs-lookup"><span data-stu-id="13a80-499">Balance the performance gain of large batches with the risks of temporary or catastrophic failures.</span></span> <span data-ttu-id="13a80-500">Qual è la conseguenza di più tentativi o di perdita dei dati nel batch?</span><span class="sxs-lookup"><span data-stu-id="13a80-500">What is the consequence of retries or loss of the data in the batch?</span></span> 
  * <span data-ttu-id="13a80-501">Testare i batch con le massime dimensioni per verificare che il database SQL non li rifiuti.</span><span class="sxs-lookup"><span data-stu-id="13a80-501">Test the largest batch size to verify that SQL Database does not reject it.</span></span>
  * <span data-ttu-id="13a80-502">Creare le impostazioni di configurazione che controllano l'invio in batch, ad esempio le dimensioni dei batch o la finestra temporale di buffering.</span><span class="sxs-lookup"><span data-stu-id="13a80-502">Create configuration settings that control batching, such as the batch size or the buffering time window.</span></span> <span data-ttu-id="13a80-503">Queste impostazioni offrono flessibilità.</span><span class="sxs-lookup"><span data-stu-id="13a80-503">These settings provide flexibility.</span></span> <span data-ttu-id="13a80-504">È possibile modificare il comportamento di invio in batch in produzione senza ridistribuire il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="13a80-504">You can change the batching behavior in production without redeploying the cloud service.</span></span>
* <span data-ttu-id="13a80-505">Evitare l'esecuzione parallela di batch che operano su una singola tabella in un database.</span><span class="sxs-lookup"><span data-stu-id="13a80-505">Avoid parallel execution of batches that operate on a single table in one database.</span></span> <span data-ttu-id="13a80-506">Se si sceglie di dividere un singolo batch tra più thread di lavoro, eseguire i test per determinare il numero ideale di thread.</span><span class="sxs-lookup"><span data-stu-id="13a80-506">If you do choose to divide a single batch across multiple worker threads, run tests to determine the ideal number of threads.</span></span> <span data-ttu-id="13a80-507">Dopo una soglia non specificata, più thread determinano una riduzione delle prestazioni invece di un aumento.</span><span class="sxs-lookup"><span data-stu-id="13a80-507">After an unspecified threshold, more threads will decrease performance rather than increase it.</span></span>
* <span data-ttu-id="13a80-508">Considerare il buffering in base a dimensioni e tempo come modalità di implementazione dell'invio in batch per più scenari.</span><span class="sxs-lookup"><span data-stu-id="13a80-508">Consider buffering on size and time as a way of implementing batching for more scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13a80-509">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="13a80-509">Next steps</span></span>
<span data-ttu-id="13a80-510">Questo articolo descrive in che modo le tecniche di progettazione e codifica di database correlate all'invio in batch possano migliorare le prestazioni e la scalabilità delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="13a80-510">This article focused on how database design and coding techniques related to batching can improve your application performance and scalability.</span></span> <span data-ttu-id="13a80-511">Questo è però solo uno dei fattori della strategia complessiva.</span><span class="sxs-lookup"><span data-stu-id="13a80-511">But this is just one factor in your overall strategy.</span></span> <span data-ttu-id="13a80-512">Per altri modi per migliorare le prestazioni e la scalabilità, vedere le [indicazioni sulle prestazioni del database SQL di Azure per i database singoli](sql-database-performance-guidance.md) e le [considerazioni su prezzo e prestazioni per un pool elastico](sql-database-elastic-pool-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="13a80-512">For more ways to improve performance and scalability, see [Azure SQL Database performance guidance for single databases](sql-database-performance-guidance.md) and [Price and performance considerations for an elastic pool](sql-database-elastic-pool-guidance.md).</span></span>

