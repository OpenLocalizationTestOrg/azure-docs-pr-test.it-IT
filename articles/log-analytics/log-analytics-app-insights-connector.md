---
title: i dati dell'app Azure Application Insights aaaView | Documenti Microsoft
description: "È possibile utilizzare i problemi di prestazioni toodiagnose soluzione Application Insights Connector hello e comprendere cosa gli utenti con l'app, il monitoraggio con Application Insights."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 49280cad-3526-43e1-a365-c6a3bf66db52
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: banders
ms.openlocfilehash: 38109337ebbc8970dccb65365ba8284d9cee19a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-connector-solution-preview-in-operations-management-suite-oms"></a>Soluzione Connettore di Application Insights (anteprima) in Operations Management Suite (OMS)

![Simbolo Application Insights](./media/log-analytics-app-insights-connector/app-insights-connector-symbol.png)

Hello soluzione applicazioni Insights Connector consente di diagnosticare problemi di prestazioni e comprendere utenti operazioni con l'app quando viene monitorato con [Application Insights](../application-insights/app-insights-overview.md). Viste di hello telemetria dell'applicazione stessa che gli sviluppatori di vedere in Application Insights sono disponibili in OMS. Tuttavia, quando si integrano le app Application Insights con OMS, la visibilità delle applicazioni aumenta, dal momento che i dati operativi e applicativi si trovano in un'unica posizione. Con hello stesso viste consentono di toocollaborate con gli sviluppatori di app. viste comuni Hello consente di ridurre toodetect ora hello e risolvere i problemi di piattaforma e di applicazione sia.

Quando si utilizza la soluzione hello, è possibile:

- Visualizzare tutte le app Application Insights in un'unica posizione, anche in presenza di sottoscrizioni Azure diverse
- Correlare i dati di infrastruttura ai dati applicativi
- Visualizzare i dati applicativi con prospettive nella ricerca log
- Trasformare tramite pivot dal Log Analitica dati tooyour Application Insights in app hello OMS e portali di Azure

## <a name="connected-sources"></a>Origini connesse

La maggior parte delle altre soluzioni di Log Analitica, a differenza di dati non raccolti per Application Insights Connector hello dagli agenti. Tutti i dati utilizzati dalla soluzione hello proviene direttamente da Azure.

| Origine connessa | Supportato | Descrizione |
| --- | --- | --- |
| [Agenti di Windows](log-analytics-windows-agents.md) | No | soluzione Hello non raccoglie informazioni dagli agenti di Windows. |
| [Agenti Linux](log-analytics-linux-agents.md) | No | soluzione Hello non raccoglie informazioni dagli agenti Linux. |
| [Gruppo di gestione SCOM](log-analytics-om-agents.md) | No | soluzione Hello non raccoglie informazioni dagli agenti in un gruppo di gestione SCOM connesso. |
| [Account di archiviazione di Azure](log-analytics-azure-storage.md) | No | soluzione di Hello non non informazioni sulla raccolta dall'archiviazione di Azure. |

## <a name="prerequisites"></a>Prerequisiti

- tooaccess informazioni di Application Insights Connector, è necessario avere una sottoscrizione di Azure
- È necessario disporre di almeno una risorsa Application Insights configurata.
- È necessario essere hello proprietario o collaboratore della risorsa di Application Insights hello.

## <a name="configuration"></a>Configurazione

1. Abilitare soluzioni Azure Web App Analitica hello hello [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ApplicationInsights?tab=Overview) o tramite il processo di hello descritto in [soluzioni aggiungere Log Analitica da hello Solutions Gallery](log-analytics-add-solutions.md).
2. Nel portale OMS hello, fare clic su **impostazioni** &gt; **dati** &gt; **Application Insights**.
3. In **Selezionare una sottoscrizione**, selezionare una sottoscrizione con risorse Application Insights e quindi, in **Nome applicazione**, selezionare una o più applicazioni.
4. Fare clic su **Salva**.

In circa 30 minuti, i dati diventano disponibili e hello Application Insights riquadro viene aggiornata con i dati, ad esempio hello seguente immagine:

![Riquadro Application Insights](./media/log-analytics-app-insights-connector/app-insights-tile.png)

Altri punti tookeep presente:

