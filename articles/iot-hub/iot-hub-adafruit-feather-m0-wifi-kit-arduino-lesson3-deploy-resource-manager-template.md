---
title: 'Connettere Arduino (C) ad Azure IoT: lezione 3: Distribuzione del modello | Documentazione Microsoft'
description: L'app per le funzioni di Azure rimane in ascolto degli eventi dell'hub IoT di Azure, elabora i messaggi in ingresso e li scrive nell'archiviazione tabelle di Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: archiviazione di dati nel cloud, dati archiviati nel cloud, servizio cloud iot
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 9c8f4cd1-9511-4601-ad7e-51761a986753
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: be6105927645ae2ec56f6885c61dbcb6faf5b11f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="da4f6-104">Creare un'app per le funzioni di Azure e un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="da4f6-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="da4f6-105">[Funzioni di Azure](../../articles/azure-functions/functions-overview.md) è una soluzione che consente di eseguire facilmente piccole parti di codice, ovvero *funzioni*, nel cloud.</span><span class="sxs-lookup"><span data-stu-id="da4f6-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in the cloud.</span></span> <span data-ttu-id="da4f6-106">Un'app per le funzioni di Azure ospita l'esecuzione delle funzioni in Azure.</span><span class="sxs-lookup"><span data-stu-id="da4f6-106">An Azure function app hosts the execution of your functions in Azure.</span></span>

## <a name="what-will-you-do"></a><span data-ttu-id="da4f6-107">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="da4f6-107">What will you do</span></span>
<span data-ttu-id="da4f6-108">Usare un modello di Azure Resource Manager per creare un'app per le funzioni di Azure e un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="da4f6-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="da4f6-109">L'app per le funzioni di Azure rimane in ascolto degli eventi dell'hub IoT di Azure, elabora i messaggi in ingresso e li scrive nell'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="da4f6-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span></span>

