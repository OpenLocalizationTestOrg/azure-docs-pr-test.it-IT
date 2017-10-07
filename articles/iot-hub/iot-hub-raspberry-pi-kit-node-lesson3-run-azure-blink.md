---
title: 'Connettersi Raspberry Pi (nodo) tooAzure IoT - lezione 3: eseguire l''esempio | Documenti Microsoft'
description: Distribuire ed eseguire un tooRaspberry di applicazione di esempio 3 Pi che invia l'hub IoT tooyour messaggi e lampeggia hello LED.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: lampeggiamento led cloud pi, lampeggiamento led dal cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 427d8e5e-8af8-4249-8607-44edc90a4972
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 991c64e0b1b6f965b029560cdc6403e557841e30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a>Eseguire un toosend di applicazione di esempio i messaggi da dispositivo a cloud
## <a name="what-you-will-do"></a>Contenuto dell'esercitazione
In questo articolo verrà illustrato come toodeploy ed eseguire un'applicazione di esempio 3 Pi Raspberry che invia messaggi tooyour IoT hub. Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione
Si apprenderà come hello toouse gulp toodeploy strumento e di eseguire un'applicazione hello esempio Node.js in Pi.

## <a name="what-you-need"></a>Elementi necessari
* Prima di iniziare questa attività, è necessario che sia completata [creare un'app di Azure (funzione) e un hub IoT tooprocess e l'archivio del account di archiviazione messaggi](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md).

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Ottenere le stringhe di connessione dell'hub IoT e del dispositivo
stringa di connessione del dispositivo Hello viene utilizzato per l'hub IoT di pi greco tooconnect tooyour. stringa di connessione hub IoT Hello è usato tooconnect toohello identità nel Registro di sistema i dispositivi IoT hub toomanage hello consentiti tooconnect tooyour IoT hub. 

* Elencare tutti gli hub IoT nel gruppo di risorse eseguendo il comando CLI di Azure seguente hello:

```bash
az iot hub list -g iot-sample --query [].name
```

Utilizzare `iot-sample` come valore hello `{resource group name}` se non si sono modificati valore hello.

* Ottenere una stringa di connessione hub IoT hello eseguendo hello comando CLI di Azure seguente:

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

`{my hub name}`è il nome hello specificato quando si della creazione dell'hub IoT e registrato Pi.

* Ottenere una stringa di connessione del dispositivo hello eseguendo hello comando seguente:

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

Utilizzare `myraspberrypi` come valore hello `{device id}` se non si sono modificati valore hello.

## <a name="configure-hello-device-connection"></a>Configurare una connessione al dispositivo hello
1. Inizializzare i file di configurazione hello eseguendo hello seguenti comandi:
   
   ```bash
   npm install
   gulp init
   ```
2. File di configurazione dispositivo aprire hello `config-raspberrypi.json` nel codice di Visual Studio eseguendo hello comando seguente:
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
  
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
  
   ![config.json](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. Rendere hello seguenti sostituzioni hello `config-raspberrypi.json` file:
   
   * Sostituire **[nome host di dispositivo o indirizzo IP]** con hello dispositivo IP indirizzo o il nome host è stato creato da `device-discovery-cli` o con valore hello ereditata durante la configurazione del dispositivo.
   * Sostituire **[stringa di connessione dispositivo IoT]** con hello `device connection string` ottenute.
   * Sostituire **[stringa di connessione hub IoT]** con hello `iot hub connection string` ottenute.

Hello aggiornamento `config-raspberrypi.json` file in modo che è possibile distribuire l'applicazione di esempio hello dal computer.

## <a name="deploy-and-run-hello-sample-application"></a>Distribuire ed eseguire l'applicazione di esempio hello
Distribuire ed eseguire l'applicazione di esempio hello Pi eseguendo hello comando seguente:

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a>Verificare il funzionamento dell'applicazione di esempio hello
Dovrebbe essere hello LED che è connesso tooPi lampeggiante ogni due secondi. Ogni volta che hello LED è lampeggiante, applicazione di esempio hello invia un hub IoT tooyour di messaggio e verifica che il messaggio hello è stato inviato correttamente tooyour IoT hub. Inoltre, ogni messaggio ricevuto dall'hub IoT hello viene stampato nella finestra di console hello. applicazione di esempio Hello termina automaticamente dopo l'invio di 20 messaggi.

![Applicazione di esempio con messaggi inviati e ricevuti](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run.png)

## <a name="summary"></a>Riepilogo
È stato distribuito ed eseguito nuova applicazione di esempio blink hello in hub IoT tooyour di pi greco toosend messaggi da dispositivo a cloud. È ora possibile monitorare i messaggi quando vengono scritti toohello account di archiviazione.

## <a name="next-steps"></a>Passaggi successivi
[Leggere i messaggi con salvataggio permanente in Archiviazione di Azure](iot-hub-raspberry-pi-kit-node-lesson3-read-table-storage.md)

