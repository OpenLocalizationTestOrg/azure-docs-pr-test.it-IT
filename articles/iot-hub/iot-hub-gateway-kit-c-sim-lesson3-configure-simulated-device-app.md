---
title: 'Dispositivo simulato e gateway Azure IoT: lezione 3: Eseguire l''app di esempio | Documentazione Microsoft'
description: Esecuzione di un dispositivo simulato esempio app toosend temperatura dati tooyour hub IoT
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: dati toocloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5d051d99-9749-4150-b3c8-573b0bda9c52
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: bc2c97919e95e4e3977a8b6ac75162bf2b5017be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a><span data-ttu-id="56ddc-104">Configurare ed eseguire un'app di esempio per dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="56ddc-104">Configure and run a simulated device sample app</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="56ddc-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="56ddc-105">What you will do</span></span>

- <span data-ttu-id="56ddc-106">Repository di esempio hello clone.</span><span class="sxs-lookup"><span data-stu-id="56ddc-106">Clone hello sample repository.</span></span>
- <span data-ttu-id="56ddc-107">Usare l'hub IoT e informazioni sul dispositivo logico hello Azure CLI tooget per l'applicazione di esempio dispositivo simulato.</span><span class="sxs-lookup"><span data-stu-id="56ddc-107">Use hello Azure CLI tooget your IoT hub and logical device information for simulated device sample application.</span></span> <span data-ttu-id="56ddc-108">Configurare ed eseguire l'applicazione di esempio dispositivo simulato hello.</span><span class="sxs-lookup"><span data-stu-id="56ddc-108">Configure and run hello simulated device sample application.</span></span>

<span data-ttu-id="56ddc-109">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="56ddc-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="56ddc-110">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="56ddc-110">What you will learn</span></span>

<span data-ttu-id="56ddc-111">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="56ddc-111">In this article, you will learn:</span></span>

- <span data-ttu-id="56ddc-112">Come tooconfigure e hello esecuzione simulate dell'applicazione di esempio di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="56ddc-112">How tooconfigure and run hello simulated device sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="56ddc-113">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="56ddc-113">What you need</span></span>

<span data-ttu-id="56ddc-114">È necessario aver completato:</span><span class="sxs-lookup"><span data-stu-id="56ddc-114">You must have successfully completed</span></span>

