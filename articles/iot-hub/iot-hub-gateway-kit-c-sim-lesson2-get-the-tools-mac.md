---
title: 'Dispositivo simulato e gateway Azure IoT: lezione 2: Ottenere gli strumenti (macOS) | Documentazione Microsoft'
description: Installare gli strumenti nel computer Mac, creare un hub IoT e registrare il dispositivo nell'hub IoT hello.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: sviluppo iot, software iot, servizio cloud iot, software per internet delle cose, interfaccia della riga di comando di azure, installare python in mac, installare git in mac, esecuzione di gulp, installare node js in mac
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 42f9d186-e20c-4ef9-98cc-71d39e058b06
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 391d60f3cbb209698cae53098efed360ac0f5fad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos"></a>Ottenere strumenti hello (macOS)
> [!div class="op_single_selector"]
> * [Windows 7 o versione successiva](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>Contenuto dell'esercitazione

- Installare Git, Node.js, Gulp e Python.
- Installare hello Azure interfaccia della riga di comando (CLI di Azure). 

Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione

In questa lezione si apprenderà:

- Come tooinstall [Git](https://git-scm.com/) e [Node.js](https://nodejs.org/en/).
  - Git è un sistema distribuito open source di controllo delle versioni. applicazione di esempio Hello per questa lezione viene archiviata in Git.
  - Node.js è un runtime JavaScript con un ampio ecosistema di pacchetti.
- Come toouse [NPM](https://www.npmjs.com/) tooinstall Node.js gli strumenti di sviluppo.
  - Hello versione minima richiesta di Node.js è 4.5 LTS.
  - NPM è uno dei gestori di pacchetti hello per Node.js.
- Come tooinstall Visual Studio Code.
  - Visual Studio Code è un editor di codice sorgente multipiattaforma leggero ma potente per Windows, Linux e macOS. Dispone di un elevato supporto per funzionalità quali debug, controllo Git incorporato, evidenziazione della sintassi, completamento intelligente del codice, frammenti di codice e refactoring del codice.
- Come tooinstall Python.
  - Python è un linguaggio di programmazione dinamico, interpretato, generico e di alto livello molto diffuso.
- Come tooinstall hello CLI di Azure.
  - Hello CLI di Azure fornisce un'esperienza della riga di comando multipiattaforma di Azure. Si lavora direttamente da una riga di comando di tooprovision e gestire le risorse.
- Come un hub IoT toouse hello toocreate CLI di Azure.

## <a name="what-you-need"></a>Elementi necessari

- Un toodownload connessione Internet hello strumenti e software.
- Un computer Mac che esegue OS X Yosemite (10.10) o versione successiva.

## <a name="install-git-and-nodejs"></a>Installare Git e Node.js

tooinstall Git e Node.js, utilizzare l'utilità di gestione dei pacchetti Homebrew hello attenendosi alla procedura seguente:

1. [Scaricare](http://brew.sh/) e installare Homebrew. Se è già stato installato Homebrew, è possibile passare toostep 2.
   1. Premere `Cmd + Space` e immettere `Terminal` tooopen un terminale.
   2. Eseguire hello comando seguente:

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```

2. Installare Git e Node.js eseguendo hello comando seguente:

    ```bash
    brew install node git
    ```

## <a name="install-nodejs-development-tools"></a>Installare gli strumenti di sviluppo Node.js

Utilizzare [file gulp.js](http://gulpjs.com/) tooautomate distribuzione ed esecuzione di script.

gulp tooinstall, eseguire hello comando terminal hello seguente:

```bash
npm install -g gulp
```

Se si verificano problemi relativi all'installazione di hello, vedere hello [risoluzione dei problemi guida](iot-hub-gateway-kit-c-sim-troubleshooting.md) per soluzioni ai problemi di toocommon.

> [!Note]
> Nodo, NPM e Gulp sono gli script di automazione di richiesto toorun sviluppati in Node.js.

## <a name="install-python"></a>Installare Python

Sebbene Mac OS X venga fornito con Python 2.7, si consiglia di installare Python tramite Homebrew. Vedere [Installazione di Python in Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).

Installare Python e pip eseguendo hello comando seguente:

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a>Installare hello CLI di Azure

hello tooinstall CLI di Azure, seguire questi passaggi:

1. Eseguire i seguenti comandi in terminal hello hello:
   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
   installazione di Hello potrebbe richiedere 5 minuti.

2. Verificare l'installazione di hello eseguendo hello comando seguente:
   ```bash
   az iot -h
   ```
   Verrà visualizzato l'output seguente hello se installazione hello ha esito positivo.

   ![Verificare l'installazione dell'interfaccia della riga di comando di Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_osx.png)

## <a name="install-visual-studio-code"></a>Installare Visual Studio Code

Utilizzare Visual Studio Code in un secondo momento nei file di configurazione di hello tooedit dell'esercitazione.

[Scaricare](https://code.visualstudio.com/docs/setup/osx) e installare Visual Studio Code.

## <a name="summary"></a>Riepilogo

Aver installato tutti gli strumenti necessario hello e software nel computer Mac. L'attività successiva è toouse hello Azure CLI toocreate un hub IoT e registrare il dispositivo nell'hub IoT.

## <a name="next-steps"></a>Passaggi successivi
[Creare un hub IoT e registrare il dispositivo](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
