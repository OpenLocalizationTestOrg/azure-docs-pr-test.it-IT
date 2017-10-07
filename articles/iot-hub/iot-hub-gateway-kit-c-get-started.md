---
title: 'Dispositivo SensorTag e gateway Azure IoT: introduzione | Documentazione Microsoft'
description: Introduzione a IoT Gateway Starter Kit, creare l'hub IoT di Azure e connettersi SensorTag Gateway toohello IoT hub
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure iot hub iot gateway, Guida introduttiva a hello internet delle cose, iot toolkit
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 56d05f4e-f2c1-4b22-8701-f01e14deead6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d8e4057e7774e43c069dd3f2f2e03f098c1ac844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-sensortag"></a>Introduzione allo starter kit del gateway IoT di Azure con un dispositivo SensorTag

> [!div class="op_single_selector"]
> * [SensorTag](iot-hub-gateway-kit-c-get-started.md)
> * [Dispositivo simulato](iot-hub-gateway-kit-c-sim-get-started.md)

In questa esercitazione, è necessario innanzitutto apprendimento hello nozioni fondamentali sulle operazioni con [IoT Gateway Starter Kit](https://aka.ms/gateway-kit). Si utilizzeranno con NUC Intel che esegue Linux distretto vento e hello [SensorTag TI](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main). Si apprenderà come tooseamleesly connettersi cloud toohello di dispositivi con Azure IoT Hub.

***
**Non si dispone ancora di un kit?** Fare clic [qui](https://aka.ms/gateway-kit). **Non si dispone di un SensorTag?** [Iniziare con un dispositivo simulato](iot-hub-gateway-kit-c-sim-get-started.md) o [acquistare un SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)
***

## <a name="lesson-1-configure-your-nuc"></a>Lezione 1. Configurare il dispositivo NUC
![Diagramma di flusso della lezione 1](media/iot-hub-gateway-kit-lessons/e2e-lesson1.png)

In questa lezione, è possibile impostare NUC Intel (successivo unità di elaborazione) in hello Kit come gateway IoT di Azure, installare il pacchetto di Azure IoT Edge hello in NUC ed eseguire una funzionalità di gateway hello tooverify app di esempio.

*Toocomplete tempo stimato: 15 minuti*

Andare troppo[impostare NUC Intel come gateway IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)

## <a name="lesson-2-create-your-iot-hub"></a>Lezione 2. Creare l'hub IoT
![Diagramma di flusso della lezione 2](media/iot-hub-gateway-kit-lessons/e2e-lesson2.png)

In questa lezione, si installa strumenti hello e software nel computer host. Quindi creare l'account gratuito di Azure, eseguire il provisioning dell'hub IoT di Azure e creare il primo dispositivo nell'hub IoT hello.

Prima di iniziare questa lezione, completare la lezione 1.

### <a name="get-hello-tools"></a>Ottenere strumenti hello
Installare strumenti di hello e software nel computer host.

*Toocomplete tempo stimato: 20 minuti*

Andare troppo[strumenti hello](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)

### <a name="create-an-iot-hub-and-register-your-device"></a>Creare un hub IoT ed effettuare la registrazione del dispositivo
Creare il gruppo di risorse, l'hub IoT Azure prima di eseguire il provisioning e aggiungere primo dispositivo toohello IoT hub utilizzando hello CLI di Azure.

*Toocomplete tempo stimato: 10 minuti*

Andare troppo[creare un hub IoT e registrare il dispositivo](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="lesson-3-receive-messages-from-sensortag-and-read-messages-from-your-iot-hub"></a>Lezione 3. Ricevere messaggi da SensorTag e leggere messaggi dall'hub IoT
In questa lezione si utilizzerà script tooautomate hello configurazione ed esecuzione di un'applicazione di esempio BILITA nel gateway. Tali applicazioni utilizzano un insieme di moduli tooaggregate e trasformare i dati, elaborare i comandi o eseguono un numero qualsiasi di attività correlate. I moduli comunicano tra loro tramite un broker messaggi. applicazione di esempio Hello dispone di un modulo di tabella e un modulo di hub IoT. modulo BILITA Hello riceve dati da SensorTag attiva. Hello pacchetti ricevuti dati hello e lo invia hub IoT tooyour tramite il framework di gateway hello fornito in Azure IoT Edge di IoT hub modulo.

![Diagramma di flusso della lezione 3](media/iot-hub-gateway-kit-lessons/e2e-lesson3.png)

### <a name="configure-and-run-hello-ble-sample-app"></a>Configurare ed eseguire app di esempio BILITA hello
Configurare la connettività di hello tra SensorTag e il gateway. Quindi completare la configurazione di hello ed eseguire l'applicazione di esempio BILITA hello.

*Toocomplete tempo stimato: 15 minuti*

Andare troppo[configurare ed eseguire hello Disattiva app di esempio](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)

### <a name="read-messages-from-your-iot-hub"></a>Leggere messaggi dall'hub IoT
Eseguire il codice di esempio nell'host computer tooread messaggi dall'hub IoT.

*Toocomplete tempo stimato: 15 minuti*

Andare troppo[leggere messaggi dall'hub IoT](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)

## <a name="lesson-4-save-messages-tooazure-table-storage"></a>Lezione 4: Salvare i messaggi di archiviazione tabelle tooAzure
Creare un'app di Azure di funzione che ottiene i messaggi in arrivo dall'hub IoT e li scrive archiviazione tabella tooAzure.

![Diagramma di flusso della lezione 4](media/iot-hub-gateway-kit-lessons/e2e-lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a>Creare un'app per le funzioni di Azure e un account di archiviazione di Azure
Un'app di Azure (funzione) e un account di archiviazione di Azure, utilizzare un toocreate modello di gestione risorse di Azure.

*Toocomplete tempo stimato: 10 minuti*

Andare troppo[creare un account di archiviazione di Azure e l'app di Azure (funzione)](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)

### <a name="read-messages-persisted-in-azure-table-storage"></a>Leggere i messaggi persistenti nell'archiviazione tabelle di Azure
Monitorare i messaggi hello gateway-to-cloud quando vengono scritti nel servizio di archiviazione tabelle tooAzure.

*Toocomplete tempo stimato: 5 minuti*

Andare troppo[leggere messaggi persistenti nell'archiviazione tabelle Azure](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).

## <a name="troubleshooting"></a>Risoluzione dei problemi
Se si verificano problemi durante lezioni hello, cercare soluzioni in hello [Troubleshooting](iot-hub-gateway-kit-c-troubleshooting.md) articolo.

## <a name="explore-more"></a>Scopri di più
Visitare hello [zona di Intel IoT Gateway Kit per sviluppatori](http://software.intel.com/iot/microsoft-azure) toolearn altre.
