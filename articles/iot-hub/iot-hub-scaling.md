---
title: "scalabilità Hub IoT aaaAzure | Documenti Microsoft"
description: "Come tooscale il toosupport hub IoT la velocità effettiva dei messaggi previsti. Include un riepilogo delle opzioni per il partizionamento orizzontale e velocità effettiva di hello è supportato per ogni livello."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: e7bd4968-db46-46cf-865d-9c944f683832
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3b8bf6c44631c65b34b69752d9043c21db24bb01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-your-iot-hub-solution"></a>Ridimensionare la soluzione hub IoT
IoT Hub Azure può supportare i dispositivi connessi contemporaneamente milioni tooa. Per altre informazioni, vedere i [prezzi dell'hub IoT][lnk-pricing]. Ogni unità hub IoT mette a disposizione un certo numero di messaggi giornalieri.

tooproperly ampliamento della soluzione, considerare l'utilizzo dell'IoT Hub in questione. In particolare, valutare una velocità effettiva di picco hello necessario per hello categorie delle operazioni seguenti:

* Messaggi da dispositivo a cloud
* Messaggi da cloud a dispositivo
* Operazioni del registro delle identità

Nelle informazioni di velocità effettiva di addizione toothis, vedere [IoT Hub quote e velocità] [ IoT Hub quotas and throttles] e progettare di conseguenza la soluzione.

## <a name="device-to-cloud-and-cloud-to-device-message-throughput"></a>Velocità effettiva dei messaggi da dispositivo a cloud e da cloud a dispositivo.
Hello migliore modo toosize una soluzione di IoT Hub è traffico hello tooevaluate singolo per unità.

I messaggi da dispositivo a cloud seguono queste linee guida in caso di velocità effettiva sostenuta

| Livello | Velocità effettiva sostenuta | Frequenza di invio sostenuta |
| --- | --- | --- |
| S1 |Backup too1111 KB al minuto per unità<br/>(1,5 GB al giorno per unità) |Una media di 278 messaggi al minuto per unità<br/>(400.000 messaggi al giorno per unità) |
| S2 |Backup too16 MB al minuto per unità<br/>(22,8 GB al giorno per unità) |Una media di 4.167 messaggi al minuto per unità<br/>(6 milioni di messaggi al giorno per unità) |
| S3 |Backup too814 MB al minuto per unità<br/>(1144,4 GB al giorno per unità) |Una media di 208,333 messaggi al minuto per unità<br/>(300 milioni di messaggi al giorno per unità) |

## <a name="identity-registry-operation-throughput"></a>Velocità effettiva delle operazioni del registro delle identità
Le operazioni del Registro di sistema di identità IoT Hub non dovrebbero toobe operazioni di runtime, come se fossero principalmente provisioning toodevice correlati.

Per i dati specifici sulle prestazioni in modalità burst, vedere le [quote e limitazioni dell'hub IoT][IoT Hub quotas and throttles].

## <a name="sharding"></a>Partizionamento orizzontale
Mentre un singolo hub IoT adattabile toomillions dei dispositivi, in alcuni casi la soluzione richiede caratteristiche di prestazioni specifiche che non può garantire un singolo hub IoT. In tal caso, è consigliabile partizionare i dispositivi in più hub IoT. Hub IoT più uniformare i picchi di traffico e ottenere throughput necessario hello o tassi di operazione sono necessari.

## <a name="next-steps"></a>Passaggi successivi
toofurther esplorare le funzionalità di hello di IoT Hub, vedere:

* [Guida per gli sviluppatori dell'hub IoT][lnk-devguide]
* [Simulazione di un dispositivo con Azure IoT Edge][lnk-iotedge]

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[IoT Hub quotas and throttles]: iot-hub-devguide-quotas-throttling.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
