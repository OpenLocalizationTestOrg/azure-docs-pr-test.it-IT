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

## <a name="next-steps"></a>Passaggi successivi

Hub IoT di Azure è un servizio che consente comunicazioni bidirezionali affidabili e sicure tra il back-end della soluzione e milioni di dispositivi. Consente di hello soluzione back-end:

* Ricevere dati di telemetria su larga scala dai dispositivi.
* Dati della route dal processore di eventi flusso tooa dispositivi.
* Ricevere caricamenti di file dai dispositivi.
* Inviare messaggi da cloud a dispositivo toospecific dispositivi.

È possibile usare l'IoT Hub tooimplement terminare la propria soluzione nuovamente. Inoltre, l'IoT Hub include dispositivi di tooprovision del Registro di sistema utilizzato di identità, le proprie credenziali di sicurezza e l'hub IoT toohello tooconnect i relativi diritti. toolearn ulteriori informazioni sull'IoT Hub, vedere [che cos'è l'IoT Hub?] [lnk-iot-hub].

toolearn come IoT Hub Azure consente di attivare la gestione dei dispositivi basata su standard per gestire, configurare e aggiornare i dispositivi, si tooremotely vedere [Panoramica di gestione dei dispositivi con l'IoT Hub][lnk-device-management].

le applicazioni client tooimplement su una vasta gamma di piattaforme per dispositivi hardware e sistemi operativi, è possibile usare il dispositivo di Azure IoT hello SDK. il dispositivo di Hello SDK include librerie che semplificano l'invio dati di telemetria tooan IoT hub e la ricezione cloud a dispositivo di messaggi. Quando si usa il dispositivo di hello SDK, è possibile scegliere tra diversi toocommunicate di protocolli di rete con l'IoT Hub. toolearn informazioni, vedere hello [informazioni sul dispositivo SDK][lnk-device-sdks].

tooget avviato scrivere del codice ed esecuzione di alcuni esempi, vedere hello [iniziare con l'IoT Hub] [ lnk-getstarted] esercitazione.

Si potrebbe anche essere interessati a [Azure IoT Suite][lnk-iot-suite], che è una raccolta di soluzioni preconfigurate. IoT Suite consente tooget in tempi brevi e scala IoT progetti tooaddress IoT scenari comuni, ad esempio il monitoraggio remoto, gestione delle risorse e manutenzione predittiva.

[lnk-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-iot-hub]: iot-hub-what-is-iot-hub.md
[lnk-iot-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-iotdev]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-device-management-overview.md
