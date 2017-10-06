---
title: 'Connect Arduino (C) tooAzure IoT - lezione 3: eseguire l''esempio | Documenti Microsoft'
description: Distribuire ed eseguire un tooAdafruit di applicazione di esempio sfumatura M0 Wi-Fi che invia l'hub IoT tooyour messaggi e lampeggia hello LED.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: servizio cloud IOT, arduino inviare dati toocloud
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
ms.openlocfilehash: ddca015a3655f8a1a9de2a00e718ec0d28a5affb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a><span data-ttu-id="1604f-104">Eseguire un toosend di applicazione di esempio i messaggi da dispositivo a cloud</span><span class="sxs-lookup"><span data-stu-id="1604f-104">Run a sample application toosend device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="1604f-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="1604f-105">What you will do</span></span>
<span data-ttu-id="1604f-106">In questo articolo verrà illustrato come toodeploy ed eseguire un'applicazione di esempio nel Wi-Fi Arduino di Adafruit sfumatura M0 board tale hub IoT tooyour di Invia messaggi.</span><span class="sxs-lookup"><span data-stu-id="1604f-106">This article will show you how toodeploy and run a sample application on your Adafruit Feather M0 WiFi Arduino board that sends messages tooyour IoT hub.</span></span>

<span data-ttu-id="1604f-107">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="1604f-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="1604f-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="1604f-108">What you will learn</span></span>
<span data-ttu-id="1604f-109">Si apprenderà come hello toouse gulp toodeploy strumento e l'esecuzione di un'applicazione hello esempio Arduino sulla Lavagna Arduino.</span><span class="sxs-lookup"><span data-stu-id="1604f-109">You will learn how toouse hello gulp tool toodeploy and run hello sample Arduino application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="1604f-110">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="1604f-110">What you need</span></span>
* <span data-ttu-id="1604f-111">Prima di iniziare questa attività, è necessario che sia completata [creare un'app di Azure (funzione) e un hub IoT tooprocess e l'archivio del account di archiviazione messaggi][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="1604f-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="1604f-112">Ottenere le stringhe di connessione dell'hub IoT e del dispositivo</span><span class="sxs-lookup"><span data-stu-id="1604f-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="1604f-113">stringa di connessione dispositivo Hello è tooconnect usato l'hub IoT tooyour di Arduino Lavagna.</span><span class="sxs-lookup"><span data-stu-id="1604f-113">hello device connection string is used tooconnect your Arduino board tooyour IoT hub.</span></span> <span data-ttu-id="1604f-114">stringa di connessione hub IoT Hello è usato tooconnect IoT hub toohello dispositivo identità che rappresenta il Arduino board nell'hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="1604f-114">hello IoT hub connection string is used tooconnect your IoT hub toohello device identity that represents your Arduino board in hello IoT hub.</span></span>

* <span data-ttu-id="1604f-115">Elencare tutti gli hub IoT nel gruppo di risorse eseguendo il comando CLI di Azure seguente hello:</span><span class="sxs-lookup"><span data-stu-id="1604f-115">List all your IoT hubs in your resource group by running hello following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="1604f-116">Utilizzare `iot-sample` come valore hello `{resource group name}` se non si sono modificati valore hello.</span><span class="sxs-lookup"><span data-stu-id="1604f-116">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>

* <span data-ttu-id="1604f-117">Ottenere una stringa di connessione hub IoT hello eseguendo hello comando CLI di Azure seguente:</span><span class="sxs-lookup"><span data-stu-id="1604f-117">Get hello IoT hub connection string by running hello following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="1604f-118">`{my hub name}`è il nome hello è specificato durante la creazione dell'hub IoT e la Lavagna Arduino registrato.</span><span class="sxs-lookup"><span data-stu-id="1604f-118">`{my hub name}` is hello name that you specified when you created your IoT hub and registered your Arduino board.</span></span>

* <span data-ttu-id="1604f-119">Ottenere una stringa di connessione del dispositivo hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1604f-119">Get hello device connection string by running hello following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id mym0wifi
```

<span data-ttu-id="1604f-120">Utilizzare `mym0wifi` come valore hello `{device id}` se non si sono modificati valore hello.</span><span class="sxs-lookup"><span data-stu-id="1604f-120">Use `mym0wifi` as hello value of `{device id}` if you didn't change hello value.</span></span>
## <a name="configure-hello-device-connection"></a><span data-ttu-id="1604f-121">Configurare una connessione al dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="1604f-121">Configure hello device connection</span></span>
<span data-ttu-id="1604f-122">tooconfigure hello connessione al dispositivo, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="1604f-122">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="1604f-123">Ottenere della porta seriale del dispositivo hello con hello dispositivo individuazione cli hello:</span><span class="sxs-lookup"><span data-stu-id="1604f-123">Obtain hello serial port of hello device with hello device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="1604f-124">Si dovrebbe vedere un output simile toohello seguente e trovare hello usb porta COM per la scheda Arduino:</span><span class="sxs-lookup"><span data-stu-id="1604f-124">You should see an output that is similar toohello following and find hello usb COM port for your Arduino board:</span></span>

   ![Individuazione del dispositivo][device-discovery]

2. <span data-ttu-id="1604f-126">File aperti hello `config.json` in hello cartella lezione e aggiungere valore hello hello trovato numero di porta COM:</span><span class="sxs-lookup"><span data-stu-id="1604f-126">Open hello file `config.json` in hello lesson folder and add hello value of hello found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > <span data-ttu-id="1604f-128">Per la porta COM hello, sulla piattaforma Windows, ha il formato di hello di `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="1604f-128">For hello COM port, on Windows platform, it has hello format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="1604f-129">In macOS o Ubuntu inizia con `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="1604f-129">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

3. <span data-ttu-id="1604f-130">Inizializzare i file di configurazione hello eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="1604f-130">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   gulp install-tools
   ```
4. <span data-ttu-id="1604f-131">File di configurazione dispositivo aprire hello `config-arduino.json` nel codice di Visual Studio eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1604f-131">Open hello device configuration file `config-arduino.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```

   ![config-arduino.json][config-arduino-json]

5. <span data-ttu-id="1604f-133">Rendere hello seguenti sostituzioni hello `config-arduino.json` file:</span><span class="sxs-lookup"><span data-stu-id="1604f-133">Make hello following replacements in hello `config-arduino.json` file:</span></span>

   * <span data-ttu-id="1604f-134">Sostituire **[Wi-Fi SSID]** con il SSID Wi-Fi che è connesso a Internet toohello.</span><span class="sxs-lookup"><span data-stu-id="1604f-134">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected toohello Internet.</span></span>
   * <span data-ttu-id="1604f-135">Sostituire **[Wi-Fi password]** con la password Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="1604f-135">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="1604f-136">Rimuovere la stringa hello se il Wi-Fi non richiede una password.</span><span class="sxs-lookup"><span data-stu-id="1604f-136">Remove hello string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="1604f-137">Sostituire **[stringa di connessione dispositivo IoT]** con hello `device connection string` ottenute.</span><span class="sxs-lookup"><span data-stu-id="1604f-137">Replace **[IoT device connection string]** with hello `device connection string` you obtained.</span></span>
   * <span data-ttu-id="1604f-138">Sostituire **[stringa di connessione hub IoT]** con hello `iot hub connection string` ottenute.</span><span class="sxs-lookup"><span data-stu-id="1604f-138">Replace **[IoT hub connection string]** with hello `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1604f-139">Non è necessario specificare `azure_storage_connection_string` in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="1604f-139">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="1604f-140">Mantenerlo invariato.</span><span class="sxs-lookup"><span data-stu-id="1604f-140">Keep it as is.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="1604f-141">Distribuire ed eseguire l'applicazione di esempio hello</span><span class="sxs-lookup"><span data-stu-id="1604f-141">Deploy and run hello sample application</span></span>
<span data-ttu-id="1604f-142">Distribuire ed eseguire l'applicazione di esempio hello sulla Lavagna Arduino eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1604f-142">Deploy and run hello sample application on your Arduino board by running hello following command:</span></span>

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

> [!NOTE]
> <span data-ttu-id="1604f-143">Hello predefinito gulp attività viene eseguita `install-tools` e `run` in sequenza le attività.</span><span class="sxs-lookup"><span data-stu-id="1604f-143">hello default gulp task runs `install-tools` and `run` tasks sequentially.</span></span> <span data-ttu-id="1604f-144">Quando si [hello blink app distribuita][deployed-the-blink-app], è stato eseguito queste operazioni separatamente.</span><span class="sxs-lookup"><span data-stu-id="1604f-144">When you [deployed hello blink app][deployed-the-blink-app], you ran these tasks separately.</span></span>

## <a name="verify-that-hello-sample-application-works"></a><span data-ttu-id="1604f-145">Verificare il funzionamento dell'applicazione di esempio hello</span><span class="sxs-lookup"><span data-stu-id="1604f-145">Verify that hello sample application works</span></span>
<span data-ttu-id="1604f-146">Dovrebbe essere hello GPIO #0 incorporata e LED lampeggia ogni due secondi.</span><span class="sxs-lookup"><span data-stu-id="1604f-146">You should see hello GPIO #0 on-board LED blinking every two seconds.</span></span> <span data-ttu-id="1604f-147">Ogni volta che hello LED è lampeggiante, applicazione di esempio hello invia un hub IoT tooyour di messaggio e verifica che il messaggio hello è stato inviato correttamente tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="1604f-147">Every time hello LED blinks, hello sample application sends a message tooyour IoT hub and verifies that hello message has been successfully sent tooyour IoT hub.</span></span> <span data-ttu-id="1604f-148">Inoltre, ogni messaggio ricevuto dall'hub IoT hello viene stampato nella finestra di console hello.</span><span class="sxs-lookup"><span data-stu-id="1604f-148">In addition, each message received by hello IoT hub is printed in hello console window.</span></span> <span data-ttu-id="1604f-149">applicazione di esempio Hello termina automaticamente dopo l'invio di 20 messaggi.</span><span class="sxs-lookup"><span data-stu-id="1604f-149">hello sample application terminates automatically after sending 20 messages.</span></span>

![Applicazione di esempio con messaggi inviati e ricevuti][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="1604f-151">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="1604f-151">Summary</span></span>
<span data-ttu-id="1604f-152">È stato distribuito ed eseguito nuova applicazione di esempio blink hello in IoT hub di Arduino Lavagna toosend messaggi da dispositivo a cloud tooyour.</span><span class="sxs-lookup"><span data-stu-id="1604f-152">You've deployed and run hello new blink sample application on your Arduino board toosend device-to-cloud messages tooyour IoT hub.</span></span> <span data-ttu-id="1604f-153">È ora possibile monitorare i messaggi quando vengono scritti toohello account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1604f-153">You now monitor your messages as they are written toohello storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1604f-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1604f-154">Next steps</span></span>
<span data-ttu-id="1604f-155">[Leggere i messaggi con salvataggio permanente in Archiviazione di Azure][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="1604f-155">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/config-arduino.png
[deployed-the-blink-app]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_run_arduino.png
[read-messages-persisted-in-azure-storage]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-read-table-storage.md