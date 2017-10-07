---
title: 'Analisi scientifica dei dati scalabile in Azure Data Lake: procedura dettagliata end-to-end | Documentazione Microsoft'
description: "Modalità toouse Azure Data Lake toodo l'esplorazione e binario classificazione dei dati di attività da un set di dati."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 91a8207f-1e57-4570-b7fc-7c5fa858ffeb
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: bradsev;weig
ms.openlocfilehash: 8b05457ae7045a7aaed350a7502469f2247161e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scalable-data-science-with-azure-data-lake-an-end-to-end-walkthrough"></a>Analisi scientifica dei dati scalabile in Azure Data Lake: procedura dettagliata end-to-end
Questa procedura dettagliata illustra come toouse Azure Data Lake toodo l'esplorazione dei dati e le attività di classificazione binaria a un campione di hello NYC taxi di andata e ritorno e tariffa toopredict set di dati da una tariffa verrà corrisposto un suggerimento o meno. Contiene passaggi hello di hello [processo di analisi scientifica dei dati di Team](http://aka.ms/datascienceprocess), end-to-end, dalla formazione toomodel acquisizione di dati, quindi toohello distribuzione di un servizio web che pubblica il modello di hello.

### <a name="azure-data-lake-analytics"></a>Azure Data Lake Analytics.
Hello [Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) ha tutti toomake necessarie di funzionalità hello è più facile per i dati toostore gli esperti di dati di qualsiasi dimensione, forma e velocità e tooconduct elaborazione dei dati avanzate analitica e modellazione di machine learning con elevata scalabilità in un modo economico.   Il pagamento viene effettuato per i singoli processi, solo quando i dati vengono effettivamente elaborati. Azure Data Lake Analitica include U-SQL, un linguaggio che blend hello natura dichiarativa di SQL con la potenza espressiva hello di c# tooprovide scalabile distributed funzionalità di query. Abilita tooprocess dati non strutturati tramite l'applicazione dello schema in lettura, inserire la logica personalizzata e definiti dall'utente (UDF) funzioni e include estendibilità tooenable con granularità fine un controllo accurato sul modo in tooexecute su larga scala. toolearn ulteriori informazioni su filosofia di progettazione hello U-SQL, vedere [post di blog di Visual Studio](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).

Analisi Data Lake è anche un componente chiave di Cortana Analytics Suite e si integra con Azure SQL Data Warehouse, Power BI e Data Factory, per offrire una piattaforma completa per Big Data sul cloud e per le analisi avanzate.

Questa procedura dettagliata inizia con la descrizione hello prerequisiti e risorse che sono necessari toocomplete hello attività con Data Lake Analitica che formano processo di analisi scientifica dei dati hello e come tooinstall li. Quindi vengono delineati i passaggi di elaborazione dei dati hello utilizzando U-SQL e si conclude con la visualizzazione come toouse Python e Hive con Azure Machine Learning Studio toobuild e distribuire modelli predittivi hello. 

### <a name="u-sql-and-visual-studio"></a>U-SQL e Visual Studio
Questa procedura dettagliata consiglia l'utilizzo di set di dati di Visual Studio tooedit U-SQL script tooprocess hello. script U-SQL Hello sono descritti di seguito e fornite in un file separato. il processo di Hello include l'inserimento di esplorazione e il campionamento dei dati di hello. Viene inoltre illustrato come toorun U-SQL nello script di processo da hello portale di Azure. Hive tabelle vengono create per i dati di hello in una compilazione associata dell'hello toofacilitate del cluster HDInsight e la distribuzione di un modello di classificazione binaria in Azure Machine Learning Studio.  

### <a name="python"></a>Python
Questa procedura dettagliata contiene inoltre una sezione che illustra come toobuild e distribuire un modello predittivo tramite Python con Azure Machine Learning Studio.  Viene fornito un server Jupyter notebook con script Python hello per questi passaggi del processo. blocco appunti Hello includono il codice per alcuni passaggi di progettazione di funzionalità aggiuntive e la costruzione di modelli, ad esempio multiclasse classificazione e regressione modellazione inoltre il modello di classificazione binaria toohello descritto di seguito. attività di regressione Hello è toopredict hello suggerimento hello in base alle altre funzionalità di suggerimento. 

### <a name="azure-machine-learning"></a>Azure Machine Learning
Azure Machine Learning Studio è toobuild utilizzato e distribuire modelli predittivi hello. Queste operazioni possono essere eseguite adottando un duplice approccio: prima con gli script Python e quindi con le tabelle Hive in un cluster HDInsight (Hadoop).

