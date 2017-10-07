---
title: 'Processo di analisi scientifica dei dati del Team di Hello in azione: utilizzo di SQL Data Warehouse | Documenti Microsoft'
description: Advanced Analytics Process and Technology in azione
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 88ba8e28-0bd7-49fe-8320-5dfa83b65724
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;hangzh;weig
ms.openlocfilehash: b1b6371583a023d32e33db59464cafd8c3b767d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-data-warehouse"></a>Processo di analisi scientifica dei dati del Team di Hello in azione: utilizzo di SQL Data Warehouse
In questa esercitazione si illustrano la compilazione e distribuzione di un modello di machine learning usando SQL Data Warehouse (SQL Data Warehouse) per un set di dati disponibile pubblicamente, hello [NYC Taxi trip](http://www.andresmh.com/nyctaxitrips/) set di dati. modello di classificazione binaria Hello costruito stima o meno un suggerimento viene pagato per un di andata e ritorno e modelli per la classificazione multiclasse e regressione vengono anche illustrati in che consentono di stimare distribuzione hello per quantità suggerimento hello a pagamento.

procedura Hello segue hello [Team Data Science processo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) flusso di lavoro. Viene illustrato come toosetup un ambiente di analisi scientifica dei dati, come tooload hello dati nel data Warehouse di SQL e come usare data Warehouse SQL o un IPython Notebook tooexplore hello dati e tecnico funzionalità toomodel. È quindi possibile visualizzare come toobuild e distribuire un modello con Azure Machine Learning.

## <a name="dataset"></a>set di dati NYC Taxi trip Hello
dati di andata e ritorno Taxi NYC Hello è costituita da circa 20GB di file CSV compressi (~ 48GB non compressi), registrazione 173 milioni hello e singoli trip tariffe a pagamento per ogni itinerario. Ogni record di andata e ritorno include percorsi di ritiro e deposito hello e volte, resi anonimi hack numero di patente) (e hello numero medallion (id univoco del taxi). dati Hello copre tutti i percorsi nell'anno hello 2013 e viene forniti in hello dopo i due set di dati per ogni mese:

1. Hello **trip_data.csv** file contiene i dettagli di andata e ritorno, ad esempio il numero di passeggeri, prelievo e dropoff punti, la durata di andata e ritorno e lunghezza di andata e ritorno. Di seguito vengono forniti alcuni record di esempio:
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. Hello **trip_fare.csv** file contiene i dettagli della tariffa di hello pagata per ogni itinerario, ad esempio il tipo di pagamento, quantità tariffa, supplemento e le imposte, suggerimenti e pedaggio e hello totale pagato. Di seguito vengono forniti alcuni record di esempio:
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

Hello **chiave univoca** utilizzato viaggi toojoin\_dati e andata e ritorno\_tariffa è composta da hello e tre i campi seguenti:

* medallion,
* hack\_license e
* pickup\_datetime.

## <a name="mltasks"></a>Risolvere tre tipi di attività di stima
Abbiamo formulare tre problemi di stima in base a hello *suggerimento\_quantità* tooillustrate tre tipi di modellazione di attività:

1. **Classificazione binaria**: toopredict o meno un suggerimento è stato pagato un andata e ritorno, vale a dire un *suggerimento\_quantità* che è maggiore di $0 è un esempio positivo, mentre un *suggerimento\_quantità* $ 0 è riportato un esempio negativo.
2. **Classificazione multiclasse**: intervallo di hello toopredict del suggerimento pagato viaggi hello. Verrà diviso hello *suggerimento\_quantità* in cinque contenitori o le classi:
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. **Attività di regressione**: quantità di hello toopredict del suggerimento a pagamento per un itinerario.  

## <a name="setup"></a>Configurare un ambiente di analisi scientifica dei dati di Azure hello per analitica avanzate
tooset dell'ambiente di analisi scientifica dei dati di Azure, seguire questi passaggi.

**Creare l'account di archiviazione BLOB di Azure**

* Quando si esegue il provisioning manualmente l'archiviazione blob di Azure, scegliere una posizione geografica per l'archiviazione blob di Azure in ingresso o in più vicino possibile troppo**centro-meridionali**, ovvero in cui è archiviato i dati NYC Taxi hello. verranno copiati i dati Hello utilizzando lo strumento AzCopy dalla tooa di contenitore di hello blob pubblici archiviazione nell'account di archiviazione. Hello più vicino di archiviazione blob di Azure è tooSouth Central US, hello più veloce (passaggio 4) questa attività verrà completata.
* toocreate account manualmente l'archiviazione di Azure, hello seguire i passaggi descritti in [gli account di archiviazione di Azure su](../storage/common/storage-create-storage-account.md). Essere note toomake che sui valori hello per le seguenti credenziali di account di archiviazione saranno necessari più avanti in questa procedura dettagliata.
  
  * **Storage Account Name**
  * **Chiave dell'account di archiviazione**
  * **Nome del contenitore** (che si desidera hello toobe di dati archiviati in hello archiviazione blob di Azure)

**Effettuare il provisioning dell'istanza di Azure SQL DW.**
Seguire la documentazione di hello in [creare un Data Warehouse SQL](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) tooprovision un'istanza di SQL Data Warehouse. Verificare che sia possibile effettuare le notazioni su hello seguendo le credenziali di SQL Data Warehouse che verranno usate nei passaggi successivi.

* **Nome server**: <server Name>.database.windows.net
* **Nome SQLDW (database)**
* **Nome utente**
* **Password**

**Installare Visual Studio e SQL Server Data Tools.** Per istruzioni, vedere [Installare Visual Studio 2015 e SSDT per SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).

**Connettere tooyour data Warehouse di SQL Azure con Visual Studio.** Per istruzioni, vedere i passaggi 1 e 2 in [connettersi tooAzure SQL Data Warehouse con Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).

> [!NOTE]
> Esecuzione hello seguente query SQL sul database hello è stato creato in SQL Data Warehouse (connessione argomento, anziché hello query fornito nel passaggio 3 di hello) troppo**creare una chiave master**.
> 
> 

    BEGIN TRY
           --Try toocreate hello master key
        CREATE MASTER KEY
    END TRY
    BEGIN CATCH
           --If hello master key exists, do nothing
    END CATCH;

**Creare un'area di lavoro di Azure Machine Learning nella sottoscrizione di Azure.** Per istruzioni, vedere [Creare un'area di lavoro di Machine Learning di Azure](machine-learning-create-workspace.md).

