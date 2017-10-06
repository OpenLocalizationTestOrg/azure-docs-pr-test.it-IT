---
title: aaaSearch Analitica di traffico per la ricerca di Azure | Documenti Microsoft
description: Abilitare analitica di traffico di ricerca per un servizio di ricerca cloud ospitato in Microsoft Azure, approfondimenti toounlock su utenti e i dati di ricerca di Azure.
services: search
documentationcenter: 
author: bernitorres
manager: jlembicz
editor: 
ms.assetid: b31d79cf-5924-4522-9276-a1bb5d527b13
ms.service: search
ms.devlang: multiple
ms.workload: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/05/2017
ms.author: betorres
ms.openlocfilehash: 1d16aa63d05c1c3df1bbfbb4f09ac77705ed9d9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-search-traffic-analytics"></a>Analisi del traffico di ricerca
Analisi del traffico di ricerca è un modello per l'implementazione di un ciclo di feedback per il servizio di ricerca. Questo modello viene descritto come toocollect con Application Insights, leader del settore per il monitoraggio di servizi in più piattaforme e i dati necessari hello.

Analisi del traffico di ricerca consente di ottenere visibilità nel servizio di ricerca e informazioni dettagliate su utenti e relativo comportamento. Con i dati relativi a ciò che gli utenti potranno scegliere, è possibile toomake decisioni che consentono di migliorare ulteriormente l'esperienza di ricerca e tooback off quando i risultati di hello sono non previsto.

Ricerca di Azure offre una soluzione di telemetria che integra Azure Application Insights e Power BI tooprovide approfondita di monitoraggio e rilevamento. Poiché l'interazione con ricerca di Azure solo tramite le API, dati di telemetria hello deve essere implementata dagli sviluppatori di hello utilizzo della ricerca, attenendosi alle istruzioni hello in questa pagina.

## <a name="identify-hello-relevant-search-data"></a>Identificare i dati di ricerca rilevanti hello

le metriche di ricerca utili di toohave, è necessario toolog alcuni segnali da utenti hello hello applicazione di ricerca. Questi segnali indicano il contenuto che gli utenti sono interessati a e che essi considerano deve tootheir pertinente.

I segnali necessari per Analisi del traffico di ricerca sono due:

1. Eventi di ricerca generati dagli utenti. Sono interessanti solo le query di ricerca avviate da un utente. Ricerca richieste utilizzate toopopulate facet, contenuto aggiuntivo o qualsiasi informazione interne, non sono importanti e inclinare e definire i risultati.

2. Eventi click generato dall'utente: eseguiti i clic in questo documento, si fa riferimento tooa utente la selezione di un risultato di ricerca particolare restituito da una query di ricerca. Un clic in genere indica che un documento è un risultato rilevante per una specifica query di ricerca.

Collegando gli eventi di ricerca e fare clic con un id di correlazione, è possibile tooanalyze i comportamenti di hello di utenti per l'applicazione. Queste informazioni di ricerca sono tooobtain impossibili con solo i log di traffico di ricerca.

## <a name="how-tooimplement-search-traffic-analytics"></a>Come tooimplement ricerca analitica di traffico

segnali Hello riportato in hello precedente sezione deve essere raccolti da un'applicazione hello ricerca come hello utente interagisce con esso. Application Insights è una soluzione di monitoraggio estensibile, disponibile per più piattaforme, con opzioni di strumentazione flessibili. Utilizzo di Application Insights consente di sfruttare i vantaggi dei report di ricerca di Power BI hello creato da un'analisi dei dati hello toomake ricerca di Azure.

