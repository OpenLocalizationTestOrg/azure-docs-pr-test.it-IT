---
title: messaggistica di dispositivo a cloud Azure IoT Hub aaaUnderstand | Documenti Microsoft
description: Guida per sviluppatori - come toouse dispositivo a cloud con l'IoT Hub di messaggistica. Include informazioni sull'invio di dati di telemetria e non telemtry e l'utilizzo di routing dei messaggi toodeliver.
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
ms.openlocfilehash: 07dc8a6be747365c7efbc528ab2762b0d9790758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="send-device-to-cloud-messages-tooiot-hub"></a><span data-ttu-id="2eb47-104">Inviare i messaggi da dispositivo a cloud tooIoT Hub</span><span class="sxs-lookup"><span data-stu-id="2eb47-104">Send device-to-cloud messages tooIoT Hub</span></span>

<span data-ttu-id="2eb47-105">toosend telemetria di serie temporali e gli avvisi generati da dispositivi tooyour soluzione back-end del, inviare i messaggi da dispositivo a cloud dall'hub IoT tooyour di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2eb47-105">toosend time-series telemetry and alerts from your devices tooyour solution back end, send device-to-cloud messages from your device tooyour IoT hub.</span></span> <span data-ttu-id="2eb47-106">Per una descrizione delle altre opzioni da dispositivo a cloud supportate dall'hub IoT, vedere [Indicazioni sulle comunicazioni da dispositivo a cloud][lnk-d2c-guidance].</span><span class="sxs-lookup"><span data-stu-id="2eb47-106">For a discussion of other device-to-cloud options supported by IoT Hub, see [Device-to-cloud communications guidance][lnk-d2c-guidance].</span></span>

<span data-ttu-id="2eb47-107">I messaggi da dispositivo a cloud vengono inviati tramite un endpoint per il dispositivo (**/devices/{deviceId}/messages/events**).</span><span class="sxs-lookup"><span data-stu-id="2eb47-107">You send device-to-cloud messages through a device-facing endpoint (**/devices/{deviceId}/messages/events**).</span></span> <span data-ttu-id="2eb47-108">Regole di routing, quindi indirizzare tooone i messaggi di endpoint servizio Web hello l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2eb47-108">Routing rules then route your messages tooone of hello service-facing endpoints on your IoT hub.</span></span> <span data-ttu-id="2eb47-109">Regole di routing utilizzano hello intestazioni e corpo dei messaggi da dispositivo a cloud hello che passano attraverso il toodetermine hub in cui tooroute li.</span><span class="sxs-lookup"><span data-stu-id="2eb47-109">Routing rules use hello headers and body of hello device-to-cloud messages flowing through your hub toodetermine where tooroute them.</span></span> <span data-ttu-id="2eb47-110">Per impostazione predefinita, i messaggi vengono indirizzati toohello incorporato orientati ai servizi endpoint (**messaggi di eventi**), che è compatibile con [hub eventi][lnk-event-hubs].</span><span class="sxs-lookup"><span data-stu-id="2eb47-110">By default, messages are routed toohello built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="2eb47-111">Pertanto, è possibile utilizzare standard [integrazione degli hub di eventi e SDK] [ lnk-compatible-endpoint] messaggi da dispositivo a cloud tooreceive nella soluzione di back-end.</span><span class="sxs-lookup"><span data-stu-id="2eb47-111">Therefore, you can use standard [Event Hubs integration and SDKs][lnk-compatible-endpoint] tooreceive device-to-cloud messages in your solution back end.</span></span>

