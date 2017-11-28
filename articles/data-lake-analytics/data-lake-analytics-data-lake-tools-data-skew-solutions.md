---
title: problemi di dati inclinazione aaaResolve usando Azure Data Lake Tools per Visual Studio | Documenti Microsoft
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
ms.openlocfilehash: 3909fbd89eb40f061268cb7128f7fa84a3c33de7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-data-skew-problems-by-using-azure-data-lake-tools-for-visual-studio"></a><span data-ttu-id="6f79d-103">Risolvere i problemi di asimmetria dei dati tramite Strumenti Azure Data Lake per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6f79d-103">Resolve data-skew problems by using Azure Data Lake Tools for Visual Studio</span></span>

## <a name="what-is-data-skew"></a><span data-ttu-id="6f79d-104">Informazioni sull'asimmetria dei dati</span><span class="sxs-lookup"><span data-stu-id="6f79d-104">What is data skew?</span></span>

<span data-ttu-id="6f79d-105">In poche parole, un'asimmetria dei dati si verifica quando un valore è rappresentato in modo eccessivo.</span><span class="sxs-lookup"><span data-stu-id="6f79d-105">Briefly stated, data skew is an over-represented value.</span></span> <span data-ttu-id="6f79d-106">Si supponga di avere assegnato 50 esaminatori tax tooaudit redditi, uno esaminatore per ogni stato degli Stati Uniti.</span><span class="sxs-lookup"><span data-stu-id="6f79d-106">Imagine that you have assigned 50 tax examiners tooaudit tax returns, one examiner for each US state.</span></span> <span data-ttu-id="6f79d-107">Esaminatore Wyoming Hello, poiché sono popolamento hello è ridotto, ha toodo minimo.</span><span class="sxs-lookup"><span data-stu-id="6f79d-107">hello Wyoming examiner, because hello population there is small, has little toodo.</span></span> <span data-ttu-id="6f79d-108">California, tuttavia, Esaminatore hello viene conservata occupati a causa della popolazione di grandi dimensioni hello dello stato.</span><span class="sxs-lookup"><span data-stu-id="6f79d-108">In California, however, hello examiner is kept very busy because of hello state's large population.</span></span>
    <span data-ttu-id="6f79d-109">![Esempio di un problema di asimmetria dei dati](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)</span><span class="sxs-lookup"><span data-stu-id="6f79d-109">![Data-skew problem example](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)</span></span>

<span data-ttu-id="6f79d-110">In questo scenario, dati hello non viene distribuiti tra esaminatori tax tutti, il che significa che alcune esaminatori devono funzionare più rispetto ad altri.</span><span class="sxs-lookup"><span data-stu-id="6f79d-110">In our scenario, hello data is unevenly distributed across all tax examiners, which means that some examiners must work more than others.</span></span> <span data-ttu-id="6f79d-111">Nel processo, spesso si verificano situazioni di questo esempio imposta examiner hello.</span><span class="sxs-lookup"><span data-stu-id="6f79d-111">In your own job, you frequently experience situations like hello tax-examiner example here.</span></span> <span data-ttu-id="6f79d-112">In termini più tecnici, un vertice Ottiene molti più dati rispetto agli altri elementi, una situazione che rende il vertice hello più hello altri e che infine rallenta un intero processo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="6f79d-112">In more technical terms, one vertex gets much more data than its peers, a situation that makes hello vertex work more than hello others and that eventually slows down an entire job.</span></span> <span data-ttu-id="6f79d-113">Che cos'è peggiore, il processo di hello potrebbe non riuscire, poiché potrebbero avere vertici, ad esempio, un limite di 5 ore runtime e un limite di 6 GB di memoria.</span><span class="sxs-lookup"><span data-stu-id="6f79d-113">What's worse, hello job might fail, because vertices might have, for example, a 5-hour runtime limitation and a 6-GB memory limitation.</span></span>

## <a name="resolving-data-skew-problems"></a><span data-ttu-id="6f79d-114">Risoluzione dei problemi di asimmetria dei dati</span><span class="sxs-lookup"><span data-stu-id="6f79d-114">Resolving data-skew problems</span></span>

