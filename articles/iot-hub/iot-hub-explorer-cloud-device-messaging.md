---
title: Gestire la messaggistica dei dispositivi cloud nell'hub IoT di Azure con iothub-explorer | Microsoft Docs
description: Informazioni su come usare lo strumento iothub-explorer dell'interfaccia della riga di comando per monitorare i messaggi da dispositivo a cloud e inviare messaggi da cloud a dispositivo nell'hub IoT di Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: iothub explorer, messaggistica dei dispositivi cloud, hub iot da cloud a dispositivo, messaggistica da cloud a dispositivo
ms.assetid: 04521658-35d3-4503-ae48-51d6ad3c62cc
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: 30151b7bdc544bc36e959cc3528d37897198fc7e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-iothub-explorer-to-send-and-receive-messages-between-your-device-and-iot-hub"></a><span data-ttu-id="822bc-104">Usare iothub-explorer per inviare e ricevere messaggi tra il dispositivo e l'hub IoT</span><span class="sxs-lookup"><span data-stu-id="822bc-104">Use iothub-explorer to send and receive messages between your device and IoT Hub</span></span>

![Diagramma end-to-end](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="822bc-106">[iothub-explorer](https://github.com/azure/iothub-explorer) include una gamma di comandi che semplificano la gestione dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="822bc-106">[iothub-explorer](https://github.com/azure/iothub-explorer) has a handful of commands that makes IoT Hub management easier.</span></span> <span data-ttu-id="822bc-107">Questa esercitazione approfondisce l'uso di iothub-explorer per inviare e ricevere messaggi tra il dispositivo e l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="822bc-107">This tutorial focuses on how to use iothub-explorer to send and receive messages between your device and your IoT hub.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="822bc-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="822bc-108">What you will learn</span></span>

<span data-ttu-id="822bc-109">Informazioni su come usare iothub-explorer per monitorare i messaggi da dispositivo a cloud e inviare messaggi da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="822bc-109">You learn how to use iothub-explorer to monitor device-to-cloud messages and to send cloud-to-device messages.</span></span> <span data-ttu-id="822bc-110">I messaggi da dispositivo a cloud possono includere dati di sensori raccolti dal dispositivo e inviati all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="822bc-110">Device-to-cloud messages could be sensor data that your device collects and then sends to your IoT hub.</span></span> <span data-ttu-id="822bc-111">I messaggi da cloud a dispositivo possono includere comandi inviati dall'hub IoT al dispositivo per far lampeggiare un LED connesso a quest'ultimo.</span><span class="sxs-lookup"><span data-stu-id="822bc-111">Cloud-to-device messages could be commands that your IoT hub sends to your device to blink an LED that is connected to your device.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="822bc-112">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="822bc-112">What you will do</span></span>

- <span data-ttu-id="822bc-113">Usare iothub-explorer per monitorare i messaggi da dispositivo a cloud.</span><span class="sxs-lookup"><span data-stu-id="822bc-113">Use iothub-explorer to monitor device-to-cloud messages.</span></span>
- <span data-ttu-id="822bc-114">Usare iothub-explorer per inviare messaggi da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="822bc-114">Use iothub-explorer to send cloud-to-device messages.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="822bc-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="822bc-115">What you need</span></span>

- <span data-ttu-id="822bc-116">Completare l'esercitazione [Configurare il dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) che prevede i requisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="822bc-116">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="822bc-117">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="822bc-117">An active Azure subscription.</span></span>
  - <span data-ttu-id="822bc-118">Un hub IoT di Azure nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="822bc-118">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="822bc-119">Un'applicazione client che invia messaggi ad Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="822bc-119">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="822bc-120">iothub-explorer.</span><span class="sxs-lookup"><span data-stu-id="822bc-120">iothub-explorer.</span></span> <span data-ttu-id="822bc-121">([Installare iothub-explorer](https://github.com/azure/iothub-explorer))</span><span class="sxs-lookup"><span data-stu-id="822bc-121">([Install iothub-explorer](https://github.com/azure/iothub-explorer))</span></span>

## <a name="monitor-device-to-cloud-messages"></a><span data-ttu-id="822bc-122">Monitorare i messaggi da dispositivo a cloud</span><span class="sxs-lookup"><span data-stu-id="822bc-122">Monitor device-to-cloud messages</span></span>

<span data-ttu-id="822bc-123">Per monitorare i messaggi inviati dal dispositivo all'hub IoT, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="822bc-123">To monitor messages that are sent from your device to your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="822bc-124">Aprire una finestra della console.</span><span class="sxs-lookup"><span data-stu-id="822bc-124">Open a console window.</span></span>
1. <span data-ttu-id="822bc-125">Eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="822bc-125">Run the following command:</span></span>

   ```bash
   iothub-explorer monitor-events <device-id> --login "<IoTHubConnectionString>"
   ```

   > [!Note]
   > <span data-ttu-id="822bc-126">Ottenere `<device-id>` e `<IoTHubConnectionString>` dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="822bc-126">Get `<device-id>` and `<IoTHubConnectionString>` from your IoT hub.</span></span> <span data-ttu-id="822bc-127">Assicurarsi di aver terminato l'esercitazione precedente.</span><span class="sxs-lookup"><span data-stu-id="822bc-127">Make sure you've finished the previous tutorial.</span></span> <span data-ttu-id="822bc-128">In alternativa, è possibile provare a usare `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` se sono presenti `HostName`, `SharedAccessKeyName` e `SharedAccessKey`.</span><span class="sxs-lookup"><span data-stu-id="822bc-128">Or you can try to use `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` if you have `HostName`, `SharedAccessKeyName` and `SharedAccessKey`.</span></span>

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="822bc-129">Inviare messaggi da cloud a dispositivo</span><span class="sxs-lookup"><span data-stu-id="822bc-129">Send cloud-to-device messages</span></span>

<span data-ttu-id="822bc-130">Per inviare un messaggio dall'hub IoT al dispositivo, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="822bc-130">To send a message from your IoT hub to your device, follow these steps:</span></span>

1. <span data-ttu-id="822bc-131">Aprire una finestra della console.</span><span class="sxs-lookup"><span data-stu-id="822bc-131">Open a console window.</span></span>
1. <span data-ttu-id="822bc-132">Avviare una sessione nell'hub IoT eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="822bc-132">Start a session on your IoT hub by running the following command:</span></span>

   ```bash
   iothub-explorer login `<IoTHubConnectionString>`
   ```

1. <span data-ttu-id="822bc-133">Inviare un messaggio al dispositivo eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="822bc-133">Send a message to your device by running the following command:</span></span>

   ```bash
   iothub-explorer send <device-id> <message>
   ```

<span data-ttu-id="822bc-134">Il comando fa lampeggiare il LED di connessione al dispositivo e invia il messaggio a quest'ultimo.</span><span class="sxs-lookup"><span data-stu-id="822bc-134">The command blinks the LED that is connected to your device and sends the message to your device.</span></span>

> [!Note]
> <span data-ttu-id="822bc-135">Non è necessario che il dispositivo invii un comando ack separato in risposta all'hub IoT una volta ricevuto il messaggio.</span><span class="sxs-lookup"><span data-stu-id="822bc-135">There is no need for the device to send a separate ack command back to your IoT hub upon receiving the message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="822bc-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="822bc-136">Next steps</span></span>

<span data-ttu-id="822bc-137">È stato appreso come monitorare i messaggi da dispositivo a cloud e inviare messaggi da cloud a dispositivo tra il dispositivo IoT e l'hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="822bc-137">You’ve learned how to monitor device-to-cloud messages and send cloud-to-device messages between your IoT device and Azure IoT Hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