### <a name="scripts"></a>Script
Solo i passaggi principali hello sono descritte in questa procedura dettagliata. È possibile scaricare hello completo **script U-SQL** e **server Jupyter Notebook** da [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare a questi argomenti, è necessario disporre delle seguenti hello:

* Una sottoscrizione di Azure. Se non è già disponibile, vedere l'articolo che illustra [come ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* [Consigliato] Visual Studio 2013 o versione successiva. Se non è già installata una di queste versioni, è possibile scaricare una versione Community gratuita da [Visual Studio Community](https://www.visualstudio.com/vs/community/).

> [!NOTE]
> Invece di Visual Studio, è possibile utilizzare anche le query di Azure Data Lake toosubmit di hello portale di Azure. È verranno fornite istruzioni su come toodo così con Visual Studio e nel portale di hello nella sezione hello intitolata **elaborano i dati con U-SQL**. 
> 
> 


## <a name="prepare-data-science-environment-for-azure-data-lake"></a>Preparare un ambiente di analisi scientifica dei dati per Azure Data Lake
ambiente di analisi scientifica dei dati hello tooprepare per questa procedura dettagliata, creare hello seguenti risorse:

* Archivio Azure Data Lake (ADLS) 
* Analisi Azure Data Lake (ADLA)
* Account di archiviazione BLOB di Azure
* Account di Azure Machine Learning Studio
* Azure Data Lake Tools per Visual Studio (consigliato)

In questa sezione vengono fornite istruzioni su come toocreate di queste risorse. Se si scelgono toouse tabelle Hive con Azure Machine Learning, invece di Python, toobuild un modello, è necessario anche tooprovision un cluster HDInsight (Hadoop). In questa procedura alternativa descritta nella sezione appropriata a hello riportato di seguito.


> [!NOTE]
> Hello **archivio Azure Data Lake** è possibile creare separatamente o quando si crea hello **Azure Data Lake Analitica** come spazio di archiviazione predefinito hello. Le istruzioni fanno riferimento per la creazione di ciascuna di queste risorse separatamente di seguito, ma hello account archivio Data Lake non è necessario crearli separatamente.
>
> 

### <a name="create-an-azure-data-lake-store"></a>Creare un Archivio Azure Data Lake


Creare un ADLS da hello [portale Azure](http://portal.azure.com). Per informazioni dettagliate, vedere [Creare un cluster HDInsight con Archivio Data Lake tramite il portale di Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md). Essere tooset che di identità AAD Cluster Ciao hello **DataSource** blade di hello **configurazione facoltativa** pannello descritto non esiste. 

 ![3](./media/machine-learning-data-science-process-data-lake-walkthrough/3-create-ADLS.PNG)

### <a name="create-an-azure-data-lake-analytics-account"></a>Creare un account di Analisi Azure Data Lake
Creare un account ADLA da hello [portale Azure](http://portal.azure.com). Per informazioni dettagliate, vedere [Esercitazione: Introduzione ad Analisi Azure Data Lake con il portale di Azure](../data-lake-analytics/data-lake-analytics-get-started-portal.md). 

 ![4](./media/machine-learning-data-science-process-data-lake-walkthrough/4-create-ADLA-new.PNG)

### <a name="create-an-azure-blob-storage-account"></a>Creare un account di archiviazione BLOB di Azure
Creare un account di archiviazione Blob di Azure da hello [portale Azure](http://portal.azure.com). Per informazioni dettagliate, vedere hello crea un account di archiviazione sezione [gli account di archiviazione di Azure su](../storage/common/storage-create-storage-account.md).

 ![5](./media/machine-learning-data-science-process-data-lake-walkthrough/5-Create-Azure-Blob.PNG)

### <a name="set-up-an-azure-machine-learning-studio-account"></a>Configurare un account di Azure Machine Learning Studio
Accedere in Azure Machine Learning Studio da hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) pagina. Fare clic su hello **iniziare** pulsante e quindi scegliere un' "Area di lavoro disponibile" o "Area di lavoro Standard". In seguito sarà in grado di toocreate esperimenti in Azure Machine Learning Studio.  

### <a name="install-azure-data-lake-tools-recommended"></a>Installare Azure Data Lake Tools [consigliato]
Installare Azure Data Lake Tools per la versione di Visual Studio in uso da [Azure Data Lake Tools per Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).

 ![6](./media/machine-learning-data-science-process-data-lake-walkthrough/6-install-ADL-tools-VS.PNG)

Dopo l'installazione di hello viene completata correttamente, aprire Visual Studio. Verrà visualizzato hello Data Lake scheda hello menu nella parte superiore di hello. Quando si accede all'account Azure, le risorse di Azure dovrebbero essere visualizzato nel riquadro sinistro di hello.

 ![7](./media/machine-learning-data-science-process-data-lake-walkthrough/7-install-ADL-tools-VS-done.PNG)

## <a name="hello-nyc-taxi-trips-dataset"></a>set di dati NYC Taxi trip Hello
Hello set di dati è utilizzati qui è un set di dati disponibile pubblicamente, hello [NYC Taxi trip dataset](http://www.andresmh.com/nyctaxitrips/). dati di andata e ritorno Taxi NYC Hello è costituita da circa 20GB di file CSV compressi (~ 48GB non compressi), registrazione 173 milioni hello e singoli trip tariffe a pagamento per ogni itinerario. Ogni record di andata e ritorno include percorsi di ritiro e deposito hello e volte, resi anonimi hack numero di patente) (e hello numero medallion (id univoco del taxi). dati Hello copre tutti i percorsi nell'anno hello 2013 e viene forniti in hello dopo i due set di dati per ogni mese:

* Hello 'trip_data' CSV contiene i dettagli di andata e ritorno, ad esempio il numero di passeggeri, prelievo e dropoff punti, la durata del viaggio e lunghezza di andata e ritorno. Di seguito vengono forniti alcuni record di esempio:
  
       medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count, trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
* Hello 'trip_fare' CSV contiene i dettagli della tariffa di hello pagata per ogni itinerario, ad esempio il tipo di pagamento, quantità tariffa, supplemento e le imposte, suggerimenti e pedaggio e hello totale pagato. Di seguito vengono forniti alcuni record di esempio:
  
       medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

viaggi toojoin chiave univoca Hello\_dati e andata e ritorno\_tariffa è costituito da tre campi seguenti hello: medallion, le maggiori\_licenza e prelievo\_datetime. il file CSV non elaborati di Hello sono accessibili da un blob di archiviazione di Azure pubblico. Hello script U-SQL per il join è in hello [Join di tabelle di andata e ritorno e tariffa](#join) sezione.

## <a name="process-data-with-u-sql"></a>Elaborare i dati con U-SQL
le attività di elaborazione dei dati Hello illustrate in questa sezione includono l'inserimento, controllo della qualità, esplorazione e il campionamento dei dati di hello. Vengono inoltre illustrati come tabelle di andata e ritorno e tariffa toojoin. la sezione finale Hello Mostra esecuzione un processo con script U-SQL da hello portale di Azure. Di seguito sono riportati collegamenti sottosezione tooeach:

* [Inserimento di dati: leggere dati dal BLOB pubblico](#ingest)
* [Controlli della qualità dei dati](#quality)
* [Esplorazione dei dati](#explore)
* [Unire le tabelle relative a corse e tariffe](#join)
* [Campionamento dei dati](#sample)
* [Eseguire processi U-SQL](#run)

script U-SQL Hello sono descritti di seguito e fornite in un file separato. È possibile scaricare hello completo **script U-SQL** da [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).

tooexecute U-SQL, aprire Visual Studio, fare clic su **File--> Nuovo--> progetto**, scegliere **progetto U-SQL**, denominare e salvare la cartella tooa.

![8](./media/machine-learning-data-science-process-data-lake-walkthrough/8-create-USQL-project.PNG)

> [!NOTE]
> È possibile toouse hello Azure Portal tooexecute U-SQL anziché Visual Studio. È possibile esplorare risorse di Azure Data Lake Analitica toohello nel portale di hello e inviare query direttamente come illustrato nella seguente illustrazione hello.
> 
> 

![9](./media/machine-learning-data-science-process-data-lake-walkthrough/9-portal-submit-job.PNG)

### <a name="ingest"></a>Inserimento di dati: leggere dati dal BLOB pubblico
percorso Hello dati hello in hello blob di Azure viene fatto riferimento come  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**  e possono essere estratte con **Extractors.Csv()**. Sostituire il nome di contenitore e il nome di account di archiviazione negli script seguenti per container_name@blob_storage_account_name indirizzo wasb hello. Poiché i nomi di file hello sono nello stesso formato, è possibile utilizzare **viaggi\_data_ {\*\}CSV** tooread in tutti i file di andata e ritorno 12. 

    ///Read in Trip data
    @trip0 =
        EXTRACT 
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string
    // This is reading 12 trip data from blob
    FROM "wasb://container_name@blob_storage_account_name.blob.core.windows.net/nyctaxitrip/trip_data_{*}.csv"
    USING Extractors.Csv();

Poiché sono presenti intestazioni nella prima riga hello, è necessario intestazioni hello tooremove e modificare i tipi di colonna in quelli appropriati. È possibile salvare hello elaborato dati tooAzure Data Lake di archiviazione usando **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**account tramite l'archiviazione Blob _ o tooAzure  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** . 

    // change data types
    @trip =
        SELECT 
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        DateTime.Parse(pickup_datetime) AS pickup_datetime,
        DateTime.Parse(dropoff_datetime) AS dropoff_datetime,
        Int32.Parse(passenger_count) AS passenger_count,
        Double.Parse(trip_time_in_secs) AS trip_time_in_secs,
        Double.Parse(trip_distance) AS trip_distance,
        (pickup_longitude==string.Empty ? 0: float.Parse(pickup_longitude)) AS pickup_longitude,
        (pickup_latitude==string.Empty ? 0: float.Parse(pickup_latitude)) AS pickup_latitude,
        (dropoff_longitude==string.Empty ? 0: float.Parse(dropoff_longitude)) AS dropoff_longitude,
        (dropoff_latitude==string.Empty ? 0: float.Parse(dropoff_latitude)) AS dropoff_latitude
    FROM @trip0
    WHERE medallion != "medallion";

    ////output data tooADL
    OUTPUT @trip   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_trip.csv"
    USING Outputters.Csv(); 

    ////Output data tooblob
    OUTPUT @trip   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_trip.csv"
    USING Outputters.Csv();  

Analogamente è possibile leggere hello tariffa ai set di dati. Fare clic con il pulsante destro archivio Azure Data Lake, è possibile scegliere toolook i dati in **portale di Azure--> Esplora dati** o **Esplora File** all'interno di Visual Studio. 

 ![10](./media/machine-learning-data-science-process-data-lake-walkthrough/10-data-in-ADL-VS.PNG)

 ![11](./media/machine-learning-data-science-process-data-lake-walkthrough/11-data-in-ADL.PNG)

### <a name="quality"></a>Controlli della qualità dei dati
Dopo che è stato letto di andata e ritorno e tariffa tabelle, i controlli di qualità dei dati possono essere eseguiti nel seguente modo hello. Hello file CSV risultante può essere archiviazione Blob di output tooAzure o archivio Azure Data Lake. 

Trovare il numero di hello di medallions e un numero univoco di medallions:

    ///check hello number of medallions and unique number of medallions
    @trip2 =
        SELECT
        medallion,
        vendor_id,
        pickup_datetime.Month AS pickup_month
        FROM @trip;

    @ex_1 =
        SELECT
        pickup_month, 
        COUNT(medallion) AS cnt_medallion,
        COUNT(DISTINCT(medallion)) AS unique_medallion
        FROM @trip2
        GROUP BY pickup_month;
        OUTPUT @ex_1   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_1.csv"
    USING Outputters.Csv(); 

È possibile trovare le licenze associate a più di 100 corse:

    ///find those medallions that had more than 100 trips
    @ex_2 =
        SELECT medallion,
               COUNT(medallion) AS cnt_medallion
        FROM @trip2
        //where pickup_datetime >= "2013-01-01t00:00:00.0000000" and pickup_datetime <= "2013-04-01t00:00:00.0000000"
        GROUP BY medallion
        HAVING COUNT(medallion) > 100;
        OUTPUT @ex_2   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_2.csv"
    USING Outputters.Csv(); 

È possibile trovare i record non validi a livello di valore pickup_longitude:

    ///find those invalid records in terms of pickup_longitude
    @ex_3 =
        SELECT COUNT(medallion) AS cnt_invalid_pickup_longitude
        FROM @trip
        WHERE
        pickup_longitude <- 90 OR pickup_longitude > 90;
        OUTPUT @ex_3   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_3.csv"
    USING Outputters.Csv(); 

È possibile trovare i valori mancanti per alcune variabili:

    //check missing values
    @res =
        SELECT *,
               (medallion == null? 1 : 0) AS missing_medallion
        FROM @trip;

    @trip_summary6 =
        SELECT 
            vendor_id,
        SUM(missing_medallion) AS medallion_empty, 
        COUNT(medallion) AS medallion_total,
        COUNT(DISTINCT(medallion)) AS medallion_total_unique  
        FROM @res
        GROUP BY vendor_id;
    OUTPUT @trip_summary6
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_16.csv"
    USING Outputters.Csv();



### <a name="explore"></a>Esplorazione dei dati
È possibile eseguire alcune tooget l'esplorazione dei dati come una migliore comprensione dei dati di hello.

Trovare la distribuzione hello di trip inclinato e non inclinato:

    ///tipped vs. not tipped distribution
    @tip_or_not =
        SELECT *,
               (tip_amount > 0 ? 1: 0) AS tipped
        FROM @fare;

    @ex_4 =
        SELECT tipped,
               COUNT(*) AS tip_freq
        FROM @tip_or_not
        GROUP BY tipped;
        OUTPUT @ex_4   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_4.csv"
    USING Outputters.Csv(); 

Trovare la distribuzione hello della quantità di suggerimento con valori di taglio: 0,5,10 e 20 dollari.

    //tip class/range distribution
    @tip_class =
        SELECT *,
               (tip_amount >20? 4: (tip_amount >10? 3:(tip_amount >5 ? 2:(tip_amount > 0 ? 1: 0)))) AS tip_class
        FROM @fare;
    @ex_5 =
        SELECT tip_class,
               COUNT(*) AS tip_freq
        FROM @tip_class
        GROUP BY tip_class;
        OUTPUT @ex_5   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_5.csv"
    USING Outputters.Csv(); 

È possibile trovare le statistiche di base relative alla distanza della corsa:

    // find basic statistics for trip_distance
    @trip_summary4 =
        SELECT 
            vendor_id,
            COUNT(*) AS cnt_row,
            MIN(trip_distance) AS min_trip_distance,
            MAX(trip_distance) AS max_trip_distance,
            AVG(trip_distance) AS avg_trip_distance 
        FROM @trip
        GROUP BY vendor_id;
    OUTPUT @trip_summary4
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_14.csv"
    USING Outputters.Csv();

Trovare i percentili hello della distanza di andata e ritorno:

    // find percentiles of trip_distance
    @trip_summary3 =
        SELECT DISTINCT vendor_id AS vendor,
                        PERCENTILE_DISC(0.25) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.5) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.75) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc
        FROM @trip;
       // group by vendor_id;
    OUTPUT @trip_summary3
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_13.csv"
    USING Outputters.Csv(); 


### <a name="join"></a>Unire le tabelle relative a corse e tariffe
Le tabelle relative alle corse e alle tariffe possono essere unite in base ai valori medallion, hack_license e pickup_time.

    //join trip and fare table

    @model_data_full =
    SELECT t.*, 
    f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,  f.total_amount, f.tip_amount,
    (f.tip_amount > 0 ? 1: 0) AS tipped,
    (f.tip_amount >20? 4: (f.tip_amount >10? 3:(f.tip_amount >5 ? 2:(f.tip_amount > 0 ? 1: 0)))) AS tip_class
    FROM @trip AS t JOIN  @fare AS f
    ON   (t.medallion == f.medallion AND t.hack_license == f.hack_license AND t.pickup_datetime == f.pickup_datetime)
    WHERE   (pickup_longitude != 0 AND dropoff_longitude != 0 );

    //// output tooblob
    OUTPUT @model_data_full   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 

    ////output data tooADL
    OUTPUT @model_data_full   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 


Per ogni livello del conteggio di passeggeri, calcolare il numero di hello di record, quantità media di suggerimento, la varianza della quantità di suggerimento, percentuale di viaggi inclinati.

    // contigency table
    @trip_summary8 =
        SELECT passenger_count,
               COUNT(*) AS cnt,
               AVG(tip_amount) AS avg_tip_amount,
               VAR(tip_amount) AS var_tip_amount,
               SUM(tipped) AS cnt_tipped,
               (float)SUM(tipped)/COUNT(*) AS pct_tipped
        FROM @model_data_full
        GROUP BY passenger_count;
        OUTPUT @trip_summary8
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_17.csv"
    USING Outputters.Csv();


### <a name="sample"></a>Campionamento dei dati
È in modo casuale selezionare innanzitutto 0,1% dei dati hello tabella unita in join hello:

    //random select 1/1000 data for modeling purpose
    @addrownumberres_randomsample =
    SELECT *,
            ROW_NUMBER() OVER() AS rownum
    FROM @model_data_full;

    @model_data_random_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_randomsample
    WHERE rownum % 1000 == 0;

    OUTPUT @model_data_random_sample_1_1000   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_random_1_1000.csv"
    USING Outputters.Csv(); 

Eseguire quindi un campionamento stratificato in base alla variabile binaria tip_class:

    //stratified random select 1/1000 data for modeling purpose
    @addrownumberres_stratifiedsample =
    SELECT *,
            ROW_NUMBER() OVER(PARTITION BY tip_class) AS rownum
    FROM @model_data_full;

    @model_data_stratified_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_stratifiedsample
    WHERE rownum % 1000 == 0;
    //// output tooblob
    OUTPUT @model_data_stratified_sample_1_1000   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 
    ////output data tooADL
    OUTPUT @model_data_stratified_sample_1_1000   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 


### <a name="run"></a>Eseguire processi U-SQL
Al termine della modifica di script U-SQL, è possibile inviarli toohello server con l'account di Azure Data Lake Analitica. Fare clic su **Data Lake**, **Invia processo**, selezionare il proprio **account Analisi**, scegliere **Parallelismo** e fare clic sul pulsante **Invia**.  

 ![12](./media/machine-learning-data-science-process-data-lake-walkthrough/12-submit-USQL.PNG)

Quando processo hello è compilato correttamente, in Visual Studio verrà visualizzato lo stato di hello del processo per il monitoraggio. Al termine dell'esecuzione processo hello, è possibile anche riproduzione hello esecuzione processo e scoprire hello creare colli di bottiglia passaggi tooimprove l'efficienza del processo. È anche possibile passare tooAzure portale toocheck hello stato dei processi di U-SQL.

 ![13](./media/machine-learning-data-science-process-data-lake-walkthrough/13-USQL-running-v2.PNG)

 ![14](./media/machine-learning-data-science-process-data-lake-walkthrough/14-USQL-jobs-portal.PNG)

Ora è possibile controllare i file di output di hello in archiviazione Blob di Azure o il portale di Azure. Si utilizzerà i dati di esempio hello stratificato per la modellazione nel passaggio successivo hello.

 ![15](./media/machine-learning-data-science-process-data-lake-walkthrough/15-U-SQL-output-csv.PNG)

 ![16](./media/machine-learning-data-science-process-data-lake-walkthrough/16-U-SQL-output-csv-portal.PNG)

## <a name="build-and-deploy-models-in-azure-machine-learning"></a>Compilare e distribuire modelli in Azure Machine Learning
Viene descritto come due opzioni disponibili per i dati toopull in Azure Machine Learning toobuild e 

* Nella prima opzione hello, utilizzare i dati campionato hello che sono stato scritto tooan Blob di Azure (in hello **campionamento dei dati** passaggio precedente) e utilizzare toobuild Python e distribuire modelli da Azure Machine Learning. 
* Nella seconda opzione hello, viene eseguita una query hello in Azure Data Lake direttamente tramite una query Hive. Questa opzione richiede di creare un nuovo cluster di HDInsight o utilizzare un cluster HDInsight esistente in cui hello Hive tabelle dati NY Taxi toohello punto di archiviazione di Azure Data Lake.  Entrambe le opzioni sono illustrate di seguito. 

## <a name="option-1-use-python-toobuild-and-deploy-machine-learning-models"></a>Opzione 1: Usare Python toobuild e distribuire modelli di machine learning
toobuild e distribuire i modelli di machine learning Usa Python, creare un server Jupyter Notebook nel computer locale o in Azure Machine Learning Studio. Hello Server Jupyter Notebook fornito in [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) contiene hello tooexplore di codice completo, visualizzare i dati, progettazione di funzionalità, modellazione e distribuzione. In questo articolo viene illustrata solo modellazione hello e la distribuzione. 

### <a name="import-python-libraries"></a>Importare librerie Python
In hello toorun ordine esempio server Jupyter Notebook o file di script Python hello, hello pacchetti Python seguenti sono necessari. Se si utilizza il servizio di Azure ml Notebook hello, questi pacchetti sono stati preinstallati.

    import pandas as pd
    from pandas import Series, DataFrame
    import numpy as np
    import matplotlib.pyplot as plt
    from time import time
    import pyodbc
    import os
    from azure.storage.blob import BlobService
    import tables
    import time
    import zipfile
    import random
    import sklearn
    from sklearn.linear_model import LogisticRegression
    from sklearn.cross_validation import train_test_split
    from sklearn import metrics
    from __future__ import division
    from sklearn import linear_model
    from azureml import services


### <a name="read-in-hello-data-from-blob"></a>Leggere dati hello dal blob
* Connection String   
  
        CONTAINERNAME = 'test1'
        STORAGEACCOUNTNAME = 'XXXXXXXXX'
        STORAGEACCOUNTKEY = 'YYYYYYYYYYYYYYYYYYYYYYYYYYYY'
        BLOBNAME = 'demo_ex_9_stratified_1_1000_copy.csv'
        blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
* Leggere come testo
  
        t1 = time.time()
        data = blob_service.get_blob_to_text(CONTAINERNAME,BLOBNAME).split("\n")
        t2 = time.time()
        print(("It takes %s seconds tooread in "+BLOBNAME) % (t2 - t1))
  
  ![17](./media/machine-learning-data-science-process-data-lake-walkthrough/17-python_readin_csv.PNG)    
* Aggiungere i nomi di colonna e separare le colonne
  
        colnames = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime',
        'passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'payment_type', 'fare_amount', 'surcharge', 'mta_tax', 'tolls_amount',  'total_amount', 'tip_amount', 'tipped', 'tip_class', 'rownum']
        df1 = pd.DataFrame([sub.split(",") for sub in data], columns = colnames)
* Modificare toonumeric alcune colonne
  
        cols_2_float = ['trip_time_in_secs','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'fare_amount', 'surcharge','mta_tax','tolls_amount','total_amount','tip_amount', 'passenger_count','trip_distance'
        ,'tipped','tip_class','rownum']
        for col in cols_2_float:
            df1[col] = df1[col].astype(float)

### <a name="build-machine-learning-models"></a>Compilare modelli di Machine Learning
Abbiamo creato un toopredict modello di classificazione binaria se un trip è inclinato o non. Nel server Jupyter Notebook hello è possibile trovare altri due modelli: classificazione multiclasse e i modelli di regressione.

* È prima necessario variabili fittizio toocreate che possono essere usate in scikit-informazioni su modelli
  
        df1_payment_type_dummy = pd.get_dummies(df1['payment_type'], prefix='payment_type_dummy')
        df1_vendor_id_dummy = pd.get_dummies(df1['vendor_id'], prefix='vendor_id_dummy')
* Creare frame di dati per la modellazione hello
  
        cols_to_keep = ['tipped', 'trip_distance', 'passenger_count']
        data = df1[cols_to_keep].join([df1_payment_type_dummy,df1_vendor_id_dummy])
  
        X = data.iloc[:,1:]
        Y = data.tipped
* Training e test della suddivisione 60-40
  
        X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.4, random_state=0)
* Regressione logistica nel set di training
  
        model = LogisticRegression()
        logit_fit = model.fit(X_train, Y_train)
        print ('Coefficients: \n', logit_fit.coef_)
        Y_train_pred = logit_fit.predict(X_train)
  
       ![c1](./media/machine-learning-data-science-process-data-lake-walkthrough/c1-py-logit-coefficient.PNG)
* Assegnare un punteggio al set di dati di test
  
        Y_test_pred = logit_fit.predict(X_test)
* Calcolare le metriche di valutazione
  
        fpr_train, tpr_train, thresholds_train = metrics.roc_curve(Y_train, Y_train_pred)
        print fpr_train, tpr_train, thresholds_train
  
        fpr_test, tpr_test, thresholds_test = metrics.roc_curve(Y_test, Y_test_pred) 
        print fpr_test, tpr_test, thresholds_test
  
        #AUC
        print metrics.auc(fpr_train,tpr_train)
        print metrics.auc(fpr_test,tpr_test)
  
        #Confusion Matrix
        print metrics.confusion_matrix(Y_train,Y_train_pred)
        print metrics.confusion_matrix(Y_test,Y_test_pred)
  
       ![c2](./media/machine-learning-data-science-process-data-lake-walkthrough/c2-py-logit-evaluation.PNG)

### <a name="build-web-service-api-and-consume-it-in-python"></a>Compilare l'API del servizio Web e utilizzarla in Python
Vogliamo toooperationalize hello modello di machine learning dopo che è stata creata. Qui è usare modello logistica binario hello come esempio. Verificare che scikit hello-informazioni su versione nel computer locale è 0.15.1. Se si utilizza servizio di Azure ML studio, non è più necessario tooworry su questo argomento.

* Trovare le credenziali dell'area di lavoro dalle impostazioni di Azure Machine Learning Studio. In Azure Machine Learning Studio fare clic su **Impostazioni** --> **Nome** --> **Token di autorizzazione**. 
  
    ![c3](./media/machine-learning-data-science-process-data-lake-walkthrough/c3-workspace-id.PNG)

        workspaceid = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'
        auth_token = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'

* Creare un servizio Web
  
        @services.publish(workspaceid, auth_token) 
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float, payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(int) #0, or 1
        def predictNYCTAXI(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            inputArray = [trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH, payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS]
            return logit_fit.predict(inputArray)
* Ottenere le credenziali del servizio Web
  
        url = predictNYCTAXI.service.url
        api_key =  predictNYCTAXI.service.api_key
  
        print url
        print api_key
  
        @services.service(url, api_key)
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float,payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(float)
        def NYCTAXIPredictor(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            pass
* Chiamare un'API del servizio Web. È necessario toowait 5-10 secondi dopo il passaggio precedente hello.
  
        NYCTAXIPredictor(1,2,1,0,0,0,0,0,1)
  
       ![c4](./media/machine-learning-data-science-process-data-lake-walkthrough/c4-call-API.PNG)

## <a name="option-2-create-and-deploy-models-directly-in-azure-machine-learning"></a>Opzione 2: Creare e distribuire modelli direttamente in Azure Machine Learning
Azure Machine Learning Studio può leggere i dati direttamente dall'archivio Azure Data Lake e quindi essere toocreate utilizzato e distribuire modelli. Questo approccio utilizza una tabella Hive che punta al hello archivio Azure Data Lake. Questa operazione richiede che un cluster Azure HDInsight separato eseguirne il provisioning, in cui hello Hive viene creata nella tabella. Hello seguente mostra sezioni come toodo questo. 

### <a name="create-an-hdinsight-linux-cluster"></a>Creare un cluster HDInsight Linux
Creare un HDInsight Cluster (Linux) da hello [portale Azure](http://portal.azure.com). Per informazioni dettagliate, vedere hello **creare un cluster HDInsight con accesso tooAzure archivio Data Lake** sezione [creare un cluster HDInsight con archivio Data Lake tramite il portale di Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

 ![18](./media/machine-learning-data-science-process-data-lake-walkthrough/18-create_HDI_cluster.PNG)

### <a name="create-hive-table-in-hdinsight"></a>Creare una tabella Hive in HDInsight
È ora possibile creare toobe tabelle Hive usate in Azure Machine Learning Studio in cluster di HDInsight hello usando i dati di hello archiviati nell'archivio Azure Data Lake nel passaggio precedente hello. Passare toohello cluster HDInsight appena creato. Fare clic su **impostazioni** --> **proprietà** --> **Cluster identità AAD** --> **ADLS accesso**, Verificare che l'account archivio Azure Data Lake viene aggiunto nell'elenco di hello con lettura, scrittura e diritti di esecuzione. 

 ![19](./media/machine-learning-data-science-process-data-lake-walkthrough/19-HDI-cluster-add-ADLS.PNG)

Quindi fare clic su **Dashboard** toohello Avanti **impostazioni** pulsante e una finestra viene visualizzata. Fare clic su **visualizzazione Hive** hello angolo superiore destro della pagina hello e si visualizzeranno hello **Editor di Query**.

 ![20](./media/machine-learning-data-science-process-data-lake-walkthrough/20-HDI-dashboard.PNG)

 ![21](./media/machine-learning-data-science-process-data-lake-walkthrough/21-Hive-Query-Editor-v2.PNG)

Incolla in seguito hello Hive toocreate gli script di una tabella. Hello dell'origine dati si trova nella Guida di riferimento in questo modo archivio Azure Data Lake: **adl://data_lake_store_name.azuredatalakestore.net:443 nome_cartella/file_name**.

    CREATE EXTERNAL TABLE nyc_stratified_sample
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string,
      payment_type string,
      fare_amount string,
      surcharge string,
      mta_tax string,
      tolls_amount string,
      total_amount string,
      tip_amount string,
      tipped string,
      tip_class string,
      rownum string
      )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    LOCATION 'adl://data_lake_storage_name.azuredatalakestore.net:443/nyctaxi_folder/demo_ex_9_stratified_1_1000_copy.csv';


Al termine dell'esecuzione query hello, vengono visualizzati risultati hello simile al seguente:

 ![22](./media/machine-learning-data-science-process-data-lake-walkthrough/22-Hive-Query-results.PNG)

### <a name="build-and-deploy-models-in-azure-machine-learning-studio"></a>Compilare e distribuire modelli in Azure Machine Learning Studio
Ci sono ora pronti toobuild e distribuire un modello che stima o meno un suggerimento viene pagato con Azure Machine Learning. dati di esempio stratificato Hello sono pronto toobe utilizzati in questa classificazione binaria (suggerimento o non) problema. Hello modelli predittivi con classificazione multiclasse (tip_class) e regressione (tip_amount) può anche essere compilata e distribuita con Azure Machine Learning Studio, ma qui solo illustrare come toohandle hello maiuscole con hello modello di classificazione binaria.

1. Ottenere dati hello in Azure ML utilizzando hello **l'importazione dei dati** modulo, disponibile in hello **dati di Input e Output** sezione. Per ulteriori informazioni, vedere hello [modulo Importa dati](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) pagina di riferimento.
2. Selezionare **Query Hive** come hello **origine dati** in hello **proprietà** pannello.
3. Hello incollare lo script Hive in hello seguente **query database Hive** editor
   
        select * from nyc_stratified_sample;
4. Immettere il cluster di URI di HDInsight hello (questo è reperibile nel portale di Azure), le credenziali di Hadoop, posizione dei dati di output e il nome di contenitore/nome/chiave account di archiviazione di Azure.
   
   ![23](./media/machine-learning-data-science-process-data-lake-walkthrough/23-reader-module-v3.PNG)  

Un esempio di lettura dei dati dalla tabella Hive un esperimento di classificazione binaria è illustrato nella figura hello riportato di seguito.

 ![24](./media/machine-learning-data-science-process-data-lake-walkthrough/24-AML-exp.PNG)

Dopo aver creato l'esperimento hello, fare clic su **di servizio Web** --> **predittiva servizio Web**

 ![25](./media/machine-learning-data-science-process-data-lake-walkthrough/25-AML-exp-deploy.PNG)

Assegnazione dei punteggi esperimento, al termine, fare clic su esecuzione hello creato automaticamente **distribuzione servizio Web**

 ![26](./media/machine-learning-data-science-process-data-lake-walkthrough/26-AML-exp-deploy-web.PNG)

verrà visualizzato a breve dashboard del servizio web Hello:

 ![27](./media/machine-learning-data-science-process-data-lake-walkthrough/27-AML-web-api.PNG)

## <a name="summary"></a>Riepilogo
Seguendo questa procedura dettagliata è stato creato un ambiente di analisi scientifica dei dati per la creazione di soluzioni end-to-end scalabili in Azure Data Lake. Questo ambiente è stato utilizzato tooanalyze un ampio set di dati pubblici, portarlo passaggi canonico hello hello il processo di analisi scientifica dei dati, dall'acquisizione dati training del modello, e quindi distribuzione toohello di hello del modello come un servizio web. U-SQL è stato utilizzato tooprocess, esplorare e hello dati di esempio. Python e Hive venivano utilizzati con Azure Machine Learning Studio toobuild e distribuire modelli predittivi.

## <a name="whats-next"></a>Passaggi successivi
percorso di apprendimento Hello il [Team Data Science processo (TDSP)](http://aka.ms/datascienceprocess) fornisce collegamenti tootopics che descrivono ogni passaggio nel hello avanzate processo analitica. Esistono una serie di procedure dettagliate dettagliate su hello [procedure dettagliate di processo di analisi scientifica dei dati di Team](data-science-process-walkthroughs.md) pagina come tale showcase toouse risorse e i servizi in vari scenari analitica predittiva:

* [Processo di analisi scientifica dei dati del Team di Hello in azione: utilizzo di SQL Data Warehouse](machine-learning-data-science-process-sqldw-walkthrough.md)
* [Processo di analisi scientifica dei dati del Team di Hello in azione: utilizzo dei cluster HDInsight Hadoop](machine-learning-data-science-process-hive-walkthrough.md)
* [Processo di analisi scientifica dei dati di Team Hello: utilizzo di SQL Server](machine-learning-data-science-process-sql-walkthrough.md)
* [Panoramica dell'utilizzo di processo di analisi scientifica dei dati hello nascita in Azure HDInsight](machine-learning-data-science-spark-overview.md)