<span data-ttu-id="6f79d-115">Gli Strumenti Azure Data Lake per Visual Studio consentono di rilevare eventuali problemi di asimmetria dei dati all'interno dei processi.</span><span class="sxs-lookup"><span data-stu-id="6f79d-115">Azure Data Lake Tools for Visual Studio can help detect whether your job has a data-skew problem.</span></span> <span data-ttu-id="6f79d-116">Se esiste un problema, è possibile risolverlo provando soluzioni hello in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="6f79d-116">If a problem exists, you can resolve it by trying hello solutions in this section.</span></span>

## <a name="solution-1-improve-table-partitioning"></a><span data-ttu-id="6f79d-117">Soluzione 1. Migliorare il partizionamento delle tabelle</span><span class="sxs-lookup"><span data-stu-id="6f79d-117">Solution 1: Improve table partitioning</span></span>

### <a name="option-1-filter-hello-skewed-key-value-in-advance"></a><span data-ttu-id="6f79d-118">Opzione 1: Hello filtro inclinata valore della chiave in anticipo</span><span class="sxs-lookup"><span data-stu-id="6f79d-118">Option 1: Filter hello skewed key value in advance</span></span>

<span data-ttu-id="6f79d-119">Se non si applica la logica di business, è possibile filtrare i valori di una frequenza maggiore hello in anticipo.</span><span class="sxs-lookup"><span data-stu-id="6f79d-119">If it does not affect your business logic, you can filter hello higher-frequency values in advance.</span></span> <span data-ttu-id="6f79d-120">Ad esempio, se sono presenti molti 000 000 000 nella colonna GUID, non è tooaggregate tale valore.</span><span class="sxs-lookup"><span data-stu-id="6f79d-120">For example, if there are a lot of 000-000-000 in column GUID, you might not want tooaggregate that value.</span></span> <span data-ttu-id="6f79d-121">Prima di aggregazione, è possibile scrivere "dove GUID!"000 000-000"=" valore di toofilter hello ad alta frequenza.</span><span class="sxs-lookup"><span data-stu-id="6f79d-121">Before you aggregate, you can write “WHERE GUID != “000-000-000”” toofilter hello high-frequency value.</span></span>

### <a name="option-2-pick-a-different-partition-or-distribution-key"></a><span data-ttu-id="6f79d-122">Opzione 2. Selezionare una chiave di partizione o distribuzione differente</span><span class="sxs-lookup"><span data-stu-id="6f79d-122">Option 2: Pick a different partition or distribution key</span></span>

<span data-ttu-id="6f79d-123">In hello sopra riportato, se si desidera che il carico di lavoro di solo toocheck hello verifica fiscale tutti su hello paese, è possibile migliorare la distribuzione dei dati hello selezionando il numero di ID hello come chiave.</span><span class="sxs-lookup"><span data-stu-id="6f79d-123">In hello preceding example, if you want only toocheck hello tax-audit workload all over hello country, you can improve hello data distribution by selecting hello ID number as your key.</span></span> <span data-ttu-id="6f79d-124">Selezione di una partizione diversa o una chiave di distribuzione può talvolta distribuire dati hello più uniforme, ma è necessario assicurarsi che questa opzione non influisce sulla logica di business toomake.</span><span class="sxs-lookup"><span data-stu-id="6f79d-124">Picking a different partition or distribution key can sometimes distribute hello data more evenly, but you need toomake sure that this choice doesn’t affect your business logic.</span></span> <span data-ttu-id="6f79d-125">Ad esempio, somma di imposte hello toocalculate per ogni stato, è opportuno toodesignate _stato_ come chiave di partizione hello.</span><span class="sxs-lookup"><span data-stu-id="6f79d-125">For instance, toocalculate hello tax sum for each state, you might want toodesignate _State_ as hello partition key.</span></span> <span data-ttu-id="6f79d-126">Se si continua tooexperience questo problema, provare a utilizzare l'opzione 3.</span><span class="sxs-lookup"><span data-stu-id="6f79d-126">If you continue tooexperience this problem, try using Option 3.</span></span>

### <a name="option-3-add-more-partition-or-distribution-keys"></a><span data-ttu-id="6f79d-127">Opzione 3. Aggiungere più chiavi di partizione o distribuzione</span><span class="sxs-lookup"><span data-stu-id="6f79d-127">Option 3: Add more partition or distribution keys</span></span>

