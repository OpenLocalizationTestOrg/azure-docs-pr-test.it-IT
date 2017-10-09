---
title: aaaAzure modello dati di telemetria Insights di applicazione - evento di telemetria | Documenti Microsoft
description: Modello di dati di Application Insights per la telemetria degli eventi
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
ms.openlocfilehash: cd7dc3c5f4f3df22b7a52ee79fcad566a27a9f4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="event-telemetry-application-insights-data-model"></a>Telemetria degli eventi: modello di dati di Application Insights

È possibile creare elementi di dati di telemetria evento (in [Application Insights](app-insights-overview.md)) toorepresent un evento che si sono verificati nell'applicazione. Si tratta in genere di un'interazione dell'utente, ad esempio il clic su un pulsante o il completamento della transazione di un ordine. Può inoltre essere un evento del ciclo di vita dell'applicazione come l'inizializzazione o l'aggiornamento della configurazione. 

Semanticamente, gli eventi potrebbero non essere toorequests correlato. Se usata correttamente, la telemetria degli eventi è tuttavia più importante delle richieste o delle tracce. Eventi rappresentano dati di telemetria business e deve essere un oggetto tooseparate, meno rigide [campionamento](app-insights-api-filtering-sampling.md).

## <a name="name"></a>Nome

Nome evento. raggruppamento appropriate tooallow e metriche utile limitare l'applicazione in modo che generi un numero ridotto di nomi di evento separato. Ad esempio, non usare un nome distinto per ogni istanza generata di un evento.

Lunghezza massima: 512 caratteri

## <a name="custom-properties"></a>Proprietà personalizzate

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a>Misure personalizzate

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a>Passaggi successivi

- Per informazioni sul modello di dati e sui tipi di Application Insights, vedere il [modello di dati](application-insights-data-model.md).
- [Scrivere dati di telemetria di eventi personalizzati](app-insights-api-custom-events-metrics.md#trackevent)
- Verificare quali [piattaforme](app-insights-platforms.md) supportano Application Insights.
