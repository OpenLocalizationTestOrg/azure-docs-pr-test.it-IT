---
title: Connect Arduino (C) tooAzure IoT - risoluzione dei problemi | Documenti Microsoft
description: Pagina sulla risoluzione dei problemi per l'esperienza Arduino in Adafruit Feather M0 WiFi
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: risoluzione dei problemi in arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: fdcc56ff-4420-463c-8a0e-5a1d215a874f
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ed793041ffa1887dbe73067f7c48d2417e982866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a>Risoluzione dei problemi
## <a name="hardware-issues"></a>Problemi hardware
Per informazioni sulla risoluzione dei problemi più comuni sulla Lavagna Adafruit sfumatura M0 Wi-Fi Arduino, vedere hello [pagina sulla risoluzione dei problemi ufficiale](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500?view=all#faq).

## <a name="nodejs-package-issues"></a>Problemi del pacchetto Node.js
### <a name="no-response-during-gulp-tasks"></a>Nessuna risposta durante le attività gulp
Se si verificano problemi durante l'esecuzione di attività gulp, è possibile aggiungere hello `--verbose` opzione per il debug. Provare a eseguire attività gulp corrente tooterminate utilizzando `Ctrl + C`, e quindi eseguire hello seguendo comando all'interno dei messaggi di debug toosee finestra console. È possibile visualizzare i messaggi di errore dettagliati nell'output della console.

```bash
gulp --verbose
```

Oppure è possibile aggiungere `--listen` informazioni del log dispositivo toooutput tooopen porta seriale.

```bash
gulp --listen
``` 

### <a name="npm-issues"></a>Problemi di NPM
Provare tooupdate del pacchetto NPM con hello comando seguente:

```bash
npm install -g npm
```

Se il problema di hello esiste ancora, lasciare i commenti alla fine di hello di questo articolo o creare un problema di GitHub nel nostro [repository esempio][sample-repository].

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

* *Gestione delle identità dispositivo* tooprovision e gestire i dispositivi registrati con l'hub IoT.
* *Ricezione da dispositivo a cloud* è possibile monitorare i messaggi inviati dall'hub IoT di tooyour di dispositivo.
* *Inviare cloud a dispositivo* in modo da è possibile inviare messaggi dispositivi tooyour l'hub IoT.

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
[Esplora archivi di Microsoft Azure (anteprima)](http://storageexplorer.com) è un'applicazione autonoma da Microsoft che è possibile utilizzare toowork con dati di archiviazione di Azure in Windows, macOS e Linux. Tramite questo strumento, è possibile connettersi tooyour tabella e visualizzare i dati di hello in essa contenuti. È possibile utilizzare questo strumento tootroubleshoot i problemi di archiviazione di Azure.

<!-- Images and links -->

[sample-repository]: https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md