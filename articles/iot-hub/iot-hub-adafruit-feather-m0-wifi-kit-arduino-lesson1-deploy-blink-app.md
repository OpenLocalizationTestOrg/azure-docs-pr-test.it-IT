---
title: 'Connettersi Arduino tooAzure IoT - lezione 1: distribuire app | Documenti Microsoft'
description: Clonazione di un'applicazione hello esempio Arduino da GitHub ed eseguire gulp toodeploy questo tooyour applicazione Adafruit sfumatura M0 WiFi. Questa applicazione di esempio lampeggia hello GPIO
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: progetti led arduino, lampeggiamento led arduino, codice di lampeggiamento led arduino, programma di lampeggiamento arduino, esempio di lampeggiamento arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: b0a7d076-d580-4686-9f7d-c0712750b615
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5bf8e4ae88e070aeacf34bfc43b8d2daeeb1a2fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="dfb87-105">Creare e distribuire un'applicazione hello blink</span><span class="sxs-lookup"><span data-stu-id="dfb87-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="dfb87-106">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="dfb87-106">What you will do</span></span>
<span data-ttu-id="dfb87-107">Clonazione di un'applicazione hello esempio Arduino da GitHub e utilizzare hello gulp strumento toodeploy hello esempio applicazione tooyour Adafruit sfumatura M0 Wi-Fi Arduino Lavagna.</span><span class="sxs-lookup"><span data-stu-id="dfb87-107">Clone hello sample Arduino application from GitHub, and use hello gulp tool toodeploy hello sample application tooyour Adafruit Feather M0 WiFi Arduino board.</span></span> <span data-ttu-id="dfb87-108">applicazione di esempio Hello, hello intermittenze GPIO #13 barod LED ogni due secondi.</span><span class="sxs-lookup"><span data-stu-id="dfb87-108">hello sample application blinks hello GPIO #13 on-barod LED every two seconds.</span></span>

<span data-ttu-id="dfb87-109">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina][troubleshooting-page].</span><span class="sxs-lookup"><span data-stu-id="dfb87-109">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting-page].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="dfb87-110">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="dfb87-110">What you will learn</span></span>
* <span data-ttu-id="dfb87-111">Come toodeploy e hello esecuzione applicazione sulla Lavagna Arduino di esempio.</span><span class="sxs-lookup"><span data-stu-id="dfb87-111">How toodeploy and run hello sample application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="dfb87-112">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="dfb87-112">What you need</span></span>
<span data-ttu-id="dfb87-113">È necessario che sia completata hello seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="dfb87-113">You must have successfully completed hello following operations:</span></span>

