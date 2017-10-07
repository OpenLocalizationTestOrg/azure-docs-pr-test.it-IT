---
title: Previsione nella Guida di energia Technical aaaDemand | Documenti Microsoft
description: Una Guida tecnica toohello modello di soluzione con Microsoft Cortana Intelligence per la richiesta di previsione in energia.
services: cortana-analytics
documentationcenter: 
author: yijichen
manager: ilanr9
editor: yijichen
ms.assetid: 7f1a866b-79b7-4b97-ae3e-bc6bebe8c756
ms.service: cortana-analytics
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2016
ms.author: inqiu;yijichen;ilanr9
ms.openlocfilehash: c97b7c19c9e3a317aecc329e61a0692d2f1ec53e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="technical-guide-toohello-cortana-intelligence-solution-template-for-demand-forecast-in-energy"></a>Guida tecnica toohello Cortana modello di soluzione di Business Intelligence per la richiesta di energia di previsione
## <a name="overview"></a>**Overview**
Modelli di soluzioni sono progettati processo hello tooaccelerate della creazione di una demo E2E sopra Cortana Intelligence Suite. Un modello distribuito verrà effettuare il provisioning di abbonamento con componente necessario di Cortana Intelligence e le relazioni di hello tra. Inoltre esegue il seeding della pipeline di dati hello con dati di esempio generati da un'applicazione di simulazione di dati. Scaricare il simulatore di dati hello dal collegamento hello fornito e installarlo nel computer locale, fare riferimento a file Readme. txt toohello per istruzioni sull'utilizzo di simulatore hello. Dati generati dal simulatore hello verranno strati pipeline di dati hello e avviare la creazione di stima di machine learning che può quindi essere visualizzato nel dashboard di Power BI hello.

