---
title: 'Dispositivo simulato e gateway Azure IoT: introduzione | Documentazione Microsoft'
description: Iniziare a usare lo starter kit per il gateway IoT, creare l'hub IoT di Azure e connettere il gateway all'hub IoT
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: hub IoT di Azure, gateway IoT, introduzione a Internet delle cose, toolkit IoT
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0c110b8b-bee4-4aec-a18a-dfc292aa17a3
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 916fa40d9ac857dfa72197b40c232834593d3891
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-simulated-device"></a><span data-ttu-id="5792a-104">Introduzione allo starter kit per il gateway IoT con un dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="5792a-104">Get started with IoT Gateway Starter Kit with a simulated device</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5792a-105">SensorTag</span><span class="sxs-lookup"><span data-stu-id="5792a-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="5792a-106">Dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="5792a-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="5792a-107">In questa esercitazione vengono descritte le nozioni base per usare lo [starter kit per il gateway IoT](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="5792a-107">In this tutorial, you begin by learning the basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="5792a-108">Si userà Intel NUC che esegue Wind River Linux.</span><span class="sxs-lookup"><span data-stu-id="5792a-108">You will be working with Intel NUC that's running Wind River Linux.</span></span> <span data-ttu-id="5792a-109">Verrà illustrato come connettere i dispositivi al cloud usando l'hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="5792a-109">You will learn how to seamleesly connect your devices to the cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="5792a-110">**Se non si ha ancora un kit**, fare clic [qui](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="5792a-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="5792a-111">Lezione 1: Configurare NUC</span><span class="sxs-lookup"><span data-stu-id="5792a-111">Lesson 1: Configure your NUC</span></span>
![Diagramma di flusso della lezione 1](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson1.png)

<span data-ttu-id="5792a-113">Questa lezione illustra come configurare il dispositivo Intel NUC (Next Unit of Computing) nel kit come un gateway IoT di Azure, installare il pacchetto di Azure IoT Edge sul dispositivo NUC ed eseguire un'app di esempio per verificare la funzionalità del gateway.</span><span class="sxs-lookup"><span data-stu-id="5792a-113">In this lesson, you set up Intel NUC (Next Unit of Computing) in the Kit as an Azure IoT gateway, install the Azure IoT Edge package on NUC, and run a sample app to verify the gateway functionality.</span></span>

<span data-ttu-id="5792a-114">*Tempo previsto per il completamento: 15 minuti*</span><span class="sxs-lookup"><span data-stu-id="5792a-114">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="5792a-115">Passare a [Configurare il dispositivo Intel NUC come un gateway IoT](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)</span><span class="sxs-lookup"><span data-stu-id="5792a-115">Go to [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="5792a-116">Lezione 2. Creare l'hub IoT</span><span class="sxs-lookup"><span data-stu-id="5792a-116">Lesson 2: Create your IoT Hub</span></span>
![Diagramma di flusso della lezione 2](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson2.png)

<span data-ttu-id="5792a-118">Questa lezione illustra come installare gli strumenti e il software nel computer host.</span><span class="sxs-lookup"><span data-stu-id="5792a-118">In this lesson, you install the tools and software on your host computer.</span></span> <span data-ttu-id="5792a-119">Verrà quindi indicato come creare l'account Azure gratuito, effettuare il provisioning dell'hub IoT di Azure e creare il primo dispositivo nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5792a-119">Then you create your free Azure account, provision your Azure IoT hub and create your first device in the IoT hub.</span></span>

<span data-ttu-id="5792a-120">Prima di iniziare questa lezione, completare la lezione 1.</span><span class="sxs-lookup"><span data-stu-id="5792a-120">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-the-tools"></a><span data-ttu-id="5792a-121">Get the tools</span><span class="sxs-lookup"><span data-stu-id="5792a-121">Get the tools</span></span>
<span data-ttu-id="5792a-122">Installare strumenti e software nel computer host.</span><span class="sxs-lookup"><span data-stu-id="5792a-122">Install the tools and software on your host computer.</span></span>

<span data-ttu-id="5792a-123">*Tempo previsto per il completamento: 20 minuti*</span><span class="sxs-lookup"><span data-stu-id="5792a-123">*Estimated time to complete: 20 minutes*</span></span>

<span data-ttu-id="5792a-124">Passare a [Ottenere gli strumenti](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)</span><span class="sxs-lookup"><span data-stu-id="5792a-124">Go to [Get the tools](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="5792a-125">Creare un hub IoT ed effettuare la registrazione del dispositivo</span><span class="sxs-lookup"><span data-stu-id="5792a-125">Create an IoT hub and register your device</span></span>
<span data-ttu-id="5792a-126">Creare il gruppo di risorse, effettuare il provisioning del primo hub IoT di Azure e aggiungere il primo dispositivo all'hub IoT usando l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="5792a-126">Create your resource group, provision your first Azure IoT hub, and add your first device to the IoT hub using the Azure CLI.</span></span>

<span data-ttu-id="5792a-127">*Tempo previsto per il completamento: 10 minuti*</span><span class="sxs-lookup"><span data-stu-id="5792a-127">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="5792a-128">Passare a [Creare un hub IoT e registrare il dispositivo](iot-hub-gateway-kit-c-sim-lesson2-register-device.md).</span><span class="sxs-lookup"><span data-stu-id="5792a-128">Go to [Create an IoT hub and register your device](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-the-simulated-device-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="5792a-129">Lezione 3: Ricevere messaggi dal dispositivo simulato e leggerli dall'hub IoT</span><span class="sxs-lookup"><span data-stu-id="5792a-129">Lesson 3: Receive messages from the simulated device and read messages from your IoT hub</span></span>
<span data-ttu-id="5792a-130">In questa lezione si useranno script per automatizzare la configurazione e l'esecuzione di un'app per dispositivo simulato nel gateway.</span><span class="sxs-lookup"><span data-stu-id="5792a-130">In this lesson, you will use scripts to automate the configuration and execution of a simulated device app in your gateway.</span></span> <span data-ttu-id="5792a-131">L'app per dispositivo simulato genera dati di esempio sulla temperatura e li invia a un modulo dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5792a-131">The simulated device app generates sample temperature data and sends it to an IoT hub module.</span></span> <span data-ttu-id="5792a-132">Il modulo dell'hub IoT inserisce in pacchetti i dati ricevuti e li invia all'hub IoT tramite il framework del gateway fornito in Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="5792a-132">The IoT hub module packages the data received and sends it to your IoT hub through the gateway framework provided in Azure IoT Edge.</span></span>

![Diagramma di flusso della lezione 3](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson3.png)

### <a name="configure-and-run-a-simulated-device"></a><span data-ttu-id="5792a-134">Configurare ed eseguire un dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="5792a-134">Configure and run a simulated device</span></span>
<span data-ttu-id="5792a-135">Preparare i codici di esempio,</span><span class="sxs-lookup"><span data-stu-id="5792a-135">Prepare the sample codes.</span></span> <span data-ttu-id="5792a-136">quindi configurare ed eseguire l'applicazione di esempio per il dispositivo simulato.</span><span class="sxs-lookup"><span data-stu-id="5792a-136">Then configure and run the simulated device sample application.</span></span>

<span data-ttu-id="5792a-137">*Tempo previsto per il completamento: 15 minuti*</span><span class="sxs-lookup"><span data-stu-id="5792a-137">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="5792a-138">Passare a [Configurare ed eseguire un dispositivo simulato](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span><span class="sxs-lookup"><span data-stu-id="5792a-138">Go to [Configure and run a simulated device](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="5792a-139">Leggere messaggi dall'hub IoT</span><span class="sxs-lookup"><span data-stu-id="5792a-139">Read messages from your IoT hub</span></span>
<span data-ttu-id="5792a-140">Eseguire un codice di esempio nel computer host per leggere i messaggi dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5792a-140">Run a sample code on your host computer to read the messages from your IoT hub.</span></span>

<span data-ttu-id="5792a-141">*Tempo previsto per il completamento: 15 minuti*</span><span class="sxs-lookup"><span data-stu-id="5792a-141">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="5792a-142">Passare a [Leggere i messaggi dall'hub IoT](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="5792a-142">Go to [Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-to-azure-table-storage"></a><span data-ttu-id="5792a-143">Lezione 4. Salvare i messaggi nell'archiviazione tabelle di Azure</span><span class="sxs-lookup"><span data-stu-id="5792a-143">Lesson 4: Save messages to Azure Table storage</span></span>
<span data-ttu-id="5792a-144">Creare un'app per le funzioni di Azure in grado di recuperare i messaggi in arrivo dall'hub IoT e scriverli nell'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="5792a-144">Create an Azure function app that gets incoming messages from your IoT hub and writes them to Azure Table storage.</span></span>

![Diagramma di flusso della lezione 4](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="5792a-146">Creare un'app per le funzioni di Azure e un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="5792a-146">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="5792a-147">Usare un modello di Azure Resource Manager per creare un'app per le funzioni di Azure e un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5792a-147">Use an Azure Resource Manager template to create an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="5792a-148">*Tempo previsto per il completamento: 10 minuti*</span><span class="sxs-lookup"><span data-stu-id="5792a-148">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="5792a-149">Passare a [Creare un'app per le funzioni di Azure e un account di archiviazione di Azure](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="5792a-149">Go to [Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="5792a-150">Leggere i messaggi persistenti nell'archiviazione tabelle di Azure</span><span class="sxs-lookup"><span data-stu-id="5792a-150">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="5792a-151">Monitorare i messaggi da gateway a cloud mentre vengono scritti nell'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="5792a-151">Monitor the gateway-to-cloud messages as they are written to Azure Table storage.</span></span>

<span data-ttu-id="5792a-152">*Tempo previsto per il completamento: 5 minuti*</span><span class="sxs-lookup"><span data-stu-id="5792a-152">*Estimated time to complete: 5 minutes*</span></span>

<span data-ttu-id="5792a-153">Passare a [Leggere i messaggi persistenti nell'archiviazione tabelle di Azure](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="5792a-153">Go to [Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="5792a-154">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="5792a-154">Troubleshooting</span></span>
<span data-ttu-id="5792a-155">In caso di problemi durante le lezioni, è possibile cercare soluzioni nell'articolo [Risoluzione dei problemi](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="5792a-155">If you have any problems during the lessons, look for solutions in the [Troubleshooting](iot-hub-gateway-kit-c-sim-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="5792a-156">Scopri di più</span><span class="sxs-lookup"><span data-stu-id="5792a-156">Explore more</span></span>
<span data-ttu-id="5792a-157">Per ulteriori informazioni, visitare la pagina relativa a [Intel IoT Gateway Kit in Developer Zone](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit).</span><span class="sxs-lookup"><span data-stu-id="5792a-157">Visit the [Intel IoT Gateway Kit developer zone](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) to learn more.</span></span>