## <a name="getdata"></a>Caricare i dati di hello in SQL Data Warehouse
Aprire una console dei comandi di Windows PowerShell. Eseguire il seguente hello comandi PowerShell toodownload hello SQL file script di esempio che si condividono con l'utente in GitHub tooa locale nella directory specificata con il parametro hello *- DestDir*. È possibile modificare il valore di hello del parametro *- DestDir* tooany directory locale. Se *- DestDir* non esiste, verrà creata da hello script di PowerShell.

> [!NOTE]
> Potrebbe essere troppo**Esegui come amministratore** quando si esegue lo script di PowerShell seguente, se hello il *DestDir* directory deve tooit toocreate o toowrite con privilegi di amministratore.
> 
> 

    $source = "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/Download_Scripts_SQLDW_Walkthrough.ps1"
    $ps1_dest = "$pwd\Download_Scripts_SQLDW_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQLDW_Walkthrough.ps1 –DestDir 'C:\tempSQLDW'

Dopo la corretta esecuzione, la directory di lavoro corrente cambia troppo*- DestDir*. Dovrebbe essere possibile toosee schermo come di seguito:

![][19]

Nel *- DestDir*, eseguire lo script di PowerShell in modalità amministratore seguente hello:

    ./SQLDW_Data_Import.ps1

Quando uno script di PowerShell hello viene eseguito per hello prima volta, viene chiesto informazioni hello tooinput del data Warehouse SQL Azure e l'account di archiviazione blob di Azure. Al termine di questo script di PowerShell in esecuzione per hello prima volta, le credenziali di hello input si verrà sia stato scritto il file di configurazione tooa SQLDW.conf nella directory di lavoro presenti hello. Hello future di questo file di script di PowerShell ha hello opzione tooread necessari tutti i parametri da questo file di configurazione. Se è necessario toochange alcuni parametri, è possibile scegliere tooinput parametri hello nella schermata di hello al prompt dei comandi per l'eliminazione di questo file di configurazione e l'immissione di valori dei parametri hello come richiesto o valori di parametro hello toochange modificando hello SQLDW.conf file nel *- DestDir* directory.

> [!NOTE]
> In ordine tooavoid schema nome in conflitto con quelli già esistenti del data Warehouse SQL Azure, durante la lettura dei parametri direttamente dal file SQLDW.conf hello, un numero casuale di 3 cifre viene aggiunto il nome di schema toohello dal file SQLDW.conf hello come nome dello schema predefinito di hello per ogni esecuzione. script di PowerShell Hello può richiedere un nome di schema: è possibile specificare il nome di hello a discrezione di utente.
> 
> 

Questo **script di PowerShell** file completa hello seguenti attività:

