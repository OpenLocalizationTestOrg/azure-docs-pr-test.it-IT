---
title: 'Dispositivo simulato e gateway Azure IoT: lezione 4: Archivio tabelle | Documentazione Microsoft'
description: Salvare i messaggi da Intel NUC all'hub IoT, scriverli nell'archivio tabelle di Azure e quindi leggerli dal cloud.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: recuperare dati dal cloud, servizio cloud iot
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 78e4b6ea-968d-401e-a7dc-8f9acdb3ec1a
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: de5fae794c195132e2a487c0095845c756aa28e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="3282a-104">Leggere i messaggi con salvataggio permanente nell'archivio tabelle di Azure</span><span class="sxs-lookup"><span data-stu-id="3282a-104">Read messages persisted in Azure Table storage</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="3282a-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="3282a-105">What you will do</span></span>

- <span data-ttu-id="3282a-106">Eseguire l'applicazione di esempio gateway nel gateway che invia messaggi all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="3282a-106">Run the gateway sample application on your gateway that sends messages to your IoT hub.</span></span>
- <span data-ttu-id="3282a-107">Eseguire il codice di esempio nel computer host per leggere i messaggi nell'archivio tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="3282a-107">Run sample code on your host computer to read messages in your Azure Table storage.</span></span>

<span data-ttu-id="3282a-108">In caso di problemi, cercare le soluzioni nella pagina sulla [risoluzione dei problemi](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="3282a-108">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="3282a-109">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="3282a-109">What you will learn</span></span>

<span data-ttu-id="3282a-110">Come usare lo strumento gulp per eseguire il codice di esempio per leggere i messaggi nell'archivio tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="3282a-110">How to use the gulp tool to run the sample code to read messages in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3282a-111">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="3282a-111">What you need</span></span>

<span data-ttu-id="3282a-112">Sono state eseguite le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="3282a-112">You have have successfully done the following tasks:</span></span>

- <span data-ttu-id="3282a-113">[Creazione dell'app per le funzioni di Azure e dell'account di archiviazione di Azure](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="3282a-113">[Created the Azure function app and the Azure storage account](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md).</span></span>
- <span data-ttu-id="3282a-114">[Esecuzione dell'applicazione di esempio gateway](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span><span class="sxs-lookup"><span data-stu-id="3282a-114">[Run the gateway sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span></span>
- <span data-ttu-id="3282a-115">[Lettura di messaggi dall'hub IoT](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md).</span><span class="sxs-lookup"><span data-stu-id="3282a-115">[Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md).</span></span>

## <a name="get-your-azure-storage-connection-strings"></a><span data-ttu-id="3282a-116">Ottenere le stringhe di connessione di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="3282a-116">Get your Azure storage connection strings</span></span>

<span data-ttu-id="3282a-117">All'inizio di questa lezione è stato creato un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="3282a-117">Early in this lesson, you successfully created an Azure storage account.</span></span> <span data-ttu-id="3282a-118">Per ottenere la stringa di connessione dell'account di archiviazione di Azure, usare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3282a-118">To get the connection string of the Azure storage account, run the following commands:</span></span>

* <span data-ttu-id="3282a-119">Elencare tutti gli account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="3282a-119">List all your storage accounts.</span></span>

```bash
az storage account list -g iot-gateway --query [].name
```

* <span data-ttu-id="3282a-120">Ottenere la stringa di connessione di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="3282a-120">Get azure storage connection string.</span></span>

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

<span data-ttu-id="3282a-121">Usare `iot-gateway` come valore di `{resource group name}` se nella lezione 2 non si è modificato il valore.</span><span class="sxs-lookup"><span data-stu-id="3282a-121">Use `iot-gateway` as the value of `{resource group name}` if you didn't change the value in Lesson 2.</span></span>

## <a name="configure-the-device-connection"></a><span data-ttu-id="3282a-122">Configurare la connessione del dispositivo</span><span class="sxs-lookup"><span data-stu-id="3282a-122">Configure the device connection</span></span>

<span data-ttu-id="3282a-123">Aggiornare il file `config-azure.json` in modo che il codice di esempio eseguito nel computer host possa leggere i messaggi nell'archivio tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="3282a-123">Update the `config-azure.json` file so that the sample code that runs on the host computer can read message in your Azure Table storage.</span></span> <span data-ttu-id="3282a-124">Per configurare la connessione al dispositivo, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="3282a-124">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="3282a-125">Aprire il file di configurazione del dispositivo `config-azure.json` eseguendo questi comandi:</span><span class="sxs-lookup"><span data-stu-id="3282a-125">Open the device configuration file `config-azure.json` by running the following commands:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![configurazione](media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. <span data-ttu-id="3282a-127">Sostituire `[Azure storage connection string]` con la stringa di connessione di archiviazione di Azure ottenuta.</span><span class="sxs-lookup"><span data-stu-id="3282a-127">Replace `[Azure storage connection string]` with the Azure storage connection string that you obtained.</span></span>

   <span data-ttu-id="3282a-128">`[IoT hub connection string]` dovrebbe già essere stata sostituita nella sezione [Leggere messaggi dall'hub IoT di Azure](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md) della lezione 3.</span><span class="sxs-lookup"><span data-stu-id="3282a-128">`[IoT hub connection string]` should already be replaced in section [Read messages from Azure IoT Hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md) in Lesson3.</span></span>

## <a name="read-messages-in-your-azure-table-storage"></a><span data-ttu-id="3282a-129">Leggere i messaggi nell'archivio tabelle di Azure</span><span class="sxs-lookup"><span data-stu-id="3282a-129">Read messages in your Azure Table storage</span></span>

<span data-ttu-id="3282a-130">Eseguire l'applicazione di esempio gateway e leggere i messaggi usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="3282a-130">Run the gateway sample application and read Azure Table storage messages by the following command:</span></span>

```bash
gulp run --table-storage
```

<span data-ttu-id="3282a-131">L'hub IoT attiva l'applicazione per le funzioni di Azure per salvare il messaggio nell'archivio tabelle di Azure quando arriva il nuovo messaggio.</span><span class="sxs-lookup"><span data-stu-id="3282a-131">Your IoT hub triggers your Azure Function application to save message into your Azure Table storage when new message arrives.</span></span>
<span data-ttu-id="3282a-132">Il comando `gulp run` esegue l'applicazione di esempio gateway che invia i messaggi all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="3282a-132">The `gulp run` command runs gateway sample application that sends messages to your IoT hub.</span></span> <span data-ttu-id="3282a-133">Con il parametro `table-storage`, genera anche un processo figlio per ricevere il messaggio salvato nell'archivio tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="3282a-133">With `table-storage` parameter, it also spawns a child process to receive the saved message in your Azure Table storage.</span></span>

<span data-ttu-id="3282a-134">I messaggi inviati e ricevuti vengono visualizzati tutti immediatamente nella stessa finestra della console nel computer host.</span><span class="sxs-lookup"><span data-stu-id="3282a-134">The messages that are being sent and received are all displayed instantly on the same console window in the host machine.</span></span> <span data-ttu-id="3282a-135">L'istanza dell'applicazione di esempio terminerà automaticamente in 40 secondi.</span><span class="sxs-lookup"><span data-stu-id="3282a-135">The sample application instance will terminate automatically in 40 seconds.</span></span>

   ![Lettura gulp](media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table_simudev.png)


## <a name="summary"></a><span data-ttu-id="3282a-137">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="3282a-137">Summary</span></span>

<span data-ttu-id="3282a-138">È stato eseguito il codice di esempio per leggere i messaggi nell'archivio tabelle di Azure, salvati dall'applicazione per le funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="3282a-138">You've run the sample code to read the messages in your Azure Table storage saved by your Azure Function application.</span></span>
