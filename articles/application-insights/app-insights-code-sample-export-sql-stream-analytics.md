---
title: Esportare tooSQL da Azure Application Insights | Documenti Microsoft
description: Esportare in modo continuo tooSQL di dati di Application Insights con flusso Analitica.
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 48903032-2c99-4987-9948-d6e4559b4a63
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/06/2015
ms.author: bwren
ms.openlocfilehash: 58b579499113751a088dc7e66cbec71529773322
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-export-toosql-from-application-insights-using-stream-analytics"></a>Procedura dettagliata: Esportare tooSQL da Application Insights con flusso Analitica
Questo articolo viene illustrato come toomove i dati di telemetria da [Azure Application Insights] [ start] in un database SQL di Azure tramite [esportazione continua] [ export] e [Analitica di flusso di Azure](https://azure.microsoft.com/services/stream-analytics/). 

L'esportazione continua sposta i dati di telemetria in Archiviazione di Azure in formato JSON. Viene l'analisi degli oggetti JSON hello utilizzando Azure flusso Analitica e creare le righe in una tabella di database.

(Più in generale, l'esportazione continua è hello modo toodo la propria analisi dei dati di telemetria hello App Insights tooApplication di trasmissione. È possibile adattare questa toodo di esempio di codice altre operazioni con i dati di telemetria hello esportata, ad esempio aggregazione dei dati.)

Si inizierà con il presupposto hello che si disponga già di app hello da toomonitor.

In questo esempio, si utilizzerà dati della visualizzazione pagina hello, ma hello stesso modello può essere estesa facilmente tooother i tipi di dati, ad esempio gli eventi personalizzati e le eccezioni. 

## <a name="add-application-insights-tooyour-application"></a>Aggiungere l'applicazione tooyour Application Insights
tooget avviato:

1. [Installare Application Insights per le pagine Web](app-insights-javascript.md). 
   
    (In questo esempio sarà dedicata all'elaborazione di dati della visualizzazione pagina dal browser client hello, ma è anche possibile configurare Application Insights per hello sul lato server il [Java](app-insights-java-get-started.md) o [ASP.NET](app-insights-asp-net.md) app e processo di richiesta dipendenze e altri dati di telemetria di server.)
2. Pubblicare l'app e controllare i dati di telemetria visualizzati nella risorsa di Application Insights.

## <a name="create-storage-in-azure"></a>Creare l'archivio in Azure
L'esportazione continua restituisce sempre l'account di archiviazione Azure tooan di dati, pertanto è necessario innanzitutto archiviazione hello toocreate.

1. Creare un account di archiviazione nella sottoscrizione in hello [portale di Azure][portal].
   
    ![Nel portale di Azure scegliere Nuovo, Dati, Archiviazione Selezionare Classica, scegliere Crea. Specificare un nome di archiviazione.](./media/app-insights-code-sample-export-sql-stream-analytics/040-store.png)
2. Creare un contenitore
   
    ![In hello nuova risorsa di archiviazione, selezionare i contenitori, fare clic su riquadro contenitori hello, quindi su Aggiungi](./media/app-insights-code-sample-export-sql-stream-analytics/050-container.png)
3. Chiave di accesso di archiviazione hello copia
   
    È necessario prima tooset hello toohello input flusso analitica servizio.
   
    ![Nel servizio di archiviazione hello, aprire le impostazioni, chiavi e richiedere una copia della chiave di accesso primaria hello](./media/app-insights-code-sample-export-sql-stream-analytics/21-storage-key.png)

## <a name="start-continuous-export-tooazure-storage"></a>Avviare l'esportazione continua tooAzure archiviazione
1. Nel portale di Azure hello, Sfoglia risorsa di Application Insights toohello creata per l'applicazione.
   
    ![Scegliere Sfoglia, Application Insights e quindi l'applicazione](./media/app-insights-code-sample-export-sql-stream-analytics/060-browse.png)
2. Creare un'esportazione continua.
   
    ![Scegliere Impostazioni, Esportazione continua, Aggiungi](./media/app-insights-code-sample-export-sql-stream-analytics/070-export.png)

    Selezionare l'account di archiviazione hello creato in precedenza:

    ![Set di destinazione dell'esportazione hello](./media/app-insights-code-sample-export-sql-stream-analytics/080-add.png)

    Impostare i tipi di evento hello da toosee:

    ![Scegliere i tipi di eventi](./media/app-insights-code-sample-export-sql-stream-analytics/085-types.png)


1. Lasciare che alcuni dati si accumulino. Attendere che gli utenti usino l'applicazione per qualche tempo. Verranno restituiti i dati di telemetria e sarà possibile esaminare i grafici statistici in [Esplora metriche](app-insights-metrics-explorer.md) e i singoli eventi in [Ricerca diagnostica](app-insights-diagnostic-search.md). 
   
    E inoltre dati hello esporterà tooyour archiviazione. 
2. Controllare i dati di hello esportata, nel portale di hello - Scegli **Sfoglia**, selezionare l'account di archiviazione, quindi **contenitori** - o in Visual Studio. In Visual Studio, scegliere **Visualizza/Cloud Explorer**e aprire Azure/Archiviazione. (Se non si dispone di questa opzione, è necessario tooinstall hello Azure SDK: aprire finestra di dialogo Nuovo progetto hello e Visual c# / Cloud / ottenere Microsoft Azure SDK per .NET.)
   
    ![In Visual Studio aprire Esplora server, Azure, Archiviazione](./media/app-insights-code-sample-export-sql-stream-analytics/087-explorer.png)
   
    Prendere nota di parte in comune hello del nome di percorso hello, che viene derivato dalla chiave di nome e la strumentazione dell'applicazione hello. 

gli eventi di Hello vengono scritti i file tooblob in formato JSON. Ogni file può contenere uno o più eventi. In modo desideriamo tooread hello dati dell'evento e filtro campi hello desiderato. Sono disponibili tutti i tipi di operazioni che è possibile farlo con dati hello, ma il piano è oggi database SQL toouse flusso Analitica toomove hello dati tooa. In questo modo sarà facile toorun moltissimi interessanti di query.

## <a name="create-an-azure-sql-database"></a>Creare un database SQL di Azure
Ancora una volta a partire dalla sottoscrizione in [portale di Azure][portal], creare database hello (e un nuovo server, a meno che non si dispone già uno) toowhich si scriverà dati hello.

![Nuovo, Dati, SQL](./media/app-insights-code-sample-export-sql-stream-analytics/090-sql.png)

Verificare che il server di database hello consente l'accesso tooAzure servizi:

![Sfoglia, server, il server, le impostazioni, Firewall, consentire l'accesso a tooAzure](./media/app-insights-code-sample-export-sql-stream-analytics/100-sqlaccess.png)

## <a name="create-a-table-in-azure-sql-db"></a>Creare una tabella nel database SQL di Azure
La connessione a database toohello creato nella sezione precedente di hello con lo strumento di gestione preferiti. In questa procedura dettagliata verranno usati gli [strumenti di gestione di SQL Server](https://msdn.microsoft.com/ms174173.aspx) (SSMS).

![](./media/app-insights-code-sample-export-sql-stream-analytics/31-sql-table.png)

Creare una nuova query ed eseguire hello T-SQL seguente:

```SQL

CREATE TABLE [dbo].[PageViewsTable](
    [pageName] [nvarchar](max) NOT NULL,
    [viewCount] [int] NOT NULL,
    [url] [nvarchar](max) NULL,
    [urlDataPort] [int] NULL,
    [urlDataprotocol] [nvarchar](50) NULL,
    [urlDataHost] [nvarchar](50) NULL,
    [urlDataBase] [nvarchar](50) NULL,
    [urlDataHashTag] [nvarchar](max) NULL,
    [eventTime] [datetime] NOT NULL,
    [isSynthetic] [nvarchar](50) NULL,
    [deviceId] [nvarchar](50) NULL,
    [deviceType] [nvarchar](50) NULL,
    [os] [nvarchar](50) NULL,
    [osVersion] [nvarchar](50) NULL,
    [locale] [nvarchar](50) NULL,
    [userAgent] [nvarchar](max) NULL,
    [browser] [nvarchar](50) NULL,
    [browserVersion] [nvarchar](50) NULL,
    [screenResolution] [nvarchar](50) NULL,
    [sessionId] [nvarchar](max) NULL,
    [sessionIsFirst] [nvarchar](50) NULL,
    [clientIp] [nvarchar](50) NULL,
    [continent] [nvarchar](50) NULL,
    [country] [nvarchar](50) NULL,
    [province] [nvarchar](50) NULL,
    [city] [nvarchar](50) NULL
)

CREATE CLUSTERED INDEX [pvTblIdx] ON [dbo].[PageViewsTable]
(
    [eventTime] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, SORT_IN_TEMPDB = OFF, DROP_EXISTING = OFF, ONLINE = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON)

```

![](./media/app-insights-code-sample-export-sql-stream-analytics/34-create-table.png)

In questo esempio vengono usati i dati delle visualizzazioni pagina. toosee hello altri dati disponibili, esaminare l'output JSON e vedere hello [Esporta modello di dati](app-insights-export-data-model.md).

## <a name="create-an-azure-stream-analytics-instance"></a>Creare un'istanza di analisi di flusso di Azure
Da hello [portale di Azure classico](https://manage.windowsazure.com/), selezionare il servizio di Azure flusso Analitica hello e creare un nuovo processo di flusso Analitica:

![](./media/app-insights-code-sample-export-sql-stream-analytics/37-create-stream-analytics.png)

![](./media/app-insights-code-sample-export-sql-stream-analytics/38-create-stream-analytics-form.png)

Quando viene creato il nuovo processo di hello, espandere i dettagli:

![](./media/app-insights-code-sample-export-sql-stream-analytics/41-sa-job.png)

#### <a name="set-blob-location"></a>Impostare il percorso BLOB
Impostarlo input tootake dal blob di esportazione continua:

![](./media/app-insights-code-sample-export-sql-stream-analytics/42-sa-wizard1.png)

A questo punto è necessario hello chiave di accesso primaria dall'Account di archiviazione, annotati in precedenza. Impostare come hello chiave Account di archiviazione.

![](./media/app-insights-code-sample-export-sql-stream-analytics/46-sa-wizard2.png)

#### <a name="set-path-prefix-pattern"></a>Impostare lo schema prefisso percorso
![](./media/app-insights-code-sample-export-sql-stream-analytics/47-sa-wizard3.png)

È troppo hello tooset che il formato di data**AAAA-MM-GG** (con **trattini**).

Hello modello prefisso del percorso specifica come flusso Analitica Trova file di input hello nel servizio di archiviazione hello. È necessario tooset è toohow toocorrespond esportazione continua archivia dati hello. Impostarlo come segue:

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

Esempio:

* `webapplication27`è il nome di hello della risorsa di Application Insights, hello **tutti in lettere minuscole**. 
* `1234...`è la chiave di strumentazione hello di hello risorsa di Application Insights **con rimossi trattini**. 
* `PageViews`hello tipo di dati desiderato tooanalyze. tipi di Hello disponibili dipendono dal filtro hello impostato nell'esportazione continua. Esaminare altri tipi disponibili di hello toosee di dati esportati hello e vedere hello [Esporta modello di dati](app-insights-export-data-model.md).
* `/{date}/{time}` è uno schema scritto letteralmente.

nome hello tooget iKey della risorsa di Application Insights, aprire Essentials nella relativa pagina di panoramica e aprire le impostazioni.

#### <a name="finish-initial-setup"></a>Completare l'installazione iniziale
Verificare il formato di serializzazione hello:

![Confermare e chiudere la procedura guidata](./media/app-insights-code-sample-export-sql-stream-analytics/48-sa-wizard4.png)

Chiudere la procedura guidata hello e attendere hello toocomplete di programma di installazione.

> [!TIP]
> Utilizzare toocheck funzione di esempio hello che hello percorso di input è stato impostato correttamente. In caso di errore: verifica della presenza dei dati nel servizio di archiviazione per l'intervallo di tempo esempio hello scelto hello. Modifica definizione input hello e controllare impostare account di archiviazione hello, prefisso di percorso e Data formato correttamente.
> 
> 

## <a name="set-query"></a>Impostare la query
Aprire sezione query hello:

![In Analisi di flusso selezionare Query](./media/app-insights-code-sample-export-sql-stream-analytics/51-query.png)

Sostituire query predefinita hello con:

```SQL

    SELECT flat.ArrayValue.name as pageName
    , flat.ArrayValue.count as viewCount
    , flat.ArrayValue.url as url
    , flat.ArrayValue.urlData.port as urlDataPort
    , flat.ArrayValue.urlData.protocol as urlDataprotocol
    , flat.ArrayValue.urlData.host as urlDataHost
    , flat.ArrayValue.urlData.base as urlDataBase
    , flat.ArrayValue.urlData.hashTag as urlDataHashTag
      ,A.context.data.eventTime as eventTime
      ,A.context.data.isSynthetic as isSynthetic
      ,A.context.device.id as deviceId
      ,A.context.device.type as deviceType
      ,A.context.device.os as os
      ,A.context.device.osVersion as osVersion
      ,A.context.device.locale as locale
      ,A.context.device.userAgent as userAgent
      ,A.context.device.browser as browser
      ,A.context.device.browserVersion as browserVersion
      ,A.context.device.screenResolution.value as screenResolution
      ,A.context.session.id as sessionId
      ,A.context.session.isFirst as sessionIsFirst
      ,A.context.location.clientip as clientIp
      ,A.context.location.continent as continent
      ,A.context.location.country as country
      ,A.context.location.province as province
      ,A.context.location.city as city
    INTO
      AIOutput
    FROM AIinput A
    CROSS APPLY GetElements(A.[view]) as flat


```

Si noti che innanzitutto hello alcune proprietà sono specifiche toopage visualizzare i dati. Le esportazioni di altri tipi di dati di telemetria avranno proprietà diverse. Vedere hello [dettagliate di riferimento del modello di dati per i tipi di proprietà hello e valori.](app-insights-export-data-model.md)

## <a name="set-up-output-toodatabase"></a>Impostare toodatabase di output
Selezionare SQL come output di hello.

![In Analisi di flusso selezionare Output](./media/app-insights-code-sample-export-sql-stream-analytics/53-store.png)

Specificare il database SQL di hello.

![Specificare dettagli hello del database](./media/app-insights-code-sample-export-sql-stream-analytics/55-output.png)

Chiudere la procedura guidata hello e attende una notifica che l'output di hello è stata impostata.

## <a name="start-processing"></a>Avviare l'elaborazione
Avviare il processo di hello dalla barra delle azioni hello:

![In Analisi di flusso fare clic su Avvia.](./media/app-insights-code-sample-export-sql-stream-analytics/61-start.png)

È possibile scegliere se l'elaborazione di toostart hello dati a partire da ora o toostart con i dati precedenti. Hello quest'ultimo è utile se si è avuto l'esportazione continua è già in esecuzione per un periodo di tempo.

![In Analisi di flusso fare clic su Avvia.](./media/app-insights-code-sample-export-sql-stream-analytics/63-start.png)

Dopo alcuni minuti, tornare indietro tooSQL strumenti di gestione di Server e guardare hello i dati trasmessi. Usare ad esempio una query simile alla seguente:

    SELECT TOP 100 *
    FROM [dbo].[PageViewsTable]


## <a name="related-articles"></a>Articoli correlati
* [Esportare tooPowerBI tramite flusso Analitica](app-insights-export-power-bi.md)
* [Riferimento per i tipi di proprietà hello e i valori del modello di dati dettagliati.](app-insights-export-data-model.md)
* [Esportazione continua in Application Insights](app-insights-export-telemetry.md)
* [Application Insights](https://azure.microsoft.com/services/application-insights/)

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[export]: app-insights-export-telemetry.md
[metrics]: app-insights-metrics-explorer.md
[portal]: http://portal.azure.com/
[start]: app-insights-overview.md

