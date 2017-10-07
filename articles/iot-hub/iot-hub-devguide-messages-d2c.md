---
title: messaggistica di dispositivo a cloud Azure IoT Hub aaaUnderstand | Documenti Microsoft
description: Guida per sviluppatori - come toouse dispositivo a cloud con l'IoT Hub di messaggistica. Include informazioni sull'invio di dati di telemetria e non telemtry e l'utilizzo di routing dei messaggi toodeliver.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 07dc8a6be747365c7efbc528ab2762b0d9790758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="send-device-to-cloud-messages-tooiot-hub"></a>Inviare i messaggi da dispositivo a cloud tooIoT Hub

toosend telemetria di serie temporali e gli avvisi generati da dispositivi tooyour soluzione back-end del, inviare i messaggi da dispositivo a cloud dall'hub IoT tooyour di dispositivo. Per una descrizione delle altre opzioni da dispositivo a cloud supportate dall'hub IoT, vedere [Indicazioni sulle comunicazioni da dispositivo a cloud][lnk-d2c-guidance].

I messaggi da dispositivo a cloud vengono inviati tramite un endpoint per il dispositivo (**/devices/{deviceId}/messages/events**). Regole di routing, quindi indirizzare tooone i messaggi di endpoint servizio Web hello l'hub IoT. Regole di routing utilizzano hello intestazioni e corpo dei messaggi da dispositivo a cloud hello che passano attraverso il toodetermine hub in cui tooroute li. Per impostazione predefinita, i messaggi vengono indirizzati toohello incorporato orientati ai servizi endpoint (**messaggi di eventi**), che è compatibile con [hub eventi][lnk-event-hubs]. Pertanto, è possibile utilizzare standard [integrazione degli hub di eventi e SDK] [ lnk-compatible-endpoint] messaggi da dispositivo a cloud tooreceive nella soluzione di back-end.

L'hub IoT implementa la messaggistica da dispositivo a cloud usando un modello di messaggistica di flusso. I messaggi da dispositivo a cloud dell'IoT Hub sono più simili [hub eventi] [ lnk-event-hubs] *eventi* di [Bus di servizio] [ lnk-servicebus] *messaggi* e non è presente un numero elevato di eventi passano attraverso il servizio di hello che possa essere letto da più lettori.

Messaggistica con l'IoT Hub dispositivo a cloud presenta hello seguenti caratteristiche:

* I messaggi da dispositivo a cloud sono durevoli e mantenuto nel predefinito di un hub IoT **messaggi di eventi** endpoint per i giorni tooseven.
* I messaggi da dispositivo a cloud possono contenere al massimo 256 KB e possono essere raggruppati in batch toooptimize Invia. I batch possono avere dimensioni massime pari a 256 KB.
* Come spiegato in hello [tooIoT accesso controllo Hub] [ lnk-devguide-security] sezione IoT Hub consente il controllo di autenticazione e accesso al dispositivo.
* IoT Hub consente toocreate too10 contenuto personalizzato degli endpoint. I messaggi vengono recapitati endpoint toohello in base a route configurate sull'hub IoT. Per altre informazioni, vedere [Regole di routing](#routing-rules).
* L'hub IoT abilita milioni di dispositivi connessi contemporaneamente (vedere [Quote e limitazioni][lnk-quotas]).
* L'hub IoT non consente il partizionamento arbitrario. I messaggi da dispositivo a cloud vengono partizionati in base al valore **deviceId**di origine.

Per ulteriori informazioni sulle differenze hello hello IoT Hub e servizi di hub eventi, vedere [hub eventi di Azure e di confronto di IoT Hub Azure][lnk-comparison].

## <a name="send-non-telemetry-traffic"></a>Invio di traffico non di telemetria

Spesso, i dispositivi inoltre dati tootelemetry punta, inviano i messaggi e le richieste che necessitano di esecuzione separato e operazioni di gestione nel back-end di hello soluzione. Ad esempio, gli avvisi critici che devono attivare un'azione specifica in hello back-end. È possibile scrivere facilmente un [regola di routing] [ lnk-devguide-custom] toosend questi tipi di endpoint tooan messaggi dedicato tootheir un'elaborazione basata su un'intestazione di messaggio hello o un valore nel corpo del messaggio hello.

Per ulteriori informazioni su hello migliore modo tooprocess questo tipo di messaggio, vedere hello [esercitazione: come i messaggi da dispositivo a cloud IoT Hub tooprocess] [ lnk-d2c-tutorial] esercitazione.

## <a name="route-device-to-cloud-messages"></a>Routing di messaggi da dispositivo a cloud

Sono disponibili due opzioni per le applicazioni back-end tooyour di routing messaggi da dispositivo a cloud:

* Utilizzare hello incorporato [endpoint compatibile con Hub eventi] [ lnk-compatible-endpoint] tooenable back-end App tooread hello dispositivo a cloud per i messaggi ricevuti dall'hub hello. toolearn su endpoint compatibili con Hub eventi predefiniti di hello, vedere [leggere messaggi da dispositivo a cloud da endpoint predefiniti hello][lnk-devguide-builtin].
* Utilizzare gli endpoint toocustom di routing regole toosend messaggi nell'hub IoT. Gli endpoint personalizzati consentono i messaggi di dispositivo a cloud tooread applicazioni back-end tramite gli hub di eventi, le code del Bus di servizio o gli argomenti del Bus di servizio. toolearn sugli endpoint personalizzati e routing, vedere [usare endpoint personalizzati e le regole di routing per i messaggi da dispositivo a cloud][lnk-devguide-custom].

## <a name="anti-spoofing-properties"></a>Proprietà anti-spoofing

dispositivo tooavoid lo spoofing degli indirizzi nei messaggi da dispositivo a cloud, l'IoT Hub timbri tutti i messaggi con hello le proprietà seguenti:

* **ConnectionDeviceId**
* **ConnectionDeviceGenerationId**
* **ConnectionAuthMethod**

Hello innanzitutto due contengono hello **deviceId** e **generationId** di hello originari dispositivo, in base [le proprietà di identità dispositivo][lnk-device-properties].

Hello **ConnectionAuthMethod** proprietà contiene un oggetto JSON serializzato, con hello le proprietà seguenti:

```json
{
  "scope": "{ hub | device}",
  "type": "{ symkey | sas}",
  "issuer": "iothub"
}
```

## <a name="next-steps"></a>Passaggi successivi

Per informazioni sul SDK di hello è possibile utilizzare i messaggi da dispositivo a cloud toosend, vedere [Azure IoT SDK][lnk-sdks].

Hello [iniziare] [ lnk-get-started] le esercitazioni illustrano come toosend dispositivo a cloud messaggi da dispositivi fisici sia simulati. Per ulteriori dettagli, vedere hello [messaggi da dispositivo a cloud IoT Hub processo mediante route] [ lnk-d2c-tutorial] esercitazione.

[lnk-devguide-builtin]: iot-hub-devguide-messages-read-builtin.md
[lnk-devguide-custom]: iot-hub-devguide-messages-read-custom.md
[lnk-comparison]: iot-hub-compare-event-hubs.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[lnk-get-started]: iot-hub-get-started.md

[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/
[lnk-servicebus]: http://azure.microsoft.com/documentation/services/service-bus/
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-compatible-endpoint]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-properties]: iot-hub-devguide-identity-registry.md#device-identity-properties
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
