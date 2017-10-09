---
title: 'Dispositivo SensorTag e gateway Azure IoT: lezione 3: Eseguire l''app di esempio | Documentazione Microsoft'
description: Eseguire dati tooreceive di applicazione di esempio BILITA da BILITA SensorTag e dall'hub IoT.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Disattiva app sensore monitoraggio dell'app, la raccolta dei dati del sensore, dati da sensori, sensore dati toocloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: b33e53a1-1df7-4412-ade1-45185aec5bef
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4a8acdeadd402ffc82d3b766e1ec03a77ddcebb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-ble-sample-application"></a>Configurare ed eseguire un'applicazione di esempio BLE

## <a name="what-you-will-do"></a>Contenuto dell'esercitazione

- Repository di esempio hello clone. 
- Configurare la connettività di hello tra SensorTag e NUC Intel. 
- Usare l'hub IoT e informazioni SensorTag hello Azure CLI tooget per un'applicazione di esempio BILITA (Bluetooth consumo energetico). E configurare ed eseguire l'applicazione di esempio BILITA hello. 

Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione

Contenuto dell'articolo:

- Come tooconfigure e hello esecuzione Disattiva applicazione di esempio.

## <a name="what-you-need"></a>Elementi necessari

È necessario aver completato:

- [Create an IoT hub and register SensorTag](iot-hub-gateway-kit-c-lesson2-register-device.md) (Creare un hub IoT e registrare SensorTag)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a>Clonare il computer host toohello di hello esempio repository

repository di esempio hello tooclone, seguire questi passaggi nel computer host hello:

1. Aprire una finestra del prompt dei comandi in Windows o aprire un terminale in macOS o in Ubuntu.
2. Eseguire hello seguenti comandi:

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="set-up-hello-connectivity-between-sensortag-and-intel-nuc"></a>Configurare la connettività di hello tra SensorTag e Intel NUC

tooset della connettività di hello, seguire questi passaggi nel computer host hello:

1. Inizializzare i file di configurazione hello eseguendo hello seguenti comandi:

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

2. Aprire `config-gateway.json` nel codice di Visual Studio eseguendo hello comando seguente:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

3. Individuare hello successiva riga di codice e sostituire `[device hostname or IP address]` con hello IP indirizzo o il nome host di NUC Intel.
   ![Screenshot del gateway di configurazione](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)

4. Installare gli strumenti di supporto su Intel NUC eseguendo hello comando seguente:

   ```bash
   gulp install-tools
   ```

5. Attivare SensorTag premendo il pulsante di alimentazione hello come immagine hello e hello che dovrebbe lampeggiare LED verde.

   ![Accendere SensorTag](media/iot-hub-gateway-kit-lessons/lesson3/turn on_off sensortag.jpg)

6. Analizza i dispositivi SensorTag eseguendo hello seguenti comandi:

   ```bash
   gulp discover-sensortag
   ```

7. Testare la connettività hello hello SensorTag e Intel NUC eseguendo hello comando seguente:

   ```bash
   gulp test-connectivity --mac {mac address}
   ```

   Sostituire `{mac address}` con indirizzo MAC ottenuto nel passaggio precedente hello hello.

## <a name="get-hello-connection-string-of-sensortag"></a>Ottiene la stringa di connessione hello di SensorTag

hello tooget stringa di connessione hub IoT di Azure di SensorTag, eseguire hello comando nel computer host hello seguente:

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

`{IoT hub name}`è nome dell'hub IoT hello utilizzato. Usare iot-gateway come valore hello `{resource group name}` e utilizzare mydevice come valore hello `{device id}` se non si sono modificati valore hello nella lezione 2.

## <a name="configure-hello-ble-sample-application"></a>Configurare l'applicazione di esempio BILITA hello

tooconfigure e hello esecuzione applicazione di esempio BILITA, seguire questi passaggi nel computer host hello:

1. Aprire `config-sensortag.json` nel codice di Visual Studio eseguendo hello comando seguente:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![Screenshot di SensorTag di configurazione](media/iot-hub-gateway-kit-lessons/lesson3/config_sensortag.png)

2. Apportare hello sostituzioni nel codice hello seguenti:
   - Sostituire `[IoT hub name]` con nome dell'hub IoT hello utilizzato.
   - Sostituire `[IoT device connection string]` con la stringa di connessione hello di SensorTag ottenuto.
   - Sostituire `[device_mac_address]` con indirizzo MAC di hello SensorTag ottenuto hello.

3. Eseguire l'applicazione di esempio BILITA hello.

   hello toorun applicazione di esempio BILITA, seguire questi passaggi nel computer host hello:

   1. Accendere SensorTag.

   2. Distribuire ed eseguire l'applicazione di esempio hello BILITA Intel NUC eseguendo hello comando seguente:
   
      ```bash
      gulp run
      ```

## <a name="verify-that-hello-ble-sample-application-works"></a>Verificare il funzionamento dell'applicazione di esempio BILITA hello

Viene visualizzato un output simile hello seguente:

![Output dell'applicazione di esempio BLE](media/iot-hub-gateway-kit-lessons/lesson3/BLE_running.png)

applicazione di esempio Hello mantiene la raccolta dei dati di temperatura e lo ha inviato l'hub IoT tooyour. applicazione di esempio Hello termina automaticamente dopo l'invio di 40 secondi.

## <a name="summary"></a>Riepilogo

Siano correttamente configurare la connettività di hello tra SensorTag e Intel NUC ed eseguire un'applicazione di esempio BILITA che raccoglie e invia i dati da SensorTag tooyour IoT hub. Si è pronti toolearn come tooverify che ha ricevuto l'hub IoT hello dati.

## <a name="next-steps"></a>Passaggi successivi
[Leggere messaggi dall'hub IoT](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)