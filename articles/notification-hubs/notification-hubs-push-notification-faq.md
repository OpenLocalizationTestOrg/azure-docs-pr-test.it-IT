---
title: Hub di notifica di Azure - Domande frequenti (FAQ) | Documentazione Microsoft
description: Domande frequenti su progettazione/implementazione di soluzioni di Hub di notifica
services: notification-hubs
documentationcenter: mobile
author: ysxu
manager: erikre
keywords: notifica push, notifiche push, notifiche push iOS, notifiche push android, push ios, push android
editor: 
ms.assetid: 7b385713-ef3b-4f01-8b1f-ffe3690bbd40
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 01/19/2017
ms.author: yuaxu
ms.openlocfilehash: a70efa7fc5954966847d5a173e9b10accf4b737e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="push-notifications-with-azure-notification-hubs-frequently-asked-questions"></a>Notifiche push sicure con Hub di notifica di Azure - Domande frequenti
## <a name="general"></a>Generale
### <a name="what-is-hello-resource-structure-of-notification-hubs"></a>Che cos'è una struttura di risorsa hello degli hub di notifica?

Hub di notifica di Azure dispone di due livelli di risorse: hub e spazi dei nomi. Un hub è una risorsa di push unico che può contenere informazioni multipiattaforma push hello di un'applicazione. Uno spazio dei nomi è una raccolta di hub in un'area.

Il mapping consigliato abbina uno spazio dei nomi con un'unica app. In uno spazio dei nomi è possibile configurare un hub di produzione che funzioni con l'app di produzione, un hub di test che funzioni con l'app di test e così via.

### <a name="what-is-hello-price-model-for-notification-hubs"></a>Che cos'è il modello di prezzo hello per gli hub di notifica?
Hello dettagli prezzi più recenti sono reperibili nelle hello [prezzi di hub di notifica] pagina. Gli hub di notifica viene fatturato a livello di spazio dei nomi hello. (Per la definizione di hello uno spazio dei nomi, vedere "Novità struttura risorsa hello degli hub di notifica") Gli hub di notifica offre tre livelli:

* **Gratuito**: questo livello è un buon punto di partenza per esplorare le funzionalità push. Non è consigliabile per le applicazioni di produzione. Si ottengono 500 dispositivi e 1 milione di push inclusi per ogni spazio dei nomi al mese, senza garanzia di Contratto di servizio.
* **Base**: questo livello (o hello Standard) è consigliata per le applicazioni di produzione più piccole. Si ottengono 200.000 dispositivi e 10 milioni di push inclusi per ogni spazio dei nomi al mese come baseline. Sono incluse opzioni di aumento di quota.
* **Standard**: questo livello è consigliato per App di produzione toolarge medio. Si ottengono 10 milioni di dispositivi e 10 milioni di push inclusi per ogni spazio dei nomi al mese come baseline. Sono incluse opzioni di aumento di quota e capacità di telemetria avanzata.

Funzionalità del livello Standard:
* **Telemetria avanzata**: È possibile utilizzare gli hub di notifica per ogni messaggio telemetria tootrack qualsiasi push richieste e Platform Notification System commenti e suggerimenti per il debug.
* **Multi-tenancy**: è possibile lavorare con le credenziali di Platform Notification System a livello di spazio dei nomi. Questa opzione consente si tooeasily dividere l'hub di hello tenant stesso spazio dei nomi.
* **Push pianificate**: È possibile pianificare toobe notifiche inviate in qualsiasi momento.

