---
title: 'Connettersi Arduino tooAzure IoT - lezione 1: ottenere gli strumenti (Windows) | Documenti Microsoft'
description: Scaricare e installare gli strumenti necessari hello e software per l'applicazione di esempio per Adafruit sfumatura M0 WiFi prima hello in Windows 7 e versioni successive.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: strumenti di sviluppo arduino, sviluppo iot, software iot, software per internet delle cose, installare git in windows, installare node js in windows
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 9cfb8cd2-eafb-4ba2-b23e-d94e114ff3a6
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4dd946da6c84293987e166fd1d17fac117e94e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a>Ottenere strumenti hello (Windows 7 o versioni successive)

> [!div class="op_single_selector"]
> * [Windows 7 o versione successiva][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a>Contenuto dell'esercitazione

Scaricare strumenti di sviluppo hello e software di hello per l'applicazione di esempio per la scheda Adafruit sfumatura M0 Wi-Fi Arduino prima hello.

Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina][troubleshooting].

> [!NOTE]
> Sebbene hello programming language della logica principale hello Arduino, Node.js tools vengono utilizzati in toobuild lezioni hello e distribuire applicazioni di esempio.

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione
Contenuto dell'articolo:

* Come tooinstall Git e Node.js.
  * [Git](https://git-scm.com) è un sistema distribuito di controllo delle versioni open source. applicazione di esempio Hello per questo articolo viene archiviata in Git.
  * [Node.js](https://nodejs.org/en/) è un runtime JavaScript con un ampio ecosistema di pacchetti.
* Come toouse NPM tooinstall aggiuntive Node.js gli strumenti di sviluppo.
  * requisito di versione minima di Hello di Node.js è 4.5 LTS.
  * [NPM](https://www.npmjs.com) è uno dei hello gestori di pacchetti per Node.js.

## <a name="what-you-need"></a>Elementi necessari

toocomplete questa operazione, è necessario:

* Un toodownload connessione Internet hello gli strumenti di sviluppo e hello software.
* Un computer che esegue Windows.

## <a name="install-git-and-nodejs"></a>Installare Git e Node.js

Fare clic sui collegamenti hello sotto toodownload e installare Git e LTS Node.js per Windows.

* [Ottenere Git per Windows](https://git-scm.com/download/win/)
* [Ottenere Node.js LTS per Windows](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a>Installare altri strumenti di sviluppo Node.js

Utilizzare [file gulp.js](http://gulpjs.com) distribuzione hello tooautomate di tooyour di applicazione di esempio hello Arduino Lavagna.

Avviare il prompt dei comandi come amministratore. Installare `gulp`, `device-discovery-cli` eseguendo hello comando terminal hello seguente:

```bash
npm install -g gulp device-discovery-cli
```

Se si verificano problemi di installazione di Node.js e questi strumenti di sviluppo Node.js aggiuntivi nel computer in uso, vedere hello [risoluzione dei problemi guida] [ troubleshooting] per soluzioni ai problemi di toocommon.

## <a name="install-visual-studio-code"></a>Installare Visual Studio Code

[Scaricare](https://code.visualstudio.com/docs/setup/windows) e installare Visual Studio Code. Visual Studio Code è un editor di codice sorgente leggero, ma potente per Windows, Linux e macOS. Utilizzare questo editor in un secondo momento nel codice di esempio di hello tooedit esercitazione hello.

## <a name="summary"></a>Riepilogo

È stato installato Strumenti di sviluppo hello necessarie e software per la prima applicazione di esempio hello. attività successiva Hello è toocreate, distribuire ed eseguire l'applicazione di esempio hello sulla Lavagna Arduino.

## <a name="next-steps"></a>Passaggi successivi

[Creare e distribuire l'applicazione di esempio hello blink][create-and-deploy-the-blink-sample-application]
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-mac.md
[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[create-and-deploy-the-blink-sample-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md