- È possibile collegare solo l'area di lavoro OMS tooone App Application Insights.
- È possibile collegare solo [risorse Standard o Premium Application Insights](https://azure.microsoft.com/pricing/details/application-insights) tooOMS Analitica di Log. Tuttavia, è possibile utilizzare il livello gratuito di hello del Log Analitica.

## <a name="management-packs"></a>Management Pack

Questa soluzione non installa alcun Management Pack nei gruppi di gestione connessi.

## <a name="use-hello-solution"></a>Utilizzare una soluzione hello

Hello nelle sezioni seguenti descrivono come utilizzare i pannelli hello nella tooview dashboard di Application Insights hello e interagire con i dati dalle app.

### <a name="view-application-insights-connector-information"></a>Visualizzare le informazioni di Connettore di Application Insights

Fare clic su hello **Application Insights** riquadro tooopen hello **Application Insights** hello toosee dashboard seguenti pannelli.

![Dashboard Application Insights](./media/log-analytics-app-insights-connector/app-insights-dash01.png)

![Dashboard Application Insights](./media/log-analytics-app-insights-connector/app-insights-dash02.png)

dashboard Hello include pannelli hello illustrati nella tabella hello. Ogni pannello elenca backup too10 elementi corrispondenti ai criteri del pannello per hello specificato intervallo di ambito e tempo. È possibile eseguire una ricerca di log che restituisce tutti i record quando si fa clic **tutti** nella parte inferiore di hello del pannello hello o quando si fa clic su intestazione pannello hello.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

| **Colonna** | **Descrizione** |
| --- | --- |
| Applications - Number of applications (Applicazioni - Numero di applicazioni) | Mostra il numero di hello di applicazioni in risorse dell'applicazione. Anche gli elenchi di applicazione i nomi e per ognuno, hello conteggio di record di applicazione. Fare clic su una ricerca di log per hello numero toorun<code>Type=ApplicationInsights &#124; measure sum(SampledCount) by ApplicationName</code> <br><br>  Fare clic su un toorun nome applicazione una ricerca di log per un'applicazione hello che mostra i record di applicazione per ogni host, i record in base al tipo di dati di telemetria e tutti i dati dal tipo (basato su hello ultimo giorno). |
| Data Volume – Hosts sending data (Volume dati - Host che inviano dati) | Mostra il numero di hello degli host di computer che inviano dati. Elenca anche gli host computer e il numero di record per ogni host. Fare clic su una ricerca di log per hello numero toorun<code>Type=ApplicationInsights &#124; measure sum(SampledCount) by Host</code> <br><br> Fare clic su un toorun nome computer di una ricerca di log per l'host di hello che mostra i record di applicazione per ogni host, i record in base al tipo di dati di telemetria e tutti i dati dal tipo (basato su hello ultimo giorno). |
| Availability – Webtest results (Disponibilità - Risultati test Web) | Mostra un grafico ad anello per i risultati dei test Web, con indicazione di esito positivo o negativo. Fare clic su una ricerca di log per hello grafico toorun<code>Type=ApplicationInsights TelemetryType=Availability &#124; measure sum(SampledCount) by AvailabilityResult</code> <br><br> Risultati mostrano il numero di hello di errori per tutti i test e passate. Mostra tutte le app Web con traffico per hello ultimo minuto. Fare clic su un tooview nome applicazione, una ricerca di log che mostra i dettagli dei test web non riuscito. |
| Server Requests – Requests per hour (Richieste server - Richieste per ora) | Mostra un grafico a linee di hello richieste server ora per diverse applicazioni. Passare il mouse su una riga hello grafico toosee hello prime 3 applicazioni la ricezione di richieste per un punto nel tempo. Mostra anche un elenco di applicazioni hello riceve le richieste e il numero di hello di richieste per il periodo di hello selezionato. <br><br>Fare clic su una ricerca di log per hello grafico toorun <code>Type=ApplicationInsights TelemetryType=Request &#124; measure sum(SampledCount) by ApplicationName interval 1hour</code> che mostra un grafico a linee più dettagliato di hello richieste server ora per diverse applicazioni. <br><br> Fare clic su una ricerca di log per un'applicazione hello elenco toorun <code>Type=ApplicationInsights  ApplicationName=yourapplicationname  TelemetryType=Request</code> che mostra un elenco delle richieste e grafici per le richieste nel corso della durata di tempo e richiedere un elenco di richiesta di codici di risposta.   |
| Failures – Failed requests per hour (Errori - Richieste non riuscite per ora) | Mostra un grafico a linee di richieste di applicazione non riuscite per ora. Passare il mouse su hello grafico toosee hello prime 3 applicazioni con le richieste non riuscite per un punto nel tempo. Mostra anche un elenco di applicazioni con il numero di hello delle richieste non riuscite per ognuno. Fare clic su una ricerca di log per hello grafico toorun <code>Type=ApplicationInsights TelemetryType=Request  RequestSuccess = false &#124; measure sum(SampledCount) by ApplicationName interval 1hour</code> che mostra un grafico a linee più dettagliato delle richieste di applicazioni non riuscita. <br><br>Fare clic su una ricerca di log per un elemento in hello elenco toorun <code>Type=ApplicationInsights ApplicationName=yourapplicationname TelemetryType=Request  RequestSuccess=false</code> che Mostra richieste non riuscite, grafici per richieste non riuscite su richiesta e tempo di durata e un elenco dei codici di risposta richiesta non riuscita. |
| Exceptions – Exceptions per hour (Eccezioni - Eccezioni per ora) | Mostra un grafico a linee di eccezioni per ora. Passare il mouse su hello grafico toosee hello prime 3 applicazioni con eccezioni per un punto nel tempo. Mostra anche un elenco di applicazioni con il numero di hello di eccezioni per ognuno. Fare clic su una ricerca di log per hello grafico toorun <code>Type=ApplicationInsights TelemetryType=Exception &#124; measure sum(SampledCount) by ApplicationName interval 1hour</code> che mostra un grafico di collegamento più dettagliato delle eccezioni. <br><br>Fare clic su una ricerca di log per un elemento in hello elenco toorun <code>Type=ApplicationInsights  ApplicationName=yourapplicationname TelemetryType=Exception</code> che mostra un elenco di eccezioni, i grafici per le eccezioni richieste non riuscite e tempo e un elenco di tipi di eccezione.  |

### <a name="view-hello-application-insights-perspective-with-log-search"></a>Visualizzare il punto di vista di hello Application Insights con ricerca di log

Quando si fa clic su qualsiasi elemento nel dashboard di hello, viene visualizzato un punto di vista di Application Insights nella ricerca. prospettiva di Hello fornisce una visualizzazione estesa, in base al tipo di dati di telemetria hello selezionati. Il contenuto della visualizzazione varia pertanto in base a tipi di telemetria diversi.

Quando si fa clic in un punto qualsiasi nel Pannello di applicazioni hello, vedrai predefinito hello **applicazioni** prospettiva.

![Prospettiva Applications (Applicazioni) di Application Insights](./media/log-analytics-app-insights-connector/applications-blade-drill-search.png)

prospettiva Hello Mostra una panoramica di un'applicazione hello selezionato.

Hello **disponibilità** blade viene illustrata una visualizzazione di prospettiva diversa in cui è possibile visualizzare i risultati del test web e le richieste non riuscite correlate.

![Prospettiva Availability di Application Insights](./media/log-analytics-app-insights-connector/availability-blade-drill-search.png)

Quando fa clic su un punto qualsiasi in hello **richieste Server** o **errori** pannelli, prospettiva hello componenti modificare toogive è una visualizzazione che toorequests correlati.

![Pannello Failures (Errori) di Application Insights](./media/log-analytics-app-insights-connector/server-requests-failures-drill-search.png)

Quando fa clic su un punto qualsiasi in hello **eccezioni** pannello, vedrai una visualizzazione personalizzata in base tooexceptions.

![Pannello Exceptions (Eccezioni) di Application Insights](./media/log-analytics-app-insights-connector/exceptions-blade-drill-search.png)

Indipendentemente dal fatto se si fa clic su un elemento uno hello **Application Insights Connector** dashboard, all'interno di hello **ricerca** pagina stessa, qualsiasi query che restituisce dati di Application Insights mostrano hello Prospettiva di Application Insights. Se vengono visualizzati i dati di Application Insights, ad esempio un **&#42;** query illustra anche scheda prospettiva hello come hello seguente immagine:

![Application Insights ](./media/log-analytics-app-insights-connector/app-insights-search.png)

A seconda delle query di ricerca hello vengono aggiornati i componenti di prospettiva. Ciò significa che è possibile filtrare i risultati di hello utilizzando qualsiasi campo di ricerca che fornisce hello toosee possibilità hello dati da:

- Tutte le applicazioni
- Una singola applicazione selezionata
- Un gruppo di applicazioni

### <a name="pivot-tooan-app-in-hello-azure-portal"></a>App pivot tooan hello portale di Azure

Pannelli di Application Insights Connector sono progettate tooenable toopivot toohello selezionato app Application Insights *quando si usa il portale di OMS hello*. È possibile utilizzare la soluzione hello come piattaforma di monitoraggio ad alto livello che consente di risolvere un'app. Quando viene visualizzato un potenziale problema in tutte le applicazioni connessione, è possibile entrambi drill al suo interno in ricerca OMS, oppure è possibile trasformare tramite pivot direttamente app Application Insights toohello.

toopivot, fare clic sui puntini di sospensione hello (**...** ) che viene visualizzato all'estremità hello di ogni riga e selezionare **aperto in Application Insights**.

>[!NOTE]
>**Apri in Application Insights** non è disponibile nel portale di Azure hello.

![Apri in Application Insights](./media/log-analytics-app-insights-connector/open-in-app-insights.png)

### <a name="sample-corrected-data"></a>Dati con correzione di campionamento

Application Insights fornisce  *[campionamento correzione](../application-insights/app-insights-sampling.md)*  toohelp ridurre il traffico di dati di telemetria. Quando si abilita il campionamento nell'app di Application Insights, si ottiene un numero ridotto di voci archiviate in Application Insights e in OMS. Mentre la coerenza dei dati viene mantenuta nella hello **Application Insights Connector** pagina e prospettive, è necessario correggere manualmente i dati campionati per le query personalizzate.

Di seguito è riportato un esempio di correzione di campionamento in una query di ricerca log:

```
Type=ApplicationInsights | measure sum(SampledCount) by TelemetryType
```

Hello **campionate conteggio** campo è presente in tutte le voci e numero di punti dati che rappresenta la voce hello di hello Mostra. Se si attiva il campionamento per l'app di Application Insights, **SampledCount** è maggiore di 1. numero effettivo di voci che l'applicazione genera, hello somma di hello toocount **campionate conteggio** campi.

Campionamento interessa solo hello numero totale di voci che l'applicazione genera l'errore. Non è necessario toocorrect di campionamento per quali campi metrica **RequestDuration** o **AvailabilityDuration** perché tali campi mostrano la media hello per le voci rappresentate.

## <a name="input-data"></a>Dati di input

soluzione Hello riceve hello seguenti tipi di dati di telemetria di dati da app connesse Application Insights:

- Disponibilità
- Eccezioni
- Requests
- Visualizzazioni di pagina: per l'area di lavoro di tooreceive visualizzazioni di pagina, è necessario configurare il toocollect App tali informazioni. Per altre informazioni, vedere [PageViews](../application-insights/app-insights-api-custom-events-metrics.md#page-views).
- Eventi personalizzati e per l'area di lavoro tooreceive gli eventi personalizzati, è necessario configurare il toocollect App tali informazioni. Per altre informazioni, vedere [TrackEvent](../application-insights/app-insights-api-custom-events-metrics.md#trackevent).

I dati vengono ricevuti da OMS da Application Insights appena disponibili.

## <a name="output-data"></a>Dati di output

Viene creato un record con un *tipo* di *ApplicationInsights* per ogni tipo di dati di input. Record di ApplicationInsights hanno le proprietà visualizzate in hello le sezioni seguenti:

### <a name="generic-fields"></a>Campi generici

| Proprietà | Descrizione |
| --- | --- |
| Tipo | ApplicationInsights |
| ClientIP |   |
| TimeGenerated | Ora del record di hello |
| ApplicationId | Chiave di strumentazione dell'applicazione di Application Insights hello |
| ApplicationName | Nome dell'app Application Insights hello |
| RoleInstance | ID dell'host server |
| DeviceType | Dispositivo client |
| ScreenResolution |   |
| Continent | In cui ha origine la richiesta hello continente |
| Paese | Paese in cui ha origine la richiesta hello |
| Province | Provincia, stato o delle impostazioni locali in cui hello richiesta ha avuto origine |
| city | Città o il paese in cui ha origine la richiesta hello |
| isSynthetic | Indica se la richiesta hello è stata creata da un utente o dal metodo automatizzato. True = generata dall'utente o false = metodo automatizzato |
| SamplingRate | Percentuale di telemetria generato da hello SDK tooportal inviato. L'intervallo è 0,0-100,0. |
| SampledCount | 100/(SamplingRate). Ad esempio, 4 =&gt; 25% |
| IsAuthenticated | True o false |
| OperationID | Gli elementi che hanno lo stesso ID operazione vengono visualizzate come elementi correlati nel portale di hello hello. In genere ID di richiesta di hello |
| ParentOperationID | ID dell'operazione di hello padre |
| OperationName |   |
| SessionId | GUID toouniquely identificare di sessione hello in cui è stato creato richiesta hello |
| SourceSystem | ApplicationInsights |

### <a name="availability-specific-fields"></a>Campi specifici di disponibilità

| Proprietà | Descrizione |
| --- | --- |
| TelemetryType | Disponibilità |
| AvailabilityTestName | Nome del test web hello |
| AvailabilityRunLocation | Origine geografica della richiesta HTTP |
| AvailabilityResult | Indica il risultato positivo hello del test web hello |
| AvailabilityMessage | messaggio Hello collegati i test web toohello |
| AvailabilityCount | 100/(SamplingRate). Ad esempio, 4 =&gt; 25% |
| DataSizeMetricValue | 1,0 o 0,0 |
| DataSizeMetricValue | 100/(SamplingRate). Ad esempio, 4 =&gt; 25% |
| AvailabilityDuration | Tempo, espresso in millisecondi, di durata del test web hello |
| AvailabilityDurationCount | 100/(SamplingRate). Ad esempio, 4 =&gt; 25% |
| AvailabilityValue |   |
| AvailabilityMetricCount |   |
| AvailabilityTestId | GUID univoco per il test web hello |
| AvailabilityTimestamp | Timestamp preciso del test di disponibilità hello |
| AvailabilityDurationMin | Per i record campionati, questo campo Mostra durata del test web minimo di hello (millisecondi) per i punti dati hello rappresentato |
| AvailabilityDurationMax | Per i record campionati, questo campo Mostra hello web massima durata del test (millisecondi) per i punti dati hello rappresentato |
| AvailabilityDurationStdDev | Per i record campionati, questo campo indica la deviazione standard di hello tra tutte le durate di test web (in millisecondi) per i punti dati hello rappresentato |
| AvailabilityMin |   |
| AvailabilityMax |   |
| AvailabilityStdDev | &nbsp;  |

### <a name="exception-specific-fields"></a>Campi specifici di eccezione

| Tipo | ApplicationInsights |
| --- | --- |
| TelemetryType | Eccezione |
| ExceptionType | Tipo di eccezione hello |
| ExceptionMethod | metodo Hello che crea eccezione hello |
| ExceptionAssembly | Assembly include il framework di hello e versione nonché il token di chiave pubblica di hello |
| ExceptionGroup | Tipo di eccezione hello |
| ExceptionHandledAt | Indica il livello hello hello eccezione gestita |
| ExceptionCount | 100/(SamplingRate). Ad esempio, 4 =&gt; 25% |
| ExceptionMessage | Messaggio di eccezione hello |
| ExceptionStack | Stack completo dell'eccezione hello |
| ExceptionHasStack | True se l'eccezione include uno stack |



### <a name="request-specific-fields"></a>Campi specifici di richiesta

| Proprietà | Descrizione |
| --- | --- |
| Tipo | ApplicationInsights |
| TelemetryType | Richiesta |
| ResponseCode | Tooclient risposta inviata HTTP |
| RequestSuccess | Indica l'esito positivo o negativo. True o false. |
| RequestID | ID toouniquely identificare richiesta hello |
| RequestName | GET/POST + base URL |
| RequestDuration | Tempo, espresso in secondi della durata richiesta hello |
| URL | URL della richiesta di hello escluso host |
| Host | Host del server Web |
| URLBase | URL completo della richiesta di hello |
| ApplicationProtocol | Tipo di protocollo utilizzato dall'applicazione hello |
| RequestCount | 100/(SamplingRate). Ad esempio, 4 =&gt; 25% |
| RequestDurationCount | 100/(SamplingRate). Ad esempio, 4 =&gt; 25% |
| RequestDurationMin | Per i record campionati, questo campo Mostra durata minima richiesta di hello (millisecondi) per i punti dati hello rappresentato. |
| RequestDurationMax | Per i record campionati, questo campo Mostra durata massima della richiesta di hello (millisecondi) per i punti dati hello rappresentato |
| RequestDurationStdDev | Per i record campionati, questo campo indica la deviazione standard di hello tra tutte le durate richiesta (in millisecondi) per i punti dati hello rappresentato |

## <a name="sample-log-searches"></a>Ricerche di log di esempio

Questa soluzione non dispone di un set di esempio illustrato nel dashboard di hello ricerche nei log. Tuttavia, query di ricerca di log di esempio con le descrizioni vengono visualizzate in hello [informazioni di visualizzazione Application Insights Connector](#view-application-insights-connector-information) sezione.

## <a name="next-steps"></a>Passaggi successivi

- Utilizzare [ricerca nei Log](log-analytics-log-searches.md) tooview informazioni dettagliate per le applicazioni di Application Insights.
