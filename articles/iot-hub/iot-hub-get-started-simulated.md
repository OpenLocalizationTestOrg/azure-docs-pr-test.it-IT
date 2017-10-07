---
title: Introduzione alla connessione dispositivi simulati tooAzure IoT Hub | Documenti Microsoft
description: "Informazioni su come toocreate simulati i dispositivi IoT e connetterli tooAzure IoT Hub. I dispositivi è possono inviare dati di telemetria tooIoT Hub e Iot Hub è possibile monitorare e gestire i dispositivi."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
keywords: esercitazione sull'hub iot azure
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dobett
ms.openlocfilehash: 2c9b76477d12c853abd93aa96043417a013daaef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-get-started-with-simulated-devices-tutorials"></a><span data-ttu-id="a0029-105">Hub IoT di Azure - Esercitazioni introduttive per i dispositivi simulati</span><span class="sxs-lookup"><span data-stu-id="a0029-105">Azure IoT Hub get started with simulated devices tutorials</span></span>

<span data-ttu-id="a0029-106">Queste esercitazioni vengono fornite informazioni si tooAzure IoT Hub e il dispositivo di hello SDK.</span><span class="sxs-lookup"><span data-stu-id="a0029-106">These tutorials introduce you tooAzure IoT Hub and hello device SDKs.</span></span> <span data-ttu-id="a0029-107">esercitazioni di Hello riguardano IoT scenari toodemonstrate hello funzionalità comuni dell'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a0029-107">hello tutorials cover common IoT scenarios toodemonstrate hello capabilities of IoT Hub.</span></span> <span data-ttu-id="a0029-108">Hello esercitazioni viene inoltre illustrano come toocombine IoT Hub con altri Azure dei servizi e toobuild degli strumenti più potenti soluzioni IoT.</span><span class="sxs-lookup"><span data-stu-id="a0029-108">hello tutorials also illustrate how toocombine IoT Hub with other Azure services and tools toobuild more powerful IoT solutions.</span></span> <span data-ttu-id="a0029-109">le esercitazioni Hello elencate nella tabella seguente hello illustrano come toocreate simulati i dispositivi IoT.</span><span class="sxs-lookup"><span data-stu-id="a0029-109">hello tutorials listed in hello following table show you how toocreate simulated IoT devices.</span></span>

| <span data-ttu-id="a0029-110">Linguaggio di programmazione</span><span class="sxs-lookup"><span data-stu-id="a0029-110">Programming language</span></span> |
|----------------------|
| <span data-ttu-id="a0029-111">[.NET][Sim_NET]</span><span class="sxs-lookup"><span data-stu-id="a0029-111">[.NET][Sim_NET]</span></span>      |
| <span data-ttu-id="a0029-112">[Java][Sim_Jav]</span><span class="sxs-lookup"><span data-stu-id="a0029-112">[Java][Sim_Jav]</span></span>      |
| <span data-ttu-id="a0029-113">[Node.js][Sim_Nd]</span><span class="sxs-lookup"><span data-stu-id="a0029-113">[Node.js][Sim_Nd]</span></span>    |
| <span data-ttu-id="a0029-114">[Python][Sim_Pyth]</span><span class="sxs-lookup"><span data-stu-id="a0029-114">[Python][Sim_Pyth]</span></span>   |

<span data-ttu-id="a0029-115">Inoltre, è possibile utilizzare un bordo IoT gateway tooenable simulato dispositivi tooconnect tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a0029-115">In addition, you can use an IoT Edge gateway tooenable simulated devices tooconnect tooyour IoT hub.</span></span>

| <span data-ttu-id="a0029-116">Linguaggio di programmazione</span><span class="sxs-lookup"><span data-stu-id="a0029-116">Programming language</span></span> | <span data-ttu-id="a0029-117">Piattaforma</span><span class="sxs-lookup"><span data-stu-id="a0029-117">Platform</span></span>           |
|----------------------|------------------- |
| <span data-ttu-id="a0029-118">C</span><span class="sxs-lookup"><span data-stu-id="a0029-118">C</span></span>                    | <span data-ttu-id="a0029-119">[Linux][Sim_Lnx]</span><span class="sxs-lookup"><span data-stu-id="a0029-119">[Linux][Sim_Lnx]</span></span>   |
| <span data-ttu-id="a0029-120">C</span><span class="sxs-lookup"><span data-stu-id="a0029-120">C</span></span>                    | <span data-ttu-id="a0029-121">[Windows][Sim_Win]</span><span class="sxs-lookup"><span data-stu-id="a0029-121">[Windows][Sim_Win]</span></span> |

[!INCLUDE [iot-hub-get-started-extended](../../includes/iot-hub-get-started-extended.md)]

[Sim_NET]: iot-hub-csharp-csharp-getstarted.md
[Sim_Jav]: iot-hub-java-java-getstarted.md
[Sim_Nd]: iot-hub-node-node-getstarted.md
[Sim_Pyth]: iot-hub-python-getstarted.md
[Sim_Lnx]: iot-hub-linux-iot-edge-get-started.md
[Sim_Win]: iot-hub-windows-iot-edge-get-started.md
