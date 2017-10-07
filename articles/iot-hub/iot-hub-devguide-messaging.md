---
title: messaggistica di Azure IoT Hub aaaUnderstand | Documenti Microsoft
description: Guida per gli sviluppatori - Messaggistica da dispositivo a cloud e da cloud a dispositivo con l'hub IoT. Include informazioni sui formati dei messaggi e sui protocolli di comunicazione supportati.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3fc5f1a3-3711-4611-9897-d4db079b4250
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: a610741e23e243f392f1c042f9ab4a00d42f734f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="device-to-cloud-and-cloud-to-device-messaging-with-iot-hub"></a><span data-ttu-id="38aae-104">Messaggistica da dispositivo a cloud e da cloud a dispositivo con l'hub IoT</span><span class="sxs-lookup"><span data-stu-id="38aae-104">Device-to-cloud and cloud-to-device messaging with IoT Hub</span></span>

<span data-ttu-id="38aae-105">Usare l'IoT Hub messaggistica toocommunicate con i dispositivi da:</span><span class="sxs-lookup"><span data-stu-id="38aae-105">Use IoT Hub messaging toocommunicate with your devices by:</span></span>

* <span data-ttu-id="38aae-106">L'invio di [da dispositivo a cloud] [ lnk-d2c] messaggi dalla soluzione tooyour dispositivi back-end.</span><span class="sxs-lookup"><span data-stu-id="38aae-106">Sending [device-to-cloud][lnk-d2c] messages from your devices tooyour solution back end.</span></span>
* <span data-ttu-id="38aae-107">L'invio di [cloud a dispositivo] [ lnk-c2d] i messaggi dalla soluzione hello nuovamente terminare tooyour dispositivi.</span><span class="sxs-lookup"><span data-stu-id="38aae-107">Sending [cloud-to-device][lnk-c2d] messages from hello solution back end tooyour devices.</span></span>

<span data-ttu-id="38aae-108">Proprietà principali di funzionalità di messaggistica IoT Hub sono hello e affidabilità dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="38aae-108">Core properties of IoT Hub messaging functionality are hello reliability and durability of messages.</span></span> <span data-ttu-id="38aae-109">Queste proprietà consentono la connettività di resilienza toointermittent sul lato dispositivo hello e tooload picchi in elaborazione sul lato cloud hello di eventi.</span><span class="sxs-lookup"><span data-stu-id="38aae-109">These properties enable resilience toointermittent connectivity on hello device side, and tooload spikes in event processing on hello cloud side.</span></span> <span data-ttu-id="38aae-110">L'hub IoT implementa *almeno una volta* le garanzie di recapito per la messaggistica da dispositivo a cloud e da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="38aae-110">IoT Hub implements *at least once* delivery guarantees for both device-to-cloud and cloud-to-device messaging.</span></span>

<span data-ttu-id="38aae-111">Per le funzionalità di toohello un'introduzione di IoT Hub, vedere gli articoli di hello [Azure e Internet of Things] [ lnk-azure-iot] e [Panoramica del servizio dell'IoT Hub Azure hello] [lnk-iot-hub-overview].</span><span class="sxs-lookup"><span data-stu-id="38aae-111">For an introduction toohello capabilities of IoT Hub, see hello articles [Azure and Internet of Things][lnk-azure-iot] and [Overview of hello Azure IoT Hub service][lnk-iot-hub-overview].</span></span>

## <a name="when-toouse-iot-hub-messaging"></a><span data-ttu-id="38aae-112">Quando toouse Hub IoT messaggistica</span><span class="sxs-lookup"><span data-stu-id="38aae-112">When toouse IoT Hub messaging</span></span>

<span data-ttu-id="38aae-113">Utilizzare i messaggi da dispositivo a cloud per l'invio di avvisi e i dati di telemetria serie ora dall'app del dispositivo e cloud a dispositivo per app per dispositivi tooyour notifiche unidirezionale.</span><span class="sxs-lookup"><span data-stu-id="38aae-113">Use device-to-cloud messages for sending time series telemetry and alerts from your device app, and cloud-to-device messages for one-way notifications tooyour device app.</span></span>

* <span data-ttu-id="38aae-114">Fare riferimento troppo[materiale sussidiario per la comunicazione da dispositivo a cloud] [ lnk-d2c-guidance] se in dubbio tra l'utilizzo di messaggi da dispositivo a cloud, proprietà segnalata o caricamento del file.</span><span class="sxs-lookup"><span data-stu-id="38aae-114">Refer too[Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using device-to-cloud messages, reported properties, or file upload.</span></span>
* <span data-ttu-id="38aae-115">Fare riferimento troppo[indicazioni di comunicazione Cloud a dispositivo] [ lnk-c2d-guidance] se in dubbio tra l'utilizzo di messaggi da cloud a dispositivo, le proprietà desiderate o metodi diretti.</span><span class="sxs-lookup"><span data-stu-id="38aae-115">Refer too[Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using cloud-to-device messages, desired properties, or direct methods.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38aae-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="38aae-116">Next steps</span></span>

* <span data-ttu-id="38aae-117">Informazioni sulla [messaggistica da dispositivo a cloud][lnk-d2c] dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="38aae-117">Learn about IoT Hub [device-to-cloud messaging][lnk-d2c].</span></span>
* <span data-ttu-id="38aae-118">Informazioni sulla [messaggistica da cloud a dispositivo][lnk-c2d] dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="38aae-118">Learn about IoT Hub [cloud-to-device messaging][lnk-c2d].</span></span>

[lnk-azure-iot]: iot-hub-what-is-azure-iot.md
[lnk-iot-hub-overview]: iot-hub-what-is-iot-hub.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md