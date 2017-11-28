---
title: IoT Hub Azure - introduzione connessione cloud toohello di dispositivi IoT | Documenti Microsoft
description: "Informazioni su come tooconnect le lavagne IoT e starter kit tooAzure IoT Hub. I dispositivi è possono inviare dati di telemetria tooIoT Hub e IoT Hub è possibile monitorare e gestire i dispositivi."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
keywords: esercitazione sull'hub iot azure
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: dobett
ms.openlocfilehash: 6dc956308009091532019ff84aec881f042f0104
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-get-started-tutorials"></a><span data-ttu-id="b9b35-105">Esercitazioni introduttive sull'Hub IoT Azure</span><span class="sxs-lookup"><span data-stu-id="b9b35-105">Azure IoT Hub get started tutorials</span></span>

<span data-ttu-id="b9b35-106">È possibile utilizzare Azure IoT Hub hello Azure IoT soluzioni dei dispositivi e gli SDK toobuild Internet delle cose (IoT):</span><span class="sxs-lookup"><span data-stu-id="b9b35-106">You can use Azure IoT Hub and hello Azure IoT device SDKs toobuild Internet of Things (IoT) solutions:</span></span>

* <span data-ttu-id="b9b35-107">IoT Hub Azure è un servizio completamente gestito nel cloud hello che si connette in modo sicuro, consente di monitorare e gestire i dispositivi IoT.</span><span class="sxs-lookup"><span data-stu-id="b9b35-107">Azure IoT Hub is a fully managed service in hello cloud that securely connects, monitors, and manages your IoT devices.</span></span> <span data-ttu-id="b9b35-108">Utilizzare hello dispositivo IoT di Azure SDK tooimplement i dispositivi IoT.</span><span class="sxs-lookup"><span data-stu-id="b9b35-108">Use hello Azure IoT Device SDKs tooimplement your IoT devices.</span></span>
* <span data-ttu-id="b9b35-109">Usare un gateway IoT in scenari IoT più complessi.</span><span class="sxs-lookup"><span data-stu-id="b9b35-109">Use an IoT gateway in more complex IoT scenarios.</span></span> <span data-ttu-id="b9b35-110">Ad esempio, in cui è necessario tooconsider fattori, ad esempio dispositivi legacy, i costi di larghezza di banda, i criteri di sicurezza e privacy o l'elaborazione dati di bordo.</span><span class="sxs-lookup"><span data-stu-id="b9b35-110">For example, where you need tooconsider factors such as legacy devices, bandwidth costs, security and privacy policies, or edge data processing.</span></span> <span data-ttu-id="b9b35-111">In questi scenari, si utilizza Azure IoT Edge tooimplement un gateway che si connette l'hub IoT tooyour dispositivi.</span><span class="sxs-lookup"><span data-stu-id="b9b35-111">In these scenarios, you use Azure IoT Edge tooimplement a gateway that connects devices tooyour IoT hub.</span></span>

## <a name="what-hello-tutorials-cover"></a><span data-ttu-id="b9b35-112">Le esercitazioni di hello riguardano</span><span class="sxs-lookup"><span data-stu-id="b9b35-112">What hello tutorials cover</span></span>

<span data-ttu-id="b9b35-113">Queste esercitazioni vengono fornite informazioni si tooAzure IoT Hub e il dispositivo di hello SDK.</span><span class="sxs-lookup"><span data-stu-id="b9b35-113">These tutorials introduce you tooAzure IoT Hub and hello device SDKs.</span></span> <span data-ttu-id="b9b35-114">esercitazioni di Hello riguardano IoT scenari toodemonstrate hello funzionalità comuni dell'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b9b35-114">hello tutorials cover common IoT scenarios toodemonstrate hello capabilities of IoT Hub.</span></span> <span data-ttu-id="b9b35-115">Hello esercitazioni viene inoltre illustrano come toocombine IoT Hub con altri Azure dei servizi e toobuild degli strumenti più potenti soluzioni IoT.</span><span class="sxs-lookup"><span data-stu-id="b9b35-115">hello tutorials also illustrate how toocombine IoT Hub with other Azure services and tools toobuild more powerful IoT solutions.</span></span> <span data-ttu-id="b9b35-116">Nelle esercitazioni di hello, è possibile scegliere i dispositivi IoT simulati o reali toouse.</span><span class="sxs-lookup"><span data-stu-id="b9b35-116">In hello tutorials, you can choose toouse either simulated or real IoT devices.</span></span> <span data-ttu-id="b9b35-117">Inoltre, sono disponibili come toouse un gateway tooenable dispositivi tooconnect tooyour l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b9b35-117">In addition, you can learn how toouse a gateway tooenable devices tooconnect tooyour IoT hub.</span></span>

