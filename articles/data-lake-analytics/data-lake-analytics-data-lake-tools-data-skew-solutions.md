---
title: Risolvere i problemi di asimmetria dei dati tramite Strumenti Azure Data Lake per Visual Studio | Documentazione Microsoft
description: Potenziali risoluzioni dei problemi di asimmetria dei dati tramite Strumenti Azure Data Lake per Visual Studio.
services: data-lake-analytics
documentationcenter: 
author: yanancai
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/16/2016
ms.author: yanacai
ms.openlocfilehash: 9b284ef33be4b935569fc368d81ddf040b2c2b7d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="resolve-data-skew-problems-by-using-azure-data-lake-tools-for-visual-studio"></a><span data-ttu-id="f1d47-103">Risolvere i problemi di asimmetria dei dati tramite Strumenti Azure Data Lake per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f1d47-103">Resolve data-skew problems by using Azure Data Lake Tools for Visual Studio</span></span>

## <a name="what-is-data-skew"></a><span data-ttu-id="f1d47-104">Informazioni sull'asimmetria dei dati</span><span class="sxs-lookup"><span data-stu-id="f1d47-104">What is data skew?</span></span>

<span data-ttu-id="f1d47-105">In poche parole, un'asimmetria dei dati si verifica quando un valore è rappresentato in modo eccessivo.</span><span class="sxs-lookup"><span data-stu-id="f1d47-105">Briefly stated, data skew is an over-represented value.</span></span> <span data-ttu-id="f1d47-106">Si supponga di avere incaricato 50 esaminatori di imposte per controllare le dichiarazioni dei redditi, un esaminatore per ogni stato degli Stati Uniti.</span><span class="sxs-lookup"><span data-stu-id="f1d47-106">Imagine that you have assigned 50 tax examiners to audit tax returns, one examiner for each US state.</span></span> <span data-ttu-id="f1d47-107">L'esaminatore del Wyoming, che ha una popolazione ridotta, ha poco da fare.</span><span class="sxs-lookup"><span data-stu-id="f1d47-107">The Wyoming examiner, because the population there is small, has little to do.</span></span> <span data-ttu-id="f1d47-108">In California, invece, l'esaminatore è molto indaffarato a causa della popolazione di notevole entità.</span><span class="sxs-lookup"><span data-stu-id="f1d47-108">In California, however, the examiner is kept very busy because of the state's large population.</span></span>
    <span data-ttu-id="f1d47-109">![Esempio di un problema di asimmetria dei dati](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)</span><span class="sxs-lookup"><span data-stu-id="f1d47-109">![Data-skew problem example](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)</span></span>

<span data-ttu-id="f1d47-110">In questo scenario, i dati sono distribuiti in modo non uniforme tra tutti gli esaminatori di imposta, il che significa che alcuni esaminatori lavorano di più rispetto ad altri.</span><span class="sxs-lookup"><span data-stu-id="f1d47-110">In our scenario, the data is unevenly distributed across all tax examiners, which means that some examiners must work more than others.</span></span> <span data-ttu-id="f1d47-111">Nell'attività personale, non di rado si verificano situazioni simili allo scenario degli esaminatori di imposta qui presentato.</span><span class="sxs-lookup"><span data-stu-id="f1d47-111">In your own job, you frequently experience situations like the tax-examiner example here.</span></span> <span data-ttu-id="f1d47-112">In termini più tecnici, un vertice ottiene molti più dati rispetto agli altri elementi, una situazione che costringe il vertice a lavorare di più rispetto agli altri e che, di conseguenza, rallenta l'intero processo.</span><span class="sxs-lookup"><span data-stu-id="f1d47-112">In more technical terms, one vertex gets much more data than its peers, a situation that makes the vertex work more than the others and that eventually slows down an entire job.</span></span> <span data-ttu-id="f1d47-113">Ancor peggio, il processo potrebbe avere esito negativo in quanto i vertici potrebbero presentare, ad esempio, un limite di runtime di 5 ore e un limite della memoria pari a 6 GB.</span><span class="sxs-lookup"><span data-stu-id="f1d47-113">What's worse, the job might fail, because vertices might have, for example, a 5-hour runtime limitation and a 6-GB memory limitation.</span></span>

