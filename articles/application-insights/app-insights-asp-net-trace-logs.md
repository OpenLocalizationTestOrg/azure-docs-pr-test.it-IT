---
title: registri di traccia di .NET aaaExplore in Application Insights
description: Cercare i log generati con Trace, NLog o Log4Net.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0c2a084f-6e71-467b-a6aa-4ab222f17153
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 6bfcd9e5751c3656236d7eb2fc09321740171a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="explore-net-trace-logs-in-application-insights"></a>Esplorare i log di traccia .NET in Application Insights
Se si utilizza NLog, log4Net o Trace per la traccia diagnostica nell'applicazione ASP.NET, è possibile disporre i log inviati troppo[Azure Application Insights][start], in cui è possibile esplorare ed eseguire ricerche essi. I log verranno uniti hello altri dati di telemetria provenienti dall'applicazione, in modo che sia possibile identificare hello tracce associate a ogni richiesta dell'utente di manutenzione e correlarli con altri eventi e i report sulle eccezioni.

> [!NOTE]
> È necessario un modulo di acquisizione registro hello? questo adattatore è utile per i logger terze parti, ma se NLog, log4Net o System.Diagnostics.Trace non sono già in uso, chiamare direttamente [TrackTrace() di Application Insights](app-insights-api-custom-events-metrics.md#tracktrace).
>
>

## <a name="install-logging-on-your-app"></a>Installare la registrazione nell'applicazione
Installare il framework di registrazione scelto nel progetto. Verrà inserita una voce nel file app.config o web.config.

Se si utilizza Trace, è necessario tooadd tooweb.config una voce:

```XML

    <configuration>
     <system.diagnostics>
       <trace autoflush="false" indentsize="4">
         <listeners>
           <add name="myListener"
             type="System.Diagnostics.TextWriterTraceListener"
             initializeData="TextWriterOutput.log" />
           <remove name="Default" />
         </listeners>
       </trace>
     </system.diagnostics>
   </configuration>
```
## <a name="configure-application-insights-toocollect-logs"></a>Configura Application Insights toocollect log
**[Aggiungere Application Insights tooyour progetto](app-insights-asp-net.md)**  se non è che ancora. Verrà visualizzata un'opzione tooinclude hello log agente di raccolta dati.

In alternativa, **configurare Application Insights** facendo clic con il pulsante destro del mouse in Esplora soluzioni. L'opzione hello troppo**configurare la traccia raccolta**.

*Il menu di Application Insights o  l'opzione di raccolta non viene visualizzata?* Vedere [Risoluzione dei problemi](#troubleshooting).

## <a name="manual-installation"></a>Installazione manuale
Utilizzare questo metodo se il tipo di progetto non è supportato dal programma di installazione di hello Application Insights (ad esempio un desktop progetto Windows).

1. Se si intende toouse log4Net o NLog, installarlo nel progetto.
2. In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto e scegliere **Gestisci pacchetti NuGet**.
3. Cercare "Application Insights"
4. Selezionare pacchetto appropriato hello - uno di:

   * Microsoft.ApplicationInsights.TraceListener (toocapture Trace chiamate)
   * Microsoft.ApplicationInsights.EventSourceListener (toocapture EventSource eventi)
   * Microsoft.ApplicationInsights.EtwListener (eventi ETW toocapture)
   * Microsoft.ApplicationInsights.NLogTarget
   * Microsoft.ApplicationInsights.Log4NetAppender

pacchetto NuGet Hello installa gli assembly necessari hello e anche di modificare il file Web. config o App. config.

## <a name="insert-diagnostic-log-calls"></a>Inserire chiamate di log di diagnostica
Se si usa System.Diagnostics.Trace, una tipica chiamata sarà simile alla seguente:

    System.Diagnostics.Trace.TraceWarning("Slow response - database01");

Se si preferisce log4net o NLog:

    logger.Warn("Slow response - database01");

## <a name="using-eventsource-events"></a>Uso degli eventi EventSource
È possibile configurare [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) tooApplication toobe inviati eventi informazioni come le tracce. Installare innanzitutto hello `Microsoft.ApplicationInsights.EventSourceListener` pacchetto NuGet. Modificare quindi `TelemetryModules` sezione di hello [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md) file.

```xml
    <Add Type="Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule, Microsoft.ApplicationInsights.EventSourceListener">
      <Sources>
        <Add Name="MyCompany" Level="Verbose" />
      </Sources>
    </Add>
```

Per ogni origine, è possibile impostare hello seguenti parametri:
 * `Name`Specifica il nome di hello di hello EventSource toocollect.
 * `Level`Specifica hello toocollect livello di registrazione. Può essere uno tra `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.
 * `Keywords`(Facoltativo) specifica il valore intero hello di toouse combinazioni di parole chiave.

## <a name="using-diagnosticsource-events"></a>Uso degli eventi DiagnosticSource
È possibile configurare [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) tooApplication toobe inviati eventi informazioni come le tracce. Installare innanzitutto hello [ `Microsoft.ApplicationInsights.DiagnosticSourceListener` ](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) pacchetto NuGet. Modificare quindi hello `TelemetryModules` sezione di hello [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md) file.

```xml
    <Add Type="Microsoft.ApplicationInsights.DiagnsoticSourceListener.DiagnosticSourceTelemetryModule, Microsoft.ApplicationInsights.DiagnosticSourceListener">
      <Sources>
        <Add Name="MyDiagnosticSourceName" />
      </Sources>
    </Add>
```

Per ogni DiagnosticSource desiderato tootrace, aggiungere una voce con hello `Name` toohello nome del DiagnosticSource del set di attributi.

## <a name="using-etw-events"></a>Uso degli eventi ETW
È possibile configurare toobe eventi ETW inviato tooApplication informazioni come le tracce. Installare innanzitutto hello `Microsoft.ApplicationInsights.EtwCollector` pacchetto NuGet. Modificare quindi `TelemetryModules` sezione di hello [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md) file.

> [!NOTE] 
> Eventi ETW possono essere raccolti solo se hello di hosting processo hello SDK è in esecuzione in un'identità che è un membro di "Performance Log Users" o gli amministratori.

```xml
    <Add Type="Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule, Microsoft.ApplicationInsights.EtwCollector">
      <Sources>
        <Add ProviderName="MyCompanyEventSourceName" Level="Verbose" />
      </Sources>
    </Add>
```

Per ogni origine, è possibile impostare hello seguenti parametri:
 * `ProviderName`è il nome di hello del toocollect di provider ETW hello.
 * `ProviderGuid`Specifica hello GUID di hello toocollect di provider ETW, può essere utilizzato al posto di `ProviderName`.
 * `Level`Imposta hello toocollect livello di registrazione. Può essere uno tra `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.
 * `Keywords`(Facoltativo) set hello intero toouse combinazioni di parole chiave.

## <a name="using-hello-trace-api-directly"></a>Utilizzo diretto di hello traccia API
È possibile chiamare API di traccia di Application Insights hello direttamente. adattatori di registrazione Hello usare questa API.

ad esempio:

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow response - database01");

Un vantaggio TrackTrace è possibile inserire dati relativamente lunghi nel messaggio hello. Ad esempio, è possibile codificare dati POST.

Inoltre, è possibile aggiungere un messaggio tooyour livello di gravità. E, come gli altri dati di telemetria, è possibile aggiungere i valori delle proprietà che è possibile utilizzare il filtro toohelp o ricerca per diversi set di tracce. ad esempio:

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

In tal modo, [ricerca][diagnostic], tooeasily escludere tutti i messaggi hello di un livello di gravità specifico relative tooa particolare database.

## <a name="explore-your-logs"></a>Esplorare i log
Eseguire l'app in modalità debug o distribuirla.

Nel pannello della panoramica dell'app in [portale Application Insights hello][portal], scegliere [ricerca][diagnostic].

![In Application Insights scegliere Cerca](./media/app-insights-asp-net-trace-logs/020-diagnostic-search.png)

![Cerca](./media/app-insights-asp-net-trace-logs/10-diagnostics.png)

Ad esempio, è possibile:

* Filtrare in base alle tracce dei log o agli elementi con proprietà specifiche
* Esaminare un elemento specifico in modo dettagliato
* Trovare altri dati di telemetria relativi toohello stessa richiesta dell'utente (ovvero, con hello stesso OperationId)
* Salvare la configurazione hello di questa pagina come preferito

> [!NOTE]
> **Campionamento.** Se l'applicazione invia una grande quantità di dati e si utilizza hello Application Insights SDK per ASP.NET versione 2.0.0-beta3 o versione successiva, funzionalità di campionamento adattivo hello possono operare e inviare solo una percentuale dei dati di telemetria. [Altre informazioni sul campionamento.](app-insights-sampling.md)
>
>

## <a name="next-steps"></a>Passaggi successivi
[Diagnosticare errori ed eccezioni in ASP.NET][exceptions]

[Altre informazioni sulla ricerca][diagnostic].

## <a name="troubleshooting"></a>Risoluzione dei problemi
### <a name="how-do-i-do-this-for-java"></a>Come procedere per Java?
Hello utilizzare [schede log Java](app-insights-java-trace-logs.md).

### <a name="theres-no-application-insights-option-on-hello-project-context-menu"></a>Non sono disponibili opzioni di Application Insights nel menu di scelta rapida progetto hello
* Verificare che Strumenti Application Insights sia installato nel computer di sviluppo. In Visual Studio, scegliere Strumenti, Estensioni e Aggiornamenti e cercare Strumenti Application Insights. Se non si trova in scheda installati hello, aprire hello Online scheda e installarlo.
* Potrebbe trattarsi di un tipo di progetto non supportato da Strumenti Application Insights. Usare l' [installazione manuale](#manual-installation).

### <a name="no-log-adapter-option-in-hello-configuration-tool"></a>Nessuna opzione adapter log nello strumento di configurazione hello
* È necessario prima registrazione hello tooinstall framework.
* Se si usa System.Diagnostics.Trace, verificare di [aver eseguito la configurazione in `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).
* È stato ottenuto versione più recente di hello di Application Insights? In Visual Studio **strumenti** menu, scegliere **estensioni e aggiornamenti**, aprire hello e **aggiornamenti** scheda. Se gli strumenti per sviluppatori Analitica è presente, fare clic su tooupdate è.

### <a name="emptykey"></a>Viene visualizzato l'errore: "La chiave di strumentazione non può essere vuota"
Sembra che è stato installato hello registrazione pacchetto Nuget adapter senza installare Application Insights.

In Esplora soluzioni fare clic con il pulsante destro del mouse su `ApplicationInsights.config` e scegliere **Aggiorna Application Insights**. Si otterrà una finestra di dialogo Invita toosign in tooAzure e creare una risorsa di Application Insights, o riutilizzare uno esistente. Il problema verrà in tal modo risolto.

### <a name="i-can-see-traces-in-diagnostic-search-but-not-hello-other-events"></a>È possibile vedere tracce in ricerca di diagnostica, ma non hello altri eventi
In alcuni casi può richiedere un po' di tempo per tutti hello tooget di eventi e le richieste tramite pipeline hello.

### <a name="limits"></a>Quanti dati vengono conservati?
Molti fattori influiscono quantità hello dei dati da mantenere. Vedere hello [limiti](app-insights-api-custom-events-metrics.md#limits) sezione della pagina di metriche di hello cliente eventi per ulteriori informazioni. 

### <a name="im-not-seeing-some-of-hello-log-entries-that-i-expect"></a>Non vengono visualizzati alcuni hello voci di log previsti
Se l'applicazione invia una grande quantità di dati e si utilizza hello Application Insights SDK per ASP.NET versione 2.0.0-beta3 o versione successiva, funzionalità di campionamento adattivo hello possono operare e inviare solo una percentuale dei dati di telemetria. [Altre informazioni sul campionamento.](app-insights-sampling.md)

## <a name="add"></a>Passaggi successivi
* [Configurare i test di disponibilità e velocità di risposta][availability]
* [Risoluzione dei problemi][qna]

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[portal]: https://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
