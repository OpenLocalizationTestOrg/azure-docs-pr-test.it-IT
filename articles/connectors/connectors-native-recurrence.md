---
title: trigger di ricorrenza aaaAdd hello in App per la logica | Documenti Microsoft
description: Panoramica del trigger di ricorrenza hello e come toouse con un'app per la logica di Azure.
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 51dd4f22-7dc5-41af-a0a9-e7148378cd50
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e7c625c382a88a1e7cdfff4ddc0caf55727232bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-recurrence-trigger"></a>Introduzione a trigger ricorrenza hello
Tramite il trigger di ricorrenza hello, è possibile creare potenti flussi di lavoro nel cloud hello.

Ad esempio, è possibile:

* Pianificare un toorun del flusso di lavoro una stored procedure SQL ogni giorno.
* Un riepilogo di tutti i TWEET all'interno di hello ultima settimana su un determinato hashtag di posta elettronica.

tooget avviato tramite trigger ricorrenza hello in un'app di logica, vedere [creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-a-recurrence-trigger"></a>Usare un trigger di ricorrenza
Un trigger è un evento che può essere utilizzato toostart hello flusso di lavoro che è definito in un'app di logica. [Altre informazioni sui trigger](connectors-overview.md).

Di seguito è riportata una sequenza di esempio di come tooset di una ricorrenza attivare in un'app di logica:

1. Aggiungere hello **ricorrenza** trigger come primo passaggio di hello in un'app di logica.
2. Specificare i parametri di hello per l'intervallo di ricorrenza hello.

Hello logica app verrà avviata un'esecuzione dopo ogni intervallo di tempo.

![Trigger HTTP](./media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a>Dettagli del trigger
i trigger di ricorrenza Hello è hello seguenti proprietà che è possibile configurare.

Attiva un'app per la logica dopo un intervallo di tempo specificato.
Un asterisco (*) indica che è un campo obbligatorio.

| Nome visualizzato | Nome proprietà | Descrizione |
| --- | --- | --- |
| Frequenza* |frequency |unità di Hello di tempo: `Second`, `Minute`, `Hour`, `Day`, o `Year`. |
| Intervallo* |interval |intervallo di Hello di hello dato frequenza ricorrenza hello. |
| Fuso orario |timeZone |Se viene fornito un valore startTime senza una differenza dall'ora UTC, verrà usato tale valore timeZone. |
| Ora di inizio |startTime |ora di inizio Hello in [formato ISO 8601](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations). |

<br>

## <a name="next-steps"></a>Passaggi successivi
A questo punto, provare a piattaforma hello e [creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md). È possibile esplorare altri connettori disponibile in App per la logica di hello esaminando il nostro [elenco API](apis-list.md).

