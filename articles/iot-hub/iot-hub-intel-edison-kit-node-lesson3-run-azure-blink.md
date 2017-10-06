---
title: 'Connettersi Edison Intel (nodo) tooAzure IoT - lezione 3: inviare messaggi | Documenti Microsoft'
description: Distribuire ed eseguire un tooIntel di applicazione di esempio Edison che invia l'hub IoT tooyour messaggi e lampeggia hello LED.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: servizio cloud IOT, arduino inviare dati toocloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 1b3b1074-f4d4-42ac-b32c-55f18b304b44
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ebd4c7558544d64086fb4cd615cee546aeed2fc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a><span data-ttu-id="cd4e5-104">Eseguire un toosend di applicazione di esempio i messaggi da dispositivo a cloud</span><span class="sxs-lookup"><span data-stu-id="cd4e5-104">Run a sample application toosend device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="cd4e5-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="cd4e5-105">What you will do</span></span>
<span data-ttu-id="cd4e5-106">In questo articolo verrà illustrato come toodeploy ed eseguire un'applicazione di esempio in Edison Intel che invia messaggi tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="cd4e5-106">This article will show you how toodeploy and run a sample application on Intel Edison that sends messages tooyour IoT hub.</span></span> <span data-ttu-id="cd4e5-107">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="cd4e5-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="cd4e5-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="cd4e5-108">What you will learn</span></span>
<span data-ttu-id="cd4e5-109">È verrà illustrato come hello toouse gulp toodeploy strumento ed eseguire un'applicazione hello esempio C nel Edison.</span><span class="sxs-lookup"><span data-stu-id="cd4e5-109">You will learn how toouse hello gulp tool toodeploy and run hello sample C application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="cd4e5-110">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="cd4e5-110">What you need</span></span>
* <span data-ttu-id="cd4e5-111">Prima di iniziare questa attività, è necessario che sia completata [creare un'app di Azure (funzione) e un hub IoT tooprocess e l'archivio del account di archiviazione messaggi][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="cd4e5-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="cd4e5-112">Ottenere le stringhe di connessione dell'hub IoT e del dispositivo</span><span class="sxs-lookup"><span data-stu-id="cd4e5-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="cd4e5-113">stringa di connessione del dispositivo Hello è tooconnect usato l'hub IoT tooyour Edison.</span><span class="sxs-lookup"><span data-stu-id="cd4e5-113">hello device connection string is used tooconnect Edison tooyour IoT hub.</span></span> <span data-ttu-id="cd4e5-114">stringa di connessione hub IoT Hello è usato tooconnect IoT hub toohello dispositivo identità rappresentata Edison nell'hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="cd4e5-114">hello IoT hub connection string is used tooconnect your IoT hub toohello device identity that represents Edison in hello IoT hub.</span></span>

* <span data-ttu-id="cd4e5-115">Elencare tutti gli hub IoT nel gruppo di risorse eseguendo il comando CLI di Azure seguente hello:</span><span class="sxs-lookup"><span data-stu-id="cd4e5-115">List all your IoT hubs in your resource group by running hello following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="cd4e5-116">Utilizzare `iot-sample` come valore hello `{resource group name}` se non si sono modificati valore hello.</span><span class="sxs-lookup"><span data-stu-id="cd4e5-116">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>

* <span data-ttu-id="cd4e5-117">Ottenere una stringa di connessione hub IoT hello eseguendo hello comando CLI di Azure seguente:</span><span class="sxs-lookup"><span data-stu-id="cd4e5-117">Get hello IoT hub connection string by running hello following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="cd4e5-118">`{my hub name}`è il nome hello specificato quando si della creazione dell'hub IoT ed Edison registrato.</span><span class="sxs-lookup"><span data-stu-id="cd4e5-118">`{my hub name}` is hello name that you specified when you created your IoT hub and registered Edison.</span></span>

* <span data-ttu-id="cd4e5-119">Ottenere una stringa di connessione del dispositivo hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="cd4e5-119">Get hello device connection string by running hello following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

<span data-ttu-id="cd4e5-120">Utilizzare `myinteledison` come valore hello `{device id}` se non si sono modificati valore hello.</span><span class="sxs-lookup"><span data-stu-id="cd4e5-120">Use `myinteledison` as hello value of `{device id}` if you didn't change hello value.</span></span>

## <a name="configure-hello-device-connection"></a><span data-ttu-id="cd4e5-121">Configurare una connessione al dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="cd4e5-121">Configure hello device connection</span></span>
1. <span data-ttu-id="cd4e5-122">Inizializzare i file di configurazione hello eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="cd4e5-122">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

2. <span data-ttu-id="cd4e5-123">File di configurazione dispositivo aprire hello `config-edison.json` nel codice di Visual Studio eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="cd4e5-123">Open hello device configuration file `config-edison.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![config.json](media/iot-hub-intel-edison-lessons/lesson3/config.png)
3. <span data-ttu-id="cd4e5-125">Rendere hello seguenti sostituzioni hello `config-edison.json` file:</span><span class="sxs-lookup"><span data-stu-id="cd4e5-125">Make hello following replacements in hello `config-edison.json` file:</span></span>

   * <span data-ttu-id="cd4e5-126">Sostituire **[nome host di dispositivo o indirizzo IP]** con indirizzo IP del dispositivo hello è contrassegnato come inattivo quando è stato configurato il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cd4e5-126">Replace **[device hostname or IP address]** with hello device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="cd4e5-127">Sostituire **[stringa di connessione dispositivo IoT]** con hello `device connection string` ottenute.</span><span class="sxs-lookup"><span data-stu-id="cd4e5-127">Replace **[IoT device connection string]** with hello `device connection string` you obtained.</span></span>
   * <span data-ttu-id="cd4e5-128">Sostituire **[stringa di connessione hub IoT]** con hello `iot hub connection string` ottenute.</span><span class="sxs-lookup"><span data-stu-id="cd4e5-128">Replace **[IoT hub connection string]** with hello `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cd4e5-129">Non è necessario specificare `azure_storage_connection_string` in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="cd4e5-129">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="cd4e5-130">Mantenerlo invariato.</span><span class="sxs-lookup"><span data-stu-id="cd4e5-130">Keep it as is.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="cd4e5-131">Distribuire ed eseguire l'applicazione di esempio hello</span><span class="sxs-lookup"><span data-stu-id="cd4e5-131">Deploy and run hello sample application</span></span>
<span data-ttu-id="cd4e5-132">Distribuire ed eseguire l'applicazione di esempio hello Edison eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="cd4e5-132">Deploy and run hello sample application on Edison by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a><span data-ttu-id="cd4e5-133">Verificare il funzionamento dell'applicazione di esempio hello</span><span class="sxs-lookup"><span data-stu-id="cd4e5-133">Verify that hello sample application works</span></span>
<span data-ttu-id="cd4e5-134">Dovrebbe essere hello LED che è connesso tooEdison lampeggiante ogni due secondi.</span><span class="sxs-lookup"><span data-stu-id="cd4e5-134">You should see hello LED that is connected tooEdison blinking every two seconds.</span></span> <span data-ttu-id="cd4e5-135">Ogni volta che hello LED è lampeggiante, applicazione di esempio hello invia un hub IoT tooyour di messaggio e verifica che il messaggio hello è stato inviato correttamente tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="cd4e5-135">Every time hello LED blinks, hello sample application sends a message tooyour IoT hub and verifies that hello message has been successfully sent tooyour IoT hub.</span></span> <span data-ttu-id="cd4e5-136">Inoltre, ogni messaggio ricevuto dall'hub IoT hello viene stampato nella finestra di console hello.</span><span class="sxs-lookup"><span data-stu-id="cd4e5-136">In addition, each message received by hello IoT hub is printed in hello console window.</span></span> <span data-ttu-id="cd4e5-137">applicazione di esempio Hello termina automaticamente dopo l'invio di 20 messaggi.</span><span class="sxs-lookup"><span data-stu-id="cd4e5-137">hello sample application terminates automatically after sending 20 messages.</span></span>

![Applicazione di esempio con messaggi inviati e ricevuti][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="cd4e5-139">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="cd4e5-139">Summary</span></span>
<span data-ttu-id="cd4e5-140">È stato distribuito ed eseguito nuova applicazione di esempio blink hello in Edison toosend l'hub IoT tooyour messaggi da dispositivo a cloud.</span><span class="sxs-lookup"><span data-stu-id="cd4e5-140">You've deployed and run hello new blink sample application on Edison toosend device-to-cloud messages tooyour IoT hub.</span></span> <span data-ttu-id="cd4e5-141">È ora possibile monitorare i messaggi quando vengono scritti toohello account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="cd4e5-141">You now monitor your messages as they are written toohello storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd4e5-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cd4e5-142">Next steps</span></span>
<span data-ttu-id="cd4e5-143">[Leggere i messaggi con salvataggio permanente in Archiviazione di Azure][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="cd4e5-143">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-intel-edison-lessons/lesson3/gulp_run.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-node-lesson3-read-table-storage.md