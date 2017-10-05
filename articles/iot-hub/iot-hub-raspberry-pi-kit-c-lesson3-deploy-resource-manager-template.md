---
title: 'Connettere Raspberry Pi (C) ad Azure IoT: lezione 3: Distribuzione del modello | Documentazione Microsoft'
description: L'app per le funzioni di Azure rimane in ascolto degli eventi dell'hub IoT di Azure, elabora i messaggi in ingresso e li scrive nell'archiviazione tabelle di Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: archiviazione di dati nel cloud, dati archiviati nel cloud, servizio cloud iot
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 4bcfb071-b3ae-48cc-8ea5-7e7434732287
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b8bab31489f2e912b51212cb58cb598a9db9b59d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="e124c-104">Creare un'app per le funzioni di Azure e un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e124c-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="e124c-105">[Funzioni di Azure](../../articles/azure-functions/functions-overview.md) è una soluzione che consente di eseguire facilmente piccole parti di codice, ovvero *funzioni*, nel cloud.</span><span class="sxs-lookup"><span data-stu-id="e124c-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in the cloud.</span></span> <span data-ttu-id="e124c-106">Un'app per le funzioni di Azure ospita l'esecuzione delle funzioni in Azure.</span><span class="sxs-lookup"><span data-stu-id="e124c-106">An Azure function app hosts the execution of your functions in Azure.</span></span>

