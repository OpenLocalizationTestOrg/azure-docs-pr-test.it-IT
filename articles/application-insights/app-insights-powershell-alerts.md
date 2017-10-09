---
title: gli avvisi di tooset Powershell aaaUse in Application Insights | Documenti Microsoft
description: Automatizzare la configurazione di messaggi di posta elettronica tooget Application Insights sulle modifiche di metrica.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 05d6a9e0-77a2-4a35-9052-a7768d23a196
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: d68e5f9511bb4015f59175724bc1a4a04ecf43e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooset-alerts-in-application-insights"></a>Utilizzare PowerShell tooset avvisi in Application Insights
È possibile automatizzare la configurazione di hello di [avvisi](app-insights-alerts.md) in [Application Insights](app-insights-overview.md).

È inoltre possibile [impostare tooautomate webhook l'avviso tooan risposta](../monitoring-and-diagnostics/insights-webhooks-alerts.md).

> [!NOTE]
> Se si desidera toocreate risorse e gli avvisi a hello stesso tempo, prendere in considerazione [utilizzando un modello di gestione risorse di Azure](app-insights-powershell.md).
>
>

## <a name="one-time-setup"></a>Installazione singola
Se non si è mai usato PowerShell con la sottoscrizione di Azure:

Installare il modulo di Azure Powershell hello computer hello in cui si desidera script hello toorun.

* Installare [Installazione guidata piattaforma Web Microsoft (v5 o versione successiva)](http://www.microsoft.com/web/downloads/platform.aspx).
* Utilizzarlo tooinstall Microsoft Azure Powershell

## <a name="connect-tooazure"></a>Connettersi tooAzure
Avviare PowerShell di Azure e [connettere sottoscrizione tooyour](/powershell/azure/overview):

```PowerShell

    Add-AzureAccount
```


## <a name="get-alerts"></a>Ottenere gli avvisi
    Get-AzureAlertRmRule -ResourceGroup "Fabrikam" [-Name "My rule"] [-DetailedOutput]

## <a name="add-alert"></a>Aggiungere un avviso
    Add-AlertRule  -Name "{ALERT NAME}" -Description "{TEXT}" `
     -ResourceGroup "{GROUP NAME}" `
     -ResourceId "/subscriptions/{SUBSCRIPTION ID}/resourcegroups/{GROUP NAME}/providers/microsoft.insights/components/{APP RESOURCE NAME}" `
     -MetricName "{METRIC NAME}" `
     -Operator GreaterThan  `
     -Threshold {NUMBER}   `
     -WindowSize {HH:MM:SS}  `
     [-SendEmailToServiceOwners] `
     [-CustomEmails "EMAIL1@X.COM","EMAIL2@Y.COM" ] `
     -Location "East US" // must be East US at present
     -RuleType Metric



## <a name="example-1"></a>Esempio 1
Invia messaggio se le richieste tooHTTP risposta del server di hello, calcolare la media di 5 minuti, è inferiore a 1 secondo. La risorsa di Application Insights è denominata IceCreamWebApp e si trova nel gruppo di risorse Fabrikam. Sto proprietario hello di hello sottoscrizione di Azure.

Hello GUID è l'ID sottoscrizione hello (non hello chiave di strumentazione di un'applicazione hello).

    Add-AlertRule -Name "slow responses" `
     -Description "email me if hello server responds slowly" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "request.duration" `
     -Operator GreaterThan `
     -Threshold 1 `
     -WindowSize 00:05:00 `
     -SendEmailToServiceOwners `
     -Location "East US" -RuleType Metric

## <a name="example-2"></a>Esempio 2
Un'applicazione in cui usare [trackmetric ()](app-insights-api-custom-events-metrics.md#trackmetric) tooreport una metrica denominata "salesPerHour". Inviare un messaggio di posta elettronica toomy colleghi se "salesPerHour" scende di sotto di 100, calcolare la media di più di 24 ore.

    Add-AlertRule -Name "poor sales" `
     -Description "slow sales alert" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "salesPerHour" `
     -Operator LessThan `
     -Threshold 100 `
     -WindowSize 24:00:00 `
     -CustomEmails "satish@fabrikam.com","lei@fabrikam.com" `
     -Location "East US" -RuleType Metric

Hello stessa regola può essere utilizzato per metrica hello segnalato tramite hello [parametro misura](app-insights-api-custom-events-metrics.md#properties) di rilevamento di un'altra chiamata, ad esempio TrackEvent o trackPageView.

## <a name="metric-names"></a>Nomi delle metriche
| Nome metrica | Nome schermata | Descrizione |
| --- | --- | --- |
| `basicExceptionBrowser.count` |Eccezioni del browser |Numero di eccezioni non rilevate generate nel browser hello. |
| `basicExceptionServer.count` |Eccezioni del server |Numero di eccezioni non gestite generate da app hello |
| `clientPerformance.clientProcess.value` |Tempo di elaborazione client |Tempo trascorso tra la ricezione ultimo byte di hello di un documento fino a quando non viene caricato hello DOM. Le richieste asincrone potrebbero essere ancora in fase di elaborazione. |
| `clientPerformance.networkConnection.value` |Tempo di connessione alla rete per il caricamento della pagina |Browser hello ora accetta tooconnect toohello rete. Può essere 0 se memorizzato nella cache. |
| `clientPerformance.receiveRequest.value` |Tempo per la ricezione della risposta |Tempo trascorso tra l'invio richiesta toostarting tooreceive risposta browser. |
| `clientPerformance.sendRequest.value` |Tempo per l'invio della richiesta |Tempo impiegato dal toosend richiesta del browser. |
| `clientPerformance.total.value` |Tempo di caricamento della pagina del browser |Tempo compreso tra la richiesta utente e il caricamento di DOM, fogli di stile, script e immagini. |
| `performanceCounter.available_bytes.value` |Memoria disponibile |Memoria fisica immediatamente disponibile per l'allocazione a un processo o utilizzabile dal sistema. |
| `performanceCounter.io_data_bytes_per_sec.value` |Velocità di elaborazione I/O |Totale byte al secondo lette e scritte toofiles, rete e dispositivi. |
| `performanceCounter.number_of_exceps_thrown_per_sec.value` |Frequenza di eccezioni |Eccezioni generate al secondo. |
| `performanceCounter.percentage_processor_time.value` |CPU processo |Hello percentuale di tempo di tutti i thread di processo utilizzato da istruzioni del tooexecution hello processore per processo dell'applicazione hello. |
| `performanceCounter.percentage_processor_total.value` |Tempo processore |Percentuale tempo processore hello Hello trascorre in thread non inattivo. |
| `performanceCounter.process_private_bytes.value` |Byte privati processo |Memoria assegnata in modo esclusivo toohello monitorati i processi dell'applicazione. |
| `performanceCounter.request_execution_time.value` |Tempo di esecuzione della richiesta di ASP.NET |Tempo di esecuzione della richiesta più recente di hello. |
| `performanceCounter.requests_in_application_queue.value` |Richieste ASP.NET nella coda di esecuzione |Lunghezza della coda di richieste applicazione hello. |
| `performanceCounter.requests_per_sec.value` |Percentuale di richieste ASP.NET |Frequenza di tutti richieste applicazione toohello al secondo da ASP.NET. |
| `remoteDependencyFailed.durationMetric.count` |Errori di dipendenze |Numero di chiamate non riuscite effettuate dalle risorse di tooexternal hello server applicazioni. |
| `request.duration` |Tempo di risposta del server |Tempo tra la ricezione di una richiesta HTTP e il completamento dell'invio risposta hello. |
| `request.rate` |Frequenza di richieste |Frequenza di applicazione di toohello tutte le richieste al secondo. |
| `requestFailed.count` |Richieste non riuscite |Conteggio delle richieste HTTP per cui è stato restituito un codice di risposta maggiore o uguale a 400 |
| `view.count` |Visualizzazioni pagina |Conteggio delle richieste utente del client per una pagina Web. Il traffico sintetico è filtrato. |
| {nome metrica personalizzato} |{nome metrica} |Il valore della metrica segnalati da [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) o hello [parametro misurazioni di una chiamata di rilevamento](app-insights-api-custom-events-metrics.md#properties). |

le metriche Hello vengono inviate da moduli diversi dati di telemetria:

| Gruppo metrica | Modulo dell'agente di raccolta |
| --- | --- |
| basicExceptionBrowser,<br/>clientPerformance,<br/>view |[JavaScript browser](app-insights-javascript.md) |
| performanceCounter |[Prestazioni](app-insights-configuration-with-applicationinsights-config.md) |
| remoteDependencyFailed |[Dipendenza](app-insights-configuration-with-applicationinsights-config.md) |
| request,<br/>requestFailed |[Richiesta server](app-insights-configuration-with-applicationinsights-config.md) |

## <a name="webhooks"></a>Webhook
È possibile [automatizzare l'avviso tooan risposta](../monitoring-and-diagnostics/insights-webhooks-alerts.md). Azure richiamerà l'indirizzo Web specificato quando viene generato un avviso.

## <a name="see-also"></a>Vedere anche
* [Script tooconfigure Application Insights](app-insights-powershell-script-create-resource.md)
* [Creare risorse Application Insights e test web da modelli](app-insights-powershell.md)
* [Automatizzare l'accoppiamento tra Microsoft Azure Diagnostics tooApplication Insights](app-insights-powershell-azure-diagnostics.md)
* [Automatizzare l'avviso tooan risposta](../monitoring-and-diagnostics/insights-webhooks-alerts.md)
