---
title: Panoramica di IoT Hub aaaAzure | Documenti Microsoft
description: "Panoramica del servizio dell'IoT Hub Azure hello: che cos'è l'IoT Hub, internet di modelli di comunicazione di operazioni, i gateway e il modello di comunicazione assistita da servizio di hello e la connettività dei dispositivi"
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0b46868a1ec9e13c8f107b90269c5307f4ba27c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-hello-azure-iot-hub-service"></a>Panoramica di hello servizio IoT Hub Azure

Benvenuti tooAzure IoT Hub. In questo articolo viene fornita una panoramica dell'IoT Hub di Azure e descrive perché è consigliabile utilizzare questo tooimplement servizio una soluzione di Internet delle cose (IoT). L'hub IoT di Azure è un servizio completamente gestito che consente comunicazioni bidirezionali affidabili e sicure tra milioni di dispositivi IoT e un back-end della soluzione. L'hub IoT di Azure:

* Offre più opzioni di comunicazione dispositivo a cloud e cloud a dispositivo, inclusi la messaggistica unidirezionale, il trasferimento di file e i metodi di risposta alle richieste.
* Fornisce messaggi dichiarativa incorporata routing tooother servizi di Azure.
* Offre un archivio in cui eseguire query sui metadati e informazioni di stato sincronizzate.
* Abilita comunicazioni sicure e controllo di accesso tramite chiavi di sicurezza per dispositivo o certificati X.509.
* Fornisce un monitoraggio esteso per gli eventi relativi alla connettività dei dispositivi e alla gestione delle identità dei dispositivi.
* Include le librerie di dispositivo per i linguaggi più diffusi hello e piattaforme.

