---
featureFlags: usabilla
title: 'Connettersi Raspberry Pi (nodo) tooAzure IoT - lezione 3: archivio tabelle | Documenti Microsoft'
description: Monitorare i messaggi da dispositivo a cloud hello man mano che vengono scritte tooyour archiviazione di tabelle di Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: recuperare dati dal cloud, servizio cloud iot
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 9965bd54-61da-479b-aaad-5604850a2be5
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d3c2c8086d3561b7603e18ed00492fcaa0593b87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="613cf-104">Leggere i messaggi con salvataggio permanente in Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="613cf-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="613cf-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="613cf-105">What you will do</span></span>
<span data-ttu-id="613cf-106">I messaggi da dispositivo a cloud monitoraggio hello inviati dall'hub IoT di tooyour Raspberry Pi 3 come messaggi hello vengono scritti tooyour archiviazione di tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="613cf-106">Monitor hello device-to-cloud messages that are sent from Raspberry Pi 3 tooyour IoT hub as hello messages are written tooyour Azure Table storage.</span></span> <span data-ttu-id="613cf-107">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="613cf-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="613cf-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="613cf-108">What you will learn</span></span>
<span data-ttu-id="613cf-109">In questo articolo si apprenderà come messaggi tooread attività di lettura dei messaggi di toouse hello gulp persistente nell'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="613cf-109">In this article, you will learn how toouse hello gulp read-message task tooread messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="613cf-110">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="613cf-110">What you need</span></span>
<span data-ttu-id="613cf-111">Prima di iniziare questo processo, è necessario avere completato correttamente [eseguire l'applicazione di esempio hello Azure blink Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md).</span><span class="sxs-lookup"><span data-stu-id="613cf-111">Before starting this process, you must have successfully completed [Run hello Azure blink sample application on Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md).</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="613cf-112">Leggere i nuovi messaggi dall'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="613cf-112">Read new messages from your storage account</span></span>
<span data-ttu-id="613cf-113">Nell'articolo precedente hello, esecuzione di un'applicazione di esempio sulla Pi.</span><span class="sxs-lookup"><span data-stu-id="613cf-113">In hello previous article, you ran a sample application on Pi.</span></span> <span data-ttu-id="613cf-114">applicazione di esempio Hello inviato hub IoT Azure tooyour di messaggi.</span><span class="sxs-lookup"><span data-stu-id="613cf-114">hello sample application sent messages tooyour Azure IoT hub.</span></span> <span data-ttu-id="613cf-115">messaggi hello inviati hub IoT tooyour vengono archiviati nell'archiviazione tabelle Azure tramite app di Azure funzione hello.</span><span class="sxs-lookup"><span data-stu-id="613cf-115">hello messages sent tooyour IoT hub are stored into your Azure Table storage via hello Azure function app.</span></span> <span data-ttu-id="613cf-116">Messaggi di tooread stringa di connessione di hello archiviazione di Azure è necessario dall'archivio tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="613cf-116">You need hello Azure storage connection string tooread messages from your Azure Table storage.</span></span>

<span data-ttu-id="613cf-117">i messaggi tooread archiviati nell'archiviazione tabelle di Azure, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="613cf-117">tooread messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="613cf-118">Ottenere la stringa di connessione hello eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="613cf-118">Get hello connection string by running hello following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="613cf-119">Hello primo comando Recupera hello `storage name` utilizzato nella stringa di hello secondo comando tooget hello connessione.</span><span class="sxs-lookup"><span data-stu-id="613cf-119">hello first command retrieves hello `storage name` that is used in hello second command tooget hello connection string.</span></span> <span data-ttu-id="613cf-120">Utilizzare `iot-sample` come valore hello `{resource group name}` se non si sono modificati valore hello.</span><span class="sxs-lookup"><span data-stu-id="613cf-120">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>
2. <span data-ttu-id="613cf-121">File di configurazione Open hello `config-raspberrypi.json` nel codice di Visual Studio eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="613cf-121">Open hello configuration file `config-raspberrypi.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
3. <span data-ttu-id="613cf-122">Sostituire `[Azure storage connection string]` con stringa di connessione hello ottenuto nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="613cf-122">Replace `[Azure storage connection string]` with hello connection string you got in step 1.</span></span>
4. <span data-ttu-id="613cf-123">Salvare hello `config-raspberrypi.json` file.</span><span class="sxs-lookup"><span data-stu-id="613cf-123">Save hello `config-raspberrypi.json` file.</span></span>
5. <span data-ttu-id="613cf-124">Inviare nuovamente i messaggi e leggerli dall'archivio tabelle di Azure eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="613cf-124">Send messages again and read them from your Azure Table storage by running hello following command:</span></span>
   
   ```bash
   gulp run --read-storage
   ```
   
   <span data-ttu-id="613cf-125">Hello logica per la lettura dall'archiviazione tabelle di Azure è in hello `azure-table.js` file.</span><span class="sxs-lookup"><span data-stu-id="613cf-125">hello logic for reading from Azure Table storage is in hello `azure-table.js` file.</span></span>
   
    ![gulp run --read-storage](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_read_message.png)

## <a name="summary"></a><span data-ttu-id="613cf-127">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="613cf-127">Summary</span></span>
<span data-ttu-id="613cf-128">Siano correttamente connessi Pi tooyour IoT hub cloud hello e messaggi da dispositivo a cloud toosend di hello blink esempio applicazione utilizzata.</span><span class="sxs-lookup"><span data-stu-id="613cf-128">You've successfully connected Pi tooyour IoT hub in hello cloud and used hello blink sample application toosend device-to-cloud messages.</span></span> <span data-ttu-id="613cf-129">Sono stati usati anche hello Azure funzione app toostore in ingresso IoT hub messaggi tooyour archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="613cf-129">You also used hello Azure function app toostore incoming IoT hub messages tooyour Azure Table storage.</span></span> <span data-ttu-id="613cf-130">È ora possibile inviare messaggi da cloud a dispositivo dal tooPi hub IoT.</span><span class="sxs-lookup"><span data-stu-id="613cf-130">You can now send cloud-to-device messages from your IoT hub tooPi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="613cf-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="613cf-131">Next steps</span></span>
[<span data-ttu-id="613cf-132">Eseguire i messaggi hello esempio applicazione tooreceive cloud a dispositivo</span><span class="sxs-lookup"><span data-stu-id="613cf-132">Run hello sample application tooreceive cloud-to-device messages</span></span>](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md)

