---
title: Recapito di Griglia di eventi di Azure e nuovi tentativi
description: Viene descritto in che modo Griglia di eventi di Azure recapita gli eventi e come gestisce i messaggi non recapitati.
services: event-grid
author: djrosanova
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 01/10/2018
ms.author: darosa
ms.openlocfilehash: fe9089334deceb38186add56ce3fb1d6ecc20363
ms.sourcegitcommit: 71fa59e97b01b65f25bcae318d834358fea5224a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/11/2018
---
# <a name="event-grid-message-delivery-and-retry"></a>Recapito di messaggi di Griglia di eventi e nuovi tentativi 

Questo articolo descrive in che modo Griglia di eventi di Azure gestisce gli eventi quando il recapito non viene confermato.

Griglia di eventi fornisce il recapito durevole. Ogni messaggio viene recapitato almeno una volta per ogni sottoscrizione. Gli eventi vengono inviati immediatamente al webhook registrato di ogni sottoscrizione. Se un webhook non conferma la ricezione di un evento entro 60 secondi dal primo tentativo di recapito, Griglia di eventi esegue un nuovo tentativo di recapito dell'evento.

## <a name="message-delivery-status"></a>Stato di recapito del messaggio

Griglia di eventi usa i codici di risposta HTTP per confermare la ricezione degli eventi. 

### <a name="success-codes"></a>Codici di riuscita

I codici di risposta HTTP seguenti indicano che un evento è stato recapitato correttamente al webhook. Griglia di eventi considera il recapito completato.

- 200 - OK
- 202 - Accettato

### <a name="failure-codes"></a>Codici di errore

I codici di risposta HTTP seguenti indicano che un tentativo di recapito di un evento non è riuscito. Griglia di eventi tenta nuovamente di inviare l'evento. 

- 400 - Richiesta non valida
- 401 - Non autorizzato
- 404 - Non trovato
- 408 - Timeout richiesta
- 414 - URI richiesta troppo lungo
- 500 - Errore interno del server
- 503 - Servizio non disponibile
- 504 - Timeout gateway

Qualsiasi altro codice di risposta o la mancanza di una risposta indica un errore. Griglia di eventi esegue un nuovo tentativo di recapito. 

## <a name="retry-intervals"></a>Intervalli tra tentativi

Griglia di eventi usa criteri per i tentativi di tipo backoff esponenziale per il recapito degli eventi. Se il webhook non risponde o restituisce un codice di errore, Griglia di eventi esegue un nuovo tentativo di recapito in base alla pianificazione seguente:

1. 10 secondi
2. 30 secondi
3. 1 minuto
4. 5 minuti
5. 10 minuti
6. 30 minuti
7. 1 ora

Griglia di eventi aggiunge una piccola parte di casualità a tutti gli intervalli tra tentativi.

## <a name="retry-duration"></a>Durata dei tentativi

Con la versione di anteprima, Griglia di eventi di Azure fa scadere tutti gli eventi che non vengono recapitati entro due ore.

## <a name="next-steps"></a>Passaggi successivi

* Per visualizzare lo stato di recapito degli eventi, vedere [Monitorare il recapito dei messaggio di Griglia di eventi di Azure](monitor-event-delivery.md).
* Per un'introduzione a Griglia di eventi, vedere [Informazioni su Griglia di eventi](overview.md).
* Per iniziare rapidamente a usare Griglia di eventi, vedere [Creare e instradare eventi personalizzati con Griglia di eventi di Azure](custom-event-quickstart.md).