* <span data-ttu-id="dfb87-114">[Configurare il dispositivo][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="dfb87-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="dfb87-115">[Ottenere strumenti hello][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="dfb87-115">[Get hello tools][get-the-tools]</span></span>

## <a name="open-hello-sample-application"></a><span data-ttu-id="dfb87-116">Applicazione di esempio hello aperto</span><span class="sxs-lookup"><span data-stu-id="dfb87-116">Open hello sample application</span></span>
<span data-ttu-id="dfb87-117">hello tooopen applicazione di esempio, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="dfb87-117">tooopen hello sample application, follow these steps:</span></span>

1. <span data-ttu-id="dfb87-118">Clonare il repository di esempio hello da GitHub eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="dfb87-118">Clone hello sample repository from GitHub by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-feather-m0-getting-started.git
   ```
2. <span data-ttu-id="dfb87-119">Aprire l'applicazione di esempio hello in Visual Studio Code eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="dfb87-119">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd iot-hub-c-feather-m0-getting-started
   cd Lesson1
   code .
   ```

   ![Struttura del repository][repo-structure]

<span data-ttu-id="dfb87-121">Hello `app.ino` file hello `app` sottocartella è hello i file di origine della chiave che contiene hello codice toocontrol hello LED.</span><span class="sxs-lookup"><span data-stu-id="dfb87-121">hello `app.ino` file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="dfb87-122">Installare le dipendenze dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="dfb87-122">Install application dependencies</span></span>
<span data-ttu-id="dfb87-123">Installare le librerie di hello e altri moduli, che è necessario per l'applicazione di esempio hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="dfb87-123">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="dfb87-124">Configurare una connessione al dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="dfb87-124">Configure hello device connection</span></span>
<span data-ttu-id="dfb87-125">tooconfigure hello connessione al dispositivo, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="dfb87-125">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="dfb87-126">Ottenere della porta seriale del dispositivo hello con hello dispositivo individuazione cli hello:</span><span class="sxs-lookup"><span data-stu-id="dfb87-126">Obtain hello serial port of hello device with hello device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="dfb87-127">Si dovrebbe vedere un output simile toohello seguenti e si trova hello usb porta COM per la scheda Arduino: ![individuazione dei dispositivi][device-discovery]</span><span class="sxs-lookup"><span data-stu-id="dfb87-127">You should see an output that is similar toohello following and find hello usb COM port for your Arduino board: ![Device discovery][device-discovery]</span></span>

2. <span data-ttu-id="dfb87-128">File aperti hello `config.json` in hello cartella lezione e aggiungere valore hello hello trovato numero di porta COM:</span><span class="sxs-lookup"><span data-stu-id="dfb87-128">Open hello file `config.json` in hello lesson folder and add hello value of hello found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```
   ![config.json][config-json]
   > [!NOTE]
   > <span data-ttu-id="dfb87-130">Per la porta COM hello, sulla piattaforma Windows, ha il formato di hello di `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="dfb87-130">For hello COM port, on Windows platform, it has hello format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="dfb87-131">In macOS o Ubuntu inizia con `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="dfb87-131">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="dfb87-132">Distribuire ed eseguire l'applicazione di esempio hello</span><span class="sxs-lookup"><span data-stu-id="dfb87-132">Deploy and run hello sample application</span></span>
### <a name="install-hello-required-tools-for-your-arduino-board"></a><span data-ttu-id="dfb87-133">Installare gli strumenti di hello necessario per la scheda Arduino</span><span class="sxs-lookup"><span data-stu-id="dfb87-133">Install hello required tools for your Arduino board</span></span>

<span data-ttu-id="dfb87-134">Installare hello Hub IoT di Azure SDK per la scheda Arduino eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="dfb87-134">Install hello Azure IoT Hub SDK for your Arduino board by running hello following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="dfb87-135">Questa operazione potrebbe richiedere un toocomplete molto tempo, a seconda della connessione di rete.</span><span class="sxs-lookup"><span data-stu-id="dfb87-135">This task might take a long time toocomplete, depending on your network connection.</span></span>

> [!NOTE]
> <span data-ttu-id="dfb87-136">Uscire da hello in esecuzione l'istanza Arduino IDE esecuzione attività gulp: `install-tools`, `run`.</span><span class="sxs-lookup"><span data-stu-id="dfb87-136">Please exit hello running Arduino IDE instance when running gulp tasks: `install-tools`, `run`.</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="dfb87-137">Distribuire ed eseguire app di esempio hello</span><span class="sxs-lookup"><span data-stu-id="dfb87-137">Deploy and run hello sample app</span></span>
<span data-ttu-id="dfb87-138">Distribuire ed eseguire l'applicazione di esempio hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="dfb87-138">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp run

# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="dfb87-139">Verificare il funzionamento dell'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="dfb87-139">Verify hello app works</span></span>
<span data-ttu-id="dfb87-140">Se non viene visualizzato hello LED è lampeggiante, vedere hello [risoluzione dei problemi guida] [ troubleshooting-page] per soluzioni ai problemi di toocommon.</span><span class="sxs-lookup"><span data-stu-id="dfb87-140">If you don’t see hello LED blinking, see hello [troubleshooting guide][troubleshooting-page] for solutions toocommon problems.</span></span>

![LED lampeggiante][led-blinking]

## <a name="summary"></a><span data-ttu-id="dfb87-142">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="dfb87-142">Summary</span></span>
<span data-ttu-id="dfb87-143">È stato installato toowork strumenti hello richiesto con la scheda Arduino e distribuito un hello della tooblink Lavagna di esempio applicazione tooyour Arduino LED.</span><span class="sxs-lookup"><span data-stu-id="dfb87-143">You've installed hello required tools toowork with your Arduino board and deployed a sample application tooyour Arduino board tooblink hello LED.</span></span> <span data-ttu-id="dfb87-144">È ora possibile creare, distribuire e l'esecuzione di un'altra applicazione di esempio che si connette il tooAzure Lavagna Arduino toosend IoT Hub e ricevere messaggi.</span><span class="sxs-lookup"><span data-stu-id="dfb87-144">You can now create, deploy, and run another sample application that connects your Arduino board tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dfb87-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dfb87-145">Next steps</span></span>
<span data-ttu-id="dfb87-146">[Ottenere hello gli strumenti di Azure][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="dfb87-146">[Get hello Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting-page]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-blink-arduino-mac.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[led-blinking]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md