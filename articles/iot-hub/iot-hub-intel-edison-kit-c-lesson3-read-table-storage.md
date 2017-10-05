---
title: 'Connettere Intel Edison (C) ad Azure IoT: lezione 3: Monitorare i messaggi | Documentazione Microsoft'
description: Monitorare i messaggi da dispositivo a cloud mentre vengono scritti nell'archiviazione tabelle di Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: dati nel cloud, raccolta di dati cloud, servizio cloud IoT, dati IoT
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: cad545c3-dd88-486c-a663-d587a924ccd4
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 249b5e0e96051fa2adeedfb9befd98fc939b4d40
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="cb43e-104">Leggere i messaggi con salvataggio permanente in Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="cb43e-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="cb43e-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="cb43e-105">What you will do</span></span>
<span data-ttu-id="cb43e-106">Monitorare i messaggi da dispositivo a cloud che vengono inviati da Intel Edison all'hub IoT mentre vengono scritti nell'archivio tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="cb43e-106">Monitor the device-to-cloud messages that are sent from Intel Edison to your IoT hub as the messages are written to your Azure Table storage.</span></span> <span data-ttu-id="cb43e-107">In caso di problemi, cercare le soluzioni nella [pagina sulla risoluzione dei problemi][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="cb43e-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="cb43e-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="cb43e-108">What you will learn</span></span>
<span data-ttu-id="cb43e-109">Questo articolo illustra come usare l'attività gulp read-message per leggere i messaggi con salvataggio permanente nell'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="cb43e-109">In this article, you will learn how to use the gulp read-message task to read messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="cb43e-110">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="cb43e-110">What you need</span></span>
<span data-ttu-id="cb43e-111">Prima di avviare questo processo è necessario aver completato [Eseguire l'applicazione di esempio di Azure per il lampeggiamento in Intel Edison][run-the-azure-blink-sample-application-on-intel-edison].</span><span class="sxs-lookup"><span data-stu-id="cb43e-111">Before starting this process, you must have successfully completed [Run the Azure blink sample application on Intel Edison][run-the-azure-blink-sample-application-on-intel-edison].</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="cb43e-112">Leggere i nuovi messaggi dall'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="cb43e-112">Read new messages from your storage account</span></span>
<span data-ttu-id="cb43e-113">Nell'articolo precedente è stata eseguita un'applicazione di esempio in Edison.</span><span class="sxs-lookup"><span data-stu-id="cb43e-113">In the previous article, you ran a sample application on Edison.</span></span> <span data-ttu-id="cb43e-114">L'applicazione di esempio ha inviato messaggi all'hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="cb43e-114">The sample application sent messages to your Azure IoT hub.</span></span> <span data-ttu-id="cb43e-115">I messaggi inviati all'hub IoT vengono archiviati nell'archiviazione tabelle di Azure tramite l'app per le funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="cb43e-115">The messages sent to your IoT hub are stored into your Azure Table storage via the Azure function app.</span></span> <span data-ttu-id="cb43e-116">Per leggere i messaggi dall'archiviazione tabelle di Azure è necessaria la stringa di connessione di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="cb43e-116">You need the Azure storage connection string to read messages from your Azure Table storage.</span></span>

<span data-ttu-id="cb43e-117">Per leggere i messaggi nell'archiviazione tabelle di Azure, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="cb43e-117">To read messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="cb43e-118">Ottenere la stringa di connessione usando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="cb43e-118">Get the connection string by running the following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="cb43e-119">Il primo comando recupera il valore di `storage name` che viene usato nel secondo comando per ottenere la stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="cb43e-119">The first command retrieves the `storage name` that is used in the second command to get the connection string.</span></span> <span data-ttu-id="cb43e-120">Usare `iot-sample` come valore di `{resource group name}` se non si è modificato il valore.</span><span class="sxs-lookup"><span data-stu-id="cb43e-120">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>
2. <span data-ttu-id="cb43e-121">Aprire il file di configurazione `config-edison.json` in Visual Studio Code usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="cb43e-121">Open the configuration file `config-edison.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```
3. <span data-ttu-id="cb43e-122">Sostituire `[Azure storage connection string]` con la stringa di connessione ottenuta nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="cb43e-122">Replace `[Azure storage connection string]` with the connection string you got in step 1.</span></span>
4. <span data-ttu-id="cb43e-123">Salvare il file.`config-edison.json`</span><span class="sxs-lookup"><span data-stu-id="cb43e-123">Save the `config-edison.json` file.</span></span>
5. <span data-ttu-id="cb43e-124">Inviare nuovamente i messaggi e leggerli dall'archiviazione tabelle di Azure usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="cb43e-124">Send messages again and read them from your Azure Table storage by running the following command:</span></span>

   ```bash
   gulp run --read-storage
   ```

   <span data-ttu-id="cb43e-125">La logica per la lettura dall'archiviazione tabelle di Azure si trova nel file `azure-table.js`.</span><span class="sxs-lookup"><span data-stu-id="cb43e-125">The logic for reading from Azure Table storage is in the `azure-table.js` file.</span></span>

   ![gulp run --read-storage][gulp run]

## <a name="summary"></a><span data-ttu-id="cb43e-127">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="cb43e-127">Summary</span></span>
<span data-ttu-id="cb43e-128">È stato connesso Edison all'hub IoT nel cloud ed è stata usata l'applicazione di esempio per il lampeggiamento per inviare messaggi da dispositivo a cloud.</span><span class="sxs-lookup"><span data-stu-id="cb43e-128">You've successfully connected Edison to your IoT hub in the cloud and used the blink sample application to send device-to-cloud messages.</span></span> <span data-ttu-id="cb43e-129">È stata anche usata l'app per le funzioni di Azure per archiviare i messaggi in ingresso dell'hub IoT nell'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="cb43e-129">You also used the Azure function app to store incoming IoT hub messages to your Azure Table storage.</span></span> <span data-ttu-id="cb43e-130">È ora possibile inviare i messaggi da cloud a dispositivo dall'hub IoT a Edison.</span><span class="sxs-lookup"><span data-stu-id="cb43e-130">You can now send cloud-to-device messages from your IoT hub to Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb43e-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cb43e-131">Next steps</span></span>
<span data-ttu-id="cb43e-132">[Eseguire un'applicazione di esempio per ricevere messaggi da cloud a dispositivo][receive-cloud-to-device-messages]</span><span class="sxs-lookup"><span data-stu-id="cb43e-132">[Run a sample application to receive cloud-to-device messages][receive-cloud-to-device-messages]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[run-the-azure-blink-sample-application-on-intel-edison]: iot-hub-intel-edison-kit-c-lesson3-run-azure-blink.md
[gulp run]: media/iot-hub-intel-edison-lessons/lesson3/gulp_read_message_c.png
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-c-lesson4-send-cloud-to-device-messages.md