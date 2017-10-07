---
title: 'Dispositivo SensorTag e gateway Azure IoT: lezione 2: Ottenere gli strumenti (Ubuntu) | Documentazione Microsoft'
description: Installare strumenti di hello e software hello nel computer host che eseguono Ubuntu, creare un hub IoT e registrare il dispositivo nell'hub IoT hello.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: sviluppo iot, software iot, servizio cloud iot, software per internet delle cose, interfaccia della riga di comando di azure, installare git in ubuntu, esecuzione di gulp, installare node js in ubuntu
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0bac1412-385b-4255-a33f-9d44c35feb3e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c9edca91e791ef914b1920178b66eadd12ae0281
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a>Ottenere strumenti hello (Ubuntu 16.04)
> [!div class="op_single_selector"]
> * [Windows 7 o versione successiva](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>Contenuto dell'esercitazione

- Installare Git, Node.js, Gulp e Python.
- Installare hello Azure interfaccia della riga di comando (CLI di Azure). 

Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-gateway-kit-c-troubleshooting.md).
## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione

In questa lezione si apprenderà:

- Come tooinstall Git e Node.js.
  - Git è un sistema distribuito open source di controllo delle versioni. applicazione di esempio Hello per questa lezione viene archiviata in Git.
  - Node.js è un runtime JavaScript con un ampio ecosistema di pacchetti.
- Come gli strumenti di sviluppo toouse NPM tooinstall Node.js.
  - Hello versione minima richiesta di Node.js è 4.5 LTS.
  - NPM è uno dei gestori di pacchetti hello per Node.js.
- Come tooinstall Visual Studio Code.
  - Visual Studio Code è un editor di codice sorgente multipiattaforma leggero ma potente per Windows, Linux e macOS. Dispone di un elevato supporto per funzionalità quali debug, controllo Git incorporato, evidenziazione della sintassi, completamento intelligente del codice, frammenti di codice e refactoring del codice.
- Come tooinstall hello CLI di Azure
  - Hello CLI di Azure fornisce un'esperienza della riga di comando multipiattaforma di Azure. Si lavora direttamente da una riga di comando di tooprovision e gestire le risorse.
- Come un hub IoT toouse hello toocreate CLI di Azure.

## <a name="what-you-need"></a>Elementi necessari

- Un toodownload connessione Internet hello strumenti e software.
- Un computer che esegue Ubuntu 16.04 o versione successiva.

## <a name="install-git-and-nodejs"></a>Installare Git e Node.js

tooinstall Git e Node.js, seguire questi passaggi:

1. Premere `Ctrl + Alt + T` tooopen un terminale.
2. Eseguire hello seguenti comandi:

   ```bash
   sudo apt-get update
   curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
   sudo apt-get install -y nodejs
   sudo apt-get install git
   ```

## <a name="install-nodejs-development-tools"></a>Installare gli strumenti di sviluppo Node.js

Utilizzare [file gulp.js](http://gulpjs.com/) tooautomate distribuzione ed esecuzione di script.

gulp tooinstall, eseguire hello comando terminal hello seguente:

```bash
sudo npm install -g gulp
```

Se si verificano problemi relativi all'installazione di hello, vedere hello [risoluzione dei problemi guida](iot-hub-gateway-kit-c-troubleshooting.md) per soluzioni ai problemi di toocommon.

> [!Note]
> Nodo, NPM e Gulp sono gli script di automazione di richiesto toorun sviluppati in Node.js.

## <a name="install-hello-azure-cli"></a>Installare hello CLI di Azure

hello tooinstall CLI di Azure, seguire questi passaggi:

1. Eseguire i seguenti comandi in terminal hello hello:

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```

   installazione di Hello potrebbe richiedere 5 minuti.

2. Verificare l'installazione di hello eseguendo hello comando seguente:

   ```bash
   az iot -h
   ```
Verrà visualizzato l'output seguente hello se installazione hello ha esito positivo.
![Verificare l'installazione dell'interfaccia della riga di comando di Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)

### <a name="install-visual-studio-code"></a>Installare Visual Studio Code

Utilizzare Visual Studio Code in un secondo momento nei file di configurazione di hello tooedit dell'esercitazione.

[Scaricare](https://code.visualstudio.com/docs/setup/linux) e installare Visual Studio Code.

## <a name="summary"></a>Riepilogo

Aver installato tutti gli strumenti necessario hello e software nel computer host. L'attività successiva è toouse hello Azure CLI toocreate un hub IoT e registrare il dispositivo nell'hub IoT.

## <a name="next-steps"></a>Passaggi successivi
[Creare un hub IoT e registrare il dispositivo](iot-hub-gateway-kit-c-lesson2-register-device.md)
