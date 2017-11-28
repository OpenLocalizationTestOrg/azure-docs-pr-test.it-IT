---
title: 'Connect Arduino (C) tooAzure IoT - lezione 3: distribuzione del modello | Documenti Microsoft'
description: "app di Azure funzione Hello è in ascolto di eventi di hub IoT tooAzure, elabora i messaggi in arrivo e li scrive archiviazione tabella tooAzure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: l'archiviazione dei dati nel cloud hello, dati archiviati nel cloud, iot servizio cloud
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
ms.openlocfilehash: 6a84a6d3c5263a85c8997cf69fe446d73ab7a5fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="14399-104">Creare un'app per le funzioni di Azure e un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="14399-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="14399-105">[Funzioni di Azure](../../articles/azure-functions/functions-overview.md) è una soluzione per l'esecuzione di facilmente *funzioni* (frammenti di codice) nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="14399-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in hello cloud.</span></span> <span data-ttu-id="14399-106">Un'app di Azure funzione ospita esecuzione hello delle funzioni in Azure.</span><span class="sxs-lookup"><span data-stu-id="14399-106">An Azure function app hosts hello execution of your functions in Azure.</span></span>

## <a name="what-will-you-do"></a><span data-ttu-id="14399-107">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="14399-107">What will you do</span></span>
<span data-ttu-id="14399-108">Utilizzare un toocreate modello di gestione risorse di Azure un'app di Azure (funzione) e un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="14399-108">Use an Azure Resource Manager template toocreate an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="14399-109">app di Azure funzione Hello è in ascolto di eventi di hub IoT tooAzure, elabora i messaggi in arrivo e li scrive archiviazione tabella tooAzure.</span><span class="sxs-lookup"><span data-stu-id="14399-109">hello Azure function app listens tooAzure IoT hub events, processes incoming messages, and writes them tooAzure Table storage.</span></span>