### <a name="what-is-hello-notification-hubs-sla"></a>Che cos'è contratto di servizio hub di notifica hello?
Per i livelli Basic e Standard hub di notifica configurate correttamente le applicazioni possono inviare notifiche push o eseguire operazioni di gestione di registrazione almeno 99,9% del tempo di hello. informazioni sul contratto di servizio hello, andare toohello toolearn [contratto di servizio hub di notifica](https://azure.microsoft.com/support/legal/sla/notification-hubs/) pagina.

> [!NOTE]
> Poiché le notifiche push dipendono dai sistemi di notifica di piattaforma di terze parti (ad esempio APN di Apple e Google FCM), non c'è garanzia di contratto di servizio per il recapito dei messaggi hello. Dopo gli hub di notifica invia batch hello tooPlatform sistemi di notifica (contratto di servizio garantito), è responsabilità di hello di hello toodeliver di sistemi di notifica tramite piattaforma hello inserisce (alcun contratto di servizio garantito).

### <a name="which-customers-are-using-notification-hubs"></a>Quali clienti utilizzano Hub di notifica?
Molti clienti usano Hub di notifica. Di seguito sono elencati alcuni dei più importanti:

* Sochi 2014: centinaia di gruppi di interesse, oltre 3 milioni di dispositivi e oltre 150 milioni di notifiche inviate nelle due settimane. [Case study: Sochi]
* Skanska: [Case study: Skanska]
* Seattle Times: [Case study: Seattle Times]
* Mural.ly: [Case study: Mural.ly]
* 7Digital: [Case study: 7Digital]
* Bing App: decine di milioni di dispositivi, invio di 3 milioni di notifiche al giorno.

### <a name="how-do-i-upgrade-or-downgrade-my-hub-or-namespace-tooa-different-tier"></a>Come aggiornare o effettuare il downgrade il livello di diversi tooa hub o spazio dei nomi?
Passare toohello  **[portale di Azure]** > **gli spazi dei nomi di hub di notifica** o **gli hub di notifica**. Selezionare risorse hello tooupdate desiderato e andare troppo**tariffario**. Si noti hello seguenti requisiti:

* Hello aggiornato piano tariffario applica troppo*tutti* gli hub nello spazio dei nomi hello in uso.
* Se il numero del dispositivo supera il limite di hello del livello di hello a che esegue il downgrade, è necessario toodelete dispositivi prima effettuare il downgrade.


## <a name="design-and-development"></a>Progettazione e sviluppo
### <a name="which-server-side-platforms-do-you-support"></a>Quali piattaforme sul lato server sono supportate?
Gli SDK server sono disponibili per .NET, Java, Node.js, PHP e Python. Le API di Hub di notifica si basano su interfacce REST, pertanto è possibile lavorare direttamente con le API REST se si usano piattaforme diverse o se non si desidera una dipendenza aggiuntiva. Per ulteriori informazioni, visitare toohello [API REST degli hub di notifica] pagina.

### <a name="which-client-platforms-do-you-support"></a>Quali piattaforme client sono supportate?
È supportato l'invio di notifiche push alle piattaforme [iOS](notification-hubs-ios-apple-push-notification-apns-get-started.md), [Android](notification-hubs-android-push-notification-google-gcm-get-started.md), [Windows Universal](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md), [Windows Phone](notification-hubs-windows-mobile-push-notifications-mpns.md), [Kindle](notification-hubs-kindle-amazon-adm-push-notification.md), [Android China (via Baidu)](notification-hubs-baidu-china-android-notifications-get-started.md), Xamarin ([iOS](xamarin-notification-hubs-ios-push-notification-apns-get-started.md) e [Android](xamarin-notification-hubs-push-notifications-android-gcm.md)), [Chrome Apps](notification-hubs-chrome-push-notifications-get-started.md) e [Safari](https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSafari). Per ulteriori informazioni, visitare toohello [notifica hub introduzione esercitazioni] pagina.

### <a name="do-you-support-text-message-email-or-web-notifications"></a>Sono supportate le notifiche via SMS, messaggi di posta elettronica o Web?
Gli hub di notifica è principalmente progettata toosend notifiche toomobile app. Non offre funzionalità di posta elettronica o SMS. Tuttavia, piattaforme di terze parti che forniscono queste funzionalità possono essere integrate con le notifiche di push nativo toosend gli hub di notifica utilizzando [App per dispositivi mobili].

Inoltre, gli hub di notifica non fornisce un servizio di recapito notifica push nel browser predefinito hello. I clienti possono implementare questa funzionalità utilizzando SignalR su piattaforme di hello è supportato sul lato server. Se si desidera toosend notifiche toobrowser App nell'ambiente sandbox Chrome hello, vedere hello [esercitazione Chrome app].

### <a name="how-are-mobile-apps-and-azure-notification-hubs-related-and-when-do-i-use-them"></a>Come sono correlati App per dispositivi mobili e Hub di notifica di Azure e quando si usano?
Se si dispone di un portatile nuovamente l'app termina e si desidera tooadd solo hello funzionalità toosend push delle notifiche, è possibile usare gli hub di notifica di Azure. Se si desidera tooset il back-end di app per dispositivi mobili da zero, considerare l'utilizzo di funzionalità di App per dispositivi mobili hello di servizio App di Azure. Un'app per dispositivi mobili esegue automaticamente il provisioning di un hub di notifica in modo che è possibile inviare facilmente notifiche push dal back-end di hello app per dispositivi mobili. Prezzi per App per dispositivi mobili include gli addebiti di base hello per un hub di notifica. Si pagano solo quando si supera hello incluso inserimenti. Per ulteriori informazioni sui costi, visitare toohello [prezzi del servizio App] pagina.

### <a name="how-many-devices-can-i-support-if-i-send-push-notifications-via-notification-hubs"></a>Quanti dispositivi sono supportati se si inviano notifiche push tramite Hub di notifica?
Fare riferimento toohello [prezzi di hub di notifica] per ulteriori informazioni sul numero di hello dei dispositivi supportati.

Se è necessario il supporto per più di 10 milioni di dispositivi registrati, [contattare direttamente il supporto di Azure](https://azure.microsoft.com/overview/contact-us/) per informazioni su come ridimensionare la soluzione.

### <a name="how-many-push-notifications-can-i-send-out"></a>Quante notifiche push si può inviare?
In base al piano selezionato hello, gli hub di notifica di Azure viene ridimensionato automaticamente in base al numero di hello di notifiche che passano attraverso il sistema hello.

> [!NOTE]
> Hello costo dell'utilizzo complessivo può aumentare in base al numero di hello di notifiche push servito. Assicurarsi che sia attiva la conoscenza dei limiti di livello hello descritti nel hello [prezzi di hub di notifica] pagina.
> 
> 

I clienti usano gli hub di notifica toosend milioni di notifiche push ogni giorno. Non si dispone toodo nulla tooscale speciali hello raggiungere delle notifiche push, purché si usa l'hub di notifica di Azure.

### <a name="how-long-does-it-take-for-sent-push-notifications-tooreach-my-device"></a>Quanto tempo fa take per inviato tooreach le notifiche push il dispositivo?
In uno scenario di utilizzo normale, dove carico in ingresso hello è coerenza e, anche gli hub di notifica di Azure in grado di elaborare almeno *notifica push di 1 milione invia un minuto*. Questa frequenza potrebbe variare in base numero hello di tag, natura hello di hello in arrivo inviati e altri fattori esterni.

Durante la fase di recapito hello stimato, servizio hello calcola le destinazioni per ogni piattaforma hello e instrada i messaggi toohello Push Notification Service (PNS) in base a tag hello registrato o espressioni tag. È responsabilità di hello del dispositivo toohello di hello PNS toosend le notifiche.

Hello PNS non garantisce che qualsiasi contratto di servizio per il recapito delle notifiche. Tuttavia, la maggior parte delle notifiche push vengono recapitate tootarget dispositivi entro pochi minuti (in genere entro 10 minuti) dall'ora hello inviati tooNotification hub. Alcune notifiche potrebbero richiedere più tempo.

> [!NOTE]
> Hub di notifica di Azure dispone di un criterio in luogo toodrop le notifiche push non recapitate toohello PNS entro 30 minuti. Questo ritardo può verificarsi per diversi motivi, ma la maggior parte delle comunemente perché hello PNS è la limitazione delle richieste dell'applicazione.
> 
> 

### <a name="is-there-any-latency-guarantee"></a>La latenza è garantita?
A causa di natura hello di notifiche push (vengano recapitati da un sistema esterno, specifici della piattaforma PNS), non c'è garanzia di latenza. In genere, la maggior parte hello di notifiche push vengono recapitati entro pochi minuti.

### <a name="what-do-i-need-tooconsider-when-designing-a-solution-with-namespaces-and-notification-hubs"></a>Cosa fare quando si progetta una soluzione con gli hub di notifica e di spazi dei nomi, è necessario tooconsider?
#### <a name="mobile-appenvironment"></a>Ambiente/app per dispositivi mobili
* Usare un hub di notifica per ogni app per dispositivi mobili per ogni ambiente.
* In uno scenario multi-tenant ogni tenant deve avere un hub separato.
* Condivisione hello mai stesso hub di notifica per gli ambienti di produzione e test. Ciò potrebbe causare problemi durante l'invio delle notifiche. Apple offre endpoint Sandbox e Production Push, che hanno credenziali separate.
* Per impostazione predefinita, è possibile inviare i dispositivi di test notifiche tooyour registrato tramite il portale di Azure hello o hello Azure componente integrato in Visual Studio. soglia di Hello è impostato too10 dispositivi che vengono selezionati casualmente dal pool di registrazione hello.

> [!NOTE]
> Se l'hub è stato originariamente configurato con un certificato per Apple sandbox e quindi è stato riconfigurato toouse un certificato di produzione di Apple, hello originale i token non sono validi. Token non validi comportano toofail push. Separare l'ambiente di test da quello di produzione e usare hub diversi per ambienti diversi.
> 
> 

#### <a name="pns-credentials"></a>Credenziali PNS
Quando un'app per dispositivi mobili viene registrata con il portale per sviluppatori della piattaforma (ad esempio Apple o Google), vengono inviati un identificatore app e i token di sicurezza. back-end di Hello app offre queste funzionalità PNS della piattaforma di token toohello in modo che sia possibile inviare notifiche push toodevices. I token di sicurezza possono essere sotto forma di hello di certificati (ad esempio, Apple iOS o Windows Phone) o le chiavi di sicurezza (ad esempio, Google Android o Windows). Devono essere configurati in hub di notifica. Configurazione in genere viene eseguita a livello di hub di notifica di hello, ma possono essere eseguita anche a livello di spazio dei nomi hello in uno scenario di multi-tenant.

#### <a name="namespaces"></a>Spazi dei nomi
Gli spazi dei nomi possono essere usati anche per il raggruppamento di distribuzione. Possono anche essere utilizzati toorepresent tutti gli hub di notifica per tutti i tenant di hello stessa app in uno scenario di multi-tenant.

#### <a name="geo-distribution"></a>Distribuzione geografica
La distribuzione geografica non è sempre fondamentale negli scenari di notifiche push. PNSes diversi (ad esempio, APNS o GCM) che consentono di distribuire toodevices le notifiche push non sono distribuite in modo uniforme.

Se si dispone di un'applicazione che viene utilizzata a livello globale, è possibile creare hub in spazi dei nomi diversi tramite servizio hub di notifica hello in diverse aree di Azure in tutto il mondo hello.

> [!NOTE]
> Tuttavia non si consiglia di farlo, perché in questo modo aumenta il costo di gestione, in particolare per le registrazioni. Si consiglia di farlo solo se vi è l'esigenza esplicita.
> 
> 

### <a name="should-i-do-registrations-from-hello-app-back-end-or-directly-through-client-devices"></a>È necessario fare registrazioni dal back-end di hello app o direttamente tramite il client di dispositivi?
Registrazioni dal back-end di hello app sono utili quando si dispone di client tooauthenticate prima di creare una registrazione hello. Sono utili anche quando si dispone di tag che devono essere creati o modificati dal back-end app hello in base alla logica di app. Per ulteriori informazioni, visitare toohello [indicazioni registrazione back-end] e [indicazioni registrazione back-end 2] pagine.

### <a name="what-is-hello-push-notification-delivery-security-model"></a>Che cos'è modello di sicurezza recapito notifica push hello?
Hub di notifica di Azure usa un modello di sicurezza basato sulla [firma di accesso condiviso](../storage/common/storage-dotnet-shared-access-signature-part-1.md). È possibile utilizzare i token di firma di accesso condiviso hello a livello di spazio dei nomi radice hello o a livello di hub di notifica granulare hello. I token di firma di accesso condiviso possono essere set toofollow diverse regole di autorizzazione, ad esempio, le autorizzazioni di messaggio toosend o toolisten per le autorizzazioni di notifica. Per ulteriori informazioni, vedere hello [il modello di sicurezza degli hub di notifica] documento.

### <a name="how-should-i-handle-sensitive-payload-in-push-notifications"></a>Come si gestisce un payload sensibile nelle notifiche push?
Tutte le notifiche vengono recapitate tootarget dispositivi dal PNS della piattaforma hello. Quando tooAzure gli hub di notifica viene inviata una notifica, viene elaborata ed passato toohello rispettivi PNS.

Tutte le connessioni da hello mittente toohello gli hub di notifica di Azure toohello PNS, utilizzano HTTPS.

> [!NOTE]
> Hub di notifica di Azure non registra payload hello dei messaggi in alcun modo.
> 
> 

payload sensibili toosend, è consigliabile utilizzare un modello Push Secure. mittente Hello invia una notifica di ping con un dispositivo toohello identificatore di messaggio senza payload sensibili hello. Quando hello app sul dispositivo hello riceve payload hello, app hello chiama un'API protetta direttamente toofetch hello i dettagli del messaggio. Per una Guida su come tooimplement questo modello, visitare toohello [notifica hub Secure Push esercitazione] pagina.

## <a name="operations"></a>Operazioni
### <a name="what-support-is-provided-for-disaster-recovery"></a>Quale supporto è fornito per il ripristino di emergenza?
Vengono forniti copertura di ripristino di emergenza dei metadati da parte nostra (nome hub di notifica hello, la stringa di connessione hello e altre informazioni critiche). Quando viene attivato uno scenario di ripristino di emergenza, i dati di registrazione sono hello *solo segmento* dell'infrastruttura di hub di notifica hello che non viene persa. È necessario tooimplement toorepopulate una soluzione questi dati nel nuovo post-ripristino hub:

1. Creare un hub di notifica secondario in un controller di dominio diverso. È consigliabile crearne uno nuovo da tooshield inizio hello è da un evento di ripristino di emergenza che potrebbe interessare le funzionalità di gestione. È anche possibile creare uno alla volta hello dell'evento di ripristino di emergenza hello.

2. È necessario compilare hub di notifica secondaria hello con registrazioni hello dall'hub di notifica primario. È non consigliabile tentativo registrazioni toomaintain su entrambi hub e mantenerli sincronizzati come registrazioni disponibili in. Questa procedura non funziona correttamente a causa di tendenza di inerente hello delle registrazioni tooexpire hello lato PNS. Hub di notifica le elimina quando riceve il feedback PNS sulle registrazioni scadute o non valide.  

Per i back-end dell'app ci sono due raccomandazioni:

* Usare un back-end di app che mantenga un determinato set di registrazioni sul proprio lato. Hub di notifica secondaria hello può quindi eseguire un inserimento bulk.

* Utilizzare un back-end app che ottiene un dump regolare di registrazioni da hub di notifica primario hello come backup. Hub di notifica secondaria hello può quindi eseguire un inserimento bulk.

> [!NOTE]
> Funzionalità di esportazione/importazione di registrazioni disponibili nel livello Standard hello è descritta in hello [esportazione/importazione di registrazioni] documento.
> 
> 

Se non si ha un back-end, all'avvio di hello app nei dispositivi di destinazione, eseguono una nuova registrazione nell'hub di notifica secondaria hello. Infine hello hub di notifica secondaria saranno disponibili tutti i dispositivi attivi hello registrati.

Vi sarà un periodo di tempo in cui i dispositivi con app non aperte non riceveranno le notifiche.

### <a name="is-there-audit-log-capability"></a>È disponibile una funzionalità di log di controllo?
Tutte le operazioni di gestione degli hub di notifica passare registri toooperation, che vengono esposte in hello [portale di Azure classico].

## <a name="monitoring-and-troubleshooting"></a>Monitoraggio e risoluzione dei problemi
### <a name="what-troubleshooting-capabilities-are-available"></a>Quali funzionalità di risoluzione dei problemi sono disponibili?
Hub di notifica di Azure offre numerose funzionalità per la risoluzione dei problemi, in particolare per scenario più comune di hello di notifiche eliminate. Per informazioni dettagliate, vedere hello [la risoluzione dei problemi di hub di notifica] white paper relativo alle.

### <a name="what-telemetry-features-are-available"></a>Sono disponibili le funzionalità di telemetria?
Visualizzazione di dati di telemetria in hello Azure consente di hub di notifica [portale di Azure classico]. Dettagli delle metriche hello sono disponibili su hello [le metriche di hub di notifica] pagina.

> [!NOTE]
> Notifiche operazioni riuscite significa semplicemente che sono state inviate le notifiche push toohello esterno PNS (ad esempio, APN di Apple) o GCM per Google. È responsabilità di hello dispositivi hello PNS toodeliver hello notifiche tootarget. In genere, hello PNS non espone entità toothird metriche di recapito.  
> 
> 

È anche possibile fornire hello funzionalità tooexport hello i dati di telemetria a livello di codice (nel livello Standard hello). Per informazioni dettagliate, vedere hello [esempio metriche di hub di notifica].

[portale di Azure classico]: https://manage.windowsazure.com
[prezzi di hub di notifica]: http://azure.microsoft.com/pricing/details/notification-hubs/
[Notification Hubs SLA]: http://azure.microsoft.com/support/legal/sla/
[Case Study: Sochi]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=7942
[Case Study: Skanska]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=5847
[Case Study: Seattle Times]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=8354
[Case Study: Mural.ly]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=11592
[Case Study: 7Digital]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=3684
[API REST degli hub di notifica]: https://msdn.microsoft.com/library/azure/dn530746.aspx
[notifica hub introduzione esercitazioni]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/
[esercitazione Chrome app]: http://azure.microsoft.com/documentation/articles/notification-hubs-chrome-get-started/
[Mobile Services Pricing]: http://azure.microsoft.com/pricing/details/mobile-services/
[indicazioni registrazione back-end]: https://msdn.microsoft.com/library/azure/dn743807.aspx
[indicazioni registrazione back-end 2]: https://msdn.microsoft.com/library/azure/dn530747.aspx
[il modello di sicurezza degli hub di notifica]: https://msdn.microsoft.com/library/azure/dn495373.aspx
[notifica hub Secure Push esercitazione]: http://azure.microsoft.com/documentation/articles/notification-hubs-aspnet-backend-ios-secure-push/
[la risoluzione dei problemi di hub di notifica]: http://azure.microsoft.com/documentation/articles/notification-hubs-diagnosing/
[le metriche di hub di notifica]: https://msdn.microsoft.com/library/dn458822.aspx
[esempio metriche di hub di notifica]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/FetchNHTelemetryInExcel
[esportazione/importazione di registrazioni]: https://msdn.microsoft.com/library/dn790624.aspx
[portale di Azure]: https://portal.azure.com
[complete samples]: https://github.com/Azure/azure-notificationhubs-samples
[App per dispositivi mobili]: https://azure.microsoft.com/services/app-service/mobile/
[prezzi del servizio App]: https://azure.microsoft.com/pricing/details/app-service/
