---
title: 'Dispositivo SensorTag e gateway Azure IoT: lezione 3: Leggere i messaggi | Documentazione Microsoft'
description: Eseguire un codice di esempio nei messaggi di hello tooread computer host dall'hub IoT.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: dati nel cloud hello, la raccolta dei dati cloud, servizio cloud iot, iot dati
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
ms.openlocfilehash: d3ffbe2e83f9d61c0088b8876a7f0eea62c1fbe1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="def56-104">Leggere messaggi dall'hub IoT</span><span class="sxs-lookup"><span data-stu-id="def56-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="def56-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="def56-105">What you will do</span></span>

- <span data-ttu-id="def56-106">Eseguire il codice di esempio nell'host computer tooread messaggi dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="def56-106">Run sample code on your host computer tooread messages from your IoT hub.</span></span>

<span data-ttu-id="def56-107">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="def56-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="def56-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="def56-108">What you will learn</span></span>

<span data-ttu-id="def56-109">Come toouse hello gulp messaggi tooread strumento dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="def56-109">How toouse hello gulp tool tooread messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="def56-110">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="def56-110">What you need</span></span>

- <span data-ttu-id="def56-111">applicazione di esempio di tabella che è stato eseguito correttamente nella lezione 3 Hello.</span><span class="sxs-lookup"><span data-stu-id="def56-111">hello BLE sample application that you ran successfully in Lesson 3.</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="def56-112">Ottenere le stringhe di connessione dell'hub IoT e del dispositivo</span><span class="sxs-lookup"><span data-stu-id="def56-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="def56-113">stringa di connessione del dispositivo Hello viene utilizzato per l'hub IoT tooyour tooconnect il dispositivo (TI SensorTag o dispositivo simulato).</span><span class="sxs-lookup"><span data-stu-id="def56-113">hello device connection string is used by your device (TI SensorTag or simulated device) tooconnect tooyour IoT hub.</span></span> <span data-ttu-id="def56-114">stringa di connessione hub IoT Hello è usato tooconnect toohello identità nel Registro di sistema i dispositivi IoT hub toomanage hello consentiti tooconnect tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="def56-114">hello IoT hub connection string is used tooconnect toohello identity registry in your IoT hub toomanage hello devices that are allowed tooconnect tooyour IoT hub.</span></span>

- <span data-ttu-id="def56-115">Elencare tutti gli hub IoT nel gruppo di risorse eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="def56-115">List all your IoT hubs in your resource group by running hello following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="def56-116">Utilizzare `iot-gateway` come valore hello `{resource group name}` se non si sono modificati valore hello.</span><span class="sxs-lookup"><span data-stu-id="def56-116">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change hello value.</span></span>
- <span data-ttu-id="def56-117">Ottenere una stringa di connessione hub IoT hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="def56-117">Get hello IoT hub connection string by running hello following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="def56-118">`{my hub name}`è il nome hello specificato nella lezione 2.</span><span class="sxs-lookup"><span data-stu-id="def56-118">`{my hub name}` is hello name that you specified in Lesson 2.</span></span>

## <a name="configure-hello-device-connection-for-hello-sample-code"></a><span data-ttu-id="def56-119">Configurare la connessione di hello dispositivo per il codice di esempio hello</span><span class="sxs-lookup"><span data-stu-id="def56-119">Configure hello device connection for hello sample code</span></span>

<span data-ttu-id="def56-120">File di configurazione dispositivo hello aggiornamento `config-azure.json` in modo che l'hub IoT è possibile leggere i messaggi nel computer host.</span><span class="sxs-lookup"><span data-stu-id="def56-120">Update hello device configuration file `config-azure.json` so that you can read messages from your IoT hub on your host computer.</span></span> <span data-ttu-id="def56-121">toodo, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="def56-121">toodo this, follow these steps:</span></span>

1. <span data-ttu-id="def56-122">Aprire `config-azure.json` nel codice di Visual Studio eseguendo hello comando in una finestra della console seguente:</span><span class="sxs-lookup"><span data-stu-id="def56-122">Open `config-azure.json` in Visual Studio Code by running hello following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="def56-123">Rendere hello seguenti sostituzioni hello `config-azure.json` file:</span><span class="sxs-lookup"><span data-stu-id="def56-123">Make hello following replacements in hello `config-azure.json` file:</span></span>

   ![screenshot di config azure](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="def56-125">Sostituire `[IoT hub connection string]` con stringa di connessione hub IoT ottenuto hello.</span><span class="sxs-lookup"><span data-stu-id="def56-125">Replace `[IoT hub connection string]` with hello IoT hub connection string that you obtained.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="def56-126">Leggere messaggi dall'hub IoT</span><span class="sxs-lookup"><span data-stu-id="def56-126">Read messages from your IoT hub</span></span>

<span data-ttu-id="def56-127">Se si ha un dispositivo TI SensorTag, verificare di averlo già acceso.</span><span class="sxs-lookup"><span data-stu-id="def56-127">If you have a TI SensorTag, make sure you have already powered on your SensorTag.</span></span> <span data-ttu-id="def56-128">Eseguire l'applicazione di esempio gateway hello e leggere i messaggi di IoT Hub da hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="def56-128">Run hello gateway sample application and read IoT Hub messages by hello following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="def56-129">comando Hello esegue hello Disattiva applicazione di esempio legge e i pacchetti di dati di temperatura dal dispositivo simulato o SensorTag e invia l'hub IoT tooyour messaggio hello ogni 2 secondi.</span><span class="sxs-lookup"><span data-stu-id="def56-129">hello command runs hello BLE sample application that reads and packages temperature data from your SensorTag or simulated device and sends hello message tooyour IoT hub every 2 seconds.</span></span> <span data-ttu-id="def56-130">Inoltre, genera un messaggio di hello tooreceive processo figlio.</span><span class="sxs-lookup"><span data-stu-id="def56-130">It also spawns a child process tooreceive hello message.</span></span>

<span data-ttu-id="def56-131">messaggi Hello che vengono inviati e ricevuti sono tutti hello visualizzati immediatamente nella stessa finestra di console hello computer host.</span><span class="sxs-lookup"><span data-stu-id="def56-131">hello messages that are being sent and received are all displayed instantly on hello same console window in hello host machine.</span></span> <span data-ttu-id="def56-132">istanza di applicazione di esempio Hello verrà terminato automaticamente 40 secondi.</span><span class="sxs-lookup"><span data-stu-id="def56-132">hello sample application instance will terminate automatically in 40 seconds.</span></span>

![Applicazione di esempio BLE con messaggi inviati e ricevuti](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub.png)

## <a name="summary"></a><span data-ttu-id="def56-134">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="def56-134">Summary</span></span>

<span data-ttu-id="def56-135">Aver eseguito un tooread codice di esempio i messaggi dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="def56-135">You've run a sample code tooread messages from your IoT hub.</span></span> <span data-ttu-id="def56-136">Si è messaggi hello tooread pronto archiviati nell'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="def56-136">You're ready tooread hello messages that are stored in your Azure table storage.</span></span>

## <a name="next-steps"></a><span data-ttu-id="def56-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="def56-137">Next steps</span></span>
[<span data-ttu-id="def56-138">Creare un'app per le funzioni di Azure e un account di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="def56-138">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)


