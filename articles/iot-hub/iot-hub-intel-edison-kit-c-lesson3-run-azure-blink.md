---
title: 'Connettere Intel Edison (C) ad Azure IoT: lezione 3: Inviare i messaggi | Documentazione Microsoft'
description: Distribuire ed eseguire un'applicazione di esempio in Intel Edison che invia messaggi all'hub IoT e fa lampeggiare il LED.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: servizio cloud iot, inviare dati al cloud con arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 12672b64-795a-4dfc-86fd-df53ed3eeef7
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d104618ebb37a19c83f161beceb5c71bc89bbb56
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a><span data-ttu-id="fb75c-104">Eseguire un'applicazione di esempio per inviare messaggi da dispositivo a cloud</span><span class="sxs-lookup"><span data-stu-id="fb75c-104">Run a sample application to send device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="fb75c-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="fb75c-105">What you will do</span></span>
<span data-ttu-id="fb75c-106">Questo articolo illustra come distribuire ed eseguire un'applicazione di esempio in Intel Edison che invia messaggi all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="fb75c-106">This article will show you how to deploy and run a sample application on Intel Edison that sends messages to your IoT hub.</span></span> <span data-ttu-id="fb75c-107">In caso di problemi, cercare le soluzioni nella [pagina sulla risoluzione dei problemi][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="fb75c-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="fb75c-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="fb75c-108">What you will learn</span></span>
<span data-ttu-id="fb75c-109">Si apprenderà come usare lo strumento gulp per distribuire ed eseguire l'applicazione C di esempio in Edison.</span><span class="sxs-lookup"><span data-stu-id="fb75c-109">You will learn how to use the gulp tool to deploy and run the sample C application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="fb75c-110">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="fb75c-110">What you need</span></span>
* <span data-ttu-id="fb75c-111">Prima di iniziare questa attività, è necessario aver completato [Creare un'app per le funzioni di Azure e un account di archiviazione di Azure per elaborare e archiviare i messaggi dell'hub IoT][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="fb75c-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="fb75c-112">Ottenere le stringhe di connessione dell'hub IoT e del dispositivo</span><span class="sxs-lookup"><span data-stu-id="fb75c-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="fb75c-113">La stringa di connessione del dispositivo viene usata per connettere Edison all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="fb75c-113">The device connection string is used to connect Edison to your IoT hub.</span></span> <span data-ttu-id="fb75c-114">La stringa di connessione dell'hub IoT viene usata per connettere l'hub IoT all'identità del dispositivo che rappresenta Edison nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="fb75c-114">The IoT hub connection string is used to connect your IoT hub to the device identity that represents Edison in the IoT hub.</span></span>

* <span data-ttu-id="fb75c-115">Elencare tutti gli hub IoT nel gruppo di risorse eseguendo questo comando dell'interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="fb75c-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="fb75c-116">Usare `iot-sample` come valore di `{resource group name}` se non si è modificato il valore.</span><span class="sxs-lookup"><span data-stu-id="fb75c-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>

* <span data-ttu-id="fb75c-117">Ottenere la stringa di connessione dell'hub IoT eseguendo il comando seguente dell'interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="fb75c-117">Get the IoT hub connection string by running the following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="fb75c-118">`{my hub name}` è il nome specificato quando è stato creato l'hub IoT ed è stato registrato Edison.</span><span class="sxs-lookup"><span data-stu-id="fb75c-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered Edison.</span></span>

* <span data-ttu-id="fb75c-119">Ottenere la stringa di connessione del dispositivo usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="fb75c-119">Get the device connection string by running the following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

<span data-ttu-id="fb75c-120">Usare `myinteledison` come valore di `{device id}` se non si è modificato il valore.</span><span class="sxs-lookup"><span data-stu-id="fb75c-120">Use `myinteledison` as the value of `{device id}` if you didn't change the value.</span></span>

## <a name="configure-the-device-connection"></a><span data-ttu-id="fb75c-121">Configurare la connessione del dispositivo</span><span class="sxs-lookup"><span data-stu-id="fb75c-121">Configure the device connection</span></span>
1. <span data-ttu-id="fb75c-122">Inizializzare il file di configurazione usando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="fb75c-122">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```
   > [!NOTE]
   > <span data-ttu-id="fb75c-123">Se non è stato fatto nella lezione 1, eseguire anche il comando **gulp install-tools**.</span><span class="sxs-lookup"><span data-stu-id="fb75c-123">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

2. <span data-ttu-id="fb75c-124">Aprire il file di configurazione del dispositivo `config-edison.json` in Visual Studio Code usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="fb75c-124">Open the device configuration file `config-edison.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![config.json](media/iot-hub-intel-edison-lessons/lesson3/config.png)

3. <span data-ttu-id="fb75c-126">Sostituire i valori seguenti nel file `config-edison.json`:</span><span class="sxs-lookup"><span data-stu-id="fb75c-126">Make the following replacements in the `config-edison.json` file:</span></span>

   * <span data-ttu-id="fb75c-127">Sostituire **[device hostname or IP address]** con l'indirizzo IP del dispositivo annotato quando è stato configurato il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fb75c-127">Replace **[device hostname or IP address]** with the device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="fb75c-128">Sostituire **[IoT device connection string]** con il valore di `device connection string` ottenuto.</span><span class="sxs-lookup"><span data-stu-id="fb75c-128">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span></span>
   * <span data-ttu-id="fb75c-129">Sostituire **[IoT hub connection string]** con il valore di `iot hub connection string` ottenuto.</span><span class="sxs-lookup"><span data-stu-id="fb75c-129">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fb75c-130">Non è necessario specificare `azure_storage_connection_string` in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="fb75c-130">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="fb75c-131">Mantenerlo invariato.</span><span class="sxs-lookup"><span data-stu-id="fb75c-131">Keep it as is.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="fb75c-132">Distribuire ed eseguire l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="fb75c-132">Deploy and run the sample application</span></span>
<span data-ttu-id="fb75c-133">Distribuire ed eseguire l'applicazione di esempio in Edison eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="fb75c-133">Deploy and run the sample application on Edison by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-the-sample-application-works"></a><span data-ttu-id="fb75c-134">Verificare il funzionamento dell'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="fb75c-134">Verify that the sample application works</span></span>
<span data-ttu-id="fb75c-135">Il LED connesso a Edison dovrebbe lampeggiare ogni due secondi.</span><span class="sxs-lookup"><span data-stu-id="fb75c-135">You should see the LED that is connected to Edison blinking every two seconds.</span></span> <span data-ttu-id="fb75c-136">Ogni volta che il LED lampeggia, l'applicazione di esempio invia un messaggio all'hub IoT e verifica se il messaggio è stato inviato all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="fb75c-136">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span></span> <span data-ttu-id="fb75c-137">Ogni messaggio ricevuto dall'hub IoT viene stampato nella finestra della console.</span><span class="sxs-lookup"><span data-stu-id="fb75c-137">In addition, each message received by the IoT hub is printed in the console window.</span></span> <span data-ttu-id="fb75c-138">L'applicazione di esempio termina automaticamente dopo l'invio di 20 messaggi.</span><span class="sxs-lookup"><span data-stu-id="fb75c-138">The sample application terminates automatically after sending 20 messages.</span></span>

![Applicazione di esempio con messaggi inviati e ricevuti][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="fb75c-140">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="fb75c-140">Summary</span></span>
<span data-ttu-id="fb75c-141">È stata distribuita ed eseguita la nuova applicazione di esempio per il lampeggiamento in Edison per l'invio di messaggi da dispositivo a cloud all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="fb75c-141">You've deployed and run the new blink sample application on Edison to send device-to-cloud messages to your IoT hub.</span></span> <span data-ttu-id="fb75c-142">È ora possibile monitorare i messaggi mentre vengono scritti nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="fb75c-142">You now monitor your messages as they are written to the storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb75c-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fb75c-143">Next steps</span></span>
<span data-ttu-id="fb75c-144">[Leggere i messaggi con salvataggio permanente in Archiviazione di Azure][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="fb75c-144">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-intel-edison-lessons/lesson3/gulp_run_c.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-c-lesson3-read-table-storage.md