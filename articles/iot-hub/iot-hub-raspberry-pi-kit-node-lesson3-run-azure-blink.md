---
title: 'Connettersi Raspberry Pi (nodo) tooAzure IoT - lezione 3: eseguire l''esempio | Documenti Microsoft'
description: Distribuire ed eseguire un tooRaspberry di applicazione di esempio 3 Pi che invia l'hub IoT tooyour messaggi e lampeggia hello LED.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: lampeggiamento led cloud pi, lampeggiamento led dal cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 427d8e5e-8af8-4249-8607-44edc90a4972
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 991c64e0b1b6f965b029560cdc6403e557841e30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a><span data-ttu-id="df244-104">Eseguire un toosend di applicazione di esempio i messaggi da dispositivo a cloud</span><span class="sxs-lookup"><span data-stu-id="df244-104">Run a sample application toosend device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="df244-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="df244-105">What you will do</span></span>
<span data-ttu-id="df244-106">In questo articolo verrà illustrato come toodeploy ed eseguire un'applicazione di esempio 3 Pi Raspberry che invia messaggi tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="df244-106">This article will show you how toodeploy and run a sample application on Raspberry Pi 3 that sends messages tooyour IoT hub.</span></span> <span data-ttu-id="df244-107">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="df244-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="df244-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="df244-108">What you will learn</span></span>
<span data-ttu-id="df244-109">Si apprenderà come hello toouse gulp toodeploy strumento e di eseguire un'applicazione hello esempio Node.js in Pi.</span><span class="sxs-lookup"><span data-stu-id="df244-109">You will learn how toouse hello gulp tool toodeploy and run hello sample Node.js application on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="df244-110">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="df244-110">What you need</span></span>
* <span data-ttu-id="df244-111">Prima di iniziare questa attività, è necessario che sia completata [creare un'app di Azure (funzione) e un hub IoT tooprocess e l'archivio del account di archiviazione messaggi](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="df244-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account tooprocess and store IoT hub messages](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="df244-112">Ottenere le stringhe di connessione dell'hub IoT e del dispositivo</span><span class="sxs-lookup"><span data-stu-id="df244-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="df244-113">stringa di connessione del dispositivo Hello viene utilizzato per l'hub IoT di pi greco tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="df244-113">hello device connection string is used by your Pi tooconnect tooyour IoT hub.</span></span> <span data-ttu-id="df244-114">stringa di connessione hub IoT Hello è usato tooconnect toohello identità nel Registro di sistema i dispositivi IoT hub toomanage hello consentiti tooconnect tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="df244-114">hello IoT hub connection string is used tooconnect toohello identity registry in your IoT hub toomanage hello devices that are allowed tooconnect tooyour IoT hub.</span></span> 

* <span data-ttu-id="df244-115">Elencare tutti gli hub IoT nel gruppo di risorse eseguendo il comando CLI di Azure seguente hello:</span><span class="sxs-lookup"><span data-stu-id="df244-115">List all your IoT hubs in your resource group by running hello following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="df244-116">Utilizzare `iot-sample` come valore hello `{resource group name}` se non si sono modificati valore hello.</span><span class="sxs-lookup"><span data-stu-id="df244-116">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>

* <span data-ttu-id="df244-117">Ottenere una stringa di connessione hub IoT hello eseguendo hello comando CLI di Azure seguente:</span><span class="sxs-lookup"><span data-stu-id="df244-117">Get hello IoT hub connection string by running hello following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

<span data-ttu-id="df244-118">`{my hub name}`è il nome hello specificato quando si della creazione dell'hub IoT e registrato Pi.</span><span class="sxs-lookup"><span data-stu-id="df244-118">`{my hub name}` is hello name that you specified when you created your IoT hub and registered Pi.</span></span>

* <span data-ttu-id="df244-119">Ottenere una stringa di connessione del dispositivo hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="df244-119">Get hello device connection string by running hello following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

<span data-ttu-id="df244-120">Utilizzare `myraspberrypi` come valore hello `{device id}` se non si sono modificati valore hello.</span><span class="sxs-lookup"><span data-stu-id="df244-120">Use `myraspberrypi` as hello value of `{device id}` if you didn't change hello value.</span></span>

## <a name="configure-hello-device-connection"></a><span data-ttu-id="df244-121">Configurare una connessione al dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="df244-121">Configure hello device connection</span></span>
1. <span data-ttu-id="df244-122">Inizializzare i file di configurazione hello eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="df244-122">Initialize hello configuration file by running hello following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```
2. <span data-ttu-id="df244-123">File di configurazione dispositivo aprire hello `config-raspberrypi.json` nel codice di Visual Studio eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="df244-123">Open hello device configuration file `config-raspberrypi.json` in Visual Studio Code by running hello following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
  
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
  
   ![config.json](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. <span data-ttu-id="df244-125">Rendere hello seguenti sostituzioni hello `config-raspberrypi.json` file:</span><span class="sxs-lookup"><span data-stu-id="df244-125">Make hello following replacements in hello `config-raspberrypi.json` file:</span></span>
   
   * <span data-ttu-id="df244-126">Sostituire **[nome host di dispositivo o indirizzo IP]** con hello dispositivo IP indirizzo o il nome host è stato creato da `device-discovery-cli` o con valore hello ereditata durante la configurazione del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="df244-126">Replace **[device hostname or IP address]** with hello device IP address or host name you got from `device-discovery-cli` or with hello value inherited when you configured your device.</span></span>
   * <span data-ttu-id="df244-127">Sostituire **[stringa di connessione dispositivo IoT]** con hello `device connection string` ottenute.</span><span class="sxs-lookup"><span data-stu-id="df244-127">Replace **[IoT device connection string]** with hello `device connection string` you obtained.</span></span>
   * <span data-ttu-id="df244-128">Sostituire **[stringa di connessione hub IoT]** con hello `iot hub connection string` ottenute.</span><span class="sxs-lookup"><span data-stu-id="df244-128">Replace **[IoT hub connection string]** with hello `iot hub connection string` you obtained.</span></span>

<span data-ttu-id="df244-129">Hello aggiornamento `config-raspberrypi.json` file in modo che è possibile distribuire l'applicazione di esempio hello dal computer.</span><span class="sxs-lookup"><span data-stu-id="df244-129">Update hello `config-raspberrypi.json` file so that you can deploy hello sample application from your computer.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="df244-130">Distribuire ed eseguire l'applicazione di esempio hello</span><span class="sxs-lookup"><span data-stu-id="df244-130">Deploy and run hello sample application</span></span>
<span data-ttu-id="df244-131">Distribuire ed eseguire l'applicazione di esempio hello Pi eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="df244-131">Deploy and run hello sample application on Pi by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a><span data-ttu-id="df244-132">Verificare il funzionamento dell'applicazione di esempio hello</span><span class="sxs-lookup"><span data-stu-id="df244-132">Verify that hello sample application works</span></span>
<span data-ttu-id="df244-133">Dovrebbe essere hello LED che è connesso tooPi lampeggiante ogni due secondi.</span><span class="sxs-lookup"><span data-stu-id="df244-133">You should see hello LED that is connected tooPi blinking every two seconds.</span></span> <span data-ttu-id="df244-134">Ogni volta che hello LED è lampeggiante, applicazione di esempio hello invia un hub IoT tooyour di messaggio e verifica che il messaggio hello è stato inviato correttamente tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="df244-134">Every time hello LED blinks, hello sample application sends a message tooyour IoT hub and verifies that hello message has been successfully sent tooyour IoT hub.</span></span> <span data-ttu-id="df244-135">Inoltre, ogni messaggio ricevuto dall'hub IoT hello viene stampato nella finestra di console hello.</span><span class="sxs-lookup"><span data-stu-id="df244-135">In addition, each message received by hello IoT hub is printed in hello console window.</span></span> <span data-ttu-id="df244-136">applicazione di esempio Hello termina automaticamente dopo l'invio di 20 messaggi.</span><span class="sxs-lookup"><span data-stu-id="df244-136">hello sample application terminates automatically after sending 20 messages.</span></span>

![Applicazione di esempio con messaggi inviati e ricevuti](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run.png)

## <a name="summary"></a><span data-ttu-id="df244-138">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="df244-138">Summary</span></span>
<span data-ttu-id="df244-139">È stato distribuito ed eseguito nuova applicazione di esempio blink hello in hub IoT tooyour di pi greco toosend messaggi da dispositivo a cloud.</span><span class="sxs-lookup"><span data-stu-id="df244-139">You've deployed and run hello new blink sample application on Pi toosend device-to-cloud messages tooyour IoT hub.</span></span> <span data-ttu-id="df244-140">È ora possibile monitorare i messaggi quando vengono scritti toohello account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="df244-140">You can now monitor your messages as they are written toohello storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="df244-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="df244-141">Next steps</span></span>
[<span data-ttu-id="df244-142">Leggere i messaggi con salvataggio permanente in Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="df244-142">Read messages persisted in Azure Storage</span></span>](iot-hub-raspberry-pi-kit-node-lesson3-read-table-storage.md)

