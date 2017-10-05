---
title: Connettere un dispositivo Raspberry Pi ad Azure IoT Suite | Microsoft Docs
description: "Le esercitazioni che usano Node.js o C consentono di imparare a usare lo Starter Kit di Microsoft Azure IoT per Raspberry Pi 3 e la soluzione di monitoraggio remoto IoT Suite. È possibile scegliere un'esercitazione che simula i dati di telemetria, che usa sensori reali o che consente di eseguire aggiornamenti del firmware remoto."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: eaa6a21a08bd9068b5335a8167f54c2aa387e0e5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-microsoft-azure-iot-raspberry-pi-3-starter-kit-to-the-remote-monitoring-solution"></a><span data-ttu-id="7fd76-104">Connettere lo Starter Kit di Microsoft Azure IoT per Raspberry Pi 3 alla soluzione di monitoraggio remoto</span><span class="sxs-lookup"><span data-stu-id="7fd76-104">Connect your Microsoft Azure IoT Raspberry Pi 3 Starter Kit to the remote monitoring solution</span></span>

<span data-ttu-id="7fd76-105">Le esercitazioni di questa sezione consentono di imparare a connettere un dispositivo Raspberry Pi 3 alla soluzione di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="7fd76-105">The tutorials in this section help you learn how to connect a Raspberry Pi 3 device to the remote monitoring solution.</span></span> <span data-ttu-id="7fd76-106">Scegliere l'esercitazione appropriata al linguaggio di programmazione preferito e se si dispone o meno di hardware del sensore disponibile da usare con Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="7fd76-106">Choose the tutorial appropriate to your preferred programming language and the whether you have the sensor hardware available to use with your Raspberry Pi.</span></span>

## <a name="the-tutorials"></a><span data-ttu-id="7fd76-107">Esercitazioni</span><span class="sxs-lookup"><span data-stu-id="7fd76-107">The tutorials</span></span>

| <span data-ttu-id="7fd76-108">Esercitazione</span><span class="sxs-lookup"><span data-stu-id="7fd76-108">Tutorial</span></span> | <span data-ttu-id="7fd76-109">Note</span><span class="sxs-lookup"><span data-stu-id="7fd76-109">Notes</span></span> | <span data-ttu-id="7fd76-110">Lingue</span><span class="sxs-lookup"><span data-stu-id="7fd76-110">Languages</span></span> |
| -------- | ----- | --------- |
| <span data-ttu-id="7fd76-111">Telemetria simulata (Base)</span><span class="sxs-lookup"><span data-stu-id="7fd76-111">Simulated telemetry (Basic)</span></span>| <span data-ttu-id="7fd76-112">Consente di simulare i dati del sensore.</span><span class="sxs-lookup"><span data-stu-id="7fd76-112">Simulates sensor data.</span></span> <span data-ttu-id="7fd76-113">Usa un computer autonomo Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="7fd76-113">Uses a standalone Raspberry Pi.</span></span> | <span data-ttu-id="7fd76-114">[C][lnk-c-simulator], [Node.js][lnk-node-simulator]</span><span class="sxs-lookup"><span data-stu-id="7fd76-114">[C][lnk-c-simulator], [Node.js][lnk-node-simulator]</span></span> |
| <span data-ttu-id="7fd76-115">Sensore reale (Intermedio)</span><span class="sxs-lookup"><span data-stu-id="7fd76-115">Real sensor (Intermediate)</span></span> | <span data-ttu-id="7fd76-116">Usa i dati di un sensore BME280 connesso a Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="7fd76-116">Uses data from a BME280 sensor connected to your Raspberry Pi.</span></span> | <span data-ttu-id="7fd76-117">[C][lnk-c-basic], [Node.js][lnk-node-basic]</span><span class="sxs-lookup"><span data-stu-id="7fd76-117">[C][lnk-c-basic], [Node.js][lnk-node-basic]</span></span> |
| <span data-ttu-id="7fd76-118">Implementazione dell'aggiornamento del firmware (Avanzato)</span><span class="sxs-lookup"><span data-stu-id="7fd76-118">Implement firmware update (Advanced)</span></span>| <span data-ttu-id="7fd76-119">Usa i dati di un sensore BME280 connesso a Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="7fd76-119">Uses data from a BME280 sensor connected to your Raspberry Pi.</span></span> <span data-ttu-id="7fd76-120">Consente di eseguire aggiornamenti del firmware remoto su Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="7fd76-120">Enables remote firmware updates on your Raspberry Pi.</span></span> | <span data-ttu-id="7fd76-121">[C][lnk-c-advanced], [Node.js][lnk-node-advanced]</span><span class="sxs-lookup"><span data-stu-id="7fd76-121">[C][lnk-c-advanced], [Node.js][lnk-node-advanced]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7fd76-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7fd76-122">Next steps</span></span>

<span data-ttu-id="7fd76-123">Visitare il [Centro per sviluppatori Azure IoT](https://azure.microsoft.com/develop/iot/) per altri esempi e documentazione su Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="7fd76-123">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[lnk-node-simulator]: iot-suite-raspberry-pi-kit-node-get-started-simulator.md
[lnk-node-basic]: iot-suite-raspberry-pi-kit-node-get-started-basic.md
[lnk-node-advanced]: iot-suite-raspberry-pi-kit-node-get-started-advanced.md
[lnk-c-simulator]: iot-suite-raspberry-pi-kit-c-get-started-simulator.md
[lnk-c-basic]: iot-suite-raspberry-pi-kit-c-get-started-basic.md
[lnk-c-advanced]: iot-suite-raspberry-pi-kit-c-get-started-advanced.md