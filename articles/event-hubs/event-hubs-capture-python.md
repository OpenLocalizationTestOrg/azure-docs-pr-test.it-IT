---
title: procedura dettagliata di acquisire gli hub di eventi aaaAzure | Documenti Microsoft
description: "Esempio che utilizza hello Azure SDK Python toodemonstrate funzionalità di acquisizione degli hub di eventi di hello."
services: event-hubs
documentationcenter: 
author: djrosanova
manager: timlt
editor: 
ms.assetid: bdff820c-5b38-4054-a06a-d1de207f01f6
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: darosa;sethm
ms.openlocfilehash: 1737dcca283711d863aa970db0e80ae71814e666
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-capture-walkthrough-python"></a>Procedura dettagliata sull'acquisizione di Hub eventi: Python

Acquisizione di hub eventi è una funzionalità degli hub di eventi che si tooautomatically consente di recapitare hello flusso di dati del tooan hub eventi account di archiviazione Blob di Azure di propria scelta. Questa funzionalità rende facile tooperform elaborazione batch su dati di streaming in tempo reale. Questo articolo descrive la modalità di acquisizione di hub eventi toouse con Python. Per ulteriori informazioni sull'acquisizione di hub eventi, vedere hello [articolo introduttivo](event-hubs-archive-overview.md).

