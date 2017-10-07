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
# <a name="understand-and-use-azure-iot-sdks"></a>Comprendere e usare gli SDK di Azure IoT

Tre categorie di SDK sono disponibili per l'uso con l'hub IoT:

* **Dispositivo SDK** consentono toobuild App eseguite su dispositivi IoT. Queste App hub IoT tooyour di telemetria di trasmissione e se lo si desidera ricevano messaggi dall'hub IoT.

* **Servizio SDK** abilitare toomanage è l'hub IoT e, facoltativamente, inviare messaggi dispositivi IoT tooyour.

* **Azure IoT Edge** consente si toobuild gateway tooenable dispositivi che non utilizzano uno dei protocolli hello è supportato oppure quando è necessario tooprocess messaggi sul bordo hello.

SDK sono forniti toosupport più linguaggi di programmazione.

## <a name="azure-iot-device-sdks"></a>SDK dispositivo IoT Azure

Hello SDK dispositivo Microsoft Azure IoT contenga codice che facilita la compilazione dispositivi e applicazioni che si connettono tooand siano gestite da servizi di Azure IoT Hub.

Hello SDK di dispositivo IoT di Azure seguenti sono disponibili toodownload da GitHub:

* [Azure IoT SDK per dispositivi per C][lnk-c-device-sdk] scritto in ANSI C (C99) per la portabilità e la compatibilità multipiattaforma. Esistono due librerie client di dispositivo per C, hello basso livello **iothub_client** hello e **serializzatore**.
* [Azure IoT SDK per dispositivi per .NET][lnk-dotnet-device-sdk]
* [Azure IoT SDK per dispositivi per Java][lnk-java-device-sdk]
* [Azure IoT SDK per dispositivi per Node.js][lnk-node-device-sdk]
* [Azure IoT SDK per dispositivi per Python][lnk-python-device-sdk]

> [!NOTE]
> File Leggimi di hello nei repository GitHub hello per informazioni sull'utilizzo di linguaggio e i file binari tooinstall responsabili di pacchetto specifico della piattaforma e dipendenze nel computer di sviluppo, vedere.
> 
> 

### <a name="os-platform-and-hardware-compatibility"></a>Compatibilità delle piattaforme del sistema operativo e hardware

Per ulteriori informazioni sulla compatibilità del SDK con dispositivi hardware specifici, vedere hello [Azure Certified per catalogo dispositivo IoT][lnk-certified].

## <a name="azure-iot-service-sdks"></a>Azure IoT SDK per servizi

servizio di Azure IoT Hello SDK contengono codice toofacilitate compilazione di applicazioni che interagiscono direttamente con sicurezza e i dispositivi toomanage IoT Hub.

Hello seguente Azure IoT servizio SDK sono disponibili toodownload da GitHub:

* [Azure IoT SDK per servizi per .NET][lnk-dotnet-service-sdk]
* [Azure IoT SDK per servizi per Node.js][lnk-node-service-sdk]
* [Azure IoT SDK per servizi per Java][lnk-java-service-sdk]
* [Azure IoT SDK per dispositivi per Python][lnk-python-service-sdk]
* [Azure IoT SDK per servizi per C][lnk-c-service-sdk]

> [!NOTE]
> File Leggimi di hello nei repository GitHub hello per informazioni sull'utilizzo di linguaggio e i file binari tooinstall responsabili di pacchetto specifico della piattaforma e dipendenze nel computer di sviluppo, vedere.

## <a name="azure-iot-edge"></a>Azure IoT Edge

Azure IoT Edge contiene hello infrastruttura e i moduli toocreate IoT gateway soluzioni. È possibile estendere uno scenario end-to-end di IoT Edge toocreate gateway tooany personalizzata.

È possibile scaricare [Azure IoT Edge][lnk-iot-edge] da GitHub.

## <a name="online-api-reference-documentation"></a>Documentazione di riferimento API online

Hello elenco seguente contiene collegamenti tooonline API la documentazione di riferimento per i dispositivi IoT di Azure, servizio e librerie di gateway:

* [Internet of Things (IoT) .NET][lnk-dotnet-ref]
* [REST hub IoT][lnk-rest-ref]
* [Azure IoT SDK per dispositivi per C][lnk-c-ref]
* [Azure IoT SDK per dispositivi per Java][lnk-java-ref]
* [Azure IoT SDK per servizi per Java][lnk-java-service-ref]
* [Azure IoT SDK per dispositivi per Node.js][lnk-node-ref]
* [Azure IoT SDK per servizi per Node.js][lnk-node-service-ref]
* [Azure IoT Edge][lnk-gateway-ref]

## <a name="next-steps"></a>Passaggi successivi

Di seguito sono indicati altri argomenti di riferimento reperibili nella Guida per gli sviluppatori dell'hub IoT:

* [Endpoint dell'hub IoT][lnk-devguide-endpoints]
* [Linguaggio di query dell'hub IoT per dispositivi gemelli, processi e routing messaggi][lnk-devguide-query]
* [Quote e limitazioni][lnk-devguide-quotas]
* [Supporto di MQTT nell'hub IoT][lnk-devguide-mqtt]

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
