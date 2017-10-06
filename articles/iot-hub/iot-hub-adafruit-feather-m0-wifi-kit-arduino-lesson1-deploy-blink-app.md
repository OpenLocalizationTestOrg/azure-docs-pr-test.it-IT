---
title: 'Connettersi Arduino tooAzure IoT - lezione 1: distribuire app | Documenti Microsoft'
description: Clonazione di un'applicazione hello esempio Arduino da GitHub ed eseguire gulp toodeploy questo tooyour applicazione Adafruit sfumatura M0 WiFi. Questa applicazione di esempio lampeggia hello GPIO
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: progetti led arduino, lampeggiamento led arduino, codice di lampeggiamento led arduino, programma di lampeggiamento arduino, esempio di lampeggiamento arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: b0a7d076-d580-4686-9f7d-c0712750b615
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5bf8e4ae88e070aeacf34bfc43b8d2daeeb1a2fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a>Creare e distribuire un'applicazione hello blink
## <a name="what-you-will-do"></a>Contenuto dell'esercitazione
Clonazione di un'applicazione hello esempio Arduino da GitHub e utilizzare hello gulp strumento toodeploy hello esempio applicazione tooyour Adafruit sfumatura M0 Wi-Fi Arduino Lavagna. applicazione di esempio Hello, hello intermittenze GPIO #13 barod LED ogni due secondi.

Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina][troubleshooting-page].

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione
* Come toodeploy e hello esecuzione applicazione sulla Lavagna Arduino di esempio.

## <a name="what-you-need"></a>Elementi necessari
È necessario che sia completata hello seguenti operazioni:

* [Configurare il dispositivo][configure-your-device]
* [Ottenere strumenti hello][get-the-tools]

## <a name="open-hello-sample-application"></a>Applicazione di esempio hello aperto
hello tooopen applicazione di esempio, seguire questi passaggi:

1. Clonare il repository di esempio hello da GitHub eseguendo hello comando seguente:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-feather-m0-getting-started.git
   ```
2. Aprire l'applicazione di esempio hello in Visual Studio Code eseguendo hello seguenti comandi:

   ```bash
   cd iot-hub-c-feather-m0-getting-started
   cd Lesson1
   code .
   ```

   ![Struttura del repository][repo-structure]

Hello `app.ino` file hello `app` sottocartella è hello i file di origine della chiave che contiene hello codice toocontrol hello LED.

### <a name="install-application-dependencies"></a>Installare le dipendenze dell'applicazione
Installare le librerie di hello e altri moduli, che è necessario per l'applicazione di esempio hello eseguendo hello comando seguente:

```bash
npm install
```

## <a name="configure-hello-device-connection"></a>Configurare una connessione al dispositivo hello
tooconfigure hello connessione al dispositivo, seguire questi passaggi:

1. Ottenere della porta seriale del dispositivo hello con hello dispositivo individuazione cli hello:

   ```bash
   devdisco list --usb
   ```

   Si dovrebbe vedere un output simile toohello seguenti e si trova hello usb porta COM per la scheda Arduino: ![individuazione dei dispositivi][device-discovery]

2. File aperti hello `config.json` in hello cartella lezione e aggiungere valore hello hello trovato numero di porta COM:

   ```json
   {
       "device_port" : "COM1"
   }
   ```
   ![config.json][config-json]
   > [!NOTE]
   > Per la porta COM hello, sulla piattaforma Windows, ha il formato di hello di `COM1, COM2, ...`. In macOS o Ubuntu inizia con `/dev/`.

## <a name="deploy-and-run-hello-sample-application"></a>Distribuire ed eseguire l'applicazione di esempio hello
### <a name="install-hello-required-tools-for-your-arduino-board"></a>Installare gli strumenti di hello necessario per la scheda Arduino

Installare hello Hub IoT di Azure SDK per la scheda Arduino eseguendo hello comando seguente:

```bash
gulp install-tools
```

Questa operazione potrebbe richiedere un toocomplete molto tempo, a seconda della connessione di rete.

> [!NOTE]
> Uscire da hello in esecuzione l'istanza Arduino IDE esecuzione attività gulp: `install-tools`, `run`.

### <a name="deploy-and-run-hello-sample-app"></a>Distribuire ed eseguire app di esempio hello
Distribuire ed eseguire l'applicazione di esempio hello eseguendo hello comando seguente:

```bash
gulp run

# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

### <a name="verify-hello-app-works"></a>Verificare il funzionamento dell'applicazione hello
Se non viene visualizzato hello LED è lampeggiante, vedere hello [risoluzione dei problemi guida] [ troubleshooting-page] per soluzioni ai problemi di toocommon.

![LED lampeggiante][led-blinking]

## <a name="summary"></a>Riepilogo
È stato installato toowork strumenti hello richiesto con la scheda Arduino e distribuito un hello della tooblink Lavagna di esempio applicazione tooyour Arduino LED. È ora possibile creare, distribuire e l'esecuzione di un'altra applicazione di esempio che si connette il tooAzure Lavagna Arduino toosend IoT Hub e ricevere messaggi.

## <a name="next-steps"></a>Passaggi successivi
[Ottenere hello gli strumenti di Azure][get-the-azure-tools]

<!-- Images and links -->

[troubleshooting-page]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-blink-arduino-mac.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[led-blinking]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md