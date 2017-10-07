---
title: Modello di dati di Application Insights telemetria aaaAzure | Documenti Microsoft
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
ms.openlocfilehash: 5610519c3db8ec68d6cf787639204fb79724f511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-telemetry-data-model"></a>Modello di dati di Application Insights Telemetry

[Azure Application Insights](app-insights-overview.md) invia dati di telemetria dal toohello di applicazione web il portale di Azure, in modo che è possibile analizzare le prestazioni di hello e l'utilizzo dell'applicazione. modello di dati di telemetria Hello è standard in modo che sia possibile toocreate piattaforma e il monitoraggio indipendente dal linguaggio. 

I dati raccolti da Application Insights creano questo tipico modello di esecuzione dell'applicazione:

![Modello di applicazione di Application Insights](./media/application-insights-data-model/application-insights-data-model.png)

Hello seguenti tipi di dati di telemetria vengono utilizzati toomonitor hello esecuzione dell'applicazione. Hello tre tipi seguenti vengono in genere automaticamente raccolti da Application Insights SDK hello dal framework di applicazioni web hello:

* [**Richiesta** ](application-insights-data-model-request-telemetry.md) -generato toolog una richiesta ricevuta dall'app. Ad esempio, hello web Application Insights che SDK genera automaticamente un elemento di dati di telemetria di richiesta per ogni richiesta HTTP che riceve l'app web. 

    Un **operazione** è hello di thread di esecuzione che elabora una richiesta. È anche possibile [scrivere codice](app-insights-api-custom-events-metrics.md#trackrequest) toomonitor altri tipi di operazione, ad esempio un "riattivazione" in un sito web del processo o funzione periodicamente che elabora i dati.  Ogni operazione presenta un ID. Questo ID che può essere utilizzato too[group]((application-insights-correlation.md) tutti i dati di telemetria generati durante l'elaborazione richiesta hello l'app. Ogni operazione ha un esito positivo o negativo e una certa durata.
* [**Eccezione** ](application-insights-data-model-exception-telemetry.md) -rappresenta in genere un'eccezione che causa toofail un'operazione.
* [**Dipendenza** ](application-insights-data-model-dependency-telemetry.md) -rappresenta una chiamata dal servizio esterno tooan di app o archiviazione, ad esempio un'API REST o SQL. In ASP.NET, dipendenza chiamate tooSQL vengono definiti tramite `System.Data`. Chiamate tooHTTP endpoint sono definiti da `System.Net`. 

Application Insights offre altri tre tipi di dati per la telemetria personalizzata:

* [Traccia](application-insights-data-model-trace-telemetry.md) - usate direttamente o tramite la registrazione diagnostica tooimplement un adapter utilizzando un framework di strumentazione è tooyou familiarità, ad esempio `Log4Net` o `System.Diagnostics`.
* [Evento](application-insights-data-model-event-telemetry.md) -utilizzato in genere l'interazione dell'utente toocapture con il servizio, modelli di utilizzo tooanalyze.
* [Metrica](application-insights-data-model-metric-telemetry.md) -utilizzato tooreport le misurazioni di scalare periodiche.

Ogni elemento di dati di telemetria può definire hello [informazioni sul contesto](application-insights-data-model-context.md) come id di sessione utente o di versione dell'applicazione. Il contesto è un set di campi fortemente tipizzati che sblocca determinati scenari. Quando la versione dell'applicazione viene inizializzata correttamente, Application Insights può rilevare nuovi modelli di comportamento dell'applicazione in correlazione con la ridistribuzione. Id di sessione può essere utilizzato toocalculate hello interruzione o un impatto del problema degli utenti. Il calcolo separato dei valori dell'ID sessione per determinate dipendenze non riuscite, tracce di errore o eccezioni critiche offre una buona conoscenza dell'impatto.

Modello di dati di telemetria definisce una modalità di Application Insights troppo[correlare](application-insights-correlation.md) operazione toohello telemetria di cui fa parte. Una richiesta può ad esempio di effettuare chiamate a un database SQL e registrare informazioni di diagnostica. È possibile impostare il contesto di correlazione hello per gli elementi di dati di telemetria ricollegarlo telemetria richiesta toohello indietro.

## <a name="schema-improvements"></a>Miglioramenti allo schema

Modello di dati di Application Insights è toomodel un modo semplice e base ma potente la telemetria dell'applicazione. Si cercano scenari principali di tookeep hello modello semplice e sottile toosupport e consentire schema hello tooextend ad utenti esperti.

problemi di dati tooreport modello o lo schema e i suggerimenti usano GitHub [ApplicationInsights Home](https://github.com/Microsoft/ApplicationInsights-Home/labels/schema) repository.

## <a name="next-steps"></a>Passaggi successivi

- [Scrivere dati di telemetria personalizzati](app-insights-api-custom-events-metrics.md)
- Informazioni su come troppo[estendere e filtrare i dati di telemetria](app-insights-api-filtering-sampling.md).
- Utilizzare [campionamento](app-insights-sampling.md) toominimize quantità di dati di telemetria basata sul modello di dati.
- Verificare quali [piattaforme](app-insights-platforms.md) supportano Application Insights.
