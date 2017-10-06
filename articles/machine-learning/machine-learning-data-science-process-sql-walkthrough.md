---
title: aaaBuild e distribuire un modello di machine learning utilizza SQL Server in una macchina virtuale di Azure | Microsoft documenti
description: Advanced Analytics Process and Technology in azione
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6066b083-262c-4453-a712-a5c05acc3df8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: fashah;bradsev
ms.openlocfilehash: 30ba9a9e3cf65f75015e13f9c7876dcbccc5bc47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-server"></a>Processo di analisi scientifica dei dati del Team di Hello in azione: utilizzo di SQL Server
In questa esercitazione, si scoprirà processo hello della compilazione e distribuzione di un modello di machine learning utilizzando SQL Server e un set di dati disponibile pubblicamente, hello [NYC Taxi trip](http://www.andresmh.com/nyctaxitrips/) set di dati. procedura Hello segue un flusso di lavoro di analisi scientifica dei dati standard: inserimento esplorare i dati di hello, progettare learning toofacilitate funzionalità, quindi compilare e distribuire un modello.

## <a name="dataset"></a>Descrizione del set di dati relativo alle corse dei taxi di New York
dati di andata e ritorno Taxi NYC Hello è di circa 20GB di file CSV compressi (~ 48GB non compressi), che comprendono 173 milioni hello e singoli trip tariffe a pagamento per ogni itinerario. Ogni record di andata e ritorno include il percorso di ritiro e deposito hello e l'ora, hack anonimi (driver) il numero di licenza e numero medallion (id univoco del taxi). dati Hello copre tutti i percorsi nell'anno hello 2013 e viene forniti in hello dopo i due set di dati per ogni mese:

1. Hello 'trip_data' CSV contiene i dettagli di andata e ritorno, ad esempio il numero di passeggeri, prelievo e dropoff punti, la durata del viaggio e lunghezza di andata e ritorno. Di seguito vengono forniti alcuni record di esempio:
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. Hello 'trip_fare' CSV contiene i dettagli della tariffa di hello pagata per ogni itinerario, ad esempio il tipo di pagamento, quantità tariffa, supplemento e le imposte, suggerimenti e pedaggio e hello totale pagato. Di seguito vengono forniti alcuni record di esempio:
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

viaggi toojoin chiave univoca Hello\_dati e andata e ritorno\_tariffa è costituito da campi hello: medallion, le maggiori\_titolo e prelievo\_datetime.

## <a name="mltasks"></a>Esempi di attività di stima
Si verranno formulare tre problemi di stima in base a hello *suggerimento\_quantità*, vale a dire:

1. Classificazione binaria: consente di prevedere se sia stata lasciata una mancia per la corsa oppure no, vale a dire se un *tip\_amount* superiore a $ 0 rappresenta un esempio positivo, mentre un *tip\_amount* pari a $ 0 rappresenta un esempio negativo.
2. Classificazione multiclasse: intervallo di hello toopredict del suggerimento pagato viaggi hello. Verrà diviso hello *suggerimento\_quantità* in cinque contenitori o le classi:
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. Attività di regressione: quantità di hello toopredict del suggerimento a pagamento per un itinerario.  

## <a name="setup"></a>Impostazione hello Azure data science ambiente per analitica avanzate
Come si può vedere dal hello [pianificazione dell'ambiente](machine-learning-data-science-plan-your-environment.md) Guida, sono disponibili diverse opzioni toowork con set di dati NYC Taxi trip hello in Azure:

* Utilizzare i dati di hello in BLOB di Azure quindi modello in Azure Machine Learning
* Caricare i dati di hello in un database di SQL Server e il modello in Azure Machine Learning

In questa esercitazione verrà illustrato l'importazione bulk parallela di hello tooa di dati SQL Server, l'esplorazione dei dati, la funzionalità di progettazione verso il basso campionamento utilizzando SQL Server Management Studio nonché utilizzando IPython Notebook. Gli [script di esempio](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) e i [blocchi di appunti IPython](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) di esempio vengono condivisi in GitHub. Un toowork notebook IPython di esempio con i dati di hello in BLOB di Azure è disponibile anche in hello nello stesso percorso.

tooset dell'ambiente di analisi scientifica dei dati di Azure:

1. [Creare un account di archiviazione](../storage/common/storage-create-storage-account.md)
2. [Creare un'area di lavoro di Machine Learning di Azure](machine-learning-create-workspace.md)
3. [Eseguire il provisioning di una macchina virtuale Data Science](machine-learning-data-science-setup-sql-server-virtual-machine.md), che fornirà SQL Server e un server IPython Notebook.
   
   > [!NOTE]
   > script di esempio Hello e IPython notebook saranno macchina virtuale di analisi scientifica dei dati scaricati tooyour durante il processo di installazione di hello. Al termine del processo di script di post-installazione VM hello, esempi di hello sarà nella raccolta documenti di VM:  
   > 
   > * Script di esempio: `C:\Users\<user_name>\Documents\Data Science Scripts`  
   > * Blocchi di appunti di esempio IPython: `C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`  
   >   where `<user_name>` è il nome di accesso Windows della VM. Si farà riferimento a cartelle di esempio toohello come **gli script di esempio** e **esempio IPython notebook**.
   > 
   > 

Basato su dimensioni del set di dati hello, percorso di origine dati e ambiente di destinazione selezionati di Azure hello, questo scenario è simile troppo[Scenario \#5: grandi set di dati in un file locale, SQL Server nella macchina virtuale di Azure di destinazione](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).

## <a name="getdata"></a>Ottenere hello dati dall'origine pubblico
hello tooget [NYC Taxi trip](http://www.andresmh.com/nyctaxitrips/) set di dati dal percorso pubblico, è possibile utilizzare uno dei metodi di hello descritto in [tooand spostare dati dall'archiviazione Blob di Azure](machine-learning-data-science-move-azure-blob.md) toocopy hello tooyour dati nuova macchina virtuale.

dati hello toocopy utilizzando AzCopy:

1. Log nella macchina virtuale tooyour (VM)
2. Creare una nuova directory nel disco di dati della macchina virtuale di hello (Nota: non utilizzare hello disco temporaneo che viene fornito con hello macchina virtuale come disco dati).
3. In una finestra del prompt dei comandi, eseguire hello Azcopy della riga di comando seguente, sostituendo < path_to_data_folder > con la cartella di dati creata in (2):
   
        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S
   
    Al termine, hello AzCopy un totale di 24 compresso file CSV (12 per viaggi\_dati e 12 per viaggi\_tariffa) devono trovarsi nella cartella dati hello.
4. Decomprimere i file scaricato hello. Prendere nota hello cartella in cui risiedono i file non compresso hello. Questa cartella verrà tooas cui hello < percorso\_a\_dati\_file\>.

## <a name="dbload"></a>Importazione in blocco dei dati nel database SQL Server
Hello delle prestazioni di caricamento/trasferire grandi quantità di database SQL tooan di dati e le query successive possono essere migliorate tramite *viste e tabelle partizionate*. In questa sezione verrà seguito hello istruzioni di [parallela Bulk dei dati utilizzando SQL partizione tabelle di importazione](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) toocreate un nuovo database e caricare hello i dati in tabelle partizionate in parallelo.

1. Mentre si è connessi tooyour macchina virtuale, avviare **SQL Server Management Studio**.
2. Effettuare la connessione mediante Autenticazione di Windows.
   
    ![Connessione a SSMS][12]
3. Se non ancora aver modificato la modalità autenticazione di SQL Server hello e creato un nuovo utente di accesso SQL, aprire il file di script hello denominato **modificare\_auth.sql** in hello **gli script di esempio** cartella. Modificare nome hello predefinito dell'utente e password. Fare clic su **! Eseguire** nello script hello toorun di hello barra degli strumenti.
   
    ![Esecuzione dello script][13]
4. Verificare e/o modificare hello predefinito del database e log cartelle tooensure che nuovi database verrà archiviati in un disco dati di SQL Server. immagine di macchina virtuale SQL Server Hello ottimizzata per caricamenti DataWarehouse è preconfigurata con dischi dati e di log. Se la macchina virtuale non include un disco dati e nuovi dischi rigidi virtuali non sono aggiunti durante il processo di installazione VM hello, modificare le cartelle predefinite hello come segue:
   
   * Nome di SQL Server hello pulsante destro del mouse nel pannello e fare clic a sinistra hello **proprietà**.
     
       ![Proprietà di SQL Server][14]
   * Selezionare **le impostazioni del Database** da hello **selezione pagina** elenco toohello sinistra.
   * Verificare e/o modificare hello **percorsi predefiniti Database** toohello **disco dati** percorsi di propria scelta. In cui si trova nuovi database se creato con le impostazioni percorso di hello predefinite.
     
       ![Impostazioni predefinite del database SQL][15]  
5. toocreate un nuovo database e un set di filegroup toohold hello tabelle partizionate, aprire uno script di esempio hello **creare\_db\_default.sql**. Hello script crea un nuovo database denominato **TaxiNYC** e 12 filegroup nel percorso dati predefinito di hello. In ogni gruppo sarà presente un mese di dati trip\_data e trip\_fare. Modificare il nome del database hello, se opportuno. Fare clic su **! Eseguire** script hello toorun.
6. Successivamente, creare due tabelle delle partizioni, uno per viaggi hello\_dati e un altro per viaggi hello\_fare. Aprire uno script di esempio hello **creare\_partizionata\_Table**, che sarà:
   
   * Creare un partizione funzione toosplit hello dati in base al mese.
   * Creare un toomap lo schema di partizione di filegroup diverso tooa dati di ogni mese.
   * Creare due schema di partizione di tabelle partizionate toohello mappato: **nyctaxi\_viaggi** conterrà viaggi hello\_dati e **nyctaxi\_tariffa** conterrà viaggi hello \_presentare i dati.
     
     Fare clic su **! Eseguire** toorun hello script e creare le tabelle partizionata hello.
7. In hello **gli script di esempio** cartella, sono disponibili due script di PowerShell di esempio forniti toodemonstrate importazioni bulk parallela tooSQL Server di tabelle di dati.
   
   * **bcp\_parallela\_generic.ps1** è una script generico tooparallel importazione bulk dei dati in una tabella. Modificare questo script tooset hello input e destinazione le variabili come indicato nelle righe di commento hello nello script hello.
   * **bcp\_parallela\_nyctaxi.ps1** è una versione preconfigurata di script generico hello e può essere utilizzato tootooload entrambe le tabelle per i dati NYC Taxi trip hello.  
8. Pulsante destro del mouse hello **bcp\_parallela\_nyctaxi.ps1** nome dello script e fare clic su **modifica** tooopen in PowerShell. Hello revisione preimpostato variabili e modificare secondo nome del database selezionato tooyour, cartella di dati di input, cartella di destinazione del log e file di formato di esempio toohello percorsi **nyctaxi_trip.xml** e **nyctaxi\_ Fare.XML** (disponibile in hello **gli script di esempio** cartella).
   
    ![Importazione in blocco dei dati][16]
   
    È inoltre possibile selezionare la modalità di autenticazione hello, impostazione predefinita è autenticazione di Windows. Fare clic sulla freccia verde hello toorun barra degli strumenti hello. script Hello avvierà 24 operazioni di importazione bulk in parallelo, 12 per ogni tabella partizionata. Si può monitorare lo stato di importazione dati di hello aprendo una cartella dati predefinita di SQL Server hello come set precedente.
9. i report di script di PowerShell Hello hello iniziale e finale di volte. Quando tutti completo importazioni in blocco, viene segnalato hello ora di fine. Controllare hello destinazione log cartella tooverify importazioni bulk hello hanno avuto esito positivo, ad esempio, non segnalati errori nella cartella log della destinazione hello.
10. Il database ora è pronto per l'esplorazione, la progettazione di funzionalità e altre operazioni che si desidera eseguire. Poiché le tabelle di hello vengono partizionate in base toohello **prelievo\_datetime** campo, le query che includono **prelievo\_datetime** condizioni hello  **DOVE** clausola trarranno vantaggio rispetto allo schema di partizione hello.
11. In **SQL Server Management Studio**, esplorare uno script di esempio fornito hello **esempio\_queries.sql**. toorun delle query di esempio hello, evidenziazione hello righe di query, quindi fare clic su **! Eseguire** nella barra degli strumenti hello.
12. Hello dati NYC Taxi trip viene caricato in due tabelle separate. operazioni di join tooimprove, è consigliabile tabelle hello tooindex. script di esempio Hello **creare\_partizionata\_index.sql** crea indici partizionati nella chiave di join composti hello **medallion, le maggiori\_licenza e prelievo\_datetime**.

## <a name="dbexplore"></a>Esplorazione dei dati e progettazione di funzionalità in SQL Server
In questa sezione, si eseguirà la generazione di funzionalità e l'esplorazione dei dati mediante l'esecuzione di query SQL direttamente in hello **SQL Server Management Studio** utilizzando il database di SQL Server hello creato in precedenza. Uno script di esempio denominato **esempio\_queries.sql** è disponibile in hello **gli script di esempio** cartella. Modificare nome del database hello toochange script hello, se è diverso da predefinito hello: **TaxiNYC**.

In questo esercizio, verranno effettuate le seguenti operazioni:

* Connettersi troppo**SQL Server Management Studio** usando l'autenticazione di Windows o utilizzando l'autenticazione di SQL e hello Nome accesso SQL e una password.
* Esplorazione delle distribuzioni di dati di un numero ridotto di campi in diverse finestre temporali.
* Analizzare la qualità dei dati dei campi di longitudine e latitudine hello.
* Generare etichette di classificazione multiclasse e binaria dipende hello **suggerimento\_quantità**.
* Generazione di funzionalità calcolo/confronto delle distanze delle corse.
* Join di tabelle hello due ed estrarre un campione casuale che verrà utilizzato toobuild modelli.

Quando si è pronti tooproceed tooAzure Machine Learning, è possibile:  

1. Salvare hello finale SQL query tooextract ed esempio hello dati e copia e Incolla hello query direttamente in un [l'importazione dei dati] [ import-data] modulo in Azure Machine Learning, o
2. Mantenere hello campionato e dati decodificati Prevedi toouse per la creazione di un nuovo database modello di tabella e utilizzano nuova tabella hello in hello [l'importazione dei dati] [ import-data] modulo in Azure Machine Learning.

In questa sezione si salverà hello query finale tooextract hello dati di esempio e. secondo metodo Hello viene dimostrata in hello [l'esplorazione dei dati e funzionalità di progettazione in IPython Notebook](#ipnb) sezione.

Per una rapida verifica del numero di hello di righe e colonne in hello tabelle popolate in precedenza mediante l'importazione bulk parallela,

    -- Report number of rows in table nyctaxi_trip without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('nyctaxi_trip')

    -- Report number of columns in table nyctaxi_trip
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = 'nyctaxi_trip'

#### <a name="exploration-trip-distribution-by-medallion"></a>Esplorazione: distribuzione delle corse per licenza
In questo esempio identifica medallion hello (numeri taxi) con più di 100 trip all'interno di un determinato periodo di tempo. query Hello può costituire un vantaggio accesso alle tabelle partizionata hello poiché condizionato, dallo schema di partizione hello di **prelievo\_datetime**. Una query di set di dati completo hello renderà inoltre usare della tabella partizionata hello e/o l'analisi di indice.

    SELECT medallion, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

#### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a>Esplorazione: distribuzione delle corse per licenza e hack_license
    SELECT medallion, hack_license, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

#### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a>Valutazione della qualità dei dati: verifica dei record con longitudine o latitudine errate
In questo esempio consente di esaminare se i campi di longitudine e/o latitudine hello contenere un valore non valido (gradi in radianti devono essere compreso tra -90 e 90,) o (0, 0) le coordinate.

    SELECT COUNT(*) FROM nyctaxi_trip
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

#### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a>Esplorazione: distribuzione delle corse per le quali è stata lasciata una mancia e di quelle per le quali non è stata lasciata una mancia
In questo esempio trova il numero di hello di viaggi che sono stati inclinato e inclinato non in un determinato momento periodo (o in hello set di dati completo se per l'anno di hello completo). Questa distribuzione riflette hello binario etichetta distribuzione toobe utilizzato successivamente per la modellazione di classificazione binaria.

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM nyctaxi_fare
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

#### <a name="exploration-tip-classrange-distribution"></a>Esplorazione: distribuzione della classe o dell'intervallo delle mance
Questo esempio calcola la distribuzione di hello degli intervalli di comandi in un determinato momento periodo (o in hello set di dati completo se per l'anno di hello completo). Si tratta di distribuzione hello di classi di etichetta hello che verrà usato successivamente per la modellazione di classificazione multiclasse.

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

#### <a name="exploration-compute-and-compare-trip-distance"></a>Esplorazione: calcolo e confronto della distanza delle corse
In questo esempio converte la longitudine di ritiro e deposito hello e geography tooSQL latitudine punta, distanza di andata e ritorno hello utilizzando SQL geography punti differenza calcola e restituisce un campione casuale di risultati hello per il confronto. esempio Hello limita i risultati di hello toovalid coordinate solo tramite query valutazione della qualità dei dati hello descritti in precedenza.

    SELECT
    pickup_location=geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326)
    ,dropoff_location=geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326)
    ,trip_distance
    ,computedist=round(geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326).STDistance(geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326))/1000, 2)
    FROM nyctaxi_trip
    tablesample(0.01 percent)
    WHERE CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND   CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

#### <a name="feature-engineering-in-sql-queries"></a>Progettazione di funzionalità nelle query SQL
Hello etichetta generazione geography conversione esplorazione le query e possono essere anche usato toogenerate etichette o le funzionalità rimuovendo hello conteggio parte. Vengono forniti esempi SQL engineering di funzionalità aggiuntive in hello [l'esplorazione dei dati e funzionalità di progettazione in IPython Notebook](#ipnb) sezione. È più efficiente toorun hello funzionalità generazione query sul set di dati completo hello o un sottoinsieme di grandi dimensioni usando le query SQL eseguito direttamente sull'istanza di database di SQL Server hello. le query Hello possono essere eseguite **SQL Server Management Studio**, IPython Notebook o qualsiasi strumento/ambiente di sviluppo che può accedere a hello database locale o remota.

#### <a name="preparing-data-for-model-building"></a>Preparazione dei dati per la creazione di modelli
hello join di query seguente di Hello **nyctaxi\_viaggi** e **nyctaxi\_tariffa** tabelle, genera un'etichetta di classificazione binaria **inclinato**, etichetta di classificazione multiclasse **suggerimento\_classe**ed estrae un campione casuale di % 1 da hello aggiunti a un set di dati completo. Questa query può essere copiata successivamente incollata direttamente in hello [Azure Machine Learning Studio](https://studio.azureml.net) [l'importazione dei dati] [ import-data] modulo per l'inserimento di dati direttamente dal database di SQL Server hello istanza di Azure. query Hello esclude i record con errato (0, 0) le coordinate.

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_trip t, nyctaxi_fare f
    TABLESAMPLE (1 percent)
    WHERE t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'


## <a name="ipnb"></a>Esplorazione dei dati e progettazione di funzionalità in IPython Notebook
In questa sezione, si eseguirà l'esplorazione dei dati e la generazione di funzionalità mediante sia Python e query SQL sul database di SQL Server hello creato in precedenza. IPython notebook esempio denominato **machine-Learning-data-science-process-sql-story.ipynb** è disponibile in hello **esempio IPython notebook** cartella. Tale blocco di appunti è disponibile anche in [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).

Hello sequenza consigliata quando si utilizzano dati di grandi dimensioni può essere seguito hello:

* Lettura in un piccolo esempio dei dati hello in un frame di dati in memoria.
* Eseguire alcune visualizzazioni e delle esplorazioni utilizzando hello dati campionati.
* Provare varie combinazioni di progettazione di funzionalità mediante hello dati campionati.
* Per l'esplorazione dei dati più grande, la manipolazione dei dati e progettazione di funzionalità, utilizzare query di SQL Python tooissue direttamente nel database di SQL Server hello hello macchina virtuale di Azure.
* Decidere toouse dimensioni di esempio hello per la compilazione del modello di Azure Machine Learning.

Al termine tooproceed tooAzure Machine Learning, può:  

1. Salvare hello finale SQL query tooextract ed esempio hello dati e copia e Incolla hello query direttamente in un [l'importazione dei dati] [ import-data] modulo in Azure Machine Learning. Questo metodo è illustrato in hello [compilazione dei modelli in Azure Machine Learning](#mlmodel) sezione.    
2. Mantenere hello campionati e i dati decodificati Prevedi toouse per la creazione di una nuova tabella di database modello, quindi utilizzare nuova tabella hello in hello [l'importazione dei dati] [ import-data] modulo.

di seguito Hello sono pochi l'esplorazione dei dati, la visualizzazione dei dati e funzionalità di esempi di progettazione. Per ulteriori esempi, vedere hello esempio SQL IPython notebook hello **esempio IPython notebook** cartella.

#### <a name="initialize-database-credentials"></a>Inizializzazione delle credenziali di database
Inizializzare le impostazioni di connessione di database in hello seguenti variabili:

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database server>

#### <a name="create-database-connection"></a>Creazione della connessione di database
    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

#### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a>Segnalazione del numero di righe e di colonne nella tabella nyctaxi_trip
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('nyctaxi_trip')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('nyctaxi_trip')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* Numero di righe totali = 173179759  
* Numero di colonne totali = 14

#### <a name="read-in-a-small-data-sample-from-hello-sql-server-database"></a>Lettura in un campione di dati di dimensioni ridotte da hello Database di SQL Server
    t0 = time.time()

    query = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (0.05 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

Tabella di esempio hello tooread ora è 6.492000 secondi  
Numero di righe e di colonne recuperate = (8.4952, 21)

#### <a name="descriptive-statistics"></a>Statistiche descrittive
Sono ora dati campionato hello tooexplore pronto. Iniziamo con esaminando le statistiche descrittive per hello **viaggi\_distanza** (o qualsiasi altro) campi:

    df1['trip_distance'].describe()

#### <a name="visualization-box-plot-example"></a>Visualizzazione: esempio di box plot
Successivamente si esamina il grafico box plot di hello per hello viaggi distanza toovisualize hello quantili

    df1.boxplot(column='trip_distance',return_type='dict')

![Grafico n. 1][1]

#### <a name="visualization-distribution-plot-example"></a>Visualizzazione: esempio di tracciato di distribuzione
    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Grafico n. 2][2]

#### <a name="visualization-bar-and-line-plots"></a>Visualizzazione: tracciati a barre e linee
In questo esempio è bin distanza di andata e ritorno hello in cinque bin e visualizzare i risultati di binning hello.

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

È possibile tracciare hello sopra distribuzione bin in una barra o riga del tracciato come indicato di seguito

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Grafico n. 3][3]

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Grafico n. 4][4]

#### <a name="visualization-scatterplot-example"></a>Visualizzazione: esempio di grafico a dispersione
Viene illustrata la dispersione tra **viaggi\_ora\_in\_sec** e **viaggi\_distanza** toosee nel caso di qualsiasi correlazione

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![Grafico n. 6][6]

Analogamente è possibile controllare la relazione hello tra **frequenza\_codice** e **viaggi\_distanza**.

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![Grafico n. 8][8]

### <a name="sub-sampling-hello-data-in-sql"></a>Hello sub-campionamento dei dati in SQL
Durante la preparazione dei dati per il modello di compilazione in [Azure Machine Learning Studio](https://studio.azureml.net), è possibile decidere di su hello **toouse query SQL direttamente nel modulo di importazione dei dati hello** o permanenti hello progettata e campionati dati in una nuova tabella, è possibile utilizzare in hello [l'importazione dei dati] [ import-data] modulo con un semplice **selezionare * FROM < il\_nuova\_tabella\_nome >**.

In questa sezione che si creerà un nuovo hello toohold tabella campionata e decodificati dati. Viene fornito un esempio di una query SQL diretta per la compilazione del modello in hello [l'esplorazione dei dati e funzionalità di progettazione in SQL Server](#dbexplore) sezione.

#### <a name="create-a-sample-table-and-populate-with-1-of-hello-joined-tables-drop-table-first-if-it-exists"></a>Creare una tabella di esempio e la popola con % 1 di hello unita in join tabelle. Innanzitutto eliminare la tabella, se presente.
In questa sezione è join di tabelle di hello **nyctaxi\_viaggi** e **nyctaxi\_tariffa**, estrarre un campione casuale di % 1 e rendere persistenti i dati campionato hello in un nuovo nome di tabella  **nyctaxi\_uno\_%**:

    cursor = conn.cursor()

    drop_table_if_exists = '''
        IF OBJECT_ID('nyctaxi_one_percent', 'U') IS NOT NULL DROP TABLE nyctaxi_one_percent
    '''

    nyctaxi_one_percent_insert = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount
        INTO nyctaxi_one_percent
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (1 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
        AND   pickup_longitude <> '0' AND dropoff_longitude <> '0'
    '''

    cursor.execute(drop_table_if_exists)
    cursor.execute(nyctaxi_one_percent_insert)
    cursor.commit()

### <a name="data-exploration-using-sql-queries-in-ipython-notebook"></a>Esplorazione dei dati mediante query SQL in IPython Notebook
In questa sezione vengono analizzate le distribuzioni dei dati utilizzando i dati di % 1 campionate hello che viene mantenuti nella nuova tabella hello creato in precedenza. Si noti che esplorazioni simile possono essere eseguite mediante tabelle originali di hello, utilizzando facoltativamente **TABLESAMPLE** tooa dato periodo di tempo utilizzando hello risultati dell'esplorazione di hello toolimit sample o limitando hello **prelievo \_datetime** partizioni, come illustrato nell'hello [l'esplorazione dei dati e funzionalità di progettazione in SQL Server](#dbexplore) sezione.

#### <a name="exploration-daily-distribution-of-trips"></a>Esplorazione: distribuzione giornaliera delle corse
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a>Esplorazione: distribuzione delle corse per licenza
    query = '''
        SELECT medallion,count(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

### <a name="feature-generation-using-sql-queries-in-ipython-notebook"></a>Generazione di funzionalità mediante query SQL in IPython Notebook
In questa sezione verranno generati nuove etichette e funzionalità direttamente tramite query SQL, operano su tabella di esempio di % 1 hello è creato nella sezione precedente di hello.

#### <a name="label-generation-generate-class-labels"></a>Generazione di etichette: generazione di etichette di classe
Nell'esempio seguente di hello, si genera due set di etichette toouse per la modellazione:

1. Etichette di classe binaria **tipped** (che forniscono una stima sull'elargizione di una mancia)
2. Etichette multiclasse **suggerimento\_classe** (stima bin suggerimento hello o intervallo)
   
        nyctaxi_one_percent_add_col = '''
            ALTER TABLE nyctaxi_one_percent ADD tipped bit, tip_class int
        '''
   
        cursor.execute(nyctaxi_one_percent_add_col)
        cursor.commit()
   
        nyctaxi_one_percent_update_col = '''
            UPDATE nyctaxi_one_percent
            SET
               tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
               tip_class = CASE WHEN (tip_amount = 0) THEN 0
                                WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                                WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                                WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                                ELSE 4
                            END
        '''
   
        cursor.execute(nyctaxi_one_percent_update_col)
        cursor.commit()

#### <a name="feature-engineering-count-features-for-categorical-columns"></a>Progettazione di funzionalità: funzionalità di conteggio per le colonne relative alle categorie
In questo esempio trasforma un campo categorico in un campo numerico sostituendo ogni categoria con conteggio hello dei casi nei dati hello.

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD cmt_count int, vts_count int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B AS
        (
            SELECT medallion, hack_license,
                SUM(CASE WHEN vendor_id = 'cmt' THEN 1 ELSE 0 END) AS cmt_count,
                SUM(CASE WHEN vendor_id = 'vts' THEN 1 ELSE 0 END) AS vts_count
            FROM nyctaxi_one_percent
            GROUP BY medallion, hack_license
        )

        UPDATE nyctaxi_one_percent
        SET nyctaxi_one_percent.cmt_count = B.cmt_count,
            nyctaxi_one_percent.vts_count = B.vts_count
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion AND A.hack_license = B.hack_license
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-bin-features-for-numerical-columns"></a>Progettazione di funzionalità: funzionalità di collocazione per le colonne numeriche
In questo esempio, un campo numerico continuo viene trasformato in intervalli di categorie predefiniti, vale a dire che il campo numerico verrà trasformato in un campo di categoria.

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD trip_time_bin int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B(medallion,hack_license,pickup_datetime,trip_time_in_secs, BinNumber ) AS
        (
            SELECT medallion,hack_license,pickup_datetime,trip_time_in_secs,
            NTILE(5) OVER (ORDER BY trip_time_in_secs) AS BinNumber from nyctaxi_one_percent
        )

        UPDATE nyctaxi_one_percent
        SET trip_time_bin = B.BinNumber
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion
        AND A.hack_license = B.hack_license
        AND A.pickup_datetime = B.pickup_datetime
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-extract-location-features-from-decimal-latitudelongitude"></a>Progettazione di funzionalità: funzionalità di estrazione della posizione dalla longitudine/latitudine decimale
In questo esempio suddivide rappresentazione decimale di hello di un campo di latitudine e/o longitudine in più campi area livelli di granularità diversi, ad esempio, paese, città, città, blocco e così via. Si noti che il nuovo hello geo-i campi non sono mappati a percorsi tooactual. Per informazioni sul mapping delle località con codice geografico, vedere [Servizi REST di Bing Mappe](https://msdn.microsoft.com/library/ff701710.aspx).

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent
        ADD l1 varchar(6), l2 varchar(3), l3 varchar(3), l4 varchar(3),
            l5 varchar(3), l6 varchar(3), l7 varchar(3)
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        UPDATE nyctaxi_one_percent
        SET l1=round(pickup_longitude,0)
            , l2 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 1 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),1,1) ELSE '0' END     
            , l3 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 2 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),2,1) ELSE '0' END     
            , l4 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 3 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),3,1) ELSE '0' END     
            , l5 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 4 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),4,1) ELSE '0' END     
            , l6 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 5 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),5,1) ELSE '0' END     
            , l7 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 6 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),6,1) ELSE '0' END
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a>Verificare il modulo di finale hello della tabella trasformato hello
    query = '''SELECT TOP 100 * FROM nyctaxi_one_percent'''
    pd.read_sql(query,conn)

