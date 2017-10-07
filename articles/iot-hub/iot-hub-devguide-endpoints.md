---
title: gli endpoint IoT Hub Azure aaaUnderstand | Documenti Microsoft
description: 'Guida per gli sviluppatori: informazioni di riferimento sugli endpoint dell''hub IoT per dispositivi e per servizi.'
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 57ba52ae-19c6-43e4-bc6c-d8a5c2476e95
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 8647f15d2f2a050ad5799ea82f4d2d46db0dbec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-endpoints"></a>Informazioni di riferimento - Endpoint dell'hub IoT

## <a name="iot-hub-names"></a>Nomi dell'hub IoT

È possibile trovare il nome di hello dell'hub IoT hello che ospita l'endpoint nel portale di hello su hello **Panoramica** blade. Per impostazione predefinita, il nome DNS hello di un hub IoT è simile: `{your iot hub name}.azure-devices.net`.

È possibile usare DNS di Azure toocreate un nome DNS personalizzato per l'hub IoT. Per ulteriori informazioni, vedere [le impostazioni di DNS di Azure usare tooprovide dominio personalizzato per un servizio di Azure](../dns/dns-custom-domain.md#azure-iot).

## <a name="list-of-built-in-iot-hub-endpoints"></a>Elenco di endpoint dell'hub IoT incorporati

IoT Hub Azure è un servizio multi-tenant che espone gli attori toovarious relative funzionalità. Hello diagramma seguente mostra hello vari endpoint che espone l'IoT Hub.

![Endpoint hub IoT][img-endpoints]

Hello seguente elenco descrive gli endpoint hello:

* **Provider di risorse**. espone Hello provider di risorse IoT Hub un [Azure Resource Manager] [ lnk-arm] interfaccia. Questa interfaccia consente toocreate proprietari di sottoscrizione di Azure ed eliminare hub IoT e le proprietà di hub IoT tooupdate. Proprietà IoT Hub regolano [criteri di sicurezza a livello di hub][lnk-accesscontrol], anziché il controllo di accesso a livello di toodevice e funzionale opzioni per la messaggistica cloud a dispositivo e da dispositivo a cloud. Hello provider di risorse IoT Hub consente inoltre troppo[esportare le identità del dispositivo][lnk-importexport].
* **Gestione delle identità dei dispositivi**. Ogni hub IoT espone un set di identità di dispositivi toomanage endpoint HTTP REST (creare, recuperare, aggiornare ed eliminare). Le [identità dei dispositivi][lnk-device-identities] vengono usate per l'autenticazione dei dispositivi e il controllo di accesso.
* **Gestione dei dispositivi gemelli**. Ogni hub IoT espone un set di servizi orientati tooquery endpoint HTTP REST e aggiornamento [gemelli dispositivo] [ lnk-twins] (aggiornamento proprietà e i tag).
* **Gestione dei processi**. Ogni hub IoT espone un set di tooquery di endpoint HTTP REST orientati ai servizi e gestire [processi][lnk-jobs].
* **Endpoint del dispositivo**. Per ogni dispositivo nel Registro di sistema di hello identità, l'IoT Hub espone un set di endpoint:

  * *Invio di messaggi da dispositivo a cloud*. Un dispositivo utilizza questo endpoint troppo[inviare messaggi da dispositivo a cloud][lnk-d2c].
  * *Ricezione di messaggi da cloud a dispositivo*. Un dispositivo Usa questo tooreceive endpoint di destinazione [messaggi da cloud a dispositivo][lnk-c2d].
  * *Avvio di caricamenti di file*. Un dispositivo Usa questo tooreceive endpoint un URI di firma di accesso condiviso di archiviazione di Azure dall'IoT Hub troppo[caricare un file][lnk-upload].
  * *Recuperare e aggiornare le proprietà dei dispositivi gemelli*. Un dispositivo Usa questo tooaccess endpoint relativo [doppi dispositivo][lnk-twins]della proprietà.
  * *Ricezione di richieste di metodi diretti*. Un dispositivo Usa questo toolisten endpoint per [metodo diretto][lnk-methods]di richieste.

    Questi endpoint vengono esposti con i protocolli [MQTT v3.1.1][lnk-mqtt], HTTP 1.1 e [AMQP 1.0][lnk-amqp]. AMQP è disponibile anche su [WebSocket][lnk-websockets] sulla porta 443.

    Hello dispositivo gemelli e i metodi sono disponibili endpoint solo quando si utilizza hello [MQTT v3.1.1] [ lnk-mqtt] protocollo.