## <a name="resolving-data-skew-problems"></a><span data-ttu-id="f1d47-114">Risoluzione dei problemi di asimmetria dei dati</span><span class="sxs-lookup"><span data-stu-id="f1d47-114">Resolving data-skew problems</span></span>

<span data-ttu-id="f1d47-115">Gli Strumenti Azure Data Lake per Visual Studio consentono di rilevare eventuali problemi di asimmetria dei dati all'interno dei processi.</span><span class="sxs-lookup"><span data-stu-id="f1d47-115">Azure Data Lake Tools for Visual Studio can help detect whether your job has a data-skew problem.</span></span> <span data-ttu-id="f1d47-116">Se si verifica un problema, è possibile risolverlo tramite le soluzioni presentate in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="f1d47-116">If a problem exists, you can resolve it by trying the solutions in this section.</span></span>

## <a name="solution-1-improve-table-partitioning"></a><span data-ttu-id="f1d47-117">Soluzione 1. Migliorare il partizionamento delle tabelle</span><span class="sxs-lookup"><span data-stu-id="f1d47-117">Solution 1: Improve table partitioning</span></span>

### <a name="option-1-filter-the-skewed-key-value-in-advance"></a><span data-ttu-id="f1d47-118">Opzione 1. Filtrare in anticipo un valore chiave differente</span><span class="sxs-lookup"><span data-stu-id="f1d47-118">Option 1: Filter the skewed key value in advance</span></span>

<span data-ttu-id="f1d47-119">Se ciò non influisce sulla logica di business, è possibile filtrare in anticipo i valori a frequenza più elevata.</span><span class="sxs-lookup"><span data-stu-id="f1d47-119">If it does not affect your business logic, you can filter the higher-frequency values in advance.</span></span> <span data-ttu-id="f1d47-120">Ad esempio, se sono presenti molti 000-000-000 nella colonna GUID, l'utente potrebbe scegliere di non aggregare tale valore.</span><span class="sxs-lookup"><span data-stu-id="f1d47-120">For example, if there are a lot of 000-000-000 in column GUID, you might not want to aggregate that value.</span></span> <span data-ttu-id="f1d47-121">Prima di eseguire l'aggregazione, è possibile scrivere "WHERE GUID != "000-000-000"" per filtrare il valore ad alta frequenza.</span><span class="sxs-lookup"><span data-stu-id="f1d47-121">Before you aggregate, you can write “WHERE GUID != “000-000-000”” to filter the high-frequency value.</span></span>

### <a name="option-2-pick-a-different-partition-or-distribution-key"></a><span data-ttu-id="f1d47-122">Opzione 2. Selezionare una chiave di partizione o distribuzione differente</span><span class="sxs-lookup"><span data-stu-id="f1d47-122">Option 2: Pick a different partition or distribution key</span></span>

<span data-ttu-id="f1d47-123">Nell'esempio precedente, se si desidera solo verificare il carico di lavoro della verifica fiscale in tutto il paese, è possibile migliorare la distribuzione dei dati selezionando il numero ID come chiave.</span><span class="sxs-lookup"><span data-stu-id="f1d47-123">In the preceding example, if you want only to check the tax-audit workload all over the country, you can improve the data distribution by selecting the ID number as your key.</span></span> <span data-ttu-id="f1d47-124">La scelta di una chiave di partizione o distribuzione differente consente talvolta di distribuire i dati in modo più uniforme, ma è necessario verificare che la scelta non abbia impatto sulla logica di business.</span><span class="sxs-lookup"><span data-stu-id="f1d47-124">Picking a different partition or distribution key can sometimes distribute the data more evenly, but you need to make sure that this choice doesn’t affect your business logic.</span></span> <span data-ttu-id="f1d47-125">Ad esempio, per calcolare l'importo dell'imposta per ogni stato, è consigliabile specificare _Stato_ come chiave di partizione.</span><span class="sxs-lookup"><span data-stu-id="f1d47-125">For instance, to calculate the tax sum for each state, you might want to designate _State_ as the partition key.</span></span> <span data-ttu-id="f1d47-126">Se il problema persiste, provare con l'opzione 3.</span><span class="sxs-lookup"><span data-stu-id="f1d47-126">If you continue to experience this problem, try using Option 3.</span></span>

### <a name="option-3-add-more-partition-or-distribution-keys"></a><span data-ttu-id="f1d47-127">Opzione 3. Aggiungere più chiavi di partizione o distribuzione</span><span class="sxs-lookup"><span data-stu-id="f1d47-127">Option 3: Add more partition or distribution keys</span></span>

