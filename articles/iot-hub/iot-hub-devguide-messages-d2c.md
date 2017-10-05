---
title: Informazioni sulla messaggistica da dispositivo a cloud dell'hub IoT di Azure | Microsoft Docs
description: 'Guida per gli sviluppatori: come usare la messaggistica da dispositivo a cloud con l''hub IoT. Include informazioni sull''invio di dati di telemetria e non e sull''uso del routing per recapitare i messaggi.'
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: d856e26084ee79386a2e8e0e527804bda86b477b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="send-device-to-cloud-messages-to-iot-hub"></a><span data-ttu-id="9c1e1-104">Inviare messaggi da dispositivo a cloud all'hub IoT</span><span class="sxs-lookup"><span data-stu-id="9c1e1-104">Send device-to-cloud messages to IoT Hub</span></span>

<span data-ttu-id="9c1e1-105">Per inviare i dati e gli avvisi di telemetria di serie temporali dai dispositivi al back-end della soluzione, inviare messaggi da dispositivo a cloud dal dispositivo all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9c1e1-105">To send time-series telemetry and alerts from your devices to your solution back end, send device-to-cloud messages from your device to your IoT hub.</span></span> <span data-ttu-id="9c1e1-106">Per una descrizione delle altre opzioni da dispositivo a cloud supportate dall'hub IoT, vedere [Indicazioni sulle comunicazioni da dispositivo a cloud][lnk-d2c-guidance].</span><span class="sxs-lookup"><span data-stu-id="9c1e1-106">For a discussion of other device-to-cloud options supported by IoT Hub, see [Device-to-cloud communications guidance][lnk-d2c-guidance].</span></span>

<span data-ttu-id="9c1e1-107">I messaggi da dispositivo a cloud vengono inviati tramite un endpoint per il dispositivo (**/devices/{deviceId}/messages/events**).</span><span class="sxs-lookup"><span data-stu-id="9c1e1-107">You send device-to-cloud messages through a device-facing endpoint (**/devices/{deviceId}/messages/events**).</span></span> <span data-ttu-id="9c1e1-108">A quel punto le regole di routing reindirizzano i messaggi a uno degli endpoint di servizio nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9c1e1-108">Routing rules then route your messages to one of the service-facing endpoints on your IoT hub.</span></span> <span data-ttu-id="9c1e1-109">Le regole di routing usano le intestazioni e il corpo dei messaggi da dispositivo a cloud che passano nell'hub per determinare dove reindirizzarli.</span><span class="sxs-lookup"><span data-stu-id="9c1e1-109">Routing rules use the headers and body of the device-to-cloud messages flowing through your hub to determine where to route them.</span></span> <span data-ttu-id="9c1e1-110">Per impostazione predefinita, i messaggi vengono reindirizzati all'endpoint per servizio predefinito (**messages/events**) compatibile con [Hub eventi][lnk-event-hubs].</span><span class="sxs-lookup"><span data-stu-id="9c1e1-110">By default, messages are routed to the built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="9c1e1-111">È quindi possibile usare l'[integrazione standard di Hub eventi e gli SDK][lnk-compatible-endpoint] per ricevere i messaggi da dispositivo a cloud nel back-end della soluzione.</span><span class="sxs-lookup"><span data-stu-id="9c1e1-111">Therefore, you can use standard [Event Hubs integration and SDKs][lnk-compatible-endpoint] to receive device-to-cloud messages in your solution back end.</span></span>

<span data-ttu-id="9c1e1-112">L'hub IoT implementa la messaggistica da dispositivo a cloud usando un modello di messaggistica di flusso.</span><span class="sxs-lookup"><span data-stu-id="9c1e1-112">IoT Hub implements device-to-cloud messaging using a streaming messaging pattern.</span></span> <span data-ttu-id="9c1e1-113">I messaggi da dispositivo a cloud dell'hub IoT somigliano più a *eventi* di [Hub eventi][lnk-event-hubs] che non a *messaggi* del [bus di servizio][lnk-servicebus], poiché è presente un volume elevato di eventi che passa nel servizio ed è leggibile da più lettori.</span><span class="sxs-lookup"><span data-stu-id="9c1e1-113">IoT Hub's device-to-cloud messages are more like [Event Hubs][lnk-event-hubs] *events* than [Service Bus][lnk-servicebus] *messages* in that there is a high volume of events passing through the service that can be read by multiple readers.</span></span>

