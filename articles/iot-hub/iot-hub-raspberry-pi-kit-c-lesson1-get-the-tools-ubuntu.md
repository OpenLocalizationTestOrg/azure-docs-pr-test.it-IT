---
title: 'Connettere Raspberry Pi (C) ad Azure IoT: lezione 1: Ottenere gli strumenti (Ubuntu) | Documentazione Microsoft'
description: Scaricare e installare il software e gli strumenti necessari per la prima applicazione di esempio per Pi in Ubuntu.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: sviluppo iot, software iot, software per internet delle cose, installare git in ubuntu, esecuzione di gulp, installare node js in ubuntu
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 32cfea00-c254-4cef-8f6f-bbf807eca6b6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 28ebba82e90d91470518cd830c96e6da39d8b9b4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a>Ottenere gli strumenti (Ubuntu 16.04)

> [!div class="op_single_selector"]
> * [Windows 7 o versione successiva](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>Contenuto dell'esercitazione
Scaricare gli strumenti di sviluppo e il software per la prima applicazione di esempio per Raspberry Pi 3. In caso di problemi, cercare le soluzioni nella pagina sulla [risoluzione dei problemi](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

> [!NOTE]
> Anche se il linguaggio di programmazione della logica principale è C, le lezioni fanno uso di strumenti Node.js per individuare i dispositivi e compilare e distribuire applicazioni di esempio.

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione
Contenuto dell'articolo:

* Come installare Git e Node.js
  * [Git](https://git-scm.com) è un sistema distribuito di controllo delle versioni open source. L'applicazione di esempio per questo articolo è archiviata in Git.
  * [Node.js](https://nodejs.org/en/) è un runtime JavaScript con un ampio ecosistema di pacchetti.
* Come usare NPM per installare altri strumenti di sviluppo Node.js.
  * La versione minima richiesta di Node.js è 4.5 LTS.
  * [NPM](https://www.npmjs.com) è uno degli strumenti di gestione pacchetti per Node.js.

## <a name="what-you-need"></a>Elementi necessari
Per completare questa operazione saranno necessari:

* Una connessione Internet per scaricare gli strumenti di sviluppo e il software.
* Un computer che esegue Ubuntu 16.04 o versione successiva.

## <a name="install-git-nodejs-and-npm"></a>Installare Git, Node.js e NPM
Usare la scelta rapida da tastiera `Ctrl + Alt + T` per aprire un terminale ed eseguire questi comandi:

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a>Installare altri strumenti di sviluppo Node.js
Usare [gulp.js](http://gulpjs.com) per automatizzare la distribuzione dell'applicazione di esempio in Pi. Usare [device-discovery-cli](https://github.com/Azure/device-discovery-cli) per recuperare informazioni di rete sui dispositivi IoT.

Installare `gulp` e `device-discovery-cli` eseguendo questo comando nel terminale:

```bash
sudo npm install -g device-discovery-cli gulp
```

Se si verificano problemi durante l'installazione in Ubuntu di Node.js e di questi strumenti di sviluppo aggiuntivi, vedere la [guida alla risoluzione dei problemi](iot-hub-raspberry-pi-kit-c-troubleshooting.md) per le soluzioni alle problematiche comuni.

## <a name="install-visual-studio-code"></a>Installare Visual Studio Code
[Scaricare](https://code.visualstudio.com/docs/setup/linux) e installare Visual Studio Code. Visual Studio Code è un editor di codice sorgente leggero, ma potente per Windows, Linux e macOS. Più avanti nell'esercitazione si userà questo editor per modificare il codice di esempio.

## <a name="summary"></a>Riepilogo
Sono stati installati gli strumenti di sviluppo e il software necessari per la prima applicazione di esempio. L'attività successiva consiste nella creazione, distribuzione ed esecuzione dell'applicazione di esempio nel dispositivo Pi.

## <a name="next-steps"></a>Passaggi successivi
[Creare e distribuire l'applicazione per il lampeggiamento](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