<span data-ttu-id="f1d47-128">Invece di usare solo _Stato_ come chiave di partizione, è possibile impiegare più di una chiave per il partizionamento.</span><span class="sxs-lookup"><span data-stu-id="f1d47-128">Instead of using only _State_ as a partition key, you can use more than one key for partitioning.</span></span> <span data-ttu-id="f1d47-129">Ad esempio, è consigliabile aggiungere un _CAP_ come chiave di partizione aggiuntiva per ridurre le dimensioni della partizione dei dati e distribuire i dati in modo più uniforme.</span><span class="sxs-lookup"><span data-stu-id="f1d47-129">For example, consider adding _ZIP Code_ as an additional partition key to reduce data-partition sizes and distribute the data more evenly.</span></span>

### <a name="option-4-use-round-robin-distribution"></a><span data-ttu-id="f1d47-130">Opzione 4. Usare la distribuzione round robin</span><span class="sxs-lookup"><span data-stu-id="f1d47-130">Option 4: Use round-robin distribution</span></span>

<span data-ttu-id="f1d47-131">Qualora non sia possibile trovare una chiave adeguata per la partizione e la distribuzione, si può usare la distribuzione round robin.</span><span class="sxs-lookup"><span data-stu-id="f1d47-131">If you cannot find an appropriate key for partition and distribution, you can try to use round-robin distribution.</span></span> <span data-ttu-id="f1d47-132">La distribuzione round robin considera tutte le righe in modo uguale e le inserisce in modo casuale nei bucket corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="f1d47-132">Round-robin distribution treats all rows equally and randomly puts them into corresponding buckets.</span></span> <span data-ttu-id="f1d47-133">I dati vengono distribuiti uniformemente ma si perdono le informazioni sulla località, uno svantaggio che riduce anche le prestazioni del processo rispetto ad alcune operazioni.</span><span class="sxs-lookup"><span data-stu-id="f1d47-133">The data gets evenly distributed, but it loses locality information, a drawback that can also reduce job performance for some operations.</span></span> <span data-ttu-id="f1d47-134">In aggiunta, se si sta eseguendo un'aggregazione per risolvere un problema di chiave differente, il problema dell'asimmetria dei dati non verrà risolto.</span><span class="sxs-lookup"><span data-stu-id="f1d47-134">Additionally, if you are doing aggregation for the skewed key anyway, the data-skew problem will persist.</span></span> <span data-ttu-id="f1d47-135">Per altre informazioni sulla distribuzione round robin, vedere la sezione U-SQL Table Distributions (Distribuzioni di tabelle U-SQL) in [CREATE TABLE (U-SQL): Creating a Table with Schema](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch) (CREATE TABLE (U-SQL): creazione di una tabella con Schema).</span><span class="sxs-lookup"><span data-stu-id="f1d47-135">To learn more about round-robin distribution, see the U-SQL Table Distributions section in [CREATE TABLE (U-SQL): Creating a Table with Schema](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).</span></span>

## <a name="solution-2-improve-the-query-plan"></a><span data-ttu-id="f1d47-136">Soluzione 2. Migliorare il piano di query</span><span class="sxs-lookup"><span data-stu-id="f1d47-136">Solution 2: Improve the query plan</span></span>

### <a name="option-1-use-the-create-statistics-statement"></a><span data-ttu-id="f1d47-137">Opzione 1. Usare l'istruzione CREATE STATISTICS</span><span class="sxs-lookup"><span data-stu-id="f1d47-137">Option 1: Use the CREATE STATISTICS statement</span></span>

