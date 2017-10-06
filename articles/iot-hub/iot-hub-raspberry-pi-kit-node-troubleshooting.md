---
title: Connect Raspberry PI (C) tooAzure IoT - risoluzione dei problemi | Documenti Microsoft
description: Risoluzione dei problemi di pagina per un'esperienza hello Raspberry Pi Node.js
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Problemi di IoT, Internet delle cose
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 22cf50dc-8206-42a2-a1fc-f75fa85135fa
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8f0807104550e8e53a132f7741564b33f1db17ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a>Risoluzione dei problemi
## <a name="hardware-issues"></a>Problemi hardware
### <a name="hello-application-runs-well-but-hello-led-is-not-blinking"></a>un'applicazione Hello viene eseguita correttamente, ma hello LED è lampeggiante non
Questo problema è sempre connettività circuito toohardware correlati. Utilizzare hello problemi tooidentify i passaggi seguenti:

1. Verificare che si è scelto di hello corretto **GPIO** sulla Lavagna. le porte Hello due **GPIO GND (6 Pin)** e **04 GPIO (7 Pin)**.
2. Verificare che la polarità hello del LED sia corretta. parte di più Hello deve indicare hello **positivo**, pin anode.
3. Hello utilizzare **aggiungere 3,3 v** e **GND Pin** Raspberry Pi 3. Considera Pi hello power controller di dominio. Verificare che hello LED funziona correttamente.

