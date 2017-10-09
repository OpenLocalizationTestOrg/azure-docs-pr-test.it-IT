---
title: 'Connect Arduino (C) tooAzure IoT - lezione 4: modificare app | Documenti Microsoft'
description: Personalizzare hello toochange di messaggi hello LED di attivare e disattivare il comportamento.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: controllare il LED con Arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: d7a25430-450e-43c4-a3ed-1eed995b8b7e
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8cc438650f01ae4335d91c94df6a29e0ffbdc508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a>Modificare hello e disattivare il comportamento di hello LED
## <a name="what-you-will-do"></a>Contenuto dell'esercitazione
Personalizzare hello toochange di messaggi hello LED di attivare e disattivare il comportamento. Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) per la scheda Adafruit sfumatura M0 Wi-Fi Arduino.

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione
Utilizzare hello di toochange a funzioni aggiuntiva Arduino LED di attivare e disattivare il comportamento.

## <a name="what-you-need"></a>Elementi necessari
È necessario avere completato correttamente [eseguire un'applicazione di esempio sul cloud Arduino Lavagna tooreceive messaggi toodevice][receive-cloud-to-device-messages].

## <a name="add-functions-toomainc-and-gulpfilejs"></a>Aggiungere gulpfile.js e toomain.c di funzioni
1. Aprire l'applicazione di esempio hello nel codice di Visual Studio eseguendo hello seguenti comandi:

   ```bash
   cd Lesson4
   code .
   ```
2. Aprire hello `app.ino` file e quindi aggiungere hello seguenti funzioni dopo la funzione blinkLED():

   ```arduino
   static void turnOnLED()
   {
     digitalWrite(LED_PIN, HIGH);
   }

   static void turnOffLED()
   {
     digitalWrite(LED_PIN, LOW);
   }
   ```

   ![File app.ino con funzioni aggiunte][app-ino-file]
3. Aggiungere hello seguenti condizioni prima di hello `else if` blocco di hello `receiveMessageCallback` funzione:

   ```arduino
   else if (strcmp((const char*)value, "\"on\"") == 0)
   {
       turnOnLED();
   }
   else if (0 == strcmp((const char*)value, "\"off\"") == 0)
   {
       turnOffLED();
   }
   ```

   Ora è configurata hello applicazione toorespond toomore le istruzioni di esempio tramite i messaggi. Hello "on" istruzione attiva hello LED e hello "off" istruzione Disattiva hello LED.
4. Aprire il file gulpfile.js hello e quindi aggiungere una nuova funzione prima della funzione hello `sendMessage`:

   ```javascript
   var buildCustomMessage = function (messageId) {
     if ((messageId & 1) && (messageId < MAX_MESSAGE_COUNT)) {
       return new Message(JSON.stringify({ command: 'on', messageId: messageId }));
     } else if (messageId < MAX_MESSAGE_COUNT) {
       return new Message(JSON.stringify({ command: 'off', messageId: messageId }));
     } else {
       return new Message(JSON.stringify({ command: 'stop', messageId: messageId }));
     }
   };
   ```

   ![File gulpfile.js con funzione aggiunta][gulp-file-js]
5. In hello `sendMessage` di funzione, sostituire la riga hello `var message = buildMessage(sentMessageCount);` con una nuova riga hello mostrata nel seguente frammento di codice hello:

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. Salvare tutte le modifiche di hello.

### <a name="deploy-and-run-hello-sample-application"></a>Distribuire ed eseguire l'applicazione di esempio hello
Distribuire ed eseguire l'applicazione di esempio hello sulla Lavagna Arduino eseguendo hello comando seguente:

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

Si noterà accendere hello LED per due secondi e quindi disattivare per un altro due secondi. il messaggio "stop" ultimo Hello arresta l'applicazione di esempio hello esecuzione.

![accensione e spegnimento][on-and-off]

Congratulazioni. È stato personalizzato correttamente i messaggi hello inviati tooyour Arduino Lavagna dall'hub IoT.

### <a name="summary"></a>Riepilogo
Questa sezione facoltativa viene illustrata la modalità toocustomize dei messaggi in modo che l'applicazione di esempio hello può controllare hello e disattivare il comportamento di hello LED in modo diverso.

<!-- Images and links -->

[receive-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md
[app-ino-file]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_app_ino.png
[gulp-file-js]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_gulpfile_js.png
[on-and-off]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_on_and_off_arduino.png