* **Esegue il download e l'installazione di AzCopy**, se non è già installato
  
        $AzCopy_path = SearchAzCopy
        if ($AzCopy_path -eq $null){
               Write-Host "AzCopy.exe is not found in C:\Program Files*. Now, start installing AzCopy..." -ForegroundColor "Yellow"
            InstallAzCopy
            $AzCopy_path = SearchAzCopy
        }
            $env_path = $env:Path
            for ($i=0; $i -lt $AzCopy_path.count; $i++){
                if ($AzCopy_path.count -eq 1){
                    $AzCopy_path_i = $AzCopy_path
                } else {
                    $AzCopy_path_i = $AzCopy_path[$i]
                }
                if ($env_path -notlike '*' +$AzCopy_path_i+'*'){
                    Write-Host $AzCopy_path_i 'not in system path, add it...'
                    [Environment]::SetEnvironmentVariable("Path", "$AzCopy_path_i;$env_path", "Machine")
                    $env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine")
                    $env_path = $env:Path
                }
* **Copia di account di archiviazione blob privato tooyour dati** dal blob pubblici di hello con AzCopy
  
        Write-Host "AzCopy is copying data from public blob tooyo storage account. It may take a while..." -ForegroundColor "Yellow"
        $start_time = Get-Date
        AzCopy.exe /Source:$Source /Dest:$DestURL /DestKey:$StorageAccountKey /S
        $end_time = Get-Date
        $time_span = $end_time - $start_time
        $total_seconds = [math]::Round($time_span.TotalSeconds,2)
        Write-Host "AzCopy finished copying data. Please check your storage account tooverify." -ForegroundColor "Yellow"
        Write-Host "This step (copying data from public blob tooyour storage account) takes $total_seconds seconds." -ForegroundColor "Green"
* **Carica dati tramite Polybase (eseguendo LoadDataToSQLDW.sql) tooyour Azure SQL DW** dall'account di archiviazione blob privato con hello i comandi seguenti.
  
  * Creare uno schema
    
          EXEC (''CREATE SCHEMA {schemaname};'');
  * Creare una credenziale con ambito di database
    
          CREATE DATABASE SCOPED CREDENTIAL {KeyAlias}
          WITH IDENTITY = ''asbkey'' ,
          Secret = ''{StorageAccountKey}''
  * Creare un'origine dati esterna per un BLOB di archiviazione di Azure
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_trip_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_fare_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
  * Creare un formato di file esterno da un file con estensione csv. Dati non compressi e campi sono separati dal carattere barra verticale hello.
    
          CREATE EXTERNAL FILE FORMAT {csv_file_format}
          WITH
          (   
              FORMAT_TYPE = DELIMITEDTEXT,
              FORMAT_OPTIONS  
              (
                  FIELD_TERMINATOR ='','',
                  USE_TYPE_DEFAULT = TRUE
              )
          )
          ;
  * Creare tabelle esterne relative a tariffe e corse per il set di dati relativo alle corse dei taxi di New York nell'archivio BLOB di Azure.
    
          CREATE EXTERNAL TABLE {external_nyctaxi_fare}
          (
              medallion varchar(50) not null,
              hack_license varchar(50) not null,
              vendor_id char(3),
              pickup_datetime datetime not null,
              payment_type char(3),
              fare_amount float,
              surcharge float,
              mta_tax float,
              tip_amount float,
              tolls_amount float,
              total_amount float
          )
          with (
              LOCATION    = ''/nyctaxifare/'',
              DATA_SOURCE = {nyctaxi_fare_storage},
              FILE_FORMAT = {csv_file_format},
              REJECT_TYPE = VALUE,
              REJECT_VALUE = 12     
          )  

            CREATE EXTERNAL TABLE {external_nyctaxi_trip}
            (
                   medallion varchar(50) not null,
                   hack_license varchar(50)  not null,
                   vendor_id char(3),
                   rate_code char(3),
                   store_and_fwd_flag char(3),
                   pickup_datetime datetime  not null,
                   dropoff_datetime datetime,
                   passenger_count int,
                   trip_time_in_secs bigint,
                   trip_distance float,
                   pickup_longitude varchar(30),
                   pickup_latitude varchar(30),
                   dropoff_longitude varchar(30),
                   dropoff_latitude varchar(30)
            )
            with (
                LOCATION    = ''/nyctaxitrip/'',
                DATA_SOURCE = {nyctaxi_trip_storage},
                FILE_FORMAT = {csv_file_format},
                REJECT_TYPE = VALUE,
                REJECT_VALUE = 12         
            )

    - Caricare i dati da tabelle esterne in tooSQL di archiviazione blob di Azure Data Warehouse

            CREATE TABLE {schemaname}.{nyctaxi_fare}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_fare}
            ;

            CREATE TABLE {schemaname}.{nyctaxi_trip}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_trip}
            ;

    - Creare una tabella di dati di esempio (NYCTaxi_Sample) e inserire dati tooit dalla selezione delle query SQL sulle tabelle di andata e ritorno e tariffa hello. (Alcuni passaggi di questa procedura dettagliata è necessario toouse questa tabella di esempio.)

            CREATE TABLE {schemaname}.{nyctaxi_sample}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            (
                SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount,
                tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
                tip_class = CASE
                        WHEN (tip_amount = 0) THEN 0
                        WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                        WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                        WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                        ELSE 4
                    END
                FROM {schemaname}.{nyctaxi_trip} t, {schemaname}.{nyctaxi_fare} f
                WHERE datepart("mi",t.pickup_datetime) = 1
                AND t.medallion = f.medallion
                AND   t.hack_license = f.hack_license
                AND   t.pickup_datetime = f.pickup_datetime
                AND   pickup_longitude <> ''0''
                AND   dropoff_longitude <> ''0''
            )
            ;

posizione geografica di Hello degli account di archiviazione influisce sui tempi di caricamento.

> [!NOTE]
> A seconda della posizione geografica di hello dell'account di archiviazione blob privato, hello processo di copia dei dati da un account di archiviazione privato tooyour blob pubblico può saranno necessari circa 15 minuti o anche più e hello processo di caricamento dei dati dall'account di archiviazione Azure SQL DW tooyour può richiedere 20 minuti o più.  
> 
> 

Sarà necessario toodecide cosa fare se si dispone di origine e i file di destinazione.

> [!NOTE]
> Se toobe di file con estensione csv hello copiati dall'account di archiviazione blob privato tooyour archiviazione blob pubblici hello già esiste nell'account di archiviazione blob privato, AzCopy verrà chiesto se si desidera toooverwrite li. Se non si desidera toooverwrite così input  **n**  quando richiesto. Se si desidera toooverwrite **tutti** di essi, di input **un** quando richiesto. È anche possibile immettere **y** toooverwrite CSV file singolarmente.
> 
> 

![Grafico n. 21][21]

È possibile usare i propri dati. Se i dati sono nel computer locale in un'applicazione reale, è comunque possibile usare AzCopy tooupload locale dati tooyour privata di archiviazione blob Azure. È necessario solo hello toochange **origine** posizione, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, in hello AzCopy comando hello PowerShell script toohello locale della directory del file che contiene i dati.

> [!TIP]
> Se i dati sono già nell'archiviazione blob di Azure privato dell'applicazione di uno scenario reale, è possibile ignorare hello AzCopy passaggio hello script di PowerShell e caricare direttamente hello dati tooAzure SQL DW. Questo richiederà ulteriori la modifica di hello script tootailor toohello formato dei dati.
> 
> 