<span data-ttu-id="2eb47-112">L'hub IoT implementa la messaggistica da dispositivo a cloud usando un modello di messaggistica di flusso.</span><span class="sxs-lookup"><span data-stu-id="2eb47-112">IoT Hub implements device-to-cloud messaging using a streaming messaging pattern.</span></span> <span data-ttu-id="2eb47-113">I messaggi da dispositivo a cloud dell'IoT Hub sono più simili [hub eventi] [ lnk-event-hubs] *eventi* di [Bus di servizio] [ lnk-servicebus] *messaggi* e non è presente un numero elevato di eventi passano attraverso il servizio di hello che possa essere letto da più lettori.</span><span class="sxs-lookup"><span data-stu-id="2eb47-113">IoT Hub's device-to-cloud messages are more like [Event Hubs][lnk-event-hubs] *events* than [Service Bus][lnk-servicebus] *messages* in that there is a high volume of events passing through hello service that can be read by multiple readers.</span></span>

<span data-ttu-id="2eb47-114">Messaggistica con l'IoT Hub dispositivo a cloud presenta hello seguenti caratteristiche:</span><span class="sxs-lookup"><span data-stu-id="2eb47-114">Device-to-cloud messaging with IoT Hub has hello following characteristics:</span></span>

* <span data-ttu-id="2eb47-115">I messaggi da dispositivo a cloud sono durevoli e mantenuto nel predefinito di un hub IoT **messaggi di eventi** endpoint per i giorni tooseven.</span><span class="sxs-lookup"><span data-stu-id="2eb47-115">Device-to-cloud messages are durable and retained in an IoT hub's default **messages/events** endpoint for up tooseven days.</span></span>
* <span data-ttu-id="2eb47-116">I messaggi da dispositivo a cloud possono contenere al massimo 256 KB e possono essere raggruppati in batch toooptimize Invia.</span><span class="sxs-lookup"><span data-stu-id="2eb47-116">Device-to-cloud messages can be at most 256 KB, and can be grouped in batches toooptimize sends.</span></span> <span data-ttu-id="2eb47-117">I batch possono avere dimensioni massime pari a 256 KB.</span><span class="sxs-lookup"><span data-stu-id="2eb47-117">Batches can be at most 256 KB.</span></span>
* <span data-ttu-id="2eb47-118">Come spiegato in hello [tooIoT accesso controllo Hub] [ lnk-devguide-security] sezione IoT Hub consente il controllo di autenticazione e accesso al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2eb47-118">As explained in hello [Control access tooIoT Hub][lnk-devguide-security] section, IoT Hub enables per-device authentication and access control.</span></span>
* <span data-ttu-id="2eb47-119">IoT Hub consente toocreate too10 contenuto personalizzato degli endpoint.</span><span class="sxs-lookup"><span data-stu-id="2eb47-119">IoT Hub allows you toocreate up too10 custom endpoints.</span></span> <span data-ttu-id="2eb47-120">I messaggi vengono recapitati endpoint toohello in base a route configurate sull'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2eb47-120">Messages are delivered toohello endpoints based on routes configured on your IoT hub.</span></span> <span data-ttu-id="2eb47-121">Per altre informazioni, vedere [Regole di routing](#routing-rules).</span><span class="sxs-lookup"><span data-stu-id="2eb47-121">For more information, see [Routing rules](#routing-rules).</span></span>
* <span data-ttu-id="2eb47-122">L'hub IoT abilita milioni di dispositivi connessi contemporaneamente (vedere [Quote e limitazioni][lnk-quotas]).</span><span class="sxs-lookup"><span data-stu-id="2eb47-122">IoT Hub enables millions of simultaneously connected devices (see [Quotas and throttling][lnk-quotas]).</span></span>
* <span data-ttu-id="2eb47-123">L'hub IoT non consente il partizionamento arbitrario.</span><span class="sxs-lookup"><span data-stu-id="2eb47-123">IoT Hub does not allow arbitrary partitioning.</span></span> <span data-ttu-id="2eb47-124">I messaggi da dispositivo a cloud vengono partizionati in base al valore **deviceId**di origine.</span><span class="sxs-lookup"><span data-stu-id="2eb47-124">Device-to-cloud messages are partitioned based on their originating **deviceId**.</span></span>

