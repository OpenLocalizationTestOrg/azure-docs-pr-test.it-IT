---
title: API di Mobile Engagement Web SDK aaaAzure | Documenti Microsoft
description: "Hello procedure per hello Web SDK e gli aggiornamenti più recenti per Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8a87d5ac-d8b7-4a0d-bdee-414dbcc561b2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 06/07/2016
ms.author: piyushjo
ms.openlocfilehash: ec1261d6ad573b8c3ad6d5f616ab7bbe560d6fe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-mobile-engagement-api-in-a-web-application"></a>Utilizzare l'API di Azure Mobile Engagement di hello in un'applicazione web
Questo documento è un documento di inoltre toohello che indica come troppo[integrare Mobile Engagement in un'applicazione web](mobile-engagement-web-integrate-engagement.md). Fornisce informazioni dettagliate su come toouse hello API di Azure Mobile Engagement tooreport le statistiche dell'applicazione.

Hello Mobile Engagement API viene fornita da hello `engagement.agent` oggetto. impostazione predefinita, Azure Mobile Engagement Web SDK alias è Hello `engagement`. È possibile ridefinire l'alias da configurazione SDK hello.

## <a name="mobile-engagement-concepts"></a>Concetti relativi a Mobile Engagement
Hello dalle parti seguenti perfezionare comuni [concetti di Mobile Engagement](mobile-engagement-concepts.md) per piattaforma web hello.

### <a name="session-and-activity"></a>`Session` e `Activity`
Se l'utente hello rimane inattivo per più di pochi secondi tra due attività, hello sequenza dell'utente di attività è suddiviso in due sessioni distinte. Questi alcuni secondi vengono chiamati hello timeout della sessione.

Se l'applicazione web non vengono dichiarati fine hello dell'attività dell'utente da solo (dal chiamante hello `engagement.agent.endActivity` funzione), il server di Mobile Engagement hello scade automaticamente hello sessione utente all'interno di tre minuti dopo la chiusura di una pagina dell'applicazione hello. Si tratta del timeout della sessione server hello.

### `Crash`
I report automatici di eccezioni JavaScript non rilevate non vengono creati per impostazione predefinita. Tuttavia, è possibile segnalare arresti anomali del sistema manualmente utilizzando hello `sendCrash` funzione (vedere la sezione hello sulla segnalazione di arresti anomali del sistema).

## <a name="reporting-activities"></a>Segnalazione di attività
Creazione di report attività utente include quando un utente avvia una nuova attività e quando l'utente hello termina l'attività corrente di hello.

### <a name="user-starts-a-new-activity"></a>L'utente avvia una nuova attività
    engagement.agent.startActivity("MyUserActivity");

È necessario toocall `startActivity()` attività ogni utente in fase di modifica. Hello prima chiamata toothis funzione avvia una nuova sessione utente.

### <a name="user-ends-hello-current-activity"></a>Utente termina l'attività corrente hello
    engagement.agent.endActivity();

È necessario toocall `endActivity()` almeno una volta quando viene completata l'ultima attività utente hello. Questo indica hello Mobile Engagement Web SDK di utente hello è attualmente inattivo, che è necessario toobe sessione utente hello chiuso alla scadenza del timeout della sessione hello. Se si chiama `startActivity()` prima della scadenza del timeout della sessione hello, sessione hello viene semplicemente ripreso.

Poiché non esiste alcuna chiamata affidabile per la chiusura di finestra strumento di navigazione hello, è spesso fine hello difficili o impossibili toocatch di attività dell'utente all'interno di un ambiente web. Che è hello perché Mobile Engagement server scade automaticamente sessione utente hello entro tre minuti dopo la chiusura di una pagina dell'applicazione hello.

## <a name="reporting-events"></a>Segnalazione di eventi
La segnalazione di eventi include eventi di sessione ed eventi autonomi.

### <a name="session-events"></a>Eventi di sessione
Eventi di sessione sono in genere azioni hello tooreport utilizzati eseguite da un utente durante la sessione dell'utente hello.

**Esempio senza dati aggiuntivi:**

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login');
      // [...]
    }

**Esempio con dati aggiuntivi:**

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login', {user: 'alice'});
      // [...]
    }

### <a name="standalone-events"></a>Eventi autonomi
A differenza degli eventi di sessione, possono verificarsi eventi di autonomo all'esterno di hello contesto di una sessione.

A tale scopo, usare ``engagement.agent.sendEvent`` invece di ``engagement.agent.sendSessionEvent``.

## <a name="reporting-errors"></a>Segnalazione di errori
La segnalazione di errori include errori di sessione ed errori autonomi.

### <a name="session-errors"></a>Errori di sessione
Sessione in genere gli errori tooreport utilizzati hello abbia un impatto sull'utente hello durante hello sessione utente.

**Esempio senza dati aggiuntivi:**

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short');
      }
      // [...]
    }