Questo script di Powershell anche inserisce informazioni di Azure SQL DW in hello dati l'esplorazione dei file di esempio SQLDW_Explorations.sql, SQLDW_Explorations.ipynb e SQLDW_Explorations_Scripts.py hello in modo che questi tre file siano pronti toobe provato immediatamente al termine dell'esecuzione hello script di PowerShell.

Al termine dell'esecuzione, verrà visualizzata una schermata simile alla seguente:

![][20]

## <a name="dbexplore"></a>Esplorazione dei dati e progettazione di funzionalità in Azure SQL Data Warehouse
In questa sezione vengono effettuate l'esplorazione dei dati e la generazione di funzionalità eseguendo query SQL direttamente su Azure SQL DW usando **Visual Studio Data Tools**. Tutte le query SQL utilizzate in questa sezione sono disponibili nello script di esempio hello denominato *SQLDW_Explorations.sql*. Questo file è già stato scaricato tooyour directory locale dallo script di PowerShell hello. È anche possibile recuperarlo da [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql), Ma il file hello in GitHub non dispone di informazioni di Azure SQL DW hello collegate.

Connettersi con Visual Studio con il nome di accesso SQL DW hello e una password di Azure SQL DW tooyour e aprire hello **Esplora oggetti di SQL** tooconfirm hello database e le tabelle sono state importate. Recuperare hello *SQLDW_Explorations.sql* file.

> [!NOTE]
> tooopen un editor di query Parallel Data Warehouse (PDW), utilizzare hello **nuova Query** comando mentre è selezionato il PDW in hello **Esplora oggetti di SQL**. editor di query SQL standard Hello non è supportato da PDW.
> 
> 

Di seguito sono di tipo hello di dati eseguite attività di generazione di esplorazione e funzionalità in questa sezione:

* Esplorazione delle distribuzioni di dati di un numero ridotto di campi in diverse finestre temporali.
* Analizzare la qualità dei dati dei campi di longitudine e latitudine hello.
* Generare etichette di classificazione multiclasse e binaria dipende hello **suggerimento\_quantità**.
* Generazione di funzionalità calcolo/confronto delle distanze delle corse.
* Join di tabelle hello due ed estrarre un campione casuale che verrà utilizzato toobuild modelli.

### <a name="data-import-verification"></a>Verifica dell'importazione dei dati
Queste query offrono una rapida verifica del numero di hello di righe e colonne in tabelle compilate in precedenza mediante bulk parallela del Polybase importano, hello

    -- Report number of rows in table <nyctaxi_trip> without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')

    -- Report number of columns in table <nyctaxi_trip>
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = '<nyctaxi_trip>' AND table_schema = '<schemaname>'

**Output:** si dovrebbero ottenere 173.179.759 righe e 14 colonne.

### <a name="exploration-trip-distribution-by-medallion"></a>Esplorazione: distribuzione delle corse per licenza
Questo esempio di query identifica medallions hello (numeri taxi) completata più di 100 trip all'interno di un periodo di tempo specificato. query Hello può costituire un vantaggio accesso alle tabelle partizionata hello poiché condizionato, dallo schema di partizione hello di **prelievo\_datetime**. Una query di set di dati completo hello renderà inoltre usare della tabella partizionata hello e/o l'analisi di indice.

    SELECT medallion, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

**Output:** query hello deve restituire una tabella con righe specificando medallions hello 13,369 (taxi) e numero di andata e ritorno completata da essi in 2013 hello. Hello ultima colonna contiene il conteggio di hello del numero di hello di viaggi completata.

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a>Esplorazione: distribuzione delle corse per licenza e hack_license
In questo esempio identifica medallions hello (numeri taxi) e hack_license numeri (driver) che è stata completata più di 100 trip all'interno di un periodo di tempo specificato.

    SELECT medallion, hack_license, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

**Output:** query hello devono restituire una tabella con 13,369 righe specificando hello 13,369 Auto/driver ID completate più di 100 trip nel 2013. Hello ultima colonna contiene il conteggio di hello del numero di hello di viaggi completata.

### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a>Valutazione della qualità dei dati: verifica dei record con longitudine o latitudine errate
In questo esempio consente di esaminare se i campi di longitudine e/o latitudine hello contenere un valore non valido (gradi in radianti devono essere compreso tra -90 e 90,) o (0, 0) le coordinate.

    SELECT COUNT(*) FROM <schemaname>.<nyctaxi_trip>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

**Output:** query hello restituisce 837,467 trip contenenti campi non validi di longitudine e/o latitudine.

### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a>Esplorazione: distribuzione delle corse per le quali è stata lasciata una mancia e di quelle per le quali non è stata lasciata una mancia
In questo esempio trova il numero di hello di viaggi che sono stati inclinato rispetto al numero di hello che non sono stati inclinato in un periodo di tempo specificato (o in hello set di dati completo se per l'anno completo hello come è configurato in questo caso). Questa distribuzione riflette hello binario etichetta distribuzione toobe utilizzato successivamente per la modellazione di classificazione binaria.

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM <schemaname>.<nyctaxi_fare>
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

**Output:** hello query deve seguente hello restituito suggerimento le frequenze per anno hello inclinato 2013: 90,447,622 e 82,264,709 inclinato non.

### <a name="exploration-tip-classrange-distribution"></a>Esplorazione: distribuzione della classe o dell'intervallo delle mance
Questo esempio calcola la distribuzione di hello degli intervalli di comandi in un determinato momento periodo (o in hello set di dati completo se per l'anno di hello completo). Si tratta di distribuzione hello di classi di etichetta hello che verrà usato successivamente per la modellazione di classificazione multiclasse.

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

**Output:**

| tip_class | tip_freq |
| --- | --- |
| 1 |82230915 |
| 2 |6198803 |
| 3 |1932223 |
| 0 |82264625 |
| 4 |85765 |

### <a name="exploration-compute-and-compare-trip-distance"></a>Esplorazione: calcolo e confronto della distanza delle corse
In questo esempio converte la longitudine di ritiro e deposito hello e geography tooSQL latitudine punta, distanza di andata e ritorno hello utilizzando SQL geography punti differenza calcola e restituisce un campione casuale di risultati hello per il confronto. esempio Hello limita i risultati di hello toovalid coordinate solo tramite query valutazione della qualità dei dati hello descritti in precedenza.

    /****** Object:  UserDefinedFunction [dbo].[fnCalculateDistance] ******/
    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function toocalculate hello direct distance  in mile between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

### <a name="feature-engineering-using-sql-functions"></a>Progettazione di funzionalità con le funzioni SQL
Le funzioni SQL a volte possono essere una valida opzione per progettare funzionalità. In questa procedura dettagliata, è stato definito una SQL funzione toocalculate hello distanza diretta tra i percorsi di ritiro e dropoff hello. È possibile eseguire script SQL in seguito hello **Visual Studio Data Tools**.

Di seguito è riportato uno script SQL hello che definisce la funzione di distanza hello.

    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function calculate hello direct distance between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

Ecco un esempio toocall questa funzionalità toogenerate funzione nella query SQL:

    -- Sample query toocall hello function toocreate features
    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

**Output:** questa query genera una tabella (con 2,803,538 righe) con Latitude prelievo e dropoff e longitudine e hello corrispondente diretti chilometri. Di seguito sono risultati hello per primi 3 righe:

|  | pickup_latitude | pickup_longitude | dropoff_latitude | dropoff_longitude | DirectDistance |
| --- | --- | --- | --- | --- | --- |
| 1 |40.731804 |-74.001083 |40.736622 |-73.988953 |.7169601222 |
| 2 |40.715794 |-74,010635 |40.725338 |-74.00399 |.7448343721 |
| 3 |40.761456 |-73.999886 |40.766544 |-73.988228 |0.7037227967 |

### <a name="prepare-data-for-model-building"></a>Preparazione dei dati per la creazione del modello
hello join di query seguente di Hello **nyctaxi\_viaggi** e **nyctaxi\_tariffa** tabelle, genera un'etichetta di classificazione binaria **inclinato**, etichetta di classificazione multiclasse **suggerimento\_classe**ed estrae un esempio di hello completo aggiunti a un set di dati. campionamento Hello avviene mediante il recupero di un subset di trip hello in base al tempo di prelievo.  Questa query può essere copiata successivamente incollata direttamente in hello [Azure Machine Learning Studio](https://studio.azureml.net) [l'importazione dei dati] [ import-data] modulo per l'inserimento di dati direttamente dall'istanza di database SQL di hello in Azure. query Hello esclude i record con errato (0, 0) le coordinate.

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
    WHERE datepart("mi",t.pickup_datetime) = 1
    AND   t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

Quando si è pronti tooproceed tooAzure Machine Learning, è possibile:  

1. Salvare hello finale SQL query tooextract ed esempio hello dati e copia e Incolla hello query direttamente in un [l'importazione dei dati] [ import-data] modulo in Azure Machine Learning, o
2. Mantenere hello campionato e dati decodificati Prevedi toouse per modello di compilazione in un nuovo data Warehouse di SQL tabella e usare nuova tabella hello in hello [l'importazione dei dati] [ import-data] modulo in Azure Machine Learning. Hello script di PowerShell nel passaggio precedente ha eseguito questa operazione per l'utente. È possibile leggere direttamente dalla tabella nel modulo di importazione dei dati hello.

## <a name="ipnb"></a>Esplorazione dei dati e progettazione di funzionalità in IPython Notebook
In questa sezione, si eseguirà l'esplorazione dei dati e la generazione di funzionalità mediante entrambi Python e query SQL su SQL DW hello creato in precedenza. IPython notebook esempio denominato **SQLDW_Explorations.ipynb** e un file di script Python **SQLDW_Explorations_Scripts.py** sono stati scaricati tooyour directory locale. Sono disponibili anche in [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW). Questi due file sono identici negli script di Python. file di script Python Hello viene fornito tooyou nel caso in cui non è un server di IPython Notebook. Questi due file di Python di esempio sono stati progettati in **Python 2.7**.

le informazioni di Azure SQL DW: esempio hello IPython Notebook Hello e hello Python macchina locale scaricato tooyour file di script è stato collegato dallo script di PowerShell hello in precedenza. Possono essere eseguiti senza alcuna modifica.

Se un'area di lavoro di Azure ml è già stato configurato, è possibile caricare l'esempio hello del servizio di Azure ml IPython Notebook toohello IPython Notebook direttamente e avviarne l'esecuzione. Di seguito sono hello passaggi tooupload tooAzureML servizio IPython Notebook:

1. Nell'area di lavoro Azure ml tooyour di log, fare clic su "Studio" nella parte superiore di hello e fare clic su "Notebook" sul lato sinistro di hello della pagina web hello.
   
    ![Grafico n. 22][22]
2. Fare clic su "Nuovo" nell'angolo inferiore sinistro hello della pagina web hello e selezionare "Python 2". Fornire un notebook toohello nome, quindi fare clic su hello segno di spunta toocreate hello vuoto nuovo IPython Notebook.
   
    ![Grafico n. 23][23]
3. Fare clic sul simbolo "Jupyter" hello nell'angolo superiore sinistro di hello di hello nuovo IPython Notebook.
   
    ![Grafico n. 24][24]
4. Trascinare e rilasciare hello esempio IPython Notebook toohello **albero** pagina dei servizi di Azure ml IPython Notebook, fare clic su **caricare**. Quindi, l'esempio hello IPython Notebook sarà toohello caricato il servizio di Azure ml IPython Notebook.
   
    ![Grafico n. 25][25]

In hello toorun ordine esempio IPython Notebook o file di script Python hello, hello pacchetti Python seguenti sono necessari. Se si utilizza il servizio di Azure ml IPython Notebook hello, questi pacchetti sono stati già installati.

    - pandas
    - numpy
    - matplotlib
    - pyodbc
    - PyTables

Hello sequenza consigliata durante la compilazione di soluzioni di analisi avanzate in Azure ml con dati di grandi dimensioni può essere seguito hello:

* Lettura in un piccolo esempio dei dati hello in un frame di dati in memoria.
* Eseguire alcune visualizzazioni e delle esplorazioni utilizzando hello dati campionati.
* Provare varie combinazioni di progettazione di funzionalità mediante hello dati campionati.
* Per l'esplorazione dei dati più grande, la modifica dei dati e progettazione di funzionalità, utilizzare Python tooissue query SQL direttamente hello SQL DW.
* Decidere per l'esempio hello dimensioni toobe adatto per la compilazione del modello di Azure Machine Learning.

Hello seguito sono riportati alcuni l'esplorazione dei dati, visualizzazione dei dati ed esempi di progettazione di funzionalità. Sono disponibili ulteriori analisi di dati: esempio hello IPython Notebook e file di script Python di esempio hello.

### <a name="initialize-database-credentials"></a>Inizializzare le credenziali di database
Inizializzare le impostazioni di connessione di database in hello seguenti variabili:

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database driver>

### <a name="create-database-connection"></a>Creare la connessione al database
Di seguito è stringa di connessione hello crea hello connessione toohello database.

    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a>Segnalare il numero di righe e di colonne nella tabella <nyctaxi_trip>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_trip>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* Numero di righe totali = 173179759  
* Numero di colonne totali = 14

### <a name="report-number-of-rows-and-columns-in-table-nyctaxifare"></a>Segnalare il numero di righe e di colonne nella tabella <nyctaxi_fare>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_fare>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_fare>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* Numero di righe totali = 173179759  
* Numero di colonne totali = 11

### <a name="read-in-a-small-data-sample-from-hello-sql-data-warehouse-database"></a>Lettura in un campione di dati di dimensioni ridotte da hello Database di SQL Data Warehouse
    t0 = time.time()

    query = '''
        SELECT TOP 10000 t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
        WHERE datepart("mi",t.pickup_datetime) = 1
        AND   t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

Tabella di esempio hello tooread ora è 14.096495 secondi.  
Numero di righe e di colonne recuperate = (1000, 21)

### <a name="descriptive-statistics"></a>Statistiche descrittive
A questo punto è dati campionato hello tooexplore pronto. Iniziamo con esaminano alcune statistiche descrittive per hello **viaggi\_distanza** (o qualsiasi altro campo scelto toospecify).

    df1['trip_distance'].describe()

### <a name="visualization-box-plot-example"></a>Visualizzazione: esempio di box plot
Successivamente vengono analizzati grafico box plot di hello per hello viaggi distanza toovisualize hello quantili.

    df1.boxplot(column='trip_distance',return_type='dict')

![Grafico n. 1][1]

### <a name="visualization-distribution-plot-example"></a>Visualizzazione: esempio di tracciato di distribuzione
Grafici che visualizzano distribuzione hello e un istogramma per hello campionate distanze di andata e ritorno.

    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Grafico n. 2][2]

### <a name="visualization-bar-and-line-plots"></a>Visualizzazione: tracciati a barre e linee
In questo esempio è bin distanza di andata e ritorno hello in cinque bin e visualizzare i risultati di binning hello.

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

È possibile tracciare hello sopra distribuzione bin in una barra o riga del tracciato con:

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Grafico n. 3][3]

e

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Grafico n. 4][4]

### <a name="visualization-scatterplot-examples"></a>Visualizzazione: esempi di grafico a dispersione
Viene illustrata la dispersione tra **viaggi\_ora\_in\_sec** e **viaggi\_distanza** toosee nel caso di qualsiasi correlazione

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![Grafico n. 6][6]

Analogamente è possibile controllare la relazione hello tra **frequenza\_codice** e **viaggi\_distanza**.

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![Grafico n. 8][8]

### <a name="data-exploration-on-sampled-data-using-sql-queries-in-ipython-notebook"></a>Esplorazione nei dati campionati usando query SQL in IPython Notebook
In questa sezione vengono analizzate le distribuzioni dei dati utilizzando i dati campionato hello che viene mantenuti nella nuova tabella hello creato in precedenza. Si noti che esplorazioni simile possono essere eseguite mediante tabelle originali hello.

#### <a name="exploration-report-number-of-rows-and-columns-in-hello-sampled-table"></a>Esplorazione: Numero di righe e colonne in hello campionate tabella
    nrows = pd.read_sql('''SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_sample>')''', conn)
    print 'Number of rows in sample = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''SELECT count(*) FROM information_schema.columns WHERE table_name = ('<nyctaxi_sample>') AND table_schema = '<schemaname>'''', conn)
    print 'Number of columns in sample = %d' % ncols.iloc[0,0]

#### <a name="exploration-tippednot-tripped-distribution"></a>Esplorazione: distribuzione delle corse per cui è stata lasciata una mancia e di quelle per cui non è stata lasciata una mancia
    query = '''
        SELECT tipped, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tipped
        '''

    pd.read_sql(query, conn)

#### <a name="exploration-tip-class-distribution"></a>Esplorazione: distribuzione della classe delle mance
    query = '''
        SELECT tip_class, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tip_class
    '''

    tip_class_dist = pd.read_sql(query, conn)

#### <a name="exploration-plot-hello-tip-distribution-by-class"></a>Esplorazione: Tracciare distribuzione suggerimento hello dalla classe
    tip_class_dist['tip_freq'].plot(kind='bar')

![Grafico n. 26][26]

#### <a name="exploration-daily-distribution-of-trips"></a>Esplorazione: distribuzione giornaliera delle corse
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a>Esplorazione: distribuzione delle corse per licenza
    query = '''
        SELECT medallion,count(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-by-medallion-and-hack-license"></a>Esplorazione: distribuzione delle corse per licenza e hack_license
    query = '''select medallion, hack_license,count(*) from <schemaname>.<nyctaxi_sample> group by medallion, hack_license'''
    pd.read_sql(query,conn)


#### <a name="exploration-trip-time-distribution"></a>Esplorazione: distribuzione degli orari delle corse
    query = '''select trip_time_in_secs, count(*) from <schemaname>.<nyctaxi_sample> group by trip_time_in_secs order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-trip-distance-distribution"></a>Esplorazione: distribuzione delle distanze delle corse
    query = '''select floor(trip_distance/5)*5 as tripbin, count(*) from <schemaname>.<nyctaxi_sample> group by floor(trip_distance/5)*5 order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-payment-type-distribution"></a>Esplorazione: distribuzione dei tipi di pagamento
    query = '''select payment_type,count(*) from <schemaname>.<nyctaxi_sample> group by payment_type'''
    pd.read_sql(query,conn)

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a>Verificare il modulo di finale hello della tabella trasformato hello
    query = '''SELECT TOP 100 * FROM <schemaname>.<nyctaxi_sample>'''
    pd.read_sql(query,conn)

## <a name="mlmodel"></a>Creare modelli in Azure Machine Learning
Sono ora pronti tooproceed toomodel compilazione e distribuzione di modelli in [Azure Machine Learning](https://studio.azureml.net). dati Hello sono pronto toobe utilizzata in uno qualsiasi dei problemi di stima hello identificati in precedenza, vale a dire:

1. **Classificazione binaria**: toopredict o meno un suggerimento è stato pagato per un itinerario.
2. **Classificazione multiclasse**: intervallo di hello toopredict del suggerimento a pagamento, in base a toohello classi definite in precedenza.
3. **Attività di regressione**: quantità di hello toopredict del suggerimento a pagamento per un itinerario.  

toobegin hello esercizio di modellazione, accedi tooyour **Azure Machine Learning** dell'area di lavoro. Se non è ancora disponibile un'area di lavoro di machine learning, vedere [Creare un'area di lavoro Azure ML](machine-learning-create-workspace.md).

1. tooget avviato con Azure Machine Learning, vedere [che cos'è Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)
2. Accedi troppo[Azure Machine Learning Studio](https://studio.azureml.net).
3. pagina iniziale di Studio Hello un'ampia gamma di informazioni, video, esercitazioni, collegamenti toohello riferimento moduli e altre risorse. Per ulteriori informazioni su Azure Machine Learning, consultare hello [Centro documentazione di Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/).

Un esperimento di training tipica è costituita da hello alla procedura seguente:

1. Creazione di un esperimento **+NEW** .
2. Ottenere dati di hello in Azure ML.
3. Pre-elaborazione, trasformare e modificare i dati di hello in base alle esigenze.
4. Generazione di funzionalità, se necessario.
5. Suddividere i dati di hello in set di dati di training e la convalida o il test (o set di dati separati per ogni).
6. Selezionare uno o più algoritmi di machine learning a seconda di hello toosolve problema di apprendimento. Ad esempio, classificazione binaria, classificazione multiclasse, regressione.
7. Eseguire il training di uno o più modelli utilizzando hello training set.
8. Assegnare un punteggio hello convalida set di dati utilizzando modelli con training hello.
9. Valutare hello modelli toocompute hello le metriche pertinenti per l'apprendimento problema hello.
10. Ottimizzare i modelli di hello e selezionare hello migliore modello toodeploy.

In questo esercizio, abbiamo già esplorato e decodificati dati hello in SQL Data Warehouse e deciso tooingest dimensioni di esempio hello in Azure Machine Learning. Ecco hello procedure toobuild uno o più modelli di previsione hello:

1. Ottenere dati hello in Azure ML utilizzando hello [l'importazione dei dati] [ import-data] modulo, disponibile in hello **dati di Input e Output** sezione. Per ulteriori informazioni, vedere hello [l'importazione dei dati] [ import-data] pagina di riferimento modulo.
   
    ![Import Data di Azure ML][17]
2. Selezionare **Database SQL di Azure** come hello **origine dati** in hello **proprietà** pannello.
3. Immettere nome DNS del database hello in hello **nome server Database** campo. Formato: `tcp:<your_virtual_machine_DNS_name>,1433`
4. Immettere hello **nome del Database** nel campo corrispondente hello.
5. Immettere hello *nome utente di SQL* in hello **nome dell'account utente Server**, hello e *password* in hello **password dell'account utente Server**.
6. Controllare hello **accettare qualsiasi certificato server** opzione.
7. In hello **query Database** Modifica area di testo, incollare query hello estrae hello necessario campi (incluse eventuali campi calcolati, ad esempio etichette hello) del database e verso il basso esempi di dimensioni del campione hello dati toohello desiderato.

Un esempio di un esperimento di classificazione binaria, la lettura dei dati direttamente dal database di SQL Data Warehouse hello è nella figura che segue hello (ricordare tooreplace hello nomi nyctaxi_trip e nyctaxi_fare dallo schema hello utilizzato nel nome e hello nomi di tabella il procedura dettagliata). È possibile creare esperimenti dello stesso tipo per i problemi di classificazione multiclasse e di regressione.

![Formazione su Azure ML][10]

> [!IMPORTANT]
> In hello modellazione estrazione dei dati e il campionamento di esempi di query forniti nelle sezioni precedenti, **tutte le etichette per gli esercizi di modellazione hello tre sono inclusi nella query hello**. Un passaggio importante (obbligatorio) in ogni hello esercizi sulla modellazione è troppo**escludere** hello etichette non necessari per hello altri due problemi e qualsiasi altro **destinazione perdite**. Ad esempio, quando si utilizza una classificazione binaria, utilizzare l'etichetta hello **inclinato** ed escludere i campi di hello **suggerimento\_classe**, **suggerimento\_quantità**, e **totale\_quantità**. Hello quest'ultimo vengono pagate perdite di destinazione, perché implicano suggerimento hello.
> 
> tooexclude eventuali colonne non necessarie o perdite di destinazione, è possibile utilizzare hello [selezionare le colonne nel set di dati] [ select-columns] modulo o hello [Modifica metadati] [ edit-metadata]. Per altre informazioni, vedere le pagine di riferimento per [Select Columns in Dataset][select-columns] (Seleziona colonne in set di dati) ed [Edit Metadata][edit-metadata] (Modifica metadati).
> 
> 

## <a name="mldeploy"></a>Distribuire modelli in Azure Machine Learning
Quando il modello è pronto, è possibile distribuirlo facilmente come servizio web direttamente da esperimento hello. Per ulteriori informazioni sulla distribuzione di servizi Web Azure ML, vedere [Distribuzione di un servizio Web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

toodeploy un nuovo servizio web, è necessario:

1. Creare un esperimento di assegnazione di punteggio.
2. Distribuire il servizio web hello.

un punteggio sperimentare da toocreate un **completato** esperimento di training, fare clic su **CREATE SCORING EXPERIMENT** nella barra delle azioni inferiore hello.

![Valutazione di Azure][18]

Azure Machine Learning tenterà toocreate un esperimento di assegnazione dei punteggi in base ai componenti di hello dell'esperimento di training hello. In particolare, verranno effettuate le seguenti operazioni:

1. Salva modello con training hello e rimuovere i moduli di training modello di hello.
2. Identificare una logica **porta di input** toorepresent hello previsto schema dati di input.
3. Identificare una logica **porta di output** toorepresent dello schema output di hello web previsto del servizio.

Quando viene creato l'assegnazione dei punteggi esperimento hello, esaminarla e adattare in base alle esigenze. Un esempio tipico di regolazione sia set di dati tooreplace hello input e/o query con uno che esclude i campi di etichetta, poiché questi non saranno disponibili quando viene chiamato servizio hello. È anche una dimensione di hello tooreduce buona norma di hello alcuni record, dello schema di input sufficiente hello tooindicate tooa set di dati e/o query di input. Per la porta di output di hello, è comune tooexclude campi di tutti gli input e includere solo hello **Scored Labels** e **calcolato il punteggio della probabilità** in hello output utilizzando hello [selezionare le colonne nel set di dati ] [ select-columns] modulo.

Un esempio esperimento di assegnazione dei punteggi viene fornito nella figura hello seguente. Al termine toodeploy, fare clic su hello **servizio WEB di pubblicare** pulsante nella barra delle azioni inferiore hello.

![Pubblicazione di Azure ML][11]

## <a name="summary"></a>Riepilogo
toorecap cosa che abbiamo realizzato in questa esercitazione di questa procedura dettagliata, è stato creato un ambiente di analisi scientifica dei dati di Azure, ha collaborato con un ampio set di dati pubblici, portarlo tramite hello processo di analisi scientifica dei dati Team, tutte le modalità di hello dal training toomodel acquisizione di dati, quindi toohello distribuzione di un servizio web Azure Machine Learning.

### <a name="license-information"></a>Informazioni sulla licenza
In questa procedura dettagliata di esempio e il relativo tipo di accompagnamento notebook(s) IPython e script sono condivisi da Microsoft con licenza MIT hello. Nella directory di hello del codice di esempio hello su GitHub per ulteriori dettagli, controllare file License hello in.

## <a name="references"></a>Riferimenti
•    [Pagina di Andrés Monroy per scaricare i dati sulle corse dei taxi di NYC](http://www.andresmh.com/nyctaxitrips/)  
•    [Complemento dai dati sulle corse dei taxi di NYC di Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/)   
•    [Ricerche e statistiche su NYC Taxi and Limousine Commission](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)

[1]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sqldw-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sqldw-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlscoring.png
[19]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_download_scripts.png
[20]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_load_data.png
[21]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azcopy-overwrite.png
[22]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-1.png
[23]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-2.png
[24]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-3.png
[25]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-4.png
[26]: ./media/machine-learning-data-science-process-sqldw-walkthrough/tip_class_hist_1.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
