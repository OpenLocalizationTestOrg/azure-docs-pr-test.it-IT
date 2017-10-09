---
title: manutenzione aaaPredictive aerospaziale con Azure - Guida tecnica di soluzioni di Business Intelligence Cortana | Documenti Microsoft
description: "Una Guida tecnica toohello modello di soluzione con Microsoft Cortana Intelligence per la manutenzione predittiva aerospaziale, utilità e trasporto."
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
ms.date: 03/14/2017
ms.author: fboylu
ms.openlocfilehash: 30ddc1c101007546ae1b303bccebae3ecdacb442
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="technical-guide-toohello-cortana-intelligence-solution-template-for-predictive-maintenance-in-aerospace-and-other-businesses"></a>Guida tecnica toohello Cortana modello di soluzione di Business Intelligence per la manutenzione predittiva aerospaziale e altre aziende

## <a name="important"></a>**Importante**
Questo articolo è stato deprecato. informazioni di Hello sono ancora rilevanti toohello problema, ad esempio manutenzione predittiva in aerospaziale, ma l'articolo più recente con hello più le informazioni di toodate hello è reperibile [qui](https://github.com/Azure/cortana-intelligence-predictive-maintenance-aerospace). 

## <a name="acknowledgements"></a>**Riconoscimenti**
Autori di questo articolo sono gli esperti di gestione dati Yan Zhang, Gauher Shaheen e Fidan Boylu Uz e il programmatore Microsoft Dan Grecoe.

## <a name="overview"></a>**Overview**
Modelli di soluzioni sono progettati processo hello tooaccelerate della creazione di una demo E2E sopra Cortana Intelligence Suite. Un modello distribuito verrà provisioning la sottoscrizione con i componenti necessari Intelligence Cortana e hello le relazioni tra di essi. Inoltre esegue il seeding della pipeline di dati hello con dati di esempio generati da un'applicazione di generatore di dati che scarica e installa nel computer locale dopo aver distribuito il modello di soluzione hello. dati di Hello generati dal generatore di hello verranno strati pipeline di dati hello e avviare la generazione delle stime di apprendimento che possono quindi essere visualizzate nel dashboard di Power BI hello. il processo di distribuzione Hello guiderà diversi passaggi tooset le credenziali di soluzione. Assicurarsi che registrare queste credenziali, ad esempio nome della soluzione, username e password specificati durante la distribuzione di hello.  

obiettivo di Hello di questo documento è l'architettura di riferimento tooexplain hello e diversi componenti, il provisioning nella sottoscrizione come parte di questo modello di soluzione. documento Hello illustra anche come tooreplace i dati di esempio con dati reali di toobe toosee in grado di approfondimenti e stime dati personalizzati. Inoltre, il documento di hello illustra le parti del modello di soluzione che sarebbe necessario toobe modificato se si desidera soluzione hello toocustomize con i propri dati hello. Alla fine di hello vengono fornite istruzioni su come toobuild hello dashboard di Power BI per questo modello di soluzione.

