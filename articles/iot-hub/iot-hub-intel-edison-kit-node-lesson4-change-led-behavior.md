---
title: 'Connettersi Edison Intel (nodo) tooAzure IoT - lezione 4: Blink hello LED | Documenti Microsoft'
description: Personalizzare hello toochange di messaggi hello LED di attivare e disattivare il comportamento.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: controllare il LED con Arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 387cd97e-b05e-43c4-b252-f68ad45d524a
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: caeabe311fd1698f298c6d2b4a203ecad80ef7df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a>Modificare hello e disattivare il comportamento di hello LED
## <a name="what-you-will-do"></a>Contenuto dell'esercitazione
Personalizzare hello toochange di messaggi hello LED di attivare e disattivare il comportamento. Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina][troubleshooting].

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione
Utilizzare hello toochange funzioni aggiuntive LED di attivare e disattivare il comportamento.

## <a name="what-you-need"></a>Elementi necessari
È necessario avere completato correttamente [eseguire un'applicazione di esempio nel cloud tooreceive Edison Intel messaggi toodevice][receive-cloud-to-device-messages].

## <a name="add-functions-tooappjs-and-gulpfilejs"></a>Aggiungere gulpfile.js e tooapp.js di funzioni
1. Aprire l'applicazione di esempio hello nel codice di Visual Studio eseguendo hello seguenti comandi:

   ```bash
   cd Lesson4
   code .
   ```
2. Aprire hello `app.js` file e quindi aggiungere hello seguenti funzioni dopo la funzione blinkLED():

   ```javascript
   function turnOnLED() {
     myLed.write(1);
   }

   function turnOffLED() {
     myLed.write(0);
   }
   ```

   ![File app.js con funzioni aggiunte](media/iot-hub-intel-edison-lessons/lesson4/updated_app_node.png)
3. Aggiungere hello le condizioni seguenti prima di hello 'blink' case nel blocco switch case hello di hello `receiveMessageCallback` funzione:

   ```javascript
   case 'on':
     turnOnLED();
     break;
   case 'off':
     turnOffLED();
     break;
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
   }
   ```

   ![File gulpfile.js con funzione aggiunta][gulpfile]
5. In hello `sendMessage` di funzione, sostituire la riga hello `var message = buildMessage(sentMessageCount);` con una nuova riga hello mostrata nel seguente frammento di codice hello:

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. Salvare tutte le modifiche di hello.

### <a name="deploy-and-run-hello-sample-application"></a>Distribuire ed eseguire l'applicazione di esempio hello
Distribuire ed eseguire l'applicazione di esempio hello Edison eseguendo hello comando seguente:

```bash
gulp deploy && gulp run
```

Si noterà accendere hello LED per due secondi e quindi disattivare per un altro due secondi. il messaggio "stop" ultimo Hello arresta l'applicazione di esempio hello esecuzione.

![accensione e spegnimento][on-and-off]

Congratulazioni. È stato personalizzato correttamente i messaggi hello inviati tooEdison dall'hub IoT.

### <a name="summary"></a>Riepilogo
Questa sezione facoltativa viene illustrata la modalità toocustomize dei messaggi in modo che l'applicazione di esempio hello può controllare hello e disattivare il comportamento di hello LED in modo diverso.

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-node-lesson4-send-cloud-to-device-messages.md
[gulpfile]: media/iot-hub-intel-edison-lessons/lesson4/updated_gulpfile_node.png
[on-and-off]: media/iot-hub-intel-edison-lessons/lesson4/gulp_on_and_off_node.png
