---
title: aaaAzure Guide alla risoluzione dei problemi di Engagement Mobile
description: Guida alla risoluzione dei problemi di Azure Mobile Engagement
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 31134a29-a513-4e5e-b626-f6cf6fe04769
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: dd69bfd7019907c3e1da8df590db3b5f61606173
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement---troubleshooting-guide"></a>Azure Mobile Engagement - Guida alla risoluzione dei problemi
## <a name="introduction"></a>Introduzione
Hello seguendo la Guida alla risoluzione dei problemi aiutano a comprendere le cause principali di alcuni problemi comune e verrà consentono tootroubleshoot per conto proprio. 

## <a name="general"></a>Generale
In generale, è necessario assicurarsi sempre seguente hello:

1. Verificare che sia già stata consultata tutti i passaggi di hello necessari per l'integrazione, come descritto in questo [esercitazioni Guida introduttiva](mobile-engagement-windows-store-dotnet-get-started.md)
2. Si utilizza una versione più recente di hello del kit SDK della piattaforma hello. 
3. I test in un dispositivo reale sia un emulatore perché alcuni problemi sono solo tooemulator specifico. 
4. Assicurarsi di non superare alcun limite/limitazione di Mobile Engagement illustrato [qui](../azure-subscription-service-limits.md)
5. Se non si è in grado di tooconnect toohello Engagement Mobile back-end o visualizzare i dati non caricati in modo continuo del servizio, quindi verificare che siano non presenti gli eventi imprevisti alcun servizio in corso controllando [qui](https://azure.microsoft.com/status/)

## <a name="monitor-issues"></a>Problemi di monitoraggio
### <a name="i-am-not-seeing-my-device-showing-up-on-hello-monitor-tab"></a>Non vengono visualizzati il dispositivo visualizzato nella scheda Monitoraggio hello
Nella scheda Monitoraggio Mostra piattaforma Mobile Engagement di hello dispositivi connessi tooyour in tempo reale. Se si esegue il debug in un emulatore e in un dispositivo, in questa scheda dovrebbe essere visualizzata almeno una sessione. Se è stata distribuita l'applicazione hello, si noterà hello misuratore riflettono i dispositivi hello piattaforma toohello connesso in tempo reale di sessioni attive. 

Se il dispositivo non vengono visualizzati nella scheda Monitoraggio hello è probabilmente un problema di integrazione di SDK. Di seguito sono riportati alcuni comuni tootroubleshoot tootake passaggi:

1. Verificare che si utilizza la stringa di connessione corretta hello in app per dispositivi mobili hello ed è da hello SDK chiavi sezione e non hello API chiavi. stringa di connessione Hello si connette l'istanza di toohello app per dispositivi mobili di app di Mobile Engagement hello in cui il dispositivo verrà visualizzato nella scheda Monitoraggio hello. 
2. Per la piattaforma Windows - se la pagina esegue l'override di hello `OnNavigatedTo` (metodo), assicurarsi che toocall `base.OnNavigatedTo(e)`.
3. Se si sta integrando Mobile Engagement in un'app mobile esistente, è inoltre possibile garantire che non manchi eventuali passaggi osservando i passaggi per l'integrazione avanzata hello [qui](mobile-engagement-windows-store-integrate-engagement.md)
4. Verificare che si stanno inviando almeno una schermata/attività eseguendo l'override di pagina hello con EngagementActivity a seconda della piattaforma hello funzionino come descritto in hello [introduzione esercitazioni](mobile-engagement-windows-store-dotnet-get-started.md).

### <a name="i-am-seeing-hello-monitor-tab-showing-a-session-even-when-i-have-disconnected-or-closed-my-app-emulator"></a>Vengono visualizzati nella scheda Monitoraggio hello che mostra una sessione anche quando ho disconnessa o chiusa l'applicazione o dell'emulatore.
Se si è a questo punto solo una piattaforma di toohello connesso hello e si usa un'app di hello tooopen emulatore si tratta probabilmente a causa di tooemulator quirks. In generale, è necessario tooensure che si tornare toohello schermata nell'emulatore hello per hello app sessione toodisconnect correttamente. Inoltre, nella piattaforma Windows, durante il debug con Visual Studio, potrebbe essere necessario che in Visual Studio venga toohello tooensure **gli eventi del ciclo di vita** barra dei menu e fare clic su **Suspend** tooreally chiudere sessione Hello. Per informazioni dettagliate, vedere l' [esercitazione su Windows](mobile-engagement-windows-store-dotnet-get-started.md) . 

## <a name="analytics-issues"></a>Problemi di analisi
### <a name="i-am-not-seeing-any-data-refreshed-data-on-analytics-tab"></a>I dati o i dati aggiornati non vengono visualizzati nella scheda Analisi
I dati di analisi vengono ricalcolati a intervalli regolati e per l'aggiornamento potrebbero essere necessarie fino a 24 ore. I dati non sono in tempo reale e verranno aggiornati entro questo periodo di tempo di 24 ore.
Assicurarsi tuttavia che si stanno inviando almeno una schermata o back-end di attività toohello piattaforma entrambi override almeno una pagina con `EngagementActivity` o chiamare `SendActivity` in modo esplicito. 

### <a name="i-am-seeing-incorrectly-captured-datetime-for-a-device-on-hello-analytics-tab"></a>Data/ora acquisito in modo non corretto per un dispositivo vengono visualizzati nella scheda Analitica hello
periodo di tempo per Analitica Hello è basato sulle data hello le impostazioni degli utenti hello dei dispositivi. Verificare che hello dispositivo data hello impostato correttamente. 

## <a name="segment-issues"></a>Problemi relativi ai segmenti
### <a name="i-created-a-segment-and-it-is-showing-up-as-greyed-out-or-not-showing-any-data"></a>Il segmento creato viene visualizzato come disattivato o privo di dati
Creazione di segmento non è in tempo reale in un momento hello. Viene calcolato in hello che stesso tempo come vengono aggregati i dati analitica hello e pertanto potrebbero richiedere fino a 24 ore. Controllare nuovamente in un secondo momento, ma nel frattempo è inoltre necessario assicurarsi che le App per dispositivi mobili effettivamente inviano dati hello su base hello di cui si sono formando segmenti hello. Ad esempio, Se ad esempio un evento non viene inviato da qualsiasi dispositivo mobile "foo" quindi sarebbe eventuali dati di segmento per un segmento creato con EventName = foo come criterio di hello. È inoltre consigliabile controllare il tooensure integrazione SDK app per dispositivi mobili invia dati hello correttamente. 

## <a name="reach-or-push-notifications-issues"></a>Problemi di copertura o delle notifiche push
### <a name="my-push-messages-are-not-being-delivered"></a>I messaggi push non vengono recapitati
1. Provare a inviare le notifiche tooa test dispositivo primo tooensure che tutti i componenti di hello - app per dispositivi mobili, il servizio SDK e hello siano connessi correttamente e in grado di toodeliver le notifiche push. 
2. Invia sempre l'hello più semplice 'out-di-notifica dell'app' innanzitutto tramite una campagna di cui non è stata pianificata e non dispone di qualsiasi criterio dei destinatari specificato. Questa funzionalità è nuovamente tooprove che la connettività di notifica funzioni correttamente. 
3. Se si sono verificati problemi di recapito delle notifiche di all'interno dell'applicazione, è anche una buona primo passaggio tootry inviare prima una notifica di fuori dell'app. 
4. Verificare che hello 'Push nativo' sia configurato correttamente per app per dispositivi mobili. A seconda della piattaforma hello si prevede chiavi (Android, Windows) o certificati (iOS). Per informazioni dettagliate, vedere l' [Interfaccia utente - Impostazioni](mobile-engagement-user-interface-settings.md)
5. All'esterno dell'app notifiche potrebbe anche essere bloccate da hello utente tramite hello che pertanto verificare il sistema operativo mobile non è il caso hello. 
6. Verificare che non si sta impostando hello *destinatari ignorare push verrà inviato toousers tramite API hello* opzione hello **campagna** perché in questo modo il push della campagna sezione di una copertura notifiche è possibile solo inviare attraverso le API. 
7. Verificare che la campagna push per la verifica sia un dispositivo connesso tramite Wi-Fi e phone operatore tooeliminate hello rete connessione di rete come possibile origine di problemi.
8. Verificare che hello sistema data/ora l'emulatore sia corretto perché tutti i dispositivi sincronizzati anche interferisce con le notifiche di hello servizio notifica Push possibilità toodeliver. 

Ecco altre istruzioni per la risoluzione dei problemi specifiche per le piattaforme:

1. **iOS** 
   
   * Assicurarsi che i certificati di hello siano valide e non scadute per iOS, le notifiche Push. 
   * Assicurarsi che un certificato di *produzione* sia configurato correttamente nell'app Mobile Engagement. 
   * Assicurarsi di eseguire il test su un *dispositivo fisico reale.* simulatore iOS Hello non è in grado di elaborare i messaggi push.
   * Verificare che hello che identificatore Bundle è configurato correttamente nell'app mobile hello. Vedere le istruzioni di hello [qui](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)
   * Durante il test, utilizzare la distribuzione "Ad Hoc" nel profilo di provisioning per dispositivi mobili. Non sarà in grado di tooreceive notifica se l'applicazione viene compilata utilizzando "Debug"
2. **Android**
   
   * Assicurarsi di avere specificato numero progetto corretto hello nel file AndroidManifest.xml dell'app mobile è seguito dal carattere \n. 
     
           <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
   * Assicurarsi di non risultano mancanti o non configurato tutte le autorizzazioni nel file manifesto Android hello 
   * Verificare che il numero di progetto hello si aggiunge l'app client tooyour da hello stesso account in cui è stato ottenuto hello chiave Server GCM. Mancata corrispondenza tra hello due impedirà il push di uscita. 
   * Se si ricevono sistema notifiche ma non nell'applicazione esaminarne hello [specificare un'icona per sezione notifiche](mobile-engagement-android-get-started.md) come probabilmente non si specifica icona corretta hello nel file manifesto Android hello. 
   * Se si invia una notifica BigPicture, assicurarsi che se si dispone di server immagine esterna, quindi devono toobe in grado di toosupport HTTP "GET" e "HEAD".
