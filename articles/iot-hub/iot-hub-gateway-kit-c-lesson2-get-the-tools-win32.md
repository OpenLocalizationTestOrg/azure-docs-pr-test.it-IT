---
title: 'Dispositivo SensorTag e gateway Azure IoT: lezione 2: Ottenere gli strumenti (Windows) | Documentazione Microsoft'
description: Installare strumenti di hello e software hello nel computer host che eseguono Windows, creare un hub IoT e registrare il dispositivo nell'hub IoT hello.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: sviluppo iot, software iot, servizio cloud iot, software per internet delle cose, interfaccia della riga di comando di azure, installare git in windows, esecuzione di gulp, installare node js in windows, installare npm in windows, installare python in windows
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 18ae6ee4-574a-4d5f-9838-ca2a78165628
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 3b30b60a0115413394992061a88dde4cd442ac19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-and-later"></a>Ottenere strumenti hello (Windows 7 e versioni successive)
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
- Computer Windows.

## <a name="install-git-and-nodejs"></a>Installare Git e Node.js

Fare clic su hello seguente toodownload collegamenti e installare Git e LTS Node.js per Windows.

- [Ottenere Git per Windows](https://git-scm.com/download/win/)
- [Ottenere Node.js LTS per Windows](https://nodejs.org/en/)

## <a name="install-nodejs-development-tools"></a>Installare gli strumenti di sviluppo Node.js

Utilizzare [file gulp.js](http://gulpjs.com/) tooautomate distribuzione ed esecuzione di script.

Premere `Windows + R`, tipo `cmd` e premere `Enter` tooopen una finestra del prompt dei comandi, e quindi eseguire hello finestra di comando seguente:

```cmd
npm install -g gulp
```

Se si verificano problemi relativi all'installazione di hello, vedere hello [risoluzione dei problemi guida](iot-hub-gateway-kit-c-troubleshooting.md) per soluzioni ai problemi di toocommon.

> [!Note]
> Nodo, NPM e Gulp sono gli script di automazione di richiesto toorun sviluppati in Node.js.

## <a name="install-python"></a>Installare Python

È possibile scegliere Python 2.7, 3.4 o 3.5. In questa esercitazione si userà Python 2.7. Se è già stato installato python, andare toohello nella sezione successiva.

[Ottenere Python per Windows](https://www.python.org/downloads/)

È inoltre necessario percorso hello tooadd delle cartelle hello in Python.exe e pip.exe sono installati toohello sistema `PATH` variabile di ambiente. Per impostazione predefinita, python.exe viene installato in `C:\Python27` e pip.exe viene installato in `C:\Python27\Scripts`.

## <a name="install-hello-azure-cli"></a>Installare hello CLI di Azure

hello tooinstall CLI di Azure, seguire questi passaggi:

1. Aprire una finestra del Prompt dei comandi come amministratore.

2. Installare hello CLI di Azure eseguendo hello seguenti comandi:

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```

   installazione di Hello potrebbe richiedere 5 minuti.

3. Verificare l'installazione di hello eseguendo hello comando seguente:

   ```cmd
   az iot -h
   ```

   Verrà visualizzato l'output seguente hello se installazione hello ha esito positivo.

   ![Verificare l'installazione dell'interfaccia della riga di comando di Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_win.png)

## <a name="install-visual-studio-code"></a>Installare Visual Studio Code

Utilizzare Visual Studio Code in un secondo momento nei file di configurazione di hello tooedit dell'esercitazione.

[Scaricare](https://code.visualstudio.com/docs/setup/windows) e installare Visual Studio Code.

## <a name="summary"></a>Riepilogo

Aver installato tutti gli strumenti necessario hello e software nel computer host. L'attività successiva è toouse hello Azure CLI toocreate un hub IoT e registrare il dispositivo nell'hub IoT.

## <a name="next-steps"></a>Passaggi successivi
[Creare un hub IoT e registrare il dispositivo](iot-hub-gateway-kit-c-lesson2-register-device.md)
