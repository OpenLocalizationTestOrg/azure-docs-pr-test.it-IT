---
title: Informazioni sugli SDK dell'hub IoT | Documentazione Microsoft
description: "Guida per gli sviluppatori: informazioni e collegamenti ai vari Azure IoT SDK per dispositivi e servizi che è possibile usare per compilare app per dispositivo e app back-end."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: c5c9a497-bb03-4301-be2d-00edfb7d308f
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bcbf4b9633f58293edb19aeb33dec6602ac4ec8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="understand-and-use-azure-iot-sdks"></a><span data-ttu-id="d3481-103">Comprendere e usare gli SDK di Azure IoT</span><span class="sxs-lookup"><span data-stu-id="d3481-103">Understand and use Azure IoT SDKs</span></span>

<span data-ttu-id="d3481-104">Tre categorie di SDK sono disponibili per l'uso con l'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="d3481-104">There are three categories of SDK for working with IoT Hub:</span></span>

* <span data-ttu-id="d3481-105">Gli **SDK per dispositivi** consentono di compilare le app eseguite su dispositivi IoT.</span><span class="sxs-lookup"><span data-stu-id="d3481-105">**Device SDKs** enable you to build apps that run on your IoT devices.</span></span> <span data-ttu-id="d3481-106">Queste app inviano la telemetria all'hub IoT e, facoltativamente, ricevono messaggi dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="d3481-106">These apps send telemetry to your IoT hub, and optionally receive messages from your IoT hub.</span></span>

* <span data-ttu-id="d3481-107">Gli **SDK per servizi** consentono di gestire l'hub IoT e, facoltativamente, inviare messaggi ai dispositivi IoT.</span><span class="sxs-lookup"><span data-stu-id="d3481-107">**Service SDKs** enable you to manage your IoT hub, and optionally send messages to your IoT devices.</span></span>

* <span data-ttu-id="d3481-108">**Azure IoT Edge** consente di creare gateway per permettere l'uso di dispositivi che non usano uno dei protocolli supportati o quando è necessario elaborare messaggi sul perimetro.</span><span class="sxs-lookup"><span data-stu-id="d3481-108">**Azure IoT Edge** enables you to build gateways to enable devices that don't use one of the supported protocols, or when you need to process messages on the edge.</span></span>

<span data-ttu-id="d3481-109">Vengono forniti SDK per supportare più linguaggi di programmazione.</span><span class="sxs-lookup"><span data-stu-id="d3481-109">SDKs are provided to support multiple programming languages.</span></span>

## <a name="azure-iot-device-sdks"></a><span data-ttu-id="d3481-110">SDK dispositivo IoT Azure</span><span class="sxs-lookup"><span data-stu-id="d3481-110">Azure IoT device SDKs</span></span>

<span data-ttu-id="d3481-111">GLI SDK per dispositivi IoT di Microsoft Azure contengono codice che facilita la compilazione dei dispositivi e delle applicazioni che si connettono e sono gestite dai servizi hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="d3481-111">The Microsoft Azure IoT device SDKs contain code that facilitates building devices and applications that connect to and are managed by Azure IoT Hub services.</span></span>

<span data-ttu-id="d3481-112">I seguenti Azure IoT SDK per dispositivi sono disponibili per il download da GitHub:</span><span class="sxs-lookup"><span data-stu-id="d3481-112">The following Azure IoT device SDKs are available to download from GitHub:</span></span>

