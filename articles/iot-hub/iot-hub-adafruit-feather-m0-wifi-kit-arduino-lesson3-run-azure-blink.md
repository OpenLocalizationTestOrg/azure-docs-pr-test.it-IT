---
title: 'Connettere Arduino (C) ad Azure IoT: lezione 3: Eseguire l''esempio | Documentazione Microsoft'
description: Distribuire ed eseguire un'applicazione di esempio in Adafruit Feather M0 WiFi che invia messaggi all'hub IoT e fa lampeggiare il LED.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: servizio cloud iot, inviare dati al cloud con arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 92cce319-2b17-4c9b-889d-deac959e3e7c
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 0c17fe74dbd78abca955f7789a1674ed6333367f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a><span data-ttu-id="722df-104">Eseguire un'applicazione di esempio per inviare messaggi da dispositivo a cloud</span><span class="sxs-lookup"><span data-stu-id="722df-104">Run a sample application to send device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="722df-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="722df-105">What you will do</span></span>
<span data-ttu-id="722df-106">Questo articolo illustra come distribuire ed eseguire in una scheda Arduino Adafruit Feather M0 WiFi un'applicazione di esempio che invia messaggi all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="722df-106">This article will show you how to deploy and run a sample application on your Adafruit Feather M0 WiFi Arduino board that sends messages to your IoT hub.</span></span>

