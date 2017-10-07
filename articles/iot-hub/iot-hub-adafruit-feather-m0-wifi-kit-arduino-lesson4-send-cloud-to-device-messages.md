---
title: 'Connect Arduino (C) tooAzure IoT - lezione 4: Cloud a dispositivo | Documenti Microsoft'
description: "Un'applicazione di esempio viene eseguita nel dispositivo Adafruit Feather M0 WiFi e monitora i messaggi in ingresso dall'hub IoT. Una nuova attività gulp invia messaggi tooAdafruit Wi-Fi M0 sfumatura da hello di tooblink l'hub IoT LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: led di controllo arduino dal web, led di controllo arduino tramite web
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: a0bf53fb-29fb-485f-ba4a-6c715057b1a2
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: dcddd61ff684f49436103675938d719cb227c409
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a>Eseguire un tooreceive di applicazione di esempio i messaggi da cloud a dispositivo
In questo articolo si distribuisce un'applicazione di esempio nella scheda Arduino Adafruit Feather M0 WiFi.

applicazione di esempio Hello controlla i messaggi in ingresso dall'hub IoT. Inoltre si esegue un'attività gulp su tooyour di messaggi del toosend computer Arduino Lavagna dall'hub IoT. Quando l'applicazione di esempio hello riceve messaggi hello, lampeggia hello LED. Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina][troubleshooting].

## <a name="what-you-will-do"></a>Contenuto dell'esercitazione
* Connettere l'hub IoT hello esempio applicazione tooyour.
* Distribuire ed eseguire l'applicazione di esempio hello.
* Invio di messaggi dal hello della tooblink Lavagna di IoT hub tooyour Arduino LED.

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione
Contenuto dell'articolo:
* La modalità in ingresso toomonitor dei messaggi dall'hub IoT.
* La modalità toosend cloud a dispositivo dei messaggi dal tooyour hub IoT Arduino Lavagna.

## <a name="what-you-need"></a>Elementi necessari
* La scheda Arduino pronta all'uso. toolearn tooset la tavola da Arduino, vedere [configurare il dispositivo][configure-your-device].
* Un hub IoT creato nella propria sottoscrizione di Azure. toolearn come toocreate l'hub IoT, vedere [creare l'IoT Hub Azure][create-your-azure-iot-hub].

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a>Collegare hello esempio applicazione tooyour IoT hub

1. Assicurarsi che si è nella cartella repository hello `iot-hub-c-feather-m0-getting-started`.

   Aprire l'applicazione di esempio hello in Visual Studio Code eseguendo hello seguenti comandi:

   ```bash
   cd Lesson4
   code .
   ```

   Hello preavviso `app.ino` file hello `app` sottocartella. Hello `app.ino` è hello i file di origine della chiave che contiene i messaggi in ingresso hello codice toomonitor dall'hub IoT hello. Hello `blinkLED` funzione lampeggia hello LED.

   ![Struttura repository nell'applicazione di esempio hello][repo-structure]

2. Ottenere della porta seriale del dispositivo hello con hello dispositivo individuazione cli hello:

   ```bash
   devdisco list --usb
   ```

   Si dovrebbe vedere un output simile toohello seguente e trovare hello usb porta COM per la scheda Arduino:

   ![Individuazione del dispositivo][device-discovery]

3. File aperti hello `config.json` hello lezione cartella e il valore di input hello di trovare il numero di porta COM hello:

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > Per la porta COM hello, sulla piattaforma Windows, ha il formato di hello di `COM1, COM2, ...`. In macOS o Ubuntu inizia con `/dev/`.

4. Inizializzare i file di configurazione hello eseguendo hello seguenti comandi:

   ```bash
   # For Windows command prompt
   npm install
   gulp init
   gulp install-tools
   ```

5. Rendere hello seguenti sostituzioni hello `config-arduino.json` file:

   Se è stato completato i passaggi di hello in [creare un account di archiviazione e l'app Azure funzione] [ create-an-azure-function-app-and-storage-account] su questo computer, tutte le configurazioni di hello vengono ereditate, pertanto è possibile ignorare hello passaggio toohello attività di distribuzione e in esecuzione l'applicazione di esempio hello. Se è stato completato i passaggi di hello in [creare un account di archiviazione e l'app Azure funzione] [ create-an-azure-function-app-and-storage-account] in un computer diverso, è necessario segnaposto hello tooreplace hello `config-arduino.json` file. Hello `config-arduino.json` file si trova nella sottocartella hello della cartella principale.

   ![Contenuto del file di configurazione arduino.json hello][config-arduino-json]

   * Sostituire **[Wi-Fi SSID]** con il SSID Wi-Fi che è connesso a Internet toohello.
   * Sostituire **[Wi-Fi password]** con la password Wi-Fi. Rimuovere la stringa hello se il Wi-Fi non richiede una password.
   * Sostituire **[stringa di connessione dispositivo IoT]** con stringa di connessione hello dispositivo che si ottiene eseguendo hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` comando.
   * Sostituire **[stringa di connessione hub IoT]** con stringa di connessione hub IoT che si ottiene eseguendo hello hello `az iot hub show-connection-string --name {my hub name}` comando.

## <a name="deploy-and-run-hello-sample-application"></a>Distribuire ed eseguire l'applicazione di esempio hello
Distribuire ed eseguire l'applicazione di esempio hello sulla Lavagna Arduino eseguendo hello seguenti comandi:

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

comando gulp Hello distribuisce la Lavagna Arduino hello esempio applicazione tooyour. Quindi viene eseguita un'applicazione hello la Lavagna Arduino e un'attività separata nell'host della Lavagna di Arduino tooyour messaggi blink toosend 20 computer dall'hub IoT.

Quando si esegue l'applicazione di esempio hello, avvia l'ascolto toomessages dall'hub IoT. Nel frattempo, attività gulp hello invia messaggi di "blink" diversi dai tooyour hub IoT Arduino Lavagna. Per ogni messaggio blink hello Lavagna riceve, applicazione di esempio hello chiama hello `blinkLED` hello tooblink funzione LED.

Dovrebbe essere hello LED blink ogni due secondi, come attività gulp hello invia 20 messaggi dal tooyour hub IoT Arduino Lavagna. Hello ultimo uno è un messaggio "stop" che interrompe l'esecuzione di un'applicazione hello.

![Applicazione di esempio con comando gulp e messaggi di lampeggiamento][sample-application]

## <a name="summary"></a>Riepilogo
I messaggi inviati correttamente dal hello della tooblink Lavagna di IoT hub tooyour Arduino LED. attività successiva Hello è facoltativo: modificare hello e disattivare il comportamento di hello LED.

## <a name="next-steps"></a>Passaggi successivi
[Modificare hello e disattivare il comportamento di hello LED][change-the-on-and-off-led-behavior]


<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/repo_structure_arduino.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[create-an-azure-function-app-and-storage-account]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/config-arduino.png
[sample-application]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_blink_arduino.png
[change-the-on-and-off-led-behavior]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-change-led-behavior.md