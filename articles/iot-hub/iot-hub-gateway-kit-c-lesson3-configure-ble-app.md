---
title: 'Dispositivo SensorTag e gateway Azure IoT: lezione 3: Eseguire l''app di esempio | Documentazione Microsoft'
description: Eseguire dati tooreceive di applicazione di esempio BILITA da BILITA SensorTag e dall'hub IoT.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Disattiva app sensore monitoraggio dell'app, la raccolta dei dati del sensore, dati da sensori, sensore dati toocloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: b33e53a1-1df7-4412-ade1-45185aec5bef
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4a8acdeadd402ffc82d3b766e1ec03a77ddcebb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-ble-sample-application"></a><span data-ttu-id="5b1d6-104">Configurare ed eseguire un'applicazione di esempio BLE</span><span class="sxs-lookup"><span data-stu-id="5b1d6-104">Configure and run a BLE sample application</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="5b1d6-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="5b1d6-105">What you will do</span></span>

- <span data-ttu-id="5b1d6-106">Repository di esempio hello clone.</span><span class="sxs-lookup"><span data-stu-id="5b1d6-106">Clone hello sample repository.</span></span> 
- <span data-ttu-id="5b1d6-107">Configurare la connettività di hello tra SensorTag e NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="5b1d6-107">Set up hello connectivity between SensorTag and Intel NUC.</span></span> 
- <span data-ttu-id="5b1d6-108">Usare l'hub IoT e informazioni SensorTag hello Azure CLI tooget per un'applicazione di esempio BILITA (Bluetooth consumo energetico).</span><span class="sxs-lookup"><span data-stu-id="5b1d6-108">Use hello Azure CLI tooget your IoT hub and SensorTag information for a BLE(Bluetooth Low Energy) sample application.</span></span> <span data-ttu-id="5b1d6-109">E configurare ed eseguire l'applicazione di esempio BILITA hello.</span><span class="sxs-lookup"><span data-stu-id="5b1d6-109">And configure and run hello BLE sample application.</span></span> 

<span data-ttu-id="5b1d6-110">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="5b1d6-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5b1d6-111">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="5b1d6-111">What you will learn</span></span>

<span data-ttu-id="5b1d6-112">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="5b1d6-112">In this article, you will learn:</span></span>

- <span data-ttu-id="5b1d6-113">Come tooconfigure e hello esecuzione Disattiva applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="5b1d6-113">How tooconfigure and run hello BLE sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5b1d6-114">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="5b1d6-114">What you need</span></span>

<span data-ttu-id="5b1d6-115">È necessario aver completato:</span><span class="sxs-lookup"><span data-stu-id="5b1d6-115">You must have successfully completed</span></span>

- <span data-ttu-id="5b1d6-116">[Create an IoT hub and register SensorTag](iot-hub-gateway-kit-c-lesson2-register-device.md) (Creare un hub IoT e registrare SensorTag)</span><span class="sxs-lookup"><span data-stu-id="5b1d6-116">[Create an IoT hub and register SensorTag](iot-hub-gateway-kit-c-lesson2-register-device.md)</span></span>

## <a name="clone-hello-sample-repository-toohello-host-computer"></a><span data-ttu-id="5b1d6-117">Clonare il computer host toohello di hello esempio repository</span><span class="sxs-lookup"><span data-stu-id="5b1d6-117">Clone hello sample repository toohello host computer</span></span>

<span data-ttu-id="5b1d6-118">repository di esempio hello tooclone, seguire questi passaggi nel computer host hello:</span><span class="sxs-lookup"><span data-stu-id="5b1d6-118">tooclone hello sample repository, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="5b1d6-119">Aprire una finestra del prompt dei comandi in Windows o aprire un terminale in macOS o in Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="5b1d6-119">Open a Command Prompt window in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="5b1d6-120">Eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="5b1d6-120">Run hello following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="set-up-hello-connectivity-between-sensortag-and-intel-nuc"></a><span data-ttu-id="5b1d6-121">Configurare la connettività di hello tra SensorTag e Intel NUC</span><span class="sxs-lookup"><span data-stu-id="5b1d6-121">Set up hello connectivity between SensorTag and Intel NUC</span></span>

