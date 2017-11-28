---
title: aaaUnderstand hello Azure IoT SDK | Documenti Microsoft
description: "Guida per sviluppatori - informazioni e collegamenti toohello vari Azure IoT dispositivo e il servizio SDK che è possibile utilizzare le App per dispositivi toobuild e le applicazioni back-end."
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
ms.openlocfilehash: e319451ca97876666e1c011ee0e1a73d0a0f1ed1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-use-azure-iot-sdks"></a><span data-ttu-id="34418-103">Comprendere e usare gli SDK di Azure IoT</span><span class="sxs-lookup"><span data-stu-id="34418-103">Understand and use Azure IoT SDKs</span></span>

<span data-ttu-id="34418-104">Tre categorie di SDK sono disponibili per l'uso con l'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="34418-104">There are three categories of SDK for working with IoT Hub:</span></span>

* <span data-ttu-id="34418-105">**Dispositivo SDK** consentono toobuild App eseguite su dispositivi IoT.</span><span class="sxs-lookup"><span data-stu-id="34418-105">**Device SDKs** enable you toobuild apps that run on your IoT devices.</span></span> <span data-ttu-id="34418-106">Queste App hub IoT tooyour di telemetria di trasmissione e se lo si desidera ricevano messaggi dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="34418-106">These apps send telemetry tooyour IoT hub, and optionally receive messages from your IoT hub.</span></span>

* <span data-ttu-id="34418-107">**Servizio SDK** abilitare toomanage è l'hub IoT e, facoltativamente, inviare messaggi dispositivi IoT tooyour.</span><span class="sxs-lookup"><span data-stu-id="34418-107">**Service SDKs** enable you toomanage your IoT hub, and optionally send messages tooyour IoT devices.</span></span>

* <span data-ttu-id="34418-108">**Azure IoT Edge** consente si toobuild gateway tooenable dispositivi che non utilizzano uno dei protocolli hello è supportato oppure quando è necessario tooprocess messaggi sul bordo hello.</span><span class="sxs-lookup"><span data-stu-id="34418-108">**Azure IoT Edge** enables you toobuild gateways tooenable devices that don't use one of hello supported protocols, or when you need tooprocess messages on hello edge.</span></span>

<span data-ttu-id="34418-109">SDK sono forniti toosupport più linguaggi di programmazione.</span><span class="sxs-lookup"><span data-stu-id="34418-109">SDKs are provided toosupport multiple programming languages.</span></span>

## <a name="azure-iot-device-sdks"></a><span data-ttu-id="34418-110">SDK dispositivo IoT Azure</span><span class="sxs-lookup"><span data-stu-id="34418-110">Azure IoT device SDKs</span></span>

<span data-ttu-id="34418-111">Hello SDK dispositivo Microsoft Azure IoT contenga codice che facilita la compilazione dispositivi e applicazioni che si connettono tooand siano gestite da servizi di Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="34418-111">hello Microsoft Azure IoT device SDKs contain code that facilitates building devices and applications that connect tooand are managed by Azure IoT Hub services.</span></span>

<span data-ttu-id="34418-112">Hello SDK di dispositivo IoT di Azure seguenti sono disponibili toodownload da GitHub:</span><span class="sxs-lookup"><span data-stu-id="34418-112">hello following Azure IoT device SDKs are available toodownload from GitHub:</span></span>

