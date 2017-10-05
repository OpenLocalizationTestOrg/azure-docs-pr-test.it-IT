---
title: 'Dispositivo SensorTag e gateway Azure IoT: lezione 3: Eseguire l''app di esempio | Documentazione Microsoft'
description: Eseguire un'applicazione di esempio BLE per ricevere dati da SensorTag BLE e dall'hub IoT.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: app BLE, app di monitoraggio dei sensori, raccolta di dati dei sensori, dati dai sensori, dai dati dei sensori al cloud
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
ms.openlocfilehash: f6fa158dbe1d48be7d493efa6217e1e0a759d2f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-run-a-ble-sample-application"></a><span data-ttu-id="8f17b-104">Configurare ed eseguire un'applicazione di esempio BLE</span><span class="sxs-lookup"><span data-stu-id="8f17b-104">Configure and run a BLE sample application</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="8f17b-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="8f17b-105">What you will do</span></span>

- <span data-ttu-id="8f17b-106">Clonare il repository di esempio.</span><span class="sxs-lookup"><span data-stu-id="8f17b-106">Clone the sample repository.</span></span> 
- <span data-ttu-id="8f17b-107">Configurare la connettività tra SensorTag e Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="8f17b-107">Set up the connectivity between SensorTag and Intel NUC.</span></span> 
- <span data-ttu-id="8f17b-108">Usare l'interfaccia della riga di comando di Azure per ottenere informazioni dall'hub IoT e da SensorTag per un'applicazione di esempio BLE (Bluetooth Low Energy).</span><span class="sxs-lookup"><span data-stu-id="8f17b-108">Use the Azure CLI to get your IoT hub and SensorTag information for a BLE(Bluetooth Low Energy) sample application.</span></span> <span data-ttu-id="8f17b-109">Configurare ed eseguire l'applicazione di esempio BLE.</span><span class="sxs-lookup"><span data-stu-id="8f17b-109">And configure and run the BLE sample application.</span></span> 

