---
title: protocolli e porte di comunicazione di IoT Hub aaaAzure | Documenti Microsoft
description: "Guida per sviluppatori - descrive i protocolli di comunicazione hello è supportato per le comunicazioni da dispositivo a cloud e cloud a dispositivo e i numeri di porta hello che devono essere aperti."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3fc5f1a3-3711-4611-9897-d4db079b4250
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 31cb948f1d30edd87edb13ad0dd859c02bcc3239
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# Informazioni di riferimento: scegliere un protocollo di comunicazione

IoT Hub consente dispositivi toouse [MQTT][lnk-mqtt], MQTT tramite WebSockets, [AMQP][lnk-amqp], AMQP su WebSocket e HTTP protocolli per sul dispositivo comunicazioni. Per informazioni sulle modalità di supporto dei protocolli alle funzionalità specifiche dell'hub IoT, vedere [Indicazioni sulle comunicazioni da dispositivo a cloud][lnk-d2c-guidance] e [Indicazioni sulle comunicazioni da cloud a dispositivo][lnk-c2d-guidance].

Hello nella tabella seguente vengono forniti consigli generali hello per la scelta del protocollo:

| Protocol | Quando scegliere questo protocollo |
| --- | --- |
| MQTT <br> MQTT su WebSocket |Utilizzare in tutti i dispositivi che non richiedono tooconnect più dispositivi (ognuno con le proprie credenziali per dispositivo) su hello stessa connessione TLS. |
| AMQP <br> AMQP su WebSocket |Utilizzare nel campo e cloud vantaggio tootake gateway di connessione multiplexing tra i dispositivi. |
| HTTP |Usare per i dispositivi che non supportano altri protocolli. |

Considerare i seguenti punti quando si sceglie il protocollo per le comunicazioni lato dispositivo hello:

* **Modello da cloud a dispositivo**. HTTP non dispone di push del server tooimplement un modo efficiente. Di conseguenza, quando si usa HTTP i dispositivi eseguono il polling dell'hub IoT per i messaggi da cloud a dispositivo. Questo approccio è inefficiente per dispositivo hello e IoT Hub. In base alle attuali linee guida di HTTP, ogni dispositivo dovrebbe eseguire il polling almeno ogni 25 minuti. In hello invece, MQTT e AMQP supportano push del server quando si ricevono messaggi da cloud a dispositivo. Consentono inserimenti immediati dei messaggi da dispositivo toohello IoT Hub. Se la latenza di recapito è un problema, MQTT o AMQP sono toouse protocolli migliore hello. Per i dispositivi che si connettono raramente, è possibile usare anche il protocollo HTTP.
* **Gateway sul campo**. Quando si utilizza MQTT e HTTP, è possibile connettersi a più dispositivi (ognuno con le proprie credenziali per dispositivo) utilizzando hello stessa connessione TLS. Pertanto, per [campo scenari di gateway][lnk-azure-gateway-guidance], questi protocolli sono non ottimali perché richiedono una connessione TLS tra il gateway di campo hello e IoT Hub per ogni gateway campo toohello connessi di dispositivo.
* **Dispositivi con risorse ridotte**. Hello MQTT e librerie HTTP hanno un impatto minore rispetto a librerie AMQP hello. Di conseguenza, se hello dispositivo dispone di risorse (ad esempio, minore di 1 MB di RAM) limitate, questi protocolli potrebbero essere hello solo protocollo implementazione disponibile.
* **Attraversamento rete**. il protocollo AMQP standard di Hello utilizza la porta 5671, mentre MQTT rimane in ascolto sulla porta 8883, che potrebbe causare problemi nelle reti incluse protocolli HTTP toonon chiuso. MQTT tramite WebSockets, AMQP su WebSocket e HTTP sono disponibili toobe utilizzati in questo scenario.
* **Dimensioni del payload**. MQTT e AMQP sono protocolli binari, quindi hanno payload più compatti rispetto a HTTP.

> [!WARNING]
> Quando si usa HTTP, ogni dispositivo deve eseguire il polling dei messaggi da cloud a dispositivo ogni 25 minuti o più. Tuttavia, durante lo sviluppo, è accettabile toopoll più frequentemente ogni 25 minuti.

## Numeri di porta

I dispositivi possono comunicare con l'hub IoT in Azure tramite una serie di protocolli. In genere, scelta hello del protocollo dipende dai requisiti specifici di hello della soluzione hello. Hello nella tabella seguente sono elencate le porte in uscita hello che devono essere aperte per un dispositivo toobe in grado di toouse un protocollo specifico:

| Protocol | Porta |
| --- | --- |
| MQTT |8883 |
| MQTT su WebSocket |443 |
| AMQP |5671 |
| AMQP su WebSockets |443 |
| HTTP |443 |

Dopo aver creato un hub IoT in un'area di Azure, hello mantiene hub IoT hello stesso indirizzo IP per la durata di hello di tale hub IoT. Tuttavia, toomaintain qualità del servizio, se si sposta Microsoft hello IoT hub tooa diverse unità, quindi viene assegnata un nuovo indirizzo IP.


## Passaggi successivi

toolearn ulteriori informazioni su come IoT Hub implementa il protocollo MQTT hello, vedere [per comunicare con l'hub IoT protocollo MQTT hello][lnk-mqtt-support].

[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-mqtt-support]: iot-hub-mqtt-support.md
[lnk-amqp]: http://docs.oasis-open.org/amqp/core/v1.0/os/amqp-core-complete-v1.0-os.pdf
[lnk-mqtt]: http://docs.oasis-open.org/mqtt/mqtt/v3.1.1/mqtt-v3.1.1.pdf
[lnk-azure-gateway-guidance]: iot-hub-devguide-endpoints.md#field-gateways
