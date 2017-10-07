---
title: endpoint personalizzati di Azure IoT Hub aaaUnderstand | Documenti Microsoft
description: Guida per sviluppatori - mediante routing regole endpoint toocustom di tooroute messaggi da dispositivo a cloud.
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
ms.openlocfilehash: daa9cfb35d0853e316bbf469b034d4dadbd4e85d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-message-routes-and-custom-endpoints-for-device-to-cloud-messages"></a>Usare endpoint personalizzati e il routing dei messaggi per i messaggi da dispositivo a cloud

IoT Hub consente tooroute [messaggi da dispositivo a cloud] [ lnk-device-to-cloud] tooIoT Hub endpoint orientati ai servizi in base alle proprietà del messaggio. Routing offrono regole si hello toosend flessibilità messaggi dove servono toogo senza hello necessitano per i messaggi di servizi aggiuntivi tooprocess o toowrite ulteriore codice. Configurare ogni regola di routing ha hello le proprietà seguenti:

| Proprietà      | Descrizione |
| ------------- | ----------- |
| **Nome**      | nome univoco Hello che identifica la regola hello. |
| **Origine**    | il flusso di origine Hello dei dati di hello toobe intervenire. Ad esempio, i dati di telemetria del dispositivo. |
| **Condition** | espressione di query Hello per regola di routing hello che viene eseguito su intestazioni e corpo del messaggio hello e utilizzato toodetermine se si tratta di una corrispondenza per l'endpoint di hello. Per ulteriori informazioni sulla creazione di una condizione di route, vedere hello [riferimento - linguaggio di query per gemelli di dispositivo e i processi][lnk-devguide-query-language]. |
| **Endpoint**  | nome Hello dell'endpoint di hello in cui l'IoT Hub invia i messaggi che corrispondono alla condizione hello. Gli endpoint devono trovarsi in hello hub IoT hello stessa area, in caso contrario potrebbe essere addebitato per scrive tra aree. |

Un singolo messaggio può corrispondere a condizione di hello in più regole di routine, in cui caso IoT Hub offre endpoint toohello di messaggio hello associata a ogni regola corrispondente. IoT Hub deduplicates automaticamente anche il recapito dei messaggi, pertanto se un messaggio corrisponde a più regole che hanno tutti hello stessa destinazione, ma viene scritto toothat destinazione una volta.

Un hub IoT dispone di un [endpoint predefinito][lnk-built-in]. È possibile creare endpoint personalizzati tooroute messaggi tooby collegamento altri servizi nell'hub toohello sottoscrizione. L'hub IoT supporta attualmente l'Hub eventi, le code e gli argomenti del bus di servizio come endpoint personalizzati.

> [!WARNING]
> Le code del bus di servizio e gli argomenti che hanno abilitato con **Sessioni** o **Rilevamento duplicati** non sono supportati come endpoint personalizzati.

Per altre informazioni sulla creazione di endpoint personalizzati nell'hub IoT, vedere [Endpoint dell'hub IoT][lnk-devguide-endpoints].

Per altre informazioni sulla lettura da endpoint personalizzati, vedere:

* Lettura da [hub eventi][lnk-getstarted-eh].
* Lettura dalle [code del bus di servizio][lnk-getstarted-queue].
* Lettura dagli [argomenti del bus di servizio][lnk-getstarted-topic].

### <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sugli endpoint dell'hub IoT, vedere [Endpoint dell'hub IoT][lnk-devguide-endpoints].

Per ulteriori informazioni sul linguaggio di query hello utilizzare regole di routing toodefine, vedere [linguaggio di query IoT Hub per gemelli di dispositivo, processi e il routing dei messaggi][lnk-devguide-query-language].

Hello [messaggi da dispositivo a cloud IoT Hub processo mediante route] [ lnk-d2c-tutorial] esercitazione viene illustrato come regole di routing toouse e gli endpoint personalizzati.

[lnk-built-in]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-to-cloud]: iot-hub-devguide-messages-d2c.md
[lnk-devguide-query-language]: iot-hub-devguide-query-language.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-getstarted-eh]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-getstarted-queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[lnk-getstarted-topic]: ../service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions.md
