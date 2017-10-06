---
title: 'Dispositivo SensorTag e gateway Azure IoT: lezione 3: Leggere i messaggi | Documentazione Microsoft'
description: Eseguire un codice di esempio nei messaggi di hello tooread computer host dall'hub IoT.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: dati nel cloud hello, la raccolta dei dati cloud, servizio cloud iot, iot dati
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cc88be24-b5c0-4ef2-ba21-4e8f77f3e167
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d3ffbe2e83f9d61c0088b8876a7f0eea62c1fbe1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-from-your-iot-hub"></a>Leggere messaggi dall'hub IoT

## <a name="what-you-will-do"></a>Contenuto dell'esercitazione

- Eseguire il codice di esempio nell'host computer tooread messaggi dall'hub IoT.

Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione

Come toouse hello gulp messaggi tooread strumento dall'hub IoT.

## <a name="what-you-need"></a>Elementi necessari

- applicazione di esempio di tabella che è stato eseguito correttamente nella lezione 3 Hello.

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Ottenere le stringhe di connessione dell'hub IoT e del dispositivo

stringa di connessione del dispositivo Hello viene utilizzato per l'hub IoT tooyour tooconnect il dispositivo (TI SensorTag o dispositivo simulato). stringa di connessione hub IoT Hello è usato tooconnect toohello identità nel Registro di sistema i dispositivi IoT hub toomanage hello consentiti tooconnect tooyour IoT hub.

- Elencare tutti gli hub IoT nel gruppo di risorse eseguendo hello comando seguente:

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   Utilizzare `iot-gateway` come valore hello `{resource group name}` se non si sono modificati valore hello.
- Ottenere una stringa di connessione hub IoT hello eseguendo hello comando seguente:

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   `{my hub name}`è il nome hello specificato nella lezione 2.

## <a name="configure-hello-device-connection-for-hello-sample-code"></a>Configurare la connessione di hello dispositivo per il codice di esempio hello

File di configurazione dispositivo hello aggiornamento `config-azure.json` in modo che l'hub IoT è possibile leggere i messaggi nel computer host. toodo, seguire questi passaggi:

1. Aprire `config-azure.json` nel codice di Visual Studio eseguendo hello comando in una finestra della console seguente:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. Rendere hello seguenti sostituzioni hello `config-azure.json` file:

   ![screenshot di config azure](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   Sostituire `[IoT hub connection string]` con stringa di connessione hub IoT ottenuto hello.

## <a name="read-messages-from-your-iot-hub"></a>Leggere messaggi dall'hub IoT

Se si ha un dispositivo TI SensorTag, verificare di averlo già acceso. Eseguire l'applicazione di esempio gateway hello e leggere i messaggi di IoT Hub da hello comando seguente:

```bash
gulp run --iot-hub
```

comando Hello esegue hello Disattiva applicazione di esempio legge e i pacchetti di dati di temperatura dal dispositivo simulato o SensorTag e invia l'hub IoT tooyour messaggio hello ogni 2 secondi. Inoltre, genera un messaggio di hello tooreceive processo figlio.

messaggi Hello che vengono inviati e ricevuti sono tutti hello visualizzati immediatamente nella stessa finestra di console hello computer host. istanza di applicazione di esempio Hello verrà terminato automaticamente 40 secondi.

![Applicazione di esempio BLE con messaggi inviati e ricevuti](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub.png)

## <a name="summary"></a>Riepilogo

Aver eseguito un tooread codice di esempio i messaggi dall'hub IoT. Si è messaggi hello tooread pronto archiviati nell'archiviazione tabelle di Azure.

## <a name="next-steps"></a>Passaggi successivi
[Creare un'app per le funzioni di Azure e un account di Archiviazione di Azure](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)