In hello [portale](https://portal.azure.com) pagina per il servizio di ricerca di Azure, pannello di hello Analitica di traffico di ricerca contiene un foglio informativo per questo modello di dati di telemetria. È anche possibile selezionare o creare una risorsa di Application Insights e visualizzare i dati necessari hello, in un'unica posizione.

![Istruzioni per Analisi del traffico di ricerca][1]

### <a name="1-select-an-application-insights-resource"></a>1. Selezionare una risorsa di Application Insights

È necessario tooselect un toouse di risorsa di Application Insights o crearne uno, se non è già disponibile. È possibile utilizzare una risorsa che è già in uso toolog hello richiesto eventi personalizzati.

Quando si crea una nuova risorsa di Application Insights, sono validi tutti i tipi di applicazione per questo scenario. Selezionare hello uno che meglio si adatta piattaforma hello in uso.

Chiave di strumentazione hello è necessaria per la creazione di client di telemetria hello per l'applicazione. È possibile ottenerlo dal dashboard del portale Application Insights hello oppure è possibile ottenere dalla pagina di ricerca traffico Analitica hello, selezione istanza hello da toouse.

### <a name="2-instrument-your-application"></a>2. Instrumentare l'applicazione

Questa fase è dove instrumentare un'applicazione di ricerca personalizzato, utilizzando una risorsa di Application Insights hello il hello creato nel passaggio precedente. Esistono quattro passaggi processo toothis:

**I. Creare un client di telemetria** oggetto hello che invia gli eventi toohello risorsa di Application Insights.

*C#*

    private TelemetryClient telemetryClient = new TelemetryClient();
    telemetryClient.InstrumentationKey = "<YOUR INSTRUMENTATION KEY>";

*JavaScript*

    <script type="text/javascript">var appInsights=window.appInsights||function(config){function r(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},u=document,e=window,o="script",s=u.createElement(o),i,f;s.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js";u.getElementsByTagName(o)[0].parentNode.appendChild(s);try{t.cookie=u.cookie}catch(h){}for(t.queue=[],i=["Event","Exception","Metric","PageView","Trace","Dependency"];i.length;)r("track"+i.pop());return r("setAuthenticatedUserContext"),r("clearAuthenticatedUserContext"),config.disableExceptionTracking||(i="onerror",r("_"+i),f=e[i],e[i]=function(config,r,u,e,o){var s=f&&f(config,r,u,e,o);return s!==!0&&t["_"+i](config,r,u,e,o),s}),t}
    ({
    instrumentationKey: "<YOUR INSTRUMENTATION KEY>"
    });
    window.appInsights=appInsights;
    </script>

Per altri linguaggi e piattaforme, vedere hello completo [elenco](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).

**II. Un ID di ricerca per la correlazione richiesta** ricerca toocorrelate richieste con clic, è necessario toohave un id di correlazione che si riferisce a questi due eventi distinti. Ricerca di Azure offre un ID di ricerca quando viene richiesto con l'intestazione seguente:

*C#*

    // This sample uses hello Azure Search .NET SDK https://www.nuget.org/packages/Microsoft.Azure.Search

    var client = new SearchIndexClient(<ServiceName>, <IndexName>, new SearchCredentials(<QueryKey>)
    var headers = new Dictionary<string, List<string>>() { { "x-ms-azs-return-searchid", new List<string>() { "true" } } };
    var response = await client.Documents.SearchWithHttpMessagesAsync(searchText: searchText, searchParameters: parameters, customHeaders: headers);
    IEnumerable<string> headerValues;
    string searchId = string.Empty;
    if (response.Response.Headers.TryGetValues("x-ms-azs-searchid", out headerValues)){
     searchId = headerValues.FirstOrDefault();
    }

*JavaScript*

    request.setRequestHeader("x-ms-azs-return-searchid", "true");
    request.setRequestHeader("Access-Control-Expose-Headers", "x-ms-azs-searchid");
    var searchId = request.getResponseHeader('x-ms-azs-searchid');

**III. Registrazione degli eventi di ricerca**

Ogni volta che una richiesta di ricerca viene eseguita da un utente, è consigliabile registrare che come un evento di ricerca con hello seguente schema di un evento personalizzato di Application Insights:

**ServiceName**: nome del servizio di ricerca (string) **il SearchId**: identificatore (guid) della query di ricerca hello (disponibile in risposta alla ricerca hello) **IndexName**: indice del servizio di ricerca (string) toobe query **QueryTerms**: i termini di ricerca (stringa) immessi dall'utente hello **ResultCount**: (int) numero di documenti che sono stati restituiti (disponibile in risposta alla ricerca hello)  **ScoringProfile**: nome (string) di hello punteggio profilo utilizzato, se presente

> [!NOTE]
> Numero di richieste per le query generato dall'utente tramite l'aggiunta di $count = true tooyour query di ricerca. Ulteriori informazioni sono disponibili [qui](https://docs.microsoft.com/rest/api/searchservice/search-documents#request).
>

> [!NOTE]
> Tenere presente che le query di ricerca log tooonly generati dagli utenti.
>

*C#*

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search Id>},
    {"IndexName", <index name>},
    {"QueryTerms", <search terms>},
    {"ResultCount", <results count>},
    {"ScoringProfile", <scoring profile used>}
    };
    telemetryClient.TrackEvent("Search", properties);

*JavaScript*

    appInsights.trackEvent("Search", {
    SearchServiceName: <service name>,
    SearchId: <search id>,
    IndexName: <index name>,
    QueryTerms: <search terms>,
    ResultCount: <results count>,
    ScoringProfile: <scoring profile used>
    });

**IV. Registrazione degli eventi clic**

Ogni clic di un utente su un documento è un segnale che deve essere registrato a scopo di analisi delle ricerche. Utilizzare questi eventi di Application Insights eventi personalizzati toolog con hello seguente schema:

**ServiceName**: nome del servizio di ricerca (string) **il SearchId**: identificatore (guid) della query di ricerca correlata hello **DocId**: identificatore documento (string) **posizione** : pagina di risultati di priorità del documento hello nella ricerca hello (int)

> [!NOTE]
> Posizione fa riferimento l'ordine di tipo cardinal toohello nell'applicazione. Si è gratuita tooset questo numero, purché ha sempre hello stesso, tooallow per il confronto.
>

*C#*

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search id>},
    {"ClickedDocId", <clicked document id>},
    {"Rank", <clicked document position>}
    };
    telemetryClient.TrackEvent("Click", properties);

