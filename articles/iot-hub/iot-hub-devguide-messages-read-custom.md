---
title: endpoint personalizzati di Azure IoT Hub aaaUnderstand | Documenti Microsoft
description: Guida per sviluppatori - mediante routing regole endpoint toocustom di tooroute messaggi da dispositivo a cloud.
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
ms.openlocfilehash: daa9cfb35d0853e316bbf469b034d4dadbd4e85d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-message-routes-and-custom-endpoints-for-device-to-cloud-messages"></a><span data-ttu-id="0b15f-103">Usare endpoint personalizzati e il routing dei messaggi per i messaggi da dispositivo a cloud</span><span class="sxs-lookup"><span data-stu-id="0b15f-103">Use message routes and custom endpoints for device-to-cloud messages</span></span>

<span data-ttu-id="0b15f-104">IoT Hub consente tooroute [messaggi da dispositivo a cloud] [ lnk-device-to-cloud] tooIoT Hub endpoint orientati ai servizi in base alle proprietà del messaggio.</span><span class="sxs-lookup"><span data-stu-id="0b15f-104">IoT Hub enables you tooroute [device-to-cloud messages][lnk-device-to-cloud] tooIoT Hub service-facing endpoints based on message properties.</span></span> <span data-ttu-id="0b15f-105">Routing offrono regole si hello toosend flessibilità messaggi dove servono toogo senza hello necessitano per i messaggi di servizi aggiuntivi tooprocess o toowrite ulteriore codice.</span><span class="sxs-lookup"><span data-stu-id="0b15f-105">Routing rules give you hello flexibility toosend messages where they need toogo without hello need for additional services tooprocess messages or toowrite additional code.</span></span> <span data-ttu-id="0b15f-106">Configurare ogni regola di routing ha hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="0b15f-106">Each routing rule you configure has hello following properties:</span></span>

| <span data-ttu-id="0b15f-107">Proprietà</span><span class="sxs-lookup"><span data-stu-id="0b15f-107">Property</span></span>      | <span data-ttu-id="0b15f-108">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0b15f-108">Description</span></span> |
| ------------- | ----------- |
| <span data-ttu-id="0b15f-109">**Nome**</span><span class="sxs-lookup"><span data-stu-id="0b15f-109">**Name**</span></span>      | <span data-ttu-id="0b15f-110">nome univoco Hello che identifica la regola hello.</span><span class="sxs-lookup"><span data-stu-id="0b15f-110">hello unique name that identifies hello rule.</span></span> |
| <span data-ttu-id="0b15f-111">**Origine**</span><span class="sxs-lookup"><span data-stu-id="0b15f-111">**Source**</span></span>    | <span data-ttu-id="0b15f-112">il flusso di origine Hello dei dati di hello toobe intervenire.</span><span class="sxs-lookup"><span data-stu-id="0b15f-112">hello origin of hello data stream toobe acted upon.</span></span> <span data-ttu-id="0b15f-113">Ad esempio, i dati di telemetria del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0b15f-113">For example, device telemetry.</span></span> |
| <span data-ttu-id="0b15f-114">**Condition**</span><span class="sxs-lookup"><span data-stu-id="0b15f-114">**Condition**</span></span> | <span data-ttu-id="0b15f-115">espressione di query Hello per regola di routing hello che viene eseguito su intestazioni e corpo del messaggio hello e utilizzato toodetermine se si tratta di una corrispondenza per l'endpoint di hello.</span><span class="sxs-lookup"><span data-stu-id="0b15f-115">hello query expression for hello routing rule that is run against hello message's headers and body and used toodetermine whether it is a match for hello endpoint.</span></span> <span data-ttu-id="0b15f-116">Per ulteriori informazioni sulla creazione di una condizione di route, vedere hello [riferimento - linguaggio di query per gemelli di dispositivo e i processi][lnk-devguide-query-language].</span><span class="sxs-lookup"><span data-stu-id="0b15f-116">For more information about constructing a route condition, see hello [Reference - query language for device twins and jobs][lnk-devguide-query-language].</span></span> |
| <span data-ttu-id="0b15f-117">**Endpoint**</span><span class="sxs-lookup"><span data-stu-id="0b15f-117">**Endpoint**</span></span>  | <span data-ttu-id="0b15f-118">nome Hello dell'endpoint di hello in cui l'IoT Hub invia i messaggi che corrispondono alla condizione hello.</span><span class="sxs-lookup"><span data-stu-id="0b15f-118">hello name of hello endpoint where IoT Hub sends messages that match hello condition.</span></span> <span data-ttu-id="0b15f-119">Gli endpoint devono trovarsi in hello hub IoT hello stessa area, in caso contrario potrebbe essere addebitato per scrive tra aree.</span><span class="sxs-lookup"><span data-stu-id="0b15f-119">Endpoints should be in hello same region as hello IoT hub, otherwise you may be charged for cross-region writes.</span></span> |

