---
title: aaaAzure gli hub di notifica
description: "Informazioni su come tooadd push con hub di notifica di Azure, le funzionalità di notifica."
author: ysxu
manager: erikre
editor: 
services: notification-hubs
documentationcenter: 
ms.assetid: fcfb0ce8-0e19-4fa8-b777-6b9f9cdda178
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: multiple
ms.devlang: multiple
ms.topic: article
ms.date: 1/17/2017
ms.author: yuaxu
ms.openlocfilehash: 78ce34b6b094b560c8002ab9652f7ba4563c5c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs"></a>Hub di notifica di Azure
## <a name="overview"></a>Panoramica
Hub di notifica di Azure offre un motore di push di facile uso, multipiattaforma e con scalabilità orizzontale. Con una chiamata all'API multipiattaforma singolo, è possibile inviare facilmente piattaforma mobile tooany di notifiche push personalizzate e di destinazione da qualsiasi back-end cloud o locale.

Hub di notifica funziona perfettamente per scenari aziendali e di consumo. Di seguito sono riportati alcuni esempi degli usi di Hub di notifica fatti dai clienti:

* Inviare ultime notizie notifiche toomillions con bassa latenza.
* Inviare coupon basati sulla posizione segmenti utente toointerested.
* Inviare notifiche relative a eventi toousers o gruppi per le applicazioni di supporto/sportive/finance/giochi.
* Push contenuto promozionale tooapps tooengage e mercato toocustomers.
* Notifiche agli utenti su eventi aziendali, come nuovi messaggi ed elementi di lavoro.
* Invio di codici per l'autenticazione a più fattori.

## <a name="what-are-push-notifications"></a>Cosa sono le notifiche push?
Le notifiche push sono una forma di comunicazione tra l'app e l'utente in cui gli utenti delle app per dispositivi mobili vengono informati di determinate notizie desiderate, in genere con una finestra popup o con una finestra di dialogo. Gli utenti possono in genere scegliere tooview o chiudere il messaggio hello e scegliendo ex hello verrà aperto l'app per dispositivi mobili hello che comunicata notifica hello.

Le notifiche push sono fondamentali per le app di consumo perché aumentano l'interesse e l'uso delle app, mentre per le app aziendali favoriscono la comunicazione di informazioni aziendali aggiornate. È la comunicazione di app-utente migliore hello perché è più efficiente per i dispositivi mobili, flessibili per i mittenti notifiche hello e disponibili mentre le applicazioni corrispondenti non sono attive.

