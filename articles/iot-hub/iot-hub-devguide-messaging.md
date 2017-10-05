---
title: Informazioni sulla messaggistica hub IoT di Azure | Microsoft Docs
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
ms.openlocfilehash: f54398d7ac46bf178d2bb603669b399d25370736
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="device-to-cloud-and-cloud-to-device-messaging-with-iot-hub"></a><span data-ttu-id="bb7b0-104">Messaggistica da dispositivo a cloud e da cloud a dispositivo con l'hub IoT</span><span class="sxs-lookup"><span data-stu-id="bb7b0-104">Device-to-cloud and cloud-to-device messaging with IoT Hub</span></span>

<span data-ttu-id="bb7b0-105">Usare la messaggistica dell'hub IoT per comunicare con i dispositivi:</span><span class="sxs-lookup"><span data-stu-id="bb7b0-105">Use IoT Hub messaging to communicate with your devices by:</span></span>

* <span data-ttu-id="bb7b0-106">inviando messaggi [da dispositivo a cloud][lnk-d2c] dai dispositivi per il back-end della soluzione;</span><span class="sxs-lookup"><span data-stu-id="bb7b0-106">Sending [device-to-cloud][lnk-d2c] messages from your devices to your solution back end.</span></span>
* <span data-ttu-id="bb7b0-107">inviando messaggi [da cloud a dispositivo][lnk-c2d] dal back-end della soluzione ai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="bb7b0-107">Sending [cloud-to-device][lnk-c2d] messages from the solution back end to your devices.</span></span>

<span data-ttu-id="bb7b0-108">Le proprietà di base della funzionalità di messaggistica dell'hub IoT sono l'affidabilità e la durabilità dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="bb7b0-108">Core properties of IoT Hub messaging functionality are the reliability and durability of messages.</span></span> <span data-ttu-id="bb7b0-109">Queste proprietà consentono la resilienza in caso di connettività intermittente sul lato dispositivo e picchi di carico durante l'elaborazione degli eventi sul lato cloud.</span><span class="sxs-lookup"><span data-stu-id="bb7b0-109">These properties enable resilience to intermittent connectivity on the device side, and to load spikes in event processing on the cloud side.</span></span> <span data-ttu-id="bb7b0-110">L'hub IoT implementa *almeno una volta* le garanzie di recapito per la messaggistica da dispositivo a cloud e da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bb7b0-110">IoT Hub implements *at least once* delivery guarantees for both device-to-cloud and cloud-to-device messaging.</span></span>

<span data-ttu-id="bb7b0-111">Per un'introduzione alle funzionalità dell'hub IoT, vedere gli articoli [Azure e Internet delle cose][lnk-azure-iot] e [Panoramica del servizio hub IoT di Azure][lnk-iot-hub-overview].</span><span class="sxs-lookup"><span data-stu-id="bb7b0-111">For an introduction to the capabilities of IoT Hub, see the articles [Azure and Internet of Things][lnk-azure-iot] and [Overview of the Azure IoT Hub service][lnk-iot-hub-overview].</span></span>

## <a name="when-to-use-iot-hub-messaging"></a><span data-ttu-id="bb7b0-112">Quando usare la messaggistica dell'hub IoT</span><span class="sxs-lookup"><span data-stu-id="bb7b0-112">When to use IoT Hub messaging</span></span>

<span data-ttu-id="bb7b0-113">Usare i messaggi da dispositivo a cloud per inviare la telemetria relativa alle serie temporali e gli avvisi dall'app del dispositivo e i messaggi da cloud a dispositivo per notifiche unidirezionali all'app del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bb7b0-113">Use device-to-cloud messages for sending time series telemetry and alerts from your device app, and cloud-to-device messages for one-way notifications to your device app.</span></span>

* <span data-ttu-id="bb7b0-114">Vedere [Indicazioni sulle comunicazioni da dispositivo a cloud][lnk-d2c-guidance] in caso di dubbi tra l'uso delle proprietà segnalate, dei messaggi da dispositivo a cloud o del caricamento di file.</span><span class="sxs-lookup"><span data-stu-id="bb7b0-114">Refer to [Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using device-to-cloud messages, reported properties, or file upload.</span></span>
* <span data-ttu-id="bb7b0-115">Vedere [Indicazioni sulle comunicazioni da cloud a dispositivo][lnk-c2d-guidance] in caso di dubbi tra l'uso delle proprietà desiderate, dei metodi diretti o dei messaggi da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bb7b0-115">Refer to [Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using cloud-to-device messages, desired properties, or direct methods.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb7b0-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bb7b0-116">Next steps</span></span>

* <span data-ttu-id="bb7b0-117">Informazioni sulla [messaggistica da dispositivo a cloud][lnk-d2c] dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="bb7b0-117">Learn about IoT Hub [device-to-cloud messaging][lnk-d2c].</span></span>
* <span data-ttu-id="bb7b0-118">Informazioni sulla [messaggistica da cloud a dispositivo][lnk-c2d] dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="bb7b0-118">Learn about IoT Hub [cloud-to-device messaging][lnk-c2d].</span></span>

[lnk-azure-iot]: iot-hub-what-is-azure-iot.md
[lnk-iot-hub-overview]: iot-hub-what-is-iot-hub.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md