- [<span data-ttu-id="56ddc-115">Creare un hub IoT e registrare il dispositivo</span><span class="sxs-lookup"><span data-stu-id="56ddc-115">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a><span data-ttu-id="56ddc-116">Clonare il computer host toohello di hello esempio repository</span><span class="sxs-lookup"><span data-stu-id="56ddc-116">Clone hello sample repository toohello host computer</span></span>

<span data-ttu-id="56ddc-117">repository di esempio hello tooclone, seguire questi passaggi nel computer host hello:</span><span class="sxs-lookup"><span data-stu-id="56ddc-117">tooclone hello sample repository, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="56ddc-118">Aprire un prompt dei comandi in Windows o aprire un terminale in macOS o in Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="56ddc-118">Open a Command Prompt in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="56ddc-119">Eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="56ddc-119">Run hello following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-hello-simulated-device-and-your-nuc"></a><span data-ttu-id="56ddc-120">Configurare dispositivo simulato hello e il NUC</span><span class="sxs-lookup"><span data-stu-id="56ddc-120">Configure hello simulated device and your NUC</span></span>

1. <span data-ttu-id="56ddc-121">File di configurazione Open hello `config.json` nel codice di Visual Studio eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="56ddc-121">Open hello configuration file `config.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   code config.json
   ```

2. <span data-ttu-id="56ddc-122">Sostituire `"has_sensortag": true` con `"has_sensortag": false`.</span><span class="sxs-lookup"><span data-stu-id="56ddc-122">Replace `"has_sensortag": true` with `"has_sensortag": false`</span></span>

   ![Configurazione quando non si ha un dispositivo TI SensorTag](media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. <span data-ttu-id="56ddc-124">Inizializzare i file di configurazione hello eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="56ddc-124">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. <span data-ttu-id="56ddc-125">Aprire `config-gateway.json` nel codice di Visual Studio eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="56ddc-125">Open `config-gateway.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. <span data-ttu-id="56ddc-126">Individuare hello successiva riga di codice e sostituire `[device hostname or IP address]` con nome host o indirizzo IP di hello NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="56ddc-126">Locate hello following line of code and replace `[device hostname or IP address]` with IP address or host name of hello Intel NUC.</span></span>
   <span data-ttu-id="56ddc-127">![Screenshot del gateway di configurazione](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="56ddc-127">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

## <a name="get-hello-connection-string-of-your-iot-hub-logical-device"></a><span data-ttu-id="56ddc-128">Ottiene la stringa di connessione hello del dispositivo logico hub IoT</span><span class="sxs-lookup"><span data-stu-id="56ddc-128">Get hello connection string of your IoT hub logical device</span></span>

<span data-ttu-id="56ddc-129">hello tooget stringa di connessione hub IoT di Azure del dispositivo logico, eseguire hello comando nel computer host hello seguente:</span><span class="sxs-lookup"><span data-stu-id="56ddc-129">tooget hello Azure IoT hub connection string of your logical device, run hello following command on hello host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="56ddc-130">`{IoT hub name}`è nome dell'hub IoT hello utilizzato.</span><span class="sxs-lookup"><span data-stu-id="56ddc-130">`{IoT hub name}` is hello IoT hub name that you used.</span></span> <span data-ttu-id="56ddc-131">Usare iot-gateway come valore hello `{resource group name}` e utilizzare mydevice come valore hello `{device id}` se non si sono modificati valore hello nella lezione 2.</span><span class="sxs-lookup"><span data-stu-id="56ddc-131">Use iot-gateway as hello value of `{resource group name}` and use mydevice as hello value of `{device id}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="configure-hello-simulated-device-cloud-upload-sample-application"></a><span data-ttu-id="56ddc-132">Configurare applicazione di esempio caricamento cloud dispositivo simulato hello</span><span class="sxs-lookup"><span data-stu-id="56ddc-132">Configure hello simulated device cloud upload sample application</span></span>

<span data-ttu-id="56ddc-133">tooconfigure e hello esecuzione simulato dispositivo cloud caricare l'applicazione di esempio, seguire questi passaggi nel computer host hello:</span><span class="sxs-lookup"><span data-stu-id="56ddc-133">tooconfigure and run hello simulated device cloud upload sample application, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="56ddc-134">Aprire `config-sensortag.json` nel codice di Visual Studio eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="56ddc-134">Open `config-sensortag.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![Screenshot di SensorTag di configurazione](media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. <span data-ttu-id="56ddc-136">Apportare hello sostituzioni nel codice hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="56ddc-136">Make hello following replacements in hello code:</span></span>
   - <span data-ttu-id="56ddc-137">Sostituire `[IoT hub name]` con il nome dell'hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="56ddc-137">Replace `[IoT hub name]` with hello IoT hub name.</span></span>
   - <span data-ttu-id="56ddc-138">Sostituire `[IoT device connection string]` con la stringa di connessione hello del dispositivo logico hub IoT.</span><span class="sxs-lookup"><span data-stu-id="56ddc-138">Replace `[IoT device connection string]` with hello connection string of your IoT hub logical device.</span></span>

3. <span data-ttu-id="56ddc-139">Eseguire un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="56ddc-139">Run hello application.</span></span>

   <span data-ttu-id="56ddc-140">Distribuire ed eseguire un'applicazione hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="56ddc-140">Deploy and run hello application by running hello following command:</span></span>

   ```bash
   gulp run
   ```

## <a name="verify-hello-sample-application-works"></a><span data-ttu-id="56ddc-141">Verificare il funzionamento dell'applicazione di esempio hello</span><span class="sxs-lookup"><span data-stu-id="56ddc-141">Verify hello sample application works</span></span>

<span data-ttu-id="56ddc-142">Viene visualizzato l'output seguente hello:</span><span class="sxs-lookup"><span data-stu-id="56ddc-142">You should now see output like hello following:</span></span>

![Output dell'applicazione di esempio per il dispositivo simulato](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

<span data-ttu-id="56ddc-144">un'applicazione Hello invia temperatura dati tooyour IoT hub, che dura 40 secondi.</span><span class="sxs-lookup"><span data-stu-id="56ddc-144">hello application sends temperature data tooyour IoT hub, which lasts for 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="56ddc-145">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="56ddc-145">Summary</span></span>

<span data-ttu-id="56ddc-146">È stato configurato correttamente e hello esecuzione simulato dispositivo cloud caricamento applicazione di esempio invia l'hub IoT tooyour dati con dispositivo simulato.</span><span class="sxs-lookup"><span data-stu-id="56ddc-146">You've successfully configured and run hello simulated device cloud upload sample application which sends data tooyour IoT hub with simulated device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="56ddc-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="56ddc-147">Next steps</span></span>
[<span data-ttu-id="56ddc-148">Leggere messaggi dall'hub IoT</span><span class="sxs-lookup"><span data-stu-id="56ddc-148">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)