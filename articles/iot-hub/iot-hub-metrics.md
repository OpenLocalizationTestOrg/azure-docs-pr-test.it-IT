---
title: aaaUse metriche toomonitor IoT Hub di Azure | Documenti Microsoft
description: "Come monitorare e toouse IoT Hub Azure metriche tooassess hello integrità generale degli hub IoT."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: a47108fd-f994-4105-b21d-5b8f697b699c
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7d045013fb0229f488e72c93a6f668048b9d5c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-iot-hub-metrics"></a>Comprendere le metriche dell'hub IoT
Metriche IoT Hub consentono di migliori dati sullo stato di hello delle risorse di Azure IoT hello nella sottoscrizione di Azure. Abilitazione di metriche IoT Hub è tooassess hello integrità generale dei dispositivi di hello e hello servizio IoT Hub connesso tooit. Statistiche rivolta all'utente sono importanti perché consentono di vedere cosa accade in con i problemi relativi ai causa radice di IoT hub e della Guida senza la necessità di toocontact supporto tecnico di Azure.

Le metriche sono abilitate per impostazione predefinita. È possibile visualizzare le metriche IoT Hub hello portale di Azure.

## <a name="how-tooview-iot-hub-metrics"></a>Come tooview metriche IoT Hub
1. Creare un hub IoT. È possibile trovare istruzioni su come toocreate un hub IoT in hello [iniziare] [ lnk-get-started] Guida.
2. Aprire il pannello hello dell'hub IoT. In questa pagina fare clic su **Metrica**.
   
    ![][1]
3. Dal pannello metriche hello, è possibile visualizzare le metriche di hello per l'hub IoT e creare visualizzazioni personalizzate metriche. È possibile scegliere toosend l'endpoint di hub eventi metriche tooan dati o un account di archiviazione di Azure facendo **le impostazioni di diagnostica**.
   
    ![][2]

## <a name="iot-hub-metrics-and-how-toouse-them"></a>Le metriche di IoT Hub e come toouse li
IoT Hub fornisce alcune metriche toogive è fornita una panoramica dell'integrità di hello dell'hub e hello numero totale di dispositivi connessi. È possibile combinare informazioni provenienti da più metriche toopaint un quadro dello stato di hello dell'hub IoT hello. Hello nella tabella seguente descrive ogni hub IoT tiene traccia delle metriche di hello e come ogni metrica relativa toohello complessiva dello stato di hello hub IoT.