<span data-ttu-id="da4f6-110">In caso di problemi con la scheda Arduino per Adafruit Feather M0 WiFi, cercare le soluzioni nella [pagina sulla risoluzione dei problemi](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="da4f6-110">If you have any problems, look for solutions on the [troubleshooting page for your Adafruit Feather M0 WiFi Arduino board](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span></span>

## <a name="what-will-you-learn"></a><span data-ttu-id="da4f6-111">Concetti legati all'esercitazione</span><span class="sxs-lookup"><span data-stu-id="da4f6-111">What will you learn</span></span>
<span data-ttu-id="da4f6-112">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="da4f6-112">In this article, you will learn:</span></span>
* <span data-ttu-id="da4f6-113">Come usare [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) per distribuire le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="da4f6-113">How to use [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) to deploy Azure resources.</span></span>
* <span data-ttu-id="da4f6-114">Come usare un'app per le funzioni di Azure per elaborare i messaggi dell'hub IoT e scriverli in una tabella nell'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="da4f6-114">How to use an Azure function app to process IoT hub messages and write them to a table in Azure Table storage.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="da4f6-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="da4f6-115">What do you need</span></span>
<span data-ttu-id="da4f6-116">È necessario aver completato:</span><span class="sxs-lookup"><span data-stu-id="da4f6-116">You must have successfully completed:</span></span>
- <span data-ttu-id="da4f6-117">[Introduzione alla scheda Arduino][get-started]</span><span class="sxs-lookup"><span data-stu-id="da4f6-117">[Get started with your Arduino board][get-started]</span></span>
- <span data-ttu-id="da4f6-118">[Creare l'hub IoT di Azure][create-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="da4f6-118">[Create your Azure IoT hub][create-iot-hub]</span></span>

## <a name="open-the-sample-app"></a><span data-ttu-id="da4f6-119">Aprire l'app di esempio</span><span class="sxs-lookup"><span data-stu-id="da4f6-119">Open the sample app</span></span>
<span data-ttu-id="da4f6-120">Aprire il progetto di esempio in Visual Studio Code usando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="da4f6-120">Open the sample project in Visual Studio Code by running the following commands:</span></span>

```bash
cd Lesson3
code .
```

![Struttura del repository][repo-structure]

* <span data-ttu-id="da4f6-122">Il file `app.ino` nella sottocartella `app` è il file di origine chiave.</span><span class="sxs-lookup"><span data-stu-id="da4f6-122">The `app.ino` file in the `app` subfolder is the key source file.</span></span> <span data-ttu-id="da4f6-123">Questo file contiene il codice per inviare 20 volte un messaggio all'hub IoT e far lampeggiare il LED per ogni messaggio inviato.</span><span class="sxs-lookup"><span data-stu-id="da4f6-123">This source file contains the code to send a message 20 times to your IoT hub and blink the LED for each message it sends.</span></span>
* <span data-ttu-id="da4f6-124">`config.json` contiene le impostazioni di configurazione necessarie.</span><span class="sxs-lookup"><span data-stu-id="da4f6-124">The `config.json` contains required configuration settings.</span></span>
* <span data-ttu-id="da4f6-125">Il file `arm-template.json` è il modello di Azure Resource Manager che contiene un'app per le funzioni di Azure e un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="da4f6-125">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="da4f6-126">`arm-template-param.json` è il file di configurazione usato dal modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="da4f6-126">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span></span>
* <span data-ttu-id="da4f6-127">La sottocartella `ReceiveDeviceMessages` contiene il codice Node.js per la funzione di Azure.</span><span class="sxs-lookup"><span data-stu-id="da4f6-127">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="da4f6-128">Configurare i modelli di Azure Resource Manager e creare risorse in Azure</span><span class="sxs-lookup"><span data-stu-id="da4f6-128">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="da4f6-129">Aggiornare il file `arm-template-param.json` in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="da4f6-129">Update the `arm-template-param.json` file in Visual Studio Code.</span></span>

![Parametri del modello di Azure Resource Manager][arm-template-params]

* <span data-ttu-id="da4f6-131">Sostituire **[your IoT Hub name]** con il valore di **{my hub name}** specificato quando [è stato creato l'hub IoT ed è stata registrata la scheda Arduino][created-iot-hub-and-registered-arduino-board].</span><span class="sxs-lookup"><span data-stu-id="da4f6-131">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered your Arduino board][created-iot-hub-and-registered-arduino-board].</span></span>
* <span data-ttu-id="da4f6-132">Sostituire **[prefix string for new resources]** con il prefisso desiderato.</span><span class="sxs-lookup"><span data-stu-id="da4f6-132">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="da4f6-133">Usando un prefisso si ha la sicurezza che il nome della risorsa sia globalmente univoco per evitare conflitti.</span><span class="sxs-lookup"><span data-stu-id="da4f6-133">The prefix ensures that the resource name is globally unique to avoid conflict.</span></span> <span data-ttu-id="da4f6-134">Non usare un trattino o un numero all'inizio del prefisso.</span><span class="sxs-lookup"><span data-stu-id="da4f6-134">Do not use a dash or number initial in the prefix.</span></span>

<span data-ttu-id="da4f6-135">Dopo aver aggiornato il file `arm-template-param.json`, distribuire le risorse in Azure usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="da4f6-135">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="da4f6-136">Per creare queste risorse sono necessari circa cinque minuti.</span><span class="sxs-lookup"><span data-stu-id="da4f6-136">It takes about five minutes to create these resources.</span></span> <span data-ttu-id="da4f6-137">Mentre è in corso la creazione di risorse, è possibile passare all'articolo successivo.</span><span class="sxs-lookup"><span data-stu-id="da4f6-137">While the resource creation is in progress, you can move on to the next article.</span></span>

## <a name="summary"></a><span data-ttu-id="da4f6-138">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="da4f6-138">Summary</span></span>
<span data-ttu-id="da4f6-139">È stata creata l'app per le funzioni di Azure per elaborare i messaggi dell'hub IoT ed è stato configurato un account di archiviazione di Azure per archiviare tali messaggi.</span><span class="sxs-lookup"><span data-stu-id="da4f6-139">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span></span> <span data-ttu-id="da4f6-140">È ora possibile distribuire ed eseguire l'esempio per l'invio di messaggi da dispositivo a cloud sulla scheda Arduino.</span><span class="sxs-lookup"><span data-stu-id="da4f6-140">You can now deploy and run the sample to send device-to-cloud messages on your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da4f6-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="da4f6-141">Next steps</span></span>
<span data-ttu-id="da4f6-142">[Eseguire un'applicazione di esempio per inviare messaggi da dispositivo a cloud nella scheda Arduino][send-device-to-cloud-messages]</span><span class="sxs-lookup"><span data-stu-id="da4f6-142">[Run a sample application to send device-to-cloud messages on your Arduino board][send-device-to-cloud-messages]</span></span>

<!-- Images and links -->

[get-started]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started.md
[create-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/repo_structure_c.png
[arm-template-params]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/arm_para_arduino.png
[created-iot-hub-and-registered-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md