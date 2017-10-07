---
title: 'Dispositivo simulato e gateway Azure IoT: risoluzione dei problemi | Documentazione Microsoft'
description: Pagina sulla risoluzione dei problemi del gateway Intel NUC
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Problemi di IoT, Internet delle cose
ROBOTS: NOINDEX
ms.assetid: 3ee8f4b0-5799-40a3-8cf0-8d5aa44dbc2b
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: cc7add6273e66aadeca9a4915a44f5edf61a0a59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a>Risoluzione dei problemi

## <a name="hardware-issues"></a>Problemi hardware

### <a name="ti-sensortag-cannot-be-connected"></a>Impossibile connettere SensorTag di Texas Instruments

problemi di connettività SensorTag tootroubleshoot, utilizzare hello [SensorTag app](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).

### <a name="have-an-issue-with-intel-nuc"></a>Problema relativo a Intel NUC

problemi di avvio tootroubleshoot, fare riferimento troppo[risolvere i problemi di avvio non Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).

problemi del sistema operativo tootroubleshoot, fare riferimento troppo[risolvere i problemi del sistema operativo di Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).

tootroubleshoot altri problemi, fare riferimento troppo[Blink codici e un segnale acustico per Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).

## <a name="nodejs-package-issues"></a>Problemi del pacchetto Node.js

### <a name="no-response-during-gulp-tasks"></a>Nessuna risposta durante le attività gulp

Se si verificano problemi nell'esecuzione di attività gulp, è possibile aggiungere hello `--verbose` opzione per il debug. Provare a eseguire attività gulp corrente tooterminate utilizzando `Ctrl + C`, e quindi eseguire hello seguendo comando all'interno dei messaggi di debug toosee finestra console. È possibile visualizzare i messaggi di errore dettagliati nell'output della console.

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a>Problemi di individuazione dei dispositivi

Per semplificare la risoluzione dei problemi comuni con hello `discover-sensortag` comando, controllare hello [pagina wiki](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).

### <a name="npm-issues"></a>Problemi di npm

Provare tooupdate del pacchetto npm eseguendo hello comando seguente:

```bash
npm install -g npm
```

Se il problema di hello esiste ancora, lasciare i commenti alla fine di hello di questo articolo o creare un problema di GitHub nel nostro [repository esempio](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).

## <a name="remote-debugging"></a>Debug remoto
> Le istruzioni riportate di seguito consentono di eseguire il debug degli script node.js usati in questa esercitazione.
### <a name="run-hello-sample-application-in-debug-mode"></a>Eseguire l'applicazione di esempio hello in modalità debug

Eseguire l'applicazione di esempio hello in modalità di debug eseguendo hello comando seguente:

```bash
gulp run --debug
```

Quando il motore di debug di hello è pronto, è necessario vedere `Debugger listening on port 5858` nell'output di console hello.

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a>Configurare il dispositivo remoto di Visual Studio Code tooconnect toohello

1. Aprire hello **Debug** pannello sul lato sinistro hello.
2. Fare clic su hello verde **Avvia debug** pulsante (F5). In Visual Studio Code viene aperto un file `launch.json`.
3. Hello aggiornamento `launch.json` file con hello dopo contenuto. Sostituire `[device hostname or IP address]` con hello dispositivo effettivo IP indirizzo o il nome host.

   ``` json
   {
     "version": "0.2.0",
     "configurations": [
        {
            "name": "Attach",
            "type": "node",
            "request": "attach",
            "port": 5858,
            "address": "[device hostname or IP address]",
            "restart": false,
            "sourceMaps": false,
            "outDir": null,
            "localRoot": "${workspaceRoot}",
            "remoteRoot": "~/ble_sample"
        }
     ]
   }
   ```

