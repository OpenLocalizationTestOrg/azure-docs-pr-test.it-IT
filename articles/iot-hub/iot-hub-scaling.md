---
title: "scalabilità Hub IoT aaaAzure | Documenti Microsoft"
description: "Come tooscale il toosupport hub IoT la velocità effettiva dei messaggi previsti. Include un riepilogo delle opzioni per il partizionamento orizzontale e velocità effettiva di hello è supportato per ogni livello."
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
ms.openlocfilehash: 3b8bf6c44631c65b34b69752d9043c21db24bb01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-your-iot-hub-solution"></a><span data-ttu-id="75db6-104">Ridimensionare la soluzione hub IoT</span><span class="sxs-lookup"><span data-stu-id="75db6-104">Scale your IoT hub solution</span></span>
<span data-ttu-id="75db6-105">IoT Hub Azure può supportare i dispositivi connessi contemporaneamente milioni tooa.</span><span class="sxs-lookup"><span data-stu-id="75db6-105">Azure IoT Hub can support up tooa million simultaneously connected devices.</span></span> <span data-ttu-id="75db6-106">Per altre informazioni, vedere i [prezzi dell'hub IoT][lnk-pricing].</span><span class="sxs-lookup"><span data-stu-id="75db6-106">For more information, see [IoT Hub pricing][lnk-pricing].</span></span> <span data-ttu-id="75db6-107">Ogni unità hub IoT mette a disposizione un certo numero di messaggi giornalieri.</span><span class="sxs-lookup"><span data-stu-id="75db6-107">Each IoT Hub unit allows a certain number of daily messages.</span></span>

<span data-ttu-id="75db6-108">tooproperly ampliamento della soluzione, considerare l'utilizzo dell'IoT Hub in questione.</span><span class="sxs-lookup"><span data-stu-id="75db6-108">tooproperly scale your solution, consider your particular use of IoT Hub.</span></span> <span data-ttu-id="75db6-109">In particolare, valutare una velocità effettiva di picco hello necessario per hello categorie delle operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="75db6-109">In particular, consider hello required peak throughput for hello following categories of operations:</span></span>

* <span data-ttu-id="75db6-110">Messaggi da dispositivo a cloud</span><span class="sxs-lookup"><span data-stu-id="75db6-110">Device-to-cloud messages</span></span>
* <span data-ttu-id="75db6-111">Messaggi da cloud a dispositivo</span><span class="sxs-lookup"><span data-stu-id="75db6-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="75db6-112">Operazioni del registro delle identità</span><span class="sxs-lookup"><span data-stu-id="75db6-112">Identity registry operations</span></span>

<span data-ttu-id="75db6-113">Nelle informazioni di velocità effettiva di addizione toothis, vedere [IoT Hub quote e velocità] [ IoT Hub quotas and throttles] e progettare di conseguenza la soluzione.</span><span class="sxs-lookup"><span data-stu-id="75db6-113">In addition toothis throughput information, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles] and design your solution accordingly.</span></span>

## <a name="device-to-cloud-and-cloud-to-device-message-throughput"></a><span data-ttu-id="75db6-114">Velocità effettiva dei messaggi da dispositivo a cloud e da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="75db6-114">Device-to-cloud and cloud-to-device message throughput</span></span>
<span data-ttu-id="75db6-115">Hello migliore modo toosize una soluzione di IoT Hub è traffico hello tooevaluate singolo per unità.</span><span class="sxs-lookup"><span data-stu-id="75db6-115">hello best way toosize an IoT Hub solution is tooevaluate hello traffic on a per-unit basis.</span></span>

<span data-ttu-id="75db6-116">I messaggi da dispositivo a cloud seguono queste linee guida in caso di velocità effettiva sostenuta</span><span class="sxs-lookup"><span data-stu-id="75db6-116">Device-to-cloud messages follow these sustained throughput guidelines.</span></span>

