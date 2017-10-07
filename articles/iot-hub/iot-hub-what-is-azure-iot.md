---
title: soluzioni aaaAzure per Internet delle cose (IoT Suite) | Documenti Microsoft
description: Panoramica dell'architettura della soluzione IoT un campione e l'interrelazione toodevices, hello servizio IoT Hub di Azure, SDK dispositivo IoT di Azure, Azure IoT servizio SDK e altri servizi di Azure.
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a859e379-dca7-42fa-bdf6-1125c86ad140
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 2d934e3f988c530de6a242869c021712d2aa1576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
[!INCLUDE [iot-azure-and-iot](../../includes/iot-azure-and-iot.md)]

## <a name="next-steps"></a><span data-ttu-id="ee63e-103">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ee63e-103">Next steps</span></span>

<span data-ttu-id="ee63e-104">Hub IoT di Azure è un servizio che consente comunicazioni bidirezionali affidabili e sicure tra il back-end della soluzione e milioni di dispositivi.</span><span class="sxs-lookup"><span data-stu-id="ee63e-104">Azure IoT Hub is an Azure service that enables secure and reliable bi-directional communications between your solution back end and millions of devices.</span></span> <span data-ttu-id="ee63e-105">Consente di hello soluzione back-end:</span><span class="sxs-lookup"><span data-stu-id="ee63e-105">It enables hello solution back end to:</span></span>

* <span data-ttu-id="ee63e-106">Ricevere dati di telemetria su larga scala dai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="ee63e-106">Receive telemetry at scale from your devices.</span></span>
* <span data-ttu-id="ee63e-107">Dati della route dal processore di eventi flusso tooa dispositivi.</span><span class="sxs-lookup"><span data-stu-id="ee63e-107">Route data from your devices tooa stream event processor.</span></span>
* <span data-ttu-id="ee63e-108">Ricevere caricamenti di file dai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="ee63e-108">Receive file uploads from devices.</span></span>
* <span data-ttu-id="ee63e-109">Inviare messaggi da cloud a dispositivo toospecific dispositivi.</span><span class="sxs-lookup"><span data-stu-id="ee63e-109">Send cloud-to-device messages toospecific devices.</span></span>

<span data-ttu-id="ee63e-110">È possibile usare l'IoT Hub tooimplement terminare la propria soluzione nuovamente.</span><span class="sxs-lookup"><span data-stu-id="ee63e-110">You can use IoT Hub tooimplement your own solution back end.</span></span> <span data-ttu-id="ee63e-111">Inoltre, l'IoT Hub include dispositivi di tooprovision del Registro di sistema utilizzato di identità, le proprie credenziali di sicurezza e l'hub IoT toohello tooconnect i relativi diritti.</span><span class="sxs-lookup"><span data-stu-id="ee63e-111">In addition, IoT Hub includes an identity registry used tooprovision devices, their security credentials, and their rights tooconnect toohello IoT hub.</span></span> <span data-ttu-id="ee63e-112">toolearn ulteriori informazioni sull'IoT Hub, vedere [che cos'è l'IoT Hub?] [lnk-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="ee63e-112">toolearn more about IoT Hub, see [What is IoT Hub?][lnk-iot-hub].</span></span>

<span data-ttu-id="ee63e-113">toolearn come IoT Hub Azure consente di attivare la gestione dei dispositivi basata su standard per gestire, configurare e aggiornare i dispositivi, si tooremotely vedere [Panoramica di gestione dei dispositivi con l'IoT Hub][lnk-device-management].</span><span class="sxs-lookup"><span data-stu-id="ee63e-113">toolearn how Azure IoT Hub enables standards-based device management for you tooremotely manage, configure, and update your devices, see [Overview of device management with IoT Hub][lnk-device-management].</span></span>

<span data-ttu-id="ee63e-114">le applicazioni client tooimplement su una vasta gamma di piattaforme per dispositivi hardware e sistemi operativi, è possibile usare il dispositivo di Azure IoT hello SDK.</span><span class="sxs-lookup"><span data-stu-id="ee63e-114">tooimplement client applications on a wide variety of device hardware platforms and operating systems, you can use hello Azure IoT device SDKs.</span></span> <span data-ttu-id="ee63e-115">il dispositivo di Hello SDK include librerie che semplificano l'invio dati di telemetria tooan IoT hub e la ricezione cloud a dispositivo di messaggi.</span><span class="sxs-lookup"><span data-stu-id="ee63e-115">hello device SDKs include libraries that facilitate sending telemetry tooan IoT hub and receiving cloud-to-device messages.</span></span> <span data-ttu-id="ee63e-116">Quando si usa il dispositivo di hello SDK, è possibile scegliere tra diversi toocommunicate di protocolli di rete con l'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ee63e-116">When you use hello device SDKs, you can choose from several network protocols toocommunicate with IoT Hub.</span></span> <span data-ttu-id="ee63e-117">toolearn informazioni, vedere hello [informazioni sul dispositivo SDK][lnk-device-sdks].</span><span class="sxs-lookup"><span data-stu-id="ee63e-117">toolearn more, see hello [information about device SDKs][lnk-device-sdks].</span></span>

<span data-ttu-id="ee63e-118">tooget avviato scrivere del codice ed esecuzione di alcuni esempi, vedere hello [iniziare con l'IoT Hub] [ lnk-getstarted] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="ee63e-118">tooget started writing some code and running some samples, see hello [Get started with IoT Hub][lnk-getstarted] tutorial.</span></span>

<span data-ttu-id="ee63e-119">Si potrebbe anche essere interessati a [Azure IoT Suite][lnk-iot-suite], che è una raccolta di soluzioni preconfigurate.</span><span class="sxs-lookup"><span data-stu-id="ee63e-119">You may also be interested in [Azure IoT Suite][lnk-iot-suite], which is a collection of preconfigured solutions.</span></span> <span data-ttu-id="ee63e-120">IoT Suite consente tooget in tempi brevi e scala IoT progetti tooaddress IoT scenari comuni, ad esempio il monitoraggio remoto, gestione delle risorse e manutenzione predittiva.</span><span class="sxs-lookup"><span data-stu-id="ee63e-120">IoT Suite enables you tooget started quickly and scale IoT projects tooaddress common IoT scenarios--such as remote monitoring, asset management, and predictive maintenance.</span></span>

[lnk-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-iot-hub]: iot-hub-what-is-iot-hub.md
[lnk-iot-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-iotdev]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-device-management-overview.md