3. **Windows**
   
   * Assicurarsi di aver associato hello app con un'applicazione Windows Store valida. In Visual Studio - tooright sarà necessario fare clic su progetto hello e selezionare l'opzione "Associare App con Store" e selezionare hello app che è stato creato in Windows Store hello. Questa app di Windows Store deve essere identico a quello di hello da dove si è ottenuto hello push nativo credenziali tooconfigure nel portale Mobile Engagement hello.
   * Se si ricevono le notifiche push out-of-app ma non le notifiche in-app con l'integrazione `EngagementOverlay` , assicurarsi che la pagina includa un elemento griglia radice. EngagementOverlay utilizza hello primo "Griglia" elemento che si trova in xaml file tooadd due web visualizzazioni della pagina. Se si desidera toolocate in cui verranno impostate visualizzazioni web, è possibile definire una griglia denominata "EngagementGrid" simile al seguente, tuttavia, sarà necessario tooensure è sufficiente altezza e larghezza per hello due successivi web visualizzazioni che mostrano notifica hello e hello seguente annuncio come notifica in-app:
     
           <Grid x:Name="EngagementGrid"></Grid>

### <a name="i-created-a-push-notificationannouncement-campaign-and-even-after-it-sent-me-hello-notification-it-is-showing-as-active-what-does-it-mean"></a>È stata creata un notifica di push/annuncio/campagna e anche dopo che è inviato notifica hello, è visualizzato come 'Active'. Da cosa dipende il problema?
Hello **campagna** creato in Engagement Mobile viene chiamato in modo perché ha un significato di notifica push lunga perché i nuovi dispositivi si connettono piattaforma engagement mobile tooyour, verranno automaticamente inviati notifica hello configurare qui, a condizione che soddisfano il criterio di hello impostati nella campagna hello. La configurazione della notifica richiede più passaggi. Sarà necessario toomanually fare clic su hello **fine** pulsante campagna hello tooterminate in modo che non invia notifiche ulteriormente. 