<span data-ttu-id="6f79d-128">Invece di usare solo _Stato_ come chiave di partizione, è possibile impiegare più di una chiave per il partizionamento.</span><span class="sxs-lookup"><span data-stu-id="6f79d-128">Instead of using only _State_ as a partition key, you can use more than one key for partitioning.</span></span> <span data-ttu-id="6f79d-129">Ad esempio, si consiglia di aggiungere _CAP_ come una partizione aggiuntiva chiave tooreduce-partizione di dati di dimensioni e distribuire dati hello più uniforme.</span><span class="sxs-lookup"><span data-stu-id="6f79d-129">For example, consider adding _ZIP Code_ as an additional partition key tooreduce data-partition sizes and distribute hello data more evenly.</span></span>

### <a name="option-4-use-round-robin-distribution"></a><span data-ttu-id="6f79d-130">Opzione 4. Usare la distribuzione round robin</span><span class="sxs-lookup"><span data-stu-id="6f79d-130">Option 4: Use round-robin distribution</span></span>

<span data-ttu-id="6f79d-131">Se è possibile trovare una chiave appropriata per la partizione e la distribuzione, è possibile provare distribuzione round-robin toouse.</span><span class="sxs-lookup"><span data-stu-id="6f79d-131">If you cannot find an appropriate key for partition and distribution, you can try toouse round-robin distribution.</span></span> <span data-ttu-id="6f79d-132">La distribuzione round robin considera tutte le righe in modo uguale e le inserisce in modo casuale nei bucket corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="6f79d-132">Round-robin distribution treats all rows equally and randomly puts them into corresponding buckets.</span></span> <span data-ttu-id="6f79d-133">dati di Hello Ottiene distribuiti uniformemente, ma perde le informazioni di località, uno svantaggio che consente inoltre di ridurre le prestazioni per alcune operazioni.</span><span class="sxs-lookup"><span data-stu-id="6f79d-133">hello data gets evenly distributed, but it loses locality information, a drawback that can also reduce job performance for some operations.</span></span> <span data-ttu-id="6f79d-134">Inoltre, se si esegue l'aggregazione per la chiave asimmetrica hello comunque, problema dati inclinazione hello verrà mantenute.</span><span class="sxs-lookup"><span data-stu-id="6f79d-134">Additionally, if you are doing aggregation for hello skewed key anyway, hello data-skew problem will persist.</span></span> <span data-ttu-id="6f79d-135">toolearn ulteriori informazioni su distribuzione round-robin, vedere le distribuzioni di tabella U-SQL hello sezione [CREATE TABLE (U-SQL): creazione di una tabella con Schema](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).</span><span class="sxs-lookup"><span data-stu-id="6f79d-135">toolearn more about round-robin distribution, see hello U-SQL Table Distributions section in [CREATE TABLE (U-SQL): Creating a Table with Schema](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).</span></span>

## <a name="solution-2-improve-hello-query-plan"></a><span data-ttu-id="6f79d-136">Soluzione 2: Migliorare il piano di query di hello</span><span class="sxs-lookup"><span data-stu-id="6f79d-136">Solution 2: Improve hello query plan</span></span>

### <a name="option-1-use-hello-create-statistics-statement"></a><span data-ttu-id="6f79d-137">Opzione 1: Utilizzare l'istruzione CREATE STATISTICS hello</span><span class="sxs-lookup"><span data-stu-id="6f79d-137">Option 1: Use hello CREATE STATISTICS statement</span></span>

