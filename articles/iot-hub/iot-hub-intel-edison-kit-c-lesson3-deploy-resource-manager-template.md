---
title: 'Connect Intel Edison (C) tooAzure IoT - lezione 3: creare app di funzione | Documenti Microsoft'
description: "app di Azure funzione Hello è in ascolto di eventi di hub IoT tooAzure, elabora i messaggi in arrivo e li scrive archiviazione tabella tooAzure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: l'archiviazione dei dati nel cloud hello, dati archiviati nel cloud, iot servizio cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 739b82e9-5d4e-4485-8971-f57cbb682faf
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ef045ec2f44fe379a5e6c777d1bfb97de8b965a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="2836e-104">Creare un'app per le funzioni di Azure e un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="2836e-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="2836e-105">[Funzioni di Azure](../../articles/azure-functions/functions-overview.md) è una soluzione per l'esecuzione di facilmente *funzioni* (frammenti di codice) nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="2836e-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in hello cloud.</span></span> <span data-ttu-id="2836e-106">Un'app di Azure funzione ospita esecuzione hello delle funzioni in Azure.</span><span class="sxs-lookup"><span data-stu-id="2836e-106">An Azure function app hosts hello execution of your functions in Azure.</span></span>

## <a name="what-will-you-do"></a><span data-ttu-id="2836e-107">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="2836e-107">What will you do</span></span>
<span data-ttu-id="2836e-108">Utilizzare un toocreate modello di gestione risorse di Azure un'app di Azure (funzione) e un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2836e-108">Use an Azure Resource Manager template toocreate an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="2836e-109">app di Azure funzione Hello è in ascolto di eventi di hub IoT tooAzure, elabora i messaggi in arrivo e li scrive archiviazione tabella tooAzure.</span><span class="sxs-lookup"><span data-stu-id="2836e-109">hello Azure function app listens tooAzure IoT hub events, processes incoming messages, and writes them tooAzure Table storage.</span></span> <span data-ttu-id="2836e-110">Hello account di archiviazione viene usato per la lettura hello persistente copie dei messaggi dalla tabella di Azure.</span><span class="sxs-lookup"><span data-stu-id="2836e-110">hello storage account is used for reading hello persisted copies of messages from Azure table.</span></span> <span data-ttu-id="2836e-111">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="2836e-111">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-will-you-learn"></a><span data-ttu-id="2836e-112">Concetti legati all'esercitazione</span><span class="sxs-lookup"><span data-stu-id="2836e-112">What will you learn</span></span>
<span data-ttu-id="2836e-113">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="2836e-113">In this article, you will learn:</span></span>
* <span data-ttu-id="2836e-114">Come toouse [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure le risorse.</span><span class="sxs-lookup"><span data-stu-id="2836e-114">How toouse [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure resources.</span></span>
* <span data-ttu-id="2836e-115">Toouse di Azure come funzione app tooprocess messaggi hub IoT e per scriverli tooa tabella nell'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="2836e-115">How toouse an Azure function app tooprocess IoT hub messages and write them tooa table in Azure Table storage.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="2836e-116">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="2836e-116">What do you need</span></span>
<span data-ttu-id="2836e-117">È necessario aver completato:</span><span class="sxs-lookup"><span data-stu-id="2836e-117">You must have successfully completed:</span></span>
- <span data-ttu-id="2836e-118">[Introduzione a Intel Edison][get-started-with-your-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="2836e-118">[Get started with your Intel Edison][get-started-with-your-intel-edison]</span></span>
- <span data-ttu-id="2836e-119">[Creare l'hub IoT di Azure][create-your-azure-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="2836e-119">[Create your Azure IoT hub][create-your-azure-iot-hub]</span></span>

## <a name="open-hello-sample-app"></a><span data-ttu-id="2836e-120">App di esempio hello aperto</span><span class="sxs-lookup"><span data-stu-id="2836e-120">Open hello sample app</span></span>
<span data-ttu-id="2836e-121">Aprire il progetto di esempio hello in Visual Studio Code eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="2836e-121">Open hello sample project in Visual Studio Code by running hello following commands:</span></span>

```bash
cd Lesson3
code .
```

![Struttura del repository][repo-structure]

* <span data-ttu-id="2836e-123">file Hello in hello `app` sottocartella è il file di origine della chiave hello.</span><span class="sxs-lookup"><span data-stu-id="2836e-123">hello file in hello `app` subfolder is hello key source file.</span></span> <span data-ttu-id="2836e-124">Questo file di origine contiene toosend codice hello un messaggio di 20 volte tooyour IoT hub e blink hello LED per ogni messaggio inviato.</span><span class="sxs-lookup"><span data-stu-id="2836e-124">This source file contains hello code toosend a message 20 times tooyour IoT hub and blink hello LED for each message it sends.</span></span>
* <span data-ttu-id="2836e-125">Hello `arm-template.json` file è hello Azure Resource Manager modello contenente un'app di Azure (funzione) e un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2836e-125">hello `arm-template.json` file is hello Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="2836e-126">Hello `arm-template-param.json` tratta i file di configurazione hello utilizzato dal modello di gestione risorse di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="2836e-126">hello `arm-template-param.json` file is hello configuration file used by hello Azure Resource Manager template.</span></span>
* <span data-ttu-id="2836e-127">Hello `ReceiveDeviceMessages` sottocartella contiene codice Node.js hello hello Azure (funzione).</span><span class="sxs-lookup"><span data-stu-id="2836e-127">hello `ReceiveDeviceMessages` subfolder contains hello Node.js code for hello Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="2836e-128">Configurare i modelli di Azure Resource Manager e creare risorse in Azure</span><span class="sxs-lookup"><span data-stu-id="2836e-128">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="2836e-129">Hello aggiornamento `arm-template-param.json` file in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="2836e-129">Update hello `arm-template-param.json` file in Visual Studio Code.</span></span>

![Parametri del modello di Azure Resource Manager][arm-template-parameters]

* <span data-ttu-id="2836e-131">Sostituire **[your IoT Hub name]** con il valore di **{my hub name}** specificato durante la [creazione dell'hub IoT e registrazione di Intel Edison][created-your-iot-hub-and-registered-intel-edison].</span><span class="sxs-lookup"><span data-stu-id="2836e-131">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Intel Edison][created-your-iot-hub-and-registered-intel-edison].</span></span>
* <span data-ttu-id="2836e-132">Sostituire **[prefix string for new resources]** con il prefisso desiderato.</span><span class="sxs-lookup"><span data-stu-id="2836e-132">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="2836e-133">prefisso Hello assicura che il nome risorsa hello sia globalmente univoco tooavoid conflitto.</span><span class="sxs-lookup"><span data-stu-id="2836e-133">hello prefix ensures that hello resource name is globally unique tooavoid conflict.</span></span> <span data-ttu-id="2836e-134">Non usare un trattino o un numero iniziale nel prefisso hello.</span><span class="sxs-lookup"><span data-stu-id="2836e-134">Do not use a dash or number initial in hello prefix.</span></span>

<span data-ttu-id="2836e-135">Dopo l'aggiornamento hello `arm-template-param.json` file, distribuire hello risorse tooAzure eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2836e-135">After you update hello `arm-template-param.json` file, deploy hello resources tooAzure by running hello following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="2836e-136">Sono necessari circa cinque minuti toocreate queste risorse.</span><span class="sxs-lookup"><span data-stu-id="2836e-136">It takes about five minutes toocreate these resources.</span></span> <span data-ttu-id="2836e-137">Durante la creazione di risorse hello è in corso, è possibile spostare toohello Avanti articolo.</span><span class="sxs-lookup"><span data-stu-id="2836e-137">While hello resource creation is in progress, you can move on toohello next article.</span></span>

## <a name="summary"></a><span data-ttu-id="2836e-138">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="2836e-138">Summary</span></span>
<span data-ttu-id="2836e-139">Aver creato il tooprocess app Azure funzione messaggi hub IoT e un'archiviazione di Azure account toostore questi messaggi.</span><span class="sxs-lookup"><span data-stu-id="2836e-139">You've created your Azure function app tooprocess IoT hub messages and an Azure storage account toostore these messages.</span></span> <span data-ttu-id="2836e-140">È ora possibile distribuire ed eseguire messaggi da dispositivo a cloud toosend di esempio hello in Edison.</span><span class="sxs-lookup"><span data-stu-id="2836e-140">You can now deploy and run hello sample toosend device-to-cloud messages on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2836e-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2836e-141">Next steps</span></span>
<span data-ttu-id="2836e-142">[Eseguire un toosend di applicazione di esempio, i messaggi da dispositivo a cloud su Intel Edison][send-device-to-cloud-messages].</span><span class="sxs-lookup"><span data-stu-id="2836e-142">[Run a sample application toosend device-to-cloud messages on Intel Edison][send-device-to-cloud-messages].</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-started-with-your-intel-edison]: iot-hub-intel-edison-kit-c-get-started.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-c-get-started.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson3/repo_structure_c.png
[arm-template-parameters]: /media/iot-hub-intel-edison-lessons/lesson3/arm_para_c.png
[created-your-iot-hub-and-registered-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-intel-edison-kit-c-lesson3-run-azure-blink.md