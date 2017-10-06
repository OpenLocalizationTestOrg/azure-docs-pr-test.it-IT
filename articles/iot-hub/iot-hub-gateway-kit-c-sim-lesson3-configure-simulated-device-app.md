---
title: 'Dispositivo simulato e gateway Azure IoT: lezione 3: Eseguire l''app di esempio | Documentazione Microsoft'
description: Esecuzione di un dispositivo simulato esempio app toosend temperatura dati tooyour hub IoT
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: dati toocloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5d051d99-9749-4150-b3c8-573b0bda9c52
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: bc2c97919e95e4e3977a8b6ac75162bf2b5017be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a>Configurare ed eseguire un'app di esempio per dispositivo simulato

## <a name="what-you-will-do"></a>Contenuto dell'esercitazione

- Repository di esempio hello clone.
- Usare l'hub IoT e informazioni sul dispositivo logico hello Azure CLI tooget per l'applicazione di esempio dispositivo simulato. Configurare ed eseguire l'applicazione di esempio dispositivo simulato hello.

Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione

Contenuto dell'articolo:

- Come tooconfigure e hello esecuzione simulate dell'applicazione di esempio di dispositivo.

## <a name="what-you-need"></a>Elementi necessari

È necessario aver completato:

- [Creare un hub IoT e registrare il dispositivo](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a>Clonare il computer host toohello di hello esempio repository

repository di esempio hello tooclone, seguire questi passaggi nel computer host hello:

1. Aprire un prompt dei comandi in Windows o aprire un terminale in macOS o in Ubuntu.
2. Eseguire hello seguenti comandi:

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-hello-simulated-device-and-your-nuc"></a>Configurare dispositivo simulato hello e il NUC

1. File di configurazione Open hello `config.json` nel codice di Visual Studio eseguendo hello comando seguente:

   ```bash
   code config.json
   ```

2. Sostituire `"has_sensortag": true` con `"has_sensortag": false`.

   ![Configurazione quando non si ha un dispositivo TI SensorTag](media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. Inizializzare i file di configurazione hello eseguendo hello seguenti comandi:

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. Aprire `config-gateway.json` nel codice di Visual Studio eseguendo hello comando seguente:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. Individuare hello successiva riga di codice e sostituire `[device hostname or IP address]` con nome host o indirizzo IP di hello NUC Intel.
   ![Screenshot del gateway di configurazione](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)

## <a name="get-hello-connection-string-of-your-iot-hub-logical-device"></a>Ottiene la stringa di connessione hello del dispositivo logico hub IoT

hello tooget stringa di connessione hub IoT di Azure del dispositivo logico, eseguire hello comando nel computer host hello seguente:

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

`{IoT hub name}`è nome dell'hub IoT hello utilizzato. Usare iot-gateway come valore hello `{resource group name}` e utilizzare mydevice come valore hello `{device id}` se non si sono modificati valore hello nella lezione 2.

## <a name="configure-hello-simulated-device-cloud-upload-sample-application"></a>Configurare applicazione di esempio caricamento cloud dispositivo simulato hello

tooconfigure e hello esecuzione simulato dispositivo cloud caricare l'applicazione di esempio, seguire questi passaggi nel computer host hello:

1. Aprire `config-sensortag.json` nel codice di Visual Studio eseguendo hello comando seguente:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![Screenshot di SensorTag di configurazione](media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. Apportare hello sostituzioni nel codice hello seguenti:
   - Sostituire `[IoT hub name]` con il nome dell'hub IoT hello.
   - Sostituire `[IoT device connection string]` con la stringa di connessione hello del dispositivo logico hub IoT.

3. Eseguire un'applicazione hello.

   Distribuire ed eseguire un'applicazione hello eseguendo hello comando seguente:

   ```bash
   gulp run
   ```

## <a name="verify-hello-sample-application-works"></a>Verificare il funzionamento dell'applicazione di esempio hello

Viene visualizzato l'output seguente hello:

![Output dell'applicazione di esempio per il dispositivo simulato](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

un'applicazione Hello invia temperatura dati tooyour IoT hub, che dura 40 secondi.

## <a name="summary"></a>Riepilogo

È stato configurato correttamente e hello esecuzione simulato dispositivo cloud caricamento applicazione di esempio invia l'hub IoT tooyour dati con dispositivo simulato.

## <a name="next-steps"></a>Passaggi successivi
[Leggere messaggi dall'hub IoT](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)