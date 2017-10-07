---
title: messaggistica di Azure IoT Hub aaaUnderstand | Documenti Microsoft
description: Guida per gli sviluppatori - Messaggistica da dispositivo a cloud e da cloud a dispositivo con l'hub IoT. Include informazioni sui formati dei messaggi e sui protocolli di comunicazione supportati.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3fc5f1a3-3711-4611-9897-d4db079b4250
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: a610741e23e243f392f1c042f9ab4a00d42f734f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="device-to-cloud-and-cloud-to-device-messaging-with-iot-hub"></a>Messaggistica da dispositivo a cloud e da cloud a dispositivo con l'hub IoT

Usare l'IoT Hub messaggistica toocommunicate con i dispositivi da:

* L'invio di [da dispositivo a cloud] [ lnk-d2c] messaggi dalla soluzione tooyour dispositivi back-end.
* L'invio di [cloud a dispositivo] [ lnk-c2d] i messaggi dalla soluzione hello nuovamente terminare tooyour dispositivi.

Proprietà principali di funzionalità di messaggistica IoT Hub sono hello e affidabilità dei messaggi. Queste proprietà consentono la connettività di resilienza toointermittent sul lato dispositivo hello e tooload picchi in elaborazione sul lato cloud hello di eventi. L'hub IoT implementa *almeno una volta* le garanzie di recapito per la messaggistica da dispositivo a cloud e da cloud a dispositivo.

Per le funzionalità di toohello un'introduzione di IoT Hub, vedere gli articoli di hello [Azure e Internet of Things] [ lnk-azure-iot] e [Panoramica del servizio dell'IoT Hub Azure hello] [lnk-iot-hub-overview].

## <a name="when-toouse-iot-hub-messaging"></a>Quando toouse Hub IoT messaggistica

Utilizzare i messaggi da dispositivo a cloud per l'invio di avvisi e i dati di telemetria serie ora dall'app del dispositivo e cloud a dispositivo per app per dispositivi tooyour notifiche unidirezionale.

* Fare riferimento troppo[materiale sussidiario per la comunicazione da dispositivo a cloud] [ lnk-d2c-guidance] se in dubbio tra l'utilizzo di messaggi da dispositivo a cloud, proprietà segnalata o caricamento del file.
* Fare riferimento troppo[indicazioni di comunicazione Cloud a dispositivo] [ lnk-c2d-guidance] se in dubbio tra l'utilizzo di messaggi da cloud a dispositivo, le proprietà desiderate o metodi diretti.

## <a name="next-steps"></a>Passaggi successivi

* Informazioni sulla [messaggistica da dispositivo a cloud][lnk-d2c] dell'hub IoT.
* Informazioni sulla [messaggistica da cloud a dispositivo][lnk-c2d] dell'hub IoT.

[lnk-azure-iot]: iot-hub-what-is-azure-iot.md
[lnk-iot-hub-overview]: iot-hub-what-is-iot-hub.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md