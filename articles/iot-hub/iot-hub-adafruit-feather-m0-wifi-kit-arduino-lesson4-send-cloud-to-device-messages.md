---
title: 'Connect Arduino (C) tooAzure IoT - lezione 4: Cloud a dispositivo | Documenti Microsoft'
description: "Un'applicazione di esempio viene eseguita nel dispositivo Adafruit Feather M0 WiFi e monitora i messaggi in ingresso dall'hub IoT. Una nuova attività gulp invia messaggi tooAdafruit Wi-Fi M0 sfumatura da hello di tooblink l'hub IoT LED."
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
ms.openlocfilehash: dcddd61ff684f49436103675938d719cb227c409
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="da1e9-105">Eseguire un tooreceive di applicazione di esempio i messaggi da cloud a dispositivo</span><span class="sxs-lookup"><span data-stu-id="da1e9-105">Run a sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="da1e9-106">In questo articolo si distribuisce un'applicazione di esempio nella scheda Arduino Adafruit Feather M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="da1e9-106">In this article, you deploy a sample application on your Adafruit Feather M0 WiFi Arduino board.</span></span>

<span data-ttu-id="da1e9-107">applicazione di esempio Hello controlla i messaggi in ingresso dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="da1e9-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="da1e9-108">Inoltre si esegue un'attività gulp su tooyour di messaggi del toosend computer Arduino Lavagna dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="da1e9-108">You also run a gulp task on your computer toosend messages tooyour Arduino board from your IoT hub.</span></span> <span data-ttu-id="da1e9-109">Quando l'applicazione di esempio hello riceve messaggi hello, lampeggia hello LED.</span><span class="sxs-lookup"><span data-stu-id="da1e9-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="da1e9-110">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="da1e9-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="da1e9-111">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="da1e9-111">What you will do</span></span>
* <span data-ttu-id="da1e9-112">Connettere l'hub IoT hello esempio applicazione tooyour.</span><span class="sxs-lookup"><span data-stu-id="da1e9-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="da1e9-113">Distribuire ed eseguire l'applicazione di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="da1e9-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="da1e9-114">Invio di messaggi dal hello della tooblink Lavagna di IoT hub tooyour Arduino LED.</span><span class="sxs-lookup"><span data-stu-id="da1e9-114">Send messages from your IoT hub tooyour Arduino board tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="da1e9-115">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="da1e9-115">What you will learn</span></span>
<span data-ttu-id="da1e9-116">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="da1e9-116">In this article, you will learn:</span></span>
* <span data-ttu-id="da1e9-117">La modalità in ingresso toomonitor dei messaggi dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="da1e9-117">How toomonitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="da1e9-118">La modalità toosend cloud a dispositivo dei messaggi dal tooyour hub IoT Arduino Lavagna.</span><span class="sxs-lookup"><span data-stu-id="da1e9-118">How toosend cloud-to-device messages from your IoT hub tooyour Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="da1e9-119">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="da1e9-119">What you need</span></span>
* <span data-ttu-id="da1e9-120">La scheda Arduino pronta all'uso.</span><span class="sxs-lookup"><span data-stu-id="da1e9-120">Your Arduino board, set up for use.</span></span> <span data-ttu-id="da1e9-121">toolearn tooset la tavola da Arduino, vedere [configurare il dispositivo][configure-your-device].</span><span class="sxs-lookup"><span data-stu-id="da1e9-121">toolearn how tooset up your Arduino board, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="da1e9-122">Un hub IoT creato nella propria sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="da1e9-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="da1e9-123">toolearn come toocreate l'hub IoT, vedere [creare l'IoT Hub Azure][create-your-azure-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="da1e9-123">toolearn how toocreate your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="da1e9-124">Collegare hello esempio applicazione tooyour IoT hub</span><span class="sxs-lookup"><span data-stu-id="da1e9-124">Connect hello sample application tooyour IoT hub</span></span>

1. <span data-ttu-id="da1e9-125">Assicurarsi che si è nella cartella repository hello `iot-hub-c-feather-m0-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="da1e9-125">Make sure that you're in hello repo folder `iot-hub-c-feather-m0-getting-started`.</span></span>

   <span data-ttu-id="da1e9-126">Aprire l'applicazione di esempio hello in Visual Studio Code eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="da1e9-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="da1e9-127">Hello preavviso `app.ino` file hello `app` sottocartella.</span><span class="sxs-lookup"><span data-stu-id="da1e9-127">Notice hello `app.ino` file in hello `app` subfolder.</span></span> <span data-ttu-id="da1e9-128">Hello `app.ino` è hello i file di origine della chiave che contiene i messaggi in ingresso hello codice toomonitor dall'hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="da1e9-128">hello `app.ino` file is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="da1e9-129">Hello `blinkLED` funzione lampeggia hello LED.</span><span class="sxs-lookup"><span data-stu-id="da1e9-129">hello `blinkLED` function blinks hello LED.</span></span>

   ![Struttura repository nell'applicazione di esempio hello][repo-structure]

2. <span data-ttu-id="da1e9-131">Ottenere della porta seriale del dispositivo hello con hello dispositivo individuazione cli hello:</span><span class="sxs-lookup"><span data-stu-id="da1e9-131">Obtain hello serial port of hello device with hello device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="da1e9-132">Si dovrebbe vedere un output simile toohello seguente e trovare hello usb porta COM per la scheda Arduino:</span><span class="sxs-lookup"><span data-stu-id="da1e9-132">You should see an output that is similar toohello following and find hello usb COM port for your Arduino board:</span></span>

   ![Individuazione del dispositivo][device-discovery]

3. <span data-ttu-id="da1e9-134">File aperti hello `config.json` hello lezione cartella e il valore di input hello di trovare il numero di porta COM hello:</span><span class="sxs-lookup"><span data-stu-id="da1e9-134">Open hello file `config.json` in hello lesson folder and input hello value of hello found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > <span data-ttu-id="da1e9-136">Per la porta COM hello, sulla piattaforma Windows, ha il formato di hello di `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="da1e9-136">For hello COM port, on Windows platform, it has hello format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="da1e9-137">In macOS o Ubuntu inizia con `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="da1e9-137">On macOS or Ubuntu, it will start with `/dev/`.</span></span>

4. <span data-ttu-id="da1e9-138">Inizializzare i file di configurazione hello eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="da1e9-138">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   # For Windows command prompt
   npm install
   gulp init
   gulp install-tools
   ```

5. <span data-ttu-id="da1e9-139">Rendere hello seguenti sostituzioni hello `config-arduino.json` file:</span><span class="sxs-lookup"><span data-stu-id="da1e9-139">Make hello following replacements in hello `config-arduino.json` file:</span></span>

   <span data-ttu-id="da1e9-140">Se è stato completato i passaggi di hello in [creare un account di archiviazione e l'app Azure funzione] [ create-an-azure-function-app-and-storage-account] su questo computer, tutte le configurazioni di hello vengono ereditate, pertanto è possibile ignorare hello passaggio toohello attività di distribuzione e in esecuzione l'applicazione di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="da1e9-140">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all hello configurations are inherited, so you can skip hello step toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="da1e9-141">Se è stato completato i passaggi di hello in [creare un account di archiviazione e l'app Azure funzione] [ create-an-azure-function-app-and-storage-account] in un computer diverso, è necessario segnaposto hello tooreplace hello `config-arduino.json` file.</span><span class="sxs-lookup"><span data-stu-id="da1e9-141">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need tooreplace hello placeholders in hello `config-arduino.json` file.</span></span> <span data-ttu-id="da1e9-142">Hello `config-arduino.json` file si trova nella sottocartella hello della cartella principale.</span><span class="sxs-lookup"><span data-stu-id="da1e9-142">hello `config-arduino.json` file is in hello subfolder of your home folder.</span></span>

   ![Contenuto del file di configurazione arduino.json hello][config-arduino-json]

   * <span data-ttu-id="da1e9-144">Sostituire **[Wi-Fi SSID]** con il SSID Wi-Fi che è connesso a Internet toohello.</span><span class="sxs-lookup"><span data-stu-id="da1e9-144">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected toohello Internet.</span></span>
   * <span data-ttu-id="da1e9-145">Sostituire **[Wi-Fi password]** con la password Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="da1e9-145">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="da1e9-146">Rimuovere la stringa hello se il Wi-Fi non richiede una password.</span><span class="sxs-lookup"><span data-stu-id="da1e9-146">Remove hello string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="da1e9-147">Sostituire **[stringa di connessione dispositivo IoT]** con stringa di connessione hello dispositivo che si ottiene eseguendo hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` comando.</span><span class="sxs-lookup"><span data-stu-id="da1e9-147">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="da1e9-148">Sostituire **[stringa di connessione hub IoT]** con stringa di connessione hub IoT che si ottiene eseguendo hello hello `az iot hub show-connection-string --name {my hub name}` comando.</span><span class="sxs-lookup"><span data-stu-id="da1e9-148">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="da1e9-149">Distribuire ed eseguire l'applicazione di esempio hello</span><span class="sxs-lookup"><span data-stu-id="da1e9-149">Deploy and run hello sample application</span></span>
<span data-ttu-id="da1e9-150">Distribuire ed eseguire l'applicazione di esempio hello sulla Lavagna Arduino eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="da1e9-150">Deploy and run hello sample application on your Arduino board by running hello following commands:</span></span>

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="da1e9-151">comando gulp Hello distribuisce la Lavagna Arduino hello esempio applicazione tooyour.</span><span class="sxs-lookup"><span data-stu-id="da1e9-151">hello gulp command deploys hello sample application tooyour Arduino board.</span></span> <span data-ttu-id="da1e9-152">Quindi viene eseguita un'applicazione hello la Lavagna Arduino e un'attività separata nell'host della Lavagna di Arduino tooyour messaggi blink toosend 20 computer dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="da1e9-152">Then, it runs hello application on your Arduino board and a separate task on your host computer toosend 20 blink messages tooyour Arduino board from your IoT hub.</span></span>

<span data-ttu-id="da1e9-153">Quando si esegue l'applicazione di esempio hello, avvia l'ascolto toomessages dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="da1e9-153">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="da1e9-154">Nel frattempo, attività gulp hello invia messaggi di "blink" diversi dai tooyour hub IoT Arduino Lavagna.</span><span class="sxs-lookup"><span data-stu-id="da1e9-154">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooyour Arduino board.</span></span> <span data-ttu-id="da1e9-155">Per ogni messaggio blink hello Lavagna riceve, applicazione di esempio hello chiama hello `blinkLED` hello tooblink funzione LED.</span><span class="sxs-lookup"><span data-stu-id="da1e9-155">For each blink message that hello board receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="da1e9-156">Dovrebbe essere hello LED blink ogni due secondi, come attività gulp hello invia 20 messaggi dal tooyour hub IoT Arduino Lavagna.</span><span class="sxs-lookup"><span data-stu-id="da1e9-156">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooyour Arduino board.</span></span> <span data-ttu-id="da1e9-157">Hello ultimo uno è un messaggio "stop" che interrompe l'esecuzione di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="da1e9-157">hello last one is a "stop" message that stops hello application from running.</span></span>

![Applicazione di esempio con comando gulp e messaggi di lampeggiamento][sample-application]

## <a name="summary"></a><span data-ttu-id="da1e9-159">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="da1e9-159">Summary</span></span>
<span data-ttu-id="da1e9-160">I messaggi inviati correttamente dal hello della tooblink Lavagna di IoT hub tooyour Arduino LED.</span><span class="sxs-lookup"><span data-stu-id="da1e9-160">You’ve successfully sent messages from your IoT hub tooyour Arduino board tooblink hello LED.</span></span> <span data-ttu-id="da1e9-161">attività successiva Hello è facoltativo: modificare hello e disattivare il comportamento di hello LED.</span><span class="sxs-lookup"><span data-stu-id="da1e9-161">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da1e9-162">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="da1e9-162">Next steps</span></span>
<span data-ttu-id="da1e9-163">[Modificare hello e disattivare il comportamento di hello LED][change-the-on-and-off-led-behavior]</span><span class="sxs-lookup"><span data-stu-id="da1e9-163">[Change hello on and off behavior of hello LED][change-the-on-and-off-led-behavior]</span></span>


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