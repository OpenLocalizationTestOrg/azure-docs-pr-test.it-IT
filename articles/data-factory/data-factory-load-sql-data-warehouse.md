---
title: aaaLoad terabyte di dati in SQL Data Warehouse | Documenti Microsoft
description: Illustra come caricare 1 TB di dati in Azure SQL Data Warehouse in meno di 15 minuti con Azure Data Factory
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: a6c133c0-ced2-463c-86f0-a07b00c9e37f
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: e63f60461b082b0e3979004cb631dbf4a6710de3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-1-tb-into-azure-sql-data-warehouse-under-15-minutes-with-data-factory"></a>Caricare 1 TB di dati in Azure SQL Data Warehouse in meno di 15 minuti con Data Factory
[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) è un database basato su cloud, con possibilità di aumentare il numero di istanze, che può elaborare volumi massivi di dati relazionali e non relazionali.  Basato sull'architettura di elaborazione parallela massiva (MPP, Massively Parallel Processing), SQL Data Warehouse è ottimizzato per i carichi di lavoro dei data warehouse dell'organizzazione.  Offre l'elasticità con hello flessibilità tooscale di archiviazione del cloud e di calcolo in modo indipendente.

L'uso di Azure SQL Data Warehouse è ora più semplice dell'uso di **Azure Data Factory**.  Data Factory di Azure è un servizio di integrazione di dati basato su cloud completamente gestito, che può essere utilizzato toopopulate un SQL Data Warehouse con dati hello dal sistema esistente e risparmiare tempo prezioso durante la valutazione di SQL Data Warehouse e la compilazione del analitica soluzioni. Ecco i vantaggi principali di hello di caricare dati in Azure SQL Data Warehouse utilizzando Data Factory di Azure:

* **Facile tooset backup**: 5-intuitivo guidata non necessari di scripting.
* **Supporto completo per archivi dati**: supporto integrato per una vasta gamma di archivi dati locali e basati su cloud.
* **Protetti e conformi**: i dati vengono trasferiti tramite HTTPS ExpressRoute e presenza servizio globale garantisce i dati non oltrepassa mai confini geografici hello
* **Prestazioni ineguagliabile tramite PolyBase** – utilizzando Polybase è più efficiente modo toomove dati hello in Azure SQL Data Warehouse. Utilizza hello funzionalità blob di gestione temporanea, è possibile ottenere la velocità di carico elevato da tutti i tipi di archivi dati oltre all'archiviazione Blob di Azure che hello Polybase supporta per impostazione predefinita.

In questo articolo illustra come toouse Data Factory Copia guidata tooload 1 TB dati dall'archiviazione Blob di Azure in Azure SQL Data Warehouse in meno di 15 minuti, a una velocità effettiva superiore a 1,2 GBps.

In questo articolo vengono fornite istruzioni dettagliate per lo spostamento dei dati tramite Copia guidata hello in Azure SQL Data Warehouse.