## <a name="set-up-your-device"></a><span data-ttu-id="b9b35-118">Configurare il dispositivo</span><span class="sxs-lookup"><span data-stu-id="b9b35-118">Set up your device</span></span>

<span data-ttu-id="b9b35-119">Connettere un IoT dispositivo o il gateway tooAzure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b9b35-119">Connect an IoT device or gateway tooAzure IoT Hub.</span></span> <span data-ttu-id="b9b35-120">È possibile scegliere tooget un dispositivo fisico o simulato avviato:</span><span class="sxs-lookup"><span data-stu-id="b9b35-120">You can choose a physical or simulated device tooget started:</span></span>

| <span data-ttu-id="b9b35-121">Dispositivo IoT</span><span class="sxs-lookup"><span data-stu-id="b9b35-121">IoT device</span></span>                       | <span data-ttu-id="b9b35-122">Linguaggio di programmazione</span><span class="sxs-lookup"><span data-stu-id="b9b35-122">Programming language</span></span> |
|----------------------------------|----------------------|
| <span data-ttu-id="b9b35-123">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="b9b35-123">Raspberry Pi</span></span>                     | <span data-ttu-id="b9b35-124">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span><span class="sxs-lookup"><span data-stu-id="b9b35-124">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span></span>  |
| <span data-ttu-id="b9b35-125">DevKit di IoT</span><span class="sxs-lookup"><span data-stu-id="b9b35-125">IoT DevKit</span></span>                       | <span data-ttu-id="b9b35-126">[Arduino in VSCode][DevKit]</span><span class="sxs-lookup"><span data-stu-id="b9b35-126">[Arduino in VSCode][DevKit]</span></span>     |
| <span data-ttu-id="b9b35-127">Intel Edison</span><span class="sxs-lookup"><span data-stu-id="b9b35-127">Intel Edison</span></span>                     | <span data-ttu-id="b9b35-128">[Node.js][Ed_Nd], [C][Ed_C]</span><span class="sxs-lookup"><span data-stu-id="b9b35-128">[Node.js][Ed_Nd], [C][Ed_C]</span></span>    |
| <span data-ttu-id="b9b35-129">Adafruit Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="b9b35-129">Adafruit Feather HUZZAH ESP8266</span></span>  | <span data-ttu-id="b9b35-130">[Arduino][Hu_Ard]</span><span class="sxs-lookup"><span data-stu-id="b9b35-130">[Arduino][Hu_Ard]</span></span>              |
| <span data-ttu-id="b9b35-131">Sparkfun ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="b9b35-131">Sparkfun ESP8266 Thing Dev</span></span>       | <span data-ttu-id="b9b35-132">[Arduino][Th_Ard]</span><span class="sxs-lookup"><span data-stu-id="b9b35-132">[Arduino][Th_Ard]</span></span>              |
| <span data-ttu-id="b9b35-133">Adafruit Feather M0</span><span class="sxs-lookup"><span data-stu-id="b9b35-133">Adafruit Feather M0</span></span>              | <span data-ttu-id="b9b35-134">[Arduino][M0_Ard]</span><span class="sxs-lookup"><span data-stu-id="b9b35-134">[Arduino][M0_Ard]</span></span>              |
| <span data-ttu-id="b9b35-135">Dispositivo simulato nel PC</span><span class="sxs-lookup"><span data-stu-id="b9b35-135">Simulated device on PC</span></span>           | <span data-ttu-id="b9b35-136">[.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd], [Python][Sim_Pyth]</span><span class="sxs-lookup"><span data-stu-id="b9b35-136">[.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd], [Python][Sim_Pyth]</span></span> |
| <span data-ttu-id="b9b35-137">Simulatore di dispositivi online</span><span class="sxs-lookup"><span data-stu-id="b9b35-137">Online device simulator</span></span>         | <span data-ttu-id="b9b35-138">[Raspberry Pi (Node.js)][Ol_Sim]</span><span class="sxs-lookup"><span data-stu-id="b9b35-138">[Raspberry Pi (Node.js)][Ol_Sim]</span></span> |