<span data-ttu-id="2eb47-125">Per ulteriori informazioni sulle differenze hello hello IoT Hub e servizi di hub eventi, vedere [hub eventi di Azure e di confronto di IoT Hub Azure][lnk-comparison].</span><span class="sxs-lookup"><span data-stu-id="2eb47-125">For more information about hello differences between hello IoT Hub and Event Hubs services, see [Comparison of Azure IoT Hub and Azure Event Hubs][lnk-comparison].</span></span>

## <a name="send-non-telemetry-traffic"></a><span data-ttu-id="2eb47-126">Invio di traffico non di telemetria</span><span class="sxs-lookup"><span data-stu-id="2eb47-126">Send non-telemetry traffic</span></span>

<span data-ttu-id="2eb47-127">Spesso, i dispositivi inoltre dati tootelemetry punta, inviano i messaggi e le richieste che necessitano di esecuzione separato e operazioni di gestione nel back-end di hello soluzione.</span><span class="sxs-lookup"><span data-stu-id="2eb47-127">Often, in addition tootelemetry data points, devices send messages and requests that require separate execution and handling in hello solution back end.</span></span> <span data-ttu-id="2eb47-128">Ad esempio, gli avvisi critici che devono attivare un'azione specifica in hello back-end.</span><span class="sxs-lookup"><span data-stu-id="2eb47-128">For example, critical alerts that must trigger a specific action in hello back end.</span></span> <span data-ttu-id="2eb47-129">È possibile scrivere facilmente un [regola di routing] [ lnk-devguide-custom] toosend questi tipi di endpoint tooan messaggi dedicato tootheir un'elaborazione basata su un'intestazione di messaggio hello o un valore nel corpo del messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="2eb47-129">You can easily write a [routing rule][lnk-devguide-custom] toosend these types of messages tooan endpoint dedicated tootheir processing based on either a header on hello message or a value in hello message body.</span></span>

<span data-ttu-id="2eb47-130">Per ulteriori informazioni su hello migliore modo tooprocess questo tipo di messaggio, vedere hello [esercitazione: come i messaggi da dispositivo a cloud IoT Hub tooprocess] [ lnk-d2c-tutorial] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2eb47-130">For more information about hello best way tooprocess this kind of message, see hello [Tutorial: How tooprocess IoT Hub device-to-cloud messages][lnk-d2c-tutorial] tutorial.</span></span>

## <a name="route-device-to-cloud-messages"></a><span data-ttu-id="2eb47-131">Routing di messaggi da dispositivo a cloud</span><span class="sxs-lookup"><span data-stu-id="2eb47-131">Route device-to-cloud messages</span></span>

<span data-ttu-id="2eb47-132">Sono disponibili due opzioni per le applicazioni back-end tooyour di routing messaggi da dispositivo a cloud:</span><span class="sxs-lookup"><span data-stu-id="2eb47-132">You have two options for routing device-to-cloud messages tooyour back-end apps:</span></span>

* <span data-ttu-id="2eb47-133">Utilizzare hello incorporato [endpoint compatibile con Hub eventi] [ lnk-compatible-endpoint] tooenable back-end App tooread hello dispositivo a cloud per i messaggi ricevuti dall'hub hello.</span><span class="sxs-lookup"><span data-stu-id="2eb47-133">Use hello built-in [Event Hub-compatible endpoint][lnk-compatible-endpoint] tooenable back-end apps tooread hello device-to-cloud messages received by hello hub.</span></span> <span data-ttu-id="2eb47-134">toolearn su endpoint compatibili con Hub eventi predefiniti di hello, vedere [leggere messaggi da dispositivo a cloud da endpoint predefiniti hello][lnk-devguide-builtin].</span><span class="sxs-lookup"><span data-stu-id="2eb47-134">toolearn about hello built-in Event Hub-compatible endpoint, see [Read device-to-cloud messages from hello built-in endpoint][lnk-devguide-builtin].</span></span>
* <span data-ttu-id="2eb47-135">Utilizzare gli endpoint toocustom di routing regole toosend messaggi nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2eb47-135">Use routing rules toosend messages toocustom endpoints in your IoT hub.</span></span> <span data-ttu-id="2eb47-136">Gli endpoint personalizzati consentono i messaggi di dispositivo a cloud tooread applicazioni back-end tramite gli hub di eventi, le code del Bus di servizio o gli argomenti del Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="2eb47-136">Custom endpoints enable your back-end apps tooread device-to-cloud messages using Event Hubs, Service Bus queues, or Service Bus topics.</span></span> <span data-ttu-id="2eb47-137">toolearn sugli endpoint personalizzati e routing, vedere [usare endpoint personalizzati e le regole di routing per i messaggi da dispositivo a cloud][lnk-devguide-custom].</span><span class="sxs-lookup"><span data-stu-id="2eb47-137">toolearn about routing and custom endpoints, see [Use custom endpoints and routing rules for device-to-cloud messages][lnk-devguide-custom].</span></span>

