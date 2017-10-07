---
title: 'Connect Arduino (C) tooAzure IoT - lezione 3: archivio tabelle | Documenti Microsoft'
description: Monitorare i messaggi da dispositivo a cloud hello man mano che vengono scritte tooyour archiviazione di tabelle di Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: dati nel cloud hello, la raccolta dei dati cloud, servizio cloud iot, iot dati
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 386083e0-0dbb-48c0-9ac2-4f8fb4590772
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9fef18bc9e780e78d95f0c643a5f193125130a5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a>Leggere i messaggi con salvataggio permanente in Archiviazione di Azure
## <a name="what-you-will-do"></a>Contenuto dell'esercitazione
I messaggi da dispositivo a cloud monitoraggio hello inviato dall'hub IoT di Adafruit sfumatura M0 Wi-Fi Arduino Lavagna tooyour come messaggi hello vengono scritti tooyour archiviazione di tabelle di Azure.

Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina][troubleshooting].

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione
In questo articolo si apprenderà come messaggi tooread attività di lettura dei messaggi di toouse hello gulp persistente nell'archiviazione tabelle di Azure.

## <a name="what-you-need"></a>Elementi necessari
Prima di iniziare questo processo, è necessario avere completato correttamente [eseguire l'applicazione di esempio hello Azure blink sulla Lavagna Arduino][run-blink-application].

## <a name="read-new-messages-from-your-storage-account"></a>Leggere i nuovi messaggi dall'account di archiviazione
Nell'articolo precedente hello, è stata eseguita un'applicazione di esempio sulla Lavagna Arduino. applicazione di esempio Hello inviato hub IoT Azure tooyour di messaggi. messaggi hello inviati hub IoT tooyour vengono archiviati nell'archiviazione tabelle Azure tramite app di Azure funzione hello. Messaggi di tooread stringa di connessione di hello archiviazione di Azure è necessario dall'archivio tabelle di Azure.

i messaggi tooread archiviati nell'archiviazione tabelle di Azure, seguire questi passaggi:

1. Ottenere la stringa di connessione hello eseguendo hello seguenti comandi:

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   Hello primo comando Recupera hello `storage name` utilizzato nella stringa di hello secondo comando tooget hello connessione. Utilizzare `iot-sample` come valore hello `{resource group name}` se non si sono modificati valore hello.
2. File di configurazione Open hello `config-arduino.json` nel codice di Visual Studio eseguendo hello comando seguente:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```
3. Sostituire `[Azure storage connection string]` con stringa di connessione hello ottenuto nel passaggio 1.
4. Salvare hello `config-arduino.json` file.
5. Inviare nuovamente i messaggi e leggerli dall'archivio tabelle di Azure eseguendo hello comando seguente:

   ```bash
   gulp run --read-storage

   # You can monitor hello serial port by running listen task:
   gulp listen

   # Or you can combine above two gulp tasks into one:
   gulp run --read-storage --listen
   ```

   Hello logica per la lettura dall'archiviazione tabelle di Azure è in hello `azure-table.js` file.

   ![gulp run --read-storage][gulp-run]

## <a name="summary"></a>Riepilogo
Siano correttamente connessi hub IoT di Arduino Lavagna tooyour nel cloud hello e messaggi da dispositivo a cloud toosend di hello blink esempio applicazione utilizzata. Sono stati usati anche hello Azure funzione app toostore in ingresso IoT hub messaggi tooyour archiviazione tabelle di Azure. È ora possibile inviare messaggi da cloud a dispositivo dal tooyour hub IoT Arduino Lavagna.

## <a name="next-steps"></a>Passaggi successivi
[Inviare messaggi da cloud a dispositivo][send-cloud-to-device-messages]
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[run-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md
[gulp-run]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_read_message_arduino.png
[send-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md