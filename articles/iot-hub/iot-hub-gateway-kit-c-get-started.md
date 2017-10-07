---
title: 'Dispositivo SensorTag e gateway Azure IoT: introduzione | Documentazione Microsoft'
description: Introduzione a IoT Gateway Starter Kit, creare l'hub IoT di Azure e connettersi SensorTag Gateway toohello IoT hub
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure iot hub iot gateway, Guida introduttiva a hello internet delle cose, iot toolkit
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
ms.openlocfilehash: d8e4057e7774e43c069dd3f2f2e03f098c1ac844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-sensortag"></a><span data-ttu-id="b8924-104">Introduzione allo starter kit del gateway IoT di Azure con un dispositivo SensorTag</span><span class="sxs-lookup"><span data-stu-id="b8924-104">Get started with IoT Gateway Starter Kit with a SensorTag</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b8924-105">SensorTag</span><span class="sxs-lookup"><span data-stu-id="b8924-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="b8924-106">Dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="b8924-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="b8924-107">In questa esercitazione, è necessario innanzitutto apprendimento hello nozioni fondamentali sulle operazioni con [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="b8924-107">In this tutorial, you begin by learning hello basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="b8924-108">Si utilizzeranno con NUC Intel che esegue Linux distretto vento e hello [SensorTag TI](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span><span class="sxs-lookup"><span data-stu-id="b8924-108">You will be working with Intel NUC that's running Wind River Linux and hello [TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span></span> <span data-ttu-id="b8924-109">Si apprenderà come tooseamleesly connettersi cloud toohello di dispositivi con Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b8924-109">You will learn how tooseamleesly connect your devices toohello cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="b8924-110">**Non si dispone ancora di un kit?** Fare clic [qui](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="b8924-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="b8924-111">**Non si dispone di un SensorTag?** [Iniziare con un dispositivo simulato](iot-hub-gateway-kit-c-sim-get-started.md) o [acquistare un SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span><span class="sxs-lookup"><span data-stu-id="b8924-111">**Don't have a SensorTag?:** [Start with a simulated device](iot-hub-gateway-kit-c-sim-get-started.md) or [buy a SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="b8924-112">Lezione 1. Configurare il dispositivo NUC</span><span class="sxs-lookup"><span data-stu-id="b8924-112">Lesson 1: Configure your NUC</span></span>
![Diagramma di flusso della lezione 1](media/iot-hub-gateway-kit-lessons/e2e-lesson1.png)

<span data-ttu-id="b8924-114">In questa lezione, è possibile impostare NUC Intel (successivo unità di elaborazione) in hello Kit come gateway IoT di Azure, installare il pacchetto di Azure IoT Edge hello in NUC ed eseguire una funzionalità di gateway hello tooverify app di esempio.</span><span class="sxs-lookup"><span data-stu-id="b8924-114">In this lesson, you set up Intel NUC (Next Unit of Computing) in hello Kit as an Azure IoT gateway, install hello Azure IoT Edge package on NUC, and run a sample app tooverify hello gateway functionality.</span></span>

<span data-ttu-id="b8924-115">*Toocomplete tempo stimato: 15 minuti*</span><span class="sxs-lookup"><span data-stu-id="b8924-115">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="b8924-116">Andare troppo[impostare NUC Intel come gateway IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span><span class="sxs-lookup"><span data-stu-id="b8924-116">Go too[Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="b8924-117">Lezione 2. Creare l'hub IoT</span><span class="sxs-lookup"><span data-stu-id="b8924-117">Lesson 2: Create your IoT Hub</span></span>
![Diagramma di flusso della lezione 2](media/iot-hub-gateway-kit-lessons/e2e-lesson2.png)

<span data-ttu-id="b8924-119">In questa lezione, si installa strumenti hello e software nel computer host.</span><span class="sxs-lookup"><span data-stu-id="b8924-119">In this lesson, you install hello tools and software on your host computer.</span></span> <span data-ttu-id="b8924-120">Quindi creare l'account gratuito di Azure, eseguire il provisioning dell'hub IoT di Azure e creare il primo dispositivo nell'hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="b8924-120">Then you create your free Azure account, provision your Azure IoT hub and create your first device in hello IoT hub.</span></span>

<span data-ttu-id="b8924-121">Prima di iniziare questa lezione, completare la lezione 1.</span><span class="sxs-lookup"><span data-stu-id="b8924-121">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-hello-tools"></a><span data-ttu-id="b8924-122">Ottenere strumenti hello</span><span class="sxs-lookup"><span data-stu-id="b8924-122">Get hello tools</span></span>
<span data-ttu-id="b8924-123">Installare strumenti di hello e software nel computer host.</span><span class="sxs-lookup"><span data-stu-id="b8924-123">Install hello tools and software on your host computer.</span></span>

<span data-ttu-id="b8924-124">*Toocomplete tempo stimato: 20 minuti*</span><span class="sxs-lookup"><span data-stu-id="b8924-124">*Estimated time toocomplete: 20 minutes*</span></span>

<span data-ttu-id="b8924-125">Andare troppo[strumenti hello](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span><span class="sxs-lookup"><span data-stu-id="b8924-125">Go too[Get hello tools](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="b8924-126">Creare un hub IoT ed effettuare la registrazione del dispositivo</span><span class="sxs-lookup"><span data-stu-id="b8924-126">Create an IoT hub and register your device</span></span>
<span data-ttu-id="b8924-127">Creare il gruppo di risorse, l'hub IoT Azure prima di eseguire il provisioning e aggiungere primo dispositivo toohello IoT hub utilizzando hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="b8924-127">Create your resource group, provision your first Azure IoT hub, and add your first device toohello IoT hub using hello Azure CLI.</span></span>

<span data-ttu-id="b8924-128">*Toocomplete tempo stimato: 10 minuti*</span><span class="sxs-lookup"><span data-stu-id="b8924-128">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="b8924-129">Andare troppo[creare un hub IoT e registrare il dispositivo](iot-hub-gateway-kit-c-lesson2-register-device.md)</span><span class="sxs-lookup"><span data-stu-id="b8924-129">Go too[Create an IoT hub and register your device](iot-hub-gateway-kit-c-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-sensortag-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="b8924-130">Lezione 3. Ricevere messaggi da SensorTag e leggere messaggi dall'hub IoT</span><span class="sxs-lookup"><span data-stu-id="b8924-130">Lesson 3: Receive messages from SensorTag and read messages from your IoT hub</span></span>
<span data-ttu-id="b8924-131">In questa lezione si utilizzerà script tooautomate hello configurazione ed esecuzione di un'applicazione di esempio BILITA nel gateway.</span><span class="sxs-lookup"><span data-stu-id="b8924-131">In this lesson, you will use scripts tooautomate hello configuration and execution of a BLE sample application in your gateway.</span></span> <span data-ttu-id="b8924-132">Tali applicazioni utilizzano un insieme di moduli tooaggregate e trasformare i dati, elaborare i comandi o eseguono un numero qualsiasi di attività correlate.</span><span class="sxs-lookup"><span data-stu-id="b8924-132">Such applications use a collection of modules tooaggregate and transform data, process commands, or perform any number of related tasks.</span></span> <span data-ttu-id="b8924-133">I moduli comunicano tra loro tramite un broker messaggi.</span><span class="sxs-lookup"><span data-stu-id="b8924-133">Modules communicate with one another via a message broker.</span></span> <span data-ttu-id="b8924-134">applicazione di esempio Hello dispone di un modulo di tabella e un modulo di hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b8924-134">hello sample application has a BLE module and an IoT hub module.</span></span> <span data-ttu-id="b8924-135">modulo BILITA Hello riceve dati da SensorTag attiva.</span><span class="sxs-lookup"><span data-stu-id="b8924-135">hello BLE module receives data from BLE SensorTag.</span></span> <span data-ttu-id="b8924-136">Hello pacchetti ricevuti dati hello e lo invia hub IoT tooyour tramite il framework di gateway hello fornito in Azure IoT Edge di IoT hub modulo.</span><span class="sxs-lookup"><span data-stu-id="b8924-136">hello IoT hub module packages hello data received and sends it tooyour IoT hub through hello gateway framework provided in Azure IoT Edge.</span></span>

![Diagramma di flusso della lezione 3](media/iot-hub-gateway-kit-lessons/e2e-lesson3.png)

### <a name="configure-and-run-hello-ble-sample-app"></a><span data-ttu-id="b8924-138">Configurare ed eseguire app di esempio BILITA hello</span><span class="sxs-lookup"><span data-stu-id="b8924-138">Configure and run hello BLE sample app</span></span>
<span data-ttu-id="b8924-139">Configurare la connettività di hello tra SensorTag e il gateway.</span><span class="sxs-lookup"><span data-stu-id="b8924-139">Set up hello connectivity between SensorTag and your gateway.</span></span> <span data-ttu-id="b8924-140">Quindi completare la configurazione di hello ed eseguire l'applicazione di esempio BILITA hello.</span><span class="sxs-lookup"><span data-stu-id="b8924-140">Then finish hello configuration and run hello BLE sample application.</span></span>

<span data-ttu-id="b8924-141">*Toocomplete tempo stimato: 15 minuti*</span><span class="sxs-lookup"><span data-stu-id="b8924-141">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="b8924-142">Andare troppo[configurare ed eseguire hello Disattiva app di esempio](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span><span class="sxs-lookup"><span data-stu-id="b8924-142">Go too[Configure and run hello BLE sample app](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="b8924-143">Leggere messaggi dall'hub IoT</span><span class="sxs-lookup"><span data-stu-id="b8924-143">Read messages from your IoT hub</span></span>
<span data-ttu-id="b8924-144">Eseguire il codice di esempio nell'host computer tooread messaggi dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b8924-144">Run sample code on your host computer tooread messages from your IoT hub.</span></span>

<span data-ttu-id="b8924-145">*Toocomplete tempo stimato: 15 minuti*</span><span class="sxs-lookup"><span data-stu-id="b8924-145">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="b8924-146">Andare troppo[leggere messaggi dall'hub IoT](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="b8924-146">Go too[Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-tooazure-table-storage"></a><span data-ttu-id="b8924-147">Lezione 4: Salvare i messaggi di archiviazione tabelle tooAzure</span><span class="sxs-lookup"><span data-stu-id="b8924-147">Lesson 4: Save messages tooAzure Table storage</span></span>
<span data-ttu-id="b8924-148">Creare un'app di Azure di funzione che ottiene i messaggi in arrivo dall'hub IoT e li scrive archiviazione tabella tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b8924-148">Create an Azure function app that gets incoming messages from your IoT hub and writes them tooAzure Table storage.</span></span>

![Diagramma di flusso della lezione 4](media/iot-hub-gateway-kit-lessons/e2e-lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="b8924-150">Creare un'app per le funzioni di Azure e un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="b8924-150">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="b8924-151">Un'app di Azure (funzione) e un account di archiviazione di Azure, utilizzare un toocreate modello di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="b8924-151">Use an Azure Resource Manager template toocreate an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="b8924-152">*Toocomplete tempo stimato: 10 minuti*</span><span class="sxs-lookup"><span data-stu-id="b8924-152">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="b8924-153">Andare troppo[creare un account di archiviazione di Azure e l'app di Azure (funzione)](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="b8924-153">Go too[Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="b8924-154">Leggere i messaggi persistenti nell'archiviazione tabelle di Azure</span><span class="sxs-lookup"><span data-stu-id="b8924-154">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="b8924-155">Monitorare i messaggi hello gateway-to-cloud quando vengono scritti nel servizio di archiviazione tabelle tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b8924-155">Monitor hello gateway-to-cloud messages as they are written tooAzure Table storage.</span></span>

<span data-ttu-id="b8924-156">*Toocomplete tempo stimato: 5 minuti*</span><span class="sxs-lookup"><span data-stu-id="b8924-156">*Estimated time toocomplete: 5 minutes*</span></span>

<span data-ttu-id="b8924-157">Andare troppo[leggere messaggi persistenti nell'archiviazione tabelle Azure](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="b8924-157">Go too[Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="b8924-158">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="b8924-158">Troubleshooting</span></span>
<span data-ttu-id="b8924-159">Se si verificano problemi durante lezioni hello, cercare soluzioni in hello [Troubleshooting](iot-hub-gateway-kit-c-troubleshooting.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="b8924-159">If you have any problems during hello lessons, look for solutions in hello [Troubleshooting](iot-hub-gateway-kit-c-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="b8924-160">Scopri di più</span><span class="sxs-lookup"><span data-stu-id="b8924-160">Explore more</span></span>
<span data-ttu-id="b8924-161">Visitare hello [zona di Intel IoT Gateway Kit per sviluppatori](http://software.intel.com/iot/microsoft-azure) toolearn altre.</span><span class="sxs-lookup"><span data-stu-id="b8924-161">Visit hello [Intel IoT Gateway Kit developer zone](http://software.intel.com/iot/microsoft-azure) toolearn more.</span></span>