<span data-ttu-id="8f17b-110">In caso di problemi, cercare le soluzioni nella pagina sulla [risoluzione dei problemi](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="8f17b-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="8f17b-111">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="8f17b-111">What you will learn</span></span>

<span data-ttu-id="8f17b-112">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="8f17b-112">In this article, you will learn:</span></span>

- <span data-ttu-id="8f17b-113">Come configurare ed eseguire l'applicazione di esempio BLE.</span><span class="sxs-lookup"><span data-stu-id="8f17b-113">How to configure and run the BLE sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8f17b-114">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="8f17b-114">What you need</span></span>

<span data-ttu-id="8f17b-115">È necessario aver completato:</span><span class="sxs-lookup"><span data-stu-id="8f17b-115">You must have successfully completed</span></span>

- <span data-ttu-id="8f17b-116">[Create an IoT hub and register SensorTag](iot-hub-gateway-kit-c-lesson2-register-device.md) (Creare un hub IoT e registrare SensorTag)</span><span class="sxs-lookup"><span data-stu-id="8f17b-116">[Create an IoT hub and register SensorTag](iot-hub-gateway-kit-c-lesson2-register-device.md)</span></span>

## <a name="clone-the-sample-repository-to-the-host-computer"></a><span data-ttu-id="8f17b-117">Clonare il repository di esempio nel computer host</span><span class="sxs-lookup"><span data-stu-id="8f17b-117">Clone the sample repository to the host computer</span></span>

<span data-ttu-id="8f17b-118">Per clonare il repository di esempio, seguire questa procedura nel computer host:</span><span class="sxs-lookup"><span data-stu-id="8f17b-118">To clone the sample repository, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="8f17b-119">Aprire una finestra del prompt dei comandi in Windows o aprire un terminale in macOS o in Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="8f17b-119">Open a Command Prompt window in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="8f17b-120">Eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8f17b-120">Run the following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="set-up-the-connectivity-between-sensortag-and-intel-nuc"></a><span data-ttu-id="8f17b-121">Configurare la connettività tra SensorTag e Intel NUC</span><span class="sxs-lookup"><span data-stu-id="8f17b-121">Set up the connectivity between SensorTag and Intel NUC</span></span>

<span data-ttu-id="8f17b-122">Per configurare la connettività, seguire questa procedura nel computer host:</span><span class="sxs-lookup"><span data-stu-id="8f17b-122">To set up the connectivity, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="8f17b-123">Inizializzare il file di configurazione usando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8f17b-123">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

2. <span data-ttu-id="8f17b-124">Aprire `config-gateway.json` in Visual Studio Code usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8f17b-124">Open `config-gateway.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

3. <span data-ttu-id="8f17b-125">Trovare la riga di codice seguente e sostituire `[device hostname or IP address]` con l'indirizzo IP o il nome host di Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="8f17b-125">Locate the following line of code and replace `[device hostname or IP address]` with the IP address or host name of Intel NUC.</span></span>
   <span data-ttu-id="8f17b-126">![Screenshot del gateway di configurazione](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="8f17b-126">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

4. <span data-ttu-id="8f17b-127">Installare gli strumenti helper in Intel NUC usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8f17b-127">Install helper tools on Intel NUC by running the following command:</span></span>

   ```bash
   gulp install-tools
   ```

5. <span data-ttu-id="8f17b-128">Accendere SensorTag premendo il pulsante di alimentazione, come nell'immagine seguente. Il LED verde inizierà a lampeggiare.</span><span class="sxs-lookup"><span data-stu-id="8f17b-128">Turn on SensorTag by pressing the power button as the following picture, and the green LED should blink.</span></span>

   ![Accendere SensorTag](media/iot-hub-gateway-kit-lessons/lesson3/turn on_off sensortag.jpg)

6. <span data-ttu-id="8f17b-130">Analizzare i dispositivi SensorTag usando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8f17b-130">Scan SensorTag devices by running the following commands:</span></span>

   ```bash
   gulp discover-sensortag
   ```

7. <span data-ttu-id="8f17b-131">Testare la connettività tra SensorTag e Intel NUC usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8f17b-131">Test the connectivity between the SensorTag and Intel NUC by running the following command:</span></span>

   ```bash
   gulp test-connectivity --mac {mac address}
   ```

   <span data-ttu-id="8f17b-132">Sostituire `{mac address}` con l'indirizzo MAC ottenuto nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="8f17b-132">Replace `{mac address}` with the MAC address that you obtained in the previous step.</span></span>

## <a name="get-the-connection-string-of-sensortag"></a><span data-ttu-id="8f17b-133">Ottenere la stringa di connessione di SensorTag</span><span class="sxs-lookup"><span data-stu-id="8f17b-133">Get the connection string of SensorTag</span></span>

<span data-ttu-id="8f17b-134">Per ottenere la stringa di connessione dell'hub IoT di Azure per SensorTag, usare questo comando nel computer host:</span><span class="sxs-lookup"><span data-stu-id="8f17b-134">To get the Azure IoT hub connection string of SensorTag, run the following command on the host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="8f17b-135">`{IoT hub name}` è il nome dell'hub IoT usato.</span><span class="sxs-lookup"><span data-stu-id="8f17b-135">`{IoT hub name}` is the IoT hub name that you used.</span></span> <span data-ttu-id="8f17b-136">Usare iot-gateway come valore di `{resource group name}` e mydevice come valore di `{device id}` se nella lezione 2 non si è modificato il valore.</span><span class="sxs-lookup"><span data-stu-id="8f17b-136">Use iot-gateway as the value of `{resource group name}` and use mydevice as the value of `{device id}` if you didn't change the value in Lesson 2.</span></span>

## <a name="configure-the-ble-sample-application"></a><span data-ttu-id="8f17b-137">Configurare l'applicazione di esempio BLE</span><span class="sxs-lookup"><span data-stu-id="8f17b-137">Configure the BLE sample application</span></span>

<span data-ttu-id="8f17b-138">Per configurare ed eseguire l'applicazione di esempio BLE, seguire questa procedura nel computer host:</span><span class="sxs-lookup"><span data-stu-id="8f17b-138">To configure and run the BLE sample application, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="8f17b-139">Aprire `config-sensortag.json` in Visual Studio Code usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8f17b-139">Open `config-sensortag.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![Screenshot di SensorTag di configurazione](media/iot-hub-gateway-kit-lessons/lesson3/config_sensortag.png)

2. <span data-ttu-id="8f17b-141">Sostituire i valori seguenti nel codice:</span><span class="sxs-lookup"><span data-stu-id="8f17b-141">Make the following replacements in the code:</span></span>
   - <span data-ttu-id="8f17b-142">Sostituire `[IoT hub name]` con il nome dell'hub IoT usato.</span><span class="sxs-lookup"><span data-stu-id="8f17b-142">Replace `[IoT hub name]` with the IoT hub name that you used.</span></span>
   - <span data-ttu-id="8f17b-143">Sostituire `[IoT device connection string]` con la stringa di connessione di SensorTag ottenuta.</span><span class="sxs-lookup"><span data-stu-id="8f17b-143">Replace `[IoT device connection string]` with the connection string of SensorTag that you obtained.</span></span>
   - <span data-ttu-id="8f17b-144">Sostituire `[device_mac_address]` con l'indirizzo MAC di SensorTag ottenuto.</span><span class="sxs-lookup"><span data-stu-id="8f17b-144">Replace `[device_mac_address]` with the MAC address of the SensorTag that you obtained.</span></span>

3. <span data-ttu-id="8f17b-145">Eseguire l'applicazione di esempio BLE.</span><span class="sxs-lookup"><span data-stu-id="8f17b-145">Run the BLE sample application.</span></span>

   <span data-ttu-id="8f17b-146">Per eseguire l'applicazione di esempio BLE, seguire questa procedura nel computer host:</span><span class="sxs-lookup"><span data-stu-id="8f17b-146">To run the BLE sample application, follow these steps on the host computer:</span></span>

   1. <span data-ttu-id="8f17b-147">Accendere SensorTag.</span><span class="sxs-lookup"><span data-stu-id="8f17b-147">Turn on SensorTag.</span></span>

   2. <span data-ttu-id="8f17b-148">Distribuire ed eseguire l'applicazione di esempio BLE in Intel NUC usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8f17b-148">Deploy and run the BLE sample application on Intel NUC by running the following command:</span></span>
   
      ```bash
      gulp run
      ```

## <a name="verify-that-the-ble-sample-application-works"></a><span data-ttu-id="8f17b-149">Verificare il funzionamento dell'applicazione di esempio BLE</span><span class="sxs-lookup"><span data-stu-id="8f17b-149">Verify that the BLE sample application works</span></span>

<span data-ttu-id="8f17b-150">Verrà ora visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="8f17b-150">You should now see an output like the following:</span></span>

![Output dell'applicazione di esempio BLE](media/iot-hub-gateway-kit-lessons/lesson3/BLE_running.png)

<span data-ttu-id="8f17b-152">L'applicazione di esempio continua a raccogliere dati sulla temperatura e li invia all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8f17b-152">The sample application keeps collecting temperature data and sent it to your IoT hub.</span></span> <span data-ttu-id="8f17b-153">L'applicazione di esempio termina automaticamente dopo 40 secondi di invio.</span><span class="sxs-lookup"><span data-stu-id="8f17b-153">The sample application terminates automatically after sending 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="8f17b-154">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="8f17b-154">Summary</span></span>

<span data-ttu-id="8f17b-155">È stata configurata la connettività tra SensorTag e Intel NUC ed è stata eseguita un'applicazione di esempio BLE che raccoglie e invia dati da SensorTag all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8f17b-155">You've successfully set up the connectivity between SensorTag and Intel NUC, and run a BLE sample application which collects and sends data from SensorTag to your IoT hub.</span></span> <span data-ttu-id="8f17b-156">Ora è possibile passare all'esercitazione che illustra come verificare che l'hub IoT abbia ricevuto i dati.</span><span class="sxs-lookup"><span data-stu-id="8f17b-156">You're ready to learn how to verify that your IoT hub has received the data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f17b-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8f17b-157">Next steps</span></span>
[<span data-ttu-id="8f17b-158">Leggere messaggi dall'hub IoT</span><span class="sxs-lookup"><span data-stu-id="8f17b-158">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)