<span data-ttu-id="9c1e1-114">La messaggistica da dispositivo a cloud con hub IoT ha le caratteristiche seguenti:</span><span class="sxs-lookup"><span data-stu-id="9c1e1-114">Device-to-cloud messaging with IoT Hub has the following characteristics:</span></span>

* <span data-ttu-id="9c1e1-115">I messaggi da dispositivo a cloud sono durevoli e vengono mantenuti nell'endpoint **messages/events** predefinito in un hub IoT per un massimo di sette giorni.</span><span class="sxs-lookup"><span data-stu-id="9c1e1-115">Device-to-cloud messages are durable and retained in an IoT hub's default **messages/events** endpoint for up to seven days.</span></span>
* <span data-ttu-id="9c1e1-116">I messaggi da dispositivo a cloud possono avere dimensioni massime pari a 256 KB e possono essere raggruppati in batch per ottimizzare gli invii.</span><span class="sxs-lookup"><span data-stu-id="9c1e1-116">Device-to-cloud messages can be at most 256 KB, and can be grouped in batches to optimize sends.</span></span> <span data-ttu-id="9c1e1-117">I batch possono avere dimensioni massime pari a 256 KB.</span><span class="sxs-lookup"><span data-stu-id="9c1e1-117">Batches can be at most 256 KB.</span></span>
* <span data-ttu-id="9c1e1-118">Come illustrato nella sezione [Controllare l'accesso all'hub IoT][lnk-devguide-security], l'hub IoT consente il controllo di accesso e l'autenticazione per singoli dispositivi.</span><span class="sxs-lookup"><span data-stu-id="9c1e1-118">As explained in the [Control access to IoT Hub][lnk-devguide-security] section, IoT Hub enables per-device authentication and access control.</span></span>
* <span data-ttu-id="9c1e1-119">L'hub IoT consente di creare fino a 10 endpoint personalizzati.</span><span class="sxs-lookup"><span data-stu-id="9c1e1-119">IoT Hub allows you to create up to 10 custom endpoints.</span></span> <span data-ttu-id="9c1e1-120">I messaggi vengono recapitati agli endpoint in base alle route configurate nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9c1e1-120">Messages are delivered to the endpoints based on routes configured on your IoT hub.</span></span> <span data-ttu-id="9c1e1-121">Per altre informazioni, vedere [Regole di routing](#routing-rules).</span><span class="sxs-lookup"><span data-stu-id="9c1e1-121">For more information, see [Routing rules](#routing-rules).</span></span>
* <span data-ttu-id="9c1e1-122">L'hub IoT abilita milioni di dispositivi connessi contemporaneamente (vedere [Quote e limitazioni][lnk-quotas]).</span><span class="sxs-lookup"><span data-stu-id="9c1e1-122">IoT Hub enables millions of simultaneously connected devices (see [Quotas and throttling][lnk-quotas]).</span></span>
* <span data-ttu-id="9c1e1-123">L'hub IoT non consente il partizionamento arbitrario.</span><span class="sxs-lookup"><span data-stu-id="9c1e1-123">IoT Hub does not allow arbitrary partitioning.</span></span> <span data-ttu-id="9c1e1-124">I messaggi da dispositivo a cloud vengono partizionati in base al valore **deviceId**di origine.</span><span class="sxs-lookup"><span data-stu-id="9c1e1-124">Device-to-cloud messages are partitioned based on their originating **deviceId**.</span></span>

<span data-ttu-id="9c1e1-125">Per altre informazioni sulle differenze tra l'hub IoT e i servizi di hub eventi, vedere [Confronto tra l'hub IoT e Hub eventi di Azure][lnk-comparison].</span><span class="sxs-lookup"><span data-stu-id="9c1e1-125">For more information about the differences between the IoT Hub and Event Hubs services, see [Comparison of Azure IoT Hub and Azure Event Hubs][lnk-comparison].</span></span>