### <a name="i-created-a-push-campaign-and-i-am-receiving-notifications-successfully-however-whenever-i-open-up-hello-app-i-get-hello-same-notification-even-when-i-had-actioned-it-before"></a>È stata creata una campagna push e si ricevono notifiche correttamente, tuttavia, ogni volta che apre di app hello, viene visualizzato hello notifica stesso, anche quando non aveva prese in considerazione prima?
Si tratta probabilmente toohappen durante i test e se si usano gli emulatori o alcuni framework di test come TestFlight. Qual è il problema è qui che in ogni applicazione in esecuzione l'istanza, è l'acquisizione di un nuovo DeviceID e inviarlo back-end tooour sta causando tootreat piattaforma Mobile Engagement di hello come un nuovo dispositivo e l'invio di notifiche di hello. 

## <a name="getting-support"></a>Ottenere assistenza
Se si è autonomamente il problema di hello tooresolve non è possibile quindi è possibile:

1. Cercare il problema nel thread esistenti di hello sul forum di StackOverflow e [forum MSDN](https://social.msdn.microsoft.com/Forums/windows/en-US/home?forum=azuremobileengagement) e, se non è quindi porre una domanda non esiste. 
2. Se è stata trovata alcuna funzionalità mancante quindi aggiungere/votare hello richiesta nel nostro [forum UserVoice](https://feedback.azure.com/forums/285737-mobile-engagement/)
3. Se si ha Microsoft supporta aprire una richiesta di assistenza fornendo hello seguenti dettagli: 
   * ID sottoscrizione di Azure
   * Piattaforma (ad esempio iOS, Android e così via)
   * ID app
   * ID campagna (per problemi di notifiche push)
   * ID dispositivo
   * Versione di Mobile Engagement SDK (ad esempio Android SDK v2.1.0)
   * Dettagli dell'errore con messaggio di errore esatto e scenario

