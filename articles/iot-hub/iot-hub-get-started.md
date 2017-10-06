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
# <a name="azure-iot-hub-get-started-tutorials"></a>Esercitazioni introduttive sull'Hub IoT Azure

È possibile utilizzare Azure IoT Hub hello Azure IoT soluzioni dei dispositivi e gli SDK toobuild Internet delle cose (IoT):

* IoT Hub Azure è un servizio completamente gestito nel cloud hello che si connette in modo sicuro, consente di monitorare e gestire i dispositivi IoT. Utilizzare hello dispositivo IoT di Azure SDK tooimplement i dispositivi IoT.
* Usare un gateway IoT in scenari IoT più complessi. Ad esempio, in cui è necessario tooconsider fattori, ad esempio dispositivi legacy, i costi di larghezza di banda, i criteri di sicurezza e privacy o l'elaborazione dati di bordo. In questi scenari, si utilizza Azure IoT Edge tooimplement un gateway che si connette l'hub IoT tooyour dispositivi.

## <a name="what-hello-tutorials-cover"></a>Le esercitazioni di hello riguardano

Queste esercitazioni vengono fornite informazioni si tooAzure IoT Hub e il dispositivo di hello SDK. esercitazioni di Hello riguardano IoT scenari toodemonstrate hello funzionalità comuni dell'IoT Hub. Hello esercitazioni viene inoltre illustrano come toocombine IoT Hub con altri Azure dei servizi e toobuild degli strumenti più potenti soluzioni IoT. Nelle esercitazioni di hello, è possibile scegliere i dispositivi IoT simulati o reali toouse. Inoltre, sono disponibili come toouse un gateway tooenable dispositivi tooconnect tooyour l'hub IoT.

## <a name="set-up-your-device"></a>Configurare il dispositivo

Connettere un IoT dispositivo o il gateway tooAzure IoT Hub. È possibile scegliere tooget un dispositivo fisico o simulato avviato:

| Dispositivo IoT                       | Linguaggio di programmazione |
|----------------------------------|----------------------|
| Raspberry Pi                     | [Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]  |
| DevKit di IoT                       | [Arduino in VSCode][DevKit]     |
| Intel Edison                     | [Node.js][Ed_Nd], [C][Ed_C]    |
| Adafruit Feather HUZZAH ESP8266  | [Arduino][Hu_Ard]              |
| Sparkfun ESP8266 Thing Dev       | [Arduino][Th_Ard]              |
| Adafruit Feather M0              | [Arduino][M0_Ard]              |
| Dispositivo simulato nel PC           | [.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd], [Python][Sim_Pyth] |
| Simulatore di dispositivi online         | [Raspberry Pi (Node.js)][Ol_Sim] |

Inoltre, è possibile utilizzare un bordo IoT gateway tooenable dispositivi tooconnect tooyour l'hub IoT:

| Dispositivo gateway               | Linguaggio di programmazione | Piattaforma         |
|------------------------------|----------------------|------------------|
| Intel NUC (modello DE3815TYKE) | C                    | [Wind River Linux][NUC_Lnx] |
| Gateway simulato            | C                    | [Linux][Sim_Lnx], [Windows][Sim_Win] |

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