| <span data-ttu-id="75db6-117">Livello</span><span class="sxs-lookup"><span data-stu-id="75db6-117">Tier</span></span> | <span data-ttu-id="75db6-118">Velocità effettiva sostenuta</span><span class="sxs-lookup"><span data-stu-id="75db6-118">Sustained throughput</span></span> | <span data-ttu-id="75db6-119">Frequenza di invio sostenuta</span><span class="sxs-lookup"><span data-stu-id="75db6-119">Sustained send rate</span></span> |
| --- | --- | --- |
| <span data-ttu-id="75db6-120">S1</span><span class="sxs-lookup"><span data-stu-id="75db6-120">S1</span></span> |<span data-ttu-id="75db6-121">Backup too1111 KB al minuto per unità</span><span class="sxs-lookup"><span data-stu-id="75db6-121">Up too1111 KB/minute per unit</span></span><br/><span data-ttu-id="75db6-122">(1,5 GB al giorno per unità)</span><span class="sxs-lookup"><span data-stu-id="75db6-122">(1.5 GB/day/unit)</span></span> |<span data-ttu-id="75db6-123">Una media di 278 messaggi al minuto per unità</span><span class="sxs-lookup"><span data-stu-id="75db6-123">Average of 278 messages/minute per unit</span></span><br/><span data-ttu-id="75db6-124">(400.000 messaggi al giorno per unità)</span><span class="sxs-lookup"><span data-stu-id="75db6-124">(400,000 messages/day per unit)</span></span> |
| <span data-ttu-id="75db6-125">S2</span><span class="sxs-lookup"><span data-stu-id="75db6-125">S2</span></span> |<span data-ttu-id="75db6-126">Backup too16 MB al minuto per unità</span><span class="sxs-lookup"><span data-stu-id="75db6-126">Up too16 MB/minute per unit</span></span><br/><span data-ttu-id="75db6-127">(22,8 GB al giorno per unità)</span><span class="sxs-lookup"><span data-stu-id="75db6-127">(22.8 GB/day/unit)</span></span> |<span data-ttu-id="75db6-128">Una media di 4.167 messaggi al minuto per unità</span><span class="sxs-lookup"><span data-stu-id="75db6-128">Average of 4,167 messages/minute per unit</span></span><br/><span data-ttu-id="75db6-129">(6 milioni di messaggi al giorno per unità)</span><span class="sxs-lookup"><span data-stu-id="75db6-129">(6 million messages/day per unit)</span></span> |
| <span data-ttu-id="75db6-130">S3</span><span class="sxs-lookup"><span data-stu-id="75db6-130">S3</span></span> |<span data-ttu-id="75db6-131">Backup too814 MB al minuto per unità</span><span class="sxs-lookup"><span data-stu-id="75db6-131">Up too814 MB/minute per unit</span></span><br/><span data-ttu-id="75db6-132">(1144,4 GB al giorno per unità)</span><span class="sxs-lookup"><span data-stu-id="75db6-132">(1144.4 GB/day/unit)</span></span> |<span data-ttu-id="75db6-133">Una media di 208,333 messaggi al minuto per unità</span><span class="sxs-lookup"><span data-stu-id="75db6-133">Average of 208,333 messages/minute per unit</span></span><br/><span data-ttu-id="75db6-134">(300 milioni di messaggi al giorno per unità)</span><span class="sxs-lookup"><span data-stu-id="75db6-134">(300 million messages/day per unit)</span></span> |

## <a name="identity-registry-operation-throughput"></a><span data-ttu-id="75db6-135">Velocità effettiva delle operazioni del registro delle identità</span><span class="sxs-lookup"><span data-stu-id="75db6-135">Identity registry operation throughput</span></span>
<span data-ttu-id="75db6-136">Le operazioni del Registro di sistema di identità IoT Hub non dovrebbero toobe operazioni di runtime, come se fossero principalmente provisioning toodevice correlati.</span><span class="sxs-lookup"><span data-stu-id="75db6-136">IoT Hub identity registry operations are not supposed toobe run-time operations, as they are mostly related toodevice provisioning.</span></span>

<span data-ttu-id="75db6-137">Per i dati specifici sulle prestazioni in modalità burst, vedere le [quote e limitazioni dell'hub IoT][IoT Hub quotas and throttles].</span><span class="sxs-lookup"><span data-stu-id="75db6-137">For specific burst performance numbers, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles].</span></span>

## <a name="sharding"></a><span data-ttu-id="75db6-138">Partizionamento orizzontale</span><span class="sxs-lookup"><span data-stu-id="75db6-138">Sharding</span></span>
<span data-ttu-id="75db6-139">Mentre un singolo hub IoT adattabile toomillions dei dispositivi, in alcuni casi la soluzione richiede caratteristiche di prestazioni specifiche che non può garantire un singolo hub IoT.</span><span class="sxs-lookup"><span data-stu-id="75db6-139">While a single IoT hub can scale toomillions of devices, sometimes your solution requires specific performance characteristics that a single IoT hub cannot guarantee.</span></span> <span data-ttu-id="75db6-140">In tal caso, è consigliabile partizionare i dispositivi in più hub IoT.</span><span class="sxs-lookup"><span data-stu-id="75db6-140">In that case, it is recommended that you partition your devices into multiple IoT hubs.</span></span> <span data-ttu-id="75db6-141">Hub IoT più uniformare i picchi di traffico e ottenere throughput necessario hello o tassi di operazione sono necessari.</span><span class="sxs-lookup"><span data-stu-id="75db6-141">Multiple IoT hubs smooth traffic bursts and obtain hello required throughput or operation rates that are required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="75db6-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="75db6-142">Next steps</span></span>
<span data-ttu-id="75db6-143">toofurther esplorare le funzionalità di hello di IoT Hub, vedere:</span><span class="sxs-lookup"><span data-stu-id="75db6-143">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="75db6-144">[Guida per gli sviluppatori dell'hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="75db6-144">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="75db6-145">[Simulazione di un dispositivo con Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="75db6-145">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[IoT Hub quotas and throttles]: iot-hub-devguide-quotas-throttling.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
