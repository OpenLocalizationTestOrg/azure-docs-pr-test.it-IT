---
title: 'Dispositivo SensorTag e gateway Azure IoT: lezione 2: Ottenere gli strumenti (Ubuntu) | Documentazione Microsoft'
description: Installare gli strumenti e il software nel computer host che esegue Ubuntu, creare un hub IoT e registrare il dispositivo nell'hub IoT.
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
ms.openlocfilehash: 234b60e1f8eaff52ce07f54d4d12de2421cc1a52
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a>Ottenere gli strumenti (Ubuntu 16.04)
> [!div class="op_single_selector"]
> * [Windows 7 o versione successiva](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>Contenuto dell'esercitazione

- Installare Git, Node.js, Gulp e Python.
- Installare l'interfaccia della riga di comando di Azure. 

In caso di problemi, cercare le soluzioni nella pagina sulla [risoluzione dei problemi](iot-hub-gateway-kit-c-troubleshooting.md).
## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione

In questa lezione si apprenderà:

- Come installare Git e Node.js.
  - Git è un sistema distribuito open source di controllo delle versioni. L'applicazione di esempio per questa lezione è archiviata in Git.
  - Node.js è un runtime JavaScript con un ampio ecosistema di pacchetti.
- Come usare NPM per installare gli strumenti di sviluppo Node.js.
  - La versione minima richiesta di Node.js è 4.5 LTS.
  - NPM è uno degli strumenti di gestione pacchetti per Node.js.
- Come installare Visual Studio Code.
  - Visual Studio Code è un editor di codice sorgente multipiattaforma leggero ma potente per Windows, Linux e macOS. Dispone di un elevato supporto per funzionalità quali debug, controllo Git incorporato, evidenziazione della sintassi, completamento intelligente del codice, frammenti di codice e refactoring del codice.
- Come installare l'interfaccia della riga di comando di Azure
  - L'interfaccia della riga di comando di Azure offre un'esperienza di riga di comando multipiattaforma per Azure. Il provisioning e la gestione delle risorse vengono eseguiti direttamente dalla riga di comando.
- Come usare l'interfaccia della riga di comando di Azure per creare un hub IoT.

## <a name="what-you-need"></a>Elementi necessari

- Connessione Internet per scaricare gli strumenti e il software.
- Un computer che esegue Ubuntu 16.04 o versione successiva.

## <a name="install-git-and-nodejs"></a>Installare Git e Node.js

Per installare Git e Node.js, seguire questa procedura:

1. Premere `Ctrl + Alt + T` per aprire un terminale.
2. Eseguire i comandi seguenti:

   ```bash
   sudo apt-get update
   curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
   sudo apt-get install -y nodejs
   sudo apt-get install git
   ```

## <a name="install-nodejs-development-tools"></a>Installare gli strumenti di sviluppo Node.js

Usare [gulp.js](http://gulpjs.com/) per automatizzare la distribuzione e l'esecuzione di script.

Per installare gulp, eseguire questo comando nel terminale:

```bash
sudo npm install -g gulp
```

Se si verificano problemi con l'installazione, vedere la [Guida alla risoluzione dei problemi](iot-hub-gateway-kit-c-troubleshooting.md) per trovare le soluzioni ai problemi comuni.

> [!Note]
> Node, NPM e Gulp sono necessari per eseguire gli script di automazione sviluppati in Node.js.

## <a name="install-the-azure-cli"></a>Installare l'interfaccia della riga di comando di Azure

Per installare l'interfaccia della riga di comando di Azure, seguire questi passaggi:

1. Eseguire questi comandi nel terminale:

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```

   L'installazione potrebbe richiedere 5 minuti.

2. Verificare l'installazione usando il comando seguente:

   ```bash
   az iot -h
   ```
Se l'installazione ha esito positivo, verrà visualizzato l'output seguente.
![Verificare l'installazione dell'interfaccia della riga di comando di Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)

### <a name="install-visual-studio-code"></a>Installare Visual Studio Code

Visual Studio Code verrà usato più avanti nell'esercitazione per modificare i file di configurazione.

[Scaricare](https://code.visualstudio.com/docs/setup/linux) e installare Visual Studio Code.

## <a name="summary"></a>Riepilogo

Sono stati installati tutto il software e tutti gli strumenti necessari nel computer host. L'attività successiva consiste nell'usare l'interfaccia della riga di comando di Azure per creare un hub IoT e registrarvi il dispositivo.

## <a name="next-steps"></a>Passaggi successivi
[Creare un hub IoT e registrare il dispositivo](iot-hub-gateway-kit-c-lesson2-register-device.md)
