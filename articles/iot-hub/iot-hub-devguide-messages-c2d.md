---
title: messaggistica aaaUnderstand IoT Hub Azure cloud a dispositivo | Documenti Microsoft
description: Guida per sviluppatori - come toouse cloud a dispositivo messaggistica con l'IoT Hub. Include informazioni sul ciclo di vita del messaggio hello e opzioni di configurazione.
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
ms.openlocfilehash: 5c747b50163873d823556a8baa769c4b8f7f8c44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-from-iot-hub"></a>Inviare messaggi da cloud a dispositivo dall'hub IoT

toosend notifiche unidirezionale toohello dispositivo app dal back-end soluzione, inviare messaggi di cloud di dispositivi per dal dispositivo tooyour hub IoT. Per una descrizione delle altre opzioni da cloud a dispositivo supportate dall'hub IoT, vedere [Indicazioni sulle comunicazioni da cloud a dispositivo][lnk-c2d-guidance].

È possibile inviare messaggi da cloud a dispositivo tramite un endpoint per il servizio (**/messages/servicebound**). Un dispositivo riceve quindi messaggi hello tramite un endpoint specifico del dispositivo (**/devices/ {deviceId} / messaggi/devicebound**).

Ogni messaggio cloud a dispositivo indirizzata a un singolo dispositivo, l'impostazione hello **a** proprietà troppo**/devices/ {deviceId} / messaggi/devicebound**.

Ogni coda di dispositivo può contenere un massimo di 50 messaggi da cloud a dispositivo. Tentativo di ulteriori messaggi toohello toosend stesso dispositivo genera un errore.

## <a name="hello-cloud-to-device-message-lifecycle"></a>ciclo di vita del cloud a dispositivo messaggio Hello

recapito dei messaggi at-least-once tooguarantee, IoT Hub persiste cloud a dispositivo messaggi nelle code per ogni dispositivo. I dispositivi in modo esplicito devono riconoscere *completamento* per tooremove IoT Hub dalla coda di hello. Questo approccio garantisce la resilienza rispetto a errori di connettività e del dispositivo.

Hello diagramma seguente mostra un grafico sullo stato del ciclo di vita hello per un messaggio da cloud a dispositivo nell'IoT Hub.

![Ciclo di vita dei messaggi da cloud a dispositivo][img-lifecycle]

Quando hello servizio IoT Hub invia un messaggio tooa dispositivo, per il servizio hello Imposta stato del messaggio hello troppo**accodati**. Quando un dispositivo richiede troppo*ricezione* un messaggio, l'IoT Hub *blocchi* messaggio hello (impostando lo stato di hello troppo**invisibile**), che consente di altri thread nella hello dispositivo toostart ricezione di altri messaggi. Quando un thread dispositivo hello di un messaggio al termine dell'elaborazione notifica all'IoT Hub da *completamento* messaggio hello. IoT Hub quindi imposta lo stato di hello troppo**completato**.

Un dispositivo può anche scegliere di:

* *Rifiutare* messaggio hello, causando l'IoT Hub tooset è toohello **superato** stato. I dispositivi che si connettono tramite il protocollo MQTT hello Impossibile rifiutare i messaggi da cloud a dispositivo.
* *Abbandonare* messaggio hello, causando l'IoT Hub messaggio hello tooput nuovamente nella coda di hello, con stato hello impostato troppo**accodati**.

Un thread potrebbe non riuscire tooprocess un messaggio senza notifiche all'IoT Hub. Messaggi automaticamente in questo caso, eseguire la transizione da hello **invisibile** stato nascosto toohello **accodati** stato dopo un *timeout di visibilità (o blocco)*. il valore predefinito Hello di questo timeout è un minuto.

Un messaggio può eseguire la transizione tra hello **accodati** e **invisibile** stati, hello al massimo, numero di volte specificato in hello **max consegne** proprietà IoT Hub. Dopo che il numero di transizioni, IoT Hub Imposta stato hello del messaggio hello troppo**superato**. Analogamente, l'IoT Hub consente di impostare hello stato di un messaggio troppo**superato** dopo la scadenza (vedere [ora toolive][lnk-ttl]).