<span data-ttu-id="f1d47-138">U-SQL fornisce l'istruzione CREATE STATISTICS nelle tabelle.</span><span class="sxs-lookup"><span data-stu-id="f1d47-138">U-SQL provides the CREATE STATISTICS statement on tables.</span></span> <span data-ttu-id="f1d47-139">Questa istruzione offre al Query Optimizer altre informazioni relative alle caratteristiche dei dati, ad esempio la distribuzione dei valori, archiviati in una tabella.</span><span class="sxs-lookup"><span data-stu-id="f1d47-139">This statement gives more information to the query optimizer about the data characteristics, such as value distribution, that are stored in a table.</span></span> <span data-ttu-id="f1d47-140">Per la maggior parte delle query, il Query Optimizer genera già le statistiche necessarie per un piano di query di elevata qualità.</span><span class="sxs-lookup"><span data-stu-id="f1d47-140">For most queries, the query optimizer already generates the necessary statistics for a high-quality query plan.</span></span> <span data-ttu-id="f1d47-141">In alcuni casi, potrebbe essere necessario migliorare le prestazioni delle query creando statistiche aggiuntive con CREATE STATISTICS o modificando la struttura delle query.</span><span class="sxs-lookup"><span data-stu-id="f1d47-141">Occasionally, you might need to improve query performance by creating additional statistics with CREATE STATISTICS or by modifying the query design.</span></span> <span data-ttu-id="f1d47-142">Per altre informazioni, vedere la pagina [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) (CREATE STATISTICS (U-SQL)).</span><span class="sxs-lookup"><span data-stu-id="f1d47-142">For more information, see the [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) page.</span></span>

<span data-ttu-id="f1d47-143">Esempio di codice:</span><span class="sxs-lookup"><span data-stu-id="f1d47-143">Code example:</span></span>

    CREATE STATISTICS IF NOT EXISTS stats_SampleTable_date ON SampleDB.dbo.SampleTable(date) WITH FULLSCAN;

>[!NOTE]
><span data-ttu-id="f1d47-144">Le informazioni statistiche non vengono aggiornate in automatico.</span><span class="sxs-lookup"><span data-stu-id="f1d47-144">Statistics information is not updated automatically.</span></span> <span data-ttu-id="f1d47-145">Se si aggiornano i dati in una tabella senza generare nuovamente le statistiche, le prestazioni delle query potrebbero risultare ridotte.</span><span class="sxs-lookup"><span data-stu-id="f1d47-145">If you update the data in a table without re-creating the statistics, the query performance might decline.</span></span>

### <a name="option-2-use-skewfactor"></a><span data-ttu-id="f1d47-146">Opzione 2. Utilizzo di SKEWFACTOR</span><span class="sxs-lookup"><span data-stu-id="f1d47-146">Option 2: Use SKEWFACTOR</span></span>

<span data-ttu-id="f1d47-147">Se si desidera sommare le imposte per ogni stato, è necessario usare lo stato GROUP BY, un approccio che non evita il problema dell'asimmetria dei dati.</span><span class="sxs-lookup"><span data-stu-id="f1d47-147">If you want to sum the tax for each state, you must use GROUP BY state, an approach that doesn't avoid the data-skew problem.</span></span> <span data-ttu-id="f1d47-148">Tuttavia, è possibile inserire un suggerimento dati nella query per identificare le asimmetrie dei dati nelle chiavi, in modo da preparare un piano di esecuzione personale.</span><span class="sxs-lookup"><span data-stu-id="f1d47-148">However, you can provide a data hint in your query to identify data skew in keys so that the optimizer can prepare an execution plan for you.</span></span>

<span data-ttu-id="f1d47-149">In genere, è possibile impostare il parametro su 0,5 e 1, laddove 0,5 indica un'asimmetria non netta, mentre 1 indica un'asimmetria marcata.</span><span class="sxs-lookup"><span data-stu-id="f1d47-149">Usually, you can set the parameter as 0.5 and 1, with 0.5 meaning not much skew and 1 meaning heavy skew.</span></span> <span data-ttu-id="f1d47-150">Dal momento che il suggerimento ha un impatto sull'ottimizzazione del piano di esecuzione per l'istruzione corrente e per tutte quelle successive, è quindi necessario assicurarsi di aggiungerlo prima della potenziale aggregazione a livello della chiave con asimmetria.</span><span class="sxs-lookup"><span data-stu-id="f1d47-150">Because the hint affects execution-plan optimization for the current statement and all downstream statements, be sure to add the hint before the potential skewed key-wise aggregation.</span></span>

    SKEWFACTOR (columns) = x

    Provides a hint that the given columns have a skew factor x from 0 (no skew) through 1 (very heavy skew).

