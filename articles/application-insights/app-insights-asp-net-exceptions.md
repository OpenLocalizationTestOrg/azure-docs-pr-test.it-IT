---
title: aaaDiagnose errori ed eccezioni nei web App con Azure Application Insights | Documenti Microsoft
description: Acquisire le eccezioni da app ASP.NET insieme ai dati di telemetria della richiesta.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d1e98390-3ce4-4d04-9351-144314a42aa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 8930e6d2b29f83ea635c4ecb7afd11fc1d97d085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-exceptions-in-your-web-apps-with-application-insights"></a>Diagnosticare eccezioni nelle app Web con Application Insights
Le eccezioni nell'applicazione Web attiva vengono segnalate da [Application Insights](app-insights-overview.md). È possibile correlare le richieste non riuscite con le eccezioni e gli altri eventi di hello client e server, in modo che consente di individuare rapidamente le cause hello.

## <a name="set-up-exception-reporting"></a>Configurare la creazione di report sulle eccezioni
* le eccezioni toohave segnalate dall'app server:
  * Installare [Application Insights SDK](app-insights-asp-net.md) nel codice dell'app, oppure
  * Server Web IIS: eseguire l'[Agente di Application Insights](app-insights-monitor-performance-live-website-now.md); o
  * App web di Azure: aggiungere hello [estensione Application Insights](app-insights-azure-web-apps.md)
  * Le applicazioni web Java: hello installazione [agente APM Java](app-insights-java-agent.md)
