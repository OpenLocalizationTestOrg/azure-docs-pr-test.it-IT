---
title: 'Connect Arduino (C) tooAzure IoT - lezione 3: eseguire l''esempio | Documenti Microsoft'
description: Distribuire ed eseguire un tooAdafruit di applicazione di esempio sfumatura M0 Wi-Fi che invia l'hub IoT tooyour messaggi e lampeggia hello LED.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: servizio cloud IOT, arduino inviare dati toocloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 92cce319-2b17-4c9b-889d-deac959e3e7c
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ddca015a3655f8a1a9de2a00e718ec0d28a5affb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a>Eseguire un toosend di applicazione di esempio i messaggi da dispositivo a cloud
## <a name="what-you-will-do"></a>Contenuto dell'esercitazione
In questo articolo verrà illustrato come toodeploy ed eseguire un'applicazione di esempio nel Wi-Fi Arduino di Adafruit sfumatura M0 board tale hub IoT tooyour di Invia messaggi.

Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina][troubleshooting].

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione
Si apprenderà come hello toouse gulp toodeploy strumento e l'esecuzione di un'applicazione hello esempio Arduino sulla Lavagna Arduino.

## <a name="what-you-need"></a>Elementi necessari
* Prima di iniziare questa attività, è necessario che sia completata [creare un'app di Azure (funzione) e un hub IoT tooprocess e l'archivio del account di archiviazione messaggi][process-and-store-iot-hub-messages].

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Ottenere le stringhe di connessione dell'hub IoT e del dispositivo
stringa di connessione dispositivo Hello è tooconnect usato l'hub IoT tooyour di Arduino Lavagna. stringa di connessione hub IoT Hello è usato tooconnect IoT hub toohello dispositivo identità che rappresenta il Arduino board nell'hub IoT hello.

* Elencare tutti gli hub IoT nel gruppo di risorse eseguendo il comando CLI di Azure seguente hello:

```bash
az iot hub list -g iot-sample --query [].name
```

Utilizzare `iot-sample` come valore hello `{resource group name}` se non si sono modificati valore hello.

* Ottenere una stringa di connessione hub IoT hello eseguendo hello comando CLI di Azure seguente:

```bash
az iot hub show-connection-string --name {my hub name}
```

`{my hub name}`è il nome hello è specificato durante la creazione dell'hub IoT e la Lavagna Arduino registrato.

* Ottenere una stringa di connessione del dispositivo hello eseguendo hello comando seguente:

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id mym0wifi
```

Utilizzare `mym0wifi` come valore hello `{device id}` se non si sono modificati valore hello.
## <a name="configure-hello-device-connection"></a>Configurare una connessione al dispositivo hello
tooconfigure hello connessione al dispositivo, seguire questi passaggi:

1. Ottenere della porta seriale del dispositivo hello con hello dispositivo individuazione cli hello:

   ```bash
   devdisco list --usb
   ```

   Si dovrebbe vedere un output simile toohello seguente e trovare hello usb porta COM per la scheda Arduino:

   ![Individuazione del dispositivo][device-discovery]

2. File aperti hello `config.json` in hello cartella lezione e aggiungere valore hello hello trovato numero di porta COM:

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > Per la porta COM hello, sulla piattaforma Windows, ha il formato di hello di `COM1, COM2, ...`. In macOS o Ubuntu inizia con `/dev/`.

3. Inizializzare i file di configurazione hello eseguendo hello seguenti comandi:

   ```bash
   npm install
   gulp init
   gulp install-tools
   ```
4. File di configurazione dispositivo aprire hello `config-arduino.json` nel codice di Visual Studio eseguendo hello comando seguente:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```

   ![config-arduino.json][config-arduino-json]

5. Rendere hello seguenti sostituzioni hello `config-arduino.json` file:

   * Sostituire **[Wi-Fi SSID]** con il SSID Wi-Fi che è connesso a Internet toohello.
   * Sostituire **[Wi-Fi password]** con la password Wi-Fi. Rimuovere la stringa hello se il Wi-Fi non richiede una password.
   * Sostituire **[stringa di connessione dispositivo IoT]** con hello `device connection string` ottenute.
   * Sostituire **[stringa di connessione hub IoT]** con hello `iot hub connection string` ottenute.

   > [!NOTE]
   > Non è necessario specificare `azure_storage_connection_string` in questo articolo. Mantenerlo invariato.

## <a name="deploy-and-run-hello-sample-application"></a>Distribuire ed eseguire l'applicazione di esempio hello
Distribuire ed eseguire l'applicazione di esempio hello sulla Lavagna Arduino eseguendo hello comando seguente:

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

> [!NOTE]
> Hello predefinito gulp attività viene eseguita `install-tools` e `run` in sequenza le attività. Quando si [hello blink app distribuita][deployed-the-blink-app], è stato eseguito queste operazioni separatamente.

## <a name="verify-that-hello-sample-application-works"></a>Verificare il funzionamento dell'applicazione di esempio hello
Dovrebbe essere hello GPIO #0 incorporata e LED lampeggia ogni due secondi. Ogni volta che hello LED è lampeggiante, applicazione di esempio hello invia un hub IoT tooyour di messaggio e verifica che il messaggio hello è stato inviato correttamente tooyour IoT hub. Inoltre, ogni messaggio ricevuto dall'hub IoT hello viene stampato nella finestra di console hello. applicazione di esempio Hello termina automaticamente dopo l'invio di 20 messaggi.

![Applicazione di esempio con messaggi inviati e ricevuti][sample-application-with-sent-and-received-messages]

## <a name="summary"></a>Riepilogo
È stato distribuito ed eseguito nuova applicazione di esempio blink hello in IoT hub di Arduino Lavagna toosend messaggi da dispositivo a cloud tooyour. È ora possibile monitorare i messaggi quando vengono scritti toohello account di archiviazione.

## <a name="next-steps"></a>Passaggi successivi
[Leggere i messaggi con salvataggio permanente in Archiviazione di Azure][read-messages-persisted-in-azure-storage]
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/config-arduino.png
[deployed-the-blink-app]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_run_arduino.png
[read-messages-persisted-in-azure-storage]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-read-table-storage.md