* <span data-ttu-id="34418-113">[Azure IoT SDK per dispositivi per C][lnk-c-device-sdk] scritto in ANSI C (C99) per la portabilità e la compatibilità multipiattaforma.</span><span class="sxs-lookup"><span data-stu-id="34418-113">[Azure IoT device SDK for C][lnk-c-device-sdk] written in ANSI C (C99) for portability and broad platform compatibility.</span></span> <span data-ttu-id="34418-114">Esistono due librerie client di dispositivo per C, hello basso livello **iothub_client** hello e **serializzatore**.</span><span class="sxs-lookup"><span data-stu-id="34418-114">There are two device client libraries for C, hello low-level **iothub_client** and hello **serializer**.</span></span>
* <span data-ttu-id="34418-115">[Azure IoT SDK per dispositivi per .NET][lnk-dotnet-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="34418-115">[Azure IoT device SDK for .NET][lnk-dotnet-device-sdk]</span></span>
* <span data-ttu-id="34418-116">[Azure IoT SDK per dispositivi per Java][lnk-java-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="34418-116">[Azure IoT device SDK for Java][lnk-java-device-sdk]</span></span>
* <span data-ttu-id="34418-117">[Azure IoT SDK per dispositivi per Node.js][lnk-node-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="34418-117">[Azure IoT device SDK for Node.js][lnk-node-device-sdk]</span></span>
* <span data-ttu-id="34418-118">[Azure IoT SDK per dispositivi per Python][lnk-python-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="34418-118">[Azure IoT device SDK for Python][lnk-python-device-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="34418-119">File Leggimi di hello nei repository GitHub hello per informazioni sull'utilizzo di linguaggio e i file binari tooinstall responsabili di pacchetto specifico della piattaforma e dipendenze nel computer di sviluppo, vedere.</span><span class="sxs-lookup"><span data-stu-id="34418-119">See hello readme files in hello GitHub repositories for information about using language and platform-specific package managers tooinstall binaries and dependencies on your development machine.</span></span>
> 
> 

### <a name="os-platform-and-hardware-compatibility"></a><span data-ttu-id="34418-120">Compatibilità delle piattaforme del sistema operativo e hardware</span><span class="sxs-lookup"><span data-stu-id="34418-120">OS platform and hardware compatibility</span></span>

<span data-ttu-id="34418-121">Per ulteriori informazioni sulla compatibilità del SDK con dispositivi hardware specifici, vedere hello [Azure Certified per catalogo dispositivo IoT][lnk-certified].</span><span class="sxs-lookup"><span data-stu-id="34418-121">For more information about SDK compatibility with specific hardware devices, see hello [Azure Certified for IoT device catalog][lnk-certified].</span></span>

## <a name="azure-iot-service-sdks"></a><span data-ttu-id="34418-122">Azure IoT SDK per servizi</span><span class="sxs-lookup"><span data-stu-id="34418-122">Azure IoT service SDKs</span></span>

<span data-ttu-id="34418-123">servizio di Azure IoT Hello SDK contengono codice toofacilitate compilazione di applicazioni che interagiscono direttamente con sicurezza e i dispositivi toomanage IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="34418-123">hello Azure IoT service SDKs contain code toofacilitate building applications that interact directly with IoT Hub toomanage devices and security.</span></span>

<span data-ttu-id="34418-124">Hello seguente Azure IoT servizio SDK sono disponibili toodownload da GitHub:</span><span class="sxs-lookup"><span data-stu-id="34418-124">hello following Azure IoT service SDKs are available toodownload from GitHub:</span></span>

* <span data-ttu-id="34418-125">[Azure IoT SDK per servizi per .NET][lnk-dotnet-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="34418-125">[Azure IoT service SDK for .NET][lnk-dotnet-service-sdk]</span></span>
* <span data-ttu-id="34418-126">[Azure IoT SDK per servizi per Node.js][lnk-node-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="34418-126">[Azure IoT service SDK for Node.js][lnk-node-service-sdk]</span></span>
* <span data-ttu-id="34418-127">[Azure IoT SDK per servizi per Java][lnk-java-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="34418-127">[Azure IoT service SDK for Java][lnk-java-service-sdk]</span></span>
* <span data-ttu-id="34418-128">[Azure IoT SDK per dispositivi per Python][lnk-python-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="34418-128">[Azure IoT service SDK for Python][lnk-python-service-sdk]</span></span>
* <span data-ttu-id="34418-129">[Azure IoT SDK per servizi per C][lnk-c-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="34418-129">[Azure IoT service SDK for C][lnk-c-service-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="34418-130">File Leggimi di hello nei repository GitHub hello per informazioni sull'utilizzo di linguaggio e i file binari tooinstall responsabili di pacchetto specifico della piattaforma e dipendenze nel computer di sviluppo, vedere.</span><span class="sxs-lookup"><span data-stu-id="34418-130">See hello readme files in hello GitHub repositories for information about using language and platform-specific package managers tooinstall binaries and dependencies on your development machine.</span></span>

## <a name="azure-iot-edge"></a><span data-ttu-id="34418-131">Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="34418-131">Azure IoT Edge</span></span>

<span data-ttu-id="34418-132">Azure IoT Edge contiene hello infrastruttura e i moduli toocreate IoT gateway soluzioni.</span><span class="sxs-lookup"><span data-stu-id="34418-132">Azure IoT Edge contains hello infrastructure and modules toocreate IoT gateway solutions.</span></span> <span data-ttu-id="34418-133">È possibile estendere uno scenario end-to-end di IoT Edge toocreate gateway tooany personalizzata.</span><span class="sxs-lookup"><span data-stu-id="34418-133">You can extend IoT Edge toocreate gateways tailored tooany end-to-end scenario.</span></span>

<span data-ttu-id="34418-134">È possibile scaricare [Azure IoT Edge][lnk-iot-edge] da GitHub.</span><span class="sxs-lookup"><span data-stu-id="34418-134">You can download [Azure IoT Edge][lnk-iot-edge] from GitHub.</span></span>

## <a name="online-api-reference-documentation"></a><span data-ttu-id="34418-135">Documentazione di riferimento API online</span><span class="sxs-lookup"><span data-stu-id="34418-135">Online API reference documentation</span></span>

<span data-ttu-id="34418-136">Hello elenco seguente contiene collegamenti tooonline API la documentazione di riferimento per i dispositivi IoT di Azure, servizio e librerie di gateway:</span><span class="sxs-lookup"><span data-stu-id="34418-136">hello following list contains links tooonline API reference documentation for Azure IoT device, service, and gateway libraries:</span></span>

* <span data-ttu-id="34418-137">[Internet of Things (IoT) .NET][lnk-dotnet-ref]</span><span class="sxs-lookup"><span data-stu-id="34418-137">[Internet of Things (IoT) .NET][lnk-dotnet-ref]</span></span>
* <span data-ttu-id="34418-138">[REST hub IoT][lnk-rest-ref]</span><span class="sxs-lookup"><span data-stu-id="34418-138">[IoT Hub REST][lnk-rest-ref]</span></span>
* <span data-ttu-id="34418-139">[Azure IoT SDK per dispositivi per C][lnk-c-ref]</span><span class="sxs-lookup"><span data-stu-id="34418-139">[Azure IoT device SDK for C][lnk-c-ref]</span></span>
* <span data-ttu-id="34418-140">[Azure IoT SDK per dispositivi per Java][lnk-java-ref]</span><span class="sxs-lookup"><span data-stu-id="34418-140">[Azure IoT device SDK for Java][lnk-java-ref]</span></span>
* <span data-ttu-id="34418-141">[Azure IoT SDK per servizi per Java][lnk-java-service-ref]</span><span class="sxs-lookup"><span data-stu-id="34418-141">[Azure IoT service SDK for Java][lnk-java-service-ref]</span></span>
* <span data-ttu-id="34418-142">[Azure IoT SDK per dispositivi per Node.js][lnk-node-ref]</span><span class="sxs-lookup"><span data-stu-id="34418-142">[Azure IoT device SDK for Node.js][lnk-node-ref]</span></span>
* <span data-ttu-id="34418-143">[Azure IoT SDK per servizi per Node.js][lnk-node-service-ref]</span><span class="sxs-lookup"><span data-stu-id="34418-143">[Azure IoT service SDK for Node.js][lnk-node-service-ref]</span></span>
* <span data-ttu-id="34418-144">[Azure IoT Edge][lnk-gateway-ref]</span><span class="sxs-lookup"><span data-stu-id="34418-144">[Azure IoT Edge][lnk-gateway-ref]</span></span>

## <a name="next-steps"></a><span data-ttu-id="34418-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="34418-145">Next steps</span></span>

<span data-ttu-id="34418-146">Di seguito sono indicati altri argomenti di riferimento reperibili nella Guida per gli sviluppatori dell'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="34418-146">Other reference topics in this IoT Hub developer guide include:</span></span>

* <span data-ttu-id="34418-147">[Endpoint dell'hub IoT][lnk-devguide-endpoints]</span><span class="sxs-lookup"><span data-stu-id="34418-147">[IoT Hub endpoints][lnk-devguide-endpoints]</span></span>
* <span data-ttu-id="34418-148">[Linguaggio di query dell'hub IoT per dispositivi gemelli, processi e routing messaggi][lnk-devguide-query]</span><span class="sxs-lookup"><span data-stu-id="34418-148">[IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query]</span></span>
* <span data-ttu-id="34418-149">[Quote e limitazioni][lnk-devguide-quotas]</span><span class="sxs-lookup"><span data-stu-id="34418-149">[Quotas and throttling][lnk-devguide-quotas]</span></span>
* <span data-ttu-id="34418-150">[Supporto di MQTT nell'hub IoT][lnk-devguide-mqtt]</span><span class="sxs-lookup"><span data-stu-id="34418-150">[IoT Hub MQTT support][lnk-devguide-mqtt]</span></span>

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