<span data-ttu-id="14399-110">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina per la scheda Adafruit sfumatura M0 Wi-Fi Arduino](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="14399-110">If you have any problems, look for solutions on hello [troubleshooting page for your Adafruit Feather M0 WiFi Arduino board](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span></span>

## <a name="what-will-you-learn"></a><span data-ttu-id="14399-111">Concetti legati all'esercitazione</span><span class="sxs-lookup"><span data-stu-id="14399-111">What will you learn</span></span>
<span data-ttu-id="14399-112">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="14399-112">In this article, you will learn:</span></span>
* <span data-ttu-id="14399-113">Come toouse [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure le risorse.</span><span class="sxs-lookup"><span data-stu-id="14399-113">How toouse [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure resources.</span></span>
* <span data-ttu-id="14399-114">Toouse di Azure come funzione app tooprocess messaggi hub IoT e per scriverli tooa tabella nell'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="14399-114">How toouse an Azure function app tooprocess IoT hub messages and write them tooa table in Azure Table storage.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="14399-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="14399-115">What do you need</span></span>
<span data-ttu-id="14399-116">È necessario aver completato:</span><span class="sxs-lookup"><span data-stu-id="14399-116">You must have successfully completed:</span></span>
- <span data-ttu-id="14399-117">[Introduzione alla scheda Arduino][get-started]</span><span class="sxs-lookup"><span data-stu-id="14399-117">[Get started with your Arduino board][get-started]</span></span>
- <span data-ttu-id="14399-118">[Creare l'hub IoT di Azure][create-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="14399-118">[Create your Azure IoT hub][create-iot-hub]</span></span>

## <a name="open-hello-sample-app"></a><span data-ttu-id="14399-119">App di esempio hello aperto</span><span class="sxs-lookup"><span data-stu-id="14399-119">Open hello sample app</span></span>
<span data-ttu-id="14399-120">Aprire il progetto di esempio hello in Visual Studio Code eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="14399-120">Open hello sample project in Visual Studio Code by running hello following commands:</span></span>

```bash
cd Lesson3
code .
```

![Struttura del repository][repo-structure]

* <span data-ttu-id="14399-122">Hello `app.ino` file hello `app` sottocartella è il file di origine della chiave hello.</span><span class="sxs-lookup"><span data-stu-id="14399-122">hello `app.ino` file in hello `app` subfolder is hello key source file.</span></span> <span data-ttu-id="14399-123">Questo file di origine contiene toosend codice hello un messaggio di 20 volte tooyour IoT hub e blink hello LED per ogni messaggio inviato.</span><span class="sxs-lookup"><span data-stu-id="14399-123">This source file contains hello code toosend a message 20 times tooyour IoT hub and blink hello LED for each message it sends.</span></span>
* <span data-ttu-id="14399-124">Hello `config.json` contiene le impostazioni di configurazione necessarie.</span><span class="sxs-lookup"><span data-stu-id="14399-124">hello `config.json` contains required configuration settings.</span></span>
* <span data-ttu-id="14399-125">Hello `arm-template.json` file è hello Azure Resource Manager modello contenente un'app di Azure (funzione) e un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="14399-125">hello `arm-template.json` file is hello Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="14399-126">Hello `arm-template-param.json` tratta i file di configurazione hello utilizzato dal modello di gestione risorse di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="14399-126">hello `arm-template-param.json` file is hello configuration file used by hello Azure Resource Manager template.</span></span>
* <span data-ttu-id="14399-127">Hello `ReceiveDeviceMessages` sottocartella contiene codice Node.js hello hello Azure (funzione).</span><span class="sxs-lookup"><span data-stu-id="14399-127">hello `ReceiveDeviceMessages` subfolder contains hello Node.js code for hello Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="14399-128">Configurare i modelli di Azure Resource Manager e creare risorse in Azure</span><span class="sxs-lookup"><span data-stu-id="14399-128">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="14399-129">Hello aggiornamento `arm-template-param.json` file in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="14399-129">Update hello `arm-template-param.json` file in Visual Studio Code.</span></span>

![Parametri del modello di Azure Resource Manager][arm-template-params]

* <span data-ttu-id="14399-131">Sostituire **[your IoT Hub name]** con il valore di **{my hub name}** specificato quando [è stato creato l'hub IoT ed è stata registrata la scheda Arduino][created-iot-hub-and-registered-arduino-board].</span><span class="sxs-lookup"><span data-stu-id="14399-131">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered your Arduino board][created-iot-hub-and-registered-arduino-board].</span></span>
* <span data-ttu-id="14399-132">Sostituire **[prefix string for new resources]** con il prefisso desiderato.</span><span class="sxs-lookup"><span data-stu-id="14399-132">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="14399-133">prefisso Hello assicura che il nome risorsa hello sia globalmente univoco tooavoid conflitto.</span><span class="sxs-lookup"><span data-stu-id="14399-133">hello prefix ensures that hello resource name is globally unique tooavoid conflict.</span></span> <span data-ttu-id="14399-134">Non usare un trattino o un numero iniziale nel prefisso hello.</span><span class="sxs-lookup"><span data-stu-id="14399-134">Do not use a dash or number initial in hello prefix.</span></span>

<span data-ttu-id="14399-135">Dopo l'aggiornamento hello `arm-template-param.json` file, distribuire hello risorse tooAzure eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="14399-135">After you update hello `arm-template-param.json` file, deploy hello resources tooAzure by running hello following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="14399-136">Sono necessari circa cinque minuti toocreate queste risorse.</span><span class="sxs-lookup"><span data-stu-id="14399-136">It takes about five minutes toocreate these resources.</span></span> <span data-ttu-id="14399-137">Durante la creazione di risorse hello è in corso, è possibile spostare toohello Avanti articolo.</span><span class="sxs-lookup"><span data-stu-id="14399-137">While hello resource creation is in progress, you can move on toohello next article.</span></span>

## <a name="summary"></a><span data-ttu-id="14399-138">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="14399-138">Summary</span></span>
<span data-ttu-id="14399-139">Aver creato il tooprocess app Azure funzione messaggi hub IoT e un'archiviazione di Azure account toostore questi messaggi.</span><span class="sxs-lookup"><span data-stu-id="14399-139">You've created your Azure function app tooprocess IoT hub messages and an Azure storage account toostore these messages.</span></span> <span data-ttu-id="14399-140">È ora possibile distribuire ed eseguire i messaggi da dispositivo a cloud toosend di esempio hello sulla Lavagna Arduino.</span><span class="sxs-lookup"><span data-stu-id="14399-140">You can now deploy and run hello sample toosend device-to-cloud messages on your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="14399-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="14399-141">Next steps</span></span>
<span data-ttu-id="14399-142">[Eseguire un toosend di applicazione di esempio, i messaggi da dispositivo a cloud sulla Lavagna Arduino][send-device-to-cloud-messages]</span><span class="sxs-lookup"><span data-stu-id="14399-142">[Run a sample application toosend device-to-cloud messages on your Arduino board][send-device-to-cloud-messages]</span></span>

<!-- Images and links -->

[get-started]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started.md
[create-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/repo_structure_c.png
[arm-template-params]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/arm_para_arduino.png
[created-iot-hub-and-registered-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md