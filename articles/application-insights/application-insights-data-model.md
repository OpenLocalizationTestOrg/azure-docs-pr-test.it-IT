---
title: Modello di dati di Azure Application Insights Telemetry | Microsoft Docs
description: Panoramica sul modello di dati di Application Insights
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
ms.openlocfilehash: 511070e139c2d0fb2862e8cc61ed8ead242c71e6
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="application-insights-telemetry-data-model"></a>Modello di dati di Application Insights Telemetry

[Azure Application Insights](app-insights-overview.md) invia dati di telemetria dall'applicazione Web al portale di Azure, in modo da poter analizzare le prestazioni e l'uso dell'applicazione. Il modello di dati di telemetria è standardizzato e di conseguenza è possibile creare scenari di monitoraggio indipendenti dalla piattaforma e dal linguaggio. 

I dati raccolti da Application Insights creano questo tipico modello di esecuzione dell'applicazione:

![Modello di applicazione di Application Insights](./media/application-insights-data-model/application-insights-data-model.png)

Per monitorare l'esecuzione dell'applicazione si usano i tipi di dati di telemetria che seguono. I tre tipi seguenti vengono raccolti automaticamente da Application Insights SDK dal framework dell'applicazione Web:

* [**Richiesta**](application-insights-data-model-request-telemetry.md): tipo generato per registrare una richiesta ricevuta dall'applicazione. Ad esempio, la versione Web di Application Insights SDK genera automaticamente un elemento di telemetria di tipo richiesta per ogni richiesta HTTP ricevuta dall'app Web. 

    Un'**operazione** è il thread di esecuzione che elabora una richiesta. È anche possibile [scrivere codice](app-insights-api-custom-events-metrics.md#trackrequest) per monitorare altri tipi di operazioni, ad esempio la "riattivazione" di un processo Web o di una funzione che periodicamente elabora i dati.  Ogni operazione presenta un ID. Questo ID può essere usato per [raggruppare](application-insights-correlation.md) tutti i dati di telemetria generati durante l'elaborazione della richiesta da parte dell'app. Ogni operazione ha un esito positivo o negativo e una certa durata.
* [**Eccezione**](application-insights-data-model-exception-telemetry.md): rappresenta in genere un'eccezione che causa l'esito negativo dell'operazione.
* [**Dipendenza**](application-insights-data-model-dependency-telemetry.md): rappresenta una chiamata dall'applicazione a un servizio esterno o a una risorsa di archiviazione, ad esempio a un'API REST o a SQL. In ASP.NET le chiamate di dipendenza a SQL sono definite da `System.Data`. Le chiamate agli endpoint HTTP sono definite da `System.Net`. 

Application Insights offre altri tre tipi di dati per la telemetria personalizzata:

* [Traccia](application-insights-data-model-trace-telemetry.md): tipo usato direttamente o tramite un adapter per implementare la registrazione diagnostica con un framework di strumentazione con cui si ha familiarità, ad esempio `Log4Net` o `System.Diagnostics`.
* [Evento](application-insights-data-model-event-telemetry.md): tipo usato in genere per acquisire l'interazione dell'utente con il servizio per analizzare i modelli di utilizzo.
* [Metrica](application-insights-data-model-metric-telemetry.md): tipo usato per indicare le misurazioni scalari periodiche.

Ogni elemento di telemetria può definire [informazioni di contesto](application-insights-data-model-context.md) quali la versione dell'applicazione o l’ID della sessione utente. Il contesto è un set di campi fortemente tipizzati che sblocca determinati scenari. Quando la versione dell'applicazione viene inizializzata correttamente, Application Insights può rilevare nuovi modelli di comportamento dell'applicazione in correlazione con la ridistribuzione. L'ID sessione consente di calcolare l'interruzione del servizio o l’impatto di un problema sugli utenti. Il calcolo separato dei valori dell'ID sessione per determinate dipendenze non riuscite, tracce di errore o eccezioni critiche offre una buona conoscenza dell'impatto.

Il modello di dati di Application Insights Telemetry definisce una modalità di [correlazione](application-insights-correlation.md) dei dati di telemetria all'operazione di cui fanno parte. Una richiesta può ad esempio di effettuare chiamate a un database SQL e registrare informazioni di diagnostica. È possibile impostare il contesto di correlazione per gli elementi di telemetria che lo legano di nuovo alla telemetria delle richieste.

## <a name="schema-improvements"></a>Miglioramenti allo schema

Il modello di dati di Application Insights rappresenta un modo semplice e pratico, ma potente, per modellare i dati di telemetria dell'applicazione. Microsoft si impegna a mantenere il modello semplice ed essenziale in modo da supportare gli scenari essenziali e da consentire l'estensione dello schema per un uso avanzato.

Per segnalare problemi e suggerimenti relativi al modello di dati e allo schema, usare il repository di GitHub [ApplicationInsights-Home](https://github.com/Microsoft/ApplicationInsights-Home/labels/schema).

## <a name="next-steps"></a>Passaggi successivi

- [Scrivere dati di telemetria personalizzati](app-insights-api-custom-events-metrics.md)
- Informazioni su come [estendere e filtrare i dati di telemetria](app-insights-api-filtering-sampling.md).
- Usare il [campionamento](app-insights-sampling.md) per ridurre al minimo la quantità di dati di telemetria in base al modello di dati.
- Verificare quali [piattaforme](app-insights-platforms.md) supportano Application Insights.