|Metrica|Nome visualizzato per la metrica|Unità|Tipo di aggregazione|Descrizione|
|---|---|---|---|---|
|d2c.telemetry.ingress.allProtocol|Tentativi di invio di messaggi di telemetria|Numero|Totale|Numero di tentativi toobe di telemetria da dispositivo a cloud messaggi inviati tooyour IoT hub|
|d2c.telemetry.ingress.success|Messaggi di telemetria inviati|Numero|Totale|Numero di messaggi da dispositivo a cloud telemetria inviato tooyour IoT hub|
|c2d.commands.egress.complete.success|Comandi completati|Numero|Totale|Numero di comandi cloud a dispositivo completata dal dispositivo hello|
|c2d.commands.egress.abandon.success|Comandi abbandonati|Numero|Totale|Numero di comandi cloud a dispositivo abbandonato da dispositivo hello|
|c2d.commands.egress.reject.success|Comandi rifiutati|Numero|Totale|Numero di comandi cloud a dispositivo rifiutato dal dispositivo hello|
|devices.totalDevices|Totale dispositivi|Numero|Totale|Numero di dispositivi registrati tooyour IoT hub|
|devices.connectedDevices.allProtocol|Dispositivi connessi|Numero|Totale|Numero di dispositivi connessi tooyour IoT hub|
|d2c.telemetry.egress.success|Messaggi telemetria recapitati|Numero|Totale|Numero di volte in cui i messaggi sono stati scritti correttamente tooendpoints (totale)|
|d2c.telemetry.egress.dropped|Messaggi rimossi|Numero|Totale|Numero di messaggi ignorati perché non corrisponde alcuna route e route fallback hello è stata disabilitata|
|d2c.telemetry.egress.orphaned|Messaggi orfani|Numero|Totale|numero di Hello dei messaggi non corrisponde alcuna route inclusi route fallback hello|
|d2c.telemetry.egress.invalid|Messaggi non validi|Numero|Totale|Hello conteggio dei messaggi non recapitati a causa di tooincompatibility con endpoint hello|
|d2c.telemetry.egress.fallback|Messaggi corrispondenti alla condizione di fallback|Numero|Totale|Numero di messaggi scritti toohello fallback endpoint|
|d2c.endpoints.egress.eventHubs|I messaggi recapitati tooEvent gli endpoint Hub|Numero|Totale|Numero di volte in cui i messaggi sono stati tooEvent scritto correttamente gli endpoint di Hub|
|d2c.endpoints.latency.eventHubs|Latenza messaggi per gli endpoint di Hub eventi|Millisecondi|Media|Latenza media tra l'hub IoT toohello di messaggio in ingresso e in ingresso messaggio Hello in un endpoint di Hub eventi, in millisecondi|
|d2c.endpoints.egress.serviceBusQueues|I messaggi recapitati tooService endpoint coda del Bus|Numero|Totale|Numero di volte in cui i messaggi sono stati tooService scritto correttamente gli endpoint di coda del Bus|
|d2c.endpoints.latency.serviceBusQueues|Latenza messaggi per gli endpoint della coda del bus di servizio|Millisecondi|Media|Latenza media tra l'hub IoT toohello di messaggio in ingresso e in ingresso messaggio Hello in un endpoint di coda di Service Bus, in millisecondi|
|d2c.endpoints.egress.serviceBusTopics|I messaggi recapitati tooService gli endpoint di argomento del Bus|Numero|Totale|Numero di volte in cui i messaggi sono stati tooService scritto correttamente gli endpoint di argomento del Bus|
|d2c.endpoints.latency.serviceBusTopics|Latenza messaggi per gli endpoint dell'argomento del bus di servizio|Millisecondi|Media|Latenza media tra l'hub IoT toohello di messaggio in ingresso e in ingresso messaggio Hello in un endpoint di argomento del Bus di servizio, in millisecondi|
|d2c.endpoints.egress.builtIn.events|I messaggi recapitati toohello endpoint predefinito (messaggi e gli eventi)|Numero|Totale|Numero di volte in cui i messaggi sono stati scritti correttamente toohello endpoint predefinito (messaggi e gli eventi)|
|d2c.endpoints.latency.builtIn.events|Latenza dei messaggi per l'endpoint predefinito hello (messaggi e gli eventi)|Millisecondi|Media|Latenza media tra l'hub IoT toohello di messaggio in ingresso e in ingresso messaggio Hello in endpoint predefinito hello (messaggi e gli eventi), in millisecondi |
|d2c.twin.read.success|Letture dei dispositivi gemelli completate dai dispositivi|Numero|Totale|conteggio di Hello di letture doppi avviato dal dispositivo tutte esito positivo.|
|d2c.twin.read.failure|Letture dei dispositivi gemelli non riuscite per i dispositivi|Numero|Totale|conteggio Hello di tutti i Impossibile letture doppi avviato dal dispositivo.|
|d2c.twin.read.size|Dimensioni delle risposte di letture dei dispositivi gemelli dai dispositivi|Byte|Media|Media di Hello, min e max di eseguite correttamente avviato dal dispositivo doppio letture.|
|d2c.twin.update.success|Aggiornamenti dei dispositivi gemelli completati dai dispositivi|Numero|Totale|conteggio di Hello degli aggiornamenti di un doppio avviato dal dispositivo tutte esito positivo.|
|d2c.twin.update.failure|Aggiornamenti dei dispositivi gemelli non riusciti per i dispositivi|Numero|Totale|numero di Hello di tutti di doppi avviato dal dispositivo aggiornamenti non riusciti.|
|d2c.twin.update.size|Dimensioni degli aggiornamenti dei dispositivi gemelli dai dispositivi|Byte|Media|Hello Media, min e dimensioni massime di eseguite correttamente avviato dal dispositivo doppio gli aggiornamenti.|
|c2d.methods.success|Chiamate a metodi diretti riuscite|Numero|Totale|conteggio di Hello di chiamate dirette del metodo eseguite correttamente.|
|c2d.methods.failure|Chiamate a metodi diretti non riuscite|Numero|Totale|conteggio Hello di tutti i Impossibile chiamate dirette del metodo.|
|c2d.methods.requestSize|Dimensioni delle richieste di chiamate a metodi diretti|Byte|Media|Hello Media, min e max di richieste dirette del metodo eseguite correttamente.|
|c2d.methods.responseSize|Dimensioni delle risposte a chiamate a metodi diretti|Byte|Media|Hello Media, min e max di tutte le risposte dirette del metodo ha esito positivo.|
|c2d.twin.read.success|Letture dei dispositivi gemelli completate dal back-end|Numero|Totale|conteggio di Hello di letture di back-end avviato doppi eseguite correttamente.|
|c2d.twin.read.failure|Letture dei dispositivi gemelli non riuscite per il back-end|Numero|Totale|conteggio Hello di tutti i Impossibile letture doppi avviato dal back-end.|
|c2d.twin.read.size|Dimensioni delle risposte di letture dei dispositivi gemelli dal back-end|Byte|Media|Media di Hello, min e max di eseguite correttamente back-end avviato doppio letture.|
|c2d.twin.update.success|Aggiornamenti dei dispositivi gemelli completati dal back-end|Numero|Totale|conteggio di Hello degli aggiornamenti di back-end avviato doppi eseguite correttamente.|
|c2d.twin.update.failure|Aggiornamenti dei dispositivi gemelli non riusciti per il back-end|Numero|Totale|numero Hello di tutti di back-end avviato doppi aggiornamenti non riusciti.|
|c2d.twin.update.size|Dimensioni degli aggiornamenti dei dispositivi gemelli dal back-end|Byte|Media|Hello Media, min e le dimensioni massime di tutte le back-end avviato doppio gli aggiornamenti.|
|twinQueries.success|Query dei dispositivi gemelli completate|Numero|Totale|conteggio di Hello di tutte le query doppi ha esito positivo.|
|twinQueries.failure|Query dei dispositivi gemelli non riuscite|Numero|Totale|conteggio di Hello di tutte le query doppi non riuscita.|
|twinQueries.resultSize|Dimensioni dei risultati delle query dei dispositivi gemelli|Byte|Media|Hello Media, min e max di dimensioni del risultato hello di tutte le query doppi ha esito positivo.|
|jobs.createTwinUpdateJob.success|Creazioni di processi di aggiornamento dei dispositivi gemelli completate|Numero|Totale|conteggio di Hello di tutti alla creazione di processi di aggiornamento di un doppio.|
|jobs.createTwinUpdateJob.failure|Creazioni di processi di aggiornamento dei dispositivi gemelli non riuscite|Numero|Totale|conteggio di Hello di tutti i creazione non riuscita dei processi di aggiornamento di un doppio.|
|jobs.createDirectMethodJob.success|Creazioni di processi di chiamata al metodo completate|Numero|Totale|conteggio di Hello di tutti alla creazione di processi di chiamate dirette del metodo.|
|jobs.createDirectMethodJob.failure|Creazioni di processi di chiamata al metodo non riuscite|Numero|Totale|conteggio di Hello di tutti i creazione non riuscita dei processi di chiamate dirette del metodo.|
|jobs.listJobs.success|Processi toolist chiamate con esito positivo|Numero|Totale|conteggio di Hello di tutti i processi di toolist chiamate con esito positivo.|
|jobs.listJobs.failure|Processi toolist chiamate non riuscite|Numero|Totale|conteggio di Hello di tutti i processi toolist di chiamate non riuscite.|
|jobs.cancelJob.success|Annullamenti di processi riusciti|Numero|Totale|conteggio Hello di tutte le chiamate toocancel un processo.|
|jobs.cancelJob.failure|Annullamenti di processi non riusciti|Numero|Totale|conteggio di Hello di tutte le chiamate non riuscite toocancel un processo.|
|jobs.queryJobs.success|Query sui processi riuscite|Numero|Totale|conteggio di Hello di tutti i processi di tooquery chiamate con esito positivo.|
|jobs.queryJobs.failure|Query sui processi non riuscite|Numero|Totale|conteggio di Hello di tutti i processi tooquery di chiamate non riuscite.|
|jobs.completed|Processi completati|Numero|Totale|conteggio di Hello di tutti i processi completati.|
|jobs.failed|Processi non riusciti|Numero|Totale|conteggio di Hello di tutti i processi non riusciti.|

## <a name="next-steps"></a>Passaggi successivi
Dopo aver esaminato una panoramica delle metriche di IoT Hub, seguire questa toolearn collegamento ulteriori informazioni sulla gestione di Azure IoT Hub:

* [Monitoraggio delle operazioni][lnk-monitor]

toofurther esplorare le funzionalità di hello di IoT Hub, vedere:

* [Guida per gli sviluppatori dell'hub IoT][lnk-devguide]
* [Simulazione di un dispositivo con Azure IoT Edge][lnk-iotedge]

<!-- Links and images -->
[1]: media/iot-hub-metrics/enable-metrics-1.png
[2]: media/iot-hub-metrics/enable-metrics-2.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[lnk-operations-monitoring]: iot-hub-operations-monitoring.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-dr]: iot-hub-ha-dr.md

[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
