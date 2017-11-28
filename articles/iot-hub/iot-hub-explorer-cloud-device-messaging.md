---
title: dispositivo cloud di Azure IoT Hub aaaManage messaggistica con l'hub IOT Esplora | Documenti Microsoft
description: Scopri toouse hello messaggi di hub IOT Esplora CLI strumento toomonitor dispositivo toocloud (D2C) e inviare messaggi di toodevice (C2D) di cloud in Azure IoT Hub.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Esplora l'hub IOT, cloud dispositivo messaggistica, iot hub cloud toodevice, cloud toodevice messaggistica
ms.assetid: 04521658-35d3-4503-ae48-51d6ad3c62cc
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: 741383b5631714cc2fef3309541fd2117aa7824c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-toosend-and-receive-messages-between-your-device-and-iot-hub"></a><span data-ttu-id="9c761-104">Usare l'hub IOT Esplora toosend e ricevere messaggi tra il dispositivo e l'IoT Hub</span><span class="sxs-lookup"><span data-stu-id="9c761-104">Use iothub-explorer toosend and receive messages between your device and IoT Hub</span></span>

![Diagramma end-to-end](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="9c761-106">[iothub-explorer](https://github.com/azure/iothub-explorer) include una gamma di comandi che semplificano la gestione dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9c761-106">[iothub-explorer](https://github.com/azure/iothub-explorer) has a handful of commands that makes IoT Hub management easier.</span></span> <span data-ttu-id="9c761-107">In questa esercitazione viene illustrato come toouse hub IOT Esplora toosend e ricevere messaggi tra il dispositivo e l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9c761-107">This tutorial focuses on how toouse iothub-explorer toosend and receive messages between your device and your IoT hub.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="9c761-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="9c761-108">What you will learn</span></span>

<span data-ttu-id="9c761-109">Si apprenderà come toouse messaggi da dispositivo a cloud di hub IOT Esplora toomonitor e cloud a dispositivo toosend.</span><span class="sxs-lookup"><span data-stu-id="9c761-109">You learn how toouse iothub-explorer toomonitor device-to-cloud messages and toosend cloud-to-device messages.</span></span> <span data-ttu-id="9c761-110">I messaggi da dispositivo a cloud potrebbe essere che il dispositivo raccoglie e quindi invia l'hub IoT tooyour dati del sensore.</span><span class="sxs-lookup"><span data-stu-id="9c761-110">Device-to-cloud messages could be sensor data that your device collects and then sends tooyour IoT hub.</span></span> <span data-ttu-id="9c761-111">I messaggi da cloud a dispositivo potrebbe essere che l'hub IoT invia un LED che è un dispositivo connesso tooyour tooyour dispositivo tooblink comandi.</span><span class="sxs-lookup"><span data-stu-id="9c761-111">Cloud-to-device messages could be commands that your IoT hub sends tooyour device tooblink an LED that is connected tooyour device.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="9c761-112">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="9c761-112">What you will do</span></span>

- <span data-ttu-id="9c761-113">Utilizzare i messaggi da dispositivo a cloud di hub IOT Esplora toomonitor.</span><span class="sxs-lookup"><span data-stu-id="9c761-113">Use iothub-explorer toomonitor device-to-cloud messages.</span></span>
- <span data-ttu-id="9c761-114">Usare l'hub IOT Esplora toosend cloud a dispositivo messaggi.</span><span class="sxs-lookup"><span data-stu-id="9c761-114">Use iothub-explorer toosend cloud-to-device messages.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9c761-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="9c761-115">What you need</span></span>

- <span data-ttu-id="9c761-116">Esercitazione [configurare il dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) completato che copre hello seguenti requisiti:</span><span class="sxs-lookup"><span data-stu-id="9c761-116">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="9c761-117">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="9c761-117">An active Azure subscription.</span></span>
  - <span data-ttu-id="9c761-118">Un hub IoT di Azure nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="9c761-118">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="9c761-119">Un'applicazione client che invia l'hub IoT di Azure tooyour messaggi.</span><span class="sxs-lookup"><span data-stu-id="9c761-119">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="9c761-120">iothub-explorer.</span><span class="sxs-lookup"><span data-stu-id="9c761-120">iothub-explorer.</span></span> <span data-ttu-id="9c761-121">([Installare iothub-explorer](https://github.com/azure/iothub-explorer))</span><span class="sxs-lookup"><span data-stu-id="9c761-121">([Install iothub-explorer](https://github.com/azure/iothub-explorer))</span></span>

## <a name="monitor-device-to-cloud-messages"></a><span data-ttu-id="9c761-122">Monitorare i messaggi da dispositivo a cloud</span><span class="sxs-lookup"><span data-stu-id="9c761-122">Monitor device-to-cloud messages</span></span>

<span data-ttu-id="9c761-123">toomonitor i messaggi inviati dall'hub IoT di tooyour di dispositivo, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="9c761-123">toomonitor messages that are sent from your device tooyour IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="9c761-124">Aprire una finestra della console.</span><span class="sxs-lookup"><span data-stu-id="9c761-124">Open a console window.</span></span>
1. <span data-ttu-id="9c761-125">Eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9c761-125">Run hello following command:</span></span>

   ```bash
   iothub-explorer monitor-events <device-id> --login "<IoTHubConnectionString>"
   ```

   > [!Note]
   > <span data-ttu-id="9c761-126">Ottenere `<device-id>` e `<IoTHubConnectionString>` dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9c761-126">Get `<device-id>` and `<IoTHubConnectionString>` from your IoT hub.</span></span> <span data-ttu-id="9c761-127">Assicurarsi che aver esercitazione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="9c761-127">Make sure you've finished hello previous tutorial.</span></span> <span data-ttu-id="9c761-128">Oppure è possibile provare toouse `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` se hai `HostName`, `SharedAccessKeyName` e `SharedAccessKey`.</span><span class="sxs-lookup"><span data-stu-id="9c761-128">Or you can try toouse `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` if you have `HostName`, `SharedAccessKeyName` and `SharedAccessKey`.</span></span>

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="9c761-129">Inviare messaggi da cloud a dispositivo</span><span class="sxs-lookup"><span data-stu-id="9c761-129">Send cloud-to-device messages</span></span>

<span data-ttu-id="9c761-130">toosend un messaggio dal dispositivo tooyour hub IoT, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="9c761-130">toosend a message from your IoT hub tooyour device, follow these steps:</span></span>

1. <span data-ttu-id="9c761-131">Aprire una finestra della console.</span><span class="sxs-lookup"><span data-stu-id="9c761-131">Open a console window.</span></span>
1. <span data-ttu-id="9c761-132">Avviare una sessione dell'hub IoT eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9c761-132">Start a session on your IoT hub by running hello following command:</span></span>

   ```bash
   iothub-explorer login `<IoTHubConnectionString>`
   ```

1. <span data-ttu-id="9c761-133">Invio di un dispositivo tooyour messaggio eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9c761-133">Send a message tooyour device by running hello following command:</span></span>

   ```bash
   iothub-explorer send <device-id> <message>
   ```

<span data-ttu-id="9c761-134">comando Hello lampeggia hello LED che è un dispositivo connesso tooyour e invia dispositivo tooyour di messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="9c761-134">hello command blinks hello LED that is connected tooyour device and sends hello message tooyour device.</span></span>

> [!Note]
> <span data-ttu-id="9c761-135">Non è necessario per hello dispositivo toosend un hub IoT di ack separato comando tooyour indietro quando viene ricevuto il messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="9c761-135">There is no need for hello device toosend a separate ack command back tooyour IoT hub upon receiving hello message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c761-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9c761-136">Next steps</span></span>

<span data-ttu-id="9c761-137">Si è appreso come toomonitor dispositivo a cloud messaggi e inviare messaggi da cloud a dispositivo tra il dispositivo IoT IoT Hub di Azure.</span><span class="sxs-lookup"><span data-stu-id="9c761-137">You’ve learned how toomonitor device-to-cloud messages and send cloud-to-device messages between your IoT device and Azure IoT Hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
