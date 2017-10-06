---
title: gestione dei dispositivi IoT con l'hub IOT explorer aaaAzure | Documenti Microsoft
description: "Utilizzare hello hub IOT Esplora CLI lo strumento per la gestione dei dispositivi Azure IoT Hub, che presenta metodi diretti hello e opzioni di gestione del doppi hello proprietà desiderate."
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
ms.openlocfilehash: e0a5e6120db5c4fb12f7f8b605a56e0e4aad9217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-for-azure-iot-hub-device-management"></a><span data-ttu-id="6c0ff-104">Usare iothub-explorer per la gestione di dispositivi hub IoT di Azure</span><span class="sxs-lookup"><span data-stu-id="6c0ff-104">Use iothub-explorer for Azure IoT Hub device management</span></span>

![Diagramma end-to-end](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="6c0ff-106">[l'hub IOT Esplora](https://github.com/azure/iothub-explorer) è uno strumento CLI eseguite su un'identità di dispositivi toomanage computer host nel Registro di sistema hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6c0ff-106">[iothub-explorer](https://github.com/azure/iothub-explorer) is a CLI tool that you run on a host computer toomanage device identities in your IoT hub registry.</span></span> <span data-ttu-id="6c0ff-107">È dotato di opzioni di gestione che è possibile utilizzare tooperform diverse attività.</span><span class="sxs-lookup"><span data-stu-id="6c0ff-107">It comes with management options that you can use tooperform various tasks.</span></span>

| <span data-ttu-id="6c0ff-108">Opzione di gestione</span><span class="sxs-lookup"><span data-stu-id="6c0ff-108">Management option</span></span>          | <span data-ttu-id="6c0ff-109">Attività</span><span class="sxs-lookup"><span data-stu-id="6c0ff-109">Task</span></span>                                                                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6c0ff-110">Metodi diretti</span><span class="sxs-lookup"><span data-stu-id="6c0ff-110">Direct methods</span></span>             | <span data-ttu-id="6c0ff-111">Rendere un dispositivo di eseguire operazioni quali l'avvio o arresto di invio di messaggi o il riavvio dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="6c0ff-111">Make a device act such as starting or stopping sending messages or rebooting hello device.</span></span>                                        |
| <span data-ttu-id="6c0ff-112">Proprietà desiderate del dispositivo gemello</span><span class="sxs-lookup"><span data-stu-id="6c0ff-112">Twin desired properties</span></span>    | <span data-ttu-id="6c0ff-113">Inserire un dispositivo in determinati stati, ad esempio l'impostazione toogreen un LED o impostazione dati di telemetria hello trasmissione interval too30 minuti.</span><span class="sxs-lookup"><span data-stu-id="6c0ff-113">Put a device into certain states, such as setting an LED toogreen or setting hello telemetry send interval too30 minutes.</span></span>         |
| <span data-ttu-id="6c0ff-114">Proprietà segnalate del dispositivo gemello</span><span class="sxs-lookup"><span data-stu-id="6c0ff-114">Twin reported properties</span></span>   | <span data-ttu-id="6c0ff-115">Ottenere hello segnalato lo stato di un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6c0ff-115">Get hello reported state of a device.</span></span> <span data-ttu-id="6c0ff-116">Ad esempio, il dispositivo di hello segnala hello che LED è lampeggiante ora.</span><span class="sxs-lookup"><span data-stu-id="6c0ff-116">For example, hello device reports hello LED is blinking now.</span></span>                                    |
| <span data-ttu-id="6c0ff-117">Tag dei dispositivi gemelli</span><span class="sxs-lookup"><span data-stu-id="6c0ff-117">Twin tags</span></span>                  | <span data-ttu-id="6c0ff-118">Archiviare i metadati specifici del dispositivo nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="6c0ff-118">Store device-specific metadata in hello cloud.</span></span> <span data-ttu-id="6c0ff-119">Salve, ad esempio, il percorso di distribuzione di una macchina distributore.</span><span class="sxs-lookup"><span data-stu-id="6c0ff-119">For example, hello deployment location of a vending machine.</span></span>                         |
| <span data-ttu-id="6c0ff-120">Messaggi da cloud a dispositivo</span><span class="sxs-lookup"><span data-stu-id="6c0ff-120">Cloud-to-device messages</span></span>   | <span data-ttu-id="6c0ff-121">Invio dispositivo tooa notifiche.</span><span class="sxs-lookup"><span data-stu-id="6c0ff-121">Send notifications tooa device.</span></span> <span data-ttu-id="6c0ff-122">Ad esempio, "è molto probabile toorain oggi.</span><span class="sxs-lookup"><span data-stu-id="6c0ff-122">For example, "It is very likely toorain today.</span></span> <span data-ttu-id="6c0ff-123">Non dimenticare toobring un ombrello."</span><span class="sxs-lookup"><span data-stu-id="6c0ff-123">Don't forget toobring an umbrella."</span></span>              |
| <span data-ttu-id="6c0ff-124">Query del dispositivo gemello</span><span class="sxs-lookup"><span data-stu-id="6c0ff-124">Device twin queries</span></span>        | <span data-ttu-id="6c0ff-125">Eseguire una query tutti i dispositivi gemelli tooretrieve quelli con condizioni arbitrarie, ad esempio di identificare i dispositivi di hello che sono disponibili per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="6c0ff-125">Query all device twins tooretrieve those with arbitrary conditions, such as identifying hello devices that are available for use.</span></span> |

<span data-ttu-id="6c0ff-126">Per ulteriori spiegazioni sulle differenze di hello e istruzioni sull'uso di queste opzioni, vedere [materiale sussidiario per la comunicazione da dispositivo a cloud](iot-hub-devguide-d2c-guidance.md) e [indicazioni di comunicazione Cloud a dispositivo](iot-hub-devguide-c2d-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="6c0ff-126">For more detailed explanation on hello differences and guidance on using these options, see [Device-to-cloud communication guidance](iot-hub-devguide-d2c-guidance.md) and [Cloud-to-device communication guidance](iot-hub-devguide-c2d-guidance.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6c0ff-127">I dispositivi gemelli sono documenti JSON nei quali vengono archiviate informazioni sullo stato dei dispositivi (metadati, configurazioni e condizioni).</span><span class="sxs-lookup"><span data-stu-id="6c0ff-127">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="6c0ff-128">IoT Hub persiste doppi un dispositivo per ogni dispositivo che si connette tooit.</span><span class="sxs-lookup"><span data-stu-id="6c0ff-128">IoT Hub persists a device twin for each device that connects tooit.</span></span> <span data-ttu-id="6c0ff-129">Per altre informazioni sui dispositivi gemelli, vedere [Introduzione ai dispositivi gemelli](iot-hub-node-node-twin-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="6c0ff-129">For more information about device twins, see [Get started with device twins](iot-hub-node-node-twin-getstarted.md).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="6c0ff-130">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="6c0ff-130">What you learn</span></span>

<span data-ttu-id="6c0ff-131">Si apprende l'uso di iothub-explorer con varie opzioni di gestione presenti nel proprio computer di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="6c0ff-131">You learn using iothub-explorer with various management options on your development machine.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="6c0ff-132">Operazioni da fare</span><span class="sxs-lookup"><span data-stu-id="6c0ff-132">What you do</span></span>

<span data-ttu-id="6c0ff-133">Eseguire iothub-explorer con diverse opzioni di gestione.</span><span class="sxs-lookup"><span data-stu-id="6c0ff-133">Run iothub-explorer with various management options.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6c0ff-134">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="6c0ff-134">What you need</span></span>

- <span data-ttu-id="6c0ff-135">Esercitazione [configurare il dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) completato che copre hello seguenti requisiti:</span><span class="sxs-lookup"><span data-stu-id="6c0ff-135">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="6c0ff-136">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="6c0ff-136">An active Azure subscription.</span></span>
  - <span data-ttu-id="6c0ff-137">Un hub IoT di Azure nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="6c0ff-137">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="6c0ff-138">Un'applicazione client che invia l'hub IoT di Azure tooyour messaggi.</span><span class="sxs-lookup"><span data-stu-id="6c0ff-138">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="6c0ff-139">Verificare che il dispositivo è in esecuzione con un'applicazione client hello durante questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="6c0ff-139">Make sure your device is running with hello client application during this tutorial.</span></span>
- <span data-ttu-id="6c0ff-140">iothub-explorer, [Installare iothub-explorer](https://github.com/azure/iothub-explorer) sul computer di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="6c0ff-140">iothub-explorer, [Install iothub-explorer](https://github.com/azure/iothub-explorer) on your development machine.</span></span>

## <a name="connect-tooyour-iot-hub"></a><span data-ttu-id="6c0ff-141">Collegare tooyour IoT hub</span><span class="sxs-lookup"><span data-stu-id="6c0ff-141">Connect tooyour IoT hub</span></span>

<span data-ttu-id="6c0ff-142">Connettersi hub IoT tooyour eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6c0ff-142">Connect tooyour IoT hub by running hello following command:</span></span>

```bash
iothub-explorer login <your IoT hub connection string>
```

## <a name="use-iothub-explorer-with-direct-methods"></a><span data-ttu-id="6c0ff-143">Usare iothub-explorer con i metodi diretti</span><span class="sxs-lookup"><span data-stu-id="6c0ff-143">Use iothub-explorer with direct methods</span></span>

<span data-ttu-id="6c0ff-144">Richiamare hello `start` metodo hello dispositivo app toosend messaggi tooyour IoT hub eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6c0ff-144">Invoke hello `start` method in hello device app toosend messages tooyour IoT hub by running hello following command:</span></span>

```bash
iothub-explorer device-method <your device Id> start
```

<span data-ttu-id="6c0ff-145">Richiamare hello `stop` metodo hello dispositivo app toostop invio messaggi hub IoT tooyour eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6c0ff-145">Invoke hello `stop` method in hello device app toostop sending messages tooyour IoT hub by running hello following command:</span></span>

```bash
iothub-explorer device-method <your device Id> stop
```

## <a name="use-iothub-explorer-with-twins-desired-properties"></a><span data-ttu-id="6c0ff-146">Usare iothub-explorer con le proprietà desiderate del dispositivo gemello</span><span class="sxs-lookup"><span data-stu-id="6c0ff-146">Use iothub-explorer with twin’s desired properties</span></span>

<span data-ttu-id="6c0ff-147">Impostare un intervallo di proprietà desiderato = 3000 eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6c0ff-147">Set a desired property interval = 3000 by running hello following command:</span></span>

```bash
iothub-explorer update-twin <your device id> {\"properties\":{\"desired\":{\"interval\":3000}}}
```

<span data-ttu-id="6c0ff-148">Questa proprietà può essere letta dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6c0ff-148">This property can be read by your device.</span></span>

## <a name="use-iothub-explorer-with-twins-reported-properties"></a><span data-ttu-id="6c0ff-149">Usare iothub-explorer con le proprietà segnalate del dispositivo gemello</span><span class="sxs-lookup"><span data-stu-id="6c0ff-149">Use iothub-explorer with twin’s reported properties</span></span>

<span data-ttu-id="6c0ff-150">Ottengano hello segnalato le proprietà del dispositivo hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6c0ff-150">Get hello reported properties of hello device by running hello following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="6c0ff-151">Una delle proprietà di hello è $metadata. $lastUpdated che mostra hello ultima volta il dispositivo invia o riceve un messaggio.</span><span class="sxs-lookup"><span data-stu-id="6c0ff-151">One of hello properties is $metadata.$lastUpdated which shows hello last time this device sends or receives a message.</span></span>

## <a name="use-iothub-explorer-with-twins-tags"></a><span data-ttu-id="6c0ff-152">Usare iothub-explorer con i tag del dispositivo gemello</span><span class="sxs-lookup"><span data-stu-id="6c0ff-152">Use iothub-explorer with twin’s tags</span></span>

<span data-ttu-id="6c0ff-153">Visualizzare i tag hello e le proprietà del dispositivo hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6c0ff-153">Display hello tags and properties of hello device by running hello following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="6c0ff-154">Aggiungere un ruolo di campo = temperatura e umidità dispositivo toohello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6c0ff-154">Add a field role = temperature&humidity toohello device by running hello following command:</span></span>

```bash
iothub-explorer update-twin <your device id> "{\"tags\":{\"role\":\"temperature&humidity\"}}"

```

## <a name="use-iothub-explorer-with-cloud-to-device-messages"></a><span data-ttu-id="6c0ff-155">Usare iothub-explorer con i messaggi da cloud a dispositivo</span><span class="sxs-lookup"><span data-stu-id="6c0ff-155">Use iothub-explorer with Cloud-to-device messages</span></span>

<span data-ttu-id="6c0ff-156">Invio di un dispositivo di toohello messaggio "Hello World" eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6c0ff-156">Send a "Hello World" message toohello device by running hello following command:</span></span>

```bash
iothub-explorer send <device-id> "Hello World"
```

<span data-ttu-id="6c0ff-157">Vedere [usare hub IOT Esplora toosend e ricevere messaggi tra il dispositivo e l'IoT Hub](iot-hub-explorer-cloud-device-messaging.md) per uno scenario reale di utilizzo del comando.</span><span class="sxs-lookup"><span data-stu-id="6c0ff-157">See [Use iothub-explorer toosend and receive messages between your device and IoT Hub](iot-hub-explorer-cloud-device-messaging.md) for a real scenario of using this command.</span></span>

## <a name="use-iothub-explorer-with-device-twins-queries"></a><span data-ttu-id="6c0ff-158">Usare iothub-explorer con le query del dispositivo gemello</span><span class="sxs-lookup"><span data-stu-id="6c0ff-158">Use iothub-explorer with device twins queries</span></span>

<span data-ttu-id="6c0ff-159">Query di dispositivi con un tag di ruolo = 'temperatura e umidità' eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6c0ff-159">Query devices with a tag of role = 'temperature&humidity' by running hello following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role = 'temperature&humidity'"
```

<span data-ttu-id="6c0ff-160">Eseguire una query tutti i dispositivi, ad eccezione di quelli con un tag di ruolo = 'temperatura e umidità' eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6c0ff-160">Query all devices except those with a tag of role = 'temperature&humidity' by running hello following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role != 'temperature&humidity'"
```

## <a name="next-steps"></a><span data-ttu-id="6c0ff-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6c0ff-161">Next steps</span></span>

<span data-ttu-id="6c0ff-162">Si è appreso come toouse hub IOT-Esplora con diverse opzioni di gestione.</span><span class="sxs-lookup"><span data-stu-id="6c0ff-162">You've learned how toouse iothub-explorer with various management options.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
