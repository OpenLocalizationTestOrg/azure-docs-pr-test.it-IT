---
title: 'Dispositivo SensorTag e gateway Azure IoT: lezione 4: Archivio tabelle | Documentazione Microsoft'
description: Salvare i messaggi dall'hub IoT di Intel NUC tooyour, scriverli archiviazione tabelle tooAzure e quindi leggerli dal cloud hello.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: recuperare dati dal cloud, servizio cloud iot
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 8ca78045-ad92-4a6a-90f1-05f9668e6f0e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 29525b084eb4d6e6dfcb16d9b34f78f075d30b7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-table-storage"></a>Leggere i messaggi con salvataggio permanente nell'archivio tabelle di Azure

## <a name="what-you-will-do"></a>Contenuto dell'esercitazione

- Eseguire l'applicazione di esempio hello gateway nel gateway che invia l'hub IoT tooyour messaggi.
- Eseguire quindi un codice di esempio in messaggi host computer tooread hello nell'archiviazione tabelle di Azure. 

Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione

Hello toouse gulp come strumento toorun hello codice tooread messaggi di esempio nell'archiviazione tabelle di Azure.

## <a name="what-you-need"></a>Elementi necessari

È stato hello quanto segue:

- [Creare app di Azure funzione hello e account di archiviazione di Azure hello](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md).
- [Eseguire l'applicazione di esempio hello gateway](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md).
- [Lettura di messaggi dall'hub IoT](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md).

## <a name="get-your-azure-storage-connection-strings"></a>Ottenere le stringhe di connessione di archiviazione di Azure

All'inizio di questa lezione è stato creato un account di archiviazione di Azure. stringa di connessione tooget hello dell'account di archiviazione di Azure hello, eseguire hello seguenti comandi:

* Elencare tutti gli account di archiviazione.

```bash
az storage account list -g iot-gateway --query [].name
```

* Ottenere la stringa di connessione di archiviazione di Azure.

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

Usare iot-gateway come valore hello `{resource group name}` se non si sono modificati valore hello nella lezione 2.

## <a name="configure-hello-device-connection"></a>Configurare una connessione al dispositivo hello

Hello aggiornamento `config-azure.json` file in modo che i codice di esempio hello in esecuzione nel computer host hello può leggere messaggio nell'archiviazione tabelle di Azure. tooconfigure hello connessione al dispositivo, seguire questi passaggi:

1. File di configurazione dispositivo aprire hello `config-azure.json` eseguendo hello seguenti comandi:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![configurazione](media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. Sostituire `[Azure storage connection string]` con hello stringa di connessione di archiviazione di Azure che è stato ottenuto.

   `[IoT hub connection string]` dovrebbe già essere stata sostituita nella sezione [Leggere messaggi dall'hub IoT di Azure](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md) della lezione 3.

## <a name="read-messages-in-your-azure-table-storage"></a>Leggere i messaggi nell'archivio tabelle di Azure

Eseguire l'applicazione di esempio gateway hello e leggere i messaggi di archiviazione di tabelle di Azure da hello comando seguente:

```bash
gulp run --table-storage
```

L'hub IoT attiva il messaggio di toosave applicazione Azure funzione nell'archiviazione tabelle Azure quando arriva un messaggio nuovo.
Hello `gulp run` comando esegue l'applicazione di esempio gateway che invia l'hub IoT tooyour messaggi. Con `table-storage` parametro, anche genera un hello tooreceive del processo figlio salvato messaggio nell'archiviazione tabelle di Azure.

messaggi Hello che vengono inviati e ricevuti sono tutti hello visualizzati immediatamente nella stessa finestra di console hello computer host. istanza di applicazione di esempio Hello verrà terminato automaticamente 40 secondi.

   ![Lettura gulp](media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table.png)


## <a name="summary"></a>Riepilogo

Eseguire i messaggi hello hello esempio codice tooread nell'archiviazione tabelle di Azure salvato dall'applicazione di funzione di Azure.
