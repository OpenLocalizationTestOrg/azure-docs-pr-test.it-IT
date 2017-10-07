---
title: aaaApplication Insights per servizi Cloud di Azure | Documenti Microsoft
description: Monitorare i ruoli Web e di lavoro in modo efficace con Application Insights
services: application-insights
documentationcenter: 
keywords: WAD2AI, Diagnostica di Azure
author: CFreemanwa
manager: carmonm
editor: alancameronwills
ms.assetid: 5c7a5b34-329e-42b7-9330-9dcbb9ff1f88
ms.service: application-insights
ms.devlang: na
ms.tgt_pltfrm: ibiza
ms.topic: get-started-article
ms.workload: tbd
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: 6956ce423eea1e2cf387bd98250bae32d9501ed0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-azure-cloud-services"></a>Application Insights per Servizi cloud di Azure
Le [app del servizio cloud di Microsoft Azure](https://azure.microsoft.com/services/cloud-services/) possono essere monitorate da [Application Insights][start] in termini di disponibilità, prestazioni, errori e utilizzo combinando i dati degli SDK di Application Insights con i dati di [Diagnostica di Azure](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/azure-diagnostics) provenienti dai servizi cloud. Con il feedback hello che è ottenere sulle prestazioni di hello e l'efficacia dell'app in hello wild, è possibile prendere decisioni informate sulla direzione hello della progettazione hello in ogni ciclo di vita di sviluppo.

![Esempio](./media/app-insights-cloudservices/sample.png)

## <a name="before-you-start"></a>Prima di iniziare
Sono necessari gli elementi seguenti:

* Una sottoscrizione con [Microsoft Azure](http://azure.com). È possibile accedere con un account Microsoft, che in genere si ottiene per Windows, XBox Live o altri servizi cloud Microsoft. 
* Strumenti di Microsoft Azure 2.9 o versione successiva
* Developer Analytics Tools 7.10 o versione successiva

## <a name="quick-start"></a>Avvio rapido
Hello toomonitor modo rapido e semplice che il servizio cloud con Application Insights è toochoose che opzione quando si pubblica il servizio tooAzure.

![Esempio](./media/app-insights-cloudservices/azure-cloud-application-insights.png)

Strumenti di questa opzione l'app in fase di esecuzione, fornendo tutti i dati di telemetria di hello occorre toomonitor richieste, eccezioni e le dipendenze nel ruolo web, nonché sulle prestazioni di contatori dai ruoli di lavoro. Tutte le tracce di diagnostica generate dalla tua app vengono inviate anche tooApplication Insights.

Se non si hanno altre esigenze, non è necessario eseguire altre operazioni. I passaggi successivi prevedono la [visualizzazione delle metriche dall'app](app-insights-metrics-explorer.md), la [query dei dati con Analytics](app-insights-analytics.md) ed eventualmente la configurazione di un [dashboard](app-insights-dashboards.md). È possibile tooset backup [prove di disponibilità](app-insights-monitor-web-app-availability.md) e [aggiungere le pagine web tooyour codice](app-insights-javascript.md) prestazioni toomonitor nel browser hello.

Sono disponibili anche altre opzioni:

* Invio di dati da diversi componenti e le configurazioni della build tooseparate risorse.
* Aggiungere dati di telemetria personalizzati dall'app.

Se tali opzioni sono di interesse tooyou, continuare a leggere.

## <a name="sample-application-instrumented-with-application-insights"></a>Applicazione di esempio instrumentata con Application Insights
Dare un'occhiata [applicazione di esempio](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService) in cui Application Insights viene aggiunto il servizio di cloud tooa con due ruoli di lavoro ospitati in Azure. 

Di seguito indica come tooadapt progetto servizio cloud in hello allo stesso modo.

## <a name="plan-resources-and-resource-groups"></a>Pianificare le risorse e i gruppi di risorse
telemetria Hello dall'app verrà archiviato, analizzato e visualizzato in una risorsa di Azure di tipo Application Insights. 

Ogni risorsa appartiene il gruppo di risorse tooa. Gruppi di risorse vengono utilizzati per la gestione dei costi, per concedere l'accesso, i membri tooteam e toodeploy gli aggiornamenti in una singola transazione coordinata. Ad esempio, è possibile [scrivere un toodeploy script](../azure-resource-manager/resource-group-template-deploy.md) un servizio Cloud di Azure e il relativo monitoraggio risorse un'unica operazione di Application Insights.

### <a name="resources-for-components"></a>Risorse per i componenti
Hello consiglia schema toocreate una risorsa distinta per ogni componente dell'applicazione, vale a dire, ogni ruolo web e ruolo di lavoro. È possibile analizzare separatamente ogni componente, ma è possibile creare un [dashboard](app-insights-dashboards.md) che riunisce grafici chiave hello da tutti i componenti di hello, in modo che sia possibile confrontare e monitorarli insieme. 

Uno schema alternativo è telemetria hello toosend da più di un ruolo toohello stessa risorsa, ma [aggiungere un elemento di dati di telemetria tooeach proprietà dimensione](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer) che identifica il ruolo di origine. In questo schema metrica grafici, ad esempio eccezioni normalmente mostrano un'aggregazione dei conteggi hello da hello ruoli diversi, ma è possibile segmentare grafico hello dall'identificatore di ruolo hello quando richiesto. È inoltre possibile filtrare le ricerche da hello stessa dimensione. Questa procedura alternativa rende tooview un po' più semplice è sempre hello stesso tempo, ma anche provocare confusione toosome tra i ruoli di hello.

Dati di telemetria browser è in genere incluse in hello stessa risorsa, come il ruolo del server web.

Inserire le risorse di Application Insights hello per i diversi componenti hello in un gruppo di risorse. In questo modo è facile toomanage insieme. 

### <a name="separating-development-test-and-production"></a>Separazione di sviluppo, test e produzione
Se si sviluppa eventi personalizzati per la funzionalità successiva mentre la versione precedente di hello è in tempo reale, si desidera toosend hello sviluppo telemetria tooa separato risorsa di Application Insights. In caso contrario sarà toofind disco dati di telemetria test tra tutti hello traffico dal sito di hello in tempo reale.

tooavoid questa situazione, creare risorse separate per ogni configurazione di compilazione o "indicatore" (sviluppo, test, produzione,...) del sistema. Inserire le risorse di hello per ogni configurazione di compilazione in un gruppo di risorse separato. 

toosend hello telemetria toohello delle risorse appropriate, è possibile impostare hello Application Insights SDK in modo che sceglie una chiave di strumentazione diversi a seconda della configurazione della build hello. 

## <a name="create-an-application-insights-resource-for-each-role"></a>Creare una risorsa di Application Insights per ogni ruolo
Se si è deciso di una risorsa distinta per ogni ruolo - toocreate probabilmente di impostare una separata per ogni configurazione di compilazione - ed è più semplice toocreate tutti nel portale Application Insights hello. (Se si creano una grande quantità di risorse, è possibile [automatizzare il processo di hello](app-insights-powershell.md).

1. In hello [portale di Azure][portal], creare una nuova risorsa di Application Insights. Scegliere l'app ASP.NET per il tipo di applicazione. 

    ![Fare clic su Nuovo, Application Insights](./media/app-insights-cloudservices/01-new.png)
2. Si noti che ogni risorsa viene identificata da una chiave di strumentazione Si potrebbe essere necessaria in seguito se si desidera toomanually Configura o verifica configurazione hello di hello SDK.

    ![Fare clic su proprietà, selezionare la chiave hello e premere ctrl + C](./media/app-insights-cloudservices/02-props.png) 

## <a name="set-up-azure-diagnostics-for-each-role"></a>Configurare Diagnostica di Azure per ogni ruolo
Impostare toomonitor questa opzione l'app con Application Insights. Per i ruoli Web offre monitoraggio delle prestazioni, avvisi e diagnostica, oltre all'analisi dell'utilizzo. Per altri ruoli, è possibile cercare e il monitoraggio diagnostica Azure, ad esempio il riavvio, i contatori delle prestazioni e tooSystem.Diagnostics.Trace di chiamate. 

1. In Esplora soluzioni di Visual Studio, sotto &lt;YourCloudService&gt;, ruoli, aprire le proprietà di hello di ogni ruolo.
2. In **configurazione**, impostare **inviare dati di diagnostica tooApplication Insights** e selezionare hello risorsa di Application Insights appropriato creato in precedenza.

Se si è deciso toouse una risorsa di Application Insights distinta per ogni configurazione di compilazione, selezionare innanzitutto configurazione hello.

![Nelle proprietà di hello di ogni ruolo di Azure, configurare Application Insights](./media/app-insights-cloudservices/configure-azure-diagnostics.png)

Questo ha effetto hello di inserimento delle chiavi di strumentazione di Application Insights nel file hello denominati `ServiceConfiguration.*.cscfg`. ([Codice di esempio](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/AzureEmailService/ServiceConfiguration.Cloud.cscfg)).

Se si desidera livello hello toovary di informazioni diagnostiche inviate tooApplication Insights, è possibile farlo [modificando hello `.cscfg` direttamente i file](app-insights-azure-diagnostics.md).

## <a name="sdk"></a>Installare SDK hello in ogni progetto
Questa opzione aggiunge hello possibilità tooadd business personalizzata telemetria tooany ruolo, per un'analisi più dettagliata di come l'applicazione viene utilizzato e vengono eseguite.

In Visual Studio, è possibile configurare hello Application Insights SDK per ogni progetto di app cloud.

1. **I ruoli Web**: fare clic sul progetto hello e scegliere **Configura Application Insights** o **Aggiungi > telemetria di Application Insights**.

2. **Ruoli di lavoro**: 
 * Fare clic sul progetto hello e selezionare **Gestisci pacchetti Nuget**.
 * Aggiungere [Application Insights per server Windows](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/).

    ![Cercare "Application Insights"](./media/app-insights-cloudservices/04-ai-nuget.png)

3. Configurare hello SDK toosend dati toohello risorsa di Application Insights.

    In una funzione di avvio appropriato, impostare la chiave di strumentazione hello dall'impostazione di configurazione hello in file con estensione cscfg hello:
 
    ```C#
   
     TelemetryConfiguration.Active.InstrumentationKey = RoleEnvironment.GetConfigurationSettingValue("APPINSIGHTS_INSTRUMENTATIONKEY");
    ```
   
    Eseguire questa operazione per ogni ruolo nell'applicazione. Vedere gli esempi di hello:
   
   * [Ruolo Web](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Global.asax.cs#L27)
   * [Ruolo di lavoro](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L232)
   * [Per pagine Web](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Views/Shared/_Layout.cshtml#L13) 
4. Set hello Applicationinsights file toobe sempre copiati toohello directory di output. 
   
    (Nel file hello. config, si noterà i messaggi di richiesta è tooplace hello chiave di strumentazione non esiste. Tuttavia, per le applicazioni cloud è migliore tooset dal file con estensione cscfg hello. In questo modo che il ruolo di hello sia identificato correttamente nel portale di hello.)

#### <a name="run-and-publish-hello-app"></a>Eseguire e pubblicare l'applicazione hello
Eseguire l'app e accedere ad Azure. Risorse di Application Insights hello aperto è stato creato e si noterà singoli punti dati visualizzati in [ricerca](app-insights-diagnostic-search.md), e dati aggregati in [metrica Esplora](app-insights-metrics-explorer.md). 

Aggiungere ulteriori dati di telemetria, vedere le sezioni di hello seguenti -, quindi pubblicare app tooget in tempo reale sull'utilizzo e diagnostica commenti e suggerimenti. 

#### <a name="no-data"></a>Dati non visualizzati
* Aprire hello [ricerca] [ diagnostic] riquadro, toosee singoli eventi.
* Utilizzare l'applicazione hello, apertura di pagine diverse in modo che generi alcuni dati di telemetria.
* Attendere alcuni secondi e fare clic su Aggiorna.
* Vedere [Risoluzione dei problemi][qna].

## <a name="view-azure-diagnostic-events"></a>Visualizzare gli eventi di Diagnostica di Azure
In cui hello toofind [diagnostica Azure](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/azure-diagnostics) informazioni in Application Insights:

* I contatori delle prestazioni vengono visualizzati come metriche personalizzate. 
* I registri eventi di Windows vengono visualizzati come tracce ed eventi personalizzati.
* I log applicazioni, i log ETW e gli eventuali log dell'infrastruttura di diagnostica vengono visualizzati come tracce.

i contatori delle prestazioni toosee e i conteggi di eventi, aprire [Esplora metriche](app-insights-metrics-explorer.md) e aggiungere un nuovo grafico:

![Dati di diagnostica di Azure](./media/app-insights-cloudservices/23-wad.png)

Utilizzare [ricerca](app-insights-diagnostic-search.md) o [query Analitica](app-insights-analytics-tour.md) toosearch tra hello vari registri inviati da diagnostica di Azure di traccia. Si supponga, ad esempio, che si dispone di un'eccezione non gestita che ha causato un ruolo toocrash e riciclo. Tali informazioni viene visualizzato in hello applicazione del canale del registro eventi di Windows. È possibile utilizzare ricerca toolook hello errore registro eventi di Windows e visualizzare la traccia dello stack completa hello per hello eccezione. Che consentono di trovare hello principale causa del problema hello.

![Ricerca di dati di diagnostica di Azure](./media/app-insights-cloudservices/25-wad.png)

## <a name="more-telemetry"></a>Altri dati di telemetria
Hello sezioni seguente mostra come tooget ulteriori dati di telemetria da diversi aspetti dell'applicazione.

## <a name="track-requests-from-worker-roles"></a>Tenere traccia delle richieste dai ruoli di lavoro
In ruoli web, hello richieste modulo raccoglie automaticamente i dati sulle richieste HTTP. Vedere hello [esempio MVCWebRole](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole) per esempi di come è possibile ignorare il comportamento dell'insieme di hello predefinito. 

È possibile acquisire le prestazioni di hello dei ruoli tooworker chiamate rilevando li in hello esattamente come le richieste HTTP. In Application Insights, tipo di dati di telemetria richiesta hello misura un'unità di lavoro sul lato server denominato che è possibile programmare in modo indipendente esito positivo o negativo. Mentre le richieste HTTP vengono acquisite automaticamente da hello SDK, è possibile inserire i propri ruoli di tooworker codice tootrack richieste.

Vedere hello due esempio lavoro ruoli tooreport instrumentata richieste: [WorkerRoleA](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/WorkerRoleA) e [WorkerRoleB](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/WorkerRoleB)

## <a name="exceptions"></a>Eccezioni
Vedere [Monitoraggio delle eccezioni in Application Insights](app-insights-asp-net-exceptions.md) per informazioni su come è possibile raccogliere le eccezioni non gestite da diversi tipi di applicazioni Web.

ruolo web di esempio Hello ha controller MVC5 e API Web 2. eccezioni non gestite da hello due Hello vengono acquisite con hello gestori seguenti:

* [AiHandleErrorAttribute](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Telemetry/AiHandleErrorAttribute.cs) impostato [qui](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/App_Start/FilterConfig.cs#L12) per i controller MVC5
* [AiWebApiExceptionLogger](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Telemetry/AiWebApiExceptionLogger.cs) impostato [qui](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/App_Start/WebApiConfig.cs#L25) per i controller Web API 2

Per i ruoli di lavoro, sono disponibili due modi tootrack eccezioni:

* TrackException(ex)
* Se è stato aggiunto il pacchetto NuGet del listener di hello Application Insights traccia, è possibile utilizzare **Trace** toolog eccezioni. [Esempio di codice.](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L107)

## <a name="performance-counters"></a>Contatori delle prestazioni
Hello seguendo i contatori viene raccolti per impostazione predefinita:

    * \Process(??APP_WIN32_PROC??)\% Processor Time
    * \Memory\Available Bytes
    * \.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec
    * \Process(??APP_WIN32_PROC??)\Private Bytes
    * \Process(??APP_WIN32_PROC??)\IO Data Bytes/sec
    * \Processor(_Total)\% Processor Time

Per i ruoli Web vengono raccolti anche i contatori seguenti:

    * \ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec
    * \ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time
    * \ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue

È possibile specificare altri contatori delle prestazioni personalizzati o di Windows modificando ApplicationInsights.config, [come illustrato in questo esempio](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/ApplicationInsights.config#L14).

  ![Contatori delle prestazioni](./media/app-insights-cloudservices/OLfMo2f.png)

## <a name="correlated-telemetry-for-worker-roles"></a>Telemetria correlata per i ruoli di lavoro
È un'esperienza di diagnostica, quando è possibile verificare quali tooa led non è riuscita o una richiesta ad alta latenza. Con i ruoli web, hello che SDK configura automaticamente la correlazione tra relativi dati di telemetria. Per i ruoli di lavoro, è possibile utilizzare un tooset di inizializzatore di dati di telemetria personalizzati un attributo di contesto Operation.Id comune per tutti i tooachieve telemetria hello questo. In questo modo si toosee se è stato causato il problema di latenza/errore hello scadenza tooa dipendenza o il codice, a colpo d'occhio! 

Ecco come:

* Impostare l'Id di correlazione hello in un CallContext come illustrato [qui](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L36). In questo caso, si sta usando hello ID richiesta come id di correlazione hello
* Aggiungere un'implementazione personalizzata di TelemetryInitializer, ID correlazione toohello Operation.Id hello tooset impostata in precedenza. Per un esempio, vedere: [ItemCorrelationTelemetryInitializer](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/Telemetry/ItemCorrelationTelemetryInitializer.cs#L13)
* Aggiungere l'inizializzatore di telemetria personalizzata hello. È possibile farlo nel file Applicationinsights config hello o nel codice come illustrato [qui](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L233)

L'operazione è terminata. esperienza del portale Hello è già collegato toohelp che vedere tutti i dati di telemetria a colpo d'occhio:

![Dati di telemetria correlati](./media/app-insights-cloudservices/bHxuUhd.png)

## <a name="client-telemetry"></a>Telemetria client
[Aggiungere pagine web di JavaScript SDK tooyour hello] [ client] tooget di telemetria basate su browser, ad esempio conteggi delle visualizzazioni di pagina, i tempi di caricamento pagina, eccezioni di script e toolet scrivere telemetria personalizzata negli script di pagina.

## <a name="availability-tests"></a>Test della disponibilità
[Configurare i test web] [ availability] toomake che l'applicazione rimane in tempo reale e reattiva.

## <a name="display-everything-together"></a>Visualizzare tutti gli elementi contemporaneamente
tooget un quadro complessivo del sistema, è possibile visualizzare grafici di monitoraggio insieme in una chiave di hello [dashboard](app-insights-dashboards.md). Ad esempio, è possibile aggiungere richiesta hello e i conteggi di errori di ogni ruolo. 

Se il sistema usa altri servizi di Azure, ad esempio l'analisi di flusso, includere anche i relativi grafici di monitoraggio. 

Se si dispone di una client app per dispositivi mobili, inserire alcuni codice toosend gli eventi personalizzati su operazioni chiave utente e creare un [HockeyApp bridge](app-insights-hockeyapp-bridge-app.md). Creare query in [Analitica](app-insights-analytics.md) toodisplay hello conteggio degli eventi e aggiungerli toohello dashboard.

## <a name="example"></a>Esempio
[esempio Hello](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService) consente di monitorare un servizio che dispone di un ruolo web e i due ruoli di lavoro.

## <a name="exception-method-not-found-on-running-in-azure-cloud-services"></a>Eccezione "metodo non trovato" durante l'esecuzione dei servizi cloud di Azure
È stata eseguita la compilazione per .NET 4.6? La versione 4.6 non è supportata automaticamente nei ruoli dei servizi cloud di Azure. [Installare la versione 4.6 in ogni ruolo](../cloud-services/cloud-services-dotnet-install-dotnet.md) prima di eseguire l'app.

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Passaggi successivi
* [Configurare l'invio di informazioni di diagnostica Azure tooApplication](app-insights-azure-diagnostics.md)
* [Automatizzare la creazione di risorse di Application Insights](app-insights-powershell.md)
* [Automatizzare Diagnostica di Azure](app-insights-powershell-azure-diagnostics.md)
* [Funzioni di Azure](https://github.com/christopheranderson/azure-functions-app-insights-sample)

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[azure]: app-insights-azure.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[netlogs]: app-insights-asp-net-trace-logs.md
[portal]: http://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md 
