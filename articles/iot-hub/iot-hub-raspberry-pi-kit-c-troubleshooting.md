---
title: Connect Raspberry PI (C) tooAzure IoT - risoluzione dei problemi | Documenti Microsoft
description: Pagina sulla risoluzione dei problemi relativi all'esperienza Node.js del dispositivo Raspberry Pi
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Problemi di IoT, Internet delle cose
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 3653c79b-8a0c-41d4-b0bf-f6b4edb4d233
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4f1ea81dd25d10a39c2939f5ee5f19f6d2ba2b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a>Risoluzione dei problemi
## <a name="hardware-issues"></a>Problemi hardware
### <a name="hello-application-runs-well-but-hello-led-is-not-blinking"></a>un'applicazione Hello viene eseguita correttamente, ma hello LED è lampeggiante non
Questo problema è sempre la connettività di circuito hardware toohello correlati. Utilizzare hello problemi tooidentify i passaggi seguenti.

1. Verificare che si è scelto di hello corretto **GPIO** sulla Lavagna. le porte Hello due **GPIO GND (6 Pin)** e **04 GPIO (7 Pin)**.
2. Verificare che la polarità hello del LED sia corretta. parte di più Hello deve indicare hello **positivo**, pin anode.
3. Hello utilizzare **aggiungere 3,3 v** e **GND Pin** Raspberry Pi 3. Considera Pi hello power controller di dominio. Verificare che hello LED funziona correttamente.

![Specifiche del LED](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a>Altri problemi hardware
Per informazioni sulla risoluzione dei problemi comuni in Raspberry Pi 3, vedere hello [pagina sulla risoluzione dei problemi ufficiale](http://elinux.org/R-Pi_Troubleshooting).

## <a name="nodejs-package-issues"></a>Problemi del pacchetto Node.js
### <a name="no-response-during-gulp-tasks"></a>Nessuna risposta durante le attività gulp
Se si verificano problemi durante l'esecuzione di attività gulp, è possibile aggiungere hello `--verbose` opzione per il debug. Provare a eseguire attività gulp corrente tooterminate utilizzando `Ctrl + C`, e quindi eseguire hello seguendo comando all'interno dei messaggi di debug toosee finestra console. È possibile visualizzare i messaggi di errore dettagliati nell'output della console. 

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a>Problemi di individuazione dei dispositivi
Per semplificare la risoluzione dei problemi comuni con hello `devdisco` comando, controllare hello [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).

### <a name="npm-issues"></a>Problemi di NPM
Provare tooupdate del pacchetto NPM con hello comando seguente:

```bash
npm install -g npm
```

Se il problema di hello esiste ancora, lasciare i commenti alla fine di hello di questo articolo o creare un problema di GitHub nel nostro [repository di esempio](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)

## <a name="remote-debugging"></a>Debug remoto

Il supporto remoto sarà disponibile presto in Visual Studio Code C/C++ Extension.

Nel frattempo è possibile usare GDB tramite il terminale SSH preferito:

```bash
cd c-pi-lesson-x
sudo gdb app
```

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
[Esplora dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) viene eseguito sul computer locale di Windows e si connette l'hub IoT tooyour in Azure. Comunica con i seguenti hello [gli endpoint IoT Hub](iot-hub-devguide.md):

* *Gestione delle identità dispositivo* tooprovision e gestire i dispositivi registrati con l'hub IoT.
* *Ricezione da dispositivo a cloud* è possibile monitorare i messaggi inviati dall'hub IoT di tooyour di dispositivo.
* *Inviare cloud a dispositivo* in modo da è possibile inviare messaggi dispositivi tooyour l'hub IoT.

Configurare il `IoT hub connection string` all'interno di questo strumento toouse tutte le relative funzionalità.

### <a name="iot-hub-explorer"></a>IoT Hub Explorer
[Hub IoT Esplora](https://github.com/Azure/iothub-explorer) è uno strumento di esempio multipiattaforma CLI toomanage client dei dispositivi. Si può utilizzare hello strumento toomanage hello dispositivi nel Registro di identità hello, il monitoraggio dei messaggi da dispositivo a cloud e inviare comandi cloud a dispositivo.

tooinstall hello ultima versione (versione provvisoria) dello strumento di hub IOT Esplora di hello, eseguire hello comando nell'ambiente della riga di comando seguente:

```
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
