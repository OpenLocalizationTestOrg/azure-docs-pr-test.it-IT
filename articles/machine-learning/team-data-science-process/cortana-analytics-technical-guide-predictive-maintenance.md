---
title: Manutenzione predittiva nel settore aerospaziale con Azure - Guida tecnica alla soluzione Cortana Intelligence | Documentazione Microsoft
description: Guida tecnica del modello di soluzione con Microsoft Cortana Intelligence per la manutenzione predittiva nel settore aerospaziale, nei servizi pubblici e nei trasporti.
services: cortana-analytics
documentationcenter: 
author: fboylu
manager: jhubbard
editor: cgronlun
ms.assetid: 2c4d2147-0f05-4705-8748-9527c2c1f033
ms.service: cortana-analytics
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: fboylu
ms.openlocfilehash: 080618b844669cbea29a6a48c32e937705b06e3f
ms.sourcegitcommit: f847fcbf7f89405c1e2d327702cbd3f2399c4bc2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2017
---
# <a name="technical-guide-to-the-cortana-intelligence-solution-template-for-predictive-maintenance-in-aerospace-and-other-businesses"></a>Guida tecnica del modello di soluzione Cortana Intelligence per la manutenzione predittiva nel settore aerospaziale e in altri campi

>[!Important]
Questo articolo è stato deprecato. Le informazioni trattate sulla manutenzione predittiva nel settore aerospaziale sono ancora pertinenti, ma per informazioni aggiornate vedere [Solution Overview for Business Audiences](https://github.com/Azure/cortana-intelligence-predictive-maintenance-aerospace) (Panoramica della soluzione per destinatari aziendali).


I modelli di soluzione sono progettati per accelerare il processo di creazione di una demo end-to-end basata su Cortana Intelligence Suite. Un modello distribuito esegue il provisioning della sottoscrizione con i componenti necessari di Cortana Intelligence e quindi crea le relative relazioni interne. Esegue anche il seeding della pipeline di dati con dati di esempio generati da un'applicazione di generazione dati, da scaricare e installare nel computer locale dopo aver distribuito il modello di soluzione. I dati generati idratano la pipeline di dati e avviano la creazione di stime di Machine Learning che possono essere poi visualizzate nel dashboard di Power BI.

Il processo di distribuzione prevede diversi passaggi per l'impostazione delle credenziali della soluzione. Assicurarsi di prendere nota delle credenziali, ad esempio il nome della soluzione, il nome utente e la password forniti durante la distribuzione. 


Gli obiettivi di questo articolo sono:
- Descrivere l'architettura di riferimento e i componenti sottoposti a provisioning nella sottoscrizione.
- Dimostrare come sostituire i dati di esempio con dati propri. 
- Illustrare come modificare il modello di soluzione.  

> [!TIP]
> È possibile scaricare e stampare una [versione in formato PDF di questo articolo](http://download.microsoft.com/download/F/4/D/F4D7D208-D080-42ED-8813-6030D23329E9/cortana-analytics-technical-guide-predictive-maintenance.pdf).
> 
> 

## <a name="overview"></a>Panoramica
![Architettura di manutenzione predittiva](./media/cortana-analytics-technical-guide-predictive-maintenance/predictive-maintenance-architecture.png)

La distribuzione della soluzione comporta l'attivazione dei servizi di Azure nell'ambito di Cortana Analytics Suite (inclusi Hub eventi, Analisi di flusso, HDInsight, Data Factory e Machine Learning). Il diagramma dell'architettura mostra come costruire il modello di soluzione per la manutenzione predittiva nel settore aerospaziale. È possibile esaminare i servizi nel portale di Azure facendo clic su di essi nel diagramma del modello di soluzione creato con la distribuzione della soluzione, ad eccezione di HDInsight, di cui viene effettuato il provisioning su richiesta quando le attività della pipeline correlate devono essere eseguite e successivamente eliminate.
Scaricare una [versione completa del diagramma](http://download.microsoft.com/download/1/9/B/19B815F0-D1B0-4F67-AED3-A40544225FD1/ca-topologies-maintenance-prediction.png).

Le sezioni seguenti descrivono le parti della soluzione.

## <a name="data-source-and-ingestion"></a>Origine dati e inserimento
### <a name="synthetic-data-source"></a>Origine dati sintetica
L'origine dati usata per questo modello viene generata da un'applicazione desktop da scaricare ed eseguire localmente al termine della distribuzione.

Per trovare le istruzioni per il download e l'installazione di questa applicazione, selezionare il primo nodo denominato Predictive Maintenance Data Generator nel diagramma del modello di soluzione. Le istruzioni sono disponibili nella barra delle proprietà. Questa applicazione invia al servizio [Hub eventi di Azure](#azure-event-hub) punti dati, o eventi, che vengono usati nel flusso della soluzione. L'origine dati è derivata da dati disponibili pubblicamente nel [repository dei dati della NASA](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/) usando il [Turbofan Engine Degradation Simulation Data Set](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/#turbofan).

L'applicazione di generazione eventi popola l'Hub eventi di Azure solo quando è in esecuzione nel computer.

### <a name="azure-event-hub"></a>Hub eventi di Azure
Il servizio [Hub eventi di Azure](https://azure.microsoft.com/services/event-hubs/) è il destinatario dell'input fornito dall'origine dati sintetica.

## <a name="data-preparation-and-analysis"></a>Preparazione e analisi dei dati
### <a name="azure-stream-analytics"></a>Analisi di flusso di Azure
Usare [Analisi di flusso di Azure](https://azure.microsoft.com/services/stream-analytics/) per fornire dati di analisi in tempo quasi reale sul flusso di input dal servizio [Hub eventi di Azure](#azure-event-hub). È quindi possibile pubblicare i risultati in un dashboard di [Power BI](https://powerbi.microsoft.com), nonché archiviare tutti gli eventi in ingresso non elaborati nel servizio [Archiviazione di Azure](https://azure.microsoft.com/services/storage/) per l'elaborazione successiva con il servizio [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/).

### <a name="hdinsight-custom-aggregation"></a>Aggregazione personalizzata di HDInsight
Tramite HDInsight eseguire script [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) orchestrati da Azure Data Factory per aggregare eventi non elaborati archiviati usando il servizio Analisi di flusso di Azure.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Eseguire stime sulla vita utile rimanente di un determinato motore di aereo in base agli input ricevuti mediante il servizio [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) (orchestrato da Azure Data Factory). 

## <a name="data-publishing"></a>Pubblicazione dei dati
### <a name="azure-sql-database"></a>Database SQL di Azure
Usare [database SQL di Azure](https://azure.microsoft.com/services/sql-database/) per archiviare le stime ricevute dal servizio Azure Machine Learning che vengono poi usate nel dashboard di [Power BI](https://powerbi.microsoft.com).

## <a name="data-consumption"></a>Utilizzo dei dati
### <a name="power-bi"></a>Power BI
Usare [Power BI](https://powerbi.microsoft.com) per visualizzare un dashboard contenente le aggregazioni e gli avvisi forniti da [Analisi di flusso di Azure](https://azure.microsoft.com/services/stream-analytics/), oltre alle stime sulla vita utile rimanente archiviate nel [database SQL di Azure](https://azure.microsoft.com/services/sql-database/) e prodotte con [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/).

## <a name="how-to-bring-in-your-own-data"></a>Come inserire i propri dati
Questa sezione descrive come inserire i propri dati in Azure e quali aree è necessario modificare per i dati inseriti in questa architettura.

È poco probabile che i set di dati personali corrispondano al set di dati [Turbofan Engine Degradation Simulation Data Set](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/#turbofan) usato per questo modello di soluzione. Per poter adattare questo modello ai propri dati è fondamentale comprendere i dati e i requisiti. 

Le sezioni seguenti illustrano le parti del modello che è necessario modificare quando viene introdotto un nuovo set di dati.

### <a name="azure-event-hub"></a>Hub eventi di Azure
Il servizio Hub eventi di Azure è generico e accetta l'invio di dati in formato CSV o JSON. In Hub eventi di Azure non viene eseguita alcuna elaborazione speciale, ma è importante comprendere i dati inseriti.

Questo documento non descrive come inserire i dati, ma è possibile inviare facilmente eventi o dati a un hub eventi di Azure usando l'API di Hub eventi.

### <a name="azure-stream-analytics"></a>Analisi di flusso di Azure
Usare il servizio Analisi di flusso di Azure per fornire l'analisi quasi in tempo reale tramite la lettura dai flussi di dati e l'output dei dati in un numero qualsiasi di origini.

Per il modello di soluzione per la manutenzione predittiva nel settore aerospaziale, la query di Analisi di flusso di Azure è costituita da quattro sottoquery che usano eventi provenienti dal servizio Hub eventi di Azure e inviano l'output a quattro posizioni distinte. L'output è costituito da tre set di dati di Power BI e una posizione di archiviazione di Azure.

Per trovare la query di Analisi di flusso di Azure:

* Connettersi al portale di Azure
* Individuare i processi di Analisi di flusso ![Icona di Analisi di flusso](./media/cortana-analytics-technical-guide-predictive-maintenance/icon-stream-analytics.png) generati quando è stata distribuita la soluzione, *ad esempio*, **maintenancesa02asapbi** e **maintenancesa02asablob** per la soluzione di analisi predittiva
* Selezionare:
  
  * ***INPUT*** per visualizzare l'input della query.
  * ***QUERY*** per visualizzare la query stessa.
  * ***OUTPUT*** per visualizzare i vari output.

Per informazioni sulla costruzione di query in Analisi di flusso di Azure, vedere l'articolo di [riferimento sulle query di Analisi di flusso](https://msdn.microsoft.com/library/azure/dn834998.aspx) in MSDN.

In questa soluzione le query restituiscono tre set di dati con informazioni di analisi quasi in tempo reale sul flusso di dati in ingresso in un dashboard di Power BI fornito con questo modello di soluzione. Dal momento che la conoscenza del formato dei dati in ingresso è implicita, queste query devono essere modificate in base al formato dei propri dati.

La query nel secondo processo di analisi di flusso, **maintenancesa02asablob**, restituisce semplicemente tutti gli eventi di [Hub eventi](https://azure.microsoft.com/services/event-hubs/) ad [Archiviazione di Azure](https://azure.microsoft.com/services/storage/). Non richiede quindi alcuna modifica, indipendentemente dal formato dei dati, dal momento che le informazioni complete sull'evento vengono trasmesse all'archiviazione.

### <a name="azure-data-factory"></a>Data factory di Azure
Il servizio [Data factory di Azure](https://azure.microsoft.com/documentation/services/data-factory/) orchestra lo spostamento e l'elaborazione dei dati. Nel modello di soluzione per la manutenzione predittiva nel settore aerospaziale la data factory è costituita da tre [pipeline](../../data-factory/v1/data-factory-create-pipelines.md) che spostano ed elaborano i dati facendo uso di varie tecnologie.  Per accedere alla data factory, aprire il nodo Data factory nella parte inferiore del diagramma del modello di soluzione creato con la distribuzione della soluzione. Eventuali errori presenti nei set di dati sono dovuti al fatto che la data factory è stata distribuita prima dell'avvio del generatore di dati. Questi errori possono essere ignorati in quanto non impediscono il funzionamento della data factory.

![Errori di set di dati di Data Factory](./media/cortana-analytics-technical-guide-predictive-maintenance/data-factory-dataset-error.png)

Questa sezione illustra le [pipeline](../../data-factory/v1/data-factory-create-pipelines.md) e le [attività](../../data-factory/v1/data-factory-create-pipelines.md) necessarie contenute in [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/). Di seguito è riportata la vista diagramma della soluzione.

![Data factory di Azure](./media/cortana-analytics-technical-guide-predictive-maintenance/azure-data-factory.png)

Due delle pipeline di questa data factory contengono script [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) usati per partizionare e aggregare i dati. Se specificato, gli script vengono inseriti nell'account di [archiviazione di Azure](https://azure.microsoft.com/services/storage/) creato durante l'installazione. Il percorso è: maintenancesascript\\\\script\\\\hive\\\\ (o https://[nome della soluzione].blob.core.windows.net/maintenancesascript).

Come le query di [Analisi di flusso di Azure](#azure-stream-analytics-1), gli script [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) hanno una conoscenza implicita del formato dei dati in ingresso. Sarà quindi necessario modificare queste query in base al formato dei dati.

#### <a name="aggregateflightinfopipeline"></a>*AggregateFlightInfoPipeline*
Questa [pipeline](../../data-factory/v1/data-factory-create-pipelines.md) contiene un'unica attività [HDInsightHive](../../data-factory/v1/data-factory-hive-activity.md), che usa un servizio [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) che esegue uno script [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) per partizionare i dati inseriti in [Archiviazione di Azure](https://azure.microsoft.com/services/storage/) durante il processo di [Analisi di flusso di Azure](https://azure.microsoft.com/services/stream-analytics/).

Lo script [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) per questa attività di partizionamento è ***AggregateFlightInfo.hql***.

#### <a name="mlscoringpipeline"></a>*MLScoringPipeline*
Questa [pipeline](../../data-factory/v1/data-factory-create-pipelines.md) contiene diverse attività il cui risultato finale è costituito dalle stime con punteggio provenienti dall'esperimento di [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) associato a questo modello di soluzione.

Le attività incluse sono:

* L'attività [HDInsightHive](../../data-factory/v1/data-factory-hive-activity.md), che usa un servizio [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) che esegue uno script [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) per le operazioni necessarie di aggregazione e progettazione delle funzioni per l'esperimento di [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/).
  Lo script [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) per questa attività di partizionamento è ***PrepareMLInput.hql***.
* L'attività [Copy](https://msdn.microsoft.com/library/azure/dn835035.aspx), che sposta i risultati dall'attività [HDInsightHive](../../data-factory/v1/data-factory-hive-activity.md) a un unico BLOB di [Archiviazione di Azure](https://msdn.microsoft.com/library/azure/dn894009.aspx) accessibile dall'attività [AzureMLBatchScoring](https://azure.microsoft.com/services/storage/).
* L'attività [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx), che chiama l'esperimento di [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) con i risultati inseriti in un unico BLOB di [Archiviazione di Azure](https://azure.microsoft.com/services/storage/).

#### <a name="copyscoredresultpipeline"></a>*CopyScoredResultPipeline*
Questa [pipeline](../../data-factory/v1/data-factory-create-pipelines.md) contiene un'unica attività [Copy](https://msdn.microsoft.com/library/azure/dn835035.aspx) che sposta i risultati dell'esperimento di [Azure Machine Learning](#azure-machine-learning) da ***MLScoringPipeline*** al [database SQL di Azure](https://azure.microsoft.com/services/sql-database/) di cui è stato effettuato il provisioning durante l'installazione del modello di soluzione.

### <a name="azure-machine-learning"></a>Azure Machine Learning
L'esperimento di [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) usato per questo modello di soluzione fornisce la vita utile rimanente di un motore di aereo. L'esperimento è specifico per il set di dati usato. Per l'uso con dati propri deve essere modificato o sostituito in base alle specifiche dei dati inseriti.

Per informazioni su come è stato creato l'esperimento di Azure Machine Learning, vedere l'articolo relativo alla [manutenzione predittiva: passaggio 1 di 3, preparazione dei dati e progettazione delle funzioni](http://gallery.cortanaanalytics.com/Experiment/Predictive-Maintenance-Step-1-of-3-data-preparation-and-feature-engineering-2).

## <a name="monitor-progress"></a>Monitorare lo stato
Dopo aver avviato il generatore di dati, la pipeline inizia a disidratarsi e i diversi componenti della soluzione cominciano ad avviarsi in base ai comandi inviati da Data factory. Esistono due modi per monitorare la pipeline.

1. Uno dei processi di Analisi di flusso scrive i dati in ingresso non elaborati nell'archivio BLOB. Se si fa clic sul componente Archiviazione BLOB della soluzione dalla schermata in cui è stata distribuita la soluzione e si fa clic su Apri nel pannello di destra, verrà visualizzato il [portale di Azure](https://portal.azure.com/). Una volta nel portale, fare clic su BLOB. Nel pannello successivo viene visualizzato un elenco di contenitori. Fare clic su **maintenancesadata**. Nel pannello successivo viene visualizzata la cartella **rawdata**. All'interno della cartella rawdata sono presenti cartelle con nomi quali hour=17 e hour=18. La presenza di queste cartelle indica che i dati non elaborati sono stati generati nel computer e archiviati nell'archivio BLOB. Verranno visualizzati file con estensione csv che in tali cartelle hanno dimensioni limitate in MB.
2. L'ultimo passaggio della pipeline consiste nella scrittura di dati, ad esempio stime da Machine Learning, nel database SQL. Possono essere necessarie al massimo tre ore prima che i dati siano visibili nel database SQL. È possibile monitorare la quantità di dati disponibile nel database SQL usando il [portale di Azure](https://portal.azure.com/). Nel pannello di sinistra trovare DATABASE SQL![Icona SQL](./media/cortana-analytics-technical-guide-predictive-maintenance/icon-SQL-databases.png) e fare clic su questa voce. Individuare quindi il database **pmaintenancedb** e fare clic su di esso. Fare clic su GESTISCI nella parte inferiore della pagina successiva.
   
    ![Icona Gestisci](./media/cortana-analytics-technical-guide-predictive-maintenance/icon-manage.png).
   
    A questo punto fare clic su Nuova query ed eseguire una query per il numero di righe (ad esempio, select count(*) from PMResult). Man mano che il database cresce, il numero di righe nella tabella dovrebbe aumentare.

## <a name="power-bi-dashboard"></a>dashboard di Power BI

Configurare il dashboard di Power BI per visualizzare i dati provenienti da Analisi di flusso di Azure (percorso critico), nonché i risultati della stima in batch provenienti da Azure Machine Learning (percorso non critico).

### <a name="set-up-the-cold-path-dashboard"></a>Configurare il dashboard per il percorso non critico
Nella pipeline di dati del percorso non critico l'obiettivo è ottenere la stima della vita utile rimanente di ogni motore di aereo al termine di un volo (ciclo). Il risultato viene aggiornato ogni 3 ore per eseguire la stima su motori di aereo che hanno terminato un volo nelle 3 ore precedenti.

Power BI si connette a un database SQL di Azure come origine dati, in cui sono archiviati i risultati della stima. Si noti che quando si distribuisce la soluzione, viene visualizzata una stima nel database entro 3 ore.
Il file PBIX fornito con il download del generatore contiene alcuni dati di seeding che permettono di creare il dashboard di Power BI fin da subito. Si noti anche che in questo passaggio il download e l'installazione del software gratuito [Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)sono un prerequisito.

La procedura seguente illustra come connettere il file con estensione pbix al database SQL riattivato al momento della distribuzione della soluzione che contiene i dati per la visualizzazione, ad esempio i risultati della stima.

1. Ottenere le credenziali del database.
   
   Prima di procedere con i passaggi successivi, è necessario ottenere **il nome del server di database, il nome del database, il nome utente e la password** . I passaggi per ottenerli sono riportati di seguito.
   
   * Quando la voce **Database SQL di Azure** nel diagramma del modello di soluzione diventa verde, selezionarla e quindi fare clic su **Apri**.
   * Verrà aperta una nuova scheda o finestra del browser con la pagina del portale di Azure. Fare clic su **Gruppi di risorse** nel pannello di sinistra.
   * Selezionare la sottoscrizione usata per la distribuzione della soluzione e quindi **NomeSoluzione\_GruppoDiRisorse**.
   * Nel nuovo pannello a comparsa fare clic sull'icona ![Icona SQL](./media/cortana-analytics-technical-guide-predictive-maintenance/icon-sql.png) per accedere al database. Il nome del database si trova accanto a questa icona, ad esempio **'pmaintenancedb'**, mentre il **nome del server di database** è riportato nella proprietà Nome server ed è simile a **NomeSoluzione.database.windows.net**.
   * Il **nome utente** e la **password** del database sono quelli registrati prima durante la distribuzione della soluzione.
2. Aggiornare l'origine dati del file di report del percorso non critico con Power BI Desktop.
   
   * Nella cartella in cui è stato scaricato e decompresso il file del generatore fare doppio clic sul file **PowerBI\\PredictiveMaintenanceAerospace.pbix**. Ignorare gli eventuali messaggi di avviso visualizzati all'apertura del file. All'inizio del file fare clic su **Modifica query**.
     
     ![Modifica query](./media/cortana-analytics-technical-guide-predictive-maintenance/edit-queries.png)
   * Verranno visualizzate due tabelle, **RemainingUsefulLife** e **PMResult**. Selezionare la prima tabella e fare clic su ![Icona di impostazione query](./media/cortana-analytics-technical-guide-predictive-maintenance/icon-query-settings.png) accanto a **'Origine'** in **'PASSAGGI APPLICATI'** nel pannello **'Impostazioni query'** a destra. Ignorare gli eventuali messaggi di avviso visualizzati.
   * Nella finestra popup sostituire **Server** e **Database** con i nomi del server e del database usati e quindi fare clic su **OK**. Per il nome del server, assicurarsi di specificare la porta 1433:**NomeSoluzione.database.windows.net, 1433**. Lasciare inalterato il campo relativo al database: **pmaintenancedb**. Ignorare i messaggi di avviso visualizzati sullo schermo.
   * Nella finestra popup successiva sono disponibili due opzioni nel pannello di sinistra, **Windows** e **Database**. Fare clic su **Database** e inserire il proprio **nome utente** e **password**, ovvero il nome utente e la password immessi al momento della prima distribuzione della soluzione e della creazione del database SQL di Azure. In ***Selezionare il livello a cui applicare queste impostazioni*** selezionare l'opzione relativa al livello di database. Fare clic su **Connetti**.
   * Fare clic sulla seconda tabella **PMResult** e quindi su ![Icona navigazione](./media/cortana-analytics-technical-guide-predictive-maintenance/icon-navigation.png) accanto a **'Origine'** in **'PASSAGGI APPLICATI'** nel pannello **'Impostazioni query'** a destra, aggiornare i nomi del server e del database come descritto nei passaggi precedenti e quindi fare clic su OK.
   * Quando viene di nuovo visualizzata la pagina precedente, chiudere la finestra. Viene visualizzato il messaggio "Fare clic **Applica**". Infine, fare clic sul pulsante **Salva** per salvare le modifiche apportate. Il file di Power BI è ora connesso al server. Se le visualizzazioni sono vuote, assicurarsi di annullare le selezioni per visualizzare tutti i dati facendo clic sull'icona della gomma nell'angolo superiore destro della legenda. Usare il pulsante Aggiorna per aggiornare le visualizzazioni con i nuovi dati. Inizialmente le visualizzazioni contengono solo i dati di seeding, perché l'aggiornamento della data factory è pianificato ogni 3 ore. Dopo 3 ore, aggiornando i dati nelle visualizzazioni saranno disponibili le nuove stime.
3. (Facoltativo) Pubblicare il dashboard per il percorso non critico in [Power BI online](http://www.powerbi.com/). Si noti che per questo passaggio è necessario un account Power BI o Office 365.
   
   * Fare clic su **Pubblica** . Dopo alcuni secondi viene visualizzato un messaggio di conferma della pubblicazione in Power BI con un segno di spunta verde. Fare clic sul collegamento sotto "Apri PredictiveMaintenanceAerospace.pbix in Power BI". Per istruzioni dettagliate, vedere [Pubblicare da Power BI Desktop](https://support.powerbi.com/knowledgebase/articles/461278-publish-from-power-bi-desktop).
   * Per creare un nuovo dashboard, fare clic sul segno **+** accanto alla sezione **Dashboard** nel riquadro di sinistra. Immettere il nome "Predictive Maintenance Demo" per il nuovo dashboard.
   * Dopo aver aperto il report, fare clic su ![Icona AGGIUNGI](./media/cortana-analytics-technical-guide-predictive-maintenance/icon-pin.png) per aggiungere tutte le visualizzazioni al dashboard. Per istruzioni dettagliate, vedere [Aggiungere un riquadro a un dashboard di Power BI da un report](https://support.powerbi.com/knowledgebase/articles/430323-pin-a-tile-to-a-power-bi-dashboard-from-a-report).
     Passare alla pagina del dashboard, regolare le dimensioni e la posizione delle visualizzazioni e modificarne i titoli. Per istruzioni dettagliate su come modificare i riquadri, vedere [Modificare un riquadro: ridimensionare, spostare, rinominare, aggiungere ed eliminare un collegamento ipertestuale](https://powerbi.microsoft.com/documentation/powerbi-service-edit-a-tile-in-a-dashboard/#rename). Di seguito è riportato un dashboard di esempio a cui sono state aggiunte alcune visualizzazioni del percorso non critico.  A seconda del tempo di esecuzione del generatore di dati, i numeri nelle visualizzazioni possono variare.
     <br/>
     ![Visualizzazione finale](./media/cortana-analytics-technical-guide-predictive-maintenance/final-view.png)
     <br/>
   * Per pianificare l'aggiornamento dei dati, passare il puntatore del mouse sul set di dati **PredictiveMaintenanceAerospace**, fare clic su ![Icona con i punti di sospensione](./media/cortana-analytics-technical-guide-predictive-maintenance/icon-elipsis.png) e quindi scegliere **Pianifica aggiornamenti**.
     <br/>
     **Nota**: se viene visualizzato un messaggio di avviso, fare clic su **Modifica credenziali** e verificare che le credenziali del database siano identiche a quelle illustrate nel passaggio 1.
     <br/>
     ![Pianifica aggiornamenti](./media/cortana-analytics-technical-guide-predictive-maintenance/schedule-refresh.png)
     <br/>
   * Espandere la sezione **Pianifica aggiornamento** . Attivare l'opzione "Mantieni aggiornati i dati".
     <br/>
   * Pianificare l'aggiornamento in base alle esigenze. Per altre informazioni, vedere [Aggiornamento dei dati in Power BI](https://support.powerbi.com/knowledgebase/articles/474669-data-refresh-in-power-bi).

### <a name="setup-hot-path-dashboard"></a>Configurare il dashboard per il percorso critico
La procedura seguente mostra come visualizzare l'output dei dati da processi di Analisi di flusso generati al momento della distribuzione della soluzione. Per eseguire la procedura è necessario un account di [Power BI online](http://www.powerbi.com/) . Se non si ha un account, [crearne uno](https://powerbi.microsoft.com/pricing).

1. Aggiungere l'output di Power BI ad Analisi di flusso di Azure.
   
   * Per configurare l'output del processo di Analisi di flusso di Azure come dashboard di Power BI, è necessario seguire le istruzioni riportate in [Analisi di flusso e Power BI: dashboard di analisi in tempo reale per lo streaming dei dati](../../stream-analytics/stream-analytics-power-bi-dashboard.md).
   * Alla query di Analisi di flusso di Azure sono associati tre output: **aircraftmonitor**, **aircraftalert** e **flightsbyhour**. È possibile visualizzare la query facendo clic sulla scheda corrispondente. In corrispondenza di ognuna delle tabelle è necessario aggiungere un output alla query di Analisi di flusso di Azure. Quando si aggiunge il primo output (**aircraftmonitor**), verificare che i valori di **Alias di output**, **Nome del set di dati** e **Nome tabella** corrispondano (**aircraftmonitor**). Seguire la stessa procedura per aggiungere gli output relativi a **aircraftalert** e **flightsbyhour**. Dopo aver aggiunto le tre tabelle di output e aver avviato il processo di Analisi di flusso di Azure, viene visualizzato un messaggio di conferma (ad esempio, "L'avvio del processo di Analisi di flusso maintenancesa02asapbi è stato completato").
2. Accedere a [Power BI online](http://www.powerbi.com)
   
   * Nel riquadro di sinistra della sezione Set di dati in Area di lavoro personale vengono visualizzati i nomi ***DATASET*** **aircraftmonitor**, **aircraftalert** e **flightsbyhour**. Si tratta dei dati di flusso di cui si è eseguito il push da Analisi di flusso di Azure nel passaggio precedente. Il set di dati **flightsbyhour** potrebbe non essere visualizzato contemporaneamente agli altri due set di dati a causa della natura della query SQL sottostante. Verrà tuttavia visualizzato dopo un'ora.
   * Assicurarsi che il riquadro ***Visualizzazioni*** sia aperto e visualizzato sul lato destro dello schermo.
3. Dopo aver ottenuto il flusso dati in Power BI, è possibile iniziare a visualizzare i dati di streaming. Di seguito è riportato un dashboard di esempio a cui sono state aggiunte alcune visualizzazioni del percorso critico. È possibile creare altri riquadri del dashboard in base a set di dati appropriati. A seconda del tempo di esecuzione del generatore di dati, i numeri nelle visualizzazioni possono variare.

    ![Visualizzazione dashboard](media\cortana-analytics-technical-guide-predictive-maintenance\dashboard-view.png)

1. Di seguito sono elencati alcuni passaggi per creare uno dei riquadri sopra riportati, "Fleet View of Sensor 11 vs. Threshold 48.26":
   
   * Fare clic sul set di dati **aircraftmonitor** nella sezione Set di dati del pannello di sinistra.
   * Fare clic sull'icona **Grafico a linee** .
   * Fare clic su **Elaborati** nel riquadro **Campi** in modo che venga visualizzato nell'area "Asse" nel riquadro **Visualizzazioni**.
   * Fare clic su "s11" e "s11\_alert" in modo che entrambi vengano visualizzati in "Valori". Fare clic sulla piccola freccia accanto a **s11** e **s11\_alert** e sostituire "Somma" con "Media".
   * Fare clic su **SALVA** nella parte superiore e denominare il report "aircraftmonitor". Il report "aircraftmonitor" viene visualizzato nella sezione **Report** del riquadro **Strumento di navigazione** a sinistra.
   * Fare clic sull'icona **Aggiungi oggetto visivo** nell'angolo superiore destro di questo grafico a linee. Potrebbe essere visualizzata una finestra "Aggiungi al dashboard" che permette di scegliere un dashboard. Selezionare "Predictive Maintenance Demo" e quindi fare clic su "Aggiungi".
   * Passare il puntatore del mouse su questo riquadro nel dashboard e fare clic sull'icona "Modifica" nell'angolo superiore destro per modificarne il titolo in "Fleet View of Sensor 11 vs. Threshold 48.26" e il sottotitolo in "Average across fleet over time".

## <a name="delete-your-solution"></a>Eliminare la soluzione
Assicurarsi di arrestare il generatore di dati quando non lo si usa in modo attivo, perché l'esecuzione di questa applicazione può comportare costi elevati. Se non la si usa, è consigliabile eliminarla. Con l'eliminazione di questa soluzione vengono eliminati anche tutti i componenti di cui è stato eseguito il provisioning nella sottoscrizione durante la procedura di distribuzione. Per eliminare la soluzione, fare clic sul nome della soluzione nel riquadro sinistro del modello e quindi fare clic su **Elimina**.

## <a name="cost-estimation-tools"></a>Strumenti di stima dei costi
I due strumenti indicati di seguito permettono di comprendere meglio i costi totali per l'esecuzione del modello di soluzione per la manutenzione predittiva nel settore aerospaziale della propria sottoscrizione:

* [Calcolatore prezzi (online)](https://azure.microsoft.com/pricing/calculator/)
* [Microsoft Azure Cost Estimator Tool (PC desktop)](http://www.microsoft.com/download/details.aspx?id=43376)

