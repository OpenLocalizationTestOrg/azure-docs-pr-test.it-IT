---
title: "Procedura dettagliata sull’acquisizione di Hub eventi di Azure | Documentazione Microsoft"
description: "Un esempio che usa l'SDK di Azure Python per illustrare l'uso della funzionalità di acquisizione dell'Hub eventi."
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
ms.openlocfilehash: a764a116755c20f60e92e553bd7c896425272b85
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="event-hubs-capture-walkthrough-python"></a><span data-ttu-id="4b78a-103">Procedura dettagliata sull'acquisizione di Hub eventi: Python</span><span class="sxs-lookup"><span data-stu-id="4b78a-103">Event Hubs Capture walkthrough: Python</span></span>

<span data-ttu-id="4b78a-104">Acquisisci è una nuova funzionalità di Hub eventi che consente di distribuire automaticamente i dati di streaming dell'hub eventi a un account di archiviazione BLOB di Azure di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="4b78a-104">Event Hubs Capture is a feature of Event Hubs that enables you to automatically deliver the streaming data in your event hub to an Azure Blob storage account of your choice.</span></span> <span data-ttu-id="4b78a-105">Questa capacità rende più semplice eseguire l'elaborazione di batch su dati di streaming in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="4b78a-105">This capability makes it easy to perform batch processing on real-time streaming data.</span></span> <span data-ttu-id="4b78a-106">In questo articolo viene descritto come usare l'acquisizione di Hub eventi con Python.</span><span class="sxs-lookup"><span data-stu-id="4b78a-106">This article describes how to use Event Hubs Capture with Python.</span></span> <span data-ttu-id="4b78a-107">Per altre informazioni sull'acquisizione di Hub eventi, vedere l' [articolo con la panoramica](event-hubs-archive-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4b78a-107">For more information about Event Hubs Capture, see the [overview article](event-hubs-archive-overview.md).</span></span>