*JavaScript*

    appInsights.TrackEvent("Click", {
        SearchServiceName: <service name>,
        SearchId: <search id>,
        ClickedDocId: <clicked document id>,
        Rank: <clicked document position>
    });

### <a name="3-analyze-with-power-bi-desktop"></a>3. Eseguire l'analisi con Power BI Desktop

Dopo aver instrumentata dell'applicazione e verificare che l'applicazione sia correttamente connesso tooApplication Insights, è possibile utilizzare un modello predefinito creato da ricerca di Azure per Power BI desktop.
Il modello contiene grafici e tabelle che consentono di rendono tooimprove decisioni più informate le prestazioni di ricerca e pertinenza.

tooinstantiate hello Power BI modello di desktop, è necessario tre tipi di informazioni su Application Insights. Questi dati sono reperibile nella pagina di ricerca traffico Analitica hello, quando si seleziona hello risorse toouse

![Dati di Insights di applicazioni nel Pannello di hello Analitica di traffico di ricerca][2]

Metrica inclusa nel modello di hello Power BI desktop:

*   Fare clic su tramite velocità (CTRL): rapporto tra l'utente fa clic su un numero di ricerche totali toohello di documento specifico.
*   Ricerche senza clic: termini delle query principali per i quali non sono registrati clic.
*   Selezionato più documenti: selezionato più documenti da ID in hello ultime 24 ore, 7 giorni e 30 giorni.
*   Coppie di documenti termini comuni: condizioni che comportano hello fa clic sul documento stesso, ordinati in base al clic.
*   Tempo tooclick: clic riportato per volta dalla query di ricerca hello

![Modello di Power BI per la lettura da Application Insights][3]


## <a name="next-steps"></a>Passaggi successivi
Instrumentare i dati di ricerca applicazione tooget potente e utili informazioni sul servizio di ricerca.

Ulteriori informazioni su Application Insights sono disponibili [qui](https://go.microsoft.com/fwlink/?linkid=842905). Visitare Application Insights [pagina dei prezzi](https://azure.microsoft.com/pricing/details/application-insights/) toolearn ulteriori informazioni sulla loro diversi livelli di servizio.

Altre informazioni sulla creazione di report utili Per informazioni dettagliate, vedere [Introduzione a Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/).

<!--Image references-->
[1]: ./media/search-traffic-analytics/AzureSearch-TrafficAnalytics.png
[2]: ./media/search-traffic-analytics/AzureSearch-AppInsightsData.png
[3]: ./media/search-traffic-analytics/AzureSearch-PBITemplate.png
