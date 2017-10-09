---
title: 'Connect Raspberry PI (C) tooAzure IoT - lezione 1: distribuire app | Documenti Microsoft'
description: Clonazione di un'applicazione hello esempio C da GitHub e gulp toodeploy questa scheda tooyour Raspberry Pi 3 dell'applicazione. Questa applicazione di esempio lampeggia hello LED connesso toohello Lavagna ogni due secondi.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: lampeggiamento led raspberry pi, far lampeggiare il led con raspberry pi
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: f601d1e1-2bc3-4cc5-a6b1-0467e5304dcf
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: e90c3360c4de1873313db19561c781eb21dbf1d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a>Creare e distribuire un'applicazione hello blink
## <a name="what-you-will-do"></a>Contenuto dell'esercitazione
Clonazione di un'applicazione hello esempio C da GitHub e utilizzare hello gulp strumento toodeploy hello esempio applicazione tooRaspberry Pi 3. applicazione di esempio Hello lampeggia hello LED connesso toohello Lavagna ogni due secondi. Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione
Contenuto dell'articolo:

* Come hello toouse `device-discover-cli` tooretrieve strumento rete informazioni Pi.
* Toodeploy e hello esecuzione esempio come applicazione in Installazione guidata piattaforma.
* Come toodeploy ed eseguire il debug di applicazioni in esecuzione in modalità remota in Pi.

## <a name="what-you-need"></a>Elementi necessari
È necessario che sia completata hello seguenti operazioni:

* [Configurare il dispositivo](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md)
* [Ottenere strumenti hello](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

## <a name="obtain-hello-ip-address-and-host-name-of-pi"></a>Ottenere hello IP indirizzo e il nome host di pi greco
Aprire un prompt dei comandi in Windows o un terminale macOS o Ubuntu e quindi eseguire hello comando seguente:

```bash
devdisco list --eth
```

Verrà visualizzato un output simile toohello seguenti:

![Individuazione del dispositivo](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

Prendere nota di hello `IP address` e `hostname` di pi greco. Queste informazioni saranno necessarie più avanti in questo articolo.

> [!NOTE]
> Assicurarsi che l'installazione guidata piattaforma sia connesso toohello stessa rete del computer. Ad esempio, se il computer è connesso tooa rete wireless mentre Pi è connesso tooa rete cablata, si potrebbe visualizzare non hello IP indirizzo nell'output di hello devdisco.

## <a name="open-hello-sample-application"></a>Applicazione di esempio hello aperto
hello tooopen applicazione di esempio, seguire questi passaggi:

1. Clonare il repository di esempio hello da GitHub eseguendo hello comando seguente:
   
    ```bash
    git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started.git
    ```
2. Aprire l'applicazione di esempio hello in Visual Studio Code eseguendo hello seguenti comandi:
   
    ```bash
    cd iot-hub-c-raspberrypi-getting-started
    cd Lesson1
    code .
    ```

![Struttura del repository](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-c-mac.png)

Hello `main.c` file hello `app` sottocartella è hello i file di origine della chiave che contiene hello codice toocontrol hello LED.

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
   
   file di configurazione Hello `config-raspberrypi.json` contiene credenziali utente hello è utilizzare toolog tooPi. perdita di hello tooavoid delle credenziali dell'utente, viene generato il file di configurazione di hello nella sottocartella hello `.iot-hub-getting-started` della cartella principale di hello nel computer in uso.

2. Aprire il file di configurazione dispositivo hello in Visual Studio Code eseguendo hello comando seguente:
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```

3. Sostituire il segnaposto hello `[device hostname or IP address]` con indirizzo IP hello o il nome host hello che è stato ottenuto in precedenza in "Ottenere hello IP indirizzo e nome host di pi greco."
   
   ![Config.json](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> È possibile utilizzare la chiave SSH anziché nome utente e password quando ci si connette tooRaspberry Pi. In ordine toodo questo sarà necessario toogenerate hello chiave usando **ssh-keygen** e **pi ssh-copy-id @\<indirizzo dispositivo\>**.
>
> In Windows, questi comandi sono disponibili in **Git Bash**.
>
> MacOS è necessario toorun **brew installare ssh-copy-id**.
>
> Dopo aver caricato correttamente hello chiave toohello Raspberry Pi, sostituire **device_password** con **device_key_path** proprietà **config raspberrypi.json**.
>
> Le righe aggiornate saranno simili alle seguenti:
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

Congratulazioni. È stato creato correttamente l'applicazione di esempio prima di hello per Pi.

## <a name="deploy-and-run-hello-sample-application"></a>Distribuire ed eseguire l'applicazione di esempio hello
### <a name="install-hello-azure-iot-hub-sdk-on-pi"></a>Installare hello Azure IoT Hub SDK in Pi
Installare hello Azure IoT Hub SDK in Pi eseguendo hello comando seguente:

```bash
gulp install-tools
```

Questa operazione potrebbe richiedere qualche hello toocomplete di minuti alla prima esecuzione.

### <a name="deploy-and-run-hello-sample-app"></a>Distribuire ed eseguire app di esempio hello
Distribuire ed eseguire l'applicazione di esempio hello eseguendo hello comando seguente:

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a>Verificare il funzionamento dell'applicazione hello
applicazione di esempio Hello termina automaticamente dopo hello LED lampeggia per 20 volte. Se non viene visualizzato hello LED è lampeggiante, vedere hello [risoluzione dei problemi guida](iot-hub-raspberry-pi-kit-c-troubleshooting.md) per soluzioni ai problemi di toocommon.
![LED lampeggiante](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)

## <a name="summary"></a>Riepilogo
È stato installato hello necessario strumenti toowork con Pi e distribuito un hello tooblink di tooPi dall'applicazione di esempio LED. È ora possibile creare, distribuire e l'esecuzione di un'altra applicazione di esempio che si connette Pi tooAzure toosend IoT Hub e ricevere messaggi.

## <a name="next-steps"></a>Passaggi successivi
[Ottenere gli strumenti di Azure](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)

