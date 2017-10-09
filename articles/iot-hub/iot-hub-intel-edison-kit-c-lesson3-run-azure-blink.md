---
title: 'Connect Intel Edison (C) tooAzure IoT - lezione 3: inviare messaggi | Documenti Microsoft'
description: Distribuire ed eseguire un tooIntel di applicazione di esempio Edison che invia l'hub IoT tooyour messaggi e lampeggia hello LED.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: servizio cloud IOT, arduino inviare dati toocloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 12672b64-795a-4dfc-86fd-df53ed3eeef7
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 83615335027cc792b89d3894578fc3f7a55e5c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a>Eseguire un toosend di applicazione di esempio i messaggi da dispositivo a cloud
## <a name="what-you-will-do"></a>Contenuto dell'esercitazione
In questo articolo verrà illustrato come toodeploy ed eseguire un'applicazione di esempio in Edison Intel che invia messaggi tooyour IoT hub. Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina][troubleshooting].

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione
È verrà illustrato come hello toouse gulp toodeploy strumento ed eseguire un'applicazione hello esempio C nel Edison.

## <a name="what-you-need"></a>Elementi necessari
* Prima di iniziare questa attività, è necessario che sia completata [creare un'app di Azure (funzione) e un hub IoT tooprocess e l'archivio del account di archiviazione messaggi][process-and-store-iot-hub-messages].

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Ottenere le stringhe di connessione dell'hub IoT e del dispositivo
stringa di connessione del dispositivo Hello è tooconnect usato l'hub IoT tooyour Edison. stringa di connessione hub IoT Hello è usato tooconnect IoT hub toohello dispositivo identità rappresentata Edison nell'hub IoT hello.

* Elencare tutti gli hub IoT nel gruppo di risorse eseguendo il comando CLI di Azure seguente hello:

```bash
az iot hub list -g iot-sample --query [].name
```

Utilizzare `iot-sample` come valore hello `{resource group name}` se non si sono modificati valore hello.

* Ottenere una stringa di connessione hub IoT hello eseguendo hello comando CLI di Azure seguente:

```bash
az iot hub show-connection-string --name {my hub name}
```

`{my hub name}`è il nome hello specificato quando si della creazione dell'hub IoT ed Edison registrato.

* Ottenere una stringa di connessione del dispositivo hello eseguendo hello comando seguente:

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

Utilizzare `myinteledison` come valore hello `{device id}` se non si sono modificati valore hello.

## <a name="configure-hello-device-connection"></a>Configurare una connessione al dispositivo hello
1. Inizializzare i file di configurazione hello eseguendo hello seguenti comandi:

   ```bash
   npm install
   gulp init
   ```
   > [!NOTE]
   > Se non è stato fatto nella lezione 1, eseguire anche il comando **gulp install-tools**.

2. File di configurazione dispositivo aprire hello `config-edison.json` nel codice di Visual Studio eseguendo hello comando seguente:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![config.json](media/iot-hub-intel-edison-lessons/lesson3/config.png)

3. Rendere hello seguenti sostituzioni hello `config-edison.json` file:

   * Sostituire **[nome host di dispositivo o indirizzo IP]** con indirizzo IP del dispositivo hello è contrassegnato come inattivo quando è stato configurato il dispositivo.
   * Sostituire **[stringa di connessione dispositivo IoT]** con hello `device connection string` ottenute.
   * Sostituire **[stringa di connessione hub IoT]** con hello `iot hub connection string` ottenute.

   > [!NOTE]
   > Non è necessario specificare `azure_storage_connection_string` in questo articolo. Mantenerlo invariato.

## <a name="deploy-and-run-hello-sample-application"></a>Distribuire ed eseguire l'applicazione di esempio hello
Distribuire ed eseguire l'applicazione di esempio hello Edison eseguendo hello comando seguente:

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a>Verificare il funzionamento dell'applicazione di esempio hello
Dovrebbe essere hello LED che è connesso tooEdison lampeggiante ogni due secondi. Ogni volta che hello LED è lampeggiante, applicazione di esempio hello invia un hub IoT tooyour di messaggio e verifica che il messaggio hello è stato inviato correttamente tooyour IoT hub. Inoltre, ogni messaggio ricevuto dall'hub IoT hello viene stampato nella finestra di console hello. applicazione di esempio Hello termina automaticamente dopo l'invio di 20 messaggi.

![Applicazione di esempio con messaggi inviati e ricevuti][sample-application-with-sent-and-received-messages]

## <a name="summary"></a>Riepilogo
È stato distribuito ed eseguito nuova applicazione di esempio blink hello in Edison toosend l'hub IoT tooyour messaggi da dispositivo a cloud. È ora possibile monitorare i messaggi quando vengono scritti toohello account di archiviazione.

## <a name="next-steps"></a>Passaggi successivi
[Leggere i messaggi con salvataggio permanente in Archiviazione di Azure][read-messages-persisted-in-azure-storage]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-intel-edison-lessons/lesson3/gulp_run_c.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-c-lesson3-read-table-storage.md