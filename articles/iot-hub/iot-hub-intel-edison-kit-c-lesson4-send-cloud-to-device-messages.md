---
title: 'Connettere Intel Edison (C) ad Azure IoT: lezione 4: Ricevere i messaggi | Documentazione Microsoft'
description: "Un'applicazione di esempio viene eseguita in Edison e monitora i messaggi in ingresso dall'hub IoT. Una nuova attività gulp invia messaggi a Edison dall'hub IoT per far lampeggiare il LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: led di controllo arduino dal web, led di controllo arduino tramite web
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 820d38f3-d3b8-4249-9e2b-f1b9b771e62f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b7de7a8b53cdb1d7c2560225fce9166e555e5123
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a><span data-ttu-id="25f47-105">Eseguire un'applicazione di esempio per ricevere messaggi da cloud a dispositivo</span><span class="sxs-lookup"><span data-stu-id="25f47-105">Run a sample application to receive cloud-to-device messages</span></span>
<span data-ttu-id="25f47-106">Questo articolo illustra come distribuire un'applicazione di esempio in Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="25f47-106">In this article, you deploy a sample application on Intel Edison.</span></span> <span data-ttu-id="25f47-107">L'applicazione di esempio monitora i messaggi in ingresso provenienti dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="25f47-107">The sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="25f47-108">È anche possibile eseguire un'attività gulp nel computer per inviare messaggi a Edison dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="25f47-108">You also run a gulp task on your computer to send messages to Edison from your IoT hub.</span></span> <span data-ttu-id="25f47-109">Alla ricezione dei messaggi, l'applicazione di esempio fa lampeggiare il LED.</span><span class="sxs-lookup"><span data-stu-id="25f47-109">When the sample application receives the messages, it blinks the LED.</span></span> <span data-ttu-id="25f47-110">In caso di problemi, cercare le soluzioni nella [pagina sulla risoluzione dei problemi][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="25f47-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="25f47-111">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="25f47-111">What you will do</span></span>
* <span data-ttu-id="25f47-112">Connettere l'applicazione di esempio all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="25f47-112">Connect the sample application to your IoT hub.</span></span>
* <span data-ttu-id="25f47-113">Distribuire ed eseguire l'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="25f47-113">Deploy and run the sample application.</span></span>
* <span data-ttu-id="25f47-114">Inviare messaggi dall'hub IoT a Edison per far lampeggiare il LED.</span><span class="sxs-lookup"><span data-stu-id="25f47-114">Send messages from your IoT hub to Edison to blink the LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="25f47-115">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="25f47-115">What you will learn</span></span>
<span data-ttu-id="25f47-116">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="25f47-116">In this article, you will learn:</span></span>
* <span data-ttu-id="25f47-117">Come monitorare i messaggi in ingresso dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="25f47-117">How to monitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="25f47-118">Come inviare messaggi da cloud a dispositivo dall'hub IoT a Edison.</span><span class="sxs-lookup"><span data-stu-id="25f47-118">How to send cloud-to-device messages from your IoT hub to Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="25f47-119">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="25f47-119">What you need</span></span>
* <span data-ttu-id="25f47-120">Intel Edison, impostato per l'uso.</span><span class="sxs-lookup"><span data-stu-id="25f47-120">Intel Edison, set up for use.</span></span> <span data-ttu-id="25f47-121">Per informazioni sull'impostazione di Edison, vedere l'articolo su come [configurare il dispositivo][configure-your-device].</span><span class="sxs-lookup"><span data-stu-id="25f47-121">To learn how to set up Edison, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="25f47-122">Un hub IoT creato nella propria sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="25f47-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="25f47-123">Per informazioni sulla creazione dell'hub IoT, vedere l'articolo su come [creare l'hub IoT di Azure][create-your-azure-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="25f47-123">To learn how to create your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-the-sample-application-to-your-iot-hub"></a><span data-ttu-id="25f47-124">Connettere l'applicazione di esempio all'hub IoT</span><span class="sxs-lookup"><span data-stu-id="25f47-124">Connect the sample application to your IoT hub</span></span>
1. <span data-ttu-id="25f47-125">Assicurarsi che sia aperta la cartella `iot-hub-c-edison-getting-started` del repository.</span><span class="sxs-lookup"><span data-stu-id="25f47-125">Make sure that you're in the repo folder `iot-hub-c-edison-getting-started`.</span></span> <span data-ttu-id="25f47-126">Aprire l'applicazione di esempio in Visual Studio Code usando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="25f47-126">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="25f47-127">Il file nella sottocartella `app` è il file di origine chiave che contiene il codice per il monitoraggio dei messaggi in ingresso dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="25f47-127">The file in the `app` subfolder is the key source file that contains the code to monitor incoming messages from the IoT hub.</span></span> <span data-ttu-id="25f47-128">La funzione `blinkLED` fa lampeggiare il LED.</span><span class="sxs-lookup"><span data-stu-id="25f47-128">The `blinkLED` function blinks the LED.</span></span>

   ![Struttura del repository nell'applicazione di esempio][repo-structure]
2. <span data-ttu-id="25f47-130">Inizializzare il file di configurazione usando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="25f47-130">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="25f47-131">Se la procedura descritta in [Creare un'app per le funzioni di Azure e un account di archiviazione][create-an-azure-function-app-and-storage-account] è stata completata nello stesso computer, tutte le configurazioni vengono ereditate. È quindi possibile passare direttamente all'attività di distribuzione ed esecuzione dell'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="25f47-131">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all the configurations are inherited, so you can skip the step to the task of deploying and running the sample application.</span></span> <span data-ttu-id="25f47-132">Se la procedura descritta in [Creare un'app per le funzioni di Azure e un account di archiviazione][create-an-azure-function-app-and-storage-account] è stata completata in un computer diverso, è necessario sostituire i segnaposto nel file `config-edison.json`.</span><span class="sxs-lookup"><span data-stu-id="25f47-132">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need to replace the placeholders in the `config-edison.json` file.</span></span> <span data-ttu-id="25f47-133">Il file `config-edison.json` si trova nella sottocartella della cartella principale.</span><span class="sxs-lookup"><span data-stu-id="25f47-133">The `config-edison.json` file is in the subfolder of your home folder.</span></span>

   ![Contenuto del file config-edison.json](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * <span data-ttu-id="25f47-135">Sostituire **[device hostname or IP address]** con l'indirizzo IP del dispositivo annotato quando è stato configurato il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="25f47-135">Replace **[device hostname or IP address]** with the device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="25f47-136">Sostituire **[IoT device connection string]** con la stringa di connessione del dispositivo che si ottiene eseguendo il comando `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}`.</span><span class="sxs-lookup"><span data-stu-id="25f47-136">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="25f47-137">Sostituire **[IoT hub connection string]** con la stringa di connessione dell'hub IoT che si ottiene eseguendo il comando `az iot hub show-connection-string --name {my hub name}`.</span><span class="sxs-lookup"><span data-stu-id="25f47-137">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name}` command.</span></span>

   > [!NOTE]
   > <span data-ttu-id="25f47-138">Se non è stato fatto nella lezione 1, eseguire anche il comando **gulp install-tools**.</span><span class="sxs-lookup"><span data-stu-id="25f47-138">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="25f47-139">Distribuire ed eseguire l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="25f47-139">Deploy and run the sample application</span></span>
<span data-ttu-id="25f47-140">Distribuire ed eseguire l'applicazione di esempio in Edison eseguendo questi comandi:</span><span class="sxs-lookup"><span data-stu-id="25f47-140">Deploy and run the sample application on Edison by running the following commands:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="25f47-141">Il comando gulp distribuisce l'applicazione di esempio in Edison,</span><span class="sxs-lookup"><span data-stu-id="25f47-141">The gulp command deploys the sample application to Edison.</span></span> <span data-ttu-id="25f47-142">quindi esegue l'applicazione in Edison e un'attività separata nel computer host per inviare 20 messaggi di lampeggiamento dall'hub IoT a Edison.</span><span class="sxs-lookup"><span data-stu-id="25f47-142">Then, it runs the application on Edison and a separate task on your host computer to send 20 blink messages to Edison from your IoT hub.</span></span>

<span data-ttu-id="25f47-143">Non appena viene eseguita, l'applicazione di esempio rimane in ascolto di messaggi provenienti dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="25f47-143">After the sample application runs, it starts listening to messages from your IoT hub.</span></span> <span data-ttu-id="25f47-144">Nel frattempo, l'attività gulp invia vari messaggi di lampeggiamento dall'hub IoT a Edison.</span><span class="sxs-lookup"><span data-stu-id="25f47-144">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to Edison.</span></span> <span data-ttu-id="25f47-145">Per ogni messaggio di lampeggiamento ricevuto da Edison, l'applicazione di esempio chiama la funzione `blinkLED` per far lampeggiare il LED.</span><span class="sxs-lookup"><span data-stu-id="25f47-145">For each blink message that Edison receives, the sample application calls the `blinkLED` function to blink the LED.</span></span>

<span data-ttu-id="25f47-146">Durante l'invio dei 20 messaggi dall'hub IoT a Edison da parte dell'attività gulp, il LED dovrebbe lampeggiare ogni due secondi.</span><span class="sxs-lookup"><span data-stu-id="25f47-146">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to Edison.</span></span> <span data-ttu-id="25f47-147">L'ultimo è un messaggio "stop" che arresta l'esecuzione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="25f47-147">The last one is a "stop" message that stops the application from running.</span></span>

![Applicazione di esempio con comando gulp e messaggi di lampeggiamento][gulp-command-and-blink-messages]

## <a name="summary"></a><span data-ttu-id="25f47-149">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="25f47-149">Summary</span></span>
<span data-ttu-id="25f47-150">Sono stati inviati messaggi dall'hub IoT a Edison per far lampeggiare il LED.</span><span class="sxs-lookup"><span data-stu-id="25f47-150">You’ve successfully sent messages from your IoT hub to Edison to blink the LED.</span></span> <span data-ttu-id="25f47-151">L'attività successiva è facoltativa: modificare il comportamento di accensione e spegnimento del LED.</span><span class="sxs-lookup"><span data-stu-id="25f47-151">The next task is optional: change the on and off behavior of the LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="25f47-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="25f47-152">Next steps</span></span>
<span data-ttu-id="25f47-153">[Modificare il comportamento di accensione e spegnimento del LED][change-the-on-and-off-behavior-of-the-led]</span><span class="sxs-lookup"><span data-stu-id="25f47-153">[Change the on and off behavior of the LED][change-the-on-and-off-behavior-of-the-led]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-c-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure_c.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink_c.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-c-lesson4-change-led-behavior.md