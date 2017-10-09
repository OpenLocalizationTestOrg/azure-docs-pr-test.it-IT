---
title: aaaUse un tooconnect di gateway tooAzure un dispositivo IoT Hub IoT | Documenti Microsoft
description: Informazioni su come toouse NUC Intel come un tooconnect gateway IoT un SensorTag TI e trasmissione sensore dati tooAzure IoT Hub in hello cloud.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: gateway IOT connettersi toocloud dispositivo
ms.assetid: cb851648-018c-4a7e-860f-b62ed3b493a5
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: 418af34bf29992d46b76ae59ef548744808664c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-tooconnect-things-toohello-cloud---sensortag-tooazure-iot-hub"></a>Utilizzare il cloud IoT gateway tooconnect operazioni toohello - SensorTag tooAzure IoT Hub

> [!NOTE]
> Prima di iniziare questa esercitazione, assicurarsi di aver completato [Configurare Intel NUC come gateway IoT di Azure](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md). In [impostare NUC Intel come gateway IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), si configura il dispositivo Intel NUC hello come gateway IoT.

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione

Si apprenderà come toouse un tooconnect gateway IoT un IoT Hub di tooAzure Texas strumenti SensorTag (CC2650STK). gateway IoT Hello invia temperatura e umidità raccolti da hello SensorTag tooAzure IoT Hub.

## <a name="what-you-will-do"></a>Contenuto dell'esercitazione

- Creare un hub IoT.
- Registrare un dispositivo nell'hub IoT hello per hello SensorTag.
- Abilitare la connessione di hello tra gateway IoT hello e hello SensorTag.
- Eseguire un BILITA esempio applicazione toosend SensorTag dati tooyour hub IoT.

## <a name="what-you-need"></a>Elementi necessari