<span data-ttu-id="0b15f-120">Un singolo messaggio può corrispondere a condizione di hello in più regole di routine, in cui caso IoT Hub offre endpoint toohello di messaggio hello associata a ogni regola corrispondente.</span><span class="sxs-lookup"><span data-stu-id="0b15f-120">A single message may match hello condition on multiple routing rules, in which case IoT Hub delivers hello message toohello endpoint associated with each matched rule.</span></span> <span data-ttu-id="0b15f-121">IoT Hub deduplicates automaticamente anche il recapito dei messaggi, pertanto se un messaggio corrisponde a più regole che hanno tutti hello stessa destinazione, ma viene scritto toothat destinazione una volta.</span><span class="sxs-lookup"><span data-stu-id="0b15f-121">IoT Hub also automatically deduplicates message delivery, so if a message matches multiple rules that all have hello same destination, it is only written toothat destination once.</span></span>

<span data-ttu-id="0b15f-122">Un hub IoT dispone di un [endpoint predefinito][lnk-built-in].</span><span class="sxs-lookup"><span data-stu-id="0b15f-122">An IoT hub has a default [built-in endpoint][lnk-built-in].</span></span> <span data-ttu-id="0b15f-123">È possibile creare endpoint personalizzati tooroute messaggi tooby collegamento altri servizi nell'hub toohello sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="0b15f-123">You can create custom endpoints tooroute messages tooby linking other services in your subscription toohello hub.</span></span> <span data-ttu-id="0b15f-124">L'hub IoT supporta attualmente l'Hub eventi, le code e gli argomenti del bus di servizio come endpoint personalizzati.</span><span class="sxs-lookup"><span data-stu-id="0b15f-124">IoT Hub currently supports Event Hubs, Service Bus queues, and Service Bus topics as custom endpoints.</span></span>

> [!WARNING]
> <span data-ttu-id="0b15f-125">Le code del bus di servizio e gli argomenti che hanno abilitato con **Sessioni** o **Rilevamento duplicati** non sono supportati come endpoint personalizzati.</span><span class="sxs-lookup"><span data-stu-id="0b15f-125">Service Bus queues and topics with **Sessions** or **Duplicate Detection** enabled are not supported as custom endpoints.</span></span>

<span data-ttu-id="0b15f-126">Per altre informazioni sulla creazione di endpoint personalizzati nell'hub IoT, vedere [Endpoint dell'hub IoT][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="0b15f-126">For more information about creating custom endpoints in IoT Hub, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="0b15f-127">Per altre informazioni sulla lettura da endpoint personalizzati, vedere:</span><span class="sxs-lookup"><span data-stu-id="0b15f-127">For more information about reading from custom endpoints, see:</span></span>

* <span data-ttu-id="0b15f-128">Lettura da [hub eventi][lnk-getstarted-eh].</span><span class="sxs-lookup"><span data-stu-id="0b15f-128">Reading from [Event Hubs][lnk-getstarted-eh].</span></span>
* <span data-ttu-id="0b15f-129">Lettura dalle [code del bus di servizio][lnk-getstarted-queue].</span><span class="sxs-lookup"><span data-stu-id="0b15f-129">Reading from [Service Bus queues][lnk-getstarted-queue].</span></span>
* <span data-ttu-id="0b15f-130">Lettura dagli [argomenti del bus di servizio][lnk-getstarted-topic].</span><span class="sxs-lookup"><span data-stu-id="0b15f-130">Reading from [Service Bus topics][lnk-getstarted-topic].</span></span>

### <a name="next-steps"></a><span data-ttu-id="0b15f-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0b15f-131">Next steps</span></span>

<span data-ttu-id="0b15f-132">Per altre informazioni sugli endpoint dell'hub IoT, vedere [Endpoint dell'hub IoT][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="0b15f-132">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="0b15f-133">Per ulteriori informazioni sul linguaggio di query hello utilizzare regole di routing toodefine, vedere [linguaggio di query IoT Hub per gemelli di dispositivo, processi e il routing dei messaggi][lnk-devguide-query-language].</span><span class="sxs-lookup"><span data-stu-id="0b15f-133">For more information about hello query language you use toodefine routing rules, see [IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query-language].</span></span>

<span data-ttu-id="0b15f-134">Hello [messaggi da dispositivo a cloud IoT Hub processo mediante route] [ lnk-d2c-tutorial] esercitazione viene illustrato come regole di routing toouse e gli endpoint personalizzati.</span><span class="sxs-lookup"><span data-stu-id="0b15f-134">hello [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial shows you how toouse routing rules and custom endpoints.</span></span>

[lnk-built-in]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-to-cloud]: iot-hub-devguide-messages-d2c.md
[lnk-devguide-query-language]: iot-hub-devguide-query-language.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-getstarted-eh]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-getstarted-queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[lnk-getstarted-topic]: ../service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions.md