<span data-ttu-id="f1d47-151">Esempio di codice:</span><span class="sxs-lookup"><span data-stu-id="f1d47-151">Code example:</span></span>

    //Add a SKEWFACTOR hint.
    @Impressions =
        SELECT * FROM
        searchDM.SML.PageView(@start, @end) AS PageView
        OPTION(SKEWFACTOR(Query)=0.5)
        ;

    //Query 1 for key: Query, ClientId
    @Sessions =
        SELECT
            ClientId,
            Query,
            SUM(PageClicks) AS Clicks
        FROM
            @Impressions
        GROUP BY
            Query, ClientId
        ;

    //Query 2 for Key: Query
    @Display =
        SELECT * FROM @Sessions
            INNER JOIN @Campaigns
                ON @Sessions.Query == @Campaigns.Query
        ;   

### <a name="option-3-use-rowcount"></a><span data-ttu-id="f1d47-152">Opzione 3: Usare ROWCOUNT</span><span class="sxs-lookup"><span data-stu-id="f1d47-152">Option 3: Use ROWCOUNT</span></span>  
<span data-ttu-id="f1d47-153">Oltre a SKEWFACTOR, per casi specifici di unioni di chiavi asimmetriche, se si sa che gli altri set di righe unite sono ridotti, è possibile indicarlo all'Optimizer tramite l'aggiunta di un suggerimento ROWCOUNT nell'istruzione U-SQL prima di JOIN.</span><span class="sxs-lookup"><span data-stu-id="f1d47-153">In addition to SKEWFACTOR, for specific skewed-key join cases, if you know that the other joined row set is small, you can tell the optimizer by adding a ROWCOUNT hint in the U-SQL statement before JOIN.</span></span> <span data-ttu-id="f1d47-154">In questo modo, l'Optimizer può scegliere una strategia di aggregazione della trasmissione per migliorare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="f1d47-154">This way, optimizer can choose a broadcast join strategy to help improve performance.</span></span> <span data-ttu-id="f1d47-155">Tenere presente che ROWCOUNT non risolve il problema dell'asimmetria dei dati, ma può offrire aiuto aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="f1d47-155">Be aware that ROWCOUNT does not resolve the data-skew problem, but it can offer some additional help.</span></span>

    OPTION(ROWCOUNT = n)

    Identify a small row set before JOIN by providing an estimated integer row count.

<span data-ttu-id="f1d47-156">Esempio di codice:</span><span class="sxs-lookup"><span data-stu-id="f1d47-156">Code example:</span></span>

    //Unstructured (24-hour daily log impressions)
    @Huge   = EXTRACT ClientId int, ...
                FROM @"wasb://ads@wcentralus/2015/10/30/{*}.nif"
                ;

    //Small subset (that is, ForgetMe opt out)
    @Small  = SELECT * FROM @Huge
                WHERE Bing.ForgetMe(x,y,z)
                OPTION(ROWCOUNT=500)
                ;

    //Result (not enough information to determine simple broadcast JOIN)
    @Remove = SELECT * FROM Bing.Sessions
                INNER JOIN @Small ON Sessions.Client == @Small.Client
                ;

## <a name="solution-3-improve-the-user-defined-reducer-and-combiner"></a><span data-ttu-id="f1d47-157">Soluzione 3. Migliorare il riduttore e il combinatore definiti dall'utente</span><span class="sxs-lookup"><span data-stu-id="f1d47-157">Solution 3: Improve the user-defined reducer and combiner</span></span>

<span data-ttu-id="f1d47-158">A volte per gestire una logica di processo complessa viene usato un operatore definito dall'utente; in alcuni casi, un riduttore e un combinatore ben scritti possono ridurre il problema dell'asimmetria dei dati.</span><span class="sxs-lookup"><span data-stu-id="f1d47-158">You can sometimes write a user-defined operator to deal with complicated process logic, and a well-written reducer and combiner might mitigate a data-skew problem in some cases.</span></span>

### <a name="option-1-use-a-recursive-reducer-if-possible"></a><span data-ttu-id="f1d47-159">Opzione 1. Usare un riduttore ricorsivo se possibile</span><span class="sxs-lookup"><span data-stu-id="f1d47-159">Option 1: Use a recursive reducer, if possible</span></span>

<span data-ttu-id="f1d47-160">Per impostazione predefinita, un riduttore definito dall'utente viene eseguito in modalità non ricorsiva, ovvero il lavoro di riduzione per una chiave verrà distribuito su un unico vertice.</span><span class="sxs-lookup"><span data-stu-id="f1d47-160">By default, a user-defined reducer runs in non-recursive mode, which means that reduce work for a key is distributed into a single vertex.</span></span> <span data-ttu-id="f1d47-161">In caso di asimmetria dei dati, i set di dati di grandi dimensioni potrebbero essere elaborati in un unico vertice e richiedere un tempo di esecuzione lungo.</span><span class="sxs-lookup"><span data-stu-id="f1d47-161">But if your data is skewed, the huge data sets might be processed in a single vertex and run for a long time.</span></span>

