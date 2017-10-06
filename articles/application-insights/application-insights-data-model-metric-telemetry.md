---
title: aaaAzure modello dati di telemetria Insights di applicazione - metrica telemetria | Documenti Microsoft
description: Modello di dati di Application Insights per la metrica dei dati di telemetria
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
ms.openlocfilehash: 005e218a8451007458185f1e457a20cee93fa630
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="metric-telemetry-application-insights-data-model"></a>Metrica dei dati di telemetria: modello di dati di Application Insights

Esistono due tipi di telemetria della metrica supportata da [Application Insights](app-insights-overview.md): la metrica a misura singola e la metrica preaggregata. La misura singola è costituita semplicemente da un nome e un valore. Metrica preaggregato consente di specificare il valore minimo e massimo della metrica hello nell'intervallo di aggregazione hello e deviazione standard di esso.

La metrica dei dati di telemetria preaggregata presuppone che il periodo di aggregazione sia di un minuto.

Esistono diversi nomi di metrica noti supportati da Application Insights. 

Metrica che rappresenta i contatori di sistema e di processo:

| **Nome .NET**             | **Nome indipendente dalla piattaforma** | **Nome API REST** | **Descrizione**
| ------------------------- | -------------------------- | ----------------- | ---------------- 
| `\Processor(_Total)\% Processor Time` | Lavoro in corso... | [processorCpuPercentage](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessorCpuPercentage) | CPU computer totale
| `\Memory\Available Bytes`                 | Lavoro in corso... | [memoryAvailableBytes](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FmemoryAvailableBytes) | memoria disponibile su disco
| `\Process(??APP_WIN32_PROC??)\% Processor Time` | Lavoro in corso... | [processCpuPercentage](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessCpuPercentage) | CPU del processo di hello ospita un'applicazione hello
| `\Process(??APP_WIN32_PROC??)\Private Bytes`      | Lavoro in corso... | [processPrivateBytes](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessPrivateBytes) | memoria utilizzata dal processo di hello che ospita un'applicazione hello
| `\Process(??APP_WIN32_PROC??)\IO Data Bytes/sec` | Lavoro in corso... | [processIOBytesPerSecond](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessIOBytesPerSecond) | frequenza delle operazioni dei / o di esecuzione di processo che ospita un'applicazione hello
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec`             | Lavoro in corso... | [requestsPerSecond](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsPerSecond) | frequenza delle richieste elaborate dall'applicazione 
| `\.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec`    | Lavoro in corso... | [exceptionsPerSecond](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FexceptionsPerSecond) | frequenza delle eccezioni generate dall'applicazione
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time`   | Lavoro in corso... | [requestExecutionTime](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestExecutionTime) | tempo di esecuzione medio delle richieste
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue` | Lavoro in corso... | [requestsInQueue](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsInQueue) | numero di richieste in attesa di hello in una coda di elaborazione

## <a name="name"></a>Nome

Nome della metrica hello desideri toosee nel portale Application Insights e l'interfaccia utente. 

## <a name="value"></a>Valore

Singolo valore per la misura. Somma delle singole misure per l'aggregazione di hello.

## <a name="count"></a>Numero

Peso della metrica di metrica hello aggregato. Non deve essere impostato per una misura.

## <a name="min"></a>Min

Valore minimo della metrica hello aggregato. Non deve essere impostato per una misura.

## <a name="max"></a>max

Valore massimo della metrica hello aggregato. Non deve essere impostato per una misura.

## <a name="standard-deviation"></a>Deviazione standard

Deviazione standard della metrica hello aggregato. Non deve essere impostato per una misura.

## <a name="custom-properties"></a>Proprietà personalizzate

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a>Passaggi successivi

- Informazioni su come toouse [Application Insights API per gli eventi personalizzati e le metriche](app-insights-api-custom-events-metrics.md#trackmetric).
- Per informazioni sul modello di dati e sui tipi di Application Insights, vedere il [modello di dati](application-insights-data-model.md).
- Verificare quali [piattaforme](app-insights-platforms.md) supportano Application Insights.