<span data-ttu-id="6f79d-138">U-SQL fornisce l'istruzione CREATE STATISTICS hello nelle tabelle.</span><span class="sxs-lookup"><span data-stu-id="6f79d-138">U-SQL provides hello CREATE STATISTICS statement on tables.</span></span> <span data-ttu-id="6f79d-139">Questa istruzione offre toohello query optimizer di ulteriori informazioni sulle hello dati caratteristiche, ad esempio la distribuzione di valore, che sono archiviati in una tabella.</span><span class="sxs-lookup"><span data-stu-id="6f79d-139">This statement gives more information toohello query optimizer about hello data characteristics, such as value distribution, that are stored in a table.</span></span> <span data-ttu-id="6f79d-140">Per la maggior parte delle query, hello query optimizer genera già le statistiche necessarie per un piano di query di alta qualità hello.</span><span class="sxs-lookup"><span data-stu-id="6f79d-140">For most queries, hello query optimizer already generates hello necessary statistics for a high-quality query plan.</span></span> <span data-ttu-id="6f79d-141">In alcuni casi, potrebbe essere necessario tooimprove le prestazioni delle query creando statistiche aggiuntive con CREATE STATISTICS o modificando la progettazione di query hello.</span><span class="sxs-lookup"><span data-stu-id="6f79d-141">Occasionally, you might need tooimprove query performance by creating additional statistics with CREATE STATISTICS or by modifying hello query design.</span></span> <span data-ttu-id="6f79d-142">Per ulteriori informazioni, vedere hello [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) pagina.</span><span class="sxs-lookup"><span data-stu-id="6f79d-142">For more information, see hello [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) page.</span></span>

<span data-ttu-id="6f79d-143">Esempio di codice:</span><span class="sxs-lookup"><span data-stu-id="6f79d-143">Code example:</span></span>

    CREATE STATISTICS IF NOT EXISTS stats_SampleTable_date ON SampleDB.dbo.SampleTable(date) WITH FULLSCAN;

>[!NOTE]
><span data-ttu-id="6f79d-144">Le informazioni statistiche non vengono aggiornate in automatico.</span><span class="sxs-lookup"><span data-stu-id="6f79d-144">Statistics information is not updated automatically.</span></span> <span data-ttu-id="6f79d-145">Se si aggiornano dati hello in una tabella senza ricreare le statistiche di hello, causare un peggioramento delle prestazioni delle query hello.</span><span class="sxs-lookup"><span data-stu-id="6f79d-145">If you update hello data in a table without re-creating hello statistics, hello query performance might decline.</span></span>

### <a name="option-2-use-skewfactor"></a><span data-ttu-id="6f79d-146">Opzione 2. Utilizzo di SKEWFACTOR</span><span class="sxs-lookup"><span data-stu-id="6f79d-146">Option 2: Use SKEWFACTOR</span></span>

<span data-ttu-id="6f79d-147">Se si desidera tax hello toosum per ogni stato, è necessario utilizzare GROUP BY stato, un approccio che non evita il problema di dati inclinazione hello.</span><span class="sxs-lookup"><span data-stu-id="6f79d-147">If you want toosum hello tax for each state, you must use GROUP BY state, an approach that doesn't avoid hello data-skew problem.</span></span> <span data-ttu-id="6f79d-148">Tuttavia, è possibile fornire un suggerimento dati in tooidentify le query dati comportare un'asimmetria nelle chiavi in modo che query optimizer hello è possibile usare preparare un piano di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="6f79d-148">However, you can provide a data hint in your query tooidentify data skew in keys so that hello optimizer can prepare an execution plan for you.</span></span>

<span data-ttu-id="6f79d-149">In genere, è possibile impostare il parametro hello come 0,5 e 1, con 0,5, ovvero non molto inclinazione pesante significato inclinazione e 1.</span><span class="sxs-lookup"><span data-stu-id="6f79d-149">Usually, you can set hello parameter as 0.5 and 1, with 0.5 meaning not much skew and 1 meaning heavy skew.</span></span> <span data-ttu-id="6f79d-150">Poiché hint hello influisce sull'ottimizzazione del piano di esecuzione per l'istruzione corrente hello e tutte le istruzioni a valle, essere hint di hello tooadd assicurarsi prima di hello potenziali inclinata key-wise aggregazione.</span><span class="sxs-lookup"><span data-stu-id="6f79d-150">Because hello hint affects execution-plan optimization for hello current statement and all downstream statements, be sure tooadd hello hint before hello potential skewed key-wise aggregation.</span></span>

    SKEWFACTOR (columns) = x

    Provides a hint that hello given columns have a skew factor x from 0 (no skew) through 1 (very heavy skew).

<span data-ttu-id="6f79d-151">Esempio di codice:</span><span class="sxs-lookup"><span data-stu-id="6f79d-151">Code example:</span></span>

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

