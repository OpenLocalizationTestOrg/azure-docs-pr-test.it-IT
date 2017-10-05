---
title: Gestione dei dispositivi Azure IoT con iothub-explorer | Microsoft Docs
description: "Usare lo strumento dell'interfaccia della riga di comando iothub-explorer per la gestione di dispositivi dell'hub IoT di Azure, con i metodi diretti e le opzioni di gestione delle proprietà desiderate nei dispositivi gemelli."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: gestione dispositivi iot azure, gestione dispositivi hub iot azure, gestione dispositivi iot, gestione dispositivi hub iot
ms.assetid: b34f799a-fc14-41b9-bf45-54751163fffe
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: xshi
ms.openlocfilehash: 5b7a5057bdfb5920fbb5759bed1f5561cfa1d7e0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="use-iothub-explorer-for-azure-iot-hub-device-management"></a><span data-ttu-id="6206f-104">Usare iothub-explorer per la gestione di dispositivi hub IoT di Azure</span><span class="sxs-lookup"><span data-stu-id="6206f-104">Use iothub-explorer for Azure IoT Hub device management</span></span>

![Diagramma end-to-end](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="6206f-106">[iothub-explorer](https://github.com/azure/iothub-explorer) è uno strumento dell'interfaccia della riga di comando eseguito in un computer host che consente di gestire le identità dei dispositivi nel registro dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6206f-106">[iothub-explorer](https://github.com/azure/iothub-explorer) is a CLI tool that you run on a host computer to manage device identities in your IoT hub registry.</span></span> <span data-ttu-id="6206f-107">Include opzioni di gestione che consentono di eseguire varie attività.</span><span class="sxs-lookup"><span data-stu-id="6206f-107">It comes with management options that you can use to perform various tasks.</span></span>

| <span data-ttu-id="6206f-108">Opzione di gestione</span><span class="sxs-lookup"><span data-stu-id="6206f-108">Management option</span></span>          | <span data-ttu-id="6206f-109">Attività</span><span class="sxs-lookup"><span data-stu-id="6206f-109">Task</span></span>                                                                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6206f-110">Metodi diretti</span><span class="sxs-lookup"><span data-stu-id="6206f-110">Direct methods</span></span>             | <span data-ttu-id="6206f-111">Far eseguire un'attività al dispositivo, quale l'avvio o l'arresto dell'invio di messaggi o il riavvio del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6206f-111">Make a device act such as starting or stopping sending messages or rebooting the device.</span></span>                                        |
| <span data-ttu-id="6206f-112">Proprietà desiderate del dispositivo gemello</span><span class="sxs-lookup"><span data-stu-id="6206f-112">Twin desired properties</span></span>    | <span data-ttu-id="6206f-113">Impostare determinati stati di un dispositivo, ad esempio impostare la luce verde per un LED o impostare l'intervallo di invio dei dati di telemetria su 30 minuti.</span><span class="sxs-lookup"><span data-stu-id="6206f-113">Put a device into certain states, such as setting an LED to green or setting the telemetry send interval to 30 minutes.</span></span>         |
| <span data-ttu-id="6206f-114">Proprietà segnalate del dispositivo gemello</span><span class="sxs-lookup"><span data-stu-id="6206f-114">Twin reported properties</span></span>   | <span data-ttu-id="6206f-115">Ottenere lo stato restituito da un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6206f-115">Get the reported state of a device.</span></span> <span data-ttu-id="6206f-116">Ad esempio, il dispositivo segnala che il LED sta lampeggiando.</span><span class="sxs-lookup"><span data-stu-id="6206f-116">For example, the device reports the LED is blinking now.</span></span>                                    |
| <span data-ttu-id="6206f-117">Tag dei dispositivi gemelli</span><span class="sxs-lookup"><span data-stu-id="6206f-117">Twin tags</span></span>                  | <span data-ttu-id="6206f-118">Archiviare i metadati specifici del dispositivo nel cloud,</span><span class="sxs-lookup"><span data-stu-id="6206f-118">Store device-specific metadata in the cloud.</span></span> <span data-ttu-id="6206f-119">ad esempio il percorso di distribuzione di un distributore automatico.</span><span class="sxs-lookup"><span data-stu-id="6206f-119">For example, the deployment location of a vending machine.</span></span>                         |
| <span data-ttu-id="6206f-120">Messaggi da cloud a dispositivo</span><span class="sxs-lookup"><span data-stu-id="6206f-120">Cloud-to-device messages</span></span>   | <span data-ttu-id="6206f-121">Inviare notifiche a un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6206f-121">Send notifications to a device.</span></span> <span data-ttu-id="6206f-122">Ad esempio "Oggi è molto probabile che piova.</span><span class="sxs-lookup"><span data-stu-id="6206f-122">For example, "It is very likely to rain today.</span></span> <span data-ttu-id="6206f-123">Meglio non dimenticare l'ombrello".</span><span class="sxs-lookup"><span data-stu-id="6206f-123">Don't forget to bring an umbrella."</span></span>              |
| <span data-ttu-id="6206f-124">Query del dispositivo gemello</span><span class="sxs-lookup"><span data-stu-id="6206f-124">Device twin queries</span></span>        | <span data-ttu-id="6206f-125">Eseguire query su tutti i dispositivi gemelli per identificare quelli che si trovano in una determinata condizione, ad esempio i dispositivi disponibili per l'uso.</span><span class="sxs-lookup"><span data-stu-id="6206f-125">Query all device twins to retrieve those with arbitrary conditions, such as identifying the devices that are available for use.</span></span> |

<span data-ttu-id="6206f-126">Per altre informazioni sulle differenze e sull'uso di queste opzioni, vedere [Device-to-cloud communication guidance](iot-hub-devguide-d2c-guidance.md) (Indicazioni sulla comunicazione da dispositivo a cloud) e [Cloud-to-device communication guidance](iot-hub-devguide-c2d-guidance.md) (Indicazioni sulla comunicazione da cloud a dispositivo).</span><span class="sxs-lookup"><span data-stu-id="6206f-126">For more detailed explanation on the differences and guidance on using these options, see [Device-to-cloud communication guidance](iot-hub-devguide-d2c-guidance.md) and [Cloud-to-device communication guidance](iot-hub-devguide-c2d-guidance.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6206f-127">I dispositivi gemelli sono documenti JSON nei quali vengono archiviate informazioni sullo stato dei dispositivi (metadati, configurazioni e condizioni).</span><span class="sxs-lookup"><span data-stu-id="6206f-127">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="6206f-128">L'hub IoT rende permanente un dispositivo gemello per ogni dispositivo che si connette.</span><span class="sxs-lookup"><span data-stu-id="6206f-128">IoT Hub persists a device twin for each device that connects to it.</span></span> <span data-ttu-id="6206f-129">Per altre informazioni sui dispositivi gemelli, vedere [Introduzione ai dispositivi gemelli](iot-hub-node-node-twin-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="6206f-129">For more information about device twins, see [Get started with device twins](iot-hub-node-node-twin-getstarted.md).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="6206f-130">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="6206f-130">What you learn</span></span>

<span data-ttu-id="6206f-131">Si apprende l'uso di iothub-explorer con varie opzioni di gestione presenti nel proprio computer di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="6206f-131">You learn using iothub-explorer with various management options on your development machine.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="6206f-132">Operazioni da fare</span><span class="sxs-lookup"><span data-stu-id="6206f-132">What you do</span></span>

<span data-ttu-id="6206f-133">Eseguire iothub-explorer con diverse opzioni di gestione.</span><span class="sxs-lookup"><span data-stu-id="6206f-133">Run iothub-explorer with various management options.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6206f-134">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="6206f-134">What you need</span></span>

- <span data-ttu-id="6206f-135">Completare l'esercitazione [Configurare il dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) che prevede i requisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="6206f-135">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="6206f-136">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="6206f-136">An active Azure subscription.</span></span>
  - <span data-ttu-id="6206f-137">Un hub IoT di Azure nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="6206f-137">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="6206f-138">Un'applicazione client che invia messaggi all'hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="6206f-138">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="6206f-139">Verificare che il dispositivo sia in esecuzione con l'applicazione client durante questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="6206f-139">Make sure your device is running with the client application during this tutorial.</span></span>
- <span data-ttu-id="6206f-140">iothub-explorer, [Installare iothub-explorer](https://github.com/azure/iothub-explorer) sul computer di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="6206f-140">iothub-explorer, [Install iothub-explorer](https://github.com/azure/iothub-explorer) on your development machine.</span></span>

## <a name="connect-to-your-iot-hub"></a><span data-ttu-id="6206f-141">Accedere all'hub IoT</span><span class="sxs-lookup"><span data-stu-id="6206f-141">Connect to your IoT hub</span></span>

<span data-ttu-id="6206f-142">Accedere all'hub IoT eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6206f-142">Connect to your IoT hub by running the following command:</span></span>

```bash
iothub-explorer login <your IoT hub connection string>
```

## <a name="use-iothub-explorer-with-direct-methods"></a><span data-ttu-id="6206f-143">Usare iothub-explorer con i metodi diretti</span><span class="sxs-lookup"><span data-stu-id="6206f-143">Use iothub-explorer with direct methods</span></span>

<span data-ttu-id="6206f-144">Chiamare il metodo `start` nell'app per dispositivi per inviare messaggi all'hub IoT eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6206f-144">Invoke the `start` method in the device app to send messages to your IoT hub by running the following command:</span></span>

```bash
iothub-explorer device-method <your device Id> start
```

<span data-ttu-id="6206f-145">Chiamare il metodo `stop` nell'app per dispositivi per interrompere l'invio di messaggi all'hub IoT eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6206f-145">Invoke the `stop` method in the device app to stop sending messages to your IoT hub by running the following command:</span></span>

```bash
iothub-explorer device-method <your device Id> stop
```

## <a name="use-iothub-explorer-with-twins-desired-properties"></a><span data-ttu-id="6206f-146">Usare iothub-explorer con le proprietà desiderate del dispositivo gemello</span><span class="sxs-lookup"><span data-stu-id="6206f-146">Use iothub-explorer with twin’s desired properties</span></span>

<span data-ttu-id="6206f-147">Impostare l'intervallo di proprietà desiderato su 3000 eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6206f-147">Set a desired property interval = 3000 by running the following command:</span></span>

```bash
iothub-explorer update-twin <your device id> {\"properties\":{\"desired\":{\"interval\":3000}}}
```

<span data-ttu-id="6206f-148">Questa proprietà può essere letta dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6206f-148">This property can be read by your device.</span></span>

## <a name="use-iothub-explorer-with-twins-reported-properties"></a><span data-ttu-id="6206f-149">Usare iothub-explorer con le proprietà segnalate del dispositivo gemello</span><span class="sxs-lookup"><span data-stu-id="6206f-149">Use iothub-explorer with twin’s reported properties</span></span>

<span data-ttu-id="6206f-150">Ottenere le proprietà segnalate del dispositivo eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6206f-150">Get the reported properties of the device by running the following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="6206f-151">Una delle proprietà è $metadata.$lastUpdated, che visualizza l'ora di invio o ricezione dell'ultimo messaggio nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6206f-151">One of the properties is $metadata.$lastUpdated which shows the last time this device sends or receives a message.</span></span>

## <a name="use-iothub-explorer-with-twins-tags"></a><span data-ttu-id="6206f-152">Usare iothub-explorer con i tag del dispositivo gemello</span><span class="sxs-lookup"><span data-stu-id="6206f-152">Use iothub-explorer with twin’s tags</span></span>

<span data-ttu-id="6206f-153">Visualizzare i tag e le proprietà del dispositivo eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6206f-153">Display the tags and properties of the device by running the following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="6206f-154">Aggiungere il campo role = temperature&humidity al dispositivo eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6206f-154">Add a field role = temperature&humidity to the device by running the following command:</span></span>

```bash
iothub-explorer update-twin <your device id> "{\"tags\":{\"role\":\"temperature&humidity\"}}"

```

## <a name="use-iothub-explorer-with-cloud-to-device-messages"></a><span data-ttu-id="6206f-155">Usare iothub-explorer con i messaggi da cloud a dispositivo</span><span class="sxs-lookup"><span data-stu-id="6206f-155">Use iothub-explorer with Cloud-to-device messages</span></span>

<span data-ttu-id="6206f-156">Inviare un messaggio "Hello World" al dispositivo eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6206f-156">Send a "Hello World" message to the device by running the following command:</span></span>

```bash
iothub-explorer send <device-id> "Hello World"
```

<span data-ttu-id="6206f-157">Per uno scenario reale dell'uso di questo comando, vedere [Usare iothub-explorer per inviare e ricevere messaggi tra il dispositivo e l'hub IoT](iot-hub-explorer-cloud-device-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="6206f-157">See [Use iothub-explorer to send and receive messages between your device and IoT Hub](iot-hub-explorer-cloud-device-messaging.md) for a real scenario of using this command.</span></span>

## <a name="use-iothub-explorer-with-device-twins-queries"></a><span data-ttu-id="6206f-158">Usare iothub-explorer con le query del dispositivo gemello</span><span class="sxs-lookup"><span data-stu-id="6206f-158">Use iothub-explorer with device twins queries</span></span>

<span data-ttu-id="6206f-159">Eseguire una query su tutti i dispositivi con il tag role = 'temperature&humidity' eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6206f-159">Query devices with a tag of role = 'temperature&humidity' by running the following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role = 'temperature&humidity'"
```

<span data-ttu-id="6206f-160">Eseguire una query su tutti i dispositivi meno quelli con il tag role = 'temperature&humidity' eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6206f-160">Query all devices except those with a tag of role = 'temperature&humidity' by running the following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role != 'temperature&humidity'"
```

## <a name="next-steps"></a><span data-ttu-id="6206f-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6206f-161">Next steps</span></span>

<span data-ttu-id="6206f-162">Si è appreso l'uso di iothub-explorer con diverse opzioni di gestione.</span><span class="sxs-lookup"><span data-stu-id="6206f-162">You've learned how to use iothub-explorer with various management options.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