> [!NOTE]
>  Per informazioni generali sulle funzionalità di Data Factory di spostamento dei dati da e verso Azure SQL Data Warehouse, vedere [spostare tooand dati da Azure SQL Data Warehouse usando Azure Data Factory](data-factory-azure-sql-data-warehouse-connector.md) articolo.
>
> È anche possibile creare pipeline usando il portale di Azure, Visual Studio, PowerShell e così via. Vedere [esercitazione: copiare i dati da tooAzure Blob di Azure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per un'esercitazione rapida con istruzioni dettagliate per l'utilizzo di attività di copia hello in Data Factory di Azure.  
>
>

## <a name="prerequisites"></a>Prerequisiti
* Archivio BLOB di Azure: questo esperimento usa l'archivio BLOB di Azure (GRS) per l'archiviazione di set di dati di test TPC-H.  Se non si dispone di un account di archiviazione di Azure, ottenere informazioni [come un account di archiviazione toocreate](../storage/common/storage-create-storage-account.md#create-a-storage-account).
* [TPC-H](http://www.tpc.org/tpch/) dati: verrà toouse TPC-H come set di dati testing hello.  toodo, è necessario toouse `dbgen` dal toolkit TPC-H, che consente di generare set di dati hello.  Si può scaricare il codice sorgente per `dbgen` da [strumenti TPC](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) e compilarlo oppure download hello compilato binario da [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).  Toogenerate file flat di 1 TB per i comandi di esecuzione dbgen.exe con seguenti hello `lineitem` tabella distribuito tra i 10 file:

  * `Dbgen -s 1000 -S **1** -C 10 -T L -v`
  * `Dbgen -s 1000 -S **2** -C 10 -T L -v`
  * …
  * `Dbgen -s 1000 -S **10** -C 10 -T L -v`

    Ora hello copia generati tooAzure file Blob.  Fare riferimento troppo[spostare tooand dati da un file system locale usando Azure Data Factory](data-factory-onprem-file-system-connector.md) come toodo che tramite Copia file ADF.    
* Azure SQL Data Warehouse: in questo esperimento i dati vengono caricati nell'istanza di Azure SQL Data Warehouse creata con 6000 DWU (Data Warehouse Units)

    Fare riferimento troppo[creare un Data Warehouse di SQL Azure](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) per istruzioni dettagliate su come toocreate SQL di un Data Warehouse del database.  tooget hello carico possibile ottenere prestazioni ottimali in SQL Data Warehouse tramite Polybase, si sceglie di numero massimo di Data Warehouse unità (Dwu) consentito nell'impostazione delle prestazioni di hello, che è 6.000 Dwu.

  > [!NOTE]
  > Durante il caricamento dal Blob di Azure, prestazioni di caricamento dati di hello sono direttamente proporzionale toohello numero Dwu configurare nei hello SQL Data Warehouse:
  >
  > Il caricamento di 1 TB in un'istanza di SQL Data Warehouse con 1.000 DWU richiede 87 minuti (alla velocità effettiva di circa 200 MBps) Il caricamento di 1 TB in un'istanza di SQL Data Warehouse con 2.000 DWU richiede 46 minuti (alla velocità effettiva di circa 380 MBps) Il caricamento di 1 TB in un'istanza di SQL Data Warehouse con 6.000 DWU richiede 14 minuti (alla velocità effettiva di circa 1,2 GBps)
  >
  >

    toocreate un SQL Data Warehouse con 6.000 Dwu, scorrimento hello prestazioni tutti hello modo toohello destra:

    ![Dispositivo di scorrimento delle prestazioni](media/data-factory-load-sql-data-warehouse/performance-slider.png)

    Se un database esistente non è configurato con 6000 DWU, è possibile aumentarne la capacità tramite il portale di Azure.  Esplorare database toohello nel portale di Azure ed è disponibile un **scala** pulsante hello **Panoramica** pannello mostrato nella seguente immagine hello:

    ![Pulsante Ridimensiona](media/data-factory-load-sql-data-warehouse/scale-button.png)    

    Fare clic su hello **scala** seguente di hello tooopen pulsante pannello, spostare il valore massimo toohello del dispositivo di scorrimento hello e fare clic su **salvare** pulsante.

    ![Finestra di dialogo Ridimensiona](media/data-factory-load-sql-data-warehouse/scale-dialog.png)

    In questo esperimento i dati vengono caricati in Azure SQL Data Warehouse mediante la classe di risorse `xlargerc`.

    esigenze di copia tooachieve migliori prestazioni possibili, toobe eseguita tramite un utente di SQL Data Warehouse appartenente troppo`xlargerc` classe di risorse.  Informazioni su come toodo che seguendo [un esempio di classe di risorse utente di modificare](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).  
* Creazione dello schema di tabella di destinazione nel database di Azure SQL Data Warehouse, eseguendo l'istruzione DDL hello:

    ```SQL  
    CREATE TABLE [dbo].[lineitem]
    (
        [L_ORDERKEY] [bigint] NOT NULL,
        [L_PARTKEY] [bigint] NOT NULL,
        [L_SUPPKEY] [bigint] NOT NULL,
        [L_LINENUMBER] [int] NOT NULL,
        [L_QUANTITY] [decimal](15, 2) NULL,
        [L_EXTENDEDPRICE] [decimal](15, 2) NULL,
        [L_DISCOUNT] [decimal](15, 2) NULL,
        [L_TAX] [decimal](15, 2) NULL,
        [L_RETURNFLAG] [char](1) NULL,
        [L_LINESTATUS] [char](1) NULL,
        [L_SHIPDATE] [date] NULL,
        [L_COMMITDATE] [date] NULL,
        [L_RECEIPTDATE] [date] NULL,
        [L_SHIPINSTRUCT] [char](25) NULL,
        [L_SHIPMODE] [char](10) NULL,
        [L_COMMENT] [varchar](44) NULL
    )
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    ```
Con passaggi preliminari hello completati, è ora sono attività di copia hello tooconfigure pronto utilizzando Copia guidata hello.

## <a name="launch-copy-wizard"></a>Avviare la Copia guidata
1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Fare clic su **+ nuovo** dall'angolo superiore sinistro di hello, fare clic su **Intelligence + analitica**, fare clic su **Data Factory**.
3. In hello **nuova data factory** pannello:

   1. Immettere **LoadIntoSQLDWDataFactory** per hello **nome**.
       nome Hello di hello Azure data factory deve essere globalmente univoco. Se viene visualizzato l'errore hello: **"LoadIntoSQLDWDataFactory" nome della Data factory non è disponibile**, modificare il nome di hello di hello data factory (ad esempio, yournameLoadIntoSQLDWDataFactory) e provare a creare di nuovo. Per informazioni sulle regole di denominazione per gli elementi di Data factory, vedere l'argomento relativo alle [regole di denominazione di Data factory](data-factory-naming-rules.md) .  
   2. Selezionare la **sottoscrizione**di Azure.
   3. Per il gruppo di risorse, effettuare una delle hello alla procedura seguente:
      1. Selezionare **utilizzare esistente** tooselect un gruppo di risorse esistente.
      2. Selezionare **Crea nuovo** tooenter un nome per un gruppo di risorse.
   4. Selezionare un **percorso** per data factory di hello.
   5. Selezionare **toodashboard Pin** casella di controllo nella parte inferiore di hello del pannello hello.  
   6. Fare clic su **Crea**.
4. Una volta completata la creazione di hello, vedrai hello **Data Factory** pannello, come illustrato nella seguente immagine hello:

   ![Home page di Data factory](media/data-factory-load-sql-data-warehouse/data-factory-home-page-copy-data.png)
5. Nella home page di hello Data Factory, fare clic su hello **copiare dati** riquadro toolaunch **Copia guidata**.

   > [!NOTE]
   > Se viene visualizzato il browser web hello è bloccata su "Autorizzazione …", disabilitare o deselezionare **bloccare i cookie di terze parti e i dati del sito** (oppure) mantenere abilitato e creare un'eccezione per **login.microsoftonline.com**e quindi provare ad avviare la procedura guidata hello nuovamente.
   >
   >

## <a name="step-1-configure-data-loading-schedule"></a>Passaggio 1: Configurare una pianificazione di caricamento dei dati
primo passaggio Hello è dati hello tooconfigure durante il caricamento di pianificazione.  

In hello **proprietà** pagina:

1. Immettere **CopyFromBlobToAzureSqlDataWarehouse** per **Nome attività**
2. Selezionare l'opzione **Esegui una volta**.   
3. Fare clic su **Avanti**.  

    ![Copia guidata: pagina delle proprietà](media/data-factory-load-sql-data-warehouse/copy-wizard-properties-page.png)

## <a name="step-2-configure-source"></a>Passaggio 2: Configurare l'origine
Questa sezione è illustrato hello origine hello tooconfigure di passaggi: Blob di Azure contenente hello 1 TB TPC-file voce H.

1. Seleziona hello **archiviazione Blob di Azure** come dati hello, fare clic su **Avanti**.

    ![Copia guidata: selezionare la pagina di origine](media/data-factory-load-sql-data-warehouse/select-source-connection.png)

2. Immettere informazioni di connessione hello per hello account di archiviazione Blob di Azure, quindi fare clic su **Avanti**.

    ![Copia guidata: informazioni sulla connessione di origine](media/data-factory-load-sql-data-warehouse/source-connection-info.png)

3. Scegliere hello **cartella** riga hello TPC-H contenente i file di elemento e fare clic su **Avanti**.

    ![Copia guidata: selezionare la cartella di input](media/data-factory-load-sql-data-warehouse/select-input-folder.png)

4. Fare clic su **Avanti**, impostazioni di formato di file hello vengono rilevate automaticamente.  Verificare che il delimitatore di colonna sia toomake ' | 'anziché una virgola predefinito hello','.  Fare clic su **Avanti** dopo avere visualizzata in anteprima i dati di hello.

    ![Copia guidata: impostazioni di formattazione file](media/data-factory-load-sql-data-warehouse/file-format-settings.png)

## <a name="step-3-configure-destination"></a>Passaggio 3: Configurare la destinazione
In questa sezione viene illustrato come tooconfigure hello destinazione: `lineitem` tabella nel database di hello Azure SQL Data Warehouse.

1. Scegliere **Azure SQL Data Warehouse** come destinazione di hello, fare clic su **Avanti**.

    ![Copia guidata: selezionare l'archivio dati di destinazione](media/data-factory-load-sql-data-warehouse/select-destination-data-store.png)

2. Inserire informazioni di connessione hello per Azure SQL Data Warehouse.  Assicurarsi di specificare l'utente hello che è un membro del ruolo hello `xlargerc` (vedere hello **prerequisiti** sezione per informazioni dettagliate), fare clic su **Avanti**.

    ![Copia guidata: informazioni sulla connessione di destinazione](media/data-factory-load-sql-data-warehouse/destination-connection-info.png)

3. Scegliere la tabella di destinazione hello e fare clic su **Avanti**.

    ![Copia guidata: pagina del mapping della tabella](media/data-factory-load-sql-data-warehouse/table-mapping-page.png)

4. Nella pagina Mapping dello schema, lasciare deselezionata l'opzione "Apply column mapping" (Applica mapping di colonne) e fare clic su **Avanti**.

## <a name="step-4-performance-settings"></a>Passaggio 4: Impostazioni relative alle prestazioni

L'opzione **Allow polybase** (Consenti Polybase) è selezionata per impostazione predefinita.  Fare clic su **Avanti**.

![Copia guidata: pagina del mapping dello schema](media/data-factory-load-sql-data-warehouse/performance-settings-page.png)

## <a name="step-5-deploy-and-monitor-load-results"></a>Passaggio 5: Distribuire e monitorare i risultati del caricamento
1. Fare clic su **fine** toodeploy pulsante.

    ![Copia guidata: pagina di riepilogo](media/data-factory-load-sql-data-warehouse/summary-page.png)

2. Una volta completata la distribuzione di hello, fare clic su `Click here toomonitor copy pipeline` copia hello toomonitor avanzamento dell'esecuzione. Pipeline copia selezionare hello è stato creato in hello **attività Windows** elenco.

    ![Copia guidata: pagina di riepilogo](media/data-factory-load-sql-data-warehouse/select-pipeline-monitor-manage-app.png)

    È possibile visualizzare i dettagli di esecuzione in hello copia di hello **attività finestra Esplora** nel riquadro di destra hello, compresi hello volume di dati letti dall'origine e scritti nella destinazione, la durata e velocità effettiva Media di hello per hello eseguire.

    Come si può vedere dal hello seguente cattura di schermata e la copia di 1 TB da archiviazione Blob di Azure in SQL Data Warehouse ha impiegato 14 minuti, in modo efficace una velocità effettiva di GBps 1.22!

    ![Copia guidata: finestra di dialogo operazione completata](media/data-factory-load-sql-data-warehouse/succeeded-info.png)

## <a name="best-practices"></a>Procedure consigliate
Di seguito sono elencate alcune procedure consigliate per l'esecuzione del database di Azure SQL Data Warehouse:

* Usare una classe di risorse di dimensioni maggiori durante il caricamento in un INDICE COLUMNSTORE CLUSTER.
* Per join più efficienti, è consigliabile usare la distribuzione hash da una colonna di selezione anziché la distribuzione round robin predefinita.
* Per una maggiore velocità di carico, è consigliabile usare un heap per i dati temporanei.
* Creare statistiche al termine del caricamento di Azure SQL Data Warehouse.

Per informazioni dettagliate, vedere [Procedure consigliate per Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).

## <a name="next-steps"></a>Passaggi successivi
* [Data Factory Copia guidata](data-factory-copy-wizard.md) -questo articolo fornisce informazioni dettagliate sulla copia guidata hello.
* [Copiare l'attività manuale sulle prestazioni e ottimizzazione](data-factory-copy-activity-performance.md) -questo articolo sono contenute le misurazioni delle prestazioni di riferimento hello e Guida all'ottimizzazione.