## <a name="send-non-telemetry-traffic"></a><span data-ttu-id="9c1e1-126">Invio di traffico non di telemetria</span><span class="sxs-lookup"><span data-stu-id="9c1e1-126">Send non-telemetry traffic</span></span>

<span data-ttu-id="9c1e1-127">Spesso, oltre ai punti dati di telemetria, i dispositivi inviano messaggi e richieste che devono essere eseguiti e gestiti separatamente nel back-end della soluzione.</span><span class="sxs-lookup"><span data-stu-id="9c1e1-127">Often, in addition to telemetry data points, devices send messages and requests that require separate execution and handling in the solution back end.</span></span> <span data-ttu-id="9c1e1-128">Ad esempio, gli avvisi critici che devono attivare un'azione specifica nel back-end.</span><span class="sxs-lookup"><span data-stu-id="9c1e1-128">For example, critical alerts that must trigger a specific action in the back end.</span></span> <span data-ttu-id="9c1e1-129">È possibile scrivere facilmente una [regola di routing][lnk-devguide-custom] per l'invio di questi tipi di messaggi a un endpoint dedicato alla loro elaborazione che si basa sull'intestazione del messaggio o su un valore del corpo del messaggio.</span><span class="sxs-lookup"><span data-stu-id="9c1e1-129">You can easily write a [routing rule][lnk-devguide-custom] to send these types of messages to an endpoint dedicated to their processing based on either a header on the message or a value in the message body.</span></span>