<span data-ttu-id="b9b35-139">Inoltre, è possibile utilizzare un bordo IoT gateway tooenable dispositivi tooconnect tooyour l'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="b9b35-139">In addition, you can use an IoT Edge gateway tooenable devices tooconnect tooyour IoT hub:</span></span>

| <span data-ttu-id="b9b35-140">Dispositivo gateway</span><span class="sxs-lookup"><span data-stu-id="b9b35-140">Gateway device</span></span>               | <span data-ttu-id="b9b35-141">Linguaggio di programmazione</span><span class="sxs-lookup"><span data-stu-id="b9b35-141">Programming language</span></span> | <span data-ttu-id="b9b35-142">Piattaforma</span><span class="sxs-lookup"><span data-stu-id="b9b35-142">Platform</span></span>         |
|------------------------------|----------------------|------------------|
| <span data-ttu-id="b9b35-143">Intel NUC (modello DE3815TYKE)</span><span class="sxs-lookup"><span data-stu-id="b9b35-143">Intel NUC (model DE3815TYKE)</span></span> | <span data-ttu-id="b9b35-144">C</span><span class="sxs-lookup"><span data-stu-id="b9b35-144">C</span></span>                    | <span data-ttu-id="b9b35-145">[Wind River Linux][NUC_Lnx]</span><span class="sxs-lookup"><span data-stu-id="b9b35-145">[Wind River Linux][NUC_Lnx]</span></span> |
| <span data-ttu-id="b9b35-146">Gateway simulato</span><span class="sxs-lookup"><span data-stu-id="b9b35-146">Simulated gateway</span></span>            | <span data-ttu-id="b9b35-147">C</span><span class="sxs-lookup"><span data-stu-id="b9b35-147">C</span></span>                    | <span data-ttu-id="b9b35-148">[Linux][Sim_Lnx], [Windows][Sim_Win]</span><span class="sxs-lookup"><span data-stu-id="b9b35-148">[Linux][Sim_Lnx], [Windows][Sim_Win]</span></span> |

[!INCLUDE [iot-hub-get-started-extended](../../includes/iot-hub-get-started-extended.md)]

[Pi_Nd]: iot-hub-raspberry-pi-kit-node-get-started.md
[Pi_C]: iot-hub-raspberry-pi-kit-c-get-started.md
[Pi_Py]: iot-hub-raspberry-pi-kit-python-get-started.md
[DevKit]: iot-hub-arduino-iot-devkit-az3166-get-started.md
[Ed_Nd]: iot-hub-intel-edison-kit-node-get-started.md
[Ed_C]: iot-hub-intel-edison-kit-c-get-started.md
[Hu_Ard]: iot-hub-arduino-huzzah-esp8266-get-started.md
[Th_Ard]: iot-hub-sparkfun-esp8266-thing-dev-get-started.md
[M0_Ard]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started.md
[Sim_NET]: iot-hub-csharp-csharp-getstarted.md
[Sim_Jav]: iot-hub-java-java-getstarted.md
[Sim_Nd]: iot-hub-node-node-getstarted.md
[Sim_Pyth]: iot-hub-python-getstarted.md
[NUC_Lnx]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
[Sim_Lnx]: iot-hub-linux-iot-edge-get-started.md
[Sim_Win]: iot-hub-windows-iot-edge-get-started.md
[Ol_Sim]: iot-hub-raspberry-pi-web-simulator-get-started.md
