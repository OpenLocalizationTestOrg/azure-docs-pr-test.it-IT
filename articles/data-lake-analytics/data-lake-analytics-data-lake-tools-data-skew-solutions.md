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
# <a name="resolve-data-skew-problems-by-using-azure-data-lake-tools-for-visual-studio"></a>Risolvere i problemi di asimmetria dei dati tramite Strumenti Azure Data Lake per Visual Studio

## <a name="what-is-data-skew"></a>Informazioni sull'asimmetria dei dati

In poche parole, un'asimmetria dei dati si verifica quando un valore è rappresentato in modo eccessivo. Si supponga di avere assegnato 50 esaminatori tax tooaudit redditi, uno esaminatore per ogni stato degli Stati Uniti. Esaminatore Wyoming Hello, poiché sono popolamento hello è ridotto, ha toodo minimo. California, tuttavia, Esaminatore hello viene conservata occupati a causa della popolazione di grandi dimensioni hello dello stato.
    ![Esempio di un problema di asimmetria dei dati](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)

In questo scenario, dati hello non viene distribuiti tra esaminatori tax tutti, il che significa che alcune esaminatori devono funzionare più rispetto ad altri. Nel processo, spesso si verificano situazioni di questo esempio imposta examiner hello. In termini più tecnici, un vertice Ottiene molti più dati rispetto agli altri elementi, una situazione che rende il vertice hello più hello altri e che infine rallenta un intero processo di lavoro. Che cos'è peggiore, il processo di hello potrebbe non riuscire, poiché potrebbero avere vertici, ad esempio, un limite di 5 ore runtime e un limite di 6 GB di memoria.

## <a name="resolving-data-skew-problems"></a>Risoluzione dei problemi di asimmetria dei dati

Gli Strumenti Azure Data Lake per Visual Studio consentono di rilevare eventuali problemi di asimmetria dei dati all'interno dei processi. Se esiste un problema, è possibile risolverlo provando soluzioni hello in questa sezione.

## <a name="solution-1-improve-table-partitioning"></a>Soluzione 1. Migliorare il partizionamento delle tabelle

### <a name="option-1-filter-hello-skewed-key-value-in-advance"></a>Opzione 1: Hello filtro inclinata valore della chiave in anticipo

Se non si applica la logica di business, è possibile filtrare i valori di una frequenza maggiore hello in anticipo. Ad esempio, se sono presenti molti 000 000 000 nella colonna GUID, non è tooaggregate tale valore. Prima di aggregazione, è possibile scrivere "dove GUID!"000 000-000"=" valore di toofilter hello ad alta frequenza.

### <a name="option-2-pick-a-different-partition-or-distribution-key"></a>Opzione 2. Selezionare una chiave di partizione o distribuzione differente

In hello sopra riportato, se si desidera che il carico di lavoro di solo toocheck hello verifica fiscale tutti su hello paese, è possibile migliorare la distribuzione dei dati hello selezionando il numero di ID hello come chiave. Selezione di una partizione diversa o una chiave di distribuzione può talvolta distribuire dati hello più uniforme, ma è necessario assicurarsi che questa opzione non influisce sulla logica di business toomake. Ad esempio, somma di imposte hello toocalculate per ogni stato, è opportuno toodesignate _stato_ come chiave di partizione hello. Se si continua tooexperience questo problema, provare a utilizzare l'opzione 3.

### <a name="option-3-add-more-partition-or-distribution-keys"></a>Opzione 3. Aggiungere più chiavi di partizione o distribuzione

Invece di usare solo _Stato_ come chiave di partizione, è possibile impiegare più di una chiave per il partizionamento. Ad esempio, si consiglia di aggiungere _CAP_ come una partizione aggiuntiva chiave tooreduce-partizione di dati di dimensioni e distribuire dati hello più uniforme.

### <a name="option-4-use-round-robin-distribution"></a>Opzione 4. Usare la distribuzione round robin

