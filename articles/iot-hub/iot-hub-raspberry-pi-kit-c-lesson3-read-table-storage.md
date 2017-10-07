---
title: 'Connect Raspberry PI (C) tooAzure IoT - lezione 3: archivio tabelle | Documenti Microsoft'
description: Monitorare i messaggi da dispositivo a cloud hello man mano che vengono scritte tooyour archiviazione di tabelle di Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: recuperare dati dal cloud, servizio cloud iot
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 8c5558bb-3c31-4445-90e6-b1a978738545
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 307ce2bc595339790db7379cc011fe262c2b8734
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a>Leggere i messaggi con salvataggio permanente in Archiviazione di Azure
## <a name="what-you-will-do"></a>Contenuto dell'esercitazione
I messaggi da dispositivo a cloud monitoraggio hello inviati dall'hub IoT di tooyour Raspberry Pi 3 come messaggi hello vengono scritti tooyour archiviazione di tabelle di Azure. Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione
In questo articolo si apprenderà come messaggi tooread attività di lettura dei messaggi di toouse hello gulp persistente nell'archiviazione tabelle di Azure.

## <a name="what-you-need"></a>Elementi necessari
Prima di iniziare questo processo, è necessario avere completato correttamente [eseguire l'applicazione di esempio hello Azure blink Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson3-run-azure-blink.md).

## <a name="read-new-messages-from-your-storage-account"></a>Leggere i nuovi messaggi dall'account di archiviazione
Nell'articolo precedente hello, esecuzione di un'applicazione di esempio sulla Pi. applicazione di esempio Hello inviato hub IoT Azure tooyour di messaggi. messaggi hello inviati hub IoT tooyour vengono archiviati nell'archiviazione tabelle Azure tramite app di Azure funzione hello. Messaggi di tooread stringa di connessione di hello archiviazione di Azure è necessario dall'archivio tabelle di Azure.

i messaggi tooread archiviati nell'archiviazione tabelle di Azure, seguire questi passaggi:

1. Ottenere la stringa di connessione hello eseguendo hello seguenti comandi:

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   Hello primo comando Recupera hello `storage name` utilizzato nella stringa di hello secondo comando tooget hello connessione. Utilizzare `iot-sample` come valore hello `{resource group name}` se non si sono modificati valore hello.
2. File di configurazione Open hello `config-raspberrypi.json` nel codice di Visual Studio eseguendo hello comando seguente:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
3. Sostituire `[Azure storage connection string]` con stringa di connessione hello ottenuto nel passaggio 1.
4. Salvare hello `config-raspberrypi.json` file.
5. Inviare nuovamente i messaggi e leggerli dall'archivio tabelle di Azure eseguendo hello comando seguente:
   
   ```bash
   gulp run --read-storage
   ```
   
   Hello logica per la lettura dall'archiviazione tabelle di Azure è in hello `azure-table.js` file.
   
   ![gulp run --read-storage](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_read_message_c.png)

## <a name="summary"></a>Riepilogo
Siano correttamente connessi Pi tooyour IoT hub cloud hello e messaggi da dispositivo a cloud toosend di hello blink esempio applicazione utilizzata. Sono stati usati anche hello Azure funzione app toostore in ingresso IoT hub messaggi tooyour archiviazione tabelle di Azure. È ora possibile inviare messaggi da cloud a dispositivo dal tooPi hub IoT.

## <a name="next-steps"></a>Passaggi successivi
[Eseguire un tooreceive di applicazione di esempio i messaggi da cloud a dispositivo](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md)

