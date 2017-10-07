---
title: 'Connettersi Raspberry Pi (nodo) tooAzure IoT - lezione 1: ottenere gli strumenti (macOS) | Documenti Microsoft'
description: Scaricare e installare gli strumenti necessari hello e software per l'applicazione di esempio per Pi prima hello in macOS.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: sviluppo iot, software iot, software per internet delle cose, installare python in mac, installare git in mac, esecuzione di gulp, installare node js in mac
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 2ea6d211-c0e8-4ade-ac69-d1c2261d78c4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 382b066cb7ece7ffdeb22b162b725727b22e5fac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a>Ottenere strumenti hello (macOS 10.10)
> [!div class="op_single_selector"]
> * [Windows 7 o versione successiva](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>Contenuto dell'esercitazione
Scaricare strumenti di sviluppo hello e software di hello per l'applicazione di esempio per i 3 Pi Raspberry prima hello. Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione
Contenuto dell'articolo:

* Come tooinstall Git e Node.js.
  * [Git](https://git-scm.com) è un sistema distribuito di controllo delle versioni open source. applicazione di esempio Hello per questo articolo viene archiviata in Git.
  * [Node.js](https://nodejs.org/en/) è un runtime JavaScript con un ampio ecosistema di pacchetti.
* Come toouse NPM tooinstall aggiuntive Node.js gli strumenti di sviluppo.
  * Hello versione minima richiesta di Node.js è 4.5 LTS.
  * [NPM](https://www.npmjs.com) è uno dei hello gestori di pacchetti per Node.js.

## <a name="what-you-need"></a>Elementi necessari
toocomplete questa operazione, è necessario:

* Un toodownload connessione Internet hello gli strumenti di sviluppo e hello software.
* Un computer Mac che esegue macOS Yosemite (10.10) o versione successiva.

## <a name="install-git-and-nodejs"></a>Installare Git e Node.js
tooinstall Git e Node.js, utilizzare hello [Homebrew](http://brew.sh) utilità di gestione del pacchetto attenendosi alla procedura seguente:

1. Installare Homebrew. Se è già stato installato Homebrew, è possibile passare toostep 2.
   
   1. Premere `Cmd + Space` e immettere `Terminal` tooopen un terminale.
   2. Eseguire hello comando seguente:
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. Installare Git e Node.js eseguendo hello comando seguente:
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a>Installare altri strumenti di sviluppo Node.js
Utilizzare [file gulp.js](http://gulpjs.com) distribuzione hello tooautomate di tooPi applicazione di esempio hello. Hello utilizzare [dispositivo-individuazione-cli](https://github.com/Azure/device-discovery-cli) tooretrieve informazioni di rete sui dispositivi IoT.

Installare `gulp` e `device-discovery-cli` eseguendo hello comando terminal hello seguente:

```bash
npm install -g device-discovery-cli gulp
```

Se si verificano problemi di installazione di Node.js e questi strumenti di sviluppo aggiuntive su macOS, vedere hello [risoluzione dei problemi guida](iot-hub-raspberry-pi-kit-node-troubleshooting.md) per soluzioni ai problemi di toocommon.

## <a name="install-visual-studio-code"></a>Installare Visual Studio Code
[Scaricare](https://code.visualstudio.com/docs/setup/osx) e installare Visual Studio Code. Visual Studio Code è un editor di codice sorgente leggero, ma potente per Windows, Linux e macOS. Utilizzare questo editor in un secondo momento nel codice di esempio di hello tooedit esercitazione hello.

## <a name="summary"></a>Riepilogo
È stato installato Strumenti di sviluppo hello necessarie e software per la prima applicazione di esempio hello. attività successiva Hello è toocreate, distribuire ed eseguire l'applicazione di esempio hello in Pi.

## <a name="next-steps"></a>Passaggi successivi
[Creare e distribuire l'applicazione di esempio hello blink](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

