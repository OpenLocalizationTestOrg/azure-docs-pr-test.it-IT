---
title: Conoscere gli endpoint personalizzati di Hub IoTdi Azure | Microsoft Docs
description: 'Guida per gli sviluppatori: uso delle regole di routing per instradare i messaggi da dispositivo a cloud per gli endpoint personalizzati.'
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
ms.openlocfilehash: a21f1c61f344f96e2e03422e41fd8c5f7f841a0c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-message-routes-and-custom-endpoints-for-device-to-cloud-messages"></a><span data-ttu-id="8e400-103">Usare endpoint personalizzati e il routing dei messaggi per i messaggi da dispositivo a cloud</span><span class="sxs-lookup"><span data-stu-id="8e400-103">Use message routes and custom endpoints for device-to-cloud messages</span></span>

<span data-ttu-id="8e400-104">L'hub IoT consente di eseguire il routing dei [messaggi da dispositivo a cloud][lnk-device-to-cloud] agli endpoint per il servizio dellhub IoT in base alle proprietà dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="8e400-104">IoT Hub enables you to route [device-to-cloud messages][lnk-device-to-cloud] to IoT Hub service-facing endpoints based on message properties.</span></span> <span data-ttu-id="8e400-105">Le regole di routing offrono la flessibilità necessaria per inviare messaggi alle destinazioni desiderate, senza dover attivare altri servizi per elaborare i messaggi o scrivere codice aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="8e400-105">Routing rules give you the flexibility to send messages where they need to go without the need for additional services to process messages or to write additional code.</span></span> <span data-ttu-id="8e400-106">Ogni regola di routing configurata ha le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="8e400-106">Each routing rule you configure has the following properties:</span></span>

| <span data-ttu-id="8e400-107">Proprietà</span><span class="sxs-lookup"><span data-stu-id="8e400-107">Property</span></span>      | <span data-ttu-id="8e400-108">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8e400-108">Description</span></span> |
| ------------- | ----------- |
| <span data-ttu-id="8e400-109">**Nome**</span><span class="sxs-lookup"><span data-stu-id="8e400-109">**Name**</span></span>      | <span data-ttu-id="8e400-110">Il nome univoco che identifica la regola.</span><span class="sxs-lookup"><span data-stu-id="8e400-110">The unique name that identifies the rule.</span></span> |
| <span data-ttu-id="8e400-111">**Origine**</span><span class="sxs-lookup"><span data-stu-id="8e400-111">**Source**</span></span>    | <span data-ttu-id="8e400-112">L'origine del flusso dati su cui intervenire.</span><span class="sxs-lookup"><span data-stu-id="8e400-112">The origin of the data stream to be acted upon.</span></span> <span data-ttu-id="8e400-113">Ad esempio, i dati di telemetria del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8e400-113">For example, device telemetry.</span></span> |
| <span data-ttu-id="8e400-114">**Condition**</span><span class="sxs-lookup"><span data-stu-id="8e400-114">**Condition**</span></span> | <span data-ttu-id="8e400-115">L'espressione di query per la regola di routing che viene eseguita rispetto alle intestazione e al corpo del messaggio e usata per determinare se si tratti di una corrispondenza per l'endpoint.</span><span class="sxs-lookup"><span data-stu-id="8e400-115">The query expression for the routing rule that is run against the message's headers and body and used to determine whether it is a match for the endpoint.</span></span> <span data-ttu-id="8e400-116">Per altre informazioni sulla creazione di una condizione di route, vedere il [Riferimento: linguaggio query per dispositivi gemelli e processi][lnk-devguide-query-language].</span><span class="sxs-lookup"><span data-stu-id="8e400-116">For more information about constructing a route condition, see the [Reference - query language for device twins and jobs][lnk-devguide-query-language].</span></span> |
| <span data-ttu-id="8e400-117">**Endpoint**</span><span class="sxs-lookup"><span data-stu-id="8e400-117">**Endpoint**</span></span>  | <span data-ttu-id="8e400-118">Il nome dell'endpoint dove l'hub IoT invia i messaggi corrispondenti alla condizione.</span><span class="sxs-lookup"><span data-stu-id="8e400-118">The name of the endpoint where IoT Hub sends messages that match the condition.</span></span> <span data-ttu-id="8e400-119">Gli endpoint devono trovarsi nella stessa area dell'hub IoT, in caso contrario potrebbero essere addebitati dei costi per le scritture tra aree.</span><span class="sxs-lookup"><span data-stu-id="8e400-119">Endpoints should be in the same region as the IoT hub, otherwise you may be charged for cross-region writes.</span></span> |

