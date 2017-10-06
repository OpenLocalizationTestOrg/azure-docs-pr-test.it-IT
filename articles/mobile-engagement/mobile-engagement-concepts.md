---
title: concetti di Engagement aaaMobile | Documenti Microsoft
description: Concetti relativi ad Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8d19abd1-0a6c-4772-9fa5-5e99980ac5da
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 5aa7f28c00cd641a36a6e040c6b13d802ea6ae41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-concepts"></a>Concetti relativi ad Azure Mobile Engagement
Engagement mobile definisce alcuni concetti comuni tooall supportate le piattaforme. descritti brevemente in questo articolo.

Questo articolo è un buon punto di partenza, in caso di nuova tooMobile Engagement. Verificare inoltre che tooread hello documentazione toohello specifico della piattaforma in uso, come perfezioneranno i concetti di hello descritti in questo articolo con ulteriori dettagli ed esempi, nonché le possibili limitazioni.

## <a name="devices-and-users"></a>Dispositivi e utenti
Mobile Engagement identifica gli utenti generando un identificatore univoco per ogni dispositivo, Questo identificatore è definito l'identificatore del dispositivo hello (o `deviceid`). Viene generato in modo che tutti in esecuzione applicazioni di hello stessa condivisione dispositivo hello stesso identificatore del dispositivo.

In modo implicito, significa che Engagement Mobile considera un toobelong tooexactly un utente del dispositivo e di conseguenza, gli utenti e dispositivi sono concetti equivalenti.

## <a name="sessions-and-activities"></a>Sessioni e attività
Una sessione è un utilizzo di un'applicazione hello eseguita da un utente, hello ora hello utente inizia a utilizzare, finché non viene arrestata utente hello.

Un'attività è un utilizzo di una determinata parte secondaria di un'applicazione hello eseguita da un utente (in genere una schermata, ma può essere toohello adatto a qualsiasi applicazione).

Un utente può svolgere una sola attività per volta.

Un'attività è identificata da un nome (caratteri limitati too64) e, facoltativamente, è stato possibile incorporare alcuni dati aggiuntivi (in limite hello pari a 1024 byte).

Le sessioni vengono calcolate automaticamente dalla sequenza di hello delle attività eseguite dagli utenti. Quando l'utente hello inizia la prima attività e si arresta quando avrà terminato il suo ultima attività, viene avviata una sessione. Ciò significa che una sessione non è necessario toobe avviato o arrestato in modo esplicito. al contrario, le attività vengono avviate o arrestate in modo esplicito. Se non viene segnalata alcuna attività, non viene segnalata alcuna sessione.

## <a name="events"></a>Events
Gli eventi sono utilizzati tooreport azioni immediate (come la pressione del pulsante o gli articoli di lettura da parte degli utenti).

Un evento può essere correlata toohello sessione corrente, tooa esecuzione del processo, oppure può essere un evento autonomo.

Un evento è identificato da un nome (caratteri limitati too64) e, facoltativamente, è stato possibile incorporare alcuni dati aggiuntivi (in limite hello pari a 1024 byte).

## <a name="error"></a>Errore
Gli errori vengono utilizzati tooreport problemi rilevati correttamente dall'applicazione hello (ad esempio, le azioni dell'utente non corretta o errori della chiamata API).

Un errore può essere correlata toohello sessione corrente, tooa esecuzione del processo, oppure può essere un errore autonomo.

Un errore è identificato da un nome (caratteri limitati too64) e, facoltativamente, è stato possibile incorporare alcuni dati aggiuntivi (in limite hello pari a 1024 byte).

## <a name="job"></a>Job
I processi sono azioni tooreport utilizzato con una durata (come durata delle chiamate API, visualizzare l'ora di annunci, le attività in background o durata azioni dell'utente).

Un processo non è correlato tooa sessione, perché un'attività può essere eseguita in background di hello, senza alcuna interazione dell'utente.

Un processo è identificato da un nome (caratteri limitati too64) e, facoltativamente, è stato possibile incorporare alcuni dati aggiuntivi (in limite hello pari a 1024 byte).

## <a name="crash"></a>Arresto anomalo
Arresti anomali del sistema vengono rilasciati automaticamente dall'applicazione di Mobile Engagement SDK tooreport errori in cui i problemi non rilevati da un'applicazione hello rendono crash hello.

## <a name="application-information"></a>Informazioni sull'applicazione
Informazioni sull'applicazione (o informazioni sull'app) è utilizzato tootag utenti, vale a dire tooassociate alcuni utenti toohello dati di un'applicazione (si tratta cookie tooweb simile, con informazioni sull'app viene archiviato sul lato server hello nella piattaforma Azure Mobile Engagement hello).

Informazioni sull'App possono essere registrati tramite l'API di Mobile Engagement SDK hello o utilizzando la piattaforma Mobile Engagement hello Device API.

Informazioni sull'App è un dispositivo associato tooa di coppia chiave/valore. chiave di Hello è nome hello delle informazioni sull'app hello (too64 limitato ASCII lettere [a-zA-Z], [0-9] numeri e caratteri di sottolineatura [_]). il valore di Hello (caratteri limitati too1024) può essere qualsiasi stringa, integer, data (AAAA-MM-gg) o un valore booleano (true o false).

Qualsiasi numero di informazioni sull'app può essere associato tooa dispositivo, entro i limiti di hello definito dai termini di prezzo di hello Mobile Engagement. Per una chiave specificata, Mobile Engagement solo tiene traccia del valore impostato più recente di hello (nessuno). Impostazione o modifica il valore di hello di informazioni sull'app forza Mobile Engagement toore-valutare i criteri di gruppo di destinatari impostato in questa app informazioni (se presente) vale a dire che informazioni sull'app possono essere utilizzati tootrigger effettua il push in tempo reale.

## <a name="extra-data"></a>Dati aggiuntivi
Dati aggiuntivi (o extra) sono alcuni dati arbitrari che possono essere collegati tooevents, errori, le attività e processi.

Funzionalità aggiuntive sono strutturate in modo analogo tooJSON oggetti: essi sono costituiti da una struttura ad albero di coppie chiave/valore. Le chiavi sono lettere ASCII too64 limitato [a-zA-Z], [0-9] numeri e caratteri di sottolineatura [_]) e dimensioni totali di hello di funzionalità aggiuntive sono limitate too1024 caratteri (una volta codificati in JSON da hello Mobile Engagement SDK).

Hello intera struttura ad albero di coppie chiave/valore viene archiviato come oggetto JSON. Tuttavia, solo hello primo livello di chiavi/valori è toobe scomposti direttamente accessibile toosome avanzate funzioni come segmenti (ad esempio, è possibile facilmente definire un segmento denominato "SciFi ventole" che è costituito da tutti gli utenti di avere inviato l'evento hello almeno 10 volte denominato "content_viewed" con content_type"hello chiave" set toohello valore "scifi" in hello ultimo mese). È pertanto consigliabile extra solo di toosend di elenchi semplici di coppie chiave/valore con valori scalari (ad esempio, stringhe, date, numeri interi o booleano).

## <a name="next-steps"></a>Passaggi successivi
* [Panoramica di Windows Universal SDK per Azure Mobile Engagement](mobile-engagement-windows-store-sdk-overview.md)
* [Panoramica di Windows Phone Silverlight SDK per Azure Mobile Engagement](mobile-engagement-windows-phone-sdk-overview.md)
* [iOS SDK per Azure Mobile Engagement](mobile-engagement-ios-sdk-overview.md)
* [Android SDK per Azure Mobile Engagement](mobile-engagement-android-sdk-overview.md)

