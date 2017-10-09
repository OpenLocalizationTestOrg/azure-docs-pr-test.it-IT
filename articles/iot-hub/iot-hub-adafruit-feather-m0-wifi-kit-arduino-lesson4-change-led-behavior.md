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
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a><span data-ttu-id="2c7d5-104">Modificare hello e disattivare il comportamento di hello LED</span><span class="sxs-lookup"><span data-stu-id="2c7d5-104">Change hello on and off behavior of hello LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="2c7d5-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="2c7d5-105">What you will do</span></span>
<span data-ttu-id="2c7d5-106">Personalizzare hello toochange di messaggi hello LED di attivare e disattivare il comportamento.</span><span class="sxs-lookup"><span data-stu-id="2c7d5-106">Customize hello messages toochange hello LED’s on and off behavior.</span></span> <span data-ttu-id="2c7d5-107">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) per la scheda Adafruit sfumatura M0 Wi-Fi Arduino.</span><span class="sxs-lookup"><span data-stu-id="2c7d5-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="2c7d5-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="2c7d5-108">What you will learn</span></span>
<span data-ttu-id="2c7d5-109">Utilizzare hello di toochange a funzioni aggiuntiva Arduino LED di attivare e disattivare il comportamento.</span><span class="sxs-lookup"><span data-stu-id="2c7d5-109">Use additional Arduino functions toochange hello LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2c7d5-110">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="2c7d5-110">What you need</span></span>
<span data-ttu-id="2c7d5-111">È necessario avere completato correttamente [eseguire un'applicazione di esempio sul cloud Arduino Lavagna tooreceive messaggi toodevice][receive-cloud-to-device-messages].</span><span class="sxs-lookup"><span data-stu-id="2c7d5-111">You must have successfully completed [Run a sample application on your Arduino board tooreceive cloud toodevice messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-toomainc-and-gulpfilejs"></a><span data-ttu-id="2c7d5-112">Aggiungere gulpfile.js e toomain.c di funzioni</span><span class="sxs-lookup"><span data-stu-id="2c7d5-112">Add functions toomain.c and gulpfile.js</span></span>
1. <span data-ttu-id="2c7d5-113">Aprire l'applicazione di esempio hello nel codice di Visual Studio eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="2c7d5-113">Open hello sample application in Visual Studio code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="2c7d5-114">Aprire hello `app.ino` file e quindi aggiungere hello seguenti funzioni dopo la funzione blinkLED():</span><span class="sxs-lookup"><span data-stu-id="2c7d5-114">Open hello `app.ino` file, and then add hello following functions after blinkLED() function:</span></span>

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
3. <span data-ttu-id="2c7d5-116">Aggiungere hello seguenti condizioni prima di hello `else if` blocco di hello `receiveMessageCallback` funzione:</span><span class="sxs-lookup"><span data-stu-id="2c7d5-116">Add hello following conditions before hello `else if` block of hello `receiveMessageCallback` function:</span></span>

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

   <span data-ttu-id="2c7d5-117">Ora è configurata hello applicazione toorespond toomore le istruzioni di esempio tramite i messaggi.</span><span class="sxs-lookup"><span data-stu-id="2c7d5-117">Now you’ve configured hello sample application toorespond toomore instructions through messages.</span></span> <span data-ttu-id="2c7d5-118">Hello "on" istruzione attiva hello LED e hello "off" istruzione Disattiva hello LED.</span><span class="sxs-lookup"><span data-stu-id="2c7d5-118">hello "on" instruction turns on hello LED, and hello "off" instruction turns off hello LED.</span></span>
4. <span data-ttu-id="2c7d5-119">Aprire il file gulpfile.js hello e quindi aggiungere una nuova funzione prima della funzione hello `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="2c7d5-119">Open hello gulpfile.js file, and then add a new function before hello function `sendMessage`:</span></span>

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
5. <span data-ttu-id="2c7d5-121">In hello `sendMessage` di funzione, sostituire la riga hello `var message = buildMessage(sentMessageCount);` con una nuova riga hello mostrata nel seguente frammento di codice hello:</span><span class="sxs-lookup"><span data-stu-id="2c7d5-121">In hello `sendMessage` function, replace hello line `var message = buildMessage(sentMessageCount);` with hello new line shown in hello following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="2c7d5-122">Salvare tutte le modifiche di hello.</span><span class="sxs-lookup"><span data-stu-id="2c7d5-122">Save all hello changes.</span></span>

### <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="2c7d5-123">Distribuire ed eseguire l'applicazione di esempio hello</span><span class="sxs-lookup"><span data-stu-id="2c7d5-123">Deploy and run hello sample application</span></span>
<span data-ttu-id="2c7d5-124">Distribuire ed eseguire l'applicazione di esempio hello sulla Lavagna Arduino eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2c7d5-124">Deploy and run hello sample application on your Arduino board by running hello following command:</span></span>

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="2c7d5-125">Si noterà accendere hello LED per due secondi e quindi disattivare per un altro due secondi.</span><span class="sxs-lookup"><span data-stu-id="2c7d5-125">You should see hello LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="2c7d5-126">il messaggio "stop" ultimo Hello arresta l'applicazione di esempio hello esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2c7d5-126">hello last "stop" message stops hello sample application from running.</span></span>

![accensione e spegnimento][on-and-off]

<span data-ttu-id="2c7d5-128">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="2c7d5-128">Congratulations!</span></span> <span data-ttu-id="2c7d5-129">È stato personalizzato correttamente i messaggi hello inviati tooyour Arduino Lavagna dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2c7d5-129">You’ve successfully customized hello messages that are sent tooyour Arduino board from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="2c7d5-130">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="2c7d5-130">Summary</span></span>
<span data-ttu-id="2c7d5-131">Questa sezione facoltativa viene illustrata la modalità toocustomize dei messaggi in modo che l'applicazione di esempio hello può controllare hello e disattivare il comportamento di hello LED in modo diverso.</span><span class="sxs-lookup"><span data-stu-id="2c7d5-131">This optional section demonstrates how toocustomize messages so that hello sample application can control hello on and off behavior of hello LED in a different way.</span></span>

<!-- Images and links -->

[receive-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md
[app-ino-file]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_app_ino.png
[gulp-file-js]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_gulpfile_js.png
[on-and-off]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_on_and_off_arduino.png