## <a name="what-will-you-do"></a><span data-ttu-id="e124c-107">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="e124c-107">What will you do</span></span>
<span data-ttu-id="e124c-108">Usare un modello di Azure Resource Manager per creare un'app per le funzioni di Azure e un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e124c-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="e124c-109">L'app per le funzioni di Azure rimane in ascolto degli eventi dell'hub IoT di Azure, elabora i messaggi in ingresso e li scrive nell'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="e124c-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span></span> <span data-ttu-id="e124c-110">In caso di problemi, cercare le soluzioni nella pagina sulla [risoluzione dei problemi](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="e124c-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-will-you-learn"></a><span data-ttu-id="e124c-111">Concetti legati all'esercitazione</span><span class="sxs-lookup"><span data-stu-id="e124c-111">What will you learn</span></span>
<span data-ttu-id="e124c-112">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="e124c-112">In this article, you will learn:</span></span>
* <span data-ttu-id="e124c-113">Come usare [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) per distribuire le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="e124c-113">How to use [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) to deploy Azure resources.</span></span>
* <span data-ttu-id="e124c-114">Come usare un'app per le funzioni di Azure per elaborare i messaggi dell'hub IoT e scriverli in una tabella nell'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="e124c-114">How to use an Azure function app to process IoT hub messages and write them to a table in Azure Table storage.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="e124c-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="e124c-115">What do you need</span></span>
* <span data-ttu-id="e124c-116">È necessario aver completato:</span><span class="sxs-lookup"><span data-stu-id="e124c-116">You must have successfully completed:</span></span>
- [<span data-ttu-id="e124c-117">Introduzione a Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="e124c-117">Get started with your Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-c-get-started.md)
- [<span data-ttu-id="e124c-118">Creare l'hub IoT di Azure</span><span class="sxs-lookup"><span data-stu-id="e124c-118">Create your Azure IoT hub</span></span>](iot-hub-raspberry-pi-kit-c-get-started.md)

## <a name="open-the-sample-app"></a><span data-ttu-id="e124c-119">Aprire l'app di esempio</span><span class="sxs-lookup"><span data-stu-id="e124c-119">Open the sample app</span></span>
<span data-ttu-id="e124c-120">Aprire il progetto di esempio in Visual Studio Code usando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e124c-120">Open the sample project in Visual Studio Code by running the following commands:</span></span>

```bash
cd Lesson3
code .
```

![Struttura del repository](media/iot-hub-raspberry-pi-lessons/lesson3/repo_structure_c.png)

* <span data-ttu-id="e124c-122">Il file `main.c` nella sottocartella `app` è il file di origine chiave.</span><span class="sxs-lookup"><span data-stu-id="e124c-122">The `main.c` file in the `app` subfolder is the key source file.</span></span> <span data-ttu-id="e124c-123">Questo file contiene il codice per inviare 20 volte un messaggio all'hub IoT e far lampeggiare il LED per ogni messaggio inviato.</span><span class="sxs-lookup"><span data-stu-id="e124c-123">This source file contains the code to send a message 20 times to your IoT hub and blink the LED for each message it sends.</span></span>
* <span data-ttu-id="e124c-124">Il file `arm-template.json` è il modello di Azure Resource Manager che contiene un'app per le funzioni di Azure e un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e124c-124">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="e124c-125">`arm-template-param.json` è il file di configurazione usato dal modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e124c-125">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span></span>
* <span data-ttu-id="e124c-126">La sottocartella `ReceiveDeviceMessages` contiene il codice Node.js per la funzione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e124c-126">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="e124c-127">Configurare i modelli di Azure Resource Manager e creare risorse in Azure</span><span class="sxs-lookup"><span data-stu-id="e124c-127">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="e124c-128">Aggiornare il file `arm-template-param.json` in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e124c-128">Update the `arm-template-param.json` file in Visual Studio Code.</span></span>

![Parametri del modello di Azure Resource Manager](media/iot-hub-raspberry-pi-lessons/lesson3/arm_para_c.png)

* <span data-ttu-id="e124c-130">Sostituire **[your IoT Hub name]** con il valore di **{my hub name}** specificato quando [è stato creato l'hub IoT ed è stato registrato il dispositivo Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="e124c-130">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span></span>
* <span data-ttu-id="e124c-131">Sostituire **[prefix string for new resources]** con il prefisso desiderato.</span><span class="sxs-lookup"><span data-stu-id="e124c-131">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="e124c-132">Usando un prefisso si ha la sicurezza che il nome della risorsa sia globalmente univoco per evitare conflitti.</span><span class="sxs-lookup"><span data-stu-id="e124c-132">The prefix ensures that the resource name is globally unique to avoid conflict.</span></span> <span data-ttu-id="e124c-133">Non usare un trattino o un numero all'inizio del prefisso.</span><span class="sxs-lookup"><span data-stu-id="e124c-133">Do not use a dash or number initial in the prefix.</span></span>

<span data-ttu-id="e124c-134">Dopo aver aggiornato il file `arm-template-param.json`, distribuire le risorse in Azure usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e124c-134">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="e124c-135">Per creare queste risorse sono necessari circa cinque minuti.</span><span class="sxs-lookup"><span data-stu-id="e124c-135">It takes about five minutes to create these resources.</span></span> <span data-ttu-id="e124c-136">Mentre è in corso la creazione di risorse, è possibile passare all'articolo successivo.</span><span class="sxs-lookup"><span data-stu-id="e124c-136">While the resource creation is in progress, you can move on to the next article.</span></span>

## <a name="summary"></a><span data-ttu-id="e124c-137">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="e124c-137">Summary</span></span>
<span data-ttu-id="e124c-138">È stata creata l'app per le funzioni di Azure per elaborare i messaggi dell'hub IoT ed è stato configurato un account di archiviazione di Azure per archiviare tali messaggi.</span><span class="sxs-lookup"><span data-stu-id="e124c-138">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span></span> <span data-ttu-id="e124c-139">È ora possibile distribuire ed eseguire l'esempio per l'invio di messaggi da dispositivo a cloud sul dispositivo Pi.</span><span class="sxs-lookup"><span data-stu-id="e124c-139">You can now deploy and run the sample to send device-to-cloud messages on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e124c-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e124c-140">Next steps</span></span>
[<span data-ttu-id="e124c-141">Eseguire un'applicazione di esempio per inviare messaggi da dispositivo a cloud</span><span class="sxs-lookup"><span data-stu-id="e124c-141">Run a sample application to send device-to-cloud messages</span></span>](iot-hub-raspberry-pi-kit-c-lesson3-run-azure-blink.md)