* **Endpoint di servizio**. Ogni hub IoT espone un set di endpoint per il toocommunicate back-end di soluzioni con i dispositivi. Con un'unica eccezione, gli endpoint esposti solo utilizzando hello [AMQP] [ lnk-amqp] protocollo. endpoint di chiamata di metodo Hello viene esposto su hello protocollo HTTP.
  
  * *Ricezione di messaggi da dispositivo a cloud*. Questo endpoint è compatibile con [Hub eventi di Azure][lnk-event-hubs] Un servizio back-end può utilizzarlo hello tooread [messaggi da dispositivo a cloud] [ lnk-d2c] inviati dai dispositivi. È possibile creare endpoint personalizzati l'hub IoT in endpoint predefinito toothis di addizione.
  * *Invio di messaggi da cloud a dispositivo e ricezione di acknowledgement di recapito*. Questi endpoint consentono il toosend di back-end soluzione affidabile [messaggi da cloud a dispositivo][lnk-c2d], e tooreceive hello riconoscimenti corrispondenti di recapito o la scadenza.
  * *Ricezione di notifiche relative ai file*. Questo endpoint di messaggistica consente tooreceive di notifica quando i dispositivi correttamente carica un file. 
  * *Chiamata diretta al metodo*. Questo endpoint consente a un servizio back-end di tooinvoke un [metodo diretto] [ lnk-methods] in un dispositivo.
  * *Ricezione di eventi di monitoraggio delle operazioni*. Questo endpoint consente le operazioni di tooreceive il monitoraggio degli eventi, se il IoT hub è stato configurato tooemit li. Per altre informazioni, vedere [Monitoraggio delle operazioni dell'hub IoT][lnk-operations-mon].

Hello [Azure IoT SDK] [ lnk-sdks] descritti hello vari modi tooaccess questi endpoint.

Tutti gli endpoint IoT Hub utilizzano hello [TLS] [ lnk-tls] protocollo e nessun endpoint è esposto mai sui canali decrittografati/non protette.

## <a name="custom-endpoints"></a>Endpoint personalizzati

È possibile collegare il tooact di hub IoT tooyour sottoscrizione esistente dei servizi Azure come endpoint per il routing dei messaggi. Questi endpoint agiscono come endpoint di servizio e vengono usati come sink per il ruoting dei messaggi. Dispositivi non possono scrivere direttamente toohello altri endpoint. toolearn ulteriori informazioni su route dei messaggi, vedere l'intervento di Guida per sviluppatori di hello sul [inviando e ricevendo messaggi con l'hub IoT][lnk-devguide-messaging].

IoT Hub supporta attualmente hello servizi di Azure come endpoint aggiuntivi seguenti:

* Hub eventi
* Code del bus di servizio
* Argomenti del bus di servizio

IoT Hub sono necessari gli endpoint di servizio di accesso in scrittura toothese per toowork di routing di messaggi. Se si configurano gli endpoint tramite hello portale di Azure, vengono aggiunte delle autorizzazioni necessarie hello. Assicurarsi di configurare la velocità effettiva di servizi toosupport hello previsto. Quando si configura prima soluzione IoT, è possibile necessario toomonitor gli altri endpoint e apportare le modifiche necessarie per il carico effettivo hello.

Se un messaggio corrisponde a più route che tutti scegliere toohello stesso endpoint, l'IoT Hub offre endpoint toothat messaggio una sola volta. Pertanto, si necessità la deduplicazione tooconfigure sul argomento o coda di Service Bus. Nelle code partizionate, l'affinità della partizione garantisce l'ordinamento dei messaggi.

> [!NOTE]
> Nelle code e negli argomenti del bus di servizio usati come endpoint dell'hub IoT non devono essere abilitati le **sessioni** e il **rilevamento duplicati**. Se una di queste opzioni sono abilitata, l'endpoint di hello viene visualizzato come **non raggiungibile** in hello portale di Azure.

Per i limiti di hello numero hello di è possibile aggiungere endpoint, vedere [quote e limitazioni][lnk-devguide-quotas].

## <a name="field-gateways"></a>Gateway sul campo

In una soluzione IoT un *gateway sul campo* è posizionato tra i dispositivi e l'hub IoT È in genere si trova tooyour Chiudi dispositivi. I dispositivi comunicano direttamente con gateway campo hello utilizzando un protocollo supportato dai dispositivi hello. gateway campo Hello connette tooan endpoint IoT Hub tramite un protocollo supportato da IoT Hub. Un gateway sul campo potrebbe essere un dispositivo hardware dedicato o un computer a bassa potenza che esegue il software del gateway personalizzato.

È possibile utilizzare [Azure IoT Edge] [ lnk-iot-edge] tooimplement un gateway di campo. Bordo IoT offre funzionalità, ad esempio le comunicazioni da più dispositivi in hello il demultiplexing stessa connessione IoT Hub.

## <a name="next-steps"></a>Passaggi successivi

Di seguito sono indicati altri argomenti di riferimento reperibili nella Guida per gli sviluppatori dell'hub IoT:

* [Linguaggio di query dell'hub IoT per dispositivi gemelli, processi e routing di messaggi][lnk-devguide-query]
* [Quote e limitazioni][lnk-devguide-quotas]
* [Supporto di MQTT nell'hub IoT][lnk-devguide-mqtt]

[lnk-iot-edge]: https://github.com/Azure/iot-edge

[img-endpoints]: ./media/iot-hub-devguide-endpoints/endpoints.png
[lnk-amqp]: https://www.amqp.org/
[lnk-mqtt]: http://mqtt.org/
[lnk-websockets]: https://tools.ietf.org/html/rfc6455
[lnk-arm]: ../azure-resource-manager/resource-group-overview.md
[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/

[lnk-tls]: https://tools.ietf.org/html/rfc5246


[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-accesscontrol]: iot-hub-devguide-security.md#access-control-and-permissions
[lnk-importexport]: iot-hub-devguide-identity-registry.md#import-and-export-device-identities
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-device-identities]: iot-hub-devguide-identity-registry.md
[lnk-upload]: iot-hub-devguide-file-upload.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md

[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[lnk-operations-mon]: iot-hub-operations-monitoring.md
