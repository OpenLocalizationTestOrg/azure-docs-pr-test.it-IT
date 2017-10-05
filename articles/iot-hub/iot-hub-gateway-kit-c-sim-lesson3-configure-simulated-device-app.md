---
title: 'Dispositivo simulato e gateway Azure IoT: lezione 3: Eseguire l''app di esempio | Documentazione Microsoft'
description: Eseguire un'app di esempio per dispositivo simulato per inviare dati sulla temperatura all'hub IoT
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: dati al cloud
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
ms.openlocfilehash: 7df2d730c38a9f715e0fd57b4d436724a5727760
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a><span data-ttu-id="3596a-104">Configurare ed eseguire un'app di esempio per dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="3596a-104">Configure and run a simulated device sample app</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="3596a-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="3596a-105">What you will do</span></span>

- <span data-ttu-id="3596a-106">Clonare il repository di esempio.</span><span class="sxs-lookup"><span data-stu-id="3596a-106">Clone the sample repository.</span></span>
- <span data-ttu-id="3596a-107">Usare l'interfaccia della riga di comando di Azure per ottenere informazioni sull'hub IoT e sul dispositivo logico per l'applicazione di esempio per il dispositivo simulato.</span><span class="sxs-lookup"><span data-stu-id="3596a-107">Use the Azure CLI to get your IoT hub and logical device information for simulated device sample application.</span></span> <span data-ttu-id="3596a-108">Configurare ed eseguire l'applicazione di esempio per il dispositivo simulato.</span><span class="sxs-lookup"><span data-stu-id="3596a-108">Configure and run the simulated device sample application.</span></span>

