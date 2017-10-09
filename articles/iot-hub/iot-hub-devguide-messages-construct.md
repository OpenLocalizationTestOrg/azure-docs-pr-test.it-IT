---
title: formato del messaggio IoT Hub Azure aaaUnderstand | Documenti Microsoft
description: Guida per sviluppatori - formato hello viene fornita la descrizione e il contenuto previsto di messaggi di IoT Hub.
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
ms.openlocfilehash: 3b1567e47bc32f70c0c252996648c4035ae81243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-read-iot-hub-messages"></a>Creare e leggere messaggi dell'hub IoT

toosupport perfetta interoperabilità tra protocolli, IoT Hub definisce un formato comune per tutti i protocolli che utilizzano il dispositivo. Il formato del messaggio viene usato per i messaggi [da dispositivo a cloud][lnk-d2c] e [da cloud a dispositivo][lnk-c2d]. Un [messaggio dell'hub IoT][lnk-messaging] è costituito da:

* Un set di *proprietà del sistema*. Proprietà impostate o interpretate dall'hub IoT. Il set è predeterminato.
* Un set di *proprietà dell'applicazione*. Un dizionario di proprietà stringa che è possibile definire un'applicazione hello e l'accesso, senza la necessità di corpo del messaggio hello toodeserialize. Queste proprietà non vengono mai modificate dall'hub IoT.
* Corpo binario opaco.

I valori e i nomi di proprietà possono contenere solo caratteri ASCII alfanumerici e ``{'!', '#', '$', '%, '&', "'", '*', '*', '+', '-', '.', '^', '_', '`', '|', '~'}`` quando:

* Inviare messaggi da dispositivo a cloud utilizzando il protocollo HTTP hello.
* Invio di messaggi da cloud a dispositivo.

Per ulteriori informazioni su come tooencode e decodificare i messaggi inviati tramite protocolli diversi, vedere [Azure IoT SDK][lnk-sdks].

Hello nella tabella seguente elenca il set di hello di proprietà di sistema nei messaggi di IoT Hub.

| Proprietà | Descrizione |
| --- | --- |
| MessageId |Un identificatore definibile dall'utente per il messaggio hello utilizzato per modelli di richiesta-risposta. : Una distinzione tra maiuscole e stringa di formato (Backup too128 caratteri) di caratteri alfanumerici ASCII a 7 bit + `{'-', ':',’.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`. |
| Numero di sequenza |Numero (univoco per ogni dispositivo coda) assegnato dal messaggio di IoT Hub tooeach cloud a dispositivo. |
| Anche|Destinazione specificata nei messaggi [da cloud a dispositivo][lnk-c2d]. |
| ExpiryTimeUtc |Data e ora della scadenza del messaggio. |
| EnqueuedTime |Data e ora hello [Cloud a dispositivo] [ lnk-c2d] messaggio è stato ricevuto dall'IoT Hub. |
| CorrelationId |Proprietà stringa in un messaggio di risposta che contiene in genere hello MessageId della richiesta di hello, nei modelli di richiesta-risposta. |
| UserId |Un ID usato origine hello toospecify dei messaggi. Quando i messaggi vengono generati da IoT Hub, impostare troppo`{iot hub name}`. |
| Ack |Generatore di messaggi con commenti. Questa proprietà viene utilizzata nei messaggi messaggi da cloud a dispositivo toorequest Hub IoT toogenerate commenti e suggerimenti in seguito a consumo hello del messaggio hello dal dispositivo hello. I valori possibili: **Nessuno** (impostazione predefinita): viene generato alcun messaggio di commenti e suggerimenti, **positivo**: ricevere un messaggio di commenti e suggerimenti, se è stato completato, il messaggio hello **negativo**: ricevono un messaggio di commenti e suggerimenti, se il messaggio hello è scaduto (o è stato raggiunto il numero massimo di recapiti) senza completate dal dispositivo hello, o **completo**: positive e negative. Per altre informazioni, vedere [Commenti sui messaggi][lnk-feedback]. |
| ConnectionDeviceId |ID impostato dall'hub IoT sui messaggi da dispositivo a cloud. Contiene hello **deviceId** del dispositivo hello che ha inviato il messaggio hello. |
| ConnectionDeviceGenerationId |ID impostato dall'hub IoT sui messaggi da dispositivo a cloud. Contiene hello **generationId** (in base [le proprietà di identità dispositivo][lnk-device-properties]) del dispositivo hello che ha inviato il messaggio hello. |
| ConnectionAuthMethod |Metodo di autenticazione impostato dall'hub IoT sui messaggi da dispositivo a cloud. Questa proprietà contiene informazioni sul dispositivo hello hello autenticazione metodo usato tooauthenticate invio messaggio hello. Per ulteriori informazioni, vedere [dispositivo toocloud anti-spoofing][lnk-antispoofing]. |

## <a name="message-size"></a>Dimensioni dei messaggi

IoT Hub misure dimensione del messaggio in modo indipendente dal protocollo, prendere in considerazione solo i payload effettivo hello. dimensione Hello in byte viene calcolata come somma hello seguenti hello:

* dimensioni del corpo Hello in byte.
* dimensione Hello in byte di tutti i valori hello hello sistema di proprietà del messaggio.
* dimensione Hello in byte di tutti i nomi di proprietà utente e i valori.

I valori e nomi di proprietà sono caratteri tooASCII limitata, pertanto hello lunghezza delle stringhe di hello è uguale a dimensioni hello in byte.

## <a name="next-steps"></a>Passaggi successivi

Per informazioni sulla dimensione massima dei messaggi nell'hub IoT, vedere [Quote e limitazioni dell'hub IoT][lnk-quotas].

toolearn toocreate messaggi e letti Hub IoT in diversi linguaggi di programmazione, vedere hello [iniziare] [ lnk-get-started] esercitazioni.

[lnk-messaging]: iot-hub-devguide-messaging.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-get-started]: iot-hub-get-started.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-feedback]: iot-hub-devguide-messages-c2d.md#message-feedback
[lnk-device-properties]: iot-hub-devguide-identity-registry.md#device-identity-properties
[lnk-antispoofing]: iot-hub-devguide-messages-d2c.md#anti-spoofing-properties