modello di soluzione hello è reperibile [qui](https://gallery.cortanaintelligence.com/SolutionTemplate/Demand-Forecasting-for-Energy-1)

il processo di distribuzione Hello guiderà diversi passaggi tooset le credenziali di soluzione. Assicurarsi che registrare queste credenziali, ad esempio nome della soluzione, username e password specificati durante la distribuzione di hello.

obiettivo di Hello di questo documento è l'architettura di riferimento tooexplain hello e diversi componenti, il provisioning nella sottoscrizione come parte di questo modello di soluzione. documento Hello parla anche come tooreplace hello dati di esempio, con dati reali di proprie toobe toosee in grado di insights/stime da di dati. Inoltre, hello documento discussioni sulle parti hello di hello modello di soluzione che sarebbe necessario toobe modificato se si desidera soluzione hello toocustomize con i propri dati. Alla fine di hello vengono fornite istruzioni su come toobuild hello dashboard di Power BI per questo modello di soluzione.

## <a name="big-picture"></a>**Quadro generale**
![](media/cortana-analytics-technical-guide-demand-forecast/ca-topologies-energy-forecasting.png)

### <a name="architecture-explained"></a>Spiegazione dell'architettura
Quando si distribuisce la soluzione hello, vengono attivati i vari servizi di Azure nell'ambito di gruppo Analitica Cortana (*, ovvero* Hub eventi, Analisi di flusso, HDInsight, Data Factory, Machine Learning *e così via*. diagramma dell'architettura Hello sopra illustrato, a un livello elevato, modalità di costruzione hello Demand Forecasting per il modello di soluzione di energia da end-to-end. Si sarà in grado di tooinvestigate hello di questi servizi, fare clic su di essi nel diagramma modello di soluzione creato con la distribuzione di hello di soluzione hello. Hello le sezioni seguenti descrivono ogni parte.

## <a name="data-source-and-ingestion"></a>**Origine dati e inserimento**
### <a name="synthetic-data-source"></a>Origine dati sintetica
Per questi dati hello modello origine utilizzata viene generato da un'applicazione desktop che scaricano ed eseguono in locale al termine della distribuzione. Verrà toodownload istruzioni hello trovare e installare l'applicazione nella barra delle proprietà hello quando si seleziona primo nodo hello chiamato simulatore dati di previsione di energia in diagramma modello della soluzione hello. Questa applicazione feed hello [Hub di eventi di Azure](#azure-event-hub) servizio con punti dati o eventi, che verranno utilizzati nel resto di hello del flusso di soluzione hello.

applicazione di generazione di eventi Hello popolerà hello Hub di eventi di Azure solo mentre è in esecuzione nel computer in uso.

### <a name="azure-event-hub"></a>Hub eventi di Azure
Hello [Hub di eventi di Azure](https://azure.microsoft.com/services/event-hubs/) servizio è destinatario hello dell'input hello fornito da hello sintetica origine dati descritto in precedenza.

## <a name="data-preparation-and-analysis"></a>**Preparazione e analisi dei dati**
### <a name="azure-stream-analytics"></a>Analisi di flusso di Azure
Hello [Analitica di flusso di Azure](https://azure.microsoft.com/services/stream-analytics/) servizio viene utilizzato tooprovide quasi in tempo reale analitica nel flusso di input hello hello [Hub di eventi di Azure](#azure-event-hub) service e pubblicare i risultati in un [diPowerBI](https://powerbi.microsoft.com) dashboard, nonché l'archiviazione tutti raw toohello eventi in ingresso [di archiviazione di Azure](https://azure.microsoft.com/services/storage/) servizio per l'elaborazione successiva da hello [Data Factory di Azure](https://azure.microsoft.com/documentation/services/data-factory/) servizio.

### <a name="hd-insights-custom-aggregation"></a>Aggregazione personalizzata di HDInsight
servizio di Azure HD Insight Hello è toorun utilizzati [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) aggregazioni tooprovide script (orchestrati da Azure Data Factory) sugli eventi non elaborati hello archiviati tramite il servizio di Azure flusso Analitica hello.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) servizio viene utilizzato (orchestrati da Azure Data Factory) toomake previsione sul consumo di energia futuro di una determinata area dato hello input ricevuto.

## <a name="data-publishing"></a>**Pubblicazione dei dati**
### <a name="azure-sql-database-service"></a>Servizio database SQL di Azure
Hello [Database SQL di Azure](https://azure.microsoft.com/services/sql-database/) servizio è stime hello toostore utilizzato (gestita da Azure Data Factory) ricevute dal servizio di Azure Machine Learning che verrà utilizzato in hello hello [Power BI](https://powerbi.microsoft.com) dashboard.

## <a name="data-consumption"></a>**Uso dei dati**
### <a name="power-bi"></a>Power BI
Hello [Power BI](https://powerbi.microsoft.com) servizio viene utilizzato tooshow un dashboard che contiene le aggregazioni fornite da hello [Azure flusso Analitica](https://azure.microsoft.com/services/stream-analytics/) servizio nonché richiesta previsione risultati archiviati [SQL di Azure Database](https://azure.microsoft.com/services/sql-database/) che sono state prodotte utilizzando hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) servizio. Per istruzioni su come toobuild hello dashboard di Power BI per questo modello di soluzione, vedere toohello sezione riportata di seguito.

## <a name="how-toobring-in-your-own-data"></a>**Come toobring nei propri dati**
In questa sezione viene descritto come toobring tooAzure propri dati e aree richiederebbe cambia per dati hello è rendere questa architettura.

È improbabile che un set di dati che è portare corrisponderebbe hello set di dati utilizzato per questo modello di soluzione. Comprendere i requisiti e dei dati sarà essenziale su modificare toowork questo modello con i propri dati. Se si tratta del primo toohello l'esposizione del servizio di Azure Machine Learning, è possibile ottenere un tooit introduzione utilizzando l'esempio hello in [come toocreate l'esperimento prima](machine-learning/machine-learning-create-experiment.md).

Hello le sezioni seguenti verrà descritte le sezioni di hello del modello di hello richiederà modifiche quando è stato introdotto un nuovo set di dati.

### <a name="azure-event-hub"></a>Hub eventi di Azure
Hello [Hub di eventi di Azure](https://azure.microsoft.com/services/event-hubs/) servizio è molto generico, in modo che i dati possono essere inseriti toohello hub in formato CSV o JSON. Si verifica alcuna elaborazione particolare in hello Hub di eventi di Azure, ma è importante che comprendere i dati di hello sono inseriti.

Questo documento viene descritto come tooingest i dati, ma una possibile inviare facilmente gli eventi o dati tooan Hub di eventi di Azure, utilizzando hello [API Hub eventi](event-hubs/event-hubs-programming-guide.md).

### <a name="azure-stream-analytics"></a>Analisi di flusso di Azure
Hello [Azure flusso Analitica](https://azure.microsoft.com/services/stream-analytics/) servizio è utilizzato tooprovide quasi in tempo reale analitica per la lettura da flussi di dati e l'output del numero di tooany dati di origini.

Per hello Demand Forecasting per il modello di soluzione di energia, hello Azure flusso Analitica query è costituita da due sottoquery, ogni utilizzo di eventi da hello servizio Hub di eventi di Azure come input e con i percorsi di output tootwo distinti. L'output è costituito da un set di dati di Power BI e da una posizione di Archiviazione di Azure.

Hello [Azure flusso Analitica](https://azure.microsoft.com/services/stream-analytics/) per individuare query:

* Registrazione in hello [portale di gestione di Azure](https://manage.windowsazure.com/)
* Individuazione processi di hello flusso analitica ![](media/cortana-analytics-technical-guide-demand-forecast/icon-stream-analytics.png) che sono stati generati quando è stata distribuita la soluzione hello. Uno è per l'inserimento di archiviazione dei dati tooblob (ad esempio mytest1streaming432822asablob) e hello altri uno è per l'inserimento di dati tooPower BI (ad esempio mytest1streaming432822asapbi).
* Selezionare:

  * ***INPUT*** tooview hello input della query
  * ***QUERY*** tooview hello query
  * ***GENERA*** tooview hello output diversi

Informazioni sulla costruzione delle query Analitica di flusso di Azure sono reperibile in hello [flusso Analitica Query riferimento](https://msdn.microsoft.com/library/azure/dn834998.aspx) su MSDN.

In questa soluzione, hello processo Analitica di flusso di Azure che restituisce set di dati con informazioni analitica in tempo reale sui dashboard di hello in arrivo dati flusso tooa Power BI quasi viene fornito come parte di questo modello di soluzione. Poiché non è presente una conoscenza implicita sul formato di dati in ingresso hello, queste query necessario toobe modificato in base il formato di dati.

Hello altro processo Analitica di flusso di Azure genera tutti [Hub eventi](https://azure.microsoft.com/services/event-hubs/) eventi [di archiviazione di Azure](https://azure.microsoft.com/services/storage/) e pertanto non richiede alcuna modifica indipendentemente dal formato di dati come informazioni di evento completo hello viene inviato nel flusso toostorage.

### <a name="azure-data-factory"></a>Data factory di Azure
Hello [Data Factory di Azure](https://azure.microsoft.com/documentation/services/data-factory/) servizio gestisce lo spostamento di hello e l'elaborazione dei dati. In hello Demand Forecasting per i dati di modello di soluzione energia hello factory è costituita da dodici [pipeline](data-factory/data-factory-create-pipelines.md) che ed elaborare dati hello con varie tecnologie.

  È possibile accedere la data factory aprendo hello Data Factory nodo nella parte inferiore di hello del diagramma modello di soluzione hello creato con la distribuzione di hello di soluzione hello. Questa operazione richiederà è toohello data factory nel portale di gestione di Azure. Se si verificano errori nel set di dati, è possibile ignorare quelli come se fossero a causa di factory toodata distribuito prima che il generatore di dati hello è stato avviato. Questi errori non impediscono il funzionamento della data factory.

Questa sezione illustra hello necessario [pipeline](data-factory/data-factory-create-pipelines.md) e [attività](data-factory/data-factory-create-pipelines.md) contenuti in hello [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/). Di seguito è vista diagramma hello della soluzione hello.

![](media/cortana-analytics-technical-guide-demand-forecast/ADF2.png)

Cinque di pipeline hello di questa factory contengono [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) script toopartition utilizzati e i dati di aggregazione hello. Quando si è notato, script hello viene collocato nella hello [di archiviazione di Azure](https://azure.microsoft.com/services/storage/) account creato durante l'installazione. Il percorso sarà: demandforecasting\\\\script\\\\hive\\\\ (o https://[nome della soluzione].blob.core.windows.net/demandforecasting).

Toohello simile [Azure flusso Analitica](#azure-stream-analytics-1) query, il [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) script implicita delle informazioni sul formato di dati in ingresso hello, queste query sarebbero necessario toobe modificato in base al formato dei dati e [funzionalità engineering](machine-learning/machine-learning-feature-selection-and-engineering.md) requisiti.

#### <a name="aggregatedemanddatato1hrpipeline"></a>*AggregateDemandDataTo1HrPipeline*
Questo [pipeline](data-factory/data-factory-create-pipelines.md) pipeline contiene una singola attività - un [HDInsightHive](data-factory/data-factory-hive-activity.md) attività utilizzando un [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) che esegue un [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx)hello tooaggregate script ogni 10 secondi inviati nel flusso di dati richiesta nel livello di area livello toohourly sottostazione e inseriti nella coda [di archiviazione di Azure](https://azure.microsoft.com/services/storage/) tramite il processo di Azure flusso Analitica hello.

Lo script [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) per questa attività di partizionamento è ***AggregateDemandRegion1Hr.hql***

#### <a name="loadhistorydemanddatapipeline"></a>*LoadHistoryDemandDataPipeline*
Questa [pipeline](data-factory/data-factory-create-pipelines.md) contiene due attività:

* [HDInsightHive](data-factory/data-factory-hive-activity.md) attività utilizzando un [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) che viene eseguito un Hive tooaggregate hello oraria cronologia dati richiesta nel livello di area sottostazione toohourly livello di script e inserire in archiviazione di Azure durante hello Azure Processo di flusso Analitica
* [Copia](https://msdn.microsoft.com/library/azure/dn835035.aspx) attività che sposta hello dati aggregati da archiviazione di Azure blob toohello Database SQL di Azure che è stato eseguito il provisioning come parte dell'installazione del modello di soluzione hello.

Hello [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) script per questa attività è ***AggregateDemandHistoryRegion.hql***.

#### <a name="mlscoringregionxpipeline"></a>*MLScoringRegionXPipeline*
Questi [pipeline](data-factory/data-factory-create-pipelines.md) contengono diverse attività e il cui risultato finale è hello con punteggi stime da esperimento di Azure Machine Learning hello associata a questo modello di soluzione. Sono quasi identici ad eccezione del fatto ognuno di essi gestisce solo area diversa di hello che viene eseguita dal RegionID diversi passato nella pipeline ADF hello e script hive hello per ogni area.  
attività Hello contenute in questo sono:

* [HDInsightHive](data-factory/data-factory-hive-activity.md) attività utilizzando un [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) che viene eseguito un Hive tooperform aggregazioni di script e funzionalità di progettazione necessari per hello esperimento di Azure Machine Learning. Hello script Hive per questa attività vengono rispettivi ***PrepareMLInputRegionX.hql***.
* [Copia](https://msdn.microsoft.com/library/azure/dn835035.aspx) attività consente di spostare i risultati di hello dal hello [HDInsightHive](data-factory/data-factory-hive-activity.md) attività tooa singolo servizio di archiviazione Azure blob che è possibile accedere da hello [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) attività.
* [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) attività che chiama l'esperimento di Azure Machine Learning hello conseguente hello comporta l'inserimento in un singolo blob di archiviazione di Azure.

#### <a name="copyscoredresultregionxpipeline"></a>*CopyScoredResultRegionXPipeline*
Questi [pipeline](data-factory/data-factory-create-pipelines.md) contengono una singola attività - un [copia](https://msdn.microsoft.com/library/azure/dn835035.aspx) attività consente di spostare i risultati hello dell'esperimento di Azure Machine Learning hello dal rispettivo hello ***MLScoringRegionXPipeline *** toohello Database SQL di Azure che è stato eseguito il provisioning come parte dell'installazione del modello di soluzione hello.

#### <a name="copyaggdemandpipeline"></a>*CopyAggDemandPipeline*
Questo [pipeline](data-factory/data-factory-create-pipelines.md) contengono una singola attività - un [copia](https://msdn.microsoft.com/library/azure/dn835035.aspx) attività che sposta hello aggregare i dati di richiesta in corso da ***LoadHistoryDemandDataPipeline*** toohello Azure Database SQL che è stato eseguito il provisioning come parte dell'installazione del modello di soluzione hello.

#### <a name="copyregiondatapipeline-copysubstationdatapipeline-copytopologydatapipeline"></a>*CopyRegionDataPipeline, CopySubstationDataPipeline, CopyTopologyDataPipeline*
Questi [pipeline](data-factory/data-factory-create-pipelines.md) contengono una singola attività - un [copia](https://msdn.microsoft.com/library/azure/dn835035.aspx) attività che sposta i dati di riferimento di hello di sottostazione/area/Topologygeo che vengono caricati tooAzure blob di archiviazione come parte della soluzione hello modello installazione toohello Database SQL di Azure che è stato eseguito il provisioning come parte dell'installazione del modello di soluzione hello.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) sperimentare utilizzato per questo modello di soluzione offre una stima hello di richiesta dell'area. esperimento Hello è toohello specifico set di dati utilizzati e pertanto richiedono una sostituzione o modifica dati toohello specifico che viene portati in.

## <a name="monitor-progress"></a>**Monitorare lo stato**
Una volta avviato hello generatore di dati, pipeline hello inizia tooget Alluminosilicato e hello diversi componenti della soluzione avviare qui in azione seguente hello comandi da hello Data Factory. Esistono due modi, che è possibile monitorare pipeline hello.

1. Controllare i dati di hello dall'archiviazione Blob di Azure.

    Uno dei processi di flusso Analitica hello scrive hello in arrivo dati tooblob storage raw. Se fa clic su **archiviazione Blob di Azure** componente della soluzione da hello schermata si soluzione hello distribuita correttamente e quindi fare clic su **aprire** nel riquadro di destra hello, si passerà toohello [Portale di gestione di azure](https://portal.azure.com). Nel portale fare clic su **BLOB**. Nel riquadro successivo di hello, vedrai un elenco di contenitori. Fare clic su **"energysadata"**. Nel riquadro successivo di hello, verrà visualizzato hello **"demandongoing"** cartella. Nella cartella rawdata hello verrà visualizzato le cartelle con i nomi, ad esempio data = 28 / 01 / 2016 e così via. Se queste cartelle, indica che dati non elaborati hello sono stata generata sul computer e archiviati nell'archiviazione blob. Verranno visualizzati file che in tali cartelle devono avere dimensioni limitate in MB.
2. Controllare se hello dati dal Database di SQL Azure.

    Hello ultimo passaggio della pipeline hello è toowrite dati (ad esempio, le stime dall'apprendimento) nel Database SQL. Potrebbe essere toowait un massimo di 2 ore per hello tooappear di dati nel Database SQL. Un modo toomonitor la quantità di dati è disponibile nel Database SQL è tramite [portale di gestione di Azure](https://manage.windowsazure.com/). Nel riquadro di sinistra hello individuare i database di SQL![](media/cortana-analytics-technical-guide-demand-forecast/SQLicon2.png) e farvi clic sopra. Individuare quindi il database (ad esempio demo123456db) e selezionarlo. Nella pagina successiva di hello in **"Connetti tooyour database"** fare clic su **"Query Transact-SQL eseguire nel database SQL"**.

    In questo caso, è possibile fare clic su Nuova Query e query per il numero di righe (ad esempio, "select count da DemandRealHourly) hello" man mano che aumenta il database, hello numero di righe nella tabella hello aumenta.)
3. Controllare i dati di hello dal dashboard di Power BI.

    È possibile impostare Power BI percorso critico dashboard toomonitor hello dati non elaborati in ingresso. Seguire istruzioni hello nella sezione "Dashboard di Power BI" hello.

## <a name="power-bi-dashboard"></a>**Dashboard di Power BI**
### <a name="overview"></a>Panoramica
In questa sezione viene descritto come tooset backup toovisualize dashboard di Power BI i dati in tempo reale da Azure stream analitica (percorso critico), come anche come previsione dei risultati da Azure apprendimento (percorso freddo).

### <a name="setup-hot-path-dashboard"></a>Configurare il dashboard per il percorso critico
Hello alla procedura seguente spiega come dati in tempo reale toovisualize output dal flusso Analitica processi che sono stati generati in fase di distribuzione di soluzioni di hello. Oggetto [Power BI online](http://www.powerbi.com/) account è obbligatorio tooperform hello alla procedura seguente. Se non si ha un account, [crearne uno](https://powerbi.microsoft.com/pricing).

1. Aggiungere l'output di Power BI ad Analisi di flusso di Azure.

   * Sarà necessario istruzioni hello toofollow [Analitica di flusso di Azure e Power BI: un dashboard in tempo reale analitica visibilità in tempo reale del flusso di dati](stream-analytics/stream-analytics-power-bi-dashboard.md) tooset di output di hello del processo Analitica di flusso di Azure come il risparmio di energia Dashboard di Business Intelligence.
   * Individua hello flusso analitica processi nel [portale di gestione di Azure](https://manage.windowsazure.com). il nome del processo di hello Hello deve essere: YourSolutionName + "streamingjob" + numero casuale + "asapbi" (ad esempio demostreamingjob123456asapbi).
   * Aggiungere un output di Power BI per processo ASA hello. Set hello **Alias di Output** come **'PBIoutput'**. Impostare il valore di **Nome del set di dati** e di **Nome tabella** su **"EnergyStreamData"**. Dopo aver aggiunto l'output di hello, fare clic su **"Start"** nella parte inferiore di hello del processo di flusso Analitica hello toostart pagine hello. Verrà visualizzato un messaggio di conferma*simile al seguente*: "L'avvio del processo di Analisi di flusso myteststreamingjob12345asablob è stato completato".
2. Accedi troppo[Power BI online](http://www.powerbi.com)

   * In hello sinistra pannello set di dati nell'area di lavoro, è necessario essere in grado di toosee una nuova visualizzazione di set di dati nel riquadro di sinistra hello di Power BI. Si tratta di flusso di dati che è inseriti da Analitica di flusso di Azure nel passaggio precedente hello hello.
   * Verificare che hello ***visualizzazioni*** riquadro è aperto e viene visualizzato sul lato destro della schermata di hello.
3. Creare il riquadro "Richiesta da Timestamp" hello:

   * Fare clic su set di dati **'EnergyStreamData'** su hello sinistra pannello del set di dati.
   * Fare clic sull'icona **"Grafico a linee"** ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic8.png).
   * Fare clic su 'EnergyStreamData' nel pannello **Campi** .
   * Fare clic su **Timestamp** e verificare che sia visualizzato in "Asse". Fare clic su **"Carica"** e verificare che sia visualizzato in "Valori".
   * Fare clic su **salvare** nella parte superiore di hello e nome report hello come "EnergyStreamDataReport". report di Hello denominato "EnergyStreamDataReport" verrà visualizzato nella sezione report nel Pannello di navigazione hello a sinistra.
   * Fare clic su **"Pin Visual"** ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic6.png) icona nell'angolo superiore destro di questo grafico a linee, una finestra "Pin tooDashboard" potrebbero essere visualizzate per toochoose è un dashboard. Selezionare EnergyStreamDataReport, quindi fare clic su Pin.
   * Posizionare il mouse hello su questo riquadro nel dashboard di hello, fare clic su "edit" icona in alto a destra toochange il titolo "Richiesta da Timestamp"
4. Creare altri riquadri del dashboard in base a set di dati appropriati. visualizzazione di dashboard finale Hello è illustrato di seguito.
     ![](media/cortana-analytics-technical-guide-demand-forecast/PBIFullScreen.png)

### <a name="setup-cold-path-dashboard"></a>Configurare il dashboard per il percorso non critico
Nella pipeline di dati ad accesso sporadico percorso, obiettivo fondamentale di hello è richiesta hello tooget previsione di ogni area. Power BI si connette il database di SQL Azure tooan come origine dati, in cui sono archiviati i risultati della stima hello.

> [!NOTE]
> 1) Richiede alcune ore toocollect sufficientemente previsione dei risultati per il dashboard di hello. Si consiglia di che iniziare questo processo 2-3 ore dopo che pranzo generatore di dati hello. 2) in questo passaggio il prerequisito di hello è toodownload e installare software gratuito hello [Power BI desktop](https://powerbi.microsoft.com/desktop).
>
>

1. Ottenere le credenziali del database hello.

   Sarà necessario **nome del server, nome del database, nome utente e password di database** prima dello spostamento toonext passaggi. Di seguito sono tooguide passaggi hello è come toofind li.

   * Quando la voce **"Database SQL di Azure"** nel diagramma del modello di soluzione diventa verde, selezionarla e quindi fare clic su **"Apri"**. Sarà il portale di gestione tooAzure interattiva e verrà aperta la pagina informazioni database nonché.
   * Nella pagina di hello, è possibile trovare una sezione "Database". Vengono elencati i database di hello che è stato creato. Hello il nome del database deve essere **"Il nome della soluzione + numero casuale + 'db'"** (ad esempio, "mytest12345db").
   * Fare clic su database, nel nuovo che POP out pannello, è possibile trovare il nome del server di database nella parte superiore di hello hello. Il nome del server di database deve essere formato da **"nome della soluzione + numero casuale + "database.windows.net,1433""**, ad esempio "mytest12345.database.windows.net,1433".
   * Il database **username** e **password** sono hello stesso hello nome utente e password registrati in precedenza durante la distribuzione della soluzione hello.
2. Aggiornare l'origine dati hello del percorso freddo hello file Power BI

   * Verificare che è stata installata hello la versione più recente di [Power BI desktop](https://powerbi.microsoft.com/desktop).
   * In hello **"DemandForecastingDataGeneratorv1.0"** cartella scaricato, quindi fare doppio clic su hello **'Power BI Template\DemandForecastPowerBI.pbix'** file. visualizzazioni iniziale Hello sono basate su dati fittizi. **Nota:** se viene visualizzato un errore massaggio, verificare che è stata installata hello la versione più recente di Power BI Desktop.

     Dopo aver aperto, nella parte superiore di hello del file hello, fare clic su **modifica query**. In hello pop out finestra, fare doppio clic su **'Source'** nel riquadro di destra hello.
     ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic1.png)
   * In hello pop out finestra, sostituire **"Server"** e **"Database"** con i nomi di server e database e quindi fare clic su **"OK"**. Nome del server, assicurarsi di specificare la porta 1433 hello (**YourSolutionName.database.windows.net, 1433**). Ignorare i messaggi di avviso hello hello visualizzate.
   * Pop-successivo hello out finestra, si noterà due opzioni nel riquadro di sinistra hello (**Windows** e **Database**). Fare clic su **"Database"**, compilare il **"Username"** e **"Password"** (si tratta di hello username e password specificata quando si hello soluzione distribuita e creato un Database SQL Azure). In ***selezionare quale livello tooapply per queste impostazioni***, controllare l'opzione a livello di database. Fare quindi clic su **"Connetti"**.
   * Dopo aver toohello indietro interattiva di pagina precedente, chiudere la finestra di hello. Nel messaggio popup visualizzato fare clic su **Applica**. Infine, fare clic su hello **salvare** pulsante modifiche hello toosave. Il file di Power BI è ora stabilita connessione toohello server. Se le visualizzazioni sono vuote, assicurarsi che cancellare tutti i dati di hello selezioni hello nella hello visualizzazioni toovisualize facendo clic sull'icona della gomma hello in hello angolo superiore destro di legende hello. Scegliere visualizzazioni hello hello aggiornamento pulsante tooreflect nuovi dati. Inizialmente, viene visualizzata solo dati di inizializzazione hello in visualizzazioni come data factory di hello toorefresh pianificato ogni 3 ore. Dopo 3 ore, si noterà nuove stime riflesse nelle visualizzazioni quando si aggiornano dati hello.
3. (Facoltativo) Pubblicare il dashboard di percorso freddo hello troppo[Power BI online](http://www.powerbi.com/). Si noti che per questo passaggio è necessario un account Power BI o Office 365.

   * Fare clic su **"Pubblica"** e alcuni secondi dopo viene visualizzata una finestra visualizzazione "Pubblicazione tooPower successo BI!" Dopo alcuni secondi viene visualizzato un messaggio di conferma della pubblicazione in Power BI con un segno di spunta verde. Fare clic sul collegamento hello sotto "Demoprediction.pbix Apri in Power BI". toofind indicazioni dettagliate, vedere [pubblicare da Power BI Desktop](https://support.powerbi.com/knowledgebase/articles/461278-publish-from-power-bi-desktop).
   * un nuovo dashboard toocreate: fare clic su hello  **+**  firmare toothe successivo **dashboard** sezione nel riquadro di sinistra hello. Immettere il nome di hello "Richiesta previsione Demo" per il nuovo dashboard.
   * Dopo aver aperto il report hello, fare clic su ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic6.png) toopin tutti i dashboard visualizzazioni tooyour. toofind indicazioni dettagliate, vedere [aggiungere un dashboard di Power BI tooa riquadro da un report](https://support.powerbi.com/knowledgebase/articles/430323-pin-a-tile-to-a-power-bi-dashboard-from-a-report).
     Vai a pagina dashboard toohello e regolare hello dimensioni e la posizione delle visualizzazioni e modificare le relative posizioni. toofind istruzioni dettagliate su come tooedit i riquadri, vedere [modifica un riquadro: ridimensionare, spostare, rinominare, pin, eliminare, aggiungere un collegamento ipertestuale](https://powerbi.microsoft.com/documentation/powerbi-service-edit-a-tile-in-a-dashboard/#rename). Ecco un dashboard di esempio con alcuni tooit aggiunte visualizzazioni freddo percorso.

     ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic7.png)
4. (Facoltativo) Pianificare l'aggiornamento dell'origine dati hello.

   * tooschedule l'aggiornamento dei dati di hello, posizionare il mouse sopra hello **EnergyBPI finale** set di dati, fare clic su ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic3.png) e quindi scegliere **Pianifica aggiornamento**.
     **Nota:** se viene visualizzato un massaggio di avviso, fare clic su **Modifica credenziali** e assicurarsi che le credenziali di database sono hello uguali a quelli descritti nel passaggio 1.

     ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic4.png)
   * Espandere hello **Pianifica aggiornamento** sezione. Attivare l'opzione "Mantieni aggiornati i dati".
   * Pianificare l'aggiornamento di hello in base alle proprie esigenze. toofind ulteriori informazioni, vedere [aggiornamento dei dati in Power BI](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/).

## <a name="how-toodelete-your-solution"></a>**Come toodelete la soluzione**
Assicurarsi di arrestare il generatore di dati di hello quando si utilizza non attivamente soluzione hello come in esecuzione il generatore di dati hello comporta costi elevati. Se si utilizza non elimina soluzione hello. L'eliminazione della soluzione eliminerà tutti i componenti di hello provisioning nella sottoscrizione per la distribuzione di soluzioni di hello. soluzione hello toodelete fare clic sul nome della soluzione nel riquadro sinistro di hello del modello di soluzione hello e fare clic su Elimina.

## <a name="cost-estimation-tools"></a>**Strumenti di stima dei costi**
Hello due sono i seguenti strumenti toohelp disponibili è comprendere meglio il costo totale necessario per l'esecuzione di hello Demand Forecasting per il modello di soluzione di energia nella sottoscrizione:

* [Calcolatore prezzi (online)](https://azure.microsoft.com/pricing/calculator/)
* [Microsoft Azure Cost Estimator Tool (PC desktop)](http://www.microsoft.com/download/details.aspx?id=43376)

## <a name="acknowledgements"></a>**Riconoscimenti**
Autori di questo articolo sono il data scientist Yijing Chen e il software engineer Min Qiu di Microsoft.
