---
title: 'Connect Raspberry PI (C) tooAzure IoT - lezione 4: Cloud a dispositivo | Documenti Microsoft'
description: "Un'applicazione di esempio viene eseguita nel dispositivo Pi e monitora i messaggi in ingresso dall'hub IoT. Una nuova attività gulp invia messaggi tooPi da hello di tooblink l'hub IoT LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: cloud toodevice, messaggio dal cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: fcbc0dd0-cae3-47b0-8e58-240e4f406f75
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5596bf3a83c21f2bd54b2f83e2a8fdad7a608b94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="a7014-105">Eseguire un tooreceive di applicazione di esempio i messaggi da cloud a dispositivo</span><span class="sxs-lookup"><span data-stu-id="a7014-105">Run a sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="a7014-106">Questo articolo illustra come distribuire un'applicazione di esempio nel dispositivo Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="a7014-106">In this article, you deploy a sample application on Raspberry Pi 3.</span></span> <span data-ttu-id="a7014-107">applicazione di esempio Hello controlla i messaggi in ingresso dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a7014-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="a7014-108">Inoltre si esegue un'attività gulp su tooPi di messaggi toosend il computer dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a7014-108">You also run a gulp task on your computer toosend messages tooPi from your IoT hub.</span></span> <span data-ttu-id="a7014-109">Quando l'applicazione di esempio hello riceve messaggi hello, lampeggia hello LED.</span><span class="sxs-lookup"><span data-stu-id="a7014-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="a7014-110">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="a7014-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="a7014-111">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="a7014-111">What you will do</span></span>
* <span data-ttu-id="a7014-112">Connettere l'hub IoT hello esempio applicazione tooyour.</span><span class="sxs-lookup"><span data-stu-id="a7014-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="a7014-113">Distribuire ed eseguire l'applicazione di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="a7014-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="a7014-114">Invio di messaggi dal hello di IoT hub tooPi tooblink LED.</span><span class="sxs-lookup"><span data-stu-id="a7014-114">Send messages from your IoT hub tooPi tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a7014-115">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="a7014-115">What you will learn</span></span>
<span data-ttu-id="a7014-116">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="a7014-116">In this article, you will learn:</span></span>
* <span data-ttu-id="a7014-117">La modalità in ingresso toomonitor dei messaggi dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a7014-117">How toomonitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="a7014-118">La modalità toosend cloud a dispositivo dei messaggi dal tooPi hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a7014-118">How toosend cloud-to-device messages from your IoT hub tooPi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a7014-119">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="a7014-119">What you need</span></span>
* <span data-ttu-id="a7014-120">Raspberry Pi 3, impostato per l'uso.</span><span class="sxs-lookup"><span data-stu-id="a7014-120">Raspberry Pi 3, set up for use.</span></span> <span data-ttu-id="a7014-121">toolearn tooset di pi greco, vedere [configurare il dispositivo](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md).</span><span class="sxs-lookup"><span data-stu-id="a7014-121">toolearn how tooset up Pi, see [Configure your device](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md).</span></span>
* <span data-ttu-id="a7014-122">Un hub IoT creato nella propria sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a7014-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="a7014-123">toolearn come toocreate l'hub IoT, vedere [creare l'hub IoT e registrare Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="a7014-123">toolearn how toocreate your IoT hub, see [Create your IoT hub and register Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="a7014-124">Collegare hello esempio applicazione tooyour IoT hub</span><span class="sxs-lookup"><span data-stu-id="a7014-124">Connect hello sample application tooyour IoT hub</span></span>
1. <span data-ttu-id="a7014-125">Assicurarsi che si è nella cartella repository hello `iot-hub-c-raspberrypi-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="a7014-125">Make sure that you're in hello repo folder `iot-hub-c-raspberrypi-getting-started`.</span></span> <span data-ttu-id="a7014-126">Aprire l'applicazione di esempio hello in Visual Studio Code eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="a7014-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="a7014-127">Hello preavviso `app.c` file hello `app` sottocartella.</span><span class="sxs-lookup"><span data-stu-id="a7014-127">Notice hello `app.c` file in hello `app` subfolder.</span></span> <span data-ttu-id="a7014-128">Hello `app.c` è hello i file di origine della chiave che contiene i messaggi in ingresso hello codice toomonitor dall'hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="a7014-128">hello `app.c` file is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="a7014-129">Hello `blinkLED` funzione lampeggia hello LED.</span><span class="sxs-lookup"><span data-stu-id="a7014-129">hello `blinkLED` function blinks hello LED.</span></span>

   ![Struttura repository nell'applicazione di esempio hello](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure_c.png)
2. <span data-ttu-id="a7014-131">Inizializzare i file di configurazione hello eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="a7014-131">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="a7014-132">Se è stato completato i passaggi di hello in [creare un account di archiviazione e l'app Azure funzione](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) su questo computer, tutte le configurazioni di hello vengono ereditate, pertanto è possibile ignorare toostep toohello attività di distribuzione e l'esecuzione dell'applicazione di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="a7014-132">If you completed hello steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) on this computer, all hello configurations are inherited, so you can skip toostep toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="a7014-133">Se è stato completato i passaggi di hello in [creare un account di archiviazione e l'app Azure funzione](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) in un computer diverso, è necessario segnaposto hello tooreplace hello `config-raspberrypi.json` file.</span><span class="sxs-lookup"><span data-stu-id="a7014-133">If you completed hello steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) on a different computer, you need tooreplace hello placeholders in hello `config-raspberrypi.json` file.</span></span> <span data-ttu-id="a7014-134">Hello `config-raspberrypi.json` file si trova nella sottocartella hello della cartella principale.</span><span class="sxs-lookup"><span data-stu-id="a7014-134">hello `config-raspberrypi.json` file is in hello subfolder of your home folder.</span></span>

   ![Contenuto del file di configurazione raspberrypi.json hello](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* <span data-ttu-id="a7014-136">Sostituire **[nome host di dispositivo o indirizzo IP]** con dell'installazione guidata piattaforma IP indirizzo o il nome host che si ottiene eseguendo hello `devdisco list --eth` comando.</span><span class="sxs-lookup"><span data-stu-id="a7014-136">Replace **[device hostname or IP address]** with Pi’s IP address or host name that you get by running hello `devdisco list --eth` command.</span></span>
* <span data-ttu-id="a7014-137">Sostituire **[stringa di connessione dispositivo IoT]** con stringa di connessione hello dispositivo che si ottiene eseguendo hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` comando.</span><span class="sxs-lookup"><span data-stu-id="a7014-137">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` command.</span></span>
* <span data-ttu-id="a7014-138">Sostituire **[stringa di connessione hub IoT]** con stringa di connessione hub IoT che si ottiene eseguendo hello hello `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` comando.</span><span class="sxs-lookup"><span data-stu-id="a7014-138">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` command.</span></span>

> [!NOTE]
> <span data-ttu-id="a7014-139">Se non è stato fatto nella lezione 1, eseguire anche il comando **gulp install-tools**.</span><span class="sxs-lookup"><span data-stu-id="a7014-139">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="a7014-140">Distribuire ed eseguire l'applicazione di esempio hello</span><span class="sxs-lookup"><span data-stu-id="a7014-140">Deploy and run hello sample application</span></span>
<span data-ttu-id="a7014-141">Distribuire ed eseguire l'applicazione di esempio hello Pi eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="a7014-141">Deploy and run hello sample application on Pi by running hello following commands:</span></span>

```
gulp deploy && gulp run
```

<span data-ttu-id="a7014-142">esecuzione del comando gulp Hello hello prima attività di strumenti di installazione.</span><span class="sxs-lookup"><span data-stu-id="a7014-142">hello gulp command runs hello install-tools task first.</span></span> <span data-ttu-id="a7014-143">Distribuisce quindi tooPi applicazione di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="a7014-143">Then it deploys hello sample application tooPi.</span></span> <span data-ttu-id="a7014-144">Infine, viene eseguita un'applicazione hello Pi e un'attività separata nell'host computer toosend 20 blink messaggi tooPi dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a7014-144">Finally, it runs hello application on Pi and a separate task on your host computer toosend 20 blink messages tooPi from your IoT hub.</span></span>

<span data-ttu-id="a7014-145">Quando si esegue l'applicazione di esempio hello, avvia l'ascolto toomessages dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a7014-145">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="a7014-146">Nel frattempo, attività gulp hello invia messaggi di "blink" diversi dai tooPi hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a7014-146">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooPi.</span></span> <span data-ttu-id="a7014-147">Per ogni messaggio blink che riceve Pi, l'applicazione di esempio hello chiama hello `blinkLED` hello tooblink funzione LED.</span><span class="sxs-lookup"><span data-stu-id="a7014-147">For each blink message that Pi receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="a7014-148">Dovrebbe essere blink LED hello ogni due secondi come hello gulp attività inviati 20 messaggi dal tooPi hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a7014-148">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooPi.</span></span> <span data-ttu-id="a7014-149">Hello ultimo uno è un messaggio "stop" che interrompe l'esecuzione di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a7014-149">hello last one is a "stop" message that stops hello application from running.</span></span>

![Applicazione di esempio con comando gulp e messaggi di lampeggiamento](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink_c.png)

## <a name="summary"></a><span data-ttu-id="a7014-151">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="a7014-151">Summary</span></span>
<span data-ttu-id="a7014-152">I messaggi inviati correttamente dal hello di IoT hub tooPi tooblink LED.</span><span class="sxs-lookup"><span data-stu-id="a7014-152">You’ve successfully sent messages from your IoT hub tooPi tooblink hello LED.</span></span> <span data-ttu-id="a7014-153">attività successiva Hello è facoltativo: modificare hello e disattivare il comportamento di hello LED.</span><span class="sxs-lookup"><span data-stu-id="a7014-153">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7014-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a7014-154">Next steps</span></span>
[<span data-ttu-id="a7014-155">Modificare hello e disattivare il comportamento di hello LED</span><span class="sxs-lookup"><span data-stu-id="a7014-155">Change hello on and off behavior of hello LED</span></span>](iot-hub-raspberry-pi-kit-c-lesson4-change-led-behavior.md)