Maggiori informazioni sulle notifiche push per alcune piattaforme più comuni:
* [iOS](https://developer.apple.com/notifications/)
* [Android](https://developer.android.com/guide/topics/ui/notifiers/notifications.html)
* [Windows](http://msdn.microsoft.com/library/windows/apps/hh779725.aspx)

## <a name="how-push-notifications-work"></a>Funzionamento delle notifiche push
Le notifiche push vengono recapitate attraverso infrastrutture specifiche della piattaforma denominate *Platform Notification System* (PNS). Offrono le funzionalità di push barebone dispositivo di tooa toodelivery messaggio con un oggetto fornito la gestione e non hanno nessuna interfaccia comune. una notifica toosend tooall clienti attraverso hello iOS, Android e Windows versioni di un'app, sviluppatore hello deve funzionare con APNS (Apple Push Notification Service), FCM (messaggistica Cloud Firebase) e WNS (Windows Notification Service), durante l'invio in batch Invia Hello.

In particolare, ecco come funziona un push:

1. app client Hello decide che desidera tooreceive effettua il push pertanto hello contatti PNS tooretrieve corrispondente al relativo handle push univoco e temporanei. tipo di handle Hello dipende dal sistema hello (ad esempio, WNS ha URI mentre APN ha token).
2. app client Hello archivia l'handle nel back-end app hello o provider.
3. toosend una notifica push, hello app back-end contatta hello PNS usando hello handle tootarget un'app client specifico.
4. Hello PNS inoltra dispositivo toohello di notifica hello specificato dall'handle hello.

![][0]

## <a name="hello-challenges-of-push-notifications"></a>Hello sfide di notifiche Push
Mentre PNSes sono potenti, lasciano lo sviluppatore di app di lavoro toohello in ordine tooimplement anche push notifica scenari comuni, ad esempio la trasmissione o l'invio di utenti toosegmented le notifiche push.

Push è uno dei hello richiesto più funzionalità di servizi cloud per dispositivi mobili, perché il relativo utilizzo richiede infrastrutture complesse di logica di business principale dell'applicazione di toohello non correlati. Alcune delle problematiche infrastrutturali hello sono:

* **Dipendenza dalla piattaforma**: 

  * back-end Hello deve toohave complesse e disco rigido per gestire la logica dipendente dalla piattaforma toosend notifiche toodevices su varie piattaforme come PNSes non vengono unificati.
* **Scalabilità**:

  * In base alle linee guida dei sistemi PNS,è necessario aggiornare i token di dispositivo a ogni avvio dell'app. Ciò significa back-end hello riguarda una grande quantità di traffico e database appena tookeep hello i token di accesso aggiornati. Quando il numero di hello di dispositivi cresce toohundreds e migliaia di milioni, costo hello della creazione e gestione dell'infrastruttura è notevole.
  * PNSes la maggior parte delle non supportano i dispositivi toomultiple broadcast. Ciò significa un semplice tooa broadcast risultati di milioni di dispositivi in chiamate di un milione toohello PNSes. La scalabilità di questa quantità di traffico con latenza minima è molto complessa.
* **Routing**:
  
  * Se PNSes garantiscono un toodevices di messaggi toosend modo, la maggior parte delle notifiche di App sono destinate a utenti o gruppi di interesse. Ciò significa back-end hello deve gestire i dispositivi di tooassociate un registro di sistema con gruppi di interesse, gli utenti, le proprietà e così via. Questo sovraccarico contribuisce toohello ora toomarket costi di manutenzione e di un'app.

## <a name="why-use-notification-hubs"></a>Perché usare gli Hub di notifica?
Hub di notifica elimina tutte le complessità associate all'abilitazione autonoma del push. L'infrastruttura di notifiche push multipiattaforma e con scalabilità orizzontale riduce i codici dei push e semplifica il back-end. Con gli hub di notifica, i dispositivi sono semplicemente responsabili della registrazione i relativi handle PNS con un hub, mentre il back-end hello invia messaggi toousers o gruppi di interesse, come illustrato nella seguente illustrazione hello:

![][1]

Gli hub di notifica è il motore di push pronto all'uso con hello seguenti vantaggi:

* **Multipiattaforma**

  * Supporta tutte le principali piattaforme push tra cui iOS, Android, Window, Kindle e Baidu.
  * Una comune interfaccia toopush tooall piattaforme in formati specifici della piattaforma o indipendente dalla piattaforma senza lavoro specifico della piattaforma.
  * Consente di gestire l'handle di dispositivo in un solo posto.
* **Multi back-end**
  
  * Cloud o in locale
  * .NET, Node. js, Java e così via.
* **Insieme completo di modelli di recapito**:

  * *Trasmissione tooone o più piattaforme*: È possibile trasmettere immediatamente toomillions dei dispositivi tra le piattaforme con una singola chiamata API.
  * *Push toodevice*: È possibile fare riferimento ai dispositivi tooindividual di notifiche.
  * *Push toouser*: tag e i modelli che consentono di raggiungere tutti i dispositivi multipiattaforma di un utente.
  * *Push toosegment con tag dinamico*: funzione tag consente di segmentare i dispositivi e push toothem in base alle esigenze tooyour, se si inviano tooone segmento o un'espressione di segmenti (ad esempio active AND risiede in Seattle non nuovo utente). Anziché essere limitati toopub-sub, è possibile aggiornare i tag in un punto qualsiasi del dispositivo e in qualsiasi momento.
  * *Push localizzato*: la funzione modelli consente di ottenere la localizzazione senza influire sul codice di back-end.
  * *Push invisibile all'utente*: È possibile consente modello push-a-pull hello mediante l'invio di notifiche invisibile all'utente toodevices e attivazione di toocomplete determinati pull o azioni.
  * *Push pianificate*: È possibile pianificare toosend notifiche in qualsiasi momento.
  * *Indirizzare push*: È possibile ignorare la registrazione dispositivi con i servizi ed elenco tooa push di batch di handle di dispositivo direttamente.
  * *Push personalizzati*: le variabili push del dispositivo consentono di inviare notifiche push personalizzate specifiche per il dispositivo con coppie chiave-valore personalizzate.
* **Telemetria avanzata**
  
  * Dati di telemetria push, dispositivo, errore e operazione generale è disponibile nel portale di Azure hello e a livello di codice.
  * Per ogni messaggio telemetria tracce ogni push dal servizio tooour chiamata richiesta iniziale correttamente l'invio in batch hello effettuato il push.
  * Commenti e suggerimenti del sistema di notifica piattaforma comunica i feedback dei sistemi di notifica Platform tooassist eseguire il debug.
* **Scalabilità** 
  
  * Inviare messaggi veloce toomillions dei dispositivi senza partizionamento orizzontale riprogettazione o dispositivo.
* **Sicurezza**

  * Firma di accesso condiviso (SAS) o autenticazione federata.

## <a name="integration-with-app-service-mobile-apps"></a>Integrazione con le app per dispositivi mobili del servizio app
un'esperienza trasparente e unificata in servizi di Azure, toofacilitate [App per dispositivi mobili del servizio App] include il supporto incorporato per le notifiche push tramite hub di notifica. [App per dispositivi mobili del servizio App] offre una piattaforma di sviluppo di applicazioni per dispositivi mobili altamente scalabili e disponibili a livello globale per gli sviluppatori aziendali e integratori di sistemi che offre una vasta gamma di funzionalità agli sviluppatori di toomobile.

Gli sviluppatori di applicazioni per dispositivi mobili è possono utilizzare gli hub di notifica con hello del flusso di lavoro seguente:

1. Recuperare la gestione del dispositivo PNS
2. Registrare il dispositivo con gli Hub di notifica mediante il pratico API Register SDK client delle app per dispositivi mobili
   * Si noti che le app per dispositivi mobili consentono di eliminare tutti i tag nelle registrazioni per motivi di sicurezza. Lavorare con gli hub di notifica dal back-end direttamente tooassociate tag con i dispositivi.
3. Invio di notifiche dal back-end dell'app con hub di notifica

Ecco alcuni vantaggi portati toodevelopers con questa integrazione:

* **SDK Client di App mobile**: questi SDK di multi-piattaforma fornisce API semplice per la registrazione e comunicare con hub di notifica toohello collegato con app per dispositivi mobili hello automaticamente. Gli sviluppatori non necessarie toodig tramite le credenziali di hub di notifica e lavorare con un servizio aggiuntivo.

  * *Push toouser*: hello SDK automaticamente tag hello dispositivo con App per dispositivi mobili autenticati ID utente tooenable push toouser scenario specificato.
  * *Push toodevice*: hello SDK utilizzare automaticamente hello ID di installazione di App Mobile come GUID tooregister con gli hub di notifica, risparmiando agli sviluppatori di problemi di hello di gestione di più GUID di servizio.
* **Modello di installazione**: App per dispositivi mobili funziona con più recenti push modello toorepresent gli hub di notifica tutte le proprietà associate a un dispositivo in un'installazione di JSON in linea con servizi notifica Push che è facile toouse di push.
* **Flessibilità**: gli sviluppatori possono scegliere sempre toowork con gli hub di notifica direttamente anche con l'integrazione di hello sul posto.
* **Esperienza integrata [portale di Azure]**: Push come una funzionalità di rappresentazione visiva di App per dispositivi mobili e gli sviluppatori possono operare con facilità con hub di notifica associato hello tramite App per dispositivi mobili.

## <a name="next-steps"></a>Passaggi successivi
Nei seguenti argomenti sono disponibili altre informazioni su Hub di notifica:

* **[Uso di Hub di notifica da parte dei clienti]**
* **[Esercitazioni e guide su Hub di notifica]**
* **Introduzione ad Hub di notifica**: [iOS], [Android], [Windows Universal], [Windows Phone], [Kindle], [Xamarin.iOS], [Xamarin.Android]

[0]: ./media/notification-hubs-overview/registration-diagram.png
[1]: ./media/notification-hubs-overview/notification-hub-diagram.png
[Uso di Hub di notifica da parte dei clienti]: http://azure.microsoft.com/services/notification-hubs
[Esercitazioni e guide su Hub di notifica]: http://azure.microsoft.com/documentation/services/notification-hubs
[iOS]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started
[Android]: http://azure.microsoft.com/documentation/articles/notification-hubs-android-get-started
[Windows Universal]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started
[Windows Phone]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-phone-get-started
[Kindle]: http://azure.microsoft.com/documentation/articles/notification-hubs-kindle-get-started
[Xamarin.iOS]: http://azure.microsoft.com/documentation/articles/partner-xamarin-notification-hubs-ios-get-started
[Xamarin.Android]: http://azure.microsoft.com/documentation/articles/partner-xamarin-notification-hubs-android-get-started
[Microsoft.WindowsAzure.Messaging.NotificationHub]: http://msdn.microsoft.com/library/microsoft.windowsazure.messaging.notificationhub.aspx
[Microsoft.ServiceBus.Notifications]: http://msdn.microsoft.com/library/microsoft.servicebus.notifications.aspx
[App per dispositivi mobili del servizio App]: https://azure.microsoft.com/en-us/documentation/articles/app-service-mobile-value-prop/
[templates]: notification-hubs-templates-cross-platform-push-messages.md
[portale di Azure]: https://portal.azure.com
[tags]: (http://msdn.microsoft.com/library/azure/dn530749.aspx)
