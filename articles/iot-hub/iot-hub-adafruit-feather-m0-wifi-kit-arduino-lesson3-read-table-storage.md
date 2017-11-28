---
title: 'Connect Arduino (C) tooAzure IoT - lezione 3: archivio tabelle | Documenti Microsoft'
description: Monitorare i messaggi da dispositivo a cloud hello man mano che vengono scritte tooyour archiviazione di tabelle di Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: dati nel cloud hello, la raccolta dei dati cloud, servizio cloud iot, iot dati
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 386083e0-0dbb-48c0-9ac2-4f8fb4590772
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9fef18bc9e780e78d95f0c643a5f193125130a5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="c56cb-104">Leggere i messaggi con salvataggio permanente in Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="c56cb-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="c56cb-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="c56cb-105">What you will do</span></span>
<span data-ttu-id="c56cb-106">I messaggi da dispositivo a cloud monitoraggio hello inviato dall'hub IoT di Adafruit sfumatura M0 Wi-Fi Arduino Lavagna tooyour come messaggi hello vengono scritti tooyour archiviazione di tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="c56cb-106">Monitor hello device-to-cloud messages that are sent from your Adafruit Feather M0 WiFi Arduino board tooyour IoT hub as hello messages are written tooyour Azure Table storage.</span></span>

<span data-ttu-id="c56cb-107">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="c56cb-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c56cb-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="c56cb-108">What you will learn</span></span>
<span data-ttu-id="c56cb-109">In questo articolo si apprenderà come messaggi tooread attività di lettura dei messaggi di toouse hello gulp persistente nell'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="c56cb-109">In this article, you will learn how toouse hello gulp read-message task tooread messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c56cb-110">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="c56cb-110">What you need</span></span>
<span data-ttu-id="c56cb-111">Prima di iniziare questo processo, è necessario avere completato correttamente [eseguire l'applicazione di esempio hello Azure blink sulla Lavagna Arduino][run-blink-application].</span><span class="sxs-lookup"><span data-stu-id="c56cb-111">Before starting this process, you must have successfully completed [Run hello Azure blink sample application on your Arduino board][run-blink-application].</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="c56cb-112">Leggere i nuovi messaggi dall'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="c56cb-112">Read new messages from your storage account</span></span>
<span data-ttu-id="c56cb-113">Nell'articolo precedente hello, è stata eseguita un'applicazione di esempio sulla Lavagna Arduino.</span><span class="sxs-lookup"><span data-stu-id="c56cb-113">In hello previous article, you ran a sample application on your Arduino board.</span></span> <span data-ttu-id="c56cb-114">applicazione di esempio Hello inviato hub IoT Azure tooyour di messaggi.</span><span class="sxs-lookup"><span data-stu-id="c56cb-114">hello sample application sent messages tooyour Azure IoT hub.</span></span> <span data-ttu-id="c56cb-115">messaggi hello inviati hub IoT tooyour vengono archiviati nell'archiviazione tabelle Azure tramite app di Azure funzione hello.</span><span class="sxs-lookup"><span data-stu-id="c56cb-115">hello messages sent tooyour IoT hub are stored into your Azure Table storage via hello Azure function app.</span></span> <span data-ttu-id="c56cb-116">Messaggi di tooread stringa di connessione di hello archiviazione di Azure è necessario dall'archivio tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="c56cb-116">You need hello Azure storage connection string tooread messages from your Azure Table storage.</span></span>

<span data-ttu-id="c56cb-117">i messaggi tooread archiviati nell'archiviazione tabelle di Azure, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="c56cb-117">tooread messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="c56cb-118">Ottenere la stringa di connessione hello eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="c56cb-118">Get hello connection string by running hello following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="c56cb-119">Hello primo comando Recupera hello `storage name` utilizzato nella stringa di hello secondo comando tooget hello connessione.</span><span class="sxs-lookup"><span data-stu-id="c56cb-119">hello first command retrieves hello `storage name` that is used in hello second command tooget hello connection string.</span></span> <span data-ttu-id="c56cb-120">Utilizzare `iot-sample` come valore hello `{resource group name}` se non si sono modificati valore hello.</span><span class="sxs-lookup"><span data-stu-id="c56cb-120">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>
2. <span data-ttu-id="c56cb-121">File di configurazione Open hello `config-arduino.json` nel codice di Visual Studio eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c56cb-121">Open hello configuration file `config-arduino.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```
3. <span data-ttu-id="c56cb-122">Sostituire `[Azure storage connection string]` con stringa di connessione hello ottenuto nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="c56cb-122">Replace `[Azure storage connection string]` with hello connection string you got in step 1.</span></span>
4. <span data-ttu-id="c56cb-123">Salvare hello `config-arduino.json` file.</span><span class="sxs-lookup"><span data-stu-id="c56cb-123">Save hello `config-arduino.json` file.</span></span>
5. <span data-ttu-id="c56cb-124">Inviare nuovamente i messaggi e leggerli dall'archivio tabelle di Azure eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c56cb-124">Send messages again and read them from your Azure Table storage by running hello following command:</span></span>

   ```bash
   gulp run --read-storage

   # You can monitor hello serial port by running listen task:
   gulp listen

   # Or you can combine above two gulp tasks into one:
   gulp run --read-storage --listen
   ```

   <span data-ttu-id="c56cb-125">Hello logica per la lettura dall'archiviazione tabelle di Azure è in hello `azure-table.js` file.</span><span class="sxs-lookup"><span data-stu-id="c56cb-125">hello logic for reading from Azure Table storage is in hello `azure-table.js` file.</span></span>

   ![gulp run --read-storage][gulp-run]

## <a name="summary"></a><span data-ttu-id="c56cb-127">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="c56cb-127">Summary</span></span>
<span data-ttu-id="c56cb-128">Siano correttamente connessi hub IoT di Arduino Lavagna tooyour nel cloud hello e messaggi da dispositivo a cloud toosend di hello blink esempio applicazione utilizzata.</span><span class="sxs-lookup"><span data-stu-id="c56cb-128">You've successfully connected your Arduino board tooyour IoT hub in hello cloud and used hello blink sample application toosend device-to-cloud messages.</span></span> <span data-ttu-id="c56cb-129">Sono stati usati anche hello Azure funzione app toostore in ingresso IoT hub messaggi tooyour archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="c56cb-129">You also used hello Azure function app toostore incoming IoT hub messages tooyour Azure Table storage.</span></span> <span data-ttu-id="c56cb-130">È ora possibile inviare messaggi da cloud a dispositivo dal tooyour hub IoT Arduino Lavagna.</span><span class="sxs-lookup"><span data-stu-id="c56cb-130">You can now send cloud-to-device messages from your IoT hub tooyour Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c56cb-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c56cb-131">Next steps</span></span>
<span data-ttu-id="c56cb-132">[Inviare messaggi da cloud a dispositivo][send-cloud-to-device-messages]</span><span class="sxs-lookup"><span data-stu-id="c56cb-132">[Send cloud-to-device messages][send-cloud-to-device-messages]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[run-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md
[gulp-run]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_read_message_arduino.png
[send-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md