## <a name="anti-spoofing-properties"></a><span data-ttu-id="2eb47-138">Proprietà anti-spoofing</span><span class="sxs-lookup"><span data-stu-id="2eb47-138">Anti-spoofing properties</span></span>

<span data-ttu-id="2eb47-139">dispositivo tooavoid lo spoofing degli indirizzi nei messaggi da dispositivo a cloud, l'IoT Hub timbri tutti i messaggi con hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="2eb47-139">tooavoid device spoofing in device-to-cloud messages, IoT Hub stamps all messages with hello following properties:</span></span>

* <span data-ttu-id="2eb47-140">**ConnectionDeviceId**</span><span class="sxs-lookup"><span data-stu-id="2eb47-140">**ConnectionDeviceId**</span></span>
* <span data-ttu-id="2eb47-141">**ConnectionDeviceGenerationId**</span><span class="sxs-lookup"><span data-stu-id="2eb47-141">**ConnectionDeviceGenerationId**</span></span>
* <span data-ttu-id="2eb47-142">**ConnectionAuthMethod**</span><span class="sxs-lookup"><span data-stu-id="2eb47-142">**ConnectionAuthMethod**</span></span>

<span data-ttu-id="2eb47-143">Hello innanzitutto due contengono hello **deviceId** e **generationId** di hello originari dispositivo, in base [le proprietà di identità dispositivo][lnk-device-properties].</span><span class="sxs-lookup"><span data-stu-id="2eb47-143">hello first two contain hello **deviceId** and **generationId** of hello originating device, as per [Device identity properties][lnk-device-properties].</span></span>

<span data-ttu-id="2eb47-144">Hello **ConnectionAuthMethod** proprietà contiene un oggetto JSON serializzato, con hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="2eb47-144">hello **ConnectionAuthMethod** property contains a JSON serialized object, with hello following properties:</span></span>

```json
{
  "scope": "{ hub | device}",
  "type": "{ symkey | sas}",
  "issuer": "iothub"
}
```

## <a name="next-steps"></a><span data-ttu-id="2eb47-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2eb47-145">Next steps</span></span>

<span data-ttu-id="2eb47-146">Per informazioni sul SDK di hello è possibile utilizzare i messaggi da dispositivo a cloud toosend, vedere [Azure IoT SDK][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="2eb47-146">For information about hello SDKs you can use toosend device-to-cloud messages, see [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="2eb47-147">Hello [iniziare] [ lnk-get-started] le esercitazioni illustrano come toosend dispositivo a cloud messaggi da dispositivi fisici sia simulati.</span><span class="sxs-lookup"><span data-stu-id="2eb47-147">hello [Get Started][lnk-get-started] tutorials show you how toosend device-to-cloud messages from both simulated and physical devices.</span></span> <span data-ttu-id="2eb47-148">Per ulteriori dettagli, vedere hello [messaggi da dispositivo a cloud IoT Hub processo mediante route] [ lnk-d2c-tutorial] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2eb47-148">For more detail, see hello [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

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