In questo esempio utilizza hello [Python di Azure SDK](https://azure.microsoft.com/develop/python/) toodemonstrate la funzionalità di acquisizione hello. programma sender.py Hello invia telemetria ambiente simulato tooEvent hub in formato JSON. Hello hub eventi è configurato toouse hello acquisizione funzionalità toowrite questa archiviazione tooblob dei dati in batch. app capturereader.py Hello quindi legge tali BLOB viene creato un file di Accodamento per ogni dispositivo, quindi scrive i dati di hello in file con estensione csv.

## <a name="what-will-be-accomplished"></a>Contenuto dell'esercitazione

1. Creare un account di archiviazione Blob di Azure e un contenitore di blob in esso contenuti, tramite hello portale di Azure.
2. Creare uno spazio dei nomi di Hub eventi, utilizzando hello portale di Azure.
3. Creare un hub eventi con la funzionalità di acquisizione hello abilitata, mediante hello portale di Azure.
4. Hub di eventi toohello dati con uno script Python di trasmissione.
5. Lettura di file hello da acquisizione hello ed elaborarle con un altro script Python.

## <a name="prerequisites"></a>Prerequisiti

- Python 2.7.x
- Una sottoscrizione di Azure.
- Uno [spazio dei nomi di Hub eventi attivo e hub eventi.](event-hubs-create.md)

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="create-an-azure-storage-account"></a>Creare un account di Archiviazione di Azure
1. Accesso toohello [portale di Azure][Azure portal].
2. Nel riquadro di spostamento a sinistra di hello del portale di hello, fare clic su **New**, quindi fare clic su **archiviazione**, quindi fare clic su **Account di archiviazione**.
3. Completare i campi di hello nel Pannello di account di archiviazione hello e quindi fare clic su **crea**.
   
   ![][1]
4. Dopo aver visualizzato hello **ha avuto esito positivo di distribuzioni** messaggio, fare clic sul nome di hello del nuovo account di archiviazione hello in hello **Essentials** pannello, fare clic su **BLOB**. Quando hello **servizio Blob** fare clic su pannello **+ contenitore** nella parte superiore di hello. Contenitore con nome hello **acquisire**, quindi chiudere hello **servizio Blob** blade.
5. Fare clic su **le chiavi di accesso** hello sinistro blade e copia hello un nome dell'account di archiviazione hello e valore hello **key1**. Salvare queste tooNotepad valori o un'altra posizione temporanea.

## <a name="create-a-python-script-toosend-events-tooyour-event-hub"></a>Creare un hub di eventi tooyour Python script toosend eventi
1. Aprire l'editor preferito di Python, ad esempio[Visual Studio Code][Visual Studio Code].
2. Creare uno script chiamato **sender.py**. Questo script invia hub di eventi di 200 eventi tooyour. Si tratta di semplici letture ambientali inviate in JSON.
3. Incollare hello seguente di codice in sender.py:
   
  ```python
  import uuid
  import datetime
  import random
  import json
  from azure.servicebus import ServiceBusService
   
  sbs = ServiceBusService(service_namespace='INSERT YOUR NAMESPACE NAME', shared_access_key_name='RootManageSharedAccessKey', shared_access_key_value='INSERT YOUR KEY')
  devices = []
  for x in range(0, 10):
      devices.append(str(uuid.uuid4()))
   
  for y in range(0,20):
      for dev in devices:
          reading = {'id': dev, 'timestamp': str(datetime.datetime.utcnow()), 'uv': random.random(), 'temperature': random.randint(70, 100), 'humidity': random.randint(70, 100)}
          s = json.dumps(reading)
          sbs.send_event('INSERT YOUR EVENT HUB NAME', s)
      print y
  ```
4. Aggiornare hello precedente toouse codice il nome dello spazio dei nomi, valore della chiave e nome hub di eventi ottenuto al momento della creazione dello spazio dei nomi di hello hub eventi.

## <a name="create-a-python-script-tooread-your-capture-files"></a>Creare i file di acquisizione di un tooread script Python

1. Compilare il pannello hello e fare clic su **crea**.
2. Creare uno script chiamato **capturereader.py**. Questo script legge hello acquisiti i file e crea un file per i dati del dispositivo toowrite hello solo per quel dispositivo.
3. Incollare hello seguente di codice in capturereader.py:
   
  ```python
  import os
  import string
  import json
  import avro.schema
  from avro.datafile import DataFileReader, DataFileWriter
  from avro.io import DatumReader, DatumWriter
  from azure.storage.blob import BlockBlobService
   
  def processBlob(filename):
      reader = DataFileReader(open(filename, 'rb'), DatumReader())
      dict = {}
      for reading in reader:
          parsed_json = json.loads(reading["Body"])
          if not 'id' in parsed_json:
              return
          if not dict.has_key(parsed_json['id']):
              list = []
              dict[parsed_json['id']] = list
          else:
              list = dict[parsed_json['id']]
              list.append(parsed_json)
      reader.close()
      for device in dict.keys():
          deviceFile = open(device + '.csv', "a")
          for r in dict[device]:
              deviceFile.write(", ".join([str(r[x]) for x in r.keys()])+'\n')
   
  def startProcessing(accountName, key, container):
      print 'Processor started using path: ' + os.getcwd()
      block_blob_service = BlockBlobService(account_name=accountName, account_key=key)
      generator = block_blob_service.list_blobs(container)
      for blob in generator:
          if blob.properties.content_length != 0:
              print('Downloaded a non empty blob: ' + blob.name)
              cleanName = string.replace(blob.name, '/', '_')
              block_blob_service.get_blob_to_path(container, blob.name, cleanName)
              processBlob(cleanName)
              os.remove(cleanName)
          block_blob_service.delete_blob(container, blob.name)
  startProcessing('YOUR STORAGE ACCOUNT NAME', 'YOUR KEY', 'capture')
  ```
4. Essere toopaste che i valori appropriati di hello per il nome account di archiviazione e la chiave in hello chiamata troppo`startProcessing`.

## <a name="run-hello-scripts"></a>Eseguire gli script hello
1. Aprire un prompt dei comandi con Python nel percorso e quindi eseguire i pacchetti di prerequisiti Python tooinstall questi comandi:
   
  ```
  pip install azure-storage
  pip install azure-servicebus
  pip install avro
  ```
   
  Se si dispone di una versione precedente di archiviazione di azure o azure, potrebbe essere necessario hello toouse **-aggiornamento** opzione
   
  Potrebbe inoltre essere necessario toorun hello seguenti (non necessario nella maggior parte dei sistemi):
   
  ```
  pip install cryptography
  ```
2. Modificare la directory toowherever è stato salvato sender.py e capturereader.py ed eseguire questo comando:
   
  ```
  start python sender.py
  ```
   
  Questo comando avvia un nuovo mittente hello Python processo toorun.
3. Ora, attendere alcuni minuti toorun acquisizione hello. Digitare quindi hello comando seguente nella finestra del comando originale:
   
   ```
   python capturereader.py
   ```

   Questo processore acquisizione utilizza toodownload directory locale hello tutti i BLOB hello da account di archiviazione hello/contenitore. Elabora qualsiasi che non sono vuoti e scrive i risultati di hello come file con estensione csv in una directory locale hello.

## <a name="next-steps"></a>Passaggi successivi

Sono disponibili ulteriori informazioni sugli hub di eventi visitando hello seguenti collegamenti:

* [Panoramica dell'acquisizione di Hub eventi][Overview of Event Hubs Capture]
* Un' [applicazione di esempio completa che usa Hub eventi][sample application that uses Event Hubs].
* Hello [scalabilità l'elaborazione di eventi agli hub di eventi] [ Scale out Event Processing with Event Hubs] esempio.
* [Panoramica di Hub eventi][Event Hubs overview]

[Azure portal]: https://portal.azure.com/
[Overview of Event Hubs Capture]: event-hubs-archive-overview.md
[1]: ./media/event-hubs-archive-python/event-hubs-python1.png
[About Azure storage accounts]:../storage/common/storage-create-storage-account.md
[Visual Studio Code]: https://code.visualstudio.com/
[Event Hubs overview]: event-hubs-overview.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