<span data-ttu-id="9c1e1-130">Per altre informazioni sul modo migliore di elaborare questo tipo di messaggio, vedere l'[Esercitazione: Elaborare messaggi da dispositivo a cloud dell'hub IoT usando .Net][lnk-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="9c1e1-130">For more information about the best way to process this kind of message, see the [Tutorial: How to process IoT Hub device-to-cloud messages][lnk-d2c-tutorial] tutorial.</span></span>

## <a name="route-device-to-cloud-messages"></a><span data-ttu-id="9c1e1-131">Routing di messaggi da dispositivo a cloud</span><span class="sxs-lookup"><span data-stu-id="9c1e1-131">Route device-to-cloud messages</span></span>

<span data-ttu-id="9c1e1-132">Sono disponibili due opzioni per il routing dei messaggi da dispositivo a cloud alle app back-end:</span><span class="sxs-lookup"><span data-stu-id="9c1e1-132">You have two options for routing device-to-cloud messages to your back-end apps:</span></span>

* <span data-ttu-id="9c1e1-133">Usare l'[endpoint compatibile con Hub eventi][lnk-compatible-endpoint] predefinito per consentire alle app back-end di leggere i messaggi da dispositivo a cloud ricevuti dall'hub.</span><span class="sxs-lookup"><span data-stu-id="9c1e1-133">Use the built-in [Event Hub-compatible endpoint][lnk-compatible-endpoint] to enable back-end apps to read the device-to-cloud messages received by the hub.</span></span> <span data-ttu-id="9c1e1-134">Per informazioni sull'endpoint compatibile con l'Hub eventi predefinito, vedere [Read device-to-cloud messages from the built-in endpoint][lnk-devguide-builtin] (Leggere i messaggi da dispositivo a cloud dall'endpoint predefinito).</span><span class="sxs-lookup"><span data-stu-id="9c1e1-134">To learn about the built-in Event Hub-compatible endpoint, see [Read device-to-cloud messages from the built-in endpoint][lnk-devguide-builtin].</span></span>
* <span data-ttu-id="9c1e1-135">Usare le regole di routing per inviare messaggi a endpoint personalizzati nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9c1e1-135">Use routing rules to send messages to custom endpoints in your IoT hub.</span></span> <span data-ttu-id="9c1e1-136">Gli endpoint personalizzati consentono alle app back-end di leggere i messaggi da dispositivo a cloud mediante gli hub eventi, le code o gli argomenti del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="9c1e1-136">Custom endpoints enable your back-end apps to read device-to-cloud messages using Event Hubs, Service Bus queues, or Service Bus topics.</span></span> <span data-ttu-id="9c1e1-137">Per informazioni sugli endpoint personalizzati e di routing, vedere [Usare endpoint e regole di routing personalizzati per i messaggi da dispositivo a cloud][lnk-devguide-custom].</span><span class="sxs-lookup"><span data-stu-id="9c1e1-137">To learn about routing and custom endpoints, see [Use custom endpoints and routing rules for device-to-cloud messages][lnk-devguide-custom].</span></span>

## <a name="anti-spoofing-properties"></a><span data-ttu-id="9c1e1-138">Proprietà anti-spoofing</span><span class="sxs-lookup"><span data-stu-id="9c1e1-138">Anti-spoofing properties</span></span>

<span data-ttu-id="9c1e1-139">Per evitare lo spoofing di dispositivi nei messaggi da dispositivo a cloud, l'hub IoT contrassegna tutti i messaggi con le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="9c1e1-139">To avoid device spoofing in device-to-cloud messages, IoT Hub stamps all messages with the following properties:</span></span>

* <span data-ttu-id="9c1e1-140">**ConnectionDeviceId**</span><span class="sxs-lookup"><span data-stu-id="9c1e1-140">**ConnectionDeviceId**</span></span>
* <span data-ttu-id="9c1e1-141">**ConnectionDeviceGenerationId**</span><span class="sxs-lookup"><span data-stu-id="9c1e1-141">**ConnectionDeviceGenerationId**</span></span>
* <span data-ttu-id="9c1e1-142">**ConnectionAuthMethod**</span><span class="sxs-lookup"><span data-stu-id="9c1e1-142">**ConnectionAuthMethod**</span></span>

<span data-ttu-id="9c1e1-143">Le prime due contengono le proprietà **deviceId** e **generationId** del dispositivo di origine, come indicato in [Proprietà delle identità dei dispositivi][lnk-device-properties].</span><span class="sxs-lookup"><span data-stu-id="9c1e1-143">The first two contain the **deviceId** and **generationId** of the originating device, as per [Device identity properties][lnk-device-properties].</span></span>

<span data-ttu-id="9c1e1-144">La proprietà **ConnectionAuthMethod** contiene un oggetto serializzato JSON con le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="9c1e1-144">The **ConnectionAuthMethod** property contains a JSON serialized object, with the following properties:</span></span>

```json
{
  "scope": "{ hub | device}",
  "type": "{ symkey | sas}",
  "issuer": "iothub"
}
```

## <a name="next-steps"></a><span data-ttu-id="9c1e1-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9c1e1-145">Next steps</span></span>

<span data-ttu-id="9c1e1-146">Per informazioni sugli SDK che è possibile usare per inviare i messaggi da dispositivo a cloud, vedere [Azure IoT SDK][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="9c1e1-146">For information about the SDKs you can use to send device-to-cloud messages, see [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="9c1e1-147">Le esercitazioni di [Introduzione][lnk-get-started] illustrano come inviare messaggi da dispositivo a cloud da dispositivi fisici e simulati.</span><span class="sxs-lookup"><span data-stu-id="9c1e1-147">The [Get Started][lnk-get-started] tutorials show you how to send device-to-cloud messages from both simulated and physical devices.</span></span> <span data-ttu-id="9c1e1-148">Per altre informazioni, vedere l'esercitazione [Elaborare messaggi da dispositivo a cloud dell'hub IoT usando i route][lnk-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="9c1e1-148">For more detail, see the [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

[lnk-devguide-builtin]: iot-hub-devguide-messages-read-builtin.md
[lnk-devguide-custom]: iot-hub-devguide-messages-read-custom.md
[lnk-comparison]: iot-hub-compare-event-hubs.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[lnk-get-started]: iot-hub-get-started.md

[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/
[lnk-servicebus]: http://azure.microsoft.com/documentation/services/service-bus/
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-compatible-endpoint]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-properties]: iot-hub-devguide-identity-registry.md#device-identity-properties
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
