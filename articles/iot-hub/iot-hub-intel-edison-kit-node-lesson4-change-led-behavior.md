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
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a><span data-ttu-id="f9925-104">Modificare hello e disattivare il comportamento di hello LED</span><span class="sxs-lookup"><span data-stu-id="f9925-104">Change hello on and off behavior of hello LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="f9925-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="f9925-105">What you will do</span></span>
<span data-ttu-id="f9925-106">Personalizzare hello toochange di messaggi hello LED di attivare e disattivare il comportamento.</span><span class="sxs-lookup"><span data-stu-id="f9925-106">Customize hello messages toochange hello LED’s on and off behavior.</span></span> <span data-ttu-id="f9925-107">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="f9925-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="f9925-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="f9925-108">What you will learn</span></span>
<span data-ttu-id="f9925-109">Utilizzare hello toochange funzioni aggiuntive LED di attivare e disattivare il comportamento.</span><span class="sxs-lookup"><span data-stu-id="f9925-109">Use additional functions toochange hello LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f9925-110">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="f9925-110">What you need</span></span>
<span data-ttu-id="f9925-111">È necessario avere completato correttamente [eseguire un'applicazione di esempio nel cloud tooreceive Edison Intel messaggi toodevice][receive-cloud-to-device-messages].</span><span class="sxs-lookup"><span data-stu-id="f9925-111">You must have successfully completed [Run a sample application on Intel Edison tooreceive cloud toodevice messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-tooappjs-and-gulpfilejs"></a><span data-ttu-id="f9925-112">Aggiungere gulpfile.js e tooapp.js di funzioni</span><span class="sxs-lookup"><span data-stu-id="f9925-112">Add functions tooapp.js and gulpfile.js</span></span>
1. <span data-ttu-id="f9925-113">Aprire l'applicazione di esempio hello nel codice di Visual Studio eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="f9925-113">Open hello sample application in Visual Studio code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="f9925-114">Aprire hello `app.js` file e quindi aggiungere hello seguenti funzioni dopo la funzione blinkLED():</span><span class="sxs-lookup"><span data-stu-id="f9925-114">Open hello `app.js` file, and then add hello following functions after blinkLED() function:</span></span>

   ```javascript
   function turnOnLED() {
     myLed.write(1);
   }

   function turnOffLED() {
     myLed.write(0);
   }
   ```

   ![File app.js con funzioni aggiunte](media/iot-hub-intel-edison-lessons/lesson4/updated_app_node.png)
3. <span data-ttu-id="f9925-116">Aggiungere hello le condizioni seguenti prima di hello 'blink' case nel blocco switch case hello di hello `receiveMessageCallback` funzione:</span><span class="sxs-lookup"><span data-stu-id="f9925-116">Add hello following conditions before hello 'blink' case in hello switch-case block of hello `receiveMessageCallback` function:</span></span>

   ```javascript
   case 'on':
     turnOnLED();
     break;
   case 'off':
     turnOffLED();
     break;
   ```

   <span data-ttu-id="f9925-117">Ora è configurata hello applicazione toorespond toomore le istruzioni di esempio tramite i messaggi.</span><span class="sxs-lookup"><span data-stu-id="f9925-117">Now you’ve configured hello sample application toorespond toomore instructions through messages.</span></span> <span data-ttu-id="f9925-118">Hello "on" istruzione attiva hello LED e hello "off" istruzione Disattiva hello LED.</span><span class="sxs-lookup"><span data-stu-id="f9925-118">hello "on" instruction turns on hello LED, and hello "off" instruction turns off hello LED.</span></span>
4. <span data-ttu-id="f9925-119">Aprire il file gulpfile.js hello e quindi aggiungere una nuova funzione prima della funzione hello `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="f9925-119">Open hello gulpfile.js file, and then add a new function before hello function `sendMessage`:</span></span>

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
5. <span data-ttu-id="f9925-121">In hello `sendMessage` di funzione, sostituire la riga hello `var message = buildMessage(sentMessageCount);` con una nuova riga hello mostrata nel seguente frammento di codice hello:</span><span class="sxs-lookup"><span data-stu-id="f9925-121">In hello `sendMessage` function, replace hello line `var message = buildMessage(sentMessageCount);` with hello new line shown in hello following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="f9925-122">Salvare tutte le modifiche di hello.</span><span class="sxs-lookup"><span data-stu-id="f9925-122">Save all hello changes.</span></span>

### <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="f9925-123">Distribuire ed eseguire l'applicazione di esempio hello</span><span class="sxs-lookup"><span data-stu-id="f9925-123">Deploy and run hello sample application</span></span>
<span data-ttu-id="f9925-124">Distribuire ed eseguire l'applicazione di esempio hello Edison eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f9925-124">Deploy and run hello sample application on Edison by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="f9925-125">Si noterà accendere hello LED per due secondi e quindi disattivare per un altro due secondi.</span><span class="sxs-lookup"><span data-stu-id="f9925-125">You should see hello LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="f9925-126">il messaggio "stop" ultimo Hello arresta l'applicazione di esempio hello esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f9925-126">hello last "stop" message stops hello sample application from running.</span></span>

![accensione e spegnimento][on-and-off]

<span data-ttu-id="f9925-128">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="f9925-128">Congratulations!</span></span> <span data-ttu-id="f9925-129">È stato personalizzato correttamente i messaggi hello inviati tooEdison dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="f9925-129">You’ve successfully customized hello messages that are sent tooEdison from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="f9925-130">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="f9925-130">Summary</span></span>
<span data-ttu-id="f9925-131">Questa sezione facoltativa viene illustrata la modalità toocustomize dei messaggi in modo che l'applicazione di esempio hello può controllare hello e disattivare il comportamento di hello LED in modo diverso.</span><span class="sxs-lookup"><span data-stu-id="f9925-131">This optional section demonstrates how toocustomize messages so that hello sample application can control hello on and off behavior of hello LED in a different way.</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-node-lesson4-send-cloud-to-device-messages.md
[gulpfile]: media/iot-hub-intel-edison-lessons/lesson4/updated_gulpfile_node.png
[on-and-off]: media/iot-hub-intel-edison-lessons/lesson4/gulp_on_and_off_node.png