> [!TIP]
> È possibile scaricare e stampare una [versione in formato PDF di questo documento](http://download.microsoft.com/download/F/4/D/F4D7D208-D080-42ED-8813-6030D23329E9/cortana-analytics-technical-guide-predictive-maintenance.pdf).
> 
> 

## <a name="big-picture"></a>**Quadro generale**
![Architettura di manutenzione predittiva](media/cortana-analytics-technical-guide-predictive-maintenance/predictive-maintenance-architecture.png)

Quando si distribuisce la soluzione hello, vengono attivati i vari servizi di Azure nell'ambito di gruppo Analitica Cortana (*, ovvero* Hub eventi, Analisi di flusso, HDInsight, Data Factory, Machine Learning *e così via*. diagramma dell'architettura Hello sopra illustrato, a un livello elevato, la modalità manutenzione predittiva per il modello di soluzione aerospaziale hello viene costruita da end-to-end. Si sarà in grado di tooinvestigate questi servizi nel portale di azure hello facendo clic su di essi nel diagramma modello di soluzione hello creato con la distribuzione hello della soluzione hello eccezione hello di HDInsight perché il servizio viene eseguito il provisioning su richiesta quando hello correlati le attività della pipeline sono necessari toorun ed eliminata in seguito.
È possibile scaricare un [versione originale del diagramma hello](http://download.microsoft.com/download/1/9/B/19B815F0-D1B0-4F67-AED3-A40544225FD1/ca-topologies-maintenance-prediction.png).

Hello le sezioni seguenti descrivono ogni parte.

## <a name="data-source-and-ingestion"></a>**Origine dati e inserimento**
### <a name="synthetic-data-source"></a>Origine dati sintetica
Per questi dati hello modello origine utilizzata viene generato da un'applicazione desktop che scaricano ed eseguono in locale al termine della distribuzione. Verrà toodownload istruzioni hello trovare e installare l'applicazione nella barra delle proprietà hello quando si seleziona primo nodo hello chiamato generatore di dati di manutenzione predittiva nel diagramma modello di soluzione hello. Questa applicazione feed hello [Hub di eventi di Azure](#azure-event-hub) servizio con punti dati o eventi, che verranno utilizzati nel resto di hello del flusso di soluzione hello. Questa origine dati è costituita da o derivata dai dati disponibili pubblicamente il [repository dei dati NASA](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/) utilizzando hello [Set di dati di simulazione di Turbofan motore degradazione](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/#turbofan).

applicazione di generazione di eventi Hello popolerà hello Hub di eventi di Azure solo mentre è in esecuzione nel computer in uso.

### <a name="azure-event-hub"></a>Hub eventi di Azure
Hello [Hub di eventi di Azure](https://azure.microsoft.com/services/event-hubs/) servizio è destinatario hello dell'input hello fornito da hello sintetica origine dati descritto in precedenza.

## <a name="data-preparation-and-analysis"></a>**Preparazione e analisi dei dati**
### <a name="azure-stream-analytics"></a>Analisi di flusso di Azure
Hello [Analitica di flusso di Azure](https://azure.microsoft.com/services/stream-analytics/) servizio viene utilizzato tooprovide quasi in tempo reale analitica nel flusso di input hello hello [Hub di eventi di Azure](#azure-event-hub) service e pubblicare i risultati in un [diPowerBI](https://powerbi.microsoft.com) dashboard, nonché l'archiviazione tutti raw toohello eventi in ingresso [di archiviazione di Azure](https://azure.microsoft.com/services/storage/) servizio per l'elaborazione successiva da hello [Data Factory di Azure](https://azure.microsoft.com/documentation/services/data-factory/) servizio.

### <a name="hd-insights-custom-aggregation"></a>Aggregazione personalizzata di HDInsight
servizio di Azure HD Insight Hello è toorun utilizzati [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) aggregazioni tooprovide script (orchestrati da Azure Data Factory) sugli eventi non elaborati hello archiviati tramite il servizio di Azure flusso Analitica hello.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) servizio viene utilizzato (orchestrati da Azure Data Factory) toomake stime su hello rimanente durata utile (RUL) di un motore particolare aereo dato hello input ricevuto.

## <a name="data-publishing"></a>**Pubblicazione dei dati**
### <a name="azure-sql-database-service"></a>Servizio database SQL di Azure
Hello [Database SQL di Azure](https://azure.microsoft.com/services/sql-database/) servizio è stime hello toostore utilizzato (gestita da Azure Data Factory) ricevute dal servizio di Azure Machine Learning che verrà utilizzato in hello hello [Power BI](https://powerbi.microsoft.com) dashboard.

## <a name="data-consumption"></a>**Utilizzo dei dati**
### <a name="power-bi"></a>Power BI
Hello [Power BI](https://powerbi.microsoft.com) servizio viene utilizzato tooshow un dashboard che contiene le aggregazioni e gli avvisi forniti da hello [Azure flusso Analitica](https://azure.microsoft.com/services/stream-analytics/) servizio nonché stime RUL archiviate in [SQL di Azure Database](https://azure.microsoft.com/services/sql-database/) che sono state prodotte utilizzando hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) servizio. Per istruzioni su come toobuild hello dashboard di Power BI per questo modello di soluzione, vedere toohello sezione riportata di seguito.

## <a name="how-toobring-in-your-own-data"></a>**Come toobring nei propri dati**
In questa sezione viene descritto come toobring tooAzure propri dati e aree richiederebbe cambia per dati hello è rendere questa architettura.

È improbabile che un set di dati è portare corrisponderebbe hello set di dati utilizzato da hello [Set di dati di simulazione di Turbofan motore degradazione](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/#turbofan) utilizzata per questo modello di soluzione. Comprendere i requisiti e dei dati sarà essenziale su modificare toowork questo modello con i propri dati. Se si tratta del primo toohello l'esposizione del servizio di Azure Machine Learning, è possibile ottenere un tooit introduzione utilizzando l'esempio hello in [come toocreate l'esperimento prima](machine-learning-create-experiment.md).

Hello le sezioni seguenti verrà descritte le sezioni di hello del modello di hello richiederà modifiche quando è stato introdotto un nuovo set di dati.

### <a name="azure-event-hub"></a>Hub eventi di Azure
Hello servizio Hub di eventi di Azure è molto generico, in modo che i dati possono essere inseriti toohello hub in formato CSV o JSON. Nessuna elaborazione speciale si verifica in hello Hub di eventi di Azure, ma è importante comprendere i dati di hello sono inseriti.

Questo documento non descrive come tooingest i dati, ma è possibile inviare facilmente gli eventi o dati tooan Hub di eventi di Azure mediante hello API Hub eventi.

### <a name="azure-stream-analytics"></a>Analisi di flusso di Azure
servizio Azure flusso Analitica Hello è tooprovide utilizzati quasi in tempo reale analitica mediante la lettura da flussi di dati e l'output del numero di tooany dati di origini.

Per la manutenzione predittiva per il modello di soluzione aerospaziale hello, la query Analitica di flusso di Azure è costituita da quattro sottoquery, ogni dispendiosa in termini di eventi hello servizio Hub di eventi di Azure e con l'output in quattro posizioni distinte. L'output è costituito da tre set di dati di Power BI e una posizione di archiviazione di Azure.

Impossibile trovare Hello Azure flusso Analitica query da:

* Accesso al portale di Azure hello
* Individuazione processi di flusso Analitica hello ![icona flusso Analitica](media/cortana-analytics-technical-guide-predictive-maintenance/icon-stream-analytics.png) che sono stati generati quando è stata distribuita la soluzione hello (*ad esempio*, **maintenancesa02asapbi** e **maintenancesa02asablob** per la soluzione di manutenzione predittiva)
* Selezionare:
  
  * ***INPUT*** tooview hello input della query
  * ***QUERY*** tooview hello query
  * ***GENERA*** tooview hello output diversi

Informazioni sulla costruzione delle query Analitica di flusso di Azure sono reperibile in hello [flusso Analitica Query riferimento](https://msdn.microsoft.com/library/azure/dn834998.aspx) su MSDN.

In questa soluzione, le query hello output tre set di dati con quasi hello in arrivo dati flusso tooa dashboard di Power BI che viene fornito come parte di questo modello di soluzione di informazioni in tempo reale analitica. Poiché non è presente una conoscenza implicita sul formato di dati in ingresso hello, queste query necessario toobe modificato in base il formato di dati.

query Hello nel processo di flusso Analitica secondo hello **maintenancesa02asablob** restituisce semplicemente tutti [Hub eventi](https://azure.microsoft.com/services/event-hubs/) eventi [di archiviazione di Azure](https://azure.microsoft.com/services/storage/) e pertanto non richiede alcuna modifica indipendentemente dal formato di dati come hello informazioni sull'evento completo viene trasmessa toostorage.

### <a name="azure-data-factory"></a>Data factory di Azure
Hello [Data Factory di Azure](https://azure.microsoft.com/documentation/services/data-factory/) servizio gestisce lo spostamento di hello e l'elaborazione dei dati. Per la manutenzione predittiva per i dati di modello di soluzione aerospaziale hello factory è costituita da tre [pipeline](../data-factory/data-factory-create-pipelines.md) che ed elaborare dati hello con varie tecnologie.  È possibile accedere la data factory aprendo hello hello Data Factory nodo nella parte inferiore di hello del diagramma modello di soluzione hello creato con la distribuzione di hello di soluzione hello. Questa operazione richiederà è toohello data factory nel portale di Azure. Se si verificano errori nel set di dati, è possibile ignorare quelli come se fossero a causa di factory toodata distribuito prima che il generatore di dati hello è stato avviato. Questi errori non impediscono il funzionamento della data factory.

![Errori di set di dati di Data Factory](media/cortana-analytics-technical-guide-predictive-maintenance/data-factory-dataset-error.png)

Questa sezione illustra hello necessario [pipeline](../data-factory/data-factory-create-pipelines.md) e [attività](../data-factory/data-factory-create-pipelines.md) contenuti in hello [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/). Di seguito è vista diagramma hello della soluzione hello.

![Data factory di Azure](media/cortana-analytics-technical-guide-predictive-maintenance/azure-data-factory.png)

Due delle pipeline hello di questa factory contengono [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) script toopartition utilizzati e i dati di aggregazione hello. Quando si è notato, script hello viene collocato nella hello [di archiviazione di Azure](https://azure.microsoft.com/services/storage/) account creato durante l'installazione. Il percorso sarà: maintenancesascript\\\\script\\\\hive\\\\ (o https://[nome della soluzione].blob.core.windows.net/maintenancesascript).

Toohello simile [Azure flusso Analitica](#azure-stream-analytics-1) query, il [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) script implicita delle informazioni sul formato di dati in ingresso hello, queste query sarebbero necessario toobe modificato in base al formato dei dati e [funzionalità engineering](machine-learning-feature-selection-and-engineering.md) requisiti.

#### <a name="aggregateflightinfopipeline"></a>*AggregateFlightInfoPipeline*
Questo [pipeline](../data-factory/data-factory-create-pipelines.md) contiene una singola attività - un [HDInsightHive](../data-factory/data-factory-hive-activity.md) attività utilizzando un [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) che esegue un [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) inserire dati di script toopartition hello in [di archiviazione di Azure](https://azure.microsoft.com/services/storage/) durante il [Azure flusso Analitica](https://azure.microsoft.com/services/stream-analytics/) processo.

Lo script [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) per questa attività di partizionamento è ***AggregateFlightInfo.hql***.

#### <a name="mlscoringpipeline"></a>*MLScoringPipeline*
Questo [pipeline](../data-factory/data-factory-create-pipelines.md) contiene diverse attività e il cui risultato finale viene calcolato il punteggio hello stime da hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) esperimento associato a questo modello di soluzione.

attività Hello contenute in questo sono:

* [HDInsightHive](../data-factory/data-factory-hive-activity.md) attività utilizzando un [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) che esegue un [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) tooperform aggregazioni di script e funzionalità di progettazione necessari per hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) provare.
  Lo script [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) per questa attività di partizionamento è ***PrepareMLInput.hql***.
* [Copia](https://msdn.microsoft.com/library/azure/dn835035.aspx) attività che sposta risultati hello il [HDInsightHive](../data-factory/data-factory-hive-activity.md) tooa attività singola [di archiviazione di Azure](https://azure.microsoft.com/services/storage/) blob che è possibile accedere dal [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) attività.
* [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) attività che chiama hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) esperimento determinando risultati hello viene inseriti in una singola [di archiviazione di Azure](https://azure.microsoft.com/services/storage/) blob.

#### <a name="copyscoredresultpipeline"></a>*CopyScoredResultPipeline*
Questo [pipeline](../data-factory/data-factory-create-pipelines.md) contiene una singola attività - un [copia](https://msdn.microsoft.com/library/azure/dn835035.aspx) attività che sposta i risultati di hello di hello [Azure Machine Learning](#azure-machine-learning) sperimentare dal *** MLScoringPipeline*** toohello [Database SQL di Azure](https://azure.microsoft.com/services/sql-database/) che è stato eseguito il provisioning come parte dell'installazione del modello di soluzione.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) esperimento utilizzato per questo modello di soluzione offre hello rimanenti utile vita (RUL) di un motore aereo. esperimento Hello è toohello specifico set di dati utilizzati e pertanto richiedono una sostituzione o modifica dati toohello specifico che viene portati in.

Per informazioni sulla modalità di creazione hello esperimento di Azure Machine Learning, vedere [manutenzione predittiva: passaggio 1 di 3, la preparazione dei dati e progettazione di funzionalità](http://gallery.cortanaanalytics.com/Experiment/Predictive-Maintenance-Step-1-of-3-data-preparation-and-feature-engineering-2).

## <a name="monitor-progress"></a>**Monitorare lo stato**
 Una volta avviato hello generatore di dati, pipeline hello inizia tooget Alluminosilicato e hello diversi componenti della soluzione avviare qui in azione seguente hello comandi da hello Data Factory. Esistono due modi, che è possibile monitorare pipeline hello.

1. Uno dei processi di flusso Analitica hello scrive hello in arrivo dati tooblob storage raw. Se si fare clic sul componente di archiviazione Blob della soluzione dalla schermata hello è soluzione hello distribuita correttamente e quindi fare clic su Apri nel riquadro di destra hello, si passerà toohello [portale di gestione](https://portal.azure.com/). Una volta nel portale, fare clic su BLOB. Nel riquadro successivo di hello, vedrai un elenco di contenitori. Fare clic su **maintenancesadata**. Nel riquadro successivo di hello, verrà visualizzato hello **rawdata** cartella. Nella cartella rawdata hello vedrai cartelle con nomi quali ora = 17, ora = 18 e così via. Se queste cartelle, indica che dati non elaborati hello sono stata generata sul computer e archiviati nell'archiviazione blob. Verranno visualizzati file con estensione csv che in tali cartelle devono avere dimensioni limitate in MB.
2. Hello ultimo passaggio della pipeline hello è toowrite dati (ad esempio, le stime dall'apprendimento) nel Database SQL. Potrebbe essere toowait un massimo di tre ore per hello tooappear di dati nel Database SQL. Un modo toomonitor la quantità di dati è disponibile nel Database SQL è tramite [portale di azure](https://manage.windowsazure.com/). Nel riquadro di sinistra hello individuare i database di SQL ![icona SQL](media/cortana-analytics-technical-guide-predictive-maintenance/icon-SQL-databases.png) e farvi clic sopra. Individuare quindi il database **pmaintenancedb** e fare clic su di esso. Nella pagina successiva di hello nella parte inferiore di hello, fare clic su GESTISCI
   
    ![Icona Gestisci](media/cortana-analytics-technical-guide-predictive-maintenance/icon-manage.png).
   
    In questo caso, è possibile fare clic su Nuova Query e query per il numero di righe (ad esempio select count da PMResult) hello. Man mano che aumenta il database, hello numero di righe nella tabella hello aumenta.

## <a name="power-bi-dashboard"></a>**Dashboard di Power BI**
### <a name="overview"></a>Panoramica
In questa sezione viene descritto come tooset backup toovisualize dashboard di Power BI in tempo reale dati dal flusso di Azure Analitica (percorso critico), nonché di stima batch risultante dall'apprendimento Azure (percorso freddo).

### <a name="setup-cold-path-dashboard"></a>Configurare il dashboard per il percorso non critico
Nella pipeline di dati ad accesso sporadico percorso hello, obiettivo fondamentale di hello è tooget il RUL predittiva (rimanente vita utile) di ciascun motore aereo al termine dell'operazione un volo (ciclo). il risultato di stima Hello viene aggiornato ogni 3 ore per la stima motori hello che hanno terminato un volo durante hello ultimi 3 ore.

Power BI si connette il database di SQL Azure tooan come origine dati, in cui sono archiviati i risultati della stima. Nota: 1) al momento di distribuire la soluzione, una stima reale verrà visualizzata nel database di hello in 3 ore.
file pbix Hello fornita con il download di generatore hello contiene alcuni dati del valore di inizializzazione in modo che è possibile creare dashboard di Power BI hello immediatamente. 2) in questo passaggio il prerequisito di hello è toodownload e installare software gratuito hello [Power BI desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/).

Hello passaggi seguenti verranno istruzioni su come tooconnect hello pbix file a messaggi hello del Database SQL che è stata riattivata in fase di distribuzione della soluzione che contiene dati di hello (*ad esempio*. i risultati della stima.

1. Ottenere le credenziali del database hello.
   
   È necessario **nome del server, nome del database, nome utente e password di database** prima dello spostamento toonext passaggi. Di seguito sono tooguide passaggi hello è come toofind li.
   
   * Quando la voce **Database SQL di Azure** nel diagramma del modello di soluzione diventa verde, selezionarla e quindi fare clic su **Apri**.
   * Si noterà una nuova scheda o finestra che visualizza hello pagina del portale Azure. Fare clic su **'Gruppi di risorse'** nel riquadro di sinistra hello.
   * Selezionare una sottoscrizione hello in uso per la distribuzione di soluzioni di hello, quindi **' YourSolutionName\_gruppo di risorse '**.
   * Nel nuovo pop hello out pannello, fare clic su hello ![icona SQL](media/cortana-analytics-technical-guide-predictive-maintenance/icon-sql.png) tooaccess sull'icona del database. Il nome del database è Avanti toohello questa icona (*ad esempio*, **'pmaintenancedb'**), hello e **nome server database** è elencato in proprietà del nome Server hello e dovrebbe essere simile troppo**YourSoutionName.database.windows.net**.
   * Il database **username** e **password** sono hello stesso hello nome utente e password registrati in precedenza durante la distribuzione della soluzione hello.
2. Aggiornare l'origine di dati di hello del file di hello freddo percorso report con Power BI Desktop.
   
   * Nella cartella hello nel PC in cui è stato scaricato e decompresso il file del generatore, fare doppio clic su di **PowerBI\\PredictiveMaintenanceAerospace.pbix** file. Se vengono visualizzati i messaggi di avviso quando si apre il file hello, ignorarli. Nella parte superiore di hello del file hello, fare clic su **modifica query**.
     
     ![Modifica query](media/cortana-analytics-technical-guide-predictive-maintenance/edit-queries.png)
   * Verranno visualizzate due tabelle, **RemainingUsefulLife** e **PMResult**. Selezionare hello prima tabella e fare clic su ![icona Impostazioni Query](media/cortana-analytics-technical-guide-predictive-maintenance/icon-query-settings.png) Avanti troppo**'Source'** in **passaggi applicati** su hello destra **'Impostazioni Query'**pannello. Ignorare gli eventuali messaggi di avviso visualizzati.
   * In hello pop out finestra, sostituire **"Server"** e **'Database'** con i nomi di server e database e quindi fare clic su **'OK'**. Nome del server, assicurarsi di specificare la porta 1433 hello (**YourSoutionName.database.windows.net, 1433**). Lasciare il campo del Database hello come **pmaintenancedb**. Ignorare i messaggi di avviso hello hello visualizzate.
   * Pop-successivo hello out finestra, si noterà due opzioni nel riquadro di sinistra hello (**Windows** e **Database**). Fare clic su **'Database'**, compilare il **'Username'** e **'Password'** (si tratta di hello username e password specificata quando si hello soluzione distribuita e creato un Database SQL Azure). In ***selezionare quale livello tooapply per queste impostazioni***, controllare l'opzione a livello di database. Fare clic su **Connetti**.
   * Fare clic sulla seconda tabella hello **PMResult** quindi fare clic su ![icona di spostamento](media/cortana-analytics-technical-guide-predictive-maintenance/icon-navigation.png) Avanti troppo**'Source'** in **passaggi applicati** su hello destra **'Impostazioni query'** pannello e aggiornare il server di hello e i nomi di database come hello sopra i passaggi e fare clic su OK.
   * Dopo aver toohello indietro interattiva di pagina precedente, chiudere la finestra di hello. Nel messaggio popup visualizzato fare clic su **Applica**. Infine, fare clic su hello **salvare** pulsante modifiche hello toosave. Il file di Power BI è ora stabilita connessione toohello server. Se le visualizzazioni sono vuote, assicurarsi che cancellare tutti i dati di hello selezioni hello nella hello visualizzazioni toovisualize facendo clic sull'icona della gomma hello in hello angolo superiore destro di legende hello. Scegliere visualizzazioni hello hello aggiornamento pulsante tooreflect nuovi dati. Inizialmente, viene visualizzata solo dati di inizializzazione hello in visualizzazioni come data factory di hello toorefresh pianificato ogni 3 ore. Dopo 3 ore, si noterà nuove stime riflesse nelle visualizzazioni quando si aggiornano dati hello.
3. (Facoltativo) Pubblicare il dashboard di percorso freddo hello troppo[Power BI online](http://www.powerbi.com/). Si noti che per questo passaggio è necessario un account Power BI o Office 365.
   
   * Fare clic su **'Pubblica'** e alcuni secondi dopo viene visualizzata una finestra visualizzazione "Pubblicazione tooPower successo BI!" Dopo alcuni secondi viene visualizzato un messaggio di conferma della pubblicazione in Power BI con un segno di spunta verde. Fare clic sul collegamento hello sotto "PredictiveMaintenanceAerospace.pbix Apri in Power BI". toofind indicazioni dettagliate, vedere [pubblicare da Power BI Desktop](https://support.powerbi.com/knowledgebase/articles/461278-publish-from-power-bi-desktop).
   * un nuovo dashboard toocreate: fare clic su hello  **+**  firmare toothe successivo **dashboard** sezione nel riquadro di sinistra hello. Immettere il nome di hello "Demo manutenzione predittiva" per il nuovo dashboard.
   * Dopo aver aperto il report hello, fare clic su ![icona della PUNTINA](media/cortana-analytics-technical-guide-predictive-maintenance/icon-pin.png) toopin tutti i dashboard visualizzazioni tooyour. toofind indicazioni dettagliate, vedere [aggiungere un dashboard di Power BI tooa riquadro da un report](https://support.powerbi.com/knowledgebase/articles/430323-pin-a-tile-to-a-power-bi-dashboard-from-a-report).
     Vai a pagina dashboard toohello e regolare hello dimensioni e la posizione delle visualizzazioni e modificare le relative posizioni. toofind istruzioni dettagliate su come tooedit i riquadri, vedere [modifica un riquadro: ridimensionare, spostare, rinominare, pin, eliminare, aggiungere un collegamento ipertestuale](https://powerbi.microsoft.com/documentation/powerbi-service-edit-a-tile-in-a-dashboard/#rename). Ecco un dashboard di esempio con alcuni tooit aggiunte visualizzazioni freddo percorso.  A seconda di quanto tempo si esegue il generatore di dati, i numeri sulle visualizzazioni di hello potrebbero essere diversi.
     <br/>
     ![Visualizzazione finale](media/cortana-analytics-technical-guide-predictive-maintenance/final-view.png)
     <br/>
   * tooschedule l'aggiornamento dei dati di hello, posizionare il mouse sopra hello **PredictiveMaintenanceAerospace** set di dati, fare clic su ![icona puntini di sospensione](media/cortana-analytics-technical-guide-predictive-maintenance/icon-elipsis.png) e quindi scegliere **Pianifica aggiornamento**.
     <br/>
     **Nota:** se viene visualizzato un massaggio di avviso, fare clic su **Modifica credenziali** e assicurarsi che le credenziali di database sono hello uguali a quelli descritti nel passaggio 1.
     <br/>
     ![Pianifica aggiornamenti](media/cortana-analytics-technical-guide-predictive-maintenance/schedule-refresh.png)
     <br/>
   * Espandere hello **Pianifica aggiornamento** sezione. Attivare l'opzione "Mantieni aggiornati i dati".
     <br/>
   * Pianificare l'aggiornamento di hello in base alle proprie esigenze. toofind ulteriori informazioni, vedere [aggiornamento dei dati in Power BI](https://support.powerbi.com/knowledgebase/articles/474669-data-refresh-in-power-bi).

### <a name="setup-hot-path-dashboard"></a>Configurare il dashboard per il percorso critico
Hello alla procedura seguente spiega come dati in tempo reale toovisualize output dal flusso Analitica processi che sono stati generati in fase di distribuzione di soluzioni di hello. Oggetto [Power BI online](http://www.powerbi.com/) account è obbligatorio tooperform hello alla procedura seguente. Se non si ha un account, [crearne uno](https://powerbi.microsoft.com/pricing).

1. Aggiungere l'output di Power BI ad Analisi di flusso di Azure.
   
   * Sarà necessario istruzioni hello toofollow [Analitica di flusso di Azure e Power BI: un dashboard in tempo reale analitica visibilità in tempo reale del flusso di dati](../stream-analytics/stream-analytics-power-bi-dashboard.md) tooset di output di hello del processo Analitica di flusso di Azure come il risparmio di energia Dashboard di Business Intelligence.
   * query ASA Hello con tre output che sono **aircraftmonitor**, **aircraftalert**, e **flightsbyhour**. È possibile visualizzare la query hello facendo clic sulla scheda della query. Tooeach corrispondente di queste tabelle, sarà necessario tooadd tooASA un output. Quando si aggiunge l'output di hello prima (*ad esempio* **aircraftmonitor**) verificare che hello **Alias di Output**, **nome set di dati** e  **Nome tabella** sono hello stesso (**aircraftmonitor**). Output hello ripetere i passaggi tooadd **aircraftalert**, e **flightsbyhour**. Dopo aver aggiunto tutti e tre tabelle di output e hello ASA processo avviato, è necessario ottenere un messaggio di conferma (*ad esempio*, "Iniziale flusso Analitica processo maintenancesa02asapbi ha avuto esito positivo").
2. Accedi troppo[Power BI online](http://www.powerbi.com)
   
   * In hello sinistra pannello set di dati nell'area di lavoro di ***DATASET*** nomi **aircraftmonitor**, **aircraftalert**, e **flightsbyhour**dovrebbe essere visualizzato. Si tratta di flusso di dati è inseriti da Azure flusso Analitica nel set di dati step.hello precedente hello hello **flightsbyhour** potrebbe non essere visualizzato in hello stesso tempo come hello altri due set di dati a causa di natura toohello della query SQL hello sottostante . Verrà tuttavia visualizzato dopo un'ora.
   * Verificare che hello ***visualizzazioni*** riquadro è aperto e viene visualizzato sul lato destro della schermata di hello.
3. Dopo aver creato i dati di hello propagazione in Power BI, è possibile avviare la visualizzazione di dati in streaming hello. Di seguito è che un dashboard di esempio con alcune visualizzazioni percorso critico aggiunto tooit. È possibile creare altri riquadri del dashboard in base a set di dati appropriati. A seconda di quanto tempo si esegue il generatore di dati, i numeri sulle visualizzazioni di hello potrebbero essere diversi.

    ![Visualizzazione dashboard](media\cortana-analytics-technical-guide-predictive-maintenance\dashboard-view.png)

1. Ecco alcuni toocreate passaggi uno dei riquadri hello precedente: hello "flotta vista di Visual Studio 11 sensore. Threshold 48.26":
   
   * Fare clic su set di dati **aircraftmonitor** su hello sinistra pannello del set di dati.
   * Fare clic su hello **grafico a linee** icona.
   * Fare clic su **elaborati** in hello **campi** riquadro in modo che venga visualizzato nell'area "Asse" in hello **visualizzazioni** riquadro.
   * Fare clic su "s11" e "s11\_alert" in modo che entrambi vengano visualizzati in "Valori". Fare clic su freccia hello Avanti troppo**s11** e **s11\_avviso**, modificare "Somma" troppo "medio".
   * Fare clic su **salvare** nella parte superiore di hello e nome report hello "aircraftmonitor". Verrà visualizzato il report denominato "aircraftmonitor" in hello **report** sezione hello **Navigator** riquadro a sinistra di hello.
   * Fare clic su hello **Pin Visual** icona su hello angolo superiore destro di questo grafico a linee. È possibile selezionare un dashboard, una finestra "Pin tooDashboard" potrebbero essere visualizzate. Selezionare "Predictive Maintenance Demo" e quindi fare clic su "Aggiungi".
   * Posiziona il mouse hello su questo riquadro nel dashboard di hello, fare clic sull'icona di "Modifica" hello nella hello angolo superiore destro toochange il titolo troppo "vs Fleet visualizzazione del sensore 11. Soglia 48,26" e il sottotitolo troppo"Media tra fleet nel tempo".

## <a name="how-toodelete-your-solution"></a>**Come toodelete la soluzione**
Assicurarsi di arrestare il generatore di dati di hello quando si utilizza non attivamente soluzione hello come in esecuzione il generatore di dati hello comporta costi elevati. Se si utilizza non elimina soluzione hello. L'eliminazione della soluzione eliminerà tutti i componenti di hello provisioning nella sottoscrizione per la distribuzione di soluzioni di hello. soluzione hello toodelete fare clic sul nome della soluzione nel riquadro sinistro di hello del modello di soluzione hello e fare clic su Elimina.

## <a name="cost-estimation-tools"></a>**Strumenti di stima dei costi**
Hello due sono i seguenti strumenti toohelp disponibili è comprendere meglio il costo totale necessario per l'esecuzione di hello manutenzione predittiva per il modello di soluzione aerospaziale nella sottoscrizione:

* [Calcolatore prezzi (online)](https://azure.microsoft.com/pricing/calculator/)
* [Microsoft Azure Cost Estimator Tool (PC desktop)](http://www.microsoft.com/download/details.aspx?id=43376)

