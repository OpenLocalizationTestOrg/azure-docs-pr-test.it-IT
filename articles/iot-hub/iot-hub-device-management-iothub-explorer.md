---
title: gestione dei dispositivi IoT con l'hub IOT explorer aaaAzure | Documenti Microsoft
description: "Utilizzare hello hub IOT Esplora CLI lo strumento per la gestione dei dispositivi Azure IoT Hub, che presenta metodi diretti hello e opzioni di gestione del doppi hello proprietà desiderate."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: gestione dispositivi iot azure, gestione dispositivi hub iot azure, gestione dispositivi iot, gestione dispositivi hub iot
ms.assetid: b34f799a-fc14-41b9-bf45-54751163fffe
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: xshi
ms.openlocfilehash: e0a5e6120db5c4fb12f7f8b605a56e0e4aad9217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-for-azure-iot-hub-device-management"></a>Usare iothub-explorer per la gestione di dispositivi hub IoT di Azure

![Diagramma end-to-end](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

[l'hub IOT Esplora](https://github.com/azure/iothub-explorer) è uno strumento CLI eseguite su un'identità di dispositivi toomanage computer host nel Registro di sistema hub IoT. È dotato di opzioni di gestione che è possibile utilizzare tooperform diverse attività.

| Opzione di gestione          | Attività                                                                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| Metodi diretti             | Rendere un dispositivo di eseguire operazioni quali l'avvio o arresto di invio di messaggi o il riavvio dispositivo hello.                                        |
| Proprietà desiderate del dispositivo gemello    | Inserire un dispositivo in determinati stati, ad esempio l'impostazione toogreen un LED o impostazione dati di telemetria hello trasmissione interval too30 minuti.         |
| Proprietà segnalate del dispositivo gemello   | Ottenere hello segnalato lo stato di un dispositivo. Ad esempio, il dispositivo di hello segnala hello che LED è lampeggiante ora.                                    |
| Tag dei dispositivi gemelli                  | Archiviare i metadati specifici del dispositivo nel cloud hello. Salve, ad esempio, il percorso di distribuzione di una macchina distributore.                         |
| Messaggi da cloud a dispositivo   | Invio dispositivo tooa notifiche. Ad esempio, "è molto probabile toorain oggi. Non dimenticare toobring un ombrello."              |
| Query del dispositivo gemello        | Eseguire una query tutti i dispositivi gemelli tooretrieve quelli con condizioni arbitrarie, ad esempio di identificare i dispositivi di hello che sono disponibili per l'utilizzo. |

Per ulteriori spiegazioni sulle differenze di hello e istruzioni sull'uso di queste opzioni, vedere [materiale sussidiario per la comunicazione da dispositivo a cloud](iot-hub-devguide-d2c-guidance.md) e [indicazioni di comunicazione Cloud a dispositivo](iot-hub-devguide-c2d-guidance.md).

> [!NOTE]
> I dispositivi gemelli sono documenti JSON nei quali vengono archiviate informazioni sullo stato dei dispositivi (metadati, configurazioni e condizioni). IoT Hub persiste doppi un dispositivo per ogni dispositivo che si connette tooit. Per altre informazioni sui dispositivi gemelli, vedere [Introduzione ai dispositivi gemelli](iot-hub-node-node-twin-getstarted.md).

## <a name="what-you-learn"></a>Contenuto dell'esercitazione

Si apprende l'uso di iothub-explorer con varie opzioni di gestione presenti nel proprio computer di sviluppo.

## <a name="what-you-do"></a>Operazioni da fare

Eseguire iothub-explorer con diverse opzioni di gestione.

## <a name="what-you-need"></a>Elementi necessari

- Esercitazione [configurare il dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) completato che copre hello seguenti requisiti:
  - Una sottoscrizione di Azure attiva.
  - Un hub IoT di Azure nella sottoscrizione.
  - Un'applicazione client che invia l'hub IoT di Azure tooyour messaggi.
- Verificare che il dispositivo è in esecuzione con un'applicazione client hello durante questa esercitazione.
- iothub-explorer, [Installare iothub-explorer](https://github.com/azure/iothub-explorer) sul computer di sviluppo.

## <a name="connect-tooyour-iot-hub"></a>Collegare tooyour IoT hub

Connettersi hub IoT tooyour eseguendo hello comando seguente:

```bash
iothub-explorer login <your IoT hub connection string>
```

## <a name="use-iothub-explorer-with-direct-methods"></a>Usare iothub-explorer con i metodi diretti

Richiamare hello `start` metodo hello dispositivo app toosend messaggi tooyour IoT hub eseguendo hello comando seguente:

```bash
iothub-explorer device-method <your device Id> start
```

Richiamare hello `stop` metodo hello dispositivo app toostop invio messaggi hub IoT tooyour eseguendo hello comando seguente:

```bash
iothub-explorer device-method <your device Id> stop
```

## <a name="use-iothub-explorer-with-twins-desired-properties"></a>Usare iothub-explorer con le proprietà desiderate del dispositivo gemello

Impostare un intervallo di proprietà desiderato = 3000 eseguendo hello comando seguente:

```bash
iothub-explorer update-twin <your device id> {\"properties\":{\"desired\":{\"interval\":3000}}}
```

Questa proprietà può essere letta dal dispositivo.

## <a name="use-iothub-explorer-with-twins-reported-properties"></a>Usare iothub-explorer con le proprietà segnalate del dispositivo gemello

Ottengano hello segnalato le proprietà del dispositivo hello eseguendo hello comando seguente:

```bash
iothub-explorer get-twin <your device id>
```

Una delle proprietà di hello è $metadata. $lastUpdated che mostra hello ultima volta il dispositivo invia o riceve un messaggio.

## <a name="use-iothub-explorer-with-twins-tags"></a>Usare iothub-explorer con i tag del dispositivo gemello

Visualizzare i tag hello e le proprietà del dispositivo hello eseguendo hello comando seguente:

```bash
iothub-explorer get-twin <your device id>
```

Aggiungere un ruolo di campo = temperatura e umidità dispositivo toohello eseguendo hello comando seguente:

```bash
iothub-explorer update-twin <your device id> "{\"tags\":{\"role\":\"temperature&humidity\"}}"

```

## <a name="use-iothub-explorer-with-cloud-to-device-messages"></a>Usare iothub-explorer con i messaggi da cloud a dispositivo

Invio di un dispositivo di toohello messaggio "Hello World" eseguendo hello comando seguente:

```bash
iothub-explorer send <device-id> "Hello World"
```

Vedere [usare hub IOT Esplora toosend e ricevere messaggi tra il dispositivo e l'IoT Hub](iot-hub-explorer-cloud-device-messaging.md) per uno scenario reale di utilizzo del comando.

## <a name="use-iothub-explorer-with-device-twins-queries"></a>Usare iothub-explorer con le query del dispositivo gemello

Query di dispositivi con un tag di ruolo = 'temperatura e umidità' eseguendo hello comando seguente:

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role = 'temperature&humidity'"
```

Eseguire una query tutti i dispositivi, ad eccezione di quelli con un tag di ruolo = 'temperatura e umidità' eseguendo hello comando seguente:

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role != 'temperature&humidity'"
```

## <a name="next-steps"></a>Passaggi successivi

Si è appreso come toouse hub IOT-Esplora con diverse opzioni di gestione.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
