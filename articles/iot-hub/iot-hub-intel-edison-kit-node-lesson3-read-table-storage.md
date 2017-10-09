---
title: 'Connettersi Edison Intel (nodo) tooAzure IoT - lezione 3: monitorare messaggi | Documenti Microsoft'
description: Monitorare i messaggi da dispositivo a cloud hello man mano che vengono scritte tooyour archiviazione di tabelle di Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: dati nel cloud hello, la raccolta dei dati cloud, servizio cloud iot, iot dati
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: fa2c7efe-7e34-4e39-bb70-015c15ac69ed
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8f6371482123bc9aa12db55b38d3e8863645f981
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a>Leggere i messaggi con salvataggio permanente in Archiviazione di Azure
## <a name="what-you-will-do"></a>Contenuto dell'esercitazione
I messaggi da dispositivo a cloud monitoraggio hello inviati dall'hub IoT di Intel Edison tooyour come messaggi hello vengono scritti tooyour archiviazione tabelle di Azure. Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina][troubleshooting].

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione
In questo articolo si apprenderà come messaggi tooread attività di lettura dei messaggi di toouse hello gulp persistente nell'archiviazione tabelle di Azure.

## <a name="what-you-need"></a>Elementi necessari
Prima di iniziare questo processo, è necessario avere completato correttamente [eseguire l'applicazione di esempio hello Azure blink su Intel Edison][run-the-azure-blink-sample-application-on-intel-edison].

## <a name="read-new-messages-from-your-storage-account"></a>Leggere i nuovi messaggi dall'account di archiviazione
Nell'articolo precedente hello, esecuzione di un'applicazione di esempio sulla Edison. applicazione di esempio Hello inviato hub IoT Azure tooyour di messaggi. messaggi hello inviati hub IoT tooyour vengono archiviati nell'archiviazione tabelle Azure tramite app di Azure funzione hello. Messaggi di tooread stringa di connessione di hello archiviazione di Azure è necessario dall'archivio tabelle di Azure.

i messaggi tooread archiviati nell'archiviazione tabelle di Azure, seguire questi passaggi:

1. Ottenere la stringa di connessione hello eseguendo hello seguenti comandi:

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   Hello primo comando Recupera hello `storage name` utilizzato nella stringa di hello secondo comando tooget hello connessione. Utilizzare `iot-sample` come valore hello `{resource group name}` se non si sono modificati valore hello.
2. File di configurazione Open hello `config-edison.json` nel codice di Visual Studio eseguendo hello comando seguente:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```
3. Sostituire `[Azure storage connection string]` con stringa di connessione hello ottenuto nel passaggio 1.
4. Salvare hello `config-edison.json` file.
5. Inviare nuovamente i messaggi e leggerli dall'archivio tabelle di Azure eseguendo hello comando seguente:

   ```bash
   gulp run --read-storage
   ```

   Hello logica per la lettura dall'archiviazione tabelle di Azure è in hello `azure-table.js` file.

   ![gulp run --read-storage][gulp run]

## <a name="summary"></a>Riepilogo
Siano correttamente connessi l'hub IoT tooyour Edison nel cloud hello e messaggi da dispositivo a cloud toosend di hello blink esempio applicazione utilizzata. Sono stati usati anche hello Azure funzione app toostore in ingresso IoT hub messaggi tooyour archiviazione tabelle di Azure. È ora possibile inviare messaggi da cloud a dispositivo dal tooEdison hub IoT.

## <a name="next-steps"></a>Passaggi successivi
[Eseguire un tooreceive di applicazione di esempio i messaggi da cloud a dispositivo][receive-cloud-to-device-messages]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[run-the-azure-blink-sample-application-on-intel-edison]: iot-hub-intel-edison-kit-node-lesson3-run-azure-blink.md
[gulp run]: media/iot-hub-intel-edison-lessons/lesson3/gulp_read_message.png
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-node-lesson4-send-cloud-to-device-messages.md