![Configurazione del debug remoto](./media/iot-hub-gateway-kit-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a>Collegare l'applicazione remota toohello

Fare clic su hello verde **Avvia debug** (F5) pulsante toostart debug.

Lettura [JavaScript in Visual Studio Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn ulteriori informazioni sul debugger hello.

![Debug dell'esempio BLE](./media/iot-hub-gateway-kit-lessons/troubleshooting/debugging_ble_sample.png)

## <a name="azure-cli-issues"></a>Problemi dell'interfaccia della riga di comando di Azure

Hello Azure interfaccia della riga di comando (CLI di Azure) è una build di anteprima. soluzioni tooseek, è possibile utilizzare hello [Guida all'installazione di anteprima](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).

Se si verificano i bug con lo strumento di hello, file un [problema](https://github.com/Azure/azure-cli/issues) in hello **problemi** sezione del repository GitHub hello.

Per semplificare la risoluzione dei problemi, controllare hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).

Se vengono soddisfatti, "Impossibile trovare una versione che soddisfa il requisito di hello", versione toolastest di pip tooupgrade comando che segue hello esecuzione.

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a>Problemi di installazione di Python

### <a name="legacy-installation-issues-macos"></a>Problemi di installazione di pacchetti legacy (macOS)

Durante l'installazione di pip, viene generato un errore di autorizzazione quando vengono installati pacchetti legacy con autorizzazioni **su**. Questa situazione si verifica perché l'installazione precedente di Python con brew (macOS) non è stata disinstallata completamente. Alcuni pacchetti pip da un'installazione precedente sono stati creati da radice, causando l'errore di autorizzazione hello. soluzione hello è tooremove tali pacchetti installati dalla radice. Usare questa attività di hello toocomplete i passaggi seguenti:

1. Andare troppo`/usr/local/lib/python2.7/site-packages`
2. Elencare i pacchetti creati dall'utente root: `ls -l | grep root`
3. Disinstallare i pacchetti elencati nel passaggio 2: `sudo rm -rf {package name}`
4. Reinstallare Python.

## <a name="azure-iot-hub-issues"></a>Problemi di Hub IoT di Azure

Se è stato eseguito correttamente il provisioning dell'hub IoT di Azure con hello CLI di Azure ed è necessario un strumento toomanage hello i dispositivi che si connettono tooyour IoT hub, provare a hello gli strumenti seguenti.

### <a name="device-explorer"></a>Esplora dispositivi

[Esplora dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) viene eseguito sul computer locale di Windows e si connette l'hub IoT tooyour in Azure. Comunica con i seguenti hello [gli endpoint IoT Hub](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):

- Tooprovision di gestione di identità dispositivo e gestire i dispositivi registrati con l'hub IoT.
- È possibile monitorare i messaggi inviati dall'hub IoT di tooyour di dispositivo di ricezione da dispositivo a cloud.
- Inviata da cloud a dispositivo in modo da è possibile inviare messaggi dispositivi tooyour l'hub IoT.

Configurare la stringa di connessione hub IoT all'interno di questo strumento di toouse tutte le relative funzionalità.

### <a name="iothub-explorer"></a>iothub-explorer

[l'hub IOT Esplora](https://github.com/Azure/iothub-explorer) è uno strumento di esempio multipiattaforma CLI toomanage client dei dispositivi. Si può utilizzare hello strumento toomanage hello dispositivi nel Registro di identità hello, il monitoraggio dei messaggi da dispositivo a cloud e inviare comandi cloud a dispositivo.

tooinstall hello più recente (versione non definitiva) dello strumento di hub IOT-explorer hello, eseguire hello comando seguente:

```bash
npm install -g iothub-explorer@latest
```

tooget ulteriori informazioni su tutti hello hub IOT Esplora comandi e i relativi parametri, eseguire hello comando seguente:

```bash
iothub-explorer help
```

### <a name="hello-azure-portal"></a>Hello portale di Azure

Un'interfaccia della riga di comando completa consente di creare e gestire tutte le risorse di Azure. È inoltre possibile hello toouse [portale di Azure](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) toohelp provisioning, gestire ed eseguire il debug delle risorse di Azure.

## <a name="azure-storage-issues"></a>Problemi di Archiviazione di Azure

[Esplora archivi di Microsoft Azure (anteprima)](http://storageexplorer.com/) è un'applicazione autonoma da Microsoft che è possibile utilizzare toowork con dati di archiviazione di Azure in Windows, macOS e Linux. Tramite questo strumento, è possibile connettersi tooyour tabella e visualizzare i dati di hello in essa contenuti. È possibile utilizzare questo strumento tootroubleshoot i problemi di archiviazione di Azure.
