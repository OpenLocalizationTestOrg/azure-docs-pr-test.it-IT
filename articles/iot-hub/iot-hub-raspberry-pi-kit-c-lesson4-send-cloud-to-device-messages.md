---
title: 'Connettere Raspberry Pi (C) ad Azure IoT: lezione 4: da cloud a dispositivo | Microsoft Docs'
description: "Un'applicazione di esempio viene eseguita nel dispositivo Pi e monitora i messaggi in ingresso dall'hub IoT. Una nuova attività gulp invia messaggi al dispositivo Pi dall'hub IoT per far lampeggiare il LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: da cloud a dispositivo, messaggio dal cloud
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
ms.openlocfilehash: 86c7be931319d9995c2a7311267c7e7c03c3c1b8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a><span data-ttu-id="2c97b-105">Eseguire un'applicazione di esempio per ricevere messaggi da cloud a dispositivo</span><span class="sxs-lookup"><span data-stu-id="2c97b-105">Run a sample application to receive cloud-to-device messages</span></span>
<span data-ttu-id="2c97b-106">Questo articolo illustra come distribuire un'applicazione di esempio nel dispositivo Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="2c97b-106">In this article, you deploy a sample application on Raspberry Pi 3.</span></span> <span data-ttu-id="2c97b-107">L'applicazione di esempio monitora i messaggi in ingresso provenienti dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2c97b-107">The sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="2c97b-108">È anche possibile eseguire un'attività gulp nel computer per inviare messaggi dall'hub IoT al dispositivo Pi.</span><span class="sxs-lookup"><span data-stu-id="2c97b-108">You also run a gulp task on your computer to send messages to Pi from your IoT hub.</span></span> <span data-ttu-id="2c97b-109">Alla ricezione dei messaggi, l'applicazione di esempio fa lampeggiare il LED.</span><span class="sxs-lookup"><span data-stu-id="2c97b-109">When the sample application receives the messages, it blinks the LED.</span></span> <span data-ttu-id="2c97b-110">In caso di problemi, cercare le soluzioni nella pagina sulla [risoluzione dei problemi](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="2c97b-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="2c97b-111">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="2c97b-111">What you will do</span></span>
* <span data-ttu-id="2c97b-112">Connettere l'applicazione di esempio all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2c97b-112">Connect the sample application to your IoT hub.</span></span>
* <span data-ttu-id="2c97b-113">Distribuire ed eseguire l'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="2c97b-113">Deploy and run the sample application.</span></span>
* <span data-ttu-id="2c97b-114">Inviare messaggi dall'hub IoT al dispositivo Pi per far lampeggiare il LED.</span><span class="sxs-lookup"><span data-stu-id="2c97b-114">Send messages from your IoT hub to Pi to blink the LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="2c97b-115">Concetti legati all'esercitazione</span><span class="sxs-lookup"><span data-stu-id="2c97b-115">What you will learn</span></span>
<span data-ttu-id="2c97b-116">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="2c97b-116">In this article, you will learn:</span></span>
* <span data-ttu-id="2c97b-117">Come monitorare i messaggi in ingresso dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2c97b-117">How to monitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="2c97b-118">Come inviare messaggi da cloud a dispositivo dall'hub IoT al dispositivo Pi.</span><span class="sxs-lookup"><span data-stu-id="2c97b-118">How to send cloud-to-device messages from your IoT hub to Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2c97b-119">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="2c97b-119">What you need</span></span>
* <span data-ttu-id="2c97b-120">Raspberry Pi 3, impostato per l'uso.</span><span class="sxs-lookup"><span data-stu-id="2c97b-120">Raspberry Pi 3, set up for use.</span></span> <span data-ttu-id="2c97b-121">Per informazioni su come impostare il dispositivo Pi, vedere [Configurare il dispositivo](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md).</span><span class="sxs-lookup"><span data-stu-id="2c97b-121">To learn how to set up Pi, see [Configure your device](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md).</span></span>
* <span data-ttu-id="2c97b-122">Un hub IoT creato nella propria sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2c97b-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="2c97b-123">Per informazioni su come creare l'hub IoT, vedere [Creare l'hub IoT e registrare Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="2c97b-123">To learn how to create your IoT hub, see [Create your IoT hub and register Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span></span>

## <a name="connect-the-sample-application-to-your-iot-hub"></a><span data-ttu-id="2c97b-124">Connettere l'applicazione di esempio all'hub IoT</span><span class="sxs-lookup"><span data-stu-id="2c97b-124">Connect the sample application to your IoT hub</span></span>
1. <span data-ttu-id="2c97b-125">Assicurarsi che sia aperta la cartella `iot-hub-c-raspberrypi-getting-started` del repository.</span><span class="sxs-lookup"><span data-stu-id="2c97b-125">Make sure that you're in the repo folder `iot-hub-c-raspberrypi-getting-started`.</span></span> <span data-ttu-id="2c97b-126">Aprire l'applicazione di esempio in Visual Studio Code usando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2c97b-126">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="2c97b-127">Si noti il file `app.c` nella sottocartella `app`.</span><span class="sxs-lookup"><span data-stu-id="2c97b-127">Notice the `app.c` file in the `app` subfolder.</span></span> <span data-ttu-id="2c97b-128">`app.c` è il file di origine chiave che contiene il codice per il monitoraggio dei messaggi in ingresso dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2c97b-128">The `app.c` file is the key source file that contains the code to monitor incoming messages from the IoT hub.</span></span> <span data-ttu-id="2c97b-129">La funzione `blinkLED` fa lampeggiare il LED.</span><span class="sxs-lookup"><span data-stu-id="2c97b-129">The `blinkLED` function blinks the LED.</span></span>

   ![Struttura del repository nell'applicazione di esempio](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure_c.png)
2. <span data-ttu-id="2c97b-131">Inizializzare il file di configurazione usando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2c97b-131">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="2c97b-132">Se la procedura descritta in [Creare un'app per le funzioni di Azure e un account di archiviazione](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) è stata completata con lo stesso computer, tutte le configurazioni vengono ereditate. È quindi possibile passare direttamente all'attività di distribuzione ed esecuzione dell'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="2c97b-132">If you completed the steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) on this computer, all the configurations are inherited, so you can skip to step to the task of deploying and running the sample application.</span></span> <span data-ttu-id="2c97b-133">Se la procedura descritta in [Creare un'app per le funzioni di Azure e un account di archiviazione](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) è stata completata con un computer diverso, è necessario sostituire i segnaposto nel file `config-raspberrypi.json`.</span><span class="sxs-lookup"><span data-stu-id="2c97b-133">If you completed the steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) on a different computer, you need to replace the placeholders in the `config-raspberrypi.json` file.</span></span> <span data-ttu-id="2c97b-134">Il file `config-raspberrypi.json` si trova nella sottocartella della cartella principale.</span><span class="sxs-lookup"><span data-stu-id="2c97b-134">The `config-raspberrypi.json` file is in the subfolder of your home folder.</span></span>

   ![Contenuto del file config-raspberrypi.json](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* <span data-ttu-id="2c97b-136">Sostituire **[device hostname or IP address]** con l'indirizzo IP o il nome host del dispositivo Pi che si ottiene eseguendo il comando `devdisco list --eth`.</span><span class="sxs-lookup"><span data-stu-id="2c97b-136">Replace **[device hostname or IP address]** with Pi’s IP address or host name that you get by running the `devdisco list --eth` command.</span></span>
* <span data-ttu-id="2c97b-137">Sostituire **[IoT device connection string]** con la stringa di connessione del dispositivo che si ottiene eseguendo il comando `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}`.</span><span class="sxs-lookup"><span data-stu-id="2c97b-137">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` command.</span></span>
* <span data-ttu-id="2c97b-138">Sostituire **[IoT hub connection string]** con la stringa di connessione dell'hub IoT che si ottiene eseguendo il comando `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}`.</span><span class="sxs-lookup"><span data-stu-id="2c97b-138">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` command.</span></span>

> [!NOTE]
> <span data-ttu-id="2c97b-139">Se non è stato fatto nella lezione 1, eseguire anche il comando **gulp install-tools**.</span><span class="sxs-lookup"><span data-stu-id="2c97b-139">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="2c97b-140">Distribuire ed eseguire l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="2c97b-140">Deploy and run the sample application</span></span>
<span data-ttu-id="2c97b-141">Distribuire ed eseguire l'applicazione di esempio nel dispositivo Pi con questi comandi:</span><span class="sxs-lookup"><span data-stu-id="2c97b-141">Deploy and run the sample application on Pi by running the following commands:</span></span>

```
gulp deploy && gulp run
```

<span data-ttu-id="2c97b-142">Il comando gulp esegue innanzitutto l'attività install-tools,</span><span class="sxs-lookup"><span data-stu-id="2c97b-142">The gulp command runs the install-tools task first.</span></span> <span data-ttu-id="2c97b-143">quindi distribuisce l'applicazione di esempio nel dispositivo Pi.</span><span class="sxs-lookup"><span data-stu-id="2c97b-143">Then it deploys the sample application to Pi.</span></span> <span data-ttu-id="2c97b-144">Esegue infine l'applicazione nel dispositivo Pi e un'attività separata nel computer host per inviare 20 messaggi di lampeggiamento dall'hub IoT al dispositivo Pi.</span><span class="sxs-lookup"><span data-stu-id="2c97b-144">Finally, it runs the application on Pi and a separate task on your host computer to send 20 blink messages to Pi from your IoT hub.</span></span>

<span data-ttu-id="2c97b-145">Non appena viene eseguita, l'applicazione di esempio rimane in ascolto di messaggi provenienti dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2c97b-145">After the sample application runs, it starts listening to messages from your IoT hub.</span></span> <span data-ttu-id="2c97b-146">Nel frattempo, l'attività gulp invia vari messaggi di lampeggiamento dall'hub IoT al dispositivo Pi.</span><span class="sxs-lookup"><span data-stu-id="2c97b-146">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to Pi.</span></span> <span data-ttu-id="2c97b-147">Per ogni messaggio di lampeggiamento ricevuto dal dispositivo Pi, l'applicazione di esempio chiama la funzione `blinkLED` per far lampeggiare il LED.</span><span class="sxs-lookup"><span data-stu-id="2c97b-147">For each blink message that Pi receives, the sample application calls the `blinkLED` function to blink the LED.</span></span>

<span data-ttu-id="2c97b-148">Durante l'invio dei 20 messaggi dall'hub IoT al dispositivo Pi da parte dell'attività gulp, il LED dovrebbe lampeggiare ogni due secondi.</span><span class="sxs-lookup"><span data-stu-id="2c97b-148">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to Pi.</span></span> <span data-ttu-id="2c97b-149">L'ultimo è un messaggio "stop" che arresta l'esecuzione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2c97b-149">The last one is a "stop" message that stops the application from running.</span></span>

![Applicazione di esempio con comando gulp e messaggi di lampeggiamento](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink_c.png)

## <a name="summary"></a><span data-ttu-id="2c97b-151">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="2c97b-151">Summary</span></span>
<span data-ttu-id="2c97b-152">Sono stati inviati messaggi dall'hub IoT al dispositivo Pi per far lampeggiare il LED.</span><span class="sxs-lookup"><span data-stu-id="2c97b-152">You’ve successfully sent messages from your IoT hub to Pi to blink the LED.</span></span> <span data-ttu-id="2c97b-153">L'attività successiva è facoltativa: modificare il comportamento di accensione e spegnimento del LED.</span><span class="sxs-lookup"><span data-stu-id="2c97b-153">The next task is optional: change the on and off behavior of the LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c97b-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2c97b-154">Next steps</span></span>
[<span data-ttu-id="2c97b-155">Modificare il comportamento di accensione e spegnimento del LED</span><span class="sxs-lookup"><span data-stu-id="2c97b-155">Change the on and off behavior of the LED</span></span>](iot-hub-raspberry-pi-kit-c-lesson4-change-led-behavior.md)
