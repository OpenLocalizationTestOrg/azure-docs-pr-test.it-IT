---
featureFlags: usabilla
title: 'Connettersi Raspberry Pi (nodo) tooAzure IoT - lezione 4: Cloud a dispositivo | Documenti Microsoft'
description: "applicazione di esempio Hello viene eseguita l'installazione guidata piattaforma e controlla i messaggi in ingresso dall'hub IoT. Una nuova attività gulp invia messaggi tooPi da hello di tooblink l'hub IoT LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: cloud toodevice, messaggio dal cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6ae6539e-1163-4490-8d72-fdf7803e3054
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d69ded4e30c27378481ab2a4fb9c5b73be7bd44e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-sample-application-tooreceive-cloud-to-device-messages"></a>Eseguire i messaggi hello esempio applicazione tooreceive cloud a dispositivo
Questo articolo illustra come distribuire un'applicazione di esempio nel dispositivo Raspberry Pi 3. applicazione di esempio Hello controlla i messaggi in ingresso dall'hub IoT. Inoltre si esegue un'attività gulp su tooPi di messaggi toosend il computer dall'hub IoT. Quando l'applicazione di esempio hello riceve messaggi hello, lampeggia hello LED. Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-do"></a>Contenuto dell'esercitazione
* Connettere l'hub IoT hello esempio applicazione tooyour.
* Distribuire ed eseguire l'applicazione di esempio hello.
* Invio di messaggi dal hello di IoT hub tooPi tooblink LED.

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione
Contenuto dell'articolo:
* Come i messaggi in ingresso toomonitor dall'hub IoT
* La modalità toosend cloud a dispositivo dei messaggi dal tooPi hub IoT.

## <a name="what-you-need"></a>Elementi necessari
* Raspberry Pi 3, impostato per l'uso. toolearn tooset di pi greco, vedere [configurare il dispositivo](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md).
* Un hub IoT creato nella propria sottoscrizione di Azure. toolearn come toocreate l'hub IoT, vedere [creare l'hub IoT e registrare Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a>Collegare hello esempio applicazione tooyour IoT hub
1. Assicurarsi che si è nella cartella repository hello `iot-hub-node-raspberrypi-getting-started`. Aprire l'applicazione di esempio hello in Visual Studio Code eseguendo hello seguenti comandi:
   
   ```bash
   cd Lesson4
   code .
   ```
   
   Hello preavviso `app.js` file hello `app` sottocartella. Hello `app.js` è hello i file di origine della chiave che contiene i messaggi in ingresso hello codice toomonitor dall'hub IoT hello. Hello `blinkLED` funzione lampeggia hello LED.
   
   ![Struttura repository nell'applicazione di esempio hello](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure.png)
2. Inizializzare i file di configurazione hello usando hello seguenti comandi:
   
   ```bash
   npm install
   gulp init
   ```
   
   Se è stato completato i passaggi di hello in [creare un account di archiviazione e l'app Azure funzione](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) su questo computer, tutte le configurazioni di hello vengono ereditate, pertanto è possibile ignorare toohello attività di distribuzione e l'esecuzione dell'applicazione di esempio hello. Se è stato completato i passaggi di hello in [creare un account di archiviazione e l'app Azure funzione](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) in un computer diverso, è necessario segnaposto hello tooreplace hello `config-raspberrypi.json` file. Hello `config-raspberrypi.json` file si trova nella sottocartella hello della cartella principale.
   
   ![Contenuto del file di configurazione raspberrypi.json hello](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* Sostituire **[nome host di dispositivo o indirizzo IP]** con indirizzo IP hello hello o al nome host che si ottiene eseguendo hello `devdisco list --eth` comando.
* Sostituire **[stringa di connessione dispositivo IoT]** con stringa di connessione hello dispositivo che si ottiene eseguendo hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` comando.
* Sostituire **[stringa di connessione hub IoT]** con stringa di connessione hub IoT che si ottiene eseguendo hello hello `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` comando.

> [!NOTE]
> Se non è stato fatto nella lezione 1, eseguire anche il comando **gulp install-tools**.

## <a name="deploy-and-run-hello-sample-application"></a>Distribuire ed eseguire l'applicazione di esempio hello
Distribuire ed eseguire l'applicazione di esempio hello Pi eseguendo hello comando seguente:

```bash
gulp deploy && gulp run
```

comando Hello distribuisce tooPi applicazione di esempio hello. Quindi, viene eseguita un'applicazione hello Pi e un'attività separata nell'host computer toosend 20 blink messaggi tooPi dall'hub IoT.

Quando si esegue l'applicazione di esempio hello, avvia l'ascolto toomessages dall'hub IoT. Nel frattempo, attività gulp hello invia messaggi di "blink" diversi dai tooPi hub IoT. Per ogni messaggio blink che riceve Pi, l'applicazione di esempio hello chiama hello `blinkLED` hello tooblink funzione LED.

Dovrebbe essere blink LED hello ogni due secondi come hello gulp attività inviati 20 messaggi dal tooPi hub IoT. Hello ultimo uno è un messaggio "stop" che indica toostop applicazione hello in esecuzione.

![Applicazione di esempio con comando gulp e messaggi di lampeggiamento](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink.png)

## <a name="summary"></a>Riepilogo
I messaggi inviati correttamente dal hello di IoT hub tooPi tooblink LED. attività successiva Hello è facoltativo: modificare hello e disattivare il comportamento di hello LED.

## <a name="next-steps"></a>Passaggi successivi
[Modificare hello e disattivare il comportamento di hello LED](iot-hub-raspberry-pi-kit-node-lesson4-change-led-behavior.md)