### <a name="option-3-use-rowcount"></a><span data-ttu-id="6f79d-152">Opzione 3: Usare ROWCOUNT</span><span class="sxs-lookup"><span data-stu-id="6f79d-152">Option 3: Use ROWCOUNT</span></span>  
<span data-ttu-id="6f79d-153">Inoltre, tooSKEWFACTOR per inclinare chiave specifica join casi, se si conosce tale hello altri set di righe unite in join è piccolo, è possibile che query optimizer hello aggiungendo un hint di conteggio delle righe nell'istruzione di hello U-SQL prima di JOIN.</span><span class="sxs-lookup"><span data-stu-id="6f79d-153">In addition tooSKEWFACTOR, for specific skewed-key join cases, if you know that hello other joined row set is small, you can tell hello optimizer by adding a ROWCOUNT hint in hello U-SQL statement before JOIN.</span></span> <span data-ttu-id="6f79d-154">In questo modo, query optimizer può scegliere un toohelp strategia di join di broadcast di migliorare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="6f79d-154">This way, optimizer can choose a broadcast join strategy toohelp improve performance.</span></span> <span data-ttu-id="6f79d-155">Tenere presente che ROWCOUNT non risolto hello inclinazione di dati, ma può offrire alcune informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="6f79d-155">Be aware that ROWCOUNT does not resolve hello data-skew problem, but it can offer some additional help.</span></span>

    OPTION(ROWCOUNT = n)

    Identify a small row set before JOIN by providing an estimated integer row count.

<span data-ttu-id="6f79d-156">Esempio di codice:</span><span class="sxs-lookup"><span data-stu-id="6f79d-156">Code example:</span></span>

    //Unstructured (24-hour daily log impressions)
    @Huge   = EXTRACT ClientId int, ...
                FROM @"wasb://ads@wcentralus/2015/10/30/{*}.nif"
                ;

    //Small subset (that is, ForgetMe opt out)
    @Small  = SELECT * FROM @Huge
                WHERE Bing.ForgetMe(x,y,z)
                OPTION(ROWCOUNT=500)
                ;

    //Result (not enough information toodetermine simple broadcast JOIN)
    @Remove = SELECT * FROM Bing.Sessions
                INNER JOIN @Small ON Sessions.Client == @Small.Client
                ;

## <a name="solution-3-improve-hello-user-defined-reducer-and-combiner"></a><span data-ttu-id="6f79d-157">Soluzione 3: Migliorare la funzione di combinazione e riduttore di hello definito dall'utente</span><span class="sxs-lookup"><span data-stu-id="6f79d-157">Solution 3: Improve hello user-defined reducer and combiner</span></span>

<span data-ttu-id="6f79d-158">In alcuni casi è possibile scrivere toodeal un operatore definito dall'utente con la logica di complessità del processo e un riduttore ben scritta e una funzione di combinazione potrebbe attenuare un problema di inclinazione di dati in alcuni casi.</span><span class="sxs-lookup"><span data-stu-id="6f79d-158">You can sometimes write a user-defined operator toodeal with complicated process logic, and a well-written reducer and combiner might mitigate a data-skew problem in some cases.</span></span>

### <a name="option-1-use-a-recursive-reducer-if-possible"></a><span data-ttu-id="6f79d-159">Opzione 1. Usare un riduttore ricorsivo se possibile</span><span class="sxs-lookup"><span data-stu-id="6f79d-159">Option 1: Use a recursive reducer, if possible</span></span>

<span data-ttu-id="6f79d-160">Per impostazione predefinita, un riduttore definito dall'utente viene eseguito in modalità non ricorsiva, ovvero il lavoro di riduzione per una chiave verrà distribuito su un unico vertice.</span><span class="sxs-lookup"><span data-stu-id="6f79d-160">By default, a user-defined reducer runs in non-recursive mode, which means that reduce work for a key is distributed into a single vertex.</span></span> <span data-ttu-id="6f79d-161">Ma se i dati sono distorti, hello set di dati di grandi dimensioni potrebbero essere elaborati in un singolo vertice ed eseguire per un lungo periodo.</span><span class="sxs-lookup"><span data-stu-id="6f79d-161">But if your data is skewed, hello huge data sets might be processed in a single vertex and run for a long time.</span></span>