<span data-ttu-id="4b78a-108">Questo esempio usa [Azure Python SDK](https://azure.microsoft.com/develop/python/) per illustrare la funzionalità di acquisizione.</span><span class="sxs-lookup"><span data-stu-id="4b78a-108">This sample uses the [Azure Python SDK](https://azure.microsoft.com/develop/python/) to demonstrate the Capture feature.</span></span> <span data-ttu-id="4b78a-109">Il programma sender.py invia una simulazione di telemetria ambientale a Hub eventi in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="4b78a-109">The sender.py program sends simulated environmental telemetry to Event Hubs in JSON format.</span></span> <span data-ttu-id="4b78a-110">L'hub eventi è configurato per usare la funzione Acquisisci per scrivere i dati nell'archiviazione BLOB in batch.</span><span class="sxs-lookup"><span data-stu-id="4b78a-110">The event hub is configured to use the Capture feature to write this data to blob storage in batches.</span></span> <span data-ttu-id="4b78a-111">L'app capturereader.py legge quindi questi BLOB, crea un file aggiuntivo per dispositivo, quindi scrive i dati in file con estensione csv.</span><span class="sxs-lookup"><span data-stu-id="4b78a-111">The capturereader.py app then reads these blobs and creates an append file per device, then writes the data into .csv files.</span></span>

## <a name="what-will-be-accomplished"></a><span data-ttu-id="4b78a-112">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="4b78a-112">What will be accomplished</span></span>

1. <span data-ttu-id="4b78a-113">Creazione di un account di archiviazione BLOB di Azure e di un contenitore BLOB all'interno nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4b78a-113">Create an Azure Blob Storage account and a blob container within it, using the Azure portal.</span></span>
2. <span data-ttu-id="4b78a-114">Creazione di uno spazio dei nomi di Hub eventi nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4b78a-114">Create an Event Hub namespace, using the Azure portal.</span></span>
3. <span data-ttu-id="4b78a-115">Creazione di un hub eventi con la funzione Acquisisci abilitata nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4b78a-115">Create an event hub with the Capture feature enabled, using the Azure portal.</span></span>
4. <span data-ttu-id="4b78a-116">Invio dei dati all'hub eventi con uno script Python.</span><span class="sxs-lookup"><span data-stu-id="4b78a-116">Send data to the event hub with a Python script.</span></span>
5. <span data-ttu-id="4b78a-117">Lettura dei file dall'acquisizione ed elaborazione con un altro script Python.</span><span class="sxs-lookup"><span data-stu-id="4b78a-117">Read the files from the capture and process them with another Python script.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b78a-118">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4b78a-118">Prerequisites</span></span>

- <span data-ttu-id="4b78a-119">Python 2.7.x</span><span class="sxs-lookup"><span data-stu-id="4b78a-119">Python 2.7.x</span></span>
- <span data-ttu-id="4b78a-120">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4b78a-120">An Azure subscription</span></span>
- <span data-ttu-id="4b78a-121">Uno [spazio dei nomi di Hub eventi attivo e hub eventi.](event-hubs-create.md)</span><span class="sxs-lookup"><span data-stu-id="4b78a-121">An active [Event Hubs namespace and event hub.](event-hubs-create.md)</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="4b78a-122">Creare un account di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="4b78a-122">Create an Azure Storage account</span></span>
1. <span data-ttu-id="4b78a-123">Accedere al [portale di Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="4b78a-123">Log on to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="4b78a-124">Nel riquadro di spostamento sinistro del portale fare clic su **Nuovo**, quindi su **Archiviazione** e quindi su **Account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="4b78a-124">In the left navigation pane of the portal, click **New**, then click **Storage**, and then click **Storage Account**.</span></span>
3. <span data-ttu-id="4b78a-125">Completare i campi nel pannello dell'account di archiviazione e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4b78a-125">Complete the fields in the storage account blade and then click **Create**.</span></span>
   
   ![][1]
4. <span data-ttu-id="4b78a-126">Dopo aver visualizzato il messaggio **Deployments Succeeded** (Le distribuzioni sono riuscite), fare clic sul nome del nuovo account di archiviazione e nel pannello **Informazioni di base** fare clic su **BLOB**.</span><span class="sxs-lookup"><span data-stu-id="4b78a-126">After you see the **Deployments Succeeded** message, click the name of the new storage account and in the **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="4b78a-127">Quando si apre il pannello **Servizio BLOB**, fare clic su **+ Contenitore** in alto.</span><span class="sxs-lookup"><span data-stu-id="4b78a-127">When the **Blob service** blade opens, click **+ Container** at the top.</span></span> <span data-ttu-id="4b78a-128">Assegnare al contenitore il nome **acquisizione**, quindi chiudere il pannello **Servizio BLOB**.</span><span class="sxs-lookup"><span data-stu-id="4b78a-128">Name the container **capture**, then close the **Blob service** blade.</span></span>
5. <span data-ttu-id="4b78a-129">Fare clic su **Chiavi di accesso** nel pannello sinistro e copiare il nome dell'account di archiviazione e il valore **key1**.</span><span class="sxs-lookup"><span data-stu-id="4b78a-129">Click **Access keys** in the left blade and copy the name of the storage account and the value of **key1**.</span></span> <span data-ttu-id="4b78a-130">Salvare questi valori nel Blocco note o in un'altra posizione temporanea.</span><span class="sxs-lookup"><span data-stu-id="4b78a-130">Save these values to Notepad or some other temporary location.</span></span>

## <a name="create-a-python-script-to-send-events-to-your-event-hub"></a><span data-ttu-id="4b78a-131">Creazione di uno script Python per inviare gli eventi all'hub eventi</span><span class="sxs-lookup"><span data-stu-id="4b78a-131">Create a Python script to send events to your event hub</span></span>
1. <span data-ttu-id="4b78a-132">Aprire l'editor preferito di Python, ad esempio[Visual Studio Code][Visual Studio Code].</span><span class="sxs-lookup"><span data-stu-id="4b78a-132">Open your favorite Python editor, such as [Visual Studio Code][Visual Studio Code].</span></span>
2. <span data-ttu-id="4b78a-133">Creare uno script chiamato **sender.py**.</span><span class="sxs-lookup"><span data-stu-id="4b78a-133">Create a script called **sender.py**.</span></span> <span data-ttu-id="4b78a-134">Questo script invia 200 eventi all'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="4b78a-134">This script sends 200 events to your event hub.</span></span> <span data-ttu-id="4b78a-135">Si tratta di semplici letture ambientali inviate in JSON.</span><span class="sxs-lookup"><span data-stu-id="4b78a-135">They are simple environmental readings sent in JSON.</span></span>
3. <span data-ttu-id="4b78a-136">Incollare il seguente codice in sender.py:</span><span class="sxs-lookup"><span data-stu-id="4b78a-136">Paste the following code into sender.py:</span></span>
   
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
4. <span data-ttu-id="4b78a-137">Aggiornare il codice precedente in modo che usi il nome dello spazio dei nomi, il valore chiave e il nome dell'hub eventi ottenuti al momento della creazione dello spazio dei nomi dell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="4b78a-137">Update the preceding code to use your namespace name, key value, and event hub name that you obtained when you created the Event Hubs namespace.</span></span>

## <a name="create-a-python-script-to-read-your-capture-files"></a><span data-ttu-id="4b78a-138">Creare uno script Python per leggere i file dell'acquisizione</span><span class="sxs-lookup"><span data-stu-id="4b78a-138">Create a Python script to read your Capture files</span></span>

1. <span data-ttu-id="4b78a-139">Compilare il pannello e fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4b78a-139">Fill out the blade and click **Create**.</span></span>
2. <span data-ttu-id="4b78a-140">Creare uno script chiamato **capturereader.py**.</span><span class="sxs-lookup"><span data-stu-id="4b78a-140">Create a script called **capturereader.py**.</span></span> <span data-ttu-id="4b78a-141">Questo script legge i file di acquisizione e crea un file per dispositivo in modo da scrivere i dati solo per quel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4b78a-141">This script reads the captured files and creates a file per device to write the data only for that device.</span></span>
3. <span data-ttu-id="4b78a-142">Incollare il seguente codice in capturereader.py:</span><span class="sxs-lookup"><span data-stu-id="4b78a-142">Paste the following code into capturereader.py:</span></span>
   
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
4. <span data-ttu-id="4b78a-143">Assicurarsi di incollare i valori appropriati per il nome e la chiave dell'account di archiviazione e nella chiamata a `startProcessing`.</span><span class="sxs-lookup"><span data-stu-id="4b78a-143">Be sure to paste the appropriate values for your storage account name and key in the call to `startProcessing`.</span></span>

## <a name="run-the-scripts"></a><span data-ttu-id="4b78a-144">Esecuzione degli script</span><span class="sxs-lookup"><span data-stu-id="4b78a-144">Run the scripts</span></span>
1. <span data-ttu-id="4b78a-145">Aprire un prompt dei comandi con un percorso contenente Python, quindi eseguire questi comandi per installare i pacchetti dei prerequisiti di Python:</span><span class="sxs-lookup"><span data-stu-id="4b78a-145">Open a command prompt that has Python in its path, and then run these commands to install Python prerequisite packages:</span></span>
   
  ```
  pip install azure-storage
  pip install azure-servicebus
  pip install avro
  ```
   
  <span data-ttu-id="4b78a-146">Se si dispone di una versione precedente di Azure o dell'archiviazione di Azure, potrebbe essere necessario usare l'opzione **aggiornamento**</span><span class="sxs-lookup"><span data-stu-id="4b78a-146">If you have an earlier version of either azure-storage or azure, you may need to use the **--upgrade** option</span></span>
   
  <span data-ttu-id="4b78a-147">Potrebbe inoltre essere necessario eseguire il comando seguente (non necessario nella maggior parte dei sistemi):</span><span class="sxs-lookup"><span data-stu-id="4b78a-147">You might also need to run the following (not necessary on most systems):</span></span>
   
  ```
  pip install cryptography
  ```
2. <span data-ttu-id="4b78a-148">Modificare la directory nel punto in cui sono stati salvati sender.py e capturereader.py ed eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="4b78a-148">Change your directory to wherever you saved sender.py and capturereader.py, and run this command:</span></span>
   
  ```
  start python sender.py
  ```
   
  <span data-ttu-id="4b78a-149">Questo comando avvia un nuovo processo di Python per eseguire il mittente.</span><span class="sxs-lookup"><span data-stu-id="4b78a-149">This command starts a new Python process to run the sender.</span></span>
3. <span data-ttu-id="4b78a-150">A questo punto attendere alcuni minuti per l'esecuzione dell'acquisizione.</span><span class="sxs-lookup"><span data-stu-id="4b78a-150">Now wait a few minutes for the capture to run.</span></span> <span data-ttu-id="4b78a-151">Digitare quindi il comando seguente nella finestra di comando originale:</span><span class="sxs-lookup"><span data-stu-id="4b78a-151">Then type the following command into your original command window:</span></span>
   
   ```
   python capturereader.py
   ```

   <span data-ttu-id="4b78a-152">Questo processore dell'acquisizione usa la directory locale per scaricare tutti i BLOB dal contenitore o dall'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4b78a-152">This capture processor uses the local directory to download all the blobs from the storage account/container.</span></span> <span data-ttu-id="4b78a-153">Vengono elaborati i BLOB non vuoti e i risultati vengono scritti come file con estensione csv nella directory locale.</span><span class="sxs-lookup"><span data-stu-id="4b78a-153">It processes any that are not empty, and writes the results as .csv files into the local directory.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b78a-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4b78a-154">Next steps</span></span>

<span data-ttu-id="4b78a-155">Per ulteriori informazioni su Hub eventi visitare i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="4b78a-155">You can learn more about Event Hubs by visiting the following links:</span></span>

* <span data-ttu-id="4b78a-156">[Panoramica dell'acquisizione di Hub eventi][Overview of Event Hubs Capture]</span><span class="sxs-lookup"><span data-stu-id="4b78a-156">[Overview of Event Hubs Capture][Overview of Event Hubs Capture]</span></span>
* <span data-ttu-id="4b78a-157">Un' [applicazione di esempio completa che usa Hub eventi][sample application that uses Event Hubs].</span><span class="sxs-lookup"><span data-stu-id="4b78a-157">A complete [sample application that uses Event Hubs][sample application that uses Event Hubs].</span></span>
* <span data-ttu-id="4b78a-158">Esempio relativo alla [scalabilità orizzontale dell'elaborazione di eventi con l'Hub eventi][Scale out Event Processing with Event Hubs].</span><span class="sxs-lookup"><span data-stu-id="4b78a-158">The [Scale out Event Processing with Event Hubs][Scale out Event Processing with Event Hubs] sample.</span></span>
* <span data-ttu-id="4b78a-159">[Panoramica di Hub eventi][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="4b78a-159">[Event Hubs overview][Event Hubs overview]</span></span>

[Azure portal]: https://portal.azure.com/
[Overview of Event Hubs Capture]: event-hubs-archive-overview.md
[1]: ./media/event-hubs-archive-python/event-hubs-python1.png
[About Azure storage accounts]:../storage/common/storage-create-storage-account.md
[Visual Studio Code]: https://code.visualstudio.com/
[Event Hubs overview]: event-hubs-overview.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
