---
title: 'Dispositivo SensorTag e gateway Azure IoT: lezione 4: Creare l''app per le funzioni | Documentazione Microsoft'
description: Salvare i messaggi dall'hub IoT di Intel NUC tooyour, scriverli archiviazione tabelle tooAzure e quindi leggerli dal cloud hello.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: l'archiviazione dei dati nel cloud hello, dati archiviati nel cloud, iot servizio cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f84f9a85-e2c4-4a92-8969-f65eb34c194e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: efee3bdc15ced104651f4a500311a5fe614267c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-storage-account"></a><span data-ttu-id="7f98b-104">Creare un'app per le funzioni di Azure e un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="7f98b-104">Create an Azure function app and storage account</span></span>

<span data-ttu-id="7f98b-105">Funzioni di Azure è una soluzione per l'esecuzione di facilmente _funzioni_ (frammenti di codice) nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="7f98b-105">Azure Functions is a solution for easily running _functions_ (small pieces of code) in hello cloud.</span></span> <span data-ttu-id="7f98b-106">Un'app di Azure funzione ospita esecuzione hello delle funzioni in Azure.</span><span class="sxs-lookup"><span data-stu-id="7f98b-106">An Azure function app hosts hello execution of your functions in Azure.</span></span> 

## <a name="what-you-will-do"></a><span data-ttu-id="7f98b-107">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="7f98b-107">What you will do</span></span>

- <span data-ttu-id="7f98b-108">Utilizzare un toocreate modello di gestione risorse di Azure un'app di Azure (funzione) e un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7f98b-108">Use an Azure Resource Manager template toocreate an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="7f98b-109">app di Azure funzione Hello è in ascolto di eventi di hub IoT tooAzure, elabora i messaggi in arrivo e li scrive archiviazione tabella tooAzure.</span><span class="sxs-lookup"><span data-stu-id="7f98b-109">hello Azure function app listens tooAzure IoT hub events, processes incoming messages, and writes them tooAzure Table storage.</span></span>

<span data-ttu-id="7f98b-110">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="7f98b-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>


## <a name="what-you-will-learn"></a><span data-ttu-id="7f98b-111">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="7f98b-111">What you will learn</span></span>

<span data-ttu-id="7f98b-112">In questa lezione si apprenderà:</span><span class="sxs-lookup"><span data-stu-id="7f98b-112">In this lesson, you will learn:</span></span>

- <span data-ttu-id="7f98b-113">Come toouse toodeploy Gestione risorse di Azure le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="7f98b-113">How toouse Azure Resource Manager toodeploy Azure resources.</span></span>
- <span data-ttu-id="7f98b-114">Toouse di Azure come funzione app tooprocess messaggi IoT Hub e per scriverli tooa tabella nell'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="7f98b-114">How toouse an Azure function app tooprocess IoT Hub messages and write them tooa table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7f98b-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="7f98b-115">What you need</span></span>

<span data-ttu-id="7f98b-116">È necessario avere completata lezioni precedenti hello:</span><span class="sxs-lookup"><span data-stu-id="7f98b-116">You must have successfully completed hello previous lessons:</span></span>

- [<span data-ttu-id="7f98b-117">Lezione 1: Configurare Intel NUC come gateway IoT</span><span class="sxs-lookup"><span data-stu-id="7f98b-117">Lesson 1: Set up your Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
- [<span data-ttu-id="7f98b-118">Lezione 2: Preparare il computer host e l'hub IoT di Azure</span><span class="sxs-lookup"><span data-stu-id="7f98b-118">Lesson 2: Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
- [<span data-ttu-id="7f98b-119">Lezione 3: Ricevere messaggi da SensorTag e leggere i messaggi dall'hub IoT</span><span class="sxs-lookup"><span data-stu-id="7f98b-119">Lesson 3: Receive messages from SensorTag and read messages from IoT hub</span></span>](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)

## <a name="open-a-sample-app"></a><span data-ttu-id="7f98b-120">Aprire un'app di esempio</span><span class="sxs-lookup"><span data-stu-id="7f98b-120">Open a sample app</span></span>

<span data-ttu-id="7f98b-121">Passare tooyour `iot-hub-c-intel-nuc-gateway-getting-started` cartella repository, i file di configurazione di inizializzazione hello e hello quindi aprire un progetto di esempio nel codice di Visual Studio eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="7f98b-121">Go tooyour `iot-hub-c-intel-nuc-gateway-getting-started` repo folder, initialize hello configuration files, and then open hello sample project in Visual Studio Code by running hello following command:</span></span>

```bash
cd Lesson4
npm install
gulp init
code .
```

![Struttura del repository](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- <span data-ttu-id="7f98b-123">Hello `arm-template.json` file è hello Azure Resource Manager modello contenente un'app di Azure (funzione) e un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7f98b-123">hello `arm-template.json` file is hello Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
- <span data-ttu-id="7f98b-124">Hello `arm-template-param.json` tratta i file di configurazione hello utilizzato dal modello di gestione risorse di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="7f98b-124">hello `arm-template-param.json` file is hello configuration file used by hello Azure Resource Manager template.</span></span>
- <span data-ttu-id="7f98b-125">Hello `ReceiveDeviceMessages` sottocartella contiene codice Node.js hello hello Azure (funzione).</span><span class="sxs-lookup"><span data-stu-id="7f98b-125">hello `ReceiveDeviceMessages` subfolder contains hello Node.js code for hello Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="7f98b-126">Configurare i modelli di Azure Resource Manager e creare risorse in Azure</span><span class="sxs-lookup"><span data-stu-id="7f98b-126">Configure Azure Resource Manager templates and create resources in Azure</span></span>

<span data-ttu-id="7f98b-127">Hello aggiornamento `arm-template-param.json` file in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="7f98b-127">Update hello `arm-template-param.json` file in Visual Studio Code.</span></span>

![File JSON del modello di Azure Resource Manager](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- <span data-ttu-id="7f98b-129">Sostituire `[your IoT Hub name]` con il nome `{my hub name}` specificato nella lezione 2.</span><span class="sxs-lookup"><span data-stu-id="7f98b-129">Replace `[your IoT Hub name]` with `{my hub name}` that you specified in Lesson 2.</span></span>

<span data-ttu-id="7f98b-130">Dopo l'aggiornamento hello `arm-template-param.json` file, distribuire hello risorse tooAzure eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="7f98b-130">After you update hello `arm-template-param.json` file, deploy hello resources tooAzure by running hello following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

<span data-ttu-id="7f98b-131">Utilizzare `iot-gateway` come valore hello `{resource group name}` se non si sono modificati valore hello nella lezione 2.</span><span class="sxs-lookup"><span data-stu-id="7f98b-131">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="summary"></a><span data-ttu-id="7f98b-132">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="7f98b-132">Summary</span></span>

<span data-ttu-id="7f98b-133">Aver creato il tooprocess app Azure funzione messaggi hub IoT e un'archiviazione di Azure account toostore questi messaggi.</span><span class="sxs-lookup"><span data-stu-id="7f98b-133">You've created your Azure function app tooprocess IoT hub messages and an Azure storage account toostore these messages.</span></span> <span data-ttu-id="7f98b-134">È ora possibile leggere i messaggi vengono inviati tramite l'hub IoT tooyour di gateway.</span><span class="sxs-lookup"><span data-stu-id="7f98b-134">You can now read messages that are sent by your gateway tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f98b-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7f98b-135">Next steps</span></span>
<span data-ttu-id="7f98b-136">[Leggere i messaggi con salvataggio permanente in Archiviazione di Azure](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="7f98b-136">[Read messages persisted in Azure Storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span></span>