<span data-ttu-id="6f79d-162">tooimprove prestazioni, è possibile aggiungere un attributo in toorun di riduttore toodefine il codice in modalità ricorsiva.</span><span class="sxs-lookup"><span data-stu-id="6f79d-162">tooimprove performance, you can add an attribute in your code toodefine reducer toorun in recursive mode.</span></span> <span data-ttu-id="6f79d-163">Set di dati di grandi dimensioni hello possono quindi essere vertici toomultiple distribuita e in parallelo, che consente di velocizzare il processo.</span><span class="sxs-lookup"><span data-stu-id="6f79d-163">Then, hello huge data sets can be distributed toomultiple vertices and run in parallel, which speeds up your job.</span></span>

<span data-ttu-id="6f79d-164">toochange un toorecursive riduttore non ricorsiva, è necessario assicurarsi che l'algoritmo è associativa toomake.</span><span class="sxs-lookup"><span data-stu-id="6f79d-164">toochange a non-recursive reducer toorecursive, you need toomake sure that your algorithm is associative.</span></span> <span data-ttu-id="6f79d-165">Ad esempio, somma hello è associativa e mediana hello non.</span><span class="sxs-lookup"><span data-stu-id="6f79d-165">For example, hello sum is associative, and hello median is not.</span></span> <span data-ttu-id="6f79d-166">È inoltre necessario assicurarsi che hello di input e output per riduttore mantenere hello toomake stesso schema.</span><span class="sxs-lookup"><span data-stu-id="6f79d-166">You also need toomake sure that hello input and output for reducer keep hello same schema.</span></span>

<span data-ttu-id="6f79d-167">Attributo del riduttore ricorsivo:</span><span class="sxs-lookup"><span data-stu-id="6f79d-167">Attribute of recursive reducer:</span></span>

    [SqlUserDefinedReducer(IsRecursive = true)]

<span data-ttu-id="6f79d-168">Esempio di codice:</span><span class="sxs-lookup"><span data-stu-id="6f79d-168">Code example:</span></span>

    [SqlUserDefinedReducer(IsRecursive = true)]
    public class TopNReducer : IReducer
    {
        public override IEnumerable<IRow>
            Reduce(IRowset input, IUpdatableRow output)
        {
            //Your reducer code goes here.
        }
    }

### <a name="option-2-use-row-level-combiner-mode-if-possible"></a><span data-ttu-id="6f79d-169">Opzione 2. Usare la modalità di combinazione a livello di riga, se possibile</span><span class="sxs-lookup"><span data-stu-id="6f79d-169">Option 2: Use row-level combiner mode, if possible</span></span>

<span data-ttu-id="6f79d-170">Modalità funzione di combinazione di hint ROWCOUNT toohello simile per i casi specifici join chiave asimmetrica, tenta di toodistribute valore chiave asimmetrica set toomultiple vertici in modo che il lavoro hello può essere eseguito contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="6f79d-170">Similar toohello ROWCOUNT hint for specific skewed-key join cases, combiner mode tries toodistribute huge skewed-key value sets toomultiple vertices so that hello work can be executed concurrently.</span></span> <span data-ttu-id="6f79d-171">La modalità del combinatore non può risolvere il problema dell'asimmetria dei dati, ma può offrire un aiuto aggiuntivo per set di valori di chiavi asimmetriche di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="6f79d-171">Combiner mode can’t resolve data-skew issues, but it can offer some additional help for huge skewed-key value sets.</span></span>

<span data-ttu-id="6f79d-172">Per impostazione predefinita, in modalità funzione di combinazione di hello è completo, ovvero hello lasciato set di righe e non possono essere separate set di righe di destra.</span><span class="sxs-lookup"><span data-stu-id="6f79d-172">By default, hello combiner mode is Full, which means that hello left row set and right row set cannot be separated.</span></span> <span data-ttu-id="6f79d-173">Impostazione della modalità di hello come sinistra/destra/interna consente il join a livello di riga.</span><span class="sxs-lookup"><span data-stu-id="6f79d-173">Setting hello mode as Left/Right/Inner enables row-level join.</span></span> <span data-ttu-id="6f79d-174">sistema Hello separa i set di righe corrispondente hello e li distribuisce in più vertici eseguiti in parallelo.</span><span class="sxs-lookup"><span data-stu-id="6f79d-174">hello system separates hello corresponding row sets and distributes them into multiple vertices that run in parallel.</span></span> <span data-ttu-id="6f79d-175">Tuttavia, prima di configurare la modalità di combinazione canali hello, prestare attenzione tooensure che hello corrispondente set di righe può essere separati.</span><span class="sxs-lookup"><span data-stu-id="6f79d-175">However, before you configure hello combiner mode, be careful tooensure that hello corresponding row sets can be separated.</span></span>

