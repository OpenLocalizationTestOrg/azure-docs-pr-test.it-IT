---
title: 'Dispositivo simulato e gateway Azure IoT: lezione 4: Salvare i messaggi | Documentazione Microsoft'
description: Salvare i messaggi da Intel NUC all'hub IoT, scriverli nell'archivio tabelle di Azure e quindi leggerli dal cloud.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: archiviazione di dati nel cloud, dati archiviati nel cloud, servizio cloud iot
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: ffed0c2e-b092-40e1-9113-8196ec057d67
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c7fc47b07acede28ffe790debca7e38521726011
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-storage-account"></a><span data-ttu-id="7b804-104">Creare un'app per le funzioni di Azure e un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="7b804-104">Create an Azure function app and storage account</span></span>

<span data-ttu-id="7b804-105">Funzioni di Azure è una soluzione che consente di eseguire facilmente delle _funzioni_, ovvero piccole parti di codice, nel cloud.</span><span class="sxs-lookup"><span data-stu-id="7b804-105">Azure Functions is a solution for easily running _functions_ (small pieces of code) in the cloud.</span></span> <span data-ttu-id="7b804-106">Un'app per le funzioni di Azure ospita l'esecuzione delle funzioni in Azure.</span><span class="sxs-lookup"><span data-stu-id="7b804-106">An Azure function app hosts the execution of your functions in Azure.</span></span> 

## <a name="what-you-will-do"></a><span data-ttu-id="7b804-107">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="7b804-107">What you will do</span></span>

- <span data-ttu-id="7b804-108">Usare un modello di Azure Resource Manager per creare un'app per le funzioni di Azure e un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7b804-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="7b804-109">L'app per le funzioni di Azure rimane in ascolto degli eventi dell'hub IoT di Azure, elabora i messaggi in ingresso e li scrive nell'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="7b804-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span></span>

<span data-ttu-id="7b804-110">In caso di problemi, cercare le soluzioni nella pagina sulla [risoluzione dei problemi](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="7b804-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>


## <a name="what-you-will-learn"></a><span data-ttu-id="7b804-111">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="7b804-111">What you will learn</span></span>

<span data-ttu-id="7b804-112">In questa lezione si apprenderà:</span><span class="sxs-lookup"><span data-stu-id="7b804-112">In this lesson, you will learn:</span></span>

- <span data-ttu-id="7b804-113">Come usare Azure Resource Manager per distribuire le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="7b804-113">How to use Azure Resource Manager to deploy Azure resources.</span></span>
- <span data-ttu-id="7b804-114">Come usare un'app per le funzioni di Azure per elaborare i messaggi dell'hub IoT e scriverli in una tabella nell'archivio tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="7b804-114">How to use an Azure function app to process IoT Hub messages and write them to a table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7b804-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="7b804-115">What you need</span></span>

<span data-ttu-id="7b804-116">È necessario aver completato le lezioni precedenti:</span><span class="sxs-lookup"><span data-stu-id="7b804-116">You must have successfully completed the previous lessons:</span></span>

- [<span data-ttu-id="7b804-117">Lezione 1: Configurare Intel NUC come gateway IoT</span><span class="sxs-lookup"><span data-stu-id="7b804-117">Lesson 1: Set up your Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)
- [<span data-ttu-id="7b804-118">Lezione 2: Preparare il computer host e l'hub IoT di Azure</span><span class="sxs-lookup"><span data-stu-id="7b804-118">Lesson 2: Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
- [<span data-ttu-id="7b804-119">Lezione 3: Ricevere messaggi dal dispositivo simulato e leggerli dall'hub IoT</span><span class="sxs-lookup"><span data-stu-id="7b804-119">Lesson 3: Receive messages from the simulated device and read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)

## <a name="open-a-sample-app"></a><span data-ttu-id="7b804-120">Aprire un'app di esempio</span><span class="sxs-lookup"><span data-stu-id="7b804-120">Open a sample app</span></span>

<span data-ttu-id="7b804-121">Passare alla cartella del repository `iot-hub-c-intel-nuc-gateway-getting-started`, inizializzare i file di configurazione, quindi aprire il progetto di esempio in Visual Studio Code eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="7b804-121">Go to your `iot-hub-c-intel-nuc-gateway-getting-started` repo folder, initialize the configuration files, and then open the sample project in Visual Studio Code by running the following command:</span></span>

```bash
cd Lesson4
npm install
gulp init
code .
```

![Struttura del repository](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- <span data-ttu-id="7b804-123">Il file `arm-template.json` è il modello di Azure Resource Manager che contiene un'app per le funzioni di Azure e un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7b804-123">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
- <span data-ttu-id="7b804-124">`arm-template-param.json` è il file di configurazione usato dal modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7b804-124">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span></span>
- <span data-ttu-id="7b804-125">La sottocartella `ReceiveDeviceMessages` contiene il codice Node.js per la funzione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7b804-125">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="7b804-126">Configurare i modelli di Azure Resource Manager e creare risorse in Azure</span><span class="sxs-lookup"><span data-stu-id="7b804-126">Configure Azure Resource Manager templates and create resources in Azure</span></span>

<span data-ttu-id="7b804-127">Aggiornare il file `arm-template-param.json` in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="7b804-127">Update the `arm-template-param.json` file in Visual Studio Code.</span></span>

![File JSON del modello di Azure Resource Manager](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- <span data-ttu-id="7b804-129">Sostituire `[your IoT Hub name]` con il nome `{my hub name}` specificato nella lezione 2.</span><span class="sxs-lookup"><span data-stu-id="7b804-129">Replace `[your IoT Hub name]` with `{my hub name}` that you specified in Lesson 2.</span></span>

<span data-ttu-id="7b804-130">Dopo aver aggiornato il file `arm-template-param.json`, distribuire le risorse in Azure usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="7b804-130">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

<span data-ttu-id="7b804-131">Usare `iot-gateway` come valore di `{resource group name}` se nella lezione 2 non si è modificato il valore.</span><span class="sxs-lookup"><span data-stu-id="7b804-131">Use `iot-gateway` as the value of `{resource group name}` if you didn't change the value in Lesson 2.</span></span>

## <a name="summary"></a><span data-ttu-id="7b804-132">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="7b804-132">Summary</span></span>

<span data-ttu-id="7b804-133">È stata creata l'app per le funzioni di Azure per elaborare i messaggi dell'hub IoT ed è stato configurato un account di archiviazione di Azure per archiviare tali messaggi.</span><span class="sxs-lookup"><span data-stu-id="7b804-133">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span></span> <span data-ttu-id="7b804-134">È ora possibile leggere i messaggi inviati dal gateway all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="7b804-134">You can now read messages that are sent by your gateway to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b804-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7b804-135">Next steps</span></span>
<span data-ttu-id="7b804-136">[Leggere i messaggi con salvataggio permanente in Archiviazione di Azure](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="7b804-136">[Read messages persisted in Azure Storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span></span>
