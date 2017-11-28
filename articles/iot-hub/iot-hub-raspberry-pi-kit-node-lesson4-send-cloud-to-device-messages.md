---
featureFlags: usabilla
title: 'Connettersi Raspberry Pi (nodo) tooAzure IoT - lezione 4: Cloud a dispositivo | Documenti Microsoft'
description: "applicazione di esempio Hello viene eseguita l'installazione guidata piattaforma e controlla i messaggi in ingresso dall'hub IoT. Una nuova attività gulp invia messaggi tooPi da hello di tooblink l'hub IoT LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: cloud toodevice, messaggio dal cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6ae6539e-1163-4490-8d72-fdf7803e3054
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d69ded4e30c27378481ab2a4fb9c5b73be7bd44e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="5042e-105">Eseguire i messaggi hello esempio applicazione tooreceive cloud a dispositivo</span><span class="sxs-lookup"><span data-stu-id="5042e-105">Run hello sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="5042e-106">Questo articolo illustra come distribuire un'applicazione di esempio nel dispositivo Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="5042e-106">In this article, you deploy a sample application on Raspberry Pi 3.</span></span> <span data-ttu-id="5042e-107">applicazione di esempio Hello controlla i messaggi in ingresso dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5042e-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="5042e-108">Inoltre si esegue un'attività gulp su tooPi di messaggi toosend il computer dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5042e-108">You also run a gulp task on your computer toosend messages tooPi from your IoT hub.</span></span> <span data-ttu-id="5042e-109">Quando l'applicazione di esempio hello riceve messaggi hello, lampeggia hello LED.</span><span class="sxs-lookup"><span data-stu-id="5042e-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="5042e-110">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="5042e-110">If you have any problems, seek solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="5042e-111">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="5042e-111">What you will do</span></span>
* <span data-ttu-id="5042e-112">Connettere l'hub IoT hello esempio applicazione tooyour.</span><span class="sxs-lookup"><span data-stu-id="5042e-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="5042e-113">Distribuire ed eseguire l'applicazione di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="5042e-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="5042e-114">Invio di messaggi dal hello di IoT hub tooPi tooblink LED.</span><span class="sxs-lookup"><span data-stu-id="5042e-114">Send messages from your IoT hub tooPi tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5042e-115">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="5042e-115">What you will learn</span></span>
<span data-ttu-id="5042e-116">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="5042e-116">In this article, you will learn:</span></span>
* <span data-ttu-id="5042e-117">Come i messaggi in ingresso toomonitor dall'hub IoT</span><span class="sxs-lookup"><span data-stu-id="5042e-117">How toomonitor incoming messages from your IoT hub</span></span>
* <span data-ttu-id="5042e-118">La modalità toosend cloud a dispositivo dei messaggi dal tooPi hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5042e-118">How toosend cloud-to-device messages from your IoT hub tooPi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5042e-119">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="5042e-119">What you need</span></span>
* <span data-ttu-id="5042e-120">Raspberry Pi 3, impostato per l'uso.</span><span class="sxs-lookup"><span data-stu-id="5042e-120">Raspberry Pi 3, set up for use.</span></span> <span data-ttu-id="5042e-121">toolearn tooset di pi greco, vedere [configurare il dispositivo](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md).</span><span class="sxs-lookup"><span data-stu-id="5042e-121">toolearn how tooset up Pi, see [Configure your device](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md).</span></span>
* <span data-ttu-id="5042e-122">Un hub IoT creato nella propria sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5042e-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="5042e-123">toolearn come toocreate l'hub IoT, vedere [creare l'hub IoT e registrare Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="5042e-123">toolearn how toocreate your IoT hub, see [Create your IoT hub and register Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="5042e-124">Collegare hello esempio applicazione tooyour IoT hub</span><span class="sxs-lookup"><span data-stu-id="5042e-124">Connect hello sample application tooyour IoT hub</span></span>
1. <span data-ttu-id="5042e-125">Assicurarsi che si è nella cartella repository hello `iot-hub-node-raspberrypi-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="5042e-125">Make sure that you're in hello repo folder `iot-hub-node-raspberrypi-getting-started`.</span></span> <span data-ttu-id="5042e-126">Aprire l'applicazione di esempio hello in Visual Studio Code eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="5042e-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>
   
   ```bash
   cd Lesson4
   code .
   ```
   
   <span data-ttu-id="5042e-127">Hello preavviso `app.js` file hello `app` sottocartella.</span><span class="sxs-lookup"><span data-stu-id="5042e-127">Notice hello `app.js` file in hello `app` subfolder.</span></span> <span data-ttu-id="5042e-128">Hello `app.js` è hello i file di origine della chiave che contiene i messaggi in ingresso hello codice toomonitor dall'hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="5042e-128">hello `app.js` file is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="5042e-129">Hello `blinkLED` funzione lampeggia hello LED.</span><span class="sxs-lookup"><span data-stu-id="5042e-129">hello `blinkLED` function blinks hello LED.</span></span>
   
   ![Struttura repository nell'applicazione di esempio hello](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure.png)
2. <span data-ttu-id="5042e-131">Inizializzare i file di configurazione hello usando hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="5042e-131">Initialize hello configuration file by using hello following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```
   
   <span data-ttu-id="5042e-132">Se è stato completato i passaggi di hello in [creare un account di archiviazione e l'app Azure funzione](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) su questo computer, tutte le configurazioni di hello vengono ereditate, pertanto è possibile ignorare toohello attività di distribuzione e l'esecuzione dell'applicazione di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="5042e-132">If you completed hello steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) on this computer, all hello configurations are inherited, so you can skip toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="5042e-133">Se è stato completato i passaggi di hello in [creare un account di archiviazione e l'app Azure funzione](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) in un computer diverso, è necessario segnaposto hello tooreplace hello `config-raspberrypi.json` file.</span><span class="sxs-lookup"><span data-stu-id="5042e-133">If you completed hello steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) on a different computer, you need tooreplace hello placeholders in hello `config-raspberrypi.json` file.</span></span> <span data-ttu-id="5042e-134">Hello `config-raspberrypi.json` file si trova nella sottocartella hello della cartella principale.</span><span class="sxs-lookup"><span data-stu-id="5042e-134">hello `config-raspberrypi.json` file is in hello subfolder of your home folder.</span></span>
   
   ![Contenuto del file di configurazione raspberrypi.json hello](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* <span data-ttu-id="5042e-136">Sostituire **[nome host di dispositivo o indirizzo IP]** con indirizzo IP hello hello o al nome host che si ottiene eseguendo hello `devdisco list --eth` comando.</span><span class="sxs-lookup"><span data-stu-id="5042e-136">Replace **[device hostname or IP address]** with hello IP address of Pi or hello host name that you get by running hello `devdisco list --eth` command.</span></span>
* <span data-ttu-id="5042e-137">Sostituire **[stringa di connessione dispositivo IoT]** con stringa di connessione hello dispositivo che si ottiene eseguendo hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` comando.</span><span class="sxs-lookup"><span data-stu-id="5042e-137">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` command.</span></span>
* <span data-ttu-id="5042e-138">Sostituire **[stringa di connessione hub IoT]** con stringa di connessione hub IoT che si ottiene eseguendo hello hello `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` comando.</span><span class="sxs-lookup"><span data-stu-id="5042e-138">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` command.</span></span>

> [!NOTE]
> <span data-ttu-id="5042e-139">Se non è stato fatto nella lezione 1, eseguire anche il comando **gulp install-tools**.</span><span class="sxs-lookup"><span data-stu-id="5042e-139">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="5042e-140">Distribuire ed eseguire l'applicazione di esempio hello</span><span class="sxs-lookup"><span data-stu-id="5042e-140">Deploy and run hello sample application</span></span>
<span data-ttu-id="5042e-141">Distribuire ed eseguire l'applicazione di esempio hello Pi eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5042e-141">Deploy and run hello sample application on Pi by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="5042e-142">comando Hello distribuisce tooPi applicazione di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="5042e-142">hello command deploys hello sample application tooPi.</span></span> <span data-ttu-id="5042e-143">Quindi, viene eseguita un'applicazione hello Pi e un'attività separata nell'host computer toosend 20 blink messaggi tooPi dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5042e-143">Then, it runs hello application on Pi and a separate task on your host computer toosend 20 blink messages tooPi from your IoT hub.</span></span>

<span data-ttu-id="5042e-144">Quando si esegue l'applicazione di esempio hello, avvia l'ascolto toomessages dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5042e-144">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="5042e-145">Nel frattempo, attività gulp hello invia messaggi di "blink" diversi dai tooPi hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5042e-145">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooPi.</span></span> <span data-ttu-id="5042e-146">Per ogni messaggio blink che riceve Pi, l'applicazione di esempio hello chiama hello `blinkLED` hello tooblink funzione LED.</span><span class="sxs-lookup"><span data-stu-id="5042e-146">For each blink message that Pi receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="5042e-147">Dovrebbe essere blink LED hello ogni due secondi come hello gulp attività inviati 20 messaggi dal tooPi hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5042e-147">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooPi.</span></span> <span data-ttu-id="5042e-148">Hello ultimo uno è un messaggio "stop" che indica toostop applicazione hello in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="5042e-148">hello last one is a "stop" message that tells hello application toostop running.</span></span>

![Applicazione di esempio con comando gulp e messaggi di lampeggiamento](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink.png)

## <a name="summary"></a><span data-ttu-id="5042e-150">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="5042e-150">Summary</span></span>
<span data-ttu-id="5042e-151">I messaggi inviati correttamente dal hello di IoT hub tooPi tooblink LED.</span><span class="sxs-lookup"><span data-stu-id="5042e-151">You’ve successfully sent messages from your IoT hub tooPi tooblink hello LED.</span></span> <span data-ttu-id="5042e-152">attività successiva Hello è facoltativo: modificare hello e disattivare il comportamento di hello LED.</span><span class="sxs-lookup"><span data-stu-id="5042e-152">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5042e-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5042e-153">Next steps</span></span>
[<span data-ttu-id="5042e-154">Modificare hello e disattivare il comportamento di hello LED</span><span class="sxs-lookup"><span data-stu-id="5042e-154">Change hello on and off behavior of hello LED</span></span>](iot-hub-raspberry-pi-kit-node-lesson4-change-led-behavior.md)

