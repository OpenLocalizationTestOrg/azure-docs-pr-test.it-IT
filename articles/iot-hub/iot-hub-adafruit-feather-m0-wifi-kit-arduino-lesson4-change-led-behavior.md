---
title: 'Connettere Arduino (C) ad Azure IoT: lezione 4: Modificare l''app | Documentazione Microsoft'
description: Personalizzare i messaggi per modificare il comportamento di accensione e spegnimento del LED.
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
ms.openlocfilehash: 5009a0466f2c5689b8ab426049f4c4f02272512b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-on-and-off-behavior-of-the-led"></a><span data-ttu-id="7e3e0-104">Modificare il comportamento di accensione e spegnimento del LED</span><span class="sxs-lookup"><span data-stu-id="7e3e0-104">Change the on and off behavior of the LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="7e3e0-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="7e3e0-105">What you will do</span></span>
<span data-ttu-id="7e3e0-106">Personalizzare i messaggi per modificare il comportamento di accensione e spegnimento del LED.</span><span class="sxs-lookup"><span data-stu-id="7e3e0-106">Customize the messages to change the LED’s on and off behavior.</span></span> <span data-ttu-id="7e3e0-107">In caso di problemi con la scheda Arduino per Adafruit Feather M0 WiFi, cercare le soluzioni nella [pagina sulla risoluzione dei problemi](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="7e3e0-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="7e3e0-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="7e3e0-108">What you will learn</span></span>
<span data-ttu-id="7e3e0-109">Usare funzioni aggiuntive di Arduino per modificare il comportamento di accensione e spegnimento del LED.</span><span class="sxs-lookup"><span data-stu-id="7e3e0-109">Use additional Arduino functions to change the LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7e3e0-110">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="7e3e0-110">What you need</span></span>
<span data-ttu-id="7e3e0-111">È necessario aver completato la sezione [Eseguire l'applicazione di esempio nella scheda Arduino per ricevere messaggi da cloud a dispositivo][receive-cloud-to-device-messages].</span><span class="sxs-lookup"><span data-stu-id="7e3e0-111">You must have successfully completed [Run a sample application on your Arduino board to receive cloud to device messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-to-mainc-and-gulpfilejs"></a><span data-ttu-id="7e3e0-112">Aggiungere funzioni a main.c e gulpfile.js</span><span class="sxs-lookup"><span data-stu-id="7e3e0-112">Add functions to main.c and gulpfile.js</span></span>
1. <span data-ttu-id="7e3e0-113">Aprire l'applicazione di esempio in Visual Studio Code usando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="7e3e0-113">Open the sample application in Visual Studio code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="7e3e0-114">Aprire il file `app.ino` e aggiungere le funzioni seguenti dopo la funzione blinkLED():</span><span class="sxs-lookup"><span data-stu-id="7e3e0-114">Open the `app.ino` file, and then add the following functions after blinkLED() function:</span></span>

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
3. <span data-ttu-id="7e3e0-116">Aggiungere le condizioni seguenti prima del blocco `else if` della funzione `receiveMessageCallback`:</span><span class="sxs-lookup"><span data-stu-id="7e3e0-116">Add the following conditions before the `else if` block of the `receiveMessageCallback` function:</span></span>

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

   <span data-ttu-id="7e3e0-117">A questo punto è stata configurata l'applicazione di esempio per rispondere a più istruzioni tramite messaggi.</span><span class="sxs-lookup"><span data-stu-id="7e3e0-117">Now you’ve configured the sample application to respond to more instructions through messages.</span></span> <span data-ttu-id="7e3e0-118">L'istruzione "on" accende il LED, mentre l'istruzione "off" lo spegne.</span><span class="sxs-lookup"><span data-stu-id="7e3e0-118">The "on" instruction turns on the LED, and the "off" instruction turns off the LED.</span></span>
4. <span data-ttu-id="7e3e0-119">Aprire il file gulpfile.js e quindi aggiungere una nuova funzione prima della funzione `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="7e3e0-119">Open the gulpfile.js file, and then add a new function before the function `sendMessage`:</span></span>

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
5. <span data-ttu-id="7e3e0-121">Nella funzione `sendMessage` sostituire la riga `var message = buildMessage(sentMessageCount);` con la nuova riga illustrata nel frammento seguente:</span><span class="sxs-lookup"><span data-stu-id="7e3e0-121">In the `sendMessage` function, replace the line `var message = buildMessage(sentMessageCount);` with the new line shown in the following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="7e3e0-122">Salvare tutte le modifiche.</span><span class="sxs-lookup"><span data-stu-id="7e3e0-122">Save all the changes.</span></span>

### <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="7e3e0-123">Distribuire ed eseguire l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="7e3e0-123">Deploy and run the sample application</span></span>
<span data-ttu-id="7e3e0-124">Distribuire ed eseguire l'applicazione di esempio nella scheda Arduino usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="7e3e0-124">Deploy and run the sample application on your Arduino board by running the following command:</span></span>

```bash
gulp run
# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="7e3e0-125">Il LED deve rimanere acceso per due secondi e quindi spento per altri due secondi.</span><span class="sxs-lookup"><span data-stu-id="7e3e0-125">You should see the LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="7e3e0-126">L'ultimo messaggio "stop" arresta l'esecuzione dell'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="7e3e0-126">The last "stop" message stops the sample application from running.</span></span>

![accensione e spegnimento][on-and-off]

<span data-ttu-id="7e3e0-128">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="7e3e0-128">Congratulations!</span></span> <span data-ttu-id="7e3e0-129">I messaggi inviati dall'hub IoT alla scheda Arduino sono stati personalizzati.</span><span class="sxs-lookup"><span data-stu-id="7e3e0-129">You’ve successfully customized the messages that are sent to your Arduino board from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="7e3e0-130">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="7e3e0-130">Summary</span></span>
<span data-ttu-id="7e3e0-131">Questa sezione facoltativa illustra come personalizzare i messaggi per consentire all'applicazione di esempio di controllare il comportamento di accensione e spegnimento del LED in modo diverso.</span><span class="sxs-lookup"><span data-stu-id="7e3e0-131">This optional section demonstrates how to customize messages so that the sample application can control the on and off behavior of the LED in a different way.</span></span>

<!-- Images and links -->

[receive-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md
[app-ino-file]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_app_ino.png
[gulp-file-js]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_gulpfile_js.png
[on-and-off]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_on_and_off_arduino.png