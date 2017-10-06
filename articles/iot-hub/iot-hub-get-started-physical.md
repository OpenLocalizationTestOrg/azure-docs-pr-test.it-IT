---
title: Introduzione alla connessione dispositivi fisici tooAzure IoT Hub | Documenti Microsoft
description: "Informazioni su come tooconnect fisico dispositivi e le lavagne tooAzure IoT Hub. I dispositivi è possono inviare dati di telemetria tooIoT Hub e IoT Hub è possibile monitorare e gestire i dispositivi."
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
ms.date: 08/22/2017
ms.author: dobett
ms.openlocfilehash: 47ce289c438b2f495d499d724c38ddc4b3307425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-get-started-with-physical-devices-tutorials"></a><span data-ttu-id="beb1a-105">Hub IoT di Azure - Esercitazioni introduttive per i dispositivi fisici</span><span class="sxs-lookup"><span data-stu-id="beb1a-105">Azure IoT Hub get started with physical devices tutorials</span></span>

<span data-ttu-id="beb1a-106">Queste esercitazioni vengono fornite informazioni si tooAzure IoT Hub e il dispositivo di hello SDK.</span><span class="sxs-lookup"><span data-stu-id="beb1a-106">These tutorials introduce you tooAzure IoT Hub and hello device SDKs.</span></span> <span data-ttu-id="beb1a-107">esercitazioni di Hello riguardano IoT scenari toodemonstrate hello funzionalità comuni dell'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="beb1a-107">hello tutorials cover common IoT scenarios toodemonstrate hello capabilities of IoT Hub.</span></span> <span data-ttu-id="beb1a-108">Hello esercitazioni viene inoltre illustrano come toocombine IoT Hub con altri Azure dei servizi e toobuild degli strumenti più potenti soluzioni IoT.</span><span class="sxs-lookup"><span data-stu-id="beb1a-108">hello tutorials also illustrate how toocombine IoT Hub with other Azure services and tools toobuild more powerful IoT solutions.</span></span> <span data-ttu-id="beb1a-109">Hello esercitazioni elencate in hello seguenti tabella mostrano è come dispositivi IoT fisici toocreate.</span><span class="sxs-lookup"><span data-stu-id="beb1a-109">hello tutorials listed in hello following table show you how toocreate physical IoT devices.</span></span>

| <span data-ttu-id="beb1a-110">Dispositivo IoT</span><span class="sxs-lookup"><span data-stu-id="beb1a-110">IoT device</span></span>                       | <span data-ttu-id="beb1a-111">Linguaggio di programmazione</span><span class="sxs-lookup"><span data-stu-id="beb1a-111">Programming language</span></span> |
|---------------------------------|----------------------|
| <span data-ttu-id="beb1a-112">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="beb1a-112">Raspberry Pi</span></span>                    | <span data-ttu-id="beb1a-113">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span><span class="sxs-lookup"><span data-stu-id="beb1a-113">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span></span>  |
| <span data-ttu-id="beb1a-114">DevKit di IoT</span><span class="sxs-lookup"><span data-stu-id="beb1a-114">IoT DevKit</span></span>                      | <span data-ttu-id="beb1a-115">[Arduino in VSCode][DevKit]</span><span class="sxs-lookup"><span data-stu-id="beb1a-115">[Arduino in VSCode][DevKit]</span></span>     |
| <span data-ttu-id="beb1a-116">Intel Edison</span><span class="sxs-lookup"><span data-stu-id="beb1a-116">Intel Edison</span></span>                    | <span data-ttu-id="beb1a-117">[Node.js][Ed_Nd], [C][Ed_C]</span><span class="sxs-lookup"><span data-stu-id="beb1a-117">[Node.js][Ed_Nd], [C][Ed_C]</span></span>           |
| <span data-ttu-id="beb1a-118">Adafruit Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="beb1a-118">Adafruit Feather HUZZAH ESP8266</span></span> | <span data-ttu-id="beb1a-119">[Arduino][Hu_Ard]</span><span class="sxs-lookup"><span data-stu-id="beb1a-119">[Arduino][Hu_Ard]</span></span>              |
| <span data-ttu-id="beb1a-120">Sparkfun ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="beb1a-120">Sparkfun ESP8266 Thing Dev</span></span>      | <span data-ttu-id="beb1a-121">[Arduino][Th_Ard]</span><span class="sxs-lookup"><span data-stu-id="beb1a-121">[Arduino][Th_Ard]</span></span>              |
| <span data-ttu-id="beb1a-122">Adafruit Feather M0</span><span class="sxs-lookup"><span data-stu-id="beb1a-122">Adafruit Feather M0</span></span>             | <span data-ttu-id="beb1a-123">[Arduino][M0_Ard]</span><span class="sxs-lookup"><span data-stu-id="beb1a-123">[Arduino][M0_Ard]</span></span>              |

<span data-ttu-id="beb1a-124">Inoltre, è possibile utilizzare un bordo IoT gateway tooenable dispositivi tooconnect tooyour l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="beb1a-124">In addition, you can use an IoT Edge gateway tooenable devices tooconnect tooyour IoT hub.</span></span>

| <span data-ttu-id="beb1a-125">Dispositivo gateway</span><span class="sxs-lookup"><span data-stu-id="beb1a-125">Gateway device</span></span>               | <span data-ttu-id="beb1a-126">Linguaggio di programmazione</span><span class="sxs-lookup"><span data-stu-id="beb1a-126">Programming language</span></span> | <span data-ttu-id="beb1a-127">Piattaforma</span><span class="sxs-lookup"><span data-stu-id="beb1a-127">Platform</span></span>         |
|------------------------------|----------------------|------------------|
| <span data-ttu-id="beb1a-128">Intel NUC (modello DE3815TYKE)</span><span class="sxs-lookup"><span data-stu-id="beb1a-128">Intel NUC (model DE3815TYKE)</span></span> | <span data-ttu-id="beb1a-129">C</span><span class="sxs-lookup"><span data-stu-id="beb1a-129">C</span></span>                    | <span data-ttu-id="beb1a-130">[Wind River Linux][NUC_Lnx]</span><span class="sxs-lookup"><span data-stu-id="beb1a-130">[Wind River Linux][NUC_Lnx]</span></span> |

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
[NUC_Lnx]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
