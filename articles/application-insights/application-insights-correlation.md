---
title: Application Insights telemetria correlazione aaaAzure | Documenti Microsoft
description: Correlazione di dati di Application Insights Telemetry
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 3ed8c589d237cac5daceac939ca893b7d81a2967
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="telemetry-correlation-in-application-insights"></a>Correlazione di dati di telemetria in Application Insights

In HelloWorld dei servizi micro, ogni operazione logica richiede lavoro svolto in vari componenti del servizio hello. Ognuno di questi componenti può essere monitorato separatamente tramite [Application Insights](app-insights-overview.md). componente applicazione web di Hello comunica con le credenziali utente di autenticazione provider componente toovalidate e con dati tooget del componente hello API per la visualizzazione. componente API Hello sua può eseguire query sui dati provenienti da altri servizi e utilizzare i componenti di provider di cache e notificare hello componente fatturazione su questa chiamata. Application Insights supporta la correlazione di dati di telemetria distribuita. Consente di toodetect il componente è responsabile per errori o un calo delle prestazioni.

In questo articolo viene illustrato il modello di dati hello usato dai dati di telemetria di Application Insights toocorrelate inviati da più componenti. Tratta i protocolli e le tecniche di propagazione contesto hello. Vengono inoltre illustrate l'implementazione di hello dei concetti di correlazione hello in diversi linguaggi e piattaforme.

## <a name="telemetry-correlation-data-model"></a>Modello di dati per la correlazione di dati di telemetria

Application Insights definisce un [modello di dati](application-insights-data-model.md) per la correlazione di dati di telemetria distribuita. dati di telemetria tooassociate con operazione logica hello, ogni elemento di dati di telemetria ha un campo di contesto denominato `operation_Id`. Questo identificatore viene condiviso da ogni elemento di dati di telemetria in traccia hello distribuita. Se quindi si verifica una perdita di dati di telemetria da un singolo livello, è comunque possibile associare i dati di telemetria segnalati da altri componenti.

Operazione logica distribuite è in genere costituito da un set di operazioni più piccoli - richieste di elaborazione da uno dei componenti di hello. Tali operazioni sono definite dalla [telemetria delle richieste](application-insights-data-model-request-telemetry.md). Ogni telemetria delle richieste è dotata di un proprio `id` che la identifica in modo univoco a livello globale. E tutti i dati di telemetria - tracce, le eccezioni e così via associata a questa richiesta è necessario impostare hello `operation_parentId` valore toohello della richiesta di hello `id`.

Ogni operazione in uscita come componente di tooanother chiamata http rappresentato da [i dati di telemetria](application-insights-data-model-dependency-telemetry.md). Anche la telemetria delle dipendenze dispone di un proprio `id` globalmente univoco. La telemetria delle richieste, avviata dalla chiamata di dipendenza, lo usa come `operation_parentId`.

È possibile compilare una vista hello operazione logica distribuita utilizzando `operation_Id`, `operation_parentId`, e `request.id` con `dependency.id`. Tali campi anche definiscono ordine della causalità hello delle chiamate di telemetria.

Nell'ambiente di servizi micro, le tracce da componenti torni toohello diversi archivi. Ogni componente può avere la propria chiave di strumentazione in Application Insights. dati di telemetria tooget per operazione logica hello, è necessario tooquery dati da ogni archiviazione. Quando il numero di spazio di archiviazione è elevato, è necessario toohave un suggerimento su dove toolook successivo.

Application Insights, modello di dati definisce due campi toosolve questo problema: `request.source` e `dependency.target`. primo campo Hello identifica il componente hello che ha avviato hello dipendenza richiesta e hello secondo identifica il componente ha restituito una risposta hello di chiamata della dipendenza hello.


## <a name="example"></a>Esempio

Esaminiamo un esempio dei prezzi di STOCK applicazione che mostra hello prezzo di mercato corrente di un'azione utilizzando hello API esterna chiamata API di scorte. applicazione dei prezzi AZIONARI Hello dispone di una pagina `Stock page` aperto usando hello client web browser `GET /Home/Stock`. le query dell'applicazione Hello hello API AZIONARIO tramite una chiamata HTTP `GET /api/stock/value`.

È possibile analizzare i dati di telemetria risultanti eseguendo una query:

```
(requests | union dependencies | union pageViews) 
| where operation_Id == "STYz"
| project timestamp, itemType, name, id, operation_ParentId, operation_Id
```

Nota di visualizzazione risultati hello che tutti gli elementi di dati di telemetria condivideranno radice hello `operation_Id`. Quando ajax chiama apportate dalla pagina hello - nuovo id univoco `qJSXU` è toohello assegnati i dati di telemetria e l'id del pageView viene utilizzato come `operation_ParentId`. La richiesta del server usa a sua volta l'ID ajax come `operation_ParentId` e così via.

| itemType   | name                      | id           | operation_ParentId | operation_Id |
|------------|---------------------------|--------------|--------------------|--------------|
| pageView   | Pagina Stock                |              | STYz               | STYz         |
| dipendenza | GET /Home/Stock           | qJSXU        | STYz               | STYz         |
| richiesta    | GET /Home/Stock            | KqKwlrSt9PA = | qJSXU              | STYz         |
| dipendenza | GET /api/stock/value      | bBrf2L7mm2g = | KqKwlrSt9PA =       | STYz         |

