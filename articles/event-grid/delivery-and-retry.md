---
title: nuovo tentativo e il recapito di griglia eventi aaaAzure
description: Viene descritto in che modo Griglia di eventi di Azure recapita gli eventi e come gestisce i messaggi non recapitati.
services: event-grid
author: djrosanova
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/11/2017
ms.author: darosa
ms.openlocfilehash: 874b3bf8892fbf803ef40f29d0ec10eb50150916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-message-delivery-and-retry"></a>Recapito di messaggi di Griglia di eventi e nuovi tentativi 

Questo articolo descrive in che modo Griglia di eventi di Azure gestisce gli eventi quando il recapito non viene confermato.

Griglia di eventi fornisce il recapito durevole. Ogni messaggio viene recapitato almeno una volta per ogni sottoscrizione. Gli eventi vengono inviati immediatamente webhook toohello registrato di ogni sottoscrizione. Se un webhook non riconosce la ricezione di un evento all'interno di 60 secondi, di recapito prima hello tentano, griglia eventi tentativi di recapito dei messaggi di evento hello.

## <a name="message-delivery-status"></a>Stato di recapito del messaggio

Griglia di eventi Usa HTTP risposta codici tooacknowledge conferma recapito eventi. 

### <a name="success-codes"></a>Codici di riuscita

Hello codici di risposta HTTP seguenti indicano che un evento è stato recapitato correttamente tooyour webhook. Griglia di eventi considera il recapito completato.

- 200 - OK
- 202 - Accettato

### <a name="failure-codes"></a>Codici di errore

Hello seguenti codici di risposta HTTP indica che un tentativo di recapito eventi non è riuscita. Griglia di eventi tenta nuovamente di evento hello toosend. 

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

Griglia di eventi usa criteri per i tentativi di tipo backoff esponenziale per il recapito degli eventi. Se il webhook non risponde o restituisce un codice di errore, griglia evento tentativi di recapito in base alla pianificazione hello:

1. 10 secondi
2. 30 secondi
3. 1 minuto
4. 5 minuti
5. 10 minuti
6. 30 minuti
7. 1 ora

Griglia di eventi aggiunge gli intervalli tra tentativi di tooall una sequenza casuale di piccole dimensioni.

## <a name="retry-duration"></a>Durata dei tentativi

Durante l'anteprima di hello, tutti gli eventi che non vengono recapitati entro due ore di scadenza della griglia di eventi di Azure. Prima della disponibilità generale, questo tempo sarà maggiore too24 ore. 

## <a name="next-steps"></a>Passaggi successivi

* Per un'introduzione tooEvent griglia, vedere [sulla griglia di eventi](overview.md).
* tooquickly informazioni introduttive sull'utilizzo della griglia di eventi, vedere [route e creare eventi personalizzati con griglia di eventi di Azure](custom-event-quickstart.md).
