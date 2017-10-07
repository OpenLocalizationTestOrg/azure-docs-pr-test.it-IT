---
title: dati aaaExplore un Hadoop del cluster e creare modelli in Azure Machine Learning | Documenti Microsoft
description: Utilizzando hello Team processo di analisi scientifica dei dati per uno scenario end-to-end che utilizza un HDInsight Hadoop toobuild del cluster e distribuire un modello usando un set di dati disponibili pubblicamente.
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e9e76c91-d0f6-483d-bae7-2d3157b86aa0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: a371032e356ffc366af0d6fbe364af281b6efd19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-use-azure-hdinsight-hadoop-clusters"></a>Processo di analisi scientifica dei dati del Team di Hello in azione: cluster di utilizzare Azure HDInsight Hadoop
In questa procedura dettagliata, si usa hello [Team Data Science processo (TDSP)](data-science-process-overview.md) in un scenario end-to-end utilizzando un [cluster Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/) toostore, esplorare e funzionalità engineer dati hello pubblicamente disponibile [NYC Taxi trip](http://www.andresmh.com/nyctaxitrips/) set di dati e toodown campionare i dati di hello. Con Azure Machine Learning toohandle multiclasse e binarie classificazione e regressione delle attività di stima vengono compilati i modelli di dati hello.

Per una procedura dettagliata che illustra come toohandle cluster di un set di dati più grande (1 terabyte) per uno scenario simile utilizzando HDInsight Hadoop per l'elaborazione dati, vedere [processo di analisi scientifica dei dati di Team - i cluster Hadoop HDInsight di Azure utilizzando un set di dati di 1 TB](machine-learning-data-science-process-hive-criteo-walkthrough.md).

È inoltre possibile toouse un hello tooaccomplish di IPython notebook attività procedura dettagliata di hello presentata tramite set di dati di hello 1 TB. Gli utenti che sarebbero ad esempio tootry deve consultare questo approccio hello [procedura dettagliata Criteo utilizzando una connessione ODBC Hive](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) argomento.

## <a name="dataset"></a>Descrizione del set di dati relativo alle corse dei taxi di New York
dati di andata e ritorno Taxi NYC Hello è di circa 20GB di file compressi valori delimitati da virgole (CSV) (~ 48GB non compressi), che comprendono 173 milioni hello e singoli trip tariffe a pagamento per ogni itinerario. Ogni record di andata e ritorno include il percorso di ritiro e deposito hello e l'ora, hack anonimi (driver) il numero di licenza e numero medallion (id univoco del taxi). dati Hello copre tutti i percorsi nell'anno hello 2013 e viene forniti in hello dopo i due set di dati per ogni mese:

1. file CSV di Hello 'trip_data' contengono i dettagli di andata e ritorno, ad esempio il numero di passeggeri, prelievo e dropoff punti, la durata del viaggio e lunghezza di andata e ritorno. Di seguito vengono forniti alcuni record di esempio:
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. file CSV di Hello 'trip_fare' contengono i dettagli della tariffa di hello pagata per ogni itinerario, ad esempio il tipo di pagamento, quantità tariffa, supplemento e le imposte, suggerimenti e pedaggio e hello totale pagato. Di seguito vengono forniti alcuni record di esempio:
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

viaggi toojoin chiave univoca Hello\_dati e andata e ritorno\_tariffa è costituito da campi hello: medallion, le maggiori\_titolo e prelievo\_datetime.

tooget tutti di hello dettagli pertinenti tooa particolare di andata e ritorno, è sufficiente toojoin con tre chiavi: hello "medallion", "hack\_licenza" e "prelievo\_datetime".

Vengono descritte alcune ulteriori dettagli dei dati di hello quando è archiviarli in tabelle Hive a breve.

## <a name="mltasks"></a>Esempi di attività di stima
Quando per raggiungere i dati, determinare il tipo di hello di stime che si desidera toomake in base alle analisi consente di chiarire attività hello che sarà necessario tooinclude del processo.
Ecco tre esempi di problemi di stima che si risolvono in questa procedura dettagliata il cui formulazione è basato su hello *suggerimento\_quantità*:

1. **Classificazione binaria**: consente di prevedere se sia stata lasciata una mancia per la corsa oppure no, vale a dire se un *tip\_amount* superiore a $ 0 rappresenta un esempio positivo, mentre un *tip\_amount* pari a $ 0 rappresenta un esempio negativo.
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0
2. **Classificazione multiclasse**: intervallo di hello toopredict degli importi di suggerimento pagato viaggi hello. Verrà diviso hello *suggerimento\_quantità* in cinque contenitori o le classi:
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. **Attività di regressione**: quantità di hello toopredict del suggerimento hello a pagamento per un itinerario.  

## <a name="setup"></a>Configurare un cluster Hadoop di HDInsight per l'analisi avanzata
> [!NOTE]
> In genere, questa attività viene svolta da un **amministratore** .
> 
> 

Per impostare un ambiente Azure per l'analisi avanzata basato su un cluster HDInsight è necessario seguire questa procedura composta da tre passaggi:

1. [Creare un account di archiviazione](../storage/common/storage-create-storage-account.md): l'account di archiviazione viene usato per archiviare i dati nell'archivio BLOB di Azure. dati Hello utilizzati nei cluster di HDInsight si trovano anche qui.
2. [Personalizzare Azure HDInsight Hadoop cluster per hello avanzate processo Analitica e la tecnologia](machine-learning-data-science-customize-hadoop-cluster.md). questo passaggio consente di creare un cluster Hadoop di Azure HDInsight con la versione a 64 bit di Anaconda Python 2.7 installata in tutti i nodi. Esistono due importanti passaggi tooremember durante la personalizzazione del cluster HDInsight.
   
   * Ricordare che account di archiviazione hello toolink creato nel passaggio 1 con il cluster HDInsight quando viene creata. Questo account di archiviazione è tooaccess utilizzati i dati elaborati all'interno di cluster hello.
   * Dopo la creazione di cluster hello, abilitare nodo head di accesso remoto a toohello del cluster di hello. Passare toohello **configurazione** scheda e fare clic su **Abilita modalità remota**. Questo passaggio consente di specificare le credenziali utente hello usate per l'accesso remoto.
3. [Creare un'area di lavoro di Azure Machine Learning](machine-learning-create-workspace.md): area di lavoro questo Azure Machine Learning è modelli di apprendimento toobuild utilizzato. Questa attività è stato risolto dopo aver completato un'esplorazione dei dati iniziali e verso il basso campionamento utilizzando cluster HDInsight hello.

## <a name="getdata"></a>Ottenere dati hello da un'origine pubblica
> [!NOTE]
> In genere, questa attività viene svolta da un **amministratore** .
> 
> 

hello tooget [NYC Taxi trip](http://www.andresmh.com/nyctaxitrips/) set di dati dal percorso pubblico, è possibile utilizzare uno dei metodi di hello descritto in [tooand spostare dati dall'archiviazione Blob di Azure](machine-learning-data-science-move-azure-blob.md) macchina di tooyour toocopy hello dati.

Di seguito viene descritto come usare AzCopy tootransfer hello file contenente i dati. toodownload e installare AzCopy istruzioni hello in [introduzione hello utilità della riga di comando di AzCopy](../storage/common/storage-use-azcopy.md).

1. Da una finestra del prompt dei comandi eseguire hello comandi AzCopy seguente, sostituendo *< path_to_data_folder >* con la destinazione desiderata hello:

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S

1. Al termine della copia di hello, un totale di file compressi 24 sono nella cartella dati hello scelto. Decomprimere hello scaricato i file toohello stessa directory nel computer locale. Prendere nota della cartella hello in cui risiedono i file non compresso hello. Questa cartella verrà hello cui tooas *< percorso\_a\_unzipped_data\_file\>*  è quello che segue.

## <a name="upload"></a>Caricare contenitore del cluster Azure HDInsight Hadoop hello dati toohello predefinito
> [!NOTE]
> In genere, questa attività viene svolta da un **amministratore** .
> 
> 

In hello comandi AzCopy seguenti, sostituire hello seguenti parametri con valori reali hello specificata durante la creazione di un cluster Hadoop hello e decomprimere i file di dati hello.

* ***&#60; path_to_data_folder >*** hello directory (percorso) nel computer che contengono file di dati decompresso hello  
* ***&#60; il nome di account di archiviazione del cluster Hadoop >*** hello account di archiviazione associato al cluster HDInsight
* ***&#60; contenitore predefinito del cluster Hadoop >*** contenitore predefinito hello utilizzato dal cluster. Si noti che nome hello predefinito hello contenitore è in genere hello stesso nome come cluster hello stesso. Ad esempio, se il cluster hello viene chiamato "abc123.azurehdinsight.net", contenitore predefinito hello è abc123.
* ***&#60; chiave dell'account di archiviazione >*** hello chiave hello account di archiviazione utilizzato dal cluster

Da un prompt dei comandi o da una finestra di Windows PowerShell nel computer, eseguire hello seguenti due comandi AzCopy.

Questo comando consente di caricare i dati di andata e ritorno hello troppo***nyctaxitripraw*** directory nel contenitore predefinito hello del cluster Hadoop hello.

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxitripraw /DestKey:<storage account key> /S /Pattern:trip_data_*.csv

Questo comando consente di caricare dati tariffa hello troppo***nyctaxifareraw*** directory nel contenitore predefinito hello del cluster Hadoop hello.

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxifareraw /DestKey:<storage account key> /S /Pattern:trip_fare_*.csv

dati Hello devono ora nell'archiviazione Blob di Azure e pronto toobe utilizzati all'interno del cluster HDInsight hello.

## <a name="#download-hql-files"></a>Accedere al nodo head di hello del cluster Hadoop ed e la preparazione per l'analisi esplorativa dei dati
> [!NOTE]
> In genere, questa attività viene svolta da un **amministratore** .
> 
> 

nodo head di hello tooaccess del cluster di hello per analisi esplorative dei dati e verso il basso il campionamento dei dati di hello, attenersi alla procedura hello [hello accesso nodo Head del Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).

In questa procedura dettagliata viene usato principalmente le query scritte [Hive](https://hive.apache.org/), un linguaggio di query simile a SQL, tooperform esplorazioni di raccogliere dati. le query Hive Hello vengono archiviate nei file .hql. È quindi verso il basso di esempio questa toobe dati utilizzato all'interno di Azure Machine Learning per la creazione di modelli.

cluster di hello tooprepare per analisi esplorative dei dati, scaricare hello .hql contenenti script Hive appropriati hello da [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) tooa directory (C:\temp) locale nel nodo head hello. toodo, aprire hello **prompt dei comandi** dall'interno hello nodo head di hello hello cluster e il problema, i due comandi seguenti:

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/DataScienceProcess/DataScienceScripts/Download_DataScience_Scripts.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

Questi due comandi verranno scaricati tutti i file .hql necessari in questa directory locale di questa procedura dettagliata toohello ***C:\temp &#92;*** nel nodo head hello.

## <a name="#hive-db-tables"></a>Creare database e tabelle Hive partizionati in base al mese
> [!NOTE]
> In genere, questa attività viene svolta da un **amministratore** .
> 
> 

È ora sono tabelle Hive toocreate pronto per il set di dati taxi NYC.
Nel nodo head di hello del cluster Hadoop hello, aprire hello ***della riga di comando Hadoop*** hello desktop del nodo head hello e immettere una directory di Hive hello immettendo il comando hello

    cd %hive_home%\bin

> [!NOTE]
> **Eseguire tutti i comandi di Hive in questa procedura dettagliata da hello sopra Hive bin / prompt dei comandi. In questo modo, eventuali problemi di percorso verranno risolti automaticamente. Vengono utilizzati termini hello "Hive prompt dei comandi", "bin Hive / prompt dei comandi" e "riga di comando Hadoop" in modo intercambiabile in questa procedura dettagliata.**
> 
> 

Hello Hive prompt dei comandi, digitare hello comando nella riga di comando di Hadoop di tabelle e il nodo head hello toosubmit di hello Hive query Hive toocreate database seguente:

    hive -f "C:\temp\sample_hive_create_db_and_tables.hql"

Di seguito è contenuto hello di hello ***C:\temp\sample\_hive\_creare\_db\_e\_tables.hql*** file che crea il database Hive ***nyctaxidb *** e tabelle ***viaggi*** e ***tariffa***.

    create database if not exists nyctaxidb;

    create external table if not exists nyctaxidb.trip
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double)  
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');

    create external table if not exists nyctaxidb.fare
    (
        medallion string,
        hack_license string,
        vendor_id string,
        pickup_datetime string,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double)
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');

Questo script Hive crea due tabelle:

* tabella "di andata e ritorno" Hello contiene i dettagli di andata e ritorno di ogni interscambio (Dettagli driver, tempo di prelievo, la distanza di andata e ritorno e l'ora)
* Nella tabella "tariffa" Hello contiene dettagli tariffa (tariffa, suggerimento importo, pedaggio e supplementi).

Se per un'ulteriore assistenza con queste procedure o tooinvestigate quelli alternativi, vedere sezione hello [query Hive inviare direttamente da hello della riga di comando Hadoop ](machine-learning-data-science-move-hive-tables.md#submit).

## <a name="#load-data"></a>Caricare le tabelle tooHive dati dalle partizioni
> [!NOTE]
> In genere, questa attività viene svolta da un **amministratore** .
> 
> 

Hello NYC taxi dispone di un partizionamento naturale per mese, utilizziamo tooenable tempi di elaborazione e query più rapidi. Hello comandi di PowerShell riportati di seguito (emesso dalla directory di Hive hello utilizzando hello **della riga di comando Hadoop**) caricare dati toohello "viaggi" e "tariffa" Hive tabelle partizionate in base al mese.

    for /L %i IN (1,1,12) DO (hive -hiveconf MONTH=%i -f "C:\temp\sample_hive_load_data_by_partitions.hql")

Hello *esempio\_hive\_caricare\_dati\_da\_partitions.hql* file contiene i seguenti hello **caricare** comandi.

    LOAD DATA INPATH 'wasb:///nyctaxitripraw/trip_data_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.trip PARTITION (month=${hiveconf:MONTH});
    LOAD DATA INPATH 'wasb:///nyctaxifareraw/trip_fare_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.fare PARTITION (month=${hiveconf:MONTH});

Si noti che un numero di query Hive che utilizziamo nel processo di esplorazione hello implica la ricerca di in solo una singola partizione o in un paio di partizioni. Ma è stato possibile eseguire queste query tra tutti i dati hello.

### <a name="#show-db"></a>Visualizzare i database in un cluster HDInsight Hadoop hello
database di hello tooshow creati in cluster HDInsight Hadoop all'interno di finestra della riga di comando Hadoop hello eseguire hello nella riga di comando di Hadoop di comando seguente:

    hive -e "show databases;"

### <a name="#show-tables"></a>Mostra tabelle Hive hello nel database nyctaxidb hello
tabelle di hello tooshow nel database nyctaxidb hello, eseguire hello nella riga di comando di Hadoop di comando seguente:

    hive -e "show tables in nyctaxidb;"

È possibile verificare che le tabelle di hello sono partizionate eseguendo il comando hello riportato di seguito:

    hive -e "show partitions nyctaxidb.trip;"

Hello è previsto output è illustrato di seguito:

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 2.075 seconds, Fetched: 12 row(s)

Analogamente, è possibile assicurare che hello tariffa viene partizionata eseguendo il comando hello riportato di seguito:

    hive -e "show partitions nyctaxidb.fare;"

Hello è previsto output è illustrato di seguito:

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 1.887 seconds, Fetched: 12 row(s)

## <a name="#explore-hive"></a>Esplorare i dati e progettare le funzionalità in Hive
> [!NOTE]
> In genere, questa attività viene svolta da un **data scientist** .
> 
> 

Hello l'esplorazione dei dati e le attività di progettazione per hello dati caricati in tabelle Hive hello possono essere effettuati utilizzando le query Hive di funzionalità. Di seguito sono riportati alcuni esempi delle attività che si affronteranno in questa sezione:

* Consente di visualizzare i record di 10 superiore hello in entrambe le tabelle.
* Esplorazione delle distribuzioni di dati di un numero ridotto di campi in diverse finestre temporali.
* Analizzare la qualità dei dati dei campi di longitudine e latitudine hello.
* Generare etichette di classificazione multiclasse e binaria dipende hello **suggerimento\_quantità**.
* Generare funzioni calcolando le distanze hello diretto di andata e ritorno.

### <a name="exploration-view-hello-top-10-records-in-table-trip"></a>Esplorazione: Vista hello top 10 record di andata e ritorno tabella
> [!NOTE]
> In genere, questa attività viene svolta da un **data scientist** .
> 
> 

toosee quali dati hello sono simile, esamineremo 10 record da ogni tabella. Eseguire i seguenti due query separatamente dagli hello Hive prompt dei comandi nei record di hello della riga di comando Hadoop console tooinspect hello hello.

tooget hello primi 10 record nella tabella hello "viaggi" dal primo mese di hello:

    hive -e "select * from nyctaxidb.trip where month=1 limit 10;"

tooget hello primi 10 record nella tabella hello "tariffa" dal primo mese di hello:

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;"

È spesso utile toosave hello record tooa file per la visualizzazione semplice. Toohello una piccola modifica di sopra di query esegue questa operazione:

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;" > C:\temp\testoutput

### <a name="exploration-view-hello-number-of-records-in-each-of-hello-12-partitions"></a>Esplorazione: Numero di hello visualizzazione di record in ogni 12 partizioni hello
> [!NOTE]
> In genere, questa attività viene svolta da un **data scientist** .
> 
> 

Di interesse è hello variazioni numero hello di trip durante l'anno di calendario hello. Raggruppamento in base al mese consente toosee questa distribuzione di trip l'aspetto seguente.

    hive -e "select month, count(*) from nyctaxidb.trip group by month;"

Questa operazione produce output di hello:

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 283.406 seconds, Fetched: 12 row(s)

In questo caso, hello prima colonna è mese hello e hello secondo numero hello di trip per il mese.

È anche possibile conteggio totale hello dei record di questo set di dati di andata e ritorno eseguendo hello comando al prompt dei comandi di hello Hive directory seguente.

    hive -e "select count(*) from nyctaxidb.trip;"

Il risultato è il seguente:

    173179759
    Time taken: 284.017 seconds, Fetched: 1 row(s)

Utilizzando i comandi toothose simili per set di dati di andata e ritorno hello, è possibile rilasciare le query Hive dal prompt di directory hello Hive per hello tariffa dati toovalidate hello numero di set di record.

    hive -e "select month, count(*) from nyctaxidb.fare group by month;"

Questa operazione produce output di hello:

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 253.955 seconds, Fetched: 12 row(s)

Si noti che viene restituito hello esatta stesso numero di viaggi al mese per entrambi i set di dati. Questo fornisce la convalida prima di hello che hello dati sono stati caricati correttamente.

Il conteggio hello il numero totale di record nel set di dati tariffa hello può essere eseguito tramite comando hello seguente dal prompt dei comandi di hello Hive directory:

    hive -e "select count(*) from nyctaxidb.fare;"

Il risultato è il seguente:

    173179759
    Time taken: 186.683 seconds, Fetched: 1 row(s)

numero totale di Hello di record in entrambe le tabelle è inoltre hello stesso. Ciò fornisce una convalida secondo tale hello dati sono stati caricati correttamente.

### <a name="exploration-trip-distribution-by-medallion"></a>Esplorazione: distribuzione delle corse per licenza
> [!NOTE]
> In genere, questa attività viene svolta da un **data scientist** .
> 
> 

In questo esempio identifica medallion hello (numeri taxi) con più di 100 trip all'interno di un determinato periodo di tempo. vantaggi di query Hello da hello partizionata accesso alla tabella poiché condizionato, dalla variabile partizione hello **mese**. risultati della query Hello scritte tooa file locale queryoutput.tsv in `C:\temp` nel nodo head hello.

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

Di seguito è contenuto hello di *esempio\_hive\_viaggi\_conteggio\_da\_medallion.hql* file per l'ispezione.

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

medallion Hello nel set di dati di hello NYC taxi identifica un file cab univoco. È possibile identificare i taxi "occupati" chiedendo quali di essi hanno effettuato più di un determinato numero di corse in un intervallo di tempo specifico. esempio Hello identifica file CAB che ha effettuato più di cento viaggi in hello primi tre mesi, e Salva hello risultati tooa locale file di query C:\temp\queryoutput.tsv.

Di seguito è contenuto hello di *esempio\_hive\_viaggi\_conteggio\_da\_medallion.hql* file per l'ispezione.

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

Da hello Hive prompt dei comandi, problema hello comando riportato di seguito:

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a>Esplorazione: distribuzione delle corse per licenza e hack_license
> [!NOTE]
> In genere, questa attività viene svolta da un **data scientist** .
> 
> 

Durante l'esplorazione di un set di dati, è spesso necessario numero hello tooexamine di co-occorrenze dei gruppi di valori. In questa sezione viene fornito un esempio di come toodo per a quelle driver.

Hello *esempio\_hive\_viaggi\_conteggio\_da\_medallion\_license.hql* dati tariffa hello impostata su "medallion" e "hack_license" dei gruppi di file e restituisce i conteggi di ogni combinazione. Di seguito è riportato il contenuto del file.

    SELECT medallion, hack_license, COUNT(*) as trip_count
    FROM nyctaxidb.fare
    WHERE month=1
    GROUP BY medallion, hack_license
    HAVING trip_count > 100
    ORDER BY trip_count desc;

Questa query restituisce le combinazioni dei taxi e degli autisti, visualizzate in ordine decrescente in base al numero di corse.

Da hello Hive prompt dei comandi, eseguire:

    hive -f "C:\temp\sample_hive_trip_count_by_medallion_license.hql" > C:\temp\queryoutput.tsv

risultati della query Hello vengono scritti i file locale tooa C:\temp\queryoutput.tsv.

### <a name="exploration-assessing-data-quality-by-checking-for-invalid-longitudelatitude-records"></a>Esplorazione: valutazione della qualità dei dati mediante il controllo del record di longitudine/latitudine non validi
> [!NOTE]
> In genere, questa attività viene svolta da un **data scientist** .
> 
> 

Degli obiettivi comune di analisi esplorativa dei dati è tooweed i record non valido. Hello riportato in questa sezione determina se sia hello longitudine o latitudine campi contengono un valore molto di fuori di hello area NYC. Poiché è probabile che i record contengono un valori di latitudine, longitudine errato, è necessario tooeliminate da tutti i dati che sono toobe utilizzati per la modellazione.

Di seguito è contenuto hello di *esempio\_hive\_qualità\_assessment.hql* file per l'ispezione.

        SELECT COUNT(*) FROM nyctaxidb.trip
        WHERE month=1
        AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(pickup_latitude AS float) NOT BETWEEN 30 AND 90
        OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(dropoff_latitude AS float) NOT BETWEEN 30 AND 90);


Da hello Hive prompt dei comandi, eseguire:

    hive -S -f "C:\temp\sample_hive_quality_assessment.hql"

Hello *-S* argomento incluso in questo comando Elimina l'immagine di schermata hello lo stato dei processi di MapReduce Hive hello. Ciò è utile perché rende più leggibile di output della query Hive stampa schermata hello di hello.

### <a name="exploration-binary-class-distributions-of-trip-tips"></a>Esplorazione: distribuzioni in classi binarie delle mance delle corse
> [!NOTE]
> In genere, questa attività viene svolta da un **data scientist** .
> 
> 

Per il problema di classificazione binaria hello descritto nella hello [esempi di attività di stima](machine-learning-data-science-process-hive-walkthrough.md#mltasks) sezione, è utile tooknow se è stato specificato un suggerimento o non. Questa distribuzione delle mance è di tipo binario:

* mancia offerta (classe 1, tip\_amount > $ 0)  
* nessuna mancia (classe 0, tip\_amount = $ 0).

Hello *esempio\_hive\_inclinato\_frequencies.hql* esegue questa operazione file riportato di seguito.

    SELECT tipped, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tipped;

Da hello Hive prompt dei comandi, eseguire:

    hive -f "C:\temp\sample_hive_tipped_frequencies.hql"


### <a name="exploration-class-distributions-in-hello-multiclass-setting"></a>: Esplorazione Le distribuzioni di classe in base alle impostazioni hello multiclasse
> [!NOTE]
> In genere, questa attività viene svolta da un **data scientist** .
> 
> 

Problema di classificazione multiclasse hello descritte nella hello [esempi di attività di stima](machine-learning-data-science-process-hive-walkthrough.md#mltasks) sezione questo set di dati può anche essere applicato tooa di classificazione naturale in cui desideriamo quantità hello toopredict dei suggerimenti hello specificato. È possibile usare gli intervalli di bin toodefine suggerimento nella query hello. tooget hello distribuzioni di classe per hello diversi intervalli di suggerimento, utilizziamo hello *esempio\_hive\_suggerimento\_intervallo\_frequencies.hql* file. Di seguito è riportato il contenuto del file.

    SELECT tip_class, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount=0, 0,
            if(tip_amount>0 and tip_amount<=5, 1,
            if(tip_amount>5 and tip_amount<=10, 2,
            if(tip_amount>10 and tip_amount<=20, 3, 4)))) as tip_class, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tip_class;

Eseguire hello comando seguente dalla riga di comando Hadoop console:

    hive -f "C:\temp\sample_hive_tip_range_frequencies.hql"

### <a name="exploration-compute-direct-distance-between-two-longitude-latitude-locations"></a>Esplorazione: calcolare la distanza diretta tra due posizioni di latitudine e longitudine
> [!NOTE]
> In genere, questa attività viene svolta da un **data scientist** .
> 
> 

Presenza di una misura della distanza diretto hello consente toofind out discrepanza hello tra i file e hello effettivo attivarsi distanza. Questa funzionalità è motivare identificando che potrebbero essere minore di passeggeri tootip probabile se essi individuare tale driver hello è intenzionalmente usato li da strada molto più lunga.

confronto di hello toosee tra distanza effettiva di andata e ritorno e hello [distanza Haversine](http://en.wikipedia.org/wiki/Haversine_formula) tra i due punti di longitudine latitudine (distanza di hello "circle eccellente"), utilizziamo funzioni trigonometriche hello disponibili all'interno di Hive, in questo modo:

    set R=3959;
    set pi=radians(180);

    insert overwrite directory 'wasb:///queryoutputdir'

    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
    ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
     *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
     *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
     /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
     +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
     pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
    from nyctaxidb.trip
    where month=1
    and pickup_longitude between -90 and -30
    and pickup_latitude between 30 and 90
    and dropoff_longitude between -90 and -30
    and dropoff_latitude between 30 and 90;

Nella query hello sopra, R è raggio hello hello terra in miglia e pi greco è tooradians convertito. Si noti che i punti di longitudine latitudine hello sono i valori "filtrato" tooremove distanti da area NYC hello.

In questo caso, è scrivere la directory dei risultati tooa chiamato "queryoutputdir". Hello sequenza di comandi illustrata di seguito crea innanzitutto la directory di output e quindi esegue hello Hive.

Da hello Hive prompt dei comandi, eseguire:

    hdfs dfs -mkdir wasb:///queryoutputdir

    hive -f "C:\temp\sample_hive_trip_direct_distance.hql"


Hello risultati della query vengono scritti i BLOB Azure too9 ***queryoutputdir/000000\_0*** troppo ***queryoutputdir/000008\_0*** sotto il contenitore predefinito hello del cluster Hadoop hello.

dimensioni di hello toosee dei singoli BLOB hello, eseguiamo hello comando seguente dal prompt dei comandi di hello Hive directory:

    hdfs dfs -ls wasb:///queryoutputdir

contenuto di hello toosee di un determinato file, ad esempio 000000\_0, utilizziamo Hadoop `copyToLocal` comando, di conseguenza.

    hdfs dfs -copyToLocal wasb:///queryoutputdir/000000_0 C:\temp\tempfile

> [!WARNING]
> In presenza di file di grandi dimensioni, l'operazione `copyToLocal` può essere molto lenta e non è quindi consigliabile.  
> 
> 

Dei principali vantaggi di avere tali dati si trovano in un blob di Azure è che si può esplorare i dati di hello all'interno di Azure Machine Learning che usano hello [l'importazione dei dati] [ import-data] modulo.

## <a name="#downsample"></a>Sottocampionare i dati e creare modelli in Azure Machine Learning
> [!NOTE]
> In genere, questa attività viene svolta da un **data scientist** .
> 
> 

Dopo la fase di analisi esplorativa dati hello, siamo ora in dati di hello esempio toodown pronto per la creazione di modelli in Azure Machine Learning. In questa sezione viene illustrato come eseguire una query toodown dati esempio hello, che sono quindi accessibile dalla hello toouse un Hive [l'importazione dei dati] [ import-data] modulo in Azure Machine Learning.

### <a name="down-sampling-hello-data"></a>Il campionamento dei dati hello verso il basso
Questa procedura si articola in due passaggi. Innanzitutto è aggiungere hello **nyctaxidb.trip** e **nyctaxidb.fare** tabelle in tre le chiavi presenti in tutti i record: "medallion", "hack\_licenza", e "prelievo\_datetime". È quindi possibile generare un'etichetta di classificazione binaria **tipped** e un'etichetta di classificazione multiclasse **tip\_class**.

toobe toouse in grado di hello verso il basso dati campionati direttamente da hello [l'importazione dei dati] [ import-data] modulo in Azure Machine Learning, è necessario toostore risultati di hello di hello sopra la tabella query tooan interna Hive. In seguito, si crea una tabella interna di Hive e popola il relativo contenuto con hello unita e verso il basso dati campionati.

query Hello applica funzioni standard di Hive direttamente il toogenerate hello ora del giorno, settimana dell'anno, giorno della settimana (1 sta per lunedì e 7 sta per domenica) da hello "prelievo\_datetime" campo e hello distanza diretta tra il prelievo di hello e dropoff percorsi. Gli utenti possono fare riferimento troppo[LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) per un elenco completo di tali funzioni.

Hello query quindi verso il basso di dati di campioni hello in modo che i risultati della query hello rientrino in hello Azure Machine Learning Studio. Solo circa l'1% del set di dati originale hello viene importato in hello Studio.

Di seguito sono contenuti hello di *esempio\_hive\_preparare\_per\_aml\_full.hql* in grado di preparare i dati per il modello di compilazione in Azure Machine Learning.

        set R = 3959;
        set pi=radians(180);

        create table if not exists nyctaxidb.nyctaxi_downsampled_dataset (

        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        pickup_hour string,
        pickup_week string,
        weekday string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double,
        direct_distance double,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double,
        tipped string,
        tip_class string
        )
        row format delimited fields terminated by ','
        lines terminated by '\n'
        stored as textfile;

        --- now insert contents of hello join into hello above internal table

        insert overwrite table nyctaxidb.nyctaxi_downsampled_dataset
        select
        t.medallion,
        t.hack_license,
        t.vendor_id,
        t.rate_code,
        t.store_and_fwd_flag,
        t.pickup_datetime,
        t.dropoff_datetime,
        hour(t.pickup_datetime) as pickup_hour,
        weekofyear(t.pickup_datetime) as pickup_week,
        from_unixtime(unix_timestamp(t.pickup_datetime, 'yyyy-MM-dd HH:mm:ss'),'u') as weekday,
        t.passenger_count,
        t.trip_time_in_secs,
        t.trip_distance,
        t.pickup_longitude,
        t.pickup_latitude,
        t.dropoff_longitude,
        t.dropoff_latitude,
        t.direct_distance,
        f.payment_type,
        f.fare_amount,
        f.surcharge,
        f.mta_tax,
        f.tip_amount,
        f.tolls_amount,
        f.total_amount,
        if(tip_amount>0,1,0) as tipped,
        if(tip_amount=0,0,
        if(tip_amount>0 and tip_amount<=5,1,
        if(tip_amount>5 and tip_amount<=10,2,
        if(tip_amount>10 and tip_amount<=20,3,4)))) as tip_class

        from
        (
        select
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        pickup_datetime,
        dropoff_datetime,
        passenger_count,
        trip_time_in_secs,
        trip_distance,
        pickup_longitude,
        pickup_latitude,
        dropoff_longitude,
        dropoff_latitude,
        ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
        *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
        +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance,
        rand() as sample_key

        from nyctaxidb.trip
        where pickup_latitude between 30 and 90
            and pickup_longitude between -90 and -30
            and dropoff_latitude between 30 and 90
            and dropoff_longitude between -90 and -30
        )t
        join
        (
        select
        medallion,
        hack_license,
        vendor_id,
        pickup_datetime,
        payment_type,
        fare_amount,
        surcharge,
        mta_tax,
        tip_amount,
        tolls_amount,
        total_amount
        from nyctaxidb.fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01

toorun questa query, dalla directory Hive hello richiesta:

    hive -f "C:\temp\sample_hive_prepare_for_aml_full.hql"

Avere una tabella interna "nyctaxidb.nyctaxi_downsampled_dataset", che è possibile accedere tramite hello [l'importazione dei dati] [ import-data] modulo da Azure Machine Learning. Inoltre, sarà possibile usare questo set di dati per la creazione di modelli di Machine Learning.  

### <a name="use-hello-import-data-module-in-azure-machine-learning-tooaccess-hello-down-sampled-data"></a>Usare il modulo di importazione dei dati hello in hello tooaccess Azure Machine Learning verso il basso dati campionati
Prerequisiti per eseguire una query Hive in hello [l'importazione dei dati] [ import-data] modulo di Azure Machine Learning, è necessario accedere tooan Azure Machine Learning area di lavoro e accedere alle credenziali toohello di hello cluster e il relativo account di archiviazione associato.

Alcuni dettagli su hello [l'importazione dei dati] [ import-data] modulo e hello tooinput parametri:

**URI del server HCatalog**: se il nome del cluster hello abc123, allora si tratta semplicemente: https://abc123.azurehdinsight.net

**Nome dell'account utente Hadoop** : nome utente hello scelto per il cluster hello (**non** nome utente di accesso remoto hello)

**Password dell'account utente Hadoop** : password hello scelta per il cluster hello (**non** password di accesso remoto hello)

**Percorso dei dati di output** : si è scelto toobe Azure.

**Nome dell'account di archiviazione Azure** : nome dell'account di archiviazione predefinito hello associato hello cluster.

**Nome del contenitore di Azure** : nome del contenitore predefinito hello per cluster hello è e viene in genere hello stesso come nome del cluster hello. Per un cluster denominato "abc123", il nome del contenitore è semplicemente abc123.

> [!IMPORTANT]
> **Qualsiasi tabella a cui si desidera tooquery utilizzando hello [l'importazione dei dati] [ import-data] modulo in Azure Machine Learning deve essere una tabella interna.** Di seguito è riportato un suggerimento per determinare se una tabella T in un database D.db è una tabella interna.
> 
> 

Da hello Hive prompt dei comandi, problema hello comando:

    hdfs dfs -ls wasb:///D.db/T

Se la tabella hello è una tabella interna e viene compilata, il relativo contenuto deve essere visualizzato qui. Un altro modo toodetermine, se la tabella è una tabella interna è toouse hello Azure Storage Explorer. Utilizzare il nome del contenitore predefinito toohello toonavigate del cluster hello e quindi filtrare in base al nome di tabella hello. Se la tabella hello e il relativo contenuto è presente, questo errore conferma che è una tabella interna.

Ecco uno snapshot della query Hive hello e hello [l'importazione dei dati] [ import-data] modulo:

![Query Hive per il modulo di importazione dei dati](./media/machine-learning-data-science-process-hive-walkthrough/1eTYf52.png)

Si noti che poiché il nostro giù dati campionati risiedono nel contenitore predefinito hello, query Hive risultante hello da Azure Machine Learning è molto semplice ed è solo un "Seleziona * da nyctaxidb.nyctaxi\_sottocampionate\_dati".

set di dati Hello può ora essere usato come punto di partenza per la creazione di modelli di Machine Learning hello.

### <a name="mlmodel"></a>Creare modelli in Azure Machine Learning
Sono ora in grado di tooproceed toomodel compilazione e distribuzione di modelli in [Azure Machine Learning](https://studio.azureml.net). dati Hello sono pronti per noi toouse nella risoluzione dei problemi di stima hello identificati in precedenza:

**1. Classificazione binaria**: toopredict o meno un suggerimento è stato pagato per un itinerario.

**Strumento di apprendimento usato:** regressione logistica a due classi

a. Per questo problema, l'etichetta (o classe) di destinazione è "tipped". Il set di dati sottocampionati originale dispone di alcune colonne che indicano le perdite di destinazione per questo esperimento di classificazione. In particolare: suggerimento\_classe, suggerimento\_quantità e totale\_importo rivelare informazioni etichetta di destinazione hello che non è disponibile in fase di test. È rimuovere queste colonne dalla considerazione utilizzando hello [selezionare le colonne nel set di dati] [ select-columns] modulo.

snapshot Hello seguente mostra il nostro toopredict esperimento o meno un suggerimento è stato pagato per un determinato andata e ritorno.

![Snapshot esperimento](./media/machine-learning-data-science-process-hive-walkthrough/QGxRz5A.png)

b. Per questo esperimento, le distribuzioni dell'etichetta di destinazione sono approssimativamente 1:1.

snapshot Hello riportato di seguito mostra distribuzione hello etichette di classe suggerimento per il problema di classificazione binaria hello.

![Distribuzione delle etichette della classe relativa alla mancia](./media/machine-learning-data-science-process-hive-walkthrough/9mM4jlD.png)

Di conseguenza, si ottengono un AUC di 0.987 come illustrato nella figura che segue hello.

![Valore AUC](./media/machine-learning-data-science-process-hive-walkthrough/8JDT0F8.png)

**2. Classificazione multiclasse**: intervallo di hello toopredict degli importi di suggerimento pagato viaggi hello, utilizzate in precedenza hello classi definite.

**Strumento di apprendimento usato:** regressione logistica multiclasse

a. Per questo problema, l'etichetta (o classe) di destinazione è "tip\_class", che può assumere uno dei cinque valori (0, 1, 2, 3, 4). Come nel caso di classificazione binaria hello, sono disponibili alcune colonne che sono le perdite di destinazione per questa sperimentazione. In particolare: inclinato, suggerimento\_importo totale\_importo rivelare informazioni etichetta di destinazione hello che non è disponibile in fase di test. È rimuovere queste colonne con hello [selezionare le colonne nel set di dati] [ select-columns] modulo.

Hello snapshot seguente viene illustrato il nostro toopredict esperimento collocazione un suggerimento è probabilmente toofall (classe 0: suggerimento = $0, la classe 1: suggerimento > $0 e suggerimento < = $5, classe 2: suggerimento > $5 e suggerimento < = $10, classe 3: suggerimento > 10 e suggerimento < = $20 Classe 4: suggerimento > $20)

![Snapshot esperimento](./media/machine-learning-data-science-process-hive-walkthrough/5ztv0n0.png)

Di seguito è illustrata la distribuzione della classe di test effettiva. Vediamo che mentre la classe 0 e 1 di classe sono più comuni, hello altre classi sono rari.

![Distribuzione della classe di test](./media/machine-learning-data-science-process-hive-walkthrough/Vy1FUKa.png)

b. Per questo esercizio, usato un toolook di una matrice di confusione l'accuratezza della stima. come illustrato di seguito.

![Matrice di confusione](./media/machine-learning-data-science-process-hive-walkthrough/cxFmErM.png)

Si noti che mentre le accuratezze la classe in classi prevalente hello è abbastanza efficace, modello hello non esegue un processo valido di "apprendimento" nelle classi rari hello.

**3. Attività di regressione**: quantità di hello toopredict del suggerimento a pagamento per un itinerario.

**Strumento di apprendimento usato:** albero delle decisioni con boosting

a. Per questo problema, l'etichetta (o classe) di destinazione è "tiptip\_amount". In questo caso sono i problemi di destinazione: inclinato, suggerimento\_(classe), totale\_quantità, tutte queste variabili rivelare informazioni sulla quantità di suggerimento hello che non è in genere disponibile in fase di test. È rimuovere queste colonne con hello [selezionare le colonne nel set di dati] [ select-columns] modulo.

Hello snapshot belows Mostra la quantità di hello toopredict esperimento di hello suggerimento fornito.

![Snapshot esperimento](./media/machine-learning-data-science-process-hive-walkthrough/11TZWgV.png)

b. Per i problemi di regressione è misurare le accuratezze hello del nostro stima esaminando l'errore quadrato hello nelle stime hello, hello coefficiente di determinazione e hello come. come illustrato di seguito.

![Statistiche di stima](./media/machine-learning-data-science-process-hive-walkthrough/Jat9mrz.png)

È possibile notare che sulla hello coefficiente di determinazione 0.709, implicando 71% circa della varianza hello è spiegato dai nostri coefficienti di modello.

> [!IMPORTANT]
> informazioni su Azure Machine Learning toolearn e come tooaccess e usarlo, vedere troppo[novità Machine Learning?](machine-learning-what-is-machine-learning.md). Una risorsa molto utile per la riproduzione con una serie di esperimenti di Machine Learning in Azure Machine Learning è hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/). Raccolta di Hello riguarda una gamma di esperimenti e viene fornita un'introduzione approfondita nell'intervallo di hello delle funzionalità di Azure Machine Learning.
> 
> 

## <a name="license-information"></a>Informazioni sulla licenza
In questa procedura dettagliata di esempio e i relativi script associati vengono condivisi da Microsoft con licenza MIT hello. Nella directory di hello del codice di esempio hello su GitHub per ulteriori dettagli, controllare file License hello in.

## <a name="references"></a>Riferimenti
•    [Pagina di Andrés Monroy per scaricare i dati sulle corse dei taxi di NYC](http://www.andresmh.com/nyctaxitrips/)  
•    [Complemento dai dati sulle corse dei taxi di NYC di Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/)   
•    [Ricerche e statistiche su NYC Taxi and Limousine Commission](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)

[2]: ./media/machine-learning-data-science-process-hive-walkthrough/output-hive-results-3.png
[11]: ./media/machine-learning-data-science-process-hive-walkthrough/hive-reader-properties.png
[12]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-training.png
[13]: ./media/machine-learning-data-science-process-hive-walkthrough/create-scoring-experiment.png
[14]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-scoring.png
[15]: ./media/machine-learning-data-science-process-hive-walkthrough/amlreader.png

<!-- Module References -->
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