<span data-ttu-id="6f79d-176">Hello di esempio che segue viene illustrato un set di righe sinistro separati.</span><span class="sxs-lookup"><span data-stu-id="6f79d-176">hello example that follows shows a separated left row set.</span></span> <span data-ttu-id="6f79d-177">Ogni riga di output dipende da una singola riga di input da sinistra hello e potenzialmente dipende tutte le righe da hello destra con hello stesso valore della chiave.</span><span class="sxs-lookup"><span data-stu-id="6f79d-177">Each output row depends on a single input row from hello left, and it potentially depends on all rows from hello right with hello same key value.</span></span> <span data-ttu-id="6f79d-178">Se si imposta la modalità di combinazione canali hello come left, il sistema di hello separa hello enorme sinistra-set di righe in più piccole e li assegna toomultiple vertici.</span><span class="sxs-lookup"><span data-stu-id="6f79d-178">If you set hello combiner mode as left, hello system separates hello huge left-row set into small ones and assigns them toomultiple vertices.</span></span>

![Illustrazione della modalità del combinatore](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/combiner-mode-illustration.png)

>[!NOTE]
><span data-ttu-id="6f79d-180">Se si imposta la modalità di combinazione canali errato hello, combinazione di hello è meno efficiente e risultati hello potrebbero essere errati.</span><span class="sxs-lookup"><span data-stu-id="6f79d-180">If you set hello wrong combiner mode, hello combination is less efficient, and hello results might be wrong.</span></span>

<span data-ttu-id="6f79d-181">Attributi della modalità del combinatore:</span><span class="sxs-lookup"><span data-stu-id="6f79d-181">Attributes of combiner mode:</span></span>

- [SqlUserDefinedCombiner(Mode=CombinerMode.Full)]: Every output row potentially depends on all hello input rows from left and right with hello same key value.

- <span data-ttu-id="6f79d-182">SqlUserDefinedCombiner(Mode=CombinerMode.Left): Ogni riga di output dipende da una singola riga di input da sinistra hello (e potenzialmente tutte le righe da hello destra con hello stesso valore della chiave).</span><span class="sxs-lookup"><span data-stu-id="6f79d-182">SqlUserDefinedCombiner(Mode=CombinerMode.Left): Every output row depends on a single input row from hello left (and potentially all rows from hello right with hello same key value).</span></span>

- <span data-ttu-id="6f79d-183">qlUserDefinedCombiner(Mode=CombinerMode.Right): ogni riga di output dipende da una singola riga di input da hello destra (e potenzialmente tutte le righe da sinistra hello con hello stesso valore della chiave).</span><span class="sxs-lookup"><span data-stu-id="6f79d-183">qlUserDefinedCombiner(Mode=CombinerMode.Right): Every output row depends on a single input row from hello right (and potentially all rows from hello left with hello same key value).</span></span>

- <span data-ttu-id="6f79d-184">SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Ogni riga di output dipende da una singola riga di input da sinistra hello e hello destra con hello stesso valore.</span><span class="sxs-lookup"><span data-stu-id="6f79d-184">SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Every output row depends on a single input row from hello left and hello right with hello same value.</span></span>

<span data-ttu-id="6f79d-185">Esempio di codice:</span><span class="sxs-lookup"><span data-stu-id="6f79d-185">Code example:</span></span>

    [SqlUserDefinedCombiner(Mode = CombinerMode.Right)]
    public class WatsonDedupCombiner : ICombiner
    {
        public override IEnumerable<IRow>
            Combine(IRowset left, IRowset right, IUpdatableRow output)
        {
        //Your combiner code goes here.
        }
    }
