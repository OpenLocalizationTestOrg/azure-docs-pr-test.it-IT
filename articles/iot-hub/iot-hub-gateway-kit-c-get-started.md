---
title: 'Dispositivo SensorTag e gateway Azure IoT: introduzione | Documentazione Microsoft'
description: Informazioni introduttive sullo starter kit del gateway IoT, su come creare l'hub IoT di Azure e connettere il dispositivo SensorTag e il gateway all'hub IoT
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: hub iot di azure, gateway iot, introduzione a Internet delle cose, toolkit iot
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 56d05f4e-f2c1-4b22-8701-f01e14deead6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 624bdc7877d5048da08897f868272fd8e8f3f7b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-sensortag"></a><span data-ttu-id="2c2c5-104">Introduzione allo starter kit del gateway IoT di Azure con un dispositivo SensorTag</span><span class="sxs-lookup"><span data-stu-id="2c2c5-104">Get started with IoT Gateway Starter Kit with a SensorTag</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2c2c5-105">SensorTag</span><span class="sxs-lookup"><span data-stu-id="2c2c5-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="2c2c5-106">Dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="2c2c5-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="2c2c5-107">Questa esercitazione illustra le nozioni di base sull'uso dello [starter kit del gateway IoT](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="2c2c5-107">In this tutorial, you begin by learning the basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="2c2c5-108">Si userà un dispositivo Intel NUC che esegue Wind River Linux e il [SensorTag di TI](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main) e</span><span class="sxs-lookup"><span data-stu-id="2c2c5-108">You will be working with Intel NUC that's running Wind River Linux and the [TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span></span> <span data-ttu-id="2c2c5-109">si apprenderà come connettere con facilità i dispositivi al cloud usando l'hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="2c2c5-109">You will learn how to seamleesly connect your devices to the cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="2c2c5-110">**Non si dispone ancora di un kit?** Fare clic [qui](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="2c2c5-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="2c2c5-111">**Non si dispone di un SensorTag?** [Iniziare con un dispositivo simulato](iot-hub-gateway-kit-c-sim-get-started.md) o [acquistare un SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span><span class="sxs-lookup"><span data-stu-id="2c2c5-111">**Don't have a SensorTag?:** [Start with a simulated device](iot-hub-gateway-kit-c-sim-get-started.md) or [buy a SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="2c2c5-112">Lezione 1. Configurare il dispositivo NUC</span><span class="sxs-lookup"><span data-stu-id="2c2c5-112">Lesson 1: Configure your NUC</span></span>
![Diagramma di flusso della lezione 1](media/iot-hub-gateway-kit-lessons/e2e-lesson1.png)

<span data-ttu-id="2c2c5-114">Questa lezione illustra come configurare il dispositivo Intel NUC (Next Unit of Computing) nel kit come un gateway IoT di Azure, installare il pacchetto di Azure IoT Edge sul dispositivo NUC ed eseguire un'app di esempio per verificare la funzionalità del gateway.</span><span class="sxs-lookup"><span data-stu-id="2c2c5-114">In this lesson, you set up Intel NUC (Next Unit of Computing) in the Kit as an Azure IoT gateway, install the Azure IoT Edge package on NUC, and run a sample app to verify the gateway functionality.</span></span>

<span data-ttu-id="2c2c5-115">*Tempo previsto per il completamento: 15 minuti*</span><span class="sxs-lookup"><span data-stu-id="2c2c5-115">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="2c2c5-116">Passare a [Configurare il dispositivo Intel NUC come un gateway IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span><span class="sxs-lookup"><span data-stu-id="2c2c5-116">Go to [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="2c2c5-117">Lezione 2. Creare l'hub IoT</span><span class="sxs-lookup"><span data-stu-id="2c2c5-117">Lesson 2: Create your IoT Hub</span></span>
![Diagramma di flusso della lezione 2](media/iot-hub-gateway-kit-lessons/e2e-lesson2.png)

<span data-ttu-id="2c2c5-119">Questa lezione illustra come installare gli strumenti e il software nel computer host.</span><span class="sxs-lookup"><span data-stu-id="2c2c5-119">In this lesson, you install the tools and software on your host computer.</span></span> <span data-ttu-id="2c2c5-120">Verrà quindi indicato come creare l'account Azure gratuito, effettuare il provisioning dell'hub IoT di Azure e creare il primo dispositivo nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2c2c5-120">Then you create your free Azure account, provision your Azure IoT hub and create your first device in the IoT hub.</span></span>

<span data-ttu-id="2c2c5-121">Prima di iniziare questa lezione, completare la lezione 1.</span><span class="sxs-lookup"><span data-stu-id="2c2c5-121">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-the-tools"></a><span data-ttu-id="2c2c5-122">Get the tools</span><span class="sxs-lookup"><span data-stu-id="2c2c5-122">Get the tools</span></span>
<span data-ttu-id="2c2c5-123">Installare strumenti e software nel computer host.</span><span class="sxs-lookup"><span data-stu-id="2c2c5-123">Install the tools and software on your host computer.</span></span>

<span data-ttu-id="2c2c5-124">*Tempo previsto per il completamento: 20 minuti*</span><span class="sxs-lookup"><span data-stu-id="2c2c5-124">*Estimated time to complete: 20 minutes*</span></span>

<span data-ttu-id="2c2c5-125">Passare a [Ottenere gli strumenti](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span><span class="sxs-lookup"><span data-stu-id="2c2c5-125">Go to [Get the tools](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="2c2c5-126">Creare un hub IoT ed effettuare la registrazione del dispositivo</span><span class="sxs-lookup"><span data-stu-id="2c2c5-126">Create an IoT hub and register your device</span></span>
<span data-ttu-id="2c2c5-127">Creare il gruppo di risorse, effettuare il provisioning del primo hub IoT di Azure e aggiungere il primo dispositivo all'hub IoT usando l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="2c2c5-127">Create your resource group, provision your first Azure IoT hub, and add your first device to the IoT hub using the Azure CLI.</span></span>

<span data-ttu-id="2c2c5-128">*Tempo previsto per il completamento: 10 minuti*</span><span class="sxs-lookup"><span data-stu-id="2c2c5-128">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="2c2c5-129">Passare a [Creare un hub IoT ed effettuare la registrazione del dispositivo](iot-hub-gateway-kit-c-lesson2-register-device.md)</span><span class="sxs-lookup"><span data-stu-id="2c2c5-129">Go to [Create an IoT hub and register your device](iot-hub-gateway-kit-c-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-sensortag-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="2c2c5-130">Lezione 3. Ricevere messaggi da SensorTag e leggere messaggi dall'hub IoT</span><span class="sxs-lookup"><span data-stu-id="2c2c5-130">Lesson 3: Receive messages from SensorTag and read messages from your IoT hub</span></span>
<span data-ttu-id="2c2c5-131">Questa lezione illustra come usare gli script per automatizzare la configurazione e l'esecuzione di un'applicazione di esempio BLE nel gateway.</span><span class="sxs-lookup"><span data-stu-id="2c2c5-131">In this lesson, you will use scripts to automate the configuration and execution of a BLE sample application in your gateway.</span></span> <span data-ttu-id="2c2c5-132">Tali applicazioni utilizzano una raccolta di moduli per aggregare e trasformare dati, elaborare comandi o eseguire un numero qualsiasi di attività correlate.</span><span class="sxs-lookup"><span data-stu-id="2c2c5-132">Such applications use a collection of modules to aggregate and transform data, process commands, or perform any number of related tasks.</span></span> <span data-ttu-id="2c2c5-133">I moduli comunicano tra loro tramite un broker messaggi.</span><span class="sxs-lookup"><span data-stu-id="2c2c5-133">Modules communicate with one another via a message broker.</span></span> <span data-ttu-id="2c2c5-134">L'applicazione di esempio è costituita da un modulo BLE e un modulo dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2c2c5-134">The sample application has a BLE module and an IoT hub module.</span></span> <span data-ttu-id="2c2c5-135">Il modulo BLE riceve i dati dal dispositivo SensorTag BLE.</span><span class="sxs-lookup"><span data-stu-id="2c2c5-135">The BLE module receives data from BLE SensorTag.</span></span> <span data-ttu-id="2c2c5-136">Il modulo dell'hub IoT inserisce in pacchetti i dati ricevuti e li invia all'hub IoT tramite il framework del gateway fornito in Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="2c2c5-136">The IoT hub module packages the data received and sends it to your IoT hub through the gateway framework provided in Azure IoT Edge.</span></span>

![Diagramma di flusso della lezione 3](media/iot-hub-gateway-kit-lessons/e2e-lesson3.png)

### <a name="configure-and-run-the-ble-sample-app"></a><span data-ttu-id="2c2c5-138">Configurare eseguire l'app di esempio BLE</span><span class="sxs-lookup"><span data-stu-id="2c2c5-138">Configure and run the BLE sample app</span></span>
<span data-ttu-id="2c2c5-139">Configurare la connettività tra SensorTag e il gateway.</span><span class="sxs-lookup"><span data-stu-id="2c2c5-139">Set up the connectivity between SensorTag and your gateway.</span></span> <span data-ttu-id="2c2c5-140">Completare quindi la configurazione ed eseguire l'applicazione di esempio BLE.</span><span class="sxs-lookup"><span data-stu-id="2c2c5-140">Then finish the configuration and run the BLE sample application.</span></span>

<span data-ttu-id="2c2c5-141">*Tempo previsto per il completamento: 15 minuti*</span><span class="sxs-lookup"><span data-stu-id="2c2c5-141">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="2c2c5-142">Passare a [Configurare ed eseguire un'app di esempio BLE](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span><span class="sxs-lookup"><span data-stu-id="2c2c5-142">Go to [Configure and run the BLE sample app](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="2c2c5-143">Leggere i messaggi dall'hub IoT</span><span class="sxs-lookup"><span data-stu-id="2c2c5-143">Read messages from your IoT hub</span></span>
<span data-ttu-id="2c2c5-144">Eseguire il codice di esempio sul computer host per leggere i messaggi dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2c2c5-144">Run sample code on your host computer to read messages from your IoT hub.</span></span>

<span data-ttu-id="2c2c5-145">*Tempo previsto per il completamento: 15 minuti*</span><span class="sxs-lookup"><span data-stu-id="2c2c5-145">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="2c2c5-146">Passare a [Leggere i messaggi dall'hub IoT](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="2c2c5-146">Go to [Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-to-azure-table-storage"></a><span data-ttu-id="2c2c5-147">Lezione 4. Salvare i messaggi nell'archiviazione tabelle di Azure</span><span class="sxs-lookup"><span data-stu-id="2c2c5-147">Lesson 4: Save messages to Azure Table storage</span></span>
<span data-ttu-id="2c2c5-148">Creare un'app per le funzioni di Azure in grado di recuperare i messaggi in arrivo dall'hub IoT e scriverli nell'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="2c2c5-148">Create an Azure function app that gets incoming messages from your IoT hub and writes them to Azure Table storage.</span></span>

![Diagramma di flusso della lezione 4](media/iot-hub-gateway-kit-lessons/e2e-lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="2c2c5-150">Creare un'app per le funzioni di Azure e un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="2c2c5-150">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="2c2c5-151">Usare un modello di Azure Resource Manager per creare un'app per le funzioni di Azure e un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2c2c5-151">Use an Azure Resource Manager template to create an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="2c2c5-152">*Tempo previsto per il completamento: 10 minuti*</span><span class="sxs-lookup"><span data-stu-id="2c2c5-152">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="2c2c5-153">Passare a [Creare un'app per le funzioni di Azure e un account di archiviazione di Azure](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="2c2c5-153">Go to [Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="2c2c5-154">Leggere i messaggi persistenti nell'archiviazione tabelle di Azure</span><span class="sxs-lookup"><span data-stu-id="2c2c5-154">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="2c2c5-155">Monitorare i messaggi da gateway a cloud mentre vengono scritti nell'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="2c2c5-155">Monitor the gateway-to-cloud messages as they are written to Azure Table storage.</span></span>

<span data-ttu-id="2c2c5-156">*Tempo previsto per il completamento: 5 minuti*</span><span class="sxs-lookup"><span data-stu-id="2c2c5-156">*Estimated time to complete: 5 minutes*</span></span>

<span data-ttu-id="2c2c5-157">Passare a [Leggere i messaggi persistenti nell'archiviazione tabelle di Azure](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="2c2c5-157">Go to [Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="2c2c5-158">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="2c2c5-158">Troubleshooting</span></span>
<span data-ttu-id="2c2c5-159">In caso di problemi durante le lezioni, è possibile cercare soluzioni nell'articolo [Risoluzione dei problemi](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="2c2c5-159">If you have any problems during the lessons, look for solutions in the [Troubleshooting](iot-hub-gateway-kit-c-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="2c2c5-160">Scopri di più</span><span class="sxs-lookup"><span data-stu-id="2c2c5-160">Explore more</span></span>
<span data-ttu-id="2c2c5-161">Per ulteriori informazioni, visitare la pagina relativa a [Intel IoT Gateway Kit in Developer Zone](http://software.intel.com/iot/microsoft-azure).</span><span class="sxs-lookup"><span data-stu-id="2c2c5-161">Visit the [Intel IoT Gateway Kit developer zone](http://software.intel.com/iot/microsoft-azure) to learn more.</span></span>