![Specifiche del LED](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a>Altri problemi hardware
Per informazioni sulla risoluzione dei problemi comuni in Raspberry Pi 3, vedere hello [pagina sulla risoluzione dei problemi ufficiale](http://elinux.org/R-Pi_Troubleshooting).

## <a name="nodejs-package-issues"></a>Problemi del pacchetto Node.js
### <a name="no-response-during-gulp-tasks"></a>Nessuna risposta durante le attività gulp
Se si verificano problemi nell'esecuzione di attività gulp, è possibile aggiungere hello `--verbose` opzione per il debug. Provare a eseguire attività gulp corrente tooterminate utilizzando Ctrl + C e quindi eseguire hello comando all'interno dei messaggi di debug toosee finestra console seguente. È possibile visualizzare i messaggi di errore dettagliati nell'output della console.

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a>Problemi di individuazione dei dispositivi
Per semplificare la risoluzione dei problemi comuni con hello `devdisco` comando, controllare hello [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).

### <a name="npm-issues"></a>Problemi di npm
Provare tooupdate del pacchetto npm utilizzando hello comando seguente:

```bash
npm install -g npm
```

Se il problema di hello esiste ancora, lasciare i commenti alla fine di hello di questo articolo o creare un problema di GitHub nel nostro [repository esempio](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).

## <a name="remote-debugging"></a>Debug remoto
### <a name="run-hello-sample-application-in-debug-mode"></a>Eseguire l'applicazione di esempio hello in modalità debug
```bash
gulp run --debug
```

Quando il motore di debug di hello è pronto, è necessario vedere ```Debugger listening on port 5858``` nell'output di console hello.

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a>Configurare il dispositivo remoto di Visual Studio Code tooconnect toohello
1. Aprire hello **Debug** pannello sul lato sinistro hello.
2. Fare clic su hello verde **Avvia debug** pulsante (F5). Visual Studio Code apre un file launch.json.
3. Aggiornare file Launch hello con hello dopo contenuto. Sostituire `[device hostname or IP address]` con hello dispositivo effettivo IP indirizzo o il nome host.

> [!NOTE]
> toolearn ulteriori informazioni su hello il debug di Visual Studio, fare riferimento troppo[debug in Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).


```json
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
            "remoteRoot": null
        }
    ]
}
```

![Configurazione del debug remoto](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a>Collegare l'applicazione remota toohello
Fare clic su hello verde **Avvia debug** (F5) pulsante toostart debug.

Lettura [JavaScript in Visual Studio Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn ulteriori informazioni sul debugger hello.

![Debug remoto interattivo](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a>Problemi dell'interfaccia della riga di comando di Azure
Hello Azure interfaccia della riga di comando (CLI di Azure) è una build di anteprima. soluzioni tooseek, è possibile utilizzare hello [Guida all'installazione di anteprima](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).

Se si verificano i bug con lo strumento di hello, file un [problema](https://github.com/Azure/azure-cli/issues) in hello **problemi** sezione del repository GitHub hello.

Per semplificare la risoluzione dei problemi, controllare hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).

## <a name="python-installation-issues"></a>Problemi di installazione di Python
### <a name="legacy-installation-issues-macos"></a>Problemi di installazione di pacchetti legacy (macOS)
Durante l'installazione di pip, viene generato un errore di autorizzazione quando vengono installati pacchetti legacy con autorizzazioni **su**. Questa situazione si verifica perché l'installazione precedente di Python con brew (macOS) non è stata disinstallata completamente. Alcuni pacchetti pip da un'installazione precedente sono stati creati da radice, causando l'errore di autorizzazione hello. soluzione hello è tooremove tali pacchetti installati dalla radice. Usare questa attività di hello toocomplete i passaggi seguenti:

1. Passare a /usr/local/lib/python2.7/site-packages
2. Elencare i pacchetti creati dall'utente root: `ls -l | grep root`
3. Disinstallare i pacchetti elencati nel passaggio 2: `sudo rm -rf {package name}`
4. Reinstallare Python.

## <a name="azure-iot-hub-issues"></a>Problemi di Hub IoT di Azure
Se è stato eseguito correttamente il provisioning dell'hub IoT di Azure con Azure CLI, ed è necessario un strumento toomanage hello i dispositivi che si connettono tooyour IoT hub, provare a hello gli strumenti seguenti.

### <a name="device-explorer"></a>Esplora dispositivi
Hello [Esplora dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) strumento viene eseguito sul computer locale di Windows e si connette l'hub IoT tooyour in Azure. Comunica con i seguenti hello [gli endpoint IoT Hub](iot-hub-devguide.md):


* *Gestione delle identità dispositivo* tooprovision e gestire i dispositivi registrati con l'hub IoT.
* *Ricezione da dispositivo a cloud* è possibile monitorare i messaggi inviati dall'hub IoT di tooyour di dispositivo.
* *Inviare cloud a dispositivo* in modo da è possibile inviare messaggi dispositivi tooyour l'hub IoT.

Configurare la stringa di connessione hub IoT all'interno di questo strumento di toouse tutte le relative funzionalità.

### <a name="iothub-explorer"></a>iothub-explorer
[l'hub IOT Esplora](https://github.com/Azure/iothub-explorer) è uno strumento di esempio multipiattaforma CLI toomanage per i dispositivi. È possibile utilizzare hello strumento toomanage hello dispositivi nel Registro di sistema di hello identità, il monitoraggio dei messaggi da dispositivo a cloud e inviare messaggi di cloud a dispositivo.

tooinstall hello ultima versione (versione provvisoria) dello strumento di hub IOT Esplora di hello, eseguire hello comando nell'ambiente della riga di comando seguente:

```bash
npm install -g iothub-explorer@latest
```

È possibile utilizzare hello tooget ulteriori informazioni su tutti hello hub IOT Esplora comandi e i relativi parametri di comando seguente:

```bash
iothub-explorer help
```

### <a name="azure-portal"></a>Portale di Azure
Un'interfaccia della riga di comando completa consente di creare e gestire tutte le risorse di Azure. È inoltre possibile hello toouse [portale di Azure](../azure-portal-overview.md) toohelp provisioning, gestire ed eseguire il debug delle risorse di Azure.

## <a name="azure-storage-issues"></a>Problemi di Archiviazione di Azure
[Esplora archivi di Microsoft Azure (anteprima)](http://storageexplorer.com) è un'applicazione autonoma da Microsoft che è possibile utilizzare toowork con dati di archiviazione di Azure in Windows, macOS e Linux. Tramite questo strumento, è possibile connettersi tooyour tabella e visualizzare i dati di hello in essa contenuti. È possibile utilizzare questo strumento tootroubleshoot i problemi di archiviazione di Azure.

