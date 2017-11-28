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
# <a name="event-hubs-capture-walkthrough-python"></a><span data-ttu-id="25367-103">Procedura dettagliata sull'acquisizione di Hub eventi: Python</span><span class="sxs-lookup"><span data-stu-id="25367-103">Event Hubs Capture walkthrough: Python</span></span>

<span data-ttu-id="25367-104">Acquisizione di hub eventi è una funzionalità degli hub di eventi che si tooautomatically consente di recapitare hello flusso di dati del tooan hub eventi account di archiviazione Blob di Azure di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="25367-104">Event Hubs Capture is a feature of Event Hubs that enables you tooautomatically deliver hello streaming data in your event hub tooan Azure Blob storage account of your choice.</span></span> <span data-ttu-id="25367-105">Questa funzionalità rende facile tooperform elaborazione batch su dati di streaming in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="25367-105">This capability makes it easy tooperform batch processing on real-time streaming data.</span></span> <span data-ttu-id="25367-106">Questo articolo descrive la modalità di acquisizione di hub eventi toouse con Python.</span><span class="sxs-lookup"><span data-stu-id="25367-106">This article describes how toouse Event Hubs Capture with Python.</span></span> <span data-ttu-id="25367-107">Per ulteriori informazioni sull'acquisizione di hub eventi, vedere hello [articolo introduttivo](event-hubs-archive-overview.md).</span><span class="sxs-lookup"><span data-stu-id="25367-107">For more information about Event Hubs Capture, see hello [overview article](event-hubs-archive-overview.md).</span></span>

