---
title: 'Dispositivo simulato e gateway Azure IoT: lezione 3: Leggere i messaggi | Documentazione Microsoft'
description: Eseguire un codice di esempio sul computer host per leggere i messaggi dall'hub IoT.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: dati nel cloud, raccolta dati nel cloud, servizio cloud iot, dati iot
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5a6ec9c1-d83c-41c1-beaf-7c0d3395d77f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9fbf7958e2437d274f2692dbc235ac8147bdfa63
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="07ed6-104">Leggere i messaggi dall'hub IoT</span><span class="sxs-lookup"><span data-stu-id="07ed6-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="07ed6-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="07ed6-105">What you will do</span></span>

- <span data-ttu-id="07ed6-106">Eseguire il codice di esempio sul computer host per leggere i messaggi dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="07ed6-106">Run sample code on your host computer to read messages from your IoT hub.</span></span>

<span data-ttu-id="07ed6-107">In caso di problemi, cercare le soluzioni nella pagina sulla [risoluzione dei problemi](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="07ed6-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="07ed6-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="07ed6-108">What you will learn</span></span>

<span data-ttu-id="07ed6-109">Come usare lo strumento gulp per leggere i messaggi dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="07ed6-109">How to use the gulp tool to read messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="07ed6-110">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="07ed6-110">What you need</span></span>

- <span data-ttu-id="07ed6-111">Esempio di dispositivo simulato in [Configurare ed eseguire un'applicazione di esempio per il caricamento nel cloud del dispositivo simulato](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span><span class="sxs-lookup"><span data-stu-id="07ed6-111">The simulated device sample in [Configure and run a simulated device cloud upload sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="07ed6-112">Ottenere le stringhe di connessione dell'hub IoT e del dispositivo</span><span class="sxs-lookup"><span data-stu-id="07ed6-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="07ed6-113">La stringa di connessione del dispositivo viene usata dal dispositivo simulato per la connessione all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="07ed6-113">The device connection string is used by your simulated device to connect to your IoT hub.</span></span> <span data-ttu-id="07ed6-114">La stringa di connessione dell'hub IoT viene usata per connettersi al registro di identità nell'hub IoT per gestire i dispositivi che possono connettersi all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="07ed6-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span></span>

- <span data-ttu-id="07ed6-115">Elencare tutti gli hub IoT nel gruppo di risorse eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="07ed6-115">List all your IoT hubs in your resource group by running the following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="07ed6-116">Usare `iot-gateway` come valore di `{resource group name}` se non è stato modificato.</span><span class="sxs-lookup"><span data-stu-id="07ed6-116">Use `iot-gateway` as the value of `{resource group name}` if you didn't change it.</span></span>
- <span data-ttu-id="07ed6-117">Ottenere la stringa di connessione dell'hub IoT eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="07ed6-117">Get the IoT hub connection string by running the following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="07ed6-118">`{my hub name}` è il nome specificato nella lezione 2.</span><span class="sxs-lookup"><span data-stu-id="07ed6-118">`{my hub name}` is the name that you specified in Lesson 2.</span></span>

## <a name="configure-the-device-connection-for-the-sample-code"></a><span data-ttu-id="07ed6-119">Configurare la connessione del dispositivo per il codice di esempio</span><span class="sxs-lookup"><span data-stu-id="07ed6-119">Configure the device connection for the sample code</span></span>

<span data-ttu-id="07ed6-120">Aggiornare le configurazioni di connessione del dispositivo e dell'hub IoT in `config-azure.json` tramite i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="07ed6-120">Update IoT hub and device connection configurations in `config-azure.json` by performing the following steps:</span></span>

1. <span data-ttu-id="07ed6-121">Aprire `config-azure.json` in Visual Studio Code eseguendo questo comando in una finestra della console:</span><span class="sxs-lookup"><span data-stu-id="07ed6-121">Open `config-azure.json` in Visual Studio Code by running the following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="07ed6-122">Sostituire i valori seguenti nel file `config-azure.json`:</span><span class="sxs-lookup"><span data-stu-id="07ed6-122">Make the following replacements in the `config-azure.json` file:</span></span>

   ![screenshot di config azure](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="07ed6-124">Sostituire `[IoT hub connection string]` con la stringa di connessione dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="07ed6-124">Replace `[IoT hub connection string]` with the IoT hub connection string.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="07ed6-125">Leggere i messaggi dall'hub IoT</span><span class="sxs-lookup"><span data-stu-id="07ed6-125">Read messages from your IoT hub</span></span>

<span data-ttu-id="07ed6-126">Eseguire l'applicazione di esempio del dispositivo simulato e leggere i messaggi dell'hub IoT con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="07ed6-126">Run the simulated device sample application and read IoT Hub messages by the following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="07ed6-127">Il comando esegue l'applicazione che invia messaggi all'hub IoT ogni 2 secondi</span><span class="sxs-lookup"><span data-stu-id="07ed6-127">The command runs the application that sends messages to your IoT hub every 2 seconds.</span></span> <span data-ttu-id="07ed6-128">e genera un processo figlio per ricevere il messaggio.</span><span class="sxs-lookup"><span data-stu-id="07ed6-128">It also spawns a child process to receive the message.</span></span>

<span data-ttu-id="07ed6-129">Tutti i messaggi inviati e ricevuti vengono visualizzati immediatamente nella stessa finestra della console nel computer host.</span><span class="sxs-lookup"><span data-stu-id="07ed6-129">The messages that are being sent and received are all displayed instantly on the same console window in the host machine.</span></span> <span data-ttu-id="07ed6-130">L'applicazione verrà chiusa entro 40 secondi.</span><span class="sxs-lookup"><span data-stu-id="07ed6-130">The application will exit in 40 seconds.</span></span>

![Applicazione di esempio simulata con messaggi inviati e ricevuti](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub_simudev.png)

## <a name="summary"></a><span data-ttu-id="07ed6-132">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="07ed6-132">Summary</span></span>

<span data-ttu-id="07ed6-133">È stata eseguita l'applicazione di esempio per inviare dati all'hub IoT con un dispositivo simulato.</span><span class="sxs-lookup"><span data-stu-id="07ed6-133">You've successfully run the sample application to send data to your IoT hub with simulated device.</span></span> <span data-ttu-id="07ed6-134">Sono stati inoltre letti i messaggi inviati all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="07ed6-134">You've also read the messages that have been sent to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07ed6-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="07ed6-135">Next steps</span></span>
[<span data-ttu-id="07ed6-136">Creare un'app per le funzioni di Azure e un account di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="07ed6-136">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)