<span data-ttu-id="8e400-120">Un singolo messaggio può corrispondere alla condizione su più regole di routing. In questo caso, l'hub IoT invia il messaggio all'endpoint associato a ciascuna regola corrispondente.</span><span class="sxs-lookup"><span data-stu-id="8e400-120">A single message may match the condition on multiple routing rules, in which case IoT Hub delivers the message to the endpoint associated with each matched rule.</span></span> <span data-ttu-id="8e400-121">L'hub IoT deduplica automaticamente la consegna dei messaggi, quindi se uno di questi corrisponde a più regole che hanno tutte la stessa destinazione, verrà scritto in quella destinazione una sola volta.</span><span class="sxs-lookup"><span data-stu-id="8e400-121">IoT Hub also automatically deduplicates message delivery, so if a message matches multiple rules that all have the same destination, it is only written to that destination once.</span></span>

<span data-ttu-id="8e400-122">Un hub IoT dispone di un [endpoint predefinito][lnk-built-in].</span><span class="sxs-lookup"><span data-stu-id="8e400-122">An IoT hub has a default [built-in endpoint][lnk-built-in].</span></span> <span data-ttu-id="8e400-123">È possibile creare endpoint personalizzati per indirizzare i messaggi collegando all'hub gli altri servizi nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="8e400-123">You can create custom endpoints to route messages to by linking other services in your subscription to the hub.</span></span> <span data-ttu-id="8e400-124">L'hub IoT supporta attualmente l'Hub eventi, le code e gli argomenti del bus di servizio come endpoint personalizzati.</span><span class="sxs-lookup"><span data-stu-id="8e400-124">IoT Hub currently supports Event Hubs, Service Bus queues, and Service Bus topics as custom endpoints.</span></span>

> [!WARNING]
> <span data-ttu-id="8e400-125">Le code del bus di servizio e gli argomenti che hanno abilitato con **Sessioni** o **Rilevamento duplicati** non sono supportati come endpoint personalizzati.</span><span class="sxs-lookup"><span data-stu-id="8e400-125">Service Bus queues and topics with **Sessions** or **Duplicate Detection** enabled are not supported as custom endpoints.</span></span>

<span data-ttu-id="8e400-126">Per altre informazioni sulla creazione di endpoint personalizzati nell'hub IoT, vedere [Endpoint dell'hub IoT][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="8e400-126">For more information about creating custom endpoints in IoT Hub, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="8e400-127">Per altre informazioni sulla lettura da endpoint personalizzati, vedere:</span><span class="sxs-lookup"><span data-stu-id="8e400-127">For more information about reading from custom endpoints, see:</span></span>

* <span data-ttu-id="8e400-128">Lettura da [hub eventi][lnk-getstarted-eh].</span><span class="sxs-lookup"><span data-stu-id="8e400-128">Reading from [Event Hubs][lnk-getstarted-eh].</span></span>
* <span data-ttu-id="8e400-129">Lettura dalle [code del bus di servizio][lnk-getstarted-queue].</span><span class="sxs-lookup"><span data-stu-id="8e400-129">Reading from [Service Bus queues][lnk-getstarted-queue].</span></span>
* <span data-ttu-id="8e400-130">Lettura dagli [argomenti del bus di servizio][lnk-getstarted-topic].</span><span class="sxs-lookup"><span data-stu-id="8e400-130">Reading from [Service Bus topics][lnk-getstarted-topic].</span></span>

### <a name="next-steps"></a><span data-ttu-id="8e400-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8e400-131">Next steps</span></span>

<span data-ttu-id="8e400-132">Per altre informazioni sugli endpoint dell'hub IoT, vedere [Endpoint dell'hub IoT][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="8e400-132">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="8e400-133">Per altre informazioni sul linguaggio di query che è possibile per definire le regole di routing, vedere [Linguaggio di query dell'hub IoT per dispositivi gemelli, processi e routing dei messaggi][lnk-devguide-query-language].</span><span class="sxs-lookup"><span data-stu-id="8e400-133">For more information about the query language you use to define routing rules, see [IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query-language].</span></span>

<span data-ttu-id="8e400-134">L'esercitazione [Elaborare messaggi da dispositivo a cloud dell'hub IoT usando i route][lnk-d2c-tutorial] illustra come usare le regole di routing e gli endpoint personalizzati.</span><span class="sxs-lookup"><span data-stu-id="8e400-134">The [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial shows you how to use routing rules and custom endpoints.</span></span>

[lnk-built-in]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-to-cloud]: iot-hub-devguide-messages-d2c.md
[lnk-devguide-query-language]: iot-hub-devguide-query-language.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-getstarted-eh]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-getstarted-queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[lnk-getstarted-topic]: ../service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions.md
