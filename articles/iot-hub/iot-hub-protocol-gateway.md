---
title: gateway del protocollo IoT aaaAzure | Documenti Microsoft
description: "Toouse un Azure IoT del protocollo come funzionalità di gateway tooextend Hub IoT e protocollo supporto tooenable dispositivi tooconnect tooyour hub utilizzando protocolli non supportati dall'IoT Hub in modo nativo."
services: iot-hub
documentationcenter: 
author: kdotchkoff
manager: timlt
editor: 
ms.assetid: 555e59ae-3136-4533-8ba8-f3a3b6acf648
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: kdotchko
ms.openlocfilehash: 9cfed30149672d8f7e021a9899192105bbcdd400
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# Supportare altri protocolli per l'hub IoT
IoT Hub Azure supporta in modo nativo la comunicazione su protocolli di hello MQTT, AMQP e HTTP. In alcuni casi, i dispositivi o gateway campo potrebbe non essere in grado di toouse uno di questi protocolli standard e richiederà l'adattamento di protocollo. In questi casi, è possibile utilizzare un gateway personalizzato. Un gateway personalizzato abilitare adattamento di protocollo per gli endpoint IoT Hub bridging hello traffico tooand dall'IoT Hub. È possibile utilizzare hello [gateway del protocollo Azure IoT](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md) come un adattamento di protocollo tooenable gateway personalizzato per l'IoT Hub.

## gateway del protocollo Azure IoT
gateway del protocollo Hello Azure IoT è un framework per l'adeguamento di protocollo che è destinato a scalabilità elevata, la comunicazione bidirezionale dispositivo con l'IoT Hub. gateway del protocollo Hello è un componente di tipo pass-through che accetta le connessioni ai dispositivi tramite un protocollo specifico. Colma hello traffico tooIoT Hub tramite AMQP 1.0. gateway del protocollo Hello Azure IoT è disponibile come una flessibilità di tooprovide progetti software open source per l'aggiunta del supporto per diversi protocolli e versioni del protocollo.

È possibile distribuire gateway del protocollo hello in Azure in modo estremamente scalabile con Azure Service Fabric, i ruoli di lavoro di servizi Cloud di Azure o macchine virtuali di Windows. Inoltre, il gateway di protocollo hello può essere distribuito in ambienti locali, come gateway di campo.

gateway del protocollo Hello Azure IoT include un adattatore di protocollo MQTT che permette di toocustomize hello comportamento del protocollo MQTT se necessario. Dall'IoT Hub fornisce supporto incorporato per il protocollo di hello MQTT v3.1.1, è consigliabile solo utilizzando l'adapter di protocollo MQTT hello se sono necessari le personalizzazioni di protocollo o requisiti specifici per funzionalità aggiuntive.

scheda MQTT Hello inoltre illustrato come modello di programmazione hello per la creazione di adattatori di protocollo per altri protocolli. Inoltre, hello Azure IoT protocollo gateway modello di programmazione consente specializzato tooplug nei componenti personalizzati per l'elaborazione, ad esempio l'autenticazione personalizzata, trasformazioni di messaggi, compressione/decompressione o la crittografia o decrittografia del traffico tra i dispositivi hello e IoT Hub.

Per maggiore flessibilità, il gateway di protocollo hello e implementazione MQTT sono incluse in un progetto software open source. Ciò consente l'implementazione di hello toocustomize in base alle esigenze.

## Passaggi successivi
informazioni sul gateway del protocollo hello Azure IoT toolearn e come toouse e distribuirlo come parte della soluzione IoT, vedere:

* [Archivio gateway del protocollo IoT Azure su GitHub](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md)
* [Guida per sviluppatori del gateway del protocollo IoT Azure](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/docs/DeveloperGuide.md)

toolearn ulteriori informazioni sulla pianificazione della distribuzione di IoT Hub, vedere:

* [Eseguire il confronto con Hub eventi][lnk-compare]
* [Scalabilità, disponibilità elevata e ripristino di emergenza][lnk-scaling]
* [Guida per gli sviluppatori dell'hub IoT][lnk-devguide]

[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