Se è possibile trovare una chiave appropriata per la partizione e la distribuzione, è possibile provare distribuzione round-robin toouse. La distribuzione round robin considera tutte le righe in modo uguale e le inserisce in modo casuale nei bucket corrispondenti. dati di Hello Ottiene distribuiti uniformemente, ma perde le informazioni di località, uno svantaggio che consente inoltre di ridurre le prestazioni per alcune operazioni. Inoltre, se si esegue l'aggregazione per la chiave asimmetrica hello comunque, problema dati inclinazione hello verrà mantenute. toolearn ulteriori informazioni su distribuzione round-robin, vedere le distribuzioni di tabella U-SQL hello sezione [CREATE TABLE (U-SQL): creazione di una tabella con Schema](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).

## <a name="solution-2-improve-hello-query-plan"></a>Soluzione 2: Migliorare il piano di query di hello

### <a name="option-1-use-hello-create-statistics-statement"></a>Opzione 1: Utilizzare l'istruzione CREATE STATISTICS hello

U-SQL fornisce l'istruzione CREATE STATISTICS hello nelle tabelle. Questa istruzione offre toohello query optimizer di ulteriori informazioni sulle hello dati caratteristiche, ad esempio la distribuzione di valore, che sono archiviati in una tabella. Per la maggior parte delle query, hello query optimizer genera già le statistiche necessarie per un piano di query di alta qualità hello. In alcuni casi, potrebbe essere necessario tooimprove le prestazioni delle query creando statistiche aggiuntive con CREATE STATISTICS o modificando la progettazione di query hello. Per ulteriori informazioni, vedere hello [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) pagina.

Esempio di codice:

    CREATE STATISTICS IF NOT EXISTS stats_SampleTable_date ON SampleDB.dbo.SampleTable(date) WITH FULLSCAN;

>[!NOTE]
>Le informazioni statistiche non vengono aggiornate in automatico. Se si aggiornano dati hello in una tabella senza ricreare le statistiche di hello, causare un peggioramento delle prestazioni delle query hello.

### <a name="option-2-use-skewfactor"></a>Opzione 2. Utilizzo di SKEWFACTOR

Se si desidera tax hello toosum per ogni stato, è necessario utilizzare GROUP BY stato, un approccio che non evita il problema di dati inclinazione hello. Tuttavia, è possibile fornire un suggerimento dati in tooidentify le query dati comportare un'asimmetria nelle chiavi in modo che query optimizer hello è possibile usare preparare un piano di esecuzione.

In genere, è possibile impostare il parametro hello come 0,5 e 1, con 0,5, ovvero non molto inclinazione pesante significato inclinazione e 1. Poiché hint hello influisce sull'ottimizzazione del piano di esecuzione per l'istruzione corrente hello e tutte le istruzioni a valle, essere hint di hello tooadd assicurarsi prima di hello potenziali inclinata key-wise aggregazione.

    SKEWFACTOR (columns) = x

    Provides a hint that hello given columns have a skew factor x from 0 (no skew) through 1 (very heavy skew).

Esempio di codice:

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

### <a name="option-3-use-rowcount"></a>Opzione 3: Usare ROWCOUNT  
Inoltre, tooSKEWFACTOR per inclinare chiave specifica join casi, se si conosce tale hello altri set di righe unite in join è piccolo, è possibile che query optimizer hello aggiungendo un hint di conteggio delle righe nell'istruzione di hello U-SQL prima di JOIN. In questo modo, query optimizer può scegliere un toohelp strategia di join di broadcast di migliorare le prestazioni. Tenere presente che ROWCOUNT non risolto hello inclinazione di dati, ma può offrire alcune informazioni aggiuntive.

    OPTION(ROWCOUNT = n)

    Identify a small row set before JOIN by providing an estimated integer row count.

Esempio di codice:

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

## <a name="solution-3-improve-hello-user-defined-reducer-and-combiner"></a>Soluzione 3: Migliorare la funzione di combinazione e riduttore di hello definito dall'utente

In alcuni casi è possibile scrivere toodeal un operatore definito dall'utente con la logica di complessità del processo e un riduttore ben scritta e una funzione di combinazione potrebbe attenuare un problema di inclinazione di dati in alcuni casi.

### <a name="option-1-use-a-recursive-reducer-if-possible"></a>Opzione 1. Usare un riduttore ricorsivo se possibile

