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
# <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="42f17-104">Leggere i messaggi con salvataggio permanente nell'archivio tabelle di Azure</span><span class="sxs-lookup"><span data-stu-id="42f17-104">Read messages persisted in Azure Table storage</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="42f17-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="42f17-105">What you will do</span></span>

- <span data-ttu-id="42f17-106">Eseguire l'applicazione di esempio hello gateway nel gateway che invia l'hub IoT tooyour messaggi.</span><span class="sxs-lookup"><span data-stu-id="42f17-106">Run hello gateway sample application on your gateway that sends messages tooyour IoT hub.</span></span>
- <span data-ttu-id="42f17-107">Eseguire quindi un codice di esempio in messaggi host computer tooread hello nell'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="42f17-107">Then run a sample code on your host computer tooread hello messages in your Azure Table storage.</span></span> 

<span data-ttu-id="42f17-108">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="42f17-108">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="42f17-109">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="42f17-109">What you will learn</span></span>

<span data-ttu-id="42f17-110">Hello toouse gulp come strumento toorun hello codice tooread messaggi di esempio nell'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="42f17-110">How toouse hello gulp tool toorun hello sample code tooread messages in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="42f17-111">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="42f17-111">What you need</span></span>

<span data-ttu-id="42f17-112">È stato hello quanto segue:</span><span class="sxs-lookup"><span data-stu-id="42f17-112">You have have successfully done hello following tasks:</span></span>

- <span data-ttu-id="42f17-113">[Creare app di Azure funzione hello e account di archiviazione di Azure hello](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="42f17-113">[Created hello Azure function app and hello Azure storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md).</span></span>
- <span data-ttu-id="42f17-114">[Eseguire l'applicazione di esempio hello gateway](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md).</span><span class="sxs-lookup"><span data-stu-id="42f17-114">[Run hello gateway sample application](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md).</span></span>
- <span data-ttu-id="42f17-115">[Lettura di messaggi dall'hub IoT](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md).</span><span class="sxs-lookup"><span data-stu-id="42f17-115">[Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md).</span></span>

## <a name="get-your-azure-storage-connection-strings"></a><span data-ttu-id="42f17-116">Ottenere le stringhe di connessione di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="42f17-116">Get your Azure storage connection strings</span></span>

<span data-ttu-id="42f17-117">All'inizio di questa lezione è stato creato un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="42f17-117">Early in this lesson, you successfully created an Azure storage account.</span></span> <span data-ttu-id="42f17-118">stringa di connessione tooget hello dell'account di archiviazione di Azure hello, eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="42f17-118">tooget hello connection string of hello Azure storage account, run hello following commands:</span></span>

* <span data-ttu-id="42f17-119">Elencare tutti gli account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="42f17-119">List all your storage accounts.</span></span>

```bash
az storage account list -g iot-gateway --query [].name
```

* <span data-ttu-id="42f17-120">Ottenere la stringa di connessione di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="42f17-120">Get azure storage connection string.</span></span>

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

<span data-ttu-id="42f17-121">Usare iot-gateway come valore hello `{resource group name}` se non si sono modificati valore hello nella lezione 2.</span><span class="sxs-lookup"><span data-stu-id="42f17-121">Use iot-gateway as hello value of `{resource group name}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="configure-hello-device-connection"></a><span data-ttu-id="42f17-122">Configurare una connessione al dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="42f17-122">Configure hello device connection</span></span>

<span data-ttu-id="42f17-123">Hello aggiornamento `config-azure.json` file in modo che i codice di esempio hello in esecuzione nel computer host hello può leggere messaggio nell'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="42f17-123">Update hello `config-azure.json` file so that hello sample code that runs on hello host computer can read message in your Azure Table storage.</span></span> <span data-ttu-id="42f17-124">tooconfigure hello connessione al dispositivo, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="42f17-124">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="42f17-125">File di configurazione dispositivo aprire hello `config-azure.json` eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="42f17-125">Open hello device configuration file `config-azure.json` by running hello following commands:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![configurazione](media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. <span data-ttu-id="42f17-127">Sostituire `[Azure storage connection string]` con hello stringa di connessione di archiviazione di Azure che è stato ottenuto.</span><span class="sxs-lookup"><span data-stu-id="42f17-127">Replace `[Azure storage connection string]` with hello Azure storage connection string that you obtained.</span></span>

   <span data-ttu-id="42f17-128">`[IoT hub connection string]` dovrebbe già essere stata sostituita nella sezione [Leggere messaggi dall'hub IoT di Azure](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md) della lezione 3.</span><span class="sxs-lookup"><span data-stu-id="42f17-128">`[IoT hub connection string]` should already be replaced in section [Read messages from Azure IoT Hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md) in Lesson3.</span></span>

## <a name="read-messages-in-your-azure-table-storage"></a><span data-ttu-id="42f17-129">Leggere i messaggi nell'archivio tabelle di Azure</span><span class="sxs-lookup"><span data-stu-id="42f17-129">Read messages in your Azure Table storage</span></span>

<span data-ttu-id="42f17-130">Eseguire l'applicazione di esempio gateway hello e leggere i messaggi di archiviazione di tabelle di Azure da hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="42f17-130">Run hello gateway sample application and read Azure Table storage messages by hello following command:</span></span>

```bash
gulp run --table-storage
```

<span data-ttu-id="42f17-131">L'hub IoT attiva il messaggio di toosave applicazione Azure funzione nell'archiviazione tabelle Azure quando arriva un messaggio nuovo.</span><span class="sxs-lookup"><span data-stu-id="42f17-131">Your IoT hub triggers your Azure Function application toosave message into your Azure Table storage when new message arrives.</span></span>
<span data-ttu-id="42f17-132">Hello `gulp run` comando esegue l'applicazione di esempio gateway che invia l'hub IoT tooyour messaggi.</span><span class="sxs-lookup"><span data-stu-id="42f17-132">hello `gulp run` command runs gateway sample application that sends messages tooyour IoT hub.</span></span> <span data-ttu-id="42f17-133">Con `table-storage` parametro, anche genera un hello tooreceive del processo figlio salvato messaggio nell'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="42f17-133">With `table-storage` parameter, it also spawns a child process tooreceive hello saved message in your Azure Table storage.</span></span>

<span data-ttu-id="42f17-134">messaggi Hello che vengono inviati e ricevuti sono tutti hello visualizzati immediatamente nella stessa finestra di console hello computer host.</span><span class="sxs-lookup"><span data-stu-id="42f17-134">hello messages that are being sent and received are all displayed instantly on hello same console window in hello host machine.</span></span> <span data-ttu-id="42f17-135">istanza di applicazione di esempio Hello verrà terminato automaticamente 40 secondi.</span><span class="sxs-lookup"><span data-stu-id="42f17-135">hello sample application instance will terminate automatically in 40 seconds.</span></span>

   ![Lettura gulp](media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table.png)


## <a name="summary"></a><span data-ttu-id="42f17-137">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="42f17-137">Summary</span></span>

<span data-ttu-id="42f17-138">Eseguire i messaggi hello hello esempio codice tooread nell'archiviazione tabelle di Azure salvato dall'applicazione di funzione di Azure.</span><span class="sxs-lookup"><span data-stu-id="42f17-138">You've run hello sample code tooread hello messages in your Azure Table storage saved by your Azure Function application.</span></span>