**Esempio con dati aggiuntivi:**

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short', {length: 4});
      }
      // [...]
    }

### <a name="standalone-errors"></a>Errori autonomi
A differenza degli errori di sessione, possono verificarsi errori di autonomo all'esterno di hello contesto di una sessione.

A tale scopo, usare `engagement.agent.sendError` invece di `engagement.agent.sendSessionError`.

## <a name="reporting-jobs"></a>Segnalazione di processi
La segnalazione di processi include la segnalazione di errori ed eventi che si verificano durante un processo e la segnalazione di arresti anomali.

**Esempio:**

Se si desidera toomonitor una richiesta AJAX, utilizzare la seguente hello:

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
      // [...]
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-errors-during-a-job"></a>Segnalazione di errori durante un processo
Gli errori possono essere correlato tooa esecuzione processo anziché toohello sessione utente.

**Esempio:**

Se si desidera tooreport un errore se una richiesta AJAX non riesce:

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
        // [...]
        if (xhr.status == 0 || xhr.status >= 400) {
          engagement.agent.sendJobError('publish_xhr', 'publish', {status: xhr.status, statusText: xhr.statusText});
        }
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-events-during-a-job"></a>Segnalazione di eventi durante un processo
Gli eventi possono essere correlato tooa esecuzione processo anziché toohello la sessione utente corrente, grazie toohello `engagement.agent.sendJobEvent` (funzione).

Questa funzione opera esattamente come la funzione `engagement.agent.sendJobError`.

### <a name="reporting-crashes"></a>Segnalazione di arresti anomali
Hello utilizzare `sendCrash` tooreport funzione arresti anomali manualmente.

Hello `crashid` argomento è una stringa che identifica il tipo di hello di arresto anomalo del sistema.
Hello `crash` argomento è in genere l'analisi dello stack hello di arresto anomalo di hello sotto forma di stringa.

    engagement.agent.sendCrash(crashid, crash);

## <a name="extra-parameters"></a>Parametri aggiuntivi
È possibile collegare l'evento tooan dati arbitrari, errore, attività o processo.

dati Hello possono essere qualsiasi oggetto JSON (ma non una matrice o tipo primitivo).

**Esempio:**

    var extras = {"video_id": 123, "ref_click": "http://foobar.com/blog"};
    engagement.agent.sendEvent("video_clicked", extras);

### <a name="limits"></a>Limiti
Limiti applicati tooextra parametri sono nelle aree di hello delle espressioni regolari per le chiavi, i tipi di valore e dimensioni.

#### <a name="keys"></a>Chiavi
Ogni chiave nell'oggetto hello deve corrispondere hello espressione regolare seguente:

    ^[a-zA-Z][a-zA-Z_0-9]*

Questo significa che le chiavi devono iniziare con almeno una lettera seguita da lettere, cifre o caratteri di sottolineatura (\_).

#### <a name="values"></a>Valori
I valori sono limitate toostring, numero e i tipi booleani.

#### <a name="size"></a>Dimensione
Funzionalità aggiuntive sono limitate too1, 024 caratteri per ogni chiamata (dopo hello Mobile Engagement Web SDK viene eseguita la codifica in JSON).

## <a name="reporting-application-information"></a>Segnalazione di informazioni sull'applicazione
È possibile segnalare informazioni (o qualsiasi altra informazione specifici dell'applicazione) il rilevamento delle manualmente utilizzando hello `sendAppInfo()` (funzione).

Si noti che queste informazioni possono essere inviate in modo incrementale. Per un dispositivo specifico, verrà mantenuto solo hello valore più recente per una chiave specifica.

Ad esempio funzionalità aggiuntive di evento, è possibile utilizzare le informazioni di applicazione tooabstract oggetto JSON. Si noti che le matrici o gli oggetti secondari vengono trattati come stringhe flat, usando la serializzazione JSON.

**Esempio:**

Di seguito è riportato un esempio di codice per sesso dell'utente di hello l'invio e la data di nascita:

    var appInfos = {"birthdate":"1983-12-07","gender":"female"};
    engagement.agent.sendAppInfo(appInfos);

### <a name="limits"></a>Limiti
Limiti applicati tooapplication informazioni sono nelle aree di hello delle espressioni regolari per le chiavi e dimensioni.

#### <a name="keys"></a>Chiavi
Ogni chiave nell'oggetto hello deve corrispondere hello espressione regolare seguente:

    ^[a-zA-Z][a-zA-Z_0-9]*

Questo significa che le chiavi devono iniziare con almeno una lettera seguita da lettere, cifre o caratteri di sottolineatura (\_).

#### <a name="size"></a>Dimensione
Informazioni sull'applicazione è limitata too1, 024 caratteri per ogni chiamata (dopo hello Mobile Engagement Web SDK viene eseguita la codifica in JSON).

In hello sopra riportato, hello JSON inviati, toohello server 44 caratteri:

    {"birthdate":"1983-12-07","gender":"female"}
