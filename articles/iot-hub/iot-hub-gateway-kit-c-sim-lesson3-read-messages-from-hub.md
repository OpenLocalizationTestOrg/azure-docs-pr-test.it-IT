---
title: 'Dispositivo simulato e gateway Azure IoT: lezione 3: Leggere i messaggi | Documentazione Microsoft'
description: Eseguire un codice di esempio nei messaggi di hello tooread computer host dall'hub IoT.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: dati nel cloud hello, la raccolta dei dati cloud, servizio cloud iot, iot dati
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5a6ec9c1-d83c-41c1-beaf-7c0d3395d77f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 540575724bb5cdac4db581a226d8a02a59004d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-from-your-iot-hub"></a>Leggere messaggi dall'hub IoT

## <a name="what-you-will-do"></a>Contenuto dell'esercitazione

- Eseguire il codice di esempio nell'host computer tooread messaggi dall'hub IoT.

Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione

Come toouse hello gulp messaggi tooread strumento dall'hub IoT.

## <a name="what-you-need"></a>Elementi necessari

- esempio di dispositivo simulato Hello in [configurare ed eseguire un cloud a dispositivo simulato caricare l'applicazione di esempio](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Ottenere le stringhe di connessione dell'hub IoT e del dispositivo

stringa di connessione del dispositivo Hello viene utilizzato per l'hub IoT tooyour tooconnect il dispositivo simulato. stringa di connessione hub IoT Hello è usato tooconnect toohello identità nel Registro di sistema i dispositivi IoT hub toomanage hello consentiti tooconnect tooyour IoT hub.

- Elencare tutti gli hub IoT nel gruppo di risorse eseguendo hello comando seguente:

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   Utilizzare `iot-gateway` come valore hello `{resource group name}` se non sono state modificate.
- Ottenere una stringa di connessione hub IoT hello eseguendo hello comando seguente:

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   `{my hub name}`è il nome hello specificato nella lezione 2.

## <a name="configure-hello-device-connection-for-hello-sample-code"></a>Configurare la connessione di hello dispositivo per il codice di esempio hello

Aggiornare le configurazioni di connessione hub e dispositivo di IoT in `config-azure.json` eseguendo hello alla procedura seguente:

1. Aprire `config-azure.json` nel codice di Visual Studio eseguendo hello comando in una finestra della console seguente:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. Rendere hello seguenti sostituzioni hello `config-azure.json` file:

   ![screenshot di config azure](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   Sostituire `[IoT hub connection string]` con stringa di connessione hub IoT hello.

## <a name="read-messages-from-your-iot-hub"></a>Leggere messaggi dall'hub IoT

Eseguire l'applicazione di esempio dispositivo simulato hello e leggere i messaggi di IoT Hub da hello comando seguente:

```bash
gulp run --iot-hub
```

comando Hello esegue un'applicazione hello che invia l'hub IoT tooyour messaggi ogni 2 secondi. Inoltre, genera un messaggio di hello tooreceive processo figlio.

messaggi Hello che vengono inviati e ricevuti sono tutti hello visualizzati immediatamente nella stessa finestra di console hello computer host. un'applicazione Hello 40 secondi verrà interrotto.

![Applicazione di esempio simulata con messaggi inviati e ricevuti](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub_simudev.png)

## <a name="summary"></a>Riepilogo

Hub IoT hello esempio applicazione toosend dati tooyour aver eseguito correttamente con dispositivo simulato. È inoltre stata leggere messaggi hello che sono stati inviati tooyour IoT hub.

## <a name="next-steps"></a>Passaggi successivi
[Creare un'app per le funzioni di Azure e un account di Archiviazione di Azure](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)


