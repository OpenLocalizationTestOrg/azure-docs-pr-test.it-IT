---
title: Ridimensionamento dell'hub IoT di Azure | Microsoft Docs
description: "Come ridimensionare l'hub IoT per supportare la velocità effettiva dei messaggi prevista. Include un riepilogo della velocità effettiva supportata per ogni livello e le opzioni per il partizionamento orizzontale."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: e7bd4968-db46-46cf-865d-9c944f683832
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2cb263103da05b10c24aab71d81c43eb25987565
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="scale-your-iot-hub-solution"></a><span data-ttu-id="2aec7-104">Ridimensionare la soluzione hub IoT</span><span class="sxs-lookup"><span data-stu-id="2aec7-104">Scale your IoT hub solution</span></span>
<span data-ttu-id="2aec7-105">Hub IoT di Azure può supportare fino a un milione di dispositivi connessi contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="2aec7-105">Azure IoT Hub can support up to a million simultaneously connected devices.</span></span> <span data-ttu-id="2aec7-106">Per altre informazioni, vedere i [prezzi dell'hub IoT][lnk-pricing].</span><span class="sxs-lookup"><span data-stu-id="2aec7-106">For more information, see [IoT Hub pricing][lnk-pricing].</span></span> <span data-ttu-id="2aec7-107">Ogni unità hub IoT mette a disposizione un certo numero di messaggi giornalieri.</span><span class="sxs-lookup"><span data-stu-id="2aec7-107">Each IoT Hub unit allows a certain number of daily messages.</span></span>

<span data-ttu-id="2aec7-108">Per il ridimensionamento corretto della soluzione, considerare l'uso specifico che viene fatto dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2aec7-108">To properly scale your solution, consider your particular use of IoT Hub.</span></span> <span data-ttu-id="2aec7-109">In particolare, considerare la velocità effettiva di picco richiesta per le categorie di operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="2aec7-109">In particular, consider the required peak throughput for the following categories of operations:</span></span>

* <span data-ttu-id="2aec7-110">Messaggi da dispositivo a cloud</span><span class="sxs-lookup"><span data-stu-id="2aec7-110">Device-to-cloud messages</span></span>
* <span data-ttu-id="2aec7-111">Messaggi da cloud a dispositivo</span><span class="sxs-lookup"><span data-stu-id="2aec7-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="2aec7-112">Operazioni del registro delle identità</span><span class="sxs-lookup"><span data-stu-id="2aec7-112">Identity registry operations</span></span>

<span data-ttu-id="2aec7-113">Oltre alle informazioni sulla velocità effettiva, vedere le [quote e limitazioni dell'hub IoT][IoT Hub quotas and throttles] e progettare la propria soluzione di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="2aec7-113">In addition to this throughput information, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles] and design your solution accordingly.</span></span>

## <a name="device-to-cloud-and-cloud-to-device-message-throughput"></a><span data-ttu-id="2aec7-114">Velocità effettiva dei messaggi da dispositivo a cloud e da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2aec7-114">Device-to-cloud and cloud-to-device message throughput</span></span>
<span data-ttu-id="2aec7-115">Il modo migliore per definire le dimensioni di una soluzione hub IoT consiste nel valutare il traffico per unità.</span><span class="sxs-lookup"><span data-stu-id="2aec7-115">The best way to size an IoT Hub solution is to evaluate the traffic on a per-unit basis.</span></span>

<span data-ttu-id="2aec7-116">I messaggi da dispositivo a cloud seguono queste linee guida in caso di velocità effettiva sostenuta</span><span class="sxs-lookup"><span data-stu-id="2aec7-116">Device-to-cloud messages follow these sustained throughput guidelines.</span></span>

| <span data-ttu-id="2aec7-117">Livello</span><span class="sxs-lookup"><span data-stu-id="2aec7-117">Tier</span></span> | <span data-ttu-id="2aec7-118">Velocità effettiva sostenuta</span><span class="sxs-lookup"><span data-stu-id="2aec7-118">Sustained throughput</span></span> | <span data-ttu-id="2aec7-119">Frequenza di invio sostenuta</span><span class="sxs-lookup"><span data-stu-id="2aec7-119">Sustained send rate</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2aec7-120">S1</span><span class="sxs-lookup"><span data-stu-id="2aec7-120">S1</span></span> |<span data-ttu-id="2aec7-121">Fino a 1.111 KB al minuto per unità</span><span class="sxs-lookup"><span data-stu-id="2aec7-121">Up to 1111 KB/minute per unit</span></span><br/><span data-ttu-id="2aec7-122">(1,5 GB al giorno per unità)</span><span class="sxs-lookup"><span data-stu-id="2aec7-122">(1.5 GB/day/unit)</span></span> |<span data-ttu-id="2aec7-123">Una media di 278 messaggi al minuto per unità</span><span class="sxs-lookup"><span data-stu-id="2aec7-123">Average of 278 messages/minute per unit</span></span><br/><span data-ttu-id="2aec7-124">(400.000 messaggi al giorno per unità)</span><span class="sxs-lookup"><span data-stu-id="2aec7-124">(400,000 messages/day per unit)</span></span> |
| <span data-ttu-id="2aec7-125">S2</span><span class="sxs-lookup"><span data-stu-id="2aec7-125">S2</span></span> |<span data-ttu-id="2aec7-126">Fino a 16 MB al minuto per unità</span><span class="sxs-lookup"><span data-stu-id="2aec7-126">Up to 16 MB/minute per unit</span></span><br/><span data-ttu-id="2aec7-127">(22,8 GB al giorno per unità)</span><span class="sxs-lookup"><span data-stu-id="2aec7-127">(22.8 GB/day/unit)</span></span> |<span data-ttu-id="2aec7-128">Una media di 4.167 messaggi al minuto per unità</span><span class="sxs-lookup"><span data-stu-id="2aec7-128">Average of 4,167 messages/minute per unit</span></span><br/><span data-ttu-id="2aec7-129">(6 milioni di messaggi al giorno per unità)</span><span class="sxs-lookup"><span data-stu-id="2aec7-129">(6 million messages/day per unit)</span></span> |
| <span data-ttu-id="2aec7-130">S3</span><span class="sxs-lookup"><span data-stu-id="2aec7-130">S3</span></span> |<span data-ttu-id="2aec7-131">Fino a 814 MB al minuto per unità</span><span class="sxs-lookup"><span data-stu-id="2aec7-131">Up to 814 MB/minute per unit</span></span><br/><span data-ttu-id="2aec7-132">(1144,4 GB al giorno per unità)</span><span class="sxs-lookup"><span data-stu-id="2aec7-132">(1144.4 GB/day/unit)</span></span> |<span data-ttu-id="2aec7-133">Una media di 208,333 messaggi al minuto per unità</span><span class="sxs-lookup"><span data-stu-id="2aec7-133">Average of 208,333 messages/minute per unit</span></span><br/><span data-ttu-id="2aec7-134">(300 milioni di messaggi al giorno per unità)</span><span class="sxs-lookup"><span data-stu-id="2aec7-134">(300 million messages/day per unit)</span></span> |

## <a name="identity-registry-operation-throughput"></a><span data-ttu-id="2aec7-135">Velocità effettiva delle operazioni del registro delle identità</span><span class="sxs-lookup"><span data-stu-id="2aec7-135">Identity registry operation throughput</span></span>
<span data-ttu-id="2aec7-136">Le operazioni del registro delle identità dell'hub IoT non sono considerate operazioni di runtime perché sono per lo più correlate al provisioning dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="2aec7-136">IoT Hub identity registry operations are not supposed to be run-time operations, as they are mostly related to device provisioning.</span></span>

<span data-ttu-id="2aec7-137">Per i dati specifici sulle prestazioni in modalità burst, vedere le [quote e limitazioni dell'hub IoT][IoT Hub quotas and throttles].</span><span class="sxs-lookup"><span data-stu-id="2aec7-137">For specific burst performance numbers, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles].</span></span>

## <a name="sharding"></a><span data-ttu-id="2aec7-138">Partizionamento orizzontale</span><span class="sxs-lookup"><span data-stu-id="2aec7-138">Sharding</span></span>
<span data-ttu-id="2aec7-139">Mentre un hub IoT può essere ridimensionato fino a milioni di dispositivi, a volte la soluzione richiede caratteristiche di prestazioni specifiche che un singolo hub IoT non può garantire.</span><span class="sxs-lookup"><span data-stu-id="2aec7-139">While a single IoT hub can scale to millions of devices, sometimes your solution requires specific performance characteristics that a single IoT hub cannot guarantee.</span></span> <span data-ttu-id="2aec7-140">In tal caso, è consigliabile partizionare i dispositivi in più hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2aec7-140">In that case, it is recommended that you partition your devices into multiple IoT hubs.</span></span> <span data-ttu-id="2aec7-141">Più hub IoT appianano i picchi di traffico e ottengono il throughput necessario o i tassi di operazione richiesti.</span><span class="sxs-lookup"><span data-stu-id="2aec7-141">Multiple IoT hubs smooth traffic bursts and obtain the required throughput or operation rates that are required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2aec7-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2aec7-142">Next steps</span></span>
<span data-ttu-id="2aec7-143">Per altre informazioni sulle funzionalità dell'hub IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="2aec7-143">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="2aec7-144">[Guida per gli sviluppatori dell'hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="2aec7-144">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="2aec7-145">[Simulazione di un dispositivo con Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="2aec7-145">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[IoT Hub quotas and throttles]: iot-hub-devguide-quotas-throttling.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