<span data-ttu-id="3596a-109">In caso di problemi, cercare le soluzioni nella pagina sulla [risoluzione dei problemi](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="3596a-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="3596a-110">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="3596a-110">What you will learn</span></span>

<span data-ttu-id="3596a-111">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="3596a-111">In this article, you will learn:</span></span>

- <span data-ttu-id="3596a-112">Come configurare ed eseguire l'applicazione di esempio per il dispositivo simulato.</span><span class="sxs-lookup"><span data-stu-id="3596a-112">How to configure and run the simulated device sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3596a-113">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="3596a-113">What you need</span></span>

<span data-ttu-id="3596a-114">È necessario aver completato:</span><span class="sxs-lookup"><span data-stu-id="3596a-114">You must have successfully completed</span></span>

- [<span data-ttu-id="3596a-115">Creare un hub IoT e registrare il dispositivo</span><span class="sxs-lookup"><span data-stu-id="3596a-115">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="clone-the-sample-repository-to-the-host-computer"></a><span data-ttu-id="3596a-116">Clonare il repository di esempio nel computer host</span><span class="sxs-lookup"><span data-stu-id="3596a-116">Clone the sample repository to the host computer</span></span>

<span data-ttu-id="3596a-117">Per clonare il repository di esempio, seguire questa procedura nel computer host:</span><span class="sxs-lookup"><span data-stu-id="3596a-117">To clone the sample repository, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="3596a-118">Aprire un prompt dei comandi in Windows o aprire un terminale in macOS o in Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="3596a-118">Open a Command Prompt in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="3596a-119">Eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3596a-119">Run the following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-the-simulated-device-and-your-nuc"></a><span data-ttu-id="3596a-120">Configurare il dispositivo simulato e NUC</span><span class="sxs-lookup"><span data-stu-id="3596a-120">Configure the simulated device and your NUC</span></span>

1. <span data-ttu-id="3596a-121">Aprire il file di configurazione `config.json` in Visual Studio Code usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="3596a-121">Open the configuration file `config.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   code config.json
   ```

2. <span data-ttu-id="3596a-122">Sostituire `"has_sensortag": true` con `"has_sensortag": false`.</span><span class="sxs-lookup"><span data-stu-id="3596a-122">Replace `"has_sensortag": true` with `"has_sensortag": false`</span></span>

   ![Configurazione quando non si ha un dispositivo TI SensorTag](media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. <span data-ttu-id="3596a-124">Inizializzare il file di configurazione usando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3596a-124">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. <span data-ttu-id="3596a-125">Aprire `config-gateway.json` in Visual Studio Code usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="3596a-125">Open `config-gateway.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. <span data-ttu-id="3596a-126">Trovare la riga di codice seguente e sostituire `[device hostname or IP address]` con l'indirizzo IP o il nome host di Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="3596a-126">Locate the following line of code and replace `[device hostname or IP address]` with IP address or host name of the Intel NUC.</span></span>
   <span data-ttu-id="3596a-127">![Screenshot del gateway di configurazione](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="3596a-127">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

## <a name="get-the-connection-string-of-your-iot-hub-logical-device"></a><span data-ttu-id="3596a-128">Ottenere la stringa di connessione per il dispositivo logico dell'hub IoT</span><span class="sxs-lookup"><span data-stu-id="3596a-128">Get the connection string of your IoT hub logical device</span></span>

<span data-ttu-id="3596a-129">Per ottenere la stringa di connessione dell'hub IoT di Azure per il dispositivo logico, usare questo comando nel computer host:</span><span class="sxs-lookup"><span data-stu-id="3596a-129">To get the Azure IoT hub connection string of your logical device, run the following command on the host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="3596a-130">`{IoT hub name}` è il nome dell'hub IoT usato.</span><span class="sxs-lookup"><span data-stu-id="3596a-130">`{IoT hub name}` is the IoT hub name that you used.</span></span> <span data-ttu-id="3596a-131">Usare iot-gateway come valore di `{resource group name}` e mydevice come valore di `{device id}` se nella lezione 2 non si è modificato il valore.</span><span class="sxs-lookup"><span data-stu-id="3596a-131">Use iot-gateway as the value of `{resource group name}` and use mydevice as the value of `{device id}` if you didn't change the value in Lesson 2.</span></span>

## <a name="configure-the-simulated-device-cloud-upload-sample-application"></a><span data-ttu-id="3596a-132">Configurare l'applicazione di esempio di caricamento nel cloud per il dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="3596a-132">Configure the simulated device cloud upload sample application</span></span>

<span data-ttu-id="3596a-133">Per configurare ed eseguire l'applicazione di esempio di caricamento nel cloud per il dispositivo simulato, seguire questa procedura nel computer host:</span><span class="sxs-lookup"><span data-stu-id="3596a-133">To configure and run the simulated device cloud upload sample application, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="3596a-134">Aprire `config-sensortag.json` in Visual Studio Code usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="3596a-134">Open `config-sensortag.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![Screenshot di SensorTag di configurazione](media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. <span data-ttu-id="3596a-136">Sostituire i valori seguenti nel codice:</span><span class="sxs-lookup"><span data-stu-id="3596a-136">Make the following replacements in the code:</span></span>
   - <span data-ttu-id="3596a-137">Sostituire `[IoT hub name]` con il nome dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="3596a-137">Replace `[IoT hub name]` with the IoT hub name.</span></span>
   - <span data-ttu-id="3596a-138">Sostituire `[IoT device connection string]` con la stringa di connessione per il dispositivo logico dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="3596a-138">Replace `[IoT device connection string]` with the connection string of your IoT hub logical device.</span></span>

3. <span data-ttu-id="3596a-139">Eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3596a-139">Run the application.</span></span>

   <span data-ttu-id="3596a-140">Distribuire ed eseguire l'applicazione eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="3596a-140">Deploy and run the application by running the following command:</span></span>

   ```bash
   gulp run
   ```

## <a name="verify-the-sample-application-works"></a><span data-ttu-id="3596a-141">Verificare il funzionamento dell'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="3596a-141">Verify the sample application works</span></span>

<span data-ttu-id="3596a-142">Verrà ora visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="3596a-142">You should now see output like the following:</span></span>

![Output dell'applicazione di esempio per il dispositivo simulato](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

<span data-ttu-id="3596a-144">L'applicazione invia i dati sulla temperatura all'hub IoT per 40 secondi.</span><span class="sxs-lookup"><span data-stu-id="3596a-144">The application sends temperature data to your IoT hub, which lasts for 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="3596a-145">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="3596a-145">Summary</span></span>

<span data-ttu-id="3596a-146">È stata configurata ed eseguita l'applicazione di esempio di caricamento nel cloud dal dispositivo simulato, che invia i dati all'hub IoT con il dispositivo simulato.</span><span class="sxs-lookup"><span data-stu-id="3596a-146">You've successfully configured and run the simulated device cloud upload sample application which sends data to your IoT hub with simulated device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3596a-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3596a-147">Next steps</span></span>
[<span data-ttu-id="3596a-148">Leggere messaggi dall'hub IoT</span><span class="sxs-lookup"><span data-stu-id="3596a-148">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)