<span data-ttu-id="5b1d6-122">tooset della connettività di hello, seguire questi passaggi nel computer host hello:</span><span class="sxs-lookup"><span data-stu-id="5b1d6-122">tooset up hello connectivity, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="5b1d6-123">Inizializzare i file di configurazione hello eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="5b1d6-123">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

2. <span data-ttu-id="5b1d6-124">Aprire `config-gateway.json` nel codice di Visual Studio eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5b1d6-124">Open `config-gateway.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

3. <span data-ttu-id="5b1d6-125">Individuare hello successiva riga di codice e sostituire `[device hostname or IP address]` con hello IP indirizzo o il nome host di NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="5b1d6-125">Locate hello following line of code and replace `[device hostname or IP address]` with hello IP address or host name of Intel NUC.</span></span>
   <span data-ttu-id="5b1d6-126">![Screenshot del gateway di configurazione](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="5b1d6-126">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

4. <span data-ttu-id="5b1d6-127">Installare gli strumenti di supporto su Intel NUC eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5b1d6-127">Install helper tools on Intel NUC by running hello following command:</span></span>

   ```bash
   gulp install-tools
   ```

5. <span data-ttu-id="5b1d6-128">Attivare SensorTag premendo il pulsante di alimentazione hello come immagine hello e hello che dovrebbe lampeggiare LED verde.</span><span class="sxs-lookup"><span data-stu-id="5b1d6-128">Turn on SensorTag by pressing hello power button as hello following picture, and hello green LED should blink.</span></span>

   ![Accendere SensorTag](media/iot-hub-gateway-kit-lessons/lesson3/turn on_off sensortag.jpg)

6. <span data-ttu-id="5b1d6-130">Analizza i dispositivi SensorTag eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="5b1d6-130">Scan SensorTag devices by running hello following commands:</span></span>

   ```bash
   gulp discover-sensortag
   ```

7. <span data-ttu-id="5b1d6-131">Testare la connettività hello hello SensorTag e Intel NUC eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5b1d6-131">Test hello connectivity between hello SensorTag and Intel NUC by running hello following command:</span></span>

   ```bash
   gulp test-connectivity --mac {mac address}
   ```

   <span data-ttu-id="5b1d6-132">Sostituire `{mac address}` con indirizzo MAC ottenuto nel passaggio precedente hello hello.</span><span class="sxs-lookup"><span data-stu-id="5b1d6-132">Replace `{mac address}` with hello MAC address that you obtained in hello previous step.</span></span>

## <a name="get-hello-connection-string-of-sensortag"></a><span data-ttu-id="5b1d6-133">Ottiene la stringa di connessione hello di SensorTag</span><span class="sxs-lookup"><span data-stu-id="5b1d6-133">Get hello connection string of SensorTag</span></span>

<span data-ttu-id="5b1d6-134">hello tooget stringa di connessione hub IoT di Azure di SensorTag, eseguire hello comando nel computer host hello seguente:</span><span class="sxs-lookup"><span data-stu-id="5b1d6-134">tooget hello Azure IoT hub connection string of SensorTag, run hello following command on hello host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="5b1d6-135">`{IoT hub name}`è nome dell'hub IoT hello utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5b1d6-135">`{IoT hub name}` is hello IoT hub name that you used.</span></span> <span data-ttu-id="5b1d6-136">Usare iot-gateway come valore hello `{resource group name}` e utilizzare mydevice come valore hello `{device id}` se non si sono modificati valore hello nella lezione 2.</span><span class="sxs-lookup"><span data-stu-id="5b1d6-136">Use iot-gateway as hello value of `{resource group name}` and use mydevice as hello value of `{device id}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="configure-hello-ble-sample-application"></a><span data-ttu-id="5b1d6-137">Configurare l'applicazione di esempio BILITA hello</span><span class="sxs-lookup"><span data-stu-id="5b1d6-137">Configure hello BLE sample application</span></span>

<span data-ttu-id="5b1d6-138">tooconfigure e hello esecuzione applicazione di esempio BILITA, seguire questi passaggi nel computer host hello:</span><span class="sxs-lookup"><span data-stu-id="5b1d6-138">tooconfigure and run hello BLE sample application, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="5b1d6-139">Aprire `config-sensortag.json` nel codice di Visual Studio eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5b1d6-139">Open `config-sensortag.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![Screenshot di SensorTag di configurazione](media/iot-hub-gateway-kit-lessons/lesson3/config_sensortag.png)

2. <span data-ttu-id="5b1d6-141">Apportare hello sostituzioni nel codice hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="5b1d6-141">Make hello following replacements in hello code:</span></span>
   - <span data-ttu-id="5b1d6-142">Sostituire `[IoT hub name]` con nome dell'hub IoT hello utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5b1d6-142">Replace `[IoT hub name]` with hello IoT hub name that you used.</span></span>
   - <span data-ttu-id="5b1d6-143">Sostituire `[IoT device connection string]` con la stringa di connessione hello di SensorTag ottenuto.</span><span class="sxs-lookup"><span data-stu-id="5b1d6-143">Replace `[IoT device connection string]` with hello connection string of SensorTag that you obtained.</span></span>
   - <span data-ttu-id="5b1d6-144">Sostituire `[device_mac_address]` con indirizzo MAC di hello SensorTag ottenuto hello.</span><span class="sxs-lookup"><span data-stu-id="5b1d6-144">Replace `[device_mac_address]` with hello MAC address of hello SensorTag that you obtained.</span></span>

3. <span data-ttu-id="5b1d6-145">Eseguire l'applicazione di esempio BILITA hello.</span><span class="sxs-lookup"><span data-stu-id="5b1d6-145">Run hello BLE sample application.</span></span>

   <span data-ttu-id="5b1d6-146">hello toorun applicazione di esempio BILITA, seguire questi passaggi nel computer host hello:</span><span class="sxs-lookup"><span data-stu-id="5b1d6-146">toorun hello BLE sample application, follow these steps on hello host computer:</span></span>

   1. <span data-ttu-id="5b1d6-147">Accendere SensorTag.</span><span class="sxs-lookup"><span data-stu-id="5b1d6-147">Turn on SensorTag.</span></span>

   2. <span data-ttu-id="5b1d6-148">Distribuire ed eseguire l'applicazione di esempio hello BILITA Intel NUC eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5b1d6-148">Deploy and run hello BLE sample application on Intel NUC by running hello following command:</span></span>
   
      ```bash
      gulp run
      ```

## <a name="verify-that-hello-ble-sample-application-works"></a><span data-ttu-id="5b1d6-149">Verificare il funzionamento dell'applicazione di esempio BILITA hello</span><span class="sxs-lookup"><span data-stu-id="5b1d6-149">Verify that hello BLE sample application works</span></span>

<span data-ttu-id="5b1d6-150">Viene visualizzato un output simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="5b1d6-150">You should now see an output like hello following:</span></span>

![Output dell'applicazione di esempio BLE](media/iot-hub-gateway-kit-lessons/lesson3/BLE_running.png)

<span data-ttu-id="5b1d6-152">applicazione di esempio Hello mantiene la raccolta dei dati di temperatura e lo ha inviato l'hub IoT tooyour.</span><span class="sxs-lookup"><span data-stu-id="5b1d6-152">hello sample application keeps collecting temperature data and sent it tooyour IoT hub.</span></span> <span data-ttu-id="5b1d6-153">applicazione di esempio Hello termina automaticamente dopo l'invio di 40 secondi.</span><span class="sxs-lookup"><span data-stu-id="5b1d6-153">hello sample application terminates automatically after sending 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="5b1d6-154">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="5b1d6-154">Summary</span></span>

<span data-ttu-id="5b1d6-155">Siano correttamente configurare la connettività di hello tra SensorTag e Intel NUC ed eseguire un'applicazione di esempio BILITA che raccoglie e invia i dati da SensorTag tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="5b1d6-155">You've successfully set up hello connectivity between SensorTag and Intel NUC, and run a BLE sample application which collects and sends data from SensorTag tooyour IoT hub.</span></span> <span data-ttu-id="5b1d6-156">Si è pronti toolearn come tooverify che ha ricevuto l'hub IoT hello dati.</span><span class="sxs-lookup"><span data-stu-id="5b1d6-156">You're ready toolearn how tooverify that your IoT hub has received hello data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b1d6-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5b1d6-157">Next steps</span></span>
[<span data-ttu-id="5b1d6-158">Leggere messaggi dall'hub IoT</span><span class="sxs-lookup"><span data-stu-id="5b1d6-158">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)