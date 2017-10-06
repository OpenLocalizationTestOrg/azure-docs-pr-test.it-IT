---
title: 'Connect Intel Edison (C) tooAzure IoT - lezione 4: Blink hello LED | Documenti Microsoft'
description: Personalizzare hello toochange di messaggi hello LED di attivare e disattivare il comportamento.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: controllare il LED con Arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 9826c55a-0e24-4296-ae54-29b7fe66436a
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c51acb42aa297ca91cfe76d7b0361ad95e2fb2e4
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

## <a name="add-functions-toomainc-and-gulpfilejs"></a>Aggiungere gulpfile.js e toomain.c di funzioni
1. Aprire l'applicazione di esempio hello nel codice di Visual Studio eseguendo hello seguenti comandi:

   ```bash
   cd Lesson4
   code .
   ```
2. Aprire hello `main.c` file e quindi aggiungere hello seguenti funzioni dopo la funzione blinkLED():

   ```c
   static void turnOnLED()
   {
     mraa_gpio_write(context, 1);
   }

   static void turnOffLED()
   {
     mraa_gpio_write(context, 0);
   }
   ```

   ![File main.c con funzioni aggiunte](media/iot-hub-intel-edison-lessons/lesson4/updated_app_c.png)

3. Aggiungere hello seguenti condizioni prima di hello `else if` blocco di hello `receiveMessageCallback` funzione:

   ```c
   else if (0 == strcmp((const char*)value, "\"on\""))
   {
       turnOnLED();
   }
   else if (0 == strcmp((const char*)value, "\"off\""))
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

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-c-lesson4-send-cloud-to-device-messages.md
[gulpfile]: media/iot-hub-intel-edison-lessons/lesson4/updated_gulpfile_c.png
[on-and-off]: media/iot-hub-intel-edison-lessons/lesson4/gulp_on_and_off_c.png
