---
title: 'Dispositivo SensorTag e gateway Azure IoT: lezione 3: Leggere i messaggi | Documentazione Microsoft'
description: Eseguire un codice di esempio sul computer host per leggere i messaggi dall'hub IoT.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: dati nel cloud, raccolta dati nel cloud, servizio cloud iot, dati iot
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cc88be24-b5c0-4ef2-ba21-4e8f77f3e167
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 45f3595c4848d5c283cdf95604adf8d2c8d6a809
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="5678a-104">Leggere i messaggi dall'hub IoT</span><span class="sxs-lookup"><span data-stu-id="5678a-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="5678a-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="5678a-105">What you will do</span></span>

- <span data-ttu-id="5678a-106">Eseguire il codice di esempio sul computer host per leggere i messaggi dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5678a-106">Run sample code on your host computer to read messages from your IoT hub.</span></span>

<span data-ttu-id="5678a-107">In caso di problemi, cercare le soluzioni nella pagina sulla [risoluzione dei problemi](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="5678a-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5678a-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="5678a-108">What you will learn</span></span>

<span data-ttu-id="5678a-109">Come usare lo strumento gulp per leggere i messaggi dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5678a-109">How to use the gulp tool to read messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5678a-110">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="5678a-110">What you need</span></span>

- <span data-ttu-id="5678a-111">L'applicazione di esempio BLE eseguita nella lezione 3.</span><span class="sxs-lookup"><span data-stu-id="5678a-111">The BLE sample application that you ran successfully in Lesson 3.</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="5678a-112">Ottenere le stringhe di connessione dell'hub IoT e del dispositivo</span><span class="sxs-lookup"><span data-stu-id="5678a-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="5678a-113">La stringa di connessione del dispositivo viene usata dal dispositivo (TI SensorTag o dispositivo simulato) per la connessione all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5678a-113">The device connection string is used by your device (TI SensorTag or simulated device) to connect to your IoT hub.</span></span> <span data-ttu-id="5678a-114">La stringa di connessione all'hub IoT viene usata per la connessione al registro di identità nell'hub IoT per gestire i dispositivi a cui è consentito connettersi all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5678a-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span></span>

- <span data-ttu-id="5678a-115">Elencare tutti gli hub IoT nel gruppo di risorse usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5678a-115">List all your IoT hubs in your resource group by running the following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="5678a-116">Usare `iot-gateway` come valore di `{resource group name}` se non si è modificato il valore.</span><span class="sxs-lookup"><span data-stu-id="5678a-116">Use `iot-gateway` as the value of `{resource group name}` if you didn't change the value.</span></span>
- <span data-ttu-id="5678a-117">Ottenere la stringa di connessione all'hub IoT usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5678a-117">Get the IoT hub connection string by running the following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="5678a-118">`{my hub name}` è il nome specificato nella lezione 2.</span><span class="sxs-lookup"><span data-stu-id="5678a-118">`{my hub name}` is the name that you specified in Lesson 2.</span></span>

## <a name="configure-the-device-connection-for-the-sample-code"></a><span data-ttu-id="5678a-119">Configurare la connessione al dispositivo per il codice di esempio.</span><span class="sxs-lookup"><span data-stu-id="5678a-119">Configure the device connection for the sample code</span></span>

<span data-ttu-id="5678a-120">Aggiornare il file di configurazione del dispositivo `config-azure.json` per poter leggere i messaggi dall'hub IoT nel computer host.</span><span class="sxs-lookup"><span data-stu-id="5678a-120">Update the device configuration file `config-azure.json` so that you can read messages from your IoT hub on your host computer.</span></span> <span data-ttu-id="5678a-121">A questo scopo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="5678a-121">To do this, follow these steps:</span></span>

1. <span data-ttu-id="5678a-122">Aprire `config-azure.json` in Visual Studio Code usando il comando seguente in una finestra della console:</span><span class="sxs-lookup"><span data-stu-id="5678a-122">Open `config-azure.json` in Visual Studio Code by running the following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="5678a-123">Sostituire i valori seguenti nel file `config-azure.json`:</span><span class="sxs-lookup"><span data-stu-id="5678a-123">Make the following replacements in the `config-azure.json` file:</span></span>

   ![Screenshot della configurazione di Azure](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="5678a-125">Sostituire `[IoT hub connection string]` con la stringa di connessione all'hub IoT ottenuta.</span><span class="sxs-lookup"><span data-stu-id="5678a-125">Replace `[IoT hub connection string]` with the IoT hub connection string that you obtained.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="5678a-126">Leggere messaggi dall'hub IoT</span><span class="sxs-lookup"><span data-stu-id="5678a-126">Read messages from your IoT hub</span></span>

<span data-ttu-id="5678a-127">Se si ha un dispositivo TI SensorTag, verificare di averlo già acceso.</span><span class="sxs-lookup"><span data-stu-id="5678a-127">If you have a TI SensorTag, make sure you have already powered on your SensorTag.</span></span> <span data-ttu-id="5678a-128">Eseguire l'applicazione di esempio gateway e leggere i messaggi dell'hub IoT usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5678a-128">Run the gateway sample application and read IoT Hub messages by the following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="5678a-129">Il commando esegue l'applicazione di esempio BLE che legge e comprime i dati sulla temperatura da SensorTag o dal dispositivo simulato e invia il messaggio all'hub IoT ogni 2 secondi.</span><span class="sxs-lookup"><span data-stu-id="5678a-129">The command runs the BLE sample application that reads and packages temperature data from your SensorTag or simulated device and sends the message to your IoT hub every 2 seconds.</span></span> <span data-ttu-id="5678a-130">Genera anche un processo figlio per ricevere il messaggio.</span><span class="sxs-lookup"><span data-stu-id="5678a-130">It also spawns a child process to receive the message.</span></span>

<span data-ttu-id="5678a-131">I messaggi inviati e ricevuti vengono visualizzati tutti immediatamente nella stessa finestra della console nel computer host.</span><span class="sxs-lookup"><span data-stu-id="5678a-131">The messages that are being sent and received are all displayed instantly on the same console window in the host machine.</span></span> <span data-ttu-id="5678a-132">L'istanza dell'applicazione di esempio terminerà automaticamente in 40 secondi.</span><span class="sxs-lookup"><span data-stu-id="5678a-132">The sample application instance will terminate automatically in 40 seconds.</span></span>

![Applicazione di esempio BLE con messaggi inviati e ricevuti](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub.png)

## <a name="summary"></a><span data-ttu-id="5678a-134">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="5678a-134">Summary</span></span>

<span data-ttu-id="5678a-135">È stato eseguito un codice di esempio per leggere i messaggi dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5678a-135">You've run a sample code to read messages from your IoT hub.</span></span> <span data-ttu-id="5678a-136">Ora è possibile leggere i messaggi salvati nell'archivio tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="5678a-136">You're ready to read the messages that are stored in your Azure table storage.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5678a-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5678a-137">Next steps</span></span>
[<span data-ttu-id="5678a-138">Creare un'app per le funzioni di Azure e un account di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="5678a-138">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)