- Completare l'esercitazione [Configurare Intel NUC come gateway IoT di Azure](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) in cui si configura il dispositivo Intel NUC come gateway IoT.
- * Una sottoscrizione di Azure attiva. Se non si ha un account Azure, [creare un account Azure gratuito](https://azure.microsoft.com/free/) in pochi minuti.
- Un client SSH in esecuzione nel computer host. Si consiglia l'uso di PuTTY in Windows. Linux e macOS sono già dotati di un client SSH.
- indirizzo IP Hello e hello nome utente e password tooaccess hello gateway dal client SSH hello.
- Una connessione Internet.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

> [!NOTE]
> Qui è possibile registrare questo nuovo dispositivo per SensorTag

## <a name="enable-hello-connection-between-hello-iot-gateway-and-hello-sensortag"></a>Abilitare hello connessione tra gateway IoT hello e hello SensorTag

In questa sezione è eseguire hello seguenti attività:

- Ottenere l'indirizzo MAC hello di hello SensorTag per connessione Bluetooth.
- Avviare una connessione Bluetooth da hello IoT gateway toohello SensorTag.

### <a name="get-hello-mac-address-of-hello-sensortag-for-bluetooth-connection"></a>Ottenere l'indirizzo MAC hello di hello SensorTag per connessione Bluetooth

1. Nel computer host hello, eseguire client SSH hello e toohello IoT gateway di connessione.
1. Sbloccare Bluetooth eseguendo hello comando seguente:

   ```bash
   sudo rfkill unblock bluetooth
   ```

1. Avviare il servizio di Bluetooth hello sul gateway IoT hello e immettere un tooconfigure shell Bluetooth Bluetooth eseguendo hello seguenti comandi:

   ```bash
   sudo systemctl start bluetooth
   bluetoothctl
   ```

1. Accendere il controller Bluetooth hello eseguendo hello comando in hello Bluetooth shell seguente:

   ```bash
   power on
   ```

   ![alimentazione sul controller Bluetooth hello gateway IoT hello con bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/8_power-on-bluetooth-controller-at-bluetooth-shell-bluetoothctl.png)

1. Avvia l'analisi per i dispositivi Bluetooth circostanti eseguendo hello comando seguente:

   ```bash
   scan on
   ```

   ![Analizzare i dispositivi Bluetooth citcostanti con bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/9_start-scan-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

1. Premere hello pulsante hello SensorTag l'associazione. Hello verde LED sul hello SensorTag lampeggia.
1. In hello shell Bluetooth, dovrebbe essere hello che sensortag viene trovato. Prendere nota dell'indirizzo MAC di hello SensorTag hello. In questo esempio, è l'indirizzo MAC di hello SensorTag hello `24:71:89:C0:7F:82`.
1. Disattiva analisi hello eseguendo hello comando seguente:

   ```bash
   scan off
   ```

   ![Interrompere l'analisi dei dispositivi Bluetooth circostanti con bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/10_stop-scanning-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

### <a name="initiate-a-bluetooth-connection-from-hello-iot-gateway-toohello-sensortag"></a>Avviare una connessione Bluetooth da hello IoT gateway toohello SensorTag

1. Connettersi toohello SensorTag eseguendo hello comando seguente:

   ```bash
   connect <MAC address>
   ```

   ![Connettersi toohello SensorTag con bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/11_connect-to-sensortag-at-bluetooth-shell-bluetoothctl.png)

1. Disconnettersi hello SensorTag e uscire dalla shell Bluetooth hello eseguendo hello seguenti comandi:

   ```bash
   disconnect
   exit
   ```

   ![Disconnettersi da hello SensorTag con bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/12_disconnect-from-sensortag-at-bluetooth-shell-bluetoothctl.png)

Connessione hello tra hello SensorTag e gateway IoT hello abilitato.

## <a name="run-a-ble-sample-application-toosend-sensortag-data-tooyour-iot-hub"></a>Eseguire un BILITA esempio applicazione toosend SensorTag dati tooyour hub IoT

applicazione di esempio Bluetooth bassa energia (disattiva) Hello viene fornito da Azure IoT Edge. applicazione di esempio Hello raccoglie i dati dalla connessione attiva e inviare l'hub IoT tooyou dati hello. applicazione di esempio hello toorun, è necessario:

1. Configurare l'applicazione di esempio hello.
1. Eseguire l'applicazione di esempio hello gateway IoT hello.

### <a name="configure-hello-sample-application"></a>Configurare l'applicazione di esempio hello

1. Consente di passare toohello cartella dell'applicazione di esempio hello eseguendo hello comando seguente:

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples/ble_gateway
   ```

1. Aprire il file di configurazione di hello eseguendo hello comando seguente:

   ```bash
   vi ble_gateway.json
   ```

1. Nel file di configurazione hello compilare hello seguenti valori:

   **IoTHubName**: nome hello dell'hub IoT.

   **IoTHubSuffix**: IoTHubSuffix ottenere dalla chiave primaria di hello come hello dispositivo della stringa di connessione che si è preso nota verso il basso. Assicurarsi di ottenere la chiave primaria di hello hello dispositivo della stringa di connessione, non hello chiave primaria della stringa di connessione hub IoT. chiave primaria di Hello della stringa di connessione del dispositivo hello è nel formato hello `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.

   **Trasporto**: valore predefinito di hello è `amqp`. Questo valore Mostra protocollo hello durante transpotation. Potrebbe essere `http`, `amqp` o `mqtt`.

   **macAddress**: hello indirizzo MAC di hello SensorTag annotato verso il basso.

   **deviceID**: ID del dispositivo hello creato nell'hub IoT.

   **deviceKey**: chiave primaria di hello hello dispositivo della stringa di connessione.

   ![File di configurazione hello completa dell'applicazione di esempio BILITA hello](./media/iot-hub-iot-gateway-connect-device-to-cloud/13_edit-config-file-of-ble-sample.png)

1. Premere `ESC` e tipo `:wq` file hello toosave.

### <a name="run-hello-sample-application"></a>Eseguire l'applicazione di esempio hello

1. Verificare che hello che sensortag viene acceso.
1. Eseguire hello comando seguente:

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a>Passaggi successivi

[Usare il gateway IoT per la trasformazione dei dati del sensore con Azure IoT Edge](iot-hub-gateway-kit-c-use-iot-gateway-for-data-conversion.md)