* Installare hello [frammento JavaScript](app-insights-javascript.md) in eccezioni browser toocatch pagine web.
* In alcuni Framework dell'applicazione o con alcune impostazioni, è necessario tootake toocatch alcuni passaggi aggiuntivi altre eccezioni:
  * [Web Form](#web-forms)
  * [MVC](#mvc)
  * [API Web 1.*](#web-api-1)
  * [API Web 2.*](#web-api-2)
  * [WCF](#wcf)

## <a name="diagnosing-exceptions-using-visual-studio"></a>Diagnosticare le eccezioni con Visual Studio
Apri soluzione dell'app hello in Visual Studio toohelp con il debug.

Eseguire app di hello, nel server o nel computer di sviluppo utilizzando F5.

Aprire una finestra di ricerca di Application Insights hello in Visual Studio e impostarlo eventi toodisplay dall'app. Durante il debug, è possibile farlo solo facendo clic sul pulsante di Application Insights hello.

![Fare clic sul progetto hello e Application Insights, scegliere Apri.](./media/app-insights-asp-net-exceptions/34.png)

Si noti che è possibile filtrare le eccezioni di hello report tooshow solo.

*Se non vengono visualizzate eccezioni, vedere la sezione [Acquisizione delle eccezioni](#exceptions).*

Fare clic su un tooshow report eccezione la traccia dello stack.
Fare clic su un riferimento della riga di traccia dello stack hello, file di codice pertinente tooopen hello.  

Nel codice hello, si noti che CodeLens Mostra i dati relativi alle eccezioni di hello:

![Notifica CodeLens di eccezioni.](./media/app-insights-asp-net-exceptions/35.png)

## <a name="diagnosing-failures-using-hello-azure-portal"></a>La diagnosi di errori tramite hello portale di Azure
Panoramica di Application Insights hello dell'app, riquadro errori hello Visualizza i grafici di eccezioni e richieste HTTP non riuscite, insieme a un elenco di hello richiedere gli URL che causano errori più frequenti hello.

![Selezionare Impostazioni, Errori.](./media/app-insights-asp-net-exceptions/012-start.png)

Fare clic su tramite uno di hello Impossibile tipi di eccezione nelle occorrenze di hello elenco tooget tooindividual di eccezione hello, in cui è possibile visualizzare i dettagli di hello e traccia dello stack:

![Selezionare un'istanza di una richiesta non riuscita e con i dettagli dell'eccezione, ottenere tooinstances dell'eccezione hello.](./media/app-insights-asp-net-exceptions/030-req-drill.png)

**In alternativa,** è possibile iniziare dall'elenco di richieste a hello e trovare le eccezioni correlate tooit.

*Se non vengono visualizzate eccezioni, vedere la sezione [Acquisizione delle eccezioni](#exceptions).*


## <a name="custom-tracing-and-log-data"></a>Dati di traccia e di log personalizzati
tooget dati di diagnostica specifici tooyour app, è possibile inserire codice toosend i propri dati di telemetria. Questo nella ricerca diagnostica insieme richiesta hello, visualizzazione della pagina e altri dati raccolti automaticamente.

Sono disponibili diverse opzioni:

* [Trackevent](app-insights-api-custom-events-metrics.md#trackevent) in genere utilizzata per il monitoraggio di modelli di utilizzo, ma hello invia anche dati viene visualizzata sotto gli eventi personalizzati nella ricerca di diagnostica. Gli eventi sono denominati e possono includere proprietà di stringa e metriche numeriche, in base alle quali è possibile [filtrare le ricerche diagnostiche](app-insights-diagnostic-search.md).
* [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) permette di inviare dati più lunghi, ad esempio informazioni POST.
* [TrackException()](#exceptions) invia analisi dello stack. [Altre informazioni sulle eccezioni](#exceptions).
* Se si usa già un framework di registrazione come Log4Net o NLog, è possibile [acquisire tali log](app-insights-asp-net-trace-logs.md) e visualizzarli nella ricerca diagnostica insieme ai dati relativi alle richieste e alle eccezioni.

aprire questi eventi, toosee [ricerca](app-insights-diagnostic-search.md), aprire filtro e quindi scegliere l'evento personalizzato, traccia o eccezione.

![Eseguire il drill-through](./media/app-insights-asp-net-exceptions/viewCustomEvents.png)

> [!NOTE]
> Se l'applicazione genera un grande quantità di dati di telemetria, modulo di campionamento adattivo hello ridurrà automaticamente volume hello inviato toohello portale inviando solo una frazione rappresentativa di eventi. Gli eventi che fanno parte di hello stessa operazione verrà selezionato o deselezionato come gruppo, in modo che è possibile spostarsi tra gli eventi correlati. [Informazioni sul campionamento.](app-insights-sampling.md)
>
>

### <a name="how-toosee-request-post-data"></a>In che modo toosee richiedere dati POST
I dettagli della richiesta non includono dati di hello inviati tooyour app in una chiamata POST. toohave segnalati da questo tipo di dati:

* [Installare SDK hello](app-insights-asp-net.md) nel progetto di applicazione.
* Inserire il codice in toocall l'applicazione [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace). Inviare i dati POST hello nel parametro messaggio hello. Non è un limite di dimensioni consentito toohello, è consigliabile provare dati essenziali di toosend solo hello.
* Quando si analizza una richiesta non riuscita, è possibile trovare le tracce di hello associata.  

![Eseguire il drill-through](./media/app-insights-asp-net-exceptions/060-req-related.png)

## <a name="exceptions"></a> Acquisizione delle eccezioni e dei relativi dati di diagnostica
Inizialmente, non verrà visualizzata nel portale di hello tutte le eccezioni di hello che causano errori nell'applicazione. Si noterà che tutte le eccezioni del browser (se si usa hello [JavaScript SDK](app-insights-javascript.md) nelle pagine web). Ma la maggior parte delle eccezioni di server vengono rilevate da IIS e si dispone di un bit di codice toosee toowrite li.

È possibile:

* **Registrare le eccezioni in modo esplicito** mediante l'inserimento di codice nelle eccezioni hello tooreport gestori di eccezioni.
* **Acquisire automaticamente le eccezioni** configurando il framework di ASP.NET. indispensabile Hello sono diverse per diversi tipi di framework.

## <a name="reporting-exceptions-explicitly"></a>Segnalazione di eccezioni in modo esplicito
Hello più semplice è tooinsert tooTrackException() una chiamata in un gestore di eccezioni.

JavaScript

    try
    { ...
    }
    catch (ex)
    {
      appInsights.trackException(ex, "handler loc",
        {Game: currentGame.Name,
         State: currentGame.State.ToString()});
    }

C#

    var telemetry = new TelemetryClient();
    ...
    try
    { ...
    }
    catch (Exception ex)
    {
       // Set up some properties:
       var properties = new Dictionary <string, string>
         {{"Game", currentGame.Name}};

       var measurements = new Dictionary <string, double>
         {{"Users", currentGame.Users.Count}};

       // Send hello exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }

VB

    Dim telemetry = New TelemetryClient
    ...
    Try
      ...
    Catch ex as Exception
      ' Set up some properties:
      Dim properties = New Dictionary (Of String, String)
      properties.Add("Game", currentGame.Name)

      Dim measurements = New Dictionary (Of String, Double)
      measurements.Add("Users", currentGame.Users.Count)

      ' Send hello exception telemetry:
      telemetry.TrackException(ex, properties, measurements)
    End Try

Hello parametri di proprietà e le misure sono facoltativi, ma sono utili per [filtro e l'aggiunta di](app-insights-diagnostic-search.md) informazioni aggiuntive. Ad esempio, se si dispone di un'app che è possibile eseguire diversi giochi, è possibile trovare tutti hello eccezione report correlati tooa gioco. È possibile aggiungere tutti gli elementi desiderati come dizionario tooeach.

## <a name="browser-exceptions"></a>Eccezioni del browser
Viene segnalata la maggior parte delle eccezioni del browser.

Se la pagina web include i file di script di reti per la distribuzione del contenuto o altri domini, verificare che il tag di script con attributo hello ```crossorigin="anonymous"```, e invia tale server hello [intestazioni CORS](http://enable-cors.org/). In questo modo si tooget una traccia dello stack e i dettagli per le eccezioni JavaScript non gestite da queste risorse.

## <a name="web-forms"></a>Web Form
Per web form, hello modulo HTTP sarà eccezioni hello in grado di toocollect quando non sono configurato con CustomErrors non effettua il reindirizzamento.

Ma se si dispone di reindirizzamenti active, aggiungere hello seguenti righe toohello Application_Error funzione Global.asax.cs. Aggiungere un file Global.asax se non ne esiste già uno.

*C#*

    void Application_Error(object sender, EventArgs e)
    {
      if (HttpContext.Current.IsCustomErrorEnabled && Server.GetLastError  () != null)
      {
         var ai = new TelemetryClient(); // or re-use an existing instance

         ai.TrackException(Server.GetLastError());
      }
    }


## <a name="mvc"></a>MVC
Se hello [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) configurazione `Off`, quindi eccezioni risulteranno disponibili per hello [modulo HTTP](https://msdn.microsoft.com/library/ms178468.aspx) toocollect. Tuttavia, se è `RemoteOnly` (impostazione predefinita), o `On`, verrà cancellata l'eccezione hello e raccogliere tooautomatically non disponibile per Application Insights. Per risolvere questo problema eseguendo l'override di hello [System.Web.Mvc.HandleErrorAttribute classe](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx)e l'applicazione di classe hello sottoposto a override, come illustrato per hello MVC versioni diverse seguente ([github origine](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):

    using System;
    using System.Web.Mvc;
    using Microsoft.ApplicationInsights;

    namespace MVC2App.Controllers
    {
      [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
      public class AiHandleErrorAttribute : HandleErrorAttribute
      {
        public override void OnException(ExceptionContext filterContext)
        {
            if (filterContext != null && filterContext.HttpContext != null && filterContext.Exception != null)
            {
                //If customError is Off, then AI HTTPModule will report hello exception
                if (filterContext.HttpContext.IsCustomErrorEnabled)
                {   //or reuse instance (recommended!). see note above  
                    var ai = new TelemetryClient();
                    ai.TrackException(filterContext.Exception);
                }
            }
            base.OnException(filterContext);
        }
      }
    }

#### <a name="mvc-2"></a>MVC 2
Sostituire l'attributo HandleError hello con il nuovo attributo nel controller.

    namespace MVC2App.Controllers
    {
       [AiHandleError]
       public class HomeController : Controller
       {
    ...

[Esempio](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions)

#### <a name="mvc-3"></a>MVC 3
Registrare `AiHandleErrorAttribute` come filtro globale in Global.asax.cs:

    public class MyMvcApplication : System.Web.HttpApplication
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
         filters.Add(new AiHandleErrorAttribute());
      }
     ...

[Esempio](https://github.com/AppInsightsSamples/Mvc3UnhandledExceptionTelemetry)

#### <a name="mvc-4-mvc5"></a>MVC 4, MVC5
Registrare AiHandleErrorAttribute come filtro globale in FilterConfig.cs:

    public class FilterConfig
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
        // Default replaced with hello override tootrack unhandled exceptions
        filters.Add(new AiHandleErrorAttribute());
      }
    }

[Esempio](https://github.com/AppInsightsSamples/Mvc5UnhandledExceptionTelemetry)

## <a name="web-api-1x"></a>API Web 1.x
Eseguire l'override di System.Web.Http.Filters.ExceptionFilterAttribute:

    using System.Web.Http.Filters;
    using Microsoft.ApplicationInsights;

    namespace WebAPI.App_Start
    {
      public class AiExceptionFilterAttribute : ExceptionFilterAttribute
      {
        public override void OnException(HttpActionExecutedContext actionExecutedContext)
        {
            if (actionExecutedContext != null && actionExecutedContext.Exception != null)
            {  //or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(actionExecutedContext.Exception);    
            }
            base.OnException(actionExecutedContext);
        }
      }
    }

È possibile aggiungere questo controller toospecific attributo sottoposto a override o aggiungerlo Configurazione filtro globale toohello alla classe WebApiConfig hello:

    using System.Web.Http;
    using WebApi1.x.App_Start;

    namespace WebApi1.x
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            config.Routes.MapHttpRoute(name: "DefaultApi", routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional });
            ...
            config.EnableSystemDiagnosticsTracing();

            // Capture exceptions for Application Insights:
            config.Filters.Add(new AiExceptionFilterAttribute());
        }
      }
    }

[Esempio](https://github.com/AppInsightsSamples/WebApi_1.x_UnhandledExceptions)

Esistono un numero di case che non possono gestire i filtri eccezioni hello. ad esempio:

* Eccezioni generate dai costruttori dei controller.
* Eccezioni generate dai gestori di messaggi.
* Eccezioni generate durante il routing.
* Eccezioni generate durante la serializzazione del contenuto della risposta.

## <a name="web-api-2x"></a>API Web 2.x
Aggiungere un'implementazione di IExceptionLogger:

    using System.Web.Http.ExceptionHandling;
    using Microsoft.ApplicationInsights;

    namespace ProductsAppPureWebAPI.App_Start
    {
      public class AiExceptionLogger : ExceptionLogger
      {
        public override void Log(ExceptionLoggerContext context)
        {
            if (context !=null && context.Exception != null)
            {//or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(context.Exception);
            }
            base.Log(context);
        }
      }
    }

Aggiungere questo servizi toohello WebApiConfig:

    using System.Web.Http;
    using System.Web.Http.ExceptionHandling;
    using ProductsAppPureWebAPI.App_Start;

    namespace WebApi2WithMVC
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );
            config.Services.Add(typeof(IExceptionLogger), new AiExceptionLogger());
        }
      }
  }

[Esempio](https://github.com/AppInsightsSamples/WebApi_2.x_UnhandledExceptions)

In alternativa, è possibile:

1. Sostituire hello solo ExceptionHandler con un'implementazione personalizzata di IExceptionHandler. Viene chiamato solo quando il framework di hello è ancora in grado di toochoose la risposta del messaggio toosend (not quando connessione hello viene interrotta, ad esempio)
2. Filtri eccezioni (come descritto nella sezione hello sul controller 1. x API Web sopra) - non è stati chiamati in tutti i casi.

## <a name="wcf"></a>WCF
Aggiungere una classe che estenda Attribute e implementi IErrorHandler e IServiceBehavior.

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.ServiceModel.Description;
    using System.ServiceModel.Dispatcher;
    using System.Web;
    using Microsoft.ApplicationInsights;

    namespace WcfService4.ErrorHandling
    {
      public class AiLogExceptionAttribute : Attribute, IErrorHandler, IServiceBehavior
      {
        public void AddBindingParameters(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase,
            System.Collections.ObjectModel.Collection<ServiceEndpoint> endpoints,
            System.ServiceModel.Channels.BindingParameterCollection bindingParameters)
        {
        }

        public void ApplyDispatchBehavior(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
            foreach (ChannelDispatcher disp in serviceHostBase.ChannelDispatchers)
            {
                disp.ErrorHandlers.Add(this);
            }
        }

        public void Validate(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
        }

        bool IErrorHandler.HandleError(Exception error)
        {//or reuse instance (recommended!). see note above
            var ai = new TelemetryClient();

            ai.TrackException(error);
            return false;
        }

        void IErrorHandler.ProvideFault(Exception error,
            System.ServiceModel.Channels.MessageVersion version,
            ref System.ServiceModel.Channels.Message fault)
        {
        }
      }
    }

Aggiungere le implementazioni del servizio toohello hello attributo:

    namespace WcfService4
    {
        [AiLogException]
        public class Service1 : IService1
        {
         ...

[Esempio](https://github.com/AppInsightsSamples/WCFUnhandledExceptions)

## <a name="exception-performance-counters"></a>Contatori delle prestazioni delle eccezioni
Se dispone di [installato l'agente di Application Insights hello](app-insights-monitor-performance-live-website-now.md) sul server, è possibile ottenere un grafico della frequenza di eccezioni hello, misurata da .NET. Il grafico include le eccezioni .NET gestite e non gestite.

Aprire un pannello Esplora metrica, aggiungere un nuovo grafico e selezionare **Frequenza eccezione**, elencata sotto a Contatori delle prestazioni.

.NET framework di Hello calcola il tasso di hello contando il numero di hello delle eccezioni in un intervallo e dividendo per lunghezza hello dell'intervallo di hello.

Si noti che questo sia diverso dal numero di eccezioni"hello" calcolato dal portale Application Insights hello contando TrackException report. intervalli di campionamento Hello sono diversi e hello SDK non invia report a TrackException per tutte le eccezioni gestite e non gestite.

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="next-steps"></a>Passaggi successivi
* [Monitorare REST, SQL e altre chiamate di toodependencies](app-insights-asp-net-dependencies.md)
* [Monitorare i tempi di caricamento delle pagina, le eccezioni del browser e le chiamate AJAX](app-insights-javascript.md)
* [Monitorare i contatori delle prestazioni](app-insights-performance-counters.md)
