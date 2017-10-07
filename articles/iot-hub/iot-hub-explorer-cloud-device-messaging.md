---
title: dispositivo cloud di Azure IoT Hub aaaManage messaggistica con l'hub IOT Esplora | Documenti Microsoft
description: Scopri toouse hello messaggi di hub IOT Esplora CLI strumento toomonitor dispositivo toocloud (D2C) e inviare messaggi di toodevice (C2D) di cloud in Azure IoT Hub.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Esplora l'hub IOT, cloud dispositivo messaggistica, iot hub cloud toodevice, cloud toodevice messaggistica
ms.assetid: 04521658-35d3-4503-ae48-51d6ad3c62cc
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: 741383b5631714cc2fef3309541fd2117aa7824c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-toosend-and-receive-messages-between-your-device-and-iot-hub"></a>Usare l'hub IOT Esplora toosend e ricevere messaggi tra il dispositivo e l'IoT Hub

![Diagramma end-to-end](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

[iothub-explorer](https://github.com/azure/iothub-explorer) include una gamma di comandi che semplificano la gestione dell'hub IoT. In questa esercitazione viene illustrato come toouse hub IOT Esplora toosend e ricevere messaggi tra il dispositivo e l'hub IoT.

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione

Si apprenderà come toouse messaggi da dispositivo a cloud di hub IOT Esplora toomonitor e cloud a dispositivo toosend. I messaggi da dispositivo a cloud potrebbe essere che il dispositivo raccoglie e quindi invia l'hub IoT tooyour dati del sensore. I messaggi da cloud a dispositivo potrebbe essere che l'hub IoT invia un LED che è un dispositivo connesso tooyour tooyour dispositivo tooblink comandi.

## <a name="what-you-will-do"></a>Contenuto dell'esercitazione

- Utilizzare i messaggi da dispositivo a cloud di hub IOT Esplora toomonitor.
- Usare l'hub IOT Esplora toosend cloud a dispositivo messaggi.

## <a name="what-you-need"></a>Elementi necessari

- Esercitazione [configurare il dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) completato che copre hello seguenti requisiti:
  - Una sottoscrizione di Azure attiva.
  - Un hub IoT di Azure nella sottoscrizione.
  - Un'applicazione client che invia l'hub IoT di Azure tooyour messaggi.
- iothub-explorer. ([Installare iothub-explorer](https://github.com/azure/iothub-explorer))

## <a name="monitor-device-to-cloud-messages"></a>Monitorare i messaggi da dispositivo a cloud

toomonitor i messaggi inviati dall'hub IoT di tooyour di dispositivo, seguire questi passaggi:

1. Aprire una finestra della console.
1. Eseguire hello comando seguente:

   ```bash
   iothub-explorer monitor-events <device-id> --login "<IoTHubConnectionString>"
   ```

   > [!Note]
   > Ottenere `<device-id>` e `<IoTHubConnectionString>` dall'hub IoT. Assicurarsi che aver esercitazione precedente hello. Oppure è possibile provare toouse `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` se hai `HostName`, `SharedAccessKeyName` e `SharedAccessKey`.

## <a name="send-cloud-to-device-messages"></a>Inviare messaggi da cloud a dispositivo

toosend un messaggio dal dispositivo tooyour hub IoT, seguire questi passaggi:

1. Aprire una finestra della console.
1. Avviare una sessione dell'hub IoT eseguendo hello comando seguente:

   ```bash
   iothub-explorer login `<IoTHubConnectionString>`
   ```

1. Invio di un dispositivo tooyour messaggio eseguendo hello comando seguente:

   ```bash
   iothub-explorer send <device-id> <message>
   ```

comando Hello lampeggia hello LED che è un dispositivo connesso tooyour e invia dispositivo tooyour di messaggio hello.

> [!Note]
> Non è necessario per hello dispositivo toosend un hub IoT di ack separato comando tooyour indietro quando viene ricevuto il messaggio hello.

## <a name="next-steps"></a>Passaggi successivi

Si è appreso come toomonitor dispositivo a cloud messaggi e inviare messaggi da cloud a dispositivo tra il dispositivo IoT IoT Hub di Azure.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
