---
title: 'Connettersi Edison Intel (nodo) tooAzure IoT - lezione 4: ricezione messaggi | Documenti Microsoft'
description: "Un'applicazione di esempio viene eseguita in Edison e monitora i messaggi in ingresso dall'hub IoT. Una nuova attività gulp invia messaggi tooEdison da hello di tooblink l'hub IoT LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: led di controllo arduino dal web, led di controllo arduino tramite web
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: bc738bf6-e38d-4024-82d7-39b6c2d4bacb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: aab0ced4810dd3d4f5ba636940b06563f1db9241
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a>Eseguire un tooreceive di applicazione di esempio i messaggi da cloud a dispositivo
Questo articolo illustra come distribuire un'applicazione di esempio in Intel Edison. applicazione di esempio Hello controlla i messaggi in ingresso dall'hub IoT. Inoltre si esegue un'attività gulp su tooEdison di messaggi toosend il computer dall'hub IoT. Quando l'applicazione di esempio hello riceve messaggi hello, lampeggia hello LED. Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina][troubleshooting].

## <a name="what-you-will-do"></a>Contenuto dell'esercitazione
* Connettere l'hub IoT hello esempio applicazione tooyour.
* Distribuire ed eseguire l'applicazione di esempio hello.
* Invio di messaggi dal hello di IoT hub tooEdison tooblink LED.

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione
Contenuto dell'articolo:
* La modalità in ingresso toomonitor dei messaggi dall'hub IoT.
* La modalità toosend cloud a dispositivo dei messaggi dal tooEdison hub IoT.

## <a name="what-you-need"></a>Elementi necessari
* Intel Edison, impostato per l'uso. toolearn tooset backup Edison, vedere [configurare il dispositivo][configure-your-device].
* Un hub IoT creato nella propria sottoscrizione di Azure. toolearn come toocreate l'hub IoT, vedere [creare l'IoT Hub Azure][create-your-azure-iot-hub].

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a>Collegare hello esempio applicazione tooyour IoT hub
1. Assicurarsi che si è nella cartella repository hello `iot-hub-node-edison-getting-started`. Aprire l'applicazione di esempio hello in Visual Studio Code eseguendo hello seguenti comandi:

   ```bash
   cd Lesson4
   code .
   ```

   file Hello in hello `app` sottocartella è hello i file di origine della chiave che contiene i messaggi in ingresso hello codice toomonitor dall'hub IoT hello. Hello `blinkLED` funzione lampeggia hello LED.

   ![Struttura repository nell'applicazione di esempio hello][repo-structure]
2. Inizializzare i file di configurazione hello eseguendo hello seguenti comandi:

   ```bash
   npm install
   gulp init
   ```

   Se è stato completato i passaggi di hello in [creare un account di archiviazione e l'app Azure funzione] [ create-an-azure-function-app-and-storage-account] su questo computer, tutte le configurazioni di hello vengono ereditate, pertanto è possibile ignorare hello passaggio toohello attività di distribuzione e in esecuzione l'applicazione di esempio hello. Se è stato completato i passaggi di hello in [creare un account di archiviazione e l'app Azure funzione] [ create-an-azure-function-app-and-storage-account] in un computer diverso, è necessario segnaposto hello tooreplace hello `config-edison.json` file. Hello `config-edison.json` file si trova nella sottocartella hello della cartella principale.

   ![Contenuto del file di configurazione edison.json hello](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * Sostituire **[nome host di dispositivo o indirizzo IP]** con indirizzo IP del dispositivo hello è contrassegnato come inattivo quando è stato configurato il dispositivo.
   * Sostituire **[stringa di connessione dispositivo IoT]** con stringa di connessione hello dispositivo che si ottiene eseguendo hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` comando.
   * Sostituire **[stringa di connessione hub IoT]** con stringa di connessione hub IoT che si ottiene eseguendo hello hello `az iot hub show-connection-string --name {my hub name}` comando.

## <a name="deploy-and-run-hello-sample-application"></a>Distribuire ed eseguire l'applicazione di esempio hello
Distribuire ed eseguire l'applicazione di esempio hello Edison eseguendo hello seguenti comandi:

```bash
gulp deploy && gulp run
```

comando gulp Hello distribuisce tooEdison applicazione di esempio hello. Quindi, viene eseguita un'applicazione hello Edison e un'attività separata nell'host computer toosend 20 blink messaggi tooEdison dall'hub IoT.

Quando si esegue l'applicazione di esempio hello, avvia l'ascolto toomessages dall'hub IoT. Nel frattempo, attività gulp hello invia messaggi di "blink" diversi dai tooEdison hub IoT. Per ogni messaggio blink Edison riceve, applicazione di esempio hello chiama hello `blinkLED` hello tooblink funzione LED.

Dovrebbe essere blink LED hello ogni due secondi come hello gulp attività inviati 20 messaggi dal tooEdison hub IoT. Hello ultimo uno è un messaggio "stop" che interrompe l'esecuzione di un'applicazione hello.

![Applicazione di esempio con comando gulp e messaggi di lampeggiamento][gulp-command-and-blink-messages]

## <a name="summary"></a>Riepilogo
I messaggi inviati correttamente dal hello di IoT hub tooEdison tooblink LED. attività successiva Hello è facoltativo: modificare hello e disattivare il comportamento di hello LED.

## <a name="next-steps"></a>Passaggi successivi
[Modificare hello e disattivare il comportamento di hello LED][change-the-on-and-off-behavior-of-the-led]

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-node-lesson4-change-led-behavior.md