<span data-ttu-id="f1d47-162">Per migliorare le prestazioni, è possibile aggiungere un attributo nel codice per definire l'esecuzione del riduttore in modalità ricorsiva.</span><span class="sxs-lookup"><span data-stu-id="f1d47-162">To improve performance, you can add an attribute in your code to define reducer to run in recursive mode.</span></span> <span data-ttu-id="f1d47-163">A questo punto, i set di dati di grandi dimensioni possono essere distribuiti su più vertici ed eseguiti in parallelo, al fine di velocizzare il processo.</span><span class="sxs-lookup"><span data-stu-id="f1d47-163">Then, the huge data sets can be distributed to multiple vertices and run in parallel, which speeds up your job.</span></span>

<span data-ttu-id="f1d47-164">Per trasformare un riduttore non ricorsivo in ricorsivo è necessario assicurarsi che l'algoritmo sia associativo.</span><span class="sxs-lookup"><span data-stu-id="f1d47-164">To change a non-recursive reducer to recursive, you need to make sure that your algorithm is associative.</span></span> <span data-ttu-id="f1d47-165">Ad esempio, la somma è associativa mentre la media non lo è.</span><span class="sxs-lookup"><span data-stu-id="f1d47-165">For example, the sum is associative, and the median is not.</span></span> <span data-ttu-id="f1d47-166">È necessario anche verificare che l'input e output per il riduttore rispettino lo stesso schema.</span><span class="sxs-lookup"><span data-stu-id="f1d47-166">You also need to make sure that the input and output for reducer keep the same schema.</span></span>

<span data-ttu-id="f1d47-167">Attributo del riduttore ricorsivo:</span><span class="sxs-lookup"><span data-stu-id="f1d47-167">Attribute of recursive reducer:</span></span>

    [SqlUserDefinedReducer(IsRecursive = true)]

<span data-ttu-id="f1d47-168">Esempio di codice:</span><span class="sxs-lookup"><span data-stu-id="f1d47-168">Code example:</span></span>

    [SqlUserDefinedReducer(IsRecursive = true)]
    public class TopNReducer : IReducer
    {
        public override IEnumerable<IRow>
            Reduce(IRowset input, IUpdatableRow output)
        {
            //Your reducer code goes here.
        }
    }

### <a name="option-2-use-row-level-combiner-mode-if-possible"></a><span data-ttu-id="f1d47-169">Opzione 2. Usare la modalità di combinazione a livello di riga, se possibile</span><span class="sxs-lookup"><span data-stu-id="f1d47-169">Option 2: Use row-level combiner mode, if possible</span></span>

<span data-ttu-id="f1d47-170">Analogamente al suggerimento ROWCOUNT per specifici casi di unioni di chiavi asimmetriche, la modalità del combinatore tenta di distribuire set di valori di chiavi asimmetriche su più vertici, in modo da ottenere un'esecuzione simultanea.</span><span class="sxs-lookup"><span data-stu-id="f1d47-170">Similar to the ROWCOUNT hint for specific skewed-key join cases, combiner mode tries to distribute huge skewed-key value sets to multiple vertices so that the work can be executed concurrently.</span></span> <span data-ttu-id="f1d47-171">La modalità del combinatore non può risolvere il problema dell'asimmetria dei dati, ma può offrire un aiuto aggiuntivo per set di valori di chiavi asimmetriche di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="f1d47-171">Combiner mode can’t resolve data-skew issues, but it can offer some additional help for huge skewed-key value sets.</span></span>