Per impostazione predefinita, un riduttore definito dall'utente viene eseguito in modalità non ricorsiva, ovvero il lavoro di riduzione per una chiave verrà distribuito su un unico vertice. Ma se i dati sono distorti, hello set di dati di grandi dimensioni potrebbero essere elaborati in un singolo vertice ed eseguire per un lungo periodo.

tooimprove prestazioni, è possibile aggiungere un attributo in toorun di riduttore toodefine il codice in modalità ricorsiva. Set di dati di grandi dimensioni hello possono quindi essere vertici toomultiple distribuita e in parallelo, che consente di velocizzare il processo.

toochange un toorecursive riduttore non ricorsiva, è necessario assicurarsi che l'algoritmo è associativa toomake. Ad esempio, somma hello è associativa e mediana hello non. È inoltre necessario assicurarsi che hello di input e output per riduttore mantenere hello toomake stesso schema.

Attributo del riduttore ricorsivo:

    [SqlUserDefinedReducer(IsRecursive = true)]

Esempio di codice:

    [SqlUserDefinedReducer(IsRecursive = true)]
    public class TopNReducer : IReducer
    {
        public override IEnumerable<IRow>
            Reduce(IRowset input, IUpdatableRow output)
        {
            //Your reducer code goes here.
        }
    }

### <a name="option-2-use-row-level-combiner-mode-if-possible"></a>Opzione 2. Usare la modalità di combinazione a livello di riga, se possibile

Modalità funzione di combinazione di hint ROWCOUNT toohello simile per i casi specifici join chiave asimmetrica, tenta di toodistribute valore chiave asimmetrica set toomultiple vertici in modo che il lavoro hello può essere eseguito contemporaneamente. La modalità del combinatore non può risolvere il problema dell'asimmetria dei dati, ma può offrire un aiuto aggiuntivo per set di valori di chiavi asimmetriche di grandi dimensioni.

Per impostazione predefinita, in modalità funzione di combinazione di hello è completo, ovvero hello lasciato set di righe e non possono essere separate set di righe di destra. Impostazione della modalità di hello come sinistra/destra/interna consente il join a livello di riga. sistema Hello separa i set di righe corrispondente hello e li distribuisce in più vertici eseguiti in parallelo. Tuttavia, prima di configurare la modalità di combinazione canali hello, prestare attenzione tooensure che hello corrispondente set di righe può essere separati.

Hello di esempio che segue viene illustrato un set di righe sinistro separati. Ogni riga di output dipende da una singola riga di input da sinistra hello e potenzialmente dipende tutte le righe da hello destra con hello stesso valore della chiave. Se si imposta la modalità di combinazione canali hello come left, il sistema di hello separa hello enorme sinistra-set di righe in più piccole e li assegna toomultiple vertici.

![Illustrazione della modalità del combinatore](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/combiner-mode-illustration.png)

>[!NOTE]
>Se si imposta la modalità di combinazione canali errato hello, combinazione di hello è meno efficiente e risultati hello potrebbero essere errati.

Attributi della modalità del combinatore:

- [SqlUserDefinedCombiner(Mode=CombinerMode.Full)]: Every output row potentially depends on all hello input rows from left and right with hello same key value.

- SqlUserDefinedCombiner(Mode=CombinerMode.Left): Ogni riga di output dipende da una singola riga di input da sinistra hello (e potenzialmente tutte le righe da hello destra con hello stesso valore della chiave).

- qlUserDefinedCombiner(Mode=CombinerMode.Right): ogni riga di output dipende da una singola riga di input da hello destra (e potenzialmente tutte le righe da sinistra hello con hello stesso valore della chiave).

- SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Ogni riga di output dipende da una singola riga di input da sinistra hello e hello destra con hello stesso valore.

Esempio di codice:

    [SqlUserDefinedCombiner(Mode = CombinerMode.Right)]
    public class WatsonDedupCombiner : ICombiner
    {
        public override IEnumerable<IRow>
            Combine(IRowset left, IRowset right, IUpdatableRow output)
        {
        //Your combiner code goes here.
        }
    }
