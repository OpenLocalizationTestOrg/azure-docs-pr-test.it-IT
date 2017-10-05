---
title: 'Connettere Raspberry Pi (Node) ad Azure IoT: lezione 3: Eseguire l''esempio | Documentazione Microsoft'
description: Distribuire ed eseguire un'applicazione di esempio nel dispositivo Raspberry Pi 3 che invia messaggi all'hub IoT e fa lampeggiare il LED.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: lampeggiamento led cloud pi, lampeggiamento led dal cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 427d8e5e-8af8-4249-8607-44edc90a4972
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1c03283ee276a954f822d6eca5f0a3d5f93ec64b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a><span data-ttu-id="5adee-104">Eseguire un'applicazione di esempio per inviare messaggi da dispositivo a cloud</span><span class="sxs-lookup"><span data-stu-id="5adee-104">Run a sample application to send device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="5adee-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="5adee-105">What you will do</span></span>
<span data-ttu-id="5adee-106">Questo articolo illustra come distribuire ed eseguire nel dispositivo Raspberry Pi 3 un'applicazione di esempio che invia messaggi all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5adee-106">This article will show you how to deploy and run a sample application on Raspberry Pi 3 that sends messages to your IoT hub.</span></span> <span data-ttu-id="5adee-107">In caso di problemi, cercare le soluzioni nella pagina sulla [risoluzione dei problemi](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="5adee-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5adee-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="5adee-108">What you will learn</span></span>
<span data-ttu-id="5adee-109">Si apprenderà come usare lo strumento gulp per distribuire ed eseguire l'applicazione Node.js di esempio nel dispositivo Pi.</span><span class="sxs-lookup"><span data-stu-id="5adee-109">You will learn how to use the gulp tool to deploy and run the sample Node.js application on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5adee-110">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="5adee-110">What you need</span></span>
* <span data-ttu-id="5adee-111">Prima di iniziare questa attività è necessario aver completato [Creare un'app per le funzioni di Azure e un account di archiviazione di Azure per elaborare e archiviare i messaggi dell'hub IoT](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="5adee-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="5adee-112">Ottenere le stringhe di connessione dell'hub IoT e del dispositivo</span><span class="sxs-lookup"><span data-stu-id="5adee-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="5adee-113">La stringa di connessione del dispositivo viene usata dal dispositivo Pi per connettersi all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5adee-113">The device connection string is used by your Pi to connect to your IoT hub.</span></span> <span data-ttu-id="5adee-114">La stringa di connessione dell'hub IoT viene usata per connettersi al registro delle identità nell'hub IoT per gestire i dispositivi che possono connettersi all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5adee-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span></span> 

* <span data-ttu-id="5adee-115">Elencare tutti gli hub IoT nel gruppo di risorse eseguendo questo comando dell'interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="5adee-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="5adee-116">Usare `iot-sample` come valore di `{resource group name}` se non si è modificato il valore.</span><span class="sxs-lookup"><span data-stu-id="5adee-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>

* <span data-ttu-id="5adee-117">Ottenere la stringa di connessione dell'hub IoT eseguendo il comando seguente dell'interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="5adee-117">Get the IoT hub connection string by running the following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

<span data-ttu-id="5adee-118">`{my hub name}` è il nome specificato quando è stato creato l'hub IoT ed è stato registrato il dispositivo Pi.</span><span class="sxs-lookup"><span data-stu-id="5adee-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered Pi.</span></span>

* <span data-ttu-id="5adee-119">Ottenere la stringa di connessione del dispositivo usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5adee-119">Get the device connection string by running the following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

<span data-ttu-id="5adee-120">Usare `myraspberrypi` come valore di `{device id}` se non si è modificato il valore.</span><span class="sxs-lookup"><span data-stu-id="5adee-120">Use `myraspberrypi` as the value of `{device id}` if you didn't change the value.</span></span>

## <a name="configure-the-device-connection"></a><span data-ttu-id="5adee-121">Configurare la connessione del dispositivo</span><span class="sxs-lookup"><span data-stu-id="5adee-121">Configure the device connection</span></span>
1. <span data-ttu-id="5adee-122">Inizializzare il file di configurazione usando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="5adee-122">Initialize the configuration file by running the following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```
2. <span data-ttu-id="5adee-123">Aprire il file di configurazione del dispositivo `config-raspberrypi.json` in Visual Studio Code usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5adee-123">Open the device configuration file `config-raspberrypi.json` in Visual Studio Code by running the following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
  
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
  
   ![config.json](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. <span data-ttu-id="5adee-125">Sostituire i valori seguenti nel file `config-raspberrypi.json`:</span><span class="sxs-lookup"><span data-stu-id="5adee-125">Make the following replacements in the `config-raspberrypi.json` file:</span></span>
   
   * <span data-ttu-id="5adee-126">Sostituire **[device hostname or IP address]** con l'indirizzo IP o il nome host del dispositivo ottenuto da `device-discovery-cli` o con il valore ereditato quando è stato configurato il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5adee-126">Replace **[device hostname or IP address]** with the device IP address or host name you got from `device-discovery-cli` or with the value inherited when you configured your device.</span></span>
   * <span data-ttu-id="5adee-127">Sostituire **[IoT device connection string]** con il valore di `device connection string` ottenuto.</span><span class="sxs-lookup"><span data-stu-id="5adee-127">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span></span>
   * <span data-ttu-id="5adee-128">Sostituire **[IoT hub connection string]** con il valore di `iot hub connection string` ottenuto.</span><span class="sxs-lookup"><span data-stu-id="5adee-128">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span></span>

<span data-ttu-id="5adee-129">Aggiornare il file `config-raspberrypi.json` per poter distribuire l'applicazione di esempio dal computer.</span><span class="sxs-lookup"><span data-stu-id="5adee-129">Update the `config-raspberrypi.json` file so that you can deploy the sample application from your computer.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="5adee-130">Distribuire ed eseguire l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="5adee-130">Deploy and run the sample application</span></span>
<span data-ttu-id="5adee-131">Distribuire ed eseguire l'applicazione di esempio nel dispositivo Pi eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="5adee-131">Deploy and run the sample application on Pi by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-the-sample-application-works"></a><span data-ttu-id="5adee-132">Verificare il funzionamento dell'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="5adee-132">Verify that the sample application works</span></span>
<span data-ttu-id="5adee-133">Il LED connesso al dispositivo Pi dovrebbe lampeggiare ogni due secondi.</span><span class="sxs-lookup"><span data-stu-id="5adee-133">You should see the LED that is connected to Pi blinking every two seconds.</span></span> <span data-ttu-id="5adee-134">Ogni volta che il LED lampeggia, l'applicazione di esempio invia un messaggio all'hub IoT e verifica se il messaggio è stato inviato all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5adee-134">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span></span> <span data-ttu-id="5adee-135">Ogni messaggio ricevuto dall'hub IoT viene stampato nella finestra della console.</span><span class="sxs-lookup"><span data-stu-id="5adee-135">In addition, each message received by the IoT hub is printed in the console window.</span></span> <span data-ttu-id="5adee-136">L'applicazione di esempio termina automaticamente dopo l'invio di 20 messaggi.</span><span class="sxs-lookup"><span data-stu-id="5adee-136">The sample application terminates automatically after sending 20 messages.</span></span>

![Applicazione di esempio con messaggi inviati e ricevuti](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run.png)

## <a name="summary"></a><span data-ttu-id="5adee-138">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="5adee-138">Summary</span></span>
<span data-ttu-id="5adee-139">È stata distribuita ed eseguita la nuova applicazione di esempio per il lampeggiamento nel dispositivo Pi per l'invio di messaggi da dispositivo a cloud all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5adee-139">You've deployed and run the new blink sample application on Pi to send device-to-cloud messages to your IoT hub.</span></span> <span data-ttu-id="5adee-140">È ora possibile monitorare i messaggi mentre vengono scritti nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5adee-140">You can now monitor your messages as they are written to the storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5adee-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5adee-141">Next steps</span></span>
[<span data-ttu-id="5adee-142">Leggere i messaggi con salvataggio permanente in Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="5adee-142">Read messages persisted in Azure Storage</span></span>](iot-hub-raspberry-pi-kit-node-lesson3-read-table-storage.md)

