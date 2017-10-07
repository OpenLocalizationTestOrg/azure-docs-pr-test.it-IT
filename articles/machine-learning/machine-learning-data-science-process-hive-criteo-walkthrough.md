---
title: Processo di analisi scientifica dei dati di Team Ciao azione - utilizzando un Cluster di Azure HDInsight Hadoop in un set di dati di 1 TB | Documenti Microsoft
description: Utilizzando hello Team processo di analisi scientifica dei dati per uno scenario end-to-end che utilizza un HDInsight Hadoop toobuild del cluster e distribuire un modello usando un set di dati disponibili pubblicamente (1 TB) grandi dimensioni
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 72d958c4-3205-49b9-ad82-47998d400d2b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 59b2af02e7840cb60a4b5b2f2c8ab0611df198ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action---using-an-azure-hdinsight-hadoop-cluster-on-a-1-tb-dataset"></a>Processo di analisi scientifica dei dati di Team Ciao azione - utilizzando un Cluster di Azure HDInsight Hadoop in un set di dati di 1 TB

In questa procedura dettagliata viene descritto come usare hello Team processo di analisi scientifica dei dati in uno scenario end-to-end con un [cluster Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/) toostore, esplorare, funzionalità tecnico e verso il basso di dati di esempio da uno dei hello pubblicamente disponibile [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) set di dati. Utilizziamo Azure Machine Learning toobuild un modello di classificazione binaria per i dati. Vengono inoltre illustrati come toopublish uno di questi modelli come servizio Web.

È inoltre possibile toouse un'attività di hello IPython notebook tooaccomplish presentati in questa procedura dettagliata. Gli utenti che sarebbero ad esempio tootry deve consultare questo approccio hello [procedura dettagliata Criteo utilizzando una connessione ODBC Hive](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) argomento.

## <a name="dataset"></a>Descrizione del set di dati Criteo
Hello Criteo dati sono un set di stima fare clic su dati che è di circa 370GB dei file TSV compresso gzip (~1.3TB non compressi), che comprendono più 4.3 miliardi di record. I valori sono ottenuti da 24 giorni di dati sui clic resi disponibili da [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/). Per praticità hello di esperti di dati, è stato decompresso dati tooexperiment toous disponibile con.

Ogni record nel set di dati contiene 40 colonne:

* Hello prima colonna è una colonna di etichetta che indica se un utente fa clic su un **aggiungere** (valore 1) o non fare clic su uno (valore 0)
* le successive 13 colonne sono di tipo numerico
* le ultime 26 colonne sono di tipo categorico

colonne di Hello sono rese anonime e utilizzare una serie di nomi enumerati: "Col1" (per la colonna di etichetta hello) troppo ' Col40 "(per la colonna categorica ultimo hello).            

Di seguito è un estratto di hello innanzitutto 20 colonne di due osservazioni (righe) da questo set di dati:

    Col1    Col2    Col3    Col4    Col5    Col6    Col7    Col8    Col9    Col10    Col11    Col12    Col13    Col14    Col15            Col16            Col17            Col18            Col19        Col20

    0       40      42      2       54      3       0       0       2       16      0       1       4448    4       1acfe1ee        1b2ff61f        2e8b2631        6faef306        c6fc10d3    6fcd6dcb           
    0               24              27      5               0       2       1               3       10064           9a8cb066        7a06385f        417e6103        2170fc56        acf676aa    6fcd6dcb                      

Sono presenti valori mancanti in entrambe le colonne numeriche e categorico hello in questo set di dati. Viene descritto un metodo semplice per la gestione dei valori mancanti hello. Dettagli aggiuntivi su dati hello vengono esaminati quando è archiviarli in tabelle Hive.

**Definizione di:** *frequenza click-through (CTRL):* è hello percentuale di clic nei dati hello. In questo set di dati, Criteo hello CTR è circa 3.3% o 0.033.

## <a name="mltasks"></a>Esempi di attività di stima
Questa procedura dettagliata illustra due problemi di stima di esempio:

1. **Classificazione binaria**: stima se un utente ha fatto clic su un annuncio:
   
   * Classe 0: nessun clic
   * Classe 1: clic
2. **Regressione**: stima delle probabilità hello un fare clic su Active Directory dalla funzionalità dell'utente.

## <a name="setup"></a>Configurare un cluster Hadoop di HDInsight per l'analisi scientifica
**Nota:** in genere, questa attività viene svolta da un **amministratore**.

Per configurare l'ambiente di analisi scientifica dei dati di Azure per la creazione di soluzioni di analisi predittiva con i cluster HDInsight, sono necessari tre passaggi:

1. [Creare un account di archiviazione](../storage/common/storage-create-storage-account.md): questo account di archiviazione è toostore utilizzati dati nell'archiviazione Blob di Azure. Hello utilizzato nel cluster HDInsight vengono archiviati qui.
2. [Personalizzare i cluster Hadoop di Azure HDInsight per l'analisi scientifica dei dati](machine-learning-data-science-customize-hadoop-cluster.md): questo passaggio consente di creare un cluster Hadoop di Azure HDInsight con la versione a 64 bit di Anaconda Python 2.7 installata in tutti i nodi. Esistono due toocomplete passaggi importanti (descritti in questo argomento) per la personalizzazione del cluster HDInsight hello.
   
   * È necessario collegare l'account di archiviazione hello creato nel passaggio 1 con il cluster HDInsight quando viene creato. Questo account di archiviazione viene utilizzato per accedere ai dati che possono essere elaborati all'interno di cluster hello.
   * È necessario abilitare nodo head toohello di accesso remoto del cluster hello dopo averlo creato. Memorizza le credenziali di accesso remoto hello è possibile specificare (diverse da quelle specificate per il cluster hello al momento della relativa creazione): sono necessari toocomplete hello procedure seguenti.
3. [Creare un'area di lavoro di Azure ML](machine-learning-create-workspace.md): area di lavoro questo Azure Machine Learning è utilizzata per la creazione di modelli di machine learning dopo un'esplorazione dei dati iniziali e campionamento nel cluster HDInsight hello verso il basso.

## <a name="getdata"></a>Ottenere e utilizzare i dati da un'origine pubblica
Hello [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) set di dati è possibile accedere facendo clic sul collegamento hello, accettazione hello condizioni d'uso e fornire un nome. Ecco uno snapshot di come appare:

![Accettazione delle condizioni Criteo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/hLxfI2E.png)

Fare clic su **continua tooDownload** tooread informazioni sul set di dati hello e la relativa disponibilità.

Hello dati risiedono in un pubblico [archiviazione blob di Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) percorso: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/. "wasb" Hello fa riferimento il percorso di archiviazione Blob di tooAzure. 

1. dati Hello in questa risorsa di archiviazione blob pubblico è costituito da tre sottocartelle della cartella dati.
   
   1. Hello sottocartella *non elaborati/count/* contiene hello prima 21 giorni di dati, dal giorno\_tooday 00\_20
   2. Hello sottocartella *non elaborati/train/* è costituito da un solo giorno della data, giorno\_21
   3. Hello sottocartella *non elaborati/test/* è costituito da due giorni di dati, giorno\_22 e giorno\_23
2. Per gli utenti che desiderano toostart con dati non elaborati gzip hello, questi sono anche disponibili nella cartella principale hello *non elaborati /* come day_NN.gz, in cui NN va da too23 00.

Tooaccess un approccio alternativo, esplorare e modellare i dati che non richiedono alcun download locale è illustrato più avanti in questa procedura dettagliata, quando si creano tabelle Hive.

## <a name="login"></a>Accedere al nodo head del cluster toohello
nel nodo head toohello hello del cluster di, utilizzare hello toolog [portale di Azure](https://ms.portal.azure.com) cluster hello toolocate. Fare clic sull'icona di elephant HDInsight hello in hello a sinistra e quindi fare doppio clic sul nome di hello del cluster. Passare toohello **configurazione** scheda, fare doppio clic sull'icona CONNETTI hello nella parte inferiore di hello della pagina hello e immettere le credenziali di accesso remoto quando richiesto. Consente di procedere toohello nodo head del cluster di hello.

Ecco come appare un tipico primo log nel nodo head del cluster toohello:

![Accedi toocluster](./media/machine-learning-data-science-process-hive-criteo-walkthrough/Yys9Vvm.png)

A sinistra di hello, vediamo hello "Hadoop riga di comando", ovvero il componente di base per l'esplorazione dei dati di hello. Sono inoltre disponibili due utili URL, "Hadoop Yarn Status" e "Hadoop Name Node". URL di Hello yarn stato Mostra lo stato del processo e l'URL del nodo nome hello fornisce informazioni dettagliate sulla configurazione del cluster hello.

Ora è vengono impostate e pronto toobegin prima parte della procedura dettagliata hello: l'esplorazione dei dati utilizzando Hive e recupero di dati pronti per Azure Machine Learning.

## <a name="hive-db-tables"></a> Creare il database e le tabelle Hive
toocreate Hive tabelle per il set di dati Criteo, aprire hello ***della riga di comando Hadoop*** hello desktop del nodo head hello e immettere una directory di Hive hello immettendo il comando hello

    cd %hive_home%\bin

> [!NOTE]
> Eseguire tutti i comandi di Hive in questa procedura dettagliata da bin Hive hello / prompt dei comandi. In questo modo, eventuali problemi di percorso vengono risolti automaticamente. Vengono utilizzati termini hello "Hive prompt dei comandi", "bin Hive / prompt dei comandi", "riga di comando Hadoop" e in modo intercambiabile.
> 
> [!NOTE]
> tooexecute qualsiasi query Hive, è possibile utilizzare sempre hello seguenti comandi:
> 
> 

        cd %hive_home%\bin
        hive

Dopo aver hello REPL Hive viene visualizzato con una "hive >" firmare, tagliare e incollare tooexecute query hello è.

Hello codice seguente viene creato un database "criteo" e quindi genera l'errore 4 tabelle:

* un *tabella per la generazione di conteggi* compilato giorno giorni\_tooday 00\_20,
* un *tabella per l'utilizzo come set di dati di training hello* compilato giorno\_21, e
* due *set di dati di test di tabelle per l'utilizzo come hello* compilato giorno\_22 e giorno\_23 rispettivamente.

Il set di dati di test verranno suddivise in due tabelle diverse perché uno dei giorni hello è un giorno festivo e vogliamo toodetermine se il modello di hello in grado di rilevare le differenze tra un giorno festivo e lavorativi dalla frequenza di hello click-through.

Hello script [hive esempio &#95; &#95; creare &#95; criteo &#95; database &#95; e &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) viene visualizzato di seguito per praticità:

    CREATE DATABASE IF NOT EXISTS criteo;
    DROP TABLE IF EXISTS criteo.criteo_count;
    CREATE TABLE criteo.criteo_count (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/count';

    DROP TABLE IF EXISTS criteo.criteo_train;
    CREATE TABLE criteo.criteo_train (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/train';

    DROP TABLE IF EXISTS criteo.criteo_test_day_22;
    CREATE TABLE criteo.criteo_test_day_22 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_22';

    DROP TABLE IF EXISTS criteo.criteo_test_day_23;
    CREATE TABLE criteo.criteo_test_day_23 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_23';

È possibile notare che tutte queste tabelle sono esterne come abbiamo punto tooAzure semplicemente i percorsi di archiviazione Blob (wasb).

**Esistono due modi tooexecute Hive qualsiasi query che è importante tenere presente questo punto.**

1. **Utilizzo di hello Hive REPL della riga di comando**: hello prima di tutto è tooissue un comando "hive" e copiare e incollare una query alla hello Hive REPL della riga di comando. toodo questo, eseguire:
   
        cd %hive_home%\bin
        hive
   
     Ora in hello REPL della riga di comando, tagliare e incollare la query hello viene eseguito.
2. **Salvare una query tooa file ed eseguendo il comando di hello**: hello è secondo file di toosave hello query tooa .hql ([hive esempio &#95; &#95; creare &#95; criteo &#95; database &#95; e &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) e quindi segue hello problema comando query hello tooexecute:
   
        hive -f C:\temp\sample_hive_create_criteo_database_and_tables.hql

### <a name="confirm-database-and-table-creation"></a>Verificare la creazione del database e della tabella
Successivamente, si conferma hello creazione database hello con hello comando seguente da bin Hive hello / prompt dei comandi:

        hive -e "show databases;"

Il risultato è il seguente:

        criteo
        default
        Time taken: 1.25 seconds, Fetched: 2 row(s)

Questo errore conferma la creazione di hello del nuovo database hello, "criteo".

toosee le tabelle create, è sufficiente eseguire hello comando qui dal bin Hive hello / prompt dei comandi:

        hive -e "show tables in criteo;"

Verrà quindi visualizzato hello seguente output:

        criteo_count
        criteo_test_day_22
        criteo_test_day_23
        criteo_train
        Time taken: 1.437 seconds, Fetched: 4 row(s)

## <a name="exploration"></a> Esplorazione dei dati in Hive
È ora pronto toodo alcune attività di esplorazione di dati di base nell'Hive. È iniziare contando il numero di hello di esempi di training hello e tabelle di dati di test.

### <a name="number-of-train-examples"></a>Numero di esempi di training
contenuto di Hello [esempio &#95; hive &#95; conteggio &#95; train &#95; tabella &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) riportati di seguito:

        SELECT COUNT(*) FROM criteo.criteo_train;

Il risultato è il seguente:

        192215183
        Time taken: 264.154 seconds, Fetched: 1 row(s)

In alternativa, uno può anche rilasciare hello comando seguente da bin Hive hello / prompt dei comandi:

        hive -f C:\temp\sample_hive_count_criteo_train_table_examples.hql

### <a name="number-of-test-examples-in-hello-two-test-datasets"></a>Numero di esempi di test nei set di dati di hello due test
È ora possibile contare il numero di hello di esempi in hello due set di dati di test. contenuto di Hello [esempio &#95; hive &#95; conteggio &#95; criteo &#95; test &#95; giorno &#95; 22 &#95; tabella &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) in questa sezione sono:

        SELECT COUNT(*) FROM criteo.criteo_test_day_22;

Il risultato è il seguente:

        189747893
        Time taken: 267.968 seconds, Fetched: 1 row(s)

Come al solito, si potrebbe chiamare script hello da bin Hive hello / directory prompt dei comandi eseguendo il comando hello:

        hive -f C:\temp\sample_hive_count_criteo_test_day_22_table_examples.hql

Infine, verrà esaminato il numero di hello degli esempi di test nel set di dati di test hello in base a giorno\_23.

Hello toodo comando tratta toohello simile uno riportata solo (vedere troppo[esempio &#95; hive &#95; conteggio &#95; criteo &#95; test &#95; giorno &#95; 23 &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):

        SELECT COUNT(*) FROM criteo.criteo_test_day_23;

Il risultato è il seguente:

        178274637
        Time taken: 253.089 seconds, Fetched: 1 row(s)

### <a name="label-distribution-in-hello-train-dataset"></a>Etichetta distribuzione hello training set di dati
distribuzione di etichetta Hello hello training set di dati è di particolare interesse. toosee, si visualizza contenuto [esempio &#95; hive &#95; criteo &#95; etichetta &#95; distribuzione &#95; train &#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):

        SELECT Col1, COUNT(*) AS CT FROM criteo.criteo_train GROUP BY Col1;

Ciò produce una distribuzione etichetta hello:

        1       6292903
        0       185922280
        Time taken: 459.435 seconds, Fetched: 2 row(s)

Si noti che la percentuale hello delle etichette positivo 3.3% circa (coerente con set di dati originale hello).

### <a name="histogram-distributions-of-some-numeric-variables-in-hello-train-dataset"></a>Le distribuzioni di istogramma di alcune variabili numeriche in hello training set di dati
È possibile utilizzare nativo Hive "istogramma\_numerico" funzione toofind out è simile a quali distribuzione hello di variabili numeriche hello. Di seguito sono contenuti hello di [esempio &#95; hive &#95; criteo &#95; istogramma &#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):

        SELECT CAST(hist.x as int) as bin_center, CAST(hist.y as bigint) as bin_height FROM
            (SELECT
            histogram_numeric(col2, 20) as col2_hist
            FROM
            criteo.criteo_train
            ) a
            LATERAL VIEW explode(col2_hist) exploded_table as hist;

In tal modo si ottiene seguente hello:

        26      155878415
        2606    92753
        6755    22086
        11202   6922
        14432   4163
        17815   2488
        21072   1901
        24113   1283
        27429   1225
        30818   906
        34512   723
        38026   387
        41007   290
        43417   312
        45797   571
        49819   428
        53505   328
        56853   527
        61004   160
        65510   3446
        Time taken: 317.851 seconds, Fetched: 20 row(s)

Hello laterale visualizzazione: esplosione di combinazione di Hive funge da tooproduce un output simile a SQL anziché elenco normale hello. Si noti che in hello questa tabella, la prima colonna hello corrisponde toohello bin center e hello secondo toohello bin frequenza.

### <a name="approximate-percentiles-of-some-numeric-variables-in-hello-train-dataset"></a>Set di dati di training percentili approssimativi di alcune variabili numeriche in hello
È inoltre calcolo hello di percentili approssimativi di interesse con variabili numeriche. A tale scopo, è disponibile la funzione "percentile\_approx" nativa di Hive. contenuto di Hello [esempio &#95; hive &#95; criteo &#95; approssimativo &#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) sono:

        SELECT MIN(Col2) AS Col2_min, PERCENTILE_APPROX(Col2, 0.1) AS Col2_01, PERCENTILE_APPROX(Col2, 0.3) AS Col2_03, PERCENTILE_APPROX(Col2, 0.5) AS Col2_median, PERCENTILE_APPROX(Col2, 0.8) AS Col2_08, MAX(Col2) AS Col2_max FROM criteo.criteo_train;

Il risultato è il seguente:

        1.0     2.1418600917169246      2.1418600917169246    6.21887086390288 27.53454893115633       65535.0
        Time taken: 564.953 seconds, Fetched: 1 row(s)

Abbiamo commento che la distribuzione di hello del percentili è in genere toohello strettamente correlati istogramma distribuzione di qualsiasi variabile numerica.         

### <a name="find-number-of-unique-values-for-some-categorical-columns-in-hello-train-dataset"></a>Trovare il numero di valori univoci per alcune colonne categoriche in hello training set di dati
Continuare l'esplorazione dei dati hello, sono ora disponibili, per alcune colonne di categoria, il numero di hello di valori univoci che accettano. toodo, si visualizza contenuto [esempio &#95; hive &#95; criteo &#95; univoco &#95; valori &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):

        SELECT COUNT(DISTINCT(Col15)) AS num_uniques FROM criteo.criteo_train;

Il risultato è il seguente:

        19011825
        Time taken: 448.116 seconds, Fetched: 1 row(s)

Si noti che Col15 ha 19 milioni di valori univoci. Utilizzando le tecniche di naïve come "hot una codifica" tooencode tali variabili di categoria elevata dimensionalità non è applicabile. In particolare, viene spiegata e illustrata una tecnica avanzata e affidabile di [apprendimento in base ai conteggi](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) per affrontare il problema in modo efficiente.

Questa sottosezione è terminare analizzando hello numero di valori univoci per alcune altre colonne categoriche anche. Hello contenuto di [esempio &#95; hive &#95; criteo &#95; univoco &#95; valori &#95; più &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) sono:

        SELECT COUNT(DISTINCT(Col16)), COUNT(DISTINCT(Col17)),
        COUNT(DISTINCT(Col18), COUNT(DISTINCT(Col19), COUNT(DISTINCT(Col20))
        FROM criteo.criteo_train;

Il risultato è il seguente:

        30935   15200   7349    20067   3
        Time taken: 1933.883 seconds, Fetched: 1 row(s)

Nuovo vediamo che ad eccezione di Col20, tutti hello altre colonne hanno molti valori univoci.

### <a name="co-occurrence-counts-of-pairs-of-categorical-variables-in-hello-train-dataset"></a>Conteggi di CO-occorrenza delle coppie di variabili di categoria nelle hello training set di dati

conteggi di CO-occorrenza Hello delle coppie di variabili di categoria è anche di interesse. Ciò può essere determinato mediante il codice hello in [esempio &#95; hive &#95; criteo &#95; abbinata &#95; categorico &#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):

        SELECT Col15, Col16, COUNT(*) AS paired_count FROM criteo.criteo_train GROUP BY Col15, Col16 ORDER BY paired_count DESC LIMIT 15;

Abbiamo invertire l'ordine hello conteggi da tali eventi ed esaminare in questo caso superiore hello 15. Il risultato è il seguente:

        ad98e872        cea68cd3        8964458
        ad98e872        3dbb483e        8444762
        ad98e872        43ced263        3082503
        ad98e872        420acc05        2694489
        ad98e872        ac4c5591        2559535
        ad98e872        fb1e95da        2227216
        ad98e872        8af1edc8        1794955
        ad98e872        e56937ee        1643550
        ad98e872        d1fade1c        1348719
        ad98e872        977b4431        1115528
        e5f3fd8d        a15d1051        959252
        ad98e872        dd86c04a        872975
        349b3fec        a52ef97d        821062
        e5f3fd8d        a0aaffa6        792250
        265366bf        6f5c7c41        782142
        Time taken: 560.22 seconds, Fetched: 15 row(s)

## <a name="downsample"></a>Verso il basso il set di dati di esempio hello per Azure Machine Learning
Con i set di dati di consentirne hello e illustrato come è possibile eseguire questo tipo di esplorazione per eventuali variabili (incluse le combinazioni), è ora verso il basso il set di dati di esempio hello in modo che è possibile compilare modelli in Azure Machine Learning. Tenere presente è il problema di hello ci concentreremo invece sui: dato un set di attributi di esempio (i valori delle funzionalità da Col2 - Col40), è stimare se Col1 è 0 (nessun clic) o 1 (fare clic).

toodown campionare il training e di test % too1 set di dati della dimensione originale hello, utilizziamo funzione RAND () nativa Hive. passare allo script successivo, Hello [esempio &#95; hive &#95; criteo &#95; sottocampionamento &#95; train &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) esegue questa operazione per hello training set di dati:

        CREATE TABLE criteo.criteo_train_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        ---Now downsample and store in this table

        INSERT OVERWRITE TABLE criteo.criteo_train_downsample_1perc SELECT * FROM criteo.criteo_train WHERE RAND() <= 0.01;

Il risultato è il seguente:

        Time taken: 12.22 seconds
        Time taken: 298.98 seconds

Hello script [esempio &#95; hive &#95; criteo &#95; sottocampionamento &#95; test &#95; giorno &#95; 22 &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) non è per i dati di test, giorno\_22:

        --- Now for test data (day_22)

        CREATE TABLE criteo.criteo_test_day_22_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_22_downsample_1perc SELECT * FROM criteo.criteo_test_day_22 WHERE RAND() <= 0.01;

Il risultato è il seguente:

        Time taken: 1.22 seconds
        Time taken: 317.66 seconds


Infine, hello script [esempio &#95; hive &#95; criteo &#95; sottocampionamento &#95; test &#95; giorno &#95; 23 &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) non è per i dati di test, giorno\_23:

        --- Finally test data day_23
        CREATE TABLE criteo.criteo_test_day_23_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 srical feature; tring)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_23_downsample_1perc SELECT * FROM criteo.criteo_test_day_23 WHERE RAND() <= 0.01;

Il risultato è il seguente:

        Time taken: 1.86 seconds
        Time taken: 300.02 seconds

Con questo siamo toouse pronto campionato il nostro giù eseguire il training e set di dati per la creazione di modelli in Azure Machine Learning di test.

È un componente importante finale prima di proseguire tooAzure Machine Learning, che è una tabella di conteggio hello problemi. Nella sottosezione successiva hello, questa operazione, illustrati in maggior dettaglio.

## <a name="count"></a>Una breve descrizione nella tabella di conteggio hello
Come è stato visto, diverse variabili categoriche hanno una dimensionalità molto elevata. In questa procedura dettagliata, è presente una tecnica potente denominata [Learning con conteggi](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) tooencode queste variabili in modo efficiente e affidabile. Ulteriori informazioni su questa tecnica sono hello collegamento fornito.

[!NOTE]
>In questa procedura dettagliata, esaminato l'utilizzo di rappresentazioni compact tooproduce tabelle di conteggio di funzioni categoriche elevata dimensionalità. Non si tratta hello solo modo tooencode funzioni categoriche; Per ulteriori informazioni sulle tecniche di altri utenti interessati possono estrarre [uno-a caldo-encoding](http://en.wikipedia.org/wiki/One-hot) e [feature hashing](http://en.wikipedia.org/wiki/Feature_hashing).
>

tabelle di conteggio toobuild sui dati di conteggio hello, utilizziamo dati hello hello raw/numero di cartelle. Nella sezione di modellazione illustrare agli utenti di hello come toobuild queste funzioni conteggiano tabelle per le funzionalità categoriche da zero o, in alternativa, toouse una tabella di conteggio preesistente per le esplorazioni. In cosa indicato di seguito, quando si fa riferimento troppo "pre-creato le tabelle di conteggio", si intende l'utilizzo di tabelle di conteggio hello fornito da Microsoft. Istruzioni dettagliate su come tooaccess queste tabelle vengono fornite nella sezione successiva hello.

## <a name="aml"></a> Creare un modello con Azure Machine Learning
Il processo di creazione di un modello in Azure Machine Learning prevede i passaggi seguenti:

1. [Ottenere dati hello dalle tabelle di Hive in Azure Machine Learning](#step1)
2. [Creare l'esperimento hello: pulire dati hello e trasformare con le tabelle di conteggio](#step2)
3. [Compilazione, eseguire il training e il modello di punteggio hello](#step3)
4. [Valutazione del modello di hello](#step4)
5. [Pubblicare il modello di hello come un servizio web](#step5)

Ora siamo modelli toobuild pronto in Azure Machine Learning studio. I dati campionati verso il basso viene salvati come tabelle Hive nel cluster hello. Utilizziamo hello Azure Machine Learning **l'importazione dei dati** modulo tooread questi dati. Hello credenziali tooaccess hello account di archiviazione del cluster, vedere di seguito.

### <a name="step1"></a>Passaggio 1: Ottenere dati da tabelle Hive in Azure Machine Learning usando il modulo di importazione dei dati hello e selezionarla per un esperimento di machine learning
Per iniziare, selezionare **+NEW** -> **EXPERIMENT** -> **Blank Experiment** (+NUOVO -> ESPERIMENTO -> Esperimento vuoto). Quindi, dalla hello **ricerca** casella hello in alto a sinistra, cercare "Importazione di dati". Trascinamento della selezione hello **l'importazione dei dati** modulo nel modulo toohello esperimento canvas (hello parte centrale di schermata Ciao) toouse hello per accedere ai dati.

Si tratta di quali hello **l'importazione dei dati** aspetto durante il recupero di dati dalla tabella Hive hello:

![Acquisizione di dati con Import Data](./media/machine-learning-data-science-process-hive-criteo-walkthrough/i3zRaoj.png)

Per hello **l'importazione dei dati** modulo, i valori hello di parametro hello viene forniti in hello grafico sono soli alcuni esempi di hello sorta di valori è necessario tooprovide. Ecco alcune linee guida generali sulla configurazione per hello toofill parametro hello out **l'importazione dei dati** modulo.

1. In **Data Source**
2. In hello **query database Hive** casella, un'istruzione SELECT semplice * FROM < il\_database\_name.your\_tabella\_nome >-è sufficiente.
3. **Hcatalog server URI** (URI del server Hcatalog): se il cluster è "abc", specificare semplicemente https://abc.azurehdinsight.net.
4. **Nome dell'account utente Hadoop**: nome utente hello scelta in fase di hello entrata cluster hello. (Non hello accesso remoto nome utente!)
5. **Password dell'account utente Hadoop**: hello password hello utente al momento di hello entrata cluster hello. (Non hello password di accesso remoto!)
6. **Location of output data**: scegliere "Azure".
7. **Nome dell'account di archiviazione Azure**: hello account di archiviazione associato hello cluster
8. **Chiave dell'account di archiviazione di Azure**: chiave hello hello dell'account di archiviazione associato hello cluster.
9. **Nome del contenitore di Azure**: se il nome del cluster hello è "abc", quindi viene semplicemente "abc", in genere.

Una volta hello **l'importazione dei dati** al termine dell'acquisizione di dati (segno di spunta verde hello vedere nel modulo hello), salvare i dati come set di dati (con un nome di propria scelta). L'aspetto è il seguente:

![Salvataggio di dati con Import Data](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oxM73Np.png)

Porta di hello di output di hello rapida **l'importazione dei dati** modulo. Verranno visualizzate le opzioni **Save as dataset** (Salva come set di dati) e **Visualize** (Visualizza). Hello **Visualizza** opzione, se selezionato, consente di visualizzare 100 righe di dati di hello, insieme a un pannello destro che è utile per alcune statistiche di riepilogo. toosave dati, selezionare semplicemente **salvare come set di dati** e seguire le istruzioni.

il set di dati di tooselect hello salvato per l'utilizzo in un esperimento di apprendimento macchina, individuare hello DataSet utilizzando hello **ricerca** dialogo illustrata nella seguente illustrazione hello. Quindi è sufficiente specificare il nome assegnato al hello hello set di dati parzialmente tooaccess e trascinare hello set di dati in hello pannello principale. Il trascinamento nella finestra Pannello principale hello viene selezionata per la modellazione di machine learning.

![Set di dati del trascinamento nel pannello principale hello](./media/machine-learning-data-science-process-hive-criteo-walkthrough/cl5tpGw.png)

> [!NOTE]
> Eseguire questa operazione per eseguire il training hello e hello test set di dati. Ricordare inoltre il nome di database toouse hello e i nomi di tabella assegnato a questo scopo. i valori Hello utilizzati nella figura hello sono esclusivamente per figura purposes.* *
> 
> 

### <a name="step2"></a>Passaggio 2: Creare un semplice esperimento in Azure Machine Learning toopredict clic / non fa clic su
L'esperimento di Azure ML è simile al seguente:

![Esperimento di Machine Learning](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xRpVfrY.png)

È ora possibile esaminare i componenti chiave hello di questo esperimento. Come promemoria, dobbiamo toodrag nostri salvata di eseguire il training e di testare i set di dati nell'area di disegno esperimento tooour prima.

#### <a name="clean-missing-data"></a>Pulire i dati mancanti
Hello **Clean Missing Data** modulo cosa suggerisce il nome: vengono puliti i dati mancanti in modi che possono essere specificate dall'utente. Analizzando il modulo, è possibile vedere quanto segue:

![Pulire i dati mancanti](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0ycXod6.png)

In questo caso, è stato scelto tooreplace tutti i valori mancanti con il valore 0. Sono disponibili anche altre opzioni che possono essere visualizzati esaminando hello elenchi a discesa nel modulo hello.

#### <a name="feature-engineering-on-hello-data"></a>Progettazione di funzionalità sui dati hello
Per alcune funzioni categoriche di set di dati di grandi dimensioni possono esistere milioni di valori univoci. Non è possibile usare metodi di base come la codifica one-hot per rappresentare funzioni categoriche con dimensionalità così elevata. In questa procedura dettagliata viene illustrato come le funzioni di conteggio toouse usando incorporato toogenerate moduli di Azure Machine Learning compact rappresentazioni di queste variabili categoriche elevata dimensionalità. Hello risultato finale è un piccolo modello, tempi di training e metriche delle prestazioni sono molto simili toousing altre tecniche.

##### <a name="building-counting-transforms"></a>Compilazione di trasformazioni conteggio
funzionalità di conteggio toobuild, utilizziamo hello **compilare conteggio trasformare** modulo che è disponibile in Azure Machine Learning. modulo Hello è simile al seguente:

![Modulo Build Counting Transform](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![Modulo Build Counting Transform](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)

> [!IMPORTANT] 
> In hello **Conteggio colonne** casella, si immette le colonne che si desidera che il conteggio di tooperform. Come indicato in precedenza, si tratta in genere di colonne categoriche con dimensionalità elevata. All'avvio di hello, abbiamo detto set di dati Criteo hello è 26 colonne categoriche: da Col15 tooCol40. In questo caso, si contare su tutti gli elementi e i relativi indici (da 15 too40 separati da virgole, come illustrato).
> 

modulo hello toouse hello modalità MapReduce (appropriata per grandi set di dati), si base accesso cluster HDInsight Hadoop tooan (quello utilizzato per l'esplorazione delle funzionalità possa essere riutilizzato per questo scopo, nonché Buongiorno) e le relative credenziali. figure precedenti Hello illustrano quali hello riempita valori aspetto (sostituire i valori hello forniti a scopo illustrativo con quelli appropriati per il propria caso di utilizzo).

![Parametri del modulo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/05IqySf.png)

In hello nella figura riportata sopra viene illustrato come tooenter hello input blob percorso. Questa posizione è riservati per la creazione di tabelle di conteggio dati di hello.

Al termine dell'esecuzione questo modulo, è possibile salvare in un secondo momento trasformazione hello per facendo modulo hello hello **salvare come trasformazione** opzione:

![Opzione "Save as Transform" (Salva come trasformazione)](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IcVgvHR.png)

Nell'architettura esperimento illustrato in precedenza, set di dati hello "ytransform2" corrisponde esattamente tooa salvato trasformazione conteggio. Resto hello di questo esperimento, si presuppone che lettore hello usato un **compilare conteggio trasformare** modulo alcuni dati toogenerate conteggi e possono quindi utilizzare tali funzioni di conteggio toogenerate conteggi su train hello e set di dati di test.

##### <a name="choosing-what-count-features-tooinclude-as-part-of-hello-train-and-test-datasets"></a>Scelta di quali conteggio tooinclude funzionalità come parte del training hello e set di dati di test
Una volta che un numero di trasformare pronto, utente hello è possibile scegliere quali tooinclude funzionalità nella loro train e test set di dati tramite hello **modificare i parametri di tabella conteggio** modulo. Questo modulo viene illustrato qui per completezza, ma per semplicità non viene effettivamente usato nell'esperimento.

![Modulo Modify Count Table Parameters](./media/machine-learning-data-science-process-hive-criteo-walkthrough/PfCHkVg.png)

In questo caso, come si può notare, abbiamo scelto toouse hello solo log-odds e tooignore hello spostare la colonna. È anche possibile impostare i parametri, ad esempio hello soglia Cestino, quanti tooadd pseudo-precedente esempi per l'arrotondamento, e se toouse qualsiasi Laplaciana del rumore o non. Tutte queste funzionalità sono avanzate e risulta toobe notare che i valori predefiniti di hello rappresentano un buon punto di partenza per gli utenti che sono di nuovo tipo toothis della generazione di funzionalità.

##### <a name="data-transformation-before-generating-hello-count-features"></a>Trasformazione dei dati prima di generare le funzionalità di conteggio hello
È ora concentrarsi su un punto importante sulla trasformazione il training e test tooactually di dati precedente la generazione di funzioni di conteggio. Si noti che sono disponibili due **Execute R Script** moduli utilizzati prima che si applicano hello conteggio trasformazione tooour dati.

![Moduli Execute R Script](./media/machine-learning-data-science-process-hive-criteo-walkthrough/aF59wbc.png)

Ecco lo script R prima hello:

![Primo script R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/3hkIoMx.png)

In questo script R, rinominare il nostro toonames colonne "Col1" troppo "Col40". Questo avviene perché hello conteggio trasformazione prevede che i nomi di questo formato.

Nel secondo script R di hello, abbiamo bilanciare distribuzione hello tra classi positive e negative (classi rispettivamente 1 e 0) dalla classe di sottocampionamento hello negativo. Hello R script qui illustrato in che modo toodo questo:

![Secondo script R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/91wvcwN.png)

In questo semplice script R, si usa "pos\_neg\_rapporto" quantità di hello tooset di equilibrio tra hello positivo e negativo classi di hello. Questo è importante toodo poiché miglioramento sbilanciamento di classe in genere presenta vantaggi di prestazioni per problemi di classificazione in cui la distribuzione di classe hello è sfasato (tenere presente che in questo caso, sono disponibili classi positivo 3.3% e % 96,7 negativo).

##### <a name="applying-hello-count-transformation-on-our-data"></a>L'applicazione della trasformazione Conteggio hello sui nostri dati
Infine, è possibile utilizzare hello **Apply Transformation** tooapply modulo hello trasformazioni conteggio sul training e set di dati di test. Questo modulo accetta trasformazione Conteggio hello salvato come un input e hello training o il set di dati di test come hello altri tipi di input e restituisce i dati con le funzionalità di conteggio. come illustrato qui:

![Modulo Apply Transformation](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xnQvsYf.png)

##### <a name="an-excerpt-of-what-hello-count-features-look-like"></a>Un estratto della funzionalità di conteggio hello aspetto
È utile toosee sulle funzionalità di conteggio hello simile in questo caso. Eccone un estratto:

![Funzioni di conteggio](./media/machine-learning-data-science-process-hive-criteo-walkthrough/FO1nNfw.png)

In questo estratto, verrà indicato che per le colonne hello conteggiati in totale, è ottenere il totale hello e Accedi disparità backoffs rilevanti tooany di addizione.

Ci sono ora pronti toobuild un modello di Azure Machine Learning usando questi set di dati trasformato. Nella sezione successiva hello, ecco come questa operazione può essere eseguita.

### <a name="step3"></a>Passaggio 3: Compilazione, il training e assegnare un punteggio modello hello

#### <a name="choice-of-learner"></a>Scelta dello strumento di apprendimento
Innanzitutto, è necessario toochoose uno strumento di apprendimento. È in corso toouse un albero delle decisioni con Boosting di due classi come questo strumento di apprendimento. Ecco le opzioni predefinite di hello per questo strumento di apprendimento:

![Parametri del modulo Two-Class Boosted Decision Tree](./media/machine-learning-data-science-process-hive-criteo-walkthrough/bH3ST2z.png)

Per la sperimentazione, siamo i valori predefiniti di corso toochoose hello. È possibile notare che hello predefinite sono in genere significativo e un buon metodo tooget rapido le linee di base sulle prestazioni. È possibile migliorare sulle prestazioni da sweep di parametri se si sceglie tooonce che è una linea di base.

#### <a name="train-hello-model"></a>Modello di hello Train
Per il training, è sufficiente richiamare un modulo **Train Model** (Modello di training). Hello due input tooit sono dello strumento di apprendimento di hello Two-Class Boosted Decision Tree e il set di dati di training. come illustrato qui:

![Modulo Train Model](./media/machine-learning-data-science-process-hive-criteo-walkthrough/2bZDZTy.png)

#### <a name="score-hello-model"></a>Modello di punteggio hello
Dopo avere creato un modello con training, si è pronti tooscore su hello verifica set di dati e tooevaluate delle prestazioni. Facciamo utilizzando hello **Score Model** modulo illustrato nella seguente illustrazione, insieme a hello un **Evaluate Model** modulo:

![Modulo Score Model](./media/machine-learning-data-science-process-hive-criteo-walkthrough/fydcv6u.png)

### <a name="step4"></a>Passaggio 4: Valutazione del modello di hello
Infine, desideriamo tooanalyze le prestazioni del modello. In genere, per due problemi di classificazione (binario) di classe, un'ottima misura è hello AUC. toovisualize, abbiamo agganciare hello **Score Model** modulo tooan **Evaluate Model** modulo per questo oggetto. Fare clic su **Visualizza** su hello **Evaluate Model** modulo produce un'immagine come segue quello hello:

![Modulo di valutazione del modello per l'albero delle decisioni con boosting](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0Tl0cdg.png)

Nel file binario (o classe due) problemi di classificazione, un'ottima misura dell'accuratezza della stima è hello Area nella curva (AUC). Di seguito sono illustrati i risultati dell'uso del modello sul set di dati di test. tooget, questa porta di output di hello rapida di hello **Evaluate Model** modulo e quindi **Visualizza**.

![Visualizzazione del modulo Evaluate Model](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IRfc7fH.png)

### <a name="step5"></a>Passaggio 5: Pubblicare il modello di hello come un servizio Web
Hello possibilità toopublish un modello di Azure Machine Learning come servizi web con un minimo di confusione è una funzionalità utile per renderlo ampiamente disponibile. Al termine dell'operazione, chiunque può creare chiamate toohello web servizio con dati di input che hanno bisogno di stime per e servizio web hello utilizza hello modello tooreturn tali stime.

toodo, è innanzitutto salvare il modello con training come un oggetto modello con training. Questa operazione viene eseguita facendo clic su hello **Train Model** modulo e l'utilizzo di hello **Save as Trained Model** opzione.

È quindi necessario toocreate input e output porte per il servizio web:

* Recupera i dati in hello stesso modulo come dati hello che si richiedono stime per una porta di input
* una porta di output restituisce hello Scored Labels e le probabilità di hello associata.

#### <a name="select-a-few-rows-of-data-for-hello-input-port"></a>Selezionare alcune righe di dati per la porta di input hello
È utile toouse un **Apply SQL Transformation** modulo tooselect solo 10 righe tooserve come hello specificati dati porta di input. Selezionare solo le righe di dati per la porta di input tramite query SQL hello illustrata di seguito:

![Dati porta di input](./media/machine-learning-data-science-process-hive-criteo-walkthrough/XqVtSxu.png)

#### <a name="web-service"></a>Servizio Web
Ora è pronto toorun un esperimento di piccole dimensioni che può essere utilizzati toopublish il servizio web.

#### <a name="generate-input-data-for-webservice"></a>Generare i dati di input per il servizio Web
Come passaggio zero, poiché è grande, la tabella di conteggio hello è poche righe di dati di test e generare dati di output da esso con le funzionalità di conteggio. Questo può essere usato come formato di dati di input hello per il servizio Web. come illustrato qui:

![Creazione dati di input per l'albero delle decisioni con boosting](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OEJMmst.png)

> [!NOTE]
> Per il formato di dati di input di hello, è possibile utilizzare l'OUTPUT di hello hello **Count Featurizer** modulo. Dopo questo provare al termine dell'esecuzione, salvare l'output di hello da hello **Count Featurizer** modulo come un set di dati. Questo set di dati viene utilizzato per dati di input hello in webservice hello.
> 
> 

#### <a name="scoring-experiment-for-publishing-webservice"></a>Esperimento di assegnazione dei punteggi per la pubblicazione del servizio Web
Innanzitutto, viene illustrato l'aspetto. struttura essenziali Hello è un **Score Model** modulo che accetta l'oggetto modello sottoposto a training e alcune righe di dati di input generati in precedenza hello utilizzando hello **Count Featurizer** modulo. Utilizziamo tooproject "Selezionare le colonne nel set di dati" hello Scored etichette e le probabilità di punteggio hello.

![Select Columns in Dataset](./media/machine-learning-data-science-process-hive-criteo-walkthrough/kRHrIbe.png)

Si noti come hello **selezionare le colonne nel set di dati** modulo può essere utilizzato per il 'filtro' dati da un set di dati. Ecco contenuto hello qui:

![Applicazione di filtri con hello selezionare le colonne nel modulo di set di dati](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oVUJC9K.png)

porte di tooget hello blu di input e output, sufficiente fare clic su **preparare webservice** in basso a destra hello. Eseguendo questo esperimento consente inoltre di servizio web di hello toopublish: fare clic su hello **servizio WEB di pubblicare** icona qui destra, come illustrato nella parte inferiore di hello:

![PUBLISH WEB SERVICE](./media/machine-learning-data-science-process-hive-criteo-walkthrough/WO0nens.png)

Dopo aver pubblicato webservice hello, si ottiene pagina tooa reindirizzato pertanto:

![Dashboard del servizio Web](./media/machine-learning-data-science-process-hive-criteo-walkthrough/YKzxAA5.png)

Verrà visualizzato due collegamenti per i servizi Web sul lato sinistro hello:

* Hello **richiesta/risposta** (o il servizio RR) è destinati a singole stime ed è ciò che si utilizzano per questa esercitazione.
* Hello **esecuzione BATCH** servizio (BES) viene utilizzato per le stime in batch e richiede che le stime toomake di dati di input utilizzati hello si trovino nell'archiviazione Blob di Azure.

Fare clic sul collegamento hello **richiesta/risposta** ci ha tooa pagina che consente di ottenere pre-predefinito codice c#, python e R. Questo codice può essere facilmente usato per effettuare chiamate toohello webservice. Si noti che la chiave API in questa pagina hello necessario toobe utilizzato per l'autenticazione.

È utile toocopy questo python di codice su tooa nuova cella notebook IPython hello.

Di seguito è illustrato un segmento di codice python con chiave API corretta hello.

![Codice Python](./media/machine-learning-data-science-process-hive-criteo-walkthrough/f8N4L4g.png)

Si noti che la chiave API predefinito hello pertanto abbiamo sostituito con la chiave API del nostro webservices. Fare clic su **eseguire** su questa cella in un IPython notebook produce hello seguente risposta:

![Risposta IPython](./media/machine-learning-data-science-process-hive-criteo-walkthrough/KSxmia2.png)

Vediamo che per hello due test esempi che abbiamo chiesto (nel framework JSON hello dello script python hello), otteniamo risposte in formato hello "Scored Labels, probabilità Scored". Si noti che in questo caso, è stato scelto i valori predefiniti di hello che il codice predefinito hello fornisce (0 zero per tutte le colonne numeriche e stringa hello "value" per tutte le colonne categoriche).

Questa operazione conclude la procedura dettagliata end-to-end di mostrare come toohandle set di dati su larga scala con Azure Machine Learning. Viene avviato con un terabyte di dati, costruito un modello di stima e distribuita come servizio web nel cloud hello.

