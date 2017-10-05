---
title: Introduzione alla connessione di dispositivi simulati all'hub IoT di Azure | Microsoft Docs
description: "Informazioni su come creare dispositivi IoT simulati e connetterli all'hub IoT di Azure. I dispositivi possono inviare dati di telemetria all'hub IoT e l'hub IoT può monitorare e gestire i dispositivi."
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
ms.openlocfilehash: 436b3057509a831837159e814490959a2d7455a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-hub-get-started-with-simulated-devices-tutorials"></a><span data-ttu-id="7984f-105">Hub IoT di Azure - Esercitazioni introduttive per i dispositivi simulati</span><span class="sxs-lookup"><span data-stu-id="7984f-105">Azure IoT Hub get started with simulated devices tutorials</span></span>

<span data-ttu-id="7984f-106">Queste esercitazioni presentano l'hub IoT Azure e gli SDK per dispositivi.</span><span class="sxs-lookup"><span data-stu-id="7984f-106">These tutorials introduce you to Azure IoT Hub and the device SDKs.</span></span> <span data-ttu-id="7984f-107">Le esercitazioni concernono scenari IoT comuni per illustrare le funzionalità dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="7984f-107">The tutorials cover common IoT scenarios to demonstrate the capabilities of IoT Hub.</span></span> <span data-ttu-id="7984f-108">Le esercitazioni spiegano anche come combinare l'hub IoT con altri servizi di Azure e strumenti per creare soluzioni IoT più potenti.</span><span class="sxs-lookup"><span data-stu-id="7984f-108">The tutorials also illustrate how to combine IoT Hub with other Azure services and tools to build more powerful IoT solutions.</span></span> <span data-ttu-id="7984f-109">Le esercitazioni elencate nella tabella seguente illustrano come creare dispositivi IoT simulati.</span><span class="sxs-lookup"><span data-stu-id="7984f-109">The tutorials listed in the following table show you how to create simulated IoT devices.</span></span>

| <span data-ttu-id="7984f-110">Linguaggio di programmazione</span><span class="sxs-lookup"><span data-stu-id="7984f-110">Programming language</span></span> |
|----------------------|
| <span data-ttu-id="7984f-111">[.NET][Sim_NET]</span><span class="sxs-lookup"><span data-stu-id="7984f-111">[.NET][Sim_NET]</span></span>      |
| <span data-ttu-id="7984f-112">[Java][Sim_Jav]</span><span class="sxs-lookup"><span data-stu-id="7984f-112">[Java][Sim_Jav]</span></span>      |
| <span data-ttu-id="7984f-113">[Node.js][Sim_Nd]</span><span class="sxs-lookup"><span data-stu-id="7984f-113">[Node.js][Sim_Nd]</span></span>    |
| <span data-ttu-id="7984f-114">[Python][Sim_Pyth]</span><span class="sxs-lookup"><span data-stu-id="7984f-114">[Python][Sim_Pyth]</span></span>   |

<span data-ttu-id="7984f-115">È anche possibile usare un gateway IoT Edge per consentire ai dispositivi simulati di connettersi all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="7984f-115">In addition, you can use an IoT Edge gateway to enable simulated devices to connect to your IoT hub.</span></span>

| <span data-ttu-id="7984f-116">Linguaggio di programmazione</span><span class="sxs-lookup"><span data-stu-id="7984f-116">Programming language</span></span> | <span data-ttu-id="7984f-117">Piattaforma</span><span class="sxs-lookup"><span data-stu-id="7984f-117">Platform</span></span>           |
|----------------------|------------------- |
| <span data-ttu-id="7984f-118">C</span><span class="sxs-lookup"><span data-stu-id="7984f-118">C</span></span>                    | <span data-ttu-id="7984f-119">[Linux][Sim_Lnx]</span><span class="sxs-lookup"><span data-stu-id="7984f-119">[Linux][Sim_Lnx]</span></span>   |
| <span data-ttu-id="7984f-120">C</span><span class="sxs-lookup"><span data-stu-id="7984f-120">C</span></span>                    | <span data-ttu-id="7984f-121">[Windows][Sim_Win]</span><span class="sxs-lookup"><span data-stu-id="7984f-121">[Windows][Sim_Win]</span></span> |

[!INCLUDE [iot-hub-get-started-extended](../../includes/iot-hub-get-started-extended.md)]

[Sim_NET]: iot-hub-csharp-csharp-getstarted.md
[Sim_Jav]: iot-hub-java-java-getstarted.md
[Sim_Nd]: iot-hub-node-node-getstarted.md
[Sim_Pyth]: iot-hub-python-getstarted.md
[Sim_Lnx]: iot-hub-linux-iot-edge-get-started.md
[Sim_Win]: iot-hub-windows-iot-edge-get-started.md