Ora quando hello chiamata `GET /api/stock/value` apportate servizio esterno tooan desiderato tooknow hello identità di tale server. È pertanto possibile impostare il campo `dependency.target` in modo appropriato. Quando il servizio esterno hello non supporta il monitoraggio - `target` è impostato il nome host toohello del servizio, ad esempio hello `stock-prices-api.com`. Tuttavia se tale servizio identifica restituendo un oggetto predefinito dell'intestazione HTTP - `target` contiene l'identità del servizio hello che consente di traccia toobuild distribuita Application Insights eseguendo una query su dati di telemetria da tale servizio. 

## <a name="correlation-headers"></a>Intestazioni di correlazione

Stiamo lavorando su proposta RFC per hello [correlazione protocollo HTTP](https://github.com/lmolkova/correlation/blob/master/http_protocol_proposal_v1.md). Questa proposta definisce due intestazioni:

- `Request-Id`eseguire l'id univoco globale di hello della chiamata di hello
- `Correlation-Context`-eseguire raccolta coppie valore/nome hello di proprietà traccia hello distribuita

Hello standard definisce anche due schemi di `Request-Id` generazione - gerarchica e piana. Con schema flat hello, c'è un noto `Id` chiave definita per hello `Correlation-Context` insieme.

Application Insights definisce hello [estensione](https://github.com/lmolkova/correlation/blob/master/http_protocol_proposal_v2.md) per la correlazione hello protocollo HTTP. Usa `Request-Context` coppie nome-valore raccolta hello toopropagate di proprietà utilizzate dalle hello immediato chiamante o chiamato. Application Insights SDK viene utilizzato questo tooset intestazione `dependency.target` e `request.source` campi.

## <a name="open-tracing-and-application-insights"></a>OpenTracing e Application Insights

Ecco come si presentano i modelli di dati di [OpenTracing](http://opentracing.io/) e Application Insights: 

- `request`, `pageView` esegue il mapping troppo**intervallo** con`span.kind = server`
- `dependency`esegue il mapping troppo**intervallo** con`span.kind = client`
- `id`di un `request` e `dependency` esegue il mapping troppo**Span.Id**
- `operation_Id`esegue il mapping troppo**TraceId**
- `operation_ParentId`esegue il mapping troppo**riferimento** di tipo`ChileOf`

Per informazioni sul modello di dati e sui tipi di Application Insights, vedere il [modello di dati](application-insights-data-model.md).

Per le definizioni di OpenTracing, vedere a [specifica](https://github.com/opentracing/specification/blob/master/specification.md) e le [convenzioni semantiche](https://github.com/opentracing/specification/blob/master/semantic_conventions.md).


## <a name="telemetry-correlation-in-net"></a>Correlazione di dati di telemetria in .NET

Nel corso del tempo .NET definiti numerosi modi toocorrelate telemetria e diagnostica registri. È presente `System.Diagnostics.CorrelationManager` consentendo tootrack [LogicalOperationStack e ActivityId](https://msdn.microsoft.com/library/system.diagnostics.correlationmanager.aspx). `System.Diagnostics.Tracing.EventSource`e Windows ETW definire metodo hello [SetCurrentThreadActivityId](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.setcurrentthreadactivityid.aspx). `ILogger` usa gli [ambiti dei log](https://docs.microsoft.com/aspnet/core/fundamentals/logging#log-scopes). WCF e Http collegano la propagazione del contesto "corrente".

Queste soluzioni non consentono tuttavia il supporto automatico della traccia distribuita. `DiagnosticsSource`è toosupport un modo automatico: correlazione di computer. Librerie .NET supportano la diagnostica di origine e consentono la propagazione automatica delle macchine cross del contesto di correlazione hello tramite trasporto hello come http.

Hello [Guida tooActivities](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) nell'origine di diagnostica vengono illustrati concetti fondamentali di hello di tenere traccia delle attività. 

Componenti di base di ASP.NET 2.0 supporta l'estrazione delle intestazioni Http e avvio hello nuova attività. 

`System.Net.HttpClient`versione di partenza `<fill in>` supporta l'inserimento automatico di correlazione hello intestazioni Http e chiamata di hello http come attività di rilevamento.

È disponibile un nuovo modulo Http [Microsoft.AspNet.TelemetryCorrelation](https://www.nuget.org/packages/Microsoft.AspNet.TelemetryCorrelation/) per hello Classic ASP.NET. Questo modulo implementa correlazione di dati di telemetria usando DiagnosticsSource. Avvia l'attività in base alle intestazioni di richiesta in ingresso. Correla inoltre dati di telemetria da hello fasi diverse del processo di elaborazione della richiesta. Anche per i casi di hello quando ogni fase dell'elaborazione di IIS in esecuzione su un thread di gestione diversi.

Versione iniziale di Application Insights SDK `2.4.0-beta1` utilizza telemetria toocollect DiagnosticsSource e attività e associarlo all'attività corrente hello. 

## <a name="next-steps"></a>Passaggi successivi

- [Scrivere dati di telemetria personalizzati](app-insights-api-custom-events-metrics.md)
- Caricare tutti i componenti del microservizio in Application Insights. Controllare le [piattaforme supportate](app-insights-platforms.md).
- Per informazioni sul modello di dati e sui tipi di Application Insights, vedere il [modello di dati](application-insights-data-model.md).
- Informazioni su come troppo[estendere e filtrare i dati di telemetria](app-insights-api-filtering-sampling.md).
