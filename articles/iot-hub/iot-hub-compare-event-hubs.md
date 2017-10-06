---
title: aaaCompare IoT Hub Azure tooAzure hub eventi | Documenti Microsoft
description: Confronto di hello IoT Hub e servizi di Azure di hub eventi evidenziazione differenze funzionali e casi d'uso. confronto Hello include i protocolli supportati, gestione dei dispositivi, il monitoraggio, e il caricamento dei file.
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: aeddea62-8302-48e2-9aad-c5a0e5f5abe9
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.openlocfilehash: e5f546b54e29860498d540abfc86a41c4662c0df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="comparison-of-azure-iot-hub-and-azure-event-hubs"></a>Confronto tra l'hub IoT e Hub eventi di Azure
Uno dei casi di utilizzo principali hello per l'IoT Hub è toogather telemetria dai dispositivi. Per questo motivo, l'IoT Hub spesso viene confrontato troppo[hub eventi di Azure][Azure Event Hubs]. Ad esempio, l'IoT Hub hub eventi è un servizio che consente l'ingresso di eventi e dati di telemetria di elaborazione di eventi cloud toohello su larga scala, con bassa latenza e affidabilità elevata.

Tuttavia, i servizi di hello presentano molte differenze sono descritte in dettaglio in hello nella tabella seguente:

| Area | Hub IoT | Hub eventi |
| --- | --- | --- |
| Modelli di comunicazione | Abilita le [comunicazioni da dispositivo a cloud][lnk-d2c-guidance] (messaggistica, caricamenti di file e proprietà segnalate) e le [comunicazioni da cloud a dispositivo][lnk-c2d-guidance] (metodi diretti, proprietà desiderate, messaggistica). |Consente solo l'ingresso di eventi, considerato di solito per scenari da dispositivo a cloud. |
| Informazioni sullo stato dei dispositivi | I [dispositivi gemelli][lnk-twins] possono archiviare le informazioni sullo stato dei dispositivi ed eseguire query su tali informazioni. | Nessuna informazioni sullo stato dei dispositivi può essere archiviata. |
| Supporto dei protocolli del dispositivo |Supporta MQTT, MQTT su WebSockets, AMQP, AMQP su WebSockets e HTTP. Inoltre, l'IoT Hub funziona con hello [gateway del protocollo Azure IoT][lnk-azure-protocol-gateway], un protocolli personalizzati personalizzabile protocollo gateway implementazione toosupport. |Supporta AMQP, AMQP su WebSocket e HTTP. |
| Sicurezza |Garantisce l’identità per dispositivo e il controllo di accesso revocabile. Vedere hello [sezione sicurezza di Guida per sviluppatori di IoT Hub hello]. |Garantisce [criteri di accesso condivisi][Event Hubs - security] a livello di Hub eventi, con supporto limitato per la revoca tramite [criteri dell'entità di pubblicazione][Event Hubs publisher policies]. Soluzioni IoT sono spesso necessarie tooimplement un toosupport di soluzione personalizzata per ogni dispositivo credenziali e le misure di anti-spoofing. |
| Monitoraggio delle operazioni |Abilita IoT soluzioni toosubscribe tooa vasta gamma di dispositivo identità connettività e gestione degli eventi, ad esempio errori di autenticazione di singoli dispositivi, la limitazione delle richieste e le eccezioni di formato non valido. Tali eventi consentono tooquickly identificare i problemi di connettività a livello di singolo dispositivo hello. |Espone solo le metriche aggregate. |
| Scalabilità |È ottimizzato toosupport milioni di dispositivi connessi contemporaneamente. |Metri hello le connessioni in base [le quote di hub eventi di Azure][Azure Event Hubs quotas]. In hello invece, hub eventi consente partizione hello toospecify per ogni messaggio inviato. |
| SDK del dispositivo |Fornisce [dispositivo SDK] [ Azure IoT SDKs] per un'ampia gamma di piattaforme e le lingue, in aggiunta toodirect MQTT, AMQP e HTTP APIs. |È supportato in .NET, Java e C, in aggiunta tooAMQP e le interfacce di trasmissione HTTP. |
| Caricamento di file |Attiva i file tooupload di soluzioni di IoT dal cloud toohello dispositivi. Include un endpoint di notifica di file per l'integrazione del flusso di lavoro e una categoria di monitoraggio delle operazioni per il supporto del debug. | Non supportati. |
| Route messaggi toomultiple endpoint | Backup too10 endpoint personalizzati sono supportati. Le regole determinano come i messaggi vengono indirizzati toocustom endpoint. Per altre informazioni, vedere [Inviare e ricevere messaggi con l'hub IoT][lnk-devguide-messaging]. | Richiede codice aggiuntivo toobe scritto e ospitato per l'invio dei messaggi. |

In breve, anche se hello solo caso di utilizzo in ingresso di telemetria da dispositivo a cloud, l'IoT Hub fornisce un servizio che è progettato per la connettività dei dispositivi IoT. Continua proposte di valore hello tooexpand per questi scenari con funzionalità specifiche di IoT. Hub eventi è progettato per in ingresso di eventi su larga scala, sia nel contesto di hello degli scenari tra più Data Center e tra più Data Center.

Non è insolito che toouse sia IoT Hub e hub eventi in hello stessa soluzione. IoT Hub gestisce la comunicazione da dispositivo a cloud hello e hub eventi gestisce in ingresso evento fase successiva in motori di elaborazione in tempo reale.

### <a name="next-steps"></a>Passaggi successivi
toolearn ulteriori informazioni sulla pianificazione della distribuzione di IoT Hub, vedere [scalabilità, disponibilità elevata e ripristino di emergenza][lnk-scaling].

toofurther esplorare le funzionalità di hello di IoT Hub, vedere:

* [Guida per gli sviluppatori dell'hub IoT][lnk-devguide]
* [Simulazione di un dispositivo con IoT Edge][lnk-iotedge]

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[Azure Event Hubs]: ../event-hubs/event-hubs-what-is-event-hubs.md
[sezione sicurezza di Guida per sviluppatori di IoT Hub hello]: iot-hub-devguide-security.md
[Event Hubs - security]: ../event-hubs/event-hubs-authentication-and-security-model-overview.md
[Event Hubs publisher policies]: ../event-hubs/event-hubs-features.md#event-publishers
[Azure Event Hubs quotas]: ../event-hubs/event-hubs-quotas.md
[Azure IoT SDKs]: https://github.com/Azure/azure-iot-sdks
[lnk-azure-protocol-gateway]: iot-hub-protocol-gateway.md

[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