articolo Hello [confronto dell'IoT Hub e hub di eventi] [ lnk-compare] descrive hello le principali differenze tra questi due servizi ed evidenzia hello vantaggi derivanti dall'utilizzo IoT Hub nelle soluzioni IoT.

Per ulteriori informazioni su come Azure e l'IoT Hub proteggere soluzione IoT, vedere [sicurezza di Internet delle cose da hello messa a terra][lnk-security-ground-up].

![Hub IoT di Azure come gateway cloud in una soluzione Internet delle cose][img-architecture]

> [!NOTE]
> Per un'analisi approfondita dell'architettura di IoT, vedere hello [architettura di riferimento di Microsoft Azure IoT][lnk-refarch].

## <a name="iot-device-connectivity-challenges"></a>Problematiche relative alla connettività dei dispositivi IoT

IoT Hub e hello raccolte di dispositivi consentono di sfide hello toomeet come tooreliably e connettersi in modo sicuro i dispositivi toohello soluzione back-end. Dispositivi IoT:

* Sono spesso sistemi incorporati senza operatore umano.
* Possono trovarsi in località remote, dove l'accesso fisico è molto costoso.
* Può essere solo raggiungibile tramite hello soluzione back-end.
* Possono avere risorse di alimentazione e di elaborazione limitate.
* Possono disporre di una connettività di rete intermittente, lenta o costosa.
* Potrebbe essere necessario toouse protocolli di applicazioni proprietarie, personalizzati o specifici del settore.
* Possono essere create utilizzando un'ampia gamma di piattaforme hardware e software molto comuni.

Inoltre toohello requisiti sopra riportati, qualsiasi soluzione IoT deve inoltre offrire scalabilità, sicurezza e affidabilità. set di requisiti di connettività risultante Hello è difficile e lunga tooimplement quando si utilizzano le tecnologie tradizionali, ad esempio gestori di messaggistica e di contenitori di web.

## <a name="why-use-azure-iot-hub"></a>Perché usare l'hub IoT di Azure?

Inoltre cui tooa una vasta gamma di [da dispositivo a cloud] [ lnk-d2c-guidance] e [cloud a dispositivo] [ lnk-c2d-guidance] opzioni di comunicazione, inclusi messaggistica, file i trasferimenti e metodi di richiesta-risposta, gli indirizzi di IoT Hub Azure hello problemi di connettività dei dispositivi in hello seguenti modi:

* **Dispositivi gemelli**. Con l'uso dei [dispositivi gemelli ][lnk-twins], è possibile archiviare, sincronizzare ed eseguire query sui metadati e sulle informazioni di stato del dispositivo. I dispositivi gemelli sono documenti JSON nei quali vengono archiviate informazioni sullo stato dei dispositivi (metadati, configurazioni e condizioni). IoT Hub persiste doppi un dispositivo per ogni dispositivo che si connette tooIoT Hub.

* **Autenticazione e connettività sicura per ogni dispositivo**. È possibile eseguire il provisioning di ogni dispositivo con il proprio [chiave di sicurezza] [ lnk-devguide-security] tooenable è tooconnect tooIoT Hub. Hello [registro identità IoT Hub] [ lnk-devguide-identityregistry] le identità del dispositivo e le chiavi vengono archiviati in una soluzione. Una soluzione di back-end può aggiungere tooallow singoli dispositivi o negare elenchi tooenable il controllo completo sul dispositivo l'accesso.

* **Route da dispositivo a cloud messaggi servizi tooAzure in base alle regole dichiarative**. IoT Hub consente di toodefine messaggio route in base al routing toocontrol regole in cui l'hub invia i messaggi da dispositivo a cloud. Regole di routing non richiedono alcun codice si toowrite e possono avvenire hello del dispatcher di messaggio personalizzato di post-operazione di inserimento.

* **Monitoraggio delle operazioni di connettività dei dispositivi**. È possibile ricevere i log dettagliati sulle operazioni di gestione delle identità dei dispositivi e sugli eventi di connettività dei dispositivi. Questa funzionalità di monitoraggio consente i problemi di connettività IoT soluzione tooidentify, ad esempio i dispositivi che tooconnect con credenziali non corrette, provare a inviare messaggi troppo spesso o rifiutare tutti i messaggi da cloud a dispositivo.

* **Un set completo di librerie di dispositivi**. Gli [Azure IoT SDK per dispositivi][lnk-device-sdks] sono disponibili e supportati per vari linguaggi e piattaforme: C per diverse distribuzioni Linux, Windows e sistemi operativi in tempo reale. Gli SDK per dispositivi Azure IoT supportano inoltre linguaggi gestiti, ad esempio C#, Java e JavaScript.

* **Protocolli IoT ed estensibilità**. Se la soluzione non è possibile utilizzare librerie dispositivo hello, IoT Hub espone un protocollo pubblico che consente di dispositivi toonatively utilizzare hello MQTT v3.1.1, HTTP 1.1 o protocolli di AMQP 1.0. È anche possibile estendere toosupport IoT Hub per protocolli personalizzati da:

  * Creazione di un gateway di campo con [Azure IoT Edge] [ lnk-iot-edge] che converte i tooone protocollo personalizzato di hello tre protocolli riconosciuti dall'IoT Hub.
  * Personalizzazione hello [gateway del protocollo Azure IoT][protocol-gateway], un componente di origine aperti che viene eseguito nel cloud hello.

* **Scalabilità**. IoT Hub Azure scala toomillions di dispositivi connessi contemporaneamente e milioni di eventi al secondo.

## <a name="gateways"></a>Gateway

Un gateway in una soluzione IoT è in genere un [gateway del protocollo] [ lnk-iotedge] che viene distribuito nel cloud hello o un [gateway campo] [ lnk-field-gateway] ovvero distribuito localmente con i dispositivi. Un gateway di protocollo esegue la conversione di protocollo, ad esempio MQTT tooAMQP. Un gateway campo puoi eseguire analitica sul bordo hello, prendere le decisioni di scadenza tooreduce latenza, fornire servizi di gestione dei dispositivi, applicare la protezione e i vincoli sulla privacy e inoltre eseguire conversione di protocollo. Entrambi i tipi di gateway fungono da intermediari tra i dispositivi e l'hub IoT.

Un gateway sul campo differisce da un semplice dispositivo di routing del traffico, ad esempio un firewall o un dispositivo NAT (Network Address Translation), in quanto in genere esegue un ruolo attivo nella gestione dell'accesso e del flusso di informazioni nella soluzione.

Una soluzione può includere sia gateway di protocollo che gateway campo.

## <a name="how-does-iot-hub-work"></a>Come funziona l’Hub IoT?

IoT Hub Azure implementa hello [assistito servizio comunicazione] [ lnk-service-assisted-pattern] interazioni di hello toomediate modello tra i dispositivi e la soluzione di back-end. obiettivo di Hello assistita da servizio di comunicazione è tooestablish attendibile, bidirezionale percorsi di comunicazione tra un sistema di controllo, ad esempio IoT Hub e dispositivi speciali che vengono distribuiti nello spazio fisico non attendibile. modello Hello stabilisce hello principi seguenti:

* La sicurezza ha la precedenza su tutte le altre funzionalità.

* I dispositivi non accettano informazioni di rete non richieste. Un dispositivo stabilisce tutte le connessioni e le route in modalità solo in uscita. Per un dispositivo tooreceive un comando dal back-end di hello soluzione, il dispositivo hello deve avviare regolarmente toocheck una connessione per qualsiasi tooprocess comandi in sospeso.

* I dispositivi devono connettersi solo tooor stabilire servizi noti toowell le route che sono il peering con, ad esempio IoT Hub.

* percorso di comunicazione Hello tra dispositivi e servizi o tra dispositivi e gateway viene protetto a livello di protocollo dell'applicazione hello.

* L'autenticazione e l'autorizzazione a livello di sistema sono basate sulle identità per ogni dispositivo. Rendono le credenziali di accesso e le autorizzazioni revocabili quasi immediatamente.

* La comunicazione bidirezionale per i dispositivi che si connettono toopower sporadicamente scadenza o problemi di connettività è facilitata tenendo comandi e notifiche del dispositivo fino a quando un dispositivo si connette tooreceive li. IoT Hub conserva code specifico del dispositivo per i comandi di hello che viene inviato.

* Dati di payload dell'applicazione viene protetto separatamente per protetto transito tramite gateway tooa specifica del servizio.

Hello settore mobile è utilizzato il modello di comunicazione assistita da servizio di hello in servizi di notifica push di scala enormi tooimplement come [servizi di notifica Push Windows][lnk-wns], [Google Cloud Messaging][lnk-google-messaging], e [Apple Push Notification Service][lnk-apple-push].

L'hub IoT è supportato tramite il percorso di peering pubblico di ExpressRoute.

## <a name="next-steps"></a>Passaggi successivi

vedere toolearn come toosend messaggi da un dispositivo e riceverli da IoT Hub, nonché come instrada il messaggio tooconfigure, [inviare e ricevere messaggi con l'IoT Hub][lnk-send-messages].

toolearn come IoT Hub consente di attivare la gestione dei dispositivi basata su standard per gestire, configurare e aggiornare i dispositivi, si tooremotely vedere [Panoramica di gestione dei dispositivi con l'IoT Hub][lnk-device-management].

le applicazioni client tooimplement su una vasta gamma di piattaforme per dispositivi hardware e sistemi operativi, è possibile usare il dispositivo di Azure IoT hello SDK. il dispositivo di Hello SDK include librerie che semplificano l'invio dati di telemetria tooan IoT hub e la ricezione cloud a dispositivo di messaggi. Quando si usa il dispositivo di hello SDK, è possibile scegliere tra vari toocommunicate di protocolli di rete con l'IoT Hub. toolearn informazioni, vedere hello [informazioni sul dispositivo SDK][lnk-device-sdks].

tooget avviato scrivere del codice ed esecuzione di alcuni esempi, vedere hello [iniziare con l'IoT Hub] [ lnk-get-started] esercitazione.

[img-architecture]: media/iot-hub-what-is-iot-hub/hubarchitecture.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[protocol-gateway]: https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md
[lnk-service-assisted-pattern]: http://blogs.msdn.com/b/clemensv/archive/2014/02/10/service-assisted-communication-for-connected-devices.aspx "Comunicazione assistita con i servizi, post di blog di Clemens Vasters"
[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-iotedge]: iot-hub-protocol-gateway.md
[lnk-field-gateway]: iot-hub-devguide-endpoints.md#field-gateways
[lnk-devguide-identityregistry]: iot-hub-devguide-identity-registry.md
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-wns]: https://msdn.microsoft.com/library/windows/apps/mt187203.aspx
[lnk-google-messaging]: https://developers.google.com/cloud-messaging/
[lnk-apple-push]: https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW9
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-refarch]: http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-send-messages]: iot-hub-devguide-messaging.md
[lnk-device-management]: iot-hub-device-management-overview.md

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[lnk-security-ground-up]: iot-hub-security-ground-up.md