Sono ora pronti tooproceed toomodel compilazione e distribuzione di modelli in [Azure Machine Learning](https://studio.azureml.net). dati Hello sono pronti per uno qualsiasi dei problemi di stima hello identificati in precedenza, vale a dire:

1. Classificazione binaria: toopredict o meno un suggerimento è stato pagato per un itinerario.
2. Classificazione multiclasse: intervallo di hello toopredict del suggerimento a pagamento, in base a toohello classi definite in precedenza.
3. Attività di regressione: quantità di hello toopredict del suggerimento a pagamento per un itinerario.  

## <a name="mlmodel"></a>Compilazione di modelli in Azure Machine Learning
toobegin hello modellazione esercizio log nell'area di lavoro tooyour Azure Machine Learning. Se non è ancora disponibile un'area di lavoro di machine learning, vedere [Creare un'area di lavoro Azure Machine Learning](machine-learning-create-workspace.md).

1. tooget avviato con Azure Machine Learning, vedere [che cos'è Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)
2. Accedi troppo[Azure Machine Learning Studio](https://studio.azureml.net).
3. pagina iniziale di Studio Hello un'ampia gamma di informazioni, video, esercitazioni, collegamenti toohello riferimento moduli e altre risorse. Per ulteriori informazioni su Azure Machine Learning, consultare hello [Centro documentazione di Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/).

Un esperimento di training tipica è costituita da hello segue:

1. Creazione di un esperimento **+NEW** .
2. Ottenere dati di hello tooAzure Machine Learning.
3. Pre-elaborazione, trasformare e modificare i dati di hello in base alle esigenze.
4. Generazione di funzionalità, se necessario.
5. Suddividere i dati di hello in set di dati di training e la convalida o il test (o set di dati separati per ogni).
6. Selezionare uno o più algoritmi di machine learning a seconda di hello toosolve problema di apprendimento. Ad esempio, classificazione binaria, classificazione multiclasse, regressione.
7. Eseguire il training di uno o più modelli utilizzando hello training set.
8. Assegnare un punteggio hello convalida set di dati utilizzando modelli con training hello.
9. Valutare hello modelli toocompute hello le metriche pertinenti per l'apprendimento problema hello.
10. Ottimizzare i modelli di hello e selezionare hello migliore modello toodeploy.

In questo esercizio, abbiamo già esplorato e decodificati dati hello in SQL Server e deciso tooingest dimensioni di esempio hello in Azure Machine Learning. toobuild uno o più modelli di stima hello che si è deciso di:

1. Ottenere dati di hello tooAzure Machine Learning usando hello [l'importazione dei dati] [ import-data] modulo, disponibile in hello **dati di Input e Output** sezione. Per ulteriori informazioni, vedere hello [l'importazione dei dati] [ import-data] pagina di riferimento modulo.
   
    ![Dati di importazione di Azure Machine Learning][17]
2. Selezionare **Database SQL di Azure** come hello **origine dati** in hello **proprietà** pannello.
3. Immettere nome DNS del database hello in hello **nome server Database** campo. Formato: `tcp:<your_virtual_machine_DNS_name>,1433`
4. Immettere hello **nome del Database** nel campo corrispondente hello.
5. Immettere hello **nome utente di SQL** in hello * * aqccount nome utente e password hello in hello **password dell'account utente Server**.
6. Selezione dell'opzione **Accetta qualsiasi certificato server** .
7. In hello **query Database** Modifica area di testo, incollare query hello estrae hello necessario campi (incluse eventuali campi calcolati, ad esempio etichette hello) del database e verso il basso esempi di dimensioni del campione hello dati toohello desiderato.

Un esempio di lettura dei dati direttamente dal database di SQL Server hello un esperimento di classificazione binaria è in figura hello riportata di seguito. È possibile creare esperimenti dello stesso tipo per i problemi di classificazione multiclasse e di regressione.

![Formazione di Azure Machine Learning][10]

> [!IMPORTANT]
> In hello modellazione estrazione dei dati e il campionamento di esempi di query forniti nelle sezioni precedenti, **tutte le etichette per gli esercizi di modellazione hello tre sono inclusi nella query hello**. Un passaggio importante (obbligatorio) in ogni hello esercizi sulla modellazione è troppo**escludere** hello etichette non necessari per hello altri due problemi e qualsiasi altro **destinazione perdite**. Per ad esempio, quando si utilizza una classificazione binaria, utilizzare hello etichetta **inclinato** ed escludere i campi di hello **suggerimento\_classe**, **suggerimento\_quantità**, e **totale\_quantità**. Hello quest'ultimo vengono pagate perdite di destinazione, perché implicano suggerimento hello.
> 
> colonne non necessarie tooexclude e/o perdite di destinazione, è possibile utilizzare hello [selezionare le colonne nel set di dati] [ select-columns] modulo o hello [Modifica metadati] [ edit-metadata]. Per altre informazioni, vedere le pagine di riferimento per [Select Columns in Dataset][select-columns] (Seleziona colonne in set di dati) ed [Edit Metadata][edit-metadata] (Modifica metadati).
> 
> 

## <a name="mldeploy"></a>Distribuzione di modelli in Azure Machine Learning
Quando il modello è pronto, è possibile distribuirlo facilmente come servizio web direttamente da esperimento hello. Per ulteriori informazioni sulla distribuzione di servizi Web Azure Machine Learning, vedere [Distribuzione di un servizio Web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

toodeploy un nuovo servizio web, è necessario:

1. Creare un esperimento di assegnazione di punteggio.
2. Distribuire il servizio web hello.

un punteggio sperimentare da toocreate un **completato** esperimento di training, fare clic su **CREATE SCORING EXPERIMENT** nella barra delle azioni inferiore hello.

![Valutazione di Azure][18]

Azure Machine Learning tenterà toocreate un esperimento di assegnazione dei punteggi in base ai componenti di hello dell'esperimento di training hello. In particolare, verranno effettuate le seguenti operazioni:

1. Salva modello con training hello e rimuovere i moduli di training modello di hello.
2. Identificare una logica **porta di input** toorepresent hello previsto schema dati di input.
3. Identificare una logica **porta di output** toorepresent dello schema output di hello web previsto del servizio.

Quando viene creato l'assegnazione dei punteggi esperimento hello, esaminarla e modificare in base alle esigenze. Un esempio tipico di regolazione sia set di dati tooreplace hello input e/o query con uno che esclude i campi di etichetta, poiché questi non saranno disponibili quando viene chiamato servizio hello. È anche una dimensione di hello tooreduce buona norma di hello alcuni record, dello schema di input sufficiente hello tooindicate tooa set di dati e/o query di input. Per la porta di output di hello, è comune tooexclude campi di tutti gli input e includere solo hello **Scored Labels** e **calcolato il punteggio della probabilità** in hello output utilizzando hello [selezionare le colonne nel set di dati ] [ select-columns] modulo.

Un punteggio esperimento di esempio è in figura hello riportata di seguito. Al termine toodeploy, fare clic su hello **servizio WEB di pubblicare** pulsante nella barra delle azioni inferiore hello.

![Pubblicazione di Azure Machine Learning][11]

toorecap, in questa esercitazione, questa procedura dettagliata è stato creato un ambiente di analisi scientifica dei dati di Azure, ha collaborato con un dataset pubblici di grandi dimensioni tutte modo hello da toomodel di acquisizione di dati di training e la distribuzione di un servizio web Azure Machine Learning.

### <a name="license-information"></a>Informazioni sulla licenza
In questa procedura dettagliata di esempio e il relativo tipo di accompagnamento notebook(s) IPython e script sono condivisi da Microsoft con licenza MIT hello. Nella directory di hello del codice di esempio hello su GitHub per ulteriori dettagli, controllare file License hello in.

### <a name="references"></a>Riferimenti
•    [Pagina di Andrés Monroy per scaricare i dati sulle corse dei taxi di NYC](http://www.andresmh.com/nyctaxitrips/)  
•    [Complemento dai dati sulle corse dei taxi di NYC di Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/)   
•    [Ricerche e statistiche su NYC Taxi and Limousine Commission](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)

[1]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sql-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sql-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sql-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sql-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sql-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sql-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sql-walkthrough/amlscoring.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