Hello [come toosend cloud a dispositivo messaggi con l'IoT Hub] [ lnk-c2d-tutorial] Mostra come i messaggi da cloud a dispositivo toosend da hello cloud e ricevano in un dispositivo.

In genere, un dispositivo quando verrà completato un messaggio da cloud a dispositivo hello perdita del messaggio hello non influisce sulla logica dell'applicazione hello. Quando ad esempio, dispositivo hello è resa persistente in locale il contenuto del messaggio hello o è stata completata con un'operazione. messaggio Hello Impossibile contengono anche informazioni temporanee, il cui perdita non influirebbe funzionalità hello di un'applicazione hello. In alcuni casi, per l'attività a esecuzione prolungata, è possibile completare messaggio hello del cloud a dispositivo dopo la persistenza hello descrizione dell'attività nell'archivio locale. È quindi possibile notificare hello soluzione back-end con uno o più messaggi da dispositivo a cloud in varie fasi di avanzamento dell'attività hello.

## <a name="message-expiration-time-toolive"></a>Scadenza del messaggio (ora toolive)

Ogni messaggio da cloud a dispositivo ha una scadenza. Questa volta viene impostata dal servizio hello (in hello **ExpiryTimeUtc** proprietà), o dall'IoT Hub utilizzando hello predefinita *ora toolive* specificato come una proprietà dell'IoT Hub. Vedere [Opzioni di configurazione da cloud a dispositivo][lnk-c2d-configuration].

Un vantaggio di tootake modo comune di scadenza del messaggio e di evitare l'invio di messaggi toodisconnected dispositivi, è tooset toolive valori di ora breve. Questo approccio consente di ottenere hello stesso risultato a quella di stato di connessione del dispositivo hello, pur essendo più efficiente. Quando si richiede l'acknowledgement dei messaggi, l'IoT Hub notifica quali dispositivi sono in grado di tooreceive messaggi e i dispositivi che non sono in linea o non sono riuscita.

## <a name="message-feedback"></a>Commenti sui messaggi

Quando si invia un messaggio da cloud a dispositivo, il servizio hello può richiedere il recapito di hello del feedback per ogni messaggio riguardanti hello stato finale di tale messaggio.

| Proprietà Ack | Comportamento |
| ------------ | -------- |
| **positive** | IoT Hub genera un messaggio di commenti e suggerimenti, se e solo se il messaggio da cloud a dispositivo hello raggiunto hello **completato** stato. |
| **negative** | IoT Hub genera un messaggio di commenti e suggerimenti, se e solo se, messaggio hello del cloud a dispositivo raggiunge hello **superato** stato. |
| **full**     | L'hub IoT genera un messaggio di commenti in entrambi i casi. |

Se **Ack** è **completo**e non ricevi un messaggio di commenti e suggerimenti, significa che tale messaggio hello del feedback è scaduto. servizio Hello non è possibile sapere quale messaggio originale toohello verificato anomalo. In pratica, un servizio deve garantire che sia possibile elaborare i commenti e suggerimenti hello prima della scadenza. l'ora di scadenza massimo Hello è due giorni, che consente una notevole quantità di tempo tooget hello servizio eseguire di nuovo se si verifica un errore.

Come illustrato nella sezione [Endpoint][lnk-endpoints], l'hub IoT recapita commenti sotto forma di messaggi tramite un endpoint per servizio (**/messages/servicebound/feedback**). Hello semantica per la ricezione di commenti e suggerimenti hello uguale a quello di messaggi da cloud a dispositivo e avere hello stesso [ciclo di vita del messaggio][lnk-lifecycle]. Quando possibile, messaggi di feedback viene eseguita in batch in un singolo messaggio, con hello seguente formato:

| Proprietà     | Descrizione |
| ------------ | ----------- |
| EnqueuedTime | Timestamp che indica quando è stato creato il messaggio hello. |
| UserId       | `{iot hub name}` |
| ContentType  | `application/vnd.microsoft.iothub.feedback.json` |

corpo Hello è una matrice JSON serializzato di record, ciascuno con hello le proprietà seguenti:

| Proprietà           | Descrizione |
| ------------------ | ----------- |
| EnqueuedTimeUtc    | Timestamp che indica quando si è verificato il risultato di hello del messaggio hello. Ad esempio, hello periferica completato o messaggio hello è scaduto. |
| OriginalMessageId  | **MessageId** toowhich cloud a dispositivo messaggio hello queste informazioni di commenti e suggerimenti si riferiscano. |
| StatusCode         | Stringa obbligatoria. Usato nei messaggi con commenti generati dall'hub IoT. <br/> 'Operazione riuscita' <br/> 'Scaduto' <br/> 'Numero di distribuzioni superato' <br/> 'Rifiutato' <br/> 'Eliminato definitivamente' |
| Descrizione        | Valori stringa per **StatusCode**. |
| deviceId           | **DeviceId** del dispositivo di destinazione hello di toowhich cloud a dispositivo messaggio hello si riferisce questo frammento di commenti e suggerimenti. |
| DeviceGenerationId | **DeviceGenerationId** del dispositivo di destinazione hello di toowhich cloud a dispositivo messaggio hello si riferisce questo frammento di commenti e suggerimenti. |

servizio Hello è necessario specificare un **MessageId** per hello cloud a dispositivo messaggio toocorrelate in grado di toobe il feedback con messaggio originale.

Hello esempio seguente viene illustrato hello corpo di un messaggio di commenti e suggerimenti.

```json
[
  {
    "OriginalMessageId": "0987654321",
    "EnqueuedTimeUtc": "2015-07-28T16:24:48.789Z",
    "StatusCode": 0,
    "Description": "Success",
    "DeviceId": "123",
    "DeviceGenerationId": "abcdefghijklmnopqrstuvwxyz"
  },
  {
    ...
  },
  ...
]
```

## <a name="cloud-to-device-configuration-options"></a>Opzioni di configurazione da cloud a dispositivo

Ogni hub IoT espone hello le opzioni di configurazione per la messaggistica cloud a dispositivo seguenti:

| Proprietà                  | Descrizione | Intervallo e valore predefinito |
| ------------------------- | ----------- | ----------------- |
| defaultTtlAsIso8601       | Durata (TTL) predefinita per messaggi da cloud a dispositivo. | Intervallo ISO_8601 backup too2D (minimo 1 minuto). Predefinito: 1 ora. |
| maxDeliveryCount          | Numero massimo di recapiti per code da cloud a dispositivo per i singoli dispositivi. | 1 too100. Predefinito: 10. |
| feedback.ttlAsIso8601     | Conservazione per messaggi con commenti diretti al servizio. | Intervallo ISO_8601 backup too2D (minimo 1 minuto). Predefinito: 1 ora. |
| feedback.maxDeliveryCount |Numero massimo di recapiti per la coda di commenti. | 1 too100. Predefinito: 100. |

Per ulteriori informazioni su come tooset queste opzioni di configurazione, vedere [hub IoT creare][lnk-portal].

## <a name="next-steps"></a>Passaggi successivi

Per informazioni sul SDK di hello è possibile utilizzare i messaggi da cloud a dispositivo tooreceive, vedere [Azure IoT SDK][lnk-sdks].

tootry out la ricezione di messaggi da cloud a dispositivo, vedere hello [inviare cloud a dispositivo] [ lnk-c2d-tutorial] esercitazione.

[img-lifecycle]: ./media/iot-hub-devguide-messages-c2d/lifecycle.png

[lnk-portal]: iot-hub-create-through-portal.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-ttl]: #message-expiration-time-to-live
[lnk-c2d-configuration]: #cloud-to-device-configuration-options
[lnk-lifecycle]: #message-lifecycle
[lnk-c2d-tutorial]: iot-hub-csharp-csharp-c2d.md
