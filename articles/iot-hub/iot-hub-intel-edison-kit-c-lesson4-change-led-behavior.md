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
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a><span data-ttu-id="9511a-104">Modificare hello e disattivare il comportamento di hello LED</span><span class="sxs-lookup"><span data-stu-id="9511a-104">Change hello on and off behavior of hello LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="9511a-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="9511a-105">What you will do</span></span>
<span data-ttu-id="9511a-106">Personalizzare hello toochange di messaggi hello LED di attivare e disattivare il comportamento.</span><span class="sxs-lookup"><span data-stu-id="9511a-106">Customize hello messages toochange hello LED’s on and off behavior.</span></span> <span data-ttu-id="9511a-107">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="9511a-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="9511a-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="9511a-108">What you will learn</span></span>
<span data-ttu-id="9511a-109">Utilizzare hello toochange funzioni aggiuntive LED di attivare e disattivare il comportamento.</span><span class="sxs-lookup"><span data-stu-id="9511a-109">Use additional functions toochange hello LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9511a-110">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="9511a-110">What you need</span></span>
<span data-ttu-id="9511a-111">È necessario avere completato correttamente [eseguire un'applicazione di esempio nel cloud tooreceive Edison Intel messaggi toodevice][receive-cloud-to-device-messages].</span><span class="sxs-lookup"><span data-stu-id="9511a-111">You must have successfully completed [Run a sample application on Intel Edison tooreceive cloud toodevice messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-toomainc-and-gulpfilejs"></a><span data-ttu-id="9511a-112">Aggiungere gulpfile.js e toomain.c di funzioni</span><span class="sxs-lookup"><span data-stu-id="9511a-112">Add functions toomain.c and gulpfile.js</span></span>
1. <span data-ttu-id="9511a-113">Aprire l'applicazione di esempio hello nel codice di Visual Studio eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="9511a-113">Open hello sample application in Visual Studio code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="9511a-114">Aprire hello `main.c` file e quindi aggiungere hello seguenti funzioni dopo la funzione blinkLED():</span><span class="sxs-lookup"><span data-stu-id="9511a-114">Open hello `main.c` file, and then add hello following functions after blinkLED() function:</span></span>

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

3. <span data-ttu-id="9511a-116">Aggiungere hello seguenti condizioni prima di hello `else if` blocco di hello `receiveMessageCallback` funzione:</span><span class="sxs-lookup"><span data-stu-id="9511a-116">Add hello following conditions before hello `else if` block of hello `receiveMessageCallback` function:</span></span>

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

   <span data-ttu-id="9511a-117">Ora è configurata hello applicazione toorespond toomore le istruzioni di esempio tramite i messaggi.</span><span class="sxs-lookup"><span data-stu-id="9511a-117">Now you’ve configured hello sample application toorespond toomore instructions through messages.</span></span> <span data-ttu-id="9511a-118">Hello "on" istruzione attiva hello LED e hello "off" istruzione Disattiva hello LED.</span><span class="sxs-lookup"><span data-stu-id="9511a-118">hello "on" instruction turns on hello LED, and hello "off" instruction turns off hello LED.</span></span>
4. <span data-ttu-id="9511a-119">Aprire il file gulpfile.js hello e quindi aggiungere una nuova funzione prima della funzione hello `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="9511a-119">Open hello gulpfile.js file, and then add a new function before hello function `sendMessage`:</span></span>

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
5. <span data-ttu-id="9511a-121">In hello `sendMessage` di funzione, sostituire la riga hello `var message = buildMessage(sentMessageCount);` con una nuova riga hello mostrata nel seguente frammento di codice hello:</span><span class="sxs-lookup"><span data-stu-id="9511a-121">In hello `sendMessage` function, replace hello line `var message = buildMessage(sentMessageCount);` with hello new line shown in hello following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="9511a-122">Salvare tutte le modifiche di hello.</span><span class="sxs-lookup"><span data-stu-id="9511a-122">Save all hello changes.</span></span>

### <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="9511a-123">Distribuire ed eseguire l'applicazione di esempio hello</span><span class="sxs-lookup"><span data-stu-id="9511a-123">Deploy and run hello sample application</span></span>
<span data-ttu-id="9511a-124">Distribuire ed eseguire l'applicazione di esempio hello Edison eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9511a-124">Deploy and run hello sample application on Edison by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="9511a-125">Si noterà accendere hello LED per due secondi e quindi disattivare per un altro due secondi.</span><span class="sxs-lookup"><span data-stu-id="9511a-125">You should see hello LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="9511a-126">il messaggio "stop" ultimo Hello arresta l'applicazione di esempio hello esecuzione.</span><span class="sxs-lookup"><span data-stu-id="9511a-126">hello last "stop" message stops hello sample application from running.</span></span>

![accensione e spegnimento][on-and-off]

<span data-ttu-id="9511a-128">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="9511a-128">Congratulations!</span></span> <span data-ttu-id="9511a-129">È stato personalizzato correttamente i messaggi hello inviati tooEdison dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9511a-129">You’ve successfully customized hello messages that are sent tooEdison from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="9511a-130">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="9511a-130">Summary</span></span>
<span data-ttu-id="9511a-131">Questa sezione facoltativa viene illustrata la modalità toocustomize dei messaggi in modo che l'applicazione di esempio hello può controllare hello e disattivare il comportamento di hello LED in modo diverso.</span><span class="sxs-lookup"><span data-stu-id="9511a-131">This optional section demonstrates how toocustomize messages so that hello sample application can control hello on and off behavior of hello LED in a different way.</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-c-lesson4-send-cloud-to-device-messages.md
[gulpfile]: media/iot-hub-intel-edison-lessons/lesson4/updated_gulpfile_c.png
[on-and-off]: media/iot-hub-intel-edison-lessons/lesson4/gulp_on_and_off_c.png
