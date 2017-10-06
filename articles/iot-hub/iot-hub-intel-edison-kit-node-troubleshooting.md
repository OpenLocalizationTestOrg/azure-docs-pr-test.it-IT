---
title: 'Connettersi Edison Intel (nodo) tooAzure IoT - lezione 4: risoluzione dei problemi | Documenti Microsoft'
description: Pagina sulla risoluzione dei problemi per Node.js in Intel Edison
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: risoluzione dei problemi in arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: f11c5521-8a36-44c0-baad-f5ec26ab4618
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9502300f7f372255572b49bea45dd3e1fdaeeb37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a>Risoluzione dei problemi
## <a name="hardware-issues"></a>Problemi hardware
Per informazioni sulla risoluzione dei problemi comuni in Edison Intel, vedere hello [pagina sulla risoluzione dei problemi ufficiale](https://software.intel.com/en-us/node/637974).

## <a name="nodejs-package-issues"></a>Problemi del pacchetto Node.js
### <a name="no-response-during-gulp-tasks"></a>Nessuna risposta durante le attività gulp
Se si verificano problemi durante l'esecuzione di attività gulp, è possibile aggiungere hello `--verbose` opzione per il debug. Provare a eseguire attività gulp corrente tooterminate utilizzando `Ctrl + C`, e quindi eseguire hello seguendo comando all'interno dei messaggi di debug toosee finestra console. È possibile visualizzare i messaggi di errore dettagliati nell'output della console. 

```bash
gulp --verbose
```

### <a name="npm-issues"></a>Problemi di NPM
Provare tooupdate del pacchetto NPM con hello comando seguente:

```bash
npm install -g npm
```

Se il problema di hello esiste ancora, lasciare i commenti alla fine di hello di questo articolo o creare un problema di GitHub nel nostro [repository esempio][sample-repository].

## <a name="remote-debugging"></a>Debug remoto

### <a name="run-hello-sample-application-in-debug-mode"></a>Eseguire l'applicazione di esempio hello in modalità debug

```bash
gulp run --debug
```

Quando il motore di debug di hello è pronto, dovrebbe essere in grado di toosee ```Debugger listening on port 5858``` dall'output di console hello.

### <a name="configure-vs-code-tooconnect-toohello-remote-device"></a>Configurare il dispositivo remoto di Visual Studio Code tooconnect toohello

Aprire hello **Debug** pannello da hello lato sinistro.

Fare clic su hello verde **Avvia debug** pulsante (F5). Aprirà Visual Studio Code un **Launch** file, che è necessario tooupdate.

Hello aggiornamento **Launch** contenuto del file con hello seguente, sostituire `[device hostname or IP address]` con indirizzo IP dispositivo effettivo di hello o il nome host.  

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

![Configurazione del debug remoto](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a>Collegare l'applicazione remota toohello

Fare clic su hello verde **Avvia debug** (F5) pulsante e sfruttare il debug.

È possibile leggere [JavaScript in Visual Studio Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn ulteriori informazioni sul debugger hello.

![Debug remoto interattivo](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a>Problemi dell'interfaccia della riga di comando di Azure
Hello Azure interfaccia della riga di comando (CLI di Azure) è una build di anteprima. Cercare soluzioni in hello [Guida all'installazione di anteprima](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek soluzioni. Provare a eseguire tooupgrade cli di Azure toolatest versione quando i comandi non funzionano come previsto.

Se si verificano i bug con lo strumento di hello, file un [problema](https://github.com/Azure/azure-cli/issues) in hello **problemi** sezione del repository GitHub hello.

Per informazioni sulla risoluzione dei problemi comuni, controllare hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).

Se vengono soddisfatti, "Impossibile trovare una versione che soddisfa il requisito di hello", versione toolastest di pip tooupgrade comando che segue hello esecuzione.

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a>Problemi di installazione di Python
### <a name="legacy-installation-issues-macos"></a>Problemi di installazione di pacchetti legacy (macOS)
Durante l'installazione di **pip**, viene generato un errore di autorizzazione quando vengono installati pacchetti legacy con autorizzazioni **su**. Questa situazione si verifica perché l'installazione precedente di Python con brew (macOS) non è stata disinstallata completamente. Alcuni **pip** da radice, causando l'errore di autorizzazione hello sono stati creati i pacchetti da un'installazione precedente. soluzione hello è tooremove tali pacchetti installati dalla radice. Usare questa attività di hello toocomplete i passaggi seguenti:

1. Passare a /usr/local/lib/python2.7/site-packages
2. Elencare i pacchetti creati dall'utente root: `ls -l | grep root`
3. Disinstallare i pacchetti elencati nel passaggio 2: `sudo rm -rf {package name}`
4. Reinstallare Python.

## <a name="azure-iot-hub-issues"></a>Problemi di Hub IoT di Azure
Se hai eseguito correttamente il provisioning dell'hub IoT di Azure con `azure-cli`, ed è necessario un strumento toomanage hello i dispositivi che si connettono tooyour IoT hub, hello provare gli strumenti seguenti:

### <a name="device-explorer"></a>Esplora dispositivi
[Esplora dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) viene eseguito sul computer locale di Windows e si connette l'hub IoT tooyour in Azure. Comunica con i seguenti hello [gli endpoint IoT Hub](iot-hub-devguide.md):

- _Gestione delle identità dispositivo_ tooprovision e gestire i dispositivi registrati con l'hub IoT.
- _Ricezione da dispositivo a cloud_ è possibile monitorare i messaggi inviati dall'hub IoT di tooyour di dispositivo.
- _Inviare cloud a dispositivo_ in modo da è possibile inviare messaggi dispositivi tooyour l'hub IoT.

Configurare il `IoT hub connection string` all'interno di questo strumento toouse tutte le relative funzionalità.

### <a name="iot-hub-explorer"></a>IoT Hub Explorer
[Hub IoT Esplora](https://github.com/Azure/iothub-explorer) è uno strumento di esempio multipiattaforma CLI toomanage client dei dispositivi. Si può utilizzare hello strumento toomanage hello dispositivi nel Registro di identità hello, il monitoraggio dei messaggi da dispositivo a cloud e inviare comandi cloud a dispositivo.

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
[Esplora archivi di Microsoft Azure (anteprima)](http://storageexplorer.com) è un'applicazione autonoma di Microsoft che è possibile utilizzare toowork con [di archiviazione di Azure](https://azure.microsoft.com/en-us/services/storage/) dati in Windows, macOS e Linux. Tramite questo strumento, è possibile connettersi tooyour tabella e visualizzare i dati di hello in essa contenuti. È possibile utilizzare questo strumento tootroubleshoot i problemi di archiviazione di Azure.

## <a name="next-steps"></a>Passaggi successivi
Questa pagina include solo i problemi più comuni di hello del kit di Edison Intel. È anche possibile lasciare commenti nella parte inferiore tooreport problemi per la risoluzione del problema.

Tornare indietro troppo[introduzione Edison Intel (Node.js)](iot-hub-intel-edison-kit-node-get-started.md)

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-node-edison-getting-started