---
title: 'Connettere Arduino (C) ad Azure IoT: lezione 4: da cloud a dispositivo | Microsoft Docs'
description: "Un'applicazione di esempio viene eseguita nel dispositivo Adafruit Feather M0 WiFi e monitora i messaggi in ingresso dall'hub IoT. Una nuova attività gulp invia messaggi al dispositivo Adafruit Feather M0 WiFi dall'hub IoT per far lampeggiare il LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: led di controllo arduino dal web, led di controllo arduino tramite web
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: a0bf53fb-29fb-485f-ba4a-6c715057b1a2
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b4f4c1d86b10b64c104ac812d1f650d723322be8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a><span data-ttu-id="8a410-105">Eseguire un'applicazione di esempio per ricevere messaggi da cloud a dispositivo</span><span class="sxs-lookup"><span data-stu-id="8a410-105">Run a sample application to receive cloud-to-device messages</span></span>
<span data-ttu-id="8a410-106">In questo articolo si distribuisce un'applicazione di esempio nella scheda Arduino Adafruit Feather M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="8a410-106">In this article, you deploy a sample application on your Adafruit Feather M0 WiFi Arduino board.</span></span>

<span data-ttu-id="8a410-107">L'applicazione di esempio monitora i messaggi in ingresso provenienti dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8a410-107">The sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="8a410-108">Per inviare messaggi dall'hub IoT alla scheda Arduino è anche possibile eseguire un'attività gulp nel computer.</span><span class="sxs-lookup"><span data-stu-id="8a410-108">You also run a gulp task on your computer to send messages to your Arduino board from your IoT hub.</span></span> <span data-ttu-id="8a410-109">Alla ricezione dei messaggi, l'applicazione di esempio fa lampeggiare il LED.</span><span class="sxs-lookup"><span data-stu-id="8a410-109">When the sample application receives the messages, it blinks the LED.</span></span> <span data-ttu-id="8a410-110">In caso di problemi, cercare le soluzioni nella [pagina sulla risoluzione dei problemi][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="8a410-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="8a410-111">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="8a410-111">What you will do</span></span>
* <span data-ttu-id="8a410-112">Connettere l'applicazione di esempio all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8a410-112">Connect the sample application to your IoT hub.</span></span>
* <span data-ttu-id="8a410-113">Distribuire ed eseguire l'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="8a410-113">Deploy and run the sample application.</span></span>
* <span data-ttu-id="8a410-114">Inviare messaggi dall'hub IoT alla scheda Arduino per far lampeggiare il LED.</span><span class="sxs-lookup"><span data-stu-id="8a410-114">Send messages from your IoT hub to your Arduino board to blink the LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="8a410-115">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="8a410-115">What you will learn</span></span>
<span data-ttu-id="8a410-116">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="8a410-116">In this article, you will learn:</span></span>
* <span data-ttu-id="8a410-117">Come monitorare i messaggi in ingresso dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8a410-117">How to monitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="8a410-118">Come inviare i messaggi da cloud a dispositivo dall'hub IoT alla scheda Arduino.</span><span class="sxs-lookup"><span data-stu-id="8a410-118">How to send cloud-to-device messages from your IoT hub to your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8a410-119">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="8a410-119">What you need</span></span>
* <span data-ttu-id="8a410-120">La scheda Arduino pronta all'uso.</span><span class="sxs-lookup"><span data-stu-id="8a410-120">Your Arduino board, set up for use.</span></span> <span data-ttu-id="8a410-121">Per informazioni su come impostare la scheda Arduino, vedere [Configurare il dispositivo][configure-your-device].</span><span class="sxs-lookup"><span data-stu-id="8a410-121">To learn how to set up your Arduino board, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="8a410-122">Un hub IoT creato nella propria sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8a410-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="8a410-123">Per informazioni sulla creazione dell'hub IoT, vedere l'articolo su come [creare l'hub IoT di Azure][create-your-azure-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="8a410-123">To learn how to create your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-the-sample-application-to-your-iot-hub"></a><span data-ttu-id="8a410-124">Connettere l'applicazione di esempio all'hub IoT</span><span class="sxs-lookup"><span data-stu-id="8a410-124">Connect the sample application to your IoT hub</span></span>

1. <span data-ttu-id="8a410-125">Assicurarsi che sia aperta la cartella `iot-hub-c-feather-m0-getting-started` del repository.</span><span class="sxs-lookup"><span data-stu-id="8a410-125">Make sure that you're in the repo folder `iot-hub-c-feather-m0-getting-started`.</span></span>

   <span data-ttu-id="8a410-126">Aprire l'applicazione di esempio in Visual Studio Code usando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8a410-126">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="8a410-127">Si noti il file `app.ino` nella sottocartella `app`.</span><span class="sxs-lookup"><span data-stu-id="8a410-127">Notice the `app.ino` file in the `app` subfolder.</span></span> <span data-ttu-id="8a410-128">`app.ino` è il file di origine chiave che contiene il codice per il monitoraggio dei messaggi in ingresso dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8a410-128">The `app.ino` file is the key source file that contains the code to monitor incoming messages from the IoT hub.</span></span> <span data-ttu-id="8a410-129">La funzione `blinkLED` fa lampeggiare il LED.</span><span class="sxs-lookup"><span data-stu-id="8a410-129">The `blinkLED` function blinks the LED.</span></span>

   ![Struttura del repository nell'applicazione di esempio][repo-structure]

2. <span data-ttu-id="8a410-131">Ottenere la porta seriale del dispositivo usando l'interfaccia della riga di comando per l'individuazione del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="8a410-131">Obtain the serial port of the device with the device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="8a410-132">Verrà visualizzato un output simile al seguente e sarà rilevata la porta COM USB per la scheda Arduino:</span><span class="sxs-lookup"><span data-stu-id="8a410-132">You should see an output that is similar to the following and find the usb COM port for your Arduino board:</span></span>

   ![Individuazione del dispositivo][device-discovery]

3. <span data-ttu-id="8a410-134">Aprire il file `config.json` nella cartella della lezione e aggiungere il valore del numero della porta COM trovato:</span><span class="sxs-lookup"><span data-stu-id="8a410-134">Open the file `config.json` in the lesson folder and input the value of the found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > <span data-ttu-id="8a410-136">Per la porta COM, nella piattaforma Windows il formato è `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="8a410-136">For the COM port, on Windows platform, it has the format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="8a410-137">In macOS o Ubuntu inizia con `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="8a410-137">On macOS or Ubuntu, it will start with `/dev/`.</span></span>

4. <span data-ttu-id="8a410-138">Inizializzare il file di configurazione usando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8a410-138">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   # For Windows command prompt
   npm install
   gulp init
   gulp install-tools
   ```

5. <span data-ttu-id="8a410-139">Sostituire i valori seguenti nel file `config-arduino.json`:</span><span class="sxs-lookup"><span data-stu-id="8a410-139">Make the following replacements in the `config-arduino.json` file:</span></span>

   <span data-ttu-id="8a410-140">Se la procedura descritta in [Creare un'app per le funzioni di Azure e un account di archiviazione][create-an-azure-function-app-and-storage-account] è stata completata nello stesso computer, tutte le configurazioni vengono ereditate. È quindi possibile passare direttamente all'attività di distribuzione ed esecuzione dell'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="8a410-140">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all the configurations are inherited, so you can skip the step to the task of deploying and running the sample application.</span></span> <span data-ttu-id="8a410-141">Se la procedura descritta in [Creare un'app per le funzioni di Azure e un account di archiviazione][create-an-azure-function-app-and-storage-account] è stata completata in un computer diverso, è necessario sostituire i segnaposto nel file `config-arduino.json`.</span><span class="sxs-lookup"><span data-stu-id="8a410-141">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need to replace the placeholders in the `config-arduino.json` file.</span></span> <span data-ttu-id="8a410-142">Il file `config-arduino.json` si trova nella sottocartella della cartella principale.</span><span class="sxs-lookup"><span data-stu-id="8a410-142">The `config-arduino.json` file is in the subfolder of your home folder.</span></span>

   ![Contenuto del file config-arduino.json][config-arduino-json]

   * <span data-ttu-id="8a410-144">Sostituire **[Wi-Fi SSID]** con il codice SSID Wi-Fi che ha eseguito la connessione a Internet.</span><span class="sxs-lookup"><span data-stu-id="8a410-144">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected to the Internet.</span></span>
   * <span data-ttu-id="8a410-145">Sostituire **[Wi-Fi password]** con la password Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="8a410-145">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="8a410-146">Rimuovere la stringa se il Wi-Fi non richiede la password.</span><span class="sxs-lookup"><span data-stu-id="8a410-146">Remove the string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="8a410-147">Sostituire **[IoT device connection string]** con la stringa di connessione del dispositivo che si ottiene eseguendo il comando `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}`.</span><span class="sxs-lookup"><span data-stu-id="8a410-147">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="8a410-148">Sostituire **[IoT hub connection string]** con la stringa di connessione dell'hub IoT che si ottiene eseguendo il comando `az iot hub show-connection-string --name {my hub name}`.</span><span class="sxs-lookup"><span data-stu-id="8a410-148">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="8a410-149">Distribuire ed eseguire l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="8a410-149">Deploy and run the sample application</span></span>
<span data-ttu-id="8a410-150">Distribuire ed eseguire l'applicazione di esempio nella scheda Arduino usando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8a410-150">Deploy and run the sample application on your Arduino board by running the following commands:</span></span>

```bash
gulp run
# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="8a410-151">Il comando gulp distribuisce l'applicazione di esempio nella scheda Arduino.</span><span class="sxs-lookup"><span data-stu-id="8a410-151">The gulp command deploys the sample application to your Arduino board.</span></span> <span data-ttu-id="8a410-152">Quindi, esegue l'applicazione sulla scheda Arduino e un'attività separata sul computer host per l'invio di 20 messaggi di lampeggiamento dall'hub IoT alla scheda Arduino.</span><span class="sxs-lookup"><span data-stu-id="8a410-152">Then, it runs the application on your Arduino board and a separate task on your host computer to send 20 blink messages to your Arduino board from your IoT hub.</span></span>

<span data-ttu-id="8a410-153">Non appena viene eseguita, l'applicazione di esempio rimane in ascolto di messaggi provenienti dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8a410-153">After the sample application runs, it starts listening to messages from your IoT hub.</span></span> <span data-ttu-id="8a410-154">Nel frattempo, l'attività gulp invia vari messaggi di lampeggiamento dall'hub IoT alla scheda Arduino.</span><span class="sxs-lookup"><span data-stu-id="8a410-154">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to your Arduino board.</span></span> <span data-ttu-id="8a410-155">Per ogni messaggio di lampeggiamento ricevuto dalla scheda, l'applicazione di esempio chiama la funzione `blinkLED` per far lampeggiare il LED.</span><span class="sxs-lookup"><span data-stu-id="8a410-155">For each blink message that the board receives, the sample application calls the `blinkLED` function to blink the LED.</span></span>

<span data-ttu-id="8a410-156">Durante l'invio dei 20 messaggi dall'hub IoT alla scheda Arduino da parte dell'attività gulp, il LED dovrebbe lampeggiare ogni due secondi.</span><span class="sxs-lookup"><span data-stu-id="8a410-156">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to your Arduino board.</span></span> <span data-ttu-id="8a410-157">L'ultimo è un messaggio "stop" che arresta l'esecuzione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8a410-157">The last one is a "stop" message that stops the application from running.</span></span>

![Applicazione di esempio con comando gulp e messaggi di lampeggiamento][sample-application]

## <a name="summary"></a><span data-ttu-id="8a410-159">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="8a410-159">Summary</span></span>
<span data-ttu-id="8a410-160">Sono stati inviati messaggi dall'hub IoT alla scheda Arduino per far lampeggiare il LED.</span><span class="sxs-lookup"><span data-stu-id="8a410-160">You’ve successfully sent messages from your IoT hub to your Arduino board to blink the LED.</span></span> <span data-ttu-id="8a410-161">L'attività successiva è facoltativa: modificare il comportamento di accensione e spegnimento del LED.</span><span class="sxs-lookup"><span data-stu-id="8a410-161">The next task is optional: change the on and off behavior of the LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a410-162">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8a410-162">Next steps</span></span>
<span data-ttu-id="8a410-163">[Modificare il comportamento di accensione e spegnimento del LED][change-the-on-and-off-led-behavior]</span><span class="sxs-lookup"><span data-stu-id="8a410-163">[Change the on and off behavior of the LED][change-the-on-and-off-led-behavior]</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/repo_structure_arduino.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[create-an-azure-function-app-and-storage-account]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/config-arduino.png
[sample-application]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_blink_arduino.png
[change-the-on-and-off-led-behavior]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-change-led-behavior.md