* <span data-ttu-id="d3481-113">[Azure IoT SDK per dispositivi per C][lnk-c-device-sdk] scritto in ANSI C (C99) per la portabilità e la compatibilità multipiattaforma.</span><span class="sxs-lookup"><span data-stu-id="d3481-113">[Azure IoT device SDK for C][lnk-c-device-sdk] written in ANSI C (C99) for portability and broad platform compatibility.</span></span> <span data-ttu-id="d3481-114">Sono presenti due librerie client di dispositivi per C, l'**iothub_client** di basso livello e il **serializzatore**.</span><span class="sxs-lookup"><span data-stu-id="d3481-114">There are two device client libraries for C, the low-level **iothub_client** and the **serializer**.</span></span>
* <span data-ttu-id="d3481-115">[Azure IoT SDK per dispositivi per .NET][lnk-dotnet-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="d3481-115">[Azure IoT device SDK for .NET][lnk-dotnet-device-sdk]</span></span>
* <span data-ttu-id="d3481-116">[Azure IoT SDK per dispositivi per Java][lnk-java-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="d3481-116">[Azure IoT device SDK for Java][lnk-java-device-sdk]</span></span>
* <span data-ttu-id="d3481-117">[Azure IoT SDK per dispositivi per Node.js][lnk-node-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="d3481-117">[Azure IoT device SDK for Node.js][lnk-node-device-sdk]</span></span>
* <span data-ttu-id="d3481-118">[Azure IoT SDK per dispositivi per Python][lnk-python-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="d3481-118">[Azure IoT device SDK for Python][lnk-python-device-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="d3481-119">Vedere i file Leggimi nei repository GitHub per informazioni sull'uso di gestori di pacchetti specifici per piattaforma e linguaggio e installare file binari e dipendenze nel computer di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="d3481-119">See the readme files in the GitHub repositories for information about using language and platform-specific package managers to install binaries and dependencies on your development machine.</span></span>
> 
> 

### <a name="os-platform-and-hardware-compatibility"></a><span data-ttu-id="d3481-120">Compatibilità delle piattaforme del sistema operativo e hardware</span><span class="sxs-lookup"><span data-stu-id="d3481-120">OS platform and hardware compatibility</span></span>

<span data-ttu-id="d3481-121">Per altre informazioni sulla compatibilità SDK con i dispositivi hardware specifici, vedere il [catalogo di dispositivi Azure Certified per IoT][lnk-certified].</span><span class="sxs-lookup"><span data-stu-id="d3481-121">For more information about SDK compatibility with specific hardware devices, see the [Azure Certified for IoT device catalog][lnk-certified].</span></span>

## <a name="azure-iot-service-sdks"></a><span data-ttu-id="d3481-122">Azure IoT SDK per servizi</span><span class="sxs-lookup"><span data-stu-id="d3481-122">Azure IoT service SDKs</span></span>

<span data-ttu-id="d3481-123">I componenti Azure Iot SDK per servizi contengono codice che facilita la compilazione di applicazioni che interagiscono direttamente con l'hub IoT per gestire dispositivi e sicurezza.</span><span class="sxs-lookup"><span data-stu-id="d3481-123">The Azure IoT service SDKs contain code to facilitate building applications that interact directly with IoT Hub to manage devices and security.</span></span>

<span data-ttu-id="d3481-124">I seguenti Azure IoT SDK per servizi sono disponibili per il download da GitHub:</span><span class="sxs-lookup"><span data-stu-id="d3481-124">The following Azure IoT service SDKs are available to download from GitHub:</span></span>

* <span data-ttu-id="d3481-125">[Azure IoT SDK per servizi per .NET][lnk-dotnet-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="d3481-125">[Azure IoT service SDK for .NET][lnk-dotnet-service-sdk]</span></span>
* <span data-ttu-id="d3481-126">[Azure IoT SDK per servizi per Node.js][lnk-node-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="d3481-126">[Azure IoT service SDK for Node.js][lnk-node-service-sdk]</span></span>
* <span data-ttu-id="d3481-127">[Azure IoT SDK per servizi per Java][lnk-java-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="d3481-127">[Azure IoT service SDK for Java][lnk-java-service-sdk]</span></span>
* <span data-ttu-id="d3481-128">[Azure IoT SDK per dispositivi per Python][lnk-python-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="d3481-128">[Azure IoT service SDK for Python][lnk-python-service-sdk]</span></span>
* <span data-ttu-id="d3481-129">[Azure IoT SDK per servizi per C][lnk-c-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="d3481-129">[Azure IoT service SDK for C][lnk-c-service-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="d3481-130">Vedere i file Leggimi nei repository GitHub per informazioni sull'uso di gestori di pacchetti specifici per piattaforma e linguaggio e installare file binari e dipendenze nel computer di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="d3481-130">See the readme files in the GitHub repositories for information about using language and platform-specific package managers to install binaries and dependencies on your development machine.</span></span>

## <a name="azure-iot-edge"></a><span data-ttu-id="d3481-131">Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="d3481-131">Azure IoT Edge</span></span>

<span data-ttu-id="d3481-132">Azure IoT Edge contiene l'infrastruttura e i moduli per creare soluzioni gateway IoT.</span><span class="sxs-lookup"><span data-stu-id="d3481-132">Azure IoT Edge contains the infrastructure and modules to create IoT gateway solutions.</span></span> <span data-ttu-id="d3481-133">È possibile estendere IoT Edge per creare gateway personalizzati in base agli scenari end-to-end.</span><span class="sxs-lookup"><span data-stu-id="d3481-133">You can extend IoT Edge to create gateways tailored to any end-to-end scenario.</span></span>

<span data-ttu-id="d3481-134">È possibile scaricare [Azure IoT Edge][lnk-iot-edge] da GitHub.</span><span class="sxs-lookup"><span data-stu-id="d3481-134">You can download [Azure IoT Edge][lnk-iot-edge] from GitHub.</span></span>

## <a name="online-api-reference-documentation"></a><span data-ttu-id="d3481-135">Documentazione di riferimento API online</span><span class="sxs-lookup"><span data-stu-id="d3481-135">Online API reference documentation</span></span>

<span data-ttu-id="d3481-136">L'elenco seguente contiene un elenco di collegamenti alla documentazione di riferimento all'API online per librerie di dispositivi, servizi e gateway di Azure IoT:</span><span class="sxs-lookup"><span data-stu-id="d3481-136">The following list contains links to online API reference documentation for Azure IoT device, service, and gateway libraries:</span></span>

* <span data-ttu-id="d3481-137">[Internet of Things (IoT) .NET][lnk-dotnet-ref]</span><span class="sxs-lookup"><span data-stu-id="d3481-137">[Internet of Things (IoT) .NET][lnk-dotnet-ref]</span></span>
* <span data-ttu-id="d3481-138">[REST hub IoT][lnk-rest-ref]</span><span class="sxs-lookup"><span data-stu-id="d3481-138">[IoT Hub REST][lnk-rest-ref]</span></span>
* <span data-ttu-id="d3481-139">[Azure IoT SDK per dispositivi per C][lnk-c-ref]</span><span class="sxs-lookup"><span data-stu-id="d3481-139">[Azure IoT device SDK for C][lnk-c-ref]</span></span>
* <span data-ttu-id="d3481-140">[Azure IoT SDK per dispositivi per Java][lnk-java-ref]</span><span class="sxs-lookup"><span data-stu-id="d3481-140">[Azure IoT device SDK for Java][lnk-java-ref]</span></span>
* <span data-ttu-id="d3481-141">[Azure IoT SDK per servizi per Java][lnk-java-service-ref]</span><span class="sxs-lookup"><span data-stu-id="d3481-141">[Azure IoT service SDK for Java][lnk-java-service-ref]</span></span>
* <span data-ttu-id="d3481-142">[Azure IoT SDK per dispositivi per Node.js][lnk-node-ref]</span><span class="sxs-lookup"><span data-stu-id="d3481-142">[Azure IoT device SDK for Node.js][lnk-node-ref]</span></span>
* <span data-ttu-id="d3481-143">[Azure IoT SDK per servizi per Node.js][lnk-node-service-ref]</span><span class="sxs-lookup"><span data-stu-id="d3481-143">[Azure IoT service SDK for Node.js][lnk-node-service-ref]</span></span>
* <span data-ttu-id="d3481-144">[Azure IoT Edge][lnk-gateway-ref]</span><span class="sxs-lookup"><span data-stu-id="d3481-144">[Azure IoT Edge][lnk-gateway-ref]</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3481-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d3481-145">Next steps</span></span>

<span data-ttu-id="d3481-146">Di seguito sono indicati altri argomenti di riferimento reperibili nella Guida per gli sviluppatori dell'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="d3481-146">Other reference topics in this IoT Hub developer guide include:</span></span>

* <span data-ttu-id="d3481-147">[Endpoint dell'hub IoT][lnk-devguide-endpoints]</span><span class="sxs-lookup"><span data-stu-id="d3481-147">[IoT Hub endpoints][lnk-devguide-endpoints]</span></span>
* <span data-ttu-id="d3481-148">[Linguaggio di query dell'hub IoT per dispositivi gemelli, processi e routing messaggi][lnk-devguide-query]</span><span class="sxs-lookup"><span data-stu-id="d3481-148">[IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query]</span></span>
* <span data-ttu-id="d3481-149">[Quote e limitazioni][lnk-devguide-quotas]</span><span class="sxs-lookup"><span data-stu-id="d3481-149">[Quotas and throttling][lnk-devguide-quotas]</span></span>
* <span data-ttu-id="d3481-150">[Supporto di MQTT nell'hub IoT][lnk-devguide-mqtt]</span><span class="sxs-lookup"><span data-stu-id="d3481-150">[IoT Hub MQTT support][lnk-devguide-mqtt]</span></span>

<!-- Links and images -->

[lnk-c-device-sdk]: https://github.com/Azure/azure-iot-sdk-c
[lnk-c-service-sdk]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_service_client
[lnk-dotnet-device-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device
[lnk-java-device-sdk]: https://github.com/Azure/azure-iot-sdk-java/tree/master/device
[lnk-dotnet-service-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/service
[lnk-java-service-sdk]: https://github.com/Azure/azure-iot-sdk-java/tree/master/service
[lnk-node-device-sdk]: https://github.com/Azure/azure-iot-sdk-node/tree/master/device
[lnk-node-service-sdk]: https://github.com/Azure/azure-iot-sdk-node/tree/master/service
[lnk-python-device-sdk]: https://github.com/Azure/azure-iot-sdk-python/tree/master/device
[lnk-python-service-sdk]: https://github.com/Azure/azure-iot-sdk-python/tree/master/service
[lnk-certified]: https://catalog.azureiotsuite.com/
[lnk-iot-edge]: https://github.com/Azure/iot-edge

[lnk-dotnet-ref]: https://docs.microsoft.com/dotnet/api/microsoft.azure.devices
[lnk-c-ref]: https://azure.github.io/azure-iot-sdk-c/index.html
[lnk-java-ref]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.device
[lnk-node-ref]: https://azure.github.io/azure-iot-sdk-node/
[lnk-rest-ref]: https://docs.microsoft.com/rest/api/iothub/
[lnk-java-service-ref]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.service.auth
[lnk-node-service-ref]: https://azure.github.io/azure-iot-sdk-node/
[lnk-gateway-ref]: http://azure.github.io/iot-edge/api_reference/c/html/

[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
