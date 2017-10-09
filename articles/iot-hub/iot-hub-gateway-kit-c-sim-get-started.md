---
title: 'Dispositivo simulato e gateway Azure IoT: introduzione | Documentazione Microsoft'
description: Introduzione a IoT Gateway Starter Kit, creare l'hub IoT di Azure e collegare Gateway toohello IoT hub
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure iot hub iot gateway, Guida introduttiva a hello internet delle cose, iot toolkit
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0c110b8b-bee4-4aec-a18a-dfc292aa17a3
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1a54a5e5f1c1d9b2e657c9e4448274256e2533f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-simulated-device"></a>Introduzione allo starter kit per il gateway IoT con un dispositivo simulato

> [!div class="op_single_selector"]
> * [SensorTag](iot-hub-gateway-kit-c-get-started.md)
> * [Dispositivo simulato](iot-hub-gateway-kit-c-sim-get-started.md)

In questa esercitazione, è necessario innanzitutto apprendimento hello nozioni fondamentali sulle operazioni con [IoT Gateway Starter Kit](https://aka.ms/gateway-kit). Si userà Intel NUC che esegue Wind River Linux. Si apprenderà come tooseamleesly connettersi cloud toohello di dispositivi con Azure IoT Hub.

***
**Non si dispone ancora di un kit?** Fare clic [qui](https://aka.ms/gateway-kit).
***

## <a name="lesson-1-configure-your-nuc"></a>Lezione 1: Configurare NUC
![Diagramma di flusso della lezione 1](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson1.png)

In questa lezione, è possibile impostare NUC Intel (successivo unità di elaborazione) in hello Kit come gateway IoT di Azure, installare il pacchetto di Azure IoT Edge hello in NUC ed eseguire una funzionalità di gateway hello tooverify app di esempio.

*Toocomplete tempo stimato: 15 minuti*

Andare troppo[impostare NUC Intel come gateway IoT](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)

## <a name="lesson-2-create-your-iot-hub"></a>Lezione 2. Creare l'hub IoT
![Diagramma di flusso della lezione 2](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson2.png)

In questa lezione, si installa strumenti hello e software nel computer host. Quindi creare l'account gratuito di Azure, eseguire il provisioning dell'hub IoT di Azure e creare il primo dispositivo nell'hub IoT hello.

Prima di iniziare questa lezione, completare la lezione 1.

### <a name="get-hello-tools"></a>Ottenere strumenti hello
Installare strumenti di hello e software nel computer host.

*Toocomplete tempo stimato: 20 minuti*

Andare troppo[strumenti hello](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)

### <a name="create-an-iot-hub-and-register-your-device"></a>Creare un hub IoT ed effettuare la registrazione del dispositivo
Creare il gruppo di risorse, l'hub IoT Azure prima di eseguire il provisioning e aggiungere primo dispositivo toohello IoT hub utilizzando hello CLI di Azure.

*Toocomplete tempo stimato: 10 minuti*

Andare troppo[creare un hub IoT e registrare il dispositivo](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="lesson-3-receive-messages-from-hello-simulated-device-and-read-messages-from-your-iot-hub"></a>Lezione 3: Ricevere messaggi da dispositivo simulato hello e leggere messaggi dall'hub IoT
In questa lezione si utilizzerà script tooautomate hello configurazione ed esecuzione di un'app dispositivo simulato nel gateway. Genera dati di esempio temperatura app dispositivo simulato Hello e lo invia tooan modulo di hub IoT. Hello pacchetti ricevuti dati hello e lo invia hub IoT tooyour tramite il framework di gateway hello fornito in Azure IoT Edge di IoT hub modulo.

![Diagramma di flusso della lezione 3](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson3.png)

### <a name="configure-and-run-a-simulated-device"></a>Configurare ed eseguire un dispositivo simulato
Preparare i codici di esempio hello. Quindi Configura ed Esegui applicazione di esempio dispositivo simulato hello.

*Toocomplete tempo stimato: 15 minuti*

Andare troppo[configurare ed eseguire un dispositivo simulato](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)

### <a name="read-messages-from-your-iot-hub"></a>Leggere messaggi dall'hub IoT
Eseguire un codice di esempio nei messaggi di hello tooread computer host dall'hub IoT.

*Toocomplete tempo stimato: 15 minuti*

Andare troppo[leggere messaggi dall'hub IoT](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)

## <a name="lesson-4-save-messages-tooazure-table-storage"></a>Lezione 4: Salvare i messaggi di archiviazione tabelle tooAzure
Creare un'app di Azure di funzione che ottiene i messaggi in arrivo dall'hub IoT e li scrive archiviazione tabella tooAzure.

![Diagramma di flusso della lezione 4](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a>Creare un'app per le funzioni di Azure e un account di archiviazione di Azure
Un'app di Azure (funzione) e un account di archiviazione di Azure, utilizzare un toocreate modello di gestione risorse di Azure.

*Toocomplete tempo stimato: 10 minuti*

Andare troppo[creare un account di archiviazione di Azure e l'app di Azure (funzione)](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)

### <a name="read-messages-persisted-in-azure-table-storage"></a>Leggere i messaggi persistenti nell'archiviazione tabelle di Azure
Monitorare i messaggi hello gateway-to-cloud quando vengono scritti nel servizio di archiviazione tabelle tooAzure.

*Toocomplete tempo stimato: 5 minuti*

Andare troppo[leggere messaggi persistenti nell'archiviazione tabelle Azure](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).

## <a name="troubleshooting"></a>Risoluzione dei problemi
Se si verificano problemi durante lezioni hello, cercare soluzioni in hello [Troubleshooting](iot-hub-gateway-kit-c-sim-troubleshooting.md) articolo.

## <a name="explore-more"></a>Scopri di più
Visitare hello [zona di Intel IoT Gateway Kit per sviluppatori](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) toolearn altre.
