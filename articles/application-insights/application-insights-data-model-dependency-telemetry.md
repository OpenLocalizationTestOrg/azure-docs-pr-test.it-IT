---
title: Modello di dati di Azure Application Insights Telemetry - Telemetria delle dipendenze | Microsoft Docs
description: Modello di dati di Application Insights per la telemetria delle dipendenze
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/17/2017
ms.author: bwren
ms.openlocfilehash: 2e97c3f951f46c32802aea543b93d5ab1bb76228
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="dependency-telemetry-application-insights-data-model"></a>Telemetria delle dipendenze: modello di dati di Application Insights

In [Application Insights](app-insights-overview.md), la telemetria delle dipendenze rappresenta un'interazione del componente monitorato con un componente remoto, ad esempio SQL o un endpoint HTTP.

## <a name="name"></a>Nome

Nome del comando avviato con questa chiamata delle dipendenze. Valore di cardinalità basso. Esempi sono il nome della stored procedure e il modello di percorso URL.

## <a name="id"></a>ID

Identificatore dell'istanza di una chiamata delle dipendenze. Usato per la correlazione con l'elemento di telemetria delle richieste corrispondente a questa chiamata delle dipendenze. Per altre informazioni vedere la pagina relativa alla [correlazione](application-insights-correlation.md).

## <a name="data"></a>Dati

Comando avviato con questa chiamata delle dipendenze. Esempi sono l'istruzione SQL e l'URL HTTP con tutti i parametri di query.

## <a name="type"></a>Tipo

Nome del tipo di dipendenza. Valore di cardinalità basso per un raggruppamento logico delle dipendenze e l'interpretazione di altri campi come commandName e resultCode. Esempi sono SQL, tabelle di Azure e HTTP.

## <a name="target"></a>Destinazione

Sito di destinazione di una chiamata delle dipendenze. Esempi sono nome del server, indirizzo host. Per altre informazioni vedere la pagina relativa alla [correlazione](application-insights-correlation.md).

## <a name="duration"></a>Durata

Durata della richiesta in formato: `DD.HH:MM:SS.MMMMMM`. Deve essere inferiore a `1000` giorni.

## <a name="result-code"></a>Codice risultato

Codice risultato di una chiamata delle dipendenze. Esempi sono il codice di errore SQL e il codice di stato HTTP.

## <a name="success"></a>Success

Indicazione di chiamata con esito positivo o con esito negativo.

## <a name="custom-properties"></a>Proprietà personalizzate

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a>Misure personalizzate

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]


## <a name="next-steps"></a>Passaggi successivi

- Impostare il rilevamento delle dipendenze per [.NET](app-insights-asp-net-dependencies.md).
- Impostare il rilevamento delle dipendenze per [Java](app-insights-java-agent.md).
- [Scrivere dati di telemetria delle dipendenze personalizzate](app-insights-api-custom-events-metrics.md#trackdependency)
- Per informazioni sul modello di dati e sui tipi di Application Insights, vedere il [modello di dati](application-insights-data-model.md).
- Verificare quali [piattaforme](app-insights-platforms.md) supportano Application Insights.