<span data-ttu-id="25367-108">In questo esempio utilizza hello [Python di Azure SDK](https://azure.microsoft.com/develop/python/) toodemonstrate la funzionalità di acquisizione hello.</span><span class="sxs-lookup"><span data-stu-id="25367-108">This sample uses hello [Azure Python SDK](https://azure.microsoft.com/develop/python/) toodemonstrate hello Capture feature.</span></span> <span data-ttu-id="25367-109">programma sender.py Hello invia telemetria ambiente simulato tooEvent hub in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="25367-109">hello sender.py program sends simulated environmental telemetry tooEvent Hubs in JSON format.</span></span> <span data-ttu-id="25367-110">Hello hub eventi è configurato toouse hello acquisizione funzionalità toowrite questa archiviazione tooblob dei dati in batch.</span><span class="sxs-lookup"><span data-stu-id="25367-110">hello event hub is configured toouse hello Capture feature toowrite this data tooblob storage in batches.</span></span> <span data-ttu-id="25367-111">app capturereader.py Hello quindi legge tali BLOB viene creato un file di Accodamento per ogni dispositivo, quindi scrive i dati di hello in file con estensione csv.</span><span class="sxs-lookup"><span data-stu-id="25367-111">hello capturereader.py app then reads these blobs and creates an append file per device, then writes hello data into .csv files.</span></span>

## <a name="what-will-be-accomplished"></a><span data-ttu-id="25367-112">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="25367-112">What will be accomplished</span></span>

1. <span data-ttu-id="25367-113">Creare un account di archiviazione Blob di Azure e un contenitore di blob in esso contenuti, tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="25367-113">Create an Azure Blob Storage account and a blob container within it, using hello Azure portal.</span></span>
2. <span data-ttu-id="25367-114">Creare uno spazio dei nomi di Hub eventi, utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="25367-114">Create an Event Hub namespace, using hello Azure portal.</span></span>
3. <span data-ttu-id="25367-115">Creare un hub eventi con la funzionalità di acquisizione hello abilitata, mediante hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="25367-115">Create an event hub with hello Capture feature enabled, using hello Azure portal.</span></span>
4. <span data-ttu-id="25367-116">Hub di eventi toohello dati con uno script Python di trasmissione.</span><span class="sxs-lookup"><span data-stu-id="25367-116">Send data toohello event hub with a Python script.</span></span>
5. <span data-ttu-id="25367-117">Lettura di file hello da acquisizione hello ed elaborarle con un altro script Python.</span><span class="sxs-lookup"><span data-stu-id="25367-117">Read hello files from hello capture and process them with another Python script.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25367-118">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="25367-118">Prerequisites</span></span>

- <span data-ttu-id="25367-119">Python 2.7.x</span><span class="sxs-lookup"><span data-stu-id="25367-119">Python 2.7.x</span></span>
- <span data-ttu-id="25367-120">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="25367-120">An Azure subscription</span></span>
- <span data-ttu-id="25367-121">Uno [spazio dei nomi di Hub eventi attivo e hub eventi.](event-hubs-create.md)</span><span class="sxs-lookup"><span data-stu-id="25367-121">An active [Event Hubs namespace and event hub.](event-hubs-create.md)</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="25367-122">Creare un account di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="25367-122">Create an Azure Storage account</span></span>
1. <span data-ttu-id="25367-123">Accesso toohello [portale di Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="25367-123">Log on toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="25367-124">Nel riquadro di spostamento a sinistra di hello del portale di hello, fare clic su **New**, quindi fare clic su **archiviazione**, quindi fare clic su **Account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="25367-124">In hello left navigation pane of hello portal, click **New**, then click **Storage**, and then click **Storage Account**.</span></span>
3. <span data-ttu-id="25367-125">Completare i campi di hello nel Pannello di account di archiviazione hello e quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="25367-125">Complete hello fields in hello storage account blade and then click **Create**.</span></span>
   
   ![][1]
4. <span data-ttu-id="25367-126">Dopo aver visualizzato hello **ha avuto esito positivo di distribuzioni** messaggio, fare clic sul nome di hello del nuovo account di archiviazione hello in hello **Essentials** pannello, fare clic su **BLOB**.</span><span class="sxs-lookup"><span data-stu-id="25367-126">After you see hello **Deployments Succeeded** message, click hello name of hello new storage account and in hello **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="25367-127">Quando hello **servizio Blob** fare clic su pannello **+ contenitore** nella parte superiore di hello.</span><span class="sxs-lookup"><span data-stu-id="25367-127">When hello **Blob service** blade opens, click **+ Container** at hello top.</span></span> <span data-ttu-id="25367-128">Contenitore con nome hello **acquisire**, quindi chiudere hello **servizio Blob** blade.</span><span class="sxs-lookup"><span data-stu-id="25367-128">Name hello container **capture**, then close hello **Blob service** blade.</span></span>
5. <span data-ttu-id="25367-129">Fare clic su **le chiavi di accesso** hello sinistro blade e copia hello un nome dell'account di archiviazione hello e valore hello **key1**.</span><span class="sxs-lookup"><span data-stu-id="25367-129">Click **Access keys** in hello left blade and copy hello name of hello storage account and hello value of **key1**.</span></span> <span data-ttu-id="25367-130">Salvare queste tooNotepad valori o un'altra posizione temporanea.</span><span class="sxs-lookup"><span data-stu-id="25367-130">Save these values tooNotepad or some other temporary location.</span></span>

## <a name="create-a-python-script-toosend-events-tooyour-event-hub"></a><span data-ttu-id="25367-131">Creare un hub di eventi tooyour Python script toosend eventi</span><span class="sxs-lookup"><span data-stu-id="25367-131">Create a Python script toosend events tooyour event hub</span></span>
1. <span data-ttu-id="25367-132">Aprire l'editor preferito di Python, ad esempio[Visual Studio Code][Visual Studio Code].</span><span class="sxs-lookup"><span data-stu-id="25367-132">Open your favorite Python editor, such as [Visual Studio Code][Visual Studio Code].</span></span>
2. <span data-ttu-id="25367-133">Creare uno script chiamato **sender.py**.</span><span class="sxs-lookup"><span data-stu-id="25367-133">Create a script called **sender.py**.</span></span> <span data-ttu-id="25367-134">Questo script invia hub di eventi di 200 eventi tooyour.</span><span class="sxs-lookup"><span data-stu-id="25367-134">This script sends 200 events tooyour event hub.</span></span> <span data-ttu-id="25367-135">Si tratta di semplici letture ambientali inviate in JSON.</span><span class="sxs-lookup"><span data-stu-id="25367-135">They are simple environmental readings sent in JSON.</span></span>
3. <span data-ttu-id="25367-136">Incollare hello seguente di codice in sender.py:</span><span class="sxs-lookup"><span data-stu-id="25367-136">Paste hello following code into sender.py:</span></span>
   
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
4. <span data-ttu-id="25367-137">Aggiornare hello precedente toouse codice il nome dello spazio dei nomi, valore della chiave e nome hub di eventi ottenuto al momento della creazione dello spazio dei nomi di hello hub eventi.</span><span class="sxs-lookup"><span data-stu-id="25367-137">Update hello preceding code toouse your namespace name, key value, and event hub name that you obtained when you created hello Event Hubs namespace.</span></span>

## <a name="create-a-python-script-tooread-your-capture-files"></a><span data-ttu-id="25367-138">Creare i file di acquisizione di un tooread script Python</span><span class="sxs-lookup"><span data-stu-id="25367-138">Create a Python script tooread your Capture files</span></span>

1. <span data-ttu-id="25367-139">Compilare il pannello hello e fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="25367-139">Fill out hello blade and click **Create**.</span></span>
2. <span data-ttu-id="25367-140">Creare uno script chiamato **capturereader.py**.</span><span class="sxs-lookup"><span data-stu-id="25367-140">Create a script called **capturereader.py**.</span></span> <span data-ttu-id="25367-141">Questo script legge hello acquisiti i file e crea un file per i dati del dispositivo toowrite hello solo per quel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="25367-141">This script reads hello captured files and creates a file per device toowrite hello data only for that device.</span></span>
3. <span data-ttu-id="25367-142">Incollare hello seguente di codice in capturereader.py:</span><span class="sxs-lookup"><span data-stu-id="25367-142">Paste hello following code into capturereader.py:</span></span>
   
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
4. <span data-ttu-id="25367-143">Essere toopaste che i valori appropriati di hello per il nome account di archiviazione e la chiave in hello chiamata troppo`startProcessing`.</span><span class="sxs-lookup"><span data-stu-id="25367-143">Be sure toopaste hello appropriate values for your storage account name and key in hello call too`startProcessing`.</span></span>

## <a name="run-hello-scripts"></a><span data-ttu-id="25367-144">Eseguire gli script hello</span><span class="sxs-lookup"><span data-stu-id="25367-144">Run hello scripts</span></span>
1. <span data-ttu-id="25367-145">Aprire un prompt dei comandi con Python nel percorso e quindi eseguire i pacchetti di prerequisiti Python tooinstall questi comandi:</span><span class="sxs-lookup"><span data-stu-id="25367-145">Open a command prompt that has Python in its path, and then run these commands tooinstall Python prerequisite packages:</span></span>
   
  ```
  pip install azure-storage
  pip install azure-servicebus
  pip install avro
  ```
   
  <span data-ttu-id="25367-146">Se si dispone di una versione precedente di archiviazione di azure o azure, potrebbe essere necessario hello toouse **-aggiornamento** opzione</span><span class="sxs-lookup"><span data-stu-id="25367-146">If you have an earlier version of either azure-storage or azure, you may need toouse hello **--upgrade** option</span></span>
   
  <span data-ttu-id="25367-147">Potrebbe inoltre essere necessario toorun hello seguenti (non necessario nella maggior parte dei sistemi):</span><span class="sxs-lookup"><span data-stu-id="25367-147">You might also need toorun hello following (not necessary on most systems):</span></span>
   
  ```
  pip install cryptography
  ```
2. <span data-ttu-id="25367-148">Modificare la directory toowherever è stato salvato sender.py e capturereader.py ed eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="25367-148">Change your directory toowherever you saved sender.py and capturereader.py, and run this command:</span></span>
   
  ```
  start python sender.py
  ```
   
  <span data-ttu-id="25367-149">Questo comando avvia un nuovo mittente hello Python processo toorun.</span><span class="sxs-lookup"><span data-stu-id="25367-149">This command starts a new Python process toorun hello sender.</span></span>
3. <span data-ttu-id="25367-150">Ora, attendere alcuni minuti toorun acquisizione hello.</span><span class="sxs-lookup"><span data-stu-id="25367-150">Now wait a few minutes for hello capture toorun.</span></span> <span data-ttu-id="25367-151">Digitare quindi hello comando seguente nella finestra del comando originale:</span><span class="sxs-lookup"><span data-stu-id="25367-151">Then type hello following command into your original command window:</span></span>
   
   ```
   python capturereader.py
   ```

   <span data-ttu-id="25367-152">Questo processore acquisizione utilizza toodownload directory locale hello tutti i BLOB hello da account di archiviazione hello/contenitore.</span><span class="sxs-lookup"><span data-stu-id="25367-152">This capture processor uses hello local directory toodownload all hello blobs from hello storage account/container.</span></span> <span data-ttu-id="25367-153">Elabora qualsiasi che non sono vuoti e scrive i risultati di hello come file con estensione csv in una directory locale hello.</span><span class="sxs-lookup"><span data-stu-id="25367-153">It processes any that are not empty, and writes hello results as .csv files into hello local directory.</span></span>

## <a name="next-steps"></a><span data-ttu-id="25367-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="25367-154">Next steps</span></span>

<span data-ttu-id="25367-155">Sono disponibili ulteriori informazioni sugli hub di eventi visitando hello seguenti collegamenti:</span><span class="sxs-lookup"><span data-stu-id="25367-155">You can learn more about Event Hubs by visiting hello following links:</span></span>

* <span data-ttu-id="25367-156">[Panoramica dell'acquisizione di Hub eventi][Overview of Event Hubs Capture]</span><span class="sxs-lookup"><span data-stu-id="25367-156">[Overview of Event Hubs Capture][Overview of Event Hubs Capture]</span></span>
* <span data-ttu-id="25367-157">Un' [applicazione di esempio completa che usa Hub eventi][sample application that uses Event Hubs].</span><span class="sxs-lookup"><span data-stu-id="25367-157">A complete [sample application that uses Event Hubs][sample application that uses Event Hubs].</span></span>
* <span data-ttu-id="25367-158">Hello [scalabilità l'elaborazione di eventi agli hub di eventi] [ Scale out Event Processing with Event Hubs] esempio.</span><span class="sxs-lookup"><span data-stu-id="25367-158">hello [Scale out Event Processing with Event Hubs][Scale out Event Processing with Event Hubs] sample.</span></span>
* <span data-ttu-id="25367-159">[Panoramica di Hub eventi][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="25367-159">[Event Hubs overview][Event Hubs overview]</span></span>

[Azure portal]: https://portal.azure.com/
[Overview of Event Hubs Capture]: event-hubs-archive-overview.md
[1]: ./media/event-hubs-archive-python/event-hubs-python1.png
[About Azure storage accounts]:../storage/common/storage-create-storage-account.md
[Visual Studio Code]: https://code.visualstudio.com/
[Event Hubs overview]: event-hubs-overview.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