<span data-ttu-id="f1d47-172">Per impostazione predefinita, la modalità del combinatore è Full, ovvero il set di righe a sinistra e il set di righe a destra non possono essere separati.</span><span class="sxs-lookup"><span data-stu-id="f1d47-172">By default, the combiner mode is Full, which means that the left row set and right row set cannot be separated.</span></span> <span data-ttu-id="f1d47-173">L'impostazione della modalità su Left/Right/Inner consente l'unione a livello di riga.</span><span class="sxs-lookup"><span data-stu-id="f1d47-173">Setting the mode as Left/Right/Inner enables row-level join.</span></span> <span data-ttu-id="f1d47-174">Il sistema separa il set di righe corrispondente e le distribuisce in più vertici che vengono eseguiti in parallelo.</span><span class="sxs-lookup"><span data-stu-id="f1d47-174">The system separates the corresponding row sets and distributes them into multiple vertices that run in parallel.</span></span> <span data-ttu-id="f1d47-175">Prima di configurare la modalità del combinatore, tuttavia, assicurarsi che sia possibile separare i set di righe corrispondente.</span><span class="sxs-lookup"><span data-stu-id="f1d47-175">However, before you configure the combiner mode, be careful to ensure that the corresponding row sets can be separated.</span></span>

<span data-ttu-id="f1d47-176">L'esempio seguente illustra un set di righe sinistro separato.</span><span class="sxs-lookup"><span data-stu-id="f1d47-176">The example that follows shows a separated left row set.</span></span> <span data-ttu-id="f1d47-177">Ogni riga di output dipende da una singola riga di input a sinistra e potenzialmente da tutte le righe a destra con lo stesso valore chiave.</span><span class="sxs-lookup"><span data-stu-id="f1d47-177">Each output row depends on a single input row from the left, and it potentially depends on all rows from the right with the same key value.</span></span> <span data-ttu-id="f1d47-178">Se si imposta la modalità del combinatore su Left, il sistema separa il grande set di righe a sinistra in set più piccoli e li assegna a più vertici.</span><span class="sxs-lookup"><span data-stu-id="f1d47-178">If you set the combiner mode as left, the system separates the huge left-row set into small ones and assigns them to multiple vertices.</span></span>

![Illustrazione della modalità del combinatore](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/combiner-mode-illustration.png)

>[!NOTE]
><span data-ttu-id="f1d47-180">Se si imposta la modalità del combinatore errata, la combinazione è meno efficiente e i risultati potrebbero essere errati.</span><span class="sxs-lookup"><span data-stu-id="f1d47-180">If you set the wrong combiner mode, the combination is less efficient, and the results might be wrong.</span></span>

<span data-ttu-id="f1d47-181">Attributi della modalità del combinatore:</span><span class="sxs-lookup"><span data-stu-id="f1d47-181">Attributes of combiner mode:</span></span>

- [SqlUserDefinedCombiner(Mode=CombinerMode.Full)]: Every output row potentially depends on all the input rows from left and right with the same key value.

- <span data-ttu-id="f1d47-182">SqlUserDefinedCombiner(Mode=CombinerMode.Left): ogni riga di output dipende da una singola riga di input a sinistra e potenzialmente da tutte le righe a destra con lo stesso valore chiave.</span><span class="sxs-lookup"><span data-stu-id="f1d47-182">SqlUserDefinedCombiner(Mode=CombinerMode.Left): Every output row depends on a single input row from the left (and potentially all rows from the right with the same key value).</span></span>

- <span data-ttu-id="f1d47-183">SqlUserDefinedCombiner(Mode=CombinerMode.Right): ogni riga di output dipende da una singola riga di input a destra e potenzialmente da tutte le righe a sinistra con lo stesso valore chiave.</span><span class="sxs-lookup"><span data-stu-id="f1d47-183">qlUserDefinedCombiner(Mode=CombinerMode.Right): Every output row depends on a single input row from the right (and potentially all rows from the left with the same key value).</span></span>

- <span data-ttu-id="f1d47-184">SqlUserDefinedCombiner(Mode=CombinerMode.Inner): ogni riga di output dipende da una sola riga di input a sinistra e a destra con lo stesso valore.</span><span class="sxs-lookup"><span data-stu-id="f1d47-184">SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Every output row depends on a single input row from the left and the right with the same value.</span></span>

<span data-ttu-id="f1d47-185">Esempio di codice:</span><span class="sxs-lookup"><span data-stu-id="f1d47-185">Code example:</span></span>

    [SqlUserDefinedCombiner(Mode = CombinerMode.Right)]
    public class WatsonDedupCombiner : ICombiner
    {
        public override IEnumerable<IRow>
            Combine(IRowset left, IRowset right, IUpdatableRow output)
        {
        //Your combiner code goes here.
        }
    }