<span data-ttu-id="722df-107">In caso di problemi, cercare le soluzioni nella [pagina sulla risoluzione dei problemi][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="722df-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="722df-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="722df-108">What you will learn</span></span>
<span data-ttu-id="722df-109">Si apprenderà come usare lo strumento gulp per distribuire ed eseguire l'applicazione Arduino di esempio nella scheda Arduino.</span><span class="sxs-lookup"><span data-stu-id="722df-109">You will learn how to use the gulp tool to deploy and run the sample Arduino application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="722df-110">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="722df-110">What you need</span></span>
* <span data-ttu-id="722df-111">Prima di iniziare questa attività, è necessario aver completato [Creare un'app per le funzioni di Azure e un account di archiviazione di Azure per elaborare e archiviare i messaggi dell'hub IoT][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="722df-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="722df-112">Ottenere le stringhe di connessione dell'hub IoT e del dispositivo</span><span class="sxs-lookup"><span data-stu-id="722df-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="722df-113">La stringa di connessione del dispositivo viene usata per connettere la scheda Arduino all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="722df-113">The device connection string is used to connect your Arduino board to your IoT hub.</span></span> <span data-ttu-id="722df-114">La stringa di connessione dell'hub IoT viene usata per connettere l'hub IoT all'identità del dispositivo che rappresenta la scheda Arduino nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="722df-114">The IoT hub connection string is used to connect your IoT hub to the device identity that represents your Arduino board in the IoT hub.</span></span>

* <span data-ttu-id="722df-115">Elencare tutti gli hub IoT nel gruppo di risorse eseguendo il comando seguente dell'interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="722df-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="722df-116">Usare `iot-sample` come valore di `{resource group name}` se non si è modificato il valore.</span><span class="sxs-lookup"><span data-stu-id="722df-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>

* <span data-ttu-id="722df-117">Ottenere la stringa di connessione dell'hub IoT eseguendo il comando seguente dell'interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="722df-117">Get the IoT hub connection string by running the following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="722df-118">`{my hub name}` è il nome specificato quando è stato creato l'hub IoT ed è stata registrata la scheda Arduino.</span><span class="sxs-lookup"><span data-stu-id="722df-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered your Arduino board.</span></span>

* <span data-ttu-id="722df-119">Ottenere la stringa di connessione del dispositivo usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="722df-119">Get the device connection string by running the following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id mym0wifi
```

<span data-ttu-id="722df-120">Usare `mym0wifi` come valore di `{device id}` se non si è modificato il valore.</span><span class="sxs-lookup"><span data-stu-id="722df-120">Use `mym0wifi` as the value of `{device id}` if you didn't change the value.</span></span>
## <a name="configure-the-device-connection"></a><span data-ttu-id="722df-121">Configurare la connessione del dispositivo</span><span class="sxs-lookup"><span data-stu-id="722df-121">Configure the device connection</span></span>
<span data-ttu-id="722df-122">Per configurare la connessione al dispositivo, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="722df-122">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="722df-123">Ottenere la porta seriale del dispositivo usando l'interfaccia della riga di comando per l'individuazione del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="722df-123">Obtain the serial port of the device with the device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="722df-124">Verrà visualizzato un output simile al seguente e sarà rilevata la porta COM USB per la scheda Arduino:</span><span class="sxs-lookup"><span data-stu-id="722df-124">You should see an output that is similar to the following and find the usb COM port for your Arduino board:</span></span>

   ![Individuazione del dispositivo][device-discovery]

2. <span data-ttu-id="722df-126">Aprire il file `config.json` nella cartella della lezione e aggiungere il valore del numero della porta COM trovato:</span><span class="sxs-lookup"><span data-stu-id="722df-126">Open the file `config.json` in the lesson folder and add the value of the found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > <span data-ttu-id="722df-128">Per la porta COM, nella piattaforma Windows il formato è `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="722df-128">For the COM port, on Windows platform, it has the format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="722df-129">In macOS o Ubuntu inizia con `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="722df-129">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

3. <span data-ttu-id="722df-130">Inizializzare il file di configurazione usando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="722df-130">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   gulp install-tools
   ```
4. <span data-ttu-id="722df-131">Aprire il file di configurazione del dispositivo `config-arduino.json` in Visual Studio Code usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="722df-131">Open the device configuration file `config-arduino.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```

   ![config-arduino.json][config-arduino-json]

5. <span data-ttu-id="722df-133">Sostituire i valori seguenti nel file `config-arduino.json`:</span><span class="sxs-lookup"><span data-stu-id="722df-133">Make the following replacements in the `config-arduino.json` file:</span></span>

   * <span data-ttu-id="722df-134">Sostituire **[Wi-Fi SSID]** con il codice SSID Wi-Fi che ha eseguito la connessione a Internet.</span><span class="sxs-lookup"><span data-stu-id="722df-134">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected to the Internet.</span></span>
   * <span data-ttu-id="722df-135">Sostituire **[Wi-Fi password]** con la password Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="722df-135">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="722df-136">Rimuovere la stringa se il Wi-Fi non richiede la password.</span><span class="sxs-lookup"><span data-stu-id="722df-136">Remove the string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="722df-137">Sostituire **[IoT device connection string]** con il valore di `device connection string` ottenuto.</span><span class="sxs-lookup"><span data-stu-id="722df-137">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span></span>
   * <span data-ttu-id="722df-138">Sostituire **[IoT hub connection string]** con il valore di `iot hub connection string` ottenuto.</span><span class="sxs-lookup"><span data-stu-id="722df-138">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="722df-139">Non è necessario specificare `azure_storage_connection_string` in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="722df-139">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="722df-140">Mantenerlo invariato.</span><span class="sxs-lookup"><span data-stu-id="722df-140">Keep it as is.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="722df-141">Distribuire ed eseguire l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="722df-141">Deploy and run the sample application</span></span>
<span data-ttu-id="722df-142">Distribuire ed eseguire l'applicazione di esempio nella scheda Arduino usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="722df-142">Deploy and run the sample application on your Arduino board by running the following command:</span></span>

```bash
gulp run
# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

> [!NOTE]
> <span data-ttu-id="722df-143">L'attività gulp predefinita esegue le attività `install-tools` e `run` in sequenza.</span><span class="sxs-lookup"><span data-stu-id="722df-143">The default gulp task runs `install-tools` and `run` tasks sequentially.</span></span> <span data-ttu-id="722df-144">Quando [è stata distribuita l'app per il lampeggiamento][deployed-the-blink-app], queste attività sono state eseguite separatamente.</span><span class="sxs-lookup"><span data-stu-id="722df-144">When you [deployed the blink app][deployed-the-blink-app], you ran these tasks separately.</span></span>

## <a name="verify-that-the-sample-application-works"></a><span data-ttu-id="722df-145">Verificare il funzionamento dell'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="722df-145">Verify that the sample application works</span></span>
<span data-ttu-id="722df-146">Il LED sulla scheda n. 0 dell'interfaccia GPIO dovrebbe lampeggiare ogni due secondi.</span><span class="sxs-lookup"><span data-stu-id="722df-146">You should see the GPIO #0 on-board LED blinking every two seconds.</span></span> <span data-ttu-id="722df-147">Ogni volta che il LED lampeggia, l'applicazione di esempio invia un messaggio all'hub IoT e verifica se il messaggio è stato inviato all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="722df-147">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span></span> <span data-ttu-id="722df-148">Ogni messaggio ricevuto dall'hub IoT viene stampato nella finestra della console.</span><span class="sxs-lookup"><span data-stu-id="722df-148">In addition, each message received by the IoT hub is printed in the console window.</span></span> <span data-ttu-id="722df-149">L'applicazione di esempio termina automaticamente dopo l'invio di 20 messaggi.</span><span class="sxs-lookup"><span data-stu-id="722df-149">The sample application terminates automatically after sending 20 messages.</span></span>

![Applicazione di esempio con messaggi inviati e ricevuti][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="722df-151">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="722df-151">Summary</span></span>
<span data-ttu-id="722df-152">È stata distribuita ed eseguita la nuova applicazione di esempio per il lampeggiamento nella scheda Arduino per l'invio di messaggi da dispositivo a cloud all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="722df-152">You've deployed and run the new blink sample application on your Arduino board to send device-to-cloud messages to your IoT hub.</span></span> <span data-ttu-id="722df-153">È ora possibile monitorare i messaggi mentre vengono scritti nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="722df-153">You now monitor your messages as they are written to the storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="722df-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="722df-154">Next steps</span></span>
<span data-ttu-id="722df-155">[Leggere i messaggi con salvataggio permanente in Archiviazione di Azure][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="722df-155">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/config-arduino.png
[deployed-the-blink-app]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_run_arduino.png
[read-messages-persisted-in-azure-storage]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-read-table-storage.md