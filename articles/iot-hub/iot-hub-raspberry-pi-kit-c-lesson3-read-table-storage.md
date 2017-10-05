---
title: 'Connettere Raspberry Pi (C) ad Azure IoT: lezione 3: Archivio tabelle | Documentazione Microsoft'
description: Monitorare i messaggi da dispositivo a cloud mentre vengono scritti nell'archiviazione tabelle di Azure.
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
ms.openlocfilehash: 16b7f2e38bfe3b40d199cb6e07976433aa54ea32
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="a2698-104">Leggere i messaggi con salvataggio permanente in Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="a2698-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="a2698-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="a2698-105">What you will do</span></span>
<span data-ttu-id="a2698-106">Monitorare i messaggi da dispositivo a cloud che vengono inviati dal dispositivo Raspberry Pi 3 all'hub IoT mentre vengono scritti nell'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="a2698-106">Monitor the device-to-cloud messages that are sent from Raspberry Pi 3 to your IoT hub as the messages are written to your Azure Table storage.</span></span> <span data-ttu-id="a2698-107">In caso di problemi, cercare le soluzioni nella pagina sulla [risoluzione dei problemi](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="a2698-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a2698-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="a2698-108">What you will learn</span></span>
<span data-ttu-id="a2698-109">Questo articolo illustra come usare l'attività gulp read-message per leggere i messaggi con salvataggio permanente nell'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="a2698-109">In this article, you will learn how to use the gulp read-message task to read messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a2698-110">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="a2698-110">What you need</span></span>
<span data-ttu-id="a2698-111">Prima di avviare questo processo è necessario aver completato [Eseguire l'applicazione di esempio di Azure per il lampeggiamento nel dispositivo Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson3-run-azure-blink.md).</span><span class="sxs-lookup"><span data-stu-id="a2698-111">Before starting this process, you must have successfully completed [Run the Azure blink sample application on Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson3-run-azure-blink.md).</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="a2698-112">Leggere i nuovi messaggi dall'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="a2698-112">Read new messages from your storage account</span></span>
<span data-ttu-id="a2698-113">Nell'articolo precedente è stata eseguita un'applicazione di esempio sul dispositivo Pi.</span><span class="sxs-lookup"><span data-stu-id="a2698-113">In the previous article, you ran a sample application on Pi.</span></span> <span data-ttu-id="a2698-114">L'applicazione di esempio ha inviato messaggi all'hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="a2698-114">The sample application sent messages to your Azure IoT hub.</span></span> <span data-ttu-id="a2698-115">I messaggi inviati all'hub IoT vengono archiviati nell'archiviazione tabelle di Azure tramite l'app per le funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="a2698-115">The messages sent to your IoT hub are stored into your Azure Table storage via the Azure function app.</span></span> <span data-ttu-id="a2698-116">Per leggere i messaggi dall'archiviazione tabelle di Azure è necessaria la stringa di connessione di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a2698-116">You need the Azure storage connection string to read messages from your Azure Table storage.</span></span>

<span data-ttu-id="a2698-117">Per leggere i messaggi nell'archiviazione tabelle di Azure, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="a2698-117">To read messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="a2698-118">Ottenere la stringa di connessione usando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a2698-118">Get the connection string by running the following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="a2698-119">Il primo comando recupera il valore di `storage name` che viene usato nel secondo comando per ottenere la stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="a2698-119">The first command retrieves the `storage name` that is used in the second command to get the connection string.</span></span> <span data-ttu-id="a2698-120">Usare `iot-sample` come valore di `{resource group name}` se non si è modificato il valore.</span><span class="sxs-lookup"><span data-stu-id="a2698-120">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>
2. <span data-ttu-id="a2698-121">Aprire il file di configurazione `config-raspberrypi.json` in Visual Studio Code usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a2698-121">Open the configuration file `config-raspberrypi.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
3. <span data-ttu-id="a2698-122">Sostituire `[Azure storage connection string]` con la stringa di connessione ottenuta nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="a2698-122">Replace `[Azure storage connection string]` with the connection string you got in step 1.</span></span>
4. <span data-ttu-id="a2698-123">Salvare il file.`config-raspberrypi.json`</span><span class="sxs-lookup"><span data-stu-id="a2698-123">Save the `config-raspberrypi.json` file.</span></span>
5. <span data-ttu-id="a2698-124">Inviare nuovamente i messaggi e leggerli dall'archiviazione tabelle di Azure usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a2698-124">Send messages again and read them from your Azure Table storage by running the following command:</span></span>
   
   ```bash
   gulp run --read-storage
   ```
   
   <span data-ttu-id="a2698-125">La logica per la lettura dall'archiviazione tabelle di Azure si trova nel file `azure-table.js`.</span><span class="sxs-lookup"><span data-stu-id="a2698-125">The logic for reading from Azure Table storage is in the `azure-table.js` file.</span></span>
   
   ![gulp run --read-storage](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_read_message_c.png)

## <a name="summary"></a><span data-ttu-id="a2698-127">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="a2698-127">Summary</span></span>
<span data-ttu-id="a2698-128">È stato connesso il dispositivo Pi all'hub IoT nel cloud ed è stata usata l'applicazione di esempio per il lampeggiamento per inviare messaggi da dispositivo a cloud.</span><span class="sxs-lookup"><span data-stu-id="a2698-128">You've successfully connected Pi to your IoT hub in the cloud and used the blink sample application to send device-to-cloud messages.</span></span> <span data-ttu-id="a2698-129">È stata anche usata l'app per le funzioni di Azure per archiviare i messaggi in ingresso dell'hub IoT nell'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="a2698-129">You also used the Azure function app to store incoming IoT hub messages to your Azure Table storage.</span></span> <span data-ttu-id="a2698-130">È ora possibile inviare i messaggi da cloud a dispositivo dall'hub IoT al dispositivo Pi.</span><span class="sxs-lookup"><span data-stu-id="a2698-130">You can now send cloud-to-device messages from your IoT hub to Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2698-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a2698-131">Next steps</span></span>
[<span data-ttu-id="a2698-132">Eseguire un'applicazione di esempio per ricevere messaggi da cloud a dispositivo</span><span class="sxs-lookup"><span data-stu-id="a2698-132">Run a sample application to receive cloud-to-device messages</span></span>](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md)

