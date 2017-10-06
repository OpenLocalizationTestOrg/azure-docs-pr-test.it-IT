---
title: 'Connettersi Edison Intel (nodo) tooAzure IoT - lezione 1: distribuire app | Documenti Microsoft'
description: Clonazione di un'applicazione hello esempio C da GitHub ed eseguire gulp toodeploy questo tooyour applicazione Lavagna Edison Intel. Questa applicazione di esempio lampeggia hello LED connesso toohello Lavagna ogni due secondi.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: progetti led arduino, lampeggiamento led arduino, codice di lampeggiamento led arduino, programma di lampeggiamento arduino, esempio di lampeggiamento arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: ed2c21d0-c72c-4ac2-9e70-347e9a0711c0
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: bc03c7e45bd1ba9e9b2c8f2fec70a1be647e96b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a>Creare e distribuire un'applicazione hello blink
## <a name="what-you-will-do"></a>Contenuto dell'esercitazione
Applicazione di esempio C hello da GitHub clonare e usare hello gulp strumento toodeploy hello esempio applicazione tooIntel Edison. applicazione di esempio Hello lampeggia hello LED connesso toohello Lavagna ogni due secondi. Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina][troubleshooting].

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione
* Come applicazione in Edison esempio toodeploy e hello esecuzione.

## <a name="what-you-need"></a>Elementi necessari
È necessario che sia completata hello seguenti operazioni:

* [Configurare il dispositivo][configure-your-device]
* [Ottenere strumenti hello][get-the-tools]

## <a name="open-hello-sample-application"></a>Applicazione di esempio hello aperto
hello tooopen applicazione di esempio, seguire questi passaggi:

1. Clonare il repository di esempio hello da GitHub eseguendo hello comando seguente:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-edison-getting-started.git
   ```
2. Aprire l'applicazione di esempio hello in Visual Studio Code eseguendo hello seguenti comandi:

   ```bash
   cd iot-hub-node-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Struttura del repository][repo-structure]

file Hello in hello `app` sottocartella è hello i file di origine della chiave che contiene hello codice toocontrol hello LED.

### <a name="install-application-dependencies"></a>Installare le dipendenze dell'applicazione
Installare le librerie di hello e altri moduli, che è necessario per l'applicazione di esempio hello eseguendo hello comando seguente:

```bash
npm install
```

## <a name="configure-hello-device-connection"></a>Configurare una connessione al dispositivo hello
tooconfigure hello connessione al dispositivo, seguire questi passaggi:

1. Generare file di configurazione dispositivo hello eseguendo hello comando seguente:

   ```bash
   gulp init
   ```

   file di configurazione Hello `config-edison.json` contiene credenziali utente hello è utilizzare toolog tooEdison. perdita di hello tooavoid delle credenziali dell'utente, viene generato il file di configurazione di hello nella sottocartella hello `.iot-hub-getting-started` della cartella principale di hello nel computer in uso.

2. Aprire il file di configurazione dispositivo hello in Visual Studio Code eseguendo hello comando seguente:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. Sostituire il segnaposto hello `[device hostname or IP address]` e `[device password]` con indirizzo IP hello e una password che è contrassegnato come inattivo nella lezione precedente.

   ![Config.json](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

Congratulazioni. È stato creato correttamente l'applicazione di esempio per Edison prima hello.

## <a name="deploy-and-run-hello-sample-application"></a>Distribuire ed eseguire l'applicazione di esempio hello

### <a name="deploy-and-run-hello-sample-app"></a>Distribuire ed eseguire app di esempio hello
Distribuire ed eseguire l'applicazione di esempio hello eseguendo hello comando seguente:

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a>Verificare il funzionamento dell'applicazione hello
applicazione di esempio Hello termina automaticamente dopo hello LED lampeggia per 20 volte. Se non viene visualizzato hello LED è lampeggiante, vedere hello [risoluzione dei problemi guida] [ troubleshooting] per soluzioni ai problemi di toocommon.

![LED lampeggiante][led-blinking]

## <a name="summary"></a>Riepilogo
È stato installato hello necessario strumenti toowork con Edison e distribuito un hello tooblink di tooEdison dall'applicazione di esempio LED. È ora possibile creare, distribuire e l'esecuzione di un'altra applicazione di esempio che si connette Edison tooAzure toosend IoT Hub e ricevere messaggi.

## <a name="next-steps"></a>Passaggi successivi
[Ottenere hello gli strumenti di Azure][get-the-azure-tools]

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
