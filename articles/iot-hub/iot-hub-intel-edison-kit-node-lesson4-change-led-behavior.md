---
title: 'Connettere Intel Edison (Node) ad Azure IoT: lezione 4: Far lampeggiare il LED | Documentazione Microsoft'
description: Personalizzare i messaggi per modificare il comportamento di accensione e spegnimento del LED.
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
ms.openlocfilehash: fa99050dad62534e2825e93f1170d2f3ecf5a3ba
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-on-and-off-behavior-of-the-led"></a><span data-ttu-id="2d3b7-104">Modificare il comportamento di accensione e spegnimento del LED</span><span class="sxs-lookup"><span data-stu-id="2d3b7-104">Change the on and off behavior of the LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="2d3b7-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="2d3b7-105">What you will do</span></span>
<span data-ttu-id="2d3b7-106">Personalizzare i messaggi per modificare il comportamento di accensione e spegnimento del LED.</span><span class="sxs-lookup"><span data-stu-id="2d3b7-106">Customize the messages to change the LED’s on and off behavior.</span></span> <span data-ttu-id="2d3b7-107">In caso di problemi, cercare le soluzioni nella [pagina sulla risoluzione dei problemi][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="2d3b7-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="2d3b7-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="2d3b7-108">What you will learn</span></span>
<span data-ttu-id="2d3b7-109">Usare funzioni aggiuntive per modificare il comportamento di accensione e spegnimento del LED.</span><span class="sxs-lookup"><span data-stu-id="2d3b7-109">Use additional functions to change the LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2d3b7-110">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="2d3b7-110">What you need</span></span>
<span data-ttu-id="2d3b7-111">È necessario aver completato la sezione [Eseguire l'applicazione di esempio in Intel Edison per ricevere messaggi da cloud a dispositivo][receive-cloud-to-device-messages].</span><span class="sxs-lookup"><span data-stu-id="2d3b7-111">You must have successfully completed [Run a sample application on Intel Edison to receive cloud to device messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-to-appjs-and-gulpfilejs"></a><span data-ttu-id="2d3b7-112">Aggiungere funzioni ad app.js e gulpfile.js</span><span class="sxs-lookup"><span data-stu-id="2d3b7-112">Add functions to app.js and gulpfile.js</span></span>
1. <span data-ttu-id="2d3b7-113">Aprire l'applicazione di esempio in Visual Studio Code usando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2d3b7-113">Open the sample application in Visual Studio code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="2d3b7-114">Aprire il file `app.js` e aggiungere le funzioni seguenti dopo la funzione blinkLED():</span><span class="sxs-lookup"><span data-stu-id="2d3b7-114">Open the `app.js` file, and then add the following functions after blinkLED() function:</span></span>

   ```javascript
   function turnOnLED() {
     myLed.write(1);
   }

   function turnOffLED() {
     myLed.write(0);
   }
   ```

   ![File app.js con funzioni aggiunte](media/iot-hub-intel-edison-lessons/lesson4/updated_app_node.png)
3. <span data-ttu-id="2d3b7-116">Aggiungere le condizioni seguenti prima di 'blink' nel blocco switch-case della funzione `receiveMessageCallback`:</span><span class="sxs-lookup"><span data-stu-id="2d3b7-116">Add the following conditions before the 'blink' case in the switch-case block of the `receiveMessageCallback` function:</span></span>

   ```javascript
   case 'on':
     turnOnLED();
     break;
   case 'off':
     turnOffLED();
     break;
   ```

   <span data-ttu-id="2d3b7-117">A questo punto è stata configurata l'applicazione di esempio per rispondere a più istruzioni tramite messaggi.</span><span class="sxs-lookup"><span data-stu-id="2d3b7-117">Now you’ve configured the sample application to respond to more instructions through messages.</span></span> <span data-ttu-id="2d3b7-118">L'istruzione "on" accende il LED, mentre l'istruzione "off" lo spegne.</span><span class="sxs-lookup"><span data-stu-id="2d3b7-118">The "on" instruction turns on the LED, and the "off" instruction turns off the LED.</span></span>
4. <span data-ttu-id="2d3b7-119">Aprire il file gulpfile.js e quindi aggiungere una nuova funzione prima della funzione `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="2d3b7-119">Open the gulpfile.js file, and then add a new function before the function `sendMessage`:</span></span>

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
5. <span data-ttu-id="2d3b7-121">Nella funzione `sendMessage` sostituire la riga `var message = buildMessage(sentMessageCount);` con la nuova riga illustrata nel frammento seguente:</span><span class="sxs-lookup"><span data-stu-id="2d3b7-121">In the `sendMessage` function, replace the line `var message = buildMessage(sentMessageCount);` with the new line shown in the following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="2d3b7-122">Salvare tutte le modifiche.</span><span class="sxs-lookup"><span data-stu-id="2d3b7-122">Save all the changes.</span></span>

### <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="2d3b7-123">Distribuire ed eseguire l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="2d3b7-123">Deploy and run the sample application</span></span>
<span data-ttu-id="2d3b7-124">Distribuire ed eseguire l'applicazione di esempio in Edison eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="2d3b7-124">Deploy and run the sample application on Edison by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="2d3b7-125">Il LED deve rimanere acceso per due secondi e quindi spento per altri due secondi.</span><span class="sxs-lookup"><span data-stu-id="2d3b7-125">You should see the LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="2d3b7-126">L'ultimo messaggio "stop" arresta l'esecuzione dell'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="2d3b7-126">The last "stop" message stops the sample application from running.</span></span>

![accensione e spegnimento][on-and-off]

<span data-ttu-id="2d3b7-128">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="2d3b7-128">Congratulations!</span></span> <span data-ttu-id="2d3b7-129">I messaggi inviati dall'hub IoT a Edison sono stati personalizzati.</span><span class="sxs-lookup"><span data-stu-id="2d3b7-129">You’ve successfully customized the messages that are sent to Edison from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="2d3b7-130">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="2d3b7-130">Summary</span></span>
<span data-ttu-id="2d3b7-131">Questa sezione facoltativa illustra come personalizzare i messaggi per consentire all'applicazione di esempio di controllare il comportamento di accensione e spegnimento del LED in modo diverso.</span><span class="sxs-lookup"><span data-stu-id="2d3b7-131">This optional section demonstrates how to customize messages so that the sample application can control the on and off behavior of the LED in a different way.</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-node-lesson4-send-cloud-to-device-messages.md
[gulpfile]: media/iot-hub-intel-edison-lessons/lesson4/updated_gulpfile_node.png
[on-and-off]: media/iot-hub-intel-edison-lessons/lesson4/gulp_on_and_off_node.png
